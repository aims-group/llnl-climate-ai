# Template: AI Instructions for GitHub Repositories

## Overview

This template is useful for adding AI-assisted development into repositories by introducing:

### 1. A canonical governance file: `AGENTS.md` (single source of truth)

`AGENTS.md` defines architectural rules, coding standards, testing philosophy, and dependency policy at a structural (not version) level.

### 2. Lightweight, tool-specific instruction files: `.github/copilot-instructions.md`, `.claude/CLAUDE.md`

Tool-specific files are lightweight enforcement layers:

- Concise and behavioral
- Derived from `AGENTS.md`
- Free of version numbers and volatile configuration
- Stable even as dependencies, compilers, or CI change

The model is language-agnostic and applies across Python, C++, and other ecosystems.

## How to Use

### 1. Create an Issue in Your Repo and Assign to Copilot

Open a new GitHub issue using the [Issue Template](#issue-template) provided at the bottom of this document.

- Example title: `Add repository-level custom AI instruction files (Copilot, Agents, Claude)`
- Recommended model: Any advanced model (e.g., Claude Opus, GPT Codex)

![AI Instruction File Governance Model](repo-instructions.png)

### 2. Review Related Pull Request and Refine (as needed)

Refine with Copilot until:

- Architectural constraints are clear
- Anti-hallucination rules are strong
- Policies are language-agnostic
- Tool-specific files contain necessary workflow-specific guardrails
  (e.g., PR/diff scope constraints for Copilot, multi-file edit and refactor limits for Claude)

Example pull request: https://github.com/E3SM-Project/e3sm_diags/pull/1039

### 3. Merge

Commit and merge once satisfied.

Future architectural changes update `AGENTS.md`.
Tool-specific files should not require edits for dependency or CI version changes.

---

## Issue Template

```markdown
## Summary

Introduce repository-level AI instruction files to standardize AI-assisted development across tools and programming languages. These files define shared coding standards, architectural constraints, and project conventions so AI agents generate consistent, context-aware output without repeated prompt context.

Reference: https://code.visualstudio.com/docs/copilot/customization/custom-instructions

Establish a canonical-source and anti-drift policy to prevent instruction files from becoming stale as dependencies, CI configuration, tooling, or supported languages evolve.

## Objective

Ensure consistent AI behavior across:

- GitHub Copilot (VS Code Chat)
- Claude-based tools
- Multi-agent or automated AI workflows operating on the repository

Across all supported languages (e.g., Python, C++, and others), instruction files must:

- Reflect project coding standards
- Capture architectural patterns and cross-language constraints
- Define testing philosophy and enforcement expectations
- Encode dependency policies at a policy level (not version level)
- Document project-specific constraints
- Avoid drift-prone configuration duplication

## Canonical Source & Anti-Drift Policy

To minimize maintenance overhead and configuration drift:

1. `AGENTS.md` is the canonical, tool-agnostic and language-agnostic source of AI development rules.
2. Tool-specific instruction files are concise, derived artifacts.
3. Language-specific conventions must be defined structurally (style rules, architectural boundaries, safety constraints), not via hardcoded configuration values.
4. Volatile configuration data must never be embedded directly in tool-specific files.

### Prohibited Hardcoding

The following must not be statically embedded in tool-specific instruction files:

- Exact dependency versions (for any language)
- Version ranges or pinned constraints
- Specific compiler versions
- Specific interpreter minor versions (unless policy-level)
- CI matrix versions
- Tool configuration values
- Counts of modules, targets, drivers, or files
- Experimental feature states
- Any numeric or enumerated value that may change over time

When necessary, reference authoritative sources instead, such as:

- `pyproject.toml`
- `CMakeLists.txt`
- `setup.cfg`
- `pre-commit-config.yaml`
- `package.json`
- GitHub Actions workflows
- Build system configuration files
- Source code defaults

### Structural Over Quantitative

**Prefer:**

- Architectural rules
- Design principles
- Interface and boundary definitions
- Capability-based descriptions
- Policy-level constraints
- Language-agnostic behavioral requirements

**Avoid:**

- Numeric counts
- Enumerations of dynamic structures
- Repetition of dependency specifications
- Copying configuration values into instruction files
- Language-specific version pinning

### Regeneration Requirement

Tool-specific instruction files must:

- Remain valid if dependencies, compilers, interpreters, or CI configurations change
- Contain no drift-prone values
- Be safely regenerable from `AGENTS.md` without manual synchronization edits
- Not require updates solely due to version changes in any supported language ecosystem

## Requirements

### `AGENTS.md` (Canonical)

- Located at repository root
- Single source of truth
- Tool-agnostic and language-agnostic
- Documents:
  - System architecture and design constraints
  - Cross-language boundaries and integration rules
  - Language-specific coding standards (Python, C++, etc.) at a policy level
  - Logging and observability practices
  - Testing philosophy (unit, integration, system-level)
  - Concurrency and execution constraints
  - Dependency and build policy (policy-level only)
  - Anti-hallucination expectations for AI agents
- Must not embed volatile configuration values (versions, matrix entries, numeric counts)

### `.github/copilot-instructions.md`

- Located under `.github/`
- Applies automatically to Copilot Chat
- Concise and enforceable
- Derived from `AGENTS.md`
- Must not introduce configuration drift
- Must remain effective without duplicating volatile configuration
- Must apply across all supported languages in the repository

**Implementation Requirement:**

- The Copilot instruction file **must be created using the Copilot Instructions (Template) provided below**.
- The template must be copied structurally and adapted only to reference `AGENTS.md`.
- No additional architectural policy, configuration values, or version-specific information may be introduced beyond what is defined in `AGENTS.md`.

### `.claude/CLAUDE.md`

- Located under `.claude/`
- Compatible with Claude Code and related tools
- Concise and enforceable
- Derived from `AGENTS.md`
- Must remain effective without duplicating volatile configuration
- Must apply across all supported languages in the repository

**Implementation Requirement:**

- The Claude instruction file **must be created using the Claude Instructions (Template) provided below**.
- The template must be copied structurally and adapted only to reference `AGENTS.md`.
- No additional architectural policy, configuration values, or version-specific information may be introduced beyond what is defined in `AGENTS.md`.

## Acceptance Criteria

- [ ] `AGENTS.md` exists at repository root and is canonical.
- [ ] `AGENTS.md` defines cross-language architectural and policy constraints.
- [ ] `.github/copilot-instructions.md` exists and aligns with canonical rules.
- [ ] `.claude/CLAUDE.md` exists and aligns with canonical rules.
- [ ] Tool-specific files are created using the provided templates.
- [ ] No tool-specific file embeds volatile configuration values (across any language ecosystem).
- [ ] Tool-specific files remain valid if dependency versions, compiler versions, or CI settings change.
- [ ] AI-generated code in Python, C++, or other supported languages reflects project standards without repeated prompting.
- [ ] Documentation clearly distinguishes canonical vs. derived responsibilities.

## Governance Model

- `AGENTS.md` is the single source of truth.
- Tool-specific files are concise derivatives.
- Tool-specific files must be generated from the provided templates.
- Tool-specific files may reference `AGENTS.md`, but must not duplicate architectural policy.
- Configuration values must be referenced, not copied.
- Language ecosystems (Python, C++, etc.) must be governed at the policy level, not the version level.
- Architectural policy belongs only in `AGENTS.md`.

## Claude Instructions (Template)

> **Canonical source:** [`AGENTS.md`](../AGENTS.md) is the single source of truth for AI development rules.  
> Read and apply `AGENTS.md` in full before generating any code or responses.

### Behavior

- Apply all rules from `AGENTS.md` to every response and code generation task.
- Apply language-specific policies (Python, C++, etc.) as defined in `AGENTS.md`.
- Read relevant source files before making changes — do not assume file contents, module structure, build system, or configuration.
- Do not generate code that violates architectural constraints, coding standards, or dependency/build policies defined in `AGENTS.md`.
- Do not hallucinate files, modules, build targets, or configuration that are not present in the repository.
- Do not hardcode dependency versions, compiler versions, CI matrix values, or other volatile configuration — reference authoritative source files listed in `AGENTS.md`.
- When running commands, follow the development workflow, build system, and testing conventions defined in `AGENTS.md`.
- When uncertain about project or language conventions, consult `AGENTS.md` and the key reference files it lists before responding.

## Copilot Instructions (Template)

> **Canonical source:** [`AGENTS.md`](../AGENTS.md) is the single source of truth for AI development rules.  
> Read and apply `AGENTS.md` in full before generating any code or responses.

### Behavior

- Apply all rules from `AGENTS.md` automatically to every workspace chat response.
- Apply language-specific policies (Python, C++, etc.) as defined in `AGENTS.md`.
- Prefer repository context over speculative patterns — inspect actual files and build configuration before suggesting code.
- Do not generate code that violates architectural constraints, coding standards, or dependency/build policies defined in `AGENTS.md`.
- Do not hallucinate files, modules, build targets, or configuration that are not present in the repository.
- Do not hardcode dependency versions, compiler versions, CI matrix values, or other volatile configuration — reference authoritative source files listed in `AGENTS.md`.
- When uncertain about project or language conventions, consult `AGENTS.md` and the key reference files it lists before responding.

## Notes

Instruction files must be:

- Concise
- Enforceable
- Structural rather than configuration-specific
- Language-agnostic at the policy level
- Regenerable without ongoing manual maintenance

The goal is consistent, cross-language AI-assisted development with minimal long-term operational overhead.
```
