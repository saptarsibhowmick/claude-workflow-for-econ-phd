# Notation Registry

> All writing and review agents read this file. Prevents notation drift across papers.
> Fill in as you establish conventions. Add rows as needed.

## Core Variables

| Symbol | Meaning | Introduced In | Anti-pattern |
|---|---|---|---|
| $D_i$ | [e.g., Binary treatment indicator] | [Paper N, Section N] | [e.g., Never $T_i$ or $W_i$] |
| $Y_{it}$ | [e.g., Outcome variable] | | |
| $X_{it}$ | [e.g., Control vector] | | |
| $Z_i$ | [e.g., Instrument] | | |

## Subscript Conventions

| Subscript | Meaning |
|---|---|
| $i$ | [e.g., Unit — individual, household, or district depending on paper] |
| $t$ | [e.g., Time period] |
| $g$ | [e.g., Group / cohort] |
| $j$ | [e.g., Origin country or region] |
| $d$ | [e.g., District] |

## Operator Conventions

| Notation | Meaning | Anti-pattern |
|---|---|---|
| $\mathbb{E}[\cdot]$ | Expectations | Never $E[\cdot]$ |
| $\text{Var}(\cdot)$ | Variance | |
| $\hat{\tau}$ | Estimated treatment effect | |

## Standard Error Reporting

- Clustered at the level of treatment assignment
- Report clustering level in every table note
- Parentheses below coefficient
- Stars: \* p<0.10, \*\* p<0.05, \*\*\* p<0.01

## Paper-Specific Notation

### Paper 1
[Add paper-specific symbols here]

### Paper 2
[Add paper-specific symbols here]

### Paper 3
[Add paper-specific symbols here]
