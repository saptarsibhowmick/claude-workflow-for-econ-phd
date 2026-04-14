---
name: devils-advocate
description: "Structured debate between two perspectives on a research design decision."
argument-hint: "[decision] [option-A] vs [option-B]"
---

# Devil's Advocate — Structured Design Debate

## When to Use
When uncertain about a design choice: DiD vs synthetic control, instrument A vs instrument B, cluster at district vs province, include control X or not.

## Steps

1. **State the decision** clearly: what is being decided, what are the options
2. **Argue FOR Option A** — the strongest possible case:
   - What assumptions does it require?
   - What makes it the better choice for this specific setting?
   - What would a supportive referee say?
   - What evidence supports it?
3. **Argue FOR Option B** — the strongest possible case:
   - Same structure as above
   - No straw-manning — the best version of this argument
4. **Present the trade-off matrix**:

   | Dimension | Option A | Option B |
   |---|---|---|
   | Assumptions required | | |
   | Robustness to violations | | |
   | Data requirements | | |
   | Reviewer acceptability | | |
   | Precision | | |

5. **Recommendation** (with caveats): which option is stronger and why
6. **Document** the decision and reasoning in `pre-analysis-plan/strategy-memo.md`

## Important
- Ideally run with two separate Claude sessions (one per side) for genuine independence
- The goal is to surface the strongest version of each argument, not to confirm a prior
- Document the decision — future you will want to know why you chose Option A
