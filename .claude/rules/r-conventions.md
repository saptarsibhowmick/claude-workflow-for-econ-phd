---
path: "**/code/R/**"
---

# R Code Conventions

## Script Structure
- Numbered prefix: `00_master.R`, `01_clean.R`, `02_construct.R`, etc.
- `00_master.R` sources all scripts in order — single entry point for replication
- One logical task per script

## Prohibited Patterns
- `setwd()` — use relative paths from project root
- `sapply()` on data frames — use `vapply()` or `lapply()`
- `T` / `F` — always `TRUE` / `FALSE`
- `<<-` global assignment
- Hardcoded absolute paths
- `library()` calls inside functions
- `print()` in production code (use `message()` for diagnostics)

## Required Patterns
- `set.seed()` before any stochastic operation
- `library()` calls at the top of each script
- Relative paths from project root throughout
- Explicit `NA` handling — document every decision about missing values
- Function-per-file for reusable logic

## Fixed Effects and Clustering
- Use `fixest::feols()` or `lfe::felm()` for high-dimensional FE
- Cluster at the level of treatment assignment
- Always report clustering level in output

## Output
- Tables via `modelsummary` or `stargazer` — never manual formatting
- Figures via `ggplot2` — no base R plots in production
- All output files written programmatically to `output/`
