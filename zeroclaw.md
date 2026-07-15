# ZeroClaw

ZeroClaw is a high-performance, ultra-lightweight AI assistant runtime written in Rust. It provides a fully autonomous agent infrastructure that abstracts AI models, tools, memory, and execution environments, allowing agents to be built once and deployed anywhere. With a binary size under 9MB and runtime memory usage below 5MB, ZeroClaw is designed for edge deployments on resource-constrained hardware while maintaining enterprise-grade security through pairing codes, sandboxing, and explicit allowlists.

The architecture follows a trait-driven design where every subsystem (providers, channels, tools, memory, tunnels) is swappable via configuration without code changes. ZeroClaw supports 20+ LLM providers (OpenAI, Anthropic, Ollama, Groq, etc.), 17+ messaging channels (Telegram, Discord, Slack, WhatsApp, Matrix, etc.), and a comprehensive tool system for shell execution, file operations, memory management, browser automation, and hardware peripherals control.

## CLI Commands

### Onboard - Initialize Workspace and Configuration

Creates initial configuration with provider credentials, model selection, and channel setup. Supports both interactive wizard and command-line modes.

```bash
# Interactive wizard for full setup
zeroclaw onboard --interactive

# Quick setup with explicit parameters
zeroclaw onboard --api-key "sk-your-key" --provider openrouter --model "anthropic/claude-sonnet-4-6"

# Update only channel tokens/allowlists (preserves other settings)
zeroclaw onboard --channels-only

# Force overwrite existing config
zeroclaw onboard --force --api-key "sk-key" --provider anthropic --memory sqlite
```

### Agent - Interactive Chat and Single Message Mode

Run the AI agent for interactive conversations or single-shot queries. Supports provider/model overrides and peripheral hardware connections.

```bash
# Start interactive chat session
zeroclaw agent

# Send single message and exit
zeroclaw agent -m "Explain the Rust borrow checker in simple terms"

# Use specific provider and model
zeroclaw agent --provider ollama --model "llama3.2" --temperature 0.3

# Connect to hardware peripheral during session
zeroclaw agent --peripheral "nucleo-f401re:/dev/ttyACM0"
```

### Gateway and Daemon - Start HTTP and Runtime Services

Launch the webhook server for external integrations or the full autonomous daemon with channels, heartbeat, and scheduler.

```bash
# Start webhook gateway on default port
zeroclaw gateway
# Output: Gateway listening on 127.0.0.1:42617

# Start with custom host/port
zeroclaw gateway --host 0.0.0.0 --port 8080

# Start full autonomous runtime (gateway + channels + heartbeat)
zeroclaw daemon

# Start daemon with specific network binding
zeroclaw daemon --host 127.0.0.1 --port 42617
```

### Service Management - OS Service Lifecycle

Install and manage ZeroClaw as a background service using systemd (Linux) or OpenRC (Alpine).

```bash
# Install as user-level systemd service
zeroclaw service install

# Start the service
zeroclaw service start

# Check service status
zeroclaw service status
# Output: zeroclaw.service - ZeroClaw AI Assistant
#         Active: active (running) since Mon 2026-02-21 10:30:00 UTC

# Restart after config changes
zeroclaw service restart

# Stop and remove service
zeroclaw service stop
zeroclaw service uninstall
```

### Channel Management - Messaging Platform Integration

List, start, and diagnose messaging channel connections. Supports runtime model switching via in-chat commands.

```bash
# List configured channels
zeroclaw channel list
# Output:
# Channel     | Status    | Delivery Mode
# telegram    | configured| polling
# discord     | configured| websocket
# slack       | configured| events API

# Start all configured channels
zeroclaw channel start

# Run channel health diagnostics
zeroclaw channel doctor

# Bind Telegram user to allowlist
zeroclaw channel bind-telegram 123456789
```

### Cron - Scheduled Task Management

Create, list, and manage scheduled tasks with cron expressions, one-time delays, or recurring intervals.

