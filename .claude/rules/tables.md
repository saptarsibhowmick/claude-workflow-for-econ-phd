---
path: "**/output/tables/**"
---

# Table Conventions

- No embedded titles — titles go in the LaTeX `\caption{}`
- `booktabs` format: `\toprule`, `\midrule`, `\bottomrule` only
- No vertical lines ever
- `threeparttable` for notes below the table
- Standard errors in parentheses below coefficients
- Significance stars: * p<0.10, ** p<0.05, *** p<0.01
- Always report: N, R², clustering level, fixed effects included
- Notes section states: clustering level, fixed effects, control variables
- All tables generated programmatically — no manual formatting
- Dependent variable stated in column header or table note
