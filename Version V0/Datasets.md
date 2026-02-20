# The Datasets

| **Dataset Name** | **Primary Source** | **Link** | **Data Format** | FusionCore Versions |
| --- | --- | --- | --- | --- |
| **NASA C-MAPSS** | NASA PCoE | [Download](https://data.nasa.gov/dataset/cmapss-jet-engine-simulated-data) | Text (`.txt`) | $v_0$ - Research/benchmarking |
| **NASA C-MAPSS** | NASA PCoE | [Download](https://data.nasa.gov/dataset/cmapss-jet-engine-simulated-data) | Text (`.txt`) | $v_1$ - Hybrid model development |
| **NASA N-CMAPSS** | NASA PCoE | [Download](https://www.google.com/search?q=https://data.nasa.gov/dataset/n-cmapss-dataset) | HDF5 (`.h5`) | $v_2$ - Complex dataset |

## 1. C-MAPSS Dataset: Operational Settings, Sensors, and Fault Modes

NASA C-MAPSS (Commercial Modular Aero-Propulsion System Simulation)

We are working with the **FD001, FD002, FD003, and FD004** subsets.

- **Input:** Multivariate time-series data from 21 sensors (Temperatures, Pressures, Speeds) and 3 Operational Settings.
- **Target:** Remaining Useful Life (RUL) in cycles.
- **Challenge:** The data contains complex non-linear degradation, sensor noise, and varying operating regimes.

### 1.2 **Operational Settings (3 total)**

| Setting | Description |
| --- | --- |
| Operational Setting 1 | Sea Level Static (SLS) - Warm day |
| Operational Setting 2 | Sea Level Static (SLS) - Cold day |
| Operational Setting 3 | Cruise conditions (35,000 ft altitude) |

### 1.3 **Sensor Measurements (21 total)**

| Sensor # | Sensor Name | Unit | Description |
| --- | --- | --- | --- |
| 1 | Throttle Resolver Angle (TRA) | % | Throttle resolver angle |
| 2 | Mach Number | N/A | Aircraft Mach number |
| 3 | Altitude | feet | Altitude |
| 4 | Ambient Temperature | °C | Ambient temperature |
| 5 | Ambient Pressure | psia | Ambient pressure |
| 6 | Flight Phase | N/A | Flight phase identifier |
| 7 | Time in Cycle | cycles | Time since the beginning of the cycle |
| 8 | T24 | °R | Temperature at engine station 24 (bypass duct) |
| 9 | T30 | °R | Temperature at engine station 30 (LPC outlet) |
| 10 | T50 | °R | Temperature at engine station 50 (LPT outlet) |
| 11 | P2 | psia | Pressure at engine station 2 |
| 12 | P15 | psia | Pressure at engine station 15 (bypass duct) |
| 13 | P30 | psia | Pressure at engine station 30 (LPC outlet) |
| 14 | Nf | RPM | Corrected fan speed |
| 15 | Nc | RPM | Corrected core speed |
| 16 | Epr | ratio | Engine pressure ratio |
| 17 | Ps30 | psia | Static pressure at engine station 30 |
| 18 | Phi | ratio | Ratio of fuel flow to Ps30 |
| 19 | NRf | RPM | Physical fan speed |
| 20 | NRc | RPM | Physical core speed |
| 21 | BPR | ratio | Bypass ratio |

### 1.4 **Fault Modes (1 per dataset subset)**

| Dataset | Fault Mode | Description |
| --- | --- | --- |
| FD001 | Single fault mode | High-pressure compressor degradation with single failure mode |
| FD002 | Single fault mode | High-pressure compressor degradation with varying operational conditions |
| FD003 | Multiple fault modes | Multiple degradation modes occurring simultaneously |
| FD004 | Multiple fault modes | Multiple degradation modes with varying operational conditions |

### 1.5 **Key Dataset Characteristics**

- **Total number of trajectories**: 100 run-to-failure engine runs per dataset
- **Sensors**: 21 measurement variables (as listed above)
- **Operational conditions**: 3 different operating scenarios
- **Data structure**: Multivariate time-series data with degradation signatures
- **Target variable**: Remaining Useful Life (RUL) - measured in cycles until failure

### 1.6 **Dataset Structure Notes**

The C-MAPSS dataset is organised into four subsets (FD001-FD004) to represent varying complexity levels:

- **FD001 & FD002**: Single fault mode (one type of failure)
- **FD003 & FD004**: Multiple simultaneous fault modes (more realistic scenarios)
- **FD001 & FD003**: Single operating condition
- **FD002 & FD004**: Multiple varying operating conditions

This structure makes C-MAPSS datasets particularly suitable for developing prognostics algorithms, as researchers can test their methods on increasingly complex scenarios from simple single-fault conditions to complex multiple-fault environments with varying operational contexts

## 2. N-CMAPSS Dataset: Operational Settings, Sensors, and Fault Modes

### 2.1 **Operational Settings / Scenario Descriptors (4 total)**

| Setting | Description |
| --- | --- |
| Altitude (Alt) | Altitude at takeoff/cruise |
| Flight Mach Number (Mach) | Aircraft speed relative to sound |
| Throttle Resolver Angle (TRA) | Throttle position setting |
| Total Temperature at Fan Inlet (T2) | Temperature at engine inlet |

### 2.2 **Measured Signals/Physical Sensors (11 total)**

| Sensor # | Sensor Name | Symbol | Description |
| --- | --- | --- | --- |
| 1 | Total Pressure at Fan Inlet | P2 | Pressure at engine station 2 |
| 2 | Total Temperature at Fan Inlet | T2 | Temperature at engine inlet |
| 3 | Pressure at Low Pressure Compressor Outlet | P15 | Pressure at LPC exit |
| 4 | Temperature at Low Pressure Compressor Outlet | T24 | Temperature at bypass duct |
| 5 | Pressure at High Pressure Compressor Outlet | P30 | Pressure at HPC outlet |
| 6 | Temperature at High Pressure Compressor Outlet | T30 | Temperature at HPC outlet |
| 7 | Static Pressure at HPC Outlet | Ps30 | Static pressure at station 30 |
| 8 | Fuel Flow | Wf | Fuel flow rate |
| 9 | High Pressure Rotor Speed | Nc | Core rotor speed |
| 10 | Low Pressure Rotor Speed | Nf | Fan rotor speed |
| 11 | Engine Pressure Ratio | EPR | Total pressure ratio |

### 2.3 **Virtual Sensors (6 total)**

| Sensor # | Virtual Sensor Name | Description |
| --- | --- | --- |
| 1 | Corrected Fan Speed | Nfc |
| 2 | Corrected Core Speed | Ncc |
| 3 | Bypass Ratio | BPR |
| 4 | Burner Fuel-Air Ratio | FAR |
| 5 | Engine Health Index 1 | HI1 |
| 6 | Engine Health Index 2 | HI2 |

### 2.4 **Fault Modes / Failure Modes (7 total)**

| Dataset Subset | Fault Mode Number | Description | Affected Component(s) |
| --- | --- | --- | --- |
| DS01 | Fault Mode 1 | Fan degradation | Fan (with flow/efficiency loss) |
| DS02 | Fault Mode 2 | Low Pressure Compressor (LPC) degradation | LPC (with flow/efficiency loss) |
| DS03 | Fault Mode 3 | High Pressure Compressor (HPC) degradation | HPC (with flow/efficiency loss) |
| DS04 | Fault Mode 4 | Low Pressure Turbine (LPT) degradation | LPT (with flow/efficiency loss) |
| DS05 | Fault Mode 5 | High Pressure Turbine (HPT) degradation | HPT (with flow/efficiency loss) |
| DS06 | Fault Mode 6 | Multiple simultaneous faults | Fan + LPC (compound degradation) |
| DS07 & DS08 | Fault Mode 7 | Multiple simultaneous faults | Multiple components (HPC + LPT, ...) |

### 2.5 **Dataset Structure**

- **Number of engines (units)**: 128 turbofan engines
- **Dataset subsets**: 8 different scenarios (DS01-DS08)
- **Data organisation**: Two sets per subset - Development dataset and Test dataset
- **File format**: HDF5 (.h5 format)
- **Total variables per record**: 17 (4 operational settings + 11 measured signals + 2 RUL/health indicators)

### 2.6 **Data Contents per File:** Each data file contains:

1. **Operative Conditions $(w)$**: 4 scenario-descriptor variables (flight data)
2. **Measured Signals $(z_x)$**: 11 physical sensor measurements
3. **Virtual Sensors $(z_v)$**: 6 virtual/derived sensor values
4. **Engine Health Parameters $(\theta)$**: Model health parameters and degradation indicators
5. **RUL Label**: Remaining Useful Life in flight cycles
6. **Auxiliary Data**: Unit number, flight cycle count, flight class, health state indicators

### 2.7 **Operational Conditions (Flight Data):**

- Real flight data recorded from commercial aircraft operations
- Three flight classes based on length:
    - Short flights
    - Medium flights
    - Long flights ($> 10,000$ feet altitude)

## 3. **Key Differences from C-MAPSS:** The N-CMAPSS dataset extends C-CMAPSS by:

- Using **real flight data** instead of purely simulated data
- Providing **multiple simultaneous fault modes** (7 vs. 1 per subset in C-CMAPSS)
- **Extended degradation modeling** across 5 rotating sub-components (vs. 2 in C-CMAPSS)
- **Virtual sensors** derived from the CMAPSS model outputs
- **Real operational variability** from commercial flight conditions
- **128 unique aircraft units** reflecting realistic fleet diversity

This makes N-CMAPSS significantly more representative of real-world prognostics challenges and is particularly valuable for developing algorithms that can handle complex, multi-fault degradation scenarios under varying operational conditions.

---