```bash
# List all scheduled tasks
zeroclaw cron list

# Add task with cron expression (daily at 9am UTC)
zeroclaw cron add "0 9 * * *" "Check email and summarize important messages"

# Add task with timezone
zeroclaw cron add "0 9 * * *" --tz "America/New_York" "Morning briefing"

# Schedule one-time task with delay
zeroclaw cron once "30m" "Remind me to take a break"
zeroclaw cron once "2h" "Review pull requests"

# Add recurring task (every 15 minutes)
zeroclaw cron add-every 900000 "Check system health"

# Pause/resume tasks
zeroclaw cron pause task-id-123
zeroclaw cron resume task-id-123

# Remove task
zeroclaw cron remove task-id-123
```

### Emergency Stop - Safety Controls

Engage emergency stop levels to halt agent operations, block domains, or freeze specific tools.

```bash
# Engage full emergency stop (kill all operations)
zeroclaw estop

# Engage network-level stop
zeroclaw estop --level network-kill

# Block specific domains
zeroclaw estop --level domain-block --domain "*.chase.com" --domain "*.paypal.com"

# Freeze specific tools
zeroclaw estop --level tool-freeze --tool shell --tool browser

# Check current estop status
zeroclaw estop status
# Output: estop_level: domain-block, blocked_domains: ["*.chase.com"]

# Resume with OTP verification
zeroclaw estop resume --otp 123456
```

### Doctor - System Diagnostics

Run comprehensive diagnostics on configuration, provider connectivity, and runtime traces.

```bash
# Full system diagnostics
zeroclaw doctor
# Output:
# Config: OK (loaded from ~/.zeroclaw/config.toml)
# Provider: openrouter (connected)
# Memory: sqlite (healthy, 1,234 entries)
# Channels: 2/2 healthy

# Check model availability for specific provider
zeroclaw doctor models --provider ollama
# Output: Available models: llama3.2, qwen2.5-coder:32b, mistral

# Query runtime traces for debugging
zeroclaw doctor traces --limit 20
zeroclaw doctor traces --event tool_call_result --contains "error"
zeroclaw doctor traces --id trace-abc123
```

### Skills - Plugin Management

Install, audit, and manage skill plugins that extend agent capabilities.

```bash
# List installed skills
zeroclaw skills list
# Output:
# Name          | Version | Status
# github-pr     | 1.0.0   | active
# code-review   | 2.1.0   | active

# Audit skill for security issues before install
zeroclaw skills audit https://github.com/user/my-skill

# Install skill from git repository
zeroclaw skills install https://github.com/user/my-skill

# Install from local directory
zeroclaw skills install ./my-local-skill

# Remove installed skill
zeroclaw skills remove my-skill
```

### Hardware - USB Discovery and Peripheral Management

Discover USB devices, introspect hardware capabilities, and manage peripheral boards for embedded development.

```bash
# Discover connected USB devices
zeroclaw hardware discover
# Output:
# Device              | VID:PID     | Path
# STM32 Nucleo        | 0483:374b   | /dev/ttyACM0
# Arduino Uno         | 2341:0043   | /dev/ttyUSB0

# Get detailed device information
zeroclaw hardware introspect /dev/ttyACM0

# Get chip datasheet information
zeroclaw hardware info --chip STM32F401RE

# Add peripheral board configuration
zeroclaw peripheral add nucleo-f401re /dev/ttyACM0

# Flash firmware to connected board
zeroclaw peripheral flash --port /dev/ttyACM0

# List configured peripherals
zeroclaw peripheral list
```

## Configuration Reference

### Core Provider Configuration

Configure the default AI provider, model, and authentication in `~/.zeroclaw/config.toml`.

```toml
# Primary provider configuration
api_key = "sk-your-openrouter-key"
default_provider = "openrouter"
default_model = "anthropic/claude-sonnet-4-6"
default_temperature = 0.7

# Custom OpenAI-compatible endpoint
# default_provider = "custom:https://your-api.example.com"

# Custom Anthropic-compatible endpoint
# default_provider = "anthropic-custom:https://your-anthropic-api.com"

# Local Ollama configuration
# default_provider = "ollama"
# default_model = "llama3.2"
# api_url = "http://localhost:11434"

# llama.cpp server configuration
# default_provider = "llamacpp"
# api_url = "http://127.0.0.1:8033/v1"
# default_model = "ggml-org/gpt-oss-20b-GGUF"
```

### Memory Backend Configuration

Configure persistent memory storage with optional vector embeddings for semantic search.

