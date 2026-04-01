# Research Plan: MFC Performance Optimization via Simulation and Machine Learning

## Context

Microbial Fuel Cells (MFCs) sit at the intersection of microbiology, electrochemistry, and environmental engineering — capable of simultaneously treating wastewater and generating electricity. Despite decades of research, MFCs remain locked at the pilot/lab scale. The core bottleneck is not material science alone, but the **inability to predict, optimize, and control biological performance** in real-time. Current simulation and machine learning approaches treat the problem in silos: mechanistic models are computationally prohibitive and poorly validated, while ML models are black boxes with no generalizability.

---

## Research Gaps

### Gap 1 — Physics-Informed ML is Absent in MFCs
Physics-Informed Neural Networks (PINNs) have been successfully deployed in PEM fuel cells and bioreactors — but **have never been systematically applied to MFCs**. Current MFC ML models (ANN, LSTM, CatBoost, SVR) ignore the governing electrochemical laws (Butler-Volmer, Nernst, Monod kinetics).

### Gap 2 — ML Models Cannot Generalize Across MFC Configurations
All published ML models are trained on single reactor units with synthetic substrates (acetate). **Zero published work exists on transfer learning across MFC types**. This is the primary barrier to commercialization.

### Gap 3 — No Real-Time Adaptive Control Framework
Existing models are post-hoc (batch prediction only). **No closed-loop optimization system** exists that continuously adapts operational parameters in response to biofilm state changes.

### Gap 4 — Multi-Scale Modeling is Fragmented
CFD models (COMSOL, LBM), biofilm kinetic models, and ML models all exist — but **no integrated multi-scale surrogate** couples microscale biofilm dynamics with macroscale electrochemical performance.

### Gap 5 — No Multi-Objective Pareto Optimization of MFCs
No study has simultaneously optimized power density, COD removal, and internal resistance across all key operating parameters using a systematic DOE + surrogate approach.

---

## Problem Statement

MFC performance is governed by a tightly coupled multi-physics system (electrochemistry + microbial kinetics + mass transport + fluid dynamics) that is inherently nonlinear, spatially heterogeneous, and temporally dynamic. Current models cannot:
1. Make physically consistent predictions with limited data
2. Generalize from one MFC configuration to another
3. Enable real-time operational optimization

This prevents scale-up, increases costs (30× higher than conventional treatment), and leaves MFC technology confined to the laboratory.

---

## Novelty

### Novelty 1 — First HyperStudy-Based Surrogate Optimization for MFCs
Use Altair HyperStudy (DOE + Kriging surrogate) to build the first systematic multi-objective optimization framework for MFCs — a tool widely used in automotive/aerospace but never applied to bioelectrochemical systems.

### Novelty 2 — Multi-Objective Pareto Front for MFC Design Space
Simultaneously optimize: Power density (max) + COD removal (max) + Internal resistance (min). Generate a Pareto front revealing design trade-offs across 7 operating parameters.

### Novelty 3 — Surrogate-Based Closed-Loop Control (Altair Activate)
Use the AI Studio surrogate as a "digital plant model" inside an Altair Activate control loop. Simulate PID/MPC controllers adapting to substrate fluctuations and disturbances.

### Novelty 4 — SHAP-Based Mechanistic Insight
Apply SHAP feature importance via AI Studio to quantify the relative contribution of biological vs. physical parameters — providing explainable, actionable design rules.

---

## Methodology

### Phase 1 — COMSOL: High-Fidelity MFC Model
- Build 2D coupled model: Butler-Volmer electrochemistry + Monod biofilm + Fick's Law diffusion + Laminar flow CFD
- Validate against published polarization curves
- Run parametric sweeps across 7 parameters (see table below)

**Input Parameters:**

| Parameter | Range |
|-----------|-------|
| Temperature | 20–40°C |
| pH | 6.0–8.0 |
| External resistance | 10–1000 Ω |
| HRT | 6–48 h |
| Substrate concentration | 0.5–5 g COD/L |
| Electrode surface area | 10–100 cm² |
| Electrode spacing | 1–10 cm |

**Outputs:** Power density, voltage, COD removal, internal resistance, coulombic efficiency

### Phase 2 — HyperStudy: DOE + Surrogate + Optimization
1. Latin Hypercube Sampling (~300–500 runs)
2. Kriging surrogate model (target R² > 0.98)
3. Multi-objective optimization → Pareto front

### Phase 3 — AI Studio: ML + Explainability
1. Train: DNN, Gradient Boosting, Random Forest, SVR
2. SHAP feature importance analysis
3. Scenario and sensitivity analysis

### Phase 4 — Compose: Post-Processing
- Fit simplified design equations to Pareto results
- Automate COMSOL–HyperStudy data pipeline

### Phase 5 — Activate: Control Simulation
- Build MFC control loop (surrogate as plant)
- Compare: open-loop vs. PID vs. MPC
- Simulate disturbance rejection (substrate fluctuations)

---

## Key Performance Targets
- Surrogate model R² > 0.98 vs. COMSOL
- ML model R² > 0.95 on held-out test set
- MPC controller improves power density > 20% vs. fixed parameters
- Surrogate prediction time < 1 second (real-time capable)

---

## Publication Plan

| Paper | Journal | Focus |
|-------|---------|-------|
| Paper 1 | Bioresource Technology | COMSOL model + validation |
| Paper 2 | Renewable Energy | HyperStudy surrogate + Pareto optimization |
| Paper 3 | Journal of Power Sources | AI Studio ML + Activate control simulation |
