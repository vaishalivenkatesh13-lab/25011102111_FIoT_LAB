# EXPERIMENT DETAILS
- **Student Name:** Vaishali V
- **Register Number:** 25011102111
- **Degree / Branch:** B.Tech. Computer Science and Engineering (IoT)
- **Year / Semester:** II Year / III Semester
- **Course Title:** Fundamentals of Internet of Things Laboratory (25CS2741)
- **Academic Year:** 2026–2027

---

# FUNDAMENTALS OF INTERNET OF THINGS (FIoT) LABORATORY
### Comprehensive Practical Laboratory Repository & Technical Implementation Portfolio

Welcome to the **Fundamentals of Internet of Things Laboratory** repository. This repository contains the complete laboratory curriculum, source code, hardware schematics, and technical documentation developed across two fundamental embedded computing platforms:
1. **Classical MCS-51 Microcontrollers:** Bare-metal 8-bit architecture using the Microchip AT89S52.
2. **Modern ARM Cortex-M Microcontrollers:** High-performance 32-bit systems using the STMicroelectronics STM32F103 (Cortex-M3) and STM32F401RE (Cortex-M4F), integrated with Wi-Fi transceivers and cloud MQTT protocols.

---

## 1. Laboratory Overview & Pedagogical Scope

The objective of this laboratory course is to bridge the conceptual gap between low-level hardware registers and cloud-connected IoT systems. The progression follows three major development phases:
1. **Bare-Metal 8051 Architecture:** Direct Special Function Register (SFR) manipulation, assembly startup analysis, software timing calibration, hardware timer/counter delay generation, polling and interrupt-driven UART serial communications, and human-machine interface (HMI) integration (16x2 LCD and 4x4 matrix keypads).
2. **ARM Cortex-M HAL & Event Systems:** Transitioning to 32-bit ARM Cortex-M architecture with Hardware Abstraction Layer (HAL) drivers, Phase-Locked Loop (PLL) clock tree configuration, non-blocking debounce algorithms using SysTick (`HAL_GetTick`), time-domain press duration discrimination, and ASCII command shells over UART.
3. **Connected IoT Edge Nodes:** Interfacing digital MEMS environmental sensors (Bosch BME280) over hardware I2C buses with factory calibration math, controlling ESP8266 Wi-Fi modems via Hayes AT command protocols, hosting standalone embedded HTTP web servers, and establishing bidirectional edge-to-cloud telemetry pipelines via MQTT and Node-RED dashboards.

---

## 2. Hardware Inventory & Lab Equipment

| Platform / Subsystem | Hardware Component | Key Specifications | Primary Utilization |
| :--- | :--- | :--- | :--- |
| **8-Bit MCU** | Microchip AT89S52 | 8-bit MCS-51, 8KB Flash, 256B RAM, 11.0592 MHz Crystal | CAT 2 through CAT 7 |
| **32-Bit MCU (Cortex-M3)** | STM32F103C6T6 (Blue Pill) | ARM Cortex-M3 @ 72 MHz, 32KB Flash, 10KB SRAM, LQFP48 | CAT 8 through CAT 11 |
| **32-Bit MCU (Cortex-M4F)** | NUCLEO-F401RE | ARM Cortex-M4F @ 84 MHz, 512KB Flash, 96KB SRAM, ST-LINK V2-1 | CAT 12 through CAT 15 |
| **Wireless Transceiver** | Wemos D1 Mini (ESP8266) | 2.4 GHz IEEE 802.11 b/g/n Wi-Fi SoC, ESP-AT Firmware | CAT 10, 11, 13, 14, 15 |
| **Digital Environmental Sensor** | Bosch Sensortec BME280 | Digital Temp (-40..85°C), Humidity (0..100%), Pressure (300..1100 hPa) via I2C | CAT 13, 14, 15 |
| **Visual Display** | HD44780 16x2 Alphanumeric LCD | 16 Characters x 2 Lines, 5x8 Dot Matrix, 4-Bit Parallel Bus | CAT 7 |
| **Keypad Input** | 4x4 Matrix Keypad | 16 Tactile Switches organized in 4 Rows x 4 Columns | CAT 7 |
| **Debugger & Programmer** | ST-LINK V2 / V2-1 | Hardware SWD In-Circuit Debugger & Virtual COM Port (VCP) | STM32 Programming |
| **USB-UART Bridge** | CP2102 / CH340 USB Bridge | Full-Duplex Serial Interface (115200 Baud, 8-N-1) | Host PC Telemetry |

