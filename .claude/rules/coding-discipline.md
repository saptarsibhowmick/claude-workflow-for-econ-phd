# Coding Discipline — Always On

> Adapted from Andrej Karpathy's observations on LLM coding pitfalls.
> Source: https://github.com/forrestchang/andrej-karpathy-skills

## 1. Think Before Coding

- State assumptions explicitly — if uncertain, ASK rather than guess
- Present multiple interpretations when ambiguity exists — don't pick silently
- Push back when a simpler approach exists
- Stop when confused — name what's unclear and ask for clarification
- Never make wrong assumptions on the user's behalf and run with them

## 2. Simplicity First

- Minimum code that solves the problem, nothing speculative
- No features beyond what was asked
- No abstractions for single-use code
- No "flexibility" or "configurability" that wasn't requested
- No error handling for impossible scenarios
- If 200 lines could be 50, rewrite it
- Test: would a senior engineer say this is overcomplicated? If yes, simplify

## 3. Surgical Changes

- Touch ONLY what you must — don't "improve" adjacent code, comments, or formatting
- Don't refactor things that aren't broken
- Match existing style, even if you'd do it differently
- If you notice unrelated issues, MENTION them — don't fix them silently
- Remove imports/variables/functions that YOUR changes made unused
- Don't remove pre-existing dead code unless asked
- Test: every changed line should trace directly to the user's request
- This reinforces the deprecation protocol: don't edit files in place

## 4. Goal-Driven Execution

- Transform tasks into verifiable goals with success criteria
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- For multi-step tasks, state a brief plan with verification at each step
- Strong success criteria let Claude loop independently
- Weak criteria ("make it work") require constant clarification
