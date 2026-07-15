# Agent Zero

Agent Zero is a personal, organic agentic AI framework designed to dynamically grow and learn with you. Unlike pre-programmed agent systems, Agent Zero operates as a fully transparent, customizable, and interactive general-purpose assistant that uses the computer as its primary tool to accomplish tasks. The framework runs entirely in Docker containers, providing consistent environments across platforms with enhanced security through containerization.

The core philosophy of Agent Zero centers on flexibility and extensibility. The system employs a hierarchical multi-agent architecture where agents can create subordinate agents to delegate subtasks, maintaining clean context while solving complex problems. Every aspect of the framework—from prompts to tools to extensions—can be customized without hard-coded limitations, allowing the agent's behavior to be shaped entirely through configuration rather than code changes.

## Quick Start Installation

Pull and run Agent Zero with Docker to get started in minutes.

```bash
# Pull the Agent Zero Docker image
docker pull agent0ai/agent-zero

# Run the container exposing port 50001
docker run -p 50001:80 agent0ai/agent-zero

# Access the web UI at http://localhost:50001
```

## External API: Send Messages

The `/api_message` endpoint allows external applications to send messages to Agent Zero and receive responses. Supports text messages, file attachments, conversation continuity via context IDs, and project activation.

```javascript
// Send a basic message to Agent Zero
async function sendMessage() {
    const response = await fetch('http://localhost:50001/api_message', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'X-API-KEY': 'YOUR_API_KEY'
        },
        body: JSON.stringify({
            message: "Analyze the current directory structure and list all Python files",
            lifetime_hours: 24
        })
    });

    const data = await response.json();
    console.log('Response:', data.response);
    console.log('Context ID:', data.context_id); // Save for conversation continuation
    return data;
}

// Continue an existing conversation
async function continueConversation(contextId) {
    const response = await fetch('http://localhost:50001/api_message', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'X-API-KEY': 'YOUR_API_KEY'
        },
        body: JSON.stringify({
            context_id: contextId,
            message: "Now count the lines of code in those Python files"
        })
    });
    return response.json();
}

// Send message with file attachment
async function sendWithAttachment() {
    const fileContent = "def hello(): return 'world'";
    const base64Content = btoa(fileContent);

    const response = await fetch('http://localhost:50001/api_message', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'X-API-KEY': 'YOUR_API_KEY'
        },
        body: JSON.stringify({
            message: "Review this Python code for improvements",
            attachments: [{
                filename: "code.py",
                base64: base64Content
            }],
            project: "code-review-project" // Optionally activate a project
        })
    });
    return response.json();
}
```

## External API: Retrieve Logs

The `/api_log_get` endpoint retrieves conversation log data by context ID, returning execution history and agent responses.

```javascript
// Get conversation logs using GET request
async function getLogsGET(contextId, length = 50) {
    const params = new URLSearchParams({
        context_id: contextId,
        length: length.toString()
    });

    const response = await fetch(`http://localhost:50001/api_log_get?${params}`, {
        method: 'GET',
        headers: { 'X-API-KEY': 'YOUR_API_KEY' }
    });

    const data = await response.json();
    console.log('Total items:', data.log.total_items);
    console.log('Log items:', data.log.items);
    return data;
}

// Get logs using POST request with more control
async function getLogsPOST(contextId, length = 100) {
    const response = await fetch('http://localhost:50001/api_log_get', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'X-API-KEY': 'YOUR_API_KEY'
        },
        body: JSON.stringify({
            context_id: contextId,
            length: length
        })
    });

    const data = await response.json();
    // Response includes: context_id, log.guid, log.total_items,
    // log.returned_items, log.start_position, log.progress, log.items
    return data;
}
```

## External API: Chat Management

The `/api_terminate_chat` and `/api_reset_chat` endpoints manage chat lifecycle—terminating frees resources while resetting clears history but keeps the context alive.

```javascript
// Terminate and remove a chat context completely
async function terminateChat(contextId) {
    const response = await fetch('http://localhost:50001/api_terminate_chat', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'X-API-KEY': 'YOUR_API_KEY'
        },
        body: JSON.stringify({ context_id: contextId })
    });
    return response.json();
}

