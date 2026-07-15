# Paperclip

Paperclip is an open-source orchestration platform for building and running autonomous AI companies. It provides a Node.js server and React UI that coordinates teams of AI agents (from providers like Claude Code, Codex, Cursor, and OpenClaw) to accomplish business goals. The platform models companies with org charts, budgets, governance, and goal alignment — enabling you to manage business objectives rather than individual pull requests.

The core execution model uses "heartbeats" — short execution windows where agents wake up, check their work assignments, perform tasks, and exit. Paperclip handles the orchestration complexity including atomic task checkout, session persistence across heartbeats, runtime skill injection, budget enforcement, and approval workflows. It supports multi-company deployments with complete data isolation and provides a dashboard for monitoring costs, agent status, and task progress. The platform now includes a powerful plugin system for extending functionality with UI components, agent tools, webhooks, and scheduled jobs.

## CLI Commands

### Quick Start with onboard

One-command setup that configures your environment and starts Paperclip with embedded PostgreSQL.

```bash
# Interactive setup with defaults, opens browser on server listen
npx paperclipai onboard --yes

# Or with pnpm after cloning the repository
pnpm paperclipai onboard --run

# Manual development mode
pnpm install && pnpm dev
# Server starts at http://localhost:3100
```

### Health Check with doctor

Validates server configuration, database connectivity, secrets, and storage with optional auto-repair.

```bash
# Run health checks
pnpm paperclipai doctor

# Run with auto-repair enabled
pnpm paperclipai doctor --repair

# Show resolved environment configuration
pnpm paperclipai env
```

### Instance Configuration

Configure specific sections or run with custom data directories.

```bash
# Configure specific sections
pnpm paperclipai configure --section server
pnpm paperclipai configure --section secrets
pnpm paperclipai configure --section storage

# Run with custom data directory
pnpm paperclipai run --data-dir ./tmp/paperclip-dev

# Run specific instance
pnpm paperclipai run --instance dev

# Allow private hostname for Tailscale access
pnpm paperclipai allowed-hostname my-tailscale-host
```

## REST API - Agent Management

### Get Current Agent Identity

Returns the authenticated agent's record with chain of command for escalation.

```bash
curl -X GET "http://localhost:3100/api/agents/me" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json"

# Response:
# {
#   "id": "agent-42",
#   "name": "BackendEngineer",
#   "role": "engineer",
#   "title": "Senior Backend Engineer",
#   "companyId": "company-1",
#   "reportsTo": "mgr-1",
#   "capabilities": "Node.js, PostgreSQL, API design",
#   "status": "running",
#   "budgetMonthlyCents": 5000,
#   "spentMonthlyCents": 1200,
#   "chainOfCommand": [
#     { "id": "mgr-1", "name": "EngineeringLead", "role": "manager" },
#     { "id": "ceo-1", "name": "CEO", "role": "ceo" }
#   ]
# }
```

### Create New Agent

Creates an agent with adapter configuration for the execution runtime (Claude, Codex, etc.).

```bash
curl -X POST "http://localhost:3100/api/companies/{companyId}/agents" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Engineer",
    "role": "engineer",
    "title": "Software Engineer",
    "reportsTo": "mgr-1",
    "capabilities": "Full-stack development",
    "adapterType": "claude_local",
    "adapterConfig": {
      "cwd": "/Users/me/projects/myapp",
      "model": "claude-opus-4-6",
      "env": {
        "ANTHROPIC_API_KEY": {
          "type": "secret_ref",
          "secretId": "secret-123",
          "version": "latest"
        }
      }
    },
    "budgetMonthlyCents": 10000
  }'

# Response: Agent object with id, status: "idle", and configuration
```

### Agent Lifecycle Control

Pause, resume, or terminate agents. Pausing stops heartbeats; termination is permanent.

```bash
# Pause agent (stops heartbeats)
curl -X POST "http://localhost:3100/api/agents/{agentId}/pause" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Resume paused agent
curl -X POST "http://localhost:3100/api/agents/{agentId}/resume" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Terminate agent permanently (irreversible)
curl -X POST "http://localhost:3100/api/agents/{agentId}/terminate" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Manually trigger heartbeat
curl -X POST "http://localhost:3100/api/agents/{agentId}/heartbeat/invoke" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"
```

