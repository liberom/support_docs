# PicoClaw

PicoClaw is an ultra-lightweight personal AI assistant written in Go, designed to run on minimal hardware with less than 10MB RAM footprint. Inspired by nanobot, it was refactored from the ground up through a self-bootstrapping process where the AI agent drove the entire architectural migration. PicoClaw can operate on devices as cheap as $10 (like LicheeRV-Nano), boot in 1 second, and provides a single self-contained binary across RISC-V, ARM, and x86 architectures.

The core functionality includes an AI agent that can chat interactively, execute shell commands, read/write files, search the web, schedule cron tasks, and integrate with multiple messaging platforms (Telegram, Discord, WhatsApp, Slack, LINE, WeCom, QQ, DingTalk, etc.). It supports various LLM providers (OpenAI, Anthropic, Zhipu, DeepSeek, Groq, Ollama, and more) through a unified model-centric configuration, and extends capabilities through skills and MCP (Model Context Protocol) servers.

## CLI Commands

### picoclaw onboard - Initialize Configuration and Workspace

Creates the default configuration file and workspace directory structure. This is the first command to run after installation.

```bash
# Initialize PicoClaw with interactive setup
picoclaw onboard

# Output:
# Welcome to PicoClaw!
# Creating workspace at ~/.picoclaw/workspace...
# Creating config at ~/.picoclaw/config.json...
# First-run setup complete.
```

### picoclaw agent - Interact with the AI Agent

Send messages to the AI agent for processing. Supports both single message mode and interactive chat mode.

```bash
# Send a single message (non-interactive)
picoclaw agent -m "What is 2+2?"

# Interactive chat mode
picoclaw agent

# Specify a custom model
picoclaw agent --model claude-sonnet-4.6 -m "Explain quantum computing"

# Use a specific session key for conversation continuity
picoclaw agent -s "project-alpha" -m "Continue our discussion"

# Enable debug logging
picoclaw agent -d -m "Debug this request"
```

### picoclaw gateway - Start the Gateway Server

Starts the gateway server that handles multiple messaging channels (Telegram, Discord, WhatsApp, etc.) and webhook endpoints.

```bash
# Start the gateway with default settings
picoclaw gateway

# Start with debug logging enabled
picoclaw gateway -d

# Output:
# Starting gateway on 127.0.0.1:18790...
# Telegram channel enabled
# Discord channel enabled
# Gateway ready
```

### picoclaw cron - Manage Scheduled Tasks

Manage scheduled jobs including reminders, recurring tasks, and automated commands.

```bash
# List all scheduled jobs
picoclaw cron list

# Add a one-time reminder
picoclaw cron add --name "meeting-reminder" --at-seconds 3600 --message "Team meeting in 1 hour"

# Add a recurring task (every 2 hours)
picoclaw cron add --name "health-check" --every-seconds 7200 --message "Check server health"

# Add a cron expression based job (daily at 9am)
picoclaw cron add --name "daily-standup" --cron-expr "0 9 * * *" --message "Time for standup"

# Remove a job by ID
picoclaw cron remove --id "abc123"

# Enable/disable a job
picoclaw cron enable --id "abc123"
picoclaw cron disable --id "abc123"
```

### picoclaw skills - Manage Agent Skills

Install, search, and manage skills that extend agent capabilities.

```bash
# List all available skills
picoclaw skills list

# Search for skills in the registry
picoclaw skills search "github"

# Show details of a specific skill
picoclaw skills show github

# Install a skill from registry
picoclaw skills install weather

# Remove an installed skill
picoclaw skills remove weather
```

## Configuration

### config.json - Main Configuration File

The configuration file at `~/.picoclaw/config.json` controls all aspects of PicoClaw including models, channels, and tools.

