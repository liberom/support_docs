# Pi Monorepo

Pi is a monorepo containing a unified LLM API library (@mariozechner/pi-ai), an agent framework (@mariozechner/pi-agent-core), and a full-featured AI coding agent (@mariozechner/pi-coding-agent). The pi-ai library provides a provider-agnostic interface for streaming completions, tool calling, and reasoning across 20+ LLM providers including OpenAI, Anthropic, Google, Mistral, and many OpenAI-compatible endpoints. It handles automatic model discovery, token/cost tracking, context serialization, and seamless cross-provider handoffs mid-conversation.

The coding agent builds on this foundation to provide a complete SDK for embedding AI coding capabilities into applications. It includes built-in tools for file operations (read, write, edit), command execution (bash), and code search (grep, find). The extensible architecture supports custom tools, event hooks, permission gates, and full TUI components. Sessions persist as JSONL files with tree-based branching, enabling fork/restore workflows. The SDK can be used programmatically for custom integrations or via the CLI for interactive terminal-based coding assistance.

## Pi AI Library - Streaming LLM Completions

The pi-ai library provides unified streaming and non-streaming completion APIs across all supported providers. It uses TypeBox schemas for type-safe tool definitions with automatic validation.

```typescript
import { Type, getModel, stream, complete, Context, Tool, StringEnum } from '@mariozechner/pi-ai';

// Get a model with full type safety and auto-complete
const model = getModel('anthropic', 'claude-sonnet-4-20250514');

// Define tools with TypeBox schemas
const tools: Tool[] = [{
  name: 'get_weather',
  description: 'Get current weather for a location',
  parameters: Type.Object({
    location: Type.String({ description: 'City name or coordinates' }),
    units: StringEnum(['celsius', 'fahrenheit'], { default: 'celsius' })
  })
}];

// Build conversation context
const context: Context = {
  systemPrompt: 'You are a helpful assistant.',
  messages: [{ role: 'user', content: 'What is the weather in Tokyo?' }],
  tools
};

// Stream with full event handling
const s = stream(model, context);
for await (const event of s) {
  switch (event.type) {
    case 'text_delta':
      process.stdout.write(event.delta);
      break;
    case 'toolcall_end':
      console.log(`Tool: ${event.toolCall.name}(${JSON.stringify(event.toolCall.arguments)})`);
      // Execute tool and add result to context
      context.messages.push({
        role: 'toolResult',
        toolCallId: event.toolCall.id,
        toolName: event.toolCall.name,
        content: [{ type: 'text', text: JSON.stringify({ temp: 22, condition: 'sunny' }) }],
        isError: false,
        timestamp: Date.now()
      });
      break;
    case 'done':
      console.log(`\nFinished: ${event.reason}`);
      break;
  }
}

// Get final message with usage stats
const message = await s.result();
console.log(`Tokens: ${message.usage.input} in, ${message.usage.output} out`);
console.log(`Cost: $${message.usage.cost.total.toFixed(4)}`);

// Or use non-streaming complete()
const response = await complete(model, context);
```

## Pi AI Library - Thinking/Reasoning Support

Models with reasoning capabilities can show their internal thought process. The library provides both unified and provider-specific interfaces for controlling thinking behavior.

```typescript
import { getModel, streamSimple, completeSimple } from '@mariozechner/pi-ai';

// Many models support reasoning
const model = getModel('anthropic', 'claude-sonnet-4-20250514');
// or getModel('openai', 'gpt-5-mini');
// or getModel('google', 'gemini-2.5-flash');

// Check if model supports reasoning
if (model.reasoning) {
  console.log('Model supports thinking/reasoning');
}

// Use unified reasoning option
const response = await completeSimple(model, {
  messages: [{ role: 'user', content: 'Solve: 2x + 5 = 13' }]
}, {
  reasoning: 'medium'  // 'minimal' | 'low' | 'medium' | 'high' | 'xhigh'
});

// Access thinking and response blocks
for (const block of response.content) {
  if (block.type === 'thinking') {
    console.log('Thinking:', block.thinking);
  } else if (block.type === 'text') {
    console.log('Response:', block.text);
  }
}

// Stream thinking content in real-time
const s = streamSimple(model, {
  messages: [{ role: 'user', content: 'Explain quantum entanglement' }]
}, { reasoning: 'high' });

for await (const event of s) {
  if (event.type === 'thinking_delta') {
    process.stdout.write(event.delta);  // Stream thinking
  } else if (event.type === 'text_delta') {
    process.stdout.write(event.delta);  // Stream response
  }
}
```