```toml
[memory]
backend = "sqlite"              # "sqlite", "lucid", "postgres", "markdown", "none"
auto_save = true
embedding_provider = "openai"   # "none", "openai", "custom:https://..."
embedding_model = "text-embedding-3-small"
embedding_dimensions = 1536
vector_weight = 0.7
keyword_weight = 0.3

# PostgreSQL backend (optional)
# [storage.provider.config]
# provider = "postgres"
# db_url = "postgres://user:password@host:5432/zeroclaw"
# schema = "public"
# table = "memories"
# connect_timeout_secs = 15
```

### Security and Autonomy Configuration

Configure workspace restrictions, command allowlists, and approval workflows.

```toml
[autonomy]
level = "supervised"           # "readonly", "supervised", "full"
workspace_only = true          # Restrict to workspace directory
allowed_commands = ["git", "npm", "cargo", "ls", "cat", "grep", "python"]
forbidden_paths = ["/etc", "/root", "/proc", "/sys", "~/.ssh", "~/.gnupg", "~/.aws"]
allowed_roots = ["~/Desktop/projects", "/opt/shared-repo"]
max_actions_per_hour = 20
require_approval_for_medium_risk = true
block_high_risk_commands = true

[gateway]
host = "127.0.0.1"
port = 42617
require_pairing = true
allow_public_bind = false

[secrets]
encrypt = true                 # Encrypt API keys at rest
```

### Channel Configuration Examples

Configure messaging platform integrations with allowlists and authentication.

```toml
[channels_config]
message_timeout_secs = 300     # Base timeout for LLM responses

[channels_config.telegram]
bot_token = "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11"
allowed_users = ["username1", "123456789"]  # usernames or numeric IDs
stream_mode = "partial"        # "off" or "partial" for streaming responses
interrupt_on_new_message = true

[channels_config.discord]
bot_token = "discord-bot-token"
guild_id = "123456789012345678"
allowed_users = ["*"]          # "*" allows all users
listen_to_bots = false
mention_only = false

[channels_config.slack]
bot_token = "xoxb-your-bot-token"
app_token = "xapp-your-app-token"
channel_id = "*"               # "*" listens on all accessible channels
allowed_users = ["U1234567890"]

[channels_config.matrix]
homeserver = "https://matrix.example.com"
access_token = "syt_your_access_token"
user_id = "@zeroclaw:matrix.example.com"
device_id = "DEVICEID123"
room_id = "!room:matrix.example.com"
allowed_users = ["@admin:matrix.example.com"]

[channels_config.whatsapp]
# Cloud API mode
access_token = "EAAB..."
phone_number_id = "123456789012345"
verify_token = "your-verify-token"
allowed_numbers = ["+1234567890"]

[channels_config.nostr]
private_key = "nsec1..."       # hex or bech32 format
relays = ["wss://relay.damus.io", "wss://nos.lol"]
allowed_pubkeys = ["npub1..."] # empty = deny all, "*" = allow all
```

### Delegate Sub-Agent Configuration

Configure named sub-agents for task delegation with different models and tool permissions.

```toml
[agents.researcher]
provider = "openrouter"
model = "anthropic/claude-sonnet-4-6"
system_prompt = "You are a research assistant. Focus on finding accurate information."
max_depth = 2
agentic = true
allowed_tools = ["web_search", "http_request", "file_read"]
max_iterations = 8

[agents.coder]
provider = "ollama"
model = "qwen2.5-coder:32b"
temperature = 0.2
agentic = true
allowed_tools = ["file_read", "file_write", "file_edit", "shell"]
max_iterations = 15
```

### Model and Embedding Routing

Configure route hints to keep stable references while upgrading underlying models.

```toml
[[model_routes]]
hint = "reasoning"
provider = "openrouter"
model = "anthropic/claude-opus-4-20250514"

[[model_routes]]
hint = "fast"
provider = "groq"
model = "llama-3.3-70b-versatile"

[[model_routes]]
hint = "code"
provider = "deepseek"
model = "deepseek-coder"

[[embedding_routes]]
hint = "semantic"
provider = "openai"
model = "text-embedding-3-small"
dimensions = 1536

[query_classification]
enabled = true

[[query_classification.rules]]
hint = "reasoning"
keywords = ["explain", "analyze", "why", "compare"]
min_length = 200
priority = 10

[[query_classification.rules]]
hint = "fast"
keywords = ["hi", "hello", "thanks", "ok"]
max_length = 50
priority = 5
```

