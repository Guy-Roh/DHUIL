---
name: senior-review
description: Audit proposed code and solution plans against over-engineering, redundant error handling, unrequested features, and citation accuracy.
---

- Name: senior-review-1.0

## GLOBAL
### INVARIANTS
- ALWAYS stick to system prompt protocol
### GLOSSARY
- ST: subtask
- FT: feature task
- BG: bug task
- CT: current tasks

## INTERPRETATION
### CONDITIONALS
- WHEN auditing a solution plan OR refactoring code OR reviewing proposed architecture
    - INVOKE the Senior Engineer Simplicity Test
    - AVOID overcomplicated logic, unneeded abstractions, or speculative generalizations

## EXECUTION
### DEFAULTS
- FORMAT using 4 spaces for indentations
- FORMAT credible sources as [Name](link) with the exact line or section cited
- PREFER bun OVER node
- PREFER easy to maintain subcomponents OVER large components
- EXECUTE Senior Engineer Test: "Would a senior engineer say this is overcomplicated?"
- AVOID unrequested features
- AVOID pre-empting impossible scenarios
- AVOID overcomplicated logic
### CONDITIONALS
- WHEN checking implementation plans
    - AVOID guarding against impossible edge cases
    - AVOID redundant error handling
    - AVOID unrequested features or auxiliary tooling
    - AVOID Node-specific runtimes when bun is available
- WHEN verifying framework or API assumptions
    - SEARCH official documentation for verified API usage
    - WHEN verified documentation cannot be found
        - OUTPUT limitation explicitly
        - ASK the developer how to proceed
- WHEN a simpler path exists
    - LOG a 1-3 sentence Simplification Delta

## OUTPUT
### DEFAULTS
- AVOID emojis
- FORMAT findings with clear headings
- OUTPUT findings containing Simplification Delta and Assumptions & Unknowns
### CONDITIONALS
- WHEN ambiguities exist
    - STOP
    - ASK the developer for clarification
