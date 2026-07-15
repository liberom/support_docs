### Install OpenCode using curl

Source: https://opencode.ai/docs/index

Installs OpenCode using a curl command to download and execute the install script. This is a quick way to get started.

```bash
curl -fsSL https://opencode.ai/install | bash
```

--------------------------------

### OpenCode JSONC Configuration Example

Source: https://opencode.ai/docs/config

An example of an OpenCode configuration file in JSONC format, which supports comments. This file defines settings like the schema, theme, model, and autoupdate behavior.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  // Theme configuration
  "theme": "opencode",
  "model": "anthropic/claude-sonnet-4-5",
  "autoupdate": true
}
```

--------------------------------

### Install OpenCode CLI

Source: https://opencode.ai/docs/github

Command to install OpenCode in a GitHub repository. This command initiates an interactive setup process for the GitHub app, workflow, and secrets.

```bash
opencode github install
```

--------------------------------

### Access Windows files from WSL

Source: https://opencode.ai/docs/windows-wsl

Demonstrates how to navigate to Windows directories from within the WSL terminal. Windows drives are mounted under the `/mnt/` directory, allowing seamless file access.

```bash
cd /mnt/c/Users/YourName/project
opencode
```

--------------------------------

### Run OpenCode web client in WSL

Source: https://opencode.ai/docs/windows-wsl

Launches the OpenCode web client from within the WSL terminal, making it accessible via a browser on your Windows machine. Binding to `0.0.0.0` allows connections from your Windows host.

```bash
opencode web --hostname 0.0.0.0
```

--------------------------------

### Install OpenCode AI SDK

Source: https://opencode.ai/docs/sdk

Install the OpenCode AI SDK package using npm. This is the first step to integrating the SDK into your project.

```bash
npm install @opencode-ai/sdk
```

--------------------------------

### Install Clipboard Utilities for Linux (Wayland)

Source: https://opencode.ai/docs/troubleshooting

Installs the `wl-clipboard` utility required for copy/paste functionality in OpenCode on Linux systems utilizing the Wayland display server. This ensures seamless integration with the Wayland clipboard protocols.

```bash
apt install -y wl-clipboard
```

--------------------------------

### Run OpenCode server in WSL for Desktop App Connection

Source: https://opencode.ai/docs/windows-wsl

Starts the OpenCode server within WSL, configured to listen on all network interfaces (`0.0.0.0`) and a specified port. This allows the OpenCode Desktop app on Windows to connect to the WSL-based server.

```bash
opencode serve --hostname 0.0.0.0 --port 4096
```

--------------------------------

### Install OpenCode using Bun

Source: https://opencode.ai/docs/index

Installs the opencode-ai package globally using Bun. This method requires Bun to be installed.

```bash
bun install -g opencode-ai
```

--------------------------------

### Install OpenCode using Mise

Source: https://opencode.ai/docs/index

Installs OpenCode using Mise, a polyglot version manager. This command fetches the latest version from the specified GitHub repository.

```bash
mise use -g github:anomalyco/opencode
```

--------------------------------

### Setup Virtual Framebuffer for Headless Linux

Source: https://opencode.ai/docs/troubleshooting

Configures a virtual display buffer (`Xvfb`) for running OpenCode in headless Linux environments where a physical display is not available. This setup is necessary for enabling copy/paste functionality in such scenarios by simulating a graphical environment.

```bash
apt install -y xvfb
# and run:
Xvfb :99 -screen 0 1024x768x24 > /dev/null 2>&1 &
export DISPLAY=:99.0
```

--------------------------------

### Setting Custom OpenCode Configuration Path

Source: https://opencode.ai/docs/config

Example of setting a custom configuration file path for OpenCode using the OPENCODE_CONFIG environment variable. This allows overriding the default configuration loading mechanism.

```bash
export OPENCODE_CONFIG=/path/to/my/custom-config.json
opencode run "Hello world"
```

--------------------------------

### Configure Model Instructions

Source: https://opencode.ai/docs/config

Specify instruction files for the model using paths and glob patterns. These files guide the model's behavior and responses.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["CONTRIBUTING.md", "docs/guidelines.md", ".cursor/rules/*.md"]
}
```

--------------------------------

### Start OpenCode Web Server (Bash)

Source: https://opencode.ai/docs/cli

Starts a headless OpenCode server with a web interface. It opens a web browser to access the interface. Optionally, set OPENCODE_SERVER_PASSWORD for basic authentication.

```bash
opencode web
```

--------------------------------

### Manage Projects with JavaScript

Source: https://opencode.ai/docs/sdk

Provides examples for interacting with project-related APIs: `project.list()` to retrieve all projects and `project.current()` to get the currently active project. Both methods return arrays or single objects conforming to the Project type.

```javascript
// List all projects
const projects = await client.project.list()

// Get current project
const currentProject = await client.project.current()
```

--------------------------------

### Install OpenCode using npm

Source: https://opencode.ai/docs/index

Installs the opencode-ai package globally using npm. This method requires Node.js and npm to be installed.

```bash
npm install -g opencode-ai
```

--------------------------------

### Prompt Example for Local MCP Server

Source: https://opencode.ai/docs/mcp-servers

Demonstrates how to invoke a configured local MCP server, `mcp_everything`, within a prompt. This shows the practical application of adding and enabling MCP tools for LLM interaction.

```txt
use the mcp_everything tool to add the number 3 and 4
```

--------------------------------

### Define Custom Commands in OpenCode

Source: https://opencode.ai/docs/config

Configures custom commands for repetitive tasks using the 'command' option in opencode.jsonc. This example defines 'test' and 'component' commands with templates and descriptions.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "command": {
    "test": {
      "template": "Run the full test suite with coverage report and show any failures.\nFocus on the failing tests and suggest fixes.",
      "description": "Run tests with coverage",
      "agent": "build",
      "model": "anthropic/claude-haiku-4-5"
    },
    "component": {
      "template": "Create a new React component named $ARGUMENTS with TypeScript support.\nInclude proper typing and basic structure.",
      "description": "Create a new component"
    }
  }
}
```

--------------------------------

### Install OpenCode using Yarn

Source: https://opencode.ai/docs/index

Installs the opencode-ai package globally using Yarn. This method requires Yarn to be installed.

```bash
yarn global add opencode-ai
```

--------------------------------

### Secure OpenCode server with a password in WSL

Source: https://opencode.ai/docs/windows-wsl

Starts the OpenCode server with network access enabled and sets an environment variable for password protection. This is crucial for securing the server when accessible from outside the WSL environment.

```bash
OPENCODE_SERVER_PASSWORD=your-password opencode serve --hostname 0.0.0.0
```

--------------------------------

### Connect to OpenCode Zen Provider via Command Line

Source: https://opencode.ai/docs/providers

This example illustrates the command-line steps within the OpenCode TUI to connect to the OpenCode Zen provider. It includes running the '/connect' command, selecting 'opencode', and then using '/models' to view recommended models.

```bash
/connect
```

```bash
/models
```

--------------------------------

### Configure Code Formatters in OpenCode

Source: https://opencode.ai/docs/config

Sets up code formatters using the 'formatter' option in opencode.json. This example disables 'prettier' and configures a 'custom-prettier' with specific commands and extensions.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "formatter": {
    "prettier": {
      "disabled": true
    },
    "custom-prettier": {
      "command": ["npx", "prettier", "--write", "$FILE"],
      "environment": {
        "NODE_ENV": "development"
      },
      "extensions": [".js", ".ts", ".jsx", ".tsx"]
    }
  }
}
```

--------------------------------

### Install OpenCode using Scoop

Source: https://opencode.ai/docs/index

Installs OpenCode on Windows using the Scoop package manager. This requires Scoop to be installed.

```powershell
scoop install opencode
```

--------------------------------

### Install Clipboard Utilities for Linux (X11)

Source: https://opencode.ai/docs/troubleshooting

Installs necessary clipboard utilities for OpenCode's copy/paste functionality on Linux systems using the X11 display server. Users can choose between `xclip` or `xsel`. These tools enable the application to interact with the system clipboard.

```bash
apt install -y xclip
# or
apt install -y xsel
```

--------------------------------

### Skill File Structure and Example

Source: https://opencode.ai/docs/skills

Defines the expected directory structure for agent skills and provides an example of a `SKILL.md` file, including YAML frontmatter and markdown content.

```markdown
---
name: git-release
description: Create consistent releases and changelogs
license: MIT
compatibility: opencode
metadata:
  audience: maintainers
  workflow: github
---

## What I do

- Draft release notes from merged PRs
- Propose a version bump
- Provide a copy-pasteable `gh release create` command

## When to use me

Use this when you are preparing a tagged release. Ask clarifying questions if the target versioning scheme is unclear.

```

--------------------------------

### Install OpenCode on Arch Linux

Source: https://opencode.ai/docs/index

Installs OpenCode on Arch Linux using pacman for the stable version or paru for the latest from AUR.

```bash
sudo pacman -S opencode           # Arch Linux (Stable)
```

```bash
paru -S opencode-bin              # Arch Linux (Latest from AUR)
```

--------------------------------

### Install OpenCode using pnpm

Source: https://opencode.ai/docs/index

Installs the opencode-ai package globally using pnpm. This method requires pnpm to be installed.

```bash
pnpm install -g opencode-ai
```

--------------------------------

### Set Authentication Credentials with OpenCode AI API (JavaScript)

Source: https://opencode.ai/docs/de/sdk

Demonstrates how to set authentication credentials for different providers using the OpenCode AI client. This example shows setting an API key for Anthropic.

```javascript
await client.auth.set({
  path: { id: "anthropic" },
  body: { type: "api", key: "your-api-key" },
})
```

--------------------------------

### Create Opencode Client Instance

Source: https://opencode.ai/docs/sdk

Create a new instance of the OpenCode client, which also starts a server. This method can be configured with various options like hostname, port, and timeout. It returns an object containing the client and server instances.

```javascript
import { createOpencode } from "@opencode-ai/sdk"

const { client } = await createOpencode()
```

--------------------------------

### Start OpenCode TUI

Source: https://opencode.ai/docs/de/tui

Launches the OpenCode interactive terminal interface. It can be started in the current directory or for a specific project directory.

```bash
opencode
opencode /path/to/project
```

--------------------------------

### Setting Custom OpenCode Configuration Directory

Source: https://opencode.ai/docs/config

Example of specifying a custom directory for OpenCode configuration files using the OPENCODE_CONFIG_DIR environment variable. This custom directory can contain agents, commands, modes, and plugins.

```bash
export OPENCODE_CONFIG_DIR=/path/to/my/config-directory
opencode run "Hello world"
```

--------------------------------

### Set Tool Permissions in OpenCode

Source: https://opencode.ai/docs/config

Configures user approval requirements for specific tools using the 'permission' option in opencode.json. This example requires user approval for 'edit' and 'bash' tools.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "edit": "ask",
    "bash": "ask"
  }
}
```

--------------------------------

### OpenCode Configuration Example (JSON)

Source: https://opencode.ai/docs/enterprise

An example JSON configuration file for OpenCode, specifying schema and sharing settings. The 'share' property is set to 'disabled' by default.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "share": "disabled"
}
```

--------------------------------

### Subscribe to Real-time Events with OpenCode AI API (JavaScript)

Source: https://opencode.ai/docs/de/sdk

Provides an example of how to subscribe to server-sent events using the OpenCode AI client. It shows how to iterate over the event stream and log event details.

```javascript
// Listen to real-time events
const events = await client.event.subscribe()
for await (const event of events.stream) {
  console.log("Event:", event.type, event.properties)
}
```

--------------------------------

### Install OpenCode using Chocolatey

Source: https://opencode.ai/docs/index

Installs OpenCode on Windows using the Chocolatey package manager. This requires Chocolatey to be installed.

```powershell
choco install opencode
```

--------------------------------

### Configure Opencode Client with Options

Source: https://opencode.ai/docs/sdk

Instantiate the OpenCode client with custom configuration options. This allows overriding default settings such as hostname, port, and specifying a particular model. The example demonstrates setting a model and logging the server URL before closing the server.

```javascript
import { createOpencode } from "@opencode-ai/sdk"

const opencode = await createOpencode({
  hostname: "127.0.0.1",
  port: 4096,
  config: {
    model: "anthropic/claude-3-5-sonnet-20241022",
  },
})

console.log(`Server running at ${opencode.server.url}`)

opencode.server.close()
```

--------------------------------

### Skill Tool Description Example

Source: https://opencode.ai/docs/skills

Illustrates how OpenCode represents available skills in its tool description, including the skill name and a brief description.

```xml
<available_skills>
  <skill>
    <name>git-release</name>
    <description>Create consistent releases and changelogs</description>
  </skill>
</available_skills>

```

--------------------------------

### Ask OpenCode a Question

Source: https://opencode.ai/docs/index

Example of asking OpenCode to explain a specific part of the codebase. The '@' symbol can be used for fuzzy file searching.

```text
How is authentication handled in @packages/functions/src/api/index.ts
```

--------------------------------

### Configure Specialized Agents in OpenCode

Source: https://opencode.ai/docs/config

Defines specialized agents for specific tasks using the 'agent' option in opencode.jsonc. This example configures a 'code-reviewer' agent with a specific model, prompt, and disables file modification tools.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "code-reviewer": {
      "description": "Reviews code for best practices and potential issues",
      "model": "anthropic/claude-sonnet-4-5",
      "prompt": "You are a code reviewer. Focus on security, performance, and maintainability.",
      "tools": {
        "write": false,
        "edit": false
      }
    }
  }
}
```

--------------------------------

### Setting Environment Variables for LSP Servers (Rust Example)

Source: https://opencode.ai/docs/lsp

This JSON configuration demonstrates how to set environment variables for a specific LSP server, in this case, 'rust'. The `env` property within the server's configuration allows you to pass key-value pairs that will be available as environment variables when the LSP server starts. This is useful for configuring logging levels or other server-specific settings.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "lsp": {
    "rust": {
      "env": {
        "RUST_LOG": "debug"
      }
    }
  }
}
```

--------------------------------

### Connect to 302.AI Provider via Command Line

Source: https://opencode.ai/docs/providers

This example shows the command-line interaction for connecting to the 302.AI provider within the OpenCode TUI. It involves running the '/connect' command and entering the API key when prompted.

```bash
/connect
```

```bash
┌ API key
│
│
└ enter
```

```bash
/models
```

--------------------------------

### Install OpenCode using Homebrew

Source: https://opencode.ai/docs/index

Installs OpenCode using the Homebrew package manager on macOS and Linux. It's recommended to use the 'anomalyco/tap/opencode' for the latest releases.

```bash
brew install anomalyco/tap/opencode
```

--------------------------------

### Example AGENTS.md for Monorepo Project

Source: https://opencode.ai/docs/rules

This markdown file provides an example structure and content for an AGENTS.md file, detailing project type, structure, code standards, and monorepo conventions. It serves as a template for customizing OpenCode's behavior for a specific project.

```markdown
# SST v3 Monorepo Project

This is an SST v3 monorepo with TypeScript. The project uses bun workspaces for package management.

## Project Structure

- `packages/` - Contains all workspace packages (functions, core, web, etc.)
- `infra/` - Infrastructure definitions split by service (storage.ts, api.ts, web.ts)
- `sst.config.ts` - Main SST configuration with dynamic imports

## Code Standards

- Use TypeScript with strict mode enabled
- Shared code goes in `packages/core/` with proper exports configuration
- Functions go in `packages/functions/`
- Infrastructure should be split into logical files in `infra/`

## Monorepo Conventions

- Import shared modules using workspace names: `@my-app/core/example`
```

--------------------------------

### Configure Server Settings in opencode.json

Source: https://opencode.ai/docs/config

This snippet demonstrates how to configure server settings for OpenCode commands like `opencode serve` and `opencode web`. It covers port, hostname, mDNS, and CORS settings.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "server": {
    "port": 4096,
    "hostname": "0.0.0.0",
    "mdns": true,
    "mdnsDomain": "myproject.local",
    "cors": ["http://localhost:5173"]
  }
}
```

--------------------------------

### Install and Configure Helicone Session Plugin for OpenCode

Source: https://opencode.ai/docs/providers

This section shows how to install the `opencode-helicone-session` npm package and configure OpenCode to use it. This plugin automatically logs OpenCode conversations as sessions in Helicone by injecting specific headers.

```bash
npm install -g opencode-helicone-session
```

```json
{
  "plugin": ["opencode-helicone-session"]
}
```

--------------------------------

### Configure MCP Server Globally (JSON)

Source: https://opencode.ai/docs/mcp-servers

This JSON configuration shows a basic setup for enabling or disabling MCP servers globally. It includes an example of a local MCP server and how to toggle its tool availability.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-mcp-foo": {
      "type": "local",
      "command": ["bun", "x", "my-mcp-command-foo"]
    },
    "my-mcp-bar": {
      "type": "local",
      "command": ["bun", "x", "my-mcp-command-bar"]
    }
  },
  "tools": {
    "my-mcp-foo": false
  }
}
```

--------------------------------

### Configure Experimental Options

Source: https://opencode.ai/docs/config

Configure experimental options that are under active development. Be aware that these options are not stable and may change or be removed without notice.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "experimental": {}
}
```

--------------------------------

### GET /session

Source: https://opencode.ai/docs/server

Retrieves a list of all sessions.  This endpoint provides a way to fetch all available sessions.

```APIDOC
## GET /session

### Description
Lists all sessions.

### Method
GET

### Endpoint
/session

### Parameters
No parameters.

### Request Example
No request body.

### Response
#### Success Response (200)
- **Session[]** - An array of Session objects.

#### Response Example
[
  {
    "id": "session1",
    "title": "Session Title",
    // ... other session properties
  }
]

```

--------------------------------

### Config API

Source: https://opencode.ai/docs/sdk

Manages configuration settings, including getting general config and listing providers.

```APIDOC
## GET /config

### Description
Retrieves the general configuration information.

### Method
GET

### Endpoint
/config

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **config** (Config) - The configuration object.

#### Response Example
```json
{
  "setting1": "value1",
  "setting2": 123
}
```

## GET /config/providers

### Description
Lists available providers and their default models.

### Method
GET

### Endpoint
/config/providers

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **providers** (Provider[]) - An array of available providers.
- **default** (object) - An object mapping provider keys to their default model names.

#### Response Example
```json
{
  "providers": [
    {
      "name": "OpenAI",
      "models": ["gpt-3.5-turbo", "gpt-4"]
    }
  ],
  "default": {
    "openai": "gpt-3.5-turbo"
  }
}
```
```

--------------------------------

### Load Plugins for OpenCode

Source: https://opencode.ai/docs/config

Load custom plugins to extend OpenCode's capabilities. Plugins can be placed in specific directories or loaded directly from npm packages.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["opencode-helicone-session", "@my-org/custom-plugin"]
}
```

--------------------------------

### Use Grep by Vercel MCP Server in Prompt (Text)

Source: https://opencode.ai/docs/mcp-servers

This example prompt shows how to use the Grep by Vercel MCP server, identified as 'gh_grep', to find information on setting custom domains in an SST Astro component. It clearly states the query and the tool to use.

```text
What's the right way to set a custom domain in an SST Astro component? use the gh_grep tool
```

--------------------------------

### Subscribe to Real-time Events with JavaScript

Source: https://opencode.ai/docs/pt-br/sdk

This snippet shows how to listen to real-time events using the Opencode AI client in JavaScript. It establishes a subscription and iterates through the event stream, logging the type and properties of each received event. No external dependencies are required beyond the Opencode AI client library.

```javascript
const events = await client.event.subscribe()
for await (const event of events.stream) {
  console.log("Event:", event.type, event.properties)
}
```

--------------------------------

### Reset OpenCode Desktop App Data (Linux/macOS)

Source: https://opencode.ai/docs/troubleshooting

This command removes the OpenCode application data directory on Linux and macOS systems. This is a last resort for resolving issues when the application won't start or settings cannot be cleared through the UI. It deletes configuration files and UI state.

```bash
rm -rf ~/.local/share/opencode
```

--------------------------------

### Launch OpenCode with Wayland Support on Linux

Source: https://opencode.ai/docs/de/troubleshooting

This command attempts to launch the OpenCode application on Linux with Wayland support enabled. It's a troubleshooting step for Wayland-specific issues like blank windows or compositor errors.

```bash
OC_ALLOW_WAYLAND=1
```

--------------------------------

### Retrieve Configuration and Providers with JavaScript

Source: https://opencode.ai/docs/sdk

Illustrates how to fetch general configuration details using `config.get()` and a list of available providers along with their default models using `config.providers()`. The latter returns both providers and default model mappings.

```javascript
const config = await client.config.get()

const { providers, default: defaults } = await client.config.providers()
```

--------------------------------

### Example Custom Theme Configuration for OpenCode AI

Source: https://opencode.ai/docs/themes

This JSON file demonstrates a complete custom theme for OpenCode AI, named 'my-theme.json'. It includes a 'defs' section for defining Nord color palette values and a 'theme' section that assigns these defined colors to various UI elements and syntax highlighting categories. The theme supports both dark and light variations.

```json
{
  "$schema": "https://opencode.ai/theme.json",
  "defs": {
    "nord0": "#2E3440",
    "nord1": "#3B4252",
    "nord2": "#434C5E",
    "nord3": "#4C566A",
    "nord4": "#D8DEE9",
    "nord5": "#E5E9F0",
    "nord6": "#ECEFF4",
    "nord7": "#8FBCBB",
    "nord8": "#88C0D0",
    "nord9": "#81A1C1",
    "nord10": "#5E81AC",
    "nord11": "#BF616A",
    "nord12": "#D08770",
    "nord13": "#EBCB8B",
    "nord14": "#A3BE8C",
    "nord15": "#B48EAD"
  },
  "theme": {
    "primary": {
      "dark": "nord8",
      "light": "nord10"
    },
    "secondary": {
      "dark": "nord9",
      "light": "nord9"
    },
    "accent": {
      "dark": "nord7",
      "light": "nord7"
    },
    "error": {
      "dark": "nord11",
      "light": "nord11"
    },
    "warning": {
      "dark": "nord12",
      "light": "nord12"
    },
    "success": {
      "dark": "nord14",
      "light": "nord14"
    },
    "info": {
      "dark": "nord8",
      "light": "nord10"
    },
    "text": {
      "dark": "nord4",
      "light": "nord0"
    },
    "textMuted": {
      "dark": "nord3",
      "light": "nord1"
    },
    "background": {
      "dark": "nord0",
      "light": "nord6"
    },
    "backgroundPanel": {
      "dark": "nord1",
      "light": "nord5"
    },
    "backgroundElement": {
      "dark": "nord1",
      "light": "nord4"
    },
    "border": {
      "dark": "nord2",
      "light": "nord3"
    },
    "borderActive": {
      "dark": "nord3",
      "light": "nord2"
    },
    "borderSubtle": {
      "dark": "nord2",
      "light": "nord3"
    },
    "diffAdded": {
      "dark": "nord14",
      "light": "nord14"
    },
    "diffRemoved": {
      "dark": "nord11",
      "light": "nord11"
    },
    "diffContext": {
      "dark": "nord3",
      "light": "nord3"
    },
    "diffHunkHeader": {
      "dark": "nord3",
      "light": "nord3"
    },
    "diffHighlightAdded": {
      "dark": "nord14",
      "light": "nord14"
    },
    "diffHighlightRemoved": {
      "dark": "nord11",
      "light": "nord11"
    },
    "diffAddedBg": {
      "dark": "#3B4252",
      "light": "#E5E9F0"
    },
    "diffRemovedBg": {
      "dark": "#3B4252",
      "light": "#E5E9F0"
    },
    "diffContextBg": {
      "dark": "nord1",
      "light": "nord5"
    },
    "diffLineNumber": {
      "dark": "nord2",
      "light": "nord4"
    },
    "diffAddedLineNumberBg": {
      "dark": "#3B4252",
      "light": "#E5E9F0"
    },
    "diffRemovedLineNumberBg": {
      "dark": "#3B4252",
      "light": "#E5E9F0"
    },
    "markdownText": {
      "dark": "nord4",
      "light": "nord0"
    },
    "markdownHeading": {
      "dark": "nord8",
      "light": "nord10"
    },
    "markdownLink": {
      "dark": "nord9",
      "light": "nord9"
    },
    "markdownLinkText": {
      "dark": "nord7",
      "light": "nord7"
    },
    "markdownCode": {
      "dark": "nord14",
      "light": "nord14"
    },
    "markdownBlockQuote": {
      "dark": "nord3",
      "light": "nord3"
    },
    "markdownEmph": {
      "dark": "nord12",
      "light": "nord12"
    },
    "markdownStrong": {
      "dark": "nord13",
      "light": "nord13"
    },
    "markdownHorizontalRule": {
      "dark": "nord3",
      "light": "nord3"
    },
    "markdownListItem": {
      "dark": "nord8",
      "light": "nord10"
    },
    "markdownListEnumeration": {
      "dark": "nord7",
      "light": "nord7"
    },
    "markdownImage": {
      "dark": "nord9",
      "light": "nord9"
    },
    "markdownImageText": {
      "dark": "nord7",
      "light": "nord7"
    },
    "markdownCodeBlock": {
      "dark": "nord4",
      "light": "nord0"
    },
    "syntaxComment": {
      "dark": "nord3",
      "light": "nord3"
    },
    "syntaxKeyword": {
      "dark": "nord9",
      "light": "nord9"
    },
    "syntaxFunction": {
      "dark": "nord8",
      "light": "nord8"
    },
    "syntaxVariable": {
      "dark": "nord7",
      "light": "nord7"
    },
    "syntaxString": {
      "dark": "nord14",
      "light": "nord14"
    },
    "syntaxNumber": {
      "dark": "nord15",
      "light": "nord15"
    },
    "syntaxType": {
      "dark": "nord7",
      "light": "nord7"
    },
    "syntaxOperator": {
      "dark": "nord9",
      "light": "nord9"
    },
    "syntaxPunctuation": {
      "dark": "nord4",
      "light": "nord0"
    }
  }
}
```

--------------------------------

### Clear OpenCode Cache on Linux

Source: https://opencode.ai/docs/troubleshooting

Provides the command to remove the OpenCode cache directory on Linux systems. Clearing the cache is a crucial step for resolving issues related to corrupted application data or stuck plugin installations. This command forcefully removes the specified directory and its contents.

```bash
rm -rf ~/.cache/opencode
```

--------------------------------

### POST /session/:id/init

Source: https://opencode.ai/docs/server

Initializes the session by analyzing the app and creating `AGENTS.md`.  Requires a request body with messageID, providerID, and modelID.

```APIDOC
## POST /session/:id/init

### Description
Analyze app and create `AGENTS.md`.

### Method
POST

### Endpoint
/session/:id/init

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.

#### Request Body
- **messageID** (string) - Required - The ID of the message.
- **providerID** (string) - Required - The ID of the provider.
- **modelID** (string) - Required - The ID of the model.

### Request Example
{
  "messageID": "message1",
  "providerID": "provider1",
  "modelID": "model1"
}

### Response
#### Success Response (200)
- **boolean** - True if the initialization was successful.

#### Response Example
true

```

--------------------------------

### Configuring Initialization Options for TypeScript LSP

Source: https://opencode.ai/docs/lsp

This JSON example shows how to provide custom initialization options for the TypeScript LSP server. The `initialization` object allows you to send server-specific settings during the LSP `initialize` request. In this case, it configures the TypeScript server to prefer relative import paths.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "lsp": {
    "typescript": {
      "initialization": {
        "preferences": {
          "importModuleSpecifierPreference": "relative"
        }
      }
    }
  }
}
```

--------------------------------

### Run OpenCode using Docker

Source: https://opencode.ai/docs/index

Runs OpenCode in a Docker container. This command downloads the image if not present and starts an interactive terminal session.

```bash
docker run -it --rm ghcr.io/anomalyco/opencode
```

--------------------------------

### Substitute File Contents

Source: https://opencode.ai/docs/config

Use variable substitution with the `{file:path/to/file}` syntax to include the contents of a file directly into configuration. File paths can be relative to the config file or absolute.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["./custom-instructions.md"],
  "provider": {
    "openai": {
      "options": {
        "apiKey": "{file:~/.secrets/openai-key}"
      }
    }
  }
}
```

--------------------------------

### Connect to a Custom Provider via CLI

Source: https://opencode.ai/docs/providers

This bash command sequence demonstrates how to connect a custom AI provider using the OpenCode AI CLI. It guides the user through selecting 'Other', entering a unique provider ID, and providing the API key.

```bash
$ /connect

┌  Add credential
│
◆  Select provider
│  ...
│  ● Other
└

```

```bash
$ /connect

┌  Add credential
│
◇  Enter provider id
│  myprovider
└

```

```bash
$ /connect

┌  Add credential
│
▲  This only stores a credential for myprovider - you will need to configure it in opencode.json, check the docs for examples.
│
◇  Enter your API key
│  sk-...
└

```

--------------------------------

### Configure MCP Servers

Source: https://opencode.ai/docs/config