## Pi AI Library - Provider and Model Management

Query available providers and models, create custom models for local inference servers, and configure provider-specific options.

```typescript
import { getProviders, getModels, getModel, Model, stream } from '@mariozechner/pi-ai';

// Get all available providers
const providers = getProviders();
console.log(providers); // ['openai', 'anthropic', 'google', 'xai', 'groq', ...]

// Get all models from a provider
const models = getModels('anthropic');
for (const model of models) {
  console.log(`${model.id}: ${model.name}`);
  console.log(`  Context: ${model.contextWindow} tokens`);
  console.log(`  Vision: ${model.input.includes('image')}`);
  console.log(`  Reasoning: ${model.reasoning}`);
}

// Create custom model for Ollama (OpenAI-compatible)
const ollamaModel: Model<'openai-completions'> = {
  id: 'llama-3.1-8b',
  name: 'Llama 3.1 8B (Ollama)',
  api: 'openai-completions',
  provider: 'ollama',
  baseUrl: 'http://localhost:11434/v1',
  reasoning: false,
  input: ['text'],
  cost: { input: 0, output: 0, cacheRead: 0, cacheWrite: 0 },
  contextWindow: 128000,
  maxTokens: 32000
};

// Use custom model
const response = await stream(ollamaModel, context, { apiKey: 'dummy' });

// Custom model with compatibility settings
const litellmModel: Model<'openai-completions'> = {
  id: 'gpt-4o',
  name: 'GPT-4o (via LiteLLM)',
  api: 'openai-completions',
  provider: 'litellm',
  baseUrl: 'http://localhost:4000/v1',
  reasoning: false,
  input: ['text', 'image'],
  cost: { input: 2.5, output: 10, cacheRead: 0, cacheWrite: 0 },
  contextWindow: 128000,
  maxTokens: 16384,
  compat: {
    supportsStore: false,           // LiteLLM doesn't support store field
    supportsDeveloperRole: false,   // Use 'system' instead of 'developer'
    supportsReasoningEffort: false, // No reasoning_effort support
  }
};
```

## Pi AI Library - Image Input and Vision

Process images with vision-capable models by including base64-encoded images in user messages.

```typescript
import { readFileSync } from 'fs';
import { getModel, complete } from '@mariozechner/pi-ai';

const model = getModel('openai', 'gpt-4o-mini');

// Check if model supports images
if (model.input.includes('image')) {
  console.log('Model supports vision');
}

// Read and encode image
const imageBuffer = readFileSync('screenshot.png');
const base64Image = imageBuffer.toString('base64');

// Send image with text prompt
const response = await complete(model, {
  messages: [{
    role: 'user',
    content: [
      { type: 'text', text: 'What is shown in this image? Describe any code or UI elements.' },
      { type: 'image', data: base64Image, mimeType: 'image/png' }
    ]
  }]
});

// Access the response
for (const block of response.content) {
  if (block.type === 'text') {
    console.log(block.text);
  }
}

// Images in tool results (for vision models)
context.messages.push({
  role: 'toolResult',
  toolCallId: 'tool_xyz',
  toolName: 'screenshot',
  content: [
    { type: 'text', text: 'Screenshot captured successfully' },
    { type: 'image', data: base64Image, mimeType: 'image/png' }
  ],
  isError: false,
  timestamp: Date.now()
});
```

## Pi AI Library - OAuth Authentication

Several providers require OAuth authentication. The library provides CLI and programmatic login flows with automatic token refresh.

