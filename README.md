# STM32F042 IMU Sensor Board

A compact, USB-C powered sensor board built around the STM32F042 microcontroller and the BMI088 6-axis IMU. Designed in Altium Designer.

![PCB Render](docs/pcb_render.png)

## Overview

This board is a small, self-contained motion-sensing platform. It takes power directly from USB-C, regulates it on-board, and streams real-time accelerometer and gyroscope data from the BMI088 through an STM32F042 microcontroller over its native USB peripheral — no external USB-to-serial bridge required.

It's suited for applications such as:
- Robotics and motion control
- Flight controller / stabilization experimentation
- Motion capture
- General-purpose inertial data logging over USB

## Features

- **MCU:** STM32F042G6U6 (Arm Cortex-M0), native USB 2.0 full-speed peripheral
- **IMU:** BMI088 6-axis (accelerometer + gyroscope), SPI interface
- **Power:** Single USB-C input, on-board LTC3405 synchronous buck converter regulating to 3.3V
- **Connectivity:**
  - USB-C for power and data
  - I2C header for external sensors/modules
  - SWD header for programming and debugging
- **Form factor:** Compact footprint, mounting holes for enclosure integration

## Hardware Summary

| Block | Component | Notes |
|---|---|---|
| Power | LTC3405ES6TRMPBF | Synchronous buck, 5V → 3.3V |
| MCU | STM32F042G6U6 | UFQFPN28, USB remapped to PA9/PA10 |
| IMU | Bosch BMI088 | SPI communication, dual chip-select (accel/gyro) |
| USB | USB4105-GF-A-060 | USB-C receptacle |
| Debug | SWD header | SWDIO, SWCLK, NRST, 3V3, GND |
| Expansion | I2C header | SCL, SDA, GND, 3V3 |

## Repository Structure

```
.
├── Hardware/
│   ├── Schematics/         # Altium schematic sheets (PDF + source)
│   ├── PCB/                # Altium PCB project files
│   ├── Gerbers/            # Manufacturing output (Gerbers, drill files)
│   ├── BOM/                # Bill of materials (CSV/Excel)
│   └── 3D_Renders/         # PCB render images
├── docs/
│   └── pcb_render.png
└── README.md
```

## Getting Started

### Manufacturing
Gerber and drill files are available in `Hardware/Gerbers/` and are ready to submit to any standard PCB fabrication house (2-layer, 1.6mm, HASL or ENIG finish recommended).

### Assembly
A full BOM with part numbers and footprints is provided in `Hardware/BOM/`. All components are compatible with standard SMT assembly processes.

### Firmware
This repository covers hardware design only. Firmware for reading BMI088 data over SPI and streaming it over USB is not included here.

### Programming
Connect an SWD programmer/debugger (e.g., ST-Link) to the onboard SWD header to flash firmware.

## Design Notes

Key design considerations addressed during layout:
- Clean power delivery under the switching regulator, with ferrite bead filtering on sensitive digital rails
- High-speed USB2.0 differential pair routing
- Careful component placement given the board's compact footprint

## Credits

This project was built with guidance from the **Microcontroller-Based Hardware Design** course by **Phil's Lab (Philip Salmony)**, produced in partnership with **Altium Academy**.

## License

This hardware design is released under the [CERN-OHL-P v2](https://ohwr.org/cern_ohl_p_v2.txt) (or specify your preferred open hardware license).

## Author

Designed by **Abdulhakim (Pasha)** — Electrical Power and Machines Engineering student, Alexandria University.
