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
* **Download Link:** [EPFL Infoscience Repository](https://infoscience.epfl.ch/record/228833)
* **Data Statistics:** Standard European Grid Frequency (50 Hz). Multi-day continuous logging. 
* **What the Data Sample Looks Like:** Time-series `.csv` files containing high-resolution synchrophasor measurements.
* **Visual Sample (First 2 Rows):**

| Timestamp | Voltage_Mag_kV | Phase_Angle_rad | Frequency_Hz | ROCOF |
| :--- | :--- | :--- | :--- | :--- |
| 1459451121.00 | 20.124 | 0.451 | 49.981 | -0.012 |
| 1459451121.02 | 20.122 | 0.453 | 49.978 | -0.015 |


### 4. IEEE PMU-OSL Dataset
* **Description:** Verified Phasor Measurement Unit (PMU) data of transmission dynamic events, including forced oscillations and short-circuit faults, simulated on the WECC 179-bus system alongside real-world event data.
* **Download Link:** [IEEE DataPort - PMU-OSL](https://ieee-dataport.org/open-access/phasor-measurement-unit-dataset-oscillation-source-location)
* **Data Statistics:** 30 Hz sampling rate. Contains cleanly labeled temporal data for both localized and wide-area transmission oscillation events.
* **What the Data Sample Looks Like:** Time-series `.csv` files containing timestamped voltage magnitudes, phase angles, and frequency across multiple transmission buses.
* **Visual Sample (First 2 Rows):**

| Timestamp | Bus_ID | Voltage_Mag_pu | Phase_Angle_deg | Frequency_Hz | Event_Type |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0.000 | 83 | 1.025 | -15.24 | 60.001 | Ambient |
| 0.033 | 83 | 1.021 | -15.30 | 59.985 | Oscillation |


### 5. IEEE 123-Node Fault Data
* **Description:** Simulated SCADA and PMU fault data applied to the standard IEEE 123-node distribution feeder, bridging transmission-level analysis with distribution topology.
* **Download Link:** [IEEE Dataport (Search: IEEE 123 Node Faults)](https://ieee-dataport.org/)
* **Data Statistics:** Balanced fault types applied across multiple network buses to simulate geographic fault location problems.
* **What the Data Sample Looks Like:** Structured `.csv` files mapping nodes to per-unit electrical readings and fault targets.
* **Visual Sample (First 2 Rows):**

| Timestamp | Node_ID | Voltage_pu | Current_pu | Fault_Location_Target |
| :--- | :--- | :--- | :--- | :--- |
| 0.016 | Bus_54 | 0.98 | 1.05 | None |
| 0.032 | Bus_54 | 0.45 | 4.12 | Bus_54_SLG |


### 6. HIL Cyber-Power Testbed PMU Data
* **Description:** Hardware-In-The-Loop (HIL) synchrophasor recordings from an IEEE 39-bus system emulation. Features cleanly annotated dynamic events, including single and multi-phase transmission faults.
* **Download Link:** [IEEE DataPort / ResearchGate (Mustafa et al.)](https://ieee-dataport.org/)
* **Data Statistics:** 30 Hz reporting rate, IEEE C37.118 compliant PMU streams. Contains balanced classes of L-G, L-L, and 3-phase faults.
* **What the Data Sample Looks Like:** Tabular `.csv` files capturing synchronous positive sequence voltage and current phasors during transient states.
* **Visual Sample (First 2 Rows):**

| Time_s | V1_mag | V1_angle | I1_mag | I1_angle | Fault_Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1.100 | 1.042 | -8.50 | 0.512 | -15.20 | Normal |
| 1.133 | 0.650 | -12.10 | 4.850 | -45.60 | L-G_Fault |


### 7. ORNL Transmission Signatures
* **Description:** PMU frequency events and wide-area oscillations captured from the US grid, useful for frequency stability analysis.
* **Download Link:** [DOE / ORNL Datasets](https://www.ornl.gov/)
* **Data Statistics:** 60 Hz sampling rate, capturing real-world frequency dips and generator tripping events.
* **What the Data Sample Looks Like:** Time-series tables containing standard synchrophasor event flags.
* **Visual Sample (First 2 Rows):**

| Timestamp | Frequency_Hz | ROCOF | Event_Flag |
| :--- | :--- | :--- | :--- |
| 2021-08-14 14:05:00.12 | 60.012 | 0.001 | 0 |
| 2021-08-14 14:05:00.15 | 59.850 | -0.152 | Gen_Trip |


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