```typescript
import { getModel, complete } from '@mariozechner/pi-ai';
import {
  loginGitHubCopilot,
  loginAntigravity,
  getOAuthApiKey,
  refreshOAuthToken,
} from '@mariozechner/pi-ai/oauth';
import { readFileSync, writeFileSync } from 'fs';

// CLI login (quickest way)
// npx @mariozechner/pi-ai login github-copilot

// Programmatic OAuth login
const credentials = await loginGitHubCopilot({
  onAuth: (url, instructions) => {
    console.log(`Open: ${url}`);
    if (instructions) console.log(instructions);
  },
  onPrompt: async (prompt) => {
    // Get user input for device code
    return await getUserInput(prompt.message);
  },
  onProgress: (message) => console.log(message)
});

// Store credentials (caller's responsibility)
const auth = { 'github-copilot': { type: 'oauth', ...credentials } };
writeFileSync('auth.json', JSON.stringify(auth, null, 2));

// Later: use stored credentials with automatic refresh
const storedAuth = JSON.parse(readFileSync('auth.json', 'utf-8'));
const result = await getOAuthApiKey('github-copilot', storedAuth);

if (!result) throw new Error('Not logged in');

// Save refreshed credentials
storedAuth['github-copilot'] = { type: 'oauth', ...result.newCredentials };
writeFileSync('auth.json', JSON.stringify(storedAuth, null, 2));

// Use the API key
const model = getModel('github-copilot', 'gpt-4o');
const response = await complete(model, {
  messages: [{ role: 'user', content: 'Hello!' }]
}, { apiKey: result.apiKey });
```

## Pi AI Library - Cross-Provider Handoffs

Seamlessly switch between different LLM providers mid-conversation while preserving full context including thinking blocks, tool calls, and results.

```typescript
import { getModel, complete, Context } from '@mariozechner/pi-ai';

const context: Context = { messages: [] };

// Start with Claude
const claude = getModel('anthropic', 'claude-sonnet-4-20250514');
context.messages.push({ role: 'user', content: 'What is 25 * 18?' });

const claudeResponse = await complete(claude, context, { thinkingEnabled: true });
context.messages.push(claudeResponse);
// Claude's thinking blocks are preserved in context

// Switch to GPT-5 - it sees Claude's thinking as <thinking> tagged text
const gpt5 = getModel('openai', 'gpt-5-mini');
context.messages.push({ role: 'user', content: 'Is that calculation correct?' });

const gptResponse = await complete(gpt5, context);
context.messages.push(gptResponse);

// Switch to Gemini
const gemini = getModel('google', 'gemini-2.5-flash');
context.messages.push({ role: 'user', content: 'Summarize this conversation.' });

const geminiResponse = await complete(gemini, context);
console.log(geminiResponse.content);

// Context can be serialized and restored at any time
const serialized = JSON.stringify(context);
// ... later
const restored: Context = JSON.parse(serialized);
```

## Coding Agent SDK - Quick Start

The coding agent SDK provides a high-level interface for creating AI-powered coding sessions with built-in tools, extensions, and session management.

```typescript
import {
  createAgentSession,
  AuthStorage,
  ModelRegistry,
  SessionManager
} from "@mariozechner/pi-coding-agent";

// Set up credential storage and model registry
const authStorage = AuthStorage.create();  // Uses ~/.pi/agent/auth.json
const modelRegistry = new ModelRegistry(authStorage);

// Create a session with defaults
const { session } = await createAgentSession({
  sessionManager: SessionManager.inMemory(),
  authStorage,
  modelRegistry,
});

// Subscribe to streaming events
session.subscribe((event) => {
  switch (event.type) {
    case "message_update":
      if (event.assistantMessageEvent.type === "text_delta") {
        process.stdout.write(event.assistantMessageEvent.delta);
      }
      break;
    case "tool_execution_start":
      console.log(`\nTool: ${event.toolName}`);
      break;
    case "tool_execution_end":
      console.log(`Result: ${event.isError ? "error" : "success"}`);
      break;
    case "agent_end":
      console.log("\nAgent finished");
      break;
  }
});

// Send a prompt
await session.prompt("What files are in the current directory?");

// Access messages
console.log(`Total messages: ${session.messages.length}`);
```

