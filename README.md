# Fundamentals of IoT Laboratory – Embedded Systems & Wireless IoT Architectures

Coursework and laboratory portfolio for **25CS2741 Fundamentals of Internet of Things + Lab**  
**Student:** Vaishali V  
**Register Number:** 25011102111  
**Degree & Department:** B.Tech Computer Science and Engineering (Internet of Things)  
**Academic Year:** 2026–2027 | **Semester:** III  
**Institution:** Shiv Nadar University Chennai  

---

## Technical Overview

This repository documents the practical implementations, firmware designs, hardware schematics, and experimental analyses completed as part of the *Fundamentals of Internet of Things Laboratory* curriculum. The coursework establishes a solid foundation in low-level microcontrollers before scaling up to high-performance ARM Cortex-M processors and network-connected edge nodes:

1. **8051 Architecture (Atmel AT89S52):** Low-level bare-metal firmware development using Keil µVision C51. Experiments progress from bit-addressable SFR manipulation and modular software timing libraries to finite-state-machine switch debouncing, 4×4 matrix keypad multiplexing, 7-segment display decoding, hardware timer timebases, full-duplex asynchronous serial communication (UART), and HD44780 16×2 alphanumeric LCD interfacing in 4-bit mode.
2. **STM32 Architecture (ARM Cortex-M3 & Cortex-M4):** Advanced embedded software engineering using STM32CubeMX and the STM32 Hardware Abstraction Layer (HAL) in STM32CubeIDE. Covers digital I/O configuration, non-blocking tick-based contact debouncing, short-press versus long-press hold-time discrimination, interrupt-driven and polled UART communication, string command line interpretation, and multi-USART telemetry links.
3. **Connected IoT & Cloud Telemetry:** Edge-to-cloud integration coupling the STM32F401RE microcontroller with an external ESP8266 (Wemos D1 Mini) Wi-Fi modem and a Bosch Sensortec BME280 precision environmental sensor over I²C. Demonstrates station-mode Wi-Fi association, an embedded HTTP web server serving live sensor telemetry, and an end-to-end binary MQTT v3.1.1 protocol client publishing JSON-formatted sensor telemetry to public cloud message brokers.

Every assessment module contains an independent `README.md` providing comprehensive laboratory documentation: experimental aims, component bills of materials, technical hardware specifications, pin connection matrices, schematic diagrams, working principles, algorithmic logic/flow, source code walkthroughs, expected terminal/physical outputs, and experimental inferences.

---

## Summary of Laboratory Assessments

### 1. 8051 Microcontroller (AT89S52) – Keil µVision C51 Toolchain

| Assessment | Experiment Title | Core Architectural Concepts | Workspace Directory |
|---|---|---|---|
| [Assessment 2](8051/CAT2/) | Board Bring-Up, Direct SFR LED Blinking & Modular Millisecond Delay Module | Bit-addressable SFR registers (`sbit`), quasi-bidirectional I/O, machine cycle execution timing, modular C libraries (`delay.h` / `delay.c`) | [`TASK_2`](8051/CAT2/TASK_2_Bare_Metal_LED_Blink/), [`TASK_3`](8051/CAT2/TASK_3_Custom_Delay_Library/) |
| [Assessment 3](8051/CAT3/) | Multi-Mode LED Lighting Sequencer with Software Switch Debouncing | Active-low matrix column driving, row polling, software transient filtering, finite state machine (FSM) sequence dispatch | [`CAT3`](8051/CAT3/) |
| [Assessment 4](8051/CAT4/) | Human-Machine Interface: 4×4 Matrix Keypad, 7-Segment Display & LEDs | Row-column matrix scanning, common-cathode 7-segment segment lookup decoding, interactive multi-pattern LED operation | [`CAT4`](8051/CAT4/) |
| [Assessment 5](8051/CAT5/) | Hardware Timer 0 Polling for Precise Periodic LED Toggling | 16-bit Timer 0 Mode 1, reload constant calculation, overflow flag (`TF0`) polling, hardware-governed timebase | [`CAT5`](8051/CAT5/) |
| [Assessment 6](8051/CAT6/) | Asynchronous Serial UART Driver & Full-Duplex Terminal Loopback | Mode 1 8-bit UART, Timer 1 Mode 2 8-bit auto-reload baud synthesis (9600 baud), `SBUF` register transfer, `TI`/`RI` flag polling | [`TASK_A`](8051/CAT6/TASK_A_UART_Initialization_and_Character_Transmission/), [`TASK_B`](8051/CAT6/TASK_B_UART_Echo/) |
| [Assessment 7](8051/CAT7/) | 16×2 Alphanumeric LCD Driver & Interactive Keypad Coordinate Navigation | HD44780 4-bit nibble interface, DDRAM address positioning, dynamic numeric field formatting, 2D keypad cursor manipulation | [`TASK_7A`](8051/CAT7/TASK_7A_LCD_Initialization_and_Character_String_Display/), [`TASK_7B`](8051/CAT7/TASK_7B_Cursor_Positioning_and_Dynamic_Value_Update/), [`TASK_7C`](8051/CAT7/TASK_7C_Keypad_Based_Character_Movement/) |

