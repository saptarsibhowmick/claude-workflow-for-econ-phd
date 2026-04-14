---
name: research-ideas
description: "Generate empirical research questions based on existing literature and data landscape."
---

# Research Idea Generator

## When to Use
After major literature additions, or when looking for new directions.

## Steps

1. **Read** all `@*.md` notes in `literature/zotero-notes/` — extract YAML frontmatter (citekey, paper_type, tags, authors, year, journal) and note content
2. **Also read**: `literature/missing-lit.md`, existing strategy memos, `literature/synthesis/frontier-map.md`, `.claude/references/domain-profile.md`
3. **Generate ideas**, requiring for each:
   - **Research question** (one sentence)
   - **Empirical strategy** (DiD/IV/RDD/SC + what provides variation)
   - **Data feasibility** (what exists, what's accessible, what's missing)
   - **Contribution** (what's new relative to the frontier)
   - **Feasibility score** (1–5: 1 = publishable with existing data, 5 = data may not exist)
   - **Target journal** (based on journal-profiles.md)
   - **Relation to existing papers** (complement, extension, or independent)
4. **Append** to `literature/research-ideas.md` with date stamp

## Output Format

Prepend to `literature/research-ideas.md`:

```markdown
## YYYY-MM-DD — Research Ideas

### Idea 1: [One-sentence question]
- **Strategy:** [Estimator + variation source]
- **Data:** [Dataset(s) + accessibility]
- **Contribution:** [What's new]
- **Feasibility:** [N]/5
- **Target journal:** [Journal name]
- **Relation:** [How it connects to Papers 1–3]

### Idea 2: ...
```

## Important
- Follow append-only protocol
- Flag ideas that complement existing three objectives
- Be specific about identification — "use DiD" is insufficient; specify what provides the treatment variation