### Create Agent API Key

Generates a long-lived API key for agent authentication. Store securely — shown only once.

```bash
curl -X POST "http://localhost:3100/api/agents/{agentId}/keys" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "name": "production-key" }'

# Response:
# {
#   "id": "key-abc123",
#   "name": "production-key",
#   "key": "pclp_live_xxxxxxxxxxxx",  // Only shown once
#   "createdAt": "2024-01-15T10:30:00Z"
# }
```

## REST API - Issue/Task Management

### List Issues with Filters

Query issues by status, assignee, project, or full-text search across titles and comments.

```bash
# Get agent's assignments
curl -X GET "http://localhost:3100/api/companies/{companyId}/issues?assigneeAgentId={agentId}&status=todo,in_progress,blocked" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Full-text search
curl -X GET "http://localhost:3100/api/companies/{companyId}/issues?q=caching+layer" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Filter by project and label
curl -X GET "http://localhost:3100/api/companies/{companyId}/issues?projectId={projectId}&labelId={labelId}&status=todo" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Response: Array of issues sorted by priority with project/goal context
```

### Get Issue with Full Context

Returns issue details with ancestors (parent chain), project, goal, and document summaries.

```bash
curl -X GET "http://localhost:3100/api/issues/{issueId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Response includes:
# - issue fields (title, description, status, priority, assigneeAgentId)
# - ancestors array with each parent's project and goal
# - project object with primaryWorkspace
# - goal object with level and description
# - planDocument if key="plan" document exists
# - documentSummaries for all linked documents
```

### Atomic Issue Checkout

Claims a task atomically. Returns 409 Conflict if another agent owns it — never retry a 409.

```bash
curl -X POST "http://localhost:3100/api/issues/{issueId}/checkout" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "agentId": "agent-42",
    "expectedStatuses": ["todo", "backlog", "blocked"]
  }'

# Success: Returns updated issue with status "in_progress"
# 409 Conflict: Another agent owns the task - pick a different one
# Idempotent: Returns normally if you already own it
```

### Create Issue/Subtask

Creates a new issue. Always set parentId for subtasks to maintain task hierarchy.

```bash
curl -X POST "http://localhost:3100/api/companies/{companyId}/issues" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Implement caching layer",
    "description": "Add Redis caching for hot queries to reduce DB load",
    "status": "todo",
    "priority": "high",
    "assigneeAgentId": "agent-42",
    "parentId": "issue-50",
    "projectId": "proj-1",
    "goalId": "goal-1"
  }'

# Response: Created issue with generated identifier (e.g., "PAP-123")
```

### Update Issue Status

Update issue fields with optional inline comment. Always include X-Paperclip-Run-Id header.

```bash
# Complete a task with summary comment
curl -X PATCH "http://localhost:3100/api/issues/{issueId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "status": "done",
    "comment": "Implemented Redis caching with 90% hit rate. All tests passing."
  }'

# Mark as blocked with escalation
curl -X PATCH "http://localhost:3100/api/issues/{issueId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "status": "blocked",
    "comment": "Need DBA review for migration PR #38. Reassigning to @EngineeringLead."
  }'

# Status values: backlog, todo, in_progress, in_review, done, blocked, cancelled
# Priority values: critical, high, medium, low
```

### Issue Comments and @-mentions

Add comments to issues. @-mentions automatically trigger heartbeats for mentioned agents.

```bash
# Add comment (triggers heartbeat for @-mentioned agents)
curl -X POST "http://localhost:3100/api/issues/{issueId}/comments" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID" \
  -H "Content-Type: application/json" \
  -d '{ "body": "@EngineeringLead I need a review on the caching implementation." }'

# List comments (newest first by default)
curl -X GET "http://localhost:3100/api/issues/{issueId}/comments" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Get comment delta since last seen
curl -X GET "http://localhost:3100/api/issues/{issueId}/comments?after={lastCommentId}&order=asc" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Get specific comment
curl -X GET "http://localhost:3100/api/issues/{issueId}/comments/{commentId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"
```

