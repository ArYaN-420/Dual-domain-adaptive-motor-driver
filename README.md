# Dual Domain Adaptive Motor Driver (KERS-Enabled)
[cite_start]**An Intelligent Energy Aware Power Management System for Autonomous Robots** [cite: 23]

## 📌 Project Overview
[cite_start]This project presents a high-performance, discrete MOSFET motor driver prototype specifically designed for Line Follower Robots (LFR) and autonomous rovers[cite: 24]. [cite_start]Unlike standard driver ICs, this system implements a **Dual-Domain Arbitration Logic** that dynamically transitions between **Voltage-Regulated Speed Control** and **Current-Limited Torque Control** based on real-time load feedback and harvested energy levels[cite: 25].

[cite_start]The architecture integrates a **Passive Kinetic Energy Recovery System (KERS)**, utilizing Back-EMF to charge a $4700\mu F$ energy buffer, enabling a F1-style "Overtake" mode for temporary high-performance bursts[cite: 26].

---

## 🚀 Key Features
* [cite_start]**Discrete H-Bridge Design:** Engineered using IRLZ44N (Low-side) and IRF9540 (High-side) MOSFETs for maximum efficiency and custom gate-drive control[cite: 27].
* [cite_start]**Dual-Domain Arbitration:** Intelligent firmware logic that monitors current spikes and switches control domains to prevent stalling while optimizing speed[cite: 28].
* [cite_start]**Passive KERS:** Utilizes Back-EMF harvesting into a $4700\mu F$ capacitor buffer to stabilize power rails and store energy credits[cite: 29].
* [cite_start]**Energy Aware "Overtake" Mode:** Authorizes temporary high-torque bursts only when sufficient "Energy Credits" are stored in the capacitor[cite: 30].
* [cite_start]**Industrial-Grade Safety:** Integrated 20µs hardware/software dead-time to prevent shoot-through and 300–500ms stall protection[cite: 31].

---

## 🛠 Hardware Architecture
[cite_start]The system utilizes a low-side shunt resistor ($0.1\Omega$) amplified by an LM358 Op-Amp to provide high-resolution current feedback to the microcontroller[cite: 32].

### Component Specifications
| Component | Function | Technical Justification |
| :--- | :--- | :--- |
| **IRLZ44N** | Low-side Switch | [cite_start]Logic-level N-Channel MOSFET for direct MCU triggering[cite: 34]. |
| **IRF9540** | High-side Switch | [cite_start]P-Channel MOSFET driven by 2N2222 NPN transistors to ensure full turn-off at $V_{bat} > 5V$[cite: 35]. |
| **LM358** | Signal Conditioning | [cite_start]Discrete Op-Amp for current-to-voltage translation with custom gain[cite: 36]. |
| **4700µF Cap** | Energy Storage | [cite_start]High-capacity buffer for rail stabilization and Back-EMF harvesting[cite: 37]. |
| **1N5822** | Recovery Diode | [cite_start]High-speed Schottky diode for efficient energy capture and flyback protection[cite: 38]. |

---

## 🧠 Control Logic & Mathematics
The "Dual-Domain" core relies on an **Arbitration Threshold**. [cite_start]When motor current ($I$) exceeds the threshold, the system enters a Current-Loop to maintain torque[cite: 40].

### Signal Amplification
[cite_start]The LM358 gain is calculated to maximize ADC resolution without exceeding the 3.5V output swing limit[cite: 41]: 
$$V_{out} = V_{shunt} \times (1 + \frac{R_f}{R_{in}})$$

### Energy Storage
[cite_start]Harvested energy in the $4700\mu F$ "tank" is quantified to authorize "Boost Mode"[cite: 42]: 
$$E = 0.5 \times C \times V^2$$

### Transfer Function
[cite_start]The system models PWM effects under varying loads using the following transfer function[cite: 42]: 
$$G(s) = \frac{K}{(Js+b)(Ls+R) + K^2}$$

---


---

## ⚖ License & Intellectual Property
[cite_start]This project is developed with a **Patent-Pending** mindset, specifically regarding the "Energy-Credit-Limit" arbitration algorithm used for autonomous race logic[cite: 48]. [cite_start]All rights reserved for the unique software switching surface logic[cite: 49].
