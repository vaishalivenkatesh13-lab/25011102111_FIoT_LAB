# EXPERIMENT DETAILS
- **Student Name:** Vaishali V
- **Register Number:** 25011102111
- **Degree / Branch:** B.Tech. Computer Science and Engineering (IoT)
- **Year / Semester:** II Year / III Semester
- **Course Title:** Fundamentals of Internet of Things Laboratory (25CS2741)
- **Academic Year:** 2026–2027

---

# 8051 MICROCONTROLLER LABORATORY PLATFORM
### MCS-51 Embedded Architecture, SFR Programming & Peripheral Interfacing

This directory houses the complete set of 15 embedded C practical laboratory experiments developed for the **Microchip AT89S52 (MCS-51 architecture)** microcontroller. The curriculum begins with fundamental bare-metal register manipulation and progresses systematically through hardware timers, interrupts, serial communications, and interactive human-machine interfaces.

---

## 1. Architectural Overview & System Resources

The AT89S52 is a classical 8-bit Harvard architecture microcontroller featuring separated program and data memory spaces:
- **Processor Core:** MCS-51 8-bit CPU operating at 11.0592 MHz.
- **Machine Cycle Structure:** 1 machine cycle consists of 12 oscillator clock periods:
  $$T_{{mc}} = \frac{{12}}{{11.0592 \text{{ MHz}}}} = 1.085069 \,\mu\text{{s}}$$
- **Internal RAM:** 256 bytes total (Lower 128 bytes: 4 register banks R0–R7, bit-addressable RAM from 0x20 to 0x2F, and general scratchpad; Upper 128 bytes accessed indirectly).
- **Special Function Registers (SFRs):** Mapped from address `0x80` to `0xFF`, accessed directly via symbolic names defined in `<reg52.h>`.
- **Parallel I/O Ports:** Four 8-bit quasi-bidirectional I/O ports (Port 0: Open-drain, Ports 1–3: Internal weak pull-ups).
- **Timers/Counters:** Dual 16-bit Timer/Counters (Timer 0 and Timer 1) configurable across 4 operational modes via `TMOD`.
- **Interrupt Controller:** 6 interrupt vectors with 2 priority levels, enabled via `IE` and prioritized via `IP`.
- **Full-Duplex UART:** Hardware serial transceiver supporting standard asynchronous modes with programmable baud rates.

---

## 2. Directory Index of 8051 Experiments

```text
8051/
├── CAT2/
│   ├── TASK2B/       # Bare-Metal GPIO LED Blink (P1.0 Sink, 1 Hz)
│   └── TASK2C/       # Multi-Pattern 8-LED Chaser (Chaser, Bounce, Fill & Drain)
├── CAT3/
│   └── TASK3A/       # 4-Bit Binary Counter (0000 to 1111 on P1.0..P1.3)
├── CAT4/
│   └── TASK4A/       # 8-Bit Button-Controlled Counter (P3.2 Push-Button Input)
├── CAT5/
│   ├── TASK5A/       # Timer 0 Mode 1 Periodic Interrupt (1s Software Timebase)
│   ├── TASK5B/
│   │   ├── TASK5B.1/ # Software PWM LED Fading (Mode 2 Auto-Reload, 1 kHz)
│   │   ├── TASK5B.2/ # Dual-Frequency Blink Generator (1 Hz Normal / 5 Hz Alert)
│   │   └── TASK5B.3/ # Hardware Square Wave Generator (2 kHz Tone on P1.0)
│   └── TASK5C/       # Timer-Accurate Delay Library vs Software Busy-Wait Loops
├── CAT6/
│   ├── TASK6A/       # Polled UART Serial Transmitter (9600 Baud 8-N-1)
│   ├── TASK6B/       # Polled UART Full-Duplex Echo Transceiver
│   └── TASK6C/       # Interrupt-Driven UART with 16-Byte Circular FIFO
└── CAT7/
    ├── TASK7A/       # 16x2 Alphanumeric LCD Driver (HD44780 4-Bit Nibble Mode)
    ├── TASK7B/       # 4x4 Matrix Keypad Interfacing with LCD Text Output
    └── TASK7C/       # 2D Keypad-Driven LCD Sprite Navigation (Interactive HMI)
```

---

## 3. Peripheral Interfacing Summary

### A. Active-LOW Output Sinking Drive
The 8051's quasi-bidirectional ports feature internal pull-up FETs capable of sourcing only ~100 µA, but their internal pull-down FETs can sink up to 10–20 mA. Consequently, external LEDs are wired in **active-LOW sink configuration**:
- LED Anodes tied to +5V through 330 Ω current-limiting resistors.
- LED Cathodes tied directly to microcontroller port pins.
- Writing `0` turns the LED ON; writing `1` turns the LED OFF.

### B. Hardware Timer & Baud Rate Generation
An 11.0592 MHz crystal provides exact integer divisions for standard serial baud rates:
- **Timer 1 in Mode 2 (8-bit Auto-Reload):**
  $$\text{{TH1}} = 256 - \frac{{F_{{osc}}}}{{384 \times \text{{Baud Rate}}}} = 256 - 3 = 253 = \text{{0xFD}} \quad (\text{{for 9600 Baud}})$$
- **Timer 0 in Mode 1 (16-bit Timer):**
  $$\text{{Preload}} = 65536 - \frac{{1000 \,\mu\text{{s}}}}{{1.085069 \,\mu\text{{s}}}} = 65536 - 922 = 64614 = \text{{0xFC66}} \quad (\text{{for 1 ms tick}})$$

---

## 4. Keil µVision Toolchain & Flashing Guide

1. Open project file (`*.uvproj`) inside Keil µVision.
2. Ensure Target Device is set to **Microchip (Atmel) AT89S52**.
3. Press **F7** to compile and build target.
4. Verify Intel HEX binary is generated in the `Objects/` directory.
5. Flash binary to target using an ISP programmer (e.g. ProgISP or USBASP).
