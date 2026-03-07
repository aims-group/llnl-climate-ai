# AI Agent Instruction File Generation Prompt

Analyze this repository and generate AI agent instruction files.

The repository should support multiple coding agents while maintaining
a single canonical source of truth for repository instructions.

The generated files must be generalizable and avoid assumptions about
specific frameworks or technologies unless they clearly exist in the repository.

---

# Files to Generate

Create the following files.

## Root Instruction Files

1. AGENTS.md  
2. CLAUDE.md  
3. PLANNING.md  
4. IMPLEMENTATION.md  

## GitHub Agent Adapter

5. .github/copilot-instructions.md

## Reusable AI Templates

6. docs/ai/planning_template.md  
7. docs/ai/implementation_template.md  

AGENTS.md must be the canonical source of truth.

Other files should reference AGENTS.md where appropriate and avoid
duplicating repository rules.

Templates inside `docs/ai/` are reusable references and must not be
modified by automated agents.

PLANNING.md and IMPLEMENTATION.md are working documents that may be
updated by agents during tasks.

PLANNING.md and IMPLEMENTATION.md should be treated as local working
artifacts and typically gitignored to avoid merge conflicts or stale plans.

---

# Critical Constraints

Avoid version drift.

Do NOT include exact version numbers for:

- programming languages
- frameworks
- libraries
- development tools

Instead use general wording such as:

- "install project dependencies"
- "run the project's test suite"
- "follow the repository's conventions"

Do not invent technologies that are not present in the repository.

Do not assume a specific framework unless clearly present in the codebase.

Prefer instructions that remain valid even as the repository evolves.

---

# Planning Workflow

Agents should prefer structured planning for non-trivial changes.

The plan should follow the structure defined in:

docs/ai/planning_template.md

Typical workflow for non-trivial changes:

1. Understand the task
2. Identify relevant files
3. Create an implementation plan
4. Review the plan for completeness
5. Implement minimal and focused changes
6. Validate the result
7. Summarize modifications

If operating in an interactive environment, agents should present the
plan first and wait for confirmation before implementing.

---

# Lightweight Workflow for Small Changes

Planning and implementation templates are not required for trivial tasks.

Agents may skip `PLANNING.md` and `IMPLEMENTATION.md` if the change meets
all of the following criteria:

- modifies only a small number of files (typically 1–2)
- involves a limited number of lines changed
- does not alter architecture or system design
- does not introduce new dependencies
- does not modify public APIs, schemas, or interfaces

Examples of trivial changes:

- documentation edits
- typo fixes
- formatting or lint fixes
- small bug fixes
- minor refactors confined to a single file

For these cases agents should:

1. Make the minimal change required.
2. Verify the change does not break existing functionality.
3. Provide a short explanation in the pull request description.

For larger or more complex changes, agents should follow the full
planning and implementation workflow.

---

# AGENTS.md Requirements

AGENTS.md is the canonical guide for automated coding agents.

It should include the following sections.

## Repository Overview

Describe the purpose of the repository.

## Architecture Overview

Provide a high-level description of the project structure and major components.

Avoid framework assumptions unless clearly present.

## Development Workflow

Explain how agents should approach tasks.

Include both the lightweight workflow for small changes and the
planning-based workflow for larger changes.

## Coding Expectations

Agents should:

- read relevant files before making changes
- maintain existing architecture and conventions
- prefer minimal and focused modifications
- avoid unnecessary dependencies
- avoid introducing breaking changes unless explicitly requested

## Planning and Implementation Templates

Reusable templates are located in:

docs/ai/

Agents must:

- use `docs/ai/planning_template.md` when creating plans
- use `docs/ai/implementation_template.md` when documenting implementations
- write the active task plan to `PLANNING.md`
- write implementation summaries to `IMPLEMENTATION.md`

Agents must not modify files inside `docs/ai/`.

PLANNING.md and IMPLEMENTATION.md are working artifacts and should
generally be gitignored.

## Testing and Validation

Agents should:

- run existing tests when available
- add tests when appropriate
- provide clear verification steps for humans

## Pull Requests

When creating pull requests:

- use existing `.github` pull request templates when available
- follow repository contribution guidelines
- summarize changes clearly
- describe how the changes were tested

If multiple templates exist, select the most appropriate one.

## Handling Missing Information

If necessary information is missing:

- ask clarifying questions
- avoid guessing architecture
- document assumptions when necessary

---

# CLAUDE.md Requirements

CLAUDE.md must be minimal.

It should:

- state that AGENTS.md is the canonical instruction file
- instruct Claude-based agents to follow AGENTS.md
- avoid duplicating repository instructions

---

# Copilot Instructions Requirements

Create `.github/copilot-instructions.md`.

This file should:

- reference AGENTS.md as the canonical agent instruction file
- instruct Copilot to follow repository conventions
- remain minimal
- avoid duplicating instructions already defined in AGENTS.md

---

# PLANNING.md Requirements

PLANNING.md is the working planning document for the current task.

Agents should structure plans according to the template in:

docs/ai/planning_template.md

PLANNING.md may be updated during tasks and should generally be gitignored.

---

# IMPLEMENTATION.md Requirements

IMPLEMENTATION.md is the working implementation record for the current task.

Agents should structure implementation notes according to:

docs/ai/implementation_template.md

IMPLEMENTATION.md may be updated during tasks and should generally be gitignored.

---

# docs/ai Template Requirements

## planning_template.md

This file should contain a reusable planning template including sections such as:

- Task
- Background
- Goals
- Constraints
- Relevant files
- Step-by-step implementation plan
- Risks or edge cases
- Verification strategy

## implementation_template.md

This file should contain a reusable implementation template including sections such as:

- Task summary
- Approved plan
- Files modified
- Description of changes
- Validation steps
- Notes or assumptions

These templates must be general and reusable across tasks.

---

# Output Format

Return the generated files using the following format.

### File: AGENTS.md
<content>

### File: CLAUDE.md
<content>

### File: .github/copilot-instructions.md
<content>

### File: PLANNING.md
<content>

### File: IMPLEMENTATION.md
<content>

### File: docs/ai/planning_template.md
<content>

### File: docs/ai/implementation_template.md
<content>