## Coding Agent SDK - Session Management

Control session persistence with in-memory, file-based, or continuation modes. Sessions support tree-based branching for fork/restore workflows.

```typescript
import { createAgentSession, SessionManager } from "@mariozechner/pi-coding-agent";

// In-memory session (no persistence)
const { session: ephemeral } = await createAgentSession({
  sessionManager: SessionManager.inMemory(),
});

// New persistent session (creates new file)
const { session: newSession } = await createAgentSession({
  sessionManager: SessionManager.create(process.cwd()),
});
console.log("Session file:", newSession.sessionFile);

// Continue most recent session (or create new if none)
const { session: continued, modelFallbackMessage } = await createAgentSession({
  sessionManager: SessionManager.continueRecent(process.cwd()),
});
if (modelFallbackMessage) {
  console.log("Note:", modelFallbackMessage);  // Model restore warning
}

// List available sessions
const sessions = await SessionManager.list(process.cwd());
for (const info of sessions) {
  console.log(`${info.id}: "${info.firstMessage.slice(0, 50)}..." (${info.messageCount} messages)`);
}

// Open specific session
if (sessions.length > 0) {
  const { session: opened } = await createAgentSession({
    sessionManager: SessionManager.open(sessions[0].path),
  });
}

// Session tree operations
const sm = SessionManager.open("/path/to/session.jsonl");
const entries = sm.getEntries();        // All entries
const tree = sm.getTree();              // Full tree structure
const path = sm.getPath();              // Path from root to current leaf
sm.branch("entry-id");                  // Move leaf to earlier entry
sm.createBranchedSession("leaf-id");    // Extract path to new file
```

## Coding Agent SDK - Tools Configuration

Use built-in tool sets or configure individual tools. When using a custom cwd, use factory functions to ensure proper path resolution.

```typescript
import {
  createAgentSession,
  SessionManager,
  // Built-in tool sets (use process.cwd())
  codingTools,     // read, bash, edit, write
  readOnlyTools,   // read, grep, find, ls
  // Individual tools
  readTool, bashTool, editTool, writeTool, grepTool, findTool, lsTool,
  // Factory functions (for custom cwd)
  createCodingTools,
  createReadOnlyTools,
  createReadTool,
  createBashTool,
  createGrepTool,
} from "@mariozechner/pi-coding-agent";

// Read-only mode (uses process.cwd())
await createAgentSession({
  tools: readOnlyTools,
  sessionManager: SessionManager.inMemory(),
});

// Custom tool selection
await createAgentSession({
  tools: [readTool, bashTool, grepTool],
  sessionManager: SessionManager.inMemory(),
});

// With custom cwd - MUST use factory functions!
const customCwd = "/path/to/project";
await createAgentSession({
  cwd: customCwd,
  tools: createCodingTools(customCwd),  // Tools resolve paths relative to customCwd
  sessionManager: SessionManager.inMemory(),
});

// Or pick specific tools for custom cwd
await createAgentSession({
  cwd: customCwd,
  tools: [
    createReadTool(customCwd),
    createBashTool(customCwd),
    createGrepTool(customCwd)
  ],
  sessionManager: SessionManager.inMemory(),
});
```

## Coding Agent SDK - API Keys and Auth

Configure API key resolution with runtime overrides, stored credentials, and environment variables.

```typescript
import {
  createAgentSession,
  AuthStorage,
  ModelRegistry,
  SessionManager
} from "@mariozechner/pi-coding-agent";

// Default locations: ~/.pi/agent/auth.json and ~/.pi/agent/models.json
const authStorage = AuthStorage.create();
const modelRegistry = new ModelRegistry(authStorage);

// Runtime API key override (not persisted to disk)
authStorage.setRuntimeApiKey("anthropic", "sk-my-temp-key");

// Custom auth storage location
const customAuthStorage = AuthStorage.create("/my/app/auth.json");
const customModelRegistry = new ModelRegistry(
  customAuthStorage,
  "/my/app/models.json"
);

await createAgentSession({
  sessionManager: SessionManager.inMemory(),
  authStorage: customAuthStorage,
  modelRegistry: customModelRegistry,
});

// Get available models (only those with valid API keys)
const available = await modelRegistry.getAvailable();
console.log("Available models:", available.map(m => `${m.provider}/${m.id}`));

// Find specific model (doesn't check if API key exists)
const model = modelRegistry.find("anthropic", "claude-sonnet-4-20250514");
```

