# Topic 1: Transmission Dynamic Events & PMU Data

## Overview
This document contains the detailed data statistics, structural schemas, and direct download sources for the datasets categorized under Power Line Fault Detection, Transmission Dynamics, and PMU (Phasor Measurement Unit) data. 

As per project requirements, the datasets below strictly focus on transmission and high-level distribution network faults to ensure a comprehensive overview of grid anomalies, entirely excluding device-level and maintenance logs. All datasets are grounded in verified, peer-reviewed publications or official industry benchmarks.

---

### 1. UCI Electrical Grid Stability

- **Data Type:** Simulated —> generated via mathematical modeling of the
  Decentral Smart Grid Control (DSGC) differential equation system.
  No real grid hardware was used.

- **Description:** A simulated dataset representing a 4-node star-topology
  grid with one electricity supplier and three consumers. The DSGC system
  links electricity price directly to grid frequency, allowing participants
  to adjust consumption in response to price signals. Each instance
  represents one simulation run with randomized input conditions, and the
  output records whether the grid remained stable or collapsed under those
  conditions. Useful as a foundational benchmark for binary grid stability
  classification.

- **Network/System:** 4-node star topology —> 1 supplier node (Node 1) +
  3 consumer nodes (Nodes 2, 3, 4).

- **Number of PMUs:** Not applicable — no physical or simulated PMU sensors
  are used. Variables represent node-level quantities derived directly from
  the DSGC mathematical model.

- **Recording Duration & Sampling Resolution:** Not applicable — this
  dataset consists of independent simulation snapshots, not time-series
  recordings. Each row represents one complete simulation run.

- **Network Topology Provided:** Partially — the 4-node star architecture
  is described in the original paper. No standard IEEE bus model files are
  provided since this is a custom mathematical model.

- **Download Link:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/471/electrical+grid+stability+simulated+data)

- **Data Statistics:** 60,000 simulation instances. 12 input features,
  1 continuous target (`stab`), 1 categorical target (`stabf`).
  Class distribution: ~36% stable, ~64% unstable.

---

#### Variable Meanings

| Variable | Physical Meaning | Range |
|---|---|---|
| `tau1` | Reaction time of the **supplier node** — how fast the producer responds to price changes (seconds) | 0.5 – 10 s |
| `tau2, tau3, tau4` | Reaction time of each **consumer node** — how fast each consumer adjusts usage in response to price (seconds) | 0.5 – 10 s |
| `p1` | Net power of the **supplier node** — always positive (generating). Non-predictive feature: p1 = −(p2+p3+p4). Exclude from model training. | 1.5 – 6.0 |
| `p2, p3, p4` | Net power of each **consumer node** — always negative (consuming) | −2.0 – −0.5 |
| `g1` | Price elasticity coefficient (gamma) of the **supplier** — sensitivity to electricity price changes | 0.05 – 1.00 |
| `g2, g3, g4` | Price elasticity coefficient of each **consumer node** | 0.05 – 1.00 |
| `stab` | Maximum real part of the characteristic equation root — if positive the system is unstable, if negative the system is stable. Do not use alongside `stabf` as a target. | Real number |
| `stabf` | Binary stability label derived from `stab`. **Primary classification target.** | `stable` / `unstable` |

---

#### Event Labels

| Label | Meaning | Count (approx.) |
|---|---|---|
| `stable` | Grid remains balanced — frequency deviation is controlled and the system does not collapse | ~21,600 (36%) |
| `unstable` | Grid becomes unbalanced — frequency deviation grows and the system would collapse without intervention | ~38,400 (64%) |

---

- **Visual Sample (First 2 Rows):**

| tau1 | tau2 | p1 | p2 | g1 | stab | stabf |
|---|---|---|---|---|---|---|
| 2.959 | 3.079 | 3.763 | −1.221 | 0.650 | 0.055 | unstable |
| 9.304 | 4.902 | 2.009 | −1.469 | 0.859 | −0.137 | stable |

