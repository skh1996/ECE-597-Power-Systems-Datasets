# High-Fidelity Power Systems Datasets (ECE-597)

**Author:** Saad Khan | MS in Electrical Engineering, Illinois Institute of Technology  
**Course:** ECE-597 (Special Problems)  

## Overview
This repository serves as a curated library of high-quality, verified datasets for Data-Driven Power System applications. The focus is on three critical domains: **Transmission Dynamic Events (PMU/Faults)**, **Distribution Network Topology**, and **Non-Intrusive Load Monitoring (NILM)**. 

The datasets compiled here prioritize real-world grid conditions, verified simulation benchmarks, and include detailed statistics on sampling rates, class balance, and data schemas.

---

## 1. Transmission Dynamic Events & PMU Data
**Focus:** Fault detection, oscillation monitoring, and grid stability using Phasor Measurement Units (PMU), SCADA logs, and high-resolution waveforms.

*(Click on any dataset name to view detailed statistics, data schemas, and download links).*

| Dataset Name | Data Type (Sampling) | Events / Labels | Verified Paper / Benchmark |
| :--- | :--- | :--- | :--- |
| **1. [VSB Power Line Fault Detection](01_Transmission_Faults.md)** | Waveforms (50 Hz) | Partial Discharge (PD) Precursors | *Howard et al., 2018.* |
| **2. [UCI Electrical Grid Stability](01_Transmission_Faults.md)** | Numerical (Simulated) | Stable vs. Unstable Grid States | *Arzamasov et al., 2018.* |
| **3. [EPFL Campus Grid PMU Data](01_Transmission_Faults.md)** | PMU (50 Hz) | Voltage Sags, Normal Operations | *Pignati et al., 2016.* |
| **4. [Electrical Line Fault Detection](01_Transmission_Faults.md)** | Waveforms (High Res) | 11 Types (L-G, L-L, 3-Phase Faults) | *IEEE Benchmark Dataset, 2023.* |
| **5. [IEEE 123-Node Fault Data](01_Transmission_Faults.md)** | Simulated SCADA/PMU | SLG, LL, LLG Fault Locations | *Dashtdar et al., 2022.* |
| **6. [LANL Open Source Grid Events](01_Transmission_Faults.md)** | Topology/Events | Contingencies, Line Outages | *Coffrin et al., 2018.* |
| **7. [ORNL Transmission Signatures](01_Transmission_Faults.md)** | PMU (60 Hz) | Frequency Events, Oscillations | *Bank et al., 2010.* |
| **8. [Power System Faults (SCADA)](01_Transmission_Faults.md)** | SCADA Logs (1/min) | Line Break, Transformer Failure | *Applied ML Benchmark, Kaggle.* |

---

## 2. Distribution Network Topology & Loading
*(Data collection in progress...)*

---

## 3. Non-Intrusive Load Monitoring (NILM)
*(Data collection in progress...)*
