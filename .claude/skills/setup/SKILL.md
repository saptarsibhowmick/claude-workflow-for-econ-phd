---
name: setup
description: "First-time project setup. Checks prerequisites (Zotero MCP), asks for paper count, generates folder structure, and configures all templates."
---

# Project Setup

> Run this skill once at the start of your dissertation project.
> It checks prerequisites, asks configuration questions, and generates the full project structure.

## Step 1: Check Zotero MCP Connection

Before anything else, verify that Zotero MCP is connected.

**Test:** Attempt to call `zotero_search_items` (or equivalent) with a trivial query like "test".

**If the call succeeds:**
- Report: "✓ Zotero MCP is connected."
- Proceed to Step 1b.

**If the call fails or the tool is not available:**
- Report:
  ```
  ✗ Zotero MCP is not connected.
  
  This scaffold is designed to work with Zotero for literature management.
  You have several options for connecting Zotero:
  
  RECOMMENDED:
  • zotero-mcp by 54yyyu (Python, most feature-rich):
    https://github.com/54yyyu/zotero-mcp
    Install: pip install zotero-mcp-server && zotero-mcp setup
  
  ALTERNATIVES:
  • zotero-mcp plugin by cookjohn (Zotero 7 plugin, write access):
    https://github.com/cookjohn/zotero-mcp
  • mcp-zotero by kaliaboi (Node.js, lightweight):
    https://github.com/kaliaboi/mcp-zotero
  • mcp-pyzotero by gyger (Python, local API):
    https://github.com/gyger/mcp-pyzotero
  
  ALSO RECOMMENDED — Desktop Commander MCP:
    https://github.com/wonderwhy-er/DesktopCommanderMCP
    Install: npx @wonderwhy-er/desktop-commander@latest setup
    
    Desktop Commander gives Claude full filesystem access and native PDF
    reading capabilities. This significantly improves the reliability of
    reading PDFs from your Zotero Library folder during literature note
    creation. Without it, Claude may struggle to access PDFs stored outside
    the project directory.
  
  After installing, restart Claude Code and run /setup again.
  ```
- Ask: "Would you like to continue setup without Zotero, or stop and install it first?"
- If continuing without Zotero: note in CLAUDE.md that Zotero is not connected, and the `/missing-lit` skill will use web search only. Skip Steps 1b and 2, proceed to Step 3.

## Step 1b: Check Better BibTeX

**Only if Zotero MCP is connected.** Better BibTeX (BBT) is required for citekey-based paper lookup.

**Test:** Take any item returned from the Step 1 search. Call `zotero_get_item_metadata`
with `format: bibtex` on that item. Check whether the bibtex output begins with
`@type{citekey,` (e.g., `@article{becker2019,`).

**If the bibtex output contains a citekey:**
- Report: "✓ Better BibTeX is installed."
- Proceed to Step 2.

**If the bibtex output has no citekey, returns an error, or looks malformed:**
- Report:
  ```
  ✗ Better BibTeX does not appear to be installed in Zotero.
  
  This scaffold requires Better BibTeX (BBT) citekeys for paper lookup.
  Without BBT, Claude cannot reliably identify papers in your library.
  
  Install Better BibTeX:
    https://retorque.re/zotero-better-bibtex/
  
  Steps:
    1. Download the .xpi file from the link above
    2. In Zotero: Tools → Add-ons → Install Add-on From File → select the .xpi
    3. Restart Zotero
    4. BBT will auto-generate citekeys for all items in your library
  
  After installing, restart Claude Code and run /setup again.
  ```
- Ask: "Would you like to continue setup without Better BibTeX, or stop and install it first?"
- If continuing without BBT: note the limitation in CLAUDE.md. Literature note creation will require manual citekey entry rather than auto-lookup.

## Step 2: Configure Zotero PDF Access

**Only if Zotero MCP is connected.** Ask the user:

> **What is the full path to your Zotero PDF storage folder?**
> This is where Zotero stores PDF attachments on your machine.
> Examples:
> - macOS with Google Drive: `/Users/yourname/Library/CloudStorage/GoogleDrive-you@gmail.com/My Drive/Zotero/Library`
> - macOS local: `/Users/yourname/Zotero/storage`
> - Linux: `/home/yourname/Zotero/storage`
> - Windows: `C:\Users\yourname\Zotero\storage`

Save the answer to `literature/zotero-config.md`:

