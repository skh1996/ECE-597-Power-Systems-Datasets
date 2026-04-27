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
  and power to swing back and forth at a sustained frequency, if
  undetected this can damage equipment or cause cascading failures.
  The library provides labeled cases where the oscillation source location
  is known, so researchers can train and validate their detection
  algorithms against a ground truth. Used as the official dataset for
  the 2021 IEEE-NASPI Oscillation Source Location Contest.

- **What "Locating" the Oscillation Means:** Each case provides PMU
  measurements from multiple buses across the grid. The task is to
  identify **which specific generator, load, or bus is the source**
  injecting the periodic disturbance, not just that an oscillation
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
  > Note: Free IEEE account required to access dataset files.
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


### 3. PSML: Multi-Scale Transmission + Distribution PMU Disturbance Dataset

- **Data Type:** ⚠️ Simulated — This dataset is generated from a combined transmission and distribution grid simulation using PSS/E and OpenDSS.
  Although simulated, it is driven by real-world load, weather, and renewable generation data (2018–2020), resulting in physically realistic measurements.
  All PMU data is synthetic and not collected from real devices.

- **Description:** A multi-scale time-series dataset capturing grid
  dynamics at both minute-level (steady-state load and renewable
  profiles) and millisecond-level (transient disturbance events). The
  T+D co-simulation connects a PSS/E 23-bus transmission system with
  two IEEE 13-bus distribution systems, exchanging real-time voltage
  and power data between them at every time step. This joint simulation
  captures interaction effects between transmission and distribution
  that conventional transmission-only datasets miss. Developed by
  Texas A&M University, USC, MIT, and Purdue University and published
  in Nature Scientific Data (2022).

- **Network/System:**
  - Transmission: PSS/E 23-bus system (high-voltage bulk grid)
  - Distribution: Two IEEE 13-bus systems connected to the transmission
    grid via coupling buses
  - Load profiles: 66 real U.S. load zones from CAISO, ERCOT, MISO,
    PJM, NYISO, ISONE — covering 2018–2020

- **Number of PMUs:**
  - Millisecond-level data: PMU-equivalent measurements at all
    transmission buses (23 buses) and all distribution nodes
  - Minute-level data: Node-level voltage and branch power measurements
    across the full T+D system

- **PMU Placement:** Measurements are collected at every bus in the
  23-bus transmission system and at every node in both IEEE 13-bus
  distribution feeders. Full system observability — no partial
  coverage.

- **Recording Duration & Sampling Resolution:**
  - Millisecond-level PMU data: Each disturbance scenario captures
    the full transient event window. Sampled at approximately
    **960 time steps per scenario** at millisecond resolution.
  - Minute-level load/renewable data: **3 years** of continuous
    data (2018–2020) at **1-minute resolution** across 66 U.S.
    load zones.

- **Network Topology Provided:** Yes:
  - PSS/E 23-bus transmission model and IEEE 13-bus distribution
    model are standard benchmark systems widely available in the
    power systems community
  - Joint simulation Python code provided in the GitHub repository
    for full reproducibility

