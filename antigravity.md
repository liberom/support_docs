# Google Antigravity Documentation Reference

## Introduction

Google Antigravity is an agentic development platform that evolves the traditional IDE into an agent-first development environment. The platform enables developers to work at a higher, task-oriented level by managing AI agents across multiple workspaces while retaining a familiar AI-powered IDE experience at its core. Antigravity provides agents with autonomous capabilities to operate across the editor, terminal, and browser, emphasizing verification and higher-level communication via tasks and artifacts.

This repository contains a local mirror of the official Google Antigravity documentation extracted from `https://antigravity.google/docs/`. It serves as an offline, searchable, and version-controlled snapshot for reference purposes. The documentation covers the complete feature set including the Agent system, Editor capabilities, Browser integration, MCP (Model Context Protocol) support, Skills framework, and various artifact types used for agent-user communication.

## Core Components

### Agent System

The Agent is the main AI functionality within Google Antigravity—a multi-step reasoning system powered by frontier LLMs that can reason over existing code, use tools including browser automation, and communicate through tasks and artifacts.

```bash
# Agent conversation modes
# Planning Mode: For deep research, complex tasks, or collaborative work
# Fast Mode: For simple tasks that can be completed quickly

# Agent settings location
# Global rules: ~/.gemini/GEMINI.md
# Workspace rules: .agent/rules/

# Terminal command auto-execution policies
# - Request Review: Never auto-execute (except allowlist)
# - Always Proceed: Never ask for review (except denylist)
```

### Model Selection

Antigravity offers multiple frontier models from the Google Vertex Model Garden for core reasoning tasks.

```bash
# Available reasoning models:
# - Gemini 3 Pro (high)
# - Gemini 3 Pro (low)
# - Gemini 3 Flash
# - Claude Sonnet 4.5
# - Claude Sonnet 4.5 (thinking)
# - Claude Opus 4.5 (thinking)
# - GPT-OSS

# Additional specialized models (not user-configurable):
# - Nano Banana Pro: Generative image tool
# - Gemini 2.5 Pro UI Checkpoint: Browser subagent actuation
# - Gemini 2.5 Flash: Checkpointing and context summarization
# - Gemini 2.5 Flash Lite: Codebase semantic search
```

### Editor Features

The Editor is the primary entry point—a VS Code-based surface with rich AI-enabled features including Tab completions, Command prompts, and Agent integration.

```bash
# Keyboard shortcuts
# Open Agent Manager: Cmd + E (Mac) / Ctrl + E (Windows)
# Open Settings: Cmd + , (Mac) / Ctrl + , (Windows)
# Trigger Command: Cmd + I (Mac) / Ctrl + I (Windows)
# Toggle Terminal: Cmd + J (Mac) / Ctrl + J (Windows)
# Open Quick Picker: Cmd + P (Mac) / Ctrl + P (Windows)

# Tab features
# - Supercomplete: File-wide code suggestions
# - Tab-to-Jump: Navigate to next logical edit location
# - Tab-to-Import: Auto-add missing import statements
```

### Browser Integration

Antigravity can open, read, and control a Chrome browser for testing, reading internet data, and automating browser tasks via a specialized subagent.

```bash
# Browser subagent capabilities:
# - Clicking, scrolling, typing
# - Reading console logs
# - DOM capture, screenshots, markdown parsing
# - Video recording of actions

# Browser security settings:
# - Denylist: Server-side check via Google Superroots BadUrlsChecker
# - Allowlist: Local text file for trusted URLs
# - Runs in separate Chrome profile for isolation

# Chrome profile location setting:
# Configurable in Settings > Browser section
```

### MCP Integration

The Model Context Protocol allows Antigravity to securely connect to local tools, databases, and external services for real-time context.

