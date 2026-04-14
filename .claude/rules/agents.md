# Agent Rules — Always On

## Worker-Critic Separation

Every agent that creates something has a paired critic that checks its work.
The critic can read but NEVER edit. The worker can edit but NEVER approve itself.

## Three-Strikes Escalation

If a worker-critic pair cannot resolve after 3 rounds:

| Pair | Escalation Target |
|---|---|
| Coder + coder-critic | → Strategist (design may be wrong) |
| Writer + writer-critic | → Domain-referee (framing may need rethinking) |
| Strategist + strategist-critic | → Author (fundamental design disagreement) |

## Severity Gradient

Critics calibrate harshness by project phase:
- **Discovery**: Encouraging — focus on coverage, not perfection
- **Execution**: Precise — enforce numerical discipline and reproducibility
- **Peer Review**: Adversarial — simulate hostile referees

## Multi-Model Strategy

| Task Type | Model | Rationale |
|---|---|---|
| Deep reasoning (strategy, peer review, blindspot) | Opus | Nuanced judgment required |
| Fast constrained work (linting, compilation) | Sonnet | Speed over depth |
| Default | Inherit | Session model |
