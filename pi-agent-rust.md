# Pi Agent Rust

Pi Agent Rust is a high-performance AI coding agent CLI written in Rust, designed as a from-scratch port of the original Pi Agent by Mario Zechner. It provides instant startup, stable streaming, and a robust extension security model with 8 built-in tools for file manipulation, code search, and shell execution. The agent supports multiple LLM providers including Anthropic, OpenAI, Google Gemini, Cohere, Azure, AWS Bedrock, GitHub Copilot, and GitLab Duo.

Built on two purpose-built Rust libraries (asupersync for structured concurrency and rich_rust for terminal output), Pi Agent Rust delivers 4-5x faster performance than Node.js implementations and 12x lower memory usage in realistic workloads. The project emphasizes security with capability-gated hostcalls, two-stage extension execution guards, and a trust lifecycle system for extension management.

## CLI Usage

The main CLI provides session management, model configuration, and tool execution capabilities.

```bash
# Start a new session with a message
pi "explain this code"

# Include files in context using @ prefix
pi @file.rs "review this"

# Continue previous session
pi -c
pi --continue

# Resume from session picker UI
pi -r
pi --resume

# Non-interactive print mode (process & exit)
pi -p "what is 2+2"

# Use specific model and provider
pi --provider anthropic --model claude-opus-4 "help me refactor"

# Set extended thinking level (off/minimal/low/medium/high/xhigh)
pi --thinking high "solve this complex problem"

# Custom system prompt
pi --system-prompt "You are a Rust expert" "explain ownership"

# Append to system prompt
pi --append-system-prompt "Be concise" "explain this"

# Specify tools to enable (default: read,bash,edit,write,grep,find,ls,hashline_edit)
pi --tools "read,grep,bash" "search for errors"

# Disable all tools
pi --no-tools "just chat"

# Load specific extension
pi -e extension.js "run with extension"
pi --extension my-ext.js --extension other-ext.js "multiple extensions"

# Extension policy modes: safe, balanced, permissive
pi --extension-policy safe "run securely"

# Export session to HTML
pi --export output.html

# List available models (with optional filter)
pi --list-models
pi --list-models "claude*"

# List supported providers
pi --list-providers

# Session management options
pi --session /path/to/session.jsonl "use specific session"
pi --session-dir /custom/sessions "use custom session directory"
pi --no-session "ephemeral mode, don't save"
pi --session-durability throughput "optimize for speed"
```

## Subcommands

Package management and configuration subcommands for extensions, skills, and themes.

```bash
# Install extension from npm
pi install npm:@org/my-extension

# Install from git repository
pi install git:https://github.com/user/extension

# Install locally (project-specific)
pi install --local ./my-extension

# Remove extension
pi remove npm:my-extension
pi remove --local npm:my-extension

# Update all packages or specific one
pi update
pi update npm:my-extension

# Refresh extension index cache
pi update-index

# Search available extensions
pi search "git workflow"
pi search --tag automation --limit 10 "commit"

# Show extension details
pi info auto-commit-on-exit

# List installed packages
pi list

# Configuration commands
pi config              # Open config UI
pi config --show       # Print config summary
pi config --paths      # Show config file paths
pi config --json       # Output config as JSON

# Diagnose environment health
pi doctor
pi doctor /path/to/extension.js
pi doctor --format json --fix

# Migrate session files to v2 format
pi migrate /path/to/session.jsonl
pi migrate --dry-run /sessions/directory
```

## Interactive Slash Commands

Commands available during an interactive Pi session for navigation and control.

```
/help, /h, /?           Show help message
/login [provider]       Login/setup credentials
/logout [provider]      Remove stored credentials
/clear, /cls            Clear conversation history
/model, /m [id]         Open model selector or switch directly
/thinking, /t [level]   Set thinking level (off/minimal/low/medium/high/xhigh)
/scoped-models [patterns|clear]  Show or set scoped models for cycling
/history, /hist         Show input history
/export [path]          Export conversation to HTML
/session, /info         Show session info (path, tokens, cost)
/settings               Open settings selector
/theme [name]           List or switch themes
/resume, /r             Pick and resume a previous session
/new                    Start a new session
/copy, /cp              Copy last assistant message to clipboard
/name <name>            Set session display name
/hotkeys, /keys         Show keyboard shortcuts
/changelog              Show changelog entries
/tree                   Show session branch tree summary
/fork [id|index]        Fork from a user message
/compact [notes]        Compact older context with optional instructions
/reload                 Reload skills/prompts from disk
/share                  Upload session HTML to GitHub gist
/exit, /quit, /q        Exit Pi
```

