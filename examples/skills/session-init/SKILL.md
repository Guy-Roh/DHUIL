---
name: session-init
description: Initialize session rules, determine codebase versus Obsidian vault mode, ensure agent directories exist, and establish the next task counter ID.
---

## GLOBAL
### INVARIANTS
- ALWAYS stick to system prompt protocol
### DEFAULTS
- AVOID diversion from workspace initialization protocols without explicit developer override
### GLOSSARY
- VT: vault task
- RT: research task
- FT: feature task
- BG: bug task
- ST: subtask
- ER: error log
- CT: current tasks

## INTERPRETATION
### CONDITIONALS
- WHEN starting a session OR entering a new workspace OR /session-init is invoked
    - INVOKE workspace mode detection and task register initialization
    - AVOID skipping directory verification or task counter resolution

## EXECUTION
### DEFAULTS
- AVOID overwriting existing /agent/current_tasks.md
- EXECUTE exactly once at session startup
### CONDITIONALS
- WHEN .obsidian EXISTS in workspace root
    - WRITE /agent/vault-tasks and /agent/research if not existing
    - WHEN /agent/current_tasks.md EXISTS NOT
        - WRITE /agent/current_tasks.md with Vault Tasks headers
- WHEN .obsidian EXISTS NOT in workspace root
    - WRITE /agent/bugs, /agent/features, /agent/errors, and /agent/research if not existing
    - WHEN /agent/current_tasks.md EXISTS NOT
        - WRITE /agent/current_tasks.md with Bugs and New features headers
- WHEN determining task ID sequence
    - READ /agent/current_tasks.md AND SEARCH /agent directory recursively for task identifiers matching (?:RT|FT|BG|ST|ER|VT)-[0-9]+
    - LOG maximum numeric ID as HIGHEST_ID
    - LOG HIGHEST_ID + 1 as NEXT_ID

## OUTPUT
### DEFAULTS
- FORMAT output with simple headings and clickable markdown links
- OUTPUT initialization summary containing Mode, Tasks file link, Highest Task ID, and Next Task ID
- STOP
- VERIFY with developer
