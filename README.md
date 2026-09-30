# Declarative Hybrid Universal Instruction Language (DHUIL)

## Overview

DHUIL (Declarative Hybrid Universal Instruction Language) is a markdown enhancement to write agent prompts with clearer structure than pure natural language with minimal token overhead.

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

- Major functional blocks: Level 2 headings (`## <BLOCK>`):
    - `## GLOBAL`
    - `## INTERPRETATION`
    - `## EXECUTION`
    - `## OUTPUT`

- Rule classifications: Level 3 headings (`### <CLASSIFICATION>`):
    - `### INVARIANTS`
    - `### DEFAULTS`
    - `### CONDITIONALS`
    - `### GLOSSARY`
    - `### SKILLS`

All block titles and classification headings are written uppercase.

- Rules are written as bullet points and indented bullet points within for condition-action-policy rules
- 4 spaces per indentation level

### CAP Tags

#### Conditional
- `WHEN <condition>`: Primary trigger clause.
- `MEANING <semantic_criteria>`: Clarification of the trigger's semantic meaning.
- `CONTAINS <text/symbol>`: Substring or element matching condition.
- `EXISTS <target>`: Check existence of a file, directory, variable, or state.
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
- `READ <target>`: Inspect or view specific files or content directly without searching.
- `ASK <target>`: Request clarification or explicit permission.
- `WRITE <target>`: Create or edit text or files on disk.
- `FORMAT <target>`: Apply structural formatting.
- `EXECUTE <command>`: Run a specific terminal command or script.
- `LOG <target>`: Record reasoning, plans, or step-by-step notes.
- `VERIFY <condition/target>`: Perform verification with developer or run validation checks (e.g. `VERIFY with developer`, `VERIFY with bun run build`).

#### Policy
- `ALWAYS`: Explicit absolute invariant.
- `AVOID <action>`: Explicit negative constraint (forbidding behaviors, tool usage, assumptive actions, or deviations).
- `ONLY <action/scope>`: Restrict permitted actions, tools, or scope.
- `INSTEAD <action>`: Substitute an alternative action in place of a default or disallowed behavior (often paired as `AVOID <action> INSTEAD <action>`).
- `PREFER <resource> OVER <resource>`: Explicit prioritization of tools, runtimes, languages, or approaches.

## The 4 Main Blocks

### `## GLOBAL`
Defines system-wide fallbacks, strict non-diversion invariants, and domain-specific acronym definitions utilized across logs, tasks, and conversations.

Canonical Sub-blocks:
- `### INVARIANTS`: Absolute non-negotiable invariants and protocols.
- `### DEFAULTS`: Universal default operational parameters and formatting rules.
- `### GLOSSARY`: Domain terminology and task prefix definitions.

Structure:
```markdown
## GLOBAL
### INVARIANTS
- ALWAYS stick to system prompt protocol
### GLOSSARY
- <ACRONYM>: <definition>
```

### `## INTERPRETATION`
Instructions on the interpretation of the input message.

Canonical Sub-blocks:
- `### CONDITIONALS`: Rules for detecting questions vs imperative commands, prompt keywords, explicit option requests, and intent classification.
- `### SKILLS`: Dynamic skill routing triggered by specific input requests (e.g., revision requests triggering `fail-log`).

Structure:
```markdown
## INTERPRETATION
### CONDITIONALS
- WHEN <input condition>
    - <ACTION DIRECTIVE>
    - <POLICY DIRECTIVE>
### SKILLS
- WHEN <input condition>
    - INVOKE the SKILL <skill-name> ...
```

### `## EXECUTION`
Governs dynamic runtime behavior, task logging lifecycle, engineering defaults, and execution workflows.

Canonical Sub-blocks:
- `### DEFAULTS`: Static engineering and operational standards (indentation rules, senior review standards, runtime preferences, link formatting, approval halt policies).
- `### CONDITIONALS`: Dynamic runtime behaviors (session init detection, uncertainty halts, API verification, documentation absence protocols, logging triggers).
- `### SKILLS`: Task scaffolding (`new-task`), post-mortem logging (`fail-log`), and test runners.

Structure:
```markdown
## EXECUTION
### DEFAULTS
- FORMAT ...
- ALWAYS ...
### CONDITIONALS
- WHEN <execution state or trigger>
    - <ACTION DIRECTIVE>
    - VERIFY with developer
### SKILLS
- WHEN <lifecycle event>
    - VERIFY with <validation command>
    - INVOKE the SKILL <skill-name> ...
```

### `## OUTPUT`
Controls response synthesis and final message delivery back to the developer. Governs tone, language clarity, length bounds, domain term definitions, and visual constraints (e.g., emoji bans).

Canonical Sub-blocks:
- `### DEFAULTS`: Universal output constraints (e.g., emoji bans, formatting structure).
- `### CONDITIONALS`: Dynamic response adaptations (e.g., inline definitions for niche terminology, concise explanation modes).

Structure:
```markdown
## OUTPUT
### DEFAULTS
- AVOID emojis under any circumstance, even when prompted.
### CONDITIONALS
- WHEN <response context condition>
    - OUTPUT <formatting directive>
```

## Reference Implementations & Examples

### System Prompts
- [jason.md](examples/system-prompts/jason.md): Complete DHUIL system prompt reference implementation.

### Skills
- [session-init](examples/skills/session-init/SKILL.md): Session initialization and workspace mode detection.
- [new-task](examples/skills/new-task/SKILL.md): Task scaffolding and root-cause formulation.
- [fail-log](examples/skills/fail-log/SKILL.md): Post-mortem logging and error tracking.
- [senior-review](examples/skills/senior-review/SKILL.md): Code review and quality verification.
- [react-formatting](examples/skills/react-formatting/SKILL.md): React, TypeScript, and Tailwind CSS formatting standards.
- [in-depth-explanation](examples/skills/in-depth-explanation/SKILL.md): Structured technical explanation skill.

## Tooling & Editor Support

- [VS Code Extension](extensions/dhuil-vscode/): Syntax highlighting and language support for DHUIL instructions inside Markdown files.