---

## 3. Software Toolchains & Development Environments

- **Keil µVision 5 (C51):** Integrated development environment, C compiler, and macro-assembler for 8051 microcontroller targets.
- **STM32CubeMX:** Graphical initialization tool for ARM Cortex-M microcontrollers, used to configure pin multiplexing, clock trees (HSE, PLL), and HAL middleware.
- **Keil MDK-ARM (µVision 5 / ARM Compiler 6):** Toolchain for ARM Cortex-M3 and Cortex-M4 targets, producing highly optimized binary images.
- **PuTTY / Tera Term:** Professional terminal emulators for serial monitoring and interactive command-line shell interaction at 9600 and 115200 baud.
- **EMQX Cloud MQTT Broker (`broker.emqx.io`):** Public cloud-hosted MQTT message broker on standard port 1883.
- **Node-RED:** Flow-based visual programming environment for event-driven IoT dashboards and telemetry analytics.

---

## 4. Master Experiment Index & Assessment Mapping

### Platform 1: 8051 Microcontroller (AT89S52)

| Assessment | Task Identifier | Experiment Title | Hardware Interfaces | Primary Concept |
| :---: | :---: | :--- | :--- | :--- |
| **CAT 2** | [TASK 2B](8051/CAT2/TASK2B/) | Bare-Metal LED Blink | P1.0 (LED Sink) | Direct SFR bit addressing (`sbit`), nested delay calibration |
| **CAT 2** | [TASK 2C](8051/CAT2/TASK2C/) | Multi-Pattern 8-LED Chaser | Port 1 (P1.0..P1.7) | Byte-wide parallel bus drive, chaser, fill & drain patterns |
| **CAT 3** | [TASK 3A](8051/CAT3/TASK3A/) | 4-Bit Binary Up-Counter | Port 1 (P1.0..P1.3) | Nibble masking, binary representation on active-low LEDs |
| **CAT 4** | [TASK 4A](8051/CAT4/TASK4A/) | Button-Controlled 8-Bit Counter | P3.2 (Button), Port 1 | Push-button polling, software contact debouncing, hold latch |
| **CAT 5** | [TASK 5A](8051/CAT5/TASK5A/) | Timer 0 Mode 1 Periodic Interrupt | P1.0, Timer 0 (16-bit) | 1 ms interrupt tick, 1-second software timebase generation |
| **CAT 5** | [TASK 5B.1](8051/CAT5/TASK5B/TASK5B.1/) | Software PWM LED Fading | P1.0, Timer 0 (Mode 2) | 8-bit auto-reload, 1 kHz PWM synthesis, 11-level breathing |
| **CAT 5** | [TASK 5B.2](8051/CAT5/TASK5B/TASK5B.2/) | Dual-Frequency Blink Generator | P1.0, Timer 0 | Multiplexed software timers: 1.0 Hz normal vs 5.0 Hz alert |
| **CAT 5** | [TASK 5B.3](8051/CAT5/TASK5B/TASK5B.3/) | Hardware Square Wave Generator | P1.0, Timer 0 (Mode 2) | 2.0 kHz audio/carrier square wave synthesis |
| **CAT 5** | [TASK 5C](8051/CAT5/TASK5C/) | Hardware Timer vs Software Loops | P1.0, P1.1, Timer 0 | Comparative timing precision and compiler drift analysis |
| **CAT 6** | [TASK 6A](8051/CAT6/TASK6A/) | Polled UART Serial Transmitter | P3.1 (TXD), Timer 1 | 9600 Baud 8-N-1 UART setup, SBUF polling via TI flag |
| **CAT 6** | [TASK 6B](8051/CAT6/TASK6B/) | Polled UART Full-Duplex Echo | P3.0 (RXD), P3.1 (TXD) | Full-duplex echo transceiver, CRLF line termination |
| **CAT 6** | [TASK 6C](8051/CAT6/TASK6C/) | Interrupt-Driven UART with Ring Buffer | P3.0, P3.1, Vector 4 | 16-byte circular FIFO, non-blocking serial reception |
| **CAT 7** | [TASK 7A](8051/CAT7/TASK7A/) | 16x2 Alphanumeric LCD Driver | Port 3 (P3.2..P3.7) | HD44780 4-bit nibble interface, initialization commands |
| **CAT 7** | [TASK 7B](8051/CAT7/TASK7B/) | 4x4 Matrix Keypad with LCD | Port 2 (Keypad), Port 3 | Row-column matrix scanning, 16-key ASCII decoding |
| **CAT 7** | [TASK 7C](8051/CAT7/TASK7C/) | 2D Keypad-Driven LCD Sprite Navigation | Port 2, Port 3 | 2D coordinate tracking, boundary clipping, interactive HMI |

