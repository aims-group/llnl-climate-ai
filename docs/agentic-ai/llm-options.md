# LLM Options for Agentic Scientific Code at LLNL

## Table of Contents

- [Overview](#overview)
- [What this page is not](#what-this-page-is-not)
- [When to use which option](#when-to-use-which-option)
- [Option 1 - LLNL-Provided LLMs (Recommended)](#option-1---llnl-provided-llms-recommended)
  - [1. LivAI API](#1-livai-api)
  - [2. Livermore Computing LLamaMe](#2-livermore-computing-llamame)
- [Option 2 - Open-Source/Self-Hosted LLMs](#option-2---open-sourceself-hosted-llms)
  - [1. LLaMA 3.1 (8B)](#1-llama-31-8b)
  - [Other candidates (if allowed)](#other-candidates-if-allowed)
- [Option 3 - Hosted commercial APIs](#option-3---hosted-commercial-apis)
  - [1. Claude 3.5 Sonnet](#1-claude-35-sonnet)
  - [2. GPT-4.1 / GPT-4o](#2-gpt-41--gpt-4o)

## Overview

This page covers large language models (LLMs) suitable for **agentic workflows** in scientific code. It is opinionated based on my (Tom’s) personal workflow and experience, but can be curated based on a general pattern across the team.

Whenever possible, use [**LLNL-provided LLM APIs** (Option 1)](<https://e3sm.atlassian.net/wiki/spaces/IPD/pages/5821923334/Getting+Started+-+LLMs+for+scientific+agentic+prototyping#Option-1---LLNL-Provided-LLMs-(Recommended)>) as they avoid self-hosting overhead and do not require personal commercial subscriptions. **Self-hosted open-source models** are a good alternative for rapid local prototyping when policy allows.

All usage must comply with **LLNL AI Proper Guidance** and is restricted to **unclassified data only**.

## What this page is not

- Not for production deployment
- Not an authorization document
- Not for classified or sensitive data

## When to use which option

| Use case                         | Recommended option         |
| -------------------------------- | -------------------------- |
| Quick PoC, no setup              | Option 1 – LivAI           |
| LC workflows / on-cluster agents | Option 1 – LLamaMe         |
| Offline prototyping              | Option 2 – Self-hosted     |
| External demo / paper figures    | Option 3 – Commercial APIs |

## Option 1 - LLNL-Provided LLMs (Recommended)

**Summary:** Lab-approved, lowest friction, policy-aligned option.

**Pros:**

- ✅ Fully aligned with LLNL AI Proper Guidance
- ✅ No personal billing or subscriptions
- ✅ No self-hosting or model maintenance
- ✅ Centralized credentialing and access control
- ✅ Suitable for demos, internal tools, and exploratory agents

**Cons:**

- ⚠️ Limited model selection compared to the open market
- ⚠️ Usage caps ($500 yearly)
- ⚠️ Knowledge cutoff may lag newest public releases
- ⚠️ Less control over low-level model configuration

### 1. LivAI API

**What it is:**
LivAI provides API access to multiple commercial models (e.g., OpenAI and Anthropic) through a single LLNL-approved interface.

**How to request/use:**

- Request access [here](https://llnl.servicenowservices.com/ess?id=kb_article_view&sysparm_article=KB0026324)
- [Getting started with LivAI API: usage, model selection, and spend caps](https://llnl.servicenowservices.com/ess?id=kb_article_view&sysparm_article=KB0026324#a2)

**Notes:**

- Knowledge cutoff is typically ~2023–2024, which is sufficient for most proof-of-concepts
- There is a $500 yearly usage cap

**Resources:**

- [Usage Dashboard](https://livai-tools.llnl.gov/usage/dashboard)
- [Swagger API Docs](https://livai-api.llnl.gov/)
- [Using Claude Code with LivAPI](https://llnl.servicenowservices.com/ess?id=kb_article_view&table=kb_knowledge&sys_kb_id=50da87dc47babe1808b62464336d43aa&recordUrl=%2Fkb_view.do%3Fsys_kb_id%3D50da87dc47babe1808b62464336d43aa) – supported as of Jan/2026. includes guide for Claude Code CLI and Claude Code VS Code Extension (which includes CLI through VS Code terminal)

**Pros**

- ✅ Fastest way to start (no infra, no installs)
- ✅ Access to high-quality frontier models
- ✅ Good default choice for agentic PoCs
- ✅ Stable APIs for tools, planning, and code generation

**Cons**

- ⚠️ Yearly usage limit
- ⚠️ Internet-style models (not domain-specialized)
- ⚠️ Cannot run fully offline (requires LLNL network access/VPN)

### 2. Livermore Computing LLamaMe

**What it is:**
An LLM API service hosted by Livermore Computing (LC) for use on LC systems (CZ, RZ, SCF).

**Data allowed:**
Unclassified LLNL data appropriate for the LC zone you are working in (follow LC & cyber rules).

**How to request/use:**

1.  Go to [https://hpc.llnl.gov/services/cloud-services/ai-ml-services](https://hpc.llnl.gov/services/cloud-services/ai-ml-services)
2.  Click [https://hpc.llnl.gov/services/cloud-services/ai-ml-services/llamame-llm-api-service](https://hpc.llnl.gov/services/cloud-services/ai-ml-services/llamame-llm-api-service)
3.  Obtain an API key via [https://hpc.llnl.gov/services/cloud-services/launchit](https://hpc.llnl.gov/services/cloud-services/launchit)

**Support:**

- LC Hotline: [lc-hotline@llnl.gov](mailto:lc-hotline@llnl.gov), (925) 422‑4531

**Pros**

- ✅ Designed for LC environments and workflows
- ✅ No external data egress
- ✅ Good fit for on-cluster agents and pipelines
- ✅ Stable and supported by LC

**Cons**

- ⚠️ Only available on LC systems
- ⚠️ Model selection may lag commercial APIs
- ⚠️ Less suitable for quick laptop-based PoCs

## Option 2 - Open-Source/Self-Hosted LLMs

**Summary:** Best for offline work, experimentation, and understanding model behavior—but with higher setup and maintenance cost.

These LLMs require hosting via an LLM backend such as **Ollama**. Follow the **LLNL AI Proper Guidance Page** before using any open-source LLM.

**Key policy notes:**

- Unclassified data only
- Model must not originate from a sensitive country
- Presence on Hugging Face does not imply approval (e.g., **Qwen 2.5 is not permitted**)

**Pros:**

- ✅ Full control over prompts, context, and runtime
- ✅ Can run fully offline
- ✅ No per-token costs
- ✅ Useful for rapid local iteration and debugging

**Cons:**

- ⚠️ You are responsible for compliance and vetting
- ⚠️ Requires GPU/CPU resources and setup (can be much slower)
- ⚠️ Lower capability than frontier commercial models
- ⚠️ More prompt engineering required for agents

Note: These are examples based on personal use.

### 1. LLaMA 3.1 (8B)

- Link: [https://www.llama.com/llama3_1/](https://www.llama.com/llama3_1/)

**Pros:**

- ✅ Strong instruction following for its size
- ✅ Good balance of quality and performance
- ✅ Widely supported by tooling (Ollama, vLLM)

**Cons:**

- ⚠️ Needs more prompt scaffolding for planning
- ⚠️ Weaker long-horizon reasoning
- ⚠️ Tool use less reliable than larger modelsOthers

### Other candidates (if allowed)

- **Mixtral** – Strong MoE reasoning, higher resource cost
- **Phi-3** – Lightweight, good for structured tasks
- **Gemma** – Clean outputs, weaker reasoning depth

(Add models here only after verifying policy compliance.)

## Option 3 - Hosted commercial APIs (e.g., GPT, Claude)

**Summary:** Highest model quality, best for polished demos and figures—but not LLNL-provisioned. The ones listed here are examples.

⚠️ Requires a **personal account with active billing**. LLNL does **not** provide API credits, and LLNL accounts may not be used. Instead, use [LivAI API](https://e3sm.atlassian.net/wiki/spaces/AIMS/pages/5931204609/LLM+Options+for+Agentic+Scientific+Code+at+LLNL#1.-LivAI).

**Pros:**

- ✅ Access to best-in-class frontier models
- ✅ Excellent tool use and agentic behavior
- ✅ Fast inference and high reliability
- ✅ Ideal for external demos and paper figures

**Cons:**

- ⚠️ Personal cost and billing management
- ⚠️ Not centrally approved or provisioned by LLNL
- ⚠️ Data handling must be carefully validated