## Coding Agent SDK - Custom System Prompt

Override the system prompt using a ResourceLoader.

```typescript
import {
  createAgentSession,
  DefaultResourceLoader,
  SessionManager
} from "@mariozechner/pi-coding-agent";

const loader = new DefaultResourceLoader({
  systemPromptOverride: () => `You are a helpful coding assistant.

## Guidelines
- Write clean, well-documented code
- Explain your reasoning
- Ask clarifying questions when needed

## Available Tools
You have access to read, write, edit, and bash tools.`,
});
await loader.reload();

const { session } = await createAgentSession({
  resourceLoader: loader,
  sessionManager: SessionManager.inMemory(),
});

await session.prompt("Help me refactor this function");
```

## Extensions - Custom Tool Registration

Extensions can register custom tools that the LLM can call. Tools use TypeBox schemas for type-safe parameters.

```typescript
// ~/.pi/agent/extensions/hello.ts
import { Type } from "@mariozechner/pi-ai";
import type { ExtensionAPI } from "@mariozechner/pi-coding-agent";

export default function (pi: ExtensionAPI) {
  pi.registerTool({
    name: "hello",
    label: "Hello",
    description: "A simple greeting tool",
    // Optional: one-line entry in system prompt's Available tools section
    promptSnippet: "Greet a user by name",
    // Optional: tool-specific guidelines added when tool is active
    promptGuidelines: ["Use this tool when user asks for a greeting"],
    parameters: Type.Object({
      name: Type.String({ description: "Name to greet" }),
    }),

    async execute(toolCallId, params, signal, onUpdate, ctx) {
      // Check for cancellation
      if (signal?.aborted) {
        return { content: [{ type: "text", text: "Cancelled" }] };
      }

      // Stream progress updates
      onUpdate?.({
        content: [{ type: "text", text: "Preparing greeting..." }],
        details: { progress: 50 },
      });

      return {
        content: [{ type: "text", text: `Hello, ${params.name}!` }],
        details: { greeted: params.name },  // For rendering & state
      };
    },
  });
}
```

## Extensions - Event Hooks and Permission Gates

Extensions can subscribe to lifecycle events and block dangerous operations.

```typescript
// ~/.pi/agent/extensions/permission-gate.ts
import type { ExtensionAPI } from "@mariozechner/pi-coding-agent";

export default function (pi: ExtensionAPI) {
  const dangerousPatterns = [
    /\brm\s+(-rf?|--recursive)/i,
    /\bsudo\b/i,
    /\b(chmod|chown)\b.*777/i
  ];

  // Block dangerous bash commands
  pi.on("tool_call", async (event, ctx) => {
    if (event.toolName !== "bash") return;

    const command = event.input.command as string;
    const isDangerous = dangerousPatterns.some(p => p.test(command));

    if (isDangerous) {
      if (!ctx.hasUI) {
        return { block: true, reason: "Dangerous command blocked (no UI)" };
      }

      const choice = await ctx.ui.select(
        `Dangerous command:\n\n  ${command}\n\nAllow?`,
        ["Yes", "No"]
      );

      if (choice !== "Yes") {
        return { block: true, reason: "Blocked by user" };
      }
    }
  });

  // Inject context before each agent turn
  pi.on("before_agent_start", async (event, ctx) => {
    return {
      message: {
        customType: "my-extension",
        content: "Remember to be careful with destructive operations.",
        display: false,  // Don't show in TUI
      },
      systemPrompt: event.systemPrompt + "\n\nAlways confirm before deleting files.",
    };
  });

  // React to session events
  pi.on("session_start", async (_event, ctx) => {
    ctx.ui.notify("Permission gate active", "info");
  });

  pi.on("agent_end", async (event, ctx) => {
    console.log(`Agent finished with ${event.messages.length} new messages`);
  });
}
```

