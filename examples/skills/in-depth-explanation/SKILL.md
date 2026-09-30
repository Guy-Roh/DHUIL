---
name: in-depth-explanation
description: Deliver deep, mechanically precise explanations for complex code, math, and computer science concepts grounded in critical rationalism and first principles, with optional markdown file export.
---

## GLOBAL
### INVARIANTS
- ALWAYS stick to system prompt protocol
### GLOSSARY
- WITHMD: write explanation to file in /agent/explanations/
- NOMD: output explanation directly to chat
- RT: research task
- CT: current tasks

## INTERPRETATION
### CONDITIONALS
- WHEN a prompt CONTAINS "WITHMD"
    - ONLY WRITE explanation to disk
- WHEN a prompt CONTAINS "NOMD" OR NOT CONTAINS "WITHMD"
    - ONLY OUTPUT explanation to prompt

## EXECUTION
### DEFAULTS
- FORMAT using 4 spaces for indentations
- AVOID academic citations or link audits unless explicitly requested
### CONDITIONALS
- WHEN framing the explanation
    - OUTPUT core mechanical reality in plain terms
- WHEN analyzing causality
    - AVOID citing low-level hardware or compiler trivia
- WHEN detailing data transformations
    - LOG step-by-step visual logic
- WHEN presenting structured data
    - PREFER concrete numbers and small tables OVER dense descriptive text
- WHEN a prompt CONTAINS "WITHMD"
    - WRITE explanation to /agent/explanations/<topic-name>.md
    - UPDATE /agent/current_tasks.md

## OUTPUT
### DEFAULTS
- AVOID emojis
- FORMAT explanations with clear headings, structured tables, and concise code blocks
### CONDITIONALS
- WHEN a prompt CONTAINS "WITHMD"
    - OUTPUT link to created file in /agent/explanations/
- WHEN a prompt CONTAINS "NOMD" OR NOT CONTAINS "WITHMD"
    - OUTPUT explanation directly to chat
- WHEN a response CONTAINS niche terms
    - OUTPUT brief inline explanation
