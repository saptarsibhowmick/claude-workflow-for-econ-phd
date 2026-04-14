---
path: "**/code/python/**"
---

# Python Code Conventions

## Script Structure
- Numbered prefix: `00_master.py`, `01_clean.py`, etc.
- `00_master.py` runs all scripts via `subprocess` or `exec`
- Type hints on function signatures
- Docstrings on all functions

## Required Patterns
- `numpy.random.seed()` or `random.seed()` before stochastic operations
- `pathlib.Path` for all file paths (no string concatenation)
- `pandas` for data manipulation, `statsmodels` or `linearmodels` for estimation
- Explicit NA handling with documented decisions
- Virtual environment or `requirements.txt` for reproducibility

## Prohibited Patterns
- Hardcoded absolute paths
- `print()` in production code (use `logging`)
- Bare `except:` clauses
- Mutable default arguments

## Output
- Tables via `stargazer` (Python port) or formatted DataFrames to LaTeX
- Figures via `matplotlib` or `seaborn` — save to `output/figures/`
