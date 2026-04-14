---
path: "**/paper/**"
---

# LaTeX Conventions

- `\citet{}` for textual citations, `\citep{}` for parenthetical
- Equation numbering: number only equations that are referenced in text
- No orphan paragraphs (single sentence between headings)
- `\input{}` for tables (from `output/tables/`) — never paste table content
- `\includegraphics{}` for figures (from `output/figures/`) — relative paths
- Cross-references via `\label{}` and `\ref{}`
- Compile with XeLaTeX + BibTeX (3-pass: xelatex → bibtex → xelatex × 2)
- Zero warnings policy — all overfull/underfull boxes must be resolved
