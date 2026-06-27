# 👾 ESP32-C3 Stealth Retro Console

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![ESP32-C3](https://img.shields.io/badge/Hardware-ESP32--C3-blue.svg)
![Status](https://img.shields.io/badge/Status-Project_Active-brightgreen.svg)

A custom, solid-state, retro-futuristic handheld game console built around the **Waveshare ESP32-C3-Zero**. 

This project discards the mechanical switches of the 90s for a completely "stealth" modern architecture. Utilizing capacitive touch, deep-sleep power management, and over-the-air (OTA) wireless flashing, it functions like a high-tech smart device disguised as a minimalist 8-bit pocket toy.

---

## ✨ Key Features
* **Solid-State Interface:** Zero moving parts. Controls are handled by internal TTP223 capacitive sensors reading your thumbs through a solid 3D-printed faceplate.
* **Invisible Power System:** No mechanical switches. A 1.5-second hold on the center pad wakes the console from a 5µA Deep Sleep. A 2.0-second hold puts it back to sleep.
* **Over-The-Air (OTA) Updates:** Hold `UP + DOWN` to toggle the internal Wi-Fi. Beam new games into the processor wirelessly.
* **Living UI:** Animated "Living Eyes" greet you on boot, transitioning to a game menu via double-tap.
* **High-Contrast Display:** Features a crisp 1.3-inch Full White OLED (SH1106) for perfect blacks and zero motion blur.

---

## 🛠️ Hardware Stack
This build utilizes "Dead Bug" point-to-point wiring to achieve an ultra-thin profile.

| Component | Purpose |
| :--- | :--- |
| **Waveshare ESP32-C3-Zero** | 160MHz RISC-V Brain with Wi-Fi. |
| **1.3" OLED (SH1106)** | Pure white emissive display. |
| **5x TTP223 Modules** | Capacitive D-Pad and Action buttons. |
| **Passive Buzzer** | 8-bit PWM sound generation. |
| **TP4056 Module** | USB-C Li-Po charging. |
| **600mAh Li-Po** | Powers ~7 hours of active play. |

---

## 🔌 Wiring & Logic
The battery is permanently connected, relying on the ESP32’s RTC controller to maintain a 5µA standby current—allowing for years of shelf life.

* **Power:** Battery -> TP4056 -> ESP32 5V.
* **Signal Mapping:** * `GPIO 0, 1, 2, 3` -> D-Pad (Left, Right, Down, Up).
    * `GPIO 4` -> Rotate (Hardware Wake-up).
    * `GPIO 5` -> Buzzer Signal.
    * `GPIO 6, 7` -> OLED (SCL/SDA).

---

## 🎮 Controls & Gestures
* **Wake/Turn ON:** Long-press `ROTATE` (1.5s).
* **Turn OFF:** Long-press `ROTATE` (2.0s).
* **Start Game:** Single-tap `ROTATE` in Menu.
* **Jump/Flap:** Tap `UP`.
* **Toggle Wi-Fi:** Long-press `UP + DOWN` (1.5s).

---

## 🚀 Flashing & Deployment

To deploy the console firmware to your ESP32-C3-Zero, we utilize a streamlined web-based flashing tool.

1. **Access the Portal:** Navigate to the official deployment interface at:
   [https://robonavigators.github.io/](https://robonavigators.github.io/)
   
2. **Connect Device:** Plug your ESP32-C3-Zero into your computer using a data-capable USB-C cable. 
   > *Note: Ensure your cable is capable of data transfer, as some USB-C cables are power-only.*

3. **Select & Flash:**
   * Select your hardware target (`ESP32-C3`) from the dashboard.
   * Click the **Connect** button in your browser to pair with the device.
   * Click **Install/Flash** to push the firmware directly to the RISC-V processor. 

The web-based tool will automatically handle the baud rate and memory address offsets. Once the progress bar reaches 100%, your console will automatically reboot and start the **Living Eyes** boot animation!

---

## 📄 License
MIT License

Copyright (c) 2026 [Your Name/Handle]

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
