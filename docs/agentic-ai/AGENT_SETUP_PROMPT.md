# Minimal AI Agent Instruction File Generation Prompt

Analyze this repository and generate minimal AI agent instruction files.

The goal is to provide **repository-level instructions for coding agents**
while remaining compatible with different agent workflows used by other
teams or tools.

The generated files must be **generalizable**, **tool-agnostic**, and avoid
assumptions about specific frameworks or technologies unless they clearly
exist in the repository.

---

# Files to Generate

Create the following files.

## Root Instruction Files

1. AGENTS.md  
2. CLAUDE.md  

## GitHub Agent Adapter

3. .github/copilot-instructions.md

---

# Design Principles

AGENTS.md must be the **canonical source of truth** for repository instructions.

Other files should reference AGENTS.md and avoid duplicating repository rules.

The instructions should remain compatible with multiple coding agents
and different team workflows.

Do not assume that planning files, templates, or other agent artifacts
exist unless they are clearly present in the repository.

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

Prefer instructions that remain valid even as the repository evolves.

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

Instructions should remain compatible with different agent workflows.

Do not require specific planning tools or files unless they already
exist in the repository.

## Coding Expectations

Agents should:

- read relevant files before making changes
- maintain existing architecture and conventions
- prefer minimal and focused modifications
- avoid unnecessary dependencies
- avoid introducing breaking changes unless explicitly requested

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

# Output Format

Return the generated files using the following format.

### File: AGENTS.md
<content>

### File: CLAUDE.md
<content>

### File: .github/copilot-instructions.md
<content>
