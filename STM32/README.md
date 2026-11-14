# EXPERIMENT DETAILS
- **Student Name:** Vaishali V
- **Register Number:** 25011102111
- **Degree / Branch:** B.Tech. Computer Science and Engineering (IoT)
- **Year / Semester:** II Year / III Semester
- **Course Title:** Fundamentals of Internet of Things Laboratory (25CS2741)
- **Academic Year:** 2026–2027

---

# STM32 EMBEDDED SYSTEMS & IOT PLATFORM
### 32-Bit ARM Cortex-M Architecture, Hardware Abstraction Layer & Cloud IoT Protocols

This directory contains the complete collection of 18 embedded systems and Internet of Things experiments developed for the **STM32 32-bit ARM Cortex-M** family. Implementations span from low-level register abstractions and non-blocking event-driven programming up to edge sensor drivers, HTTP web servers, and cloud MQTT telemetry pipelines.

---

## 1. Architectural Overview & System Platforms

### A. STM32F103C6T6 (Blue Pill Board) — CAT 8 to CAT 11
- **CPU Core:** 32-bit ARM Cortex-M3 running at 72 MHz.
- **Memory:** 32 KB Flash memory, 10 KB SRAM.
- **Clock Tree:** 8 MHz HSE crystal, Phase-Locked Loop (PLL) multiplication to 72 MHz SYSCLK, 36 MHz APB1, 72 MHz APB2.
- **Peripherals:** Dual USARTs, multi-channel timers, advanced GPIO with software pull-up/pull-down controls.

### B. STM32F401RET6 (NUCLEO-F401RE Board) — CAT 12 to CAT 15
- **CPU Core:** 32-bit ARM Cortex-M4 with single-precision hardware Floating Point Unit (FPU) and DSP instructions running at 84 MHz.
- **Memory:** 512 KB Flash memory, 96 KB SRAM.
- **Clock Tree:** 8 MHz ST-LINK MCO into HSE, PLL multiplication to 84 MHz core clock.
- **Peripherals:** Hardware I2C (Standard & Fast Mode), multiple high-speed USARTs, integrated ST-LINK V2-1 virtual COM port.

---

## 2. Directory Index of STM32 Experiments

```text
STM32/
├── CAT8/
│   ├── TASK8A/       # GPIO Push-Button Follower (PA15 Input -> PC13 Active-LOW LED)
│   ├── TASK8B/       # Non-Blocking Software Debounced Toggle (>50 ms Window)
│   └── TASK8C/       # Short Press (<1s) vs Long Press (≥1s Continuous 100ms Blink)
├── CAT9/
│   ├── TASK9A/       # USART2 Asynchronous Transceiver Echo & 1s 'A' Heartbeat
│   └── TASK9B/       # String-Based ASCII Command Interpreter (LED ON/OFF/STATUS)
├── CAT10/
│   ├── TASK10A/      # Dual-UART Hardware Bridge (USART1 ESP8266 <-> USART2 PC)
│   └── TASK10B/      # ESP8266 AT Command Profiler & 2.4 GHz Access Point Scanner
├── CAT11/
│   ├── TASK10C/      # Wi-Fi Station Association (AT+CWJAP), IP Query & TCP Socket
│   └── TASK10D/      # Embedded HTTP Web Server on Port 80 with Web LED Controls
├── CAT12/
│   ├── TASK12A/      # NUCLEO-F401RE 84 MHz PLL Bring-Up & 1.0 Hz LD2 Blink
│   ├── TASK12B/      # Debounced User Button Toggle with Persistent State Memory
│   └── TASK12C/      # Three-Tier Press Classifier (Short/Long/Very-Long Reset)
├── CAT13/
│   ├── TASK13A/      # Bosch BME280 I2C Sensor Driver & 64-Bit Compensation Math
│   └── TASK13B/      # Environmental REST API Server Serving JSON Telemetry
├── CAT14/
│   ├── TASK14A/      # Cloud MQTT Telemetry Publisher via Course ESPLib
│   ├── TASK14B/      # Cloud MQTT Remote Actuation Subscriber (Topic Actuation)
│   └── TASK14C/      # BME280 MQTT Telemetry Streaming to Node-RED Dashboard
└── CAT15/            # IoT-Based Smart Irrigation & Agricultural Monitoring System
```

---

## 3. IoT Communication & Protocol Stack

1. **Hardware I2C Environmental Sensing:** Communicates with the Bosch Sensortec BME280 over I2C1 (PB8 SCL, PB9 SDA) at 100 kHz. Reads factory calibration coefficients from non-volatile memory and applies 64-bit integer compensation polynomials to extract calibrated temperature (°C), relative humidity (%RH), and pressure (hPa).
2. **Hayes AT Command Wi-Fi Management:** Transmits structured ASCII commands (`AT+CWJAP`, `AT+CIFSR`, `AT+CIPSERVER`) over USART1 at 115200 baud to manage network association and TCP/IP socket connections.
3. **HTTP 1.1 Web Server:** Implements standalone HTTP services on TCP Port 80, parsing incoming `+IPD` frames and generating dynamic HTML pages with control endpoints.
4. **MQTT 3.1.1 Cloud Telemetry:** Uses the course `ESPLib` driver to establish binary MQTT connections to `broker.emqx.io:1883`, publishing periodic JSON payloads to telemetry topics and subscribing to control topics for remote actuator switching.

---

## 4. Compilation & Debugging Instructions

1. Open project via `MDK-ARM/*.uvprojx` in Keil MDK-ARM, or import into STM32CubeIDE.
2. Select debugger: **ST-Link Debugger** in SWD mode.
3. Build the target project (**F7**).
4. Download and flash firmware (**F8**).
5. Open serial terminal (PuTTY) on target COM port at **115200 Baud, 8-N-1** to observe live system telemetry.