```json
{
  "agents": {
    "defaults": {
      "workspace": "~/.picoclaw/workspace",
      "restrict_to_workspace": true,
      "model_name": "gpt4",
      "max_tokens": 8192,
      "temperature": 0.7,
      "max_tool_iterations": 20,
      "summarize_message_threshold": 20,
      "summarize_token_percent": 75
    }
  },
  "model_list": [
    {
      "model_name": "gpt4",
      "model": "openai/gpt-5.2",
      "api_key": "sk-your-openai-key",
      "api_base": "https://api.openai.com/v1"
    },
    {
      "model_name": "claude-sonnet",
      "model": "anthropic/claude-sonnet-4.6",
      "api_key": "sk-ant-your-key"
    },
    {
      "model_name": "deepseek",
      "model": "deepseek/deepseek-chat",
      "api_key": "sk-your-deepseek-key"
    },
    {
      "model_name": "ollama-llama",
      "model": "ollama/llama3"
    }
  ],
  "channels": {
    "telegram": {
      "enabled": true,
      "token": "YOUR_TELEGRAM_BOT_TOKEN",
      "allow_from": ["YOUR_USER_ID"]
    },
    "discord": {
      "enabled": true,
      "token": "YOUR_DISCORD_BOT_TOKEN",
      "allow_from": [],
      "group_trigger": {
        "mention_only": true
      }
    }
  },
  "tools": {
    "web": {
      "brave": {
        "enabled": true,
        "api_key": "YOUR_BRAVE_API_KEY",
        "max_results": 5
      },
      "duckduckgo": {
        "enabled": true,
        "max_results": 5
      }
    },
    "mcp": {
      "enabled": true,
      "servers": {
        "filesystem": {
          "enabled": true,
          "command": "npx",
          "args": ["-y", "@modelcontextprotocol/server-filesystem", "/tmp"]
        }
      }
    }
  },
  "heartbeat": {
    "enabled": true,
    "interval": 30
  },
  "gateway": {
    "host": "127.0.0.1",
    "port": 18790
  }
}
```

### Environment Variables

Override configuration settings using environment variables.

```bash
# Override config file path
export PICOCLAW_CONFIG=/etc/picoclaw/production.json

# Override home directory
export PICOCLAW_HOME=/opt/picoclaw

# Override specific settings
export PICOCLAW_AGENTS_DEFAULTS_WORKSPACE=/srv/picoclaw/workspace
export PICOCLAW_AGENTS_DEFAULTS_RESTRICT_TO_WORKSPACE=false
export PICOCLAW_HEARTBEAT_ENABLED=false
export PICOCLAW_HEARTBEAT_INTERVAL=60
export PICOCLAW_GATEWAY_HOST=0.0.0.0
export PICOCLAW_GATEWAY_PORT=8080

# Run with custom configuration
PICOCLAW_CONFIG=/srv/picoclaw/main.json picoclaw gateway
```

## Tools API

### read_file - Read File Contents

Read the contents of a file within the workspace.

```go
// Tool implementation
tool := tools.NewReadFileTool(workspace, restrictToWorkspace)

// Parameters schema
{
  "type": "object",
  "properties": {
    "path": {
      "type": "string",
      "description": "Path to the file to read"
    }
  },
  "required": ["path"]
}

// Example usage via agent
// Agent request: "Read the contents of config.json"
// Tool call: {"path": "config.json"}
// Returns: File content as string
```

### write_file - Write File Contents

Write content to a file within the workspace with atomic write operations.

```go
// Tool implementation
tool := tools.NewWriteFileTool(workspace, restrictToWorkspace)

// Parameters schema
{
  "type": "object",
  "properties": {
    "path": {
      "type": "string",
      "description": "Path to the file to write"
    },
    "content": {
      "type": "string",
      "description": "Content to write to the file"
    }
  },
  "required": ["path", "content"]
}

// Example usage via agent
// Agent request: "Create a README.md with project description"
// Tool call: {"path": "README.md", "content": "# My Project\n\nDescription here."}
// Returns: "File written: README.md"
```