- **Citation:** V. Arzamasov, K. Böhm, P. Jochem, *"Towards Concise
  Models of Grid Stability,"* 2018 IEEE International Conference on
  Communications, Control, and Computing Technologies for Smart Grids
  (SmartGridComm), Aalborg, 2018, pp. 1–6.
  DOI: [10.1109/SmartGridComm.2018.8587498](https://doi.org/10.1109/SmartGridComm.2018.8587498)



### 2. IEEE Test Cases Library — Forced/Sustained Power System Oscillations

- **Data Type:** Mixed:
  - Simulated — WECC 179-bus cases (27 cases) and WECC 240-bus cases
    (13 cases) are generated via time-domain simulation using Powertech
    Lab's TSAT software with EPRI's PMU Emulator applied to mimic real
    PMU device behavior including missing samples.
  - Real field data — 6 cases of actual oscillatory events recorded
    from the ISO New England (ISO-NE) transmission system using field-
    deployed PMUs.

- **Description:** A benchmark library created specifically for developing
  and testing algorithms that locate the source of power system
  oscillations. Power system oscillations occur when generators or loads
  inject a periodic disturbance into the grid causing voltage, current,
  and power to swing back and forth at a sustained frequency — if
  undetected this can damage equipment or cause cascading failures.
  The library provides labeled cases where the oscillation source location
  is known, so researchers can train and validate their detection
  algorithms against a ground truth. Used as the official dataset for
  the 2021 IEEE-NASPI Oscillation Source Location Contest.

- **What "Locating" the Oscillation Means:** Each case provides PMU
  measurements from multiple buses across the grid. The task is to
  identify **which specific generator, load, or bus is the source**
  injecting the periodic disturbance — not just that an oscillation
  exists, but pinpointing its origin. The answer (ground truth label)
  for each simulated case is documented in the case description file.

- **Network/System:**
  - Sub-dataset 1: WECC 179-bus transmission system (simplified Western
    US grid model, PSS/E V30 format)
  - Sub-dataset 2: WECC 240-bus transmission system (NREL reduced model,
    243 buses, 146 generating units at 56 plants)
  - Sub-dataset 3: ISO New England actual transmission system
    (topology partially provided via PDF map)
  - Sub-dataset 4: 14-bus inverter-based system (GFL and GFM inverter
    models, PoW data only)

- **Number of PMUs:**
  - WECC 179-bus: PMUs at all generator buses and major transmission
    buses — full system observability
  - WECC 240-bus: Partial observability — PMUs at a subset of buses
    and branches (monitored locations listed in provided XLSX file)
  - ISO-NE: Multiple field PMUs across the New England transmission
    system (locations shown in provided PDF map)

- **PMU Placement:** Topology and monitoring files provided with each
  case. For WECC 240-bus, the file `Monitored_buses&branches.xlsx`
  lists all monitored buses and branches. For ISO-NE, a PDF map of
  measurement locations is included per case.

- **Recording Duration & Sampling Resolution:**
  - WECC 179-bus: Variable per case — typically several minutes of
    simulation capturing the onset and sustained period of oscillation.
    Sampled at **30 Hz** (30 samples per second).
  - WECC 240-bus: **90 seconds** per case — 30 seconds pre-event
    window + 60 seconds post-event window. Sampled at **30 Hz**.
  - ISO-NE real cases: Duration varies per event — field recordings
    capturing actual oscillation onset and decay.
  - 14-bus PoW: Sub-cycle resolution waveform data (higher than PMU
    rate) stored as MATLAB `.mat` files.

- **Network Topology Provided:** Yes — for all sub-datasets:
  - WECC 179-bus: `.raw` (power flow) and `.dyr` (dynamic data) model
    files compatible with PSS/E V30
  - WECC 240-bus: Full TSAT model files (`.pfb`, `.dyr`, `.tudm` etc.)
    developed by NREL
  - ISO-NE: PDF map of measurement locations per case
  - 14-bus: MATLAB model files included

- **Download Link:** [IEEE DataPort — Test Cases Library on Forced/Sustained Power System Oscillations](https://ieee-dataport.org/documents/test-cases-library-forcedsustained-power-system-oscillations)
  > ⚠️ Free IEEE account required to access dataset files.
  > DOI: [10.21227/a6hg-n822](https://dx.doi.org/10.21227/a6hg-n822)

- **Data Statistics:**

| Sub-dataset | Type | Cases | Buses | Sampling |
|---|---|---|---|---|
| WECC 179-bus | Simulated | 18 forced oscillation + 9 natural mode = 27 cases | 179 | 30 Hz |
| WECC 240-bus | Simulated | 13 forced oscillation cases | 240 | 30 Hz |
| ISO New England | Real field data | 6 actual oscillation events | Real US grid | Field PMU rate |
| 14-bus PoW | Simulated | 6 forced + 5 natural mode = 11 cases | 14 | Sub-cycle (PoW) |

---

#### Variable Meanings (PMU data files)

Each PMU case folder contains separate `.txt` files, one per
measurement channel:

| File / Field | Physical Meaning |
|---|---|
| `BusVolMag.txt` | Bus voltage magnitude in per-unit (pu) at each monitored bus — how strong the voltage is relative to the nominal value |
| `BusVolAng.txt` | Bus voltage phase angle in degrees — the timing offset of the voltage waveform at each bus relative to a reference |
| `LinCurMag.txt` | Line current magnitude in pu — how much current is flowing through each monitored transmission line |
| `LinCurAng.txt` | Line current phase angle in degrees — timing offset of the current waveform on each line |
| `RotorAng.txt` | Generator rotor angle in degrees — angular position of the generator rotor relative to a reference, indicates generator swing behavior during oscillation |
| `RotorSpd.txt` | Generator rotor speed in pu — deviation of generator speed from nominal (1.0 pu = synchronous speed). Values above or below 1.0 indicate the generator is oscillating. |

---

#### Event Labels

| Label | Meaning | Cases |
|---|---|---|
| Forced Oscillation (FO) | A periodic external disturbance is injected at a specific generator, load, or HVDC device causing the whole grid to oscillate. The source location is the labeled ground truth. | 18 (WECC 179) + 13 (WECC 240) + 6 (WECC 14-bus PoW) |
| Natural Mode Oscillation (ND) | The grid's own internal electromechanical modes become poorly damped and start oscillating without any external forcing. Source is the weakly damped mode location. | 9 (WECC 179) + 5 (WECC 14-bus PoW) |
| Actual Oscillation Event | Real oscillation events recorded from the ISO New England grid. Source location identified and verified by ISO-NE engineers. | 6 (ISO-NE field data) |

> The ground truth source location for each case is documented in
> `Description.txt` inside each case folder. The modeling task is
> source localization — given the PMU time-series, predict which
> bus or generator ID is the oscillation source..

---

- **Visual Sample (Illustrative Schema — `BusVolMag.txt`):**

| Time_s | Bus_4 (pu) | Bus_79 (pu) | Bus_118 (pu) | Bus_151 (pu) |
|---|---|---|---|---|
| 0.000 | 1.023 | 1.018 | 1.031 | 1.009 |
| 0.033 | 1.021 | 1.015 | 1.029 | 1.006 |

- **Citation:** Bin Wang, Slava Maslennikov, Kai Sun, Pablo Gill Estevez,
  *"Test Cases Library on Forced/Sustained Power System Oscillations,"*
  IEEE DataPort, 2025.
  DOI: [10.21227/a6hg-n822](https://dx.doi.org/10.21227/a6hg-n822)


### 4. PSML: Multi-Scale Transmission + Distribution PMU Disturbance Dataset

- **Description:** A first-of-its-kind open-access multi-scale PMU time-series dataset generated through a novel joint Transmission + Distribution (T+D) co-simulation platform (PSS/E 23-bus transmission + two IEEE 13-bus distribution systems via OpenDSS). Contains millisecond-resolution voltage, current, and power measurements across transmission buses during labeled dynamic disturbance events — including short-circuit faults, generator trips, load changes, and natural oscillations. Developed by Texas A&M University, USC, MIT, and Purdue University. Published in *Nature Scientific Data* (2022).
- **Download Link:** [Zenodo — PSML Dataset (DOI: 10.5281/zenodo.5130612)](https://zenodo.org/record/5130612)
- **GitHub (Code + Benchmarks):** [tamu-engineering-research/Open-source-power-dataset](https://github.com/tamu-engineering-research/Open-source-power-dataset)
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


### 5. HIL Cyber-Power Testbed PMU Data — IEEE 39-Bus

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


### 6. ORNL Grid Event Signature Library (GESL) — Transmission Signature Library

- **Description:** A large open-source repository of real transmission-level PMU data, developed by ORNL and LLNL under the DOE Office of Electricity. It includes 1,694 labeled transmission events and 2,500+ total PMU and Point-on-Wave signatures collected from U.S. utilities across two interconnections. Events cover generator trips, oscillations, faults, frequency disturbances, and line trips, all anonymized and consistently labeled.

- **Download Link:** [ORNL Grid Event Signature Library (GESL)](https://gesl.ornl.gov)
  > Note: Free account required. Data accessible via web Dashboard or Python API. 
  
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


### 7. IRTSD: IBR-Rich Transmission System Disturbance Dataset

- **Description:** A large-scale open-source electromagnetic transient (EMT) dataset focused on transmission system disturbances in grids with high inverter-based resource (IBR/renewable) penetration (~40% IBR). Developed by Pacific Northwest National Laboratory (PNNL) under the DOE SENTIENT project. Contains 5,500 labeled event cases and ~1.4 million signal recordings covering a wide frequency range (0.5 Hz to 4 kHz), including both commonplace disturbances and emergent IBR-related phenomena not covered by conventional PMU datasets. Addresses a critical gap in the power systems ML community: the lack of publicly available data capturing IBR-specific transmission dynamics.
- **Download Link:** [IEEE DataPort — IRTSD (Open Access)](https://ieee-dataport.org/open-access/irtsd-open-source-data-and-toolset-electromagnetic-transient-analysis-disturbances-and)
- **Data Statistics:** 5,500 labeled event cases across 4 event types: short-circuit faults (180 cases), forced oscillations (576 cases), generator trips (15 cases), and IBR control malfunctions (>4,000 cases). Each case is a `.csv` file (~19–25 MB) with currents, voltages, active/reactive powers, and frequency sampled from detailed PMU models. Total dataset size: ~29.56 GB. PSCAD model files and Python generation scripts also included for reproducibility.
- **Data Format:** Individual `.csv` files per event (e.g., `SENT_Model_v02_fault_case_1.csv`, `SENT_Model_v02_forc_osc_case_1.csv`, `SENT_Model_v02_gen_trip_case_1.csv`, `SENT_Model_v02_ibr_mc_case_1.csv`), organized by event type and operating condition folder.
- **What the Data Sample Looks Like:** Each `.csv` file is a time-series table where columns represent labeled signal channels — bus voltages, branch currents, active/reactive power flows, and frequency — sampled at sub-millisecond resolution during the disturbance window.
- **Visual Sample (Illustrative Schema):**

| Time (s) | V_Bus1 (pu) | I_Branch1 (pu) | P_Branch1 (pu) | Q_Branch1 (pu) | Freq (Hz) | Event_Label |
| --- | --- | --- | --- | --- | --- | --- |
| 0.0000 | 1.021 | 0.412 | 0.387 | 0.091 | 60.000 | Normal |
| 0.0167 | 0.643 | 2.841 | 1.823 | 0.654 | 59.850 | Fault |

- **Citation:** Brett Ross, Kaveri Mahapatra, *"IRTSD: Open-Source Data and Toolset for Electromagnetic Transient Analysis of Disturbances and IBR Control Malfunctions in Transmission Systems,"* IEEE DataPort, December 2024. DOI: [10.21227/mp6d-j677](https://dx.doi.org/10.21227/mp6d-j677)

### 8. VSB Power Line Fault Detection
* **Description:** Three-phase voltage measurements from medium-voltage overhead lines to detect Partial Discharge (PD), a critical precursor to catastrophic grid failure.
* **Download Link:** [Kaggle - VSB Power Line Fault Detection](https://www.kaggle.com/c/vsb-power-line-fault-detection/data)
* **Data Statistics:** High-frequency 20ms duration signals (800,000 measurements per signal). 8,712 total signals. Highly Imbalanced (~95% Normal, ~5% Faults).
* **What the Data Sample Looks Like:** A `.parquet` file containing continuous numeric arrays mapped to a binary target.
* **Visual Sample (First 2 Rows):**

| signal_id | phase_0 (V) | phase_1 (V) | phase_2 (V) | target |
| :--- | :--- | :--- | :--- | :--- |
| 0 | 18 | -16 | -5 | 0 |
| 1 | 17 | -17 | -6 | 1 |

- **Citation:** S. Misák, J. Fulnecek, T. Vantuch, T. Buriánek, T. Jezowicz, *"A Complex Classification Approach of Partial Discharges from Covered Conductors in Real Environment,"* IEEE Transactions on Dielectrics and Electrical Insulation, vol. 24, no. 2, pp. 1097–1104, 2017. DOI: [10.1109/TDEI.2017.006135](https://doi.org/10.1109/TDEI.2017.006135)