### Hardware and Peripheral Configuration

Configure hardware connections for embedded development and IoT integrations.

```toml
[hardware]
enabled = true
transport = "serial"           # "none", "native", "serial", "probe"
serial_port = "/dev/ttyACM0"
baud_rate = 115200
workspace_datasheets = true    # Enable datasheet RAG for pin lookups

[peripherals]
enabled = true
datasheet_dir = "docs/datasheets"

[[peripherals.boards]]
board = "nucleo-f401re"
transport = "serial"
path = "/dev/ttyACM0"
baud = 115200

[[peripherals.boards]]
board = "esp32"
transport = "websocket"
```

## Gateway API Reference

### Health Check Endpoint

Public endpoint for monitoring gateway availability. No authentication required.

```bash
curl http://127.0.0.1:42617/health
# Response:
# {"status":"ok","version":"0.1.7"}
```

### Pairing Endpoint

Exchange the one-time pairing code (displayed at startup) for a bearer token.

```bash
# Get pairing code from gateway startup logs:
# INFO Gateway pairing code: 847291

curl -X POST http://127.0.0.1:42617/pair \
  -H "X-Pairing-Code: 847291"
# Response:
# {"token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...","expires_in":86400}
```

### Webhook Message Endpoint

Send messages to the agent via authenticated webhook. Supports idempotency keys for retry safety.

```bash
# Send a message to the agent
curl -X POST http://127.0.0.1:42617/webhook \
  -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9..." \
  -H "Content-Type: application/json" \
  -H "X-Idempotency-Key: unique-request-id-123" \
  -d '{"message": "List the files in the current directory"}'
# Response:
# {
#   "response": "Here are the files in the current directory:\n- README.md\n- src/\n- Cargo.toml",
#   "tool_calls": [{"name": "shell", "result": "README.md\nsrc\nCargo.toml"}]
# }
```

### WhatsApp Webhook Verification

Meta webhook verification endpoint for WhatsApp Cloud API integration.

```bash
# Meta sends verification request during webhook setup
curl "http://127.0.0.1:42617/whatsapp?hub.mode=subscribe&hub.verify_token=your-verify-token&hub.challenge=challenge123"
# Response: challenge123
```

## Python Companion Package (zeroclaw-tools)

### Basic Agent Creation

Create a LangGraph-based agent with consistent tool calling across any OpenAI-compatible provider.

```python
import asyncio
from zeroclaw_tools import create_agent, shell, file_read, file_write
from langchain_core.messages import HumanMessage

async def main():
    # Create agent with selected tools
    agent = create_agent(
        tools=[shell, file_read, file_write],
        model="glm-5",
        api_key="your-api-key",
        base_url="https://api.z.ai/api/coding/paas/v4"
    )

    # Execute task with automatic tool loop
    result = await agent.ainvoke({
        "messages": [HumanMessage(content="Create a Python script that lists all .py files")]
    })

    print(result["messages"][-1].content)

asyncio.run(main())
```

### Custom Tool Creation

Extend agent capabilities with custom tools using the `@tool` decorator.

```python
from zeroclaw_tools import tool, create_agent
from langchain_core.messages import HumanMessage
import httpx

@tool
def fetch_weather(city: str) -> str:
    """Fetch current weather for a city using OpenWeatherMap API."""
    api_key = os.environ.get("OPENWEATHER_API_KEY")
    url = f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"
    response = httpx.get(url)
    data = response.json()
    return f"Weather in {city}: {data['weather'][0]['description']}, {data['main']['temp']}°C"

@tool
def calculate_expression(expression: str) -> str:
    """Safely evaluate a mathematical expression."""
    allowed_chars = set("0123456789+-*/.() ")
    if not all(c in allowed_chars for c in expression):
        return "Error: Invalid characters in expression"
    return str(eval(expression))

# Use custom tools with agent
agent = create_agent(
    tools=[fetch_weather, calculate_expression],
    model="gpt-4o",
    api_key="your-openai-key"
)
```

### Discord Bot Integration

Deploy ZeroClaw as a Discord bot with user allowlisting and guild restrictions.

