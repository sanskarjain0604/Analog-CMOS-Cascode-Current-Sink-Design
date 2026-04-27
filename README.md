# CMOS Cascode Current Sink Design

## Project Overview

This project involves the design and simulation of a CMOS cascode current sink capable of generating a stable reference current of **100 µA**.

The design is optimized to operate across three supply voltages (**1.2 V, 1.8 V, and 2.5 V**) using a **65 nm CMOS process**. This current sink is intended to serve as a bias stage for subsequent circuit blocks, ensuring robust operation under supply variations.

---

## Technical Specifications

- **Process Node:** 65 nm CMOS (Cadence Virtuoso)  
- **Reference Current ($I_{ref}$):** 100 µA  
- **Supply Voltages ($V_{DD}$):** 1.2 V, 1.8 V, 2.5 V  

### Transistor Models Used
- **2.5 V:** nsvt25, psvt25  
- **1.8 V:** nsvt18, psvt18  
- **1.2 V:** nlvtlp, plvtlp *(Low $V_t$ devices for headroom)*  

- **Target Region:** All transistors operate in **saturation (Region 2)**  

---

## Design Methodology

The design followed a structured approach:

### 1. Theoretical Estimation
Initial sizing was based on the square-law equation:

$$
I_D = \frac{1}{2} \mu C_{ox} \frac{W}{L} (V_{GS} - V_{th})^2
$$

### 2. Iterative Refinement
Device sizes ($W/L$) and resistor values ($R$) were tuned to ensure saturation across all conditions.

### 3. Headroom Management
Low threshold voltage ($V_t$) devices were used for the **1.2 V design** to maintain proper voltage stacking.

---

## Summary of Results

| $V_{DD}$ | Resistor ($R$) | $V_{out,min}$ | Output Resistance ($R_{out}$) |
|----------|---------------|--------------|------------------------------|
| 2.5 V    | 2 kΩ          | 0.3059 V     | 92 kΩ – 121 kΩ               |
| 1.8 V    | 1.85 kΩ       | 0.21 V       | 41 kΩ – 58 kΩ                |
| 1.2 V    | 1 kΩ          | 0.1487 V     | 12 kΩ – 16 kΩ                |

---

## Performance Analysis

### PVT Sensitivity

- The circuit exhibits **strong temperature sensitivity**  
- $V_{out,min}$ variation ranges from **±40% to 80%** across extreme temperatures (-40°C to 125°C)  
- Process corners (SS, FF) introduce variation, but **temperature is the dominant factor**

### Local Mismatch Analysis

Mismatch in critical devices (M11, M14) was analyzed:

- **2.5 V Supply:** Moderate sensitivity ($S \approx 2.4 - 5.0 \, V/V$)  
- **1.2 V Supply:** Sensitivity increases significantly due to limited headroom  

---

## Conclusion

The design successfully achieves a **stable 100 µA current** across multiple supply voltages.

- Low $V_t$ devices are essential for **1.2 V operation**
- However, they introduce **higher mismatch sensitivity**
- Temperature variation remains the primary limitation for precision performance
