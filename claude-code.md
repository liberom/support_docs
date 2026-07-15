# Claude Code

Claude Code is Anthropic's agentic coding tool that lives in your terminal, understands your codebase, and helps you code faster through natural language commands. It executes routine tasks, explains complex code, handles git workflows, and integrates with your IDE—all via conversational interactions. Use it in your terminal, VS Code, or tag @claude on GitHub.

This repository contains the official Claude Code plugins, examples, and configuration templates. The plugin system extends Claude Code with custom slash commands, specialized agents, hooks for event-driven automation, and MCP (Model Context Protocol) integrations. Plugins enable teams to standardize workflows, enforce coding guidelines, and automate repetitive development tasks across projects.

## Installation

Install Claude Code using one of the recommended methods.

```bash
# MacOS/Linux (Recommended)
curl -fsSL https://claude.ai/install.sh | bash

# Homebrew (MacOS/Linux)
brew install --cask claude-code

# Windows (PowerShell)
irm https://claude.ai/install.ps1 | iex

# Windows Package Manager
winget install Anthropic.ClaudeCode

# NPM (Deprecated)
npm install -g @anthropic-ai/claude-code

# Navigate to your project and start Claude Code
cd /path/to/your/project
claude
```

## Plugin Structure

Standard Claude Code plugin directory structure for creating custom extensions.

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json          # Plugin metadata and configuration
├── commands/                 # Slash commands (*.md files)
├── agents/                   # Specialized AI agents (*.md files)
├── skills/                   # Agent skills with SKILL.md
├── hooks/                    # Event handlers (hooks.json + scripts)
│   └── hooks.json
├── .mcp.json                 # External MCP tool configuration
└── README.md                 # Plugin documentation
```

```json
// Example .claude-plugin/plugin.json
{
  "name": "my-custom-plugin",
  "version": "1.0.0",
  "description": "A custom Claude Code plugin for workflow automation",
  "author": {
    "name": "Your Name",
    "email": "you@example.com"
  }
}
```

## /commit - Create Git Commit

Automatically stage changes and create a well-formatted git commit based on your current diff.

```markdown
<!-- File: commands/commit.md -->
---
allowed-tools: Bash(git add:*), Bash(git status:*), Bash(git commit:*)
description: Create a git commit
---

## Context

- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Current branch: !`git branch --show-current`
- Recent commits: !`git log --oneline -10`

## Your task

Based on the above changes, create a single git commit.
Stage and create the commit using a single message.
```

```bash
# Usage in Claude Code
/commit

# Claude will:
# 1. Review git status and diff
# 2. Stage appropriate files
# 3. Generate a descriptive commit message
# 4. Create the commit
```

## /commit-push-pr - Full Git Workflow

Complete git workflow automation: create branch, commit, push, and open a pull request.

```markdown
<!-- File: commands/commit-push-pr.md -->
---
allowed-tools: Bash(git checkout --branch:*), Bash(git add:*), Bash(git status:*), Bash(git push:*), Bash(git commit:*), Bash(gh pr create:*)
description: Commit, push, and open a PR
---

## Context

- Current git status: !`git status`
- Current git diff (staged and unstaged changes): !`git diff HEAD`
- Current branch: !`git branch --show-current`

## Your task

Based on the above changes:

1. Create a new branch if on main
2. Create a single commit with an appropriate message
3. Push the branch to origin
4. Create a pull request using `gh pr create`
```

```bash
# Usage in Claude Code
/commit-push-pr

# Claude will automatically:
# 1. Check if on main branch and create feature branch if needed
# 2. Stage and commit all changes
# 3. Push to remote with upstream tracking
# 4. Open a pull request with auto-generated description
```

## /code-review - Automated PR Review

Multi-agent code review system with confidence-based scoring to filter false positives.

```markdown
<!-- File: commands/code-review.md -->
---
allowed-tools: Bash(gh pr view:*), Bash(gh pr diff:*), Bash(gh pr comment:*), mcp__github_inline_comment__create_inline_comment
description: Code review a pull request
---