```python
import os
from zeroclaw_tools.integrations import DiscordBot

# Create Discord bot with security restrictions
bot = DiscordBot(
    token=os.environ["DISCORD_TOKEN"],
    guild_id=123456789012345678,
    allowed_users=["123456789", "987654321"],  # Discord user IDs
    model="anthropic/claude-sonnet-4-6",
    api_key=os.environ["OPENROUTER_API_KEY"],
    base_url="https://openrouter.ai/api/v1"
)

# Custom command handler
@bot.command("summarize")
async def summarize_url(ctx, url: str):
    """Summarize content from a URL."""
    result = await bot.agent.ainvoke({
        "messages": [HumanMessage(content=f"Fetch and summarize: {url}")]
    })
    await ctx.send(result["messages"][-1].content)

bot.run()
```

### CLI Usage

Use zeroclaw-tools from the command line for quick agent interactions.

```bash
# Set environment variables
export API_KEY="your-api-key"
export API_BASE="https://openrouter.ai/api/v1"

# Single message execution
zeroclaw-tools "List all Python files in the current directory and count lines of code"

# Interactive mode
zeroclaw-tools -i

# With specific model
zeroclaw-tools --model "anthropic/claude-sonnet-4-6" "Explain this error: ImportError: No module named 'foo'"
```

## Built-in Tools Reference

### Shell Tool

Execute shell commands with security policy enforcement and workspace restrictions.

```json
{
  "name": "shell",
  "parameters": {
    "command": "git status",
    "working_directory": "/path/to/repo"
  }
}
// Result: {"success": true, "output": "On branch main\nnothing to commit, working tree clean"}
```

### File Operations

Read, write, and edit files with path validation and security checks.

```json
// file_read
{"name": "file_read", "parameters": {"path": "src/main.rs", "line_start": 1, "line_end": 50}}

// file_write
{"name": "file_write", "parameters": {"path": "output.txt", "content": "Hello, World!"}}

// file_edit (surgical edits)
{"name": "file_edit", "parameters": {
  "path": "config.toml",
  "old_text": "temperature = 0.7",
  "new_text": "temperature = 0.5"
}}
```

### Memory Tools

Store and recall information with semantic search capabilities.

```json
// memory_store
{"name": "memory_store", "parameters": {
  "key": "user_preferences",
  "content": "User prefers concise responses with code examples"
}}

// memory_recall
{"name": "memory_recall", "parameters": {"query": "user preferences", "limit": 5}}
// Result: {"success": true, "output": "[{\"key\": \"user_preferences\", \"content\": \"User prefers...\", \"score\": 0.92}]"}

// memory_forget
{"name": "memory_forget", "parameters": {"key": "user_preferences"}}
```

### HTTP Request Tool

Make HTTP requests to allowed domains with configurable timeouts and size limits.

```json
{
  "name": "http_request",
  "parameters": {
    "method": "POST",
    "url": "https://api.example.com/data",
    "headers": {"Authorization": "Bearer token123"},
    "body": "{\"query\": \"search term\"}",
    "timeout_secs": 30
  }
}
```

### Delegate Tool

Delegate tasks to specialized sub-agents with different models and tool permissions.

```json
{
  "name": "delegate",
  "parameters": {
    "agent": "researcher",
    "task": "Find recent papers on transformer architectures published in 2025"
  }
}
// Uses the "researcher" sub-agent configured in [agents.researcher]
```

## Summary

ZeroClaw serves as a comprehensive AI assistant runtime for teams requiring lightweight, secure, and highly configurable agent deployments. Primary use cases include edge AI deployments on resource-constrained hardware (Raspberry Pi, IoT devices), multi-channel communication hubs that unify Telegram, Discord, Slack, and other platforms under a single agent, and embedded development workflows with direct hardware peripheral control. The trait-driven architecture enables seamless provider switching between cloud APIs (OpenAI, Anthropic, OpenRouter) and local models (Ollama, llama.cpp, vLLM) without code changes.

Integration patterns center around the configuration-first approach where `config.toml` defines all provider credentials, channel connections, security policies, and tool permissions. For webhook integrations, the gateway API provides authenticated endpoints with pairing codes and bearer tokens. The Python companion package (`zeroclaw-tools`) offers LangGraph-based tool calling for environments requiring consistent tool execution across providers with inconsistent native support. Hardware integrations follow a board-agnostic protocol supporting STM32 Nucleo, Arduino, ESP32, and Raspberry Pi GPIO through serial, USB, and WebSocket transports.
