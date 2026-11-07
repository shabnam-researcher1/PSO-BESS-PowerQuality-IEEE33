# Optimal Location and Sizing of Battery Energy Storage System (BESS) for Power Quality Improvement

This repository contains the simulation models, optimization framework, and complete analysis for evaluating the optimal sizing, placement, and operation of Battery Energy Storage Systems (BESS) in distribution feeders to improve power quality, mitigate voltage fluctuations, and minimize system losses.

---

## 📌 Project Overview

Modern electrical distribution systems face operational challenges such as severe voltage drops and high power losses, particularly in long radial feeders under peak demand conditions. This project implements a **Particle Swarm Optimization (PSO)** algorithm integrated with **OpenDSS** and **Python** to determine the optimal allocation and capacity of BESS units using the benchmark **IEEE 33-Bus Radial Distribution Network**.

### Key Highlights
* **Co-Simulation Framework**: Built using **Python** (`py_dss_interface`, `PuLP`, `pandas`) interfaced with **OpenDSS** for rigorous 24-hour time-series power flow analysis.
* **Distribution Load Flow**: Employs the **BIBC/BCBV (Bus Injection to Branch Current / Branch Current to Bus Voltage)** matrix formulation for fast and accurate power flow computations.
* **Peak-Shaving Strategy**: Automated operational scheduling where BESS charges during off-peak hours ($00:00 - 07:00$) and discharges during peak hours ($15:00 - 21:00$).
* **Reactive Power Support**: Active inverter control providing dynamic reactive power ($Q$) support throughout the 24-hour operating cycle.

---

## 📐 System Specifications & Optimization Setup

### Test Network
* **System**: Standard IEEE 33-Bus Radial Distribution Feeder
* **Base Voltage**: $13.8\text{ kV}$
* **Base Case Losses**: $5035.29\text{ kWh/day}$
* **Base Case Voltage Minimum**: $0.9004\text{ p.u.}$ (violates standard $0.95\text{ p.u.}$ lower limit)

### Optimization Formulation
* **Objective Function**: Minimize daily total active power losses ($P_{\text{loss}}$) and overall annual operational costs.
* **Operational Constraints**:
  * Voltage limits: $0.95\text{ p.u.} \le V_i(t) \le 1.05\text{ p.u.}$
  * Battery State of Charge: $SOC_{\min} \le SOC(t) \le SOC_{\max}$
  * Line thermal limits: $I_{ij} / I_{\text{max}} < 1.0$
  * Inverter apparent power rating: $S_{\text{inv}} \ge 1.2 P_{\text{rated}}$
  * Daily cycling limit: $\le 1\text{ cycle/day}$

---

## 📊 Comparative Performance Results

The framework evaluates five operational scenarios, ranging from the base network configuration up to four optimally placed BESS units:

| Parameter | Base Case (No BESS) | 1 BESS Unit | 2 BESS Units | 3 BESS Units | 4 BESS Units |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Optimal Bus Location(s)** | — | **Bus 16** | **Buses 32, 16** | **Buses 16, 31, 33** | **Buses 16, 12, 31, 33** |
| **Total Daily Loss (kWh/day)** | 5035.29 | 4140.09 | 3201.45 | **3199.19** | 3596.50 |
| **Minimum Voltage ($V_{\min}$, p.u.)** | 0.9004 | 0.9139 | 0.9383 | 0.9462 | **0.9500** |
| **Peak Branch Loading (p.u.)** | 0.8493 | 0.7649 | 0.7162 | **0.7002** | 0.7414 |
| **Loss Reduction (%)** | — | 17.77% | **36.41%** | **36.46%** | 28.57% |
| **Payback Period (Years)** | — | **0.98** | 1.03 | 1.94 | 1.56 |

### Summary of Findings
1. **Best Technical & Economic Balance**: The **2 BESS configuration (Buses 16 & 32)** offers the optimal trade-off, achieving a **36.41% reduction in power losses** with a short payback period of **1.03 years**.
2. **Maximum Loss Reduction**: The **3 BESS configuration** yields the highest energy loss reduction (**36.46%**), raising $V_{\min}$ to $0.9462\text{ p.u.}$, but requires a longer payback period of **1.94 years**.
3. **Diminishing Returns**: Expanding to **4 BESS units** increases daily losses to $3596.50\text{ kWh/day}$ due to excessive cumulative charging overhead.

---

## 🛠️ Software Requirements & Tech Stack

* **Programming Language**: Python 3.x
* **Simulation Engine**: OpenDSS (Electric Power Research Institute)
* **Python Libraries**: `py_dss_interface`, `PuLP`, `pandas`, `matplotlib`, `numpy`
* **Diagramming & Analysis**: Draw.io, Microsoft Excel

---

## 👥 Authors & Acknowledgments

**Project Team:**
* **Nabin Kumar Rajbanshi** (ACE078BEL006)
* **Pratiksha Paneru** (ACE078BEL010)
* **Shabnam Praween** (ACE078BEL016)

**Supervision:**
* **Er. Awnish Kumar Thakur** (Supervisor)
* **Er. Rabin Shrestha** (Deputy Head of Department)

*Department of Electrical Engineering, Advanced College of Engineering and Management (ACEM), Tribhuvan University, Institute of Engineering (IOE), Balkhu, Kathmandu, Nepal.*