## Extensions - Commands and Shortcuts

Register custom slash commands and keyboard shortcuts.

```typescript
// ~/.pi/agent/extensions/commands.ts
import type { ExtensionAPI, AutocompleteItem } from "@mariozechner/pi-coding-agent";

export default function (pi: ExtensionAPI) {
  // Simple command
  pi.registerCommand("stats", {
    description: "Show session statistics",
    handler: async (args, ctx) => {
      const count = ctx.sessionManager.getEntries().length;
      ctx.ui.notify(`${count} entries in session`, "info");
    }
  });

  // Command with argument auto-completion
  pi.registerCommand("deploy", {
    description: "Deploy to an environment",
    getArgumentCompletions: (prefix: string): AutocompleteItem[] | null => {
      const envs = ["dev", "staging", "prod"];
      const items = envs.map(e => ({ value: e, label: e }));
      const filtered = items.filter(i => i.value.startsWith(prefix));
      return filtered.length > 0 ? filtered : null;
    },
    handler: async (args, ctx) => {
      if (!args) {
        ctx.ui.notify("Usage: /deploy <environment>", "error");
        return;
      }
      ctx.ui.notify(`Deploying to ${args}...`, "info");
      // Deployment logic here
    },
  });

  // Keyboard shortcut
  pi.registerShortcut("ctrl+shift+s", {
    description: "Quick save checkpoint",
    handler: async (ctx) => {
      const leafId = ctx.sessionManager.getLeafId();
      if (leafId) {
        pi.setLabel(leafId, `checkpoint-${Date.now()}`);
        ctx.ui.notify("Checkpoint saved", "success");
      }
    },
  });
}
```

## Extensions - Stateful Tool with Session Persistence

Build tools that maintain state across session restarts by storing state in tool result details.

```typescript
// ~/.pi/agent/extensions/todo.ts
import { StringEnum } from "@mariozechner/pi-ai";
import type { ExtensionAPI, ExtensionContext } from "@mariozechner/pi-coding-agent";
import { Type } from "@sinclair/typebox";

interface Todo { id: number; text: string; done: boolean; }
interface TodoDetails { todos: Todo[]; nextId: number; }

export default function (pi: ExtensionAPI) {
  let todos: Todo[] = [];
  let nextId = 1;

  // Reconstruct state from session entries
  const reconstructState = (ctx: ExtensionContext) => {
    todos = [];
    nextId = 1;

    for (const entry of ctx.sessionManager.getBranch()) {
      if (entry.type !== "message") continue;
      const msg = entry.message;
      if (msg.role !== "toolResult" || msg.toolName !== "todo") continue;

      const details = msg.details as TodoDetails | undefined;
      if (details) {
        todos = details.todos;
        nextId = details.nextId;
      }
    }
  };

  // Reconstruct on session events (start, switch, fork, tree navigation)
  pi.on("session_start", async (_event, ctx) => reconstructState(ctx));
  pi.on("session_switch", async (_event, ctx) => reconstructState(ctx));
  pi.on("session_fork", async (_event, ctx) => reconstructState(ctx));
  pi.on("session_tree", async (_event, ctx) => reconstructState(ctx));

  pi.registerTool({
    name: "todo",
    label: "Todo",
    description: "Manage todos. Actions: list, add (text), toggle (id), clear",
    parameters: Type.Object({
      action: StringEnum(["list", "add", "toggle", "clear"] as const),
      text: Type.Optional(Type.String()),
      id: Type.Optional(Type.Number()),
    }),

    async execute(_toolCallId, params, _signal, _onUpdate, _ctx) {
      switch (params.action) {
        case "add": {
          if (!params.text) throw new Error("text required for add");
          const newTodo = { id: nextId++, text: params.text, done: false };
          todos.push(newTodo);
          return {
            content: [{ type: "text", text: `Added todo #${newTodo.id}` }],
            details: { todos: [...todos], nextId } as TodoDetails,
          };
        }
        case "toggle": {
          const todo = todos.find(t => t.id === params.id);
          if (!todo) throw new Error(`Todo #${params.id} not found`);
          todo.done = !todo.done;
          return {
            content: [{ type: "text", text: `Toggled #${todo.id}` }],
            details: { todos: [...todos], nextId } as TodoDetails,
          };
        }
        case "list":
          return {
            content: [{ type: "text", text: todos.length
              ? todos.map(t => `[${t.done ? "x" : " "}] #${t.id}: ${t.text}`).join("\n")
              : "No todos" }],
            details: { todos: [...todos], nextId } as TodoDetails,
          };
        case "clear":
          todos = [];
          nextId = 1;
          return {
            content: [{ type: "text", text: "Cleared all todos" }],
            details: { todos: [], nextId: 1 } as TodoDetails,
          };
      }
    },
  });
}
```

## Agent Core - Low-Level Agent Loop

The agent-core package provides a lower-level Agent class for direct control over the LLM interaction loop.

```typescript
import { Agent } from "@mariozechner/pi-agent-core";
import { getModel } from "@mariozechner/pi-ai";
import { Type } from "@sinclair/typebox";