### list_dir - List Directory Contents

List files and directories in a given path.

```go
// Tool implementation
tool := tools.NewListDirTool(workspace, restrictToWorkspace)

// Parameters schema
{
  "type": "object",
  "properties": {
    "path": {
      "type": "string",
      "description": "Path to list"
    }
  },
  "required": ["path"]
}

// Example usage via agent
// Agent request: "List files in the current directory"
// Tool call: {"path": "."}
// Returns:
// DIR:  config
// DIR:  scripts
// FILE: main.go
// FILE: README.md
```

### exec - Execute Shell Commands

Execute shell commands with safety guards and workspace restrictions.

```go
// Tool implementation
tool, err := tools.NewExecToolWithConfig(workingDir, restrictToWorkspace, config)
tool.SetTimeout(60 * time.Second)

// Parameters schema
{
  "type": "object",
  "properties": {
    "command": {
      "type": "string",
      "description": "The shell command to execute"
    },
    "working_dir": {
      "type": "string",
      "description": "Optional working directory for the command"
    }
  },
  "required": ["command"]
}

// Example usage via agent
// Agent request: "Check disk usage"
// Tool call: {"command": "df -h"}
// Returns: Command output with disk usage information

// Safety: The following patterns are blocked by default:
// - rm -rf, sudo, chmod, chown
// - shutdown, reboot, poweroff
// - Writes to block devices
// - Fork bombs and command injection
```

### web_search - Search the Web

Search the web using configured providers (Brave, Tavily, DuckDuckGo, Perplexity).

```go
// Tool implementation
tool, err := tools.NewWebSearchTool(tools.WebSearchToolOptions{
    BraveEnabled:    true,
    BraveAPIKey:     "YOUR_API_KEY",
    BraveMaxResults: 5,
    DuckDuckGoEnabled: true,
    DuckDuckGoMaxResults: 5,
})

// Parameters schema
{
  "type": "object",
  "properties": {
    "query": {
      "type": "string",
      "description": "Search query"
    },
    "count": {
      "type": "integer",
      "description": "Number of results (1-10)",
      "minimum": 1,
      "maximum": 10
    }
  },
  "required": ["query"]
}

// Example usage via agent
// Agent request: "Search for latest Go release notes"
// Tool call: {"query": "Go 1.22 release notes", "count": 5}
// Returns:
// Results for: Go 1.22 release notes (via Brave)
// 1. Go 1.22 Release Notes - The Go Programming Language
//    https://go.dev/doc/go1.22
//    Go 1.22 is released with new features...
```

### web_fetch - Fetch URL Content

Fetch a URL and extract readable content from HTML pages.

```go
// Tool implementation
tool, err := tools.NewWebFetchToolWithProxy(50000, "http://proxy:8080", 10*1024*1024)

// Parameters schema
{
  "type": "object",
  "properties": {
    "url": {
      "type": "string",
      "description": "URL to fetch"
    },
    "maxChars": {
      "type": "integer",
      "description": "Maximum characters to extract",
      "minimum": 100
    }
  },
  "required": ["url"]
}

// Example usage via agent
// Agent request: "Fetch the weather from example.com"
// Tool call: {"url": "https://example.com/weather", "maxChars": 10000}
// Returns: JSON with url, status, extractor type, truncated flag, and extracted text
```

### cron - Schedule Tasks and Reminders

Schedule one-time reminders, recurring tasks, or system commands.