Provide a code review for the given pull request.

Steps:
1. Launch haiku agent to check PR status (closed, draft, already reviewed)
2. Launch haiku agent to find relevant CLAUDE.md files
3. Launch sonnet agent to summarize PR changes
4. Launch 4 parallel review agents:
   - 2 CLAUDE.md compliance agents
   - 2 Bug detection agents (using Opus)
5. Validate each issue with follow-up agents
6. Filter to high-signal issues only
7. Output summary or post inline comments with --comment flag
```

```bash
# Usage in Claude Code
/code-review

# Review and post comments to GitHub
/code-review --comment

# Expected output without --comment:
# ## Code Review Summary
#
# ### Critical Issues (2 found)
# - [Bug Agent]: Null pointer dereference at src/api.ts:45
# - [CLAUDE.md]: Missing error handling per guidelines
#
# ### No Issues Found Categories
# - Security vulnerabilities
# - Type errors
```

## /feature-dev - Guided Feature Development

Comprehensive 7-phase feature development workflow with specialized agents.

```markdown
<!-- File: commands/feature-dev.md -->
---
description: Guided feature development with codebase understanding and architecture focus
argument-hint: Optional feature description
---

# Feature Development

## Core Principles
- Ask clarifying questions before implementation
- Understand existing code patterns first
- Read files identified by exploration agents
- Use TodoWrite to track all progress

## Phases
1. Discovery - Understand requirements
2. Codebase Exploration - Launch code-explorer agents
3. Clarifying Questions - Resolve all ambiguities
4. Architecture Design - Launch code-architect agents
5. Implementation - Build with approval
6. Quality Review - Launch code-reviewer agents
7. Summary - Document what was built
```

```bash
# Usage in Claude Code
/feature-dev Add user authentication with OAuth support

# Claude will:
# 1. Create todo list with all phases
# 2. Launch 2-3 code-explorer agents to understand codebase
# 3. Ask clarifying questions (OAuth providers, session handling, etc.)
# 4. Launch code-architect agents with different approaches
# 5. Present architecture options and get approval
# 6. Implement chosen approach
# 7. Launch code-reviewer agents for quality check
# 8. Summarize changes and next steps
```

## code-explorer Agent

Specialized agent for deep codebase analysis and feature tracing.

```markdown
<!-- File: agents/code-explorer.md -->
---
name: code-explorer
description: Deeply analyzes existing codebase features by tracing execution paths, mapping architecture layers, understanding patterns and abstractions
tools: Glob, Grep, LS, Read, NotebookRead, WebFetch, TodoWrite, WebSearch
model: sonnet
color: yellow
---

You are an expert code analyst specializing in tracing feature implementations.

## Analysis Approach

1. **Feature Discovery** - Find entry points, core files, boundaries
2. **Code Flow Tracing** - Follow call chains, trace data transformations
3. **Architecture Analysis** - Map abstraction layers, identify patterns
4. **Implementation Details** - Key algorithms, error handling, performance

## Output

- Entry points with file:line references
- Step-by-step execution flow
- Key components and responsibilities
- List of essential files for understanding the feature
```

```bash
# Agent is automatically launched by /feature-dev command
# Or invoke directly via Task tool:

# In Claude Code conversation:
"Launch a code-explorer agent to analyze the authentication system"

# Agent returns:
# - Entry points: src/auth/index.ts:15, src/middleware/auth.ts:8
# - Flow: Request → AuthMiddleware → TokenValidator → UserService
# - Key files to read: auth/index.ts, models/user.ts, middleware/auth.ts
```

## code-architect Agent

Architecture design agent that creates implementation blueprints.

```markdown
<!-- File: agents/code-architect.md -->
---
name: code-architect
description: Designs feature architectures by analyzing existing patterns and providing implementation blueprints
tools: Glob, Grep, LS, Read, NotebookRead, WebFetch, TodoWrite, WebSearch
model: sonnet
color: green
---

