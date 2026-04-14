# File Safety Rule — Always On

## The Core Rule

Claude NEVER deletes or modifies any existing file. Every change creates a fresh file.

## Deprecation Procedure

To update any file:
1. MOVE existing file to `_deprecated/` in the same directory with prefix `YYYY-MM-DD_`
2. CREATE the new version fresh at the original path
3. APPEND an entry to `_deprecation-log.md` in the same directory
4. If `_deprecated/` or `_deprecation-log.md` do not exist, create them

## Deprecation Log Entry Format

```markdown
## YYYY-MM-DD · filename.ext
- **Reason**: [Why the file was updated]
- **Deprecated to**: _deprecated/YYYY-MM-DD_filename.ext
- **Session**: session-logs/YYYY-MM-DD_session-N.md
- **Breaking changes**: [Any downstream effects]
```

## File Tiers

### Tier 1: Permanently Immutable (NEVER touched)
- `data/raw/*` — Source data
- `data/resources/*` — Source documents
- `data/raw/restricted/*` — IRB/DUA-restricted data (also NEVER read)
- `code/replication/*` — Referee 2's scripts
- `correspondence/*` — All reports and responses
- `session-logs/*` — Session history

### Tier 2: Deprecate-and-Replace (standard workflow)
- `code/R/*.R`, `code/python/*.py`, `code/stata/*.do`
- `data/processed/*`, `data/codebook/*`
- `literature/zotero-notes/*`, `literature/synthesis/*`
- `paper/*`, `presentations/*`
- `pre-analysis-plan/*`
- `CLAUDE.md`, `MEMORY.md`

### Tier 3: Regenerable Outputs (batch deprecation before re-run)
- `output/tables/*`, `output/figures/*`, `output/logs/*`

### Tier 4: Append-Only (content accumulates, nothing removed)
- `literature/missing-lit.md`
- `literature/research-ideas.md`
- `bibliography.bib`
- `_deprecation-log.md` files
