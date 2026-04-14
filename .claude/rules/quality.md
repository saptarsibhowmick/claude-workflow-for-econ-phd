# Quality Gates — Always On

## Scoring Thresholds

| Score | Threshold | Action |
|---|---|---|
| 80+ | Commit | `git commit` allowed |
| 90+ | Push | `git push` to remote |
| 95+ | Submission | Paper ready for journal |
| < 80 | Blocked | Must fix before committing |

## Score Deductions

| Issue | Deduction | Category |
|---|---|---|
| Code does not run end-to-end | -30 | Critical |
| Results differ across languages (>6 decimal places) | -25 | Critical |
| Missing value handling error | -20 | Critical |
| No set.seed() in stochastic code | -15 | Major |
| Hardcoded absolute paths | -15 | Major |
| Outputs not programmatically generated | -15 | Major |
| Missing variable documentation in codebook | -10 | Major |
| Prohibited code patterns (setwd, sapply on df, T/F) | -10 | Major |
| Notation inconsistency with registry | -5 | Minor |
| Console print statements in production code | -3 | Minor |

## Mandatory Verification

Claude cannot report a task as "done" without:
1. Running the code (or confirming it runs)
2. Checking that output files are fresh (timestamps match the run)
3. Scoring against the relevant gate
