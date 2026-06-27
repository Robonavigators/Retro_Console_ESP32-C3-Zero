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
* **Signal Mapping:**
    * `GPIO 0` -> TTP_LEFT
    * `GPIO 1` -> TTP_RIGHT
    * `GPIO 2` -> TTP_DOWN
    * `GPIO 3` -> TTP_UP
    * `GPIO 4` -> TTP_ROTATE (Hardware Wake-up)
    * `GPIO 5` -> BUZZER_SIGNAL
    * `GPIO 6, 7` -> OLED (SCL/SDA)

### 📌 Pin Mapping Diagram
```text
       ┌───────────────────────────┐
       │     ESP32-C3-Zero         │
       │                           │
  GND ─┤─ (GND)       (3V3) ─┤──┬───► VCC Bus (OLED, TTPs, Buzzer)
  5V  ─┤─ (5V)        (GND) ─┤──┴───► GND Bus
       │                           │
GPIO 0 ├──────────► TTP_LEFT       │
GPIO 1 ├──────────► TTP_RIGHT      │
GPIO 2 ├──────────► TTP_DOWN       │
GPIO 3 ├──────────► TTP_UP         │
GPIO 4 ├──────────► TTP_ROTATE     │
GPIO 5 ├──────────► BUZZER_SIGNAL  │
GPIO 6 ├──────────► OLED_SCL       │
GPIO 7 ├──────────► OLED_SDA       │
       └───────────────────────────┘