Configure the MCP servers that OpenCode will use. This option allows for specifying which MCP servers to integrate with for enhanced functionality.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {}
}
```

--------------------------------

### Confirm Feature Implementation

Source: https://opencode.ai/docs/index

An example of instructing OpenCode to proceed with making the changes after reviewing and approving the plan. This command triggers the code generation and modification process.

```text
Sounds good! Go ahead and make the changes.
```

--------------------------------

### Manage GitHub Agent

Source: https://opencode.ai/docs/cli

Commands for integrating and running the GitHub agent for repository automation. This includes installing the agent and running it, typically within GitHub Actions.

```bash
opencode github [command]
opencode github install
opencode github run
opencode github run --event <github_event> --token <github_token>
```

--------------------------------

### Initialize OpenCode Project

Source: https://opencode.ai/docs/index

Initializes OpenCode for the current project. This command analyzes the project and creates an AGENTS.md file, which helps OpenCode understand the project structure.

```bash
/init
```

--------------------------------

### Start ACP Server (Bash)

Source: https://opencode.ai/docs/cli

Starts an Agent Client Protocol (ACP) server that communicates via stdin/stdout using nd-JSON. The `--cwd` flag specifies the working directory.

```bash
opencode acp
```

--------------------------------

### Provide Design Reference in Plan Mode

Source: https://opencode.ai/docs/index

Example of providing additional context or design references to OpenCode in 'Plan mode'. This can include referencing existing designs or uploading images.

```text
We'd like to design this new screen using a design I've used before.
[Image #1] Take a look at this image and use it as a reference.
```

--------------------------------

### Add Test Local MCP Server in OpenCode

Source: https://opencode.ai/docs/mcp-servers

Provides an example of adding the `@modelcontextprotocol/server-everything` MCP server locally. This configuration uses `npx` to run the server command, making it available for use in prompts by referencing its name (e.g., `mcp_everything`).

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "mcp_everything": {
      "type": "local",
      "command": ["npx", "-y", "@modelcontextprotocol/server-everything"]
    }
  }
}
```

--------------------------------

### Start OpenCode TUI

Source: https://opencode.ai/docs/cli

Initiate the OpenCode Terminal User Interface (TUI). This command can optionally take a project argument and supports various flags for customization.

```bash
opencode [project]
opencode --continue
opencode -c
opencode --session <session_id>
opencode -s <session_id>
opencode --fork
opencode --prompt <prompt>
opencode --model <provider/model>
opencode -m <provider/model>
opencode --agent <agent>
opencode --port <port>
opencode --hostname <hostname>
```

--------------------------------

### GET /session/:id/children

Source: https://opencode.ai/docs/server

Retrieves the child sessions of a given session.  This endpoint is used to get the sessions that are children of a specific session.

```APIDOC
## GET /session/:id/children

### Description
Gets a session's child sessions.

### Method
GET

### Endpoint
/session/:id/children

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the parent session.

### Request Example
No request body.

### Response
#### Success Response (200)
- **Session[]** - An array of child Session objects.

#### Response Example
[
  {
    "id": "childSession1",
    "title": "Child Session Title",
    // ... other session properties
  }
]

```

--------------------------------

### Reset OpenCode Desktop App Data (Windows)

Source: https://opencode.ai/docs/troubleshooting

This instruction guides users to manually delete the OpenCode application data directory on Windows. This action is recommended as a last resort for troubleshooting startup or settings issues when in-app options are unavailable. It clears stored configurations and UI states.

```batch
Press WIN+R and delete: %USERPROFILE%\.local\share\opencode
```

--------------------------------

### Connect to GitHub Copilot

Source: https://opencode.ai/docs/providers

Instructions for connecting to GitHub Copilot with OpenCode. This involves running a command, navigating to a GitHub URL, and entering a provided code for authorization.

```text
/connect

┌ Login with GitHub Copilot
│
│ https://github.com/login/device
│
│ Enter code: 8F43-6FCF
│
└ Waiting for authorization...

/models
```

--------------------------------

### Get Current Path Information with JavaScript

Source: https://opencode.ai/docs/sdk

Demonstrates the usage of the `path.get()` method to retrieve information about the current path. The response is expected to be of type `Path`.

```javascript
// Get current path information
const pathInfo = await client.path.get()
```

--------------------------------

### Describe Feature in Plan Mode

Source: https://opencode.ai/docs/index

An example of describing a new feature request to OpenCode while in 'Plan mode'. This provides detailed instructions for the AI to generate a plan.

```text
When a user deletes a note, we'd like to flag it as deleted in the database.
Then create a screen that shows all the recently deleted notes.
From this screen, the user can undelete a note or permanently delete it.
```

--------------------------------

### OpenCode TUI Configuration (opencode.json)

Source: https://opencode.ai/docs/tui

Defines the configuration for the OpenCode Text User Interface (TUI) stored in the opencode.json file. This example shows settings for scroll speed and scroll acceleration, with scroll acceleration taking precedence.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "tui": {
    "scroll_speed": 3,
    "scroll_acceleration": {
      "enabled": true
    }
  }
}
```

--------------------------------

### Configure LLM Provider and Models in opencode.json

Source: https://opencode.ai/docs/config

This snippet illustrates how to configure LLM providers and models in OpenCode. It specifies the main model and a separate 'small_model' for lightweight tasks, along with provider-specific options like timeout and cache key.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {},
  "model": "anthropic/claude-sonnet-4-5",
  "small_model": "anthropic/claude-haiku-4-5"
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "anthropic": {
      "options": {
        "timeout": 600000,
        "setCacheKey": true
      }
    }
  }
}
```

--------------------------------

### Upgrade OpenCode (Bash)

Source: https://opencode.ai/docs/cli

Updates OpenCode to the latest version or a specific version. The `--method` flag specifies the installation method.

```bash
opencode upgrade [target]
```

```bash
opencode upgrade
```

```bash
opencode upgrade v0.1.48
```

--------------------------------

### Manage Sessions with OpenCode AI API (JavaScript)

Source: https://opencode.ai/docs/de/sdk

Demonstrates how to create, list, and interact with sessions using the OpenCode AI client. This includes sending prompts and injecting context without triggering an AI response.

```javascript
const session = await client.session.create({
  body: { title: "My session" },
})

const sessions = await client.session.list()

// Send a prompt message
const result = await client.session.prompt({
  path: { id: session.id },
  body: {
    model: { providerID: "anthropic", modelID: "claude-3-5-sonnet-20241022" },
    parts: [{ type: "text", text: "Hello!" }],
  },
})

// Inject context without triggering AI response (useful for plugins)
await client.session.prompt({
  path: { id: session.id },
  body: {
    noReply: true,
    parts: [{ type: "text", text: "You are a helpful assistant." }],
  },
})
```

--------------------------------

### OpenCode Remote and Local Configuration for MCP Jira

Source: https://opencode.ai/docs/config

Demonstrates how to configure MCP Jira settings. The remote configuration disables Jira by default, while a local configuration can override this to enable it.

```json
{
  "mcp": {
    "jira": {
      "type": "remote",
      "url": "https://jira.example.com/mcp",
      "enabled": false
    }
  }
}
```

```json
{
  "mcp": {
    "jira": {
      "type": "remote",
      "url": "https://jira.example.com/mcp",
      "enabled": true
    }
  }
}
```

--------------------------------

### Start Headless OpenCode Server

Source: https://opencode.ai/docs/cli

Initiates a headless OpenCode server, providing API access without the TUI. This is useful for integrating OpenCode functionality into other applications or workflows. Security can be enhanced by setting the OPENCODE_SERVER_PASSWORD environment variable.

```bash
opencode serve
```

--------------------------------

### Disabling a Specific Formatter (Prettier)

Source: https://opencode.ai/docs/formatters

This example demonstrates how to disable a specific formatter, 'prettier', by setting its 'disabled' property to 'true' within the 'formatter' configuration.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "formatter": {
    "prettier": {
      "disabled": true
    }
  }
}
```

--------------------------------

### GET /session/status

Source: https://opencode.ai/docs/server

Retrieves the status of all sessions.  The response is a dictionary mapping session IDs to their respective statuses.

```APIDOC
## GET /session/status

### Description
Gets session status for all sessions.

### Method
GET

### Endpoint
/session/status

### Parameters
No parameters.

### Request Example
No request body.

### Response
#### Success Response (200)
- **{ [sessionID: string]: SessionStatus }** - A dictionary of session statuses, keyed by session ID.

#### Response Example
{
  "session1": "running",
  "session2": "idle"
}

```

--------------------------------

### Customize Keybinds in OpenCode

Source: https://opencode.ai/docs/config

Allows customization of keybindings through the 'keybinds' option in opencode.json. An empty object indicates default keybinds or no custom keybinds are set.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "keybinds": {}
}
```

--------------------------------

### Configure Theme in opencode.json

Source: https://opencode.ai/docs/config

This snippet demonstrates how to set the visual theme for OpenCode in the configuration file. It uses the 'theme' option, which can be set to an empty string or a specific theme name.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "theme": ""
}
```

--------------------------------

### Enable Specific Providers

Source: https://opencode.ai/docs/config

Specify an allowlist of providers to be enabled. Only the listed providers will be active, and all others will be ignored. This option is overridden by disabled_providers.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "enabled_providers": ["anthropic", "openai"]
}
```

--------------------------------

### GET /session/:id/todo

Source: https://opencode.ai/docs/server

Retrieves the todo list associated with a specific session.  This endpoint provides access to the todo items for a given session.

```APIDOC
## GET /session/:id/todo

### Description
Gets the todo list for a session.

### Method
GET

### Endpoint
/session/:id/todo

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.

### Request Example
No request body.

### Response
#### Success Response (200)
- **Todo[]** - An array of Todo objects.

#### Response Example
[
  {
    "id": "todo1",
    "text": "Todo Item Text",
    // ... other todo properties
  }
]

```

--------------------------------

### Connect to OpenCode Zen

Source: https://opencode.ai/docs/providers

Connects to OpenCode Zen by running the /connect command and entering the provided API key. This allows access to a list of tested and verified models.

```txt
/connect
```

```txt
┌ API key
│
│
└ enter
```

--------------------------------

### Configure Cloudflare AI Gateway models in Opencode config

Source: https://opencode.ai/docs/providers

Example of how to configure Cloudflare AI Gateway models directly within the Opencode configuration file.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "cloudflare-ai-gateway": {
      "models": {
        "openai/gpt-4o": {},
        "anthropic/claude-sonnet-4": {}
      }
    }
  }
}
```

--------------------------------

### Run opencode Serve Command

Source: https://opencode.ai/docs/server

The `opencode serve` command initiates a headless HTTP server. It accepts options to configure the listening port, hostname, and CORS origins. The `--cors` option can be specified multiple times to allow multiple origins.

```bash
opencode serve [--port <number>] [--hostname <string>] [--cors <origin>]
```

```bash
opencode serve --cors http://localhost:5173 --cors https://app.example.com
```

--------------------------------

### Control Context Compaction in OpenCode

Source: https://opencode.ai/docs/config

Manages context compaction behavior with the 'compaction' option in opencode.json. Options include 'auto', 'prune', and 'reserved' tokens for buffer.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "compaction": {
    "auto": true,
    "prune": true,
    "reserved": 10000
  }
}
```

--------------------------------

### GET /session/:id

Source: https://opencode.ai/docs/server

Retrieves details for a specific session, identified by its ID.  This endpoint provides a way to fetch the details of a specific session.

```APIDOC
## GET /session/:id

### Description
Gets session details.

### Method
GET

### Endpoint
/session/:id

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.

### Request Example
No request body.

### Response
#### Success Response (200)
- **Session** - The session object.

#### Response Example
{
  "id": "session1",
  "title": "Session Title",
  // ... other session properties
}

```

--------------------------------

### Clear OpenCode Provider Package Cache (Windows)

Source: https://opencode.ai/docs/troubleshooting

This instruction guides users to manually delete the OpenCode provider package cache on Windows. This action helps resolve AI_APICallError issues caused by outdated or corrupted provider packages. Restarting OpenCode after clearing the cache will prompt it to download the latest packages.

```batch
Press WIN+R and delete: %USERPROFILE%\.cache\opencode
```

--------------------------------

### Substitute Environment Variables

Source: https://opencode.ai/docs/config

Use variable substitution with the `{env:VARIABLE_NAME}` syntax to reference environment variables within configuration files. If an environment variable is not set, it will be replaced with an empty string.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "{env:OPENCODE_MODEL}",
  "provider": {
    "anthropic": {
      "models": {},
      "options": {
        "apiKey": "{env:ANTHROPIC_API_KEY}"
      }
    }
  }
}
```

--------------------------------

### Configure ignore patterns in .ignore file

Source: https://opencode.ai/docs/de/tools

This text file example shows how to configure ignore patterns for tools like ripgrep within OpenCode AI. By using the '!' prefix, specific directories like 'node_modules/', 'dist/', and 'build/' are explicitly included in searches, overriding default behavior that respects .gitignore.

```text
!node_modules/
!dist/
!build/
```

--------------------------------

### Configure Sharing Feature in OpenCode

Source: https://opencode.ai/docs/config

Sets the behavior for the sharing feature using the 'share' option in opencode.json. Options include 'manual', 'auto', and 'disabled'.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "share": "manual"
}
```

--------------------------------

### Handle SDK Errors

Source: https://opencode.ai/docs/sdk

Implement error handling for SDK operations using a try-catch block. This example shows how to catch potential errors when fetching a session and log the error message.

```typescript
try {
  await client.session.get({ path: { id: "invalid-id" } })
} catch (error) {
  console.error("Failed to get session:", (error as Error).message)
}
```

--------------------------------

### Use Sentry MCP Server in Prompt (Text)

Source: https://opencode.ai/docs/mcp-servers

This is an example of a natural language prompt that utilizes the Sentry MCP server to query Sentry issues. The prompt specifies the action and the tool to be used.

```text
Show me the latest unresolved issues in my project. use sentry
```

--------------------------------

### GET /session/:id/diff

Source: https://opencode.ai/docs/server

Retrieves the diff for a session, optionally filtered by a message ID.  This endpoint provides the differences between session states.

```APIDOC
## GET /session/:id/diff

### Description
Get the diff for this session.

### Method
GET

### Endpoint
/session/:id/diff

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.

#### Query Parameters
- **messageID** (string) - Optional - The ID of the message.

### Request Example
No request body.

### Response
#### Success Response (200)
- **FileDiff[]** - An array of FileDiff objects.

#### Response Example
[
  {
    "file": "file1.txt",
    "diff": "..."
  }
]

```

--------------------------------

### Check Server Health with JavaScript

Source: https://opencode.ai/docs/sdk

Example of how to use the `global.health()` method from the SDK to check the server's health status and retrieve its version. This is a fundamental API call for verifying service availability.

```javascript
const health = await client.global.health()
console.log(health.data.version)
```

--------------------------------

### Configure LLM Tool Usage in opencode.json

Source: https://opencode.ai/docs/config

This snippet shows how to manage the tools an LLM can use within the OpenCode configuration file. It includes boolean flags to enable or disable specific tools like 'write' and 'bash'.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "tools": {
    "write": false,
    "bash": false
  }
}
```

--------------------------------

### Disable Specific Providers

Source: https://opencode.ai/docs/config

Disable providers that are automatically loaded to prevent them from being used, even if credentials are available. This option takes priority over enabled_providers.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "disabled_providers": ["openai", "gemini"]
}
```

--------------------------------

### External Directory Permissions (JSON)

Source: https://opencode.ai/docs/permissions

Manage access to paths outside the working directory using `external_directory`. Home directory expansion (`~` or `$HOME`) can be used in patterns. This example allows all actions under `~/projects/personal/`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "external_directory": {
      "~/projects/personal/**": "allow"
    }
  }
}
```

--------------------------------

### Create a New Agent via CLI

Source: https://opencode.ai/docs/agents

Create new agents interactively using the 'opencode agent create' command. This process includes specifying the save location, agent description, system prompt, identifier, and accessible tools.

```bash
opencode agent create
```

--------------------------------

### Control Autoupdate Behavior in OpenCode

Source: https://opencode.ai/docs/config

Disables automatic updates on startup using the 'autoupdate' option in opencode.json. Setting it to 'notify' will only show notifications for new versions.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "autoupdate": false
}
```

--------------------------------

### Custom Agent Skill Permissions Override

Source: https://opencode.ai/docs/skills

Provides an example of how to override global skill permissions for a specific custom agent by defining permissions in the agent's frontmatter.

```yaml
---
permission:
  skill:
    "documents-*": "allow"
---

```

--------------------------------

### Create Opencode Client Only

Source: https://opencode.ai/docs/sdk

Create a client instance to connect to an already running OpenCode server. This is useful when the server is managed separately. It requires the server's base URL and offers options for fetch implementation, response parsing, and error handling.

```javascript
import { createOpencodeClient } from "@opencode-ai/sdk"

const client = createOpencodeClient({
  baseUrl: "http://localhost:4096",
})
```

--------------------------------

### Configure TUI Settings in opencode.json

Source: https://opencode.ai/docs/config

This snippet shows how to configure Text User Interface (TUI) specific settings in the opencode.json file. It includes options for scroll speed, scroll acceleration, and diff style.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "tui": {
    "scroll_speed": 3,
    "scroll_acceleration": {
      "enabled": true
    },
    "diff_style": "auto"
  }
}
```

--------------------------------

### Define Tool Arguments with Plain Zod Object

Source: https://opencode.ai/docs/custom-tools

This example shows an alternative way to define tool arguments by directly importing and using Zod. It defines a 'param' argument as a string with a description and includes the tool's description and execution logic.

```typescript
import { z } from "zod"