You are a senior software architect delivering actionable architecture blueprints.

## Core Process

1. **Pattern Analysis** - Extract existing conventions and architectural decisions
2. **Architecture Design** - Make decisive choices, ensure integration
3. **Implementation Blueprint** - Specify every file, component, and data flow

## Output

- Patterns & Conventions Found with file:line references
- Architecture Decision with rationale
- Component Design with responsibilities
- Implementation Map with specific files to create/modify
- Build Sequence as phased checklist
```

```bash
# Agent launched by /feature-dev during Phase 4
# Provides structured output:

# ## Architecture Decision: OAuth2 with PKCE Flow
#
# ### Patterns Found
# - Existing auth uses JWT tokens (src/auth/jwt.ts:12)
# - Middleware pattern for route protection
#
# ### Files to Create
# - src/auth/oauth/provider.ts - OAuth provider interface
# - src/auth/oauth/google.ts - Google OAuth implementation
#
# ### Build Sequence
# 1. Create provider interface
# 2. Implement Google provider
# 3. Add OAuth routes
# 4. Update auth middleware
```

## /pr-review-toolkit:review-pr - Comprehensive PR Review

Multi-agent PR review with specialized analyzers for different code quality aspects.

```markdown
<!-- File: commands/review-pr.md -->
---
description: "Comprehensive PR review using specialized agents"
argument-hint: "[review-aspects]"
allowed-tools: ["Bash", "Glob", "Grep", "Read", "Task"]
---

# Comprehensive PR Review

## Available Review Aspects
- **comments** - Analyze code comment accuracy
- **tests** - Review test coverage quality
- **errors** - Check error handling for silent failures
- **types** - Analyze type design and invariants
- **code** - General code review
- **simplify** - Simplify code for clarity
- **all** - Run all applicable reviews (default)

## Agents
- comment-analyzer: Verifies comment accuracy
- pr-test-analyzer: Reviews behavioral test coverage
- silent-failure-hunter: Finds silent failures
- type-design-analyzer: Analyzes type encapsulation
- code-reviewer: Checks guidelines compliance
- code-simplifier: Simplifies complex code
```

```bash
# Full review (default)
/pr-review-toolkit:review-pr

# Specific aspects only
/pr-review-toolkit:review-pr tests errors

# Review only code comments
/pr-review-toolkit:review-pr comments

# Parallel review (faster)
/pr-review-toolkit:review-pr all parallel

# Expected output:
# # PR Review Summary
#
# ## Critical Issues (1 found)
# - [silent-failure-hunter]: Catch block swallows error at api.ts:89
#
# ## Important Issues (2 found)
# - [pr-test-analyzer]: Missing edge case test for null input
# - [type-design-analyzer]: Type allows invalid state
#
# ## Strengths
# - Good separation of concerns
# - Clear function naming
```

## /hookify - Create Custom Behavior Hooks

Create hooks to prevent unwanted behaviors through conversation analysis.

```markdown
<!-- File: commands/hookify.md -->
---
description: Create hooks to prevent unwanted behaviors
argument-hint: Optional specific behavior to address
allowed-tools: ["Read", "Write", "AskUserQuestion", "Task", "Grep", "TodoWrite", "Skill"]
---

# Hookify - Create Hooks from Unwanted Behaviors

## Steps
1. Gather behavior from arguments or analyze conversation
2. Present findings using AskUserQuestion
3. Generate rule files (.claude/hookify.{name}.local.md)
4. Confirm creation - rules active immediately
```

```bash
# Create hook from explicit instruction
/hookify Don't use rm -rf without asking me first

# Analyze conversation for problematic behaviors
/hookify

# List existing rules
/hookify:list

