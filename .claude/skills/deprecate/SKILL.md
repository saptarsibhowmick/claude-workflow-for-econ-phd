---
name: deprecate
description: "Safely deprecate a file following the deprecation protocol."
argument-hint: "[filepath] [reason]"
---

# Deprecate File

## Steps

1. **Verify** the file exists and is not in a Tier 1 (immutable) location
2. **Create** `_deprecated/` directory in the same folder if it doesn't exist
3. **Move** the file to `_deprecated/YYYY-MM-DD_filename.ext`
4. **Create or append** to `_deprecation-log.md` in the same directory:
   ```markdown
   ## YYYY-MM-DD · filename.ext
   - **Reason**: [provided reason]
   - **Deprecated to**: _deprecated/YYYY-MM-DD_filename.ext
   - **Session**: [current session log path]
   - **Breaking changes**: [any downstream effects]
   ```
5. **Report** the deprecation to the author

## Validation

Before deprecating, check:
- Is the file in `data/raw/`? → REFUSE (Tier 1: immutable)
- Is the file in `code/replication/`? → REFUSE (Tier 1: immutable)
- Is the file in `correspondence/`? → REFUSE (Tier 1: immutable)
- Is the file in `session-logs/`? → REFUSE (Tier 1: immutable)
- Is the file in `data/raw/restricted/`? → REFUSE (Tier 1: immutable + sensitive)

If any check fails, explain why the file cannot be deprecated and suggest alternatives.
