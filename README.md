# Self-Balancing Robot — STM32

A two-wheeled self-balancing robot built around an STM32 microcontroller, using IMU sensor fusion (Kalman filter) and PID control to maintain an upright equilibrium. A companion ESP32 handles wireless communication, and a desktop application provides remote control and live telemetry.

**Demo video:** https://youtu.be/Z_mbFLvszcI

## Overview

The robot continuously estimates its tilt angle from an MPU6050 IMU, fuses the accelerometer and gyroscope readings with a Kalman filter to reduce noise and drift, and feeds the estimate into a PID control loop that drives the motors to keep the robot balanced (within ±2° tilt error). The STM32 (real-time control core) and ESP32 (wireless bridge) communicate over UART, allowing the robot to be remotely controlled and monitored from a desktop GUI over Bluetooth.

## Features

- Real-time balance control using PID
- Kalman filter–based sensor fusion (MPU6050 accelerometer + gyroscope)
- Dual-microcontroller architecture (STM32 for control, ESP32 for wireless communication)
- Bluetooth-based remote control via a custom Python desktop application
- Live telemetry streaming to the desktop app

## Architecture

```
 MPU6050 (IMU) ──► STM32 (Kalman Filter + PID Control) ──► Motor Drivers
                          │
                          │ UART
                          ▼
                       ESP32 ──► Bluetooth ──► Desktop Controller (Python GUI)
```

## Repository Structure

| Path | Description |
|---|---|
| `STM32_code/` | Firmware for the STM32 — sensor fusion, PID control loop, motor drive logic |
| `ESP32_code/` | Firmware for the ESP32 — UART bridge to STM32, Bluetooth communication |
| `Desktop_Controller/` | Python desktop application for remote control and telemetry visualization |
| `doc/documentation_v1.0/` | Full project documentation |

## Getting Started

### Hardware Requirements
- STM32 development board
- ESP32 development board
- MPU6050 IMU
- Motor driver + DC motors with encoders (or equivalent drive setup)
- Chassis, battery, and wiring

### STM32 Firmware
See [`STM32_code/`](./STM32_code) for the control firmware. Flash it to the STM32 using your preferred toolchain (e.g., STM32CubeIDE).

### ESP32 Firmware
See [`ESP32_code/`](./ESP32_code) for the wireless bridge firmware. Flash it using the Arduino IDE or PlatformIO.

### Desktop Controller
See [`Desktop_Controller/`](./Desktop_Controller) for the Python GUI. Pair with the ESP32 over Bluetooth to send commands and view live telemetry.

## Documentation

Full documentation is available at [`doc/documentation_v1.0`](./doc/documentation_v1.0), covering hardware setup, wiring diagrams, and firmware details.

## Demo

Watch the robot balancing in action: https://youtu.be/Z_mbFLvszcI

