---
path: "**/code/stata/**"
---

# Stata Code Conventions

## Script Structure
- Numbered prefix: `00_master.do`, `01_clean.do`, etc.
- `00_master.do` runs all scripts in order via `do`
- Version statement at top: `version 17` (or your version)
- `set more off` and `clear all` at script start

## Prohibited Patterns
- Absolute paths — use relative from project root via `global root`
- `cd` to change directories — use full relative paths
- Abbreviations in commands that could be ambiguous

## Required Patterns
- `set seed` before any stochastic operation
- `log using` for all estimation scripts
- `eststo` / `esttab` for table output
- `capture log close` at top of each script
- Explicit merge diagnostics: always check `_merge` and document decisions

## Fixed Effects and Clustering
- Use `reghdfe` for multi-way FE (not `areg` — it drops singletons silently)
- Cluster at the level of treatment assignment
- Report clustering level in all table notes

## Output
- Tables via `esttab` or `outreg2` to LaTeX
- Figures via `graph export` to PDF
- All output written to `output/`
