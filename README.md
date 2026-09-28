# DHUIL Specification (Declarative Heuristic Universal Instruction Language)

## Overview

DHUIL (Declarative Heuristic Universal Instruction Language) is a way to write AI prompts in a way that is both easy to read and easy for agents to follow. 
It is heuristic in nature in the sense that it tries to make the best out of the probabilistic nature of current LLM agents.

## Architectural Communication Graph

The DHUIL communication pipeline connects the developer and the agent through three core functional stages:

```
+---------------+     Input Message      +------------------+
|   Developer   | ---------------------> |  Interpretation  |
+---------------+                        +------------------+
        ^                                          |
        |                                          v
        | Output Message (Response)      +------------------+
        +------------------------------- |      Agent       |
                                         +------------------+
                                               |      ^
                                      Workflow |      | Execution
                                               v      |
                                         +------------------+
                                         |    Execution     |
                                         |   / Workflow     |
                                         +------------------+
```

DHUIL provides explicit instructions governing each stage of this graph:
1. `Interpretation`: interpretation of the input messages
2. `Execution` (or Workflow)
3. `Output`: how messages back should be structured
4. `Global`: Universal invariants, fallback protocols, and glossaries

### Advantages of DHUIL
- Easy to write and maintain within Obsidian or standard IDEs unlike XML-based markup for prompting
- Minimal token usage with bullet points for individual rules

## Syntax Primitives & Formatting Rules

### Document Hierarchy
- Header metadata: Key-value list at the root (`- Name: ...`, `- Codename: ...`).
- Major functional blocks: Level 2 headings (`## Interpretation`, `## Execution`, `## Output`, `## Global`).
- Rule classifications: Level 3 headings 
	- `### Defaults`
	- `### Conditionals`
	- `### Glossary`
- Sub-categories / extensions: Level 4 headings (`#### Skills`, `#### Tools`).
- Rules are written as bullet points and indented bullet points within for condition-action-policy rules
- All nested directives and conditional sub-actions must use exactly 4 spaces per indentation level.

### Conditional Predicates
Conditional statements evaluate context, syntax triggers, or operational states:
- `WHEN <condition>`: Primary trigger clause.
- `MEANING <semantic_criteria>`: Clarification of the trigger's semantic meaning.
- `OR <condition>`: Alternative trigger condition.
- `AND <condition>`: Conjunctive trigger condition.

### Action Directives
Action blocks beneath conditionals define imperative agent behaviors:
- `OUTPUT <action>`: Produce a specific response format or content.
- `AVOID <action>`: Explicit negative constraint (forbidding behaviors, tool usage, assumptive actions, or deviations).
- `INVOKE <skill>`: Trigger an external skill or subagent workflow.
- `STOP`: Immediately halt execution.
- `ASK <developer>`: Request clarification or explicit permission.
- `WRITE <target>`: Edit file on disk.
- `FORMAT <target>`: Apply structural formatting.
- `PREFER <resource> OVER <resource>`: Prefer specific tools, runtimes, or methods.

## The 4 Main Blocks
### `## Interpretation`
Instructions on the interpretation of the input message

- `#### Conditionals`: Rules for detecting questions vs imperative commands, prompt keywords (`qq`), explicit option requests, and intent classification.
- `##### Skills`: Dynamic skill routing triggered by specific input requests (e.g., revision requests triggering `fail-log`).

Structure:
```markdown
## Interpretation
#### Conditionals
- WHEN <input condition>
    - <ACTION DIRECTIVE>
    - <POLICY DIRECTIVE>
##### Skills
- WHEN <input condition>
    - INVOKE the SKILL <skill-name> ...
```

### `## Execution`

Canonical Sub-blocks:
- `#### Defaults`: Static engineering and operational standards (indentation rules, senior review standards, runtime preferences, link formatting, approval halt policies).
- `#### Conditionals`: Dynamic runtime behaviors (session init detection, uncertainty halts, API verification, documentation absence protocols, logging triggers).
- `##### Skills`: Task scaffolding (`new-task`), post-mortem logging (`fail-log`), and test runners.

Structure:
```markdown
## Execution
#### Defaults
- FORMAT ...
- ADHERE ...
- USE ...
- NEVER ...
- ALWAYS ...
#### Conditionals
- WHEN <execution state or trigger>
    - <ACTION DIRECTIVE>
    - <ACTION DIRECTIVE>
##### Skills
- WHEN <lifecycle event>
    - INVOKE the SKILL <skill-name> ...
```

### `## Output`
Controls response synthesis and final message delivery back to the developer. Governs tone, language clarity, length bounds, domain term definitions, and visual constraints (e.g., emoji bans).

Canonical Sub-blocks:
- `#### Defaults`: Universal output constraints.
- `#### Conditionals`: Dynamic response adaptations (e.g., inline definitions for niche terminology, concise explanation modes).

Structure:
```markdown
## Output
#### Defaults
- AVOID emojis under any circumstance, even when prompted.
#### Conditionals
- WHEN <response context condition>
    - OUTPUT <formatting directive>
```

### Global`
Defines system-wide fallbacks, strict non-diversion invariants, and domain-specific acronym definitions utilized across logs, tasks, and conversations.

Canonical Sub-blocks:
- `#### Defaults`: Universal non-diversion and protocol enforcement rules.
- `#### Glossary`: Domain terminology and task prefix definitions (e.g., `RT`, `FT`, `BG`, `ST`, `ER`, `CV`, `CT`, `VT`).

Structure:
```markdown
## Global
#### Defaults
- AVOID diversion from these protocols or specific skills without explicit developer override.
#### Glossary
- <ACRONYM>: <definition>
```

## 5. Reference Implementations

