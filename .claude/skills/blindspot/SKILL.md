---
name: blindspot
description: "Peripheral vision audit — find what the author has become blind to in their results. Run in a FRESH TERMINAL."
---

# Blindspot Audit

> Based on Scott Cunningham's Blindspot skill (MixtapeTools).
> The Shklovsky Principle: by the time you've spent months on a paper, the main finding has collapsed your attention. Blindspot makes the stone stony again.

## CRITICAL: Fresh Terminal Required

This skill MUST be run in a new Claude Code session with no prior context from the authoring sessions. The separation is what makes it work — the auditing Claude has no prior commitments to the author's narrative.

## Steps

1. **Read the paper** in `paper-N/paper/main.tex` or the latest draft
2. **Read all output**: tables in `output/tables/`, figures in `output/figures/`
3. **Read the strategy memo**: `pre-analysis-plan/strategy-memo.md`
4. **Read the codebook**: `data/codebook/variables.md`, `data/codebook/sample.md`
5. **Apply the Blindspot Grid** (four quadrants):

### The Blindspot Grid

| | Things Present in Output | Things Absent from Output |
|---|---|---|
| **Vices** (problems) | Anomalies normalized — outliers not questioned, coefficient signs rationalized, patterns dismissed as noise | Checks never run — subgroups not split, placebo tests missing, robustness not attempted |
| **Virtues** (opportunities) | Richness ignored — heterogeneity patterns, mechanism evidence in appendix tables, interesting coefficients on controls | Extensions not considered — natural next questions the data can answer, adjacent literatures not connected |

6. **For each finding**, document:
   - What was found (specific table/figure/coefficient)
   - Which quadrant it falls in
   - Why the author likely missed it
   - Recommended action (investigate, discuss, add, remove)
   - Severity (critical / important / minor)

7. **File the report** in `paper-N/correspondence/blindspot/YYYY-MM-DD_blindspot-report.md`

## Output Format

```markdown
# Blindspot Report — Paper [N]
Date: YYYY-MM-DD

## Vices — Problems Hiding in Plain Sight
### [Finding 1]
- **Location:** Table 3, Column 4
- **Issue:** [Description]
- **Why missed:** [Author likely focused on...]
- **Action:** [Investigate / discuss / remove]
- **Severity:** Critical

## Vices — Checks Never Run
### [Finding 1]
...

## Virtues — Richness Being Ignored
### [Finding 1]
...

## Virtues — Extensions Not Considered
### [Finding 1]
...

## Summary
[N] findings: [X] critical, [Y] important, [Z] minor.
```

## Important
- NEVER modify author files — read only
- File the report in correspondence/blindspot/ — this is an immutable record
- The author responds in a separate response file