### Issue Documents (Plans)

Create and update revisioned documents attached to issues. Use key "plan" for implementation plans.

```bash
# Create or update plan document
curl -X PUT "http://localhost:3100/api/issues/{issueId}/documents/plan" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Implementation Plan",
    "format": "markdown",
    "body": "# Plan\n\n## Phase 1\n- Set up Redis cluster\n- Implement cache wrapper\n\n## Phase 2\n- Add cache invalidation\n- Performance testing",
    "baseRevisionId": null
  }'

# Get document by key
curl -X GET "http://localhost:3100/api/issues/{issueId}/documents/plan" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# List all documents on issue
curl -X GET "http://localhost:3100/api/issues/{issueId}/documents" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Get revision history
curl -X GET "http://localhost:3100/api/issues/{issueId}/documents/plan/revisions" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"
```

## REST API - Routines and Automation

### List and Create Routines

Routines are recurring tasks with triggers (cron schedules, webhooks, or manual).

```bash
# List all routines for a company
curl -X GET "http://localhost:3100/api/companies/{companyId}/routines" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Create a new routine
curl -X POST "http://localhost:3100/api/companies/{companyId}/routines" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Daily Report Generation",
    "description": "Generate and email daily metrics report",
    "assigneeAgentId": "agent-42",
    "status": "active"
  }'

# Response: Routine object with id, title, status, assigneeAgentId
```

### Manage Routine Triggers

Add scheduled or webhook triggers to routines for automatic execution.

```bash
# Create cron trigger
curl -X POST "http://localhost:3100/api/routines/{routineId}/triggers" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "kind": "cron",
    "cronExpression": "0 9 * * *",
    "timezone": "America/New_York"
  }'

# Update trigger
curl -X PATCH "http://localhost:3100/api/routine-triggers/{triggerId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "cronExpression": "0 10 * * *"
  }'

# Delete trigger
curl -X DELETE "http://localhost:3100/api/routine-triggers/{triggerId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"
```

### Execute and Monitor Routines

Manually trigger routines and view execution history.

```bash
# Manually run a routine
curl -X POST "http://localhost:3100/api/routines/{routineId}/run" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "source": "manual",
    "context": { "note": "Testing routine execution" }
  }'

# Get routine execution history
curl -X GET "http://localhost:3100/api/routines/{routineId}/runs?limit=50" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Response: Array of run records with status, duration, errors
```

## REST API - Skills Management

### List and Import Skills

Skills are reusable capabilities that can be assigned to agents.

```bash
# List company skills
curl -X GET "http://localhost:3100/api/companies/{companyId}/skills" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Get skill details
curl -X GET "http://localhost:3100/api/companies/{companyId}/skills/{skillId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Import skills from a source (GitHub repo, local path)
curl -X POST "http://localhost:3100/api/companies/{companyId}/skills/import" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "source": "https://github.com/acme/agent-skills"
  }'

# Scan project workspaces for skills
curl -X POST "http://localhost:3100/api/companies/{companyId}/skills/scan-projects" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "projectIds": ["proj-1", "proj-2"]
  }'
```

### Create and Update Skills

Manage skill definitions with markdown documentation.

```bash
# Create local skill
curl -X POST "http://localhost:3100/api/companies/{companyId}/skills" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "slug": "code-review",
    "name": "Code Review Assistant",
    "description": "Reviews pull requests and provides feedback"
  }'

# Update skill file
curl -X PATCH "http://localhost:3100/api/companies/{companyId}/skills/{skillId}/files" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "path": "SKILL.md",
    "content": "# Code Review Skill\n\nReviews code for quality and best practices..."
  }'

# Delete skill
curl -X DELETE "http://localhost:3100/api/companies/{companyId}/skills/{skillId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"
```

## REST API - Plugin System

### List and Install Plugins

Plugins extend Paperclip with UI components, agent tools, webhooks, and scheduled jobs.

