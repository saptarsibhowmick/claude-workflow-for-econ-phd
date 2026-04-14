# Logging Rule — Always On

## Session Logging — 3 Triggers

1. **After plan approval** — Create session log with goal, plan summary, rationale
2. **During implementation** — Append 1–3 lines as key decisions happen
3. **At session end** — Add accomplishments, open questions, where to pick up

## [LEARN] Tag Protocol

When the author corrects Claude, capture it immediately:

```
[LEARN:tag] Correction text. Discovered YYYY-MM-DD session N.
```

Tags should be searchable categories: `stata`, `r-plotting`, `clustering`, `data`, `latex`, `notation`.

The `/tools learn` command can be used to extract corrections from a session log and append them to MEMORY.md.

## Research Journal

Each paper maintains `quality_reports/research_journal.md` — a running timeline of phase transitions, major decisions, and score changes.

## Deprecation Logging

Every deprecation operation must be logged in the local `_deprecation-log.md`. See file-safety rule for format.
