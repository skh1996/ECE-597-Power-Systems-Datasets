# High-Fidelity Power Systems Datasets (ECE-597)

**Author:** Saad Khan | MS in Electrical Engineering, Illinois Institute of Technology  
**Course:** ECE-597 (Special Problems)

**Professor:** Mr. Ren Wang

## Overview
This repository serves as a curated library of high-quality, verified datasets for Data-Driven Power System applications. The focus is on three critical domains: **Transmission Dynamic Events (PMU/Faults)**, **Distribution Network Topology**, and **Non-Intrusive Load Monitoring (NILM)**. 

The datasets compiled here prioritize real-world grid conditions, verified simulation benchmarks, and include detailed statistics on sampling rates, class balance, and data quality.

---

## 1. Transmission Dynamic Events & PMU Data
**Focus:** Fault detection, oscillation monitoring, and grid stability using Phasor Measurement Units (PMU), SCADA logs, and high-resolution waveforms.

### Dataset Summary Table

| Dataset Name & Link | Data Type (Sampling) | Events / Labels | Verified Paper / Benchmark |
| :--- | :--- | :--- | :--- |
| **1. [VSB Power Line Fault Detection](https://www.kaggle.com/c/vsb-power-line-fault-detection)** | Waveforms (50 Hz) | Partial Discharge (PD) Precursors | *Howard et al., "VSB Power Line Fault Detection," 2018.* |
| **2. [UCI Electrical Grid Stability](https://archive.ics.uci.edu/dataset/471/electrical+grid+stability+simulated+data)** | Numerical (Simulated) | Stable vs. Unstable Grid States | *Arzamasov et al., "Towards Concise Models of Grid Stability," IEEE SmartGridComm 2018.* |
| **3. [EPFL Campus Grid PMU Data](https://infoscience.epfl.ch/record/228833)** | PMU (50 Hz) | Voltage Sags, Normal Operations | *Pignati et al., "Real-time State Estimation of the EPFL-Campus Grid," PSCC 2016.* |
| **4. [Electrical Line Fault Detection](https://figshare.com/articles/dataset/Dataset_for_Electrical_Line_Fault_Detection_Classification/30615710)** | Waveforms (High Res) | 11 Types (L-G, L-L, 3-Phase Faults) | *Standard IEEE Benchmark Dataset, Figshare 2023.* |
| **5. [IEEE 123-Node Fault Data](https://ieee-dataport.org/)** | Simulated SCADA/PMU | SLG, LL, LLG Fault Locations | *Dashtdar et al., "Fault Location in Radial Distribution Networks," 2022.* |
| **6. [LANL Open Source Grid Events](https://github.com/lanl-ansi/PowerModels.jl)** | Topology/Events | Contingencies, Line Outages | *Coffrin et al., "PowerModels.jl: Open-Source Framework," PSCC 2018.* |
| **7. [ORNL Transmission Signatures](https://www.ornl.gov/)** | PMU (60 Hz) | Frequency Events, Oscillations | *Bank et al., "Visualization of Wide-Area Frequency Measurement," IEEE PES 2010.* |
| **8. [Power System Faults (SCADA)](https://www.kaggle.com/datasets/ziya07/power-system-faults-dataset)** | SCADA Logs (1/min) | Line Break, Transformer Failure | *Applied ML Benchmark for Predictive Maintenance, Kaggle.* |

### Deep Dive: Dataset Statistics & Quality Analysis

#### A. VSB Power Line Fault Detection (Gold Standard)
* **Description:** Three-phase voltage measurements from medium-voltage overhead lines to detect Partial Discharge (PD).
* **Data Statistics:** High-frequency 20ms duration signals (800,000 measurements per signal). Highly Imbalanced (~95% Normal, ~5% Faults).
* **Quality Note:** Excellent benchmark for noise robustness; includes real-world background noise from the Czech Republic grid.

#### B. UCI Electrical Grid Stability
* **Description:** A mathematically rigorous simulated dataset representing a 4-node star architecture grid, predicting system stability after disturbances.
* **Data Statistics:** 12 inputs (Reaction time, Power, Price elasticity) with a Binary Stability Label (Stable/Unstable). 60,000 instances total.
* **Quality Note:** High fidelity. Data is generated using a differential equation solver, making it highly accurate for control theory applications.

#### C. EPFL Campus Grid PMU Data
* **Description:** Real-world Phasor Measurement Unit (PMU) data collected from a live university campus grid in Switzerland.
* **Data Statistics:** Standard European Grid Frequency (50 Hz). Features include Voltage Magnitude, Phase Angle, Frequency, and ROCOF.
* **Quality Note:** One of the rare publicly available *real-world* PMU datasets, excellent for validating algorithms without security redactions.

## 2. Distribution Network Topology & Loading
*(Data collection in progress...)*

---

## 3. Non-Intrusive Load Monitoring (NILM)
*(Data collection in progress...)*