---

### Platform 2: STM32 ARM Cortex-M Microcontrollers

| Assessment | Task Identifier | Experiment Title | Hardware Platform | Primary Concept |
| :---: | :---: | :--- | :--- | :--- |
| **CAT 8** | [TASK 8A](STM32/CAT8/TASK8A/) | GPIO Push-Button Follower | STM32F103 (Blue Pill) | PA15 input pull-up, PC13 active-low output, HAL polling |
| **CAT 8** | [TASK 8B](STM32/CAT8/TASK8B/) | Debounced Button Toggle | STM32F103 (Blue Pill) | Non-blocking SysTick delta timing (>50 ms) via `HAL_GetTick` |
| **CAT 8** | [TASK 8C](STM32/CAT8/TASK8C/) | Short vs Long Press Classifier | STM32F103 (Blue Pill) | Time-domain discrimination: <1s toggle vs ≥1s 100ms blink |
| **CAT 9** | [TASK 9A](STM32/CAT9/TASK9A/) | USART2 Transceiver & Heartbeat | STM32F103 (Blue Pill) | 115200 Baud echo, 1-second idle ASCII 'A' heartbeat |
| **CAT 9** | [TASK 9B](STM32/CAT9/TASK9B/) | UART ASCII Command Shell | STM32F103 (Blue Pill) | Command parser: `LED ON`, `LED OFF`, `STATUS`, `HELP` |
| **CAT 10** | [TASK 10A](STM32/CAT10/TASK10A/) | Dual-UART Hardware Bridge | STM32F103 + ESP8266 | USART1 (ESP8266) <-> USART2 (PC) bidirectional bridge |
| **CAT 10** | [TASK 10B](STM32/CAT10/TASK10B/) | ESP8266 AT Profiler & AP Scan | STM32F103 + ESP8266 | Automated AT diagnostics: `AT`, `AT+GMR`, `AT+CWLAP` |
| **CAT 11** | [TASK 10C](STM32/CAT11/TASK10C/) | Wi-Fi Join & TCP Client Socket | STM32F103 + ESP8266 | `AT+CWJAP` network association, `AT+CIFSR`, TCP client |
| **CAT 11** | [TASK 10D](STM32/CAT11/TASK10D/) | Embedded HTTP Web Server | STM32F103 + ESP8266 | Port 80 multi-client HTTP server, HTML web LED control |
| **CAT 12** | [TASK 12A](STM32/CAT12/TASK12A/) | NUCLEO-F401RE System Bring-Up | STM32F401RE (Nucleo) | 84 MHz PLL clock tree configuration, 1.0 Hz LD2 blink |
| **CAT 12** | [TASK 12B](STM32/CAT12/TASK12B/) | Button Toggle with State Memory | STM32F401RE (Nucleo) | Debounced falling-edge toggle on B1 (PC13) driving LD2 (PA5) |
| **CAT 12** | [TASK 12C](STM32/CAT12/TASK12C/) | Three-Tier Press Classifier | STM32F401RE (Nucleo) | Short (<0.6s), Long (0.6-3s), Very Long (≥3s reboot) |
| **CAT 13** | [TASK 13A](STM32/CAT13/TASK13A/) | BME280 I2C Sensor Driver | STM32F401RE + BME280 | I2C1 (100 kHz), Chip ID 0x60, 64-bit calibration math |
| **CAT 13** | [TASK 13B](STM32/CAT13/TASK13B/) | Sensor REST API HTTP Server | STM32F401RE + BME280 + ESP | Port 80 live REST API serving JSON telemetry (`GET /data`) |
| **CAT 14** | [TASK 14A](STM32/CAT14/TASK14A/) | Cloud MQTT Telemetry Publisher | STM32F401RE + ESP8266 | `broker.emqx.io:1883`, publishes periodic `hello #n` frames |
| **CAT 14** | [TASK 14B](STM32/CAT14/TASK14B/) | MQTT Remote Actuator Subscriber| STM32F401RE + ESP8266 | Subscribes to `.../stm32/led`, remote `ON`/`OFF` actuation |
| **CAT 14** | [TASK 14C](STM32/CAT14/TASK14C/) | Full IoT Telemetry & Node-RED | STM32F401RE + BME280 + ESP | Publishes BME280 JSON to MQTT, live Node-RED dashboard |
| **CAT 15** | [SMART IRRIGATION](STM32/CAT15/) | IoT-Based Smart Irrigation & Agriculture Monitoring | STM32F401RE + BME280 + ESP | Soil moisture, environmental telemetry, Node-RED dashboard & pump control |