export default {
  description: "Tool description",
  args: {
    param: z.string().describe("Parameter description"),
  },
  async execute(args, context) {
    // Tool implementation
    return "result"
  },
}
```

--------------------------------

### Get Mailto Link from Configuration

Source: https://opencode.ai/docs/enterprise

This snippet demonstrates how to retrieve an email address from a configuration file to construct a 'mailto' link. It imports configuration settings and exports a constant containing the email link.

```javascript
import config from "../../../config.mjs"
export const email = `mailto:${config.email}`
```

--------------------------------

### Set Log Level for Detailed Diagnostics

Source: https://opencode.ai/docs/de/troubleshooting

This command allows you to increase the verbosity of OpenCode's logging to capture more detailed diagnostic information, which is useful for debugging.

```bash
opencode --log-level DEBUG
```

--------------------------------

### Configure OpenCode AI Flow in GitLab CI/CD (YAML)

Source: https://opencode.ai/docs/gitlab

This YAML configuration defines the steps for setting up and running OpenCode AI within a GitLab CI/CD pipeline. It includes installing necessary tools like opencode-ai and glab, configuring authentication, setting up git, and executing the OpenCode AI command with a prompt.

```yaml
image: node:22-slim
commands:
  - echo "Installing opencode"
  - npm install --global opencode-ai
  - echo "Installing glab"
  - export GITLAB_TOKEN=$GITLAB_TOKEN_OPENCODE
  - apt-get update --quiet && apt-get install --yes curl wget gpg git && rm --recursive --force /var/lib/apt/lists/*
  - curl --silent --show-error --location "https://raw.githubusercontent.com/upciti/wakemeops/main/assets/install_repository" | bash
  - apt-get install --yes glab
  - echo "Configuring glab"
  - echo $GITLAB_HOST
  - echo "Creating OpenCode auth configuration"
  - mkdir --parents ~/.local/share/opencode
  - |
    cat > ~/.local/share/opencode/auth.json << EOF
    {
      "anthropic": {
        "type": "api",
        "key": "$ANTHROPIC_API_KEY"
      }
    }
    EOF
  - echo "Configuring git"
  - git config --global user.email "opencode@gitlab.com"
  - git config --global user.name "OpenCode"
  - echo "Testing glab"
  - glab issue list
  - echo "Running OpenCode"
  - |
    opencode run "
    You are an AI assistant helping with GitLab operations.

    Context: $AI_FLOW_CONTEXT
    Task: $AI_FLOW_INPUT
    Event: $AI_FLOW_EVENT

    Please execute the requested task using the available GitLab tools.
    Be thorough in your analysis and provide clear explanations.

    <important>
    Please use the glab CLI to access data from GitLab. The glab CLI has already been authenticated. You can run the corresponding commands.

    If you are asked to summarize an MR or issue or asked to provide more information then please post back a note to the MR/Issue so that the user can see it.
    You don't need to commit or push up changes, those will be done automatically based on the file changes you make.
    </important>
    "
  - git checkout --branch $CI_WORKLOAD_REF origin/$CI_WORKLOAD_REF
  - echo "Checking for git changes and pushing if any exist"
  - |
    if ! git diff --quiet || ! git diff --cached --quiet || [ --not --zero "$(git ls-files --others --exclude-standard)" ]; then
      echo "Git changes detected, adding and pushing..."
      git add .
      if git diff --cached --quiet; then
        echo "No staged changes to commit"
      else
        echo "Committing changes to branch: $CI_WORKLOAD_REF"
        git commit --message "Codex changes"
        echo "Pushing changes up to $CI_WORKLOAD_REF"
        git push https://gitlab-ci-token:$GITLAB_TOKEN@$GITLAB_HOST/gl-demo-ultimate-dev-ai-epic-17570/test-java-project.git $CI_WORKLOAD_REF
        echo "Changes successfully pushed"
      fi
    else
      echo "No git changes detected, skipping push"
    fi
variables:
  - ANTHROPIC_API_KEY
  - GITLAB_TOKEN_OPENCODE
  - GITLAB_HOST

```

--------------------------------

### Configure Private NPM Registry Authentication

Source: https://opencode.ai/docs/enterprise

This snippet demonstrates how to authenticate with a private NPM registry, such as JFrog Artifactory, for use with OpenCode Enterprise. It includes commands for logging in and examples of manual configuration.

```bash
npm login --registry=https://your-company.jfrog.io/api/npm/npm-virtual/
```

```bash
registry=https://your-company.jfrog.io/api/npm/npm-virtual/
//your-company.jfrog.io/api/npm/npm-virtual/:_authToken=${NPM_AUTH_TOKEN}
```

--------------------------------

### Commands API

Source: https://opencode.ai/docs/server

Endpoint for listing all available commands.

```APIDOC
## GET /command

### Description
List all commands.

### Method
GET

### Endpoint
/command

### Response
#### Success Response (200)
- **Command[]** - An array of command objects.

#### Response Example
[
  {
    "name": "list_files",
    "description": "List files in the current directory."
  },
  {
    "name": "run_script",
    "description": "Run a script."
  }
]
```

--------------------------------

### Disable Plugins Globally in OpenCode Configuration

Source: https://opencode.ai/docs/de/troubleshooting

This JSON configuration snippet shows how to disable all plugins by setting the 'plugin' key to an empty array. This is a common step when troubleshooting issues caused by faulty plugins.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": []
}
```

--------------------------------

### Set Default Agent in OpenCode

Source: https://opencode.ai/docs/config

Configures the default agent to be used when none is explicitly specified, using the 'default_agent' option in opencode.json. The default agent must be a primary agent.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "default_agent": "plan"
}
```

--------------------------------

### Configure AWS Authentication via Environment Variables for OpenCode

Source: https://opencode.ai/docs/providers

Set environment variables to authenticate with AWS services when running OpenCode. Supports AWS access keys, named profiles, and Bedrock bearer tokens for quick setup.

```bash
# Option 1: Using AWS access keys
AWS_ACCESS_KEY_ID=XXX AWS_SECRET_ACCESS_KEY=YYY opencode

# Option 2: Using named AWS profile
AWS_PROFILE=my-profile opencode

# Option 3: Using Bedrock bearer token
AWS_BEARER_TOKEN_BEDROCK=XXX opencode
```

--------------------------------

### Configure Amazon Bedrock Provider in opencode.json

Source: https://opencode.ai/docs/config

This snippet shows provider-specific configuration for Amazon Bedrock within OpenCode. It includes AWS-specific options such as region, profile, and a custom endpoint for VPC endpoints.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "amazon-bedrock": {
      "options": {
        "region": "us-east-1",
        "profile": "my-aws-profile",
        "endpoint": "https://bedrock-runtime.us-east-1.vpce-xxxxx.amazonaws.com"
      }
    }
  }
}
```

--------------------------------

### Execute Python Script from TypeScript Tool

Source: https://opencode.ai/docs/custom-tools

This example shows how to create a TypeScript tool definition that invokes an external Python script to perform a task (adding two numbers). It uses Bun's shell utility (`Bun.$`) to execute the Python script, passing arguments and capturing the output.

```typescript
import { tool } from "@opencode-ai/plugin"
import path from "path"

export default tool({
  description: "Add two numbers using Python",
  args: {
    a: tool.schema.number().describe("First number"),
    b: tool.schema.number().describe("Second number"),
  },
  async execute(args, context) {
    const script = path.join(context.worktree, ".opencode/tools/add.py")
    const result = await Bun.$`python3 ${script} ${args.a} ${args.b}`.text()
    return result.trim()
  },
})
```

--------------------------------

### Enable Bash Tool in OpenCode

Source: https://opencode.ai/docs/tools

Configure the 'bash' tool permission to 'allow' in your opencode.json file. This enables the LLM to execute shell commands directly within your project's environment, facilitating tasks like package installation or status checks.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "bash": "allow"
  }
}
```

--------------------------------

### Define Multiple Tools in a TypeScript File

Source: https://opencode.ai/docs/custom-tools

This example demonstrates exporting multiple tools, 'add' and 'multiply', from a single TypeScript file. Each exported tool becomes a separate entity with a name formatted as '<filename>_<exportname>'. Both tools define their arguments and execution logic.

```typescript
import { tool } from "@opencode-ai/plugin"

export const add = tool({
  description: "Add two numbers",
  args: {
    a: tool.schema.number().describe("First number"),
    b: tool.schema.number().describe("Second number"),
  },
  async execute(args) {
    return args.a + args.b
  },
})

export const multiply = tool({
  description: "Multiply two numbers",
  args: {
    a: tool.schema.number().describe("First number"),
    b: tool.schema.number().describe("Second number"),
  },
  async execute(args) {
    return args.a * args.b
  },
})
```

--------------------------------

### Manage Local Plugin Dependencies with package.json

Source: https://opencode.ai/docs/plugins

This JSON configuration file is used to declare npm package dependencies for local plugins. By including a package.json in your config directory, OpenCode can automatically install these dependencies using Bun at startup, making them available for your plugins to import and use.

```json
{
  "dependencies": {
    "shescape": "^2.1.0"
  }
}
```

--------------------------------

### Connect to Groq Provider

Source: https://opencode.ai/docs/providers

Steps to connect to the Groq AI provider. This involves obtaining an API key from the Groq console, running the connect command in OpenCode, and entering the API key when prompted.

```text
/connect

┌ API key
│
│
└ enter

/models
```

--------------------------------

### Configure File Watcher Ignore Patterns

Source: https://opencode.ai/docs/config

Set file watcher ignore patterns using glob syntax to exclude specific directories like node_modules, dist, or .git from being watched. This helps in managing noisy directories and improving performance.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "watcher": {
    "ignore": ["node_modules/**", "dist/**", ".git/**"]
  }
}
```

--------------------------------

### Configure Agents with JSON

Source: https://opencode.ai/docs/agents

Defines various agents (build, plan, code-reviewer) with their modes, models, prompts, and tool configurations in a JSON format. This is the primary method for setting up agent behavior.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "build": {
      "mode": "primary",
      "model": "anthropic/claude-sonnet-4-20250514",
      "prompt": "{file:./prompts/build.txt}",
      "tools": {
        "write": true,
        "edit": true,
        "bash": true
      }
    },
    "plan": {
      "mode": "primary",
      "model": "anthropic/claude-haiku-4-20250514",
      "tools": {
        "write": false,
        "edit": false,
        "bash": false
      }
    },
    "code-reviewer": {
      "description": "Reviews code for best practices and potential issues",
      "mode": "subagent",
      "model": "anthropic/claude-sonnet-4-20250514",
      "prompt": "You are a code reviewer. Focus on security, performance, and maintainability.",
      "tools": {
        "write": false,
        "edit": false
      }
    }
  }
}
```

--------------------------------

### POST /session

Source: https://opencode.ai/docs/server

Creates a new session.  The request body allows for specifying optional parameters like parentID and title.

```APIDOC
## POST /session

### Description
Creates a new session.

### Method
POST

### Endpoint
/session

### Parameters
#### Request Body
- **parentID** (string) - Optional - The ID of the parent session.
- **title** (string) - Optional - The title of the session.

### Request Example
{
  "title": "New Session",
  "parentID": "parentSessionID"
}

### Response
#### Success Response (200)
- **Session** - The newly created Session object.

#### Response Example
{
  "id": "session2",
  "title": "New Session",
  "parentID": "parentSessionID",
  // ... other session properties
}

```

--------------------------------

### Configure Helicone Models in OpenCode

Source: https://opencode.ai/docs/providers

This JSON configuration allows you to manually add models from Helicone's directory to your OpenCode setup. You need to provide the model ID from Helicone's model directory and optionally a custom name for display within OpenCode.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "helicone": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Helicone",
      "options": {
        "baseURL": "https://ai-gateway.helicone.ai"
      },
      "models": {
        "gpt-4o": {
          "name": "GPT-4o"
        },
        "claude-sonnet-4-20250514": {
          "name": "Claude Sonnet 4"
        }
      }
    }
  }
}
```

--------------------------------

### Create Custom Theme Directory (Bash)

Source: https://opencode.ai/docs/themes

These commands demonstrate how to create the necessary directory structure for custom OpenCode themes in both user-specific and project-specific locations. It utilizes standard bash commands for directory creation.

```bash
mkdir -p ~/.config/opencode/themes
vim ~/.config/opencode/themes/my-theme.json
```

```bash
mkdir -p .opencode/themes
vim .opencode/themes/my-theme.json
```

--------------------------------

### Disable OpenCode Keybind Example

Source: https://opencode.ai/docs/keybinds

This JSON snippet demonstrates how to disable a specific keybinding in OpenCode. By setting the value of a keybind to 'none' in the opencode.json configuration, that particular shortcut will no longer be active. This is useful for avoiding conflicts or removing unwanted shortcuts.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "keybinds": {
    "session_compact": "none"
  }
}
```

--------------------------------

### Define Custom Mode in Markdown

Source: https://opencode.ai/docs/modes

Creates a custom 'review' mode using a Markdown file. This mode is configured with a specific model, temperature, and disabled tools, along with a system prompt guiding the AI's behavior for code reviews.

```markdown
---
model: anthropic/claude-sonnet-4-20250514
temperature: 0.1
tools:
  write: false
  edit: false
  bash: false
---

You are in code review mode. Focus on:

- Code quality and best practices
- Potential bugs and edge cases
- Performance implications
- Security considerations

Provide constructive feedback without making direct changes.
```

--------------------------------

### Generate Structured JSON Output

Source: https://opencode.ai/docs/sdk

Request structured JSON output from the model by providing a JSON schema in the `format` option. The SDK uses a `StructuredOutput` tool to validate the response against the schema. The example demonstrates requesting company information and accessing the structured output.

```typescript
const result = await client.session.prompt({
  path: { id: sessionId },
  body: {
    parts: [{ type: "text", text: "Research Anthropic and provide company info" }],
    format: {
      type: "json_schema",
      schema: {
        type: "object",
        properties: {
          company: { type: "string", description: "Company name" },
          founded: { type: "number", description: "Year founded" },
          products: {
            type: "array",
            items: { type: "string" },
            description: "Main products",
          },
        },
        required: ["company", "founded"],
      },
    },
  },
})

// Access the structured output
console.log(result.data.info.structured_output)
// { company: "Anthropic", founded: 2021, products: ["Claude", "Claude API"] }
```

--------------------------------

### Session Analysis and Initialization API

Source: https://opencode.ai/docs/de/server

Endpoint to analyze an application and create an AGENTS.md file for a session.

```APIDOC
## POST /session/:id/init

### Description
Analyze the application and create an AGENTS.md file for the session.

### Method
POST

### Endpoint
/session/:id/init

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.
#### Request Body
- **messageID** (string) - Required - The ID of the message to initiate analysis from.
- **providerID** (string) - Required - The ID of the AI provider.
- **modelID** (string) - Required - The ID of the AI model to use.

### Request Example
```json
{
  "messageID": "msg_xyz",
  "providerID": "openai",
  "modelID": "gpt-4"
}
```

### Response
#### Success Response (200)
- **success** (boolean) - Indicates if the AGENTS.md file was created successfully.

#### Response Example
```json
true
```
```

--------------------------------

### Instance API

Source: https://opencode.ai/docs/server

Endpoint for disposing of the current instance.

```APIDOC
## POST /instance/dispose

### Description
Dispose of the current instance.

### Method
POST

### Endpoint
/instance/dispose

### Response
#### Success Response (200)
- **boolean** - Indicates if the instance was successfully disposed.

#### Response Example
```json
true
```
```

--------------------------------

### Set SAP AI Core Deployment and Resource Group

Source: https://opencode.ai/docs/providers

Optionally sets the SAP AI Core deployment ID and resource group as environment variables when running the opencode command. These settings should align with your specific SAP AI Core setup.

```bash
AICORE_DEPLOYMENT_ID=your-deployment-id AICORE_RESOURCE_GROUP=your-resource-group opencode
```

--------------------------------

### Customizing and Adding Formatters

Source: https://opencode.ai/docs/formatters

This JSON configuration shows how to customize existing formatters like 'prettier' or add new custom formatters. It includes specifying the command, environment variables, and associated file extensions for each formatter.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "formatter": {
    "prettier": {
      "command": ["npx", "prettier", "--write", "$FILE"],
      "environment": {
        "NODE_ENV": "development"
      },
      "extensions": [".js", ".ts", ".jsx", ".tsx"]
    },
    "custom-markdown-formatter": {
      "command": ["deno", "fmt", "$FILE"],
      "extensions": [".md"]
    }
  }
}
```

--------------------------------

### Disabling a Specific LSP Server (TypeScript Example)

Source: https://opencode.ai/docs/lsp

This JSON configuration demonstrates how to disable a specific LSP server, in this case, the TypeScript server. By setting the `disabled` property to `true` within the server's configuration object, OpenCode will not enable or run the TypeScript LSP server, even if TypeScript files are detected.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "lsp": {
    "typescript": {
      "disabled": true
    }
  }
}
```

--------------------------------

### Connect to Ollama Cloud

Source: https://opencode.ai/docs/providers

Instructions for using Ollama Cloud with OpenCode. This involves generating an API key from Ollama.com, using the `/connect` command, and importantly, pulling the desired model locally using the `ollama pull` command.

```bash
ollama pull gpt-oss:20b-cloud

```

--------------------------------

### Set EDITOR Environment Variable (Windows CMD)

Source: https://opencode.ai/docs/tui

Sets the default text editor for OpenCode commands in the Windows Command Prompt (CMD). Examples include notepad and GUI editors like VS Code with the '--wait' flag. To make the setting permanent, use the System Properties > Environment Variables dialog.

```batch
set EDITOR=notepad

# For GUI editors, VS Code, Cursor, VSCodium, Windsurf, Zed, etc.
# include --wait
set EDITOR=code --wait
```

--------------------------------

### Global Skill Permissions Configuration

Source: https://opencode.ai/docs/skills

Shows how to configure global permissions for agent skills using pattern matching in the `opencode.json` file. It details 'allow', 'deny', and 'ask' behaviors.

```json
{
  "permission": {
    "skill": {
      "*": "allow",
      "pr-review": "allow",
      "internal-*": "deny",
      "experimental-*": "ask"
    }
  }
}

```

--------------------------------

### Authentication API

Source: https://opencode.ai/docs/server

Endpoint for setting authentication credentials.

```APIDOC
## PUT /auth/:id

### Description
Set authentication credentials. Body must match provider schema.

### Method
PUT

### Endpoint
/auth/:id

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the authentication provider.

#### Query Parameters
None

#### Request Body
- **credentials** (object) - Required - The authentication credentials matching the provider schema.

### Request Example
```json
{
  "credentials": {
    "username": "user",
    "password": "secret"
  }
}
```

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the credentials were set successfully.

#### Response Example
```json
true
```
```

--------------------------------

### Specify Custom Prompt File in JSON

Source: https://opencode.ai/docs/agents

Uses the `prompt` configuration in `opencode.json` to specify a custom system prompt file for an agent. The path is relative to the config file's location.

```json
{
  "agent": {
    "review": {
      "prompt": "{file:./prompts/code-review.txt}"
    }
  }
}
```

--------------------------------

### Configure Agent Permissions in opencode.json

Source: https://opencode.ai/docs/agents

Define permissions for agent actions like 'edit', 'bash', and 'webfetch' using 'ask', 'allow', or 'deny'. Permissions can be overridden per agent or for specific bash commands using glob patterns. The last matching rule takes precedence, so wildcards should generally be placed first.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "edit": "deny"
  }
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "edit": "deny"
  },
  "agent": {
    "build": {
      "permission": {
        "edit": "ask"
      }
    }
  }
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "build": {
      "permission": {
        "bash": {
          "git push": "ask",
          "grep *": "allow"
        }
      }
    }
  }
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "build": {
      "permission": {
        "bash": {
          "git *": "ask"
        }
      }
    }
  }
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "build": {
      "permission": {
        "bash": {
          "*": "ask",
          "git status *": "allow"
        }
      }
    }
  }
}
```

--------------------------------

### Configure Self-Hosted GitLab Duo

Source: https://opencode.ai/docs/providers

Sets up a self-hosted GitLab Duo instance by defining environment variables for the instance URL, AI Gateway URL, and API token. It also includes a JSON configuration for specifying the small model and disabling session sharing.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "small_model": "gitlab/duo-chat-haiku-4-5",
  "share": "disabled"
}
```

--------------------------------

### Find and Read Files with OpenCode AI API (JavaScript)

Source: https://opencode.ai/docs/de/sdk

Illustrates how to search for text within files, find files and directories by name, and read the content of a specific file using the OpenCode AI client. Supports various query parameters for file searching.

```javascript
// Search and read files
const textResults = await client.find.text({
  query: { pattern: "function.*opencode" },
})

const files = await client.find.files({
  query: { query: "*.ts", type: "file" },
})

const directories = await client.find.files({
  query: { query: "packages", type: "directory", limit: 20 },
})

const content = await client.file.read({
  query: { path: "src/index.ts" },
})
```

--------------------------------

### Project APIs

Source: https://opencode.ai/docs/server

Endpoints for managing and retrieving project information.

```APIDOC
## GET /project

### Description
List all available projects.

### Method
GET

### Endpoint
/project

### Response
#### Success Response (200)
- **Project[]** (array) - An array of project objects.

#### Response Example
```json
[
  {
    "id": "project-1",
    "name": "Example Project"
  }
]
```

## GET /project/current

### Description
Get information about the currently active project.

### Method
GET

### Endpoint
/project/current

### Response
#### Success Response (200)
- **Project** (object) - The current project object.

#### Response Example
```json
{
  "id": "project-1",
  "name": "Example Project"
}
```
```

--------------------------------

### Tools API (Experimental)

Source: https://opencode.ai/docs/server

Experimental endpoints for listing and retrieving tool information.

```APIDOC
## GET /experimental/tool/ids

### Description
List all tool IDs.

### Method
GET

### Endpoint
/experimental/tool/ids

### Response
#### Success Response (200)
- **ToolIDs** - An object containing a list of tool IDs.

#### Response Example
{
  "ids": [
    "tool_1",
    "tool_2"
  ]
}

## GET /experimental/tool?provider=<p>&model=<m>

### Description
List tools with JSON schemas for a model.

### Method
GET

### Endpoint
/experimental/tool

### Query Parameters
- **provider** (string) - Required - The tool provider.
- **model** (string) - Required - The model to list tools for.

### Response
#### Success Response (200)
- **ToolList** - A list of tools with their JSON schemas.

#### Response Example
{
  "tools": [
    {
      "id": "tool_1",
      "name": "Calculator",
      "description": "Performs calculations.",
      "schema": {
        "type": "object",
        "properties": {
          "operation": {"type": "string", "enum": ["add", "subtract"]},
          "operands": {"type": "array", "items": {"type": "number"}}
        },
        "required": ["operation", "operands"]
      }
    }
  ]
}
```

--------------------------------

### List Available Models

Source: https://opencode.ai/docs/cli

Retrieves a list of all available models from configured providers. Optionally, it can filter models by a specific provider. This command is essential for identifying the correct model names for use in configurations.

```bash
opencode models [provider]
```

```bash
opencode models anthropic
```

```bash
opencode models --refresh
```

--------------------------------

### List All Models

Source: https://opencode.ai/docs/zen

Endpoint to retrieve a list of all available models and their metadata.

```APIDOC
## GET /zen/v1/models

### Description
Fetches a comprehensive list of all available AI models supported by OpenCode AI, including their IDs and metadata.

### Method
GET

### Endpoint
`https://opencode.ai/zen/v1/models`

### Parameters
None

### Response
#### Success Response (200)
- **models** (array) - An array of model objects.
  - **id** (string) - The unique identifier for the model.
  - **name** (string) - The human-readable name of the model.
  - **description** (string) - A brief description of the model's capabilities.

#### Response Example
```json
[
  {
    "id": "gpt-5.2",
    "name": "GPT 5.2",
    "description": "OpenAI GPT 5.2 model."
  },
  {
    "id": "claude-opus-4-6",
    "name": "Claude Opus 4.6",
    "description": "Anthropic Claude Opus 4.6 model."
  },
  {
    "id": "gemini-3.1-pro",
    "name": "Gemini 3.1 Pro",
    "description": "Google Gemini 3.1 Pro model."
  }
]
```
```

--------------------------------

### Configure Agent Description in JSON

Source: https://opencode.ai/docs/agents

Sets a brief description for an agent within the `opencode.json` configuration file. This option is required for defining an agent's purpose.

```json
{
  "agent": {
    "review": {
      "description": "Reviews code for best practices and potential issues"
    }
  }
}
```

--------------------------------

### Path and VCS APIs

Source: https://opencode.ai/docs/server

Endpoints for retrieving the current path and Version Control System (VCS) information.

```APIDOC
## GET /path

### Description
Get the current working path.

### Method
GET

### Endpoint
/path

### Response
#### Success Response (200)
- **Path** (object) - The current path information.

#### Response Example
```json
{
  "path": "/path/to/current/directory"
}
```

## GET /vcs

### Description
Get Version Control System (VCS) information for the current project.

### Method
GET

### Endpoint
/vcs

### Response
#### Success Response (200)
- **VcsInfo** (object) - The VCS information for the project.

#### Response Example
```json
{
  "type": "git",
  "branch": "main",
  "commit": "abcdef123456"
}
```
```

--------------------------------

### Basic OpenCode Configuration

Source: https://opencode.ai/docs/formatters

This JSON snippet shows the basic structure for configuring formatters in an OpenCode project. The 'formatter' object is where all formatter-related settings are defined.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "formatter": {}
}
```

--------------------------------

### Select Model via Command Line in OpenCode

Source: https://opencode.ai/docs/providers

Use the `/models` command in OpenCode to list and select available models. This command is used after configuring the provider and authentication.

```text
/models
```

--------------------------------

### Connect to SAP AI Core

Source: https://opencode.ai/docs/providers

Connects to SAP AI Core by running the /connect command and entering the service key JSON obtained from the SAP BTP Cockpit. Alternatively, the service key can be set as an environment variable.

```txt
/connect
```

```txt
┌ Service key
│
│
└ enter
```

--------------------------------

### Switch to Plan Mode

Source: https://opencode.ai/docs/index

Represents pressing the Tab key to switch OpenCode into 'Plan mode'. In this mode, OpenCode suggests changes without implementing them, allowing for review and iteration.

```text
<TAB>
```

--------------------------------

### POST /session/:id/permissions/:permissionID

Source: https://opencode.ai/docs/server

Responds to a permission request.  Allows granting or denying permissions for the session.

```APIDOC
## POST /session/:id/permissions/:permissionID

### Description
Respond to a permission request.

### Method
POST

### Endpoint
/session/:id/permissions/:permissionID

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.
- **permissionID** (string) - Required - The ID of the permission.

#### Request Body
- **response** (boolean) - Required - The response to the permission request.
- **remember** (boolean) - Optional - Whether to remember the response.

### Request Example
{
  "response": true,
  "remember": true
}

### Response
#### Success Response (200)
- **boolean** - True if the response was successfully processed.

#### Response Example
true

```

--------------------------------

### Define Agents with Markdown

Source: https://opencode.ai/docs/agents

Allows agent configuration using Markdown files, specifying description, mode, model, temperature, and tools. The filename determines the agent name. This offers an alternative to JSON configuration.

```markdown
---
description: Reviews code for quality and best practices
mode: subagent
model: anthropic/claude-sonnet-4-20250514
temperature: 0.1
tools:
  write: false
  edit: false
  bash: false
---

You are in code review mode. Focus on:

- Code quality and best practices
- Potential bugs and edge cases
- Performance implications
- Security considerations

Provide constructive feedback without making direct changes.
```

--------------------------------

### POST /session/:id/summarize

Source: https://opencode.ai/docs/server

Summarizes the session using a specified provider and model.  This endpoint generates a summary of the session's content.

```APIDOC
## POST /session/:id/summarize

### Description
Summarize the session.

### Method
POST

### Endpoint
/session/:id/summarize

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.

#### Request Body
- **providerID** (string) - Required - The ID of the provider.
- **modelID** (string) - Required - The ID of the model.

### Request Example
{
  "providerID": "provider1",
  "modelID": "model1"
}

### Response
#### Success Response (200)
- **boolean** - True if the summarization was successful.

#### Response Example
true

```

--------------------------------

### LSP, Formatters & MCP Endpoints

Source: https://opencode.ai/docs/server

Endpoints for retrieving the status of LSP servers, formatters, and MCP servers, as well as dynamically adding MCP servers.

```APIDOC
## GET /lsp

### Description
Get LSP server status.

### Method
GET

### Endpoint
/lsp

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **LSPStatus[]** (array) - An array of LSP server status objects.

#### Response Example
```json
[
  {
    "name": "lsp-server-1",
    "status": "running",
    "version": "1.0.0"
  }
]
```

## GET /formatter

### Description
Get formatter status.

### Method
GET

### Endpoint
/formatter

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **FormatterStatus[]** (array) - An array of formatter status objects.

#### Response Example
```json
[
  {
    "name": "prettier",
    "status": "enabled",
    "version": "2.8.8"
  }
]
```

## GET /mcp

### Description
Get MCP server status.

### Method
GET

### Endpoint
/mcp

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **{ [name: string]: MCPStatus }** (object) - An object where keys are MCP server names and values are their status objects.

#### Response Example
```json
{
  "mcp-server-1": {
    "status": "active",
    "config": {
      "topic": "/mcp/topic/1"
    }
  }
}
```

## POST /mcp

### Description
Add MCP server dynamically.

### Method
POST

### Endpoint
/mcp

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **name** (string) - Required - The name of the MCP server.
- **config** (object) - Required - The configuration object for the MCP server.

### Request Example
```json
{
  "name": "new-mcp-server",
  "config": {
    "topic": "/mcp/new/topic"
  }
}
```

### Response
#### Success Response (200)
- **MCPStatus** (object) - The status object of the newly added MCP server.

#### Response Example
```json
{
  "status": "active",
  "config": {
    "topic": "/mcp/new/topic"
  }
}
```
```

--------------------------------

### Access OpenAPI Specification

Source: https://opencode.ai/docs/server

The server publishes an OpenAPI 3.1 specification that can be viewed at the `/doc` endpoint. This spec is useful for generating clients, inspecting request/response types, or using Swagger explorers.

```bash
http://<hostname>:<port>/doc
```

--------------------------------

### Log Entry and List Agents with JavaScript

Source: https://opencode.ai/docs/sdk

Shows two common `app` API operations: writing a log entry using `app.log()` and retrieving a list of available agents with `app.agents()`. The log entry requires a structured body, while agents returns an array of Agent objects.

```javascript
// Write a log entry
await client.app.log({
  body: {
    service: "my-app",
    level: "info",
    message: "Operation completed",
  },
})

// List available agents
const agents = await client.app.agents()
```

--------------------------------

### Session Analysis and Initialization

Source: https://opencode.ai/docs/de/sdk

Endpoints for initializing session analysis and aborting running sessions.

```APIDOC
## POST /session/init

### Description
Analyzes an application within a session and creates an `AGENTS.md` file.

### Method
POST

### Endpoint
/session/init

### Parameters
#### Query Parameters
- **path** (string) - Required - The unique identifier for the session.
#### Request Body
- **body** (object) - Required - Initialization payload. (Structure depends on specific initialization needs)

### Request Example
```json
{
  "appPath": "/path/to/your/app"
}
```

### Response
#### Success Response (200)
- **result** (boolean) - True if initialization was successful, false otherwise.

#### Response Example
```json
true
```

## POST /session/abort

### Description
Aborts a currently running session.

### Method
POST

### Endpoint
/session/abort

### Parameters
#### Query Parameters
- **path** (string) - Required - The unique identifier for the session to abort.

### Request Example
```
/session/abort?path=session-123
```

### Response
#### Success Response (200)
- **result** (boolean) - True if the session was aborted successfully, false otherwise.

#### Response Example
```json
true
```
```

--------------------------------

### Files API

Source: https://opencode.ai/docs/server

Endpoints for searching, retrieving, and managing files and directories within the workspace.

```APIDOC
## GET /find?pattern=<pat>

### Description
Search for text in files.

### Method
GET

### Endpoint
/find

### Query Parameters
- **pattern** (string) - Required - The text pattern to search for.

### Response
#### Success Response (200)
- Array of match objects with `path`, `lines`, `line_number`, `absolute_offset`, `submatches`.

#### Response Example
[
  {
    "path": "src/main.js",
    "lines": [
      "console.log('Hello');"
    ],
    "line_number": 10,
    "absolute_offset": 150,
    "submatches": [
      {
        "text": "Hello",
        "start": 12,
        "end": 17
      }
    ]
  }
]

## GET /find/file?query=<q>

### Description
Find files and directories by name.

### Method
GET

### Endpoint
/find/file

### Query Parameters
- **query** (string) - Required - Search string (fuzzy match).
- **type** (string) - Optional - Limit results to "file" or "directory".
- **directory** (string) - Optional - Override the project root for the search.
- **limit** (integer) - Optional - Max results (1–200).
- **dirs** (string) - Optional - Legacy flag ("false" returns only files).

### Response
#### Success Response (200)
- **string[]** - An array of file and directory paths.

#### Response Example
[
  "src/components/Button.jsx",
  "public/index.html"
]

## GET /find/symbol?query=<q>

### Description
Find workspace symbols.

### Method
GET

### Endpoint
/find/symbol

### Query Parameters
- **query** (string) - Required - The symbol name to search for.

### Response
#### Success Response (200)
- **Symbol[]** - An array of symbol objects.

#### Response Example
[
  {
    "name": "App",
    "kind": "class",
    "location": {
      "uri": "file:///path/to/App.js",
      "range": {
        "start": {"line": 10, "character": 0},
        "end": {"line": 50, "character": 0}
      }
    }
  }
]

## GET /file?path=<path>

### Description
List files and directories.

### Method
GET

### Endpoint
/file

### Query Parameters
- **path** (string) - Required - The path to list files and directories from.

### Response
#### Success Response (200)
- **FileNode[]** - An array of file and directory nodes.

#### Response Example
[
  {
    "name": "src",
    "type": "directory",
    "children": [
      {
        "name": "index.js",
        "type": "file"
      }
    ]
  }
]

## GET /file/content?path=<p>

### Description
Read a file.

### Method
GET

### Endpoint
/file/content

### Query Parameters
- **path** (string) - Required - The path to the file.

### Response
#### Success Response (200)
- **FileContent** - The content of the file.

#### Response Example
{
  "content": "console.log('Hello, world!');",
  "contentType": "text/javascript"
}

## GET /file/status

### Description
Get status for tracked files.

### Method
GET

### Endpoint
/file/status

### Response
#### Success Response (200)
- **File[]** - An array of file status objects.

#### Response Example
[
  {
    "path": "src/main.js",
    "status": "modified"
  }
]
```

--------------------------------

### Project API

Source: https://opencode.ai/docs/sdk

Manages projects, allowing listing all projects and retrieving the current project.

```APIDOC
## GET /projects

### Description
Lists all available projects.

### Method
GET

### Endpoint
/projects

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **projects** (Project[]) - An array of projects.

#### Response Example
```json
[
  {
    "id": "project-1",
    "name": "My Project"
  }
]
```

## GET /project/current

### Description
Retrieves the currently active project.

### Method
GET

### Endpoint
/project/current

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **project** (Project) - The current project object.

#### Response Example
```json
{
  "id": "project-1",
  "name": "My Project"
}
```
```

--------------------------------

### Loading a Skill via Tool

Source: https://opencode.ai/docs/skills

Demonstrates the JavaScript code used by an agent to load a specific skill by its name using the `skill` tool.

```javascript
skill({ name: "git-release" })

```

--------------------------------

### Agents API

Source: https://opencode.ai/docs/server

Endpoint for listing all available agents.

```APIDOC
## GET /agent

### Description
List all available agents.

### Method
GET

### Endpoint
/agent

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **Agent[]** (array) - An array of agent objects.

#### Response Example
```json
[
  {
    "name": "agent-1",
    "version": "1.0"
  }
]
```
```

--------------------------------

### Manage Model Context Protocol (MCP) Servers

Source: https://opencode.ai/docs/cli

Commands for managing Model Context Protocol (MCP) servers, including adding new servers, listing existing ones, and authenticating with OAuth-enabled servers.

```bash
opencode mcp [command]
opencode mcp add
opencode mcp list
opencode mcp ls
opencode mcp auth [name]
opencode mcp auth list
opencode mcp auth ls
```

--------------------------------

### Use Context7 MCP Server in Prompt (Text)

Source: https://opencode.ai/docs/mcp-servers

This text prompt demonstrates how to instruct an agent to use the Context7 MCP server for tasks like configuring a Cloudflare Worker script. It specifies the desired action and the tool.

```text
Configure a Cloudflare Worker script to cache JSON API responses for five minutes. use context7
```

--------------------------------

### Connect to Moonshot AI

Source: https://opencode.ai/docs/providers

Instructions to connect OpenCode with Moonshot AI. This involves obtaining an API key from the Moonshot AI console and then using the `/connect` command within OpenCode to register the provider and API key.

```text
/connect

```

--------------------------------

### Enable webfetch tool in opencode.json

Source: https://opencode.ai/docs/de/tools

This JSON configuration snippet enables the 'webfetch' tool in OpenCode AI, allowing the LLM to retrieve and read content from web pages. This is useful for accessing online documentation or researching information. The configuration sets the 'webfetch' permission to 'allow'.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "webfetch": "allow"
  }
}
```

--------------------------------

### Docs API

Source: https://opencode.ai/docs/server

Endpoint for retrieving the OpenAPI 3.1 specification.

```APIDOC
## GET /doc

### Description
OpenAPI 3.1 specification.

### Method
GET

### Endpoint
/doc

### Parameters
None

### Response
#### Success Response (200)
- **HTML page with OpenAPI spec** (html) - An HTML page displaying the OpenAPI 3.1 specification.

#### Response Example
```html
<!DOCTYPE html>
<html>
<head>
  <title>OpenAPI Specification</title>
</head>
<body>
  <h1>OpenAPI 3.1 Specification</h1>
  <pre>...</pre>
</body>
</html>
```
```

--------------------------------

### Logging API

Source: https://opencode.ai/docs/server

Endpoint for writing log entries to the system.

```APIDOC
## POST /log

### Description
Write log entry. Body: `{ service, level, message, extra? }`

### Method
POST

### Endpoint
/log

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **service** (string) - Required - The service name for the log entry.
- **level** (string) - Required - The log level (e.g., 'info', 'warn', 'error').
- **message** (string) - Required - The log message.
- **extra** (object) - Optional - Additional key-value pairs for the log entry.

### Request Example
```json
{
  "service": "my-app",
  "level": "info",
  "message": "User logged in",
  "extra": {
    "userId": "123"
  }
}
```

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the log entry was written successfully.

#### Response Example
```json
true
```
```

--------------------------------

### Prompting and File Referencing in OpenCode

Source: https://opencode.ai/docs/de/tui

Demonstrates how to interact with OpenCode by sending messages and referencing files. File content is automatically added to the conversation when referenced using the '@' symbol.

```text
Give me a quick summary of the codebase.
@packages/functions/src/api/index.ts
How is auth handled in @packages/functions/src/api/index.ts?
```

--------------------------------

### Path API

Source: https://opencode.ai/docs/sdk

Provides information about the current path.

```APIDOC
## GET /path

### Description
Gets the current path information.

### Method
GET

### Endpoint
/path

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **path** (Path) - The current path object.

#### Response Example
```json
{
  "current": "/usr/local/bin"
}
```
```

--------------------------------

### Enable Exa AI websearch with environment variable

Source: https://opencode.ai/docs/de/tools

This bash command demonstrates how to enable the 'websearch' tool, powered by Exa AI, when launching OpenCode. Setting the OPENCODE_ENABLE_EXA environment variable to a truthy value like '1' activates this functionality, which is useful for real-time web searches.

```bash
OPENCODE_ENABLE_EXA=1 opencode
```

--------------------------------

### Connect to Azure OpenAI with Opencode

Source: https://opencode.ai/docs/providers

Instructions to connect Opencode AI to Azure OpenAI. This involves creating an Azure OpenAI resource, deploying a model, and configuring Opencode with the resource name and API key.

```bash
AZURE_RESOURCE_NAME=XXX opencode
```

```bash
export AZURE_RESOURCE_NAME=XXX
```

--------------------------------

### JavaScript Configuration for typesUrl

Source: https://opencode.ai/docs/server

This JavaScript code snippet defines the URL for type definitions, likely used for generating SDKs or interacting with the API. It constructs the URL using a configuration object.

```javascript
import config from "../../../config.mjs"
export const typesUrl = `${config.github}/blob/dev/packages/sdk/js/src/gen/types.gen.ts`
```

--------------------------------

### Configure OAuth for Self-Hosted GitLab

Source: https://opencode.ai/docs/providers

Sets up OAuth for self-hosted GitLab instances by defining the client ID environment variable. This requires creating a new application in GitLab settings with specific scopes and a callback URL.

```bash
export GITLAB_OAUTH_CLIENT_ID=your_application_id_here
```

--------------------------------

### Connect to OpenCode Provider

Source: https://opencode.ai/docs/index

Initiates the connection process to an LLM provider within the OpenCode TUI. This command is used to link OpenCode with your chosen AI model.

```bash
/connect
```

--------------------------------

### Control TUI Interface with JavaScript

Source: https://opencode.ai/docs/sdk

Demonstrates how to append text to the prompt and display a success toast notification using the TUI control methods. Requires the OpenCode AI client library.

```javascript
await client.tui.appendPrompt({
  body: { text: "Add this to prompt" },
})

await client.tui.showToast({
  body: { message: "Task completed", variant: "success" },
})
```

--------------------------------

### Navigate to Project Directory

Source: https://opencode.ai/docs/index

Changes the current directory to the specified project path. This is a standard shell command used before initializing or running OpenCode within a project.

```bash
cd /path/to/project
```

--------------------------------

### Configure Temperature and Prompt for Modes

Source: https://opencode.ai/docs/modes

Configures 'temperature' and 'prompt' settings for 'analyze', 'build', and 'brainstorm' modes in opencode.json. This allows for fine-tuning AI behavior and specifying custom system prompts for each mode.

```json
{
  "mode": {
    "analyze": {
      "temperature": 0.1,
      "prompt": "{file:./prompts/analysis.txt}"
    },
    "build": {
      "temperature": 0.3
    },
    "brainstorm": {
      "temperature": 0.7,
      "prompt": "{file:./prompts/creative.txt}"
    }
  }
}
```

--------------------------------

### Configure Local MCP Server in OpenCode

Source: https://opencode.ai/docs/mcp-servers

Illustrates how to configure a local MCP server in `opencode.jsonc`. It specifies the server type as 'local', provides the command to execute (e.g., using `npx`), and allows setting environment variables. This enables running local tools alongside the LLM.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-local-mcp-server": {
      "type": "local",
      // Or ["bun", "x", "my-mcp-command"]
      "command": ["npx", "-y", "my-mcp-command"],
      "enabled": true,
      "environment": {
        "MY_ENV_VAR": "my_env_var_value"
      }
    }
  }
}
```

--------------------------------

### Global APIs

Source: https://opencode.ai/docs/server

Endpoints for checking server health and subscribing to global events.

```APIDOC
## GET /global/health

### Description
Get server health and version information.

### Method
GET

### Endpoint
/global/health

### Response
#### Success Response (200)
- **healthy** (boolean) - Indicates if the server is healthy.
- **version** (string) - The current version of the server.

#### Response Example
```json
{
  "healthy": true,
  "version": "1.0.0"
}
```

## GET /global/event

### Description
Get global events as a Server-Sent Events (SSE) stream.

### Method
GET

### Endpoint
/global/event

### Response
#### Success Response (200)
- **Event stream** - A stream of events.

#### Response Example
(SSE stream format)
```

--------------------------------

### Command with Arguments Placeholder

Source: https://opencode.ai/docs/commands

Define custom commands that accept arguments using the $ARGUMENTS placeholder in the prompt. This allows dynamic input to tailor the command's execution. Positional parameters like $1, $2, etc., can also be used for specific argument access.

```markdown
---
description: Create a new component
---

Create a new React component named $ARGUMENTS with TypeScript support.
Include proper typing and basic structure.
```

--------------------------------

### Config API

Source: https://opencode.ai/docs/server

Endpoints for retrieving and updating configuration information, as well as listing available providers and their default models.

```APIDOC
## GET /config

### Description
Get the current configuration information.

### Method
GET

### Endpoint
/config

### Parameters
#### Query Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **config** (Config) - The configuration object.

#### Response Example
```json
{
  "config": {
    "setting1": "value1",
    "setting2": "value2"
  }
}
```

## PATCH /config

### Description
Update the configuration settings.

### Method
PATCH

### Endpoint
/config

### Parameters
#### Query Parameters
None

#### Request Body
- **config** (Config) - The configuration object to update.

### Request Example
```json
{
  "config": {
    "setting1": "new_value1"
  }
}
```

### Response
#### Success Response (200)
- **config** (Config) - The updated configuration object.

#### Response Example
```json
{
  "config": {
    "setting1": "new_value1",
    "setting2": "value2"
  }
}
```

## GET /config/providers

### Description
List all available providers and their default models.

### Method
GET

### Endpoint
/config/providers

### Parameters
#### Query Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **providers** (Provider[]) - An array of available providers.
- **default** (object) - An object mapping provider keys to their default model identifiers.

#### Response Example
```json
{
  "providers": [
    {
      "id": "provider1",
      "name": "Provider One"
    }
  ],
  "default": {
    "provider1": "modelA"
  }
}
```
```

--------------------------------

### App API

Source: https://opencode.ai/docs/sdk

Allows for application-level operations like writing logs and listing agents.

```APIDOC
## POST /app/log

### Description
Writes a log entry to the application.

### Method
POST

### Endpoint
/app/log

### Parameters
#### Query Parameters
None

#### Request Body
- **service** (string) - The name of the service writing the log.
- **level** (string) - The log level (e.g., 'info', 'warn', 'error').
- **message** (string) - The log message content.

### Response
#### Success Response (200)
- **success** (boolean) - Indicates if the log entry was written successfully.

#### Response Example
```json
{
  "success": true
}
```

## GET /app/agents

### Description
Lists all available agents.

### Method
GET

### Endpoint
/app/agents

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **agents** (Agent[]) - An array of available agents.

#### Response Example
```json
[
  {
    "id": "agent-1",
    "name": "Default Agent"
  }
]
```
```

--------------------------------

### Replace Session Compaction Prompt

Source: https://opencode.ai/docs/plugins

This plugin replaces the entire default compaction prompt with a custom one. It sets the 'output.prompt' property within the 'experimental.session.compacting' hook to define a new structure for summarizing session details, including task status, file modifications, blockers, and next steps. This offers complete control over the compaction output.

```typescript
import type { Plugin } from "@opencode-ai/plugin"

export const CustomCompactionPlugin: Plugin = async (ctx) => {
  return {
    "experimental.session.compacting": async (input, output) => {
      // Replace the entire compaction prompt
      output.prompt = `
You are generating a continuation prompt for a multi-agent swarm session.

Summarize:
1. The current task and its status
2. Which files are being modified and by whom
3. Any blockers or dependencies between agents
4. The next steps to complete the work

Format as a structured prompt that a new agent can use to resume work.
`
    },
  }
}
```

--------------------------------

### POST /session/:id/share

Source: https://opencode.ai/docs/server

Shares a session.  This action makes the session accessible to others.

```APIDOC
## POST /session/:id/share

### Description
Share a session.

### Method
POST

### Endpoint
/session/:id/share

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to share.

### Request Example
No request body.

### Response
#### Success Response (200)
- **Session** - The updated Session object.

#### Response Example
{
  "id": "session1",
  "title": "Shared Session",
  // ... other session properties
}

```

--------------------------------

### Reference External Files in opencode.json

Source: https://opencode.ai/docs/rules

This JSON configuration shows how to use the 'instructions' field in opencode.json to reference external files. This is the recommended approach for managing instructions across different parts of your project or from shared repositories.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["docs/development-standards.md", "test/testing-guidelines.md", "packages/*/AGENTS.md"]
}
```

--------------------------------

### Executing Shell Commands in OpenCode

Source: https://opencode.ai/docs/de/tui

Shows how to execute shell commands directly within the OpenCode TUI by prefixing the command with '!'. The output of the command is displayed as a tool result in the conversation.

```bash
!ls -la
```

--------------------------------

### Limit Agent Iterations with Max Steps (JSON)

Source: https://opencode.ai/docs/agents

Controls the maximum number of iterations an agent can perform before outputting text only, using the `steps` configuration in `opencode.json`. This helps manage costs by limiting agentic actions.

```json
{
  "agent": {
    "quick-thinker": {
      "description": "Fast reasoning with limited iterations",
      "prompt": "You are a quick thinker. Solve problems with minimal steps.",
      "steps": 5
    }
  }
}
```

--------------------------------

### Configure Avante.nvim for OpenCode ACP

Source: https://opencode.ai/docs/acp

Set up Avante.nvim to use OpenCode as an ACP provider. This involves defining the command and arguments for OpenCode in your Neovim configuration. Environment variables, such as an API key, can also be passed.

```lua
{
  acp_providers = {
    ["opencode"] = {
      command = "opencode",
      args = { "acp" }
    }
  }
}
```

```lua
{
  acp_providers = {
    ["opencode"] = {
      command = "opencode",
      args = { "acp" },
      env = {
        OPENCODE_API_KEY = os.getenv("OPENCODE_API_KEY")
      }
    }
  }
}
```

--------------------------------

### Import Configuration and Export Constants (JavaScript)

Source: https://opencode.ai/docs/zen

This snippet imports configuration settings and exports constants for console and email. It assumes a config.mjs file exists in the parent directory.

```javascript
import config from "../../../config.mjs"
export const console = config.console
export const email = `mailto:${config.email}`
```

--------------------------------

### Configure GitLab Duo Connection

Source: https://opencode.ai/docs/providers

Connects to GitLab Duo, supporting both OAuth and Personal Access Token authentication. It allows selection of Claude-based models and provides configuration options for self-hosted instances.

```txt
/connect
```

```txt
┌ Select auth method
│
│ OAuth (Recommended)
│ Personal Access Token
└
```

```txt
/models
```

--------------------------------

### Session Analysis and Control API

Source: https://opencode.ai/docs/sdk

Endpoints for initializing, aborting, and summarizing sessions.

```APIDOC
## POST /sessions/{path}/init

