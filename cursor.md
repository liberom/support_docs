### Start Cursor Agent (Bash)

Source: https://cursor.com/docs/cli/installation

Initiates the Cursor Agent after it has been installed and its directory has been added to the PATH.

```bash
agent
```

--------------------------------

### Verify Cursor CLI Installation (Bash)

Source: https://cursor.com/docs/cli/installation

Verifies that the Cursor CLI has been installed successfully by checking its version. This command should be run after the initial installation.

```bash
agent --version
```

--------------------------------

### Start Interactive Agent Session

Source: https://cursor.com/docs/cli/index

Demonstrates how to start an interactive conversational session with the AI agent. It also shows how to provide an initial prompt to guide the session.

```bash
# Start interactive session
agent

# Start with initial prompt
agent "refactor the auth module to use JWT tokens"
```

--------------------------------

### Install Cursor CLI (Bash)

Source: https://cursor.com/docs/cli/installation

Installs the Cursor CLI using a curl command piped to bash. This is the primary installation method for macOS, Linux, and Windows (WSL). It fetches and executes the installation script.

```bash
curl https://cursor.com/install -fsS | bash
```

--------------------------------

### Install and Run Cursor CLI

Source: https://cursor.com/docs/cli/index

Provides instructions for installing the Cursor CLI using a curl command and initiating an interactive session.

```bash
# Install
curl https://cursor.com/install -fsS | bash

# Run interactive session
agent
```

--------------------------------

### Example NDJSON Sequence for File Operations

Source: https://cursor.com/docs/cli/reference/output-format

A comprehensive NDJSON sequence demonstrating a typical agent workflow involving reading a file ('README.md') and writing a summary to another file ('summary.txt').

```json
{"type":"system","subtype":"init","apiKeySource":"login","cwd":"/Users/user/project","session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff","model":"Claude 4 Sonnet","permissionMode":"default"}
{"type":"user","message":{"role":"user","content":[{"type":"text","text":"Read README.md and create a summary"}]},"session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff"}
{"type":"assistant","message":{"role":"assistant","content":[{"type":"text","text":"I'll read the README.md file"}]},"session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff"}
{"type":"tool_call","subtype":"started","call_id":"toolu_vrtx_01NnjaR886UcE8whekg2MGJd","tool_call":{"readToolCall":{"args":{"path":"README.md"}}},"session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff"}
{"type":"tool_call","subtype":"completed","call_id":"toolu_vrtx_01NnjaR886UcE8whekg2MGJd","tool_call":{"readToolCall":{"args":{"path":"README.md"},"result":{"success":{"content":"# Project\n\nThis is a sample project...","isEmpty":false,"exceededLimit":false,"totalLines":54,"totalChars":1254}}}},"session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff"}
{"type":"assistant","message":{"role":"assistant","content":[{"type":"text","text":"Based on the README, I'll create a summary"}]},"session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff"}
{"type":"tool_call","subtype":"started","call_id":"toolu_vrtx_01Q3VHVnWFSKygaRPT7WDxrv","tool_call":{"writeToolCall":{"args":{"path":"summary.txt","fileText":"# README Summary\n\nThis project contains...","toolCallId":"toolu_vrtx_01Q3VHVnWFSKygaRPT7WDxrv"}}},"session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff"}
{"type":"tool_call","subtype":"completed","call_id":"toolu_vrtx_01Q3VHVnWFSKygaRPT7WDxrv","tool_call":{"writeToolCall":{"args":{"path":"summary.txt","fileText":"# README Summary\n\nThis project contains...","toolCallId":"toolu_vrtx_01Q3VHVnWFSKygaRPT7WDxrv"},"result":{"success":{"path":"/Users/user/project/summary.txt","linesCreated":19,"fileSize":942}}}},"session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff"}
{"type":"assistant","message":{"role":"assistant","content":[{"type":"text","text":"Done! I've created the summary in summary.txt"}]},"session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff"}
{"type":"result","subtype":"success","duration_ms":5234,"duration_api_ms":5234,"is_error":false,"result":"I'll read the README.md fileBased on the README, I'll create a summaryDone! I've created the summary in summary.txt","session_id":"c6b62c6f-7ead-4fd6-9922-e952131177ff","request_id":"10e11780-df2f-45dc-a1ff-4540af32e9c0"}
```

