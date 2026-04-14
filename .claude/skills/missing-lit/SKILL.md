---
name: missing-lit
description: "Find gaps in the literature based on existing Obsidian notes. Searches for high-quality articles the author may have missed."
---

# Missing Literature Finder

## When to Use
Invoke periodically (every 4–6 weeks) or when starting a new paper chapter. Finds structural gaps in the literature collection.

## Important: Note Location

Literature notes live in `literature/zotero-notes/` in the project directory.
Each note is named `@{citekey}.md` with structured YAML frontmatter.
See `.claude/rules/literature-notes.md` for the exact format.

## Steps

1. **Read all `@*.md` notes** in `literature/zotero-notes/`
   - Each note has YAML frontmatter with: `citekey`, `paper_type`, `tags`, `authors`, `year`, `journal`
   - Tags use lowercase kebab-case: `forced-migration`, `DiD`, `Germany`, etc.
   - Paper types: `empirical`, `theoretical`, `review`, `methodological`, `report`, `mixed`
3. **Extract dimensions from frontmatter and note content:**
   - Topics (from `tags`)
   - Methods (from `tags` — e.g., `DiD`, `IV`, `RDD`)
   - Geographies (from `tags` — e.g., `Germany`, `Turkey`)
   - Datasets (from `tags` and note body)
   - Time periods (from note body)
   - Cited authors (from `authors` field)
4. **Identify structural gaps:**
   - Methods used in related fields but not yet applied to the author's topic
   - Geographic regions with relevant phenomena but no empirical work in the collection
   - Datasets mentioned in papers but not yet exploited
   - Recent working papers (NBER, IZA, CEPR, SSRN) not in the collection
   - Seminal papers from the domain profile not yet in notes
   - Paper types underrepresented (e.g., all empirical, no methodological)
5. **Search** for recent papers in:
   - Top-5 journals + field journals (from journal-profiles.md)
   - NBER working papers
   - IZA discussion papers
   - CEPR discussion papers
   - SSRN
6. **Append findings** to `literature/missing-lit.md` with:
   - Date stamp
   - Paper title, authors, year, source
   - Relevance score (1–5)
   - Why it matters for the dissertation
   - Which paper(s) it's most relevant to
7. **Flag** any paper that could directly challenge or strengthen the author's identification strategy

## Output Format

Prepend new entries to `literature/missing-lit.md` (append-only file):

```markdown
## YYYY-MM-DD — Missing Literature Scan

### Scanned
- Notes folder: {output_folder from config}
- Total notes read: {N}
- Paper types: {N} empirical, {N} theoretical, {N} review, {N} methodological
- Geographies covered: {list}
- Methods covered: {list}

### High Priority
- **Author (Year)** "Title" — *Journal*
  Relevance: 5/5. [Why it matters]. Relevant to Paper [N].

### Medium Priority
- ...

### Gaps Identified
[Summary of structural gaps found in this scan]
```

## Important
- Follow the deprecation protocol for append-only files
- Never remove existing entries
- If an entry was wrong, add a correction entry rather than editing
- Respect the existing YAML frontmatter format — do not propose changes to how notes are structured