## Read Tool

Read file contents with support for text files and images. Handles large files with pagination via offset/limit parameters.

```json
{
  "name": "read",
  "parameters": {
    "path": "src/main.rs",
    "offset": 1,
    "limit": 100,
    "hashline": false
  }
}
```

```bash
# Example tool call from agent
# Reads lines 1-100 from src/main.rs
{
  "path": "src/main.rs",
  "offset": 1,
  "limit": 100
}

# Read with hashline mode for precise edits
{
  "path": "src/main.rs",
  "hashline": true
}
# Output format: N#AB:content where N is line number, AB is content hash

# Read an image file (jpg, png, gif, webp)
{
  "path": "screenshot.png"
}
# Returns base64-encoded image attachment
```

## Bash Tool

Execute shell commands with timeout control and output streaming. Output is truncated to last 2000 lines or 50KB.

```json
{
  "name": "bash",
  "parameters": {
    "command": "cargo build --release",
    "timeout": 120
  }
}
```

```bash
# Simple command execution
{
  "command": "ls -la"
}

# Long-running command with custom timeout
{
  "command": "cargo test --all",
  "timeout": 300
}

# Disable timeout for indefinite execution
{
  "command": "./long-running-server.sh",
  "timeout": 0
}

# Pipeline commands
{
  "command": "grep -r 'TODO' src/ | wc -l"
}
```

## Edit Tool

Replace text in files using exact string matching with fuzzy Unicode normalization support.

```json
{
  "name": "edit",
  "parameters": {
    "path": "src/main.rs",
    "old_text": "fn old_function() {\n    // old code\n}",
    "new_text": "fn new_function() {\n    // new improved code\n}"
  }
}
```

```bash
# Replace function implementation
{
  "path": "src/lib.rs",
  "old_text": "pub fn calculate(x: i32) -> i32 {\n    x * 2\n}",
  "new_text": "pub fn calculate(x: i32) -> i32 {\n    x.saturating_mul(2)\n}"
}

# Fix import statement
{
  "path": "src/main.rs",
  "old_text": "use std::io;",
  "new_text": "use std::io::{self, Write};"
}
```

## Write Tool

Write or overwrite file contents. Creates parent directories if needed.

```json
{
  "name": "write",
  "parameters": {
    "path": "src/new_module.rs",
    "content": "//! New module\n\npub fn hello() {\n    println!(\"Hello!\");\n}"
  }
}
```

```bash
# Create a new Rust file
{
  "path": "src/utils.rs",
  "content": "pub fn format_duration(secs: u64) -> String {\n    format!(\"{}s\", secs)\n}"
}

# Create configuration file
{
  "path": "config.toml",
  "content": "[server]\nhost = \"localhost\"\nport = 8080"
}
```

## Grep Tool

Search file contents using regular expressions with context lines support.

```json
{
  "name": "grep",
  "parameters": {
    "pattern": "fn\\s+\\w+",
    "path": "src/",
    "include": "*.rs",
    "context": 2,
    "limit": 100
  }
}
```

```bash
# Search for function definitions
{
  "pattern": "pub fn \\w+",
  "path": "src/",
  "include": "*.rs"
}

# Search with context lines
{
  "pattern": "TODO|FIXME",
  "path": ".",
  "context": 3,
  "limit": 50
}

# Case-insensitive search
{
  "pattern": "error",
  "path": "logs/",
  "include": "*.log"
}
```

## Find Tool

Find files by name pattern using glob matching.

```json
{
  "name": "find",
  "parameters": {
    "pattern": "*.rs",
    "path": "src/",
    "limit": 1000
  }
}
```

```bash
# Find all Rust files
{
  "pattern": "*.rs",
  "path": "src/"
}

# Find test files
{
  "pattern": "*_test.rs",
  "path": "."
}

# Find configuration files
{
  "pattern": "*.{json,toml,yaml}",
  "path": "."
}
```

## Ls Tool

List directory contents with file metadata.

```json
{
  "name": "ls",
  "parameters": {
    "path": "src/",
    "limit": 500
  }
}
```

```bash
# List current directory
{
  "path": "."
}

# List source directory
{
  "path": "src/",
  "limit": 100
}
```

## Hashline Edit Tool

Precise line-based editing using hashline references from the read tool's hashline mode.