# Rule file format example:
# .claude/hookify.warn-dangerous-rm.local.md
```

```markdown
<!-- Example generated rule file -->
---
name: warn-dangerous-rm
enabled: true
event: bash
pattern: rm\s+-rf
action: warn
---

Warning: Dangerous rm command detected.
Please verify the path is correct before proceeding.
```

## PreToolUse Hook - Bash Command Validator

Python hook that validates bash commands before execution.

```python
#!/usr/bin/env python3
"""
Claude Code Hook: Bash Command Validator
Runs as PreToolUse hook for Bash tool.
Validates commands against rules - here it suggests rg over grep.

hooks.json configuration:
{
  "hooks": {
    "PreToolUse": [{
      "matcher": "Bash",
      "hooks": [{
        "type": "command",
        "command": "python3 /path/to/bash_command_validator.py"
      }]
    }]
  }
}
"""

import json
import re
import sys

# Validation rules: (regex pattern, message)
_VALIDATION_RULES = [
    (
        r"^grep\b(?!.*\|)",
        "Use 'rg' (ripgrep) instead of 'grep' for better performance",
    ),
    (
        r"^find\s+\S+\s+-name\b",
        "Use 'rg --files -g pattern' instead of 'find -name'",
    ),
]

def _validate_command(command: str) -> list[str]:
    issues = []
    for pattern, message in _VALIDATION_RULES:
        if re.search(pattern, command):
            issues.append(message)
    return issues

def main():
    try:
        input_data = json.load(sys.stdin)
    except json.JSONDecodeError as e:
        print(f"Error: Invalid JSON input: {e}", file=sys.stderr)
        sys.exit(1)  # Exit 1: show stderr to user, not Claude

    tool_name = input_data.get("tool_name", "")
    if tool_name != "Bash":
        sys.exit(0)

    command = input_data.get("tool_input", {}).get("command", "")
    if not command:
        sys.exit(0)

    issues = _validate_command(command)
    if issues:
        for message in issues:
            print(f"• {message}", file=sys.stderr)
        sys.exit(2)  # Exit 2: block tool call, show stderr to Claude

if __name__ == "__main__":
    main()
```

## Security Guidance Hook

PreToolUse hook that warns about potential security issues when editing files.

```json
// File: hooks/hooks.json
{
  "description": "Security reminder hook for file edits",
  "hooks": {
    "PreToolUse": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "python3 ${CLAUDE_PLUGIN_ROOT}/hooks/security_reminder_hook.py"
          }
        ],
        "matcher": "Edit|Write|MultiEdit"
      }
    ]
  }
}
```

```python
# Security patterns monitored:
# - Command injection (subprocess, os.system, exec)
# - XSS vulnerabilities (innerHTML, document.write)
# - eval() usage
# - Dangerous HTML patterns
# - Pickle deserialization
# - SQL injection patterns
# - Hardcoded credentials
# - Unsafe file operations
# - os.system calls
```

## /new-sdk-app - Agent SDK Project Setup

Interactive setup for new Claude Agent SDK applications.

```markdown
<!-- File: commands/new-sdk-app.md -->
---
description: Create and setup a new Claude Agent SDK application
argument-hint: [project-name]
---

## Workflow

1. Ask language preference (TypeScript or Python)
2. Get project name
3. Determine agent type (coding, business, custom)
4. Choose starting point (minimal, basic, specific example)
5. Confirm tooling (npm/yarn/pnpm, pip/poetry)
6. Create project structure
7. Install latest SDK version
8. Verify code compiles/runs
9. Launch verifier agent for validation
```

```bash
# Usage
/new-sdk-app my-coding-agent

# Claude will ask step by step:
# 1. "Would you like to use TypeScript or Python?"
# 2. (uses provided name: my-coding-agent)
# 3. "What kind of agent? (coding, business, custom)"
# 4. "Starting point? (minimal hello world, basic features, specific example)"
# 5. "I'll use npm - is that OK or prefer pnpm/yarn?"

