# Usage Guide

Day-to-day workflow, commands, agents, and verification protocols.

---

## The Workflow Loop

Every session follows the same pattern:

```
Start session → Read context → Spec (if complex) → Plan → Execute → Verify → Log → End
```

### Starting a Session

```bash
cd claude-workflow-for-econ-phd    # or cd paper-1/ for paper-specific work
claude
```

Claude auto-reads `CLAUDE.md` and `MEMORY.md`. Your first message should either be:
- `"Read session-logs/ and tell me where we left off."` (continuing work)
- `"Today's goal: [specific, bounded task]."` (new task)

### Ending a Session

Run the shutdown skill:

```
/done
```

This automatically:
1. Writes a session log to `session-logs/`
2. Updates MEMORY.md with any `[LEARN]` corrections from this session
3. Updates the paper's CLAUDE.md if key decisions were made
4. Stages all files with `git add -A`

Then review and commit:
```bash
git commit -m "session YYYY-MM-DD: [brief description]" && git push
```

Then `/exit` or `Ctrl+C`.

---

## Commands

| Command | What It Does | When to Use |
|---|---|---|
| `/setup` | Check Zotero, configure project, generate paper dirs | Once at start |
| `/done` | End-of-session shutdown — log, MEMORY.md, commit | Every session end |
| `/missing-lit` | Scan literature for gaps | Every 4–6 weeks |
| `/research-ideas` | Generate empirical questions | After major lit additions |
| `/blindspot` | Peripheral vision audit (FRESH TERMINAL) | After results, before writing |
| `/referee2` | Full 5-audit verification (FRESH TERMINAL) | Before submission |
| `/new-paper [N] [topic]` | Scaffold a new paper directory | Once per paper |
| `/deprecate [file] [reason]` | Safely deprecate a file | When updating any file |
| `/devils-advocate [A] vs [B]` | Structured design debate | Major design decisions |

---

## Agents

### Worker-Critic Pairs

| Phase | Worker | What It Creates | Critic | What It Checks |
|---|---|---|---|---|
| Strategy | Strategist | Strategy memo, PAP | Strategist-critic | Assumptions, inference, design |
| Execution | Coder | Analysis scripts | Coder-critic | 16 checks incl. numerical discipline |
| Writing | Writer | Paper sections | Writer-critic | 8 checks incl. argument structure |

### Peer Review Agents

| Agent | Role | Focus |
|---|---|---|
| Editor | Desk review | Scope, referee assignment, editorial decision |
| Domain-referee | Blind review | Contribution, literature, external validity |
| Methods-referee | Blind review | Identification, estimation, robustness |

### Infrastructure

| Agent | Role |
|---|---|
| Verifier | Compilation + replication package audit |
| Orchestrator | Agent dispatch, quality gates, escalation |

---

## The Verification System

### Layer 1: Continuous Checks (every session)

Before committing:
- Does the master runner execute without error?
- Are all output files fresh (timestamps match)?
- Are there any prohibited code patterns?
- Score ≥ 80?

### Layer 2: Cross-Language Replication (per major result)

For each headline result:
1. Replicate in at least one additional language (R/Stata/Python)
2. Compare: coefficients to 6 decimal places, SEs to 4, N exact match
3. Document in `code/replication/comparison/cross-language-comparison.md`
4. Any discrepancy is a bug — investigate every one

### Layer 3: Referee 2 Audit (before submission)

**Must be run in a FRESH TERMINAL:**

1. Open a new terminal (fresh Claude context)
2. `cd paper-N && claude`
3. Paste: `"Read .claude/skills/referee2/SKILL.md and run the full 5-audit protocol on this paper. Primary language is R."`
4. Claude runs all 5 audits, files report in `correspondence/referee2/`
5. Author responds point-by-point
6. Iterate until verdict is "Accept"

### Blindspot Audit (before writing)

Also in a FRESH TERMINAL:

1. Open a new terminal
2. `cd paper-N && claude`
3. Paste: `"Read .claude/skills/blindspot/SKILL.md and run the Blindspot audit on this paper."`
4. Report filed in `correspondence/blindspot/`