---

### 2. STM32 Embedded Microcontrollers – STM32CubeIDE & HAL Drivers

| Assessment | Experiment Title | Hardware Platform | Key Embedded Principles | Workspace Directory |
|---|---|---|---|---|
| [Assessment 8](STM32/CAT8/) | STM32 GPIO Bring-Up, Event Detection & Push-Duration Classification | Blue Pill (STM32F103C6T6A) | Push-pull GPIO output, internal pull-up digital input, non-blocking `HAL_GetTick()` debouncing, short (<1 s) vs. long (≥1 s) press detection | [`TASK_8A`](STM32/CAT8/TASK_8A_GPIO_Input_Output/), [`TASK_8B`](STM32/CAT8/TASK_8B_Event_Based_Control/), [`TASK_8C`](STM32/CAT8/TASK_8C_Short_Press_vs_Long_Press/) |
| [Assessment 9](STM32/CAT9/) | Serial UART Interface & String-Based LED Command Interpreter | Blue Pill (STM32F103C6T6A) | HAL UART polling, diagnostic periodic beacons, circular line buffering, delimiter parsing (`\r`/`\n`), string command dispatch | [`TASK_9A`](STM32/CAT9/TASK_9A_Basic_UART_Communication/), [`TASK_9B`](STM32/CAT9/TASK_9B_String_Based_Application_Logic/) |
| [Assessment 10](STM32/CAT10/) | STM32 to ESP8266 Modem Interfacing via AT Command Architecture | Blue Pill (STM32F103C8T6) | Dual asynchronous USART bridging (`USART1` modem, `USART2` console), AT command sequencing, Wi-Fi station scan, join, and IP acquisition | [`TASK_9A`](STM32/CAT10/TASK_9A_Establish_STM32_Wemos_UART_Communication/), [`TASK_9B`](STM32/CAT10/TASK_9B_Explore_ESP8266_AT_Command_Interface/), [`TASK_9C`](STM32/CAT10/TASK_9C_Connect_Wemos_to_WiFi/) |
| [Assessment 11](STM32/CAT11/) | Cortex-M4 GPIO Bring-Up & Multi-Mode Push-Button Control | NUCLEO-F401RE | HSE bypass clock distribution (84 MHz sysclk), active-high LED control, non-blocking multi-mode state latching | [`Core`](STM32/CAT11/Core/) |
| [Assessment 12](STM32/CAT12/) | BME280 I²C Environmental Sensing & Embedded HTTP Web Server | NUCLEO-F401RE | Master-mode I²C at 100 kHz, Bosch BME280 compensation API integration, interrupt-driven UART buffer assembly, raw HTTP/1.1 response generation | [`Core`](STM32/CAT12/Core/) |
| [Assessment 13](STM32/CAT13/) | Custom ESP8266 MQTT Client & Live Cloud Environmental Telemetry | NUCLEO-F401RE | Custom modular ESP8266 API (`ESPLib`), binary MQTT v3.1.1 `CONNECT`/`PUBLISH` frame packaging, JSON sensor payload serialization, cloud broker streaming | [`Core`](STM32/CAT13/Core/) |

---

## Hardware Inventory & Module Specifications

