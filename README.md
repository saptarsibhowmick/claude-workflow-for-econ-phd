# Claude Workflow for Econ PhD

> A Claude Code scaffold for managing a multi-paper PhD dissertation — from literature review to journal submission. Built for empirical economics, adaptable to adjacent fields.

**Built on the work of:** [Pedro Sant'Anna](https://github.com/pedrohcgs/claude-code-my-workflow) (claude-code-my-workflow), [Hugo Sant'Anna](https://github.com/hugosantanna/clo-author) (Clo-Author), [Scott Cunningham](https://github.com/scunning1975/MixtapeTools) (MixtapeTools), and [Paul Goldsmith-Pinkham](https://paulgp.substack.com/p/getting-started-with-claude-code) (Researcher's Setup Guide).

---

## What This Is

A ready-to-fork project structure for a PhD dissertation consisting of **multiple publishable papers** (the "three-essays" model is common in economics, but the scaffold supports 2, 3, 4, or more). You describe tasks in plain English. Claude plans the approach, dispatches specialized agents, reviews quality, fixes issues, and presents results.

### What's Included

- **Complete directory structure** for a multi-paper dissertation with master literature review
- **File safety system** — Claude never deletes or modifies files; everything uses deprecate-and-replace
- **12 rules** (always-on and path-scoped) governing code conventions, quality, and workflow
- **8 custom skills** (`/setup`, `/missing-lit`, `/research-ideas`, `/blindspot`, `/referee2`, `/new-paper`, `/deprecate`, `/devils-advocate`)
- **11 agent definitions** (strategist, coder, writer, domain-referee, methods-referee, and their critics)
- **4 hooks** for file protection, context survival, and session management
- **Three-layer verification** — continuous checks → cross-language replication → Referee 2 audit
- **Deprecation protocol** — no file is ever lost; old versions are timestamped and preserved
- **IRB/sensitive data handling** — restricted data directories that Claude cannot access
- **Obsidian-compatible** — the project folder works as an Obsidian vault if you want graph view and manual editing (optional, not required)
- **Zotero integration** — designed to work with Zotero MCP for literature management
- **PDF splitting literature pipeline** — reads Zotero PDFs in 4-page chunks (Cunningham's methodology), classifies papers into 6 types, extracts structured information using type-dependent templates, and writes `@citekey.md` notes to `literature/zotero-notes/`. Paper-level copies are made automatically when relevant. No Obsidian MCP required (though the project folder works as an Obsidian vault if you want graph view).

### Who This Is For

- PhD students in empirical economics writing multi-essay dissertations
- Researchers in adjacent fields (finance, political science, development studies, public policy) who can adapt the domain profile
- Anyone who wants a structured, auditable, AI-assisted research workflow

---

## Quick Start

### Prerequisites

| Tool | Required For | Install |
|---|---|---|
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | Everything | `npm install -g @anthropic-ai/claude-code` |
| [Git](https://git-scm.com) | Version control | Pre-installed on macOS; `brew install git` on Mac |
| [R](https://www.r-project.org/) | Analysis & figures | [r-project.org](https://www.r-project.org/) |
| [Stata](https://www.stata.com/) | Cross-language replication | License required |
| XeLaTeX | Paper & dissertation compilation | [TeX Live](https://tug.org/texlive/) or [MacTeX](https://tug.org/mactex/) |

**Optional:**

| Tool | Required For |
|---|---|
| [Desktop Commander MCP](https://github.com/wonderwhy-er/DesktopCommanderMCP) | Recommended: filesystem access + PDF reading for Zotero literature notes |
| [Obsidian](https://obsidian.md/) | Optional: browse markdown notes with graph view (install LaTeX Suite plugin for equations) |
| [Zotero](https://www.zotero.org/) + [Better BibTeX](https://retorque.re/zotero-better-bibtex/) | Reference management |
| [Ghostty](https://ghostty.org/) | Modern terminal (recommended) |
| [Zellij](https://zellij.dev/) | Terminal multiplexer for split-pane work |
| Python | Additional analysis language |
| [Quarto](https://quarto.org) | Web-based presentations |

### Step 1: Fork & Clone

```bash
gh repo fork saptarsibhowmick/claude-workflow-for-econ-phd --clone
cd claude-workflow-for-econ-phd
```

Or manually:

```bash
git clone https://github.com/saptarsibhowmick/claude-workflow-for-econ-phd.git
cd claude-workflow-for-econ-phd
```

### Step 2: Start Claude Code

```bash
claude
```

### Step 3: Run Setup

Claude will check your Zotero connection, ask how many papers your dissertation will include, and generate the full structure.

```
/setup
```

Claude will:
1. Check if Zotero MCP is connected (auto-registers via `claude mcp add` if not — restart required)
2. Ask for your dissertation topic, paper count, and details for each paper
3. Generate `paper-1/` through `paper-N/` directories from the template
4. Fill in CLAUDE.md, domain profile, journal profiles, and notation registry
5. Update the dissertation chapter structure to match your paper count
6. Commit the configured scaffold

### Step 4: Start Working

Once setup is done, describe what you need:

- `"Process this paper from Zotero"` — creates structured literature notes
- `/missing-lit` — finds gaps in your literature
- `/research-ideas` — generates empirical questions
- `"Set up the data pipeline for Paper 1"` — creates cleaning and analysis scripts
- `/referee2` — runs the full 5-audit verification protocol
- `/blindspot` — finds what you've become blind to in your results
- `"Review my paper before submission"` — runs all critics in parallel

---

## Skills (Slash Commands)

### `/setup` — First-Time Project Configuration

Run once when you start your dissertation. Checks prerequisites and builds your project.

```
/setup
```

**What it does:**
1. Tests Zotero MCP connection → auto-runs `claude mcp add zotero -- uvx zotero-mcp serve` if not connected (restart required after)
2. Verifies Better BibTeX is installed → points to [retorque.re/zotero-better-bibtex](https://retorque.re/zotero-better-bibtex/) if missing
3. Asks for your Zotero PDF folder path → saves to `literature/zotero-config.md`
4. Asks: dissertation topic, number of papers, details for each paper, primary language, name/institution/supervisor, target journals, field/subfields
5. Generates `paper-1/` through `paper-N/` from the template
6. Fills in CLAUDE.md, domain profile, journal profiles, notation registry
7. Updates dissertation chapter structure
8. Commits the configured scaffold

---

### `/missing-lit` — Literature Gap Finder

Scans your existing literature notes and searches for papers you may have missed.

```
/missing-lit
```

**What it does:**
1. Reads all `@citekey.md` notes in `literature/zotero-notes/`
2. Extracts topics, methods, geographies, datasets from YAML tags
3. Identifies structural gaps (understudied regions, unused methods, missing working papers)
4. Searches NBER, IZA, CEPR, SSRN, and top journals for recent papers
5. Appends findings to `literature/missing-lit.md` with relevance scores

**When to run:** Every 4–6 weeks, or when starting a new paper chapter.

---

### `/research-ideas` — Empirical Question Generator

Generates research questions based on your literature and data landscape.

```
/research-ideas
```

**What it does:**
1. Reads all notes, missing-lit, synthesis files, and domain profile
2. Generates ideas with: research question, empirical strategy, data feasibility, contribution, feasibility score (1–5), target journal
3. Flags ideas that complement your existing papers
4. Appends to `literature/research-ideas.md`

**When to run:** After major literature additions, or when exploring new directions.

---

### `/referee2` — Systematic 5-Audit Verification

The most important quality tool. Runs a full independent audit of your paper.

```
# MUST be run in a FRESH TERMINAL — open a new Claude Code session
cd paper-1
claude
/referee2
```

**The five audits:**

| Audit | What It Checks |
|---|---|
| Code Audit | Missing values, merge diagnostics, variable construction, edge cases |
| Cross-Language Replication | Independent scripts in 2 other languages, compared to 6 decimal places |
| Directory Audit | Relative paths, naming, replication-readiness |
| Output Automation | All tables/figures generated by code, nothing manual |
| Econometrics Audit | Identification, clustering, specification, robustness |

**Critical rules:**
- Referee 2 NEVER modifies your code — it creates its own scripts in `code/replication/`
- Reports are filed in `correspondence/referee2/` (immutable)
- You respond point-by-point; iterate until verdict is "Accept"

**When to run:** Before submission. Also useful on partial results to build the habit early.

---

### `/blindspot` — Peripheral Vision Audit

Finds what you've become blind to in your own results. Based on Cunningham's Shklovsky principle.

```
# MUST be run in a FRESH TERMINAL
cd paper-1
claude
/blindspot
```

**The Blindspot Grid:**

| | Things Present | Things Absent |
|---|---|---|
| **Problems** | Anomalies you've normalized | Checks you never ran |
| **Opportunities** | Richness you're ignoring | Extensions you haven't considered |

**Output:** Report filed in `correspondence/blindspot/` with specific findings, locations (table/figure/column), and recommended actions.

**When to run:** After results are stable, before you start writing.

---

### `/new-paper` — Scaffold a New Paper

Creates a complete paper directory from the template.

```
/new-paper 4 "labor market effects of refugee integration policies"
```

**What it does:**
1. Copies `paper-template/` to `paper-N/`
2. Fills in the paper-level CLAUDE.md with topic and strategy
3. Creates empty templates for codebook, strategy memo, master runner
4. Updates master CLAUDE.md and dissertation structure
5. Commits

---

### `/deprecate` — Safe File Replacement

Safely deprecates a file following the immutability protocol.

```
/deprecate paper-1/code/R/04_estimate.R "Switched from OLS to IV specification"
```

**What it does:**
1. Checks the file isn't in an immutable location (data/raw, correspondence, etc.)
2. Moves it to `_deprecated/YYYY-MM-DD_filename.ext`
3. Logs the change in `_deprecation-log.md`

You (or Claude) then create the fresh replacement at the original path.

---

### `/devils-advocate` — Structured Design Debate

Generates the strongest case for two competing design choices.

```
/devils-advocate "DiD with staggered treatment" vs "Synthetic control"
```

**What it does:**
1. Argues FOR Option A — strongest possible case
2. Argues FOR Option B — strongest possible case (no straw-manning)
3. Presents a trade-off matrix (assumptions, robustness, data needs, reviewer acceptability)
4. Recommends with caveats
5. Documents the decision in the strategy memo

**When to use:** Major design decisions — estimator choice, instrument selection, clustering level, sample restrictions.

---

## Agents

Agents are specialized Claude personas dispatched automatically by the orchestrator. You rarely invoke them directly — they run behind the scenes when you describe a task.

### Worker-Critic Pairs

Every agent that creates something has a paired critic that checks it. The critic can read but never edit. The worker can edit but never approve itself. If they can't agree after 3 rounds, the issue escalates to you.

| Phase | Worker | Creates | Critic | Checks |
|---|---|---|---|---|
| Strategy | **Strategist** | Strategy memo, PAP, identification design | **Strategist-critic** | Assumptions, inference, clustering, falsification |
| Execution | **Coder** | Analysis scripts with numerical discipline | **Coder-critic** | 16 checks: strategy alignment, reproducibility, prohibited patterns |
| Writing | **Writer** | Paper sections using argument moves | **Writer-critic** | 8 checks: structure, claims-evidence, notation, AI pattern detection |

### Peer Review Agents

Simulate journal submission. Invoked when you ask Claude to review your paper.

| Agent | Role | What It Does |
|---|---|---|
| **Editor** | Desk reviewer | Screens for scope, assigns referee dispositions (Structuralist, Credibility, Measurement, Policy, Theory, Skeptic), synthesizes editorial decision classifying issues as FATAL / ADDRESSABLE / TASTE |
| **Domain-referee** | Blind reviewer | Evaluates contribution, literature positioning, external validity. Every major comment includes "what would change my mind" |
| **Methods-referee** | Blind reviewer | Evaluates identification, estimation, inference, robustness. Paper-type aware (reduced-form, structural, descriptive) |

### Infrastructure Agents

| Agent | What It Does |
|---|---|
| **Verifier** | Standard mode: 4 checks (compiles? runs? fresh? valid refs?). Submission mode: 10 checks (adds AEA replication package audit) |
| **Orchestrator** | Dispatches worker-critic pairs, enforces quality gates (80/90/95), escalates after 3 failed rounds, tracks scores |

---

## Verification System

Three layers, from lightest to heaviest:

| Layer | What | When | How |
|---|---|---|---|
| **Continuous** | Does it run? Outputs fresh? Score ≥ 80? | Every session | Automatic before commits |
| **Cross-language** | R = Stata = Python to 6 decimal places | Per major result | `/referee2` Audit 2, or manual |
| **Referee 2** | Full 5-audit protocol in fresh terminal | Before submission | `/referee2` in new session |
| **Blindspot** | Peripheral vision audit in fresh terminal | Before writing | `/blindspot` in new session |

---

## Quality Gates

| Score | Threshold | Meaning |
|---|---|---|
| **80+** | Commit | Safe to save progress locally |
| **90+** | Push | Ready to push to remote |
| **95+** | Submission | Paper ready for journal submission |
| **< 80** | Blocked | Must fix issues before committing |

---

## Documentation

| Document | What It Covers |
|---|---|
| **[SETUP.md](SETUP.md)** | Detailed installation, configuration, and first-session walkthrough |
| **[USAGE.md](USAGE.md)** | Day-to-day workflow, all commands, all agents, verification protocols |
| **[CLAUDE.md](CLAUDE.md)** | The master project constitution (Claude reads this every session) |

---

## Workflow Phases

| Phase | What Happens | Key Tools |
|---|---|---|
| **0. Setup** | Fork, `/setup`, configure | `/setup` |
| **1. Discovery** | Process papers, find gaps, generate ideas | Zotero MCP, `/missing-lit`, `/research-ideas` |
| **2. Strategy** | Write strategy memo and PAP before any code | Strategist agent, `/devils-advocate` |
| **3. Execution** | Data cleaning → estimation → figures | Coder agent, `explorations/` sandbox |
| **4. Verification** | Cross-language replication, independent audit | `/referee2`, `/blindspot` |
| **5. Writing** | LaTeX manuscript with argument moves | Writer agent |
| **6. Presentations** | Beamer/Quarto slides | `presentations/` |
| **7. Submission** | Replication package, simulated peer review | Verifier agent, Editor + referees |
| **8. Compilation** | Combine papers into dissertation | `dissertation/main.tex` |

---

## Project Structure

```
claude-workflow-for-econ-phd/
│
├── CLAUDE.md                     # Project constitution — Claude reads every session
├── MEMORY.md                     # Persistent learnings [LEARN:tag] format
├── README.md                     # You are here
├── SETUP.md                      # Installation & configuration guide
├── USAGE.md                      # Day-to-day usage guide
│
├── .claude/                      # Claude Code configuration
│   ├── settings.json             # Hooks and permissions
│   ├── rules/                    # Auto-loading rules (always-on + path-scoped)
│   ├── references/               # Domain profile, journal profiles, notation
│   ├── skills/                   # Custom slash commands
│   └── agents/                   # Specialized agent definitions
│
├── literature/                   # Master literature review
│   ├── docs/                     # Non-Zotero PDFs and documents
│   ├── zotero-notes/             # Structured notes from Zotero papers
│   │                             # (@citekey.md format, created by Claude
│   │                             #  using PDF splitting + extraction templates)
│   ├── synthesis/                # Frontier maps, method/data landscapes
│   ├── missing-lit.md            # Gap analysis (append-only)
│   ├── research-ideas.md         # Empirical questions (append-only)
│   └── bibliography.bib          # Master BibTeX (auto-synced from Zotero)
│
├── paper-template/               # Template for each paper (copied by /setup)
│   ├── CLAUDE.md                 # Paper-specific context
│   ├── literature/zotero-notes/  # Copies of relevant notes from master
│   ├── pre-analysis-plan/        # Strategy memo + PAP
│   ├── data/                     # raw/ (immutable), processed/, codebook/
│   ├── code/                     # R/, python/, stata/, replication/
│   ├── output/                   # tables/, figures/, logs/
│   ├── paper/                    # main.tex, sections/, submitted/, responses/
│   ├── presentations/            # beamer/, quarto/
│   ├── explorations/             # Sandbox with relaxed quality gates
│   ├── correspondence/           # referee2/, blindspot/, supervisor/
│   ├── quality_reports/          # specs/, plans/, session_logs/, scores/
│   └── replication-package/      # AEA-format replication package
│
├── paper-1/ ... paper-N/         # Generated by /setup (2, 3, 4+ papers)
│
├── dissertation/                 # Final compiled dissertation
│   ├── main.tex
│   ├── frontmatter/              # title-page, acknowledgment, abstract
│   ├── chapters/                 # introduction, lit-review, papers, conclusion
│   └── backmatter/               # references, appendix
│
├── session-logs/                 # Master session logs (cross-project)
├── correspondence/supervisor/    # Supervisor meeting notes
└── templates/                    # Reusable templates
```

---

## Core Principles

These are drawn from the four source frameworks and encoded into the scaffold's rules:

1. **Claude never deletes or modifies existing files.** Every change creates a fresh file. Old versions go to `_deprecated/` with a timestamp. ([Deprecation Protocol](USAGE.md#deprecation-protocol))

2. **Design before results.** No estimation code is written until a strategy memo exists. Point estimates are not interpreted until the design is intentional. (Cunningham)

3. **Adversarial review requires separation.** Referee 2 and Blindspot audits run in a fresh terminal with no access to the authoring session's history. (Cunningham)

4. **Cross-language verification.** Every headline result is replicated in at least one additional language. If R ≠ Stata to 6 decimal places, something is wrong. (Cunningham)

5. **Context degrades with length.** Keep sessions focused (5–10 turns). Write state to files. Compact intentionally. (Goldsmith-Pinkham)

6. **The critic can't fix; the fixer can't approve.** Worker-critic agent pairs ensure no self-congratulatory review. (P. Sant'Anna)

7. **If it's not documented, it didn't happen.** Every audit produces a report. Every response is filed. Every session produces a log. (Cunningham)

8. **Plan first, then execute.** Complex tasks start with a requirements spec, then a plan, then execution. (P. Sant'Anna)

---

## Acknowledgments & Thank You

This scaffold would not exist without the generosity of four economists who openly shared their AI-assisted research workflows with the academic community. Each contributed foundational ideas that are woven throughout this project.

### Pedro H. C. Sant'Anna — Emory University

**Repository:** [claude-code-my-workflow](https://github.com/pedrohcgs/claude-code-my-workflow) · **Guide:** [psantanna.com/claude-code-my-workflow](https://psantanna.com/claude-code-my-workflow/)

Pedro built the infrastructure that makes everything else possible. The orchestrator architecture (contractor mode, dependency-driven dispatch), the quality gate system (80/90/95 scoring), the plan-first workflow, the adversarial critic-fixer loop, the hooks system (pre-compact context capture, session restoration), MEMORY.md with [LEARN] tags, effort levels, constitutional governance, the explorations sandbox, and session logging — all originate in his work. His workflow was developed over 6+ sessions building a PhD course at Emory (800+ slides across 6 lectures) and has been adopted by 15+ research groups. The comprehensiveness and precision of his documentation set the standard for the entire ecosystem.

### Hugo Sant'Anna — University of Alabama at Birmingham

**Repository:** [clo-author](https://github.com/hugosantanna/clo-author) · **Documentation:** [hsantanna.org/clo-author](https://hsantanna.org/clo-author/)

Hugo took Pedro's infrastructure and reoriented it specifically for empirical economics publication. His contributions include the 17-agent system organized by research phase (discovery → strategy → execution → peer review → submission), paper-type awareness (reduced-form, structural, theory+empirics, descriptive), the simulated peer review system with referee dispositions and "what would change my mind" statements, the journal profiles system (30 journals pre-populated), the `/revise` command for real R&R responses, the Verifier agent with AEA replication package audit, multi-model strategy for cost optimization, path-scoped rules, and the weighted scoring protocol. The Clo-Author is the most domain-specific of the four frameworks and directly informs the agent architecture used here.

### Scott Cunningham — Baylor University

**Repository:** [MixtapeTools](https://github.com/scunning1975/MixtapeTools) · **Book:** [Causal Inference: The Mixtape](https://mixtape.scunning.com) · **Substack:** [causalinf.substack.com](https://causalinf.substack.com)

Scott contributed the verification philosophy that anchors this scaffold's quality system. The Referee 2 protocol (five systematic audits — code, cross-language replication, directory, output automation, econometrics — run in a fresh terminal by a Claude instance that never saw the original work) is the single most valuable practice in this toolkit. The principle that "Referee 2 never modifies author code" ensures genuine independence. He also contributed the Blindspot audit (based on Shklovsky's defamiliarization principle — finding what the author can no longer see), the cross-language replication discipline (R = Stata = Python to 6 decimal places, or something is wrong), the CLAUDE.md template for project memory, the documentation-as-first-class-output philosophy, "design before results," and the insight that verification through visualization catches errors that numbers alone miss.

### Paul Goldsmith-Pinkham — Yale School of Management

**Substack:** [A Causal Affair](https://paulgp.substack.com/) · **Video Series:** [Markus Academy](https://www.youtube.com/watch?v=HzgByl5ZsWE)

Paul provided the pedagogical foundation that makes the other three frameworks accessible. His "ladder of AI coding tools" (from copy-paste ChatGPT through agentic IDEs to autonomous containers) gives researchers the mental model to understand where Claude Code sits. His explanation of the context window — why performance degrades with length, how compaction works, and why long sessions produce worse output than short ones — is the most important conceptual contribution for day-to-day practice. He also contributed the terminal setup recommendations (Ghostty + Zellij for split-pane work), the IRB/sensitive data heuristic ("if you wouldn't put it on Dropbox, don't put it in front of Claude"), the ESC key trick for context management, the directed compaction technique, and the Cowork vs. Claude Code distinction.

### A Note to Users

If this scaffold helps your research, consider citing or acknowledging these four authors in your work. They shared their workflows openly so the community could build on them. Pass it forward.

---

## License

MIT License. Use freely for research, teaching, or any academic purpose. Attribution appreciated.
