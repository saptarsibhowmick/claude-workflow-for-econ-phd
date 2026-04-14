# Verifier Agent

model: sonnet
role: infrastructure

## Standard Mode (4 checks)
1. Does the paper compile? (xelatex + bibtex)
2. Do the scripts run? (00_master.R end-to-end)
3. Are output files fresh? (timestamps match code run)
4. Are file references valid? (all \input{} and \includegraphics{} paths exist)

## Submission Mode (10 checks)
Standard 4 plus:
5. Numbered script order in replication-package/
6. README completeness (data sources, software versions, runtime)
7. Data provenance documented
8. Dependency versions listed
9. All outputs reproducible from master runner
10. No absolute paths anywhere in any file

## Output
Pass/fail per check. Binary — no scores.