### Description
Analyzes an application and creates an `AGENTS.md` file for the session.

### Method
POST

### Endpoint
/sessions/{path}/init

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session.
#### Request Body
- **body** (object) - Required - The initialization payload.

### Request Example
```json
{
  "appPath": "/path/to/app"
}
```

### Response
#### Success Response (200)
- **result** (boolean) - True if initialization was successful, false otherwise.

#### Response Example
```json
{
  "result": true
}
```

## POST /sessions/{path}/abort

### Description
Aborts a currently running session.

### Method
POST

### Endpoint
/sessions/{path}/abort

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session to abort.

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **result** (boolean) - True if the session was aborted successfully, false otherwise.

#### Response Example
```json
{
  "result": true
}
```

## POST /sessions/{path}/summarize

### Description
Summarizes the content of a session.

### Method
POST

### Endpoint
/sessions/{path}/summarize

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session to summarize.
#### Request Body
- **body** (object) - Optional - Payload for summarization, if any.

### Request Example
```json
{
  "options": "detailed"
}
```

### Response
#### Success Response (200)
- **result** (boolean) - True if summarization was successful, false otherwise.

#### Response Example
```json
{
  "result": true
}
```
```

--------------------------------

### Configure OpenCode Theme

Source: https://opencode.ai/docs/themes

This snippet shows how to set a specific theme for OpenCode in its configuration file. It assumes the configuration is in JSON format and specifies the 'theme' property.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "theme": "tokyonight"
}
```

--------------------------------

### GitHub Actions Workflow with Custom OpenCode Prompt for Pull Requests

Source: https://opencode.ai/docs/github

This GitHub Actions workflow demonstrates how to use OpenCode with a custom prompt to review pull requests. The prompt is configured to check for code quality issues, potential bugs, and suggest improvements, allowing for tailored code review criteria.

```yaml
- uses: anomalyco/opencode/github@latest
  with:
    model: anthropic/claude-sonnet-4-5
    prompt: |
      Review this pull request:
      - Check for code quality issues
      - Look for potential bugs
      - Suggest improvements
```

--------------------------------

### Control TUI Interface with OpenCode AI API (JavaScript)

Source: https://opencode.ai/docs/de/sdk

Shows how to interact with the Text User Interface (TUI) using the OpenCode AI client. This includes appending text to the prompt, displaying toast notifications, and other TUI control functions.

```javascript
// Control TUI interface
await client.tui.appendPrompt({
  body: { text: "Add this to prompt" },
})

await client.tui.showToast({
  body: { message: "Task completed", variant: "success" },
})
```

--------------------------------

### Configure opencode.json for GitLab Provider

Source: https://opencode.ai/docs/providers

This JSON configuration snippet sets up the opencode.json file to use the GitLab provider. It specifies the instance URL and enables feature flags for Duo Agent Platform.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "gitlab": {
      "options": {
        "instanceUrl": "https://gitlab.com",
        "featureFlags": {
          "duo_agent_platform_agentic_chat": true,
          "duo_agent_platform": true
        }
      }
    }
  }
}
```

--------------------------------

### POST /session/:id/fork

Source: https://opencode.ai/docs/server

Forks an existing session at a specified message.  Allows creating a new session based on a previous state.

```APIDOC
## POST /session/:id/fork

### Description
Fork an existing session at a message.

### Method
POST

### Endpoint
/session/:id/fork

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to fork.

#### Request Body
- **messageID** (string) - Optional - The ID of the message to fork from.

### Request Example
{
  "messageID": "message1"
}

### Response
#### Success Response (200)
- **Session** - The newly forked Session object.

#### Response Example
{
  "id": "session3",
  "title": "Forked Session",
  // ... other session properties
}

```

--------------------------------

### Configure Tool Permissions in opencode.json

Source: https://opencode.ai/docs/zh-tw/tools

This JSON configuration snippet demonstrates how to set permissions for various OpenCode tools within the opencode.json file. Permissions can be set to 'allow', 'deny', or 'ask' for individual tools or using wildcards for multiple tools.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "edit": "deny",
    "bash": "ask",
    "webfetch": "allow"
  }
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "mymcp_*": "ask"
  }
}
```

--------------------------------

### Command with File Reference

Source: https://opencode.ai/docs/commands

Include the content of specified files directly within the prompt using the '@' symbol followed by the filename. This enables commands to reference and analyze existing code or configuration files as part of the LLM's context.

```markdown
---
description: Review component
---

Review the component in @src/components/Button.tsx.
Check for performance issues and suggest improvements.
```

--------------------------------

### Provider API

Source: https://opencode.ai/docs/server

Endpoints for managing AI providers, including listing them, retrieving authentication methods, and handling OAuth authorization flows.

```APIDOC
## GET /provider

### Description
List all available providers, including default and connected providers.

### Method
GET

### Endpoint
/provider

### Parameters
#### Query Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **all** (Provider[]) - An array of all providers.
- **default** (object) - Default provider settings.
- **connected** (string[]) - An array of connected provider IDs.

#### Response Example
```json
{
  "all": [
    {
      "id": "provider1",
      "name": "Provider One"
    }
  ],
  "default": {
    "provider1": "modelA"
  },
  "connected": ["provider1"]
}
```

## GET /provider/auth

### Description
Get the authentication methods for each provider.

### Method
GET

### Endpoint
/provider/auth

### Parameters
#### Query Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **[providerID]** (ProviderAuthMethod[]) - An object where keys are provider IDs and values are arrays of their authentication methods.

#### Response Example
```json
{
  "provider1": [
    {
      "type": "oauth2",
      "client_id": "your_client_id"
    }
  ]
}
```

## POST /provider/{id}/oauth/authorize

### Description
Initiate the OAuth authorization flow for a specific provider.

### Method
POST

### Endpoint
/provider/{id}/oauth/authorize

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the provider to authorize.

#### Query Parameters
None

### Request Example
None (Authorization redirect is handled by the provider)

### Response
#### Success Response (200)
- **authorization_url** (string) - The URL to redirect the user to for authorization.

#### Response Example
```json
{
  "authorization_url": "https://example.com/oauth/authorize?client_id=..."
}
```

## POST /provider/{id}/oauth/callback

### Description
Handle the callback from the OAuth provider after user authorization.

### Method
POST

### Endpoint
/provider/{id}/oauth/callback

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the provider handling the callback.

#### Query Parameters
- **code** (string) - Required - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter used to prevent CSRF attacks.

### Request Example
None (Callback is typically a GET request with query parameters, but this endpoint is POST for simplicity in some frameworks)

### Response
#### Success Response (200)
- **success** (boolean) - True if the callback was handled successfully, false otherwise.

#### Response Example
```json
{
  "success": true
}
```
```

--------------------------------

### Adding a Custom LSP Server Configuration

Source: https://opencode.ai/docs/lsp

This JSON configuration illustrates how to add a custom LSP server to OpenCode. You define a unique name for your custom server (e.g., 'custom-lsp') and provide the `command` to execute it along with the `extensions` it should handle. This allows integration with any language server that follows the LSP protocol.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "lsp": {
    "custom-lsp": {
      "command": ["custom-lsp-server", "--stdio"],
      "extensions": [".custom"]
    }
  }
}
```

--------------------------------

### OpenCode Slash Commands

Source: https://opencode.ai/docs/de/tui

Lists various slash commands available in the OpenCode TUI for performing actions such as connecting providers, managing sessions, exporting conversations, and accessing help.

```bash
/connect
/compact
/details
/editor
/exit
/export
/help
/init
/models
/new
/redo
/sessions
/share
/theme
/thinking
/undo
/unshare
```

--------------------------------

### Select a Model in OpenCode

Source: https://opencode.ai/docs/models

This command allows users to select a model within the OpenCode environment. It's a simple interface for choosing the desired language model.

```bash
/models
```

--------------------------------

### Define Custom Command in Markdown

Source: https://opencode.ai/docs/commands

Create custom commands by defining markdown files in the 'commands/' directory. The frontmatter specifies command properties like description, agent, and model, while the content serves as the prompt template. The filename determines the command name.

```markdown
---
description: Run tests with coverage
agent: build
model: anthropic/claude-3-5-sonnet-20241022
---

Run the full test suite with coverage report and show any failures.
Focus on the failing tests and suggest fixes.
```

--------------------------------

### Configuration API

Source: https://opencode.ai/docs/de/server

Endpoints for retrieving and updating the website's configuration settings.

```APIDOC
## GET /config

### Description
Retrieves the current configuration information for the website.

### Method
GET

### Endpoint
/config

### Parameters
#### Path Parameters
None

#### Query Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **config** (Config) - The current configuration object.

#### Response Example
```json
{
  "config": {
    "someSetting": "value"
  }
}
```

## PATCH /config

### Description
Updates the website's configuration settings.

### Method
PATCH

### Endpoint
/config

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **config** (Config) - The configuration object with updated values.

### Request Example
```json
{
  "config": {
    "newSetting": "newValue"
  }
}
```

### Response
#### Success Response (200)
- **config** (Config) - The updated configuration object.

#### Response Example
```json
{
  "config": {
    "someSetting": "value",
    "newSetting": "newValue"
  }
}
```

## GET /config/providers

### Description
Lists available providers and their default models.

### Method
GET

### Endpoint
/config/providers

### Parameters
#### Path Parameters
None

#### Query Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **providers** (Provider[]) - An array of available provider objects.
- **default** (object) - An object mapping keys to default model strings.

#### Response Example
```json
{
  "providers": [
    {
      "id": "provider1",
      "name": "Provider One"
    }
  ],
  "default": {
    "provider1": "model-a"
  }
}
```
```

--------------------------------

### Session Management API

Source: https://opencode.ai/docs/de/sdk

APIs for creating, listing, and interacting with AI sessions, including sending prompts and injecting context.

```APIDOC
## POST /api/sessions/{id}/permissions/{permissionId}

### Description
Respond to a permission request for a specific session and permission.

### Method
POST

### Endpoint
`/api/sessions/{id}/permissions/{permissionId}`

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.
- **permissionId** (string) - Required - The ID of the permission.

### Request Body
(No specific request body documented, assumed to be empty or handled by the client library)

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the permission request was successfully responded to.

### Request Example
```javascript
// Assuming 'client' is an initialized Opencode AI client
// const response = await client.session.postSessionByIdPermissionsByPermissionId({
//   path: { id: "session-id", permissionId: "permission-id" },
//   body: {}
// });
```

## POST /api/sessions

### Description
Create a new AI session.

### Method
POST

### Endpoint
`/api/sessions`

### Parameters
#### Request Body
- **title** (string) - Required - The title for the new session.

### Response
#### Success Response (200)
- **session** (object) - The created session object, containing at least an `id`.

### Request Example
```javascript
const session = await client.session.create({ body: { title: "My session" } });
```

## GET /api/sessions

### Description
List all available AI sessions.

### Method
GET

### Endpoint
`/api/sessions`

### Parameters
(No parameters documented)

### Response
#### Success Response (200)
- **sessions** (array) - An array of session objects.

### Request Example
```javascript
const sessions = await client.session.list();
```

## POST /api/sessions/{id}/prompt

### Description
Send a prompt message to a specific AI session or inject context without a reply.

### Method
POST

### Endpoint
`/api/sessions/{id}/prompt`

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to send the prompt to.

#### Request Body
- **model** (object) - Optional - Specifies the AI model to use (e.g., `{ providerID: "anthropic", modelID: "claude-3-5-sonnet-20241022" }`).
- **parts** (array) - Required - An array of content parts, where each part can be text or other media types (e.g., `[{ type: "text", text: "Hello!" }]`).
- **noReply** (boolean) - Optional - If true, the AI will not generate a response. Useful for injecting context.

### Response
#### Success Response (200)
- (Response structure depends on whether `noReply` is true or false. If false, it will contain the AI's response.)

### Request Example
```javascript
// Sending a prompt and getting a response
const result = await client.session.prompt({
  path: { id: session.id },
  body: {
    model: { providerID: "anthropic", modelID: "claude-3-5-sonnet-20241022" },
    parts: [{ type: "text", text: "Hello!" }],
  },
});

// Injecting context without AI response
await client.session.prompt({
  path: { id: session.id },
  body: {
    noReply: true,
    parts: [{ type: "text", text: "You are a helpful assistant." }],
  },
});
```
```

--------------------------------

### Manage OpenCode Sessions

Source: https://opencode.ai/docs/cli

Provides commands for managing OpenCode sessions. This includes listing available sessions with options to filter and format the output.

```bash
opencode session [command]
```

```bash
opencode session list
```

--------------------------------

### Configure Custom Prompt for a Mode

Source: https://opencode.ai/docs/modes

Specifies a custom system prompt file for the 'review' mode in opencode.json. The path is relative to the configuration file's location, enabling tailored instructions for specific modes.

```json
{
  "mode": {
    "review": {
      "prompt": "{file:./prompts/code-review.txt}"
    }
  }
}
```

--------------------------------

### Connect to Scaleway Generative APIs with Opencode

Source: https://opencode.ai/docs/providers

This snippet shows how to connect Opencode to Scaleway's Generative APIs. It involves obtaining an API key from the Scaleway console and then using the `/connect` and `/models` commands in Opencode.

```txt
/connect

```

```txt
┌ API key
│
│
└ enter

```

```txt
/models

```

--------------------------------

### Enable websearch tool in opencode.json

Source: https://opencode.ai/docs/de/tools

This JSON configuration snippet enables the 'websearch' tool within OpenCode AI, utilizing Exa AI for web searches. It allows the LLM to find relevant information online, which is particularly useful when data goes beyond the training set. This tool requires specific provider configurations or environment variables.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "websearch": "allow"
  }
}
```

--------------------------------

### Connect to Cloudflare AI Gateway with Opencode

Source: https://opencode.ai/docs/providers

Instructions to connect Opencode AI to Cloudflare AI Gateway. This involves setting environment variables for Account ID and Gateway ID, and providing an API token.

```bash
export CLOUDFLARE_ACCOUNT_ID=your-32-character-account-id
export CLOUDFLARE_GATEWAY_ID=your-gateway-id
```

```txt
/connect
```

```txt
┌ API key
│
│
└ enter
```

```bash
export CLOUDFLARE_API_TOKEN=your-api-token
```

```txt
/models
```

--------------------------------

### Add Custom Models for ZenMux in Opencode Configuration

Source: https://opencode.ai/docs/providers

This JSON snippet demonstrates how to add custom models for the ZenMux provider in the opencode.json configuration file. This allows users to specify additional models beyond the defaults.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "zenmux": {
      "models": {
        "somecoolnewmodel": {}
      }
    }
  }
}

```

--------------------------------

### Enable Remote MCP Server from Organization Defaults

Source: https://opencode.ai/docs/mcp-servers

Shows how to enable a specific MCP server from an organization's remote configuration in the local `opencode.json` file. This allows users to opt-in to servers provided by their organization. Local configuration values override remote defaults.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "jira": {
      "type": "remote",
      "url": "https://jira.example.com/mcp",
      "enabled": true
    }
  }
}
```

--------------------------------

### Implement a Basic OpenCode Plugin in JavaScript

Source: https://opencode.ai/docs/plugins

This JavaScript code defines a basic OpenCode plugin. The plugin function receives a context object containing project details, a client for AI interaction, and Bun's shell API. It returns an object where keys are hook names (e.g., 'tool.execute.before') and values are asynchronous functions that modify behavior.

```javascript
export const MyPlugin = async ({ project, client, $, directory, worktree }) => {
  console.log("Plugin initialized!")

  return {
    // Hook implementations go here
  }
}
```

--------------------------------

### Configure Modes in opencode.json

Source: https://opencode.ai/docs/modes

Defines the 'build' and 'plan' modes with specific model, prompt, and tool configurations within the opencode.json file. This allows for granular control over AI behavior for different tasks.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mode": {
    "build": {
      "model": "anthropic/claude-sonnet-4-20250514",
      "prompt": "{file:./prompts/build.txt}",
      "tools": {
        "write": true,
        "edit": true,
        "bash": true
      }
    },
    "plan": {
      "model": "anthropic/claude-haiku-4-20250514",
      "tools": {
        "write": false,
        "edit": false,
        "bash": false
      }
    }
  }
}
```

--------------------------------

### Control Agent Tool Availability in opencode.json

Source: https://opencode.ai/docs/agents

Manage which tools are accessible to an agent by setting them to true or false in the opencode.json configuration. Agent-specific configurations override global settings. Wildcards can be used to control multiple tools simultaneously, such as disabling all tools from a specific server.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "tools": {
    "write": true,
    "bash": true
  },
  "agent": {
    "plan": {
      "tools": {
        "write": false,
        "bash": false
      }
    }
  }
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "agent": {
    "readonly": {
      "tools": {
        "mymcp_*": false,
        "write": false,
        "edit": false
      }
    }
  }
}
```

--------------------------------

### Built-in Agent Skill Permissions Override

Source: https://opencode.ai/docs/skills

Demonstrates how to set specific skill permissions for a built-in agent, such as 'plan', within the `opencode.json` configuration.

```json
{
  "agent": {
    "plan": {
      "permission": {
        "skill": {
          "internal-*": "allow"
        }
      }
    }
  }
}

```

--------------------------------

### Manage OpenCode Authentication

Source: https://opencode.ai/docs/cli

Handle authentication for various providers used by OpenCode. This includes logging in, listing authenticated providers, and logging out.

```bash
opencode auth [command]
opencode auth login
opencode auth list
opencode auth ls
opencode auth logout
```

--------------------------------

### Configure Custom Instructions in opencode.json

Source: https://opencode.ai/docs/rules

This JSON configuration demonstrates how to specify custom instruction files within your opencode.json. It allows you to include multiple markdown files for instructions, including those from remote URLs.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["CONTRIBUTING.md", "docs/guidelines.md", ".cursor/rules/*.md"]
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": ["https://raw.githubusercontent.com/my-org/shared-rules/main/style.md"]
}
```

--------------------------------

### Documentation Agent Configuration

Source: https://opencode.ai/docs/agents

Configuration for a 'docs-writer' agent designed for writing and maintaining project documentation. It specifies 'subagent' mode and disables the 'bash' tool, focusing on clear explanations and proper structure.

```markdown
---

```

```markdown
description: Writes and maintains project documentation

```

```markdown
mode: subagent

```

```markdown
tools:
  bash: false

```

```markdown
---

```

```markdown

You are a technical writer. Create clear, comprehensive documentation.

```

```markdown

Focus on:

- Clear explanations
- Proper structure
- Code examples
- User-friendly language

```

--------------------------------

### Default .env File Permissions (JSON)

Source: https://opencode.ai/docs/permissions

Configure default permissions for file reading, specifically denying access to `.env` and `.env.*` files while allowing `.env.example` files.

```json
{
  "permission": {
    "read": {
      "*": "allow",
      "*.env": "deny",
      "*.env.*": "deny",
      "*.env.example": "allow"
    }
  }
}
```

--------------------------------

### Structured Logging with Client App Log

Source: https://opencode.ai/docs/plugins

This plugin shows how to use 'client.app.log()' for structured logging instead of 'console.log'. It logs an 'info' level message with service details and extra data. This provides more organized and detailed logs for debugging and monitoring.

```typescript
export const MyPlugin = async ({ client }) => {
  await client.app.log({
    body: {
      service: "my-plugin",
      level: "info",
      message: "Plugin initialized",
      extra: { foo: "bar" },
    },
  })
}
```

--------------------------------

### Google Gemini Endpoints

Source: https://opencode.ai/docs/zen

Endpoints for accessing Google's Gemini models.

```APIDOC
## GET /zen/v1/models/gemini-3.1-pro

### Description
This endpoint provides metadata for the Gemini 3.1 Pro model.

### Method
GET

### Endpoint
`https://opencode.ai/zen/v1/models/gemini-3.1-pro`

### Parameters
None

### Response
#### Success Response (200)
- **id** (string) - The model ID.
- **name** (string) - The model name.
- **description** (string) - A description of the model.

#### Response Example
```json
{
  "id": "gemini-3.1-pro",
  "name": "Gemini 3.1 Pro",
  "description": "Google's advanced multimodal large language model."
}
```
```

```APIDOC
## GET /zen/v1/models/gemini-3-pro

### Description
This endpoint provides metadata for the Gemini 3 Pro model.

### Method
GET

### Endpoint
`https://opencode.ai/zen/v1/models/gemini-3-pro`

### Parameters
None

### Response
#### Success Response (200)
- **id** (string) - The model ID.
- **name** (string) - The model name.
- **description** (string) - A description of the model.

#### Response Example
```json
{
  "id": "gemini-3-pro",
  "name": "Gemini 3 Pro",
  "description": "Google's multimodal large language model."
}
```
```

```APIDOC
## GET /zen/v1/models/gemini-3-flash

### Description
This endpoint provides metadata for the Gemini 3 Flash model.

### Method
GET

### Endpoint
`https://opencode.ai/zen/v1/models/gemini-3-flash`

### Parameters
None

### Response
#### Success Response (200)
- **id** (string) - The model ID.
- **name** (string) - The model name.
- **description** (string) - A description of the model.

#### Response Example
```json
{
  "id": "gemini-3-flash",
  "name": "Gemini 3 Flash",
  "description": "Google's fast and efficient multimodal large language model."
}
```
```

--------------------------------

### Enable LSP Tool in OpenCode

Source: https://opencode.ai/docs/tools

Grant 'allow' permission for the experimental 'lsp' tool in opencode.json. This enables interaction with Language Server Protocol servers for code intelligence features like definitions, references, and hover information.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "lsp": "allow"
  }
}
```

--------------------------------

### Configure HTTPS and HTTP Proxies with OpenCode

Source: https://opencode.ai/docs/network

Sets environment variables to define HTTPS and HTTP proxy servers for OpenCode. It also specifies local addresses to bypass the proxy, which is crucial for local server communication.

```bash
export HTTPS_PROXY=https://proxy.example.com:8080

export HTTP_PROXY=http://proxy.example.com:8080

export NO_PROXY=localhost,127.0.0.1
```

--------------------------------

### Granular Permissions with Object Syntax (JSON)

Source: https://opencode.ai/docs/permissions

