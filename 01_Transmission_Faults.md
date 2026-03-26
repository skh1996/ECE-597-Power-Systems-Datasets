# Topic 1: Transmission Dynamic Events & PMU Data

## Overview
This document contains the detailed data statistics, structural schemas, and direct download sources for the datasets categorized under Power Line Fault Detection, Transmission Dynamics, and PMU (Phasor Measurement Unit) data. 

As per project requirements, the datasets below strictly focus on transmission and high-level distribution network faults to ensure a comprehensive overview of grid anomalies, entirely excluding device-level and maintenance logs. All datasets are grounded in verified, peer-reviewed publications or official industry benchmarks.

---

### 1. VSB Power Line Fault Detection
* **Description:** Three-phase voltage measurements from medium-voltage overhead lines to detect Partial Discharge (PD), a critical precursor to catastrophic grid failure.
* **Download Link:** [Kaggle - VSB Power Line Fault Detection](https://www.kaggle.com/c/vsb-power-line-fault-detection/data)
* **Data Statistics:** High-frequency 20ms duration signals (800,000 measurements per signal). 8,712 total signals. Highly Imbalanced (~95% Normal, ~5% Faults).
* **What the Data Sample Looks Like:** A `.parquet` file containing continuous numeric arrays mapped to a binary target.
* **Visual Sample (First 2 Rows):**

| signal_id | phase_0 (V) | phase_1 (V) | phase_2 (V) | target |
| :--- | :--- | :--- | :--- | :--- |
| 0 | 18 | -16 | -5 | 0 |
| 1 | 17 | -17 | -6 | 1 |


### 2. UCI Electrical Grid Stability
* **Description:** A mathematically rigorous simulated dataset representing a 4-node star architecture grid, predicting system stability after control disturbances.
* **Download Link:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/471/electrical+grid+stability+simulated+data)
* **Data Statistics:** 60,000 instances total. 12 input features and 1 predictive target.
* **What the Data Sample Looks Like:** A standard `.csv` file detailing reaction times (`tau`), power balance (`p`), and the categorical stability label (`stabf`).
* **Visual Sample (First 2 Rows):**

| tau1 | tau2 | p1 | p2 | g1 | stabf |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2.959 | 3.079 | 3.763 | -1.221 | 0.650 | unstable |
| 9.304 | 4.902 | 2.009 | -1.469 | 0.859 | stable |