```go
// Tool implementation
tool, err := tools.NewCronTool(cronService, executor, msgBus, workspace, restrict, timeout, config)

// Parameters schema
{
  "type": "object",
  "properties": {
    "action": {
      "type": "string",
      "enum": ["add", "list", "remove", "enable", "disable"],
      "description": "Action to perform"
    },
    "message": {
      "type": "string",
      "description": "The reminder/task message"
    },
    "command": {
      "type": "string",
      "description": "Optional shell command to execute"
    },
    "at_seconds": {
      "type": "integer",
      "description": "One-time: seconds from now when to trigger"
    },
    "every_seconds": {
      "type": "integer",
      "description": "Recurring: interval in seconds"
    },
    "cron_expr": {
      "type": "string",
      "description": "Cron expression for complex schedules"
    },
    "job_id": {
      "type": "string",
      "description": "Job ID (for remove/enable/disable)"
    },
    "deliver": {
      "type": "boolean",
      "description": "If true, send directly to channel"
    }
  },
  "required": ["action"]
}

// Example: One-time reminder
// Tool call: {"action": "add", "message": "Check email", "at_seconds": 600}
// Returns: "Cron job added: Check email (id: abc123)"

// Example: Recurring task
// Tool call: {"action": "add", "message": "Health check", "every_seconds": 3600}

// Example: List jobs
// Tool call: {"action": "list"}
// Returns:
// Scheduled jobs:
// - Check email (id: abc123, one-time)
// - Health check (id: def456, every 3600s)
```

## Skills System

### Creating a Custom Skill

Skills are Markdown files with YAML frontmatter that extend agent capabilities.

```markdown
<!-- File: ~/.picoclaw/workspace/skills/weather/SKILL.md -->
---
name: weather
description: "Get weather information for any location using wttr.in"
---

# Weather Skill

Use wttr.in to get weather information for any location.

## Get Current Weather

```bash
curl -s "wttr.in/London?format=3"
```

## Get Detailed Forecast

```bash
curl -s "wttr.in/Tokyo"
```

## Get Weather in JSON

```bash
curl -s "wttr.in/Paris?format=j1" | jq '.current_condition[0]'
```
```

### Loading Skills Programmatically

```go
import "github.com/sipeed/picoclaw/pkg/skills"

// Create skills loader with search paths
loader := skills.NewSkillsLoader(
    "~/.picoclaw/workspace",           // workspace (project-level)
    "~/.picoclaw/skills",              // global skills
    "/usr/share/picoclaw/skills",      // builtin skills
)

// List all available skills
allSkills := loader.ListSkills()
for _, skill := range allSkills {
    fmt.Printf("Skill: %s (%s)\n", skill.Name, skill.Source)
    fmt.Printf("  Description: %s\n", skill.Description)
    fmt.Printf("  Path: %s\n", skill.Path)
}

// Load a specific skill content
content, found := loader.LoadSkill("github")
if found {
    fmt.Println(content)
}

// Load multiple skills for agent context
skillsContext := loader.LoadSkillsForContext([]string{"github", "weather"})

// Build XML summary of all skills
summary := loader.BuildSkillsSummary()
// Returns:
// <skills>
//   <skill>
//     <name>github</name>
//     <description>Interact with GitHub using the gh CLI</description>
//     <location>/path/to/SKILL.md</location>
//     <source>workspace</source>
//   </skill>
// </skills>
```

## MCP Integration

### Configuring MCP Servers

Configure MCP (Model Context Protocol) servers for extended tool capabilities.

```json
{
  "tools": {
    "mcp": {
      "enabled": true,
      "servers": {
        "filesystem": {
          "enabled": true,
          "command": "npx",
          "args": ["-y", "@modelcontextprotocol/server-filesystem", "/tmp"]
        },
        "github": {
          "enabled": true,
          "command": "npx",
          "args": ["-y", "@modelcontextprotocol/server-github"],
          "env": {
            "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_xxxxx"
          }
        },
        "context7": {
          "enabled": true,
          "type": "http",
          "url": "https://mcp.context7.com/mcp",
          "headers": {
            "CONTEXT7_API_KEY": "ctx7sk-xxxxx"
          }
        },
        "postgres": {
          "enabled": true,
          "command": "npx",
          "args": ["-y", "@modelcontextprotocol/server-postgres", "postgresql://user:pass@localhost/db"],
          "env_file": ".env.postgres"
        }
      }
    }
  }
}
```