```json
{
  "name": "hashline_edit",
  "parameters": {
    "path": "src/main.rs",
    "edits": [
      {"hashline": "42#AB", "content": "    let result = compute();"},
      {"hashline": "43#CD", "delete": true}
    ]
  }
}
```

```bash
# Edit specific lines by hash reference
{
  "path": "src/lib.rs",
  "edits": [
    {"hashline": "10#F3", "content": "use std::collections::HashMap;"},
    {"hashline": "15#A7", "content": "    let mut map = HashMap::new();"}
  ]
}

# Delete a line
{
  "path": "src/main.rs",
  "edits": [
    {"hashline": "25#BC", "delete": true}
  ]
}
```

## Configuration

Settings can be configured via `settings.json` in the Pi config directory or via CLI flags.

```json
{
  "theme": "dark",
  "defaultProvider": "anthropic",
  "defaultModel": "claude-sonnet-4-5",
  "defaultThinkingLevel": "medium",
  "enabledModels": ["claude*", "gpt-4*"],
  "steeringMode": "one-at-a-time",
  "quietStartup": true,
  "shellPath": "/bin/bash",
  "sessionStore": "jsonl",
  "sessionDurability": "balanced",
  "extensionPolicy": {
    "profile": "balanced",
    "allowDangerous": false
  },
  "repairPolicy": {
    "mode": "suggest"
  },
  "compaction": {
    "enabled": true,
    "threshold": 50000
  },
  "images": {
    "autoResize": true,
    "blockImages": false
  },
  "thinkingBudgets": {
    "minimal": 1024,
    "low": 4096,
    "medium": 10000,
    "high": 20000,
    "xhigh": 50000
  }
}
```

## Provider Configuration

Supported LLM providers with authentication methods.

```bash
# Environment variables for provider authentication
export ANTHROPIC_API_KEY="sk-ant-..."
export OPENAI_API_KEY="sk-..."
export GOOGLE_API_KEY="..."
export COHERE_API_KEY="..."
export AZURE_OPENAI_API_KEY="..."
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."

# Provider aliases
# anthropic -> Anthropic Claude models
# openai -> OpenAI GPT models
# google, gemini -> Google Gemini models
# google-vertex, vertexai -> Google Vertex AI
# amazon-bedrock, bedrock -> AWS Bedrock
# azure-openai, azure -> Azure OpenAI
# github-copilot, copilot -> GitHub Copilot
# gitlab, gitlab-duo -> GitLab Duo
# cohere -> Cohere Command models

# Use auth.json for persistent credentials
# Located in Pi config directory
{
  "anthropic": {
    "apiKey": "sk-ant-..."
  },
  "openai": {
    "apiKey": "sk-..."
  }
}
```

## Extension Development

Extensions can add custom tools, commands, and hooks to Pi Agent.

```javascript
// extension.js - Basic extension structure
export default {
  name: "my-extension",
  version: "1.0.0",

  // Define custom tools
  tools: [
    {
      name: "my_tool",
      description: "A custom tool",
      parameters: {
        type: "object",
        properties: {
          input: { type: "string", description: "Input value" }
        },
        required: ["input"]
      },
      execute: async (params, context) => {
        return { result: `Processed: ${params.input}` };
      }
    }
  ],

  // Define slash commands
  commands: [
    {
      name: "mycmd",
      description: "Run my custom command",
      execute: async (args, context) => {
        return { message: "Command executed!" };
      }
    }
  ],

  // Lifecycle hooks
  onLoad: async (context) => {
    console.log("Extension loaded");
  },

  onUnload: async (context) => {
    console.log("Extension unloaded");
  }
};
```

```bash
# Load extension via CLI
pi -e ./my-extension.js "use my extension"

# Install from npm
pi install npm:my-extension

# Extension policy profiles control capabilities:
# - safe: Minimal permissions, no exec/env access
# - balanced: Standard permissions with mediated exec
# - permissive: Full permissions (use with trusted extensions only)
pi --extension-policy safe -e untrusted-ext.js "run safely"
```

Pi Agent Rust is ideal for developers who need a fast, reliable AI coding assistant directly in their terminal workflow. The single-binary deployment eliminates runtime dependencies while the robust session management enables seamless continuation of complex coding tasks across multiple sessions.

The extension system enables customization for team-specific workflows, with security controls that allow organizations to define capability policies appropriate for their environment. Integration patterns range from simple interactive usage to programmatic access via print mode (`-p`) for scripts and automation, with JSON and RPC output modes available for structured integration with other tools.


