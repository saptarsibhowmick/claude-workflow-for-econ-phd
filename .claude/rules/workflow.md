# Workflow Rule — Always On

## Plan-First Protocol

For any non-trivial task (more than ~3 steps or ambiguous goal):

1. **Spec** (if complex): Ask 3–5 clarifying questions → create requirements spec with MUST/SHOULD/MAY → save to `quality_reports/specs/` → get approval
2. **Plan**: Draft approach, files involved, verification steps → save to `quality_reports/plans/` → get approval
3. **Execute**: Implement the plan, following all file safety rules
4. **Verify**: Run quality checks, confirm outputs are fresh, score against gates
5. **Log**: Update session log with what was done, decisions made, open questions

Plans survive context compression because they are saved to disk.

## Contractor Mode

After a plan is approved, enter contractor mode:
- Coordinate everything autonomously
- Only return to the author when there is genuine ambiguity or a decision to make
- Run the full verify → review → fix → re-verify loop
- Score against quality gates before reporting done
- Never report "done" without actually verifying the output

## Session Management

- Keep sessions focused: 5–10 turns on one bounded task
- At ~60% context usage, compact proactively: `/compact remember [critical decisions]`
- Write state to files — conversations evaporate, files persist
- Before ending any session, write a session log to `session-logs/`

## Session Log Format

```markdown
# Session Log — YYYY-MM-DD Session N

## Goal
[What was the objective of this session]

## What Was Done
[Concrete actions taken]

## Decisions Made
[Design choices, with rationale]

## Open Questions
[Unresolved issues for next session]

## Where to Pick Up
[Exact next step for the next session]
```