--------------------------------

### Text Output Format Example

Source: https://cursor.com/docs/cli/reference/output-format

Illustrates the 'text' output format, which exclusively provides the final assistant message, omitting intermediate tool calls and progress updates. This is suitable for scripts needing only the agent's ultimate response.

```text
The command to move this branch onto main is `git rebase --onto main HEAD~3`.
```

--------------------------------

### Minimal Cursor CLI Configuration (JSON)

Source: https://cursor.com/docs/cli/reference/configuration

A basic `cli-config.json` file with essential settings, including version, editor mode, and permission allowances. This serves as a starting point for customizing the CLI.

```json
{
  "version": 1,
  "editor": { "vimMode": false },
  "permissions": { "allow": ["Shell(ls)"], "deny": [] }
}
```

--------------------------------

### Selecting Models with Cursor CLI Slash Commands (Bash)

Source: https://cursor.com/docs/cli/reference/configuration

Examples of using bash commands to select different models within the Cursor CLI using slash commands. This allows users to switch between AI models for different tasks.

```bash
/model auto
/model gpt-5
/model sonnet-4
```

--------------------------------

### Add Cursor CLI to PATH (Zsh)

Source: https://cursor.com/docs/cli/installation

Appends the Cursor CLI's binary directory to the system's PATH environment variable for the zsh shell. This ensures the 'agent' command is accessible globally.

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

--------------------------------

### Add Cursor CLI to PATH (Bash)

Source: https://cursor.com/docs/cli/installation

Appends the Cursor CLI's binary directory to the system's PATH environment variable for the bash shell. This allows the 'agent' command to be run from any directory.

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

--------------------------------

### Enable Vim Mode in Cursor CLI (JSON)

Source: https://cursor.com/docs/cli/reference/configuration

Example of a `cli-config.json` file to enable Vim keybindings within the Cursor CLI. This configuration affects editor behavior.

```json
{
  "version": 1,
  "editor": { "vimMode": true },
  "permissions": { "allow": ["Shell(ls)"], "deny": [] }
}
```

--------------------------------

### Update Cursor CLI (Bash)

Source: https://cursor.com/docs/cli/installation

Manually updates the Cursor CLI to the latest available version. This command can be used for both 'update' and 'upgrade' operations.

```bash
agent update
```

```bash
agent upgrade
```

--------------------------------

### Stream JSON Event Types for Cursor CLI

Source: https://cursor.com/docs/cli/reference/output-format

The 'stream-json' output format uses newline-delimited JSON (NDJSON) to emit events during command execution. This includes system initialization, user messages, assistant messages, and tool call events (started and completed). This format is ideal for real-time processing and monitoring.

```json
{
  "type": "system",
  "subtype": "init",
  "apiKeySource": "env|flag|login",
  "cwd": "/absolute/path",
  "session_id": "<uuid>",
  "model": "<model display name>",
  "permissionMode": "default"
}
```

```json
{
  "type": "user",
  "message": {
    "role": "user",
    "content": [{ "type": "text", "text": "<prompt>" }]
  },
  "session_id": "<uuid>"
}
```

```json
{
  "type": "assistant",
  "message": {
    "role": "assistant",
    "content": [{ "type": "text", "text": "<complete message text>" }]
  },
  "session_id": "<uuid>"
}
```

```json
{
  "type": "tool_call",
  "subtype": "started",
  "call_id": "<string id>",
  "tool_call": {
    "readToolCall": {
      "args": { "path": "file.txt" }
    }
  },
  "session_id": "<uuid>"
}
```

```json
{
  "type": "tool_call",
  "subtype": "completed",
  "call_id": "<string id>",
  "tool_call": {
    "readToolCall": {
      "args": { "path": "file.txt" },
      "result": {
        "success": {
          "content": "file contents...",
          "isEmpty": false,
          "exceededLimit": false,
          "totalLines": 54,
          "totalChars": 1254
        }
      }
    }
  },
  "session_id": "<uuid>"
}
```