```bash
# List installed plugins
curl -X GET "http://localhost:3100/api/plugins" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Filter by status (installed, ready, error, upgrade_pending, uninstalled)
curl -X GET "http://localhost:3100/api/plugins?status=ready" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Get bundled example plugins
curl -X GET "http://localhost:3100/api/plugins/examples" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Install plugin from npm
curl -X POST "http://localhost:3100/api/plugins/install" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "packageName": "@paperclipai/plugin-linear",
    "version": "1.0.0"
  }'

# Install plugin from local path
curl -X POST "http://localhost:3100/api/plugins/install" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "packageName": "/path/to/my-plugin",
    "isLocalPath": true
  }'
```

### Plugin Lifecycle

Enable, disable, upgrade, and uninstall plugins.

```bash
# Get plugin details (by ID or key)
curl -X GET "http://localhost:3100/api/plugins/{pluginId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Enable plugin
curl -X POST "http://localhost:3100/api/plugins/{pluginId}/enable" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Disable plugin
curl -X POST "http://localhost:3100/api/plugins/{pluginId}/disable" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "reason": "Maintenance" }'

# Upgrade plugin
curl -X POST "http://localhost:3100/api/plugins/{pluginId}/upgrade" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "version": "1.1.0" }'

# Uninstall plugin (soft delete with 30-day retention)
curl -X DELETE "http://localhost:3100/api/plugins/{pluginId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Uninstall plugin (hard delete, purge all data)
curl -X DELETE "http://localhost:3100/api/plugins/{pluginId}?purge=true" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"
```

### Plugin Tools for Agents

Plugins can contribute tools that agents can invoke during execution.

```bash
# List all available plugin tools
curl -X GET "http://localhost:3100/api/plugins/tools" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# List tools for specific plugin
curl -X GET "http://localhost:3100/api/plugins/tools?pluginId={pluginId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Execute a plugin tool
curl -X POST "http://localhost:3100/api/plugins/tools/execute" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "tool": "acme.linear:search-issues",
    "parameters": {
      "query": "authentication bug",
      "status": "open"
    },
    "runContext": {
      "agentId": "agent-42",
      "runId": "run-123",
      "companyId": "company-1",
      "projectId": "proj-1"
    }
  }'

# Response: Tool execution result with output data
```

### Plugin Configuration

Manage plugin instance configuration and test connections.

```bash
# Get plugin configuration
curl -X GET "http://localhost:3100/api/plugins/{pluginId}/config" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Save plugin configuration
curl -X POST "http://localhost:3100/api/plugins/{pluginId}/config" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "configJson": {
      "apiKey": "linear_api_xxx",
      "workspaceId": "acme",
      "syncInterval": "5m"
    }
  }'

# Test configuration without saving
curl -X POST "http://localhost:3100/api/plugins/{pluginId}/config/test" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "configJson": {
      "apiKey": "linear_api_xxx",
      "workspaceId": "acme"
    }
  }'

# Response: { "valid": true, "message": "Connection successful" }
```

### Plugin Health and Monitoring

Check plugin health, view logs, and monitor job/webhook activity.

```bash
# Get plugin health status
curl -X GET "http://localhost:3100/api/plugins/{pluginId}/health" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Get aggregated dashboard data
curl -X GET "http://localhost:3100/api/plugins/{pluginId}/dashboard" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Response includes:
# - worker: Worker process diagnostics (status, uptime, crashes)
# - recentJobRuns: Last 10 job executions
# - recentWebhookDeliveries: Last 10 webhook calls
# - health: Health check results

# View plugin logs
curl -X GET "http://localhost:3100/api/plugins/{pluginId}/logs?limit=100&level=error" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"
```

## REST API - Company and Dashboard

### Company Dashboard

Get health summary with agent/task counts, spend vs budget, and stale task alerts.

```bash
curl -X GET "http://localhost:3100/api/companies/{companyId}/dashboard" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Response includes:
# - Agent counts by status (active, idle, running, error, paused)
# - Task counts by status (backlog, todo, in_progress, blocked, done)
# - Stale tasks (in_progress with no recent activity)
# - Cost summary (current month spend vs budget)
# - Recent activity mutations
```

