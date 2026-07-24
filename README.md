# 6DOF-Gaming-Gun
A dual-microcontroller haptic input device using ESP32 (BLE) and Arduino Pro Micro (HID).

# Wireless 6-DOF Motion Gaming Controller 🎮

A custom-engineered dual-unit Haptic Interface Device (HID) designed for FPS gaming. This project splits control inputs between two independent microcontrollers to emulate a fully functional keyboard and mouse setup using physical motion and gesture tracking.

![Project Status](https://img.shields.io/badge/Status-Prototype-orange)
![Platform](https://img.shields.io/badge/Platform-ESP32%20%7C%20Arduino-blue)
![Language](https://img.shields.io/badge/Language-C%2B%2B-green)

## 📖 Project Overview
Unlike standard gamepads, this controller separates movement and aiming into two distinct hands, mimicking the ergonomics of a "Gun" controller but with the precision of a PC mouse.

* **Left Hand (Movement):** Wireless ESP32 unit transmitting WASD/Jump/Reload commands via Bluetooth Low Energy (BLE).
* **Right Hand (Aiming):** Arduino Pro Micro unit handling gyroscopic aiming and trigger inputs via high-speed USB HID.

## 🚀 Key Features
* **Split-Architecture Design:** Decoupled power and processing domains for optimal performance.
* **Gyroscopic Aiming:** Uses MPU6050 sensor fusion (I2C) to map angular velocity to cursor movement.
* **Drift Compensation:** Implemented custom "Deadzone" software filtering to eliminate sensor noise and cursor drift.
* **Wireless Low-Latency:** BLE integration for the movement pad to ensure tether-free ergonomics.
* **Constraint-Driven Design:** Simplified "Combat Configuration" focusing on essential inputs for lightweight handling.

## 🛠️ Hardware Architecture

### Components Used
* **Microcontrollers:** ESP32 DevKit V1 (Left Unit), Arduino Pro Micro 5V/16MHz (Right Unit)
* **Sensor:** MPU6050 (6-Axis Accelerometer/Gyroscope)
* **Power:** 4x AA Battery Series Rail (6V) with voltage regulation.
* **Inputs:** Tactile Push Buttons (Omron/Generic).

### 🔌 Pinout & Wiring Configuration

#### Right Hand (Aiming Unit - USB)
*Powered via USB connection to PC.*

| Component | Pin | Function | Protocol |
| :--- | :--- | :--- | :--- |
| **MPU6050 SDA** | D2 | Gyro Data | I2C |
| **MPU6050 SCL** | D3 | Gyro Clock | I2C |
| **Trigger** | D9 | Fire (Left Click) | GPIO (Pull-up) |
| **Scope** | D8 | Zoom (Right Click) | GPIO (Pull-up) |

#### Left Hand (Movement Unit - Wireless)
*Powered via 6V Battery Pack to VIN.*

| Key Map | Pin | Notes |
| :--- | :--- | :--- |
| **W (Forward)** | D13 | Internal Pull-up |
| **A (Left)** | D12 | Internal Pull-up |
| **S (Backward)** | D14 | Internal Pull-up |
| **D (Right)** | D27 | Internal Pull-up |
| **Jump (Space)** | D26 | Internal Pull-up |
| **Reload (R)** | D25 | Internal Pull-up |

## 🧠 Technical Challenges & Solutions

### 1. The "Brownout" Instability
**Problem:** The ESP32's WiFi/Bluetooth radio caused significant voltage dips when powered by standard 3x AA batteries (4.5V), causing the regulator to reset.
**Solution:** Engineered a 4x AA series circuit (6V) to provide sufficient voltage headroom (Dropout Voltage + Operating Voltage) for the onboard AMS1117 regulator.

### 2. Sensor Drift
**Problem:** The MPU6050 is highly sensitive and picks up micro-tremors (hand shake), causing the cursor to "crawl" when stationary.
**Solution:** Implemented a software-side "Deadzone Filter" that ignores angular velocity values below a threshold (`int deadzone = 250`), ensuring the aim remains steady when holding angles.

## 📸 Media
<img width="1576" height="2914" alt="IMG_20251222_162754907 jpg" src="https://github.com/user-attachments/assets/09eda3fa-e126-47c4-a018-a352c4fa361c" />
<img width="3834" height="956" alt="IMG_20251222_162814207 jpg" src="https://github.com/user-attachments/assets/13858aef-f6aa-402c-bba3-82357c88042e" />
<img width="4096" height="1492" alt="IMG_20251222_162845795 jpg" src="https://github.com/user-attachments/assets/7d7751a9-da1e-4525-ba9e-0d000e07b971" />



---
*Created by Satyam Krishnan Dutta - Electronics & Communication Engineering, NIT Jamshedpur*
