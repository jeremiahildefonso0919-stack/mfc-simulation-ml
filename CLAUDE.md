# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a research project — not a software application. The output is scientific papers, simulation models, and data pipelines. There is no build system, test suite, or server to run. Work here involves: editing Python scripts, managing simulation data, and maintaining documentation.

## Repository Structure

- `comsol/` — COMSOL `.mph` model files. These are binary and not human-readable. Changes here happen in the COMSOL GUI, not in code.
- `hyperstudy/` — Altair HyperStudy study files and DOE run outputs.
- `ai-studio/` — Altair AI Studio exported model files.
- `activate/` — Altair Activate control loop models.
- `data/raw/` — Raw COMSOL parametric sweep outputs (CSV). Gitignored except `.gitkeep`; large files stay local.
- `data/processed/` — Cleaned datasets ready for ML training.
- `data/experimental/` — Literature experimental data used for COMSOL model validation.
- `scripts/` — Python scripts for data processing, post-processing COMSOL outputs, and analysis.
- `results/` — Figures, Pareto front plots, tables for publication.
- `docs/` — Research notes and the full research plan (`docs/research-plan.md`).

## Python Scripts

Scripts in `scripts/` are standalone — no shared package or imports between them. Run them directly:

```bash
python scripts/<script_name>.py
```

No virtual environment is pre-configured. Install dependencies as needed per script. Prefer `pandas`, `numpy`, `matplotlib`, `scipy`, and `scikit-learn` for data work.

## Data Flow

```
COMSOL parametric sweep → data/raw/ (CSV)
        ↓
  scripts/ (cleaning, feature engineering)
        ↓
  data/processed/ (CSV, ready for ML)
        ↓
  HyperStudy / AI Studio / scripts/
        ↓
  results/ (figures, tables)
```

## Governing Equations (Reference)

The COMSOL model couples these equations:
- **Butler-Volmer** — anode/cathode electrochemical kinetics
- **Monod kinetics** — substrate consumption and biofilm growth rates
- **Nernst equation** — open-circuit potential
- **Fick's Law** — substrate/product diffusion through biofilm and bulk

COMSOL input parameters and their ranges are defined in `docs/research-plan.md`. Output quantities are: power density (W/m²), cell voltage (V), COD removal (%), internal resistance (Ω), coulombic efficiency (%).

## Git Conventions

Commit after each meaningful unit of work. Message format:

```
<verb> <what> [for <purpose>]

Examples:
  Add COMSOL 2D base model with Butler-Volmer kinetics
  Add HyperStudy LHS DOE with 300 sample points
  Add power density prediction script using processed dataset
  Update research plan with Phase 2 methodology details
```

Always push after committing — this repo is the version-controlled backup of all simulation work.

## Key Research Context

The three novel claims of this work (important when writing scripts or analysis):
1. **First Altair HyperStudy surrogate optimization applied to MFCs** — Kriging surrogate target R² > 0.98
2. **Multi-objective Pareto front** across 7 parameters: maximize power density + COD removal, minimize internal resistance
3. **Surrogate-based closed-loop control** — AI Studio model used as plant in Altair Activate PID/MPC simulation

Performance targets to validate against: surrogate R² > 0.98, ML R² > 0.95, MPC power improvement > 20% vs. fixed parameters.
