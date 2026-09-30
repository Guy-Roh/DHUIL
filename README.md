# DHUIL Specification (Declarative Heuristic Universal Instruction Language)

## 1. Overview

DHUIL (Declarative Heuristic Universal Instruction Language) is a way for AI agent system prompts to be easy to read and easy to follow. 
It is heuristic in nature in the sense that it tries to make the best out of the probabilistic nature of current LLM agents.

## 2. Architectural Communication Graph

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
1. `Interpretation`: How the Agent receives, parses, and evaluates developer input messages.
2. `Execution` (Workflow): How the Agent plans, runs commands, uses tools, consults documentation, logs tasks, and implements code.
3. `Output`: How the Agent structures, tones, and formats responses returned to the developer.
4. `Global`: Universal invariants, fallback protocols, and domain glossaries applying across all stages.

## 3. Syntax Primitives & Formatting Rules

DHUIL uses a declarative, plain-text Markdown grammar designed for high machine scannability and strict execution compliance.

### 3.1 Document Hierarchy
- Header metadata: Key-value list at the root (`- Name: ...`, `- Codename: ...`).
- Major functional blocks: Level 2 headings (`## Interpretation`, `## Execution`, `## Output`, `## Global`).
- Rule classifications: Level 4 headings (`#### Defaults`, `#### Conditionals`, `#### Glossary`).
- Sub-categories / extensions: Level 5 headings (`##### Skills`, `##### Tools`).

### 3.2 Indentation Standard
- All nested directives and conditional sub-actions must use exactly 4 spaces per indentation level.
- Multi-condition or multi-action trees must branch cleanly using 4-space indented unordered lists (`-`).

### 3.3 Conditional Predicates
Conditional statements evaluate context, syntax triggers, or operational states:
- `WHEN <condition>`: Primary trigger clause.
- `MEANING <semantic_criteria>`: Clarification of the trigger's semantic meaning.
- `OR <condition>`: Alternative trigger condition.
- `AND <condition>`: Conjunctive trigger condition.

### 3.4 Action Directives
Action blocks beneath conditionals define imperative agent behaviors:
- `OUTPUT <action>`: Produce a specific response format or content.
- `AVOID <action>` / `DO NOT <action>`: Explicit negative constraint (forbidding behaviors, tool usage, assumptive actions, or deviations).
- `INVOKE <skill>`: Trigger an external skill or subagent workflow.
- `STOP`: Immediately halt execution.
- `ASK <developer>`: Request clarification or explicit permission.
- `WRITE <target>`: Record information or task state to disk.
- `FORMAT <target> AS <rule>`: Apply structural formatting.
- `USE <resource>`: Prefer specific tools, runtimes, or methods.
- `ALWAYS <rule>`: Universal positive invariant within a block.
- `NEVER <rule>`: Universal negative invariant within a block.

## 4. The 4 Canonical Functional Blocks

### 4.1 Header Metadata
Specifies the system prompt identity, versioning, and designated agent codename.

Syntax:
```markdown
- Name: <Version-Identifier>
- Codename: <Agent-Codename>
```

### 4.2 `## Interpretation`
Controls the input-parsing layer. Governs how user queries, commands, intent modifiers, and fast-path keywords are routed before any tool or execution logic runs.

Canonical Sub-blocks:
- `#### Conditionals`: Rules for detecting questions vs imperative commands, prompt keywords (`qq`), explicit option requests, and intent classification.
- `##### Skills`: Dynamic skill routing triggered by specific input requests (e.g., revision requests triggering `fail-log`).

Structure:
```markdown
## Interpretation
#### Conditionals
- WHEN <input condition>
    - <ACTION DIRECTIVE>
    - <CONSTRAINT DIRECTIVE>
##### Skills
- WHEN <input condition>
    - INVOKE the SKILL <skill-name> ...
```

### 4.3 `## Execution`
Controls the workflow and execution engine. Governs tooling, coding practices, research policies, documentation verification, directory handling, error logging, and developer approval gates.

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

### 4.4 `## Output`
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

### 4.5 `## Global`
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

## 5. Reference Implementation: DHUI-X 4.7.3

see /examples/system-prompts/jason.md