# Then creates:
# my-coding-agent/
# ├── package.json
# ├── tsconfig.json
# ├── src/index.ts
# ├── .env.example
# └── .gitignore
```

## /ralph-loop - Iterative Development Loop

Self-referential AI loop for iterative development until task completion.

```markdown
<!-- File: commands/ralph-loop.md -->
---
description: "Start Ralph Wiggum loop in current session"
argument-hint: "PROMPT [--max-iterations N] [--completion-promise TEXT]"
allowed-tools: ["Bash(${CLAUDE_PLUGIN_ROOT}/scripts/setup-ralph-loop.sh:*)"]
---

Execute the setup script to initialize the Ralph loop.

When you try to exit, the loop feeds the SAME PROMPT back.
You'll see previous work in files and git history.

CRITICAL: If a completion promise is set, only output it
when the statement is completely TRUE.
```

```bash
# Start iterative loop
/ralph-loop "Refactor the authentication module to use async/await"

# With iteration limit
/ralph-loop "Fix all TypeScript errors" --max-iterations 5

# With completion condition
/ralph-loop "Add tests until coverage reaches 80%" --completion-promise "Test coverage is at least 80%"

# Cancel the loop
/cancel-ralph
```

## frontend-design Skill

Auto-invoked skill for creating distinctive, production-grade frontend interfaces.

```markdown
<!-- File: skills/frontend-design/SKILL.md -->
---
name: frontend-design
description: Create distinctive, production-grade frontend interfaces. Use when building web components, pages, or applications. Generates creative, polished code avoiding generic AI aesthetics.
---

## Design Thinking

Before coding, commit to a BOLD aesthetic direction:
- Purpose: What problem? Who uses it?
- Tone: Brutally minimal, maximalist, retro-futuristic, organic, luxury, playful...
- Differentiation: What makes this UNFORGETTABLE?

## Frontend Aesthetics Guidelines

- **Typography**: Avoid generic fonts (Arial, Inter). Choose distinctive, characterful fonts.
- **Color**: Dominant colors with sharp accents. Use CSS variables.
- **Motion**: CSS animations, scroll-triggering, staggered reveals.
- **Spatial**: Asymmetry, overlap, diagonal flow, grid-breaking.
- **Backgrounds**: Gradient meshes, noise textures, layered transparencies.

NEVER use: overused fonts, purple gradients on white, predictable layouts.
```

```bash
# Skill auto-triggers when user asks for frontend work:
"Build a landing page for my SaaS product"
"Create a dashboard component with charts"
"Design a pricing table"

# Claude applies the skill guidance automatically:
# - Chooses distinctive aesthetic direction
# - Uses creative typography choices
# - Implements motion and micro-interactions
# - Avoids generic AI aesthetics
```

## claude-opus-4-5-migration Skill

Migrate code and prompts from older Claude models to Opus 4.5.

```markdown
<!-- File: skills/claude-opus-4-5-migration/SKILL.md -->
---
name: claude-opus-4-5-migration
description: Migrate from Claude Sonnet 4.0, Sonnet 4.5, or Opus 4.1 to Opus 4.5. Handles model string updates and prompt adjustments.
---

## Migration Workflow

1. Search codebase for model strings
2. Update to Opus 4.5 strings (platform-specific)
3. Remove unsupported beta headers
4. Add effort parameter set to "high"
5. Summarize changes

## Model String Updates

| Platform | Opus 4.5 Model String |
|----------|----------------------|
| Anthropic API | `claude-opus-4-5-20251101` |
| AWS Bedrock | `anthropic.claude-opus-4-5-20251101-v1:0` |
| Vertex AI | `claude-opus-4-5@20251101` |
| Azure AI Foundry | `claude-opus-4-5-20251101` |
```

```bash
# Trigger the skill:
"Migrate my codebase to use Opus 4.5"
"Update all Claude API calls to the latest Opus model"

