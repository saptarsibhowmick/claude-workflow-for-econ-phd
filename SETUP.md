# Setup Guide

Step-by-step instructions for configuring the scaffold for your dissertation.

---

## 1. Prerequisites

### Required

Install these before starting:

```bash
# Claude Code
npm install -g @anthropic-ai/claude-code

# Verify
claude --version
```

You also need R, Stata (licensed), and a LaTeX distribution (TeX Live or MacTeX). Git should already be installed on macOS.

### Recommended Terminal Setup

Following Goldsmith-Pinkham's recommendation, invest 15 minutes in a better terminal:

```bash
# Ghostty — fast, GPU-accelerated terminal
brew install ghostty

# Zellij — terminal multiplexer for split-pane work
brew install zellij

# Oh My Zsh — better shell experience
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

**Zellij split-pane workflow:** Run Claude Code on the left, watch file changes on the right. `Ctrl+p` then `d` to split. `Alt+arrow` to navigate.

### Optional

- **Obsidian** — for manual markdown editing and graph view. The project folder is already structured as a valid vault.
- **Zotero + Better BibTeX** — for reference management. Connect via Zotero MCP.
- **Quarto** — for web-based presentations.
- **Python** — for additional analysis language.

---

## 2. Fork and Clone

```bash
# Using GitHub CLI
gh repo fork ORIGINAL_REPO/claude-workflow-for-econ-phd --clone
cd claude-workflow-for-econ-phd

