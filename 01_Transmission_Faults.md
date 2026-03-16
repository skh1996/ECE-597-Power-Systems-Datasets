# Topic 1: Transmission Dynamic Events & PMU Data

## Overview
This document contains the detailed data statistics, structural schemas, and direct download sources for the datasets categorized under Power Line Fault Detection, Transmission Dynamics, and PMU (Phasor Measurement Unit) data. 

As per project requirements, the datasets below include both transmission and high-level distribution network faults to ensure a comprehensive overview of grid anomalies.

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


### 4. Electrical Line Fault Detection 
* **Description:** A clean, simulated dataset covering 4 different Transmission Line (TL) configurations explicitly designed for testing ML classification models.
* **Download Link:** [Figshare - Electrical Line Fault Dataset](https://figshare.com/articles/dataset/Dataset_for_Electrical_Line_Fault_Detection_Classification/30615710)
* **Data Statistics:** ~10 MB lightweight format. Perfectly balanced classes covering 11 distinct fault types.
* **What the Data Sample Looks Like:** A `.csv` file containing 3-phase Voltage and Current waveforms mapped to a categorical fault label.
* **Visual Sample (First 2 Rows):**

| Va | Vb | Vc | Ia | Ib | Ic | Fault_Type |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| -0.12 | 0.85 | -0.73 | 45.2 | -22.1 | -23.1 | No_Fault |
| 0.05 | -0.88 | 0.83 | 315.4 | -20.5 | -22.9 | L-G_PhaseA |


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


### 6. LANL Open Source Grid Events
* **Description:** Contingency and line outage data used for grid topology studies and cascading failure analysis.
* **Download Link:** [GitHub - PowerModels.jl Data](https://github.com/lanl-ansi/PowerModels.jl)
* **Data Statistics:** Covers various standard IEEE test cases ranging from the 14-bus to the 300-bus systems. 
* **What the Data Sample Looks Like:** Text files in the `.m` (Matpower) format detailing matrix arrays for buses, branches, and network status.
* **Visual Sample (Branch Matrix Array excerpt):**

| fbus | tbus | r | x | b | rateA | status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 2 | 0.019 | 0.059 | 0.052 | 9900 | 1 |
| 1 | 5 | 0.054 | 0.223 | 0.049 | 9900 | 0 |


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


### 8. Power System Faults (SCADA)
* **Description:** A dataset mimicking SCADA logs that provides environmental and operational context rather than just raw electrical waveforms.
* **Download Link:** [Kaggle - Power System Faults Dataset](https://www.kaggle.com/datasets/ziya07/power-system-faults-dataset)
* **Data Statistics:** Granular 1-minute interval sampling.
* **What the Data Sample Looks Like:** A tabular `.csv` containing columns for both physical and environmental telemetry.
* **Visual Sample (First 2 Rows):**

| Timestamp | Voltage_kV | Current_A | Temp_C | Wind_Speed_ms | Maintenance_Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 2023-10-01 08:00 | 11.5 | 320 | 22 | 5.2 | Normal |
| 2023-10-01 08:01 | 4.2 | 950 | 22 | 18.5 | Fault_Line_Break |