```json
// Custom MCP server configuration location:
// Access via "..." dropdown > MCP Store > Manage MCP Servers > View raw config
// File: mcp_config.json

// Supported integrations include:
// - Databases: BigQuery, PostgreSQL, MySQL, MongoDB, Redis, Spanner
// - DevOps: GitHub, Heroku, Netlify, Firebase
// - Project Management: Linear, Notion, Atlassian, Dart
// - Design: Figma Dev Mode
// - Payments: Stripe, PayPal
// - AI/ML: Perplexity Ask, Pinecone
```

### Skills Framework

Skills are reusable packages extending agent capabilities, following an open standard with instructions for specific task types.

```markdown
<!-- Skill directory locations -->
<!-- Workspace-specific: <workspace-root>/.agent/skills/<skill-folder>/ -->
<!-- Global: ~/.gemini/antigravity/skills/<skill-folder>/ -->

<!-- Required SKILL.md structure -->
---
name: my-skill
description: Helps with a specific task. Use when you need to do X or Y.
---

# My Skill

Detailed instructions for the agent.

## When to use this skill
- Use this when...

## How to use it
Step-by-step guidance for the agent.
```

### Rules and Workflows

Rules are manually defined constraints for the Agent at local and global levels. Workflows define step sequences for repetitive tasks.

```markdown
<!-- Global rules location: ~/.gemini/GEMINI.md -->
<!-- Workspace rules location: .agent/rules/ -->

<!-- Rule activation modes -->
<!-- - Manual: Activated via @ mention in Agent input -->
<!-- - Always On: Applied to all conversations -->
<!-- - Model Decision: Applied based on natural language description -->
<!-- - Glob: Applied to files matching pattern (e.g., *.js, src/**/*.ts) -->

<!-- Workflow invocation -->
<!-- Use /workflow-name in Agent conversation -->
<!-- Workflows can call other workflows: /workflow-1 can include "Call /workflow-2" -->

<!-- File reference syntax in rules -->
<!-- @filename - relative to rules file location -->
<!-- @/path/to/file.md - absolute or workspace-relative path -->
```

### Artifacts

Artifacts are anything the agent creates to accomplish work or communicate with users, including markdown files, diff views, diagrams, images, and browser recordings.

```bash
# Artifact types:
# - Task List: Tracks complex task progress
# - Implementation Plan: Architects codebase changes
# - Walkthrough: Summarizes completed changes
# - Knowledge Items: Persistent memory across conversations
# - Browser Screenshots: Page state captures
# - Browser Recordings: Action playback videos

# Artifact review policies:
# - Always Proceed: Agent never asks for review
# - Request Review: Agent always asks for review

# Artifact storage location:
# ~/.antigravity/ (application root folder)
```

### Secure Mode

Secure Mode provides enhanced security controls restricting agent access to external resources and sensitive operations.

```bash
# Secure Mode enforces:
# - Browser URL Allowlist/Denylist for external resources
# - Terminal Auto Execution: Always "Request Review"
# - Browser Javascript Execution: Always "Request Review"
# - Artifact Review: Always "Request Review"
# - File System: Respects .gitignore, workspace isolation enabled

# Access restrictions in Secure Mode:
# - Agent can only access files within designated workspace
# - External file access disabled
# - Terminal allowlist ignored
```

## Summary

Google Antigravity serves developers who want to leverage AI agents for complex software development tasks including feature implementation, UI iteration, bug fixing, research, and report generation. The platform's primary use cases include managing multiple AI agents across different workspaces, automating browser-based testing and data collection, maintaining persistent knowledge across coding sessions, and creating reusable workflows for repetitive development processes. The Agent Manager provides a birds-eye view for orchestrating dozens of agents simultaneously while the Editor offers a familiar code-writing experience augmented with AI features.

Integration patterns center around the Skills framework for extending agent capabilities, the MCP protocol for connecting external tools and databases, and the Rules/Workflows system for codifying team-specific conventions and processes. Developers can customize agent behavior through workspace-specific or global configuration files, define security policies via Secure Mode, and create persistent memories through Knowledge Items. The platform supports a progressive disclosure pattern where agents discover and activate relevant skills based on conversation context, enabling flexible automation while maintaining user control over sensitive operations.
