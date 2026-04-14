---
name: new-paper
description: "Scaffold a new paper directory with the full structure, CLAUDE.md, and empty templates."
argument-hint: "[paper-number] [short-topic-description]"
---

# New Paper Scaffold

## Steps

1. **Create the directory structure** for `paper-N/`:
   ```
   paper-N/
   ├── CLAUDE.md
   ├── literature/
   ├── pre-analysis-plan/
   │   ├── strategy-memo.md
   │   └── pap-draft.md
   ├── data/
   │   ├── raw/public/
   │   ├── raw/restricted/
   │   ├── processed/
   │   ├── resources/
   │   ├── codebook/
   │   │   ├── variables.md
   │   │   ├── sample.md
   │   │   └── data-sources.md
   │   └── synthetic/
   ├── code/
   │   ├── R/00_master.R
   │   ├── python/
   │   ├── stata/
   │   └── replication/
   ├── output/
   │   ├── tables/
   │   ├── figures/
   │   └── logs/
   ├── paper/
   │   ├── main.tex
   │   ├── sections/
   │   ├── submitted/
   │   └── responses/
   ├── presentations/
   │   ├── beamer/
   │   └── quarto/
   ├── explorations/
   ├── correspondence/
   │   ├── referee2/
   │   ├── blindspot/
   │   └── supervisor/
   ├── quality_reports/
   │   ├── specs/
   │   ├── plans/
   │   ├── session_logs/
   │   └── scores/
   └── replication-package/
       ├── README.md
       ├── code/
       ├── data/
       └── output/
   ```

2. **Create paper-specific CLAUDE.md** from template with the topic filled in
3. **Create empty template files**: strategy-memo.md, variables.md, sample.md, data-sources.md, 00_master.R
4. **Create .gitkeep** files in empty directories
5. **Update master CLAUDE.md** project state to include the new paper
6. **Commit**: `git add paper-N/ && git commit -m "scaffold: paper-N — [topic]"`
