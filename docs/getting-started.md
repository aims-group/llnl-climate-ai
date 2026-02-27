# AI Tools for Climate Software Engineering at LLNL

_Last updated: February 2026_

## Table of Contents

- [Purpose](#purpose)
- [LLNL Resources](#llnl-resources)
- [Responsible & Secure Use](#responsible--secure-use)
- [Why Use AI for Climate Software?](#why-use-ai-for-climate-software)
- [AI Tool Quick Reference](#ai-tool-quick-reference)
  - [1. Daily Coding (Fast Iteration)](#1-daily-coding-fast-iteration)
  - [2. Deep Refactoring & Codebase Changes](#2-deep-refactoring--codebase-changes)
  - [3. Design, Documentation & Scientific Reasoning](#3-design-documentation--scientific-reasoning)
  - [4. Agentic Workflows & Automation](#4-agentic-workflows--automation)
  - [Additional Tools (Not LLNL-Provisioned)](#additional-tools-not-llnl-provisioned)

- [Recommended Default Workflow](#recommended-default-workflow)
- [When to Use What Tool](#when-to-use-what-tool)
- [Summary](#summary)

## Purpose

This guide provides resources for using AI in climate software engineering at LLNL. It covers paired programming tools, AI agents for structured workflows, and enterprise AI platforms.

The goal is to help climate scientists and software engineers improve productivity, maintainability, and code quality while adhering to LLNL policy and responsible AI practices.

## LLNL Resources

Consult these resources before adopting new tools or workflows:

- **LLNL AI Edge (aiEDGE)** – Central hub for AI tools, policies, trainings, and events
  [https://aiedge.llnl.gov/](https://aiedge.llnl.gov/)

- **Policies and Guidelines**
  [https://aiedge.llnl.gov/policies-and-guidelines-new-](https://aiedge.llnl.gov/policies-and-guidelines-new-)

- **LLNL ServiceNow AI Services** – AI-related knowledge base articles
  [https://llnl.servicenowservices.com/ess?id=kb_category&kb_id=f520125fdb8b83001a9efd0e0f96193f&kb_category=be1b9d5d87256edce87ffff5cebb352b](https://llnl.servicenowservices.com/ess?id=kb_category&kb_id=f520125fdb8b83001a9efd0e0f96193f&kb_category=be1b9d5d87256edce87ffff5cebb352b)

- **LLNL AI Proper Guidance (ServiceNow)**
  [https://llnl.servicenowservices.com/ess?id=kb_article_view&sys_kb_id=177ac4c41b51f6d08c875428624bcb7a](https://llnl.servicenowservices.com/ess?id=kb_article_view&sys_kb_id=177ac4c41b51f6d08c875428624bcb7a)

Models must be approved and used only with unclassified/open data. Do not use models sourced from sensitive countries.

## Responsible & Secure Use

AI tools assist development; scientific correctness and compliance remain the developer’s responsibility.

### Do

- Use approved LLM services only
- Verify AI-generated code before merging
- Generate tests and validate scientific correctness
- Use environment variables for API tokens
- Ensure compliance with export control and lab policies

### Do Not

- Upload controlled, classified, or sensitive data
- Share credentials or secrets
- Assume AI output is scientifically correct without validation

## Why Use AI for Climate Software?

Climate and Earth system software often involves:

- Large, evolving codebases
- HPC workflows and job scripts
- Complex data processing (NetCDF, xarray, Dask, CMIP)
- Legacy research code transitioning to production systems

AI tools can help by:

- Accelerating paired programming and code completion
- Explaining unfamiliar or legacy code
- Refactoring multi-file modules
- Generating tests and documentation
- Supporting structured, agent-based automation

AI should accelerate engineering productivity — not replace scientific validation or peer review.

## AI Tool Quick Reference

### 1. Daily Coding (Fast Iteration)

**Use:** GitHub Copilot
[https://github.com/features/copilot](https://github.com/features/copilot)

Capabilities:

- Inline code suggestions
- Test/function generation
- Boilerplate reduction

When:

- Writing new functions
- Routine coding
- Small updates

LLNL note: Subscription required (not lab-provided).

### 2. Deep Refactoring & Codebase Changes

**Use:** Claude Code (CLI or IDE extension)
[https://code.claude.com/docs/en/overview](https://code.claude.com/docs/en/overview)
[https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code](https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code)

Capabilities:

- Multi-file reasoning
- Architectural refactoring
- Debugging complex logic
- Terminal-based agent workflows

When:

- Large refactors
- Modernization
- Structured improvements

LLNL note: Access via LivAI API (lab-provided).

Setup instructions:
See the **Getting Started guide in this repository**:

```
docs/claude-code-livai-macos.md
```

### 3. Design, Documentation & Scientific Reasoning

**Use:** ChatGPT or Claude (Enterprise)

Capabilities:

- Explaining scientific algorithms
- Architecture comparisons
- Drafting documentation
- Converting notebooks into modules

When:

- Planning systems
- Writing documentation
- Reasoning through workflows

LLNL note: Enterprise access available via LLNL AD credentials.

### 4. Agentic Workflows & Automation

**Use:**

- **GitHub Copilot Agents**
  [https://docs.github.com/en/copilot/how-tos/use-copilot-agents](https://docs.github.com/en/copilot/how-tos/use-copilot-agents)

- **Claude Code CLI**
  [https://code.claude.com/docs/en/overview](https://code.claude.com/docs/en/overview)

- **LLM Integration in Code**
  (See repository examples under future workflow docs)

Capabilities:

- Plan → execute → validate
- Multi-step refactors
- Automated documentation
- Repository-wide updates

When:

- Large-scale changes
- Structured automation
- Supplementing scientific workflows

For Claude CLI setup with LivAI, see:

```
docs/claude-code-livai-macos.md
```

### Additional Tools (Not LLNL-Provisioned)

- OpenAI Codex / advanced GitHub agent models
- Cursor (AI-native IDE)
- Self-hosted open-source LLMs (LLaMA, Mixtral, etc.)
- Personal commercial APIs

All usage must comply with LLNL AI Proper Guidance and is restricted to unclassified data.

## Recommended Default Workflow

- Copilot → Daily coding
- Claude Code → Complex refactoring
- ChatGPT / Claude Enterprise → Design and documentation
- Agent workflows → Structured automation

AI increases clarity and productivity; scientific correctness and compliance remain the developer’s responsibility.

## When to Use What Tool

| Scenario                      | Recommended Tool    |
| ----------------------------- | ------------------- |
| Writing new functions         | Copilot             |
| Refactoring multiple modules  | Claude Code         |
| Designing system architecture | ChatGPT             |
| Debugging complex logic       | Claude Code         |
| Generating documentation      | ChatGPT or Claude   |
| Large automated changes       | Claude CLI / Agents |

## Summary

AI tools can significantly accelerate climate software engineering by supporting:

- Paired programming
- Code modernization
- Documentation and testing
- Agent-based automation

A practical baseline stack includes:

- GitHub Copilot
- Claude Code
- ChatGPT
- Agent workflows for complex tasks

Use AI to improve clarity, maintainability, and productivity — while maintaining scientific rigor and adherence to LLNL policies.