Define granular permissions using an object syntax, allowing different actions based on tool input patterns. Rules are evaluated by pattern match, with the last matching rule taking precedence.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "bash": {
      "*": "ask",
      "git *": "allow",
      "npm *": "allow",
      "rm *": "deny",
      "grep *": "allow"
    },
    "edit": {
      "*": "deny",
      "packages/web/src/content/docs/*.mdx": "allow"
    }
  }
}
```

--------------------------------

### Configure OpenCode in GitLab CI Component

Source: https://opencode.ai/docs/gitlab

This snippet shows how to include the OpenCode CI component in your `.gitlab-ci.yml` file. It allows for custom configuration directories, authentication via environment variables, and passing custom commands or prompts.

```yaml
include:
  - component: $CI_SERVER_FQDN/nagyv/gitlab-opencode/opencode@2
    inputs:
      config_dir: ${CI_PROJECT_DIR}/opencode-config
      auth_json: $OPENCODE_AUTH_JSON # The variable name for your OpenCode authentication JSON
      command: optional-custom-command
      message: "Your prompt here"
```

--------------------------------

### Configure LM Studio for Local Models in OpenCode

Source: https://opencode.ai/docs/providers

This JSON configuration allows OpenCode to connect to local AI models served through LM Studio. It specifies the npm package for OpenAI compatibility, the local server's base URL, and maps local model IDs to display names.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "lmstudio": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "LM Studio (local)",
      "options": {
        "baseURL": "http://127.0.0.1:1234/v1"
      },
      "models": {
        "google/gemma-3n-e4b": {
          "name": "Gemma 3n-e4b (local)"
        }
      }
    }
  }
}
```

--------------------------------

### Import Session Data (Bash)

Source: https://opencode.ai/docs/cli

Imports session data from a JSON file or an OpenCode share URL. Supports both local file paths and remote URLs.

```bash
opencode import <file>
```

```bash
opencode import session.json
```

```bash
opencode import https://opncd.ai/s/abc123
```

--------------------------------

### Enable Skill Tool in OpenCode

Source: https://opencode.ai/docs/tools

Allow the 'skill' tool by setting its permission to 'allow' in opencode.json. This enables the LLM to load and process content from 'SKILL.md' files within your project.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "skill": "allow"
  }
}
```

--------------------------------

### Configure Task Permissions for Agents

Source: https://opencode.ai/docs/agents

Control which subagents an agent can invoke using the 'permission.task' setting with glob patterns. Rules are evaluated in order, with the last matching rule taking precedence. Denied agents are removed from the Task tool description.

```json
{
  "agent": {
    "orchestrator": {
      "mode": "primary",
      "permission": {
        "task": {
          "*": "deny",
          "orchestrator-*": "allow",
          "code-reviewer": "ask"
        }
      }
    }
  }
}
```

--------------------------------

### Connect to Azure Cognitive Services with Opencode

Source: https://opencode.ai/docs/providers

Instructions to connect Opencode AI to Azure Cognitive Services. This involves creating an Azure OpenAI resource, deploying a model, and configuring Opencode with the resource name and API key.

```bash
AZURE_COGNITIVE_SERVICES_RESOURCE_NAME=XXX opencode
```

```bash
export AZURE_COGNITIVE_SERVICES_RESOURCE_NAME=XXX
```

--------------------------------

### Configure npm Plugins in opencode.json

Source: https://opencode.ai/docs/plugins

This JSON configuration snippet shows how to specify npm packages to be used as OpenCode plugins. It lists the plugin names directly within the 'plugin' array in the opencode.json file. Both regular and scoped npm packages are supported.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["opencode-helicone-session", "opencode-wakatime", "@my-org/custom-plugin"]
}
```

--------------------------------

### Set Agent Mode in opencode.json

Source: https://opencode.ai/docs/agents

Control how an agent can be used by setting its mode to 'primary', 'subagent', or 'all' in the opencode.json configuration. If no mode is specified, it defaults to 'all'.

```json
{
  "agent": {
    "review": {
      "mode": "subagent"
    }
  }
}
```

--------------------------------

### OpenCode AI Commands for GitHub Issues and Pull Requests

Source: https://opencode.ai/docs/github

This section details various commands that can be used within GitHub issues and pull requests to interact with OpenCode AI. These commands allow users to request explanations, fixes, or specific code modifications directly through comments.

```text
/opencode explain this issue
/opencode fix this
Delete the attachment from S3 when the note is removed /oc
/oc add error handling here
```

--------------------------------

### Explain GitLab Issue using OpenCode AI (Command)

Source: https://opencode.ai/docs/gitlab

This is a command-line instruction to trigger OpenCode AI to explain a GitLab issue. The command is typically posted as a comment in a GitLab issue, prefixed with '@opencode'.

```shell
@opencode explain this issue
```

--------------------------------

### View OpenCode Statistics

Source: https://opencode.ai/docs/cli

Displays token usage and cost statistics for OpenCode sessions. This command helps users monitor their resource consumption and associated costs.

```bash
opencode stats
```

--------------------------------

### Configure Google Vertex AI Environment Variables

Source: https://opencode.ai/docs/providers

This bash snippet demonstrates how to set environment variables required for using Google Vertex AI with OpenCode. It includes project ID, optional location, and authentication credentials.

```bash
GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account.json GOOGLE_CLOUD_PROJECT=your-project-id opencode

# Or add to ~/.bash_profile:
export GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account.json
export GOOGLE_CLOUD_PROJECT=your-project-id
export VERTEX_LOCATION=global
```

--------------------------------

### File Search and Read API

Source: https://opencode.ai/docs/sdk

Endpoints for searching files and directories within the workspace and reading file content.

```APIDOC
## POST /api/find/text

### Description
Searches for text patterns within files in the workspace.

### Method
POST

### Endpoint
/api/find/text

### Parameters
#### Request Body
- **query** (object) - Required - The search query parameters.
  - **pattern** (string) - Required - The text pattern to search for.

### Request Example
```json
{
  "query": {
    "pattern": "function.*opencode"
  }
}
```

### Response
#### Success Response (200)
- **matches** (array) - An array of match objects.
  - **path** (string) - The path to the file where the match was found.
  - **lines** (array) - An array of lines containing the match.
  - **line_number** (integer) - The line number of the match.
  - **absolute_offset** (integer) - The absolute offset of the match within the file.
  - **submatches** (array) - Details about submatches within the line.

#### Response Example
```json
[
  {
    "path": "src/index.ts",
    "lines": [
      "function opencodeAI() {"
    ],
    "line_number": 10,
    "absolute_offset": 150,
    "submatches": [
      {
        "text": "opencodeAI",
        "start": 9,
        "length": 10
      }
    ]
  }
]
```

## POST /api/find/files

### Description
Finds files and directories by name within the workspace.

### Method
POST

### Endpoint
/api/find/files

### Parameters
#### Request Body
- **query** (object) - Required - The search query parameters.
  - **query** (string) - Required - The file or directory name pattern to search for.
  - **type** (string) - Optional - The type of item to find, either "file" or "directory".
  - **directory** (string) - Optional - The directory to start the search from, overriding the project root.
  - **limit** (integer) - Optional - The maximum number of results to return (1-200).

### Request Example
```json
{
  "query": {
    "query": "*.ts",
    "type": "file"
  }
}
```

### Response
#### Success Response (200)
- **paths** (array) - An array of strings, where each string is a path to a found file or directory.

#### Response Example
```json
[
  "src/index.ts",
  "src/utils/helpers.ts"
]
```

## POST /api/find/symbols

### Description
Finds workspace symbols (e.g., functions, classes, variables).

### Method
POST

### Endpoint
/api/find/symbols

### Parameters
#### Request Body
- **query** (object) - Required - The search query parameters.
  - **pattern** (string) - Required - The pattern to search for symbols.

### Request Example
```json
{
  "query": {
    "pattern": "myFunction"
  }
}
```

### Response
#### Success Response (200)
- **symbols** (array) - An array of symbol objects.
  - **name** (string) - The name of the symbol.
  - **kind** (string) - The type of the symbol (e.g., "function", "class").
  - **location** (object) - The location of the symbol in the workspace.
    - **path** (string) - The file path.
    - **range** (object) - The range within the file.
      - **start** (object) - Start position.
      - **end** (object) - End position.

#### Response Example
```json
[
  {
    "name": "myFunction",
    "kind": "function",
    "location": {
      "path": "src/myModule.ts",
      "range": {
        "start": {"line": 5, "character": 0},
        "end": {"line": 15, "character": 1}
      }
    }
  }
]
```

## POST /api/file/read

### Description
Reads the content of a specified file.

### Method
POST

### Endpoint
/api/file/read

### Parameters
#### Request Body
- **query** (object) - Required - The query parameters for reading the file.
  - **path** (string) - Required - The path to the file to read.

### Request Example
```json
{
  "query": {
    "path": "src/index.ts"
  }
}
```

### Response
#### Success Response (200)
- **type** (string) - The type of content, either "raw" or "patch".
- **content** (string) - The content of the file.

#### Response Example
```json
{
  "type": "raw",
  "content": "// This is the content of index.ts"
}
```

## POST /api/file/status

### Description
Gets the status for tracked files in the repository.

### Method
POST

### Endpoint
/api/file/status

### Parameters
#### Request Body
- **query** (object) - Optional - Query parameters for filtering file status.
  - **path** (string) - Optional - Filter status for a specific file path.

### Request Example
```json
{
  "query": {
    "path": "src/components/Button.tsx"
  }
}
```

### Response
#### Success Response (200)
- **files** (array) - An array of file status objects.
  - **path** (string) - The path of the file.
  - **status** (string) - The status of the file (e.g., "modified", "added", "untracked").

#### Response Example
```json
[
  {
    "path": "src/components/Button.tsx",
    "status": "modified"
  }
]
```
```

--------------------------------

### Authentication API

Source: https://opencode.ai/docs/de/sdk

API for setting authentication credentials for different providers.

```APIDOC
## POST /api/auth/{id}

### Description
Set authentication credentials for a specific provider.

### Method
POST

### Endpoint
`/api/auth/{id}`

### Parameters
#### Path Parameters
- **id** (string) - Required - The identifier of the authentication provider (e.g., `"anthropic"`).

#### Request Body
- **type** (string) - Required - The type of authentication (e.g., `"api"`).
- **key** (string) - Required - The API key or secret for the provider.

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the authentication credentials were set successfully.

### Request Example
```javascript
await client.auth.set({
  path: { id: "anthropic" },
  body: { type: "api", key: "your-api-key" },
});
```
```

--------------------------------

### Enable Grep Tool in OpenCode

Source: https://opencode.ai/docs/tools

Allow the 'grep' tool by setting its permission to 'allow' in opencode.json. This enables fast content searching across your codebase using regular expressions and supports filtering by file patterns.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "grep": "allow"
  }
}
```

--------------------------------

### Session Command and Shell Execution

Source: https://opencode.ai/docs/de/sdk

Endpoints for sending commands and executing shell commands within a session.

```APIDOC
## POST /session/command

### Description
Sends a command to a session.

### Method
POST

### Endpoint
/session/command

### Parameters
#### Query Parameters
- **path** (string) - Required - The unique identifier for the session.
#### Request Body
- **body** (object) - Required - The command payload.
  - **command** (string) - The command to execute.

### Request Example
```json
{
  "path": "session-123",
  "body": {
    "command": "list_files"
  }
}
```

### Response
#### Success Response (200)
- **response** (object) - The result of the command execution.
  - **info** (AssistantMessage) - The AI message metadata.
  - **parts** (Part[]) - An array of message parts.

#### Response Example
```json
{
  "info": {"id": "msg-ghi", "sender": "assistant"},
  "parts": [{"type": "text", "content": "Files listed successfully."}]
}
```

## POST /session/shell

### Description
Runs a shell command within a session.

### Method
POST

### Endpoint
/session/shell

### Parameters
#### Query Parameters
- **path** (string) - Required - The unique identifier for the session.
#### Request Body
- **body** (object) - Required - The shell command payload.
  - **command** (string) - The shell command to execute.

### Request Example
```json
{
  "path": "session-123",
  "body": {
    "command": "ls -l"
  }
}
```

### Response
#### Success Response (200)
- **response** (AssistantMessage) - The AI message containing the shell command output.

#### Response Example
```json
{
  "info": {"id": "msg-jkl", "sender": "assistant"},
  "parts": [{"type": "text", "content": "total 8\n-rw-r--r-- 1 user group 1024 Jan 1 10:00 file1.txt"}]
}
```
```

--------------------------------

### Events API

Source: https://opencode.ai/docs/server

Endpoint for streaming server-sent events, including connection events and bus events.

```APIDOC
## GET /event

### Description
Server-sent events stream. First event is `server.connected`, then bus events.

### Method
GET

### Endpoint
/event

### Parameters
None

### Response
#### Success Response (200)
- **Server-sent events stream** (stream) - A stream of server-sent events.

#### Response Example
```
event: server.connected
data: {"message": "Connected to event stream"}

event: some.bus.event
data: {"payload": "some data"}
```
```

--------------------------------

### Run OpenCode CLI Command

Source: https://opencode.ai/docs/cli

Execute OpenCode CLI commands to interact with the AI. The 'run' command allows specifying a task description to be processed by the AI.

```bash
opencode
opencode run "Explain how closures work in JavaScript"
```

--------------------------------

### Add SAP AI Core Service Key to Bash Profile

Source: https://opencode.ai/docs/providers

Adds the SAP AI Core service key to the ~/.bash_profile file, ensuring it is available as an environment variable for all opencode sessions.

```bash
export AICORE_SERVICE_KEY='{"clientid":"...","clientsecret":"...","url":"...","serviceurls":{"AI_API_URL":"..."}}'
```

--------------------------------

### Scheduled OpenCode Task using GitHub Actions

Source: https://opencode.ai/docs/github

This YAML workflow demonstrates how to schedule OpenCode to run automated tasks on a weekly basis. It requires ANTHROPIC_API_KEY for authentication and specifies a prompt for the task. Permissions for contents, pull-requests, and issues are granted for creating branches or PRs.

```yaml
name: Scheduled OpenCode Task

on:
  schedule:
    - cron: "0 9 * * 1" # Every Monday at 9am UTC

jobs:
  opencode:
    runs-on: ubuntu-latest
    permissions:
      id-token: write
      contents: write
      pull-requests: write
      issues: write
    steps:
      - name: Checkout repository
        uses: actions/checkout@v6
        with:
          persist-credentials: false

      - name: Run OpenCode
        uses: anomalyco/opencode/github@latest
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        with:
          model: anthropic/claude-sonnet-4-20250514
          prompt: |
            Review the codebase for any TODO comments and create a summary.
            If you find issues worth addressing, open an issue to track them.
```

--------------------------------

### Configure Manual Sharing in OpenCode

Source: https://opencode.ai/docs/share

Sets OpenCode to manual sharing mode via the configuration file. In this mode, conversations are not shared automatically and require the '/share' command to be initiated.

```json
{
  "$schema": "https://opncd.ai/config.json",
  "share": "manual"
}
```

--------------------------------

### Advanced Custom Provider Configuration with API Key and Headers

Source: https://opencode.ai/docs/providers

This advanced JSON configuration for a custom AI provider includes setting the API key via an environment variable and defining custom headers for authentication. It also specifies model limits for context and output tokens, which helps OpenCode AI manage resource allocation.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "myprovider": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "My AI ProviderDisplay Name",
      "options": {
        "baseURL": "https://api.myprovider.com/v1",
        "apiKey": "{env:ANTHROPIC_API_KEY}",
        "headers": {
          "Authorization": "Bearer custom-token"
        }
      },
      "models": {
        "my-model-name": {
          "name": "My Model Display Name",
          "limit": {
            "context": 200000,
            "output": 65536
          }
        }
      }
    }
  }
}
```

--------------------------------

### OpenCode Default Keybinds Configuration

Source: https://opencode.ai/docs/keybinds

This JSON object defines the default keybindings for various actions within OpenCode. It includes settings for session management, editor navigation, message handling, model selection, agent control, and input manipulation. The 'leader' key is used for many shortcuts, which can be customized.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "keybinds": {
    "leader": "ctrl+x",
    "app_exit": "ctrl+c,ctrl+d,<leader>q",
    "editor_open": "<leader>e",
    "theme_list": "<leader>t",
    "sidebar_toggle": "<leader>b",
    "scrollbar_toggle": "none",
    "username_toggle": "none",
    "status_view": "<leader>s",
    "tool_details": "none",
    "session_export": "<leader>x",
    "session_new": "<leader>n",
    "session_list": "<leader>l",
    "session_timeline": "<leader>g",
    "session_fork": "none",
    "session_rename": "none",
    "session_share": "none",
    "session_unshare": "none",
    "session_interrupt": "escape",
    "session_compact": "<leader>c",
    "session_child_cycle": "<leader>right",
    "session_child_cycle_reverse": "<leader>left",
    "session_parent": "<leader>up",
    "messages_page_up": "pageup,ctrl+alt+b",
    "messages_page_down": "pagedown,ctrl+alt+f",
    "messages_line_up": "ctrl+alt+y",
    "messages_line_down": "ctrl+alt+e",
    "messages_half_page_up": "ctrl+alt+u",
    "messages_half_page_down": "ctrl+alt+d",
    "messages_first": "ctrl+g,home",
    "messages_last": "ctrl+alt+g,end",
    "messages_next": "none",
    "messages_previous": "none",
    "messages_copy": "<leader>y",
    "messages_undo": "<leader>u",
    "messages_redo": "<leader>r",
    "messages_last_user": "none",
    "messages_toggle_conceal": "<leader>h",
    "model_list": "<leader>m",
    "model_cycle_recent": "f2",
    "model_cycle_recent_reverse": "shift+f2",
    "model_cycle_favorite": "none",
    "model_cycle_favorite_reverse": "none",
    "variant_cycle": "ctrl+t",
    "command_list": "ctrl+p",
    "agent_list": "<leader>a",
    "agent_cycle": "tab",
    "agent_cycle_reverse": "shift+tab",
    "input_clear": "ctrl+c",
    "input_paste": "ctrl+v",
    "input_submit": "return",
    "input_newline": "shift+return,ctrl+return,alt+return,ctrl+j",
    "input_move_left": "left,ctrl+b",
    "input_move_right": "right,ctrl+f",
    "input_move_up": "up",
    "input_move_down": "down",
    "input_select_left": "shift+left",
    "input_select_right": "shift+right",
    "input_select_up": "shift+up",
    "input_select_down": "shift+down",
    "input_line_home": "ctrl+a",
    "input_line_end": "ctrl+e",
    "input_select_line_home": "ctrl+shift+a",
    "input_select_line_end": "ctrl+shift+e",
    "input_visual_line_home": "alt+a",
    "input_visual_line_end": "alt+e",
    "input_select_visual_line_home": "alt+shift+a",
    "input_select_visual_line_end": "alt+shift+e",
    "input_buffer_home": "home",
    "input_buffer_end": "end",
    "input_select_buffer_home": "shift+home",
    "input_select_buffer_end": "shift+end",
    "input_delete_line": "ctrl+shift+d",
    "input_delete_to_line_end": "ctrl+k",
    "input_delete_to_line_start": "ctrl+u",
    "input_backspace": "backspace,shift+backspace",
    "input_delete": "ctrl+d,delete,shift+delete",
    "input_undo": "ctrl+-,super+z",
    "input_redo": "ctrl+.,super+shift+z",
    "input_word_forward": "alt+f,alt+right,ctrl+right",
    "input_word_backward": "alt+b,alt+left,ctrl+left",
    "input_select_word_forward": "alt+shift+f,alt+shift+right",
    "input_select_word_backward": "alt+shift+b,alt+shift+left",
    "input_delete_word_forward": "alt+d,alt+delete,ctrl+delete",
    "input_delete_word_backward": "ctrl+w,ctrl+backspace,alt+backspace",
    "history_previous": "up",
    "history_next": "down",
    "terminal_suspend": "ctrl+z",
    "terminal_title_toggle": "none",
    "tips_toggle": "<leader>h",
    "display_thinking": "none"
  }
}
```

--------------------------------

### Create 'debug' Mode Configuration (Markdown)

Source: https://opencode.ai/docs/modes

This markdown file defines a project-specific 'debug' mode for OpenCode AI. It sets a low temperature, enables 'bash', 'read', 'grep', and 'write' tools, and disables 'edit'. The accompanying text describes the mode's purpose: investigating and diagnosing issues using commands and file inspection.

```markdown
---
temperature: 0.1
tools:
  bash: true
  read: true
  grep: true
  write: false
  edit: false
---

You are in debug mode. Your primary goal is to help investigate and diagnose issues.

Focus on:

- Understanding the problem through careful analysis
- Using bash commands to inspect system state
- Reading relevant files and logs
- Searching for patterns and anomalies
- Providing clear explanations of findings

Do not make any changes to files. Only investigate and report.
```

--------------------------------

### Set GitLab Environment Variables

Source: https://opencode.ai/docs/providers

Configures environment variables for connecting to a self-hosted GitLab instance, including the instance URL, AI Gateway URL, and a personal access token. These are typically added to the bash profile.

```bash
export GITLAB_INSTANCE_URL=https://gitlab.company.com
export GITLAB_AI_GATEWAY_URL=https://ai-gateway.company.com
export GITLAB_TOKEN=glpat-...
```

--------------------------------

### Session Children and Todo API

Source: https://opencode.ai/docs/de/server

Endpoints to retrieve child sessions and the todo list for a specific session.

```APIDOC
## GET /session/:id/children

### Description
Get the child sessions for a given session.

### Method
GET

### Endpoint
/session/:id/children

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the parent session.

### Request Example
None

### Response
#### Success Response (200)
- **children** (Session[]) - An array of child session objects.

#### Response Example
```json
[
  {
    "id": "child_session_789",
    "title": "Child Session 1",
    "createdAt": "2023-10-27T10:10:00Z"
  }
]
```

## GET /session/:id/todo

### Description
Get the todo list associated with a specific session.

### Method
GET

### Endpoint
/session/:id/todo

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.

### Request Example
None

### Response
#### Success Response (200)
- **todos** (Todo[]) - An array of todo items for the session.

#### Response Example
```json
[
  {
    "id": "todo_abc",
    "task": "Implement feature X",
    "completed": false
  }
]
```
```

--------------------------------

### Secure opencode Serve with Password

Source: https://opencode.ai/docs/server

The opencode server can be protected using HTTP basic authentication by setting the `OPENCODE_SERVER_PASSWORD` environment variable. The username defaults to 'opencode' but can be overridden with `OPENCODE_SERVER_USERNAME`.

```bash
OPENCODE_SERVER_PASSWORD=your-password opencode serve
```

--------------------------------

### Session Management API

Source: https://opencode.ai/docs/sdk

Provides endpoints for managing sessions, including listing, creating, updating, and deleting them.

```APIDOC
## GET /sessions

### Description
Lists all available sessions.

### Method
GET

### Endpoint
/sessions

### Parameters
#### Query Parameters
- **None**

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **sessions** (Session[]) - An array of session objects.

#### Response Example
```json
{
  "sessions": [
    {
      "id": "sess_123",
      "name": "My First Session"
    }
  ]
}
```

## GET /sessions/{path}

### Description
Retrieves details for a specific session.

### Method
GET

### Endpoint
/sessions/{path}

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session.

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **session** (Session) - The session object.

#### Response Example
```json
{
  "session": {
    "id": "sess_123",
    "name": "My First Session"
  }
}
```

## POST /sessions

### Description
Creates a new session.

### Method
POST

### Endpoint
/sessions

### Parameters
#### Request Body
- **body** (object) - Required - The session creation payload.

### Request Example
```json
{
  "name": "New Session"
}
```

### Response
#### Success Response (200)
- **session** (Session) - The newly created session object.

#### Response Example
```json
{
  "session": {
    "id": "sess_456",
    "name": "New Session"
  }
}
```

## DELETE /sessions/{path}

### Description
Deletes a specific session.

### Method
DELETE

### Endpoint
/sessions/{path}

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session to delete.

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **result** (boolean) - True if the session was deleted successfully, false otherwise.

#### Response Example
```json
{
  "result": true
}
```

## PUT /sessions/{path}

### Description
Updates properties of an existing session.

### Method
PUT

### Endpoint
/sessions/{path}

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session to update.
#### Request Body
- **body** (object) - Required - The session update payload.

### Request Example
```json
{
  "name": "Updated Session Name"
}
```

### Response
#### Success Response (200)
- **session** (Session) - The updated session object.

#### Response Example
```json
{
  "session": {
    "id": "sess_123",
    "name": "Updated Session Name"
  }
}
```
```

--------------------------------

### Enable Glob Tool in OpenCode

Source: https://opencode.ai/docs/tools

Configure the 'glob' tool permission to 'allow' in opencode.json to enable file searching using glob patterns. This tool returns matching file paths, sorted by their modification time.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "glob": "allow"
  }
}
```

--------------------------------

### Session Management API

Source: https://opencode.ai/docs/sdk

Endpoints for managing and interacting with AI sessions, including creating, listing, prompting, commanding, and reverting messages.

```APIDOC
## POST /api/session/create

### Description
Creates a new AI session.

### Method
POST

### Endpoint
/api/session/create

### Parameters
#### Request Body
- **title** (string) - Required - The title of the session.

### Request Example
```json
{
  "title": "My session"
}
```

### Response
#### Success Response (200)
- **id** (string) - The unique identifier for the created session.

#### Response Example
```json
{
  "id": "session_12345"
}
```

## GET /api/session/list

### Description
Retrieves a list of all available AI sessions.

### Method
GET

### Endpoint
/api/session/list

### Response
#### Success Response (200)
- **sessions** (array) - An array of session objects.

#### Response Example
```json
[
  {
    "id": "session_12345",
    "title": "My session"
  }
]
```

## POST /api/session/{id}/prompt

### Description
Sends a prompt message to a specific AI session. This can be used to get an AI response or to inject context without a reply.

### Method
POST

### Endpoint
/api/session/{id}/prompt

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to send the prompt to.

#### Request Body
- **parts** (array) - Required - An array of message parts, typically containing text.
  - **type** (string) - Required - The type of the part (e.g., "text").
  - **text** (string) - Required - The content of the text part.
- **model** (object) - Optional - The model to use for the prompt.
  - **providerID** (string) - Required - The ID of the model provider.
  - **modelID** (string) - Required - The ID of the model.
- **noReply** (boolean) - Optional - If true, the AI will not generate a response, only process the context.

### Request Example
```json
{
  "parts": [
    { "type": "text", "text": "Hello!" }
  ],
  "model": {
    "providerID": "anthropic",
    "modelID": "claude-3-5-sonnet-20241022"
  }
}
```

### Response
#### Success Response (200)
- **message** (object) - The AI's response message. Type depends on `noReply` and model capabilities.

#### Response Example
```json
{
  "message": {
    "type": "assistant",
    "content": [
      { "type": "text", "text": "Hello there! How can I help you today?" }
    ]
  }
}
```

## POST /api/session/{id}/command

### Description
Sends a command to a specific AI session.

### Method
POST

### Endpoint
/api/session/{id}/command

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to send the command to.

#### Request Body
- **command** (string) - Required - The command to send.

### Request Example
```json
{
  "command": "run_analysis"
}
```

### Response
#### Success Response (200)
- **info** (object) - Information about the command execution, likely an AssistantMessage.
- **parts** (array) - An array of parts related to the command output.

#### Response Example
```json
{
  "info": {
    "type": "assistant",
    "content": [
      { "type": "text", "text": "Analysis complete." }
    ]
  },
  "parts": [
    { "type": "text", "text": "Details of analysis..." }
  ]
}
```

## POST /api/session/{id}/shell

### Description
Runs a shell command within a specific AI session.

### Method
POST

### Endpoint
/api/session/{id}/shell

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to run the shell command in.

#### Request Body
- **command** (string) - Required - The shell command to execute.

### Request Example
```json
{
  "command": "ls -l"
}
```

### Response
#### Success Response (200)
- **message** (object) - An AssistantMessage containing the output of the shell command.

#### Response Example
```json
{
  "message": {
    "type": "assistant",
    "content": [
      { "type": "text", "text": "total 8\n-rw-r--r-- 1 user group 1024 Jan 1 10:00 file.txt\ndrwxr-xr-x 2 user group 4096 Jan 1 10:00 dir" }
    ]
  }
}
```

## POST /api/session/{id}/revert

### Description
Reverts a message in a specific AI session.

### Method
POST

### Endpoint
/api/session/{id}/revert

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session containing the message to revert.

#### Request Body
- **messageId** (string) - Required - The ID of the message to revert.

### Request Example
```json
{
  "messageId": "message_abcde"
}
```

### Response
#### Success Response (200)
- **session** (object) - The updated session object.

#### Response Example
```json
{
  "session": {
    "id": "session_12345",
    "title": "My session",
    "messages": [
      // ... updated messages
    ]
  }
}
```

## POST /api/session/{id}/unrevert

### Description
Restores previously reverted messages in a specific AI session.

### Method
POST

### Endpoint
/api/session/{id}/unrevert

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to restore messages in.

### Request Example
```json
{} // No request body needed
```

### Response
#### Success Response (200)
- **session** (object) - The updated session object with restored messages.

#### Response Example
```json
{
  "session": {
    "id": "session_12345",
    "title": "My session",
    "messages": [
      // ... messages including restored ones
    ]
  }
}
```

## POST /api/session/{sessionId}/permissions/{permissionId}

### Description
Responds to a permission request within a session.

### Method
POST

### Endpoint
/api/session/{sessionId}/permissions/{permissionId}

### Parameters
#### Path Parameters
- **sessionId** (string) - Required - The ID of the session.
- **permissionId** (string) - Required - The ID of the permission request.

#### Request Body
- **allowed** (boolean) - Required - Whether the permission is allowed.

### Request Example
```json
{
  "allowed": true
}
```

### Response
#### Success Response (200)
- **result** (boolean) - Indicates if the response was successful.

#### Response Example
```json
{
  "result": true
}
```
```

--------------------------------

### Configure opencode.json for GitLab Plugin

Source: https://opencode.ai/docs/providers