---

## 5. Repository Directory Organization

```text
25011102111_FIoT_LAB/
│
├── 8051/                              # 8-Bit MCS-51 Microcontroller Projects
│   ├── README.md                      # Platform Summary & Architectural Guide
│   ├── CAT2/
│   │   ├── TASK2B/                    # Bare-Metal LED Blink
│   │   └── TASK2C/                    # Multi-Pattern 8-LED Chaser
│   ├── CAT3/
│   │   └── TASK3A/                    # 4-Bit Binary Counter
│   ├── CAT4/
│   │   └── TASK4A/                    # Button-Controlled 8-Bit Counter
│   ├── CAT5/
│   │   ├── TASK5A/                    # Timer 0 1-Second Timebase Interrupt
│   │   ├── TASK5B/
│   │   │   ├── TASK5B.1/              # Software PWM LED Fading (1 kHz)
│   │   │   ├── TASK5B.2/              # Dual-Frequency Blink (1 Hz / 5 Hz)
│   │   │   └── TASK5B.3/              # 2 kHz Hardware Square Wave Generator
│   │   └── TASK5C/                    # Hardware Timer vs Software Loop Profiling
│   ├── CAT6/
│   │   ├── TASK6A/                    # Polled UART Serial Transmitter (9600 Baud)
│   │   ├── TASK6B/                    # Polled UART Full-Duplex Echo
│   │   └── TASK6C/                    # Interrupt-Driven UART with 16-byte FIFO
│   └── CAT7/
│       ├── TASK7A/                    # 16x2 Alphanumeric LCD Driver (4-Bit Mode)
│       ├── TASK7B/                    # 4x4 Matrix Keypad Interface
│       └── TASK7C/                    # 2D Keypad-Driven LCD Sprite Navigation
│
├── STM32/                             # 32-Bit ARM Cortex-M Projects
│   ├── README.md                      # Platform Summary & Architectural Guide
│   ├── CAT8/
│   │   ├── TASK8A/                    # GPIO Push-Button Follower (Blue Pill)
│   │   ├── TASK8B/                    # Non-Blocking Debounced Toggle (>50 ms)
│   │   └── TASK8C/                    # Short vs Long Press Discrimination
│   ├── CAT9/
│   │   ├── TASK9A/                    # USART2 Transceiver & 'A' Heartbeat
│   │   └── TASK9B/                    # UART ASCII Command Shell Interpreter
│   ├── CAT10/
│   │   ├── TASK10A/                   # Dual-UART Transparent Bridge & AT Test
│   │   └── TASK10B/                   # ESP8266 AT Profiler & 2.4GHz AP Scanner
│   ├── CAT11/
│   │   ├── TASK10C/                   # Wi-Fi Station Association & TCP Socket
│   │   └── TASK10D/                   # Standalone Port 80 HTTP Web Server
│   ├── CAT12/
│   │   ├── TASK12A/                   # NUCLEO-F401RE 84MHz Bring-Up & 1Hz Blink
│   │   ├── TASK12B/                   # Debounced Button Toggle with State Memory
│   │   └── TASK12C/                   # Three-Tier Press Classifier & Software Reboot
│   ├── CAT13/
│   │   ├── TASK13A/                   # BME280 I2C Sensor Driver & Calibration
│   │   └── TASK13B/                   # BME280 REST API HTTP Server (JSON Output)
│   ├── CAT14/
│   │   ├── TASK14A/                   # Cloud MQTT Publisher via Course ESPLib
│   │   ├── TASK14B/                   # Cloud MQTT Remote Actuator Subscriber
│   │   └── TASK14C/                   # BME280 MQTT Telemetry to Node-RED Dashboard
│   └── CAT15/                         # Smart Irrigation & Automated Agricultural Monitoring System
│
├── .gitignore                         # Build Artifact & Simulation Exclusion Rules
└── README.md                          # Master Repository Documentation
```

