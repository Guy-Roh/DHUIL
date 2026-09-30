---
name: react-formatting
description: Guidelines and formatting standards for writing React, Next.js, TypeScript (.tsx), and Tailwind CSS frontend components.
---

- Name: frontend-react-1.0

## Global
### Defaults
- FORMAT using 4 spaces for indentations.
- PREFER .tsx extension for React components and .ts for hooks, utilities, and types.
- PREFER easy to maintain subcomponents OVER large monolithic components.
- PREFER explicit interface definitions OVER implicit prop types.
- AVOID any type in TypeScript codebases.
- PREFER kebab-case for file names and PascalCase for React component names.
- PREFER cn helper utility OVER string template interpolation for conditional Tailwind classes.
### Glossary
- FT: feature task
- BG: bug task
- RT: research task
- CT: current tasks

## Interpretation
#### Conditionals
- WHEN authoring or refactoring React components (.tsx) OR Next.js pages OR frontend UI code
    - INVOKE React TypeScript frontend formatting standards
    - AVOID monolithic components exceeding 150 lines

## Execution
#### Defaults
- ALWAYS author component files using .tsx extension.
- ALWAYS place semantic descriptive class names before utility Tailwind classes (e.g. className="header-cta-container flex items-center gap-4").
- ALWAYS export explicit TypeScript interfaces for component props (e.g. interface ButtonProps { ... }).
- ALWAYS type children props as React.ReactNode.
- ALWAYS type standard DOM event handlers explicitly (e.g. React.MouseEvent<HTMLButtonElement>, React.ChangeEvent<HTMLInputElement>).
- ALWAYS initialize useRef with explicit DOM element types and null (e.g. useRef<HTMLDivElement>(null)).
- ALWAYS separate complex state, side effects, or data fetching into dedicated custom hooks.
- PREFER Tailwind theme tokens OVER arbitrary CSS values.
- AVOID inline CSS style objects.
- AVOID deep JSX nesting exceeding 3 levels.
- AVOID type assertions (as Type) when type narrowing or guards are possible.
#### Conditionals
- WHEN writing conditional styles
    - PREFER clsx or twMerge helper functions
- WHEN managing component state
    - PREFER explicitly generic useState declarations when type cannot be inferred (e.g. useState<User | null>(null))
    - WHEN state is shared across features
        - LIFT state to nearest common parent or React context provider
- WHEN building UI primitives
    - WRITE reusable components in dedicated src/components/ directory

## Output
#### Defaults
- AVOID emojis.
- FORMAT component code with clear vertical separation:
    - 1. Imports
    - 2. TypeScript interfaces and types
    - 3. Component definition and hook invocations
    - 4. Event handlers and computed values
    - 5. JSX return markup