### Using MCP Manager Programmatically

```go
import (
    "context"
    "github.com/sipeed/picoclaw/pkg/mcp"
    "github.com/sipeed/picoclaw/pkg/config"
)

// Create MCP manager
manager := mcp.NewManager()

// Load from configuration
cfg, _ := config.LoadConfig("~/.picoclaw/config.json")
err := manager.LoadFromConfig(context.Background(), cfg)
if err != nil {
    log.Fatal(err)
}

// Get all connected servers
servers := manager.GetServers()
for name, conn := range servers {
    fmt.Printf("Server: %s\n", name)
    for _, tool := range conn.Tools {
        fmt.Printf("  Tool: %s - %s\n", tool.Name, tool.Description)
    }
}

// Call a tool on a specific server
result, err := manager.CallTool(
    context.Background(),
    "filesystem",
    "read_file",
    map[string]any{"path": "/tmp/test.txt"},
)
if err != nil {
    log.Fatal(err)
}
fmt.Printf("Result: %v\n", result)

// Close all connections when done
manager.Close()
```

## Docker Deployment

### Running with Docker Compose

Deploy PicoClaw using Docker with multiple profiles and configurations.

```bash
# Clone the repository
git clone https://github.com/sipeed/picoclaw.git
cd picoclaw

# First run - generates config file
docker compose -f docker/docker-compose.yml --profile gateway up
# Container exits after creating docker/data/config.json

# Edit configuration
vim docker/data/config.json

# Start gateway in background
docker compose -f docker/docker-compose.yml --profile gateway up -d

# Check logs
docker compose -f docker/docker-compose.yml logs -f picoclaw-gateway

# Run agent mode (one-shot)
docker compose -f docker/docker-compose.yml run --rm picoclaw-agent -m "What is 2+2?"

# Interactive agent mode
docker compose -f docker/docker-compose.yml run --rm picoclaw-agent

# Update to latest version
docker compose -f docker/docker-compose.yml pull
docker compose -f docker/docker-compose.yml --profile gateway up -d

# Stop all services
docker compose -f docker/docker-compose.yml --profile gateway down
```

## Heartbeat and Periodic Tasks

### HEARTBEAT.md - Automatic Task Execution

Create a HEARTBEAT.md file in your workspace for automatic periodic task execution.

```markdown
<!-- File: ~/.picoclaw/workspace/HEARTBEAT.md -->
# Periodic Tasks

## Quick Tasks (respond directly)
- Report current time
- Check system uptime

## Long Tasks (use spawn for async)
- Search the web for AI news and summarize
- Check email and report important messages
- Monitor server health and alert if issues found
```

```json
{
  "heartbeat": {
    "enabled": true,
    "interval": 30
  }
}
```

## Summary

PicoClaw serves as a powerful yet lightweight AI assistant platform suitable for edge computing, IoT devices, personal automation, and resource-constrained environments. Its primary use cases include running AI agents on minimal hardware (Raspberry Pi Zero, RISC-V boards, old Android phones via Termux), integrating with multiple messaging platforms for chatbot deployments, scheduling and automating tasks through the cron system, and extending capabilities through skills and MCP servers. The unified model-centric configuration makes it easy to switch between LLM providers without code changes.

Integration patterns typically involve: (1) deploying the gateway server to handle multiple chat channels simultaneously, (2) using the agent CLI for scripted automation and CI/CD pipelines, (3) creating custom skills to encode domain-specific knowledge and workflows, (4) connecting MCP servers for database access, file operations, or API integrations, and (5) using the heartbeat system for proactive monitoring and automated responses. The sandboxed execution environment with configurable workspace restrictions ensures safe operation in multi-tenant or untrusted environments while the atomic file operations provide reliability on embedded flash storage.