--------------------------------

### Using MCP Tools with Agent (Bash)

Source: https://cursor.com/docs/cli/mcp

Demonstrates how to leverage MCP tools through the Cursor CLI agent. It includes checking available servers, inspecting server tools, and running agent commands that automatically utilize MCP functionalities.

```bash
# Check what MCP servers are available
agent mcp list

# See what tools a specific server provides
agent mcp list-tools playwright

# Use agent - it automatically uses MCP tools when helpful
agent -p "Navigate to google.com and take a screenshot of the search page"
```

--------------------------------

### List Configured MCP Servers (Bash)

Source: https://cursor.com/docs/cli/mcp

Displays all configured MCP servers and their connection status. It shows server names, identifiers, status, configuration source, and transport method.

```bash
agent mcp list
```

--------------------------------

### List Available Tools from MCP Server (Bash)

Source: https://cursor.com/docs/cli/mcp

Retrieves a list of tools provided by a specific MCP server, including their names, descriptions, and parameter requirements. This helps in understanding the capabilities of an MCP server.

```bash
agent mcp list-tools <identifier>
```

--------------------------------

### Login to MCP Server (Bash)

Source: https://cursor.com/docs/cli/mcp

Authenticates with a specified MCP server that is configured in your mcp.json file. This command is necessary to establish a connection and utilize the server's features.

```bash
agent mcp login <identifier>
```

--------------------------------

### Enable MCP Server (Bash)

Source: https://cursor.com/docs/cli/mcp

Activates a specified MCP server, making its tools available for use with the agent. This command can also be executed as a slash command in interactive mode.

```bash
agent mcp enable <identifier>
```

--------------------------------

### Manage Cursor CLI Sessions

Source: https://cursor.com/docs/cli/index

Explains how to manage past conversations or sessions with the AI agent. This includes listing all previous chats, resuming the latest conversation, or resuming a specific conversation using its chat ID.

```bash
# List all previous chats
agent ls

# Resume latest conversation
agent resume

# Resume specific conversation
agent --resume="chat-id-here"
```

--------------------------------

### File Read Tool Call Arguments (JSON)

Source: https://cursor.com/docs/cli/reference/output-format

Demonstrates the JSON structure for arguments when initiating a file read operation using the readToolCall. The 'path' field specifies the file to be read.

```json
{
  "path": "file.txt"
}
```

--------------------------------

### File Write Tool Call Arguments (JSON)

Source: https://cursor.com/docs/cli/reference/output-format

Illustrates the JSON structure for arguments when initiating a file write operation using the writeToolCall. It includes the file path, content, and a unique tool call ID.

```json
{
  "path": "file.txt",
  "fileText": "content...",
  "toolCallId": "id"
}
```

--------------------------------

### Configure Permissions in Cursor CLI (JSON)

Source: https://cursor.com/docs/cli/reference/configuration

Demonstrates how to configure specific permissions (allow and deny lists) for operations within the Cursor CLI using `cli-config.json`. This is crucial for security and controlling CLI actions.

```json
{
  "version": 1,
  "editor": { "vimMode": false },
  "permissions": {
    "allow": ["Shell(ls)", "Shell(echo)"],
    "deny": ["Shell(rm)"]
  }
}
```

--------------------------------

### Configure Cursor CLI Permissions (JSON)

Source: https://cursor.com/docs/cli/reference/permissions

This JSON configuration demonstrates how to set 'allow' and 'deny' rules for shell commands and file read/write operations within the Cursor CLI. Permissions are managed in CLI configuration files.

```json
{
  "permissions": {
    "allow": [
      "Shell(ls)",
      "Shell(git)",
      "Read(src/**/*.ts)",
      "Write(package.json)"
    ],
    "deny": ["Shell(rm)", "Read(.env*)", "Write(**/*.key)"]
  }
}
```

--------------------------------