- **Download Link:** [Zenodo — PSML Dataset](https://zenodo.org/record/5130612)
  > Fully open access — no login required.
  > Direct download:
  > `wget https://zenodo.org/record/5130612/files/PSML.zip?download=1`
  > GitHub (code + benchmarks): [tamu-engineering-research/Open-source-power-dataset](https://github.com/tamu-engineering-research/Open-source-power-dataset)

- **Data Statistics:**
  - Millisecond-level disturbance events: Multiple forced oscillation
    and natural oscillation scenarios, each with 960 time steps ×
    91 measurement channels
  - Minute-level load/renewable: 66 load zones × 3 years (2018–2020)
    × 12 fields per zone
  - License: CC BY 4.0

---

#### Variable Meanings

**Millisecond-level transmission file (`trans.csv`):**

| Field | Physical Meaning |
|---|---|
| `Time(s)` | Timestamp at millisecond resolution |
| `VOLT ###` | Per-unit voltage magnitude at transmission bus `###` — e.g. `VOLT 151` is the voltage at Bus 151 |
| `POWR ### TO ### CKT #` | Active power (MW) flowing in branch `#` from bus `###` to bus `###` — e.g. `POWR 151 TO 152 CKT 1` |
| `VARS ### TO ### CKT #` | Reactive power (MVAR) flowing in branch `#` from bus `###` to bus `###` |

**Millisecond-level distribution file (`dist.csv`):**

| Field | Physical Meaning |
|---|---|
| `Time(s)` | Timestamp at millisecond resolution |
| `####.###.#` | Per-unit voltage magnitude of a specific phase at a distribution node. Format: `[T-bus].[D-bus].[phase]` — e.g. `3005.633.1` = phase A voltage at distribution bus 633 connected to transmission bus 3005 |

**Disturbance metadata file (`info.csv`):**

| Field | Physical Meaning |
|---|---|
| Start time | When the disturbance begins in the simulation (seconds) |
| End time | When the disturbance ends (seconds) |
| Location | Which bus or generator is the source of the disturbance |
| Type | Category of the disturbance event (see Event Labels below) |
#### Event Labels

| Label | Meaning | Location in Data |
|---|---|---|
| `Forced Oscillation` | An external periodic signal is injected at a specific bus or generator causing sustained grid-wide power swings. Source bus/generator recorded in `info.csv`. | `Millisecond/Forced_Oscillation/row_#/info.csv` |
| `Natural Oscillation` | The grid's internal electromechanical modes become underdamped and begin oscillating without external forcing. Source mode and location recorded in `info.csv`. | `Millisecond/Natural_Oscillation/row_#/info.csv` |

---

- **Visual Sample (`trans.csv` — Millisecond-level):**

| Time(s) | VOLT 151 (pu) | VOLT 152 (pu) | POWR 151 TO 152 CKT 1 | VARS 151 TO 152 CKT 1 |
|---|---|---|---|---|
| 0.0000 | 1.023 | 1.019 | 0.412 | 0.087 |
| 0.0167 | 0.651 | 0.704 | 1.823 | 0.541 |

- **Citation:** Zheng, X., Xu, N., Trinh, L., Wu, D., Huang, T.,
  Sivaranjani, S., Liu, Y., & Xie, L. (2022). *A multi-scale
  time-series dataset with benchmark for machine learning in
  decarbonized energy grids.* Nature Scientific Data, 9, 359.
  DOI: [10.1038/s41597-022-01455-7](https://doi.org/10.1038/s41597-022-01455-7)


### 4. HIL Cyber-Power Testbed PMU Data — IEEE 39-Bus

- **Data Type:** Hardware-in-the-Loop (HIL) — the IEEE 39-bus power
  system is emulated in real-time using a Real-Time Digital Simulator
  (RTDS). Physical PMU hardware devices and software PMUs are connected
  to the RTDS outputs to generate IEEE C37.118-compliant synchrophasor
  measurements. This bridges pure simulation and real field data — the
  grid model is simulated but the PMU hardware behavior, communication
  delays, and measurement noise are real.

- **Description:** High-fidelity synchrophasor recordings from a
  real-time HIL testbed at West Virginia University built on the IEEE
  39-bus transmission system. The testbed integrates RTDS, hardware
  and software PMUs, Real-Time Automation Controller (RTAC), and ns-3
  network emulation to reproduce realistic grid dynamics including
  communication latency and event-driven transients. Covers a wide
  range of labeled grid events designed to reflect actual system
  behavior. Developed at West Virginia University (NSF-funded). An
  earlier version of this dataset served as the official competition
  dataset at IEEE SGSMA 2024, Washington DC.

- **Network/System:** IEEE 39-bus New England transmission system —
  a standard benchmark representing a simplified model of the New
  England power grid with 39 buses, 10 generators, 19 loads, and
  46 transmission lines operating at 100 kV–345 kV.

- **Number of PMUs:** 26 PMUs optimally placed across the IEEE 39-bus
  system. 24 software PMUs (PMU51–PMU74) and 2 hardware PMUs
  (SEL401, SEL451) — totaling 26 measurement points.

- **PMU Placement:** PMUs are placed at 26 of the 39 buses, prioritizing
  generator terminal buses and major transmission corridors for
  maximum observability. Each PMU produces an independent `.csv` file.
  Full placement details are provided in the accompanying paper
  `SGSMA_2025.pdf` available on the dataset page.

- **Recording Duration & Sampling Resolution:** Continuous multi-event
  recordings pre-split into Training and Testing sets. Each PMU file
  contains the full time-series across all events in sequence.
  Reported at **30 Hz** (30 samples per second), IEEE C37.118
  compliant, GPS-synchronized via IEEE 1588 PTP to within ±1 μs.

- **Network Topology Provided:** ✅ Yes — the IEEE 39-bus system
  topology, line parameters, generator parameters, and load data are
  publicly available as a standard IEEE benchmark. The RTDS simulation
  model details are documented in `SGSMA_2025.pdf` on the dataset page.

- **Download Link:** [IEEE DataPort — High-Fidelity Synchrophasor Dataset from a Real-Time HIL Testbed](https://ieee-dataport.org/documents/high-fidelity-synchrophasor-dataset-real-time-hil-testbed-state-estimation-and-event)
  > ⚠️ Free IEEE account required. Total size: ~314.67 MB.
  > DOI: [10.21227/0mp1-fe58](https://dx.doi.org/10.21227/0mp1-fe58)

- **Data Statistics:**
  - 26 PMU files per split (Training + Testing)
  - Files: `PMU51.csv` through `PMU74.csv` (software PMUs) +
    `SEL401.csv` and `SEL451.csv` (hardware PMUs)
  - Training set: ~22–23 MB per PMU file
  - Testing set: ~11–13 MB per PMU file
  - Total: ~314.67 MB

---

#### Variable Meanings

Each PMU `.csv` file contains the following 14 measurement columns
per timestamp, representing three-phase synchrophasor quantities
at that PMU's bus location:

| Field | Physical Meaning |
|---|---|
| `Timestamp` | UTC-synchronized time of each measurement frame (GPS-locked to ±1 μs) |
| `Va_mag` | Phase A voltage magnitude in per-unit (pu) — strength of voltage on phase A relative to nominal |
| `Vb_mag` | Phase B voltage magnitude in per-unit (pu) |
| `Vc_mag` | Phase C voltage magnitude in per-unit (pu) |
| `Va_ang` | Phase A voltage phase angle in degrees — timing offset of phase A voltage waveform relative to GPS reference |
| `Vb_ang` | Phase B voltage phase angle in degrees |
| `Vc_ang` | Phase C voltage phase angle in degrees |
| `Ia_mag` | Phase A current magnitude in per-unit (pu) — amount of current flowing into/out of the bus on phase A |
| `Ib_mag` | Phase B current magnitude in per-unit (pu) |
| `Ic_mag` | Phase C current magnitude in per-unit (pu) |
| `Ia_ang` | Phase A current phase angle in degrees |
| `Ib_ang` | Phase B current phase angle in degrees |
| `Ic_ang` | Phase C current phase angle in degrees |
| `Freq_Hz` | Instantaneous grid frequency in Hz — nominal is 60 Hz. Deviations indicate generation-load imbalance. |
| `ROCOF` | Rate of Change of Frequency (Hz/s) — how fast the frequency is changing. Large ROCOF values indicate a sudden generator trip or major fault. |
| `Event_Label` | Categorical label identifying the event type at this timestamp (see Event Labels below) |

---

#### Event Labels

| Label | Meaning |
|---|---|
| `Normal` | Steady-state grid operation — no disturbance occurring |
| `Generator_Trip` | A generator suddenly disconnects from the grid causing frequency drop and power redistribution |
| `Generator_Reconnection` | A previously tripped generator reconnects, causing transient voltage and frequency recovery |
| `Load_Variation` | Gradual or step change in load demand at one or more buses |
| `Load_Shedding` | Deliberate disconnection of load to prevent frequency collapse |
| `Line_Outage` | A transmission line is disconnected causing power to reroute through remaining lines |
| `Fault_Event` | Short-circuit or other fault condition on a bus or transmission line |

---

- **Visual Sample (Illustrative Schema):**

| Timestamp | Va_mag (pu) | Va_ang (deg) | Ia_mag (pu) | Ia_ang (deg) | Freq_Hz | ROCOF | Event_Label |
|---|---|---|---|---|---|---|---|
| 1.100 | 1.042 | -8.50 | 0.512 | -15.20 | 60.001 | 0.000 | Normal |
| 1.133 | 0.651 | -12.10 | 4.850 | -45.60 | 59.980 | -0.042 | Fault_Event |

- **Citation:** M. Mustafa Hussain, Purna Kukadiya, Anurag Srivastava,
  *"High-Fidelity Synchrophasor Dataset from a Real-Time HIL Testbed
  for State Estimation and Event Analysis,"* IEEE DataPort,
  December 2025.
  DOI: [10.21227/0mp1-fe58](https://dx.doi.org/10.21227/0mp1-fe58)

### 5. ORNL Grid Event Signature Library (GESL)

- **Data Type:** ✅ Real field data — signatures are collected directly
  from operational U.S. electric utility grids. All data providers are
  anonymized to enable open sharing while protecting grid security and
  utility confidentiality.

- **Description:** The largest open-access repository of real
  transmission-level power grid event signatures, developed jointly
  by Oak Ridge National Laboratory (ORNL), Lawrence Livermore National
  Laboratory (LLNL), and Pacific Northwest National Laboratory (PNNL)
  under the U.S. DOE Office of Electricity. The library collects,
  labels, and standardizes PMU and Point-on-Wave (PoW) recordings from
  multiple U.S. utility providers into a single searchable platform.
  All events are labeled using a uniform three-level taxonomy
  (Group → Class → Subclass) applied consistently across all data
  sources. Designed to serve as a go-to benchmark resource for grid
  event detection and AI/ML algorithm development and validation.

- **Network/System:** Real operational U.S. transmission and
  distribution grids contributed by multiple anonymous utility
  providers across two interconnections (Eastern and Western). No
  single standard IEEE test case — data represents diverse real
  grid topologies and configurations.

- **Number of PMUs:** 2,191 PMU signatures and 443 PoW signatures
  in the library as of the latest published count, sourced from
  approximately 500 unique PMUs across the United States contributed
  by multiple utility providers.

- **PMU Placement:** Field-deployed PMUs at real transmission
  substations and distribution nodes across the U.S. grid. Exact
  locations are anonymized — each event record includes a PDF map
  or metadata file indicating the general measurement location
  within the anonymized grid topology.

- **Recording Duration & Sampling Resolution:** Varies per event
  and sensor type:
  - PMU data: typically 30–60 Hz reporting rate (30–60 samples
    per second), capturing event windows from seconds to minutes
  - PoW data: sub-cycle resolution (higher than PMU rate),
    capturing fast transients at microsecond-level detail
  - Each downloaded signature includes the full event window
    with pre-event baseline and post-event recovery period

- **Network Topology Provided:** ⚠️ Partially — topology is
  anonymized to protect utility confidentiality. Each event record
  includes a description of the measurement context (transmission
  level vs. distribution level, voltage class, sensor type) but
  not the full grid model.

- **Download Link:** [ORNL Grid Event Signature Library (GESL)](https://gesl.ornl.gov)
  > ⚠️ Free account required (valid email only, no institutional
  > affiliation needed). Once logged in:
  > 1. Click **Signature Dashboard**
  > 2. Filter by event type, sensor type, voltage level, or date
  > 3. Preview waveform plot before downloading
  > 4. Download individual event records as `.csv` files
  > A Python API is also available for programmatic bulk access.

- **Data Statistics:**
  - 2,191 PMU signatures + 443 PoW signatures (and growing)
  - 550+ registered users from industry, academia, and national labs
  - Data spans two U.S. interconnections across multiple utility
    providers and instrument configurations
  - Uniform three-level event taxonomy applied across all records

---

#### Event Label Taxonomy

GESL uses a three-level hierarchical labeling system — Group,
Class, and Subclass — applied uniformly across all data providers. 
The major event groups relevant to transmission dynamic analysis are:

| Group | Class | Subclass (Examples) | Physical Meaning |
|---|---|---|---|
| **Fault** | Transmission Fault | Line-to-Ground, Line-to-Line, Three-Phase | Short circuit events on transmission lines or buses causing sudden voltage drop and current surge |
| **Generation** | Generator Trip | Sudden loss | A generator suddenly disconnects from the grid causing frequency drop and power redistribution across remaining generators |
| **Generation** | Generator Reconnection | Planned, Unplanned | A previously offline generator reconnects, causing transient voltage and frequency recovery |
| **Load** | Load Shedding | Automatic, Manual | Deliberate disconnection of load to prevent frequency collapse during generation shortage |
| **Oscillation** | Forced Oscillation | Low frequency, Subsynchronous | Periodic disturbance injected by a malfunctioning device causing grid-wide power swings |
| **Oscillation** | Natural Mode | Inter-area, Local | Poorly damped electromechanical modes causing sustained oscillation without external forcing |
| **Switching** | Line Trip | Automatic, Manual | Transmission line disconnection due to relay operation or planned switching |
| **Transient** | Capacitor Bank | Switching-in, Switching-out | Short current surge when capacitor banks switch, can cause brief voltage transients |

---

#### Variable Meanings (Per Downloaded Event `.csv`)

Each downloaded signature file contains time-series synchrophasor
measurements. The available channels depend on the sensor type
and provider, but the standard PMU fields are:

| Field | Physical Meaning |
|---|---|
| `Timestamp` | UTC time of each measurement frame, GPS-synchronized |
| `V_mag` | Voltage magnitude in per-unit (pu) or kV — strength of voltage at the measurement point |
| `V_ang` | Voltage phase angle in degrees — timing offset of the voltage waveform relative to GPS reference |
| `I_mag` | Current magnitude in pu or amps — amount of current flowing at the measurement point |
| `I_ang` | Current phase angle in degrees |
| `Freq_Hz` | Instantaneous grid frequency in Hz — nominal 60 Hz (Eastern/Western US) or 50 Hz |
| `ROCOF` | Rate of Change of Frequency (Hz/s) — how rapidly the frequency is changing; large values indicate major generation or load events |
| `Event_Tag` | Three-level hierarchical label: Group / Class / Subclass (e.g., `Generation / Generator_Trip / Sudden_Loss`) |

> **Note:** Not all fields are present in every record — availability
> depends on the sensor type (PMU vs. PoW) and what the contributing
> utility provided. The dashboard shows available channels for each
> signature before download.

---

- **Visual Sample (Illustrative Schema):**

| Timestamp | V_mag (pu) | V_ang (deg) | Freq_Hz | ROCOF | Event_Tag |
|---|---|---|---|---|---|
| 2021-08-14 14:05:00.12 | 1.021 | -14.85 | 60.012 | 0.001 | Normal |
| 2021-08-14 14:05:00.15 | 0.874 | -18.20 | 59.850 | -0.152 | Generation/Generator_Trip/Sudden_Loss |

- **Citation:** Aaron J. Wilson, Ali Riza Ekti, Jim Follum,
  Shuchismita Biswas, Christabella Annalicia, Jhi-Young Joo,
  Omer Aziz, Jamie Lian, *"The Grid Event Signature Library:
  An Open-Access Repository of Power System Measurement
  Signatures,"* IEEE Access, May 2024.
  DOI: [10.1109/ACCESS.2024.3404886](https://doi.org/10.1109/ACCESS.2024.3404886)


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
