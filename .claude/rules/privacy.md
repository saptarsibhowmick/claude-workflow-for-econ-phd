# Intellectual Property and Privacy — Always On

## Core Rule

The contents of this project — research ideas, identification strategies, data
constructions, preliminary findings, unpublished manuscripts, strategy memos,
and all working documents — are the author's confidential intellectual property.

## Rules for Claude

1. **Never share, reference, or describe the author's research ideas, questions,
   or strategies in any context outside this project.** This includes not
   summarising them when asked by other users, not using them as examples, and
   not referencing them in other conversations.

2. **Never post, upload, publish, or transmit any project content to external
   services.** This includes: web forms, APIs, social media, forums, email
   drafts, shared documents, or any URL outside the project directory.

3. **Never include research ideas, strategy details, or preliminary findings
   in git commit messages, PR descriptions, or any content that may become
   publicly visible.** Use generic descriptions: "update estimation code"
   not "add IV strategy using distance to conflict as instrument."

4. **Never expose file contents when searching the web.** When running
   `/missing-lit` or `/research-ideas`, search using generic academic terms
   only — never paste the author's specific research question, hypothesis,
   or novel contribution into a search query.

5. **Session logs and MEMORY.md stay local.** These files contain decision
   rationale that could reveal research direction. They must never be
   shared externally.

6. **Strategy memos are maximally sensitive.** The `pre-analysis-plan/`
   directory contains the author's identification strategy before publication.
   Being scooped on a novel identification strategy is a career-level risk
   for a PhD student. Treat these files with the same caution as restricted data.

7. **Draft manuscripts are confidential until submitted.** Files in `paper/`
   are unpublished work. Never reference their contents externally.

## Git Commit Message Conventions (Privacy-Safe)

GOOD: "update cleaning script" / "add robustness check" / "revise introduction"
BAD:  "add refugee spillover DiD using 2015 shock" / "IV using distance to Aleppo"

The commit message goes to GitHub. If the repo is public, the world can read it.

## Reminder

Claude's conversation history is processed by Anthropic but not shared with
other users. However, the author's ideas should still be treated as confidential
within conversations — do not volunteer details about the research beyond what
is needed for the current task.
