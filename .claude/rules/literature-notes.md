# Literature Notes Integration — Always On

## Architecture

```
literature/zotero-notes/          ← MASTER: all notes live here
    @becker2019.md
    @facchini2006.md
    ...

paper-1/literature/zotero-notes/  ← COPIES of notes relevant to Paper 1
paper-2/literature/zotero-notes/  ← COPIES of notes relevant to Paper 2
...
```

**Master notes** are created in `literature/zotero-notes/` by reading PDFs from
Zotero. **Paper-level copies** are made by Claude when a note is relevant to a
specific paper. The master copy is the source of truth — paper-level copies are
for convenience and context.

## How Notes Are Created

The workflow uses the **zotero-to-obsidian** methodology (adapted for filesystem):

1. User provides a Better BibTeX citekey (e.g., `@becker2019`)
2. Claude searches Zotero via MCP (`zotero_search_items`), verifies the citekey
3. Claude extracts the PDF path from the bibtex `file` field
4. The PDF is accessed from the user's **Zotero Library folder**. The path
   is stored in `literature/zotero-config.md` (configured during `/setup`).
   Read this config file to get the `pdf_folder` path before attempting PDF
   access. PDFs are NOT stored in this project. **Desktop Commander MCP** is
   recommended for reliable filesystem access to the Zotero Library folder
   ([github.com/wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP)).
5. The PDF is split into 4-page chunks using PyPDF2
6. Chunks are read in batches of 3 (~12 pages), with running notes updated after each batch
7. The paper is classified (empirical, theoretical, review, methodological, report, mixed)
8. Information is extracted using the type-dependent template (A–F)
9. The structured note is written to `literature/zotero-notes/@{citekey}.md`

## Note Filename Convention

All notes: `@{bbt_citekey}.md` (e.g., `@becker2019.md`, `@facchini2006.md`)

## YAML Frontmatter Format (Do Not Deviate)

```yaml
---
title: "{Full Paper Title}"
citekey: {BBT citekey}
authors:
  - {Author 1}
  - {Author 2}
year: {YYYY}
journal: "{Journal Name}"
volume: {volume number}
issue: {issue number}
pages: "{page range}"
doi: "{DOI}"
zotero_key: {Zotero Item Key}
paper_type: {empirical|theoretical|review|methodological|report|mixed}
tags:
  - {tag1}
  - {tag2}
---
```

Rules:
- `citekey`, `zotero_key`, `paper_type`: unquoted
- `title`, `journal`, `doi`, `pages`: quoted (double quotes)
- `volume`, `issue`, `year`: numeric, unquoted
- No `pdf:` field, no `date_analysed:` field
- Omit `volume`, `issue`, `pages` if not available (don't leave blank)

## Note Heading

After YAML frontmatter:
```
# {Author(s)} ({Year}) — {Short Title}
```

Then the extraction sections from the appropriate template (see below).

## Tag Conventions

All tags lowercase kebab-case. Categories:
- **Paper type**: `empirical`, `theoretical`, `review-paper`, `methodological`, `report`, `mixed-theory-empirical`
- **Topic**: `forced-migration`, `refugee-labour-market`, `social-cohesion`, `displacement`, `human-capital`
- **Method**: `DiD`, `IV`, `RDD`, `RCT`, `structural-estimation`, `panel-data`
- **Geography**: `Germany`, `Turkey`, `Colombia`
- **Data**: `SOEP`, `census`, `admin-data`, `satellite-data`

Tags are for linking and filtering. No one-off tags.

## Extraction Templates (6 Types)

- **A: Empirical** — research question, identification strategy, data (be maximally specific: dataset name, source, unit, N, time period, variables), empirical methods (specification, FE, clustering), results (with numbers: $\hat{\beta}$, SE, table/column), robustness, contribution, replication feasibility
- **B: Theoretical** — question, model setup, key assumptions, propositions/theorems, comparative statics, calibration, limitations, contribution
- **C: Review** — scope, taxonomy, key findings across studies, methodological patterns, gaps identified, key references to follow up
- **D: Methodological** — problem, proposed method, theoretical properties, Monte Carlo, empirical illustration, practical guidance, limitations, contribution
- **E: Report** — topic, key facts (with numbers), evidence synthesised, policy implications, data sources, gaps
- **F: Mixed** — all of Template B + sections 2–8 of Template A with bridging section

## PDF Splitting Methodology

Papers are split into 4-page chunks using PyPDF2, then read in batches of 3 splits
(~12 pages per batch). After each batch, extracted information is written to running
notes before proceeding to the next batch. This:
- Forces focused engagement (prevents skimming)
- Creates checkpoints (errors caught before next batch builds on them)
- Accumulates detail rather than summarizing
- Controls for attention degradation over long documents

This methodology originates from Scott Cunningham's split-pdf skill.

## Copying Notes to Paper Directories

When starting work on a specific paper, Claude should:
1. Read all notes in `literature/zotero-notes/`
2. Identify which notes are relevant to the paper's research question and strategy
3. **Copy** (not move) relevant notes to `paper-N/literature/zotero-notes/`
4. The master copy always stays in `literature/zotero-notes/`
5. If a master note is updated (deprecated-and-replaced), the paper-level copy should also be updated

## Equations and Specificity

- Use LaTeX: `$...$` for inline, `$$...$$` for display
- Reproduce estimating equations, model specifications, key coefficients
- Be specific: "$\hat{\beta} = -0.032$ $(SE = 0.011)$, Table 3, Column 4" beats "they find a negative effect"
- Say "Not reported in the paper" rather than guessing

## What Skills Read From

- `/missing-lit` reads `literature/zotero-notes/` to find gaps
- `/research-ideas` reads `literature/zotero-notes/` to generate questions
- Both output to `literature/` (missing-lit.md, research-ideas.md)
