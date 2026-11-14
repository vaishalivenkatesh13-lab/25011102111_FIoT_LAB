# EXPERIMENT DETAILS
- **Student Name:** Vaishali V
- **Register Number:** 25011102111
- **Degree / Branch:** B.Tech. Computer Science and Engineering (IoT)
- **Year / Semester:** II Year / III Semester
- **Course Title:** Fundamentals of Internet of Things Laboratory (25CS2741)
- **Academic Year:** 2026–2027

---

# CAT 15: INTEGRATED MULTI-TOPIC IOT EDGE NODE (COURSE CAPSTONE)

## 1. Circuit Diagram & Hardware Description

![Circuit Diagram](circuit.png)

### Hardware Description
This final capstone project consolidates all embedded systems concepts acquired across the course into a complete, bidirectional IoT edge node on the STM32F401RE (NUCLEO-F401RE).
- **Sensory Subsystem:** Bosch Sensortec BME280 digital environmental sensor connected over I2C1 (PB8 SCL, PB9 SDA) with 4.7 kΩ pull-ups.
- **Communications Gateway:** ESP8266 Wi-Fi modem operating over USART1 (PA9 TX, PA10 RX) at 115200 baud, connected to public MQTT broker `broker.emqx.io:1883`.
- **Local Actuator & User Interface:** LD2 User LED on PA5, User Button B1 on PC13, and serial diagnostics on USART2 (PA2 TX).
- **Functional Architecture:**
  - *Periodic Telemetry Publication:* Dispatches environmental JSON frames to `vaishali/stm32/bme280` every 2000 ms.
  - *Cloud Actuation Subscription:* Subscribes to `vaishali/stm32/led` to execute real-time commands (`ON`, `OFF`, `TOGGLE`).
  - *Edge Threshold Alerts:* Monitors temperature; if it exceeds 30.0 °C, an immediate priority alert message is dispatched to `vaishali/stm32/alerts`.

---

## 2. Core Logic / Pseudocode / Code Base

### Working Principle
The architecture utilizes a cooperative non-blocking scheduling loop:
1. Every 2 seconds, sensor data is polled and published via MQTT.
2. The incoming MQTT buffer is checked every loop iteration for actuation commands.
3. If temperature crosses predefined threshold limits, an emergency alert is triggered.
4. Auto-reconnection logic recovers from network drops without blocking the main CPU loop.

### Step-by-Step Pseudocode
```text
BEGIN PROGRAM
    INITIALIZE BME280, USART1, USART2, ESP8266
    CONNECT to WiFi AND MQTT Broker ("broker.emqx.io")
    SUBSCRIBE to "vaishali/stm32/led"

    GLOBAL last_pub_time = 0

    MAIN:
        WHILE TRUE DO:
            now = HAL_GetTick()

            // 1. Check for incoming cloud actuation messages
            IF ESPLib_MQTT_CheckIncoming(&topic, &msg) THEN:
                IF strcmp(msg, "ON") == 0 THEN:
                    HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET)
                ELSE IF strcmp(msg, "OFF") == 0 THEN:
                    HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET)
                ELSE IF strcmp(msg, "TOGGLE") == 0 THEN:
                    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5)
                END IF
            END IF

            // 2. Periodic Telemetry Broadcast
            IF (now - last_pub_time) >= 2000 THEN:
                bme280_read(&t, &h, &p)
                
                // Alert evaluation
                IF t > 30.0 THEN:
                    ESPLib_MQTT_Publish("vaishali/stm32/alerts", "{\"alert\":\"HIGH_TEMPERATURE\"}")
                END IF

                json = sprintf("{\"temp\":%.2f,\"humidity\":%.2f,\"pressure\":%.2f}", t, h, p)
                ESPLib_MQTT_Publish("vaishali/stm32/bme280", json)
                last_pub_time = now
            END IF
        END WHILE
END PROGRAM
```

---

## 3. Expected Output & Inference

### Expected Output
- Continuous environmental telemetry published to `vaishali/stm32/bme280`.
- Immediate actuator response when publishing `ON`/`OFF` to `vaishali/stm32/led`.
- Real-time alert notifications when applying external heat to the BME280 sensor.

### Inference
This capstone system demonstrates the complete lifecycle of a modern industrial IoT device: robust hardware abstraction, real-time sensor processing, non-blocking state machine execution, and secure bi-directional cloud connectivity.
