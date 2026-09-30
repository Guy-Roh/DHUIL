---
name: fail-log
description: Record a structured post-mortem entry in the active task log and update current_tasks.md when an implementation attempt fails, a build breaks, or revisions are requested.
---

- Name: fail-log-1.0

## GLOBAL
### INVARIANTS
- ALWAYS stick to system prompt protocol
### GLOSSARY
- ER: error log
- CT: current tasks
- BG: bug task
- FT: feature task
- RT: research task
- ST: subtask
- AT: attempt

## INTERPRETATION
### CONDITIONALS
- WHEN an implementation attempt fails OR a build breaks OR developer requests revisions
    - WRITE post-mortem log entry
    - UPDATE /agent/current_tasks.md
    - AVOID repeating prior failed implementations or unverified assumptions

## EXECUTION
### DEFAULTS
- AVOID marking a failed or revised task as completed
- INSTEAD set status to pending - awaiting developer feedback
- STOP
- AWAIT developer instructions
### CONDITIONALS
- WHEN formatting post-mortem entry
    - WRITE 6-line post-mortem containing:
        - Line 1: Attempted (files and components touched)
        - Line 2: Failure Root Cause (exact error message or unexpected behavior)
        - Line 3: Build Status (bun run build verification result)
        - Line 4: Reversions (what changes were reverted vs kept)
        - Line 5: Missing Info / References (missing documentation or official links needed)
        - Line 6: Next Proposed Attempt (precise next action)
- WHEN locating active task log
    - SEARCH /agent/bugs, /agent/features, /agent/vault-tasks, or /agent/research for the task matching active scope
- WHEN synchronizing task register
    - UPDATE /agent/current_tasks.md under the active task ID with 1-sentence attempt summary
    - WRITE task status in /agent/current_tasks.md as pending - awaiting developer feedback

## OUTPUT
### DEFAULTS
- AVOID emojis
- OUTPUT concise post-mortem summary
- STOP
- AWAIT developer direction