This JSON configuration snippet adds the GitLab plugin to opencode.json. This plugin is recommended for comprehensive GitLab repository management, including merge requests, issues, and pipelines.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "plugin": ["@gitlab/opencode-gitlab-plugin"]
}
```

--------------------------------

### Set Global Permissions (JSON)

Source: https://opencode.ai/docs/permissions

Configure global permissions for all actions using a simple string value or a more detailed object. The '*' key acts as a catch-all for any action not explicitly defined.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "*": "ask",
    "bash": "allow",
    "edit": "deny"
  }
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": "allow"
}
```

--------------------------------

### Define Tool Arguments with Zod Schema

Source: https://opencode.ai/docs/custom-tools

This code illustrates how to define tool arguments using `tool.schema`, which is based on Zod. It specifies that the 'query' argument must be a string and provides a description for it.

```typescript
args: {
  query: tool.schema.string().describe("SQL query to execute")
}
```

--------------------------------

### Configure Global Model Options in OpenCode

Source: https://opencode.ai/docs/models

This JSON configuration allows for global settings of model options for different providers like OpenAI and Anthropic. It enables fine-tuning parameters such as reasoning effort and verbosity for specific models.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "openai": {
      "models": {
        "gpt-5": {
          "options": {
            "reasoningEffort": "high",
            "textVerbosity": "low",
            "reasoningSummary": "auto",
            "include": ["reasoning.encrypted_content"]
          }
        }
      }
    },
    "anthropic": {
      "models": {
        "claude-sonnet-4-5-20250929": {
          "options": {
            "thinking": {
              "type": "enabled",
              "budgetTokens": 16000
            }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Enable todowrite tool in opencode.json

Source: https://opencode.ai/docs/de/tools

This JSON configuration snippet enables the 'todowrite' tool within the OpenCode AI project. It specifies permissions for the LLM to manage todo lists during coding sessions, aiding in tracking progress for complex operations. The tool is disabled for subagents by default.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "todowrite": "allow"
  }
}
```

--------------------------------

### Session Sharing API

Source: https://opencode.ai/docs/sdk

Endpoints for sharing and unsharing sessions.

```APIDOC
## POST /sessions/{path}/share

### Description
Shares a specific session.

### Method
POST

### Endpoint
/sessions/{path}/share

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session to share.

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **session** (Session) - The shared session object.

#### Response Example
```json
{
  "session": {
    "id": "sess_123",
    "name": "My Shared Session",
    "shared": true
  }
}
```

## POST /sessions/{path}/unshare

### Description
Unshares a specific session.

### Method
POST

### Endpoint
/sessions/{path}/unshare

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session to unshare.

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **session** (Session) - The unshared session object.

#### Response Example
```json
{
  "session": {
    "id": "sess_123",
    "name": "My Unshared Session",
    "shared": false
  }
}
```
```

--------------------------------

### OpenAI Compatible Endpoints

Source: https://opencode.ai/docs/zen

Endpoints for models compatible with OpenAI's API, such as MiniMax, GLM, and Kimi.

```APIDOC
## POST /zen/v1/responses

### Description
This endpoint is used to get responses from OpenAI-compatible models like GPT 5.2, GPT 5.1, and their Codex variants.

### Method
POST

### Endpoint
`https://opencode.ai/zen/v1/responses`

### Parameters
#### Query Parameters
- **model** (string) - Required - The ID of the model to use (e.g., `gpt-5.2-codex`).

#### Request Body
- **prompt** (string) - Required - The input prompt for the model.
- **max_tokens** (integer) - Optional - The maximum number of tokens to generate.

### Request Example
```json
{
  "prompt": "Translate the following English text to French: 'Hello, world!'",
  "max_tokens": 60
}
```

### Response
#### Success Response (200)
- **choices** (array) - An array of response choices from the model.
  - **text** (string) - The generated text.

#### Response Example
```json
{
  "choices": [
    {
      "text": "Bonjour le monde!"
    }
  ]
}
```
```

```APIDOC
## POST /zen/v1/chat/completions

### Description
This endpoint is used for chat-based interactions with various models, including MiniMax, GLM, Kimi, and Qwen3 Coder.

### Method
POST

### Endpoint
`https://opencode.ai/zen/v1/chat/completions`

### Parameters
#### Query Parameters
- **model** (string) - Required - The ID of the model to use (e.g., `minimax-m2.5`, `glm-5`, `kimi-k2`).

#### Request Body
- **messages** (array) - Required - An array of message objects representing the conversation history.
  - **role** (string) - The role of the message sender (e.g., `user`, `assistant`).
  - **content** (string) - The content of the message.
- **max_tokens** (integer) - Optional - The maximum number of tokens to generate.

### Request Example
```json
{
  "messages": [
    {"role": "user", "content": "What is the capital of France?"}
  ],
  "max_tokens": 50
}
```

### Response
#### Success Response (200)
- **choices** (array) - An array of response choices.
  - **message** (object)
    - **role** (string) - The role of the message sender (e.g., `assistant`).
    - **content** (string) - The generated message content.

#### Response Example
```json
{
  "choices": [
    {
      "message": {
        "role": "assistant",
        "content": "The capital of France is Paris."
      }
    }
  ]
}
```
```

--------------------------------

### Configure Model in opencode.json

Source: https://opencode.ai/docs/models

Specifies the model to be used by OpenCode via its configuration file. The format expected is 'provider/model'. This setting is checked after command-line flags.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "anthropic/claude-sonnet-4-20250514"
}
```

--------------------------------

### Configure Tool Permissions in OpenCode

Source: https://opencode.ai/docs/tools

Configure tool behavior in OpenCode using the 'permission' field in opencode.json. You can explicitly allow, deny, or require approval ('ask') for specific tools like 'edit', 'bash', and 'webfetch'. This JSON configuration controls how the LLM can interact with your project's environment.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "edit": "deny",
    "bash": "ask",
    "webfetch": "allow"
  }
}
```

--------------------------------

### Enable question tool in opencode.json

Source: https://opencode.ai/docs/de/tools

This JSON configuration snippet enables the 'question' tool in OpenCode AI, allowing the LLM to interact with the user by asking questions. This is valuable for clarifying instructions, gathering preferences, or making decisions during task execution. The configuration grants 'allow' permission for the 'question' tool.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "question": "allow"
  }
}
```

--------------------------------

### Set Command Description in opencode.json

Source: https://opencode.ai/docs/commands

The `description` option in `opencode.json` provides a brief explanation of a command's functionality. This description is displayed in the TUI when a user interacts with the command. It is a key-value pair within the command's configuration.

```json
{
  "command": {
    "test": {
      "description": "Run tests with coverage"
    }
  }
}
```

--------------------------------

### Configure Wildcard Tool Permissions in OpenCode

Source: https://opencode.ai/docs/tools

Use wildcard characters in the 'permission' field of opencode.json to manage permissions for multiple tools simultaneously. This is particularly useful for applying a consistent permission setting (e.g., 'ask') to all tools originating from an MCP server, denoted by a pattern like 'mymcp_*'.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "mymcp_*": "ask"
  }
}
```

--------------------------------

### Pass Provider-Specific Model Options

Source: https://opencode.ai/docs/agents

Pass additional options directly to the provider as model options by specifying them in the agent configuration. This allows utilization of provider-specific features like 'reasoningEffort' for OpenAI models.

```json
{
  "agent": {
    "deep-thinker": {
      "description": "Agent that uses high reasoning effort for complex problems",
      "model": "openai/gpt-5",
      "reasoningEffort": "high",
      "textVerbosity": "low"
    }
  }
}
```

--------------------------------

### Authentication Management

Source: https://opencode.ai/docs/sdk

Manage authentication credentials for accessing OpenCode AI services. This includes setting API keys and other necessary authentication details.

```APIDOC
## Authentication API

### Description
Manages authentication credentials for the OpenCode AI client.

### Method

#### `auth.set({ path, body })`
Sets the authentication credentials for a specific service.

- **path** (object) - Required - Path parameters for the authentication.
  - **id** (string) - Required - The identifier of the service (e.g., 'anthropic').
- **body** (object) - Required - The authentication details.
  - **type** (string) - Required - The type of authentication (e.g., 'api').
  - **key** (string) - Required - The authentication key or token.

### Request Example
```javascript
await client.auth.set({
  path: { id: "anthropic" },
  body: { type: "api", key: "your-api-key" },
});
```

### Response
- **boolean** - Indicates success or failure of setting authentication.
```

--------------------------------

### Command with Positional Arguments

Source: https://opencode.ai/docs/commands

Create commands that utilize positional arguments for dynamic input. $1, $2, and subsequent parameters can be used to reference individual arguments passed to the command, enabling more granular control over prompt generation.

```markdown
---
description: Create a new file with content
---

Create a file named $1 in the directory $2
with the following content: $3
```

--------------------------------

### Enable Read Tool in OpenCode

Source: https://opencode.ai/docs/tools

Set the 'read' permission to 'allow' in opencode.json to enable the LLM to read file contents. This tool supports fetching specific line ranges, making it efficient for accessing parts of large files.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "read": "allow"
  }
}
```

--------------------------------

### Event Subscription

Source: https://opencode.ai/docs/sdk

Subscribe to real-time events streamed from the OpenCode AI server. This allows for listening to various events and their properties as they occur.

```APIDOC
## Events API

### Description
Provides functionality to subscribe to server-sent events.

### Method

#### `event.subscribe()`
Establishes a connection to the server-sent events stream.

### Response
- **Server-sent events stream** - An object containing a stream of events.
  - **stream** (AsyncIterableIterator) - An iterator for receiving events.
    - **event.type** (string) - The type of the event.
    - **event.properties** (object) - Additional properties associated with the event.

### Request Example
```javascript
// Listen to real-time events
const events = await client.event.subscribe();
for await (const event of events.stream) {
  console.log("Event:", event.type, event.properties);
}
```
```

--------------------------------

### Customize Session Compaction Context

Source: https://opencode.ai/docs/plugins

This plugin customizes the context included when a session is compacted. It uses the 'experimental.session.compacting' hook to push additional custom context, such as current task status and important decisions, into the compaction prompt. This helps preserve relevant state across session compactions.

```typescript
import type { Plugin } from "@opencode-ai/plugin"

export const CompactionPlugin: Plugin = async (ctx) => {
  return {
    "experimental.session.compacting": async (input, output) => {
      // Inject additional context into the compaction prompt
      output.context.push(`
## Custom Context

Include any state that should persist across compaction:
- Current task status
- Important decisions made
- Files being actively worked on
`)
    },
  }
}
```

--------------------------------

### Enable List Tool in OpenCode

Source: https://opencode.ai/docs/tools

Allow the 'list' tool by setting its permission to 'allow' in opencode.json. This enables the LLM to list directory contents and filter results using glob patterns.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "list": "allow"
  }
}
```

--------------------------------

### Manage OpenCode Agents

Source: https://opencode.ai/docs/cli

Commands for managing agents within OpenCode. This includes creating new agents with custom configurations and listing existing agents.

```bash
opencode agent [command]
opencode agent create
opencode agent list
```

--------------------------------

### Control Response Randomness with Temperature (JSON)

Source: https://opencode.ai/docs/agents

Adjusts the creativity and determinism of an agent's responses using the `temperature` setting in `opencode.json`. Lower values yield focused results, while higher values increase creativity.

```json
{
  "agent": {
    "plan": {
      "temperature": 0.1
    },
    "creative": {
      "temperature": 0.8
    }
  }
}
```

```json
{
  "agent": {
    "analyze": {
      "temperature": 0.1,
      "prompt": "{file:./prompts/analysis.txt}"
    },
    "build": {
      "temperature": 0.3
    },
    "brainstorm": {
      "temperature": 0.7,
      "prompt": "{file:./prompts/creative.txt}"
    }
  }
}
```

--------------------------------

### TUI Operations

Source: https://opencode.ai/docs/sdk

This section details the various methods available for interacting with the Text User Interface (TUI) of OpenCode AI. These methods allow for appending text, opening dialogs, submitting prompts, and more.

```APIDOC
## TUI Operations API

### Description
Provides methods to control and interact with the Text User Interface (TUI) of OpenCode AI.

### Methods

#### `tui.appendPrompt({ body })`
Appends text to the current prompt.

- **body** (object) - Required - The prompt text to append.
  - **text** (string) - Required - The text content to add.

### Request Example
```javascript
await client.tui.appendPrompt({
  body: { text: "Add this to prompt" },
});
```

### Response
- **boolean** - Indicates success or failure of the operation.

#### `tui.openHelp()`
Opens the help dialog.

### Response
- **boolean** - Indicates success or failure of the operation.

#### `tui.openSessions()`
Opens the session selector dialog.

### Response
- **boolean** - Indicates success or failure of the operation.

#### `tui.openThemes()`
Opens the theme selector dialog.

### Response
- **boolean** - Indicates success or failure of the operation.

#### `tui.openModels()`
Opens the model selector dialog.

### Response
- **boolean** - Indicates success or failure of the operation.

#### `tui.submitPrompt()`
Submits the current prompt for processing.

### Response
- **boolean** - Indicates success or failure of the operation.

#### `tui.clearPrompt()`
Clears the current prompt input.

### Response
- **boolean** - Indicates success or failure of the operation.

#### `tui.executeCommand({ body })`
Executes a specific command within the TUI.

- **body** (object) - Required - The command details.
  - **command** (string) - Required - The command to execute.

### Response
- **boolean** - Indicates success or failure of the operation.

#### `tui.showToast({ body })`
Displays a toast notification to the user.

- **body** (object) - Required - The toast notification details.
  - **message** (string) - Required - The message content of the toast.
  - **variant** (string) - Optional - The style variant of the toast (e.g., 'success', 'error').

### Request Example
```javascript
await client.tui.showToast({
  body: { message: "Task completed", variant: "success" },
});
```

### Response
- **boolean** - Indicates success or failure of the operation.
```

--------------------------------

### POST /session/:id/abort

Source: https://opencode.ai/docs/server

Aborts a running session.  This action stops the session's current operations.

```APIDOC
## POST /session/:id/abort

### Description
Abort a running session.

### Method
POST

### Endpoint
/session/:id/abort

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to abort.

### Request Example
No request body.

### Response
#### Success Response (200)
- **boolean** - True if the session was successfully aborted.

#### Response Example
true

```

--------------------------------

### Configure Ollama for Local Models in OpenCode

Source: https://opencode.ai/docs/providers

This JSON configuration enables OpenCode to use local models hosted by Ollama. It utilizes the OpenAI-compatible npm package, sets the Ollama local server URL, and defines the mapping for local models like Llama 2.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "ollama": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama (local)",
      "options": {
        "baseURL": "http://localhost:11434/v1"
      },
      "models": {
        "llama2": {
          "name": "Llama 2"
        }
      }
    }
  }
}
```

--------------------------------

### Default LSP Server Configuration in OpenCode

Source: https://opencode.ai/docs/lsp

This JSON snippet shows the default structure for configuring LSP servers within OpenCode. It includes a schema definition and an empty `lsp` object, indicating that all LSP servers are enabled by default. Customizations are made by adding specific server configurations within the `lsp` object.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "lsp": {}
}
```

--------------------------------

### Enable toread tool in opencode.json

Source: https://opencode.ai/docs/de/tools

This JSON configuration snippet enables the 'todoread' tool within the OpenCode AI project. It grants the LLM permission to read existing todo lists, which is crucial for tracking pending or completed tasks. Like 'todowrite', this tool is disabled for subagents by default.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "todoread": "allow"
  }
}
```

--------------------------------

### Configure Agent Permissions in Markdown Agents

Source: https://opencode.ai/docs/agents

Set tool permissions within Markdown agent configurations, including specific command permissions for bash tools using glob patterns. This allows fine-grained control over agent capabilities.

```markdown
---
description: Code review without edits
mode: subagent
permission:
  edit: deny
  bash:
    "*": ask
    "git diff": allow
    "git log*": allow
    "grep *": allow
  webfetch: deny
---

Only analyze code and suggest changes.
```

--------------------------------

### Configure Amazon Bedrock with VPC Endpoint in OpenCode JSON

Source: https://opencode.ai/docs/providers

Configure Amazon Bedrock provider in `opencode.json` to use a custom VPC endpoint. This is useful for secure and private network access to Bedrock.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "amazon-bedrock": {
      "options": {
        "region": "us-east-1",
        "profile": "production",
        "endpoint": "https://bedrock-runtime.us-east-1.vpce-xxxxx.amazonaws.com"
      }
    }
  }
}
```

--------------------------------

### GitHub Actions Workflow for Issue Triage with OpenCode

Source: https://opencode.ai/docs/github

This GitHub Actions workflow automatically triages newly opened issues. It first checks if the issue author's account is older than 30 days to filter out potential spam. If the account meets the age criteria, it proceeds to use OpenCode to review the issue and provide relevant documentation links or guidance.

```yaml
name: Issue Triage

on:
  issues:
    types: [opened]

jobs:
  triage:
    runs-on: ubuntu-latest
    permissions:
      id-token: write
      contents: write
      pull-requests: write
      issues: write
    steps:
      - name: Check account age
        id: check
        uses: actions/github-script@v7
        with:
          script: |
            const user = await github.rest.users.getByUsername({
              username: context.payload.issue.user.login
            });
            const created = new Date(user.data.created_at);
            const days = (Date.now() - created) / (1000 * 60 * 60 * 24);
            return days >= 30;
          result-encoding: string

      - uses: actions/checkout@v6
        if: steps.check.outputs.result == 'true'
        with:
          persist-credentials: false

      - uses: anomalyco/opencode/github@latest
        if: steps.check.outputs.result == 'true'
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        with:
          model: anthropic/claude-sonnet-4-20250514
          prompt: |
            Review this issue. If there's a clear fix or relevant docs:
            - Provide documentation links
            - Add error handling guidance for code examples
            Otherwise, do not comment.
```

--------------------------------

### Configure Agent Model in opencode.json

Source: https://opencode.ai/docs/agents

Override the default model for an agent in the opencode.json configuration. This allows using different models optimized for specific tasks, such as a faster model for planning and a more capable one for implementation. If not specified, primary agents use the global model, and subagents inherit from their invoker.

```json
{
  "agent": {
    "plan": {
      "model": "anthropic/claude-haiku-4-20250514"
    }
  }
}
```

--------------------------------

### Review GitLab Merge Request using OpenCode AI (Command)

Source: https://opencode.ai/docs/gitlab

This command prompts OpenCode AI to review a GitLab merge request. By posting this comment on a merge request, OpenCode will analyze the changes and provide feedback.

```shell
@opencode review this merge request
```

--------------------------------

### Configure Custom OpenAI-Compatible Provider in opencode.json

Source: https://opencode.ai/docs/providers

This JSON configuration defines a custom AI provider that is compatible with OpenAI's API. It specifies the npm package to use, a display name, API endpoint, and available models. This allows OpenCode AI to interact with third-party AI services.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "myprovider": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "My AI ProviderDisplay Name",
      "options": {
        "baseURL": "https://api.myprovider.com/v1"
      },
      "models": {
        "my-model-name": {
          "name": "My Model Display Name"
        }
      }
    }
  }
}
```

--------------------------------

### Configure Auto-Sharing in OpenCode

Source: https://opencode.ai/docs/share

Enables automatic sharing for all new conversations in OpenCode by setting the 'share' option to 'auto' in the configuration file. A share link will be generated for every new conversation.

```json
{
  "$schema": "https://opncd.ai/config.json",
  "share": "auto"
}
```

--------------------------------

### Debug MCP Server OAuth Connection

Source: https://opencode.ai/docs/cli

Helps in debugging issues related to OAuth connections for an MCP server. It allows users to diagnose and resolve problems with authentication and authorization.

```bash
opencode mcp debug <name>
```

--------------------------------

### Configure llama.cpp Local Models in OpenCode

Source: https://opencode.ai/docs/providers

This JSON configuration enables OpenCode to use local language models served by llama.cpp. It specifies the OpenAI-compatible endpoint of the local server and maps local model identifiers to their configurations, including context and output limits.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "llama.cpp": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "llama-server (local)",
      "options": {
        "baseURL": "http://127.0.0.1:8080/v1"
      },
      "models": {
        "qwen3-coder:a3b": {
          "name": "Qwen3-Coder: a3b-30b (local)",
          "limit": {
            "context": 128000,
            "output": 65536
          }
        }
      }
    }
  }
}
```

--------------------------------

### Attach TUI to OpenCode Backend

Source: https://opencode.ai/docs/cli

Connect the OpenCode TUI to a running OpenCode backend server. This is useful for using the TUI with a remote backend, supporting session continuation and directory specification.

```bash
opencode attach [url]
opencode web --port 4096 --hostname 0.0.0.0
opencode attach http://10.20.30.40:4096
opencode attach --dir <directory>
opencode attach -s <session_id>
```

--------------------------------

### Implement a Basic OpenCode Plugin in TypeScript

Source: https://opencode.ai/docs/plugins

This TypeScript code defines a basic OpenCode plugin. The plugin function receives a context object containing project details, a client for AI interaction, and Bun's shell API. It returns an object where keys are hook names (e.g., 'tool.execute.before') and values are asynchronous functions that modify behavior.

```typescript
import type { Plugin } from "@opencode-ai/plugin"

export const MyPlugin: Plugin = async ({ project, client, $, directory, worktree }) => {
  console.log("Plugin initialized!")

  return {
    // Hook implementations go here
  }
}
```

--------------------------------

### Manage MCP Server Authentication via CLI

Source: https://opencode.ai/docs/mcp-servers

Command-line interface commands for managing MCP server authentication. These commands allow manual triggering of authentication flows, listing server statuses, and removing stored credentials.

```bash
opencode mcp auth my-oauth-server
```

```bash
opencode mcp list
```

```bash
opencode mcp logout my-oauth-server
```

```bash
opencode mcp auth list
```

```bash
opencode mcp debug my-oauth-server
```

--------------------------------

### Set EDITOR Environment Variable (Linux/macOS)

Source: https://opencode.ai/docs/tui

Configures the default text editor for OpenCode commands on Linux and macOS systems. It demonstrates setting the EDITOR variable to various editors like nano, vim, or GUI editors with the '--wait' flag. For persistence, add the export command to your shell profile (e.g., ~/.bashrc, ~/.zshrc).

```bash
# Example for nano or vim
export EDITOR=nano
export EDITOR=vim

# For GUI editors, VS Code, Cursor, VSCodium, Windsurf, Zed, etc.
# include --wait
export EDITOR="code --wait"
```

--------------------------------

### Proxy Authentication for OpenCode

Source: https://opencode.ai/docs/network

Configures proxy authentication by including username and password directly in the proxy URL environment variable. This method is suitable for basic authentication but users are advised to use more secure methods for credentials.

```bash
export HTTPS_PROXY=http://username:password@proxy.example.com:8080
```

--------------------------------

### TUI (Terminal User Interface) Endpoints

Source: https://opencode.ai/docs/server

Endpoints for interacting with the Terminal User Interface, including prompt manipulation, dialogs, and command execution.

```APIDOC
## POST /tui/append-prompt

### Description
Append text to the prompt.

### Method
POST

### Endpoint
/tui/append-prompt

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **text** (string) - Required - The text to append to the prompt.

### Request Example
```json
{
  "text": "Some text to append."
}
```

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```

## POST /tui/open-help

### Description
Open the help dialog.

### Method
POST

### Endpoint
/tui/open-help

### Parameters
None

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```

## POST /tui/open-sessions

### Description
Open the session selector.

### Method
POST

### Endpoint
/tui/open-sessions

### Parameters
None

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```

## POST /tui/open-themes

### Description
Open the theme selector.

### Method
POST

### Endpoint
/tui/open-themes

### Parameters
None

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```

## POST /tui/open-models

### Description
Open the model selector.

### Method
POST

### Endpoint
/tui/open-models

### Parameters
None

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```

## POST /tui/submit-prompt

### Description
Submit the current prompt.

### Method
POST

### Endpoint
/tui/submit-prompt

### Parameters
None

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```

## POST /tui/clear-prompt

### Description
Clear the prompt.

### Method
POST

### Endpoint
/tui/clear-prompt

### Parameters
None

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```

## POST /tui/execute-command

### Description
Execute a command.

### Method
POST

### Endpoint
/tui/execute-command

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **command** (string) - Required - The command to execute.

### Request Example
```json
{
  "command": "git status"
}
```

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```

## POST /tui/show-toast

### Description
Show toast notification.

### Method
POST

### Endpoint
/tui/show-toast

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **title** (string) - Optional - The title of the toast.
- **message** (string) - Required - The message content of the toast.
- **variant** (string) - Optional - The variant of the toast (e.g., 'info', 'success', 'warning', 'error').

### Request Example
```json
{
  "title": "Notification",
  "message": "Operation completed successfully.",
  "variant": "success"
}
```

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```

## GET /tui/control/next

### Description
Wait for the next control request.

### Method
GET

### Endpoint
/tui/control/next

### Parameters
None

### Response
#### Success Response (200)
- **Control request object** (object) - An object representing the control request.

#### Response Example
```json
{
  "type": "input",
  "data": "Please enter your name."
}
```

## POST /tui/control/response

### Description
Respond to a control request.

### Method
POST

### Endpoint
/tui/control/response

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **body** (any) - Required - The response to the control request.

### Request Example
```json
{
  "body": "John Doe"
}
```

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the operation was successful.

#### Response Example
```json
true
```
```

--------------------------------

### Messages API

Source: https://opencode.ai/docs/server

Endpoints for managing messages within a session, including listing, sending, and retrieving message details. Supports both synchronous and asynchronous message sending.

```APIDOC
## GET /session/:id/message

### Description
List messages in a session.

### Method
GET

### Endpoint
/session/:id/message

### Query Parameters
- **limit** (integer) - Optional - Maximum number of messages to return.

### Response
#### Success Response (200)
- **info** (Message) - Information about the message.
- **parts** (Part[]) - Array of message parts.

#### Response Example
{
  "info": {
    "id": "msg_abc123",
    "role": "user",
    "content": "Hello, world!"
  },
  "parts": [
    {
      "content": "Hello, world!",
      "contentType": "text"
    }
  ]
}

## POST /session/:id/message

### Description
Send a message and wait for the response.

### Method
POST

### Endpoint
/session/:id/message

### Request Body
- **messageID** (string) - Optional - The ID of the message.
- **model** (string) - Optional - The model to use for the response.
- **agent** (string) - Optional - The agent to use for the response.
- **noReply** (boolean) - Optional - If true, the agent will not reply.
- **system** (string) - Optional - System prompt to use.
- **tools** (object) - Optional - Tools to use for the response.
- **parts** (object) - Optional - Message parts to send.

### Response
#### Success Response (200)
- **info** (Message) - Information about the message.
- **parts** (Part[]) - Array of message parts.

#### Response Example
{
  "info": {
    "id": "msg_def456",
    "role": "assistant",
    "content": "Hi there!"
  },
  "parts": [
    {
      "content": "Hi there!",
      "contentType": "text"
    }
  ]
}

## GET /session/:id/message/:messageID

### Description
Get message details.

### Method
GET

### Endpoint
/session/:id/message/:messageID

### Response
#### Success Response (200)
- **info** (Message) - Information about the message.
- **parts** (Part[]) - Array of message parts.

#### Response Example
{
  "info": {
    "id": "msg_abc123",
    "role": "user",
    "content": "Hello, world!"
  },
  "parts": [
    {
      "content": "Hello, world!",
      "contentType": "text"
    }
  ]
}

## POST /session/:id/prompt_async

### Description
Send a message asynchronously (no wait).

### Method
POST

### Endpoint
/session/:id/prompt_async

### Request Body
- **messageID** (string) - Optional - The ID of the message.
- **model** (string) - Optional - The model to use for the response.
- **agent** (string) - Optional - The agent to use for the response.
- **noReply** (boolean) - Optional - If true, the agent will not reply.
- **system** (string) - Optional - System prompt to use.
- **tools** (object) - Optional - Tools to use for the response.
- **parts** (object) - Optional - Message parts to send.

### Response
#### Success Response (204)
No Content.

## POST /session/:id/command

### Description
Execute a slash command.

### Method
POST

### Endpoint
/session/:id/command

### Request Body
- **messageID** (string) - Optional - The ID of the message.
- **agent** (string) - Optional - The agent to use for the command.
- **model** (string) - Optional - The model to use for the command.
- **command** (string) - Required - The command to execute.
- **arguments** (object) - Optional - Arguments for the command.

### Response
#### Success Response (200)
- **info** (Message) - Information about the message.
- **parts** (Part[]) - Array of message parts.

#### Response Example
{
  "info": {
    "id": "msg_ghi789",
    "role": "assistant",
    "content": "Command executed successfully."
  },
  "parts": [
    {
      "content": "Command executed successfully.",
      "contentType": "text"
    }
  ]
}

## POST /session/:id/shell

### Description
Run a shell command.

### Method
POST

### Endpoint
/session/:id/shell

### Request Body
- **agent** (string) - Required - The agent to use for the shell command.
- **model** (string) - Optional - The model to use for the shell command.
- **command** (string) - Required - The shell command to run.

### Response
#### Success Response (200)
- **info** (Message) - Information about the message.
- **parts** (Part[]) - Array of message parts.

#### Response Example
{
  "info": {
    "id": "msg_jkl012",
    "role": "assistant",
    "content": "Shell command output."
  },
  "parts": [
    {
      "content": "Shell command output.",
      "contentType": "text"
    }
  ]
}
```

--------------------------------

### Configure Custom Model Variants in OpenCode

Source: https://opencode.ai/docs/models