// Reset chat history while keeping context_id alive
async function resetChat(contextId) {
    const response = await fetch('http://localhost:50001/api_reset_chat', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'X-API-KEY': 'YOUR_API_KEY'
        },
        body: JSON.stringify({ context_id: contextId })
    });

    // After reset, continue with fresh conversation using same context_id
    const data = await response.json();
    console.log('Chat reset, context preserved:', data.context_id);
    return data;
}

// Complete workflow: send, work, then cleanup
async function workflowWithCleanup() {
    const result = await sendMessage();
    const contextId = result.context_id;

    // Do work...
    await continueConversation(contextId);

    // Clean up when done
    await terminateChat(contextId);
}
```

## External API: File Retrieval

The `/api_files_get` endpoint retrieves file contents by paths, returning files as base64 encoded data for processing uploaded attachments or generated files.

```javascript
// Retrieve files by their paths
async function getFiles(filePaths) {
    const response = await fetch('http://localhost:50001/api_files_get', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
            'X-API-KEY': 'YOUR_API_KEY'
        },
        body: JSON.stringify({
            paths: filePaths  // Array of paths like ["/a0/usr/uploads/file.txt"]
        })
    });

    const data = await response.json();

    // Convert base64 back to text for text files
    for (const [filename, base64Content] of Object.entries(data)) {
        try {
            const textContent = atob(base64Content);
            console.log(`${filename}: ${textContent.substring(0, 200)}...`);
        } catch (e) {
            console.log(`${filename}: Binary file (${base64Content.length} chars)`);
        }
    }
    return data;
}

