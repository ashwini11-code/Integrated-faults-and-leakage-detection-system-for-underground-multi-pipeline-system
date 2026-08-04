#  ESP32 Multi-Utility Pipe Monitoring System

An IoT-based multi-utility pipeline monitoring and fault detection system powered by an **ESP32 microcontroller**. This system continuously tracks parameters across **Water, Gas, Electrical, and Optical** utilities, alerting users to leakages, line drops, structural cracks, and fault conditions in real time via an LCD display and auditory alarms.

---

##  System Features

* 💧 **Water Flow & Quality Monitoring:** Tracks water flow rate in liters per minute (LPM) and measures pH levels for water safety.
* ⛽ **Gas Flow & Leakage Detection:** Calculates gas flow rates and utilizes an MQ gas sensor to detect hazardous gas leaks.
* ⚡ **Electrical Fault Simulation:** Monitors line status and allows manual fault toggling via a physical switch mechanism.
* 👁️ **Optical Pipe Crack Detection:** Employs an LDR sensor to detect structural cracks via light loss/exposure.
* 🚨 **Automated Alert System:** 
  * Active **Buzzer Alarm** triggers globally upon any line failure or hazardous gas leakage.
  * **Dual Status LEDs** (Red/Green pairs) for immediate visual diagnostic per utility.
* 📺 **Dynamic LCD Display:** Alternates screen views between system operational status and real-time pH readings.

---

## 🔌 Pin Mapping & Hardware Setup

| Component | Pin Function | ESP32 GPIO | Description / Usage |
| :--- | :--- | :--- | :--- |
| **LCD 16x2** | RS, EN, D4, D5, D6, D7 | `GPIO 13, 12, 14, 27, 26, 25` | Display output |
| **Water Flow Sensor** | Pulse Input | `GPIO 18` | Interrupt-driven pulse counter |
| **Gas Flow Sensor** | Pulse Input | `GPIO 5` | Interrupt-driven pulse counter |
| **MQ Gas Sensor** | Analog Output | `GPIO 34` | Gas leak detection (Input-only pin) |
| **LDR Sensor** | Analog Output | `GPIO 35` | Crack/Light detection (Input-only pin) |
| **pH Sensor** | Analog Output | `GPIO 36` | Water pH calculation (Input-only pin) |
| **ACS712 Current** | Analog Output | `GPIO 32` | Electrical monitoring |
| **Manual Elec Switch**| Digital Input | `GPIO 15` | Fault simulation toggle switch |
| **Buzzer** | Output | `GPIO 2` | Active fault alarm |
| **Status LEDs** | Output (R1, G1 ... R4, G4) | `GPIO 17, 16, 23, 19, 21, 22, 4, 33` | Dual status indicator LEDs |

---

## 📊 Fault Logic & Thresholds

| Parameter | Sensor | Normal Condition | Fault Condition |
| :--- | :--- | :--- | :--- |
| **Water Line** | Water Flow Sensor | Flow $\ge$ 0.2 LPM | Flow < 0.2 LPM |
| **Gas Flow** | Gas Flow Sensor | Flow $\ge$ 0.2 LPM | Flow < 0.2 LPM |
| **Gas Leakage** | MQ Sensor | ADC Raw $\le$ 3000 | ADC Raw > 3000 |
| **Optical Pipe** | LDR Sensor | Light Value $\ge$ 1200 | Light Value < 1200 |
| **Electrical Line** | Digital Switch | Switch State = HIGH | Switch State = LOW |

---

##  Getting Started

### Prerequisites

1. **Arduino IDE:** Install the latest [Arduino IDE](https://www.arduino.cc/en/software).
2. **ESP32 Board Package:**
   * Open Arduino IDE $\rightarrow$ **Preferences** $\rightarrow$ Add to *Additional Boards Manager URLs*:
     `https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json`
   * Go to **Tools** $\rightarrow$ **Board** $\rightarrow$ **Boards Manager**, search for `esp32` by Espressif, and install it.
3. **Libraries:**
   * Install the built-in **LiquidCrystal** library (`#include <LiquidCrystal.h>`).

### Installation & Flashing

1. Clone this repository to your local computer:
   ```bash
   git clone [https://github.com/YOUR_USERNAME/ESP32-Multi-Pipe-Monitor.git](https://github.com/YOUR_USERNAME/ESP32-Multi-Pipe-Monitor.git)
