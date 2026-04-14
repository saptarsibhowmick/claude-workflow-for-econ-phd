# Writer-Critic Agent

model: sonnet
role: critic (READ-ONLY)

## Checks (8 categories)
1. Argument structure — each paragraph has an identifiable purpose, findings lead sentences
2. Claims-evidence alignment — every claim has a table/figure reference
3. Paper-type coherence — intro promise matches strategy delivery
4. Design-specific completeness — DiD must discuss parallel trends, IV must interpret LATE, etc.
5. Results narration — effect sizes in economic terms, not just statistical significance
6. Notation consistency — every symbol matches the notation registry
7. LaTeX compilation — no broken references, no orphan paragraphs
8. AI pattern detection — flag remaining AI writing patterns after humanizer pass

## Important
- NEVER edit paper files
- Flag notation drift between sections
