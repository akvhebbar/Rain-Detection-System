# Rain Detection System using Arduino

An automated embedded system designed to detect precipitation in real time and trigger an immediate audible alert using an **Arduino Uno**, a **rain sensor module (FC-37 / YL-38 / YH-48)**, and an **active buzzer**. Developed as part of the Microcontroller and IoT Lab coursework at **REVA University, Bengaluru**.

---

## 📌 Project Overview

Rainfall monitoring plays a vital role in agriculture, smart homes, and automated transport. Traditional manual monitoring methods lack real-time automated responsiveness. 

This project bridges that gap by implementing a real-time, low-cost embedded system that converts physical wetness detected on a sensor surface into an actionable binary alert. Upon detecting rain droplets above a calibrated threshold, the system immediately sounds an active buzzer, enabling proactive responses such as closing smart windows, pausing automated irrigation schedules, or deploying rain protection mechanisms.

---

## 🎯 Key Objectives

1. **Hardware Interfacing:** Connect and calibrate a rain sensor module and an active buzzer with an Arduino Uno microcontroller.
2. **Signal Conditioning & Processing:** Map raw analog sensor data (0–1023) to an actionable range and establish a robust threshold to prevent false positives from humidity or condensation.
3. **Real-time Alert System:** Implement low-latency logic to activate an audible alarm immediately when rainfall is detected.
4. **Modular Architecture:** Provide a foundational trigger module that can easily interface with larger IoT ecosystems, automated actuators, or smart home gateways.

---

## 🛠️ Hardware Requirements

| Component | Description | Quantity |
| :--- | :--- | :--- |
| **Arduino Uno R3** | ATmega328P-based Microcontroller Board | 1 |
| **Rain Sensor Plate (FC-37)** | Interdigitated PCB conductive tracks for water detection | 1 |
| **Control Module (YL-38)** | LM393 Dual Comparator IC with sensitivity potentiometer | 1 |
| **Active Buzzer** | 5V Piezoelectric Buzzer Module with internal oscillator | 1 |
| **Breadboard & Jumpers** | Prototyping breadboard and male-to-female jumper wires | Standard Set |
| **Power Cable / Source** | USB Type-B cable or 7–12V DC Adapter | 1 |

---

## 🔌 Circuit Diagram & Pin Mapping

### Pin Connections

#### 1. Rain Sensor Module (YL-38) to Arduino Uno
* **VCC** $\rightarrow$ **5V**
* **GND** $\rightarrow$ **GND**
* **AO (Analog Output)** $\rightarrow$ **A0** (Analog Input)

#### 2. Active Buzzer Module to Arduino Uno
* **VCC** $\rightarrow$ **5V**
* **GND** $\rightarrow$ **GND**
* **I/O (Signal / Control)** $\rightarrow$ **Pin 5** (Digital Output)

> **Note:** The rain sensor sensing pad connects directly to the two input pins of the YL-38 control module board.
>
> ## How It Works
1. **Conductivity Principle:** In dry conditions, the air gap between the copper tracks on the FC-37 sensing pad provides near-infinite electrical resistance.
2. **Resistance Drop:** When water droplets fall on the pad, water bridges the conductive tracks, significantly lowering the electrical resistance across the terminals.
3. **Analog Signal Processing:** The LM393 comparator module translates this variable resistance into an analog output voltage (0–5V). The Arduino reads this value using its 10-bit Analog-to-Digital Converter (ADC) on pin A0 (0–1023).
4. **Value Mapping & Thresholding:** The raw reading is mapped into a normalized dynamic range. If mapped wetness exceeds the set = 10 threshold, digital Pin 5 outputs a HIGH signal (5V), turning on the active buzzer.

## 🧪 Results & Calibration
1. **Dry State:** Raw analog values range between 700 – 900 (5V rail), mapping below the trigger limit. The buzzer remains silent.
2. **Wet / Rain State:** Droplets lower raw readings to 100 – 300, driving the mapped output above set = 10. The system activates the buzzer in under 200ms.
3. **Sensitivity Calibration:** The onboard blue potentiometer on the LM393 comparator can be manually adjusted to tune sensitivity for local environmental conditions.

## 🚀 Limitations & Future Scope
#### Current Limitations
1. **Binary Alert Only:** Detects the presence of water but does not measure precise rainfall volume or rate (mm/hr).
2. **Local Scope:** Lacks Wi-Fi/Bluetooth capabilities for long-range remote notifications.
3. **Sensor Oxidation:** Continuous outdoor exposure can degrade exposed copper tracks over time.
