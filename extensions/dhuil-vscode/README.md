# DHUIL Language Support for VS Code

Provides syntax highlighting, selectable language mode, and formatting rules for DHUIL (Declarative Hybrid Universal Instruction Language) instructions inside standard Markdown (`.md`) files or dedicated DHUIL documents.

## Features

- **Selectable Language Mode**: Switch any document to `DHUIL` mode via the language indicator in the status bar or the Command Palette (`Change Language Mode`).
- **Markdown Compatibility**: Fully interoperable with standard Markdown formatting (headings, lists, code blocks, links, emphasis).
- **Markdown Injection**: Automatically injects DHUIL Condition, Action, and Policy tag highlights into Markdown files (`text.html.markdown`).
- **CAP & Structure Syntax Highlighting**:
    - **Block Titles** (`## GLOBAL`, `## INTERPRETATION`, `## EXECUTION`, `## OUTPUT`): mapped to block title heading scopes.
    - **Rule Classifications** (`### INVARIANTS`, `### DEFAULTS`, `### CONDITIONALS`, `### GLOSSARY`, `### SKILLS`): mapped to rule classification scopes.
    - **Conditionals** (`WHEN`, `MEANING`, `CONTAINS`, `OR`, `AND`, `NOT`, `WITH`): mapped to control keyword scopes.
    - **Actions** (`OUTPUT`, `INVOKE`, `UPDATE`, `STOP`, `AWAIT`, `SEARCH`, `ASK`, `WRITE`, `FORMAT`, `EXECUTE`, `LOG`): mapped to function / action scopes.
    - **Policies** (`ALWAYS`, `AVOID`, `ONLY`, `INSTEAD`, `PREFER`, `OVER`): mapped to storage modifier scopes.

## Local Installation

To install and use this extension in your local VS Code / Cursor / VSCodium environment:

### Option 1: Symlink (Recommended for development)

```bash
mkdir -p ~/.vscode/extensions
ln -s "$(pwd)" ~/.vscode/extensions/dhuil-vscode
```

For Cursor:
```bash
mkdir -p ~/.cursor/extensions
ln -s "$(pwd)" ~/.cursor/extensions/dhuil-vscode
```

### Option 2: Copy folder

```bash
mkdir -p ~/.vscode/extensions/dhuil-vscode
cp -r * ~/.vscode/extensions/dhuil-vscode/
```

After creating the link or copying, restart or reload VS Code (`Developer: Reload Window` from the Command Palette).