---

## The Deprecation Protocol

**Claude never deletes or modifies any existing file.**

### How Updates Work

1. Old file → moved to `_deprecated/YYYY-MM-DD_filename.ext`
2. New file → created fresh at the original path
3. Change logged in `_deprecation-log.md`

### File Tiers

| Tier | Files | Rule |
|---|---|---|
| 1: Immutable | `data/raw/`, `code/replication/`, `correspondence/`, `session-logs/` | NEVER touched |
| 2: Deprecate-and-Replace | Code, notes, papers, strategy docs | Standard protocol |
| 3: Regenerable | `output/tables/`, `output/figures/` | Batch deprecate before re-run |
| 4: Append-Only | `missing-lit.md`, `research-ideas.md`, `bibliography.bib` | Content accumulates |

### Recovery

If something goes wrong:
1. Check `_deprecated/` in the relevant directory
2. Check `_deprecation-log.md` for context
3. Check `git log` for full history
4. Check `session-logs/` for the session that made the change

---

## Session Management

### Context Window Rules

From Goldsmith-Pinkham: the context window degrades with length. Practical implications:

- **Keep sessions focused:** 5–10 turns on one bounded task
- **Be specific:** Not "analyze this data" but "Load X.csv, compute Y, check for outliers above Z"
- **Compact at 60%:** `/compact remember [critical decisions]`
- **Write state to files:** Conversations evaporate; files persist
- **Use ESC:** If Claude is heading wrong, hit ESC and restart from an earlier point

### The [LEARN] Tag System

When you correct Claude, capture it:

```
[LEARN:stata] Always use reghdfe not areg for multi-way FE. 
Discovered 2026-04-14 session 2.
```

Claude reads MEMORY.md every session. Tagged corrections prevent repeating mistakes.

---

## Quality Gates

| Score | Threshold | What It Means |
|---|---|---|
| 80+ | Commit | Safe to save progress |
| 90+ | Push | Ready for remote |
| 95+ | Submission | Paper ready for journal |
| < 80 | Blocked | Must fix before committing |

---

## IRB and Sensitive Data

If you work with restricted data:

- Place it in `data/raw/restricted/` — Claude CANNOT read this directory
- Create anonymized versions in `data/synthetic/` for Claude to work with
- Never include PII in session logs, MEMORY.md, or any file outside `data/`
- The `.gitignore` excludes `data/raw/restricted/` from version control

**Goldsmith-Pinkham's heuristic:** If you wouldn't put it on Dropbox, don't put it in front of Claude.

---

## Phases of a Dissertation

| Phase | What Happens | Key Commands |
|---|---|---|
| 0. Setup | Fork, configure, connect tools | Starter prompt |
| 1. Discovery | Literature review, gap analysis | `/missing-lit`, `/research-ideas` |
| 2. Strategy | Pre-analysis plan, strategy memo | Strategist agent |
| 3. Execution | Data cleaning, estimation, figures | Coder agent, explorations/ |
| 4. Verification | Cross-language replication, Referee 2 | `/referee2`, `/blindspot` |
| 5. Writing | LaTeX manuscript | Writer agent |
| 6. Presentations | Beamer/Quarto slides | Presentations/ |
| 7. Submission | Replication package, peer review sim | Verifier agent |
| 8. Compilation | Combine into dissertation | dissertation/main.tex |

---

## Tips

- **Start lean.** You don't need all 11 agents on day one. Start with CLAUDE.md, file safety, and session logs. Add agents as you need them.
- **Supervisor integration.** File meeting notes in `correspondence/supervisor/`. Mark approved decisions with `[APPROVED BY SUPERVISOR YYYY-MM-DD]` in the strategy memo.
- **Cross-paper consistency.** Track shared definitions in `MEMORY.md` under "Cross-Paper Consistency." If Paper 1's main estimate changes, note which other papers reference it.
- **Constitutional governance.** After 4–6 weeks, formalize your non-negotiable patterns as Constitutional Articles in CLAUDE.md.