# Or manually
git clone https://github.com/YOUR_USERNAME/claude-workflow-for-econ-phd.git
cd claude-workflow-for-econ-phd
```

---

## 3. First Session — Automated Setup

Start Claude Code and run the setup skill:

```bash
claude
```

Then type:

```
/setup
```

The setup skill will:

### 3a. Check Zotero MCP Connection

Claude will test whether Zotero MCP is connected. If it's not, Claude will attempt to auto-register it by running:

```bash
claude mcp add zotero -- uvx zotero-mcp serve
```

If auto-registration succeeds, you'll need to restart Claude Code and run `/setup` again for the connection to take effect.

If auto-registration fails (e.g., `uvx` not installed), you'll see manual installation options:

| MCP Server | Language | Key Feature | Link |
|---|---|---|---|
| **zotero-mcp** (recommended) | Python | Most feature-rich, semantic search | [github.com/54yyyu/zotero-mcp](https://github.com/54yyyu/zotero-mcp) |
| **zotero-mcp plugin** | Zotero plugin | Write access, native integration | [github.com/cookjohn/zotero-mcp](https://github.com/cookjohn/zotero-mcp) |
| **mcp-zotero** | Node.js | Lightweight, quick setup | [github.com/kaliaboi/mcp-zotero](https://github.com/kaliaboi/mcp-zotero) |
| **mcp-pyzotero** | Python | Local API, Zotero 7 | [github.com/gyger/mcp-pyzotero](https://github.com/gyger/mcp-pyzotero) |

**Quick install (recommended option):**
```bash
pip install zotero-mcp-server
zotero-mcp setup    # Auto-configures for Claude
```

**Also recommended: Desktop Commander MCP**

Desktop Commander gives Claude full filesystem access and native PDF reading capabilities. This significantly improves the reliability of reading Zotero PDFs during literature note creation — without it, Claude may not be able to access PDFs stored in your Zotero Library folder (which is typically outside the project directory).

```bash
npx @wonderwhy-er/desktop-commander@latest setup
```

GitHub: [github.com/wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP)

All options work best with **Better BibTeX** installed in Zotero: [retorque.re/zotero-better-bibtex](https://retorque.re/zotero-better-bibtex/)

You can continue setup without Zotero — the scaffold will work, but literature management skills will use web search only instead of your library.

### 3b. Configure Your Project

Claude will ask you:

1. **Dissertation topic** (2–3 sentences)
2. **Number of publishable chapters/papers** — this is flexible: 2, 3, 4, or more depending on your program's requirements
3. **Details for each paper** — short title, likely identification strategy
4. **Primary analysis language** (R / Stata / Python)
5. **Your name, institution, supervisor**
6. **Target journals and research field**

### 3c. Generate Structure

Based on your answers, Claude will:
- Generate `paper-1/` through `paper-N/` directories from the `paper-template/`
- Each paper gets its own `literature/zotero-notes/` folder (for copies of relevant notes)
- Fill in all CLAUDE.md files (master + per-paper)
- Configure the domain profile, journal profiles, and notation registry
- Update `dissertation/main.tex` to include the correct number of chapter inputs
- Create chapter stubs for each paper
- Clean up the template directory
- Make an initial git commit

### Literature Notes Workflow

After setup, your literature workflow is:

1. **Add a paper:** Say `"analyse paper @citekey"` — Claude finds it in Zotero, splits the PDF, reads it in chunks, and writes a structured note to `literature/zotero-notes/@citekey.md`
2. **Scan for gaps:** Run `/missing-lit` — reads all notes, finds what's missing
3. **Generate ideas:** Run `/research-ideas` — reads notes + gaps, generates empirical questions
4. **Copy to paper:** When working on Paper N, Claude copies relevant notes from `literature/zotero-notes/` to `paper-N/literature/zotero-notes/`

PDFs are read directly from your Zotero Library folder (via the path in the bibtex metadata). They are never copied into the project.

---

## 4. Manual Configuration (Alternative)

If you prefer to configure things yourself:

### 4a. Fill in CLAUDE.md

Open `CLAUDE.md` and replace all `[BRACKETED PLACEHOLDERS]`:
- Project title, institution, supervisor
- Paper topics and research questions
- Current phase

### 4b. Fill in Domain Profile

Open `.claude/references/domain-profile.md`:
- Your field and subfields
- Common identification strategies in your area
- Data sources you expect to use
- Target journals (ranked by tier)
- 10–15 seminal references

### 4c. Fill in Journal Profiles

Open `.claude/references/journal-profiles.md`:
- Review the pre-populated profiles
- Add any journals specific to your subfield
- Adjust priorities based on your knowledge of each journal's culture

### 4d. Fill in Notation Registry

Open `.claude/references/notation-registry.md`:
- Core variable symbols ($D_i$, $Y_{it}$, etc.)
- Subscript conventions
- Standard error reporting conventions

### 4e. Fill in Paper-Level CLAUDE.md

For each paper (`paper-1/CLAUDE.md`, etc.):
- Research question
- Identification strategy
- Data sources
- Current phase

---

## 5. Connect External Tools

### Zotero MCP (for literature management)

If you use Zotero, connect it via MCP so Claude can search your library:

1. Install the Zotero MCP server
2. Ensure Better BibTeX is installed in Zotero
3. Configure the connection in Claude Code

### Obsidian (optional — for manual browsing)

Obsidian MCP is **not required**. If you want to browse your notes with graph view:

1. Open the project folder as an Obsidian vault
2. Install the **LaTeX Suite** community plugin for equation rendering
3. All `@citekey.md` notes in `literature/zotero-notes/` will be visible

### Desktop Commander MCP (recommended — for PDF access)

Desktop Commander gives Claude filesystem access to read PDFs from your Zotero Library folder:

```bash
npx @wonderwhy-er/desktop-commander@latest setup
```

GitHub: [github.com/wonderwhy-er/DesktopCommanderMCP](https://github.com/wonderwhy-er/DesktopCommanderMCP)

---

## 6. Verify the Setup

Run these checks:

```bash
# In Claude Code:
# 1. Check that Claude reads the project context
"What is my dissertation about? List my papers."

# 2. Check that rules are loaded
"What are my file safety rules?"

# 3. Check that skills are available
"What slash commands are available?"

# 4. Test the deprecation protocol
/deprecate paper-1/CLAUDE.md "Testing deprecation protocol"
```

---

## 7. Git Configuration

```bash
# Initialize (if not already)
git init

# Review .gitignore
cat .gitignore

# First commit
git add -A
git commit -m "scaffold: initial project setup"

# Set up remote
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
git push -u origin main
```

**Important:** The `.gitignore` is configured to track `_deprecated/` folders and `_deprecation-log.md` files. Never add these to `.gitignore`.

---

## 8. Day 1 Checklist

- [ ] Claude Code installed and authenticated
- [ ] Repository forked and cloned
- [ ] Starter prompt pasted, configuration adapted
- [ ] CLAUDE.md placeholders filled in
- [ ] Domain profile filled in
- [ ] At least one journal profile reviewed
- [ ] Git initialized with first commit
- [ ] Terminal setup (Ghostty + Zellij) configured
- [ ] First session log written to `session-logs/`

---

## What's Next

Read **[USAGE.md](USAGE.md)** for the day-to-day workflow, all commands, agent descriptions, and the verification protocol.
