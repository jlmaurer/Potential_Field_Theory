# Geophys 5432 — Potential Field Theory in Geophysics

Course materials for **Geophys 5432**, including Python lab notebooks and homework assignments organized by module.

## Repository contents

| Path | Description |
|---|---|
| `labs/M*/` | Jupyter lab notebooks (one per module) |
| `homeworks/M*/` | Homework assignments in Quarto (`.qmd`) and compiled PDF |
| `datasets/M*/` | Data files used by the labs |
| `projects/` | Final project description and starter notebook |
| `Geophys5432_Syllabus.qmd` | Course syllabus source |
| `Geophys5432_Course_Outline.qmd` | Week-by-week course outline source |

## Modules

| Module | Topic |
|---|---|
| M0 | Mathematical & Python foundations |
| M1 | Potential fields and Green's identities |
| M2 | Newtonian gravity and applications |
| M3 | Geomagnetism and crustal magnetic anomalies |
| M4 | Spherical harmonic analysis |
| M5 | Forward modeling and inversion |
| M6 | Spectral methods and field transformations |
| M6.5 | Fourier continuation and phase transforms |
| M7 | Capstone project — regional geoid analysis |

## Getting started

### Prerequisites

- Python 3.10+ with `numpy`, `scipy`, `matplotlib` (and optionally `pyshtools` for M4)
- [Quarto](https://quarto.org/) to render `.qmd` homework files

### Set up a Python environment

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install numpy scipy matplotlib jupyter pyshtools
```

### Run a lab notebook

```bash
jupyter notebook labs/M0/lab0.ipynb
```

### Render a homework PDF

```bash
quarto render homeworks/M1/homework1.qmd
```

## License

[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE) — free to use, adapt, and redistribute with attribution.