const agent = new Agent({
  initialState: {
    systemPrompt: "You are a helpful assistant.",
    model: getModel("anthropic", "claude-sonnet-4-20250514"),
    thinkingLevel: "medium",
    tools: [{
      name: "read_file",
      label: "Read File",
      description: "Read a file's contents",
      parameters: Type.Object({
        path: Type.String({ description: "File path" }),
      }),
      execute: async (toolCallId, params, signal, onUpdate) => {
        const content = await fs.readFile(params.path, "utf-8");
        return {
          content: [{ type: "text", text: content }],
          details: { path: params.path, size: content.length },
        };
      },
    }],
  },

  // Preflight each tool call (can block)
  beforeToolCall: async ({ toolCall, args, context }) => {
    if (toolCall.name === "bash") {
      return { block: true, reason: "bash disabled" };
    }
  },

  // Postprocess each tool result
  afterToolCall: async ({ toolCall, result, isError, context }) => {
    if (!isError) {
      return { details: { ...result.details, audited: true } };
    }
  },
});

// Subscribe to events
agent.subscribe((event) => {
  if (event.type === "message_update" && event.assistantMessageEvent.type === "text_delta") {
    process.stdout.write(event.assistantMessageEvent.delta);
  }
});

// Send prompt
await agent.prompt("Read the package.json file");

// State management
agent.setModel(getModel("openai", "gpt-4o"));
agent.setThinkingLevel("high");
agent.setTools([...newTools]);

// Control
agent.abort();              // Cancel current operation
await agent.waitForIdle();  // Wait for completion

// Steering during tool execution
agent.steer({
  role: "user",
  content: "Stop! Focus on error handling instead.",
  timestamp: Date.now(),
});

// Follow-up after completion
agent.followUp({
  role: "user",
  content: "Now summarize what you found.",
  timestamp: Date.now(),
});
```

## Summary

The Pi monorepo provides a comprehensive stack for building LLM-powered applications. At its foundation, pi-ai delivers a unified API across 20+ providers with features like streaming, tool calling, reasoning support, and seamless cross-provider handoffs. The pi-agent-core package adds stateful agent management with event streaming and tool execution hooks. The pi-coding-agent package combines these into a full-featured SDK with file operations, session persistence, and an extensible architecture for custom tools and permission gates.

Integration patterns range from simple streaming completions to complex multi-provider workflows. For embedded use cases, the SDK's `createAgentSession()` provides all defaults while allowing full customization of tools, models, and behavior through extensions. Extensions can register tools, intercept events, gate permissions, and persist state across sessions. The session tree structure enables sophisticated branching and restoration workflows for iterative coding assistance. Whether building a CLI tool, web service, or custom IDE integration, the modular architecture supports both minimal configurations and advanced customizations.

