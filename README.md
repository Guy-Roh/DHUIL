# DHUIL Specification (Declarative Hybrid Universal Instruction Language)

## Overview

DHUIL (Declarative Hybrid Universal Instruction Language) is a way to write AI prompts in a way that is both easy to read and easy for agents to follow.
Declarative in the expression of its logic
Hybrid in the way that it combines structured programming patterns with natural language
Universal by using model-agnostic declarative keywords

## Architectural Communication Graph
DHUIL allows explicit instructions governing each stage of this pipeline:
1. `GLOBAL`: Universal invariants, defaults, and glossaries
2. `INTERPRETATION`: interpretation of the input messages
3. `EXECUTION` (or Workflow)
4. `OUTPUT`: how messages back should be structured

## Syntax Primitives & Formatting Rules

### Document Hierarchy
- Header metadata: Key-value list at the root (`- Name: ...`, optional `- Codename: ...`). 
  - Skill files simply use the default YAML header.

- Major functional blocks: Level 2 headings:
	- GLOBAL
	- INTERPRETATION
	- EXECUTION
	- OUTPUT

- Rule classifications: Level 3 headings 
	- INVARIANTS
	- DEFAULTS
	- CONDITIONALS
	- GLOSSARY
	- SKILLS

All block titles and tags are written uppercase

- Rules are written as bullet points and indented bullet points within for condition-action-policy rules
- 4 spaces per indentation level

### CAP Tags

#### Conditional
- `WHEN <condition>`: Primary trigger clause.
- `MEANING <semantic_criteria>`: Clarification of the trigger's semantic meaning.
- `CONTAINS <text/symbol>`: Substring or element matching condition.
- `OR <condition>`: Alternative trigger condition.
- `AND <condition>`: Conjunctive trigger condition.
- `NOT <condition>`: Negation condition.
- `WITH <condition>`: Contextual qualifier or state condition.

#### Action
- `OUTPUT <action>`: Produce a specific response format, text, or content.
- `INVOKE <skill>`: Trigger an external skill or subagent workflow.
- `UPDATE <target>`: Modify an existing file, register, or state.
- `STOP`: Immediately halt execution.
- `AWAIT <condition/verification>`: Pause execution pending external event or approval.
- `SEARCH <target>`: Search files, codebase, or official documentation.
- `ASK <target>`: Request clarification or explicit permission.
- `WRITE <target>`: Create or edit or text in files on disk.
- `FORMAT <target>`: Apply structural formatting.
- `EXECUTE <command>`: Run a specific terminal command or script.
- `LOG <target>`: Record reasoning, plans, or step-by-step notes.

#### Policy
- `ALWAYS`: explicit absolute invariant.
- `AVOID <action>`: Explicit negative constraint (forbidding behaviors, tool usage, assumptive actions, or deviations).
- `ONLY <action/scope>`: Restrict permitted actions, tools, or scope.
- `INSTEAD <action>`: Substitute an alternative action in place of a default or disallowed behavior.
- `PREFER <resource> OVER <resource>`: Explicit prioritization of tools, runtimes, languages, or approaches.

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

### `## Global`
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

## Reference Implementations & Examples

### System Prompts
- [jason.md](examples/system-prompts/jason.md): Complete DHUIL system prompt reference implementation.

### Skills
- [session-init](examples/skills/session-init/SKILL.md): Session initialization and workspace mode detection.
- [new-task](examples/skills/new-task/SKILL-dhuil.md): Task scaffolding and root-cause formulation.
- [fail-log](examples/skills/fail-log/SKILL.md): Post-mortem logging and error tracking.
- [senior-review](examples/skills/senior-review/SKILL-dhuil.md): Code review and quality verification.
- [system-troubleshoot](examples/skills/system-troubleshoot/SKILL-dhuil.md): System troubleshooting workflows.
- [in-depth-explanation](examples/skills/in-depth-explanation/SKILL.md): Structured technical explanation skill.

## Tooling & Editor Support

- [VS Code Extension](extensions/dhuil-vscode/): Syntax highlighting and language support for DHUIL instructions inside Markdown files.
