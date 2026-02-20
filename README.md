<img width="273" height="121" alt="FusionCore" src="https://github.com/user-attachments/assets/692079cc-0f95-4386-bf88-2256625293c6" />

# FusionCore: Physics-Aware Predictive Maintenance Framework

**FusionCore $v_0$** is a research-led framework designed to solve the "Structural Leakage" and "Uncertainty Quantification" problems in aerospace prognostics. Moving beyond standard regression, FusionCore implements a rigorous **Zero-Leakage Normalisation** pipeline and a **Forensic Validation Gate** to ensure Remaining Useful Life $(RUL)$ estimations are driven by physical thermodynamic degradation signals rather than temporal metadata artefacts.

## 1. Executive Summary

Predictive maintenance in safety-critical domains, such as aerospace operations, demands more than just low Root Mean Square Error $(RMSE)$; it requires **statistical honesty**, **interpretability**, and **quantifiable operational risk**.

FusionCore $v_0$ establishes a mathematically verified "Ground Truth" by subjecting State-of-the-Art $(SOTA)$ deep learning architectures to forensic stress testing against the NASA C-MAPSS dataset (FD001–FD004). The objective is to construct a model that learns the physics of degradation—not merely the passage of time—by explicitly mapping statistical anomalies to empirical aerodynamic efficiency loss and material fatigue.

## 2. The Core Engineering Challenges & Solutions

Standard deep learning models often exhibit "too-good-to-be-true" performance in research settings due to critical structural flaws. FusionCore remediates these through explicit physical grounding:

- **The "Piecewise Linear" Trap:** Assuming engines degrade linearly from cycle 1 mathematically violates fatigue mechanics . FusionCore implements a **Clipped RUL** target (capped at 125 cycles), serving as the algorithmic equivalent of the elastic zone in a stress-strain curve, preventing the model from overfitting to early-life stochastic noise .
- **Regime Blindness:** Models frequently mistake altitude-driven pressure drops for compressor failure. We resolve this via a **Zero-Leakage Normalisation** protocol. $K$-Means clustering identifies flight envelopes exclusively on the training split, and a $Z$-Score transformation decouples environmental variance from mechanical variance .

$$Z=\frac{X_{raw}-\mu_{regime}}{\sigma_{regime}}$$

- **Structural Temporal Leakage:** Time-series models often "cheat" by memorising row indices. FusionCore subjects all feature spaces to a cryptographic sanitisation phase, shuffling targets to prove the absence of temporal leakage.

## 3. The 5-Phase Architecture Pipeline

The repository is structured around a strict 5-phase execution plan:

1. **Exploratory Data Analysis & Physics Grounding:** Isolating true thermodynamic variance from environmental constants using Variance Thresholding $\left(\tau=1\times10^{-5}\right)$.
2. **Zero-Leakage Normalisation:** Unifying multi-regime datasets (FD002, FD004) into a regime-agnostic $Z$-space without forward-looking bias.
3. **Physics-Aware Feature Engineering:** Replacing opaque lags with explicit thermodynamic virtual sensors, such as Compressor Pressure Ratio $\left(CPR=\frac{P_{30}}{P_{24}}\right)$ and Thermal Efficiency Proxies, alongside kinematic derivatives .
4. **The Forensic Stress Test:** Proving data sanitisation using a highly interpretable XGBoost baseline and SHAP values .
5. **SOTA Benchmarking:** Pitting advanced Transformer topologies against probabilistic RNNs via Optuna Bayesian Optimisation (TPE algorithm).

## 4. Benchmarked Architectures

We benchmark three SOTA paradigms to solve the "Reliability Triangle" of Risk, Clarity, and Pattern Recognition. Evaluation goes beyond RMSE, heavily weighting the **NASA Asymmetric Scoring Function** and **Class 2 ($<30$ cycles) Recall** for operational safety .

| **Architecture** | **Role** | **Engineering Rationale** |
| --- | --- | --- |
| **DeepAR** | **The Risk Estimator** | Probabilistic autoregressive RNN. Produces a probability distribution for RUL, allowing for uncertainty bounding ($10^{th}$ to $90^{th}$ percentiles) to assess in-flight failure risk. |
| **Temporal Fusion Transformer (TFT)** | **The Glass Box** | Utilises specific attention mechanisms to provide multi-horizon interpretability. Allows engineers to audit which specific virtual sensors drive the degradation predictions. |
| **PatchTST** | **The Pattern Recogniser** | Segments time-series into semantic "patches" using Channel-Independence. Excels at capturing long-term kinematic trends whilst remaining robust to high-frequency sensor noise. |

## 5. Author

**Michele Maestrini**

Data Science/ML Engineer $||$ Specialising in Aerospace Predictive Maintenance $||$ Time-Series Analysis



[LinkedIn](www.linkedin.com/in/michele-maestrini)
