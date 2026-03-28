# High-Fidelity Power Systems Datasets (ECE-597)

**Author:** Saad Khan | MS in Electrical Engineering, Illinois Institute of Technology  
**Course:** ECE-597 (Special Problems)  

## Overview
This repository serves as a curated library of high-quality, verified datasets for Data-Driven Power System applications. The focus is on three critical domains: **Transmission Dynamic Events (PMU/Faults)**, **Distribution Network Topology**, and **Non-Intrusive Load Monitoring (NILM)**. 

The datasets compiled here prioritize real-world grid conditions and verified simulation benchmarks, and they include detailed statistics on sampling rates, class balance, and data schemas.

---

## 1. Transmission Dynamic Events & PMU Data
**Focus:** Fault detection, oscillation monitoring, and grid stability using Phasor Measurement Units (PMU), SCADA logs, and high-resolution waveforms. All datasets exclude device-level maintenance data and are grounded in verified, peer-reviewed publications or official industry benchmarks.

> 💡 **NAVIGATION TIP:** Click on any dataset name below to view detailed statistics, data schemas, and direct download links.

| Dataset Name | Data Type (Sampling) | Events / Labels | Verified Paper / Benchmark |
| :--- | :--- | :--- | :--- |
| **1. [UCI Electrical Grid Stability](01_Transmission_Faults.md)** | Numerical (Simulated) | Stable vs. Unstable Grid States | *Arzamasov et al., "Towards Concise Models of Grid Stability," IEEE 2018.* |
| **2. [EPFL Campus Grid PMU Data](01_Transmission_Faults.md)** | PMU (50 Hz) | Voltage Sags, Normal Operations | *Pignati et al., "Real-time State Estimation of the EPFL-Campus Grid," 2016.* |
| **3. [IEEE Test Cases Library — Forced/Sustained Power System Oscillations](https://github.com/skh1996/ECE-597-Power-Systems-Datasets/blob/main/01_Transmission_Faults.md)** | PMU (.txt/.csv) + PoW (.mat) | Forced Oscillations, Natural Mode Oscillations, Actual ISO-NE Events | *Wang et al., "Test Cases Library on Forced/Sustained Power System Oscillations," IEEE DataPort, DOI: 10.21227/a6hg-n822, 2025.* |
| **4. [PSML: Multi-Scale T+D PMU Disturbance Dataset](01_Transmission_Faults.md)** | PMU Waveforms (ms-resolution, 91 channels) | Transmission Faults, Generator Trips, Natural Oscillations | *Zheng et al., "A Multi-Scale Time-Series Dataset with Benchmark for ML in Decarbonized Energy Grids," Nature Scientific Data, 2022.* |
| **5. [HIL Cyber-Power Testbed PMU Data](01_Transmission_Faults.md)** | PMU CSV (30 Hz, 14 vars/PMU, 26 buses) | Generator Trips, Load Events, Line Outages, Fault Events | *Hussain et al., "High-Fidelity Synchrophasor Dataset from a Real-Time HIL Testbed for State Estimation and Event Analysis," IEEE DataPort, DOI: 10.21227/0mp1-fe58, 2025.* |
| **6. [ORNL Grid Event Signature Library (GESL)](01_Transmission_Faults.md)** | Real PMU + PoW Waveforms (30–60 Hz) | Generator Trips, Forced Oscillations, Frequency Events, Faults | *Wilson et al., "The Grid Event Signature Library: An Open-Access Repository of Power System Measurement Signatures," IEEE Access, DOI: 10.1109/ACCESS.2024.3404886, 2024.* |
| **7. [IRTSD: IBR-Rich Transmission System Disturbance Dataset](01_Transmission_Faults.md)** | EMT-PMU CSV (0.5 Hz–4 kHz, 5,500 events) | Faults, Forced Oscillations, Generator Trips, IBR Malfunctions | *Ross & Mahapatra, "IRTSD: Open-Source Data and Toolset for Electromagnetic Transient Analysis of Disturbances and IBR Control Malfunctions in Transmission Systems," IEEE DataPort, DOI: 10.21227/mp6d-j677, 2024.* |
| **8. [VSB Power Line Fault Detection](01_Transmission_Faults.md)** | Waveforms (50 Hz) | Partial Discharge (PD) Precursors | *Howard et al., "VSB Power Line Fault Detection," 2018.* |

## 2. Distribution Network Topology & Loading
*(Data collection in progress...)*

---

## 3. Non-Intrusive Load Monitoring (NILM)
*(Data collection in progress...)*
