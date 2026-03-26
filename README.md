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
| **1. [VSB Power Line Fault Detection](01_Transmission_Faults.md)** | Waveforms (50 Hz) | Partial Discharge (PD) Precursors | *Howard et al., "VSB Power Line Fault Detection," 2018.* |
| **2. [UCI Electrical Grid Stability](01_Transmission_Faults.md)** | Numerical (Simulated) | Stable vs. Unstable Grid States | *Arzamasov et al., "Towards Concise Models of Grid Stability," IEEE 2018.* |
| **3. [EPFL Campus Grid PMU Data](01_Transmission_Faults.md)** | PMU (50 Hz) | Voltage Sags, Normal Operations | *Pignati et al., "Real-time State Estimation of the EPFL-Campus Grid," 2016.* |
| **4. [IEEE Test Cases Library — Forced/Sustained Power System Oscillations](https://github.com/skh1996/ECE-597-Power-Systems-Datasets/blob/main/01_Transmission_Faults.md)** | PMU (.txt/.csv) + PoW (.mat) | Forced Oscillations, Natural Mode Oscillations, Actual ISO-NE Events | *Wang et al., "Test Cases Library on Forced/Sustained Power System Oscillations," IEEE DataPort, DOI: 10.21227/a6hg-n822, 2025.* |
| **5. [IEEE 123-Node Fault Data](01_Transmission_Faults.md)** | Simulated SCADA/PMU | SLG, LL, LLG Fault Locations | *Dashtdar et al., "Fault Location in Radial Distribution Networks," 2022.* |
| **6. [HIL Cyber-Power Testbed PMU Data](01_Transmission_Faults.md)** | PMU (30 Hz) | Single/Multi-Phase Transmission Faults | *Mustafa et al., "Hardware-In-The-Loop Cyber-Power Testbed," IEEE.* |
| **7. [ORNL Transmission Signatures](01_Transmission_Faults.md)** | PMU (60 Hz) | Frequency Events, Oscillations | *Bank et al., "Visualization of Wide-Area Frequency Measurement," 2010.* |
| **8. [BPA PMU Line Event Dataset](01_Transmission_Faults.md)** | PMU Streams | L-G, L-L Transmission Fault Signatures | *"Smart grid line event classification using supervised learning over PMU data streams," IEEE IGSC 2015.* |
---

## 2. Distribution Network Topology & Loading
*(Data collection in progress...)*

---

## 3. Non-Intrusive Load Monitoring (NILM)
*(Data collection in progress...)*
