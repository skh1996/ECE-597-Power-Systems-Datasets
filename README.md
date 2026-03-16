# High-Fidelity Power Systems Datasets (ECE-597)

**Author:** Saad Khan | MS in Electrical Engineering, Illinois Institute of Technology  
**Course:** ECE-597 (Special Problems)  

## Overview
This repository serves as a curated library of high-quality, verified datasets for Data-Driven Power System applications. The focus is on three critical domains: **Transmission Dynamic Events (PMU/Faults)**, **Distribution Network Topology**, and **Non-Intrusive Load Monitoring (NILM)**. 

The datasets compiled here prioritize real-world grid conditions, verified simulation benchmarks, and include detailed statistics on sampling rates, class balance, and data quality.

---

## 1. Powerline Fault Detection / Transmission Dynamic Events & PMU Data
**Focus:** Fault detection, oscillation monitoring, and grid stability using Phasor Measurement Units (PMU) and high-resolution waveforms.

### Dataset Summary Table

| Dataset Name | Data Type | Sampling | Events / Labels | Quality / Source |
| :--- | :--- | :--- | :--- | :--- |
| **1. VSB Power Line Fault Detection** | Waveforms | 50 Hz | Partial Discharge (PD) | **High** (Kaggle/VSB Univ) |
| **2. Electrical Line Fault Detection** | Waveforms | High Res | 11 Fault Types (L-G, L-L, 3-Phase) | **High** (Figshare) |
| **3. Mendeley PMU Labeled Data** | PMU | 50 Hz | SLG, LL, LLG Faults | **Medium** (Simulated) |
| **4. Power System Faults (SCADA)** | SCADA | 1/min | Line Break, Transformer Failure | **Medium** (Kaggle) |
| **5. UCI Grid Stability Simulation** | Numerical | N/A | Stable vs. Unstable | **High** (UCI Repo) |
| **6. ORNL Transmission Signatures** | PMU | 60 Hz | Frequency Events, Oscillations | **Very High** (DOE/ORNL) |
| **7. EPFL Campus Grid PMU Data** | PMU | 50 Hz | Voltage Sags, Normal Ops | **High** (Real-World) |
| **8. Power Quality Fault Dataset** | Waveforms | High Res | Sags, Swells, Harmonics | **High** (Kaggle) |

### Deep Dive: Dataset Statistics & Quality Analysis

#### A. VSB Power Line Fault Detection (Gold Standard)
* **Description:** Three-phase voltage measurements from medium-voltage overhead lines to detect Partial Discharge (PD), a precursor to grid failure.
* **Citation:** Howard et al., "VSB Power Line Fault Detection," 2018.
* **Data Statistics:**
  * **Sampling Rate:** High-frequency (20ms duration signals).
  * **Resolution:** 800,000 measurements per signal.
  * **Class Balance:** Highly Imbalanced (~95% Normal, ~5% Faults).
* **Quality Note:** Excellent benchmark for noise robustness, as it includes real-world background noise from the Czech Republic grid.

#### B. UCI Electrical Grid Stability
* **Description:** A mathematically rigorous simulated dataset representing a 4-node star architecture grid, predicting system stability after disturbances.
* **Citation:** Arzamasov, V. et al., "Towards Concise Models of Grid Stability," IEEE SmartGridComm 2018.
* **Data Statistics:**
  * **Features:** 12 inputs (Reaction time, Power, Price elasticity).
  * **Target:** Binary Stability Label (Stable/Unstable).
  * **Size:** 60,000 instances (Numerical CSV).
* **Quality Note:** High fidelity. Data is generated using a differential equation solver, making it highly accurate for control theory applications.

#### C. EPFL Campus Grid PMU Data
* **Description:** Real-world Phasor Measurement Unit (PMU) data collected from a live university campus grid in Switzerland.
* **Citation:** Pignati et al., "Real-time State Estimation of the EPFL-Campus Grid," PSCC 2016.
* **Data Statistics:**
  * **Sampling Rate:** 50 Hz (Standard European Grid Frequency).
  * **Parameters:** Voltage Magnitude, Phase Angle, Frequency, ROCOF.
* **Quality Note:** One of the few publicly available real-world PMU datasets, excellent for validating state estimation algorithms without security redactions.

---

## 2. Distribution Network Topology & Loading
*(Data collection in progress...)*

---

## 3. Non-Intrusive Load Monitoring (NILM)
*(Data collection in progress...)*