### Generic Function Tool Call Structure (JSON)

Source: https://cursor.com/docs/cli/reference/output-format

Represents a flexible structure for calling various tools using the 'tool_call.function'. It includes the tool's name and its arguments in a string format.

```json
{
  "name": "tool_name",
  "arguments": "..."
}
```

--------------------------------

### Run Cursor CLI in Non-Interactive Mode

Source: https://cursor.com/docs/cli/index

Illustrates how to use the Cursor CLI in a non-interactive mode for scripts and automation. This includes specifying a prompt, model, and output format, as well as integrating with git changes.

```bash
# Run with specific prompt and model
agent -p "find and fix performance issues" --model "gpt-5"

# Use with git changes included for review
agent -p "review these changes for security issues" --output-format text
```

--------------------------------

### Successful File Write Tool Call Result (JSON)

Source: https://cursor.com/docs/cli/reference/output-format

Shows the JSON structure for a successful completion of a file write operation. It includes the absolute path of the created file, the number of lines written, and the total file size.

```json
{
  "path": "/absolute/path",
  "linesCreated": 19,
  "fileSize": 942
}
```

--------------------------------

### Check Authentication Status in Cursor CLI

Source: https://cursor.com/docs/cli/reference/authentication

Verify the current authentication status, account information, and endpoint configuration for the Cursor CLI.

```bash
agent status
```

--------------------------------

### API Key Authentication for Cursor CLI (Environment Variable)

Source: https://cursor.com/docs/cli/reference/authentication

Authenticate the Cursor CLI using an API key set as an environment variable. This is recommended for automation and CI/CD environments.

```bash
export CURSOR_API_KEY=your_api_key_here
agent "implement user authentication"
```

--------------------------------

### API Key Authentication for Cursor CLI (Command Line Flag)

Source: https://cursor.com/docs/cli/reference/authentication

Authenticate the Cursor CLI using an API key provided as a command-line flag. Useful for specific command executions.

```bash
agent --api-key your_api_key_here "implement user authentication"
```

--------------------------------

### Troubleshooting Cursor CLI Config Errors (Bash)

Source: https://cursor.com/docs/cli/reference/configuration

A bash command to resolve Cursor CLI configuration errors by temporarily moving the problematic `cli-config.json` file. This helps in debugging by isolating the configuration issue.

```bash
mv ~/.cursor/cli-config.json ~/.cursor/cli-config.json.bad
```

--------------------------------

### Browser Authentication for Cursor CLI

Source: https://cursor.com/docs/cli/reference/authentication

Perform browser-based login, check authentication status, and log out of the Cursor CLI. This method is recommended for interactive use.

```bash
agent login
agent status
agent logout
```

--------------------------------

### Successful Terminal Result Event (JSON)

Source: https://cursor.com/docs/cli/reference/output-format

The final event emitted upon successful completion of an agent's task. It contains details like session ID, request ID, duration, and the full assistant text result.

```json
{
  "type": "result",
  "subtype": "success",
  "duration_ms": 1234,
  "duration_api_ms": 1234,
  "is_error": false,
  "result": "<full assistant text>",
  "session_id": "<uuid>",
  "request_id": "<optional request id>"
}
```

--------------------------------

### JSON Output Format for Cursor CLI

Source: https://cursor.com/docs/cli/reference/output-format

The 'json' output format emits a single JSON object for successful command completion. It aggregates text and tool events into a final result. On failure, an error message is sent to stderr without a JSON object. This format is suitable for programmatic parsing.

```json
{
  "type": "result",
  "subtype": "success",
  "is_error": false,
  "duration_ms": 1234,
  "duration_api_ms": 1234,
  "result": "<full assistant text>",
  "session_id": "<uuid>",
  "request_id": "<optional request id>"
}
```

--------------------------------

### Disable MCP Server (Bash)

Source: https://cursor.com/docs/cli/mcp

Deactivates a specified MCP server, removing its tools from the agent's available functions. This command mirrors the functionality of the /mcp disable slash command.

```bash
agent mcp disable <identifier>
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.