# Topic 1: Transmission Dynamic Events & PMU Data

## Overview
This document contains the detailed data statistics, structural schemas, and direct download sources for the datasets categorized under Power Line Fault Detection, Transmission Dynamics, and PMU (Phasor Measurement Unit) data. 

As per project requirements, the datasets below include both transmission and high-level distribution network faults to ensure a comprehensive overview of grid anomalies.

---

### 1. VSB Power Line Fault Detection
* **Description:** Three-phase voltage measurements from medium-voltage overhead lines to detect Partial Discharge (PD), a critical precursor to catastrophic grid failure.
* **Download Link:** [Kaggle - VSB Power Line Fault Detection](https://www.kaggle.com/c/vsb-power-line-fault-detection/data)
* **Data Statistics:** High-frequency 20ms duration signals (800,000 measurements per signal). 8,712 total signals. Highly Imbalanced (~95% Normal, ~5% Faults).
* **What the Data Sample Looks Like:** A `.parquet` file containing three continuous numeric arrays: `phase_0` (Voltage A), `phase_1` (Voltage B), and `phase_2` (Voltage C), mapped to a binary `target` column (0 = Healthy, 1 = Fault).

### 2. UCI Electrical Grid Stability
* **Description:** A mathematically rigorous simulated dataset representing a 4-node star architecture grid, predicting system stability after control disturbances.
* **Download Link:** [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/471/electrical+grid+stability+simulated+data)
* **Data Statistics:** 60,000 instances total. 12 input features and 1 predictive target.
* **What the Data Sample Looks Like:** A standard `.csv` file where each row represents a time step. Columns include grid parameters like `tau1` to `tau4` (Reaction Time), `p1` to `p4` (Power Balance), and a categorical `stabf` (Stable/Unstable label).

### 3. EPFL Campus Grid PMU Data
* **Description:** Real-world Phasor Measurement Unit (PMU) data collected from a live university campus grid in Switzerland during normal and anomalous operations.
* **Download Link:** [EPFL Infoscience Repository](https://infoscience.epfl.ch/record/228833)
* **Data Statistics:** Standard European Grid Frequency (50 Hz). Multi-day continuous logging. 
* **What the Data Sample Looks Like:** Time-series `.csv` files containing high-resolution columns for `Timestamp`, `Voltage_Magnitude`, `Phase_Angle`, `Frequency`, and `ROCOF` (Rate of Change of Frequency).

### 4. Electrical Line Fault Detection 
* **Description:** A clean, simulated dataset covering 4 different Transmission Line (TL) configurations explicitly designed for testing ML classification models.
* **Download Link:** [Figshare - Electrical Line Fault Dataset](https://figshare.com/articles/dataset/Dataset_for_Electrical_Line_Fault_Detection_Classification/30615710)
* **Data Statistics:** ~10 MB lightweight format. Perfectly balanced classes covering 11 distinct fault types (Single Line-to-Ground, Line-to-Line, 3-Phase, etc.).
* **What the Data Sample Looks Like:** A `.csv` file containing 3-phase Voltage and Current waveforms (`Va`, `Vb`, `Vc`, `Ia`, `Ib`, `Ic`) mapped to a `Fault_Type` categorical label.

### 5. IEEE 123-Node Fault Data
* **Description:** Simulated SCADA and PMU fault data applied to the standard IEEE 123-node distribution feeder, bridging transmission-level analysis with distribution topology.
* **Download Link:** [IEEE Dataport (Search: IEEE 123 Node Faults)](https://ieee-dataport.org/)
* **Data Statistics:** Balanced fault types applied across multiple network buses to simulate geographic fault location problems.
* **What the Data Sample Looks Like:** Structured `.csv` files mapping `Node_ID` to `Voltage_pu` (per unit), `Current_pu`, and a `Fault_Location` target identifier.

### 6. LANL Open Source Grid Events
* **Description:** Contingency and line outage data used for grid topology studies and cascading failure analysis.
* **Download Link:** [GitHub - PowerModels.jl Data](https://github.com/lanl-ansi/PowerModels.jl)
* **Data Statistics:** Covers various standard IEEE test cases ranging from the 14-bus to the 300-bus systems. 
* **What the Data Sample Looks Like:** Text files in the `.m` (Matpower) format detailing matrix arrays for `bus`, `branch`, `gen` (generators), and network `status` (active/outage).

### 7. ORNL Transmission Signatures
* **Description:** PMU frequency events and wide-area oscillations captured from the US grid, useful for frequency stability analysis.
* **Download Link:** [DOE / ORNL Datasets](https://www.ornl.gov/)
* **Data Statistics:** 60 Hz sampling rate, capturing real-world frequency dips and generator tripping events.
* **What the Data Sample Looks Like:** Time-series tables containing standard synchrophasor data: `Timestamp`, `Frequency_Hz`, and an `Event_Flag`.

### 8. Power System Faults (SCADA)
* **Description:** A dataset mimicking SCADA logs that provides environmental and operational context rather than just raw electrical waveforms.
* **Download Link:** [Kaggle - Power System Faults Dataset](https://www.kaggle.com/datasets/ziya07/power-system-faults-dataset)
* **Data Statistics:** Granular 1-minute interval sampling.
* **What the Data Sample Looks Like:** A tabular `.csv` containing columns for both physical and environmental data: `Voltage`, `Current`, `Temperature`, `Wind_Speed`, and `Maintenance_Status`.