| Hardware Component | Utilized In | Technical Specifications & Implementation Roles |
|---|---|---|
| **AT89S52 Microcontroller Development Board** | CAT 2 – CAT 7 | 8-bit MCS-51 core, 11.0952 MHz quartz crystal oscillator (1.0815 µs machine cycle), 8 KB In-System Programmable (ISP) flash memory, bit-addressable Port 1–Port 3 registers, onboard active-low LED (`P1.0`), common-cathode 7-segment display, 4×4 matrix keypad, HD44780 LCD socket. |
| **STM32 Blue Pill (STM32F103C6 / C8)** | CAT 8 – CAT 10 | 32-bit ARM Cortex-M3 core, 72 MHz max operating frequency (8 MHz HSE crystal with internal PLL), 32 KB / 64 KB flash memory, 20 KB SRAM, onboard active-low indicator LED on `PC13`, programmed via ST-LINK SWD interface. |
| **STM32 NUCLEO-F401RE Development Board** | CAT 11 – CAT 13 | 32-bit ARM Cortex-M4 CPU with single-precision hardware FPU, 84 MHz sysclk (HSE bypass from onboard ST-LINK debugger), 512 KB flash, 96 KB SRAM, green user LED `LD2` on `PA5`, blue tactile push-button `B1` on `PC13`. |
| **Wemos D1 Mini (ESP8266 Wi-Fi Transceiver)** | CAT 10, CAT 12, CAT 13 | 2.4 GHz IEEE 802.11 b/g/n wireless modem operating with standard Espressif AT firmware (115200 baud, 8-N-1); executes Wi-Fi network management, TCP client/server socket routing, and HTTP/MQTT data bridging. |
| **Bosch Sensortec BME280 Environmental Sensor** | CAT 12, CAT 13 | Combined digital humidity (0–100% RH), barometric pressure (300–1100 hPa), and ambient temperature (−40°C to +85°C) sensor communicating over I²C (slave address `0x76`); reads calibrated factory compensation coefficients. |
| **USB-to-TTL UART Bridge (CP2102 / FTDI / CH340)** | CAT 6, CAT 9, CAT 10, CAT 12 | 3.3 V / 5 V logic-level serial interface linking microcontroller hardware UART lines to host workstation serial terminal emulators (PuTTY / Serial Studio). |

---

## Software Toolchains & Libraries

| Tool / Framework | Role & Scope |
|---|---|
| **Keil µVision 5 (C51 Toolchain)** | IDE, C compiler, macro assembler (`STARTUP.A51`), and linker utilized for all AT89S52 bare-metal embedded C projects. Generates production-ready Intel `.hex` binary images. |
| **STM32CubeIDE & STM32CubeMX** | Integrated Development Environment and graphical pinout/clock-tree initialization tool for ARM Cortex-M systems. Manages project configurations (`.ioc`, `.project`, `.cproject`). |
| **STM32Cube HAL Drivers (F1 & F4)** | STMicroelectronics Hardware Abstraction Layer libraries bundled inside the respective assessment directories, providing peripheral drivers for GPIO, UART, I²C, RCC, and Core System services. |
| **Bosch Sensortec BME280 Driver (v3.5.1)** | Sensor manufacturer API (`bme280.c`, `bme280.h`, `bme280_defs.h`) providing factory calibration curve compensation for pressure, temperature, and relative humidity. |
| **PuTTY Serial Monitor** | Terminal emulator configured for serial sessions at 9600 baud (8051) and 115200 baud (STM32) for live diagnostics, command submission, and data logging. |

---

## Project Repository Structure

