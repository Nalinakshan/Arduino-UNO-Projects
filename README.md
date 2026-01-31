
# ☀️ Helios: Dual-Axis Solar Tracker

### 👤 **Created by: Nalinakshan (Code Knight)**

* *Student & Embedded Systems Enthusiast*
* *Harnessing the power of the sun through automation.*

---

## 📜 Project Overview

**Helios** is an intelligent, dual-axis solar tracking system designed to maximize the efficiency of photovoltaic (solar) panels. Unlike static solar panels, this system actively monitors light intensity and adjusts its position (Horizontal and Vertical) to ensure the panel always faces the sun directly.

### 💡 Key Features

* **Dual-Axis Movement:** Tracks the sun's path from East to West (Azimuth) and its seasonal height changes (Altitude).
* **Smart Sensing:** Uses 4 Light Dependent Resistors (LDRs) to detect light intensity differences.
* **Jitter Prevention:** Includes a `tolerance` threshold to prevent the motors from twitching due to minor light fluctuations.
* **Automated Calibration:** Moves servos to a default starting position on boot.

---

## 🛠️ Hardware Requirements

To build this project, you will need the following components:

1. **Microcontroller:** Arduino Uno (or compatible board).
2. **Actuators:** 2x Servo Motors (SG90 or MG995).
* *1x Horizontal (Bottom)*
* *1x Vertical (Top)*


3. **Sensors:** 4x LDRs (Light Dependent Resistors).
4. **Resistors:** 4x 10kΩ resistors (for voltage divider circuit).
5. **Mounting:** Pan-tilt bracket kit or custom frame.
6. **Power Supply:** 5V external power source (recommended for servos).

---

## 🔌 Circuit & Pinout Configuration

Based on the code structure, wire your components as follows:

### 🧩 LDR Sensor Array

The sensors function as a voltage divider. Connect one leg of the LDR to 5V, and the other leg to the Analog Pin **AND** to GND via a 10kΩ resistor.

| Sensor Position | Variable Name | Arduino Pin |
| --- | --- | --- |
| **Top Left** | `ldrlt` | **A0** |
| **Top Right** | `ldrrt` | **A3** |
| **Bottom Left** | `ldrld` | **A1** |
| **Bottom Right** | `ldrrd` | **A2** |

### ⚙️ Servo Motors

| Motor Axis | Arduino Pin | Limits (Degrees) |
| --- | --- | --- |
| **Horizontal (Base)** | **Pin 2** | 5° - 175° |
| **Vertical (Tilt)** | **Pin 13** | 1° - 100° |

> **⚠️ Note on Power:** Do not power large servos directly from the Arduino's 5V pin if the load is heavy. Use an external power source with a common ground.

---

## 🧠 Code Logic & Algorithm

The system operates on a comparative algorithm loop:

1. **Data Acquisition:** Reads analog values (0-1023) from all four LDRs.
2. **Averaging:** Calculates the average light intensity for:
* Top vs. Bottom (`avt` vs `avd`)
* Left vs. Right (`avl` vs `avr`)


3. **Comparison:**
* Calculates the difference (`dvert` and `dhoriz`).
* Checks if the difference exceeds the **Tolerance** (`tol = 90`).


4. **Adjustment:**
* If **Top > Bottom**: Tilt Up.
* If **Left > Right**: Rotate Left.
* (And vice versa).


5. **Constraints:** Software limits ensure the servos do not hit the mechanical stops (e.g., Vertical is limited to 100° to prevent crashing into the base).

---

## 🚀 Installation

1. **Clone the Repository:**
```bash
git clone https://github.com/YourUsername/Helios-Solar-Tracker.git

```


2. **Open in Arduino IDE:** Load the `.ino` file.
3. **Install Libraries:** Ensure the `<Servo.h>` library is installed (Standard in Arduino IDE).
4. **Connect & Upload:** Select your Board and COM Port, then hit Upload.

---

> "The sun does not move for us, so we must move for the sun." – Code Knight

*Last Updated: 2026*
