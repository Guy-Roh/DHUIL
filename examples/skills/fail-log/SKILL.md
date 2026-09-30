---
name: fail-log
description: Record a structured post-mortem entry in the active task log and update current_tasks.md when an implementation attempt fails, a build breaks, or revisions are requested.
---

## GLOBAL
### INVARIANTS
- ALWAYS stick to system prompt protocol

## INTERPRETATION
#### CONDITIONALS
- WHEN an implementation attempt fails OR a build breaks OR developer requests revisions
    - WRITE a post-mortem logging and
    - UPDATE task register.
    - AVOID repeating prior failed implementations or unverified assumptions.

## EXECUTION
#### DEFAULTS
- FORMAT the attempt breakdown
    - APPEND a new `### Attempt N` or `### Subtask N` block to the task log.
    - WRITE the 6-line post-mortem containing:
        - Line 1: Attempted (files and components touched)
        - Line 2: Failure Root Cause (exact error message or unexpected behavior)
        - Line 3: Build Status (bun run build verification result)
        - Line 4: Reversions (what changes were reverted vs kept)
        - Line 5: Missing Info / References (missing documentation or official links needed)
        - Line 6: Next Proposed Attempt (precise next action)
- NEVER mark a failed or revised task as completed; set status to pending - awaiting developer feedback or blocked.
- HALT after logging and AWAIT developer instructions.
#### CONDITIONALS
- WHEN locating active task log
    - SEARCH `/agent/bugs`, `/agent/features`, `/agent/vault-tasks`, or `/agent/research` for the task matching the active scope.

- WHEN synchronizing task register
    - UPDATE `/agent/current_tasks.md` under the active task ID with a 1-sentence attempt summary.
    - WRITE task status in `current_tasks.md` as `pending - awaiting developer feedback`.

## OUTPUT
#### DEFAULTS
- OUTPUT concise post-mortem summary and prompt developer for the next direction.

