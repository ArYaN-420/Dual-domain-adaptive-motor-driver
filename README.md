# Dual Domain Adaptive Motor Driver (KERS-Enabled)
**An Intelligent Energy Aware Power Management System for Autonomous Robots** 

## 📌 Project Overview
This project presents a high-performance, discrete MOSFET motor driver prototype specifically designed for Line Follower Robots (LFR) and autonomous rovers.
Unlike standard driver ICs, this system implements a **Dual-Domain Arbitration Logic** that dynamically transitions between **Voltage-Regulated Speed Control** and **Current-Limited Torque Control** based on real-time load feedback and harvested energy levels.

The architecture integrates a **Passive Kinetic Energy Recovery System (KERS)**, utilizing Back-EMF to charge a $4700\mu F$ energy buffer, enabling a F1-style "Overtake" mode for temporary high-performance bursts.

---

## 🚀 Key Features
* **Discrete H-Bridge Design:** Engineered using IRLZ44N (Low-side) and IRF9540 (High-side) MOSFETs for maximum efficiency and custom gate-drive control.
* **Dual-Domain Arbitration:** Intelligent firmware logic that monitors current spikes and switches control domains to prevent stalling while optimizing speed.
* **Passive KERS:** Utilizes Back-EMF harvesting into a $4700\mu F$ capacitor buffer to stabilize power rails and store energy credits.
* **Energy Aware "Overtake" Mode:** Authorizes temporary high-torque bursts only when sufficient "Energy Credits" are stored in the capacitor.
* **Industrial-Grade Safety:** Integrated 20µs hardware/software dead-time to prevent shoot-through and 300–500ms stall protection.

---

## 🛠 Hardware Architecture
The system utilizes a low-side shunt resistor ($0.1\Omega$) amplified by an LM358 Op-Amp to provide high-resolution current feedback to the microcontroller.

### Component Specifications
| Component | Function | Technical Justification |
| :--- | :--- | :--- |
| **IRLZ44N** | Low-side Switch | Logic-level N-Channel MOSFET for direct MCU triggering. |
| **IRF9540** | High-side Switch | P-Channel MOSFET driven by 2N2222 NPN transistors to ensure full turn-off at $V_{bat} > 5V$. |
| **LM358** | Signal Conditioning | Discrete Op-Amp for current-to-voltage translation with custom gain. |
| **4700µF Cap** | Energy Storage | High-capacity buffer for rail stabilization and Back-EMF harvesting. |
| **1N5822** | Recovery Diode | High-speed Schottky diode for efficient energy capture and flyback protection. |

---

## 🧠 Control Logic & Mathematics
The "Dual-Domain" core relies on an **Arbitration Threshold**. When motor current ($I$) exceeds the threshold, the system enters a Current-Loop to maintain torque\.

### Signal Amplification
The LM358 gain is calculated to maximize ADC resolution without exceeding the 3.5V output swing limit: 
$$V_{out} = V_{shunt} \times (1 + \frac{R_f}{R_{in}})$$

### Energy Storage
Harvested energy in the $4700\mu F$ "tank" is quantified to authorize "Boost Mode": 
$$E = 0.5 \times C \times V^2$$

### Transfer Function
The system models PWM effects under varying loads using the following transfer function: 
$$G(s) = \frac{K}{(Js+b)(Ls+R) + K^2}$$

---


---

