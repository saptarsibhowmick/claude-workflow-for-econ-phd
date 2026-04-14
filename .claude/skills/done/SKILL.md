---
name: done
description: "End-of-session shutdown sequence. Saves session log, updates MEMORY.md, updates CLAUDE.md, and stages a git commit."
---

# Session Shutdown

> Run this before exiting Claude Code. Handles the full shutdown sequence automatically.

## Steps (execute all in order)

### 1. Write Session Log

Create a new file in `session-logs/YYYY-MM-DD_session-N.md` where N increments
based on how many session logs exist for today.

Contents:

```markdown
# Session Log — YYYY-MM-DD Session N

## Goal
[What was the objective of this session — infer from conversation]

## What Was Done
[List concrete actions taken during this session]

## Decisions Made
[Design choices, variable definitions, specification changes — with rationale]

## Corrections Made
[Any mistakes caught and fixed, or user corrections to Claude's work]

## Open Questions
[Unresolved issues for next session]

## Where to Pick Up
[Exact next step for the next session]
```

### 2. Update MEMORY.md

Scan the conversation for any corrections the user made. For each correction,
append a `[LEARN:tag]` entry to MEMORY.md:

```
[LEARN:tag] Correction text. Discovered YYYY-MM-DD session N.
```

If no corrections were made this session, skip this step and note
"No new [LEARN] entries this session" in the session log.

### 3. Update Paper CLAUDE.md (if applicable)

If working on a specific paper, check whether any key decisions were made:
- New variable definitions
- Specification changes
- Clustering decisions
- Data source additions
- Supervisor-approved decisions

If yes, update the relevant paper's `CLAUDE.md` under "Key Decisions Made":
```
- YYYY-MM-DD: [Decision]. Reason: [Why].
```

Follow the deprecation protocol: deprecate the old CLAUDE.md, create fresh.

### 4. Stage Git Commit

Run:
```bash
git add -A
```

Then report to the user:
```
Session saved. Files staged for commit. Run this to commit and push:

  git commit -m "session YYYY-MM-DD: [brief description]" && git push

You can now exit with /exit or Ctrl+C.
```

Do NOT run `git commit` automatically — the user should review the commit
message and confirm. Only stage the files.

## Important

- Follow ALL file safety rules (deprecation protocol) when updating MEMORY.md and CLAUDE.md
- Follow privacy rules — keep commit message generic, no research details
- This skill replaces the manual shutdown checklist
