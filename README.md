<img width="273" height="121" alt="FusionCore" src="https://github.com/user-attachments/assets/692079cc-0f95-4386-bf88-2256625293c6" />


# FusionCore: Risk-Aware Predictive Maintenance System

**FusionCore** is a research-led benchmarking framework designed to solve the "Cold Start" and "Regime Shift" problems in aerospace prognostics. Unlike standard RUL regressors, FusionCore evaluates the trade-off between **Model Explainability** (TFT) and **Inference Latency** (TSMixer) to determine the optimal deployment architecture for edge-constrained environments.

---

## 1. Executive Summary

Predictive maintenance in safety-critical domains (Aerospace, Space) requires more than just low RMSE. It demands **reliability under regime shift** and **interpretability for human engineers**.

FusionCore v0 establishes a rigorous "Ground Truth" by benchmarking three distinct architectural paradigms against the NASA CMAPSS Gold Standard. The goal is not just to predict failure, but to de-risk the architectural decision-making process for future industrial deployment.

---

## 2. The Problem

Standard deep learning models often fail in real-world industrial settings due to two critical blind spots:

1. **Non-Stationarity:** Sensor data drifts over time independent of faults (e.g., sensor aging vs component aging).
2. **Regime Blindness:** Models mistake high-altitude cruise conditions for engine failure because they lack context-aware normalisation.

**The FusionCore Hypothesis:**

> *A physics-informed hybrid architecture that explicitly models operating regimes will outperform "black box" Deep Learning models in false-positive rates, even if RMSE is similar.*

---

## 3. The Solution (FusionCore v0)

We benchmark three SOTA paradigms to cover the "Startup Value Triangle" of Speed, Accuracy, and Simplicity.

| Architecture | Role | Why This Model? |
| --- | --- | --- |
| **AutoGluon (TimeSeries)** | **The Baseline** | An automated ensemble of statistical (ARIMA/ETS) and tree-based models. Acts as the "sanity check"—if Deep Learning cannot beat this, it is not worth deploying. |
| **Temporal Fusion Transformer (TFT)** | **The Glass Box** | An attention-based architecture that offers **interpretability**. It allows us to visualise exactly which sensors the model focuses on as the engine degrades. |
| **TSMixer (Google)** | **The Speed King** | An all-MLP architecture that offers comparable accuracy to Transformers but with significantly lower **inference latency**, making it ideal for embedded/edge deployment. |

---

## 4. Key Results (Phase 0 Diagnostics)

*Prior to training, our extensive EDA (see `docs/technical_report_v0.pdf`) revealed:*

* **Regime Shift:** In dataset FD002, engines cycle through 6 distinct operating clusters. Random splitting results in **Data Leakage**.
* *Mitigation:* Implemented strict **Unit-Wise Splitting** protocols.


* **Sensor Redundancy:** Sensors 1, 5, 10, 16, 18, and 19 exhibit zero variance and are removed to improve Signal-to-Noise Ratio (SNR).
* **Stationarity:** Sensors T24 (LPC Temp) and T30 (HPC Temp) exhibit non-stationary trends that correlate with RUL, validating their use as primary features.

---

## 5. Repository Structure

```text
FusionCore/
├── docs/                  # Technical deep-dives and PDF reports
│   ├── technical_report_v0.pdf
│   └── benchmarking_protocols.pdf
├── notebooks/             # Exploratory Data Analysis & Experiments
│   ├── 01_EDA_Diagnostics.ipynb    # Initial sensor analysis
│   ├── 02_EDA_Regimes.ipynb        # Stationarity & Regime math (The "Missing Maths")
│   └── 03_Benchmark_Comparison.ipynb
├── src/                   # Modular source code
│   ├── data/              # Data loaders and regime-normalisation logic
│   └── models/            # TFT, TSMixer, and AutoGluon definitions
├── requirements.txt       # Python dependencies
└── README.md              # This file

```

---

## 6. Usage

To reproduce the regime analysis:

```bash
# 1. Install dependencies
pip install -r requirements.txt

# 2. Run the Regime Diagnostics
jupyter notebook notebooks/02_EDA_Regimes.ipynb

```

---

## 7. Roadmap

* **Phase 0 (Current):** SOTA Benchmarking & Diagnostic EDA.
* **Phase 1:** Physics-Informed Hybridisation (Injecting Thermodynamic Ratios).
* **Phase 2:** Scaling to N-CMAPSS (2021) using PySpark/BigQuery.
* **Phase 3:** **FusionScale** – Agentic AI & RAG for automated maintenance prescriptions.

---

## 8. Author

**[Your Name]**
*MSc Data Science | Specialising in Aerospace Predictive Maintenance*
[Link to your Portfolio/LinkedIn]

---

**Next Step:** Once you have saved this file, we should generate the **Python Code** for `notebooks/02_EDA_Regimes.ipynb` to fill the "Missing Maths" gap mentioned in Section 4. **Shall I generate that code now?**
