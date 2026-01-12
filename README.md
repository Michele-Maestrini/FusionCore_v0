<img width="1860" height="417" alt="AX-FC" src="https://github.com/user-attachments/assets/1e6cf905-6252-4c59-8e3e-eed19502efcb" />

# FusionCore

**FusionCore** is an end-to-end temporal intelligence pipeline designed to ingest, fuse, and analyse heterogeneous time-series datasets at scale, with a primary focus on predictive maintenance and system health forecasting for space and aerospace systems.

FusionCore integrates data ingestion, temporal harmonisation, feature construction, and sequence-based time-series modelling into a single, reproducible workflow. The reference modelling implementation uses a **Temporal Fusion Transformer (TFT)** to validate the integrity and usefulness of the fused datasets.

The project is intentionally foundational. Each version builds upon the previous one, enabling the progressive development of more advanced AI technologies for space exploration, including long-duration missions, lunar and Martian operations, and future asteroid mining systems.

---

## Architecture Overview

FusionCore is implemented as a **layered, end-to-end temporal intelligence system**.

### 1. Ingestion Layer (Raw / Bronze)

* Batch ingestion of heterogeneous datasets (time series, events, metadata)
* Immutable preservation of raw source data
* Capture of provenance, ingestion timestamps, and dataset versions
* Support for CSV, Parquet, and JSON formats

**Output:** Source-faithful raw datasets with no silent transformations.

---

### 2. Harmonisation & Quality Layer (Silver)

* Schema validation and schema versioning
* Data quality checks (nulls, ranges, duplicates)
* Canonical identifier mapping (e.g. asset or engine identifiers)
* Temporal standardisation to a canonical time index
* Explicit handling of gaps and irregular sampling

**Output:** Clean, standardised, temporally consistent datasets.

---

### 3. Fusion & Feature Layer (Gold)

* Multi-source temporal alignment using entity keys and time
* Anchor time-series designation
* Construction of model-ready features:

  * Time-varying observed covariates
  * Time-varying known covariates
  * Optional static attributes
* Label generation for degradation modelling (e.g. Remaining Useful Life)

**Output:** Analysis-ready fused datasets suitable for sequence-based modelling.

---

### 4. Modelling Layer (Temporal Fusion Transformer)

* Offline training of a Temporal Fusion Transformer (TFT)
* Grouped sequence modelling (per asset or system)
* Encoder–decoder temporal windows
* Strict prevention of temporal leakage
* Baseline configuration used for validation, not hyper-optimisation

**Output:** Predictive degradation forecasts and model diagnostics.

---

### 5. Evaluation & Reproducibility Layer

* Baseline forecasting metrics (e.g. MAE, RMSE)
* Stability checks across repeated runs
* Full traceability to dataset versions, schemas, and model configurations

---

## Data Lineage & Versioning

FusionCore enforces **explicit data lineage and version control** at every stage of the pipeline.

* **Raw (Bronze):**
  Immutable snapshots of source datasets with ingestion timestamps and dataset identifiers.

* **Clean (Silver):**
  Versioned schemas and validated records; no destructive overwrites.

* **Fused (Gold):**
  Deterministic outputs tagged with:

  * Dataset version
  * Schema version
  * Configuration hash
  * Execution timestamp

All downstream modelling artefacts reference the exact FusionCore dataset version used for training, ensuring full reproducibility.

---

## Model Configuration Summary (TFT)

FusionCore v0 includes a **reference Temporal Fusion Transformer configuration** used to validate fused datasets.

### 1. Purpose

To confirm that FusionCore outputs are structurally and temporally compatible with advanced sequence-based models used in system health and degradation analysis.

### 2. Baseline Configuration

* Model type: Temporal Fusion Transformer
* Framework: PyTorch Forecasting
* Task: Regression (Remaining Useful Life)
* Group identifier: `asset_id` / `engine_id`
* Time index: `cycle` or canonical timestamp
* Encoder window: 30–50 timesteps
* Prediction horizon: 1 timestep (baseline)
* Normalisation: Group-wise (per entity)
* Loss function: MAE or RMSE

### 3. Scope Constraints

* Offline training only
* No real-time inference
* No hyperparameter optimisation beyond baseline
* Model accuracy is not a v0 acceptance criterion

---

## Datasets

FusionCore v0 uses **public, well-documented datasets from leading aerospace research organisations**, ensuring relevance to space-adjacent systems and long-term mission reliability.

### 1. Primary Dataset (Anchor Time Series)

**NASA Turbofan Engine Degradation Dataset (C-MAPSS)**
Provider: NASA Ames Prognostics Center of Excellence

* Multivariate run-to-failure time series
* Multiple sensor channels per engine
* Explicit degradation trajectories
* Widely used benchmark in prognostics research

**Role in FusionCore**

* Anchor time series
* Primary source for temporal fusion and modelling
* Remaining Useful Life (RUL) target generation

---

### 2. Event & Label Data

**Failure and Degradation Annotations (C-MAPSS)**
Provider: NASA Ames Prognostics Center of Excellence

* End-of-life indicators
* Failure cycle annotations

**Role in FusionCore**

* Event alignment
* Supervised learning targets
* Temporal integrity validation

---

## Dataset Download Instructions & URLs

### NASA C-MAPSS (Primary Dataset)

* [NASA PCoE Data Repository:](https://data.nasa.gov/dataset/cmapss-jet-engine-simulated-data)

Download the appropriate `FD00x` dataset archive and place it in the `raw/` directory.

---

## Scope (v0)

FusionCore v0 is an **offline, experimental research system**.
It is **not** a production platform and does not provide real-time inference or automated decision-making.

---

## Long-Term Vision

FusionCore is the foundational intelligence layer for **Astrolytics Xplorion**.
Future systems will extend this core to support increasingly autonomous, resilient AI technologies for space exploration—from Earth orbit to the Moon, Mars, and future asteroid mining operations.

---