This JSON configuration demonstrates how to define custom model variants within OpenCode. It allows for specific settings like reasoning effort and text verbosity to be applied to different named variants of a model.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "opencode": {
      "models": {
        "gpt-5": {
          "variants": {
            "high": {
              "reasoningEffort": "high",
              "textVerbosity": "low",
              "reasoningSummary": "auto"
            },
            "low": {
              "reasoningEffort": "low",
              "textVerbosity": "low",
              "reasoningSummary": "auto"
            }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Authenticate Sentry MCP Server (Bash)

Source: https://opencode.ai/docs/mcp-servers

This bash command is used to authenticate the Sentry MCP server with OpenCode. It initiates an OAuth flow that opens a browser for user authorization.

```bash
opencode mcp auth sentry
```

--------------------------------

### Import TypeScript Definitions

Source: https://opencode.ai/docs/sdk

Import TypeScript type definitions for various SDK components like Session, Message, and Part. These types enhance code safety and provide autocompletion during development.

```typescript
import type { Session, Message, Part } from "@opencode-ai/sdk"
```

--------------------------------

### Configure Model for a Mode

Source: https://opencode.ai/docs/modes

Sets a specific AI model for the 'plan' mode in the opencode.json configuration. This allows using different models optimized for distinct tasks, such as a faster model for planning.

```json
{
  "mode": {
    "plan": {
      "model": "anthropic/claude-haiku-4-20250514"
    }
  }
}
```

--------------------------------

### Template Option in JSON Configuration

Source: https://opencode.ai/docs/commands

The 'template' option within the JSON configuration defines the core prompt sent to the LLM for a specific command. This is a mandatory setting for custom commands configured via JSON.

```json
{
  "command": {
    "test": {
      "template": "Run the full test suite with coverage report and show any failures.\nFocus on the failing tests and suggest fixes."
    }
  }
}
```

--------------------------------

### Configure CodeCompanion.nvim for OpenCode ACP

Source: https://opencode.ai/docs/acp

Integrate OpenCode as an ACP agent within CodeCompanion.nvim for chat interactions. This configuration specifies 'opencode' as the adapter name and allows for setting a specific model. Environment variables can be configured separately.

```lua
require("codecompanion").setup({
  interactions = {
    chat = {
      adapter = {
        name = "opencode",
        model = "claude-sonnet-4",
      },
    },
  },
})
```

--------------------------------

### Configure Helicone Custom Headers in OpenCode

Source: https://opencode.ai/docs/providers

This JSON configuration demonstrates how to add custom headers to the Helicone provider in OpenCode. These headers can be used for features like caching and user tracking. The `options.headers` object within the provider configuration specifies these custom headers.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "helicone": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Helicone",
      "options": {
        "baseURL": "https://ai-gateway.helicone.ai",
        "headers": {
          "Helicone-Cache-Enabled": "true",
          "Helicone-User-Id": "opencode"
        }
      }
    }
  }
}
```

--------------------------------

### OpenCode GitHub Actions Workflow

Source: https://opencode.ai/docs/github

A GitHub Actions workflow file (.github/workflows/opencode.yml) that triggers OpenCode based on issue or pull request comment events containing '/oc' or '/opencode'. It checks out the repository, runs the OpenCode action, and requires environment variables for API keys.

```yaml
name: opencode

on:
  issue_comment:
    types: [created]
  pull_request_review_comment:
    types: [created]

jobs:
  opencode:
    if: |
      contains(github.event.comment.body, '/oc') ||
      contains(github.event.comment.body, '/opencode')
    runs-on: ubuntu-latest
    permissions:
      id-token: write
    steps:
       - name: Checkout repository
         uses: actions/checkout@v6
         with:
           fetch-depth: 1
           persist-credentials: false

       - name: Run OpenCode
        uses: anomalyco/opencode/github@latest
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        with:
          model: anthropic/claude-sonnet-4-20250514
          # share: true
          # github_token: xxxx

```

--------------------------------

### Configure Custom Command in JSON

Source: https://opencode.ai/docs/commands

Configure custom commands using the 'command' option in the OpenCode JSON configuration file. This method allows specifying the prompt template, description, agent, and model for each command. The key in the 'command' object becomes the command name.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "command": {
    "test": {
      "template": "Run the full test suite with coverage report and show any failures.\nFocus on the failing tests and suggest fixes.",
      "description": "Run tests with coverage",
      "agent": "build",
      "model": "anthropic/claude-3-5-sonnet-20241022"
    }
  }
}
```

--------------------------------

### Windows Terminal Shift+Enter Configuration

Source: https://opencode.ai/docs/keybinds

Configuration for Windows Terminal to send a custom input for 'Shift+Enter'. This involves modifying the 'actions' and 'keybindings' arrays in the settings.json file.

```json
"actions": [
  {
    "command": {
      "action": "sendInput",
      "input": "\u001b[13;2u"
    },
    "id": "User.sendInput.ShiftEnterCustom"
  }
]
```

```json
"keybindings": [
  {
    "keys": "shift+enter",
    "id": "User.sendInput.ShiftEnterCustom"
  }
]
```

--------------------------------

### Configure Context7 MCP Server (JSON)

Source: https://opencode.ai/docs/mcp-servers

This JSON configuration sets up the Context7 MCP server for remote access. It includes the server URL and an optional section for API key authentication using environment variables.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "context7": {
      "type": "remote",
      "url": "https://mcp.context7.com/mcp",
      "headers": {
        "CONTEXT7_API_KEY": "{env:CONTEXT7_API_KEY}"
      }
    }
  }
}
```

--------------------------------

### Define Custom 'docs' Mode with Tools (JSON)

Source: https://opencode.ai/docs/modes

This JSON configuration defines a custom 'docs' mode for OpenCode AI. It specifies a prompt file and enables 'write', 'edit', 'read', 'grep', and 'glob' tools, while disabling 'bash'. This mode is suitable for documentation generation tasks that may involve file manipulation.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mode": {
    "docs": {
      "prompt": "{file:./prompts/documentation.txt}",
      "tools": {
        "write": true,
        "edit": true,
        "bash": false,
        "read": true,
        "grep": true,
        "glob": true
      }
    }
  }
}
```

--------------------------------

### Global API

Source: https://opencode.ai/docs/sdk

Provides access to global system information, such as health status and version.

```APIDOC
## GET /global/health

### Description
Checks the health status and version of the server.

### Method
GET

### Endpoint
/global/health

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **healthy** (boolean) - Indicates if the server is healthy.
- **version** (string) - The current version of the server.

#### Response Example
```json
{
  "healthy": true,
  "version": "1.0.0"
}
```
```

--------------------------------

### Define Custom Tools for OpenCode AI

Source: https://opencode.ai/docs/plugins

This plugin demonstrates how to add custom tools to OpenCode AI. It uses the 'tool' helper to define a tool named 'mytool' with a string argument and an execution function. Custom tools are available alongside built-in tools and can override them if names conflict.

```typescript
import { type Plugin, tool } from "@opencode-ai/plugin"

export const CustomToolsPlugin: Plugin = async (ctx) => {
  return {
    tool: {
      mytool: tool({
        description: "This is a custom tool",
        args: {
          foo: tool.schema.string(),
        },
        async execute(args, context) {
          const { directory, worktree } = context
          return `Hello ${args.foo} from ${directory} (worktree: ${worktree})`
        },
      }),
    },
  }
}
```

--------------------------------

### Command with Shell Output Injection

Source: https://opencode.ai/docs/commands

Inject the output of bash commands directly into the prompt using the _!`command`_ syntax. This allows commands to dynamically gather information from the shell environment, such as test results or git logs, to inform the LLM.

```markdown
---
description: Analyze test coverage
---

Here are the current test results:
!`npm test`

Based on these results, suggest improvements to increase coverage.
```

```markdown
---
description: Review recent changes
---

Recent git commits:
!`git log --oneline -10`

Review these changes and suggest any improvements.
```

--------------------------------

### Configure OpenRouter Models in opencode.json

Source: https://opencode.ai/docs/providers

Allows customization of OpenRouter models within the opencode.json configuration file. You can add new models or specify provider options for existing ones.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "openrouter": {
      "models": {
        "somecoolnewmodel": {}
      }
    }
  }
}
```

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "openrouter": {
      "models": {
        "moonshotai/kimi-k2": {
          "options": {
            "provider": {
              "order": ["baseten"],
              "allow_fallbacks": false
            }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Python Script for Adding Numbers

Source: https://opencode.ai/docs/custom-tools

This Python script is designed to be executed by a custom tool. It takes two integer command-line arguments, calculates their sum, and prints the result to standard output.

```python
import sys

a = int(sys.argv[1])
b = int(sys.argv[2])
print(a + b)
```

--------------------------------

### Session Content API

Source: https://opencode.ai/docs/sdk

Endpoints for retrieving session messages and their parts.

```APIDOC
## GET /sessions/{path}/messages

### Description
Lists all messages within a specific session.

### Method
GET

### Endpoint
/sessions/{path}/messages

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session.

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **messages** (Array<{ info: Message, parts: Part[] }>) - An array of message objects, each containing message info and its parts.

#### Response Example
```json
{
  "messages": [
    {
      "info": {
        "id": "msg_abc",
        "content": "Hello!"
      },
      "parts": [
        {
          "type": "text",
          "content": "Hello!"
        }
      ]
    }
  ]
}
```

## GET /sessions/{path}/message

### Description
Retrieves details for a specific message within a session.

### Method
GET

### Endpoint
/sessions/{path}/message

### Parameters
#### Path Parameters
- **path** (string) - Required - The unique identifier of the session.
#### Query Parameters
- **messageId** (string) - Required - The unique identifier of the message.

### Request Example
```json
{}
```

### Response
#### Success Response (200)
- **messageDetails** ({ info: Message, parts: Part[] }) - An object containing message info and its parts.

#### Response Example
```json
{
  "messageDetails": {
    "info": {
      "id": "msg_abc",
      "content": "Hello!"
    },
    "parts": [
      {
        "type": "text",
        "content": "Hello!"
      }
    ]
  }
}
```
```

--------------------------------

### Configure Vercel AI Gateway Provider Routing in Opencode

Source: https://opencode.ai/docs/providers

This JSON snippet shows how to configure provider routing order for Vercel AI Gateway within the opencode.json configuration file. It allows specifying a sequence of providers to try for model requests.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "vercel": {
      "models": {
        "anthropic/claude-sonnet-4": {
          "options": {
            "order": ["anthropic", "vertex"]
          }
        }
      }
    }
  }
}

```

--------------------------------

### Run OpenCode in Non-Interactive Mode

Source: https://opencode.ai/docs/cli

Executes OpenCode commands directly via a prompt, bypassing the interactive TUI. This is ideal for scripting and automation. It supports attaching to a running server instance to leverage existing sessions and avoid cold boot times.

```bash
opencode run [message..]
```

```bash
opencode run "Explain the use of context in Go"
```

```bash
# Start a headless server in one terminal
opencode serve

# In another terminal, run commands that attach to it
opencode run --attach http://localhost:4096 "Explain async/await in JavaScript"
```

--------------------------------

### Define Reusable Colors in OpenCode AI Theme

Source: https://opencode.ai/docs/themes

The 'defs' section in the theme JSON allows you to define reusable color values. These definitions can then be referenced throughout the 'theme' section, promoting consistency and easier management of color schemes. No external dependencies are required.

```json
{
  "defs": {
    "nord0": "#2E3440",
    "nord1": "#3B4252",
    "nord2": "#434C5E",
    "nord3": "#4C566A",
    "nord4": "#D8DEE9",
    "nord5": "#E5E9F0",
    "nord6": "#ECEFF4",
    "nord7": "#8FBCBB",
    "nord8": "#88C0D0",
    "nord9": "#81A1C1",
    "nord10": "#5E81AC",
    "nord11": "#BF616A",
    "nord12": "#D08770",
    "nord13": "#EBCB8B",
    "nord14": "#A3BE8C",
    "nord15": "#B48EAD"
  }
}
```

--------------------------------

### Global CLI Flags (Bash)

Source: https://opencode.ai/docs/cli

Global flags applicable to all OpenCode CLI commands. These include options for help, version, printing logs, and setting the log level.

```bash
--help, -h
--version, -v
--print-logs
--log-level
```

--------------------------------

### POST /session/:id/unrevert

Source: https://opencode.ai/docs/server

Restores all reverted messages within the session.  This action undoes the effects of all reverts.

```APIDOC
## POST /session/:id/unrevert

### Description
Restore all reverted messages.

### Method
POST

### Endpoint
/session/:id/unrevert

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.

### Request Example
No request body.

### Response
#### Success Response (200)
- **boolean** - True if the restoration was successful.

#### Response Example
true

```

--------------------------------

### Specify Agent for Command Execution in opencode.json

Source: https://opencode.ai/docs/commands

The `agent` configuration option in `opencode.json` allows you to specify which agent should execute a particular command. If the specified agent is a subagent, it will trigger a subagent invocation by default, unless `subtask` is set to `false`. This is an optional setting; if omitted, the command defaults to the current agent.

```json
{
  "command": {
    "review": {
      "agent": "plan"
    }
  }
}
```

--------------------------------

### Access Tool Context Information

Source: https://opencode.ai/docs/custom-tools

This TypeScript tool definition demonstrates how to access and utilize context information provided to the tool during execution. It retrieves details like agent, sessionID, messageID, directory, and worktree from the context object.

```typescript
import { tool } from "@opencode-ai/plugin"

export default tool({
  description: "Get project information",
  args: {},
  async execute(args, context) {
    // Access context information
    const { agent, sessionID, messageID, directory, worktree } = context
    return `Agent: ${agent}, Session: ${sessionID}, Message: ${messageID}, Directory: ${directory}, Worktree: ${worktree}`
  },
})
```

--------------------------------

### Configure Provider Base URL in OpenCode JSON

Source: https://opencode.ai/docs/providers

This JSON snippet demonstrates how to configure a custom base URL for a specific AI provider (Anthropic in this case) within the OpenCode configuration file. This is useful for routing requests through proxy services or custom endpoints.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "anthropic": {
      "options": {
        "baseURL": "https://api.anthropic.com/v1"
      }
    }
  }
}
```

--------------------------------

### Skill Name Validation Regex

Source: https://opencode.ai/docs/skills

Presents the regular expression used to validate the format of skill names, ensuring they adhere to specific character and separator rules.

```regex
^[a-z0-9]+(-[a-z0-9]+)*$

```

--------------------------------

### Handle Structured Output Error in TypeScript

Source: https://opencode.ai/docs/sdk

Demonstrates how to check for and handle a StructuredOutputError if the model fails to produce valid structured output after retries. It logs the error message and the number of attempts made.

```typescript
if (result.data.info.error?.name === "StructuredOutputError") {
  console.error("Failed to produce structured output:", result.data.info.error.message)
  console.error("Attempts:", result.data.info.error.retries)
}
```

--------------------------------

### Events API

Source: https://opencode.ai/docs/de/sdk

API for subscribing to server-sent events.

```APIDOC
## GET /api/event/subscribe

### Description
Subscribe to a stream of server-sent events.

### Method
GET

### Endpoint
`/api/event/subscribe`

### Parameters
(No parameters)

### Response
#### Success Response (200)
- **stream** (ReadableStream) - A stream of event objects, each with a `type` and `properties`.

### Request Example
```javascript
const events = await client.event.subscribe();
for await (const event of events.stream) {
  console.log("Event:", event.type, event.properties);
}
```
```

--------------------------------

### Configure Zed Editor for OpenCode ACP

Source: https://opencode.ai/docs/acp

Add OpenCode as an agent server in Zed's settings.json. This allows Zed to communicate with OpenCode via the ACP protocol using the `opencode acp` command. You can also bind a keyboard shortcut for easier access.

```json
{
  "agent_servers": {
    "OpenCode": {
      "command": "opencode",
      "args": ["acp"]
    }
  }
}
```

```json
[
  {
    "bindings": {
      "cmd-alt-o": [
        "agent::NewExternalAgentThread",
        {
          "agent": {
            "custom": {
              "name": "OpenCode",
              "command": {
                "command": "opencode",
                "args": ["acp"]
              }
            }
          }
        }
      ]
    }
  }
]
```

--------------------------------

### Control Response Diversity with Top P

Source: https://opencode.ai/docs/agents

Control response diversity and randomness using the 'top_p' option, which ranges from 0.0 to 1.0. Lower values result in more focused responses, while higher values yield more diverse outputs.

```json
{
  "agent": {
    "brainstorm": {
      "top_p": 0.9
    }
  }
}
```

--------------------------------

### Override or Add Custom Variants in OpenCode

Source: https://opencode.ai/docs/models

This JSON configuration illustrates how to override existing model variants or add new custom ones for providers like OpenAI. It shows how to define specific configurations for variants like 'thinking' or disable variants entirely.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "openai": {
      "models": {
        "gpt-5": {
          "variants": {
            "thinking": {
              "reasoningEffort": "high",
              "textVerbosity": "low"
            },
            "fast": {
              "disabled": true
            }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Configure Grep by Vercel MCP Server (JSON)

Source: https://opencode.ai/docs/mcp-servers

This JSON configuration adds the Grep by Vercel MCP server for searching code snippets on GitHub. It specifies the server type as 'remote' and provides the corresponding URL.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "gh_grep": {
      "type": "remote",
      "url": "https://mcp.grep.app"
    }
  }
}
```

--------------------------------

### Configure Remote MCP Server in OpenCode

Source: https://opencode.ai/docs/mcp-servers

Shows how to configure a remote MCP server in `opencode.json`. It specifies the server type as 'remote', provides the server's URL, and includes an option for custom headers, such as authentication tokens, to access the remote service.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-remote-mcp": {
      "type": "remote",
      "url": "https://my-mcp-server.com",
      "enabled": true,
      "headers": {
        "Authorization": "Bearer MY_API_KEY"
      }
    }
  }
}
```

--------------------------------

### OpenCode Share Command

Source: https://opencode.ai/docs/share

Manually triggers the sharing of the current OpenCode conversation. This command generates a unique public URL for the session and copies it to the clipboard.

```shell
/share
```

--------------------------------

### Set SAP AI Core Service Key via Environment Variable

Source: https://opencode.ai/docs/providers

Sets the SAP AI Core service key as an environment variable for the opencode command. This is an alternative to entering the key during the /connect process.

```bash
AICORE_SERVICE_KEY='{"clientid":"...","clientsecret":"...","url":"...","serviceurls":{"AI_API_URL":"..."}}' opencode
```

--------------------------------

### Session Summarization API

Source: https://opencode.ai/docs/de/server

Endpoint to generate a summary for a session.

```APIDOC
## POST /session/:id/summarize

### Description
Generate a summary for the entire session.

### Method
POST

### Endpoint
/session/:id/summarize

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to summarize.
#### Request Body
- **providerID** (string) - Required - The ID of the AI provider to use for summarization.
- **modelID** (string) - Required - The ID of the AI model to use for summarization.

### Request Example
```json
{
  "providerID": "openai",
  "modelID": "gpt-3.5-turbo"
}
```

### Response
#### Success Response (200)
- **success** (boolean) - Indicates if the summarization process was initiated successfully.

#### Response Example
```json
true
```
```

--------------------------------

### POST /session/:id/revert

Source: https://opencode.ai/docs/server

Reverts a specific message within the session.  Allows undoing changes made by a particular message.

```APIDOC
## POST /session/:id/revert

### Description
Revert a message.

### Method
POST

### Endpoint
/session/:id/revert

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.

#### Request Body
- **messageID** (string) - Required - The ID of the message to revert.
- **partID** (string) - Optional - The ID of the part to revert.

### Request Example
{
  "messageID": "message1",
  "partID": "part1"
}

### Response
#### Success Response (200)
- **boolean** - True if the reversion was successful.

#### Response Example
true

```

--------------------------------

### Configure Custom Inference Profile for Bedrock Model in OpenCode

Source: https://opencode.ai/docs/providers

Specify custom inference profiles for specific Bedrock models in `opencode.json`. This ensures correct caching and model identification using ARNs.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "amazon-bedrock": {
      "models": {
        "anthropic-claude-sonnet-4.5": {
          "id": "arn:aws:bedrock:us-east-1:xxx:application-inference-profile/yyy"
        }
      }
    }
  }
}
```

--------------------------------

### Export Session Data (Bash)

Source: https://opencode.ai/docs/cli

Exports session data as JSON. If no session ID is provided, the user will be prompted to select from available sessions.

```bash
opencode export [sessionID]
```

--------------------------------

### PATCH /session/:id

Source: https://opencode.ai/docs/server

Updates the properties of an existing session.  Allows modification of session attributes like the title.

```APIDOC
## PATCH /session/:id

### Description
Update session properties.

### Method
PATCH

### Endpoint
/session/:id

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to update.

#### Request Body
- **title** (string) - Optional - The new title for the session.

### Request Example
{
  "title": "Updated Session Title"
}

### Response
#### Success Response (200)
- **Session** - The updated Session object.

#### Response Example
{
  "id": "session1",
  "title": "Updated Session Title",
  // ... other session properties
}

```

--------------------------------

### Grant Permissions for GitHub Token Authentication

Source: https://opencode.ai/docs/github

YAML snippet showing the necessary permissions to grant the GitHub Action runner when using the built-in GITHUB_TOKEN for authentication with OpenCode, enabling operations like commits and pull requests.

```yaml
permissions:
  id-token: write
  contents: write
  pull-requests: write
  issues: write

```

--------------------------------

### TUI (Text User Interface) API

Source: https://opencode.ai/docs/de/sdk

APIs for interacting with and controlling the Text User Interface elements.

```APIDOC
## POST /api/tui/appendPrompt

### Description
Append text to the current prompt in the TUI.

### Method
POST

### Endpoint
`/api/tui/appendPrompt`

### Parameters
#### Request Body
- **text** (string) - Required - The text to append to the prompt.

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the text was successfully appended.

### Request Example
```javascript
await client.tui.appendPrompt({ body: { text: "Add this to prompt" } });
```

## POST /api/tui/openHelp

### Description
Open the help dialog in the TUI.

### Method
POST

### Endpoint
`/api/tui/openHelp`

### Parameters
(No parameters)

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the help dialog was opened.

### Request Example
```javascript
await client.tui.openHelp();
```

## POST /api/tui/openSessions

### Description
Open the session selector dialog in the TUI.

### Method
POST

### Endpoint
`/api/tui/openSessions`

### Parameters
(No parameters)

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the session selector was opened.

### Request Example
```javascript
await client.tui.openSessions();
```

## POST /api/tui/openThemes

### Description
Open the theme selector dialog in the TUI.

### Method
POST

### Endpoint
`/api/tui/openThemes`

### Parameters
(No parameters)

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the theme selector was opened.

### Request Example
```javascript
await client.tui.openThemes();
```

## POST /api/tui/openModels

### Description
Open the model selector dialog in the TUI.

### Method
POST

### Endpoint
`/api/tui/openModels`

### Parameters
(No parameters)

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the model selector was opened.

### Request Example
```javascript
await client.tui.openModels();
```

## POST /api/tui/submitPrompt

### Description
Submit the current prompt in the TUI.

### Method
POST

### Endpoint
`/api/tui/submitPrompt`

### Parameters
(No parameters)

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the prompt was submitted.

### Request Example
```javascript
await client.tui.submitPrompt();
```

## POST /api/tui/clearPrompt

### Description
Clear the current prompt in the TUI.

### Method
POST

### Endpoint
`/api/tui/clearPrompt`

### Parameters
(No parameters)

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the prompt was cleared.

### Request Example
```javascript
await client.tui.clearPrompt();
```

## POST /api/tui/executeCommand

### Description
Execute a command within the TUI.

### Method
POST

### Endpoint
`/api/tui/executeCommand`

### Parameters
#### Request Body
- **command** (string) - Required - The command to execute.

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the command was executed successfully.

### Request Example
```javascript
// Assuming 'client' is an initialized Opencode AI client
// await client.tui.executeCommand({ body: { command: "some-command" } });
```

## POST /api/tui/showToast

### Description
Show a toast notification in the TUI.

### Method
POST

### Endpoint
`/api/tui/showToast`

### Parameters
#### Request Body
- **message** (string) - Required - The message to display in the toast.
- **variant** (string) - Optional - The variant of the toast (e.g., `"success"`, `"error"`, `"info"`).

### Response
#### Success Response (200)
- **boolean** (boolean) - Indicates if the toast was shown.

### Request Example
```javascript
await client.tui.showToast({ body: { message: "Task completed", variant: "success" } });
```
```

--------------------------------

### Anthropic Authentication Options in OpenCode

Source: https://opencode.ai/docs/providers

Display of authentication method selection for Anthropic within the OpenCode terminal interface. Options include Claude Pro/Max, creating an API key, or manual entry.

```text
┌ Select auth method
│
│ Claude Pro/Max
│ Create an API Key
│ Manually enter API Key
└
```

--------------------------------

### DELETE /session/:id

Source: https://opencode.ai/docs/server

Deletes a session and all its associated data.  This action is irreversible.

```APIDOC
## DELETE /session/:id

### Description
Deletes a session and all its data.

### Method
DELETE

### Endpoint
/session/:id

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to delete.

### Request Example
No request body.

### Response
#### Success Response (200)
- **boolean** - True if the session was successfully deleted.

#### Response Example
true

```

--------------------------------

### Define a Single Tool in TypeScript

Source: https://opencode.ai/docs/custom-tools

This snippet shows how to define a single custom tool named 'database' using the `tool()` helper in TypeScript. It includes a description, argument schema using Zod, and an execute function. The filename '.opencode/tools/database.ts' determines the tool name.

```typescript
import { tool } from "@opencode-ai/plugin"

export default tool({
  description: "Query the project database",
  args: {
    query: tool.schema.string().describe("SQL query to execute"),
  },
  async execute(args) {
    // Your database logic here
    return `Executed query: ${args.query}`
  },
})
```

--------------------------------

### Send macOS Notifications with AppleScript

Source: https://opencode.ai/docs/plugins

This plugin sends a system notification on macOS when a session is completed. It utilizes the 'osascript' command to execute AppleScript. This is useful for alerting users to the end of a process.

```javascript
export const NotificationPlugin = async ({ project, client, $, directory, worktree }) => {
  return {
    event: async ({ event }) => {
      // Send notification on session completion
      if (event.type === "session.idle") {
        await $`osascript -e 'display notification "Session completed!" with title "opencode"'`
      }
    },
  }
}
```

--------------------------------

### Enable Edit Tool in OpenCode

Source: https://opencode.ai/docs/tools

Grant 'allow' permission for the 'edit' tool in opencode.json to permit the LLM to modify existing files. This tool performs exact string replacements, serving as the primary mechanism for code alterations by the LLM.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "edit": "allow"
  }
}
```

--------------------------------

### File Operations API

Source: https://opencode.ai/docs/de/sdk

APIs for searching text within files, finding files and directories, and reading file content.

```APIDOC
## POST /api/find/text

### Description
Search for text patterns within files in the workspace.

### Method
POST

### Endpoint
`/api/find/text`

### Parameters
#### Query Parameters
- **pattern** (string) - Required - The regular expression pattern to search for.

### Response
#### Success Response (200)
- **matches** (array) - An array of match objects, each containing `path`, `lines`, `line_number`, `absolute_offset`, and `submatches`.

### Request Example
```javascript
const textResults = await client.find.text({ query: { pattern: "function.*opencode" } });
```

## POST /api/find/files

### Description
Find files and directories by name within the workspace or a specified directory.

### Method
POST

### Endpoint
`/api/find/files`

### Parameters
#### Query Parameters
- **query** (string) - Required - The filename or pattern to search for (e.g., `"*.ts"`).
- **type** (string) - Optional - Specifies whether to find `"file"` or `"directory"`.
- **directory** (string) - Optional - Overrides the project root for the search.
- **limit** (integer) - Optional - Maximum number of results to return (1-200).

### Response
#### Success Response (200)
- **paths** (string[]) - An array of file or directory paths matching the query.

### Request Example
```javascript
// Find TypeScript files
const files = await client.find.files({ query: { query: "*.ts", type: "file" } });

// Find directories with a limit
const directories = await client.find.files({ query: { query: "packages", type: "directory", limit: 20 } });
```

## POST /api/find/symbols

### Description
Find workspace symbols (e.g., functions, classes, variables).

### Method
POST

### Endpoint
`/api/find/symbols`

### Parameters
#### Query Parameters
- **query** (string) - Required - The symbol name or pattern to search for.

### Response
#### Success Response (200)
- **symbols** (Symbol[]) - An array of symbol objects.

### Request Example
```javascript
// Assuming 'client' is an initialized Opencode AI client
// const symbols = await client.find.symbols({ query: { query: "myFunction" } });
```

## POST /api/file/read

### Description
Read the content of a specific file.

### Method
POST

### Endpoint
`/api/file/read`

### Parameters
#### Query Parameters
- **path** (string) - Required - The path to the file to read.

### Response
#### Success Response (200)
- **type** (string) - The type of content returned (`"raw"` or `"patch"`).
- **content** (string) - The content of the file.

### Request Example
```javascript
const content = await client.file.read({ query: { path: "src/index.ts" } });
```

## POST /api/file/status

### Description
Get the status for tracked files (e.g., modified, added, deleted).

### Method
POST

### Endpoint
`/api/file/status`

### Parameters
#### Query Parameters
- **query** (object) - Optional - Query parameters for filtering file status.

### Response
#### Success Response (200)
- **files** (File[]) - An array of file status objects.

### Request Example
```javascript
// Assuming 'client' is an initialized Opencode AI client
// const fileStatus = await client.file.status({ query: {} });
```
```

--------------------------------

### Disable Skill Tool for Built-in Agent

Source: https://opencode.ai/docs/skills

Illustrates how to disable the skill tool for a built-in agent, like 'plan', within the `opencode.json` configuration.

```json
{
  "agent": {
    "plan": {
      "tools": {
        "skill": false
      }
    }
  }
}

```

--------------------------------

### Enable MCP Per Agent with Glob Pattern (JSON)

Source: https://opencode.ai/docs/mcp-servers

This JSON configuration shows how to disable an MCP server globally while enabling it for a specific agent using a glob pattern. This allows for fine-grained control over MCP availability.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-mcp": {
      "type": "local",
      "command": ["bun", "x", "my-mcp-command"],
      "enabled": true
    }
  },
  "tools": {
    "my-mcp*": false
  },
  "agent": {
    "my-agent": {
      "tools": {
        "my-mcp*": true
      }
    }
  }
}
```