# Claude will find and replace model strings:
# Before: client.messages.create(model="claude-sonnet-4-5-20250929", ...)
# After:  client.messages.create(model="claude-opus-4-5-20251101", ...)

# And add effort parameter:
# client.messages.create(model="claude-opus-4-5-20251101", effort="high", ...)
```

## Settings Configuration

Example managed settings for organization-wide deployments.

```json
// settings-strict.json - Maximum security configuration
{
  "permissions": {
    "disableBypassPermissionsMode": "disable",
    "ask": ["Bash"],
    "deny": ["WebSearch", "WebFetch"]
  },
  "allowManagedPermissionRulesOnly": true,
  "allowManagedHooksOnly": true,
  "strictKnownMarketplaces": [],
  "sandbox": {
    "autoAllowBashIfSandboxed": false,
    "excludedCommands": [],
    "network": {
      "allowUnixSockets": [],
      "allowAllUnixSockets": false,
      "allowLocalBinding": false,
      "allowedDomains": [],
      "httpProxyPort": null,
      "socksProxyPort": null
    },
    "enableWeakerNestedSandbox": false
  }
}
```

```bash
# Settings hierarchy (highest to lowest priority):
# 1. Managed settings (enterprise policy)
# 2. User settings (~/.claude/settings.json)
# 3. Project settings (.claude/settings.json)
# 4. Local settings (.claude/settings.local.json)

# Apply settings locally for testing:
cp settings-strict.json ~/.claude/settings.json

# Or for project-specific settings:
cp settings-strict.json .claude/settings.json
```

## /plugin-dev:create-plugin - Plugin Creation Workflow

Guided 8-phase workflow for building complete Claude Code plugins.

```markdown
<!-- File: commands/create-plugin.md -->
---
description: Guided end-to-end plugin creation workflow
argument-hint: Optional plugin description
allowed-tools: ["Read", "Write", "Grep", "Glob", "Bash", "TodoWrite", "AskUserQuestion", "Skill", "Task"]
---

## Phases

1. Discovery - Understand plugin purpose
2. Component Planning - Determine needed components
3. Detailed Design - Resolve ambiguities
4. Plugin Structure - Create directories and manifest
5. Component Implementation - Build each component
6. Validation - Run plugin-validator agent
7. Testing - Verify in Claude Code
8. Documentation - Complete README and next steps
```

```bash
# Start plugin creation
/plugin-dev:create-plugin A plugin for managing database migrations

# Claude guides through each phase:
# Phase 1: "What problem does this plugin solve?"
# Phase 2: Presents component plan table
# Phase 3: Asks clarifying questions per component
# Phase 4: Creates directory structure
# Phase 5: Implements each component using specialized skills
# Phase 6: Runs validation agents
# Phase 7: Provides testing checklist
# Phase 8: Finalizes documentation

# Output structure:
# db-migrations/
# ├── .claude-plugin/plugin.json
# ├── commands/create-migration.md
# ├── commands/run-migrations.md
# ├── agents/migration-validator.md
# ├── skills/migration-patterns/SKILL.md
# └── README.md
```

---

Claude Code plugins enable powerful workflow automation and team standardization. The plugin system supports slash commands for user-initiated actions, specialized agents for autonomous tasks, skills for domain knowledge injection, hooks for event-driven automation, and MCP integrations for external services. Teams can share plugins via marketplaces, enforce coding standards through hooks, and automate repetitive tasks like code review, PR creation, and feature development workflows.

Common integration patterns include: using `/commit-push-pr` for standardized git workflows, deploying `/code-review` for automated PR quality checks, implementing custom hooks to enforce project-specific rules (like requiring tests or blocking dangerous commands), creating specialized agents for domain-specific analysis, and building skills that inject context-aware guidance during development. The hierarchical settings system allows organizations to enforce security policies at the enterprise level while giving developers flexibility for project-specific customization.
