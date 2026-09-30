---
name: session-init
description: Initialize session rules, determine codebase versus Obsidian vault mode, ensure agent directories exist, and establish the next task counter ID.
---

## GLOBAL
### INVARIANTS
- ALWAYS stick to system prompt protocol

## Interpretation
#### Conditionals
- WHEN starting a session OR entering a new workspace OR /session-init is invoked
    - INVOKE workspace mode detection and task register initialization
    - AVOID skipping directory verification or task counter resolution

## Execution
#### Defaults
- AVOID overwriting existing /agent/current_tasks.md
- EXECUTE exactly once at session startup
#### Conditionals
- WHEN .obsidian directory exists in workspace root
    - WRITE /agent/vault-tasks and /agent/research if not existing
    - WHEN /agent/current_tasks.md exists NOT
        - WRITE /agent/current_tasks.md with Vault Tasks headers
- WHEN .obsidian directory exists in workspace root NOT
    - WRITE /agent/bugs, /agent/features, /agent/errors, and /agent/research if not existing
    - WHEN /agent/current_tasks.md exists NOT
        - WRITE /agent/current_tasks.md with Bugs and New features headers
- WHEN determining task ID sequence
    - SEARCH /agent directory recursively for task identifiers matching (?:RT|FT|BG|ST|ER|VT)-[0-9]+
    - LOG maximum numeric ID as HIGHEST_ID
    - LOG HIGHEST_ID + 1 as NEXT_ID

## Output
#### Defaults
- FORMAT output with simple headings and clickable markdown links
- OUTPUT initialization summary containing Mode, Tasks file link, Highest Task ID, and Next Task ID
- STOP
- AWAIT developer instructions

## Global
#### Defaults
- AVOID diversion from workspace initialization protocols without explicit developer override
#### Glossary
- VT: vault task
- RT: research task
- FT: feature task
- BG: bug task
- ST: subtask
- ER: error log
- CT: current tasks