--------------------------------

### Configure JetBrains IDEs for OpenCode ACP

Source: https://opencode.ai/docs/acp

Integrate OpenCode into JetBrains IDEs by adding an entry to your `acp.json` file. This configuration specifies the absolute path to the OpenCode executable and the 'acp' argument for ACP communication.

```json
{
  "agent_servers": {
    "OpenCode": {
      "command": "/absolute/path/bin/opencode",
      "args": ["acp"]
    }
  }
}
```

--------------------------------

### Globally Disabling All LSP Servers

Source: https://opencode.ai/docs/lsp

This JSON configuration shows how to disable all Language Server Protocol (LSP) servers globally within OpenCode. By setting the `lsp` property to `false`, OpenCode will not attempt to download or run any LSP servers, regardless of file type or project dependencies.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "lsp": false
}
```

--------------------------------

### Configure Remote MCP Server with Pre-registered OAuth Credentials

Source: https://opencode.ai/docs/mcp-servers

This configuration enables a remote MCP server connection with pre-registered OAuth credentials. Provide 'clientId', 'clientSecret', and desired 'scope'. These values can be sourced from environment variables for security.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-oauth-server": {
      "type": "remote",
      "url": "https://mcp.example.com/mcp",
      "oauth": {
        "clientId": "{env:MY_MCP_CLIENT_ID}",
        "clientSecret": "{env:MY_MCP_CLIENT_SECRET}",
        "scope": "tools:read tools:execute"
      }
    }
  }
}
```

--------------------------------

### Configure Custom CA Certificates for OpenCode

Source: https://opencode.ai/docs/network

Sets the NODE_EXTRA_CA_CERTS environment variable to specify the path of a custom CA certificate file. This allows OpenCode to trust custom Certificate Authorities for secure HTTPS connections, including proxy and direct API access.

```bash
export NODE_EXTRA_CA_CERTS=/path/to/ca-cert.pem
```

--------------------------------

### Configure Sentry MCP Server (JSON)

Source: https://opencode.ai/docs/mcp-servers

This JSON snippet configures the Sentry MCP server, specifying its type as 'remote' and providing the necessary URL. After configuration, authentication via the command line is required.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "sentry": {
      "type": "remote",
      "url": "https://mcp.sentry.dev/mcp",
      "oauth": {}
    }
  }
}
```

--------------------------------

### Automated Pull Request Review with OpenCode

Source: https://opencode.ai/docs/github

This GitHub Actions workflow automatically triggers OpenCode to review pull requests when they are opened, updated, or reopened. It requires GITHUB_TOKEN and ANTHROPIC_API_KEY for authentication. If no prompt is provided, OpenCode defaults to a standard PR review.

```yaml
name: opencode-review

on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

jobs:
  review:
    runs-on: ubuntu-latest
    permissions:
      id-token: write
      contents: read
      pull-requests: read
      issues: read
    steps:
      - uses: actions/checkout@v6
        with:
          persist-credentials: false
      - uses: anomalyco/opencode/github@latest
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          model: anthropic/claude-sonnet-4-20250514
          use_github_token: true
          prompt: |
            Review this pull request:
            - Check for code quality issues
            - Look for potential bugs
            - Suggest improvements
```

--------------------------------

### Session Permissions API

Source: https://opencode.ai/docs/de/server

Endpoint to respond to a permission request for a session.

```APIDOC
## POST /session/:id/permissions/:permissionID

### Description
Respond to a specific permission request within a session.

### Method
POST

### Endpoint
/session/:id/permissions/:permissionID

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.
- **permissionID** (string) - Required - The ID of the permission request to respond to.
#### Request Body
- **response** (string) - Required - The response to the permission request (e.g., 'allow', 'deny').
- **remember** (boolean) - Optional - Whether to remember this decision for future requests.

### Request Example
```json
{
  "response": "allow",
  "remember": true
}
```

### Response
#### Success Response (200)
- **success** (boolean) - Indicates if the permission response was processed successfully.

#### Response Example
```json
true
```
```

--------------------------------

### Provider API

Source: https://opencode.ai/docs/de/server

Endpoints for managing and authenticating with external providers.

```APIDOC
## GET /provider

### Description
Lists all available providers, including their default settings and connected status.

### Method
GET

### Endpoint
/provider

### Parameters
#### Path Parameters
None

#### Query Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **all** (Provider[]) - An array of all provider objects.
- **default** (object) - Default provider settings.
- **connected** (string[]) - An array of IDs for connected providers.

#### Response Example
```json
{
  "all": [
    {
      "id": "provider1",
      "name": "Provider One"
    }
  ],
  "default": {
    "provider1": "model-a"
  },
  "connected": ["provider1"]
}
```

## GET /provider/auth

### Description
Retrieves the authentication methods available for each provider.

### Method
GET

### Endpoint
/provider/auth

### Parameters
#### Path Parameters
None

#### Query Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **[providerID]** (ProviderAuthMethod[]) - An object where keys are provider IDs and values are arrays of their authentication methods.

#### Response Example
```json
{
  "provider1": [
    {
      "type": "oauth2",
      "clientId": "..."
    }
  ]
}
```

## POST /provider/{id}/oauth/authorize

### Description
Initiates the OAuth authorization flow for a specific provider.

### Method
POST

### Endpoint
/provider/{id}/oauth/authorize

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the provider to authorize.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **authorizationUrl** (string) - The URL to redirect the user to for OAuth authorization.

#### Response Example
```json
{
  "authorizationUrl": "https://example.com/auth/authorize?client_id=..."
}
```

## POST /provider/{id}/oauth/callback

### Description
Handles the callback from the OAuth provider after user authorization.

### Method
POST

### Endpoint
/provider/{id}/oauth/callback

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the provider handling the callback.

#### Query Parameters
None

#### Request Body
- **code** (string) - Required - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter used in the authorization request.

### Request Example
```json
{
  "code": "received_auth_code",
  "state": "some_random_string"
}
```

### Response
#### Success Response (200)
- **success** (boolean) - Indicates if the callback was processed successfully.

#### Response Example
```json
{
  "success": true
}
```
```

--------------------------------

### Uninstall OpenCode (Bash)

Source: https://opencode.ai/docs/cli

Uninstalls OpenCode and removes all related files. Flags like `--keep-config`, `--keep-data`, `--dry-run`, and `--force` modify the uninstallation behavior.

```bash
opencode uninstall
```

--------------------------------

### Session Management API

Source: https://opencode.ai/docs/de/server

Endpoints for managing sessions, including listing all sessions, creating new sessions, retrieving session details, deleting sessions, and updating session properties.

```APIDOC
## GET /session

### Description
List all available sessions.

### Method
GET

### Endpoint
/session

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **sessions** (Session[]) - An array of session objects.

#### Response Example
```json
[
  {
    "id": "session_123",
    "title": "My First Session",
    "createdAt": "2023-10-27T10:00:00Z"
  }
]
```

## POST /session

### Description
Create a new session.

### Method
POST

### Endpoint
/session

### Parameters
#### Request Body
- **parentID** (string) - Optional - The ID of the parent session.
- **title** (string) - Optional - The title for the new session.

### Request Example
```json
{
  "title": "New Project Session"
}
```

### Response
#### Success Response (200)
- **session** (Session) - The newly created session object.

#### Response Example
```json
{
  "id": "session_456",
  "title": "New Project Session",
  "createdAt": "2023-10-27T10:05:00Z"
}
```

## GET /session/:id

### Description
Retrieve details for a specific session.

### Method
GET

### Endpoint
/session/:id

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to retrieve.

### Request Example
None

### Response
#### Success Response (200)
- **session** (Session) - The session object with details.

#### Response Example
```json
{
  "id": "session_123",
  "title": "My First Session",
  "createdAt": "2023-10-27T10:00:00Z"
}
```

## DELETE /session/:id

### Description
Delete a session and all its associated data.

### Method
DELETE

### Endpoint
/session/:id

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to delete.

### Request Example
None

### Response
#### Success Response (200)
- **success** (boolean) - Indicates if the deletion was successful.

#### Response Example
```json
true
```

## PATCH /session/:id

### Description
Update properties of an existing session.

### Method
PATCH

### Endpoint
/session/:id

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to update.
#### Request Body
- **title** (string) - Optional - The new title for the session.

### Request Example
```json
{
  "title": "Updated Session Title"
}
```

### Response
#### Success Response (200)
- **session** (Session) - The updated session object.

#### Response Example
```json
{
  "id": "session_123",
  "title": "Updated Session Title",
  "createdAt": "2023-10-27T10:00:00Z"
}
```
```

--------------------------------

### Restrict Edits in External Directories (JSON)

Source: https://opencode.ai/docs/permissions

Combine `external_directory` with specific tool permissions to create nuanced access controls. This configuration allows reads but denies edits within `~/projects/personal/`.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "external_directory": {
      "~/projects/personal/**": "allow"
    },
    "edit": {
      "~/projects/personal/**": "deny"
    }
  }
}
```

--------------------------------

### Override Default Model for a Command in opencode.json

Source: https://opencode.ai/docs/commands

The `model` configuration option in `opencode.json` enables you to override the default language model used for executing a specific command. This allows for flexibility in choosing models based on command requirements. This is an optional configuration.

```json
{
  "command": {
    "analyze": {
      "model": "anthropic/claude-3-5-sonnet-20241022"
    }
  }
}
```

--------------------------------

### Anthropic Claude Endpoints

Source: https://opencode.ai/docs/zen

Endpoints for interacting with Anthropic's Claude models.

```APIDOC
## POST /zen/v1/messages

### Description
This endpoint is used to send messages to and receive responses from Anthropic's Claude models.

### Method
POST

### Endpoint
`https://opencode.ai/zen/v1/messages`

### Parameters
#### Query Parameters
- **model** (string) - Required - The ID of the Claude model to use (e.g., `claude-opus-4-6`, `claude-sonnet-4.5`).

#### Request Body
- **messages** (array) - Required - An array of message objects representing the conversation history.
  - **role** (string) - The role of the message sender (e.g., `user`, `assistant`).
  - **content** (string) - The content of the message.
- **max_tokens** (integer) - Optional - The maximum number of tokens to generate.

### Request Example
```json
{
  "messages": [
    {"role": "user", "content": "Explain the concept of recursion in programming."} 
  ],
  "max_tokens": 300
}
```

### Response
#### Success Response (200)
- **content** (array) - An array of content blocks in the response.
  - **type** (string) - The type of content (e.g., `text`).
  - **text** (string) - The text content of the response.

#### Response Example
```json
{
  "content": [
    {
      "type": "text",
      "text": "Recursion in programming is a method where the solution to a problem depends on solutions to smaller instances of the same problem. In essence, a function calls itself."
    }
  ]
}
```
```

--------------------------------

### Configure AWS Authentication in Bash Profile for OpenCode

Source: https://opencode.ai/docs/providers

Persistently configure AWS profile and region in your bash profile for OpenCode usage. This ensures consistent authentication across sessions.

```bash
export AWS_PROFILE=my-dev-profile
export AWS_REGION=us-east-1
```

--------------------------------

### Configure Remote MCP Server with Automatic OAuth

Source: https://opencode.ai/docs/mcp-servers

This configuration sets up a remote MCP server connection. OpenCode will automatically handle OAuth authentication if the server requires it. Ensure the 'type' is 'remote' and provide the server's 'url'.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-oauth-server": {
      "type": "remote",
      "url": "https://mcp.example.com/mcp"
    }
  }
}
```

--------------------------------

### Inherit Terminal Defaults in OpenCode AI Theme

Source: https://opencode.ai/docs/themes

To create themes that seamlessly blend with your terminal's color scheme, you can use the special value 'none' for any color property. This tells OpenCode AI to use the terminal's default foreground or background color as specified. This is useful for ensuring readability and aesthetic consistency.

```json
{
  "theme": {
    "text": "none",
    "background": "none"
  }
}
```

--------------------------------

### Inject Environment Variables into Shell

Source: https://opencode.ai/docs/plugins

This plugin injects custom environment variables into all shell executions, including AI tools and user terminals. It modifies the 'shell.env' hook to add variables like 'MY_API_KEY' and 'PROJECT_ROOT'. This is useful for providing necessary context to shell commands.

```javascript
export const InjectEnvPlugin = async () => {
  return {
    "shell.env": async (input, output) => {
      output.env.MY_API_KEY = "secret"
      output.env.PROJECT_ROOT = input.cwd
    },
  }
}
```

--------------------------------

### Set EDITOR Environment Variable (Windows PowerShell)

Source: https://opencode.ai/docs/tui

Configures the default text editor for OpenCode commands using Windows PowerShell. It shows how to set the EDITOR environment variable for editors like notepad and VS Code with the '--wait' flag. For permanent changes, modify your PowerShell profile.

```powershell
$env:EDITOR = "notepad"

# For GUI editors, VS Code, Cursor, VSCodium, Windsurf, Zed, etc.
# include --wait
$env:EDITOR = "code --wait"
```

--------------------------------

### Define 'refactor' Mode with Specific Model (Markdown)

Source: https://opencode.ai/docs/modes

This markdown file configures a global 'refactor' mode for OpenCode AI, specifying an Anthropic model and a temperature. It enables 'edit', 'read', 'grep', and 'glob' tools while disabling others. The description outlines the mode's focus on improving code quality and maintainability.

```markdown
---
model: anthropic/claude-sonnet-4-20250514
temperature: 0.2
tools:
  edit: true
  read: true
  grep: true
  glob: true
---

You are in refactoring mode. Focus on improving code quality without changing functionality.

Priorities:

- Improve code readability and maintainability
- Apply consistent naming conventions
- Reduce code duplication
- Optimize performance where appropriate
- Ensure all tests continue to pass
```

--------------------------------

### Configure Temperature for Modes

Source: https://opencode.ai/docs/modes

Adjusts the 'temperature' setting for different modes in opencode.json to control the randomness and creativity of AI responses. Lower values are for focused tasks, higher for creative exploration.

```json
{
  "mode": {
    "plan": {
      "temperature": 0.1
    },
    "creative": {
      "temperature": 0.8
    }
  }
}
```

--------------------------------

### Configure Tools in Readonly Mode (JSON)

Source: https://opencode.ai/docs/modes

This JSON snippet demonstrates how to configure the 'readonly' mode in OpenCode AI, specifically disabling 'write', 'edit', and 'bash' tools while enabling 'read', 'grep', and 'glob'. This is useful for scenarios where you want to inspect code or files without making any modifications.

```json
{
  "mode": {
    "readonly": {
      "tools": {
        "write": false,
        "edit": false,
        "bash": false,
        "read": true,
        "grep": true,
        "glob": true
      }
    }
  }
}
```

--------------------------------

### Session Sharing API

Source: https://opencode.ai/docs/de/server

Endpoints for sharing and unsharing a session.

```APIDOC
## POST /session/:id/share

### Description
Share a session, making it accessible to others.

### Method
POST

### Endpoint
/session/:id/share

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to share.

### Request Example
None

### Response
#### Success Response (200)
- **session** (Session) - The session object, potentially with updated sharing information.

#### Response Example
```json
{
  "id": "session_123",
  "title": "My First Session",
  "shared": true,
  "createdAt": "2023-10-27T10:00:00Z"
}
```

## DELETE /session/:id/share

### Description
Unshare a session, revoking access for others.

### Method
DELETE

### Endpoint
/session/:id/share

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to unshare.

### Request Example
None

### Response
#### Success Response (200)
- **session** (Session) - The session object, potentially with updated sharing information.

#### Response Example
```json
{
  "id": "session_123",
  "title": "My First Session",
  "shared": false,
  "createdAt": "2023-10-27T10:00:00Z"
}
```
```

--------------------------------

### Session Messaging API

Source: https://opencode.ai/docs/de/sdk

Endpoints for listing and retrieving messages within a session, and sending prompts.

```APIDOC
## GET /session/messages

### Description
Lists all messages within a specific session.

### Method
GET

### Endpoint
/session/messages

### Parameters
#### Query Parameters
- **path** (string) - Required - The unique identifier for the session.

### Request Example
```
/session/messages?path=session-123
```

### Response
#### Success Response (200)
- **messages** (Array) - An array containing message info and parts.
  - **info** (Message) - The message metadata.
  - **parts** (Part[]) - An array of message parts.

#### Response Example
```json
[
  {
    "info": {"id": "msg-abc", "sender": "user"},
    "parts": [{"type": "text", "content": "Hello"}]
  }
]
```

## GET /session/message

### Description
Retrieves details for a specific message within a session.

### Method
GET

### Endpoint
/session/message

### Parameters
#### Query Parameters
- **path** (string) - Required - The unique identifier for the session.
- **messageId** (string) - Required - The unique identifier for the message.

### Request Example
```
/session/message?path=session-123&messageId=msg-abc
```

### Response
#### Success Response (200)
- **message** (object) - Contains message info and parts.
  - **info** (Message) - The message metadata.
  - **parts** (Part[]) - An array of message parts.

#### Response Example
```json
{
  "info": {"id": "msg-abc", "sender": "user"},
  "parts": [{"type": "text", "content": "Hello"}]
}
```

## POST /session/prompt

### Description
Sends a prompt message to a session.

### Method
POST

### Endpoint
/session/prompt

### Parameters
#### Query Parameters
- **path** (string) - Required - The unique identifier for the session.
#### Request Body
- **body** (object) - Required - The prompt message payload.
  - **content** (string) - The text content of the prompt.
  - **noReply** (boolean) - Optional - If true, only the user message is sent without an AI reply.

### Request Example
```json
{
  "path": "session-123",
  "body": {
    "content": "What is the capital of France?",
    "noReply": false
  }
}
```

### Response
#### Success Response (200)
- **response** (object) - The AI's response or confirmation.
  - **info** (AssistantMessage) - The AI message metadata.
  - **parts** (Part[]) - An array of message parts.

#### Response Example
```json
{
  "info": {"id": "msg-def", "sender": "assistant"},
  "parts": [{"type": "text", "content": "The capital of France is Paris."}]
}
```
```

--------------------------------

### Fix GitLab Issue using OpenCode AI (Command)

Source: https://opencode.ai/docs/gitlab

This command instructs OpenCode AI to fix an issue in GitLab. When posted in an issue, OpenCode will create a new branch, implement the necessary changes, and open a merge request.

```shell
@opencode fix this
```

--------------------------------

### Enable MCP Server in OpenCode Config

Source: https://opencode.ai/docs/mcp-servers

Defines how to enable or disable MCP servers within the OpenCode configuration file (`opencode.jsonc`). MCP servers are added under the `mcp` key, each with a unique name and an `enabled` flag. Setting `enabled` to `false` temporarily disables a server without removing it.

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "name-of-mcp-server": {
      // ...
      "enabled": true
    },
    "name-of-other-mcp-server": {
      // ...
    }
  }
}
```

--------------------------------

### Session Revert API

Source: https://opencode.ai/docs/de/server

Endpoints for reverting and restoring messages within a session.

```APIDOC
## POST /session/:id/revert

### Description
Revert a specific message within a session.

### Method
POST

### Endpoint
/session/:id/revert

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.
#### Request Body
- **messageID** (string) - Required - The ID of the message to revert.
- **partID** (string) - Optional - The specific part of the message to revert, if applicable.

### Request Example
```json
{
  "messageID": "msg_def",
  "partID": "part_1"
}
```

### Response
#### Success Response (200)
- **success** (boolean) - Indicates if the message was reverted successfully.

#### Response Example
```json
true
```

## POST /session/:id/unrevert

### Description
Restore all messages that have been previously reverted in a session.

### Method
POST

### Endpoint
/session/:id/unrevert

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.

### Request Example
None

### Response
#### Success Response (200)
- **success** (boolean) - Indicates if all reverted messages were restored successfully.

#### Response Example
```json
true
```
```

--------------------------------

### Security Auditor Agent Configuration

Source: https://opencode.ai/docs/agents

Configuration for a 'security-auditor' agent focused on performing security audits and identifying vulnerabilities. It runs in 'subagent' mode, disables 'write' and 'edit' tools, and emphasizes input validation, authentication, and data exposure risks.

```markdown
---

```

```markdown
description: Performs security audits and identifies vulnerabilities

```

```markdown
mode: subagent

```

```markdown
tools:
  write: false
  edit: false

```

```markdown
---

```

```markdown

You are a security expert. Focus on identifying potential security issues.

```

```markdown

Look for:

- Input validation vulnerabilities
- Authentication and authorization flaws
- Data exposure risks
- Dependency vulnerabilities
- Configuration security issues

```

--------------------------------

### DELETE /session/:id/share

Source: https://opencode.ai/docs/server

Unshares a session.  This action removes sharing permissions for the session.

```APIDOC
## DELETE /session/:id/share

### Description
Unshare a session.

### Method
DELETE

### Endpoint
/session/:id/share

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to unshare.

### Request Example
No request body.

### Response
#### Success Response (200)
- **Session** - The updated Session object.

#### Response Example
{
  "id": "session1",
  "title": "Unshared Session",
  // ... other session properties
}

```

--------------------------------

### Session Forking API

Source: https://opencode.ai/docs/de/server

Endpoint to fork an existing session at a specific message.

```APIDOC
## POST /session/:id/fork

### Description
Fork an existing session starting from a specific message.

### Method
POST

### Endpoint
/session/:id/fork

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to fork.
#### Request Body
- **messageID** (string) - Optional - The ID of the message to fork from. If not provided, forks from the latest message.

### Request Example
```json
{
  "messageID": "msg_pqr"
}
```

### Response
#### Success Response (200)
- **session** (Session) - The newly created forked session object.

#### Response Example
```json
{
  "id": "session_forked_101",
  "title": "Forked Session",
  "createdAt": "2023-10-27T10:15:00Z"
}
```
```

--------------------------------

### Set Default Model in OpenCode Config

Source: https://opencode.ai/docs/models

This JSON configuration snippet demonstrates how to set a default language model for OpenCode. It specifies the model ID, which includes the provider and model name, for consistent use.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "lmstudio/google/gemma-3n-e4b"
}
```

--------------------------------

### Customize Agent UI Color

Source: https://opencode.ai/docs/agents

Customize the agent's visual appearance in the UI using the 'color' option. Accepts valid hex color codes or theme colors like 'primary', 'secondary', 'accent', etc.

```json
{
  "agent": {
    "creative": {
      "color": "#ff6b6b"
    },
    "code-reviewer": {
      "color": "accent"
    }
  }
}
```

--------------------------------

### Session Abort API

Source: https://opencode.ai/docs/de/server

Endpoint to abort a currently running session.

```APIDOC
## POST /session/:id/abort

### Description
Abort a session that is currently in progress.

### Method
POST

### Endpoint
/session/:id/abort

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session to abort.

### Request Example
None

### Response
#### Success Response (200)
- **success** (boolean) - Indicates if the session was aborted successfully.

#### Response Example
```json
true
```
```

--------------------------------

### Disabling All Formatters Globally

Source: https://opencode.ai/docs/formatters

To disable all code formatters across the entire project, set the 'formatter' property to 'false' in the OpenCode configuration file.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "formatter": false
}
```

--------------------------------

### Force Subagent Invocation with Subtask in opencode.json

Source: https://opencode.ai/docs/commands

The `subtask` boolean option in `opencode.json` forces a command to trigger a subagent invocation, even if the agent's mode is set to `primary`. This is useful for isolating command execution within a separate context, preventing pollution of the primary context. This is an optional configuration.

```json
{
  "command": {
    "analyze": {
      "subtask": true
    }
  }
}
```

--------------------------------

### Override Built-in Tool with Custom Tool

Source: https://opencode.ai/docs/custom-tools

This TypeScript snippet shows how to override a built-in tool, in this case, 'bash'. By naming the custom tool file '.opencode/tools/bash.ts', it takes precedence over the default 'bash' tool. The custom tool provides a restricted wrapper.

```typescript
import { tool } from "@opencode-ai/plugin"

export default tool({
  description: "Restricted bash wrapper",
  args: {
    command: tool.schema.string(),
  },
  async execute(args) {
    return `blocked: ${args.command}`
  },
})
```

--------------------------------

### Disable Skill Tool for Custom Agent

Source: https://opencode.ai/docs/skills

Shows how to completely disable the skill tool for a custom agent by setting `tools.skill` to `false` in the agent's frontmatter.

```yaml
---
tools:
  skill: false
---

```

--------------------------------

### Session Status API

Source: https://opencode.ai/docs/de/server

Endpoint to retrieve the current status for all sessions.

```APIDOC
## GET /session/status

### Description
Get the status for all sessions.

### Method
GET

### Endpoint
/session/status

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **statusMap** (object) - An object where keys are session IDs and values are SessionStatus objects.

#### Response Example
```json
{
  "session_123": "active",
  "session_456": "inactive"
}
```
```

--------------------------------

### OpenCode Plugin: Escape Bash Commands

Source: https://opencode.ai/docs/plugins

This TypeScript plugin demonstrates how to hook into the 'tool.execute.before' event to modify command arguments. It uses the 'shescape' library to escape characters in bash commands before they are executed, preventing potential security issues or command injection.

```typescript
import { escape } from "shescape"

export const MyPlugin = async (ctx) => {
  return {
    "tool.execute.before": async (input, output) => {
      if (input.tool === "bash") {
        output.args.command = escape(output.args.command)
      }
    },
  }
}
```

--------------------------------

### Disable an Agent with JSON

Source: https://opencode.ai/docs/agents

Sets the `disable` option to `true` in `opencode.json` to deactivate a specific agent. This is useful for temporarily or permanently excluding an agent from operation.

```json
{
  "agent": {
    "review": {
      "disable": true
    }
  }
}
```

--------------------------------

### Session Diff API

Source: https://opencode.ai/docs/de/server

Endpoint to retrieve the difference (diff) for a session, optionally at a specific message.

```APIDOC
## GET /session/:id/diff

### Description
Get the file differences for a session.

### Method
GET

### Endpoint
/session/:id/diff

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the session.
#### Query Parameters
- **messageID** (string) - Optional - The ID of the message to generate the diff up to.

### Request Example
None

### Response
#### Success Response (200)
- **diffs** (FileDiff[]) - An array of file difference objects.

#### Response Example
```json
[
  {
    "fileName": "README.md",
    "changes": [
      {
        "type": "added",
        "content": "New line added."
      }
    ]
  }
]
```
```

--------------------------------

### Configure Disabled Sharing in OpenCode

Source: https://opencode.ai/docs/share

Disables the sharing feature entirely in OpenCode by setting the 'share' option to 'disabled' in the configuration file. This ensures no conversations can be shared publicly.

```json
{
  "$schema": "https://opncd.ai/config.json",
  "share": "disabled"
}
```

--------------------------------

### Prevent .env File Reading

Source: https://opencode.ai/docs/plugins

This plugin prevents OpenCode AI from reading sensitive .env files. It intercepts tool execution and throws an error if a 'read' tool is attempted on a file path containing '.env'. This enhances security by protecting environment variables.

```javascript
export const EnvProtection = async ({ project, client, $, directory, worktree }) => {
  return {
    "tool.execute.before": async (input, output) => {
      if (input.tool === "read" && output.args.filePath.includes(".env")) {
        throw new Error("Do not read .env files")
      }
    },
  }
}
```

--------------------------------

### Disable MCPs Globally with Glob Pattern (JSON)

Source: https://opencode.ai/docs/mcp-servers

This JSON configuration demonstrates how to disable all MCPs matching a glob pattern, such as 'my-mcp*', globally. This is useful for managing multiple MCPs efficiently.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-mcp-foo": {
      "type": "local",
      "command": ["bun", "x", "my-mcp-command-foo"]
    },
    "my-mcp-bar": {
      "type": "local",
      "command": ["bun", "x", "my-mcp-command-bar"]
    }
  },
  "tools": {
    "my-mcp*": false
  }
}
```

--------------------------------

### Logout MCP Server Credentials

Source: https://opencode.ai/docs/cli

Removes OAuth credentials for a specified MCP server. This command is useful for managing authentication tokens and ensuring secure access to MCP services.

```bash
opencode mcp logout [name]
```

--------------------------------

### OpenCode Unshare Command

Source: https://opencode.ai/docs/share

Stops sharing the current OpenCode conversation and removes its public accessibility. This action deletes the associated share link and conversation data.

```shell
/unshare
```

--------------------------------

### Hide Subagent from Autocomplete in opencode.json

Source: https://opencode.ai/docs/agents

Hide a subagent from the '@' autocomplete menu by setting `hidden: true` in the opencode.json configuration. This is useful for internal subagents invoked programmatically. This setting only affects user visibility and does not prevent programmatic invocation if permissions allow.

```json
{
  "agent": {
    "internal-helper": {
      "mode": "subagent",
      "hidden": true
    }
  }
}
```

--------------------------------

### Disable Claude Code Compatibility in Bash

Source: https://opencode.ai/docs/rules

These bash commands allow you to disable Claude Code compatibility features in OpenCode. You can disable all Claude support, or specifically disable prompts or skills.

```bash
export OPENCODE_DISABLE_CLAUDE_CODE=1        # Disable all .claude support
```

```bash
export OPENCODE_DISABLE_CLAUDE_CODE_PROMPT=1 # Disable only ~/.claude/CLAUDE.md
```

```bash
export OPENCODE_DISABLE_CLAUDE_CODE_SKILLS=1 # Disable only .claude/skills
```

--------------------------------

### Disable Automatic OAuth for MCP Server

Source: https://opencode.ai/docs/mcp-servers

This configuration disables automatic OAuth detection for a remote MCP server, allowing for alternative authentication methods like API keys. Set 'oauth' to 'false' and provide necessary headers, such as 'Authorization'.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "mcp": {
    "my-api-key-server": {
      "type": "remote",
      "url": "https://mcp.example.com/mcp",
      "oauth": false,
      "headers": {
        "Authorization": "Bearer {env:MY_API_KEY}"
      }
    }
  }
}
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.