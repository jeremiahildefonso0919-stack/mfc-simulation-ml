# MFC Simulation & ML Optimization

An integrated simulation-optimization framework for Microbial Fuel Cell (MFC) performance enhancement using multi-physics modeling and surrogate-based machine learning.

## Research Overview

**Problem:** MFC performance is governed by a tightly coupled multi-physics system (electrochemistry + microbial kinetics + mass transport + fluid dynamics) that is nonlinear, spatially heterogeneous, and temporally dynamic. No existing framework can simulate MFC behavior across scales, predict performance degradation, and enable real-time optimization.

**Approach:** COMSOL Multiphysics for high-fidelity simulation → Altair HyperStudy for DOE and surrogate modeling → Altair AI Studio for ML → Altair Activate for closed-loop control simulation.

## Project Structure

```
mfc-simulation-ml/
├── comsol/                  # COMSOL model files (.mph)
├── hyperstudy/              # HyperStudy study files and DOE results
├── ai-studio/               # Altair AI Studio model exports
├── activate/                # Altair Activate control simulation models
├── data/
│   ├── raw/                 # Raw simulation outputs
│   ├── processed/           # Cleaned datasets for ML
│   └── experimental/        # Literature experimental data for validation
├── scripts/                 # Python post-processing and analysis scripts
├── results/                 # Figures, tables, Pareto fronts
├── docs/                    # Research notes, literature review
└── README.md
```

## Key Research Gaps Addressed

1. **No multi-objective Pareto optimization** of MFCs across all operating parameters simultaneously
2. **No surrogate-model-based control** framework for real-time MFC optimization
3. **Altair HyperStudy never applied** to bioelectrochemical systems
4. **No closed-loop control simulation** using data-driven surrogate as plant model

## Tools

| Tool | Purpose |
|------|---------|
| COMSOL Multiphysics | Multi-physics MFC model (electrochemical + biofilm + CFD) |
| Altair HyperStudy | DOE, Kriging/RBF surrogate, Pareto optimization |
| Altair AI Studio | ML model training, SHAP feature importance |
| Altair Compose | Mathematical post-processing, scripting |
| Altair Activate | Closed-loop PID/MPC control simulation |

## Target Journals

- *Bioresource Technology* — COMSOL model + validation
- *Renewable Energy* — HyperStudy surrogate + Pareto optimization
- *Journal of Power Sources* — ML model + control simulation

## Status

- [ ] Phase 1: COMSOL multi-physics model development and validation
- [ ] Phase 2: HyperStudy DOE and surrogate model construction
- [ ] Phase 3: AI Studio ML model training and feature importance analysis
- [ ] Phase 4: Compose post-processing and design rule derivation
- [ ] Phase 5: Activate closed-loop control simulation