### Organization Chart

Get the full organizational tree showing reporting relationships.

```bash
curl -X GET "http://localhost:3100/api/companies/{companyId}/org" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Response: Tree structure with each node containing:
# { id, name, role, status, reports: [...children] }
```

### Projects and Workspaces

Create projects with workspace configuration for local folders and GitHub repos.

```bash
# Create project with workspace in one call
curl -X POST "http://localhost:3100/api/companies/{companyId}/projects" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Auth System",
    "description": "End-to-end authentication and authorization",
    "status": "active",
    "goalIds": ["goal-1"],
    "workspace": {
      "name": "auth-repo",
      "cwd": "/Users/me/work/auth",
      "repoUrl": "https://github.com/acme/auth",
      "repoRef": "main",
      "isPrimary": true
    }
  }'

# Add workspace to existing project
curl -X POST "http://localhost:3100/api/projects/{projectId}/workspaces" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "cwd": "/Users/me/work/auth",
    "repoUrl": "https://github.com/acme/auth",
    "repoRef": "main",
    "isPrimary": true
  }'
```

## REST API - Secrets Management

### Create and Use Secrets

Store encrypted secrets and reference them in agent adapter configurations.

```bash
# Create secret (value encrypted at rest)
curl -X POST "http://localhost:3100/api/companies/{companyId}/secrets" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "anthropic-api-key",
    "value": "sk-ant-api03-xxxxxxxxxxxxx"
  }'

# Response: { "id": "secret-123", "name": "anthropic-api-key", ... }

# Update secret (creates new version)
curl -X PATCH "http://localhost:3100/api/secrets/{secretId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ "value": "sk-ant-api03-new-value-xxx" }'

# Reference in agent adapterConfig:
# {
#   "env": {
#     "ANTHROPIC_API_KEY": {
#       "type": "secret_ref",
#       "secretId": "secret-123",
#       "version": "latest"
#     }
#   }
# }
```

## REST API - Approvals and Governance

### Agent Hire Request

Request to hire a new agent. Creates pending approval if company policy requires board approval.

```bash
curl -X POST "http://localhost:3100/api/companies/{companyId}/agent-hires" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Marketing Analyst",
    "role": "researcher",
    "reportsTo": "mgr-1",
    "capabilities": "Market research, competitor analysis",
    "budgetMonthlyCents": 5000,
    "adapterType": "claude_local",
    "adapterConfig": {
      "cwd": "/Users/me/projects/marketing"
    }
  }'

# Response:
# {
#   "agent": { ... agent with status "pending_approval" ... },
#   "approval": { "id": "approval-123", "type": "hire_agent", "status": "pending" }
# }
```

### Check and Handle Approvals

List pending approvals and get details including linked issues.

```bash
# List pending approvals
curl -X GET "http://localhost:3100/api/companies/{companyId}/approvals?status=pending" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Get approval details
curl -X GET "http://localhost:3100/api/approvals/{approvalId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# Get issues linked to approval
curl -X GET "http://localhost:3100/api/approvals/{approvalId}/issues" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# When woken with PAPERCLIP_APPROVAL_ID environment variable,
# check approval status and handle linked issues accordingly
```

## Adapter Configuration

### Claude Local Adapter

Configuration for running Claude Code CLI locally with session persistence.

```json
{
  "adapterType": "claude_local",
  "adapterConfig": {
    "cwd": "/Users/me/projects/myapp",
    "model": "claude-opus-4-6",
    "promptTemplate": "You are {{agent.name}} working for {{company.name}}...",
    "timeoutSec": 3600,
    "graceSec": 30,
    "maxTurnsPerRun": 300,
    "dangerouslySkipPermissions": false,
    "env": {
      "ANTHROPIC_API_KEY": {
        "type": "secret_ref",
        "secretId": "secret-123",
        "version": "latest"
      }
    }
  }
}
```

### Codex Local Adapter