```
25011102111_FIoT_LAB/
├── .gitignore                      # Git exclusion rules for IDE artifacts and object files
├── README.md                       # Main laboratory documentation and portfolio overview
├── 8051/                           # AT89S52 8051 microcontroller laboratory assessments
│   ├── CAT2/                       # Board bring-up, LED blink, and custom delay library
│   │   ├── README.md
│   │   ├── circuit.png
│   │   ├── TASK_2_Bare_Metal_LED_Blink/
│   │   └── TASK_3_Custom_Delay_Library/
│   ├── CAT3/                       # Push-button controlled multi-pattern LED sequencer
│   │   ├── README.md
│   │   ├── circuit.png
│   │   └── Objects/day2.hex
│   ├── CAT4/                       # 4x4 matrix keypad, 7-segment display, and LED HMI
│   │   ├── README.md
│   │   ├── circuit.png
│   │   └── Objects/sevenseg.hex
│   ├── CAT5/                       # Hardware Timer 0 polling and timebase generation
│   │   ├── README.md
│   │   ├── circuit.png
│   │   └── Objects/timers.hex
│   ├── CAT6/                       # Serial UART transmission and terminal character echo
│   │   ├── README.md
│   │   ├── circuit.png
│   │   ├── TASK_A_UART_Initialization_and_Character_Transmission/
│   │   └── TASK_B_UART_Echo/
│   └── CAT7/                       # 16x2 alphanumeric LCD driver and keypad navigation
│       ├── README.md
│       ├── circuit.png
│       ├── TASK_7A_LCD_Initialization_and_Character_String_Display/
│       ├── TASK_7B_Cursor_Positioning_and_Dynamic_Value_Update/
│       └── TASK_7C_Keypad_Based_Character_Movement/
└── STM32/                          # ARM Cortex-M3 & Cortex-M4 laboratory assessments
    ├── CAT8/                       # Blue Pill GPIO bring-up, event control, and press duration
    │   ├── README.md
    │   ├── circuit.png
    │   ├── TASK_8A_GPIO_Input_Output/
    │   ├── TASK_8B_Event_Based_Control/
    │   └── TASK_8C_Short_Press_vs_Long_Press/
    ├── CAT9/                       # Blue Pill UART serial echo and string command parser
    │   ├── README.md
    │   ├── circuit.png
    │   ├── TASK_9A_Basic_UART_Communication/
    │   └── TASK_9B_String_Based_Application_Logic/
    ├── CAT10/                      # STM32 to Wemos D1 Mini AT command Wi-Fi interfacing
    │   ├── README.md
    │   ├── circuit.png
    │   ├── TASK_9A_Establish_STM32_Wemos_UART_Communication/
    │   ├── TASK_9B_Explore_ESP8266_AT_Command_Interface/
    │   └── TASK_9C_Connect_Wemos_to_WiFi/
    ├── CAT11/                      # NUCLEO-F401RE Cortex-M4 GPIO bring-up and button latching
    │   ├── README.md
    │   ├── circuit.png
    │   └── Core/
    ├── CAT12/                      # BME280 I2C sensor integration and ESP8266 HTTP web server
    │   ├── README.md
    │   ├── circuit.png
    │   └── Core/
    └── CAT13/                      # Custom ESP8266 MQTT client publishing BME280 telemetry
        ├── README.md
        ├── circuit.png
        └── Core/
```

---

## Build & Flashing Guidelines

### 8051 Microcontroller Projects (Keil µVision)
1. Launch **Keil µVision 5** and open the target project file (`.uvproj`) located within the relevant experiment subfolder.
2. Verify target device configuration: ensure target crystal oscillator frequency is set to `11.0592 MHz` / `11.0952 MHz` and **Create HEX File** is checked under **Project → Options for Target → Output**.
3. Compile and assemble the firmware by pressing **F7** (or selecting **Project → Build Target**).
4. Connect the AT89S52 development kit via the dedicated SPI ISP programmer.
5. Use an ISP utility (such as ProgISP / ATMEL FLIP) to flash the generated Intel `.hex` binary (retained inside `Objects/`) onto the target MCU.

### STM32 Microcontroller Projects (STM32CubeIDE)
1. Open **STM32CubeIDE** and choose a clean workspace directory.
2. Select **File → Import → General → Existing Projects into Workspace**, browse to the required experiment directory, and import the project.
3. If hardware pins or clocks require re-inspection, open the `.ioc` file to view the STM32CubeMX device configuration.
4. Build the target project by pressing **Ctrl + B** (or selecting **Project → Build Project**).
5. Connect the STM32 board (Blue Pill via ST-LINK V2 SWD or Nucleo via onboard ST-LINK USB interface).
6. Click **Run → Debug** (or **Run → Run**) to flash the target memory and execute the program.
7. *Note for Wireless Experiments (CAT 10, CAT 12, CAT 13):* Update the Wi-Fi credentials (`SSID` and `PASSWORD`) macros inside `Core/Src/main.c` before compiling.

---

## Student Identity & Attribution

- **Student Name:** Vaishali V
- **Register Number:** 25011102111
- **Program:** B.Tech Computer Science and Engineering (IoT)
- **Course:** Fundamentals of Internet of Things + Lab (25CS2741)
- **Academic Year:** 2026–2027