```markdown
---
pdf_folder: "{user's answer}"
bbt_verified: {true|false}
date_configured: {YYYY-MM-DD}
---

# Zotero Configuration

- **pdf_folder**: Absolute path to Zotero PDF storage directory.
  Claude reads PDFs from this location during literature note creation.
  Update this path if your Zotero library moves.
- **bbt_verified**: Whether Better BibTeX was detected during setup.
```

Then report:
```
✓ Zotero configured.

Literature notes will be stored in literature/zotero-notes/ as @citekey.md files.
When you say "analyse paper @citekey", Claude will:
  1. Find the paper in Zotero via MCP
  2. Access the PDF from: {pdf_folder}
  3. Split it into 4-page chunks and read in batches
  4. Classify the paper and extract structured information
  5. Write the note to literature/zotero-notes/@citekey.md

When working on a specific paper (e.g., Paper 1), Claude will copy
relevant notes from literature/zotero-notes/ to paper-1/literature/zotero-notes/.

Optional: If you open this project folder in Obsidian, all markdown notes
are browsable with graph view. Install LaTeX Suite for equation rendering.
```

## Step 3: Gather Project Configuration

Ask the user the following questions. Wait for answers before proceeding.

1. **What is your dissertation topic?** (2–3 sentences)
2. **How many publishable chapters/papers will your dissertation include?**
   (Common: 3 for economics, but could be 2, 4, or more depending on your program)
3. **For each paper, provide:**
   - A short title or topic description
   - The likely identification strategy (DiD, IV, RDD, SC, structural, descriptive, or "undecided")
4. **What is your primary analysis language?** (R / Stata / Python)
5. **Your name, institution, and supervisor's name**
6. **Target journal tier** (Top 5, top field, or strong field — or specific journal names)
7. **Your research field and subfields** (for the domain profile)

## Step 4: Generate Paper Directories

For each paper (based on the number provided in Step 3):

1. **Copy** the entire `paper-template/` directory to `paper-N/` (where N is 1, 2, 3, ...)
2. **Update** `paper-N/CLAUDE.md` with the paper-specific topic, strategy, and phase
3. **Update** `paper-N/pre-analysis-plan/strategy-memo.md` header with the paper's question
4. **Update** `paper-N/code/R/00_master.R` (or .do / .py) header with the paper number
5. **Update** `paper-N/quality_reports/research_journal.md` with the paper number
6. **Update** `paper-N/replication-package/README.md` with the paper number

Also update `dissertation/chapters/` to include one chapter stub per paper:
- `paper-1.tex`, `paper-2.tex`, ..., `paper-N.tex`
- Update `dissertation/main.tex` to `\input{}` all paper chapters

## Step 5: Configure Master Files

1. **CLAUDE.md** — Fill in all placeholders:
   - Project title, institution, supervisor
   - All paper topics and research questions
   - Current phase (typically "SETUP" at this point)

2. **MEMORY.md** — Leave template structure, no changes needed yet

3. **`.claude/references/domain-profile.md`** — Fill in:
   - Field and subfields
   - Common identification strategies
   - Known data sources (ask the user if unsure)
   - Target journals
   - Seminal references (ask the user for 5–10 foundational papers)

4. **`.claude/references/journal-profiles.md`** — Review pre-populated profiles, ask if any need adjustment for the user's specific subfield

5. **`.claude/references/notation-registry.md`** — Start with core variables if the user already has conventions; otherwise leave as template

## Step 6: Update Dissertation Structure

Based on the paper count:
1. Update `dissertation/main.tex` to include the correct number of `\input{chapters/paper-N}` lines
2. Create chapter stubs for each paper in `dissertation/chapters/`
3. Update `dissertation/cross-paper-checks.md` column headers for the actual number of papers

## Step 7: Clean Up Template

After all paper directories are generated:
1. **Delete** the `paper-template/` directory (it's no longer needed — each paper-N/ is independent)
2. Or **rename** it to `_paper-template/` if the user wants to keep it for future reference

## Step 8: Initial Commit

```bash
git add -A
git commit -m "scaffold: project setup — [N] papers on [topic]"
```

## Step 9: Report

Present a summary:
- Number of papers created
- Zotero connection status
- Obsidian connection status
- Files configured
- What to do next (suggested first task: process literature, or draft a strategy memo)

## Important
- Follow all file safety rules during setup
- Do not modify the template files — copy them, then modify the copies
- Ask for user confirmation before committing