### 3. EPFL Campus Grid PMU Data
* **Description:** Real-world Phasor Measurement Unit (PMU) data collected from a live university campus grid in Switzerland during normal and anomalous operations.
* **Download Link:** [EPFL Infoscience Repository](https://github.com/DESL-EPFL/Point-on-wave-Data-of-EPFL-campus-Distribution-Network/tree/master)
* **Data Statistics:** Standard European Grid Frequency (50 Hz). Multi-day continuous logging. 
* **What the Data Sample Looks Like:** Time-series `.csv` files containing high-resolution synchrophasor measurements.
* **Visual Sample (First 2 Rows):**

| Timestamp | Voltage_Mag_kV | Phase_Angle_rad | Frequency_Hz | ROCOF |
| :--- | :--- | :--- | :--- | :--- |
| 1459451121.00 | 20.124 | 0.451 | 49.981 | -0.012 |
| 1459451121.02 | 20.122 | 0.453 | 49.978 | -0.015 |


### 4. IEEE Test Cases Library — Forced/Sustained Power System Oscillations

- **Description:** A comprehensive benchmark library of PMU and Point-on-Wave (PoW) data for power system oscillation source location. Includes simulated forced and natural mode oscillation cases on the WECC 179-bus and WECC 240-bus systems, 6 actual oscillatory event recordings from ISO New England, and a new PoW dataset on a 14-bus inverter-based system. Developed by ISO New England and the University of Tennessee, Knoxville, and used as the official dataset for the 2021 IEEE-NASPI Oscillation Source Location Contest.
- **Download Link:** [IEEE DataPort — Test Cases Library on Forced/Sustained Power System Oscillations](https://ieee-dataport.org/documents/test-cases-library-forcedsustained-power-system-oscillations)
- **Data Statistics:** PMU data sampled at 30 Hz (WECC 179-bus: 18 forced oscillation + 9 natural mode cases; WECC 240-bus: 13 forced oscillation cases; ISO New England: 6 real-world events). PoW data on a 14-bus system: 6 forced + 5 natural mode cases. Total download size: ~540 MB across four archives.
- **Data Formats:** `.txt` and `.csv` for PMU data; `.mat` for PoW data; simulation model files in `.raw`, `.dyr`, `.pfb`, `.dat` formats (compatible with Powertech DSATools/TSAT and PSS/E).
- **What the Data Sample Looks Like:** Each PMU case folder contains separate `.txt` files for bus voltage magnitudes (`BusVolMag`), bus voltage angles (`BusVolAng`), line current magnitudes (`LinCurMag`), and line current angles (`LinCurAng`), plus rotor speed and angle for generator buses. ISO-NE real-world cases are provided as `.csv` files.
- **Visual Sample (Illustrative Schema):**

| Time_s | BusVolMag (pu) | BusVolAng (deg) | LinCurMag (pu) | LinCurAng (deg) | RotorSpd (pu) |
| --- | --- | --- | --- | --- | --- |
| 0.000 | 1.024 | -14.82 | 0.412 | -22.10 | 1.000 |
| 0.033 | 1.021 | -15.10 | 0.431 | -23.40 | 0.999 |

- **Citation:** Bin Wang, Slava Maslennikov, Kai Sun, Pablo Gill Estevez, *"Test Cases Library on Forced/Sustained Power System Oscillations"*, IEEE DataPort, 2025. DOI: [10.21227/a6hg-n822](https://dx.doi.org/10.21227/a6hg-n822)


### 5. PSML: Multi-Scale Transmission + Distribution PMU Disturbance Dataset

- **Description:** A first-of-its-kind open-access multi-scale PMU time-series dataset generated through a novel joint Transmission + Distribution (T+D) co-simulation platform (PSS/E 23-bus transmission + two IEEE 13-bus distribution systems via OpenDSS). Contains millisecond-resolution voltage, current, and power measurements across transmission buses during labeled dynamic disturbance events — including short-circuit faults, generator trips, load changes, and natural oscillations. Developed by Texas A&M University, USC, MIT, and Purdue University. Published in *Nature Scientific Data* (2022).
- **Download Link:** [Zenodo — PSML Dataset (DOI: 10.5281/zenodo.5130612)](https://zenodo.org/record/5130612)
> GitHub (Code + benchmarks): [tamu-engineering-research/Open-source-power-dataset](https://github.com/tamu-engineering-research/Open-source-power-dataset)
- **Data Statistics:**
  - Millisecond-resolution PMU streams: **960 time steps × 91 channels** per scenario (voltage magnitude, voltage phase angle, current magnitude, current phase angle, real power, reactive power, frequency)
  - Disturbance types: short-circuit faults, generator trips, load disturbances, natural oscillations — each with labeled `info.csv` (start time, end time, location, type)
  - Minute-resolution load + renewable data: 66 U.S. load zones, 2018–2020 (3 years)
- **Data Format:** `.csv` files organized per disturbance scenario:
  - `trans.csv` — Transmission bus voltages and branch power flows (millisecond resolution)
  - `dist.csv` — Three-phase distribution node voltages (millisecond resolution)
  - `info.csv` — Disturbance metadata: type, start/end time, source location
- **What the Data Sample Looks Like:** Each disturbance scenario folder contains three `.csv` files. The transmission file (`trans.csv`) has millisecond timestamps with per-unit voltage at each bus and active/reactive power on each branch.
- **Visual Sample (Illustrative Schema — `trans.csv`):**

| Time(s) | VOLT\_151 (pu) | VOLT\_152 (pu) | POWR\_151\_TO\_152 (pu) | VARS\_151\_TO\_152 (pu) | Disturbance\_Type |
| --- | --- | --- | --- | --- | --- |
| 0.0000 | 1.023 | 1.019 | 0.412 | 0.087 | Normal |
| 0.0167 | 0.651 | 0.704 | 1.823 | 0.541 | Short\_Circuit\_Fault |

- **Citation:** Zheng, X., Xu, N., Trinh, L., Wu, D., Huang, T., Sivaranjani, S., Liu, Y., & Xie, L. (2022). *A multi-scale time-series dataset with benchmark for machine learning in decarbonized energy grids.* Nature Scientific Data, 9, 359. DOI: [10.1038/s41597-022-01455-7](https://doi.org/10.1038/s41597-022-01455-7)


### 6. HIL Cyber-Power Testbed PMU Data — IEEE 39-Bus

- **Description:** High-fidelity synchrophasor recordings from a real-time Hardware-in-the-Loop (HIL) testbed built on the IEEE 39-bus transmission system with 26 optimally placed PMUs. Integrates RTDS, hardware PMUs, RTAC, and ns-3 network emulation to reproduce realistic grid dynamics including communication delays. Covers generator trips, load shedding, line outages, and fault events. Developed at West Virginia University (NSF-funded).
- **Download Link:** [IEEE DataPort — High-Fidelity Synchrophasor Dataset from a Real-Time HIL Testbed](https://ieee-dataport.org/documents/high-fidelity-synchrophasor-dataset-real-time-hil-testbed-state-estimation-and-event)
  > Free IEEE account required. DOI: [10.21227/0mp1-fe58](https://dx.doi.org/10.21227/0mp1-fe58)

- **Data Statistics:** 26 PMU buses on the IEEE 39-bus system. 14 variables per timestamp: three-phase voltage/current magnitudes and angles, frequency, and ROCOF. IEEE C37.118 compliant, GPS-synchronized. Pre-split into Training/Testing folders, one `.csv` per PMU. Total size: ~315 MB.
- **What the Data Sample Looks Like:** Individual `.csv` files per PMU (e.g., `PMU51.csv` through `PMU74.csv`, `SEL401.csv`, `SEL451.csv`), each containing 14 electrical measurement columns with an event label per row.
- **Visual Sample (Illustrative Schema):**

| Timestamp | Va_mag (pu) | Va_ang (deg) | Ia_mag (pu) | Ia_ang (deg) | Freq_Hz | ROCOF | Event_Label |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1.100 | 1.042 | -8.50 | 0.512 | -15.20 | 60.001 | 0.000 | Normal |
| 1.133 | 0.651 | -12.10 | 4.850 | -45.60 | 59.980 | -0.042 | Fault_Event |

- **Citation:** M. Mustafa Hussain, Purna Kukadiya, Anurag Srivastava, *"High-Fidelity Synchrophasor Dataset from a Real-Time HIL Testbed for State Estimation and Event Analysis,"* IEEE DataPort, December 2025. DOI: [10.21227/0mp1-fe58](https://dx.doi.org/10.21227/0mp1-fe58)


### 7. ORNL Grid Event Signature Library (GESL) — Transmission Signature Library

- **Description:** A large open-source repository of real transmission-level PMU data, developed by ORNL and LLNL under the DOE Office of Electricity. It includes 1,694 labeled transmission events and 2,500+ total PMU and Point-on-Wave signatures collected from U.S. utilities across two interconnections. Events cover generator trips, oscillations, faults, frequency disturbances, and line trips, all anonymized and consistently labeled.

- - **Download Link:** [ORNL Grid Event Signature Library (GESL)](https://gesl.ornl.gov)
  > ⚠️ Free account required (valid email only). Data accessible via web Dashboard or Python API. 
  
- **Data Statistics:**  
  1,694 unique labeled transmission PMU events. PMU data at 30–60 Hz reporting rate; PoW data at higher resolution. Data spans two U.S. interconnections, multiple utility providers, and diverse instrument configurations. Uniform event taxonomy applied across Primary, Class, and Sub-Class label levels.

- **What the Data Sample Looks Like:**  
  Each event record is a `.csv` file containing time-series synchrophasor measurements (voltage magnitude, voltage angle, current magnitude, current angle, frequency, ROCOF) from one or more PMUs, along with an event tag and metadata file.

- **Visual Sample (Illustrative Schema):**

| Timestamp              | V_mag (pu) | V_ang (deg) | Freq_Hz | ROCOF  | Event_Tag      |
|------------------------|------------|--------------|---------|--------|----------------|
| 2021-08-14 14:05:00.12 | 1.021      | -14.85       | 60.012  | 0.001  | Normal         |
| 2021-08-14 14:05:00.15 | 0.874      | -18.20       | 59.850  | -0.152 | Generator_Trip |

- **Citation:**  
  Aaron J. Wilson, Ali Riza Ekti, Jim Follum, Shuchismita Biswas, Christabella Annalicia, Jhi-Young Joo, Omer Aziz, Jamie Lian,  
  *"The Grid Event Signature Library: An Open-Access Repository of Power System Measurement Signatures,"* IEEE Access, May 2024.  
  DOI: https://doi.org/10.1109/ACCESS.2024.3404886


### 8. BPA PMU Line Event Dataset
* **Description:** Actual transmission line fault signatures (Line-to-Ground, Line-to-Line) captured from the Bonneville Power Administration's (BPA) operational grid PMU data streams, strictly avoiding device-level maintenance data.
* **Download Link:** [IEEE Xplore (Dataset Repository via Paper)](https://ieeexplore.ieee.org/)
* **Data Statistics:** High-fidelity 60 Hz PMU recordings from the Pacific Northwest grid. Highly imbalanced to reflect real-world event rarity.
* **What the Data Sample Looks Like:** Time-series `.csv` logs detailing active/reactive power, voltage, and frequency variations aligned with protective relay logs.
* **Visual Sample (First 2 Rows):**

| Timestamp_UTC | Substation | V_Mag_kV | Freq_Hz | ROCOF | Relay_Trip |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 14:02:11.000 | SUB_A | 502.1 | 60.002 | 0.001 | 0 |
| 14:02:11.016 | SUB_A | 415.5 | 59.950 | -0.085 | 1 |