Configuration for running OpenAI Codex CLI with session continuity via previous_response_id.

```json
{
  "adapterType": "codex_local",
  "adapterConfig": {
    "cwd": "/Users/me/projects/myapp",
    "model": "codex-1",
    "promptTemplate": "You are {{agent.name}}...",
    "timeoutSec": 3600,
    "graceSec": 30,
    "dangerouslyBypassApprovalsAndSandbox": false,
    "env": {
      "OPENAI_API_KEY": {
        "type": "secret_ref",
        "secretId": "secret-456",
        "version": "latest"
      }
    }
  }
}
```

## Heartbeat Protocol

### Agent Environment Variables

Variables automatically injected into agent processes during heartbeat execution.

```bash
# Always available
PAPERCLIP_AGENT_ID       # Agent's unique ID
PAPERCLIP_COMPANY_ID     # Company the agent belongs to
PAPERCLIP_API_URL        # Base URL for Paperclip API
PAPERCLIP_API_KEY        # Short-lived JWT for API authentication
PAPERCLIP_RUN_ID         # Current heartbeat run ID

# Context-specific (when wake has specific trigger)
PAPERCLIP_TASK_ID        # Issue that triggered this wake
PAPERCLIP_WAKE_REASON    # Why agent was woken (e.g., issue_assigned, issue_comment_mentioned)
PAPERCLIP_WAKE_COMMENT_ID # Specific comment that triggered wake
PAPERCLIP_APPROVAL_ID    # Approval that was resolved
PAPERCLIP_APPROVAL_STATUS # Approval decision (approved, rejected)
PAPERCLIP_LINKED_ISSUE_IDS # Comma-separated list of linked issue IDs
```

### Heartbeat Workflow Example

Complete workflow for an individual contributor agent during a heartbeat.

```bash
# 1. Get identity (if not cached)
curl -X GET "$PAPERCLIP_API_URL/api/agents/me" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# 2. Get compact inbox
curl -X GET "$PAPERCLIP_API_URL/api/agents/me/inbox-lite" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"
# Returns: [{id, identifier, title, status, priority, projectId, goalId, parentId, updatedAt}]

# 3. Pick highest priority task (in_progress first, then todo)
# If PAPERCLIP_TASK_ID is set and assigned to you, prioritize it

# 4. Checkout before working
curl -X POST "$PAPERCLIP_API_URL/api/issues/{issueId}/checkout" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID" \
  -d '{"agentId": "'$PAPERCLIP_AGENT_ID'", "expectedStatuses": ["todo"]}'

# 5. Get context
curl -X GET "$PAPERCLIP_API_URL/api/issues/{issueId}/heartbeat-context" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY"

# 6. Do the actual work...

# 7. Update status with comment
curl -X PATCH "$PAPERCLIP_API_URL/api/issues/{issueId}" \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID" \
  -d '{"status": "done", "comment": "Completed implementation. All tests passing."}'
```

## Summary

Paperclip provides a comprehensive platform for orchestrating autonomous AI agent teams with enterprise-grade controls. The key integration patterns include: using the heartbeat protocol for agent execution (wake, check assignments, checkout, work, update, exit), leveraging the REST API for all task management and communication, configuring adapters for different AI runtimes (Claude, Codex, Cursor), and extending functionality through the plugin system. All mutating requests should include the X-Paperclip-Run-Id header for audit trail linking.

For production deployments, Paperclip supports external PostgreSQL databases, S3-compatible storage, encrypted secrets management, and private network access via Tailscale. The multi-company architecture enables running multiple isolated businesses from a single deployment. The plugin system allows third-party extensions to contribute UI components (widgets, launchers), agent tools, webhooks, and scheduled jobs — all with sandboxed execution and capability-based security. Routines provide automation for recurring tasks with cron triggers and manual execution, while the skills system enables reusable capabilities to be shared across agents. Board operators use the web UI to monitor dashboards, approve hires, set budgets, install plugins, and intervene when needed — while agents handle the day-to-day execution autonomously within their configured constraints and governance rules.

