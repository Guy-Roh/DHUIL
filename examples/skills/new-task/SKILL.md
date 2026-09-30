---
name: new-task
description: Plan and scaffold a new feature, bug fix, research task, or subtask before modifying project files. Initializes task logs in agent directories and updates current_tasks.md.
---

- Name: new-task-1.0

## GLOBAL
### INVARIANTS
- ALWAYS stick to system prompt protocol
### GLOSSARY
- FT: feature task
- BG: bug task
- RT: research task
- VT: vault task
- ST: subtask
- AT: attempt
- CT: current tasks

## INTERPRETATION
### CONDITIONALS
- WHEN beginning a new task OR preparing to modify or create project files OR beginning a new subtask
    - INVOKE task scoping and root cause formulation
    - AVOID modifying project files before developer approval

## EXECUTION
### DEFAULTS
- FORMAT agent logs with simple headings (# to #####) only
- AVOID bold text (**)
- FORMAT using 4 spaces for indentations
- FORMAT credible sources as [Name](link) with the exact line or section cited
- AVOID marking a task as completed
- INSTEAD set status to pending
- AWAIT developer verification
- FORMAT tasks using correct numbering
    - MAIN TASKS (VT, RT, FT, BG) as H1 # in task log and as filename
        - <task-number digits=3>-<task-type-abbr>-<short-description>
        - EXAMPLE 034-RT-marketing-research
    - SUB-TASKS (ST) as H2 ## in task log
        - <task-number digits=3>-<task-type-abbr>-ST<sub-task-number digits=2>-<short-description>
        - EXAMPLE 034-RT-ST03-behance-scrape
    - ATTEMPT (AT) as H3 ### in task log
        - <task-number digits=3>-<task-type-abbr>-ST<sub-task-number digits=2>-<short-description>-AT<attempt-number>
        - EXAMPLE 034-RT-ST03-behance-scrape-AT02
### CONDITIONALS
- WHEN checking workspace mode
    - SEARCH workspace root for .obsidian
    - WHEN .obsidian exists
        - WRITE /agent/vault-tasks and /agent/research if not existing
    - WHEN NOT .obsidian exists
        - WRITE /agent/bugs, /agent/features, /agent/errors, and /agent/research if not existing
- WHEN evaluating task scope
    - SEARCH /agent/current_tasks.md
    - WHEN an existing task covers this scope
        - WRITE new subtask as H2 ## in the existing task file
        - AVOID creating duplicate task files
    - WHEN NOT an existing task covers this scope
        - SEARCH /agent directory for highest 3-digit task number
        - WRITE new task file using format <digits=3>-<task-type-abbr>-<short-description>.md
            - Bug: /agent/bugs/<digits=3>-BG-<short-description>.md
            - Feature: /agent/features/<digits=3>-FT-<short-description>.md
            - Research: /agent/research/<digits=3>-RT-<short-description>.md
            - Vault Task: /agent/vault-tasks/<digits=3>-VT-<short-description>.md
- WHEN scaffolding task log
    - LOG Plain Root Cause: 1-2 plain sentences explaining what is happening
    - LOG Technical Root Cause: precise technical breakdown of mechanism
    - LOG step-by-step implementation plan detailing touched files and untouched files
    - UPDATE /agent/current_tasks.md with task link and pending status

## OUTPUT
### DEFAULTS
- AVOID emojis
- FORMAT output with simple headings and clickable markdown links
- OUTPUT structured proposal containing Plain Root Cause, Technical Root Cause, Implementation Plan, and Touched Files
- STOP
- AWAIT developer approval