// Example: retrieve uploaded files
getFiles([
    "/a0/usr/uploads/document.txt",
    "/a0/usr/uploads/data.json"
]);
```

## MCP Server Configuration

Agent Zero can connect to external MCP (Model Context Protocol) servers to extend its capabilities with additional tools like browser automation, database access, and workflow automation.

```json
// MCP configuration in Settings > MCP/A2A > External MCP Servers
{
  "mcpServers": {
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest"]
    },
    "sqlite": {
      "command": "uvx",
      "args": ["mcp-server-sqlite", "--db-path", "/root/db.sqlite"]
    },
    "external-api": {
      "url": "https://api.example.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

```bash
# Tools become available with server prefix
# Server: chrome-devtools → Tool: chrome_devtools.navigate_to_url
# Server: sqlite → Tool: sqlite.execute_query

# Using MCP tools in prompts:
# "Use chrome_devtools to navigate to https://example.com and take a screenshot"
# "Query the sqlite database for all users created today"
```

## MCP Server: Agent Zero as MCP Server

Agent Zero can expose itself as an MCP server, allowing other MCP-compatible clients (like Claude Code, Cursor, or other agents) to connect and use Agent Zero's capabilities.

```json
// MCP client configuration to connect to Agent Zero
{
    "mcpServers": {
        "agent-zero": {
            "type": "sse",
            "url": "http://localhost:50001/mcp/t-YOUR_API_TOKEN/sse"
        },
        "agent-zero-http": {
            "type": "streamable-http",
            "url": "http://localhost:50001/mcp/t-YOUR_API_TOKEN/http/"
        },
        "agent-zero-with-project": {
            "type": "sse",
            "url": "http://localhost:50001/mcp/t-YOUR_API_TOKEN/p-my-project/sse"
        }
    }
}
```

## A2A (Agent-to-Agent) Communication

The A2A protocol enables Agent Zero instances to communicate with each other for distributed workflows, task delegation, and long-running collaboration.

```bash
# A2A Connection URL format
http://YOUR_HOST:PORT/a2a/t-YOUR_API_TOKEN

# With project context
http://YOUR_HOST:PORT/a2a/t-YOUR_API_TOKEN/p-PROJECT_NAME

# Test A2A connectivity
curl -X POST http://localhost:50001/a2a/t-YOUR_TOKEN \
  -H "Content-Type: application/json" \
  -d '{"message": "Hello from another agent"}'
```

```javascript
// Enable A2A in Settings > MCP/A2A > A0 A2A Server
// Connection URLs are automatically generated from your credentials

// Use cases:
// - Two Agent Zero instances collaborating on different aspects of a task
// - Main agent delegates frontend work to specialized agent:
//   http://localhost:8081/a2a/t-frontend-token/p-webapp-ui
// - Remote agent collaboration across servers
```

## WebSocket Real-Time Communication

Agent Zero provides a WebSocket infrastructure for real-time communication between frontend and backend, replacing polling-based approaches with event-driven updates.

```javascript
// Frontend WebSocket client usage
import { getNamespacedClient, createCorrelationId } from '/js/websocket.js';

const websocket = getNamespacedClient('/state_sync');

// Connect (lazy connection - happens automatically on first use)
await websocket.connect();

// Emit fire-and-forget event
websocket.emit('dashboard_event', { action: 'refresh' });

// Request with response (aggregates from multiple handlers)
const { correlationId, results } = await websocket.request(
    'refresh_metrics',
    { duration: '1h' },
    { timeoutMs: 2000, correlationId: createCorrelationId('metrics') }
);

results.forEach(({ handlerId, ok, data, error }) => {
    if (ok) console.log(`${handlerId}: ${JSON.stringify(data)}`);
    else console.warn(`${handlerId} error:`, error);
});

// Subscribe to server events
websocket.on('dashboard_update', (envelope) => {
    const { handlerId, correlationId, ts, data } = envelope;
    console.log('Update from', handlerId, ':', data);
});

// Cleanup subscriptions
websocket.off('dashboard_update');
```

## WebSocket Backend Handler

Create custom WebSocket handlers to process events and emit responses from the backend.

```python
# File: python/websocket_handlers/dashboard_handler.py
from python.helpers.websocket import WebSocketHandler
from typing import Any

class DashboardHandler(WebSocketHandler):
    @classmethod
    def get_event_types(cls) -> list[str]:
        return ["dashboard_refresh", "dashboard_push"]

    async def process_event(self, event_type: str, data: dict[str, Any], sid: str) -> dict | None:
        if event_type == "dashboard_refresh":
            stats = await self._load_stats(data.get("scope", "all"))
            return {"ok": True, "stats": stats}

        if event_type == "dashboard_push":
            # Broadcast to all clients except sender
            await self.broadcast(
                "dashboard_update",
                {"stats": data.get("stats", {}), "source": sid},
                exclude_sids=sid,
            )
            return None  # Fire-and-forget, no response

    async def _load_stats(self, scope: str) -> dict:
        # Load and return dashboard statistics
        return {"active_sessions": 5, "tasks_completed": 42, "scope": scope}
```

## Creating Custom Extensions

Extensions hook into specific points in the agent's lifecycle to modify or enhance behavior. Create extensions by inheriting from the Extension base class.

```python
# File: agents/my-agent/extensions/agent_init/_10_custom_extension.py
from python.helpers.extension import Extension

class CustomExtension(Extension):
    async def execute(self, **kwargs):
        # Customize agent during initialization
        self.agent.agent_name = "CustomAgent" + str(self.agent.number)

        # Add custom data to agent context
        self.agent.set_data("custom_config", {
            "max_retries": 3,
            "timeout": 30
        })

        # Log initialization
        from python.helpers.print_style import PrintStyle
        PrintStyle(font_color="#00FF00").print(
            f"Custom extension initialized for {self.agent.agent_name}"
        )
```

```python
# Extension points available:
# - agent_init: When agent is initialized
# - before_main_llm_call: Before calling the LLM
# - message_loop_start: Start of message processing
# - message_loop_prompts_before: Before prompts are processed
# - message_loop_prompts_after: After prompts are processed
# - message_loop_end: End of message processing
# - monologue_start/end: During agent reasoning
# - response_stream: When streaming responses
# - system_prompt: When processing system prompts
```

## Creating Custom Tools

Tools provide specific functionality that agents can invoke. Create tools by inheriting from the Tool base class.

```python
# File: agents/my-agent/tools/custom_tool.py
from python.helpers.tool import Tool, Response

class CustomTool(Tool):
    async def execute(self, **kwargs):
        # Get parameters from tool call
        query = self.args.get("query", "")
        limit = self.args.get("limit", 10)

        # Perform tool action
        results = await self._search_database(query, limit)

        # Return response to agent
        return Response(
            message=f"Found {len(results)} results for '{query}':\n" +
                    "\n".join(results),
            break_loop=False  # Continue agent loop
        )

    async def _search_database(self, query: str, limit: int) -> list:
        # Implement search logic
        return [f"Result {i}: {query}" for i in range(min(limit, 5))]
```

```markdown
<!-- File: agents/my-agent/prompts/agent.system.tool.custom_tool.md -->
## custom_tool
Search the database for information.
Use when you need to find data matching a query.

**Parameters:**
- query (string, required): Search query
- limit (integer, optional): Maximum results (default: 10)

**Example:**
~~~json
{
    "tool_name": "custom_tool",
    "tool_args": {
        "query": "user authentication",
        "limit": 5
    }
}
~~~
```

## Creating Skills (SKILL.md Standard)

Skills provide contextual expertise using the open SKILL.md standard. Skills are dynamically loaded when relevant and compatible with Claude Code, Cursor, and other AI tools.

```yaml
# File: usr/skills/code-reviewer/SKILL.md
---
name: "code-reviewer"
description: "Review code for quality, security, and best practices. Use when asked to review, check, or audit code."
version: "1.0.0"
author: "Your Name"
tags: ["review", "quality", "security", "code"]
trigger_patterns:
  - "review code"
  - "check code"
  - "code audit"
  - "security review"
---

# Code Reviewer

## When to Use
Activate when the user asks to review, check, audit, or assess code quality.

## Review Process

### Step 1: Security Analysis
Check for common vulnerabilities:
- SQL injection risks
- XSS vulnerabilities
- Hardcoded secrets
- Unsafe input handling

### Step 2: Code Quality
Evaluate:
- Error handling completeness
- Code organization and readability
- Naming conventions
- Documentation coverage

### Step 3: Performance
Look for:
- Inefficient loops or queries
- Memory leaks potential
- Unnecessary computations

## Output Format
Provide findings in this structure:

```markdown
## Code Review Summary

### Security Issues
- [CRITICAL/HIGH/MEDIUM/LOW] Description

### Quality Concerns
- Issue description and recommendation

### Performance Notes
- Optimization suggestions

### Recommendations
1. Priority action items
```

## Example Review
**User**: "Review this function for issues"

**Response**: Analyzing the function for security, quality, and performance...
```

## Project Configuration

Projects provide isolated workspaces with dedicated context, instructions, memory, and secrets. Configure projects via the UI or programmatically.

```json
// File: usr/projects/my-project/.a0proj/project.json
{
    "name": "my-project",
    "description": "Web application development project",
    "color": "#3498db",
    "memory_isolation": true,
    "file_structure": {
        "enabled": true,
        "max_depth": 5,
        "max_files": 100,
        "gitignore_patterns": [
            ".a0proj/",
            "node_modules/",
            "__pycache__/",
            ".git/",
            "venv/"
        ]
    }
}
```

```bash
# Project directory structure
/a0/usr/projects/my-project/
├── .a0proj/
│   ├── project.json          # Project configuration
│   ├── instructions/         # Custom prompts injected into context
│   │   └── main.md          # Primary instructions for this project
│   ├── knowledge/           # Project-specific knowledge base
│   ├── memory/              # Isolated memory storage
│   ├── secrets.env          # Project secrets (API_KEY=xxx)
│   └── variables.env        # Project variables (ENV=production)
├── src/                     # Your project files
└── data/
```

```markdown
<!-- File: usr/projects/my-project/.a0proj/instructions/main.md -->
## Your Role
You are a senior web developer working on the my-project application.

## Operational Context
- Work directory: `/usr/projects/my-project/`
- Source code: `/usr/projects/my-project/src/`
- Use TypeScript for all new code
- Follow the existing code style and patterns

## Key Responsibilities
1. Implement features according to specifications
2. Write tests for all new functionality
3. Update documentation when making changes
4. Ensure code passes linting and type checks
```

## Task Scheduling

Tasks enable automated or scheduled work in isolated contexts. Configure scheduled, planned, or ad-hoc tasks via the UI or programmatically.

```python
# Task types:
# - Scheduled: Cron-based recurring execution
# - Planned: Specific date/time execution list
# - Ad-hoc: Manual execution only

# Common cron patterns:
# "0 9 * * *"      - Every day at 9 AM
# "0 * * * *"      - Every hour
# "0 10 * * 1"     - Every Monday at 10 AM
# "*/15 * * * *"   - Every 15 minutes
# "0 0 1 * *"      - First day of month at midnight
```

```markdown
<!-- Example task configurations -->

## Daily Report Task
- **Name**: "Morning Inbox Summary"
- **Type**: Scheduled (0 9 * * *)
- **Project**: "Email Automation"
- **Prompt**: "Check my Gmail inbox for new messages from the last 24 hours. Summarize important emails by category and highlight any urgent items."

## Server Monitoring Task
- **Name**: "Server Health Check"
- **Type**: Scheduled (*/30 * * * *)
- **Project**: "DevOps Monitoring"
- **Prompt**: "Check server status, CPU usage, and disk space. Alert me if any metric exceeds threshold."

## Campaign Automation Task
- **Name**: "Product Launch Sequence"
- **Type**: Planned
- **Executions**:
  - 2026-03-01 09:00 - Send launch announcement
  - 2026-03-03 14:00 - Send feature highlights
  - 2026-03-07 10:00 - Send customer testimonials
- **Project**: "Marketing Campaigns"
```

## Prompts with Dynamic Variables

Prompts support variable placeholders and dynamic loaders for runtime customization.

```markdown
<!-- File: prompts/agent.system.datetime.md -->
# Current system date and time of user
- current datetime: {{date_time}}
- rely on this info always up to date
```

```python
# File: prompts/agent.system.tools.py
# Dynamic variable loader - runs at prompt processing time
from python.helpers.files import VariablesPlugin
from python.helpers import files
import os
from typing import Any

class Tools(VariablesPlugin):
    def get_variables(self, file: str, backup_dirs: list[str] | None = None) -> dict[str, Any]:
        # Dynamically collect all tool instruction files
        folder = files.get_abs_path(os.path.dirname(file))
        folders = [folder]
        if backup_dirs:
            folders.extend([files.get_abs_path(d) for d in backup_dirs])

        prompt_files = files.get_unique_filenames_in_dirs(folders, "agent.system.tool.*.md")

        tools = []
        for prompt_file in prompt_files:
            tool = files.read_file(prompt_file)
            tools.append(tool)

        return {"tools": "\n\n".join(tools)}
```

```markdown
<!-- File includes syntax -->
# Agent Zero System Manual

{{ include "agent.system.main.role.md" }}

{{ include "agent.system.main.environment.md" }}

{{ include "agent.system.main.communication.md" }}

<!-- Variables from dynamic loaders -->
# Available Tools
{{tools}}
```

## Environment Variables Configuration

Configure Agent Zero settings via environment variables with the `A0_SET_` prefix.

```bash
# Docker environment configuration
docker run -p 50001:80 \
  -e A0_SET_chat_model_provider=openrouter \
  -e A0_SET_chat_model_name=anthropic/claude-3.5-sonnet \
  -e A0_SET_utility_model_provider=openrouter \
  -e A0_SET_utility_model_name=anthropic/claude-3-haiku \
  -e AUTH_LOGIN=admin \
  -e AUTH_PASSWORD=secure_password \
  agent0ai/agent-zero

# Common settings:
# A0_SET_chat_model_provider - LLM provider (openrouter, openai, anthropic, etc.)
# A0_SET_chat_model_name - Model name for chat
# A0_SET_utility_model_provider - Provider for utility tasks
# A0_SET_utility_model_name - Model for summarization/memory
# A0_SET_embedding_model_provider - Provider for embeddings
# AUTH_LOGIN / AUTH_PASSWORD - Web UI authentication
```

Agent Zero serves as a comprehensive platform for building autonomous AI assistants that can execute code, search the web, manage files, maintain persistent memory, and communicate with users and other agents. The framework excels at complex, multi-step tasks requiring tool orchestration, from financial analysis and code generation to automated monitoring and workflow automation. Its hierarchical multi-agent architecture allows breaking down complex problems into delegated subtasks while maintaining context isolation.

The extensibility model—combining custom prompts, tools, extensions, and skills—enables tailoring Agent Zero for specific domains or workflows without modifying core code. Integration patterns span REST APIs for external applications, WebSockets for real-time communication, MCP for tool interoperability, and A2A for agent-to-agent collaboration. Whether deployed locally for personal assistance or scaled across servers for enterprise automation, Agent Zero provides the building blocks for sophisticated AI agent systems that learn and adapt to user needs over time.