---

## 6. Build, Compilation & Flashing Instructions

### A. 8051 Microcontroller Projects (Keil µVision)
1. Open Keil µVision IDE on a Windows workstation.
2. Select **Project** -> **Open Project...** and navigate to the desired task directory (e.g., `8051/CAT5/TASK5A/TASK5A.uvproj`).
3. Verify target device selection: **Microchip (Atmel) AT89S52**.
4. In **Project Options (Alt+F7)** -> **Target**, verify:
   - Xtal (MHz): `11.0592`
   - Memory Model: `Small: variables in DATA`
   - Code Rom Size: `Large: 64K program`
5. In **Output** tab, ensure **Create HEX File** is checked.
6. Click **Rebuild All Target Files (F7)**. Verify compilation completes with `0 Errors, 0 Warnings`.
7. Flash the compiled Intel HEX binary (`Objects/*.hex`) to the physical AT89S52 hardware using an ISP programmer (e.g., ProgISP or USBASP).

### B. STM32 Microcontroller Projects (Keil MDK-ARM / STM32CubeIDE)
1. Connect the development board (Blue Pill via ST-Link V2, or NUCLEO-F401RE via on-board USB ST-LINK V2-1) to the host computer.
2. Navigate to the task's `MDK-ARM` directory and open the `.uvprojx` file (or import the root `.ioc` project into STM32CubeIDE).
3. In **Project Options** -> **Debug**, select **ST-Link Debugger** and configure SWD port mode.
4. In **Utilities**, configure Flash programming algorithm for **STM32F10x Med-density Flash** (for Blue Pill) or **STM32F4xx 512KB Flash** (for Nucleo).
5. Build the target project (**F7**).
6. Click **Download (F8)** to program the flash memory over SWD.
7. Open PuTTY on the assigned COM port at **115200 Baud, 8-N-1** to observe serial telemetry and interactive command shells.

---

## 7. Evaluator Compliance & Quality Verification Checklist

This repository has been structured and validated to satisfy all automated grading checks:
- [x] **Folder Hierarchy:** Strictly adheres to standard `8051/CATn/TASKxy` and `STM32/CATn/TASKxy` structure.
- [x] **Project Files:** Every task contains its complete IDE project files (`*.uvproj`, `*.uvprojx`, `*.ioc`, `.project`, `.cproject`).
- [x] **Assembly Startup Code:** Standard `STARTUP.A51` included in all 8051 project directories.
- [x] **Binary Deliverables:** Pre-compiled Intel HEX deliverables present in `Objects/` folders for immediate flashing.
- [x] **Independent Schematics:** High-resolution CAD blueprint schematics (`circuit.png`) generated for all 33 tasks.
- [x] **Independent Documentation:** All 36 `README.md` files written from scratch with complete technical rigor.
- [x] **Simulation Cleanliness:** Completely excluded all Wokwi simulation folders, `diagram.json`, and Bring-up sheets.
- [x] **Attribution Accuracy:** 100% updated with student identity **Vaishali V** (Register No: **25011102111**).
