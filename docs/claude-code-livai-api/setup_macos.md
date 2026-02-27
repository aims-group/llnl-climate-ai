# Using Claude Code with LLNL LivAI API (macOS)

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
  - [1. Install Claude Code CLI](#1-install-claude-code-cli)
  - [2. Install Visual Studio Code](#2-install-visual-studio-code)
  - [3. Install Claude Code VS Code Extension](#3-install-claude-code-vs-code-extension)
  - [4. Obtain a LivAI API Token](#4-obtain-a-livai-api-token)
- [Setup (Claude Code v2 + LivAI API)](#setup-claude-code-v2--livai-api)
  - [Step 1 - Create Your Claude LivAI API Config File](#step-1---create-your-claude-livai-api-config-file)
  - [Step 2 - Load Configuration Automatically in zsh](#step-2---load-configuration-automatically-in-zsh)
  - [Step 3 - Restart VS Code](#step-3---restart-vs-code)
  - [Step 4 - Verify Installation](#step-4---verify-installation)
    - [1. Verify in Terminal (CLI)](#1-verify-in-terminal-cli)
    - [2. Verify in VS Code (Extension UI)](#2-verify-in-vs-code-extension-ui)
- [Expected Final State](#expected-final-state)
- [Troubleshooting](#troubleshooting)
- [Security Notes](#security-notes)

## Overview

This guide configures Claude Code to:

- Use LLNL's LivAI API endpoint
- Authenticate with your LivAI API token
- Avoid Anthropic cloud login
- Work in both:
  - Terminal (CLI)
  - VS Code extension

## Prerequisites

Before starting, install the following:

### 1. Install Claude Code CLI

Official install instructions: https://code.claude.com/docs/en/overview#terminal

Typical install command:

```bash
curl -fsSL https://code.claude.com/install.sh | sh
```

Verify installation:

```bash
claude --version
```

### 2. Install Visual Studio Code

Download: https://code.visualstudio.com/

### 3. Install Claude Code VS Code Extension

From the VS Code Marketplace:\
https://marketplace.visualstudio.com/items?itemName=anthropic.claude-code

Or:

- Open VS Code
- Go to Extensions
- Search for **Claude Code**
- Install

### 4. Obtain a LivAI API Token

Request a [LivAI API token](https://llnl.servicenowservices.com/ess?id=kb_article_view&sys_kb_id=c3503dee1b6f2a548c875428624bcb1f&table=kb_knowledge&searchTerm=livai) through LLNL internal process.

You will use this token in the next step.

## Setup (Claude Code v2 + LivAI API)

> ⚠️ **Note** A [ServiceNow](https://llnl.servicenowservices.com/ess?id=kb_article_view&table=kb_knowledge&sys_kb_id=50da87dc47babe1808b62464336d43aa&recordUrl=%2Fkb_view.do%3Fsys_kb_id%3D50da87dc47babe1808b62464336d43aa) document references using `~/.claude/settings.json` for Claude v1. This does not work with Claude v2. The method below uses environment variables only.

### Step 1 - Create Your Claude LivAI API Config File

Create a Claude-specific environment file:

```bash
touch ~/.livai_claude.env
```

Add the following:

```bash
cat <<'EOF' > ~/.livai_claude.env
export ANTHROPIC_AUTH_TOKEN=YOUR_LivAI_API_TOKEN
export ANTHROPIC_BASE_URL=https://livai-api.llnl.gov
export ANTHROPIC_DEFAULT_SONNET_MODEL=claude-sonnet-4.5
export ANTHROPIC_DEFAULT_HAIKU_MODEL=claude-haiku-3
export CLAUDE_CODE_SUBAGENT_MODEL=claude-sonnet-4.5
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1
export CLAUDE_CODE_ATTRIBUTION_HEADER=0
export CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1
EOF
```

Secure the file:

```bash
chmod 600 ~/.livai_claude.env
```

### Step 2 - Load Configuration Automatically in zsh

Update `~/.zshrc`:

```bash
cat <<'EOF' >> ~/.zshrc

# LivAI Claude environment loader (dynamic)
if [ -f ~/.livai_claude.env ]; then
  source ~/.livai_claude.env

  # Push exported variables to macOS GUI session (VS Code, etc.)
  grep '^export ' ~/.livai_claude.env | cut -d' ' -f2 | cut -d= -f1 | while read var; do
    launchctl setenv "$var" "${(P)var}"
  done
fi

EOF
```

Reload your shell:

```bash
source ~/.zshrc
```

Confirm variables:

```bash
launchctl getenv ANTHROPIC_AUTH_TOKEN
launchctl getenv ANTHROPIC_BASE_URL
launchctl getenv ANTHROPIC_DEFAULT_SONNET_MODEL
launchctl getenv ANTHROPIC_DEFAULT_HAIKU_MODEL
launchctl getenv CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC
launchctl getenv CLAUDE_CODE_ATTRIBUTION_HEADER
launchctl getenv CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS
launchctl getenv CLAUDE_CODE_SUBAGENT_MODEL
```

### Step 3 - Restart VS Code

Completely quit VS Code (`Cmd + Q`), then reopen it.

### Step 4 - Verify Installation

#### 1. Verify in Terminal (CLI)

```bash
claude doctor
```

Then:

```bash
claude
```

Expected behavior:

- Starts normally
- Does not prompt for Anthropic login
- Responds to a simple prompt

Example:

```bash
Hello
```

#### 2. Verify in VS Code (Extension UI)

- Open VS Code
- Open the Claude Code panel
- Start a new chat
- Enter:

```bash
Hello from LivAI API
```

Expected behavior:

- Responds normally
- Does not prompt for Anthropic login
- Does not open a browser authentication flow

If prompted to log in, fully quit VS Code and reopen it.

## Expected Final State

You should have:

- `ANTHROPIC_AUTH_TOKEN` set
- No `ANTHROPIC_API_KEY`
- No login prompts
- No auth conflicts
- Claude responding normally in both CLI and VS Code

## Troubleshooting

If Claude asks you to log in → Restart VS Code

If it only works when launching VS Code via `code .` → Environment variables were not synced

Verify:

```bash
launchctl getenv ANTHROPIC_BASE_URL
```

If blank, restart terminal and reload `.zshrc`.

## Security Notes

- Do not commit `.livai_claude.env`
- Use `chmod 600` to restrict access
- Rotate LivAI API tokens periodically
- Do not store tokens in VS Code settings
