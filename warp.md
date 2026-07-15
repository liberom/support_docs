### Example setup commands

Source: https://docs.warp.dev/agent-platform/cloud-agents/environments

Best practice examples for environment setup commands that ensure repeatability and stability.

```shell
# Safer patterns (repeatable and stable)
mkdir -p .cache
npm ci
```

--------------------------------

### Initialize Project Environment

Source: https://docs.warp.dev/agent-platform/cloud-agents/environments

A basic setup sequence for creating a cache directory and installing dependencies. It is recommended to ensure these commands are idempotent to prevent failures on subsequent runs.

```shell
mkdir -p .cache
npm install
```

--------------------------------

### Create environment with guided setup

Source: https://docs.warp.dev/agent-platform/cloud-agents/environments

Uses the /create-environment command to automatically inspect repositories and suggest configuration. It supports local paths, owner/repo formats, and GitHub URLs as inputs.

```shellscript
# Local file paths
/create-environment ./warp-internal ./warp-server

# owner/repo
/create-environment warpdotdev/warp-internal warpdotdev/warp-server

# GitHub URLs
/create-environment 
https://github.com/warpdotdev/warp-internal.git
```

--------------------------------

### POST /api/v1/agent/run

Source: https://docs.warp.dev/reference/api-and-sdk/quickstart

Submits a prompt to start a new asynchronous agent run within a specified environment.

```APIDOC
## POST /api/v1/agent/run

### Description
Starts a new agent run by submitting a prompt and an environment configuration.

### Method
POST

### Endpoint
https://app.warp.dev/api/v1/agent/run

### Parameters
#### Request Body
- **prompt** (string) - Required - The task description for the agent.
- **config** (object) - Required - Configuration object containing the environment_id.

### Request Example
{
  "prompt": "Scan the repo for outdated dependencies and summarize the findings.",
  "config": {
    "environment_id": "<ENV_ID>"
  }
}

### Response
#### Success Response (200)
- **run_id** (string) - The unique identifier for the created agent run.

#### Response Example
{
  "run_id": "run_abc123"
}
```

--------------------------------

### Database Indexing and Subquery Optimization

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-create-priority-matrix-for-database-optimization

Examples of creating indexes for performance and refactoring inefficient subqueries using Window Functions.

```sql
-- Missing Index Analysis
CREATE INDEX idx_orders_status_created ON orders(status, created_at);

-- Subquery Optimization using Window Function
WITH product_stats AS (
  SELECT *,
         AVG(price) OVER (PARTITION BY category_id) AS avg_category_price
  FROM products
)
SELECT * FROM product_stats WHERE price > avg_category_price;
```

--------------------------------

### Install Warp on Linux

Source: https://docs.warp.dev/enterprise/getting-started/getting-started-developers

Commands to install Warp on Debian/Ubuntu and Fedora/RHEL systems, or using an install script. Ensure you have the necessary permissions to install packages.

```bash
# Debian/Ubuntu
sudo dpkg -i warp-terminal_*.deb

# Fedora/RHEL
sudo rpm -i warp-terminal-*.rpm

# Or use the install script
curl -fsSL https://warp.dev/install.sh | bash
```

--------------------------------

### Install Oz Agent Worker using Go

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Installs the Oz agent worker using the Go toolchain. After installation, the worker can be started with an API key and a worker ID. Ensure the WARP_API_KEY environment variable is set.

```bash
go install github.com/warpdotdev/oz-agent-worker@latest
oz-agent-worker --api-key "$WARP_API_KEY" --worker-id "my-worker"
```

--------------------------------

### POST /environment

Source: https://docs.warp.dev/reference/cli/integration-setup

Creates a new environment with a specified Docker image, repositories, and setup commands.

```APIDOC
## POST /environment

### Description
Creates a new environment configuration for your project using the Oz CLI.

### Method
POST

### Endpoint
oz environment create

### Parameters
#### Query Parameters
- **--name** (string) - Required - Human-readable label for the environment.
- **--docker-image** (string) - Optional - Docker image name from Docker Hub.
- **--repo** (string) - Optional - Repository path (owner/repo). Can be repeated.
- **--setup-command** (string) - Optional - Commands to run during setup. Can be repeated.
- **--description** (string) - Optional - Brief description of the environment.

### Request Example
```sh
oz environment create \
  --name "web-dev" \
  --docker-image "node:20-bullseye" \
  --repo "org/frontend" \
  --setup-command "npm install"
```

### Response
#### Success Response (200)
- **ID** (string) - The unique identifier for the created environment.
```

--------------------------------

### GET /api/v1/agent/runs

Source: https://docs.warp.dev/reference/api-and-sdk/quickstart

Lists all recent agent runs associated with the authenticated account.

```APIDOC
## GET /api/v1/agent/runs

### Description
Retrieves a list of recent agent runs.

### Method
GET

### Endpoint
https://app.warp.dev/api/v1/agent/runs

### Response
#### Success Response (200)
- **runs** (array) - A list of run objects containing status and metadata.

#### Response Example
{
  "runs": [
    { "run_id": "run_1", "state": "SUCCEEDED" },
    { "run_id": "run_2", "state": "INPROGRESS" }
  ]
}
```

--------------------------------

### POST /integration/slack

Source: https://docs.warp.dev/reference/cli/integration-setup

Connects an existing environment to a Slack integration.

```APIDOC
## POST /integration/slack

### Description
Creates a Slack integration for a specific environment ID.

### Method
POST

### Endpoint
oz integration create slack

### Parameters
#### Query Parameters
- **--environment** (string) - Required - The unique ID of the environment to link.

### Request Example
```bash
oz integration create slack --environment <ENV_ID>
```

### Response
#### Success Response (200)
- **status** (string) - Confirmation of integration creation.
```

--------------------------------

### Create Bitbucket environment with setup commands

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/bitbucket

Creates a new Warp environment configured to clone a Bitbucket repository upon initialization. It uses a setup command with an API token injected at runtime to ensure secure authentication.

```bash
oz environment create \
  --name "my-bitbucket-cloud-env" \
  --docker-image <image> \
  --setup-command 'git clone https://x-bitbucket-api-token-auth:$BITBUCKET_API_TOKEN@bitbucket.org/your-workspace/your-repo.git' \
  --setup-command 'cd your-repo && <install dependencies>'
```

--------------------------------

### GET /api/v1/agent/runs/<RUN_ID>

Source: https://docs.warp.dev/reference/api-and-sdk/quickstart

Retrieves the current status and details of a specific agent run.

```APIDOC
## GET /api/v1/agent/runs/<RUN_ID>

### Description
Fetches the current state of a specific agent run using its unique ID.

### Method
GET

### Endpoint
https://app.warp.dev/api/v1/agent/runs/<RUN_ID>

### Parameters
#### Path Parameters
- **RUN_ID** (string) - Required - The unique ID of the agent run.

### Response
#### Success Response (200)
- **state** (string) - The current status (QUEUED, INPROGRESS, SUCCEEDED, FAILED).
- **status_message** (string) - Optional - Error details if the run failed.
- **session_link** (string) - Optional - URL to the full run transcript.

#### Response Example
{
  "state": "SUCCEEDED",
  "session_link": "https://oz.warp.dev/runs/run_abc123"
}
```

--------------------------------

### Example JSON Response for environment_setup_failed

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/environment-setup-failed

This JSON object illustrates the structure of the error response when environment setup fails. It includes the error type, a specific title describing the failure, the HTTP status, the instance of the error, and a retryable flag.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/environment-setup-failed",
  "title": "Failed to clone repository: branch 'main' not found in acme/backend",
  "status": 500,
  "instance": "/api/v1/agent/tasks",
  "error": "Failed to clone repository: branch 'main' not found in acme/backend",
  "retryable": false
}
```

--------------------------------

### Install Oz CLI on Linux and Windows

Source: https://docs.warp.dev/reference/cli/cli

Commands to install the Oz CLI package on Linux systems using apt or the Warp application on Windows using WinGet.

```bash
sudo apt install oz-preview
```

```powershell
winget install Warp.Warp
```

--------------------------------

### Install Warp on Windows using WinGet

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Installs Warp on Windows using the WinGet package manager. This command requires WinGet to be installed and configured on your system. After installation, Warp can be found in the Start menu.

```powershell
winget install Warp.Warp
```

--------------------------------

### Verify Docker Installation

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Command to verify that the Docker daemon is correctly installed and running on the host machine, which is a prerequisite for the default Docker-based worker backend.

```bash
docker info
```

--------------------------------

### Direct Backend Command-Line Example (Bash)

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting/managed-worker-reference

Example of launching the Warp agent worker with the 'direct' backend using command-line arguments. This includes setting the API key, worker ID, and specifying the backend.

```bash
oz-agent-worker --api-key "$WARP_API_KEY" --worker-id "my-worker" --backend direct
```

--------------------------------

### Create Slack integration via Oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/quickstart

Commands to initialize a Slack integration for a specific Oz environment. Supports optional default prompts to customize agent behavior for all triggered runs.

```bash
oz integration create slack --environment <ENV_ID>
```

```bash
oz integration create slack \
  --environment <ENV_ID> \
  --prompt "Always open a draft PR and request review from the team-leads group."
```

--------------------------------

### Manage Cloud Agent Runs (Shell)

Source: https://docs.warp.dev/reference/cli/cli

Provides examples for listing recent cloud agent runs with an optional limit and retrieving details for a specific run using its ID.

```shell
# List recent runs (default: 10)
oz run list
oz run list --limit 20

# Get details for a specific run
oz run get <RUN_ID>
```

--------------------------------

### Download and Prepare Warp AppImage

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Downloads the single-file AppImage executable for Warp and grants it execution permissions. Separate commands are provided for x64 and ARM64 architectures.

```bash
# On x64 systems
curl -L "https://app.warp.dev/download?package=appimage" -o Warp-x64.AppImage
chmod +x Warp-x64.AppImage
```

```bash
# On ARM64 systems
curl -L "https://app.warp.dev/download?package=appimage_arm64" -o Warp-ARM64.AppImage
chmod +x Warp-ARM64.AppImage
```

--------------------------------

### Manually Configure Warp Apt Repository on Debian/Ubuntu

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Manually configures the Warp apt repository and installs Warp on Debian or Ubuntu-based systems. This involves downloading a GPG key, setting up the repository file, and updating the package list. Requires sudo privileges and the `wget` and `gpg` packages.

```bash
sudo apt-get install wget gpg
wget -qO- https://releases.warp.dev/linux/keys/warp.asc | gpg --dearmor > warpdotdev.gpg
sudo install -D -o root -g root -m 644 warpdotdev.gpg /etc/apt/keyrings/warpdotdev.gpg
sudo sh -c 'echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/warpdotdev.gpg] https://releases.warp.dev/linux/deb stable main" > /etc/apt/sources.list.d/warpdotdev.list'
rm warpdotdev.gpg
sudo apt update && sudo apt install warp-terminal
```

--------------------------------

### Create a Warp development environment via CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations

Initializes a new remote development environment by scanning local repositories or remote URLs. This command triggers a guided flow to configure Docker images, dependencies, and setup commands.

```shell
/create-environment
/create-environment ./frontend ./backend
/create-environment your-org/repo-name
/create-environment https://github.com/your-org/api.git
```

--------------------------------

### Install Warp on Debian/Ubuntu (Deb Package)

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Installs Warp on Debian or Ubuntu-based Linux distributions by downloading and installing a .deb package. This method also sets up the Warp apt repository for automatic updates. Requires sudo privileges.

```bash
sudo apt install ./<file>.deb
```

--------------------------------

### Create a cloud environment using Oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/slack

Initializes a new cloud environment by specifying a Docker image, required GitHub repositories, and optional setup commands. This environment serves as the containerized runtime for the agent.

```bash
oz environment create \
  --name <name> \
  --docker-image <image> \
  --repo <owner/repo> \
  --setup-command "<command>"
```

--------------------------------

### Create Warp environment via CLI

Source: https://docs.warp.dev/reference/cli/integration-setup

Commands to initialize a Warp environment using the /create-environment slash command. This command analyzes local repositories, GitHub URLs, or owner/repo paths to configure Docker images and setup scripts for agents.

```bash
# File paths
/create-environment ./warp-internal ./warp-server

# owner/repo
/create-environment warpdotdev/warp-internal warpdotdev/warp-server

# GitHub URLs
/create-environment https://github.com/warpdotdev/warp-internal.git
```

--------------------------------

### Manually Configure Warp Yum Repository

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Manually imports the GPG signing key and adds the Warp repository to the system's zypp configuration. This is an alternative to the direct RPM installation method.

```bash
sudo rpm --import https://releases.warp.dev/linux/keys/warp.asc
sudo sh -c 'echo -e "[warpdotdev]\nname=warpdotdev\ntype=rpm-md\nbaseurl=https://releases.warp.dev/linux/rpm/stable\nenabled=1\nautorefresh=1\ngpgcheck=1\ngpgkey=https://releases.warp.dev/linux/keys/warp.asc\nkeeppackages=0" > /etc/zypp/repos.d/warpdotdev.repo'
sudo zypper install warp-terminal
```

--------------------------------

### Create Slack Integration with CLI

Source: https://docs.warp.dev/reference/cli/integration-setup

Sets up a Slack integration for a specified Warp environment using the CLI. This requires a pre-existing environment ID.

```bash
oz integration create slack --environment <ENV_ID>
```

--------------------------------

### Install Warp via RPM Package

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Installs the Warp terminal using the zypper package manager on OpenSUSE or SLE systems. This method automatically configures the necessary repository for future updates.

```bash
sudo zypper install ./<file>.rpm
```

--------------------------------

### Create an Agent Run

Source: https://docs.warp.dev/reference/api-and-sdk/quickstart

Submits a prompt to the Oz API to initiate an agent task within a specific cloud environment. The request returns a run ID used for tracking the asynchronous process.

```bash
curl -X POST https://app.warp.dev/api/v1/agent/run \
  -H "Authorization: Bearer $WARP_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "Scan the repo for outdated dependencies and summarize the findings.",
    "config": {
      "environment_id": "<ENV_ID>"
    }
  }'
```

--------------------------------

### Install Warp on Arch Linux (Pacman Package)

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Installs Warp on Arch Linux-based distributions by downloading and installing a .pkg.tar.zst package. Requires sudo privileges.

```bash
sudo pacman -U ./<file>.pkg.tar.zst
```

--------------------------------

### List Recent Agent Runs

Source: https://docs.warp.dev/reference/api-and-sdk/quickstart

Fetches a collection of recent agent runs associated with the authenticated account. Useful for auditing or managing multiple tasks.

```bash
curl "https://app.warp.dev/api/v1/agent/runs" \
  -H "Authorization: Bearer $WARP_API_KEY"
```

--------------------------------

### Install Warp on RHEL/Fedora/CentOS (RPM Package)

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Installs Warp on RHEL, Fedora, or CentOS-based Linux distributions by downloading and installing an .rpm package. This method also sets up the Warp yum repository. Requires sudo privileges.

```bash
sudo dnf install ./<file>.rpm
```

--------------------------------

### MCP Server JSON Configuration Example

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

An example of a valid MCP JSON object that can be used inline or in a file to configure MCP servers for agent connections. It shows configurations for GitHub and Sentry.

```json
{
  "github": {
    "url": "https://api.githubcopilot.com/mcp/"
  },
  "sentry": {
    "command": "npx",
    "args": ["-y", "mcp-remote@latest", "https://mcp.sentry.dev/mcp"]
  }
}
```

--------------------------------

### Example Windows Launch Configuration YAML

Source: https://docs.warp.dev/terminal/sessions/launch-configurations

A sample YAML configuration demonstrating how to define multiple windows, each containing tabs with specific titles, working directories (cwd), and colors. The 'cwd' must be an absolute path.

```yaml
# Warp Launch Configuration
#
# This configuration has two windows, 
# each with one tab in different starting directories.

---
name: Example Windows
windows:
  - tabs:
      - title: Documents
        layout:
          cwd: /Users/warp-user/Documents
        color: blue
  - tabs:
      - title: Warp User
        layout:
          cwd: /Users/warp-user
        color: green

```

--------------------------------

### Manually Configure Warp Yum Repository on RHEL/Fedora/CentOS

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Manually configures the Warp yum repository and installs Warp on RHEL, Fedora, or CentOS-based systems. This involves importing the GPG key and creating a repository configuration file. Requires sudo privileges.

```bash
sudo rpm --import https://releases.warp.dev/linux/keys/warp.asc
sudo sh -c 'echo -e "[warpdotdev]\nname=warpdotdev\nbaseurl=https://releases.warp.dev/linux/rpm/stable\nenabled=1\ngpgcheck=1\ngpgkey=https://releases.warp.dev/linux/keys/warp.asc" > /etc/yum.repos.d/warpdotdev.repo'
sudo dnf install warp-terminal
```

--------------------------------

### Database Connection Configuration

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-create-priority-matrix-for-database-optimization

Recommended configuration settings for database connection pools to manage concurrency and timeouts.

```json
{
  "connectionLimit": 50,
  "queueLimit": 100,
  "acquireTimeout": 30000,
  "waitForConnections": true,
  "idleTimeout": 300000,
  "enableKeepAlive": true,
  "keepAliveInitialDelay": 10
}
```

--------------------------------

### Manually Configure Warp Pacman Repository on Arch Linux

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Manually configures the Warp pacman repository and installs Warp on Arch Linux-based systems. This involves adding the repository to pacman.conf and importing the signing key. Requires sudo privileges.

```bash
sudo sh -c "echo -e '\n[warpdotdev]\nServer = https://releases.warp.dev/linux/pacman/$repo/$arch' >> /etc/pacman.conf"
sudo pacman-key -r "linux-maintainers@warp.dev"
sudo pacman-key --lsign-key "linux-maintainers@warp.dev"
sudo pacman -Sy warp-terminal
```

--------------------------------

### Authenticate with Warp API

Source: https://docs.warp.dev/reference/api-and-sdk/quickstart

Sets the required environment variable for API authentication. This variable is used by subsequent CLI commands to authorize requests.

```bash
export WARP_API_KEY="wk-..."
```

--------------------------------

### Manage and update environments

Source: https://docs.warp.dev/agent-platform/cloud-agents/environments

Commands for listing, retrieving, updating, and deleting environments via the Oz CLI. Updates allow for adding or removing repositories and setup commands dynamically.

```shell
# List environments
oz environment list

# View an environment’s configuration
oz environment get <ENV_ID>

# Update an environment
oz environment update <ENV_ID> --repo owner/repo
oz environment update <ENV_ID> --remove-repo owner/repo
oz environment update <ENV_ID> --setup-command "your command"
oz environment update <ENV_ID> --remove-setup-command "exact command"
oz environment update <ENV_ID> --name "new name"
oz environment update <ENV_ID> --description "Updated description"
oz environment update <ENV_ID> --docker-image node:22

# Delete an environment
oz environment delete <ENV_ID>
```

--------------------------------

### Direct Backend Configuration Example (YAML)

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting/managed-worker-reference

Example of configuring the 'direct' backend in a YAML configuration file for the Warp agent worker. This specifies the worker ID and the root directory for workspaces.

```yaml
worker_id: "my-worker"
backend:
  direct:
    workspace_root: "/var/lib/oz/workspaces"
```

--------------------------------

### Configure Workflow YAML Schema

Source: https://docs.warp.dev/terminal/entry/yaml-workflows

Examples of YAML configuration properties for Warp workflows, including tags and argument definitions.

```yaml
tags: ["git", "GitHub"]
```

```yaml
name: Example Workflow
command: echo {{string}}
arguments:
  - name: string
    description: The value to echo
```

--------------------------------

### Build Oz Agent Worker from Source

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Builds the Oz agent worker from its source code. This involves cloning the repository, navigating into the directory, compiling the binary, and then running the worker with necessary credentials. Requires Git and Go to be installed.

```bash
git clone https://github.com/warpdotdev/oz-agent-worker.git
cd oz-agent-worker
go build -o oz-agent-worker
./oz-agent-worker --api-key "$WARP_API_KEY" --worker-id "my-worker"
```

--------------------------------

### Example Tabs Launch Configuration YAML

Source: https://docs.warp.dev/terminal/sessions/launch-configurations

A sample YAML configuration illustrating the structure for defining tabs within a Launch Configuration. It shows how to set custom tab titles, colors (using ANSI terminal colors), and their corresponding Warp theme-derived appearance.

```yaml
# Warp Launch Configuration
#

```

--------------------------------

### Download Warp AppImage for x64 Systems

Source: https://docs.warp.dev/getting-started/quickstart/installation-and-setup

Downloads the Warp AppImage for x64 architecture using curl and makes it executable with chmod. This is the primary method for installing Warp on compatible Linux systems.

```bash
# On x64 systems
curl -L "https://app.warp.dev/download?package=appimage" -o Warp-x64.AppImage
chmod +x Warp-x64.AppImage
```

--------------------------------

### Install Warp on macOS using Homebrew

Source: https://docs.warp.dev/getting-started/readme-1/installation-and-setup

Installs Warp on macOS using the Homebrew package manager. Ensure Homebrew is installed before running this command. After installation, Warp can be found in the Applications folder.

```bash
brew install --cask warp
```

--------------------------------

### Accessing CLI Help and Version Information

Source: https://docs.warp.dev/reference/cli/troubleshooting

Commands to retrieve built-in documentation for specific CLI operations and verify the current installation version.

```bash
oz help
oz help agent run
oz help mcp
oz --version
```

--------------------------------

### Install System Packages on Ubuntu for Warp

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

These commands install essential system packages on Ubuntu that are often required for Warp to function correctly, especially in environments like WSL or VMs. This includes Xorg, Wayland, fonts, utilities, and graphics drivers.

```bash
sudo apt install xserver-xorg
sudo apt install wayland
sudo apt install fonts-hack
sudo apt install wslu
sudo apt install mesa-utils
sudo apt install mesa-vulkan-drivers
sudo apt install xdg-desktop-portal xdg-desktop-portal-gtk zenity
sudo apt install wl-clipboard
```

--------------------------------

### Install NVIDIA Drivers on Various Linux Distributions

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

This section provides commands to install or update NVIDIA GPU drivers on different Linux distributions like Ubuntu, Fedora, Arch Linux, and openSUSE. Proper driver installation is crucial for Warp's graphical rendering.

```bash
# For Ubuntu:
sudo ubuntu-drivers install
# For Fedora:
sudo dnf install akmod-nvidia
# For Arch Linux:
sudo pacman -S nvidia
# For openSUSE:
sudo zypper install x11-video-nvidiaG05
```

--------------------------------

### DELETE /environment

Source: https://docs.warp.dev/reference/cli/integration-setup

Deletes an existing environment by its ID.

```APIDOC
## DELETE /environment

### Description
Removes an environment from the system.

### Method
DELETE

### Endpoint
oz environment delete <ID>

### Parameters
#### Path Parameters
- **ID** (string) - Required - The unique identifier of the environment.

#### Query Parameters
- **--force** (boolean) - Optional - Skip confirmation checks for environments used by integrations.

### Request Example
```bash
oz environment delete <ID> --force
```
```

--------------------------------

### Database Execution Plan Analysis

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-create-priority-matrix-for-database-optimization

SQL commands to generate detailed execution plans for PostgreSQL and MySQL to identify performance bottlenecks.

```sql
-- PostgreSQL
EXPLAIN (ANALYZE, BUFFERS, FORMAT JSON);

-- MySQL
EXPLAIN FORMAT=JSON;
```

--------------------------------

### GET /runs

Source: https://docs.warp.dev/reference/api-and-sdk/models

Retrieves a paginated list of agent runs, sorted by updated_at in descending order.

```APIDOC
## GET /runs

### Description
Retrieves a paginated list of agent runs. Use the page_info.next_cursor field to fetch subsequent pages. Results are sorted by updated_at descending by default.

### Method
GET

### Endpoint
/runs

### Parameters
#### Query Parameters
- **cursor** (string) - Optional - The pagination cursor for the next page of results.
- **limit** (integer) - Optional - The number of items to return per page.

### Request Example
GET /runs?limit=10

### Response
#### Success Response (200)
- **runs** (array) - A list of RunItem objects.
- **page_info** (object) - Pagination metadata including next_cursor.

#### Response Example
{
  "runs": [
    {
      "run_id": "run_123",
      "title": "Data Analysis Task",
      "state": "SUCCEEDED",
      "created_at": "2023-10-27T10:00:00Z",
      "updated_at": "2023-10-27T10:05:00Z"
    }
  ],
  "page_info": {
    "next_cursor": "abc_789"
  }
}
```

--------------------------------

### CloudEnvironmentConfig Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for configuring cloud environments, including Docker images, repository cloning, and setup commands.

```APIDOC
## CloudEnvironmentConfig Object

### Description
Configuration for a cloud environment used by scheduled agents, defining the runtime environment and initialization steps.

### Properties
- **name** (string) - Human-readable name for the environment
- **description** (string) - Optional description of the environment
- **docker_image** (string) - Docker image to use (e.g., "ubuntu:latest")
- **github_repos** (array) - List of GitHub repositories to clone
- **setup_commands** (array) - Shell commands to run during setup

### Request Example
{
  "name": "dev-env",
  "docker_image": "ubuntu:latest",
  "github_repos": [{"owner": "org", "repo": "project"}],
  "setup_commands": ["npm install"]
}
```

--------------------------------

### Test Astro API Endpoints

Source: https://docs.warp.dev/university/developer-workflows/beginner/how-to-create-project-rules-for-an-existing-project-astro-%2B-typescript-%2B-tailwind

Example curl commands to verify the functionality of API routes, including retrieving brewfiles and package rankings.

```bash
# Test brewfile retrieval
curl "http://localhost:4321/api/getBrewfiles.json"

# Test specific brewfile by ID
curl "http://localhost:4321/api/getBrewfiles.json?id=DOCUMENT_ID"

# Test package rankings
curl "http://localhost:4321/api/getRankedPackages.json"
```

--------------------------------

### Managing Environments and Integrations

Source: https://docs.warp.dev/reference/cli/troubleshooting

Commands to list, inspect, update, and delete environments and integrations. These are used to verify configurations, manage linked repositories, and handle setup commands.

```bash
oz integration list
oz environment get <ENV_ID>
oz environment update <ENV_ID> --repo owner/repo
oz environment update <ENV_ID> --remove-repo owner/repo
oz environment update <ENV_ID> --setup-command "your command"
oz environment update <ENV_ID> --remove-setup-command "exact command"
oz environment delete <ID> --force
```

--------------------------------

### List Available Models (Shell)

Source: https://docs.warp.dev/reference/cli/cli

Demonstrates the command to list all available models that can be used with the agent.

```shell
oz model list
```

--------------------------------

### Create environment with Oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/environments

Manually defines an environment using the Oz CLI with specific Docker images, repositories, and setup commands. This is ideal for automated workflows or custom configurations.

```shell
oz environment create \
  --name <name> \
  --docker-image <image> \
  --repo <owner/repo> \
  --repo <owner/repo> \
  --setup-command "<command1>" \
  --setup-command "<command2>" \
  --description "Optional description"
```

--------------------------------

### Run Specific Skill Workflows

Source: https://docs.warp.dev/reference/cli/skills

Examples of executing specific deployment and code review workflows using cloud agents. These commands illustrate how to target specific repositories and skill files within an organizational structure.

```bash
# Run a deploy skill from a specific repo
oz agent run-cloud \
  --environment SVhg783GBFQHk1OfdPfFU9 \
  --skill "myorg/backend:.warp/skills/deploy/SKILL.md" \
  --prompt "deploy to staging"

# Run a code review skill
oz agent run-cloud \
  --environment SVhg783GBFQHk1OfdPfFU9 \
  --skill "myorg/backend:code-review" \
  --prompt "review the latest PR"
```

--------------------------------

### Example Secret Environment Variable

Source: https://docs.warp.dev/agent-platform/cloud-agents/secrets

Illustrates how a secret is exposed as an environment variable within a cloud agent's execution environment. The secret name is used as the environment variable name.

```bash
METABASE_API_KEY=********
```

--------------------------------

### Caching Layer Implementation

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-create-priority-matrix-for-database-optimization

A JavaScript utility function to implement Redis-based caching for database queries to reduce load.

```javascript
const getCachedOrQuery = async (key, query, ttl = 3600) => {
  const cached = await redis.get(key);
  if (cached) return JSON.parse(cached);

  const result = await db.query(query);
  await redis.setex(key, ttl, JSON.stringify(result));
  return result;
};
```

--------------------------------

### Check Agent Run Status

Source: https://docs.warp.dev/reference/api-and-sdk/quickstart

Retrieves the current state of an agent run using its unique ID. Returns status values such as QUEUED, INPROGRESS, SUCCEEDED, or FAILED.

```bash
curl "https://app.warp.dev/api/v1/agent/runs/<RUN_ID>" \
  -H "Authorization: Bearer $WARP_API_KEY"
```

--------------------------------

### List Environment Base Images (Shell)

Source: https://docs.warp.dev/reference/cli/cli

Shows the command to list suggested base images for creating cloud environments.

```shell
oz environment image list
```

--------------------------------

### GET /agent

Source: https://docs.warp.dev/agent-platform/cloud-agents/skills-as-agents

Retrieves a list of available skills and agent configurations accessible to the authenticated user.

```APIDOC
## GET /agent

### Description
Lists all available skills and agent configurations discovered from the user's environments and repositories.

### Method
GET

### Endpoint
/agent

### Parameters
None

### Response
#### Success Response (200)
- **skills** (array) - List of available skill objects
- **environments** (array) - List of configured environments

#### Response Example
{
  "skills": [
    { "name": "code-cleanup", "repo": "owner/repo" }
  ]
}
```

--------------------------------

### Example MCP Server Configuration (JSON)

Source: https://docs.warp.dev/agent-platform/cloud-agents/mcp

Demonstrates a JSON configuration for defining MCP servers, including HTTP and Stdio transports. This configuration specifies the URL for a GitHub MCP server and the command, arguments, and environment variables for a dbt MCP server.

```json
{
  "github": {
    "url": "https://mcp.example.com/github"
  },
  "dbt": {
    "command": "uvx",
    "args": ["dbt-mcp"],
    "env": {
      "DBT_HOST": "https://example.us1.dbt.com",
      "DBT_SERVICE_TOKEN": "${DBT_SERVICE_TOKEN}"
    }
  }
}
```

--------------------------------

### Configure GitHub SSE MCP Server

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This JSON configuration defines a GitHub SSE (Server-Sent Events) based MCP server using a provided URL. This setup is for remote or locally hosted MCP endpoints.

```json
{
  "GitHub": {
    "url": "https://api.githubcopilot.com/mcp/"
  }
}
```

--------------------------------

### Structured PR Review Prompt for Warp AI

Source: https://docs.warp.dev/university/developer-workflows/power-user/how-to-review-prs-like-a-senior-dev

This prompt guides Warp's AI to analyze a pull request and format the output for quick review by maintainers. It includes sections for risk assessment, critical issues, concerns, and a decision guide, along with formatting rules for clarity and efficiency. The output aims to provide actionable insights and speed up the review process.

```markdown
## Prompt: Structured PR Review Format

> Review this pull request and format your response for rapid scanning by a busy maintainer. Follow the structure below.

---

### 1. 🚨 Risk Assessment

**Overall Risk:** 🔴 HIGH | 🟠 MEDIUM | 🟢 LOW  
**Complexity:** [Simple | Moderate | Complex | Very Complex]  
**Blast Radius:** [Isolated | Module-wide | System-wide | External APIs affected]  
**Requires Immediate Review:** [YES / NO – why]

---

### 2. 🔍 Critical Issues  
_If none, write “None found” and skip to the next section._

#### 1. [CRITICAL ISSUE TITLE]  
**File:** `path/to/file.js:L125`  
**Impact:** Data loss / Security hole / System crash  
**Fix:**  
// Quick code fix example here

---

### 3. ⚠️ Concerns  
_Should discuss or fix before merge. If none, write “None found.”_  

**Examples:**  
- [PERFORMANCE] Unindexed query on large table  
- [SECURITY] Missing input sanitization in login form  

---

### 4. 🎯 Maintainer Decision Guide  

**Merge confidence:** [0–100]%
- □ Safe to merge after fixing blockers  
- □ Needs architecture discussion first  
- □ Requires performance testing  
- □ Get security team review  
- □ Author should split into smaller PRs  

**Time to properly review:** ~[X] minutes  
**Recommended reviewer expertise:** [Backend | Security | Database | Frontend]  

---

### 5. 🧭 Formatting Rules  

- Use emoji headers for instant visual recognition  
- Keep sections short; if empty, say “None found”  
- Blockers get full detail, everything else stays concise  
- Include code examples only for blockers  
- Bold key impact/risk words  
- Use consistent prefixes like [SECURITY], [PERFORMANCE], [LOGIC] for easy scanning  
- If PR is genuinely fine, end with: ✅ “This PR is safe to merge as-is.”

```

--------------------------------

### Configure Worker with YAML File

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting/managed-worker-reference

Shows how to execute the worker binary using a YAML configuration file for complex setups, where CLI flags take precedence over file values.

```bash
oz-agent-worker --api-key "$WARP_API_KEY" --config-file config.yaml
```

--------------------------------

### Configure Notion CLI Server using npx

Source: https://docs.warp.dev/knowledge-and-collaboration/mcp

This configuration sets up the Notion CLI server using npx. It installs and runs mcp-remote, pointing it to the Notion MCP endpoint.

```json
{
  "Notion": {
    "command": "npx",
    "args": ["-y", "mcp-remote", "https://mcp.notion.com/mcp"]
  }
}
```

--------------------------------

### Astro Project Development Commands

Source: https://docs.warp.dev/university/developer-workflows/beginner/how-to-create-project-rules-for-an-existing-project-astro-%2B-typescript-%2B-tailwind

Standard CLI commands for managing an Astro-based project, including dependency installation, development server execution, and production builds.

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Run Astro CLI commands
npm run astro
```

--------------------------------

### Run oz-agent-worker via Docker

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting/managed-worker-reference

Example command to launch the worker container with various configuration flags, including volume mounts, environment variable passing, and concurrency limits.

```bash
docker run -v /var/run/docker.sock:/var/run/docker.sock \
  -e WARP_API_KEY="$WARP_API_KEY" \
  warpdotdev/oz-agent-worker \
  --worker-id "prod-runner-1" \
  --log-level debug \
  --no-cleanup \
  --max-concurrent-tasks 4 \
  --idle-on-complete 10m \
  -v /opt/shared-cache:/cache:ro \
  -e NPM_TOKEN=your_token \
  -e GITHUB_TOKEN
```

--------------------------------

### GET /agent/schedules

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Retrieve a list of all scheduled agents accessible to the authenticated user, sorted alphabetically by name.

```APIDOC
## GET /agent/schedules

### Description
Retrieve all scheduled agents accessible to the authenticated user. Results are sorted alphabetically by name.

### Method
GET

### Endpoint
/agent/schedules

### Parameters
None

### Request Example
GET /agent/schedules

### Response
#### Success Response (200)
- **agents** (array) - A list of scheduled agent objects.

#### Response Example
{
  "agents": [
    {
      "name": "daily-cleanup",
      "description": "Runs daily cleanup tasks",
      "last_ran": "2023-10-27T10:00:00Z",
      "next_run": "2023-10-28T10:00:00Z"
    }
  ]
}
```

--------------------------------

### Generate Docker Infrastructure with Warp AI

Source: https://docs.warp.dev/university/developer-workflows/devops/how-to-create-a-production-ready-docker-setup

A prompt designed for Warp AI to analyze a project directory and automatically generate a multi-stage Dockerfile, docker-compose.yml, and .dockerignore file. The prompt ensures the output is optimized for security, image size, and environment-specific configurations.

```text
Analyze my entire project directory structure, package files, and configuration to generate a complete production-ready Docker setup. I need:

A multi-stage Dockerfile optimized for my specific language/framework with proper layer caching, security best practices, and minimal image size
A docker-compose.yml for both development and production environments with all necessary services, networks, volumes, and environment variable handling
A comprehensive .dockerignore file that excludes unnecessary files but keeps what's needed for the build
Startup scripts and health check configurations
Documentation explaining each Docker command and why specific choices were made

Please detect my project type automatically and configure everything accordingly. Include comments explaining the optimization decisions.
```

--------------------------------

### Slow Query Logging Configuration

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-create-priority-matrix-for-database-optimization

Configures database engines to log queries that exceed a specific execution time threshold. This is essential for identifying bottlenecks in production environments.

```postgresql
ALTER SYSTEM SET log_min_duration_statement = '1000';  -- Log queries over 1s
ALTER SYSTEM SET log_statement = 'all';
ALTER SYSTEM SET log_duration = on;
```

```mysql
SET GLOBAL slow_query_log = 'ON';
SET GLOBAL long_query_time = 1;
SET GLOBAL log_output = 'TABLE';
```

--------------------------------

### GET /agent/artifacts/{artifactUid}

Source: https://docs.warp.dev/reference/api-and-sdk/models

Retrieves a signed download URL for a specific artifact, such as a screenshot, using its unique identifier.

```APIDOC
## GET /agent/artifacts/{artifactUid}

### Description
Retrieves a signed download URL for a specific artifact, primarily used for retrieving screenshot data associated with a screenshot artifact.

### Method
GET

### Endpoint
/agent/artifacts/{artifactUid}

### Parameters
#### Path Parameters
- **artifactUid** (string) - Required - The unique identifier of the artifact to retrieve.

### Response
#### Success Response (200)
- **url** (string) - The signed URL to download the artifact content.

#### Response Example
{
  "url": "https://storage.example.com/artifacts/123?token=xyz"
}
```

--------------------------------

### Initialize Workflow Directory

Source: https://docs.warp.dev/terminal/entry/yaml-workflows

Commands to create the necessary directory structure for storing custom workflows on different operating systems.

```bash
mkdir -p $HOME/.warp/workflows/
```

```powershell
New-Item -Path "$env:APPDATA\warp\Warp\data\workflows\" -ItemType Directory
```

```bash
mkdir -p ${XDG_DATA_HOME:-$HOME/.local/share}/warp-terminal/workflows/
```

--------------------------------

### GET /agent/runs

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieve a list of agent runs with optional filtering by name.

```APIDOC
## GET /agent/runs

### Description
Retrieves a list of agent runs. Use the `name` query parameter to filter runs by their human-readable label.

### Method
GET

### Endpoint
/agent/runs

### Parameters
#### Query Parameters
- **name** (string) - Optional - Filter runs by the human-readable label assigned during creation.

### Response
#### Success Response (200)
- **runs** (array) - List of agent run objects.

#### Response Example
{
  "runs": [
    {
      "run_id": "run_123",
      "name": "nightly-dependency-check"
    }
  ]
}
```

--------------------------------

### GET /agent/schedules/{scheduleId}

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Retrieve detailed information about a specific scheduled agent, including its configuration, history, and next scheduled run time.

```APIDOC
## GET /agent/schedules/{scheduleId}

### Description
Retrieve detailed information about a specific scheduled agent, including its configuration, history, and next scheduled run time.

### Method
GET

### Endpoint
/agent/schedules/{scheduleId}

### Parameters
#### Path Parameters
- **scheduleId** (string) - Required - The unique identifier of the scheduled agent

### Request Example
GET /agent/schedules/sched_12345

### Response
#### Success Response (200)
- **ScheduledAgentItem** (object) - The detailed object containing configuration and history metadata.

#### Response Example
{
  "name": "daily-backup-agent",
  "docker_image": "ubuntu:latest",
  "last_ran": "2023-10-27T10:00:00Z",
  "next_run": "2023-10-28T10:00:00Z"
}
```

--------------------------------

### Configure Atlassian CLI Server using npx

Source: https://docs.warp.dev/knowledge-and-collaboration/mcp

This configuration sets up the Atlassian CLI server using npx. It installs and runs mcp-remote, pointing it to the Atlassian MCP SSE endpoint.

```json
{
  "Atlassian": {
    "command": "npx",
    "args": ["-y", "mcp-remote", "https://mcp.atlassian.com/v1/sse"]
  }
}
```

--------------------------------

### GET /api/v1/schedules/{id}

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Retrieve detailed information about a specific scheduled agent, including its configuration, history, and next scheduled run time.

```APIDOC
## GET /api/v1/schedules/{id}

### Description
Retrieve detailed information about a specific scheduled agent, including its configuration, history, and next scheduled run time.

### Method
GET

### Endpoint
https://app.warp.dev/api/v1/schedules/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - Unique identifier for the scheduled agent

### Request Example
GET /api/v1/schedules/agent-123-abc

### Response
#### Success Response (200)
- **id** (string) - Unique identifier for the scheduled agent
- **name** (string) - Human-readable name for the schedule
- **cron_schedule** (string) - Cron expression defining when the agent runs
- **enabled** (boolean) - Whether the schedule is currently active
- **prompt** (string) - The prompt/instruction for the agent to execute
- **created_at** (string) - Timestamp when the schedule was created
- **updated_at** (string) - Timestamp when the schedule was last updated

#### Response Example
{
  "id": "agent-123-abc",
  "name": "Daily Cleanup",
  "cron_schedule": "0 9 * * *",
  "enabled": true,
  "prompt": "Perform daily cleanup tasks",
  "created_at": "2023-10-01T10:00:00Z",
  "updated_at": "2023-10-01T10:00:00Z"
}
```

--------------------------------

### Retrieve Secrets via HashiCorp Vault CLI

Source: https://docs.warp.dev/knowledge-and-collaboration/warp-drive/environment-variables

A command-line example for fetching a specific secret field from HashiCorp Vault. This command is stored by Warp and executed at runtime to inject the secret into the terminal environment.

```bash
vault kv get -field=password secret/staging/app/server/creds
```

--------------------------------

### Run Managed Worker via Docker

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Starts the oz-agent-worker daemon using Docker. It mounts the host's Docker socket to allow the worker to spawn isolated task containers.

```bash
docker run -v /var/run/docker.sock:/var/run/docker.sock \
  -e WARP_API_KEY="$WARP_API_KEY" \
  warpdotdev/oz-agent-worker --worker-id "my-worker"
```

--------------------------------

### Query Performance Testing with Jest

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-create-priority-matrix-for-database-optimization

A unit test pattern to verify that database queries execute within acceptable latency thresholds. It measures the execution time of a query and asserts it against a maximum duration.

```javascript
describe('Query Performance', () => {
  test('User listing should complete under 100ms', async () => {
    const start = Date.now();
    await db.query('SELECT * FROM users LIMIT 1000');
    expect(Date.now() - start).toBeLessThan(100);
  });
});
```

--------------------------------

### GET /agent/runs

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieve a paginated list of agent runs with optional filtering. Results default to `sort_by=updated_at` and `sort_order=desc`.

```APIDOC
## GET /agent/runs

### Description
Retrieve a paginated list of agent runs with optional filtering. Results default to `sort_by=updated_at` and `sort_order=desc`.

### Method
GET

### Endpoint
/agent/runs

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - Maximum number of runs to return (min: 1, max: 500, default: 20)
- **cursor** (string) - Optional - Pagination cursor from previous response
- **sort_by** (string) - Optional - Sort field for results. Enum: `updated_at` (default), `created_at`, `title`, `agent`
- **sort_order** (string) - Optional - Sort direction. Enum: `asc`, `desc` (default: `desc`)
- **state** (array of RunState) - Optional - Filter by run state. Can be specified multiple times to match any of the given states.
- **name** (string) - Optional - Filter by agent config name
- **model_id** (string) - Optional - Filter by model ID
- **creator** (string) - Optional - Filter by creator UID (user or service account)
- **source** (RunSourceType) - Optional - Filter by run source type
- **created_after** (string) - Optional - Filter runs created after this timestamp (RFC3339 format)
- **created_before** (string) - Optional - Filter runs created before this timestamp (RFC3339 format)
- **updated_after** (string) - Optional - Filter runs updated after this timestamp (RFC3339 format)

### Request Example
```
GET /agent/runs?limit=10&sort_by=created_at&state=completed&state=failed
```

### Response
#### Success Response (200)
- **runs** (array) - List of agent runs.
- **page_info** (PageInfo) - Pagination metadata.

#### Response Example
```json
{
  "runs": [
    {
      "id": "run-123",
      "title": "My Agent Run",
      "state": "completed",
      "created_at": "2023-10-27T10:00:00Z",
      "updated_at": "2023-10-27T10:05:00Z",
      "creator": "user-abc",
      "model_id": "model-xyz",
      "source": "api"
    }
  ],
  "page_info": {
    "has_next_page": true,
    "next_cursor": "cursor-456"
  }
}
```
```

--------------------------------

### GET /api/v1/runs

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieve a paginated list of agent runs with optional filtering capabilities. Results are sorted by updated_at in descending order by default.

```APIDOC
## GET /api/v1/runs

### Description
Retrieve a paginated list of agent runs. Use the returned `page_info.next_cursor` to fetch subsequent pages of results.

### Method
GET

### Endpoint
https://app.warp.dev/api/v1/runs

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - Number of runs to return per page.
- **cursor** (string) - Optional - Cursor for pagination.
- **sort_by** (string) - Optional - Field to sort by (default: updated_at).
- **sort_order** (string) - Optional - Sort direction (asc or desc, default: desc).

### Request Example
GET /api/v1/runs?limit=10&sort_order=desc

### Response
#### Success Response (200)
- **runs** (array) - List of agent run objects.
- **page_info** (object) - Pagination metadata including `next_cursor`.

#### Response Example
{
  "runs": [
    {
      "run_id": "run_123",
      "title": "Example Agent Run",
      "state": "SUCCEEDED",
      "created_at": "2023-10-27T10:00:00Z"
    }
  ],
  "page_info": {
    "next_cursor": "abc-123-def"
  }
}
```

--------------------------------

### Initialize and Open Project Rules in Warp

Source: https://docs.warp.dev/university/developer-workflows/beginner/how-to-create-project-rules-for-an-existing-project-astro-%2B-typescript-%2B-tailwind

Commands to generate a starter Warp.md file in the project root and open it in the side editor for configuration.

```shell
/init
/open-project-rules
```

--------------------------------

### Cursor-Based Pagination in SQL

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-create-priority-matrix-for-database-optimization

Implements efficient pagination using a cursor-based approach. This method is more performant than OFFSET-based pagination for large datasets as it leverages indexed columns for filtering.

```sql
SELECT * FROM posts
WHERE created_at < $cursor
ORDER BY created_at DESC
LIMIT 20;
```

--------------------------------

### Get Artifact Details

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieve an artifact by its UUID. For screenshot artifacts, this endpoint returns a time-limited signed download URL.

```APIDOC
## GET /agent/artifacts/{artifactUid}

### Description
Retrieve an artifact by its UUID. For screenshot artifacts, returns a time-limited signed download URL.

### Method
GET

### Endpoint
/agent/artifacts/{artifactUid}

### Parameters
#### Path Parameters
- **artifactUid** (string) - Required - The unique identifier (UUID) of the artifact

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **artifact_uid** (string) - Unique identifier (UUID) for the artifact
- **artifact_type** (string) - Type of the artifact (e.g., SCREENSHOT)
- **created_at** (string) - Timestamp when the artifact was created (RFC3339)
- **data** (object) - Data specific to the artifact type. For screenshot artifacts, this includes a download URL.
  - **download_url** (string) - Time-limited signed URL to download the screenshot
  - **expires_at** (string) - Timestamp when the download URL expires (RFC3339)
  - **content_type** (string) - MIME type of the screenshot (e.g., image/png)
  - **description** (string) - Optional description of the screenshot

#### Response Example
```json
{
  "artifact_uid": "a1b2c3d4-e5f6-7890-1234-567890abcdef",
  "artifact_type": "SCREENSHOT",
  "created_at": "2023-10-27T10:00:00Z",
  "data": {
    "download_url": "https://example.com/download/screenshot.png?token=...",
    "expires_at": "2023-10-27T11:00:00Z",
    "content_type": "image/png",
    "description": "Screenshot of the login page"
  }
}
```

#### Error Responses
- **400 Bad Request**: Missing artifact UID.
- **401 Unauthorized**: Authentication required.
- **403 Forbidden**: No permission to access artifact.
- **404 Not Found**: Artifact not found or unsupported artifact type.
```

--------------------------------

### GET /agent

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieve a list of available agents (skills) that can be used to run tasks, with options for filtering and sorting.

```APIDOC
## GET /agent

### Description
Retrieve a list of available agents (skills) that can be used to run tasks. Agents are discovered from environments or a specific repository.

### Method
GET

### Endpoint
/agent

### Parameters
#### Query Parameters
- **repo** (string) - Optional - Optional repository specification to list agents from (format: "owner/repo").
- **refresh** (boolean) - Optional - When true, clears the agent list cache before fetching.
- **sort_by** (string) - Optional - Sort order: "name" (default) or "last_run".
- **include_malformed_skills** (boolean) - Optional - When true, includes skills with malformed SKILL.md files.

### Request Example
GET /agent?repo=owner/repo&sort_by=name

### Response
#### Success Response (200)
- **agents** (array) - List of available agents.

#### Response Example
{
  "agents": [
    {
      "name": "example-agent",
      "description": "An example agent"
    }
  ]
}
```

--------------------------------

### GET /agent/runs/{runId}

Source: https://docs.warp.dev/reference/api-and-sdk/models

Retrieves the status and details of a specific agent run using the unique run identifier.

```APIDOC
## GET /agent/runs/{runId}

### Description
Poll this endpoint using the run_id received from an agent creation request to retrieve the current status and state of the run.

### Method
GET

### Endpoint
/agent/runs/{runId}

### Parameters
#### Path Parameters
- **runId** (string) - Required - The unique identifier for the agent run.

### Response
#### Success Response (200)
- **run_id** (string) - Unique identifier for the created run
- **task_id** (string) - Deprecated identifier for the task
- **state** (RunState) - Current state of the run (QUEUED, PENDING, CLAIMED, INPROGRESS, SUCCEEDED, FAILED, BLOCKED, ERROR, CANCELLED)
- **at_capacity** (boolean) - Whether the system was at capacity when the run was created

#### Response Example
{
  "run_id": "run_12345",
  "task_id": "run_12345",
  "state": "INPROGRESS",
  "at_capacity": false
}
```

--------------------------------

### GET /api/v1/runs/{run_id}

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieve detailed information about a specific agent run, including the full prompt, session link, and resolved configuration.

```APIDOC
## GET /api/v1/runs/{run_id}

### Description
Retrieve detailed information about a specific agent run. This includes the run's lifecycle state, original prompt, timestamps, session links, and resolved agent configuration.

### Method
GET

### Endpoint
https://app.warp.dev/api/v1/runs/{run_id}

### Parameters
#### Path Parameters
- **run_id** (string) - Required - The unique identifier for the agent run.

### Request Example
GET /api/v1/runs/run_12345

### Response
#### Success Response (200)
- **run_id** (string) - Unique identifier for the run
- **title** (string) - Human-readable title for the run
- **state** (string) - Current state (QUEUED, PENDING, CLAIMED, INPROGRESS, SUCCEEDED, FAILED, BLOCKED, ERROR, CANCELLED)
- **prompt** (string) - The prompt/instruction for the agent
- **created_at** (string) - Timestamp when the run was created
- **session_link** (string) - URL to view the agent session

#### Response Example
{
  "run_id": "run_12345",
  "title": "Example Run",
  "state": "SUCCEEDED",
  "prompt": "Write a function to add two numbers",
  "created_at": "2023-10-27T10:00:00Z",
  "session_link": "https://app.warp.dev/sessions/12345"
}
```

--------------------------------

### N+1 Query Optimization

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-create-priority-matrix-for-database-optimization

Refactoring code to replace sequential queries inside a loop with a single batched JOIN query to improve performance.

```javascript
// Current Implementation
const users = await db.query('SELECT * FROM users');
for (const user of users) {
  user.posts = await db.query('SELECT * FROM posts WHERE user_id = ?', [user.id]);
}

// Optimized Version
const usersWithPosts = await db.query(`
  SELECT u.*,
         COALESCE(json_agg(p.*) FILTER (WHERE p.id IS NOT NULL), '[]') AS posts
  FROM users u
  LEFT JOIN posts p ON p.user_id = u.id
  GROUP BY u.id;
`);
```

--------------------------------

### GET /agent/runs/{runId}

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieve detailed information about a specific agent run, including the full prompt, session link, and resolved configuration.

```APIDOC
## GET /agent/runs/{runId}

### Description
Retrieve detailed information about a specific agent run, including the full prompt, session link, and resolved configuration.

### Method
GET

### Endpoint
/agent/runs/{runId}

### Parameters
#### Path Parameters
- **runId** (string) - Required - The unique identifier of the run

### Response
#### Success Response (200)
- **RunItem** (object) - Detailed information about the agent run.

#### Error Responses
- **400** - Missing run ID
- **401** - Authentication required
- **403** - No permission to access run
- **404** - Run not found

### Response Example
{
  "run_id": "run_12345",
  "prompt": "Execute command...",
  "session_link": "https://warp.dev/sessions/123",
  "status": "completed"
}
```

--------------------------------

### Schedule Recurring Agent Tasks with Oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/quickstart

Automate routine maintenance tasks by scheduling agents to run on a cron schedule. This example sets up a weekly dependency check that runs every Monday at 10 AM and opens a pull request for updates. Requires an environment ID.

```bash
oz schedule create \
  --name "weekly-dependency-check" \
  --cron "0 10 * * 1" \
  --environment <ENV_ID> \
  --prompt "check for dependency updates and open PR"
```

--------------------------------

### Create Linear Integration via CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/linear

This command initializes a Linear integration for a specific Warp environment. It requires an environment ID and triggers a browser-based authentication flow to authorize the Oz app within the Linear workspace.

```bash
oz integration create linear --environment <ENV_ID>
```

--------------------------------

### Case-Insensitive Regex Example

Source: https://docs.warp.dev/support-and-community/privacy-and-security/secret-redaction

Demonstrates how to make a regular expression case-insensitive by prepending `(?i)`. This ensures that the pattern matches variations in capitalization, such as 'password', 'Password', and 'PASSWORD'.

```regex
(?i)password
```

--------------------------------

### Share Agent Session with Users and Teams (Shell)

Source: https://docs.warp.dev/reference/cli/cli

Demonstrates how to use the `--share` flag in the `oz agent run` command to share an agent's session with specific users or teams, with options for view-only or edit access.

```shell
# Share the agent's session with yourself:
oz agent run --share --prompt "fix the compiler error"

# Give specific users view-only access to a session:
oz agent run --share firstuser@example.com --share otheruser@example.com --prompt "fix the compiler error"

# Let any user on your team edit the session:
oz agent run --share team:edit --prompt "fix the compiler error"
```

--------------------------------

### Run Warp on Windows for All Users

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

This command sets the WGPU_BACKEND environment variable to 'vulkan,gl' and then executes the Warp terminal application installed for all users on Windows. It's used to ensure Warp utilizes specific graphics backends.

```powershell
$env:WGPU_BACKEND="vulkan,gl"; & "$env:PROGRAMFILES\Warp\warp.exe"
```

--------------------------------

### Run Warp Preview with verbose logging on Windows

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

Sets environment variables for WGPU logging and executes the Warp Preview binary. This is useful for capturing detailed diagnostic information during startup.

```powershell
$env:RUST_LOG="wgpu_core=info,wgpu_hal=info"; & "$env:PROGRAMFILES\WarpPreview\preview.exe"
```

--------------------------------

### Batch Insert Optimization in SQL

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-create-priority-matrix-for-database-optimization

Optimizes database insertion performance by grouping multiple records into a single INSERT statement. This reduces the overhead of individual network round-trips and transaction commits.

```sql
INSERT INTO users (name, email, created_at) VALUES
  ($1, $2, $3),
  ($4, $5, $6),
  ... -- batch in groups of 1000
```

--------------------------------

### Starship Timeout Configuration

Source: https://docs.warp.dev/terminal/appearance/prompt

Example of setting the `command_timeout` variable in Starship's configuration to resolve timeout errors. Refer to Starship documentation for detailed options.

```toml
# Example: Set command_timeout to 5 seconds
[options]
command_timeout = 5

```

--------------------------------

### GET /websites/warp_dev/runs

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieves a list of runs for the warp_dev project. Supports filtering by environment ID, skill, schedule ID, artifact type, and a fuzzy search query.

```APIDOC
## GET /websites/warp_dev/runs

### Description
Retrieves a list of runs for the warp_dev project. Supports filtering by environment ID, skill, schedule ID, artifact type, and a fuzzy search query.

### Method
GET

### Endpoint
/websites/warp_dev/runs

### Parameters
#### Query Parameters
- **environment_id** (string) - Optional - Filter runs by environment ID
- **skill** (string) - Optional - Filter runs by skill spec (e.g., "owner/repo:path/to/SKILL.md"). Alias for skill_spec.
- **skill_spec** (string) - Optional - Filter runs by skill spec (e.g., "owner/repo:path/to/SKILL.md")
- **schedule_id** (string) - Optional - Filter runs by the scheduled agent ID that created them
- **artifact_type** (string) - Optional - Filter runs by artifact type (PLAN or PULL_REQUEST). Enum: ["PLAN", "PULL_REQUEST", "SCREENSHOT"]
- **q** (string) - Optional - Fuzzy search query across run title, prompt, and skill_spec

### Response
#### Success Response (200)
- **runs** (array) - List of runs

#### Error Response (400)
- **code** (string) - Error code
- **message** (string) - Error message

#### Error Response (401)
- **code** (string) - Error code
- **message** (string) - Error message
```

--------------------------------

### Start Postgres REPL in Warp

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-write-sql-commands-inside-a-postgres-repl

This command initiates an interactive PostgreSQL REPL session within the Warp terminal. It requires specifying the username and database name. The output is a psql prompt ready for SQL commands.

```bash
psql -U postgres -d my_database
```

--------------------------------

### Handle external_authentication_required JSON responses

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/external-authentication-required

Example JSON error responses for the external_authentication_required error. These payloads include metadata such as the provider, auth_url, and inaccessible_repos to help clients resolve authorization issues.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/external-authentication-required",
  "title": "User is not connected to GitHub",
  "status": 401,
  "instance": "/api/v1/agent/tasks",
  "error": "User is not connected to GitHub. Authorize access here: https://...",
  "retryable": false,
  "provider": "github",
  "auth_url": "https://github.com/login/oauth/authorize?..."
}
```

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/external-authentication-required",
  "title": "User does not have access to the following repositories in the environment: acme/backend",
  "status": 401,
  "detail": "inaccessible repos: acme/backend",
  "instance": "/api/v1/agent/tasks",
  "error": "User does not have access to the following repositories in the environment: acme/backend (inaccessible repos: acme/backend)",
  "retryable": false,
  "provider": "github",
  "auth_url": "https://github.com/apps/warp-dev/installations/new",
  "inaccessible_repos": ["acme/backend"]
}
```

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/external-authentication-required",
  "title": "Unable to locate your Warp account",
  "status": 401,
  "instance": "/api/v1/agent/tasks",
  "error": "Unable to locate your Warp account",
  "retryable": false,
  "provider": "slack"
}
```

--------------------------------

### POST /agent/run

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Spawns a cloud agent with a prompt and optional configuration. The agent is queued for execution and assigned a unique run ID. Use the run_id to poll GET /agent/runs/{runId} for status updates.

```APIDOC
## POST /agent/run

### Description
Spawn a cloud agent with a prompt and optional configuration. The agent will be queued for execution and assigned a unique run ID.

### Method
POST

### Endpoint
/agent/run

### Parameters
#### Request Body
- **prompt** (string) - Required - The prompt to send to the agent.
- **model** (string) - Optional - The model to use for the agent run. Defaults to the environment's default model.
- **max_tokens** (integer) - Optional - The maximum number of tokens to generate. Defaults to the model's default.
- **temperature** (number) - Optional - The sampling temperature for the model. Defaults to the model's default.
- **stream** (boolean) - Optional - Whether to stream the response. Defaults to false.
- **attachments** (array) - Optional - A list of base64-encoded file attachments to include with the prompt.
  - **file_name** (string) - Required - Name of the attached file.
  - **mime_type** (string) - Required - MIME type of the attachment. Supported image types: image/jpeg, image/png, image/gif, image/webp.
  - **data** (string) - Required - Base64-encoded attachment data.

### Request Example
```json
{
  "prompt": "Summarize the following document.",
  "model": "gpt-4o",
  "max_tokens": 1000,
  "temperature": 0.7,
  "stream": true,
  "attachments": [
    {
      "file_name": "document.pdf",
      "mime_type": "application/pdf",
      "data": "JVBERi0xLjQKJcO..."
    }
  ]
}
```

### Response
#### Success Response (200)
- **run_id** (string) - Unique identifier for the created run.
- **task_id** (string) - Unique identifier for the task (same as run_id). Deprecated - use run_id instead.
- **state** (string) - Current state of the run. Possible values: QUEUED, PENDING, CLAIMED, INPROGRESS, SUCCEEDED, FAILED, BLOCKED, ERROR, CANCELLED.
- **at_capacity** (boolean) - Whether the system is at capacity when the run was created.

#### Response Example
```json
{
  "run_id": "run-12345abcde",
  "task_id": "run-12345abcde",
  "state": "QUEUED",
  "at_capacity": false
}
```

#### Error Response (400, 401, 403)
- **type** (string) - A URI reference that identifies the problem type.
- **title** (string) - A short, human-readable summary of the problem type.
- **status** (integer) - The HTTP status code for this occurrence of the problem.
- **detail** (string) - A human-readable explanation specific to this occurrence of the problem.
- **instance** (string) - The request path that generated this error.
- **error** (string) - Human-readable error message combining title and detail.
- **retryable** (boolean) - Whether the request can be retried.
- **trace_id** (string) - OpenTelemetry trace ID for debugging and support requests.

#### Error Response Example
```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/invalid_prompt",
  "title": "Invalid Request",
  "status": 400,
  "detail": "The prompt cannot be empty.",
  "instance": "/agent/run",
  "error": "Invalid prompt: The prompt cannot be empty.",
  "retryable": false,
  "trace_id": "abcdef1234567890"
}
```
```

--------------------------------

### Referencing Warp Drive Objects as Context in Prompts

Source: https://docs.warp.dev/reference/cli/warp-drive

This example shows how to include Warp Drive objects (workflows, notebooks, rules) as context for an agent by referencing them within the prompt string using a specific ID format. This enhances the agent's understanding and execution by providing relevant background information.

```bash
$ oz agent run --prompt "Follow the instructions in <notebook:gq1CMAUWLtaL1CpEoTDQ3y>"
```

--------------------------------

### Create a Slack integration using Oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/slack

Registers a Slack integration for a specific environment. Supports optional custom system prompts to standardize agent behavior across all interactions.

```bash
oz integration create slack --environment <ENV_ID>

oz integration create slack \
  --environment <ENV_ID> \
  --prompt "Always prefix PR titles with '[WARP]' and include detailed test steps."
```

--------------------------------

### Set Warp Environment Variables for Linux

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

These examples show how to set environment variables to control Warp's behavior on Linux, such as enabling Wayland or specifying the default GPU adapter for WSL. These can be temporarily set or exported for persistence.

```bash
# Default to Wayland:
WARP_ENABLE_WAYLAND=1
# Set Default GPU for WSL:
MESA_D3D12_DEFAULT_ADAPTER_NAME=NVIDIA
# Set Graphics APIs:
WGPU_BACKEND=gl
```

--------------------------------

### Execute Cloud Agents with Skills

Source: https://docs.warp.dev/reference/cli/skills

Demonstrates how to run cloud agents using the --skill flag with fully qualified paths or repository-based identifiers. These commands require an environment ID and a prompt to provide context for the skill execution.

```bash
# Fully qualified (recommended)
oz agent run-cloud -e <ENV_ID> --skill "owner/repo:skill-name" --prompt "deploy to staging"

# With full path
oz agent run-cloud -e <ENV_ID> --skill "warpdotdev/warp-server:.warp/skills/deploy/SKILL.md" --prompt "deploy to staging"
```

--------------------------------

### Uninstall Warp and Remove Data on macOS

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/logging-out-and-uninstalling

Commands to remove Warp Stable and Preview installations, including application defaults, logs, and local application support directories.

```bash
# Remove Warp settings defaults
defaults delete dev.warp.Warp-Stable
# Remove Warp logs
sudo rm -r $HOME/Library/Logs/warp.log
# Remove Warp database, codebase context, and mcp logs
sudo rm -r "$HOME/Library/Group Containers/2BBY89MBSN.dev.warp/Library/Application Support/dev.warp.Warp-Stable"
# Remove Warp user files, themes, and launch configurations
sudo rm -r $HOME/.warp
```

```bash
# Remove Warp Preview settings defaults
defaults delete dev.warp.Warp-Preview
# Remove Warp Preview logs
sudo rm -r $HOME/Library/Logs/warp_preview.log
# Remove Warp Preview database, codebase context, and mcp logs
sudo rm -r "$HOME/Library/Group Containers/2BBY89MBSN.dev.warp/Library/Application Support/dev.warp.Warp-Preview"
```

--------------------------------

### List Available Skills (Shell)

Source: https://docs.warp.dev/reference/cli/cli

Shows how to list all discovered agent skills using the `oz agent list` command. It also includes an option to filter skills by a specific repository.

```shell
oz agent list
oz agent list --repo owner/repo
```

--------------------------------

### Create First-Party Integration CLI Command

Source: https://docs.warp.dev/agent-platform/cloud-agents/platform

This command is used to create a first-party integration with Warp. It registers webhooks with a third-party system to receive events, extract context, and create tasks. The specific arguments for '...' will depend on the integration being set up.

```bash
oz integration create ...
```

--------------------------------

### Get Slack SSE Server URL

Source: https://docs.warp.dev/knowledge-and-collaboration/mcp

This JSON object provides the URL for the Slack Server-Sent Events (SSE) endpoint. Replace 'your-mcp-host.com' with your actual MCP host.

```json
{
  "Slack": {
    "url": "https://your-mcp-host.com/api/mcp/slack/sse"
  }
}
```

--------------------------------

### GET /agent/sessions/{sessionUuid}/redirect

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Checks if a shared session should be redirected to a conversation transcript. Returns a conversation ID if available, or an empty object if no redirect is required.

```APIDOC
## GET /agent/sessions/{sessionUuid}/redirect

### Description
Check whether a shared session should redirect to a conversation transcript. Returns a conversation_id if the agent sandbox has finished and conversation data is available, or an empty object if no redirect is needed.

### Method
GET

### Endpoint
/agent/sessions/{sessionUuid}/redirect

### Parameters
#### Path Parameters
- **sessionUuid** (string) - Required - The UUID of the shared session

### Request Example
GET /agent/sessions/123e4567-e89b-12d3-a456-426614174000/redirect

### Response
#### Success Response (200)
- **conversation_id** (string) - Optional - The conversation ID to redirect to (only present when redirect is needed)

#### Response Example
{
  "conversation_id": "conv_987654321"
}
```

--------------------------------

### Example JSON Response for integration_not_configured Error

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/integration-not-configured

This JSON object illustrates the structure of the response when the integration_not_configured error occurs. It includes standard error fields along with integration-specific metadata like 'integration_name' and 'setup_url'.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/integration-not-configured",
  "title": "Slack integration is not configured",
  "status": 400,
  "instance": "/api/v1/agent/tasks",
  "error": "Slack integration is not configured",
  "retryable": false,
  "integration_name": "slack",
  "setup_url": "https://oz.warp.dev/integrations"
}
```

--------------------------------

### Configure Chroma Package Search CLI MCP Server

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This JSON configuration sets up a Chroma Package Search CLI-based MCP server using npx. It requires a Chroma API key for authentication and specifies the endpoint URL.

```json
{
    "package-search": {
      "command": "npx",
      "args": ["mcp-remote", "https://mcp.trychroma.com/package-search/v1", "--header", "x-chroma-token: ${X_CHROMA_TOKEN}"],
      "env": {
        "X_CHROMA_TOKEN": "<YOUR_CHROMA_API_KEY>"
      }
    }
}
```

--------------------------------

### Configure GitHub CLI MCP Server

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This JSON configuration sets up a GitHub CLI-based MCP server using Docker. It requires a GitHub Personal Access Token for authentication.

```json
{
  "GitHub": {
    "command": "docker",
    "args": ["run","-i","--rm","-e","GITHUB_PERSONAL_ACCESS_TOKEN","ghcr.io/github/github-mcp-server"],
    "env": {
      "GITHUB_PERSONAL_ACCESS_TOKEN": "<your_github_token>"
    }
  }
}
```

--------------------------------

### Configure Multiple MCP Servers with JSON

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

Add multiple MCP servers by providing a JSON configuration snippet. Each server is defined with a unique key and can be configured with commands, arguments, or external URLs and headers. This allows for flexible integration of various services.

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/files"]
    },
    "notes": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-notes", "--notes-dir", "/Users/you/Documents/notes"]
    },
    "externalDocs": {
      "url": "http://localhost:4000/mcp/stream",
      "headers": {
            "my-header": "my-header-value"
      }
    }
  }
}
```

--------------------------------

### Get Notion SSE Server URL

Source: https://docs.warp.dev/knowledge-and-collaboration/mcp

This JSON object provides the URL for the Notion Server-Sent Events (SSE) endpoint. This URL is used for real-time data streaming from Notion.

```json
{
  "Notion": {
    "url": "https://mcp.notion.com/sse"
  }
}
```

--------------------------------

### Connecting to Remote Docker Daemon (Bash)

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting/managed-worker-reference

Example of configuring environment variables in Bash to connect the Warp agent worker to a remote Docker daemon using TLS. This involves setting DOCKER_HOST, DOCKER_TLS_VERIFY, and DOCKER_CERT_PATH.

```bash
export DOCKER_HOST="tcp://remote-host:2376"
export DOCKER_TLS_VERIFY=1
export DOCKER_CERT_PATH="/path/to/certs"
oz-agent-worker --api-key "$WARP_API_KEY" --worker-id "my-worker"
```

--------------------------------

### HTML Embed for Shared Blocks

Source: https://docs.warp.dev/terminal/blocks/block-sharing

This snippet shows an example of an HTML iframe used to embed a shared block on a web page. It includes attributes for the source URL, title, styling, and permissions.

```html
<iframe src="https://app.warp.dev/block/embed/qn0g1CqQnkYjEafPH5HCVT"
title="server script error" style="width: 712px; height: 397px; border:0;
overflow:hidden;" allow="clipboard-read; clipboard-write"></iframe>
```

--------------------------------

### Get session redirect API endpoint

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieves redirect information for a specific shared session. It returns a conversation_id if the agent sandbox has completed processing, or an empty object if no redirect is required.

```json
{
  "openapi": "3.0.0",
  "paths": {
    "/agent/sessions/{sessionUuid}/redirect": {
      "get": {
        "summary": "Get session redirect",
        "operationId": "getSessionRedirect",
        "parameters": [
          {
            "name": "sessionUuid",
            "in": "path",
            "required": true,
            "schema": { "type": "string" }
          }
        ],
        "responses": {
          "200": {
            "description": "Redirect information",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "conversation_id": { "type": "string" }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Add Repository Workflow

Source: https://docs.warp.dev/terminal/entry/yaml-workflows

This snippet demonstrates how to add a workflow to a specific repository. It involves navigating to the repository's root, creating the necessary .warp/workflows directory if it doesn't exist, and copying a local workflow file into this directory.

```bash
cd {{repository_path}}
mkdir -p .warp/workflows/
cp ~/path/to/my_awesome_workflow.yaml {{path_to_local_workflow_folder}}
```

--------------------------------

### Budget Exceeded Error

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/budget-exceeded

This error occurs when a team has reached its configured spending budget limit. It prevents new tasks or runs that would exceed the budget from starting.

```APIDOC
## Budget Exceeded Error

### Description
The `budget_exceeded` error is returned when your team has reached the spending budget limit configured in team settings. This prevents any new tasks, scheduled runs, or integration-triggered runs that would exceed the budget from starting.

### Method
This is an error response, not a specific API endpoint. It is typically returned with a `403 Forbidden` HTTP status.

### Endpoint
This error can occur on various endpoints related to task execution, such as `/api/v1/agent/tasks`.

### Parameters
N/A

### Request Example
N/A

### Response
#### Error Response (403 Forbidden)
- **type** (string) - A URI reference that identifies the problem type.
- **title** (string) - A short, human-readable summary of the problem.
- **status** (integer) - The HTTP status code.
- **instance** (string) - A URI that identifies this specific occurrence of the problem.
- **error** (string) - A human-readable explanation specific to this occurrence of the problem.
- **retryable** (boolean) - Indicates if the request can be retried.

#### Response Example
```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/budget-exceeded",
  "title": "Monthly spending budget of $50 has been reached.",
  "status": 403,
  "instance": "/api/v1/agent/tasks",
  "error": "Monthly spending budget of $50 has been reached.",
  "retryable": false
}
```

### How to resolve
1. Increase the spending budget in your team settings.
2. Wait for the budget period to reset (e.g., at the start of the next billing cycle).

If you do not have administrative privileges, contact your team administrator.
```

--------------------------------

### Define a Warp Agent Skill

Source: https://docs.warp.dev/agent-platform/capabilities/skills

Skills are defined using a markdown file structure with YAML frontmatter. The metadata includes a unique name and description, while the body provides step-by-step instructions and examples for the agent.

```markdown
---
name: add-feature-flag
description: Add a new feature flag to the codebase with proper configuration and documentation
---

# Add Feature Flag

## Instructions
1. Ask the user for the feature flag name and default value
2. Add the flag definition to `config/feature_flags.yaml`
3. Create a helper function in `src/utils/flags.ts`
4. Update the feature flags documentation in `docs/FEATURE_FLAGS.md`

## Configuration Format
Feature flags should follow this format in the YAML file:

feature_name:
  default: false
  description: "What this flag controls"
  owner: "team-name"

## Examples
- "Add a feature flag for the new checkout flow"
- "Create a flag to enable dark mode for beta users"
```

--------------------------------

### Run One-Off Agent in Cloud Environment

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/gitlab

Executes a one-off agent in the cloud environment to verify its functionality. Requires the environment ID and a prompt for the agent's task. This command is used to test the agent's connectivity and basic operation before integrating with external services.

```bash
oz agent run-cloud --environment <ENV_ID> --prompt "Your task here"
```

--------------------------------

### JSON Error Response for resource_unavailable

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/resource-unavailable

Example JSON payloads returned by the Warp API when a task encounters a resource_unavailable error. These responses include the error type, status code, and trace ID for debugging purposes.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/resource-unavailable",
  "title": "Agent capacity is temporarily full. Your task will be retried automatically, or you can try again later.",
  "status": 429,
  "instance": "/api/v1/agent/tasks",
  "error": "Agent capacity is temporarily full. Your task will be retried automatically, or you can try again later.",
  "retryable": true,
  "trace_id": "abc123..."
}
```

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/resource-unavailable",
  "title": "Failed to create a sandbox instance for your agent. This is typically a transient issue — your task will be retried automatically.",
  "status": 500,
  "instance": "/api/v1/agent/tasks",
  "error": "Failed to create a sandbox instance for your agent. This is typically a transient issue — your task will be retried automatically.",
  "retryable": true,
  "trace_id": "abc123..."
}
```

--------------------------------

### Example JSON Response for authentication_required Error

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/authentication-required

This JSON object represents a typical error response when authentication is required but not provided or invalid. It includes error details, status code, and instance information.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/authentication-required",
  "title": "Your API key is invalid or has expired. Please generate a new key and try again.",
  "status": 401,
  "instance": "/api/v1/agent/tasks",
  "error": "Your API key is invalid or has expired. Please generate a new key and try again.",
  "retryable": false
}
```

--------------------------------

### Create a Reusable Skill with Warp CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/quickstart

This command initiates the process of turning a successful agent workflow into a reusable skill. Follow the prompts to define and save your task. Skills can then be scheduled, triggered from integrations, or shared with your team.

```bash
/create-skill
```

--------------------------------

### POST /agent/run-cloud

Source: https://docs.warp.dev/agent-platform/capabilities/computer-use

Initiates a new agent run in the cloud with Computer Use capabilities enabled.

```APIDOC
## POST /agent/run-cloud

### Description
Creates a new agent run in a sandboxed cloud environment. By setting the `computer_use_enabled` flag, the agent gains the ability to interact with the desktop GUI, perform clicks, and type text.

### Method
POST

### Endpoint
/agent/run-cloud

### Parameters
#### Request Body
- **prompt** (string) - Required - The task description for the agent.
- **computer_use_enabled** (boolean) - Optional - Enables the Computer Use experimental feature (default: false).
- **environment_id** (string) - Optional - The specific environment configuration ID to use for the run.

### Request Example
{
  "prompt": "Build a button component that matches this design, then test it in the browser",
  "computer_use_enabled": true,
  "environment_id": "env-12345"
}

### Response
#### Success Response (200)
- **run_id** (string) - Unique identifier for the created agent run.
- **status** (string) - Current status of the agent initialization.

#### Response Example
{
  "run_id": "run_abc789",
  "status": "queued"
}
```

--------------------------------

### Example operation_not_supported JSON Response

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/operation-not-supported

This JSON object illustrates the structure of the 'operation_not_supported' error response from the Warp API. It includes the error type, title, HTTP status, instance, a detailed error message, and retryability.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/operation-not-supported",
  "title": "Self-hosted agent runs cannot be cancelled with the API.",
  "status": 422,
  "instance": "/api/v1/agent/tasks/abc123/cancel",
  "error": "Self-hosted agent runs cannot be cancelled with the API.",
  "retryable": false
}
```

--------------------------------

### Configure Linear CLI MCP Server

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This JSON configuration sets up a Linear CLI-based MCP server using npx. It connects to the Linear MCP service.

```json
{
  "Linear": {
    "command": "npx",
    "args": ["-y","mcp-remote","https://mcp.linear.app/sse"]
  }
}
```

--------------------------------

### Example JSON response for integration_disabled error

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/integration-disabled

This JSON object represents the standard error response returned by the API when a task fails due to a disabled integration. It includes the error type, status code, and a descriptive message for the user.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/integration-disabled",
  "title": "This integration is disabled. Please enable it in Oz.",
  "status": 403,
  "instance": "/api/v1/agent/tasks",
  "error": "This integration is disabled. Please enable it in Oz.",
  "retryable": false
}
```

--------------------------------

### Example Insufficient Credits Error Response (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/insufficient-credits

This JSON object represents the structure of the insufficient_credits error response from the Warp API. It includes details like the error type, title, HTTP status, and a trace ID.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/insufficient-credits",
  "title": "Your team has run out of add-on credits. Purchase more credits in your team's billing settings to continue.",
  "status": 403,
  "instance": "/api/v1/agent/tasks",
  "error": "Your team has run out of add-on credits. Purchase more credits in your team's billing settings to continue.",
  "retryable": false,
  "trace_id": "abc123..."
}
```

--------------------------------

### Integrate Oz Agent in GitHub Actions

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Demonstrates how to use the official Oz agent GitHub Action to automate agent execution within a CI/CD pipeline. Requires a valid API key stored in repository secrets.

```yaml
- name: Run Oz agent
  uses: warpdotdev/oz-agent-action@v1
  with:
    prompt: "Review the code changes on this branch"
    warp_api_key: ${{ secrets.WARP_API_KEY }}
```

--------------------------------

### Configure Figma Remote MCP Server

Source: https://docs.warp.dev/knowledge-and-collaboration/mcp

This configuration enables the official Figma remote MCP server, which supports OAuth for easy setup. After adding this configuration in Warp, a browser window will open for Figma authentication.

```json
{
  "Figma": {
    "url": "https://mcp.figma.com/mcp"
  }
}
```

--------------------------------

### Retrieve artifact details via OpenAPI specification

Source: https://docs.warp.dev/reference/api-and-sdk/agent

This OpenAPI definition describes the GET request for fetching artifact details by UUID. It includes schema definitions for successful artifact responses and standardized RFC 7807 error handling.

```json
{
  "openapi": "3.0.0",
  "paths": {
    "/agent/artifacts/{artifactUid}": {
      "get": {
        "summary": "Get artifact details",
        "operationId": "getArtifact",
        "parameters": [
          {
            "name": "artifactUid",
            "in": "path",
            "required": true,
            "schema": { "type": "string" }
          }
        ],
        "responses": {
          "200": {
            "description": "Artifact details with download information"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Example Not Authorized Error Response (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/not-authorized

This JSON object represents a typical error response when a 'not_authorized' error occurs. It includes details about the error type, title, HTTP status, specific details, instance identifier, and retryability.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/not-authorized",
  "title": "You do not have permission for this operation.",
  "status": 403,
  "detail": "user is not a member of the team",
  "instance": "/api/v1/agent/tasks/abc123",
  "error": "You do not have permission for this operation. (user is not a member of the team)",
  "retryable": false
}
```

--------------------------------

### Example Resource Not Found API Response (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/resource-not-found

This JSON object illustrates the structure of a 'resource_not_found' error response from the Warp API. It includes the error type, title, HTTP status, a detailed message about the missing resource, the instance of the request, a general error message, and retryability status.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/resource-not-found",
  "title": "The requested resource was not found.",
  "status": 404,
  "detail": "environment abc123 not found",
  "instance": "/api/v1/agent/tasks",
  "error": "The requested resource was not found. (environment abc123 not found)",
  "retryable": false
}
```

--------------------------------

### YAML Configuration for Accent Gradient (Left/Right) in Warp Theme

Source: https://docs.warp.dev/terminal/appearance/custom-themes

This YAML snippet shows how to configure a horizontal gradient for the accent color in a Warp theme. It uses 'left' and 'right' keys to define the start and end colors of the gradient.

```yaml
accent:
   left: '#abcdef'
   right: '#fedcba'
```

--------------------------------

### Conflict Error JSON Response

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/conflict

An example of the JSON response returned by the Warp API when a 409 Conflict error occurs. It includes the error type, a descriptive title, the status code, the instance path, and the retryable flag.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/conflict",
  "title": "Pending agent runs cannot be cancelled, retry after a moment.",
  "status": 409,
  "instance": "/api/v1/agent/tasks/abc123/cancel",
  "error": "Pending agent runs cannot be cancelled, retry after a moment.",
  "retryable": true
}
```

--------------------------------

### Example Content Policy Violation JSON Response

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/content-policy-violation

This JSON object represents a typical response when a content policy violation occurs. It includes error details, status code, and a trace ID for support.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/content-policy-violation",
  "title": "Unable to start cloud agent. Please try again or contact support if the issue persists.",
  "status": 403,
  "instance": "/api/v1/agent/tasks",
  "error": "Unable to start cloud agent. Please try again or contact support if the issue persists.",
  "retryable": false,
  "trace_id": "abc123..."
}
```

--------------------------------

### Budget Exceeded API Error Response

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/budget-exceeded

An example of the JSON response returned by the Warp API when a team's spending budget has been reached. It includes the error type, status code, and a descriptive message regarding the budget limit.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/budget-exceeded",
  "title": "Monthly spending budget of $50 has been reached.",
  "status": 403,
  "instance": "/api/v1/agent/tasks",
  "error": "Monthly spending budget of $50 has been reached.",
  "retryable": false
}
```

--------------------------------

### Example invalid_request API Response (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/invalid-request

This JSON object illustrates the structure of an invalid_request error response from the Warp API. It includes the error type, a human-readable title, the HTTP status code, a detailed explanation of the validation issue, the request instance, and a retryability flag.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/invalid-request",
  "title": "The request contains invalid or missing parameters.",
  "status": 400,
  "detail": "schedule_id is required",
  "instance": "/api/v1/agent/tasks",
  "error": "The request contains invalid or missing parameters. (schedule_id is required)",
  "retryable": false
}
```

--------------------------------

### Authenticate and Run Oz Agent via CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Configures the environment with an API key and executes the Oz agent with a specific prompt and sharing permissions. This is the primary method for running agents in unmanaged environments.

```bash
export WARP_API_KEY="your_team_api_key"
oz agent run --prompt "Refactor the authentication module" --share team
```

--------------------------------

### Run agent with MCP server configuration

Source: https://docs.warp.dev/reference/cli/mcp-servers

Demonstrates various ways to pass MCP server configurations to the agent, including UUID references, inline JSON, and external file paths.

```shell
# Using UUID
oz agent run --mcp "1deb1b14-b6e5-4996-ae99-233b7555d2d0" --prompt "who last updated the README?"

# Using Inline JSON
oz agent run --mcp '{"github": {"url": "https://api.githubcopilot.com/mcp/"}}' --prompt "list open issues"

# Using File Path
oz agent run --mcp ./my-mcp-config.json --prompt "list open issues"
```

--------------------------------

### Configure Sentry CLI MCP Server

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This JSON configuration sets up a Sentry CLI-based MCP server using npx. It connects to the Sentry MCP service.

```json
{
  "Sentry": {
    "command": "npx",
    "args": ["-y","mcp-remote@latest","https://mcp.sentry.dev/mcp"]
  }
}
```

--------------------------------

### Run Warp with Enhanced Logging on Windows

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

These PowerShell commands launch Warp or Warp Preview with enhanced logging enabled for 'wgpu_core' and 'wgpu_hal'. This is recommended for troubleshooting graphical glitches or crashes, providing more detailed diagnostic information.

```powershell
# Run if Warp on Windows is installed for a single user
$env:RUST_LOG="wgpu_core=info,wgpu_hal=info"; & "$env:LOCALAPPDATA\Programs\Warp\warp.exe"

# Run if Warp on Windows is installed for all users
$env:RUST_LOG="wgpu_core=info,wgpu_hal=info"; & "$env:PROGRAMFILES\Warp\warp.exe"

# Run if Warp Preview on Windows is installed for a single user
$env:RUST_LOG="wgpu_core=info,wgpu_hal=info"; & "$env:LOCALAPPDATA\Programs\WarpPreview\preview.exe"
```

--------------------------------

### Download Warp AppImage for ARM64 Systems

Source: https://docs.warp.dev/getting-started/quickstart/installation-and-setup

Downloads the Warp AppImage specifically for ARM64 architecture using curl and makes it executable with chmod. This ensures compatibility with ARM-based Linux devices.

```bash
# On ARM64 systems
curl -L "https://app.warp.dev/download?package=appimage_arm64" -o Warp-ARM64.AppImage
chmod +x Warp-ARM64.AppImage
```

--------------------------------

### Project Skill Directory Structure (File Tree)

Source: https://docs.warp.dev/agent-platform/capabilities/skills

Shows a typical file system structure for organizing project-level skills. It highlights the recommended `.agents/skills/` directory and other supported locations like `.claude/skills/` and `.github/skills/`, each containing individual skill subdirectories with a `SKILL.md` file.

```filetree
your-project/
├── .agents/
│   └── skills/
│       ├── add-feature-flag/
│       │   └── SKILL.md
│       └── run-migrations/
│           └── SKILL.md
├── .claude/
│   └── skills/
│       └── review-code/
│           └── SKILL.md
└── .github/
    └── skills/
        └── create-release/
            └── SKILL.md

```

--------------------------------

### Define Workflow Storage Paths

Source: https://docs.warp.dev/terminal/entry/yaml-workflows

Displays the directory paths required to store local Warp workflows on macOS, Windows, and Linux systems.

```bash
$HOME/.warp/workflows/
```

```powershell
$env:APPDATA\warp\Warp\data\workflows\
```

```bash
${XDG_DATA_HOME:-$HOME/.local/share}/warp-terminal/workflows/
```

--------------------------------

### MCP Server Configuration

Source: https://docs.warp.dev/reference/api-and-sdk/models

Configuration for attaching an MCP server to an agent run.

```APIDOC
## MCP Server Configuration

### Description
Configuration for a single MCP (Model Context Protocol) server to attach to an agent run. Exactly one of `warp_id`, `command`, or `url` must be provided, corresponding to the three supported transports.

### Object: MCPServerConfig

- **warp_id** (string) - Reference a Warp-managed shared MCP server by UUID
- **command** (string) - Command to execute to start the MCP server
- **url** (string) - URL of the MCP server

```

--------------------------------

### Configure Notion MCP Server

Source: https://docs.warp.dev/knowledge-and-collaboration/rules

Sets up Notion integration via npx CLI or SSE URL. Allows interaction with Notion pages and databases.

```json
{
  "Notion": {
    "command": "npx",
    "args": ["-y", "mcp-remote", "https://mcp.notion.com/mcp"]
  }
}
```

```json
{
  "Notion": {
    "url": "https://mcp.notion.com/sse"
  }
}
```

--------------------------------

### Run Warp with Enhanced Logging on macOS

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

These commands execute Warp or Warp Preview with increased logging verbosity for specific components (wgpu_core, wgpu_hal). This is useful for diagnosing graphical issues or application crashes by capturing more detailed log information.

```bash
# Run if Warp on macOS is installed
RUST_LOG=wgpu_core=info,wgpu_hal=info /Applications/Warp.app/Contents/MacOS/stable

# Run if Warp Preview on macOS is installed
RUST_LOG=wgpu_core=info,wgpu_hal=info /Applications/WarpPreview.app/Contents/MacOS/preview
```

--------------------------------

### POST /agent/run

Source: https://docs.warp.dev/agent-platform/cloud-agents/skills-as-agents

Initiates a new agent run based on a specific skill specification and provided context.

```APIDOC
## POST /agent/run

### Description
Starts an agent execution using a defined skill. The skill provides the base instructions, while the prompt provides specific context for the run.

### Method
POST

### Endpoint
/agent/run

### Request Body
- **prompt** (string) - Required - Additional context for this specific run
- **config** (object) - Required - Configuration settings
  - **environment_id** (string) - Required - The ID of the environment to run in
  - **skill_spec** (string) - Required - The fully qualified skill identifier (owner/repo:skill-name)

### Request Example
{
  "prompt": "additional context for this run",
  "config": {
    "environment_id": "<ENV_ID>",
    "skill_spec": "owner/repo:skill-name"
  }
}

### Response
#### Success Response (200)
- **run_id** (string) - Unique identifier for the agent execution
- **status** (string) - Current status of the run

#### Response Example
{
  "run_id": "abc-123-xyz",
  "status": "queued"
}
```

--------------------------------

### Execute Local Agents with Skills

Source: https://docs.warp.dev/reference/cli/skills

Shows how to invoke skills when running local agents. While local skills are often auto-discovered, they can be explicitly defined using the --skill flag.

```bash
oz agent run --skill "owner/repo:skill-name" --prompt "additional context"
```

--------------------------------

### Run Warp Agent Locally

Source: https://docs.warp.dev/reference/cli/cli

Executes an agent in the local environment. Requires a prompt and optionally accepts MCP servers and agent profiles. Key flags include --cwd for directory, --name for labeling, and --share for collaboration.

```sh
oz agent run --prompt "set up a new Rust crate named warp-cli"
I'll run a few terminal commands to:
- Check if this is a Git repo and Cargo workspace
- Create a new binary crate named warp-cli
```

--------------------------------

### Authenticate and Run Agents with Oz CLI

Source: https://docs.warp.dev/reference/cli/cli

Commands for authenticating the CLI via interactive login or API keys, and executing agent tasks.

```bash
oz login
```

```sh
export WARP_API_KEY="wk-xxx..."
oz agent run --prompt "analyze this codebase"
```

--------------------------------

### Configure Slack MCP Server

Source: https://docs.warp.dev/knowledge-and-collaboration/rules

Sets up Slack integration using npx for CLI or an SSE URL. Requires bot and app tokens for workspace access.

```json
{
  "Slack": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-slack"],
    "env": {
      "SLACK_BOT_TOKEN": "xoxb-<your-bot-token>",
      "SLACK_APP_TOKEN": "xapp-<your-app-token>",
      "SLACK_TEAM_ID": "T<your_workspace_id>",
      "SLACK_CHANNEL_IDS": "<your_channel_id-1>, <your_channel_id-2>",
      "MCP_MODE": "stdio"
    }
  }
}
```

```json
{
  "Slack": {
    "url": "https://your-mcp-host.com/api/mcp/slack/sse"
  }
}
```

--------------------------------

### POST /agent/runs

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Creates a new agent run. This is the preferred method for initiating agent tasks.

```APIDOC
## POST /agent/runs

### Description
Creates a new agent run. This is the preferred endpoint for creating new agent runs and is an alias for POST /agent/run.

### Method
POST

### Endpoint
/agent/runs

### Request Body
- **prompt** (string) - Required - The instruction or prompt for the agent.
- **config** (object) - Optional - Configuration settings for the agent execution.

### Request Example
{
  "prompt": "Analyze the provided logs and summarize errors."
}

### Response
#### Success Response (200)
- **run_id** (string) - Unique identifier for the created run.
- **task_id** (string) - Deprecated identifier for the task.
- **state** (string) - The initial state of the run (e.g., QUEUED, PENDING).
- **at_capacity** (boolean) - Whether the system is at capacity.

#### Response Example
{
  "run_id": "run_12345",
  "task_id": "run_12345",
  "state": "QUEUED",
  "at_capacity": false
}
```

--------------------------------

### Running Agents Locally

Source: https://docs.warp.dev/reference/cli/cli

Execute agent tasks on your local machine using the `oz agent run` command. This command allows for specifying a prompt and optional configurations like MCP servers and agent profiles.

```APIDOC
## Running Agents Locally

### Description
Execute agent tasks on your local machine using the `oz agent run` command. This command allows for specifying a prompt and optional configurations like MCP servers and agent profiles.

### Method
CLI Command

### Endpoint
`oz agent run`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

**Key flags:**

*   `--prompt <PROMPT>` - The task for the agent to perform.
*   `--cwd <PATH>` (`-C`) - Run from a different directory.
*   `--name <NAME>` (`-n`) - Label the run for grouping and traceability.
*   `--share` - Share the session with teammates.
*   `--profile <ID>` - Use a specific agent profile.
*   `--model <MODEL_ID>` - Override the default model.
*   `--skill <SPEC>` - Use a skill as the base prompt.
*   `--mcp <SPEC>` - Start one or more MCP servers before execution. Can be repeated.
*   `--environment <ID>` (`-e`) - Run in a specific cloud environment.
*   `--file <PATH>` (`-f`) - Load run configuration from a YAML or JSON file.

### Request Example
```sh
oz agent run --prompt "set up a new Rust crate named warp-cli"
```

### Response
#### Success Response (200)
The agent will automatically carry out the task, printing out tool calls and responses as it works.

#### Response Example
```
I'll run a few terminal commands to:
- Check if this is a Git repo and Cargo workspace
- Create a new binary crate named warp-cli
```
```

--------------------------------

### Configure Grafana CLI MCP Server

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This JSON configuration sets up a Grafana CLI-based MCP server using Docker. It requires Grafana URL and API key environment variables.

```json
{
  "Grafana": {
    "command": "docker",
    "args": ["run","--rm","-i","-e","GRAFANA_URL","-e","GRAFANA_API_KEY","mcp/grafana","-t","stdio","-debug"],
    "env": {
      "GRAFANA_URL": "http://localhost:3000",
      "GRAFANA_API_KEY": "<your_grafana_key>"
    }
  }
}
```

--------------------------------

### Run Source Types

Source: https://docs.warp.dev/reference/api-and-sdk/models

Details the different sources that can create a run within the Warp system.

```APIDOC
## Run Source Types

### Description
This section defines the various sources from which a run can be initiated within the Warp platform.

### Enum: RunSourceType

Source that created the run:

- `LINEAR` - Created from Linear integration
- `API` - Created via the Warp API
- `SLACK` - Created from Slack integration
- `LOCAL` - Created from local CLI/app
- `SCHEDULED_AGENT` - Created by a scheduled agent
- `WEB_APP` - Created from the Warp web app
- `GITHUB_ACTION` - Created from a GitHub action
- `CLOUD_MODE` - Created from a Cloud Mode
- `CLI` - Created from the CLI

```

--------------------------------

### Pagination and Ownership Metadata

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the standard structures for resource ownership and cursor-based pagination used across the API.

```APIDOC
## Resource Metadata Structures

### Description
This section defines the standard objects used for identifying resource ownership and handling paginated data responses.

### Ownership Object
- **owner_uid** (string) - Required - UID of the owning user or team.

### PageInfo Object
- **has_next_page** (boolean) - Required - Whether there are more results available.
- **next_cursor** (string) - Optional - Opaque cursor for fetching the next page. When has_next_page is true, pass this as the cursor parameter on the next request.

### Response Example
{
  "owner_uid": "user_12345",
  "page_info": {
    "has_next_page": true,
    "next_cursor": "eyJhbGciOiJIUzI1NiJ9"
  }
}
```

--------------------------------

### Create platform integrations via Oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations

Registers a new integration for Slack or Linear using a specific environment ID. These commands initiate an authorization flow to connect the Oz agent to the respective workspace.

```shell
oz integration create slack --environment <ENV_ID>
oz integration create linear --environment <ENV_ID>
```

--------------------------------

### MCPServerConfig Schema Details (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the configuration for a single MCP (Model Context Protocol) server, supporting different transport methods like Warp-managed servers, local command execution, or remote HTTP/SSE connections.

```json
{
  "MCPServerConfig": {
    "type": "object",
    "description": "Configuration for a single MCP (Model Context Protocol) server to attach to an agent run.\nExactly one of warp_id, command, or url must be provided, corresponding to the three\nsupported transports:\n- warp_id: reference a Warp-managed shared MCP server by UUID\n- command + args: launch a local stdio-based MCP server process\n- url: connect to a remote SSE or HTTP MCP server\n",
    "properties": {
      "warp_id": {
        "type": "string",
        "description": "Reference to a Warp shared MCP server by UUID"
      },
      "command": {
        "type": "string",
        "description": "Stdio transport - command to run"
      },
      "args": {
        "type": "array",
        "items": {
          "type": "string"
        },
        "description": "Stdio transport - command arguments"
      },
      "url": {
        "type": "string",
        "format": "uri",
        "description": "SSE/HTTP transport - server URL"
      },
      "env": {
        "type": "object",
        "additionalProperties": {
          "type": "string"
        },
        "description": "Environment variables for the server"
      },
      "headers": {
        "type": "object",
        "additionalProperties": {
          "type": "string"
        },
        "description": "HTTP headers for SSE/HTTP transport"
      }
    }
  }
}
```

--------------------------------

### Enable Computer Use via CLI

Source: https://docs.warp.dev/agent-platform/capabilities/computer-use

Control the Computer Use feature when initiating cloud agent runs through the Warp CLI using specific flags.

```bash
oz agent run-cloud --computer-use --prompt "<task>"
oz agent run-cloud --no-computer-use --prompt "<task>"
```

--------------------------------

### GitHub MCP Server Configuration

Source: https://docs.warp.dev/university/end-to-end-builds/building-a-real-time-chat-app-github-mcp-%2B-railway

Configuration block for integrating the GitHub Model Context Protocol (MCP) server into Warp. This allows the AI agent to interact with GitHub repositories directly.

```json
{
  "github": {
    "command": "docker",
    "args": [
      "run",
      "-i",
      "--rm",
      "-e",
      "GITHUB_PERSONAL_ACCESS_TOKEN",
      "ghcr.io/github/github-mcp-server"
    ],
    "env": {
      "GITHUB_PERSONAL_ACCESS_TOKEN": "your_token_here"
    }
  }
}
```

--------------------------------

### CloudEnvironmentConfig Schema Details (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Describes the configuration for a cloud environment used by scheduled agents, including its name and a brief description.

```json
{
  "CloudEnvironmentConfig": {
    "type": "object",
    "description": "Configuration for a cloud environment used by scheduled agents",
    "properties": {
      "name": {
        "type": "string",
        "description": "Human-readable name for the environment"
      },
      "descr": {
        "type": "string",
        "description": "Description of the environment"
      }
    }
  }
}
```

--------------------------------

### Combine multiple MCP servers

Source: https://docs.warp.dev/reference/cli/mcp-servers

Shows how to include multiple MCP server configurations in a single agent execution by repeating the --mcp flag.

```shell
oz agent run \
  --mcp "1deb1b14-b6e5-4996-ae99-233b7555d2d0" \
  --mcp '{"sentry": {"url": "https://mcp.sentry.dev/sse"}}' \
  --prompt "open a PR that fixes the top Sentry error"
```

--------------------------------

### Configure GitHub MCP Server

Source: https://docs.warp.dev/knowledge-and-collaboration/rules

Provides configurations for connecting GitHub via CLI using Docker or via an SSE endpoint. Requires a GitHub Personal Access Token for authentication.

```json
{
  "GitHub": {
    "command": "docker",
    "args": ["run","-i","--rm","-e","GITHUB_PERSONAL_ACCESS_TOKEN","ghcr.io/github/github-mcp-server"],
    "env": {
      "GITHUB_PERSONAL_ACCESS_TOKEN": "<your_github_token>"
    }
  }
}
```

```json
{
  "GitHub": {
    "url": "https://api.githubcopilot.com/mcp/"
  }
}
```

--------------------------------

### Skill with Argument Placeholders (Markdown)

Source: https://docs.warp.dev/agent-platform/capabilities/skills

Demonstrates a skill defined in Markdown that utilizes argument placeholders for dynamic content. It shows how `$0`, `$1`, `$2`, and `$ARGUMENTS` are replaced with provided values during skill invocation.

```markdown
---
name: explain-topic
description: Explain a topic for a specific audience in a given tone
---

# Explain Topic

Explain $0 for an audience of $1 professionals.

Use a $2 tone.

Full request: $ARGUMENTS

```

--------------------------------

### Combine Multiple MCP Servers

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

Demonstrates how to combine multiple MCP servers for a single agent run by repeating the `--mcp` flag. This allows for integration with several external services simultaneously.

```bash
$ oz agent run \
  --mcp "1deb1b14-b6e5-4996-ae99-233b7555d2d0" \
  --mcp '{"sentry": {"url": "https://mcp.sentry.dev/sse"}}' \
  --prompt "open a PR that fixes the top Sentry error"
```

--------------------------------

### POST /agent/schedules

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Creates a new scheduled agent. This endpoint allows for the configuration of agents that will run on a schedule, including details about the environment, repository, and execution commands.

```APIDOC
## POST /agent/schedules

### Description
Create a new scheduled agent that runs on a defined schedule.

### Method
POST

### Endpoint
/agent/schedules

### Parameters
#### Request Body
- **name** (string) - Required - Name of the scheduled agent.
- **description** (string) - Optional - Description for the scheduled agent.
- **schedule** (string) - Required - Cron expression defining the schedule.
- **agent_config** (object) - Required - Configuration for the agent.
  - **docker_image** (string) - Required - Docker image to use.
  - **github_repos** (array) - Optional - List of GitHub repositories to clone.
    - **owner** (string) - Required - GitHub repository owner.
    - **repo** (string) - Required - GitHub repository name.
  - **setup_commands** (array) - Optional - Shell commands to run during setup.
- **environment** (object) - Optional - Resolved environment configuration.
  - **name** (string) - Required - Human-readable name for the environment.
  - **description** (string) - Optional - Optional description of the environment.
  - **docker_image** (string) - Required - Docker image to use.
  - **github_repos** (array) - Optional - List of GitHub repositories to clone.
    - **owner** (string) - Required - GitHub repository owner.
    - **repo** (string) - Required - GitHub repository name.
  - **setup_commands** (array) - Optional - Shell commands to run during environment setup.
- **scope** (object) - Required - Ownership scope for the resource.
  - **type** (string) - Required - Type of ownership ("User" or "Team").
  - **uid** (string) - Required - UID of the owning user or team.

### Request Example
```json
{
  "name": "My Scheduled Agent",
  "description": "Runs a daily cleanup task.",
  "schedule": "0 0 * * *",
  "agent_config": {
    "docker_image": "ubuntu:latest",
    "setup_commands": [
      "apt-get update",
      "apt-get install -y some-package"
    ]
  },
  "environment": {
    "name": "Development Environment",
    "docker_image": "python:3.9-slim",
    "github_repos": [
      {
        "owner": "my-org",
        "repo": "my-repo"
      }
    ]
  },
  "scope": {
    "type": "Team",
    "uid": "team-123"
  }
}
```

### Response
#### Success Response (200)
- **id** (string) - Unique identifier for the scheduled agent.
- **name** (string) - Name of the scheduled agent.
- **description** (string) - Description for the scheduled agent.
- **schedule** (string) - Cron expression defining the schedule.
- **agent_config** (object) - Configuration for the agent.
- **environment** (object) - Resolved environment configuration.
- **created_at** (string) - Timestamp when the schedule was created (RFC3339).
- **updated_at** (string) - Timestamp when the schedule was last updated (RFC3339).
- **created_by** (object) - Information about the creator.
- **updated_by** (object) - Information about the last updater.
- **history** (object) - History of the scheduled agent runs.
- **scope** (object) - Ownership scope for the resource.

#### Response Example
```json
{
  "id": "schedule-abc123xyz",
  "name": "My Scheduled Agent",
  "description": "Runs a daily cleanup task.",
  "schedule": "0 0 * * *",
  "agent_config": {
    "docker_image": "ubuntu:latest",
    "setup_commands": [
      "apt-get update",
      "apt-get install -y some-package"
    ]
  },
  "environment": {
    "name": "Development Environment",
    "docker_image": "python:3.9-slim",
    "github_repos": [
      {
        "owner": "my-org",
        "repo": "my-repo"
      }
    ]
  },
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:00:00Z",
  "created_by": {
    "type": "user",
    "uid": "user-456",
    "display_name": "Jane Doe",
    "email": "jane.doe@example.com"
  },
  "updated_by": {
    "type": "user",
    "uid": "user-456",
    "display_name": "Jane Doe",
    "email": "jane.doe@example.com"
  },
  "history": {
    "last_ran": null,
    "next_run": "2023-10-28T00:00:00Z"
  },
  "scope": {
    "type": "Team",
    "uid": "team-123"
  }
}
```
```

--------------------------------

### Passing MCP servers as inline JSON or a file

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

MCP server configurations can be provided directly as inline JSON or by referencing a JSON configuration file.

```APIDOC
## Passing MCP servers as inline JSON or a file

You can pass MCP configuration inline or via a file:

```
# Inline JSON
$ oz agent run --mcp '{"github": {"url": "https://api.githubcopilot.com/mcp/"}}' --prompt "list open issues"

# From a file
$ oz agent run --mcp ./my-mcp-config.json --prompt "list open issues"
```

The file must contain a valid MCP JSON object. For example:

```
{
  "github": {
    "url": "https://api.githubcopilot.com/mcp/"
  },
  "sentry": {
    "command": "npx",
    "args": ["-y", "mcp-remote@latest", "https://mcp.sentry.dev/mcp"]
  }
}
```
```

--------------------------------

### Astro Project File Structure

Source: https://docs.warp.dev/university/developer-workflows/beginner/how-to-create-project-rules-for-an-existing-project-astro-%2B-typescript-%2B-tailwind

This snippet illustrates the directory structure of the Astro project. It highlights key directories such as `pages` for API routes and page components, `components` for UI elements, `lib` for business logic, `types` for TypeScript definitions, `data` for static assets, and `firebase` for configuration.

```tree
src/
├── pages/
│   ├── api/           # Astro API routes (serverless functions)
│   ├── index.astro    # Homepage with hero and marquee
│   ├── brewfiles.astro # Search and browse brewfiles
│   └── leaderboard.astro # Package popularity rankings
├── components/        # Astro and React components
├── lib/              # Core business logic and utilities
├── types/            # TypeScript type definitions
├── data/             # Static data and package dictionaries
└── firebase/         # Firebase configuration
```

--------------------------------

### Authenticate with Oz CLI using API keys

Source: https://docs.warp.dev/reference/cli/api-keys

Demonstrates how to authenticate the Oz CLI using an API key. Users can either set the key as an environment variable for session-wide access or pass it directly via a command flag.

```shell
export WARP_API_KEY="wk-xxx..."
oz agent run --prompt "analyze this codebase"
```

```shell
oz agent run --api-key "wk-xxx..." --prompt "analyze this codebase"
```

--------------------------------

### Request Usage

Source: https://docs.warp.dev/reference/api-and-sdk/models

Provides information on resource usage for a specific run.

```APIDOC
## Request Usage

### Description
Resource usage information for the run.

### Object: RequestUsage

- **inference_cost** (number) - Cost of LLM inference for the run
- **compute_cost** (number) - Cost of compute resources for the run

```

--------------------------------

### Access MCP Server Logs Directory

Source: https://docs.warp.dev/knowledge-and-collaboration/mcp

Commands to navigate to the local directory where Warp stores MCP server logs, categorized by operating system.

```bash
cd "$HOME/Library/Group Containers/2BBY89MBSN.dev.warp/Library/Application Support/dev.warp.Warp-Stable/mcp"
```

```powershell
Set-Location $env:LOCALAPPDATA\warp\Warp\data\logs\mcp
```

```bash
cd "${XDG_STATE_HOME:-$HOME/.local/state}/warp-terminal/mcp"
```

--------------------------------

### Running Cloud Agent with Config File (Shell)

Source: https://docs.warp.dev/agent-platform/cloud-agents/mcp

Command to execute a Warp cloud agent using a specified configuration file. This shell command includes the environment ID, the path to the agent configuration file, and the user prompt.

```sh
oz agent run-cloud --environment <ENV_ID> -f my-agent-config.json --prompt "Check for regressions in the last deploy"
```

--------------------------------

### Execute Standard Shell Commands in Warp

Source: https://docs.warp.dev/university/developer-workflows/beginner/welcome-to-warp

Demonstrates the use of standard Unix-like shell commands within the Warp terminal. These commands function identically to traditional terminal environments, providing a familiar interface for system navigation.

```bash
ls
pwd
```

--------------------------------

### Run an agent task

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Spawn a cloud agent with a prompt and optional configuration. The agent will be queued for execution and assigned a unique run ID.

```APIDOC
## POST /api/v1/agent/runs

### Description
Spawns a cloud agent with a prompt and optional configuration. The agent will be queued for execution and assigned a unique run ID.

### Method
POST

### Endpoint
/api/v1/agent/runs

### Parameters
#### Request Body
- **prompt** (string) - Optional - The prompt/instruction for the agent to execute. Required unless a skill is specified via the skill field or config.skill_spec.
- **skill** (string) - Optional - Skill specification to use as the base prompt for the agent. Supported formats: "repo:skill_name", "repo:skill_path", "org/repo:skill_name", "org/repo:skill_path". When provided, this takes precedence over config.skill_spec.
- **config** (object) - Optional - Per-run configuration for a cloud agent. Controls which LLM model is used, which skill (SKILL.md) drives the agent's instructions, which environment the agent executes in, any MCP servers to enable, and optional base prompt overrides. All fields are optional; when omitted, the agent uses the system default for each setting.
  - **name** (string) - Optional - Human-readable label for grouping, filtering, and traceability. Automatically set to the skill name when running a skill-based agent.
  - **model_id** (string) - Optional - LLM model to use (uses team default if not specified).
  - **base_prompt** (string) - Optional - Custom base prompt for the agent.
  - **environment_id** (string) - Optional - UID of the environment to run the agent in.
  - **skill_spec** (string) - Optional - Skill specification identifying which agent skill to use. Format: "{owner}/{repo}:{skill_path}". Example: "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md".
  - **mcp_servers** (object) - Optional - Map of MCP server configurations by name.
  - **computer_use_enabled** (boolean) - Optional - Controls whether computer use is enabled for this agent. Defaults to false.
  - **worker_host** (string) - Optional - Self-hosted worker ID that should execute this task. If not specified or set to "warp", the task runs on Warp-hosted workers.
- **title** (string) - Optional - Custom title for the run (auto-generated if not provided).
- **team** (boolean) - Optional - Whether to create a team-owned run. Defaults to true for users on a single team.
- **conversation_id** (string) - Optional - Optional conversation ID to continue an existing conversation.
- **attachments** (array) - Optional - Optional file attachments to include with the prompt (max 5). Attachments are uploaded to cloud storage and made available to the agent.
- **interactive** (boolean) - Optional - Whether the run should be interactive. Defaults to false.

### Request Example
```json
{
  "prompt": "Write a summary of the latest project status.",
  "config": {
    "model_id": "claude-3-opus-20240229",
    "environment_id": "env_abc123"
  },
  "title": "Project Status Summary"
}
```

### Response
#### Success Response (200)
- **run_id** (string) - The unique ID assigned to the agent run.
- **status** (string) - The initial status of the agent run (e.g., "queued").

#### Response Example
```json
{
  "run_id": "run_xyz789",
  "status": "queued"
}
```
```

--------------------------------

### Configure Slack CLI Server using npx

Source: https://docs.warp.dev/knowledge-and-collaboration/mcp

This configuration sets up the Slack CLI server using npx. It requires Slack bot token, app token, team ID, and channel IDs as environment variables. MCP mode is set to stdio.

```json
{
  "Slack": {
    "command": "npx",
    "args": ["-y", "@modelcontextprotocol/server-slack"],
    "env": {
      "SLACK_BOT_TOKEN": "xoxb-<your-bot-token>",
      "SLACK_APP_TOKEN": "xapp-<your-app-token>",
      "SLACK_TEAM_ID": "T<your_workspace_id>",
      "SLACK_CHANNEL_IDS": "<your_channel_id-1>, <your_channel_id-2>",
      "MCP_MODE": "stdio"
    }
  }
}
```

--------------------------------

### Run Agent with MCP Server from File

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

Connects an agent to an external service using an MCP server configuration defined in a JSON file. This is suitable for complex or reusable configurations.

```bash
$ oz agent run --mcp ./my-mcp-config.json --prompt "list open issues"
```

--------------------------------

### Authenticate AWS CLI

Source: https://docs.warp.dev/enterprise/enterprise-features/bring-your-own-llm

Command used by team members to authenticate their local environment with AWS before using Warp.

```bash
aws login
```

--------------------------------

### MCP Server Configuration Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Details the structure of the MCPServerConfig object, used for configuring MCP servers for agent runs.

```APIDOC
## MCPServerConfig Object

### Description
Configuration for a single MCP (Model Context Protocol) server to attach to an agent run.

### Properties
Exactly one of `warp_id`, `command`, or `url` must be provided, corresponding to the three supported transports:
- **warp_id** (string) - Reference a Warp-managed shared MCP server by UUID.
- **command** (string) - Stdio transport - command to run.
- **args** (array) - Stdio transport - arguments for the command. Items are strings.
- **url** (string) - Connect to a remote SSE or HTTP MCP server.

### Example
#### Using warp_id
```json
{
  "warp_id": "warp_mcp_server_uuid"
}
```

#### Using command and args
```json
{
  "command": "/usr/local/bin/my_mcp_server",
  "args": ["--port", "8080"]
}
```

#### Using url
```json
{
  "url": "http://mcp.example.com/stream"
}
```
```

--------------------------------

### Cloud Environment Config Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Configuration for a cloud environment used by scheduled agents.

```APIDOC
## Cloud Environment Config Object

### Description
Configuration for a cloud environment used by scheduled agents.

### Properties
- **name** (string) - Human-readable name for the environment.
- **description** (string) - Description of the environment.
```

--------------------------------

### Naming Runs

Source: https://docs.warp.dev/reference/cli/cli

Assign a configuration name to agent runs using the `--name` flag for easier tracking, filtering, and searching of related runs.

```APIDOC
## Naming Runs

### Description
Assign a configuration name to agent runs using the `--name` flag for easier tracking, filtering, and searching of related runs. This is particularly useful for grouping recurring workflows or custom automations.

### Method
CLI Flag

### Endpoint
`--name <NAME>` (used with `oz agent run` and `oz agent run-cloud`)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

**How names work:**

*   **Skill-based runs**: The name is automatically set to the skill name.
*   **Custom runs**: Set `--name` to a consistent value describing the workflow's intent.

**Why naming matters:**

Allows you to answer questions like "how many distinct workflows are we running?" and "how often does this particular workflow run?" You can filter runs by name using the `name` query parameter on `GET /agent/runs` in the Oz API.

### Request Example
```sh
# Name a recurring workflow for easy tracking
oz agent run-cloud \
  --environment <ENVIRONMENT_ID> \
  --name "nightly-dependency-check" \
  --prompt "Check for outdated dependencies and open a PR with updates"

# Skill-based runs are named automatically
oz agent run-cloud \
  --environment <ENVIRONMENT_ID> \
  --skill "myorg/backend:code-review" \
  --prompt "review the latest PR"
```

### Response
#### Success Response (200)
Runs are labeled with the provided name, enabling easier management and analysis.

#### Response Example
None provided, as this describes a flag's behavior.
```

--------------------------------

### Create Theme Directory (macOS/Linux)

Source: https://docs.warp.dev/terminal/appearance/custom-themes

Creates the necessary directory structure for custom themes on macOS and Linux. This is a prerequisite for adding custom theme files to Warp Terminal.

```bash
mkdir -p $HOME/.warp/themes/
```

```bash
mkdir -p ${XDG_DATA_HOME:-$HOME/.local/share}/warp-terminal/themes/
```

--------------------------------

### MCP Server Config Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Configuration for an MCP server to attach to an agent run.

```APIDOC
## MCP Server Config Object

### Description
Configuration for a single MCP (Model Context Protocol) server to attach to an agent run. Exactly one of warp_id, command, or url must be provided, corresponding to the three supported transports:
- warp_id: reference a Warp-managed shared MCP server by UUID
- command + args: launch a local stdio-based MCP server process
- url: connect to a remote SSE or HTTP MCP server

### Properties
- **warp_id** (string) - Reference to a Warp shared MCP server by UUID.
- **command** (string) - Stdio transport - command to run.
- **args** (array of strings) - Stdio transport - command arguments.
- **url** (string, format: uri) - SSE/HTTP transport - server URL.
- **env** (object) - Environment variables for the server.
- **headers** (object) - HTTP headers for SSE/HTTP transport.
```

--------------------------------

### Warp Panes Configuration

Source: https://docs.warp.dev/terminal/sessions/launch-configurations

Demonstrates setting up split panes within tabs in a Warp launch configuration. Supports nested splits and different split directions (vertical/horizontal).

```yaml
# Warp Launch Configuration
#
# This configuration is two windows, each with split panes. 
# The first window contains a vertically split tab with two panes.
# The second window contains a horizontally split tab, 
# with a vertically split tab on the right.

---
name: Example Panes
windows:
  - tabs:
      - title: Downloads and Warp User
        layout:
          split_direction: vertical
          panes:
            - cwd: /Users/warp-user/Downloads
            - cwd: /Users/warp-user
        color: blue
  - tabs:
      - title: Desktop, Documents, and Warp User
        layout:
          split_direction: horizontal
          panes:
            - cwd: /Users/warp-user/Desktop
            - split_direction: vertical
              panes:
                - cwd: /Users/warp-user/Documents
                - cwd: /Users/warp-user
        color: green
```

--------------------------------

### Configure API Key Environment Variable

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Sets the team-scoped API key as an environment variable for the current session to authenticate the worker with the Warp backend.

```bash
export WARP_API_KEY="your_team_api_key"
```

--------------------------------

### Combine Skills and Custom Prompts in GitHub Actions

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/github-actions

Shows how to refine agent behavior by combining a pre-defined skill with a specific prompt. This allows for specialized tasks like focusing a code review on security vulnerabilities.

```yaml
with:
  skill: 'code-review'
  prompt: 'Focus on security vulnerabilities in authentication code'
  warp_api_key: ${{ secrets.WARP_API_KEY }}
```

--------------------------------

### GitHubRepo Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for specifying a GitHub repository to be cloned into a cloud environment.

```APIDOC
## GitHubRepo Object

### Description
Used to identify a GitHub repository by its owner and repository name for environment provisioning.

### Properties
- **owner** (string) - Required - GitHub repository owner (user or organization).
- **repo** (string) - Required - GitHub repository name.

### Example
{
  "owner": "warp-dev",
  "repo": "api-docs"
}
```

--------------------------------

### Bash Script for Generating Warp Theme Previews

Source: https://docs.warp.dev/terminal/appearance/custom-themes

This bash command executes a Python script to generate theme previews, typically used when contributing new themes. It assumes the script is located in the `./scripts/` directory and the theme is being added to the `standard` directory.

```bash
# Assuming you're adding the theme to the `standard` directory:
python3 ./scripts/gen_theme_previews.py standard
```

--------------------------------

### Zip Warp Preview Logs on macOS

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

This command zips the Warp Preview log files from the user's Library directory to the Desktop. It utilizes the 'zip' utility to create an archive. Ensure Warp Preview is not running during log collection.

```bash
zip -j ~/Desktop/warp_preview-logs.zip ~/Library/Logs/warp_preview.log*
```

--------------------------------

### Define GitHubRepo Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for identifying a GitHub repository. It requires both the owner and the repository name to facilitate cloning into cloud environments.

```json
{
  "type": "object",
  "description": "A GitHub repository identified by owner and repository name",
  "required": ["owner", "repo"],
  "properties": {
    "owner": { "type": "string", "description": "GitHub repository owner" },
    "repo": { "type": "string", "description": "GitHub repository name" }
  }
}
```

--------------------------------

### AgentListEnvironment Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Represents an environment where a skill variant can be executed.

```APIDOC
## AgentListEnvironment Object

### Description
An environment in which a skill variant is available and can be executed.

### Properties
- **uid** (string) - Required - Unique identifier for the environment
- **name** (string) - Required - Human-readable name of the environment
```

--------------------------------

### POST /schedules

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Creates a new scheduled agent that triggers automatically based on a provided cron expression.

```APIDOC
## POST /schedules

### Description
Creates a new agent scheduled to run on a specific cron interval.

### Method
POST

### Endpoint
/schedules

### Request Body
- **CreateScheduledAgentRequest** (object) - Required - The configuration object containing the agent details and cron expression.

### Request Example
{
  "agent_id": "agent_123",
  "cron": "0 * * * *"
}

### Response
#### Success Response (201)
- **ScheduledAgentItem** (object) - The created scheduled agent resource.

#### Error Responses
- **400** - Invalid request (missing required fields, invalid cron expression)
- **401** - Authentication required
- **403** - No permission or feature not available

#### Response Example
{
  "id": "sched_abc123",
  "agent_id": "agent_123",
  "cron": "0 * * * *",
  "status": "active"
}
```

--------------------------------

### Route Runs to Self-Hosted Worker via API

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Initiates a run via the Oz API and directs it to a self-hosted worker by including the `worker_host` field in the request payload. This allows programmatic control over task routing. Requires authentication with an API key.

```bash
curl -X POST https://app.warp.dev/api/v1/agent/run \
  --header 'Authorization: Bearer YOUR_API_KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "prompt": "Refactor the authentication module",
    "config": {
      "environment_id": "ENV_ID",
      "worker_host": "my-worker"
    }
  }'
```

--------------------------------

### Route Runs to Self-Hosted Worker via Integrations

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Configures integrations to route tasks to a self-hosted worker. When creating or updating an integration, the `--host` flag specifies the worker ID. All tasks initiated through this integration will then be processed by the designated worker.

```bash
oz integration create slack --host "my-worker" ...
oz integration update linear --host "my-worker" ...
```

--------------------------------

### AgentListSource Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the metadata for a source repository where a skill variant is located.

```APIDOC
## AgentListSource Object

### Description
Source repository metadata identifying where a skill variant is defined.

### Properties
- **owner** (string) - Required - GitHub repository owner
- **name** (string) - Required - GitHub repository name
- **skill_path** (string) - Required - Path to the skill definition file within the repository
```

--------------------------------

### POST /api/v1/schedules

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Creates a new scheduled agent that runs on a cron schedule. The agent will be triggered automatically based on the cron expression. Either a prompt or agent_config.skill_spec is required.

```APIDOC
## Create a scheduled agent

### Description
Creates a new scheduled agent that runs on a cron schedule. The agent will be triggered automatically based on the cron expression. Either a prompt or agent_config.skill_spec is required.

### Method
POST

### Endpoint
/api/v1/schedules

### Parameters
#### Request Body
- **name** (string) - Required - Human-readable name for the schedule
- **cron_schedule** (string) - Required - Cron expression defining when the agent runs (e.g., "0 9 * * *" for daily at 9am UTC)
- **prompt** (string) - Optional - The prompt/instruction for the agent to execute. Required unless agent_config.skill_spec is provided.
- **enabled** (boolean) - Optional - Whether the schedule should be active immediately (default: true)
- **agent_config** (object) - Optional - Per-run configuration for a cloud agent.
  - **name** (string) - Optional - Human-readable label for grouping, filtering, and traceability.
  - **model_id** (string) - Optional - LLM model to use (uses team default if not specified)
  - **base_prompt** (string) - Optional - Custom base prompt for the agent
  - **environment_id** (string) - Optional - UID of the environment to run the agent in
  - **skill_spec** (string) - Optional - Skill specification identifying which agent skill to use. Format: "{owner}/{repo}:{skill_path}"
  - **computer_use_enabled** (boolean) - Optional - Controls whether computer use is enabled for this agent (default: false)
  - **worker_host** (string) - Optional - Self-hosted worker ID that should execute this task.
- **team** (boolean) - Optional - Whether to create a team-owned schedule. (Defaults to true for users on a single team.)

### Request Example
```json
{
  "name": "Daily Report Generator",
  "cron_schedule": "0 8 * * *",
  "prompt": "Generate a daily summary report.",
  "enabled": true,
  "agent_config": {
    "model_id": "claude-3-opus-20240229",
    "skill_spec": "warpdotdev/warp-server:.claude/skills/report/SKILL.md"
  }
}
```

### Response
#### Success Response (200)
- **id** (string) - Unique identifier for the scheduled agent
- **name** (string) - Human-readable name for the schedule
- **cron_schedule** (string) - Cron expression defining when the agent runs
- **enabled** (boolean) - Whether the schedule is currently active
- **prompt** (string) - The prompt/instruction for the agent to execute
- **created_at** (string) - Timestamp of creation
- **updated_at** (string) - Timestamp of last update

#### Response Example
```json
{
  "id": "sch_12345abcde",
  "name": "Daily Report Generator",
  "cron_schedule": "0 8 * * *",
  "enabled": true,
  "prompt": "Generate a daily summary report.",
  "created_at": "2024-01-01T10:00:00Z",
  "updated_at": "2024-01-01T10:00:00Z"
}
```
```

--------------------------------

### API Route Dynamic Rendering in Astro

Source: https://docs.warp.dev/university/developer-workflows/beginner/how-to-create-project-rules-for-an-existing-project-astro-%2B-typescript-%2B-tailwind

This code demonstrates how to configure an API route in Astro to be dynamically rendered on Vercel. By setting `prerender` to `false`, the route will not be pre-rendered at build time, allowing for dynamic content generation.

```javascript
export const prerender = false;
```

--------------------------------

### Configure Linear SSE MCP Server

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This JSON configuration defines a Linear SSE (Server-Sent Events) based MCP server using a provided URL. This is for remote or locally hosted MCP endpoints.

```json
{
  "Linear": {
    "url": "https://mcp.linear.app/sse"
  }
}
```

--------------------------------

### Create Theme Directory (Windows)

Source: https://docs.warp.dev/terminal/appearance/custom-themes

Creates the directory for custom themes within the Warp application data path on Windows. This step is essential for Warp to recognize user-defined themes.

```powershell
New-Item -Path "$env:APPDATA\warp\Warp\data\themes\" -ItemType Directory
```

--------------------------------

### Ambient Agent Configuration

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines per-run configuration for a cloud agent, including model, skill, and environment settings.

```APIDOC
## Ambient Agent Configuration

### Description
Per-run configuration for a cloud agent. Controls which LLM model is used, which skill (SKILL.md) drives the agent's instructions, which environment the agent executes in, any MCP servers to enable, and optional base prompt overrides. All fields are optional; when omitted, the agent uses the system default for each setting.

### Object: AmbientAgentConfig

- **name** (string) - Human-readable label for grouping, filtering, and traceability. Automatically set to the skill name when running a skill-based agent. Set this explicitly to categorize runs by intent (e.g., "nightly-dependency-check") so you can filter and track them via the name query parameter on GET /agent/runs.
- **model_id** (string) - LLM model to use (uses team default if not specified)
- **base_prompt** (string) - Custom base prompt for the agent
- **environment_id** (string) - UID of the environment to run the agent in
- **skill_spec** (string) - Skill specification identifying which agent skill to use. Format: "{owner}/{repo}:{skill_path}" Example: "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md". Use the list agents endpoint to discover available skills.
- **mcp_servers** (object) - Map of MCP server configurations by name. See MCPServerConfig for details.
- **computer_use_enabled** (boolean) - Controls whether computer use is enabled for this agent. If not set, defaults to false.
- **worker_host** (string) - Self-hosted worker ID that should execute this task. If not specified or set to "warp", the task runs on Warp-hosted workers.

```

--------------------------------

### Run Warp Agent Remotely in Cloud

Source: https://docs.warp.dev/reference/cli/cli

Dispatches tasks to remote cloud environments for background processing, standardized configurations, and remote execution. Requires an environment ID and a prompt. Options include --open to view the session and --name for traceability.

```sh
oz agent run-cloud \
  --environment <ENVIRONMENT_ID> \
  --name "Repo summary" \
  --prompt "Summarize this repo and list the top 5 risky areas" \
  --open
```

--------------------------------

### Agent Configuration Schemas

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Definitions for configuring agent runs, including model selection, environment settings, and MCP server integration.

```APIDOC
## AmbientAgentConfig

### Description
Per-run configuration for a cloud agent. Controls LLM model, environment, and skill specifications.

### Request Body
- **name** (string) - Optional - Human-readable label for grouping and filtering.
- **model_id** (string) - Optional - LLM model ID.
- **base_prompt** (string) - Optional - Custom base prompt for the agent.
- **environment_id** (string) - Optional - UID of the execution environment.
- **skill_spec** (string) - Optional - Skill specification path (e.g., "owner/repo:path").
- **mcp_servers** (object) - Optional - Map of MCP server configurations.
- **computer_use_enabled** (boolean) - Optional - Enables computer use capabilities.
- **worker_host** (string) - Optional - Specific worker host ID for execution.

### Request Example
{
  "name": "my-agent-run",
  "model_id": "claude-3-5-sonnet",
  "skill_spec": "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md"
}
```

--------------------------------

### Warp Commands Configuration

Source: https://docs.warp.dev/terminal/sessions/launch-configurations

Defines commands to be executed when a launch configuration is run in Warp. Commands can be specified per pane or per tab. Supports chaining commands with `&&`.

```yaml
# Warp Launch Configuration
#
# This configuration has two windows,
# the first window executes two commands on start,
# the second window has a split pane that executes a command on start.

---
name: Example Commands
windows:
  - tabs:
      - title: Documents
        layout:
          cwd: /Users/warp-user/Documents
          commands:
            - exec: ls
            - exec: code .
        color: blue
  - tabs:
      - title: Downloads
        layout:
          split_direction: vertical
          panes:
            - cwd: /Users/warp-user/Downloads
              commands:
                - exec: curl http://example.com -o my.file
                - exec: cp my.file my.file2
            - cwd: /Users/warp-user
              commands:
                - exec: ssh user@remote.server.com
        color: green
```

--------------------------------

### AgentSkill Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Information about the agent skill used for a run.

```APIDOC
## AgentSkill Object

### Description
Information about the agent skill used for the run. Either `full_path` or `bundled_skill_id` will be set, but not both.

### Properties
- **name** (string) - Optional - Human-readable name of the skill
- **description** (string) - Optional - Description of the skill
- **full_path** (string) - Optional - Path to the SKILL.md file (for file-based skills)
- **bundled_skill_id** (string) - Optional - Unique identifier for bundled skills
```

--------------------------------

### AgentListSource Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Contains metadata about the source repository where an agent variant is defined.

```APIDOC
## AgentListSource Object

### Description
Source repository metadata identifying where a skill variant is defined.

### Schema
```json
{
  "owner": "string",
  "name": "string",
  "skill_path": "string"
}
```

### Properties
- **owner** (string) - Required - GitHub repository owner
- **name** (string) - Required - GitHub repository name
- **skill_path** (string) - Required - Path to the skill definition file within the repository
```

--------------------------------

### RequestUsage Object

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Resource usage information for a run.

```APIDOC
## RequestUsage Object

### Description
Resource usage information for the run.

### Properties
- **inference_cost** (number, double) - Cost of LLM inference for the run.
- **compute_cost** (number, double) - Cost of compute resources for the run.
```

--------------------------------

### AmbientAgentConfig Schema Details (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the per-run configuration for a cloud agent, including model ID, base prompt, environment, and skill specifications. It allows for customization of agent behavior and execution environment.

```json
{
  "AmbientAgentConfig": {
    "type": "object",
    "description": "Per-run configuration for a cloud agent. Controls which LLM model is used,\nwhich skill (SKILL.md) drives the agent's instructions, which environment\nthe agent executes in, any MCP servers to enable, and optional base prompt\noverrides. All fields are optional; when omitted, the agent uses the system\ndefault for each setting.\n",
    "properties": {
      "name": {
        "type": "string",
        "description": "Human-readable label for grouping, filtering, and traceability.\nAutomatically set to the skill name when running a skill-based agent.\nSet this explicitly to categorize runs by intent (e.g., \"nightly-dependency-check\")\nso you can filter and track them via the name query parameter on GET /agent/runs.\n"
      },
      "model_id": {
        "type": "string",
        "description": "LLM model to use (uses team default if not specified)"
      },
      "base_prompt": {
        "type": "string",
        "description": "Custom base prompt for the agent"
      },
      "environment_id": {
        "type": "string",
        "description": "UID of the environment to run the agent in"
      },
      "skill_spec": {
        "type": "string",
        "description": "Skill specification identifying which agent skill to use.\nFormat: \"{owner}/{repo}:{skill_path}\"\nExample: \"warpdotdev/warp-server:.claude/skills/deploy/SKILL.md\"\nUse the list agents endpoint to discover available skills.\n"
      },
      "mcp_servers": {
        "type": "object",
        "additionalProperties": {
          "$ref": "#/components/schemas/MCPServerConfig"
        },
        "description": "Map of MCP server configurations by name"
      },
      "computer_use_enabled": {
        "type": "boolean",
        "description": "Controls whether computer use is enabled for this agent.\nIf not set, defaults to false.\n"
      },
      "worker_host": {
        "type": "string",
        "description": "Self-hosted worker ID that should execute this task.\nIf not specified or set to \"warp\", the task runs on Warp-hosted workers.\n"
      }
    }
  }
}
```

--------------------------------

### Run Object Details

Source: https://docs.warp.dev/reference/api-and-sdk/models

This section details the structure and properties of the Run object, which represents an execution instance within the Warp system.

```APIDOC
## Run Object Details

### Description
Provides detailed information about a specific run, including its status, source, creator, usage, and configuration.

### Method
GET

### Endpoint
`/websites/warp_dev/runs/{run_id}`

### Parameters
#### Path Parameters
- **run_id** (string) - Required - The unique identifier of the run.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **id** (string) - Unique identifier for the run.
- **status** (string) - Current status of the run (e.g., PENDING, RUNNING, SUCCEEDED, FAILED).
- **source** (RunSourceType) - Source that created the run.
- **created_at** (string) - Timestamp when the run was created.
- **completed_at** (string) - Timestamp when the run was completed.
- **run_source_type** (RunSourceType) - Enum: [LINEAR, API, SLACK, LOCAL, SCHEDULED_AGENT, WEB_APP, GITHUB_ACTION, CLOUD_MODE, CLI]
- **schedule_info** (ScheduleInfo) - Metadata about the scheduled agent that triggered this run.
- **creator_info** (RunCreatorInfo) - Identity information about the principal that created the run.
- **usage** (RequestUsage) - Resource usage information for the run.
- **ambient_agent_config** (AmbientAgentConfig) - Per-run configuration for a cloud agent.
- **error** (object) - Error details if the run failed.
  - **type** (string) - Type of the error.
  - **message** (string) - Description of the error.
  - **details** (object) - Additional error details.

#### Response Example
```json
{
  "id": "run_abc123",
  "status": "SUCCEEDED",
  "source": "API",
  "created_at": "2023-10-27T10:00:00Z",
  "completed_at": "2023-10-27T10:05:00Z",
  "run_source_type": "API",
  "schedule_info": null,
  "creator_info": {
    "type": "user",
    "uid": "user_xyz789",
    "display_name": "Jane Doe",
    "email": "jane.doe@example.com",
    "photo_url": "https://example.com/photos/jane.doe.jpg"
  },
  "usage": {
    "inference_cost": 0.05,
    "compute_cost": 0.10
  },
  "ambient_agent_config": {
    "name": "My Custom Run",
    "model_id": "gpt-4",
    "base_prompt": "You are a helpful assistant.",
    "environment_id": "env_def456",
    "skill_spec": "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md",
    "mcp_servers": {},
    "computer_use_enabled": true,
    "worker_host": "warp"
  },
  "error": null
}
```

### Error Handling
- **insufficient_credits**: The user account lacks sufficient credits to perform the action.
- **feature_not_available**: The requested feature is not available.
- **external_authentication_required**: External authentication is required to proceed.
- **not_authorized**: The user is not authorized to perform this action.
- **invalid_request**: The request is malformed or invalid.
- **resource_not_found**: The requested resource could not be found.
- **budget_exceeded**: The user has exceeded their budget.
- **integration_disabled**: The integration used for this action is disabled.
- **integration_not_configured**: The integration is not configured correctly.
- **operation_not_supported**: The requested operation is not supported.
- **environment_setup_failed**: Failed to set up the execution environment.
- **content_policy_violation**: The request violates content policies.
- **conflict**: A conflict occurred, possibly due to concurrent modifications.
- **authentication_required**: Authentication is required to access this resource.
- **resource_unavailable**: The requested resource is temporarily unavailable.
- **internal_error**: An unexpected internal server error occurred.
```

--------------------------------

### Configure Agent Skills via API

Source: https://docs.warp.dev/agent-platform/cloud-agents/skills-as-agents

JSON payload structure for initiating an agent run via the Oz API. It requires a prompt and a configuration object containing the environment ID and skill specification.

```json
{
  "prompt": "additional context for this run",
  "config": {
    "environment_id": "<ENV_ID>",
    "skill_spec": "owner/repo:skill-name"
  }
}
```

--------------------------------

### Ambient Agent Config Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Configuration for a cloud agent's execution.

```APIDOC
## Ambient Agent Config Object

### Description
Per-run configuration for a cloud agent. Controls which LLM model is used, which skill (SKILL.md) drives the agent's instructions, which environment the agent executes in, any MCP servers to enable, and optional base prompt overrides. All fields are optional; when omitted, the agent uses the system default for each setting.

### Properties
- **name** (string) - Human-readable label for grouping, filtering, and traceability. Automatically set to the skill name when running a skill-based agent. Set this explicitly to categorize runs by intent (e.g., "nightly-dependency-check") so you can filter and track them via the name query parameter on GET /agent/runs.
- **model_id** (string) - LLM model to use (uses team default if not specified).
- **base_prompt** (string) - Custom base prompt for the agent.
- **environment_id** (string) - UID of the environment to run the agent in.
- **skill_spec** (string) - Skill specification identifying which agent skill to use. Format: "{owner}/{repo}:{skill_path}". Example: "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md". Use the list agents endpoint to discover available skills.
- **mcp_servers** (object) - Map of MCP server configurations by name. See `MCPServerConfig`.
- **computer_use_enabled** (boolean) - Controls whether computer use is enabled for this agent. If not set, defaults to false.
- **worker_host** (string) - Self-hosted worker ID that should execute this task. If not specified or set to "warp", the task runs on Warp-hosted workers.
```

--------------------------------

### ListAgentsResponse Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Describes the structure of the response when listing available agents. It includes a list of agents, each with its name and available variants.

```APIDOC
## ListAgentsResponse Object

### Description
Response containing available skills discoverable from the authenticated user's environments or a specific repository.

### Schema
```json
{
  "agents": [
    {
      "$ref": "#/components/schemas/AgentListItem"
    }
  ]
}
```

### Properties
- **agents** (array[AgentListItem]) - Required - List of available agents
```

--------------------------------

### Create Scheduled Agent Request Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for creating a new scheduled agent. It includes details like name, schedule, prompt, and agent configuration.

```APIDOC
## CreateScheduledAgentRequest Object

### Description
Request body for creating a new scheduled agent. Either `prompt` or `agent_config.skill_spec` is required.

### Properties

*   **name** (string) - Required - Human-readable name for the schedule.
*   **cron_schedule** (string) - Required - Cron expression defining when the agent runs (e.g., "0 9 * * *" for daily at 9am UTC).
*   **prompt** (string) - Optional - The prompt/instruction for the agent to execute. Required unless `agent_config.skill_spec` is provided.
*   **enabled** (boolean) - Optional - Whether the schedule should be active immediately. Defaults to `true`.
*   **agent_config** (object) - Optional - Per-run configuration for a cloud agent. Controls LLM model, skill, environment, MCP servers, and base prompt overrides. All fields within `agent_config` are optional; when omitted, the agent uses the system default for each setting.
    *   **name** (string) - Optional - Human-readable label for grouping, filtering, and traceability. Automatically set to the skill name when running a skill-based agent. Set this explicitly to categorize runs by intent (e.g., "nightly-dependency-check") so you can filter and track them via the name query parameter on GET /agent/runs.
    *   **model_id** (string) - Optional - LLM model to use (uses team default if not specified).
    *   **base_prompt** (string) - Optional - Custom base prompt for the agent.
    *   **environment_id** (string) - Optional - UID of the environment to run the agent in.
    *   **skill_spec** (string) - Optional - Skill specification identifying which agent skill to use. Format: "{owner}/{repo}:{skill_path}". Example: "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md". Use the list agents endpoint to discover available skills.
    *   **mcp_servers** (object) - Optional - Map of MCP server configurations by name.
        *   **[server_name]** (object) - Configuration for a single MCP (Model Context Protocol) server to attach to an agent run. Exactly one of `warp_id`, `command`, or `url` must be provided, corresponding to the three supported transports:
            *   `warp_id`: reference a Warp-managed shared MCP server by UUID.
            *   `command` + `args`: launch a local stdio-based MCP server process.
            *   `url`: connect to a remote SSE or HTTP MCP server.
            *   **warp_id** (string) - Optional - Reference to a Warp shared MCP server by UUID.
            *   **command** (string) - Optional - Stdio transport - command to run.
            *   **args** (array of strings) - Optional - Stdio transport - command arguments.
            *   **url** (string) - Optional - SSE/HTTP transport - server URL.
            *   **env** (object of strings) - Optional - Environment variables for the server.
            *   **headers** (object of strings) - Optional - HTTP headers for SSE/HTTP transport.
    *   **computer_use_enabled** (boolean) - Optional - Controls whether computer use is enabled for this agent. Defaults to `false`.
    *   **worker_host** (string) - Optional - Self-hosted worker ID that should execute this task. If not specified or set to "warp", the task runs on Warp-hosted workers.
*   **team** (boolean) - Optional - Whether to create a team-owned schedule. Defaults to `true` for users on a single team.

### Request Example
```json
{
  "name": "Daily Report Generator",
  "cron_schedule": "0 8 * * *",
  "prompt": "Generate a daily summary report.",
  "enabled": true,
  "agent_config": {
    "model_id": "claude-3-opus-20240229",
    "environment_id": "env_abc123",
    "skill_spec": "warpdotdev/warp-server:.claude/skills/reporting/SKILL.md"
  },
  "team": true
}
```

### Success Response (200)
*   **[Response fields will be documented here based on the API's actual success response structure]**

### Response Example
```json
{
  "message": "Scheduled agent created successfully.",
  "agent_id": "agent_xyz789"
}
```
```

--------------------------------

### AgentListVariant Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Details a specific agent variant, identified by its skill path. Includes instructions, source metadata, and available environments.

```APIDOC
## AgentListVariant Object

### Description
A specific skill variant, uniquely identified by its skill path in a repository. Each variant carries its own instructions (base_prompt), source repository metadata, and the list of environments it is available in.

### Schema
```json
{
  "id": "string",
  "description": "string",
  "base_prompt": "string",
  "source": {
    "$ref": "#/components/schemas/AgentListSource"
  },
  "environments": [
    {
      "$ref": "#/components/schemas/AgentListEnvironment"
    }
  ],
  "last_run_timestamp": "string (date-time)",
  "error": "string"
}
```

### Properties
- **id** (string) - Required - Stable identifier for this skill variant. Format: "{owner}/{repo}:{skill_path}". Example: "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md"
- **description** (string) - Required - Description of the agent variant
- **base_prompt** (string) - Required - Base prompt/instructions for the agent
- **source** (AgentListSource) - Required - Source repository metadata
- **environments** (array[AgentListEnvironment]) - Required - Environments where this agent variant is available
- **last_run_timestamp** (string) - Optional - Timestamp of the last time this skill was run (RFC3339)
- **error** (string) - Optional - Non-empty when the skill's SKILL.md file exists but is malformed. Contains a description of the parse failure. Only present when include_malformed_skills=true is passed to the list agents endpoint.
```

--------------------------------

### Route Runs to Self-Hosted Worker via CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Executes a cloud agent run and directs it to a specific self-hosted worker using the `--host` flag. This flag must exactly match the `--worker-id` of the target worker. It can be combined with other `run-cloud` flags.

```bash
oz agent run-cloud --prompt "Refactor the authentication module" --host "my-worker"
```

--------------------------------

### Set environment variables for remote MCP servers

Source: https://docs.warp.dev/reference/cli/mcp-servers

Demonstrates how to manually export required secrets in the shell environment before executing an agent on a remote machine.

```shell
export MY_MCP_SERVER_ACCESS_TOKEN="..."
oz agent run --mcp "904a8936-fa82-4571-b1d6-166c26197981" --prompt "use my MCP server to check for errors"
```

--------------------------------

### PlanArtifact Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Represents a PLAN artifact generated by an agent run, containing a reference to the plan document.

```APIDOC
## PlanArtifact Schema

### Description
An artifact of type PLAN produced by an agent run. Contains a reference to
a plan document created by the agent, identified by `document_uid`.

### Properties
- **artifact_type** (string) - Required - Identifies this artifact as a plan (enum: PLAN).
- **created_at** (string) - Required - Timestamp when the artifact was created (RFC3339).
- **data** (object) - Required - Data payload for a PLAN artifact.
  - **document_uid** (string) - Required - Unique identifier for the plan document.
  - **notebook_uid** (string) - Optional - Unique identifier for the associated notebook.
  - **title** (string) - Optional - Title of the plan.
```

--------------------------------

### Configure Sentry SSE MCP Server

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This JSON configuration defines a Sentry SSE (Server-Sent Events) based MCP server using a provided URL. This is used for remote or locally hosted MCP endpoints.

```json
{
  "Sentry": {
    "url": "https://mcp.sentry.dev/sse"
  }
}
```

--------------------------------

### Run Statuses and Error Codes

Source: https://docs.warp.dev/reference/api-and-sdk/models

This section details the possible statuses for a run, including success, failure, and various error conditions.

```APIDOC
## Run Statuses and Error Codes

### Description
This section outlines the various statuses a run can have, including successful completion and different types of errors that may occur.

### Enum: RunStatus

Possible values for the status of a run:

- `SUCCESS` - The run completed successfully.
- `FAILURE` - The run failed to complete.
- `RUNNING` - The run is currently in progress.
- `PENDING` - The run is waiting to be started.
- `CANCELLED` - The run was cancelled.

### Enum: WarpError

Specific error codes that can occur during a run:

- `insufficient_credits` - Not enough credits to perform the operation.
- `feature_not_available` - The requested feature is not available.
- `external_authentication_required` - Authentication with an external service is required.
- `not_authorized` - The user is not authorized to perform the action.
- `invalid_request` - The request was invalid.
- `resource_not_found` - The requested resource was not found.
- `budget_exceeded` - The budget for the operation has been exceeded.
- `integration_disabled` - The integration is disabled.
- `integration_not_configured` - The integration is not configured.
- `operation_not_supported` - The operation is not supported.
- `environment_setup_failed` - Failed to set up the environment.
- `content_policy_violation` - Prompt or setup commands violated content policy.
- `conflict` - Request conflicts with the current state of the resource.
- `authentication_required` - Request lacks valid authentication credentials.
- `resource_unavailable` - Transient infrastructure issue (retryable).
- `internal_error` - Unexpected server-side error (retryable).

```

--------------------------------

### Schedule Information

Source: https://docs.warp.dev/reference/api-and-sdk/models

Provides metadata for runs initiated by scheduled agents.

```APIDOC
## Schedule Information

### Description
Metadata about the scheduled agent that triggered this run. Only present on runs where source is `SCHEDULED_AGENT`. Contains the schedule ID, its name, and the cron expression as they were configured at the time the run was created.

### Object: ScheduleInfo

- **schedule_id** (string) - Unique identifier for the schedule
- **schedule_name** (string) - Name of the schedule at the time the run was created
- **cron_schedule** (string) - Cron expression at the time the run was created

```

--------------------------------

### Agent Configuration Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Details the structure of the AmbientAgentConfig object, used for configuring agent runs.

```APIDOC
## AmbientAgentConfig Object

### Description
Configuration for a cloud agent run, allowing customization of the LLM model, skill, environment, and more.

### Properties
- **name** (string) - Human-readable label for grouping and filtering runs. Automatically set to the skill name when running a skill-based agent. Can be set explicitly to categorize runs (e.g., "nightly-dependency-check").
- **model_id** (string) - LLM model to use. Uses the team default if not specified.
- **base_prompt** (string) - Custom base prompt for the agent.
- **environment_id** (string) - UID of the environment to run the agent in.
- **skill_spec** (string) - Skill specification identifying which agent skill to use. Format: "{owner}/{repo}:{skill_path}". Example: "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md". Use the list agents endpoint to discover available skills.
- **mcp_servers** (object) - Map of MCP server configurations by name. Additional properties are of type MCPServerConfig.
- **computer_use_enabled** (boolean) - Controls whether computer use is enabled for this agent. Defaults to false if not set.
- **worker_host** (string) - Self-hosted worker ID that should execute this task. If not specified or set to "warp", the task runs on Warp-hosted workers.

### Example
```json
{
  "name": "Nightly Dependency Check",
  "model_id": "claude-3-opus-20240229",
  "environment_id": "env_prod_us_east_1",
  "skill_spec": "myorg/myrepo:skills/dependency_check.md",
  "computer_use_enabled": true
}
```
```

--------------------------------

### AgentSkill Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Provides information about the agent skill used for a run.

```APIDOC
## AgentSkill Schema

### Description
Information about the agent skill used for the run.
Either `full_path` or `bundled_skill_id` will be set, but not both.

### Properties
- **name** (string) - Optional - Human-readable name of the skill.
- **description** (string) - Optional - Description of the skill.
- **full_path** (string) - Optional - Path to the SKILL.md file (for file-based skills).
- **bundled_skill_id** (string) - Optional - Unique identifier for bundled skills.
```

--------------------------------

### AmbientAgentConfig Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Configuration schema for defining agent behavior, including model selection, skill specifications, and MCP server integrations.

```APIDOC
## AmbientAgentConfig

### Description
Per-run configuration for a cloud agent. Controls LLM model, skill instructions, environment, and MCP server connectivity.

### Properties
- **name** (string) - Optional - Label for filtering/traceability.
- **model_id** (string) - Optional - LLM model identifier.
- **base_prompt** (string) - Optional - Custom system prompt.
- **environment_id** (string) - Optional - UID of the execution environment.
- **skill_spec** (string) - Optional - Path to skill file (e.g., "owner/repo:path").
- **mcp_servers** (object) - Optional - Map of MCP server configurations.
- **computer_use_enabled** (boolean) - Optional - Enable computer use capabilities.
- **worker_host** (string) - Optional - Specific worker ID or "warp".

### MCPServerConfig
- **warp_id** (string) - Optional - Reference to a managed MCP server.
- **command** (string) - Optional - Stdio command.
- **args** (array) - Optional - Command arguments.
- **url** (string) - Optional - Remote SSE/HTTP URL.
- **env** (object) - Optional - Environment variables.
- **headers** (object) - Optional - HTTP headers.
```

--------------------------------

### Copy Custom Theme File

Source: https://docs.warp.dev/terminal/appearance/custom-themes

Copies a user-created custom theme YAML file to the designated themes directory. This makes the new theme available for selection within Warp Terminal.

```bash
cp ~/Downloads/my_awesome_theme.yaml {{path_to_your_themes_directory_from_step1}}
```

--------------------------------

### Skill without Argument Placeholders (Markdown)

Source: https://docs.warp.dev/agent-platform/capabilities/skills

Illustrates a simple skill defined in Markdown that does not use any argument placeholders. When invoked with extra text, this text is passed as a separate user message to the agent.

```markdown
---
name: greet
description: Greet the user with an Australian-style hello
---

# Greet

Greet the user warmly in an Australian style.

```

--------------------------------

### Run an agent task (preferred)

Source: https://docs.warp.dev/reference/api-and-sdk/agent

This endpoint is an alias for POST /agent/run and is the preferred method for creating new agent runs. Its behavior is identical to POST /agent/run.

```APIDOC
## POST /agent/run

### Description
Creates a new agent run. This is the preferred endpoint for creating new agent runs.

### Method
POST

### Endpoint
/agent/run

### Parameters
#### Request Body
- **prompt** (string) - Required/Optional - The prompt/instruction for the agent to execute. Required unless a skill is specified via the skill field or config.skill_spec.
- **skill** (string) - Required/Optional - Skill specification to use as the base prompt for the agent. Supported formats: "repo:skill_name", "repo:skill_path", "org/repo:skill_name", "org/repo:skill_path". When provided, this takes precedence over config.skill_spec.
- **config** (object) - Required/Optional - Per-run configuration for a cloud agent. Controls which LLM model is used, which skill (SKILL.md) drives the agent's instructions, which environment the agent executes in, any MCP servers to enable, and optional base prompt overrides. All fields are optional; when omitted, the agent uses the system default for each setting.
- **title** (string) - Required/Optional - Custom title for the run (auto-generated if not provided).
- **team** (boolean) - Required/Optional - Whether to create a team-owned run. Defaults to true for users on a single team.
- **conversation_id** (string) - Required/Optional - Optional conversation ID to continue an existing conversation. If provided, the agent will continue from where the previous run left off.
- **attachments** (array) - Required/Optional - Optional file attachments to include with the prompt (max 5). Attachments are uploaded to cloud storage and made available to the agent.
- **interactive** (boolean) - Required/Optional - Whether the run should be interactive. If not set, defaults to false.

### Request Example
```json
{
  "prompt": "Write a short story about a robot learning to love.",
  "config": {
    "model_id": "claude-3-opus-20240229",
    "skill_spec": "warpdotdev/warp-server:examples/skills/story_generator/SKILL.md"
  },
  "title": "Robot Love Story Generation"
}
```

### Response
#### Success Response (200)
- **run_id** (string) - The unique identifier for the agent run.
- **status** (string) - The current status of the agent run (e.g., "pending", "running", "completed", "failed").
- **created_at** (string) - The timestamp when the agent run was created.

#### Response Example
```json
{
  "run_id": "run-12345abcde",
  "status": "pending",
  "created_at": "2024-07-26T10:00:00Z"
}
```
```

--------------------------------

### Set Environment Variable for Remote MCP Server

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

Shows how to set environment variables, such as access tokens, on a remote machine before running an agent that uses an MCP server. This is crucial for securely providing credentials.

```bash
export MY_MCP_SERVER_ACCESS_TOKEN="..."
$ oz agent run --mcp "904a8936-fa82-4571-b1d6-166c26197981" --prompt "use my MCP server to check for errors"
```

--------------------------------

### Define RunItem OpenAPI Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

The RunItem schema provides a comprehensive representation of an agent run. It includes metadata such as run IDs, lifecycle states, timestamps, and associated artifacts, ensuring consistent data structures for agent orchestration.

```json
{
  "type": "object",
  "description": "Full representation of a single agent run.",
  "required": ["run_id", "task_id", "title", "state", "prompt", "created_at", "updated_at"],
  "properties": {
    "run_id": { "type": "string" },
    "state": { "$ref": "#/components/schemas/RunState" },
    "prompt": { "type": "string" },
    "artifacts": {
      "type": "array",
      "items": { "$ref": "#/components/schemas/ArtifactItem" }
    }
  }
}
```

--------------------------------

### Using the --mcp flag

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

The --mcp flag allows you to connect agents to external tools by providing MCP server configurations. It accepts UUIDs, inline JSON, or file paths.

```APIDOC
## Using the `--mcp` flag

The `--mcp` flag accepts three formats:
  * **UUID** — reference a Warp-shared MCP server by its UUID (find UUIDs with `oz mcp list`)
  * **Inline JSON** — pass a full MCP JSON configuration directly as a string
  * **File path** — path to a JSON file containing the MCP configuration

You can repeat `--mcp` to include multiple servers.
```

--------------------------------

### Enable Computer Use via API

Source: https://docs.warp.dev/agent-platform/capabilities/computer-use

Configure Computer Use for agent runs by including the computer_use_enabled boolean field in the JSON request payload.

```json
{
  "prompt": "Build a button component that matches this design, then test it in the browser",
  "computer_use_enabled": true,
  "environment_id": "optional-environment-id"
}
```

--------------------------------

### GitHubRepo Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for identifying a GitHub repository by owner and name.

```APIDOC
## GitHubRepo Object

### Description
A GitHub repository identified by owner and repository name, used to specify repositories to clone into a cloud environment.

### Properties
- **owner** (string) - Required - GitHub repository owner (user or organization)
- **repo** (string) - Required - GitHub repository name

### Example
{
  "owner": "octocat",
  "repo": "hello-world"
}
```

--------------------------------

### Define MCPServerConfig Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

MCPServerConfig manages the connection to Model Context Protocol servers. It supports three transport methods: Warp-managed IDs, local stdio commands, or remote SSE/HTTP URLs.

```json
{
  "type": "object",
  "properties": {
    "warp_id": { "type": "string" },
    "command": { "type": "string" },
    "args": { "type": "array", "items": { "type": "string" } },
    "url": { "type": "string", "format": "uri" },
    "env": { "type": "object" },
    "headers": { "type": "object" }
  }
}
```

--------------------------------

### Execute Agent Skills via CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/skills-as-agents

Commands for running agent skills locally or in the cloud using the Oz CLI. The local command uses the --skill flag, while the cloud command requires an environment ID.

```bash
# Run locally with a skill
oz agent run --skill "owner/repo:skill-name" --prompt "additional context"

# Run in the cloud with a skill
oz agent run-cloud \
  --environment <ENV_ID> \
  --skill "owner/repo:skill-name" \
  --prompt "additional context"
```

--------------------------------

### Creating and Managing Git Worktrees

Source: https://docs.warp.dev/code/git-worktrees

This snippet demonstrates essential Git commands for managing worktrees. It covers creating new worktrees for existing or new branches, listing all available worktrees, and removing worktrees when they are no longer needed. These commands are executed from the terminal within a Git repository.

```bash
# Create a worktree for an existing branch
git worktree add ../my-feature feature-branch

# Create a worktree with a new branch
git worktree add -b new-branch ../new-branch main

# List all worktrees
git worktree list

# Remove a worktree when done
git worktree remove ../my-feature
```

--------------------------------

### Configure Linear MCP Server

Source: https://docs.warp.dev/knowledge-and-collaboration/rules

Configures Linear issue tracking integration via npx CLI or SSE URL. Enables project management capabilities within the terminal.

```json
{
  "Linear": {
    "command": "npx",
    "args": ["-y","mcp-remote","https://mcp.linear.app/sse"]
  }
}
```

```json
{
  "Linear": {
    "url": "https://mcp.linear.app/sse"
  }
}
```

--------------------------------

### RunState and RunSourceType Enums

Source: https://docs.warp.dev/reference/api-and-sdk/models

Definitions for the lifecycle states of a run and the various sources that can trigger an agent run.

```APIDOC
## RunState

### Description
Represents the current lifecycle state of an agent run.

### Values
- **QUEUED**: Run is waiting to be picked up
- **PENDING**: Run is being prepared
- **CLAIMED**: Run has been claimed by a worker
- **INPROGRESS**: Run is actively being executed
- **SUCCEEDED**: Run completed successfully
- **FAILED**: Run failed
- **BLOCKED**: Run is blocked (e.g., awaiting user input)
- **ERROR**: Run encountered an error
- **CANCELLED**: Run was cancelled by user

## RunSourceType

### Description
Indicates the origin or trigger mechanism for an agent run.

### Values
- **LINEAR, API, SLACK, LOCAL, SCHEDULED_AGENT, WEB_APP, GITHUB_ACTION, CLOUD_MODE, CLI**
```

--------------------------------

### Combining multiple servers

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

The `--mcp` flag can be used multiple times in a single command to combine different MCP server configurations (UUIDs, inline JSON, file paths).

```APIDOC
## Combining multiple servers

Pass `--mcp` multiple times to combine UUID references, inline JSON, and file-based configs in a single run:

```
$ oz agent run \
  --mcp "1deb1b14-b6e5-4996-ae99-233b7555d2d0" \
  --mcp '{"sentry": {"url": "https://mcp.sentry.dev/sse"}}' \
  --prompt "open a PR that fixes the top Sentry error"
```
```

--------------------------------

### ScreenshotArtifact Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Represents a SCREENSHOT artifact captured by an agent run, providing the artifact UID for download.

```APIDOC
## ScreenshotArtifact Schema

### Description
An artifact of type SCREENSHOT captured by an agent run. The `data` field
contains the artifact UID needed to retrieve a signed download URL via
GET /agent/artifacts/{artifactUid}.

### Properties
- **artifact_type** (string) - Required - Identifies this artifact as a screenshot (enum: SCREENSHOT).
- **created_at** (string) - Required - Timestamp when the artifact was created (RFC3339).
- **data** (object) - Required - Data payload for a SCREENSHOT artifact.
  - **artifact_uid** (string) - Required - Unique identifier for the screenshot artifact.
  - **mime_type** (string) - Required - MIME type of the screenshot image.
  - **description** (string) - Optional - Description of the screenshot.
```

--------------------------------

### AgentListEnvironment Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines an environment where an agent variant is available for execution.

```APIDOC
## AgentListEnvironment Object

### Description
An environment in which a skill variant is available and can be executed.

### Schema
```json
{
  "uid": "string",
  "name": "string"
}
```

### Properties
- **uid** (string) - Required - Unique identifier for the environment
- **name** (string) - Required - Human-readable name of the environment
```

--------------------------------

### List All Accessible Secrets with oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/secrets

Displays a list of all secrets the current user has access to, including their names, scopes, and last updated times. Secret values are never shown in the output.

```bash
oz secret list
```

--------------------------------

### Run Agent with Inline JSON MCP Server

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

Connects an agent to an external service by providing the MCP server configuration directly as an inline JSON string. This allows for quick configuration without a separate file.

```bash
$ oz agent run --mcp '{"github": {"url": "https://api.githubcopilot.com/mcp/"}}' --prompt "list open issues"
```

--------------------------------

### Integration Disabled Error

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/integration-disabled

Details about the integration_disabled error, including HTTP status, retryability, and task state.

```APIDOC
## Integration Disabled Error

### Description
The `integration_disabled` error occurs when a task targets an integration that is currently disabled in Oz settings. This can happen if an integration was previously active but has been turned off by a team admin.

### HTTP Status
`403 Forbidden`

### Retryable
No

### Task State
FAILED

### Example Response
```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/integration-disabled",
  "title": "This integration is disabled. Please enable it in Oz.",
  "status": 403,
  "instance": "/api/v1/agent/tasks",
  "error": "This integration is disabled. Please enable it in Oz.",
  "retryable": false
}
```

### Resolution
1. Navigate to the [Oz integrations page](https://oz.warp.dev/integrations).
2. Enable the integration that was disabled.
3. Retry the triggering event or task.
```

--------------------------------

### ScheduledAgentItem Schema Details (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Details the schema for a single scheduled agent, including its ID, name, cron schedule, enablement status, prompt, and timestamps. It also references other schema components for configuration and history.

```json
{
  "ScheduledAgentItem": {
    "type": "object",
    "required": [
      "id",
      "name",
      "cron_schedule",
      "enabled",
      "prompt",
      "created_at",
      "updated_at"
    ],
    "properties": {
      "id": {
        "type": "string",
        "description": "Unique identifier for the scheduled agent"
      },
      "name": {
        "type": "string",
        "description": "Human-readable name for the schedule"
      },
      "cron_schedule": {
        "type": "string",
        "description": "Cron expression defining when the agent runs (e.g., \"0 9 * * *\" for daily at 9am UTC)"
      },
      "enabled": {
        "type": "boolean",
        "description": "Whether the schedule is currently active"
      },
      "prompt": {
        "type": "string",
        "description": "The prompt/instruction for the agent to execute"
      },
      "last_spawn_error": {
        "type": "string",
        "nullable": true,
        "description": "Error message from the last failed spawn attempt, if any"
      },
      "agent_config": {
        "$ref": "#/components/schemas/AmbientAgentConfig"
      },
      "environment": {
        "allOf": [
          {
            "$ref": "#/components/schemas/CloudEnvironmentConfig"
          }
        ],
        "description": "Resolved environment configuration (if agent_config references an environment_id)"
      },
      "created_at": {
        "type": "string",
        "format": "date-time",
        "description": "Timestamp when the schedule was created (RFC3339)"
      },
      "updated_at": {
        "type": "string",
        "format": "date-time",
        "description": "Timestamp when the schedule was last updated (RFC3339)"
      },
      "created_by": {
        "$ref": "#/components/schemas/RunCreatorInfo"
      },
      "updated_by": {
        "$ref": "#/components/schemas/RunCreatorInfo"
      },
      "history": {
        "$ref": "#/components/schemas/ScheduledAgentHistoryItem"
      },
      "scope": {
        "$ref": "#/components/schemas/Scope"
      }
    }
  }
}
```

--------------------------------

### Remove Warp Preview Themes and Launch Configurations (Shell)

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/logging-out-and-uninstalling

This command removes themes and launch configurations associated with Warp Preview. It targets the XDG_STATE_HOME directory, specifically the .local/share subdirectory. This action will reset themes and launch settings to their defaults.

```shell
rm -r ${XDG_STATE_HOME:-$HOME/.local/share}/warp-terminal-preview
```

--------------------------------

### Manually Add Warp Repository on Ubuntu

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

This script manually adds the Warp package repository to an Ubuntu system, which is a workaround for update failures that can occur after OS upgrades. It involves downloading a GPG key, adding it to the keyring, and creating a sources list entry.

```bash
sudo apt-get install wget gpg
wget -qO- https://releases.warp.dev/linux/keys/warp.asc | gpg --dearmor > warpdotdev.gpg
sudo install -D -o root -g root -m 644 warpdotdev.gpg /etc/apt/keyrings/warpdotdev.gpg
sudo sh -c 'echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/warpdotdev.gpg] https://releases.warp.dev/linux/deb stable main" > /etc/apt/sources.list.d/warpdev.list'
rm warpdotdev.gpg
sudo apt update && sudo apt install warp-terminal
```

--------------------------------

### Clone Warp Themes Repository (macOS/Linux)

Source: https://docs.warp.dev/terminal/appearance/custom-themes

Clones the Warp themes repository into the appropriate directory for macOS or Linux systems. This allows users to access and manage a collection of pre-defined themes.

```bash
mkdir -p $HOME/.warp
cd $HOME/.warp/
git clone https://github.com/warpdotdev/themes.git
```

```bash
mkdir -p ${XDG_DATA_HOME:-$HOME/.local/share}/warp-terminal
cd ${XDG_DATA_HOME:-$HOME/.local/share}/warp-terminal/
git clone https://github.com/warpdotdev/themes.git
```

--------------------------------

### AmbientAgentConfig Object

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Per-run configuration for a cloud agent.

```APIDOC
## AmbientAgentConfig Object

### Description
Per-run configuration for a cloud agent. Controls which LLM model is used, which skill (SKILL.md) drives the agent's instructions, which environment the agent executes in, any MCP servers to enable, and optional base prompt overrides. All fields are optional; when omitted, the agent uses the system default for each setting.

### Properties
- **name** (string) - Human-readable label for grouping, filtering, and traceability. Automatically set to the skill name when running a skill-based agent. Set this explicitly to categorize runs by intent (e.g., "nightly-dependency-check") so you can filter and track them via the name query parameter on GET /agent/runs.
- **model_id** (string) - LLM model to use (uses team default if not specified).
- **base_prompt** (string) - Custom base prompt for the agent.
- **environment_id** (string) - UID of the environment to run the agent in.
- **skill_spec** (string) - Skill specification identifying which agent skill to use. Format: "{owner}/{repo}:{skill_path}". Example: "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md". Use the list agents endpoint to discover available skills.
- **mcp_servers** (object) - Map of MCP server configurations by name. See MCPServerConfig.
- **computer_use_enabled** (boolean) - Controls whether computer use is enabled for this agent. If not set, defaults to false.
```

--------------------------------

### List MCP Servers

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

Lists all MCP servers configured in your Warp account, including team-shared ones. This command helps you find the UUIDs of available MCP servers.

```bash
$ oz mcp list
+--------------------------------------+--------+
| UUID                                 | Name   |
+===============================================+
| 1deb1b14-b6e5-4996-ae99-233b7555d2d0 | github |
|--------------------------------------+--------|
| 65450c32-9eb1-4c57-8804-0861737acbc4 | linear |
|--------------------------------------+--------|
| d94ade64-0e73-47a6-b3ee-14e5afec3d90 | Sentry |
+--------------------------------------+
```

--------------------------------

### List Available Agents

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Retrieve a list of available agents (skills) that can be used to run tasks. Agents are discovered from environments or a specific repository.

```APIDOC
## GET /api/v1/agents

### Description
Retrieve a list of available agents (skills) that can be used to run tasks. Agents are discovered from environments or a specific repository.

### Method
GET

### Endpoint
/api/v1/agents

### Query Parameters
- **include_malformed_skills** (boolean) - Optional - If true, skills with malformed SKILL.md files will be included in the response with an error description.

### Response
#### Success Response (200)
- **agents** (array) - List of available agents. Each agent is an object with properties like `name` and `variants`.

#### Response Example
```json
{
  "agents": [
    {
      "name": "Deploy Skill",
      "variants": [
        {
          "id": "warpdotdev/warp-server:.claude/skills/deploy/SKILL.md",
          "description": "Deploys code to a specified environment.",
          "base_prompt": "You are a deployment assistant...",
          "source": {
            "owner": "warpdotdev",
            "name": "warp-server",
            "skill_path": ".claude/skills/deploy/SKILL.md"
          },
          "environments": [
            {
              "uid": "env-123",
              "name": "production"
            }
          ],
          "last_run_timestamp": "2023-10-27T10:00:00Z"
        }
      ]
    }
  ]
}
```
```

--------------------------------

### Configure Sentry MCP Server

Source: https://docs.warp.dev/knowledge-and-collaboration/rules

Configures Sentry integration using either an npx-based CLI command or a direct SSE URL. Facilitates monitoring and error tracking within the MCP environment.

```json
{
  "Sentry": {
    "command": "npx",
    "args": ["-y","mcp-remote@latest","https://mcp.sentry.dev/mcp"]
  }
}
```

```json
{
  "Sentry": {
    "url": "https://mcp.sentry.dev/sse"
  }
}
```

--------------------------------

### Define ScheduledAgentItem and AmbientAgentConfig Schemas

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the JSON schema for scheduled agents, including their execution schedule, environment settings, and MCP server configurations.

```json
{
  "ScheduledAgentItem": {
    "type": "object",
    "required": ["id", "name", "cron_schedule", "enabled", "prompt", "created_at", "updated_at"],
    "properties": {
      "id": { "type": "string" },
      "name": { "type": "string" },
      "cron_schedule": { "type": "string" },
      "enabled": { "type": "boolean" },
      "prompt": { "type": "string" },
      "agent_config": { "$ref": "#/components/schemas/AmbientAgentConfig" }
    }
  },
  "AmbientAgentConfig": {
    "type": "object",
    "properties": {
      "model_id": { "type": "string" },
      "skill_spec": { "type": "string" },
      "mcp_servers": { "type": "object" }
    }
  }
}
```

--------------------------------

### Define RunCreatorInfo schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the RunCreatorInfo object, which provides identity details about the user or service account that initiated a run. It includes fields for the principal type, unique identifier, display name, email, and profile photo URL.

```json
{"type":"object","description":"Identity information about the principal (user or service account) that created a run\nor scheduled agent. Present when the creator information is available.\n","properties":{"type":{"type":"string","enum":["user","service_account"],"description":"Type of the creator principal"},"uid":{"type":"string","description":"Unique identifier of the creator"},"display_name":{"type":"string","description":"Display name of the creator"},"email":{"type":"string","description":"Email address of the creator"},"photo_url":{"type":"string","format":"uri","description":"URL to the creator's photo"}}}
```

--------------------------------

### Configure Linear MCP Server in Warp

Source: https://docs.warp.dev/university/mcp-servers/linear-mcp-retrieve-issue-data

This JSON configuration defines the Linear MCP server parameters for the Warp terminal. It uses npx to execute the mcp-remote package with the Linear SSE endpoint.

```json
{
  "linear": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.linear.app/sse"],
      "env": {},
      "working_directory": null
    } 
}
```

--------------------------------

### Agent Configuration with MCP Servers (JSON)

Source: https://docs.warp.dev/agent-platform/cloud-agents/mcp

Shows how to embed MCP server configurations within a cloud agent's configuration file. This JSON structure includes agent settings like name, model ID, system prompt, environment ID, and the 'mcp_servers' object.

```json
{
  "name": "my-production-agent",
  "model_id": "claude-sonnet-4",
  "system_prompt": "You are a helpful assistant focused on backend development.",
  "environment_id": "SVhg783GBFQHk1OfdPfFU9",
  "mcp_servers": {
    "github": {
      "url": "https://mcp.example.com/github"
    },
    "dbt": {
      "command": "uvx",
      "args": ["dbt-mcp"],
      "env": {
        "DBT_HOST": "https://example.us1.dbt.com",
        "DBT_SERVICE_TOKEN": "${DBT_SERVICE_TOKEN}"
      }
    }
  }
}
```

--------------------------------

### Invoke Warp AI Input Shortcut

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-write-sql-commands-inside-a-postgres-repl

This describes the keyboard shortcut to activate Warp's AI input feature within any interactive shell. This feature allows users to input natural language commands that are translated into the appropriate syntax for the current REPL.

```text
Command + I    (macOS)
Ctrl + I       (Windows/Linux)
```

--------------------------------

### PUT /api/v1/schedules/{id}

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Updates an existing scheduled agent's configuration. All fields except agent_config are required.

```APIDOC
## PUT /api/v1/schedules/{id}

### Description
Update an existing scheduled agent's configuration. All fields except agent_config are required.

### Method
PUT

### Endpoint
/api/v1/schedules/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the scheduled agent.

#### Request Body
- **name** (string) - Required - Human-readable name for the schedule.
- **cron_schedule** (string) - Required - Cron expression defining when the agent runs.
- **enabled** (boolean) - Required - Whether the schedule should be active.
- **prompt** (string) - Required (unless agent_config.skill_spec is provided) - The prompt/instruction for the agent to execute.
- **agent_config** (object) - Optional - Configuration for the agent (model, environment, MCP servers, etc.).

### Request Example
{
  "name": "Daily Cleanup",
  "cron_schedule": "0 0 * * *",
  "enabled": true,
  "prompt": "Clean up temporary files."
}

### Response
#### Success Response (200)
- **id** (string) - Unique identifier of the updated agent.
- **name** (string) - Updated name.
- **cron_schedule** (string) - Updated cron schedule.
- **enabled** (boolean) - Updated status.

#### Response Example
{
  "id": "sch_12345",
  "name": "Daily Cleanup",
  "cron_schedule": "0 0 * * *",
  "enabled": true,
  "updated_at": "2023-10-27T10:00:00Z"
}
```

--------------------------------

### Name Cloud Runs for Tracking

Source: https://docs.warp.dev/reference/cli/cli

Assigns a configuration name to a run for grouping, filtering, and tracking workflows. Skill-based runs are named automatically, while custom runs require explicit --name flag usage.

```sh
# Name a recurring workflow for easy tracking
oz agent run-cloud \
  --environment <ENVIRONMENT_ID> \
  --name "nightly-dependency-check" \
  --prompt "Check for outdated dependencies and open a PR with updates"
```

```sh
# Skill-based runs are named automatically
oz agent run-cloud \
  --environment <ENVIRONMENT_ID> \
  --skill "myorg/backend:code-review" \
  --prompt "review the latest PR"
```

--------------------------------

### Configure Warp to Prefer Low Power GPU

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

This configuration snippet for the user_preferences.json file instructs Warp to prioritize using a low-power integrated GPU. This is a workaround for initialization errors, particularly when the default GPU is not recognized.

```json
{"prefs":{"PreferLowPowerGPU": "true",}}
```

--------------------------------

### Passing MCP servers by UUID

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

You can reference pre-configured MCP servers in your Warp account using their UUIDs.

```APIDOC
## Passing MCP servers by UUID

1. Locate the MCP server UUID using `oz mcp list`. This command lists all MCP servers configured in your Warp account, including team-shared ones:

```
$ oz mcp list
+--------------------------------------+--------+
| UUID                                 | Name   |
+===============================================+
| 1deb1b14-b6e5-4996-ae99-233b7555d2d0 | github |
|--------------------------------------+--------|
| 65450c32-9eb1-4c57-8804-0861737acbc4 | linear |
|--------------------------------------+--------|
| d94ade64-0e73-47a6-b3ee-14e5afec3d90 | Sentry |
+--------------------------------------+--------+
```

Alternatively, copy the UUID from Warp in **Settings** > **MCP Servers**.
2. Pass the UUID to `--mcp`:

```
$ oz agent run --mcp "1deb1b14-b6e5-4996-ae99-233b7555d2d0" --prompt "who last updated the README?"
```
```

--------------------------------

### Run Warp with verbose graphical debugging on Linux

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

Launches the terminal with elevated logging levels for WGPU, MESA, and EGL. This command is intended for diagnosing graphical crashes or display issues.

```bash
RUST_LOG=wgpu_core=info,wgpu_hal=info MESA_DEBUG=1 EGL_LOG_LEVEL=debug warp-terminal
RUST_LOG=wgpu_core=info,wgpu_hal=info MESA_DEBUG=1 EGL_LOG_LEVEL=debug warp-terminal-preview
```

--------------------------------

### Automate Warpification via RC files

Source: https://docs.warp.dev/terminal/warpify/subshells

These snippets use a Device Control String (DCS) to signal to Warp that a subshell is ready for integration. By appending these to your shell's RC file, you enable automatic Warpification without manual confirmation.

```zsh
printf '\eP$f{"hook": "SourcedRcFileForWarp", "value": { "shell": "zsh"}}\x9c'
```

```bash
printf '\eP$f{"hook": "SourcedRcFileForWarp", "value": { "shell": "bash"}}\x9c'
```

```fish
if status is-interactive
  printf '\eP$f{"hook": "SourcedRcFileForWarp", "value": { "shell": "fish"}}\x9c'
end
```

--------------------------------

### Configure Grafana SSE MCP Server

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This JSON configuration defines a Grafana SSE (Server-Sent Events) based MCP server using a provided URL. This is for remote or locally hosted MCP endpoints.

```json
{
  "Grafana": {
    "url": "https://your-mcp-host.com/api/mcp/grafana/sse"
  }
}
```

--------------------------------

### Generate SQL from Natural Language in Postgres REPL

Source: https://docs.warp.dev/university/developer-workflows/backend/how-to-write-sql-commands-inside-a-postgres-repl

This snippet shows how to use Warp's AI input to translate natural language requests into SQL commands for a Postgres REPL. The AI learns from the REPL's context to generate increasingly accurate and complex queries.

```sql
-- Show me all tables.
\dt
```

```sql
-- Show me our users table and our teams table.
SELECT * FROM users;
SELECT * FROM teams;
```

```sql
-- Show me all of the users who have joined Warp in the last 90 days from public email accounts (like Gmail, Yahoo, Hotmail) and are on teams of more than two people.
SELECT *
FROM users
WHERE email LIKE '%gmail.com%'
   OR email LIKE '%yahoo.com%'
   OR email LIKE '%hotmail.com%'
  AND joined_at > NOW() - INTERVAL '90 days'
  AND team_size > 2;
```

```sql
-- List all databases.
\l
```

```sql
-- Count how many users signed up this month.
SELECT COUNT(*) FROM users WHERE joined_at > date_trunc('month', NOW());
```

--------------------------------

### Route Runs to Self-Hosted Worker via Scheduled Agents

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

Configures scheduled agent runs to be executed by a self-hosted worker. The `--host` flag is used during schedule creation or update to specify the target worker ID. This ensures recurring tasks are processed by your infrastructure.

```bash
oz schedule create --name "daily-cleanup" \
  --cron "0 9 * * *" \
  --prompt "Run dead code cleanup" \
  --environment ENV_ID \
  --host "my-worker"

oz schedule update SCHEDULE_ID --host "my-worker"
```

--------------------------------

### POST /agent/schedules/{scheduleId}/resume

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Resumes a previously paused scheduled agent, enabling it to run according to its defined cron schedule.

```APIDOC
## POST /agent/schedules/{scheduleId}/resume

### Description
Resume a paused scheduled agent. The agent will start running according to its cron schedule. This sets the enabled flag to true.

### Method
POST

### Endpoint
/agent/schedules/{scheduleId}/resume

### Parameters
#### Path Parameters
- **scheduleId** (string) - Required - The unique identifier of the scheduled agent

### Request Example
{}

### Response
#### Success Response (200)
- **ScheduledAgentItem** (object) - The updated scheduled agent object

#### Response Example
{
  "id": "sched_12345",
  "enabled": true
}
```

--------------------------------

### MCPServerConfig Object Definition (JSON Schema)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the configuration for an MCP server connection. It supports three transport methods: Warp-managed servers via 'warp_id', local stdio processes via 'command' and 'args', and remote SSE/HTTP servers via 'url'. Environment variables and HTTP headers can also be specified.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "components": {
    "schemas": {
      "MCPServerConfig": {
        "type": "object",
        "description": "Configuration for a single MCP (Model Context Protocol) server to attach to an agent run.\nExactly one of warp_id, command, or url must be provided, corresponding to the three\nsupported transports:\n- warp_id: reference a Warp-managed shared MCP server by UUID\n- command + args: launch a local stdio-based MCP server process\n- url: connect to a remote SSE or HTTP MCP server\n",
        "properties": {
          "warp_id": {
            "type": "string",
            "description": "Reference to a Warp shared MCP server by UUID"
          },
          "command": {
            "type": "string",
            "description": "Stdio transport - command to run"
          },
          "args": {
            "type": "array",
            "items": {
              "type": "string"
            },
            "description": "Stdio transport - command arguments"
          },
          "url": {
            "type": "string",
            "format": "uri",
            "description": "SSE/HTTP transport - server URL"
          },
          "env": {
            "type": "object",
            "additionalProperties": {
              "type": "string"
            },
            "description": "Environment variables for the server"
          },
          "headers": {
            "type": "object",
            "additionalProperties": {
              "type": "string"
            },
            "description": "HTTP headers for SSE/HTTP transport"
          }
        }
      }
    }
  }
}
```

--------------------------------

### ArtifactResponse Object Definition (JSON Schema)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for artifact retrieval responses, currently supporting screenshot artifacts. It includes a unique identifier, type, creation timestamp, and the artifact data, which contains a download URL and expiration time for screenshots.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "components": {
    "schemas": {
      "ArtifactResponse": {
        "type": "object",
        "description": "Response for artifact retrieval. Currently supports screenshot artifacts.",
        "required": [
          "artifact_uid",
          "artifact_type",
          "created_at",
          "data"
        ],
        "properties": {
          "artifact_uid": {
            "type": "string",
            "description": "Unique identifier (UUID) for the artifact"
          },
          "artifact_type": {
            "type": "string",
            "description": "Type of the artifact (e.g., SCREENSHOT)"
          },
          "created_at": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the artifact was created (RFC3339)"
          },
          "data": {
            "$ref": "#/components/schemas/ScreenshotArtifactResponseData"
          }
        }
      },
      "ScreenshotArtifactResponseData": {
        "type": "object",
        "description": "Response data for a screenshot artifact, including a signed download URL.",
        "required": [
          "download_url",
          "expires_at",
          "content_type"
        ],
        "properties": {
          "download_url": {
            "type": "string",
            "format": "uri",
            "description": "Time-limited signed URL to download the screenshot"
          },
          "expires_at": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the download URL expires (RFC3339)"
          },
          "content_type": {
            "type": "string",
            "description": "MIME type of the screenshot (e.g., image/png)"
          },
          "description": {
            "type": "string",
            "description": "Optional description of the screenshot"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Define PageInfo pagination schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the PageInfo object used for cursor-based pagination. It includes a boolean flag for checking if more results exist and an opaque string cursor for fetching subsequent pages.

```json
{"type":"object","description":"Cursor-based pagination metadata. When has_next_page is true, pass\nnext_cursor as the cursor parameter on the next request to retrieve\nthe following page of results.\n","required":["has_next_page"],"properties":{"has_next_page":{"type":"boolean","description":"Whether there are more results available"},"next_cursor":{"type":"string","description":"Opaque cursor for fetching the next page"}}}
```

--------------------------------

### Define RequestUsage schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the RequestUsage object used to track resource consumption for a specific run. It captures costs associated with LLM inference and compute resources.

```json
{"type":"object","description":"Resource usage information for the run","properties":{"inference_cost":{"type":"number","format":"double","description":"Cost of LLM inference for the run"},"compute_cost":{"type":"number","format":"double","description":"Cost of compute resources for the run"}}}
```

--------------------------------

### Run Creator Information

Source: https://docs.warp.dev/reference/api-and-sdk/models

Details the identity of the principal (user or service account) that created a run.

```APIDOC
## Run Creator Information

### Description
Identity information about the principal (user or service account) that created a run or scheduled agent. Present when the creator information is available.

### Object: RunCreatorInfo

- **type** (string) - Type of the creator principal (`user` or `service_account`)
- **uid** (string) - Unique identifier of the creator
- **display_name** (string) - Display name of the creator
- **email** (string) - Email address of the creator
- **photo_url** (string) - URL to the creator's photo

```

--------------------------------

### Launch Configuration YAML File Locations

Source: https://docs.warp.dev/terminal/sessions/launch-configurations

Specifies the directory paths where Launch Configuration YAML files are stored on different operating systems. Ensure correct path formatting for your OS.

```bash
$HOME/.warp/launch_configurations/
```

```powershell
$env:APPDATA\warp\Warp\data\launch_configurations\
```

```bash
${XDG_DATA_HOME:-$HOME/.local/share}/warp-terminal/launch_configurations/
```

--------------------------------

### Configure Oz Agent with Skills in GitHub Actions

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/github-actions

Demonstrates how to invoke an Oz agent in a GitHub Actions workflow using a specific skill. This requires a Warp API key stored in GitHub secrets.

```yaml
- name: Run agent with a skill
  uses: warpdotdev/oz-agent-action@v1
  with:
    skill: 'code-review'
    warp_api_key: ${{ secrets.WARP_API_KEY }}
```

--------------------------------

### Define AttachmentInput Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

This schema defines the structure for submitting base64-encoded file attachments. It requires the file name, MIME type, and the encoded data string, supporting common image formats like JPEG, PNG, GIF, and WebP.

```json
{
  "type": "object",
  "description": "A base64-encoded file attachment to include with the prompt",
  "required": ["file_name", "mime_type", "data"],
  "properties": {
    "file_name": {"type": "string", "description": "Name of the attached file"},
    "mime_type": {"type": "string", "description": "MIME type of the attachment.\nSupported image types: image/jpeg, image/png, image/gif, image/webp\n"},
    "data": {"type": "string", "format": "byte", "description": "Base64-encoded attachment data"}
  }
}
```

--------------------------------

### Clone Warp Themes Repository (Windows)

Source: https://docs.warp.dev/terminal/appearance/custom-themes

Clones the Warp themes repository into the user's application data directory for Windows. This ensures themes are stored in the correct location for Warp Terminal on Windows.

```powershell
New-Item -Path "$env:APPDATA\warp\Warp\data\" -ItemType Directory
Set-Location -Path $env:APPDATA\warp\Warp\data\
git clone https://github.com/warpdotdev/themes.git
```

--------------------------------

### Zip Warp Preview Logs on Windows

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

This PowerShell command archives Warp Preview log files from the local app data directory to the Desktop. Ensure Warp Preview is closed prior to running this command. It utilizes the Compress-Archive cmdlet for creating the zip file.

```powershell
Compress-Archive -Path "$env:LOCALAPPDATA\warp\WarpPreview\data\logs\warp_preview.log*" -DestinationPath "$([Environment]::GetFolderPath('Desktop'))\warp_preview-logs.zip"
```

--------------------------------

### Remove Warp Preview Configuration Files (Shell)

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/logging-out-and-uninstalling

This command removes the configuration files for Warp Preview. It targets the XDG_CONFIG_HOME directory, defaulting to ~/.config if the environment variable is not set. This action is irreversible and will delete all custom settings.

```shell
rm -r ${XDG_CONFIG_HOME:-$HOME/.config}/warp-terminal-preview
```

--------------------------------

### Create Scheduled Agent Tasks

Source: https://docs.warp.dev/agent-platform/cloud-agents/skills-as-agents

Command to automate the execution of a skill-based agent using a cron schedule. This is useful for recurring maintenance tasks like code cleanup or dependency updates.

```bash
oz schedule create \
  --name "Weekly Code Cleanup" \
  --cron "0 10 * * 1" \
  --environment <ENV_ID> \
  --prompt "Scan for dead code and unused feature flags. Open a PR with removals."
```

--------------------------------

### Warp Active and Focus Configuration

Source: https://docs.warp.dev/terminal/sessions/launch-configurations

Configures active windows, tabs, and focused panes within a Warp launch configuration. Uses `active_window_index`, `active_tab_index`, and `is_focused` fields.

```yaml
# Warp Launch Configuration
#
# This configurations has two tabs, with the second tab active.
# Two vertical split panes in the first tab and the top pane focused.
# Two horizontal split panes in the second tab and the right pane focused.
---
name: Example Active and Focus
active_window_index: 0
windows:
  - active_tab_index: 1
    tabs:
      - title: Tab 1
        layout:
          split_direction: vertical
          panes:
            - cwd: /Users/warp-user/Documents
              is_focused: true
            - cwd: /Users/warp-user/Documents/Projects
      - title: Tab 2
        layout:
          split_direction: horizontal
          panes:
            - cwd: /Users/warp-user/Downloads
            - cwd: /Users/warp-user
              is_focused: true
```

--------------------------------

### Configure Ambient Agent Settings

Source: https://docs.warp.dev/reference/api-and-sdk/agent

The AmbientAgentConfig schema allows for granular control over agent execution, including model IDs, base prompts, and MCP server configurations.

```json
{
  "AmbientAgentConfig": {
    "type": "object",
    "properties": {
      "name": { "type": "string" },
      "model_id": { "type": "string" },
      "base_prompt": { "type": "string" },
      "environment_id": { "type": "string" },
      "skill_spec": { "type": "string" },
      "mcp_servers": { "type": "object", "additionalProperties": { "$ref": "#/components/schemas/MCPServerConfig" } },
      "computer_use_enabled": { "type": "boolean" },
      "worker_host": { "type": "string" }
    }
  }
}
```

--------------------------------

### ListRunsResponse Object Definition (OpenAPI)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure of the ListRunsResponse object using OpenAPI 3.0.0 specification. It outlines the properties for a paginated list of agent runs, including the runs themselves and pagination information.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "components": {
    "schemas": {
      "ListRunsResponse": {
        "type": "object",
        "description": "Paginated list of agent runs. Use page_info.next_cursor to fetch\nsubsequent pages. Results are sorted by updated_at descending by default.\n",
        "required": [
          "runs",
          "page_info"
        ],
        "properties": {
          "runs": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/RunItem"
            }
          },
          "page_info": {
            "$ref": "#/components/schemas/PageInfo"
          }
        }
      },
      "RunItem": {
        "type": "object",
        "description": "Full representation of a single agent run. Includes the run's identity\n(run_id, task_id, title), lifecycle state, original prompt, timestamps, optional\nsession link for viewing the agent's work, the creator's identity, resolved\nagent configuration, and any artifacts produced during the run.\n",
        "required": [
          "run_id",
          "task_id",
          "title",
          "state",
          "prompt",
          "created_at",
          "updated_at"
        ],
        "properties": {
          "run_id": {
            "type": "string",
            "description": "Unique identifier for the run"
          },
          "task_id": {
            "type": "string",
            "deprecated": true,
            "description": "Unique identifier for the task (typically matches run_id). Deprecated - use run_id instead."
          },
          "title": {
            "type": "string",
            "description": "Human-readable title for the run"
          },
          "state": {
            "$ref": "#/components/schemas/RunState"
          },
          "prompt": {
            "type": "string",
            "description": "The prompt/instruction for the agent"
          },
          "created_at": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the run was created (RFC3339)"
          },
          "updated_at": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the run was last updated (RFC3339)"
          },
          "started_at": {
            "type": "string",
            "format": "date-time",
            "nullable": true,
            "description": "Timestamp when the agent started working on the run (RFC3339)"
          },
          "status_message": {
            "$ref": "#/components/schemas/RunStatusMessage"
          },
          "source": {
            "$ref": "#/components/schemas/RunSourceType"
          },
          "schedule": {
            "$ref": "#/components/schemas/ScheduleInfo"
          },
          "session_id": {
            "type": "string",
            "description": "UUID of the shared session (if available)"
          },
          "session_link": {
            "type": "string",
            "format": "uri",
            "description": "URL to view the agent session"
          },
          "creator": {
            "$ref": "#/components/schemas/RunCreatorInfo"
          },
          "request_usage": {
            "$ref": "#/components/schemas/RequestUsage"
          },
          "agent_config": {
            "$ref": "#/components/schemas/AmbientAgentConfig"
          },
          "conversation_id": {
            "type": "string",
            "description": "UUID of the conversation associated with the run"
          },
          "is_sandbox_running": {
            "type": "boolean",
            "description": "Whether the sandbox environment is currently running"
          },
          "artifacts": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/ArtifactItem"
            },
            "description": "Artifacts created during the run (plans, pull requests, etc.)"
          },
          "agent_skill": {
            "$ref": "#/components/schemas/AgentSkill"
          },
          "scope": {
            "$ref": "#/components/schemas/Scope"
          }
        }
      },
      "RunState": {
        "type": "string",
        "enum": [
          "QUEUED",
          "PENDING",
          "CLAIMED",
          "INPROGRESS",
          "SUCCEEDED",
          "FAILED",
          "BLOCKED",
          "ERROR",
          "CANCELLED"
        ],
        "description": "Current state of the run:\n- QUEUED: Run is waiting to be picked up\n- PENDING: Run is being prepared\n- CLAIMED: Run has been claimed by a worker\n- INPROGRESS: Run is actively being executed\n- SUCCEEDED: Run completed successfully\n- FAILED: Run failed\n- BLOCKED: Run is blocked (e.g., awaiting user input or approval)\n- ERROR: Run encountered an error\n- CANCELLED: Run was cancelled by user\n"
      },
      "RunStatusMessage": {
        "type": "object",
        "description": "Status message for a run. For terminal error states, includes structured\nerror code and retryability info from the platform error catalog.\n",
        "required": [
          "message"
        ],
        "properties": {
          "message": {
            "type": "string",
            "description": "Human-readable status message"
          },
          "error_code": {
            "$ref": "#/components/schemas/PlatformErrorCode"
          },
          "retryable": {
            "type": "boolean",
            "description": "Whether the error is transient and the client may retry by submitting\na new run. Only present on terminal error states. When false, retrying\nwithout addressing the underlying cause will not succeed.\n"
          }
        }
      },
      "PlatformErrorCode": {
        "type": "string",
        "description": "Machine-readable error code identifying the problem type.\nUsed in the `type` URI of Error responses and in the `error_code`\nfield of RunStatusMessage.\n\nUser errors (run transitions to FAILED):\n- `insufficient_credits` — Team has no remaining add-on credits\n- `feature_not_available` — Required feature not enabled for user's plan\n- `external_authentication_required` — User hasn't authorized a required external service\n- `not_authorized` — Principal lacks permission for the requested operation\n- `invalid_request` — Request is malformed or contains invalid parameters\n- `resource_not_found` — Referenced resource does not exist\n- `budget_exceeded` — Spending budget limit has been reached\n- `integration_disabled` — Integration is disabled and must be enabled\n- `integration_not_configured` — Integration setup is incomplete\n- `operation_not_supported` — Requested operation not supported for this resource/state\n- `environment_setup_failed` — Client-side environment setup failed\n- `content_policy_violatio"
      }
    }
  }
}
```

--------------------------------

### ScheduleInfo Object

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Metadata about the scheduled agent that triggered a run.

```APIDOC
## ScheduleInfo Object

### Description
Metadata about the scheduled agent that triggered this run. Only present on runs where source is SCHEDULED_AGENT. Contains the schedule ID, its name, and the cron expression as they were configured at the time the run was created.

### Properties
- **schedule_id** (string) - Unique identifier for the schedule.
- **schedule_name** (string) - Name of the schedule at the time the run was created.
- **cron_schedule** (string) - Cron expression at the time the run was created.
```

--------------------------------

### Define ScreenshotArtifactResponseData Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

This schema defines the response structure for screenshot artifacts, providing a signed download URL, expiration timestamp, and content metadata. It is used to facilitate secure, time-limited access to generated screenshot files.

```json
{
  "type": "object",
  "description": "Response data for a screenshot artifact, including a signed download URL.",
  "required": ["download_url", "expires_at", "content_type"],
  "properties": {
    "download_url": {"type": "string", "format": "uri", "description": "Time-limited signed URL to download the screenshot"},
    "expires_at": {"type": "string", "format": "date-time", "description": "Timestamp when the download URL expires (RFC3339)"},
    "content_type": {"type": "string", "description": "MIME type of the screenshot (e.g., image/png)"},
    "description": {"type": "string", "description": "Optional description of the screenshot"}
  }
}
```

--------------------------------

### Configure Figma Local MCP Server

Source: https://docs.warp.dev/knowledge-and-collaboration/mcp

This configuration enables the local MCP server for Figma. Ensure the official Figma MCP Server is enabled and the Figma desktop app is updated. This server runs on localhost.

```json
{
  "Figma (Local)": {
    "url": "http://127.0.0.1:3845/mcp"
  }
}
```

--------------------------------

### Archive Warp logs on Linux

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

Compresses Warp or Warp Preview log files into a tarball in the user's home directory. This facilitates easy sharing of logs for support requests.

```bash
tar -czf ~/warp-logs.tar.gz -C ~/.local/state/warp-terminal warp.log*
tar -czf ~/warp_preview-logs.tar.gz -C ~/.local/state/warp-terminal-preview warp_preview.log*
```

--------------------------------

### Configure Ambient Agent Settings

Source: https://docs.warp.dev/reference/api-and-sdk/agent

The AmbientAgentConfig schema allows for granular control over agent execution, including model selection, environment IDs, and MCP server mapping.

```json
{
  "type": "object",
  "properties": {
    "name": { "type": "string" },
    "model_id": { "type": "string" },
    "base_prompt": { "type": "string" },
    "environment_id": { "type": "string" },
    "skill_spec": { "type": "string" },
    "mcp_servers": { "type": "object" },
    "computer_use_enabled": { "type": "boolean" },
    "worker_host": { "type": "string" }
  }
}
```

--------------------------------

### Define RunCreatorInfo Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Captures identity information for the principal that initiated a run or scheduled agent. It supports both users and service accounts with fields for UID, display name, email, and profile photo.

```json
{
  "type": "object",
  "description": "Identity information about the principal that created a run",
  "properties": {
    "type": { "type": "string", "enum": ["user", "service_account"] },
    "uid": { "type": "string" },
    "display_name": { "type": "string" },
    "email": { "type": "string" },
    "photo_url": { "type": "string", "format": "uri" }
  }
}
```

--------------------------------

### List Scheduled Agents Response Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Details about the response object returned when listing scheduled agents.

```APIDOC
## List Scheduled Agents Response Object

### Description
Response containing all scheduled agents accessible to the authenticated user, sorted alphabetically by name.

### Method
GET

### Endpoint
/agents/scheduled

### Parameters
#### Query Parameters
- **schedules** (array) - Required - List of scheduled agents

### Response
#### Success Response (200)
- **schedules** (array) - List of scheduled agents, where each item is of type `ScheduledAgentItem`.

#### Response Example
```json
{
  "schedules": [
    {
      "id": "agent-123",
      "name": "Daily Report Generator",
      "cron_schedule": "0 9 * * *",
      "enabled": true,
      "prompt": "Generate a daily summary report.",
      "last_spawn_error": null,
      "agent_config": {
        "name": "Report Generation",
        "model_id": "claude-3-opus",
        "environment_id": "env-abc",
        "skill_spec": "warpdotdev/warp-server:.claude/skills/reports/SKILL.md"
      },
      "environment": {
        "name": "Production Environment",
        "description": "Production deployment environment."
      },
      "created_at": "2023-10-27T10:00:00Z",
      "updated_at": "2023-10-27T10:05:00Z",
      "created_by": {
        "user_id": "user-xyz",
        "name": "Alice"
      },
      "updated_by": {
        "user_id": "user-xyz",
        "name": "Alice"
      },
      "history": {},
      "scope": {}
    }
  ]
}
```
```

--------------------------------

### PlatformErrorCode Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Machine-readable error code identifying the problem type.

```APIDOC
## PlatformErrorCode Object

### Description
Machine-readable error code identifying the problem type. Used in the `type` URI of Error responses and in the `error_code` field of RunStatusMessage.

### Enum Values
User errors (run transitions to FAILED):
- `insufficient_credits` — Team has no remaining add-on credits
- `feature_not_available` — Required feature not enabled for user's plan
- `external_authentication_required` — User hasn't authorized a required external service
- `not_authorized` — Principal lacks permission for the requested operation
- `invalid_request` — Request is malformed or contains invalid parameters
- `resource_not_found` — Referenced resource does not exist
- `budget_exceeded` — Spending budget limit has been reached
- `integration_disabled` — Integration is disabled and must be enabled
- `integration_not_configured` — Integration setup is incomplete
- `operation_not_supported` — Requested operation not supported for this resource/state
- `environment_setup_failed` — Client-side environment setup failed
- `content_policy_violation` — Prompt or setup commands violated content policy
- `conflict` — Request conflicts with the current state of the resource

Warp errors (run transitions to ERROR):
- `authentication_required` — Request lacks valid authentication credentials
- `resource_unavailable` — Transient infrastructure issue (retryable)
- `internal_error` — Unexpected server-side error (retryable)
```

--------------------------------

### Warp Tabs Configuration

Source: https://docs.warp.dev/terminal/sessions/launch-configurations

Defines a launch configuration with multiple tabs in a single window. Each tab can have a title, working directory, and color.

```yaml
# Warp Launch Configuration
# This configuration has two tabs in the same window.

---
name: Example Tabs
windows:
  - tabs:
      - title: Documents 
        layout:
          cwd: /Users/warp-user/Documents
        color: blue
      - title: Warp User
        layout:
          cwd: /Users/warp-user
        color: green
```

--------------------------------

### Locate MCP Logs on macOS

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This command navigates to the directory where Warp stores MCP logs on macOS. Inspecting these files can help diagnose server issues.

```bash
cd "$HOME/Library/Group Containers/2BBY89MBSN.dev.warp/Library/Application Support/dev.warp.Warp-Stable/mcp"
```

--------------------------------

### Run Agent with MCP Server by UUID

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

Connects an agent to an external service using an MCP server identified by its UUID. This is useful for referencing pre-configured servers in your Warp account.

```bash
$ oz agent run --mcp "1deb1b14-b6e5-4996-ae99-233b7555d2d0" --prompt "who last updated the README?"
```

--------------------------------

### YAML Configuration for Combined Accent and Background Gradients in Warp Theme

Source: https://docs.warp.dev/terminal/appearance/custom-themes

This YAML configuration illustrates setting gradients for both the accent and background colors in a Warp theme. It uses 'left'/'right' for the accent and 'top'/'bottom' for the background, allowing for complex color schemes.

```yaml
# accent has a gradient
accent:
  left: '#474747'
  right: '#ffffff'
# background has a gradient
background:
  top: '#474747'
  bottom: '#ffffff'
```

--------------------------------

### AgentListItem Object Schema (OpenAPI)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure of the AgentListItem object, representing a skill with one or more variants. It includes the skill's name and a list of its available variants. This schema is part of the Oz Agent API.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "components": {
    "schemas": {
      "AgentListItem": {
        "type": "object",
        "description": "A skill with one or more variants. Variants represent different versions\nof the same skill sourced from different repositories or environments.\n",
        "required": [
          "name",
          "variants"
        ],
        "properties": {
          "name": {
            "type": "string",
            "description": "Human-readable name of the agent"
          },
          "variants": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/AgentListVariant"
            },
            "description": "Available variants of this agent"
          }
        }
      },
      "AgentListVariant": {
        "type": "object",
        "description": "A specific skill variant, uniquely identified by its skill path in a repository.\nEach variant carries its own instructions (base_prompt), source repository\nmetadata, and the list of environments it is available in.\n",
        "required": [
          "id",
          "description",
          "base_prompt",
          "source",
          "environments"
        ],
        "properties": {
          "id": {
            "type": "string",
            "description": "Stable identifier for this skill variant.\nFormat: \"{owner}/{repo}:{skill_path}\"\nExample: \"warpdotdev/warp-server:.claude/skills/deploy/SKILL.md\"\n"
          },
          "description": {
            "type": "string",
            "description": "Description of the agent variant"
          },
          "base_prompt": {
            "type": "string",
            "description": "Base prompt/instructions for the agent"
          },
          "source": {
            "$ref": "#/components/schemas/AgentListSource"
          },
          "environments": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/AgentListEnvironment"
            },
            "description": "Environments where this agent variant is available"
          },
          "last_run_timestamp": {
            "type": "string",
            "format": "date-time",
            "nullable": true,
            "description": "Timestamp of the last time this skill was run (RFC3339)"
          },
          "error": {
            "type": "string",
            "description": "Non-empty when the skill's SKILL.md file exists but is malformed.\nContains a description of the parse failure. Only present when\ninclude_malformed_skills=true is passed to the list agents endpoint.\n"
          }
        }
      },
      "AgentListSource": {
        "type": "object",
        "description": "Source repository metadata identifying where a skill variant is defined.",
        "required": [
          "owner",
          "name",
          "skill_path"
        ],
        "properties": {
          "owner": {
            "type": "string",
            "description": "GitHub repository owner"
          },
          "name": {
            "type": "string",
            "description": "GitHub repository name"
          },
          "skill_path": {
            "type": "string",
            "description": "Path to the skill definition file within the repository"
          }
        }
      },
      "AgentListEnvironment": {
        "type": "object",
        "description": "An environment in which a skill variant is available and can be executed.",
        "required": [
          "uid",
          "name"
        ],
        "properties": {
          "uid": {
            "type": "string",
            "description": "Unique identifier for the environment"
          },
          "name": {
            "type": "string",
            "description": "Human-readable name of the environment"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Error Handling Specification

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting

Overview of the standard error response format used by the Oz platform API.

```APIDOC
## Error Handling (RFC 7807)

### Description
All Oz platform API errors return a structured response following the RFC 7807 standard to ensure consistent machine-readable error reporting.

### Response Format
- **type** (string) - A URI reference that identifies the problem type.
- **title** (string) - A short, human-readable summary of the problem type.
- **status** (integer) - The HTTP status code generated by the origin server.
- **detail** (string) - A human-readable explanation specific to this occurrence of the problem.
- **instance** (string) - A URI reference that identifies the specific occurrence of the problem.

### Response Example
{
  "type": "https://docs.warp.dev/errors/invalid-request",
  "title": "Invalid Request",
  "status": 400,
  "detail": "The provided request body is missing required fields.",
  "instance": "/api/v1/resource/123"
}
```

--------------------------------

### Configure Figma MCP Server

Source: https://docs.warp.dev/knowledge-and-collaboration/rules

Configures Figma integration for remote or local MCP servers. Local server requires specific configuration within the Figma desktop application.

```json
{
  "Figma": {
    "url": "https://mcp.figma.com/mcp"
  }
}
```

```json
{
  "Figma (Local)": {
    "url": "http://127.0.0.1:3845/mcp"
  }
}
```

--------------------------------

### Define RunState Enumeration

Source: https://docs.warp.dev/reference/api-and-sdk/models

This schema defines the possible states for an agent run, ranging from QUEUED to CANCELLED. It is used to track the lifecycle of an agent execution.

```json
{
  "type": "string",
  "enum": ["QUEUED", "PENDING", "CLAIMED", "INPROGRESS", "SUCCEEDED", "FAILED", "BLOCKED", "ERROR", "CANCELLED"],
  "description": "Current state of the run"
}
```

--------------------------------

### List and Execute with Warp Agent Profiles

Source: https://docs.warp.dev/reference/cli/agent-profiles

Commands to retrieve the list of available agent profiles and execute an agent task using a specific profile ID. The profile ID is required to define the scope of permissions for the agent run.

```shell
oz agent profile list
```

```shell
oz agent run --profile CWhozDJPdPCsjJ1pSG0HCN --prompt "update my CI pipeline to use nextest"
```

--------------------------------

### List Scheduled Agents

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Retrieves a list of all scheduled agents accessible to the authenticated user. The results are sorted alphabetically by name.

```APIDOC
## List Scheduled Agents

### Description
Retrieve all scheduled agents accessible to the authenticated user. Results are sorted alphabetically by name.

### Method
GET

### Endpoint
/schedules

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - Maximum number of schedules to return.
- **offset** (integer) - Optional - Number of schedules to skip before starting to collect the result set.
- **name** (string) - Optional - Filter schedules by name.
- **sort_by** (string) - Optional - Field to sort the results by. Allowed values: `name`, `created_at`, `updated_at`.
- **sort_order** (string) - Optional - Order of sorting. Allowed values: `asc`, `desc`. Defaults to `asc`.

### Request Example
```bash
curl -X GET "https://app.warp.dev/api/v1/schedules?limit=10&offset=0&sort_by=name&sort_order=asc"
     -H "Authorization: Bearer YOUR_API_KEY"
```

### Response
#### Success Response (200)
- **schedules** (array) - List of scheduled agents. Each item contains:
  - **id** (string) - Unique identifier for the scheduled agent.
  - **name** (string) - Human-readable name for the schedule.
  - **cron_schedule** (string) - Cron expression defining when the agent runs.
  - **enabled** (boolean) - Whether the schedule is currently active.
  - **prompt** (string) - The prompt/instruction for the agent to execute.
  - **created_at** (string) - Timestamp when the schedule was created (RFC3339).
  - **updated_at** (string) - Timestamp when the schedule was last updated (RFC3339).
  - **agent_config** (object) - Configuration for the agent.
  - **environment** (object) - Resolved environment configuration.
  - **created_by** (object) - Information about who created the schedule.
  - **updated_by** (object) - Information about who last updated the schedule.
  - **history** (object) - History of the scheduled agent runs.
  - **scope** (object) - Scope of the scheduled agent.

#### Response Example
```json
{
  "schedules": [
    {
      "id": "sched_12345abcde",
      "name": "Daily Report",
      "cron_schedule": "0 9 * * *",
      "enabled": true,
      "prompt": "Generate a daily summary report.",
      "created_at": "2023-10-27T10:00:00Z",
      "updated_at": "2023-10-27T10:00:00Z",
      "agent_config": {
        "model_id": "claude-3-opus-20240229",
        "skill_spec": "warpdotdev/warp-server:.claude/skills/report/SKILL.md"
      },
      "environment": {
        "id": "env_abcdef1234",
        "name": "production"
      },
      "created_by": {
        "user_id": "user_xyz789",
        "name": "Alice"
      },
      "updated_by": {
        "user_id": "user_xyz789",
        "name": "Alice"
      },
      "history": {},
      "scope": {}
    }
  ]
}
```
```

--------------------------------

### Zip Warp Logs on macOS

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

This command zips the Warp log files located in the user's Library directory to the Desktop. It uses the 'zip' utility and preserves file attributes. Ensure Warp is not running for accurate log capture.

```bash
zip -j ~/Desktop/warp-logs.zip ~/Library/Logs/warp.log*
```

--------------------------------

### YAML Configuration for Background Image in Warp Theme

Source: https://docs.warp.dev/terminal/appearance/custom-themes

This YAML snippet demonstrates how to set a background image for a Warp theme. It specifies the image path relative to the themes directory and an opacity value. Note that Warp currently only supports JPG image formats.

```yaml
name: Custom Theme
accent: '#268bd2'
cursor: '#95D886'
background: '#002b36'
details: darker
foreground: '#839496'

############################################################### SEE BELOW
background_image:
  # the path is relative to ~/.warp/themes/
  # the full path to the picture is: ~/.warp/themes/warp.jpg
  path: warp.jpg
  # the opacity value is required and can range from 0-100
  opacity: 60
############################################################### SEE ABOVE

terminal_colors:
  bright:
    black: '#002b36'
    blue: '#839496'
    cyan: '#93a1a1'
    green: '#586e75'
    magenta: '#6c71c4'
    red: '#cb4b16'
    white: '#fdf6e3'
    yellow: '#657b83'
  normal:
    black: '#073642'
    blue: '#268bd2'
    cyan: '#2aa198'
    green: '#859900'
    magenta: '#d33682'
    red: '#dc322f'
    white: '#eee8d5'
    yellow: '#b58900'
```

--------------------------------

### Locate MCP Logs on Windows

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This command sets the location to the directory where Warp stores MCP logs on Windows. Examining these files can aid in troubleshooting server problems.

```powershell
Set-Location $env:LOCALAPPDATA\warp\Warp\data\logs\mcp
```

--------------------------------

### Scope Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the ownership scope for a resource, either team or personal.

```APIDOC
## Scope Schema

### Description
Ownership scope for a resource (team or personal).

### Properties
- **type** (string) - Required - Type of ownership ("User" for personal, "Team" for team-owned).
- **uid** (string) - Optional - Unique identifier for the user or team.
```

--------------------------------

### Differentiate Docker and Worker Environment Variables

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting/managed-worker-reference

Demonstrates the distinction between environment variables passed to the worker container versus those passed to the task containers spawned by the worker.

```bash
# Docker -e: passes WARP_API_KEY to the worker container
# Worker -e: passes MY_SECRET to task containers
docker run \
  -e WARP_API_KEY="$WARP_API_KEY" \
  warpdotdev/oz-agent-worker \
  --worker-id "my-worker" \
  -e MY_SECRET=hunter2
```

--------------------------------

### Scope Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the ownership scope for a resource, either user or team.

```APIDOC
## Scope Object

### Description
Ownership scope for a resource (team or personal)

### Properties
- **type** (string) - Required - Enum: ["User", "Team"] - Type of ownership ("User" for personal, "Team" for team-owned)
- **uid** (string) - Optional - UID of the owning user or team
```

--------------------------------

### ArtifactItem Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure of an ArtifactItem, a discriminated union that represents different types of artifacts produced during an agent run.

```APIDOC
## ArtifactItem Object

### Description
A discriminated union representing an artifact produced during an agent run. The `artifact_type` field determines the variant: PLAN, PULL_REQUEST, or SCREENSHOT.

### Properties
- **artifact_type** (string) - Required - Must be one of: "PLAN", "PULL_REQUEST", "SCREENSHOT".
- **created_at** (string) - Required - Timestamp in RFC3339 format.
- **data** (object) - Required - Type-specific data payload.

### Example
{
  "artifact_type": "PLAN",
  "created_at": "2023-10-27T10:00:00Z",
  "data": {
    "document_uid": "doc_123",
    "title": "Project Plan"
  }
}
```

--------------------------------

### RunAgentRequest Object Schema (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure of the RunAgentRequest object used for creating agent runs. It specifies properties like prompt, skill, configuration, title, team, conversation ID, attachments, and interactivity. Either a prompt or a skill is required.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "components": {
    "schemas": {
      "RunAgentRequest": {
        "type": "object",
        "description": "Request body for creating a new agent run.\nEither prompt or skill (via skill field or config.skill_spec) is required.\n",
        "properties": {
          "prompt": {
            "type": "string",
            "description": "The prompt/instruction for the agent to execute.\nRequired unless a skill is specified via the skill field or config.skill_spec.\n"
          },
          "skill": {
            "type": "string",
            "description": "Skill specification to use as the base prompt for the agent.\nSupported formats:\n  - \"repo:skill_name\" - Simple name in specific repo\n  - \"repo:skill_path\" - Full path in specific repo\n  - \"org/repo:skill_name\" - Simple name with org and repo\n  - \"org/repo:skill_path\" - Full path with org and repo\nWhen provided, this takes precedence over config.skill_spec.\n"
          },
          "config": {
            "$ref": "#/components/schemas/AmbientAgentConfig"
          },
          "title": {
            "type": "string",
            "description": "Custom title for the run (auto-generated if not provided)"
          },
          "team": {
            "type": "boolean",
            "description": "Whether to create a team-owned run.\nDefaults to true for users on a single team.\n"
          },
          "conversation_id": {
            "type": "string",
            "description": "Optional conversation ID to continue an existing conversation.\nIf provided, the agent will continue from where the previous run left off.\n"
          },
          "attachments": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/AttachmentInput"
            },
            "description": "Optional file attachments to include with the prompt (max 5).\nAttachments are uploaded to cloud storage and made available to the agent.\n"
          },
          "interactive": {
            "type": "boolean",
            "description": "Whether the run should be interactive.\nIf not set, defaults to false.\n"
          }
        }
      },
      "AmbientAgentConfig": {
        "type": "object",
        "description": "Per-run configuration for a cloud agent. Controls which LLM model is used,\nwhich skill (SKILL.md) drives the agent's instructions, which environment\nthe agent executes in, any MCP servers to enable, and optional base prompt\noverrides. All fields are optional; when omitted, the agent uses the system\ndefault for each setting.\n",
        "properties": {
          "name": {
            "type": "string",
            "description": "Human-readable label for grouping, filtering, and traceability.\nAutomatically set to the skill name when running a skill-based agent.\nSet this explicitly to categorize runs by intent (e.g., \"nightly-dependency-check\")\nso you can filter and track them via the name query parameter on GET /agent/runs.\n"
          },
          "model_id": {
            "type": "string",
            "description": "LLM model to use (uses team default if not specified)"
          },
          "base_prompt": {
            "type": "string",
            "description": "Custom base prompt for the agent"
          },
          "environment_id": {
            "type": "string",
            "description": "UID of the environment to run the agent in"
          },
          "skill_spec": {
            "type": "string",
            "description": "Skill specification identifying which agent skill to use.\nFormat: \"{owner}/{repo}:{skill_path}\"\nExample: \"warpdotdev/warp-server:.claude/skills/deploy/SKILL.md\"\nUse the list agents endpoint to discover available skills.\n"
          },
          "mcp_servers": {
            "type": "object",
            "additionalProperties": {
              "$ref": "#/components/schemas/MCPServerConfig"
            },
            "description": "Map of MCP server configurations by name"
          },
          "computer_use_enabled": {
            "type": "boolean",
            "description": "Controls whether computer use is enabled for this agent.\nIf not set, defaults to false.\n"
          },
          "worker_host": {
            "type": "string",
            "description": "Self-hosted worker ID that should execute this task.\nIf not specified or set to \"warp\", the task runs on Warp-hosted workers.\n"
          }
        }
      },
      "MCPServerConfig": {
        "type": "object",
        "description": "Configuration for a single MCP (Model Context Protocol) server to attach to an agent run.\nExactly one of warp_id, command, or url must be provided, corresponding to the three\nsupported transports:\n- warp_id: reference a Warp-managed shared MCP server by UUID\n- command + args: launch a local stdio-based MCP server process\n- url: connect to a remote SSE or HTTP MCP server\n",
        "properties": {
          "warp_id": {
            "type": "string",
            "description": "Reference to a Warp shared MCP server by UUID"
          },
          "command": {
            "type": "string",
            "description": "Stdio transport - command to run"
          },
          "args": {
            "type": "array",
            "items": {
              "type": "string"
            },
            "description": "Stdio transport - command arguments"
          },
          "url": {
            "type": "string",
            "format": "uri",
            "description": "SSE/HTTP transport - server URL"
          },
          "env": {
            "type": "object",
            "additionalProperties": {
              "type": "string"
            },
            "description": "Environment variables for the server"
          },
          "headers": {
            "type": "object",
            "additionalProperties": {
              "type": "string"
            },
            "description": "HTTP headers for SSE/HTTP transport"
          }
        }
      },
      "AttachmentInput": {
        "type": "object",
        "description": "A base64-encoded file attachment to include with the prompt",
        "required": [
          "file_name",
          "mime_type",
          "data"
        ],
        "properties": {
          "file_name": {
            "type": "string",
            "description": "Name of the attached file"
          },
          "mime_type": {
            "type": "string",
            "description": "MIME type of the attachment.\nSupported image types: image/jpeg, image/png, image/gif, image/webp\n"
          },
          "data": {
            "type": "string",
            "fo"
          }
        }
      }
    }
  }
}
```

--------------------------------

### AgentListVariant Object Schema (OpenAPI)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure of the AgentListVariant object, representing a specific version of a skill. It includes a unique identifier, description, base prompt, source repository details, and available environments. This schema is part of the Oz Agent API.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "components": {
    "schemas": {
      "AgentListVariant": {
        "type": "object",
        "description": "A specific skill variant, uniquely identified by its skill path in a repository.\nEach variant carries its own instructions (base_prompt), source repository\nmetadata, and the list of environments it is available in.\n",
        "required": [
          "id",
          "description",
          "base_prompt",
          "source",
          "environments"
        ],
        "properties": {
          "id": {
            "type": "string",
            "description": "Stable identifier for this skill variant.\nFormat: \"{owner}/{repo}:{skill_path}\"\nExample: \"warpdotdev/warp-server:.claude/skills/deploy/SKILL.md\"\n"
          },
          "description": {
            "type": "string",
            "description": "Description of the agent variant"
          },
          "base_prompt": {
            "type": "string",
            "description": "Base prompt/instructions for the agent"
          },
          "source": {
            "$ref": "#/components/schemas/AgentListSource"
          },
          "environments": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/AgentListEnvironment"
            },
            "description": "Environments where this agent variant is available"
          },
          "last_run_timestamp": {
            "type": "string",
            "format": "date-time",
            "nullable": true,
            "description": "Timestamp of the last time this skill was run (RFC3339)"
          },
          "error": {
            "type": "string",
            "description": "Non-empty when the skill's SKILL.md file exists but is malformed.\nContains a description of the parse failure. Only present when\ninclude_malformed_skills=true is passed to the list agents endpoint.\n"
          }
        }
      },
      "AgentListSource": {
        "type": "object",
        "description": "Source repository metadata identifying where a skill variant is defined.",
        "required": [
          "owner",
          "name",
          "skill_path"
        ],
        "properties": {
          "owner": {
            "type": "string",
            "description": "GitHub repository owner"
          },
          "name": {
            "type": "string",
            "description": "GitHub repository name"
          },
          "skill_path": {
            "type": "string",
            "description": "Path to the skill definition file within the repository"
          }
        }
      },
      "AgentListEnvironment": {
        "type": "object",
        "description": "An environment in which a skill variant is available and can be executed.",
        "required": [
          "uid",
          "name"
        ],
        "properties": {
          "uid": {
            "type": "string",
            "description": "Unique identifier for the environment"
          },
          "name": {
            "type": "string",
            "description": "Human-readable name of the environment"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Worker Configuration Schemas

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting/managed-worker-reference

YAML configuration structures for defining worker behavior using either the Docker backend or the Direct backend.

```yaml
# Docker backend config
worker_id: "my-worker"
cleanup: true
max_concurrent_tasks: 4
idle_on_complete: "10m"
backend:
  docker:
    volumes:
      - "/data:/data:ro"
      - "/cache:/cache"
    environment:
      - name: NPM_TOKEN
        value: "your_token"
      - name: GITHUB_TOKEN  # inherits from host environment
```

```yaml
# Direct backend config
worker_id: "direct-worker"
max_concurrent_tasks: 2
backend:
  direct:
    workspace_root: "/var/lib/oz/workspaces"
    oz_path: "/usr/local/bin/oz"
    setup_command: "/opt/scripts/setup.sh"
    teardown_command: "/opt/scripts/teardown.sh"
    environment:
      - name: MY_VAR
        value: "hello"
```

--------------------------------

### Configure Grafana MCP Server

Source: https://docs.warp.dev/knowledge-and-collaboration/rules

Sets up Grafana integration using a Docker container for CLI execution or an SSE URL. Requires Grafana URL and API key for proper authentication.

```json
{
  "Grafana": {
    "command": "docker",
    "args": ["run","--rm","-i","-e","GRAFANA_URL","-e","GRAFANA_API_KEY","mcp/grafana","-t","stdio","-debug"],
    "env": {
      "GRAFANA_URL": "http://localhost:3000",
      "GRAFANA_API_KEY": "<your_grafana_key>"
    }
  }
}
```

```json
{
  "Grafana": {
    "url": "https://your-mcp-host.com/api/mcp/grafana/sse"
  }
}
```

--------------------------------

### List configured MCP servers

Source: https://docs.warp.dev/reference/cli/mcp-servers

Retrieves a list of all MCP servers currently configured in the user's Warp account, displaying their unique UUIDs and names.

```shell
oz mcp list
```

--------------------------------

### Reusing Saved Prompts with Warp Drive ID

Source: https://docs.warp.dev/reference/cli/warp-drive

This snippet demonstrates how to use a saved prompt from Warp Drive by providing its unique ID to the 'oz agent run' command. The ID is extracted from the Warp Drive sharing URL. This allows for consistent and repeatable prompt execution.

```bash
$ oz agent run --saved-prompt sgNpbUgDkmp2IImUVDc8kR
```

--------------------------------

### Zsh Prompt Configuration for Starship

Source: https://docs.warp.dev/terminal/appearance/prompt

A Zsh configuration snippet to restore the additional line after the Starship prompt. This is added to the user's .zshrc file.

```zsh
PROMPT="${PROMPT}"$'\n'

```

--------------------------------

### Define Agent Run Schema in OpenAPI

Source: https://docs.warp.dev/reference/api-and-sdk/agent

The OpenAPI schema defines the structure for creating a new agent run. It supports specifying prompts, skills, and detailed configurations like model selection, MCP server integration, and environment settings.

```json
{
  "RunAgentRequest": {
    "type": "object",
    "description": "Request body for creating a new agent run.",
    "properties": {
      "prompt": { "type": "string" },
      "skill": { "type": "string" },
      "config": { "$ref": "#/components/schemas/AmbientAgentConfig" },
      "title": { "type": "string" },
      "team": { "type": "boolean" },
      "conversation_id": { "type": "string" },
      "attachments": { "type": "array", "items": { "$ref": "#/components/schemas/AttachmentInput" } },
      "interactive": { "type": "boolean" }
    }
  }
}
```

--------------------------------

### Error Handling Schema

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Documentation regarding the standard error response format used across the Warp Dev API.

```APIDOC
## Internal Server Error

### Description
This endpoint returns a standardized error response when an unexpected condition occurs on the server.

### Method
N/A

### Endpoint
N/A

### Response
#### Error Response (500)
- **message** (string) - A description of the error encountered.
- **code** (string) - A machine-readable error identifier.

#### Response Example
{
  "message": "Internal server error",
  "code": "INTERNAL_SERVER_ERROR"
}
```

--------------------------------

### AgentListItem Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Represents a single agent, which is a skill with one or more variants. Variants can come from different repositories or environments.

```APIDOC
## AgentListItem Object

### Description
A skill with one or more variants. Variants represent different versions of the same skill sourced from different repositories or environments.

### Schema
```json
{
  "name": "string",
  "variants": [
    {
      "$ref": "#/components/schemas/AgentListVariant"
    }
  ]
}
```

### Properties
- **name** (string) - Required - Human-readable name of the agent
- **variants** (array[AgentListVariant]) - Required - Available variants of this agent
```

--------------------------------

### Create Bitbucket API Token Secret with Oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/bitbucket

This command creates a team-scoped secret named BITBUCKET_API_TOKEN using the Oz CLI. The token value is securely stored and encrypted by Warp, and it will be injected as an environment variable at runtime. This is the minimum required scope to clone a repository.

```bash
oz secret create --team BITBUCKET_API_TOKEN
```

--------------------------------

### Collect and archive Warp crash reports on macOS

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

Searches the system diagnostic reports directory for files containing the Warp bundle identifier and zips them to the Desktop. It handles the absence of files gracefully.

```bash
files=$(find ~/Library/Logs/DiagnosticReports -name "*.ips" -exec grep -l "dev\.warp" {} + 2>/dev/null) && [ -n "$files" ] && echo "$files" | xargs zip -j ~/Desktop/warp-crash-logs.zip || echo "No Warp crash reports found."
```

--------------------------------

### Remove Warp Preview User Files and Logs (Shell)

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/logging-out-and-uninstalling

This command removes user-specific files, logs, databases, and codebase context for Warp Preview. It operates on the XDG_STATE_HOME directory, defaulting to ~/.local/state. Ensure you have backed up any necessary data before execution.

```shell
rm -r ${XDG_STATE_HOME:-$HOME/.local/state}/warp-terminal-preview
```

--------------------------------

### Uninstall Warp and Remove Data on Linux

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/logging-out-and-uninstalling

Commands to uninstall Warp via various package managers and remove configuration and state directories following XDG standards.

```bash
# apt uninstall
sudo apt remove warp-terminal
# dnf uninstall
sudo dnf remove warp-terminal
# zypper uninstall
sudo zypper remove warp-terminal
# pacman uninstall
sudo pacman -R warp-terminal

# Remove Warp settings files
rm -r ${XDG_CONFIG_HOME:-$HOME/.config}/warp-terminal
# Remove Warp user files, logs, database, codebase context, and mcp logs
rm -r ${XDG_STATE_HOME:-$HOME/.local/state}/warp-terminal
# Remove Warp themes and launch configurations
rm -r ${XDG_STATE_HOME:-$HOME/.local/share}/warp-terminal
```

--------------------------------

### Send Desktop Notification (OSC 9 - Body Only) in Bash/Zsh

Source: https://docs.warp.dev/terminal/more-features/notifications

This snippet demonstrates how to send a desktop notification with only a body using the OSC 9 escape sequence in bash or zsh. It utilizes the printf command to output the escape sequence followed by the notification body and the BEL character.

```bash
printf '\033]9;Build complete\007'
```

```zsh
printf '\033]9;Build complete\007'
```

--------------------------------

### Scheduled Agent Item Object

Source: https://docs.warp.dev/reference/api-and-sdk/models

Details about an individual scheduled agent.

```APIDOC
## Scheduled Agent Item Object

### Description
Represents a single scheduled agent with its configuration and status.

### Properties
- **id** (string) - Unique identifier for the scheduled agent.
- **name** (string) - Human-readable name for the schedule.
- **cron_schedule** (string) - Cron expression defining when the agent runs (e.g., "0 9 * * *" for daily at 9am UTC).
- **enabled** (boolean) - Whether the schedule is currently active.
- **prompt** (string) - The prompt/instruction for the agent to execute.
- **last_spawn_error** (string, nullable) - Error message from the last failed spawn attempt, if any.
- **agent_config** (object) - Per-run configuration for a cloud agent. See `AmbientAgentConfig`.
- **environment** (object) - Resolved environment configuration (if agent_config references an environment_id). See `CloudEnvironmentConfig`.
- **created_at** (string, format: date-time) - Timestamp when the schedule was created (RFC3339).
- **updated_at** (string, format: date-time) - Timestamp when the schedule was last updated (RFC3339).
- **created_by** (object) - Information about the user who created the schedule. See `RunCreatorInfo`.
- **updated_by** (object) - Information about the user who last updated the schedule. See `RunCreatorInfo`.
- **history** (object) - History of the scheduled agent runs. See `ScheduledAgentHistoryItem`.
- **scope** (object) - Scope of the scheduled agent. See `Scope`.
```

--------------------------------

### Manage Warp secrets for Bitbucket authentication

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/bitbucket

Commands to create and update secure secrets within the Warp platform. These secrets are injected as environment variables at runtime, preventing exposure in logs or configuration files.

```bash
oz secret create --team BITBUCKET_TOKEN
oz secret update --value BITBUCKET_TOKEN
```

--------------------------------

### AgentSkill Schema

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Provides information about an agent skill used for a run.

```APIDOC
## AgentSkill Schema

### Description
Information about the agent skill used for the run.
Either `full_path` or `bundled_skill_id` will be set, but not both.

### Properties
- **name** (string) - Optional - Human-readable name of the skill.
- **description** (string) - Optional - Description of the skill.
- **full_path** (string) - Optional - Path to the SKILL.md file (for file-based skills).
- **bundled_skill_id** (string) - Optional - Unique identifier for bundled skills.

### Example
```json
{
  "name": "Code Review Skill",
  "description": "Analyzes code for potential issues.",
  "full_path": "/skills/code_review/SKILL.md"
}
```
```

--------------------------------

### Running Agents Remotely

Source: https://docs.warp.dev/reference/cli/cli

Dispatch agent tasks to remote environments using `oz agent run-cloud`. This is suitable for background processing, standardized team configurations, and remote execution.

```APIDOC
## Running Agents Remotely

### Description
Dispatch agent tasks to remote environments using `oz agent run-cloud`. This is suitable for background processing, standardized team configurations, and remote execution.

### Method
CLI Command

### Endpoint
`oz agent run-cloud`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

**Key flags**

*   `--environment <ENVIRONMENT_ID>` (`-e`) - Select the environment to run in.
*   `--no-environment` - Run without an environment (not recommended).
*   `--open` - View the agent's session in Warp once it's available.
*   `--name <NAME>` (`-n`) - Label the run for grouping and traceability.
*   `--mcp <SPEC>` - Start one or more MCP servers before execution. Can be repeated.
*   `--model <MODEL_ID>` - Override the default model.
*   `--skill <SPEC>` - Use a skill from the environment's repository as the base prompt.
*   `--host <WORKER_ID>` - Run on a specific self-hosted worker.
*   `--attach <PATH>` - Attach an image file to the agent query. Can be repeated (maximum 5).
*   `--computer-use` / `--no-computer-use` - Enable or disable Computer Use for this run.
*   `--file <PATH>` (`-f`) - Load run configuration from a YAML or JSON file.

**Key differences from `run`**

*   No `--cwd` — the environment determines the working directory.
*   No `--share` — sharing options are on `run`, not `run-cloud`.
*   No `--profile` — cloud runs do not use agent profiles.

### Request Example
```sh
oz agent run-cloud \
  --environment <ENVIRONMENT_ID> \
  --name "Repo summary" \
  --prompt "Summarize this repo and list the top 5 risky areas" \
  --open
```

### Response
#### Success Response (200)
Cloud runs dispatch tasks to remote environments. The agent execution status and results will be available in the Warp UI or via API.

#### Response Example
None provided, as execution is remote.
```

--------------------------------

### Scope Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the ownership scope for a resource, indicating whether it is personal or team-owned.

```APIDOC
## Scope Object

### Description
Specifies the ownership context for a resource, supporting both user-level and team-level ownership.

### Properties
- **type** (string, enum: ["User", "Team"]) - Required - Type of ownership.
- **uid** (string) - Optional - UID of the owning user or team.

### Example
{
  "type": "Team",
  "uid": "team_12345"
}
```

--------------------------------

### ArtifactItem Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for an artifact produced during an agent run. It's a discriminated union based on the 'artifact_type' field.

```APIDOC
## ArtifactItem Schema

### Description
A discriminated union representing an artifact produced during an agent run.
The `artifact_type` field determines which variant is present: PLAN, PULL_REQUEST, or SCREENSHOT. Each variant carries a data object with type-specific fields.

### Properties
- **artifact_type** (string) - Required - The type of the artifact (PLAN, PULL_REQUEST, SCREENSHOT).
- **created_at** (string) - Required - Timestamp when the artifact was created (RFC3339).
- **data** (object) - Required - Type-specific data for the artifact.
  - **PlanArtifactData**
    - **document_uid** (string) - Required - Unique identifier for the plan document.
    - **notebook_uid** (string) - Optional - Unique identifier for the associated notebook.
    - **title** (string) - Optional - Title of the plan.
  - **PullRequestArtifactData**
    - **url** (string) - Required - URL of the pull request.
    - **branch** (string) - Required - Branch name for the pull request.
  - **ScreenshotArtifactData**
    - **artifact_uid** (string) - Required - Unique identifier for the screenshot artifact.
    - **mime_type** (string) - Required - MIME type of the screenshot image.
    - **description** (string) - Optional - Description of the screenshot.
```

--------------------------------

### Error: insufficient_credits

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/insufficient-credits

Details regarding the 403 Forbidden error triggered when team credit limits are reached.

```APIDOC
## 403 Forbidden: insufficient_credits

### Description
This error occurs when a team has no remaining add-on credits to execute cloud agents or integrations. It prevents new tasks from starting until credits are replenished.

### Method
N/A (Error Response)

### Endpoint
/api/v1/agent/tasks

### Response
#### Success Response (N/A)
- This is an error state, not a successful operation.

#### Error Response (403)
- **type** (string) - URI reference to the error documentation.
- **title** (string) - Human-readable summary of the error.
- **status** (integer) - The HTTP status code (403).
- **instance** (string) - The endpoint path where the error occurred.
- **error** (string) - Detailed error message.
- **retryable** (boolean) - Indicates if the request can be retried (false).
- **trace_id** (string) - Unique identifier for the request trace.

### Response Example
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/insufficient-credits",
  "title": "Your team has run out of add-on credits. Purchase more credits in your team's billing settings to continue.",
  "status": 403,
  "instance": "/api/v1/agent/tasks",
  "error": "Your team has run out of add-on credits. Purchase more credits in your team's billing settings to continue.",
  "retryable": false,
  "trace_id": "abc123..."
}
```

--------------------------------

### Deploy Warp Agent in Kubernetes

Source: https://docs.warp.dev/agent-platform/cloud-agents/self-hosting

A Kubernetes Job configuration to run a Warp agent within a pod. It requires a WARP_API_KEY stored in a Kubernetes secret for authentication.

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: oz-agent-task
spec:
  template:
    spec:
      containers:
      - name: oz-agent
        image: warpdotdev/warp-agent:latest
        command: ["agent", "run", "--prompt", "Run the test suite and report failures"]
        env:
        - name: WARP_API_KEY
          valueFrom:
            secretKeyRef:
              name: warp-credentials
              key: api-key
      restartPolicy: Never
```

--------------------------------

### Send Desktop Notification (OSC 777 - Title + Body) in Bash/Zsh

Source: https://docs.warp.dev/terminal/more-features/notifications

This snippet shows how to send a desktop notification with both a title and body using the OSC 777 escape sequence in bash or zsh. The printf command is used to construct the escape sequence, specifying 'notify', the title, and the body, terminated by the BEL character.

```bash
printf '\033]777;notify;Deploy;Success on prod\007'
```

```zsh
printf '\033]777;notify;Deploy;Success on prod\007'
```

--------------------------------

### Conditionally disable shell configurations for Warp

Source: https://docs.warp.dev/terminal/appearance/prompt

Provides a template for wrapping shell configurations in a conditional block to ensure they only execute when the terminal is not Warp.

```bash
if [[ $TERM_PROGRAM != "WarpTerminal" ]]; then
##### WHAT YOU WANT TO DISABLE FOR WARP - BELOW

    # Unsupported Custom Prompt Code

##### WHAT YOU WANT TO DISABLE FOR WARP - ABOVE
fi
```

--------------------------------

### RunCreatorInfo Object

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Identity information about the principal that created a run or scheduled agent.

```APIDOC
## RunCreatorInfo Object

### Description
Identity information about the principal (user or service account) that created a run or scheduled agent. Present when the creator information is available.

### Properties
- **type** (string) - Type of the creator principal. Enum: `user`, `service_account`.
- **uid** (string) - Unique identifier of the creator.
- **display_name** (string) - Display name of the creator.
- **email** (string) - Email address of the creator.
- **photo_url** (string, uri) - URL to the creator's photo.
```

--------------------------------

### Starship Configuration for Warp

Source: https://docs.warp.dev/terminal/appearance/prompt

Configuration snippets for Starship to resolve known errors in Warp. This includes disabling custom modules and multi-line prompts for specific shells.

```toml
# Get editor completions based on the config schema
'' = 'https://starship.rs/config-schema.json'

# Disables the custom module
[custom]
disabled = false

```

```toml
[line_break]
disabled = true

```

--------------------------------

### Provision AWS Bedrock IAM Policy

Source: https://docs.warp.dev/enterprise/enterprise-features/bring-your-own-llm

Defines the minimum IAM policy required for Warp to invoke models on AWS Bedrock. This policy grants permissions for model invocation and response streaming using global inference profiles.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "BedrockModelAccess",
      "Effect": "Allow",
      "Action": [
        "bedrock:InvokeModel",
        "bedrock:InvokeModelWithResponseStream"
      ],
      "Resource": [
        "arn:aws:bedrock:*::foundation-model/*",
        "arn:aws:bedrock:*:*:inference-profile/*",
        "arn:aws:bedrock:*:*:application-inference-profile/*"
      ]
    }
  ]
}
```

--------------------------------

### Prompting Warp Agent for Icon Replacement (Rust)

Source: https://docs.warp.dev/university/developer-workflows/frontend-ui/how-to-replace-a-ui-element-in-warp-rust-codebase

This prompt instructs the Warp AI agent to replace all instances of a 'sparkle icon' with a new 'agent icon' within the Rust codebase, specifically mentioning the history menu. It also requests the agent to create a new branch and provide a plan before making changes.

```text
Please create a new branch for me according to the format in the attached Linear URL.

I’ve attached screenshots of what the agent mode and sparkle icons look like.
I would like you to understand those icons, search for their use in the code,
and wherever we’re using sparkles, replace them with the agent mode icon.
Specifically, make sure this happens in the history menu.
Please give me a plan before making any coding changes.
```

--------------------------------

### Configure Puppeteer MCP Server

Source: https://docs.warp.dev/university/mcp-servers/puppeteer-mcp-scraping-amazon-web-reviews

The JSON configuration required to register the Puppeteer MCP server within the Warp MCP panel. It specifies the command and arguments needed to initialize the server via npx.

```json
{
  "puppeteer": {
    "command": "npx",
    "args": [
      "-y",
      "@modelcontextprotocol/server-puppeteer"
    ],
    "env": {},
    "working_directory": null
  }
}
```

--------------------------------

### Define Agent Run Request Schema

Source: https://docs.warp.dev/reference/api-and-sdk/agent

The RunAgentRequest schema defines the payload for creating a new agent task. It supports optional configurations for LLM models, environment settings, and MCP server attachments.

```json
{
  "type": "object",
  "description": "Request body for creating a new agent run.",
  "properties": {
    "prompt": { "type": "string" },
    "skill": { "type": "string" },
    "config": { "$ref": "#/components/schemas/AmbientAgentConfig" },
    "title": { "type": "string" },
    "team": { "type": "boolean" },
    "conversation_id": { "type": "string" },
    "attachments": { "type": "array" },
    "interactive": { "type": "boolean" }
  }
}
```

--------------------------------

### Conditionally Disable Shell Configurations for Warp

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

Use these conditional blocks in your shell profile files to prevent incompatible plugins or prompts from loading specifically when the terminal is identified as Warp. This helps isolate and resolve startup issues caused by conflicting shell integrations.

```fish
if test "$TERM_PROGRAM" != "WarpTerminal"
    ##### WHAT YOU WANT TO DISABLE FOR WARP - BELOW
    # Unsupported plugin/prompt code here
    ##### WHAT YOU WANT TO DISABLE FOR WARP - ABOVE
end
```

```powershell
if ($env:TERM_PROGRAM -ne "WarpTerminal") {
    ##### WHAT YOU WANT TO DISABLE FOR WARP - BELOW
    # Unsupported plugin/prompt code here
    ##### WHAT YOU WANT TO DISABLE FOR WARP - ABOVE
}
```

--------------------------------

### Pause Scheduled Agent - OpenAPI Specification

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

This OpenAPI 3.0.0 specification defines the structure for pausing a scheduled agent. It includes details about the API endpoint, request/response formats, and security schemes.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "tags": [
    {
      "name": "schedules",
      "description": "Operations for creating and managing scheduled agents"
    }
  ],
  "servers": [
    {
      "url": "https://app.warp.dev/api/v1",
      "description": "Production server"
    }
  ],
  "security": [
    {
      "bearerAuth": []
    }
  ],
  "components": {
    "securitySchemes": {
      "bearerAuth": {
        "type": "http",
        "scheme": "bearer",
        "description": "Authentication via personal API key or service account credentials.\n"
      }
    },
    "schemas": {
      "ScheduledAgentItem": {
        "type": "object",
        "required": [
          "id",
          "name",
          "cron_schedule",
          "enabled",
          "prompt",
          "created_at",
          "updated_at"
        ],
        "properties": {
          "id": {
            "type": "string",
            "description": "Unique identifier for the scheduled agent"
          },
          "name": {
            "type": "string",
            "description": "Human-readable name for the schedule"
          },
          "cron_schedule": {
            "type": "string",
            "description": "Cron expression defining when the agent runs (e.g., \"0 9 * * *\" for daily at 9am UTC)"
          },
          "enabled": {
            "type": "boolean",
            "description": "Whether the schedule is currently active"
          },
          "prompt": {
            "type": "string",
            "description": "The prompt/instruction for the agent to execute"
          },
          "last_spawn_error": {
            "type": "string",
            "nullable": true,
            "description": "Error message from the last failed spawn attempt, if any"
          },
          "agent_config": {
            "$ref": "#/components/schemas/AmbientAgentConfig"
          },
          "environment": {
            "allOf": [
              {
                "$ref": "#/components/schemas/CloudEnvironmentConfig"
              }
            ],
            "description": "Resolved environment configuration (if agent_config references an environment_id)"
          },
          "created_at": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the schedule was created (RFC3339)"
          },
          "updated_at": {
            "type": "string",
            "format": "date-time",
            "description": "Timestamp when the schedule was last updated (RFC3339)"
          },
          "created_by": {
            "$ref": "#/components/schemas/RunCreatorInfo"
          },
          "updated_by": {
            "$ref": "#/components/schemas/RunCreatorInfo"
          },
          "history": {
            "$ref": "#/components/schemas/ScheduledAgentHistoryItem"
          },
          "scope": {
            "$ref": "#/components/schemas/Scope"
          }
        }
      },
      "AmbientAgentConfig": {
        "type": "object",
        "description": "Per-run configuration for a cloud agent. Controls which LLM model is used,\nwhich skill (SKILL.md) drives the agent's instructions, which environment\nthe agent executes in, any MCP servers to enable, and optional base prompt\noverrides. All fields are optional; when omitted, the agent uses the system\ndefault for each setting.\n",
        "properties": {
          "name": {
            "type": "string",
            "description": "Human-readable label for grouping, filtering, and traceability.\nAutomatically set to the skill name when running a skill-based agent.\nSet this explicitly to categorize runs by intent (e.g., \"nightly-dependency-check\")\nso you can filter and track them via the name query parameter on GET /agent/runs.\n"
          },
          "model_id": {
            "type": "string",
            "description": "LLM model to use (uses team default if not specified)"
          },
          "base_prompt": {
            "type": "string",
            "description": "Custom base prompt for the agent"
          },
          "environment_id": {
            "type": "string",
            "description": "UID of the environment to run the agent in"
          },
          "skill_spec": {
            "type": "string",
            "description": "Skill specification identifying which agent skill to use.\nFormat: \"{owner}/{repo}:{skill_path}\"\nExample: \"warpdotdev/warp-server:.claude/skills/deploy/SKILL.md\"\nUse the list agents endpoint to discover available skills.\n"
          },
          "mcp_servers": {
            "type": "object",
            "additionalProperties": {
              "$ref": "#/components/schemas/MCPServerConfig"
            },
            "description": "Map of MCP server configurations by name"
          },
          "computer_use_enabled": {
            "type": "boolean",
            "description": "Controls whether computer use is enabled for this agent.\nIf not set, defaults to false.\n"
          },
          "worker_host": {
            "type": "string",
            "description": "Self-hosted worker ID that should execute this task.\nIf not specified or set to \"warp\", the task runs on Warp-hosted workers.\n"
          }
        }
      },
      "MCPServerConfig": {
        "type": "object",
        "description": "Configuration for a single MCP (Model Context Protocol) server to attach to an agent run.\nExactly one of warp_id, command, or url must be provided, corresponding to the three\nsupported transports:\n- warp_id: reference a Warp-managed shared MCP server by UUID\n- command + args: launch a local stdio-based MCP server process\n- url: connect to a remote SSE or HTTP MCP server\n",
        "properties": {
          "warp_id": {
            "type": "string",
            "description": "Reference to a Warp shared MCP server by UUID"
          },
          "command": {
            "type": "string",
            "description": "Stdio transport - command to run"
          },
          "args": {
            "type": "array",
            "items": {
              "type": "string"
            },
            "description": "Stdio transport - command arguments"
          },
          "url": {
            "type": "string",
            "format": "uri",
            "description": "SSE/HTTP transport - server URL"
          },
          "env": {
            "type": "object",
            "additionalProperties": {
              "type": "string"
            },
            "description": "Environment variables for the server"
          },
          "headers": {
            "type": "object",
            "additionalProperties": {
              "type": "string"
            },
            "description": "HTTP headers for SSE/HTTP transport"
          }
        }
      },
      "CloudEnvironmentConfig": {
        "type": "object",
        "description": "Configuration for a cloud environment used by"
      }
    }
  }
}
```

--------------------------------

### Environment variables on remote machines

Source: https://docs.warp.dev/reference/cli/mcp-for-cloud-agents

When running agents on remote machines, environment variables used in MCP configurations are not synced. They must be set manually or managed using secrets.

```APIDOC
## Environment variables on remote machines

Warp syncs MCP server configuration between machines logged in with your Warp account, but **does not** sync the environment variables used in that configuration. When running on a remote machine, set any required secrets manually before running the agent:

```
export MY_MCP_SERVER_ACCESS_TOKEN="..."
$ oz agent run --mcp "904a8936-fa82-4571-b1d6-166c26197981" --prompt "use my MCP server to check for errors"
```

For cloud agent workflows, use Oz-managed secrets to store and inject credentials safely — secrets are stored in the cloud and referenced by name in your config. For local runs, a secrets manager CLI such as `op`, `pass`, or `gcloud secrets versions access` can fetch secrets on remote hosts without exposing them in your shell history.
```

--------------------------------

### Zip Warp Logs on Windows

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/sending-us-feedback

This PowerShell command compresses Warp log files located in the user's local app data directory and saves the zip archive to the Desktop. It requires Warp to be closed before execution. The command uses the Compress-Archive cmdlet.

```powershell
Compress-Archive -Path "$env:LOCALAPPDATA\warp\Warp\data\logs\warp.log*" -DestinationPath "$([Environment]::GetFolderPath('Desktop'))\warp-logs.zip"
```

--------------------------------

### Uninstall Warp and Remove Data on Windows

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/logging-out-and-uninstalling

PowerShell commands to uninstall Warp via WinGet and remove registry keys, local app data, and roaming configuration files.

```powershell
winget uninstall Warp.Warp
# Remove Warp settings in the Windows Registry
Remove-Item -Path "HKCU:\Software\Warp.dev\Warp" -Recurse -Force
# Remove Warp user files, logs, database, codebase context, and mcp logs
Remove-Item -Path "$env:LOCALAPPDATA\warp\Warp" -Recurse -Force
# Remove Warp themes and launch configurations
Remove-Item -Path "$env:APPDATA\warp\Warp" -Recurse -Force
```

```powershell
# Remove Warp Preview settings in the Windows Registry
Remove-Item -Path "HKCU:\Software\Warp.dev\Warp-Preview" -Recurse -Force
# Remove Warp Preview user files, logs, database, codebase context, and mcp logs
Remove-Item -Path "$env:LOCALAPPDATA\warp\Warp-Preview" -Recurse -Force
# Remove Warp Preview themes and launch configurations
Remove-Item -Path "$env:APPDATA\warp\Warp-Preview" -Recurse -Force
```

--------------------------------

### Update Secret Description with oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/secrets

Updates the description of an existing secret. This is useful for adding metadata, such as rotation dates or ownership, to secrets without changing their values.

```bash
oz secret update --team \
  --description "Rotated 2026-02-26; owned by platform team" \
  METABASE_API_KEY
```

--------------------------------

### Define CreateScheduledAgentRequest OpenAPI Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

The CreateScheduledAgentRequest schema defines the structure for scheduling agents, requiring a name and cron expression. It supports optional configurations for agent behavior and team ownership via the AmbientAgentConfig object.

```json
{
  "type": "object",
  "description": "Request body for creating a new scheduled agent.",
  "required": ["name", "cron_schedule"],
  "properties": {
    "name": { "type": "string" },
    "cron_schedule": { "type": "string" },
    "prompt": { "type": "string" },
    "enabled": { "type": "boolean", "default": true },
    "agent_config": { "$ref": "#/components/schemas/AmbientAgentConfig" },
    "team": { "type": "boolean" }
  }
}
```

--------------------------------

### Analyze Cloud Run Logs via Warp MCP

Source: https://docs.warp.dev/university/mcp-servers/linear-mcp-updating-tickets-with-a-lean-build-approach

This prompt instructs the Warp agent to retrieve logs from a specific Google Cloud project, categorize them by severity, and generate a histogram of message types to identify critical errors.

```text
Use the warp-server-staging gcloud project and pull logs for the last 10 minutes from the warp-server Cloud Run instance.
Organize them by info, warning, and error levels.
Create a histogram across message types, and highlight the most concerning errors to investigate.
```

--------------------------------

### ScheduledAgentHistoryItem Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for scheduler-derived history metadata associated with a scheduled agent.

```APIDOC
## ScheduledAgentHistoryItem Object

### Description
Represents the history metadata for a scheduled agent, including timestamps for the last execution and the upcoming scheduled run.

### Properties
- **last_ran** (string, date-time) - Optional - Timestamp of the last successful run (RFC3339).
- **next_run** (string, date-time) - Optional - Timestamp of the next scheduled run (RFC3339).

### Example
{
  "last_ran": "2023-10-27T10:00:00Z",
  "next_run": "2023-10-28T10:00:00Z"
}
```

--------------------------------

### Conditionally Disable Configurations for Warp (Fish)

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

This Fish shell snippet provides a method to conditionally disable configurations or plugins that are incompatible with Warp Terminal. By checking the TERM_PROGRAM environment variable, it ensures that certain code is only applied when not running within Warp, facilitating the debugging of RC file issues.

```fish
# fish (See config.fish)
if status --is-interactive; and test "$TERM_PROGRAM" != "WarpTerminal"
##### WHAT YOU WANT TO DISABLE FOR WARP - BELOW
    # Unsupported plugin/prompt code here
##### WHAT YOU WANT TO DISABLE FOR WARP - ABOVE
end

```

--------------------------------

### Locate MCP Logs on Linux

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

This command changes the directory to where Warp stores MCP logs on Linux. Reviewing these logs can help in diagnosing server-related issues.

```bash
cd "${XDG_STATE_HOME:-$HOME/.local/state}/warp-terminal/mcp"
```

--------------------------------

### Follow-up Prompt for Function Renaming (Rust)

Source: https://docs.warp.dev/university/developer-workflows/frontend-ui/how-to-replace-a-ui-element-in-warp-rust-codebase

This follow-up prompt instructs the Warp AI agent to proceed with the planned code changes and specifically rename a function from 'renderAISparklesIcon' to 'renderAgentModeIcon'. This ensures that not only the icon references but also related function names are updated.

```text
Yes, proceed — and please rename the function from renderAISparklesIcon
to something like renderAgentModeIcon.
```

--------------------------------

### Define ScheduledAgentHistoryItem Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for tracking the execution history of scheduled agents. It includes RFC3339 formatted timestamps for the last successful run and the upcoming scheduled execution.

```json
{
  "type": "object",
  "description": "Scheduler-derived history metadata for a scheduled agent",
  "properties": {
    "last_ran": {
      "type": "string",
      "format": "date-time",
      "nullable": true,
      "description": "Timestamp of the last successful run (RFC3339)"
    },
    "next_run": {
      "type": "string",
      "format": "date-time",
      "nullable": true,
      "description": "Timestamp of the next scheduled run (RFC3339)"
    }
  }
}
```

--------------------------------

### ListScheduledAgentsResponse Object Schema (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure of the response object containing a list of scheduled agents accessible to the authenticated user. It includes a 'schedules' array, where each item is a ScheduledAgentItem.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "components": {
    "schemas": {
      "ListScheduledAgentsResponse": {
        "type": "object",
        "description": "Response containing all scheduled agents accessible to the authenticated user, sorted alphabetically by name.",
        "required": [
          "schedules"
        ],
        "properties": {
          "schedules": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/ScheduledAgentItem"
            },
            "description": "List of scheduled agents"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Custom Theme YAML Structure

Source: https://docs.warp.dev/terminal/appearance/custom-themes

Defines the structure of a custom theme file in YAML format for Warp Terminal. It specifies essential properties like name, colors, and terminal color schemes.

```yaml
name: Custom Theme # Name for the theme
accent: '#268bd2' # Accent color for UI elements
cursor: '#95D886' # Input cursor color (optional; defaults to accent color if omitted)
background: '#002b36' # Terminal background color
foreground: '#839496' # The foreground color
details: darker # Whether the theme is lighter or darker
terminal_colors: # Ansi escape colors
  bright:
    black: '#002b36'
    blue: '#839496'
    cyan: '#93a1a1'
    green: '#586e75'
    magenta: '#6c71c4'
    red: '#cb4b16'
    white: '#fdf6e3'
    yellow: '#657b83'
  normal:
    black: '#073642'
    blue: '#268bd2'
    cyan: '#2aa198'
    green: '#859900'
    magenta: '#d33682'
    red: '#dc322f'
    white: '#eee8d5'
    yellow: '#b58900'
```

--------------------------------

### Update Secret Value from File with oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/secrets

Updates a secret's value using content from a specified file. This is the recommended method for rotating credentials securely, as it avoids exposing the secret in shell history.

```bash
oz secret update --team \
  --value-file new_api_key.txt \
  METABASE_API_KEY
```

--------------------------------

### POST /schedules/{id}/pause

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Pauses a scheduled agent by setting its enabled flag to false, preventing it from running until resumed.

```APIDOC
## POST /schedules/{id}/pause

### Description
Pauses a scheduled agent. The agent will not run until resumed. This sets the enabled flag to false.

### Method
POST

### Endpoint
https://app.warp.dev/api/v1/schedules/{id}/pause

### Parameters
#### Path Parameters
- **id** (string) - Required - Unique identifier for the scheduled agent

### Request Example
{}

### Response
#### Success Response (200)
- **id** (string) - Unique identifier for the scheduled agent
- **enabled** (boolean) - The updated status of the schedule (false)

#### Response Example
{
  "id": "agent-123",
  "enabled": false
}
```

--------------------------------

### YAML Configuration for Accent Gradient (Top/Bottom) in Warp Theme

Source: https://docs.warp.dev/terminal/appearance/custom-themes

This YAML snippet demonstrates how to set a vertical gradient for the accent color in a Warp theme. It utilizes 'top' and 'bottom' keys to specify the gradient's color progression from top to bottom.

```yaml
accent:
  top: '#abcdef'
  bottom: '#fedcba'
```

--------------------------------

### Access Warp Session Restoration Database (macOS, Windows, Linux)

Source: https://docs.warp.dev/terminal/sessions/session-restoration

These commands allow you to access the SQLite database where Warp stores session restoration data. The specific path to the database varies by operating system.

```bash
sqlite3 "$HOME/Library/Group Containers/2BBY89MBSN.dev.warp/Library/Application Support/dev.warp.Warp-Stable/warp.sqlite"
```

```powershell
sqlite3 $env:LOCALAPPDATA\warp\Warp\data\warp.sqlite
```

```bash
sqlite3 "${XDG_STATE_HOME:-$HOME/.local/state}/warp-terminal/warp.sqlite"
```

--------------------------------

### Update Scheduled Agent OpenAPI Schema

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Defines the request structure for updating a scheduled agent. Requires name, cron_schedule, and enabled status, while allowing optional agent_config overrides.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "components": {
    "schemas": {
      "UpdateScheduledAgentRequest": {
        "type": "object",
        "description": "Request body for updating a scheduled agent.",
        "required": ["name", "cron_schedule", "enabled"],
        "properties": {
          "name": { "type": "string" },
          "cron_schedule": { "type": "string" },
          "prompt": { "type": "string" },
          "enabled": { "type": "boolean" },
          "agent_config": { "$ref": "#/components/schemas/AmbientAgentConfig" }
        }
      }
    }
  }
}
```

--------------------------------

### Error Object Definition (JSON Schema)

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the structure for error responses, adhering to RFC 7807 (Problem Details for HTTP APIs). It includes standard fields like 'type', 'title', 'status', and 'error', along with optional fields for more detailed error information and retry guidance.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "components": {
    "schemas": {
      "Error": {
        "type": "object",
        "description": "Error response following RFC 7807 (Problem Details for HTTP APIs).\nIncludes backward-compatible extension members.\n\nThe response uses the `application/problem+json` content type.\nAdditional extension members (e.g., `auth_url`, `provider`) may be\npresent depending on the error code.\n",
        "required": [
          "type",
          "title",
          "status",
          "error"
        ],
        "properties": {
          "type": {
            "type": "string",
            "format": "uri",
            "description": "A URI reference that identifies the problem type (RFC 7807).\nFormat: `https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/{error_code}`\nSee PlatformErrorCode for the list of possible error codes.\n"
          },
          "title": {
            "type": "string",
            "description": "A short, human-readable summary of the problem type (RFC 7807)"
          },
          "status": {
            "type": "integer",
            "description": "The HTTP status code for this occurrence of the problem (RFC 7807)"
          },
          "detail": {
            "type": "string",
            "description": "A human-readable explanation specific to this occurrence of the problem (RFC 7807)"
          },
          "instance": {
            "type": "string",
            "description": "The request path that generated this error (RFC 7807)"
          },
          "error": {
            "type": "string",
            "description": "Human-readable error message combining title and detail.\nBackward-compatible extension member for older clients.\n"
          },
          "retryable": {
            "type": "boolean",
            "description": "Whether the request can be retried. When true, the error is transient\nand the request may be retried. When false, retrying without addressing\nthe underlying cause will not succeed.\n"
          },
          "trace_id": {
            "type": "string",
            "description": "OpenTelemetry trace ID for debugging and support requests"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Define Oz Agent API Schema

Source: https://docs.warp.dev/reference/api-and-sdk/agent

This OpenAPI 3.0.0 specification defines the structure for the Oz Agent API. It includes schemas for listing agents, their variants, source metadata, and error handling protocols.

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Oz Agent API",
    "version": "1.0.0"
  },
  "tags": [
    {
      "name": "agent",
      "description": "Operations for running and managing cloud agents"
    }
  ],
  "servers": [
    {
      "url": "https://app.warp.dev/api/v1",
      "description": "Production server"
    }
  ],
  "security": [
    {
      "bearerAuth": []
    }
  ],
  "components": {
    "securitySchemes": {
      "bearerAuth": {
        "type": "http",
        "scheme": "bearer",
        "description": "Authentication via personal API key or service account credentials.\n"
      }
    },
    "schemas": {
      "ListAgentsResponse": {
        "type": "object",
        "description": "Response containing available skills discoverable from the authenticated user's environments or a specific repository.",
        "required": ["agents"],
        "properties": {
          "agents": {
            "type": "array",
            "items": { "$ref": "#/components/schemas/AgentListItem" },
            "description": "List of available agents"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Configure Multi-line Shell Prompts

Source: https://docs.warp.dev/terminal/appearance/prompt

Commands to append a newline to the primary shell prompt for various environments including Bash, Zsh, Fish, PowerShell, and popular prompt frameworks like Starship.

```bash
echo -e '\nPS1="${PS1}"$'\''\n'\''' >> ~/.bashrc
```

```zsh
echo -e '\nPROMPT="${PROMPT}"$'\''\n'\''' >> ~/.zshrc
```

```fish
echo -e '\nfunctions --copy fish_prompt fish_prompt_orig; function fish_prompt; fish_prompt_orig; echo; end' >> ~/.config/fish/config.fish
```

```powershell
$rawString = @'
$originalPrompt = Get-Item Function:\prompt
Set-Item -Path Function:\prompt_original -Value $originalPrompt
function prompt {
    "$(& prompt_original)`n"
}
'@
Add-Content -Path $PROFILE -Value "`n$rawString`n"
```

```shell
p10k configure
```

```toml
echo '[line_break]\ndisabled = false' >> ~/.config/starship.toml
```

--------------------------------

### Define RunAgentResponse Schema in OpenAPI

Source: https://docs.warp.dev/reference/api-and-sdk/models

This JSON schema defines the RunAgentResponse object used by the Oz Agent API. It includes the run_id, task_id, current state, and capacity status for agent runs.

```json
{
  "type": "object",
  "description": "Response returned when an agent run is successfully created.",
  "required": ["run_id", "task_id", "state"],
  "properties": {
    "run_id": { "type": "string", "description": "Unique identifier for the created run" },
    "task_id": { "type": "string", "deprecated": true, "description": "Unique identifier for the task" },
    "state": { "$ref": "#/components/schemas/RunState" },
    "at_capacity": { "type": "boolean", "description": "Whether the system is at capacity" }
  }
}
```

--------------------------------

### Configure Oz PR Review Workflow in GitHub Actions

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/github-actions/quickstart-github-actions

A YAML configuration for a GitHub Actions workflow that triggers the Oz agent on pull request events. It requires the WARP_API_KEY secret and uses the oz-agent-action to analyze diffs and post feedback.

```yaml
name: Oz PR review

on:
  pull_request:
    types: [opened, ready_for_review]

permissions:
  contents: read
  pull-requests: write

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Review PR with Oz
        uses: warpdotdev/oz-agent-action@v1
        with:
          prompt: |
            Review the code changes on this pull request:
            1. Use `git diff origin/${{ github.base_ref }}...HEAD` to identify changes.
            2. Analyze the diff for style, security, or correctness issues.
            3. Use `gh pr review --comment` to post inline suggestions.
          warp_api_key: ${{ secrets.WARP_API_KEY }}
```

--------------------------------

### Update Scheduled Agent

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Updates an existing scheduled agent's configuration. All fields except agent_config are required.

```APIDOC
## PUT /agent/schedules/{scheduleId}

### Description
Update an existing scheduled agent's configuration. All fields except agent_config are required.

### Method
PUT

### Endpoint
/agent/schedules/{scheduleId}

### Parameters
#### Path Parameters
- **scheduleId** (string) - Required - The unique identifier of the schedule.

#### Query Parameters
None

#### Request Body
- **agent_config** (object) - Optional - Configuration for the agent, including environment and code details.
  - **environment** (object) - Optional - Configuration for the agent's execution environment.
    - **cloud_environment_config** (object) - Optional - Configuration for a cloud environment.
      - **name** (string) - Required - Human-readable name for the environment.
      - **description** (string) - Optional - Optional description of the environment.
      - **docker_image** (string) - Required - Docker image to use (e.g., "ubuntu:latest" or "registry/repo:tag").
      - **github_repos** (array) - Optional - List of GitHub repositories to clone into the environment.
        - **owner** (string) - Required - GitHub repository owner (user or organization).
        - **repo** (string) - Required - GitHub repository name.
      - **setup_commands** (array) - Optional - Shell commands to run during environment setup.
        - (string) - Shell command to execute.
  - **cron_schedule** (string) - Required - Cron schedule string (e.g., "0 * * * *").
  - **run_as** (string) - Required - The principal to run the agent as (e.g., "user:12345").
  - **name** (string) - Required - Name of the scheduled agent.
  - **description** (string) - Optional - Description of the scheduled agent.

### Request Example
```json
{
  "agent_config": {
    "environment": {
      "cloud_environment_config": {
        "name": "My Cloud Env",
        "docker_image": "ubuntu:latest",
        "github_repos": [
          {
            "owner": "my-org",
            "repo": "my-repo"
          }
        ],
        "setup_commands": [
          "apt-get update",
          "pip install -r requirements.txt"
        ]
      }
    },
    "cron_schedule": "0 * * * *",
    "run_as": "user:12345",
    "name": "My Scheduled Agent",
    "description": "Runs my agent every hour."
  }
}
```

### Response
#### Success Response (200)
- **schedule_id** (string) - The unique identifier of the updated schedule.
- **name** (string) - Name of the scheduled agent.
- **description** (string) - Description of the scheduled agent.
- **cron_schedule** (string) - Cron schedule string.
- **run_as** (string) - The principal that the agent runs as.
- **agent_config** (object) - Configuration for the agent.
  - **environment** (object) - Environment configuration.
    - **cloud_environment_config** (object) - Cloud environment configuration.
      - **name** (string) - Name of the environment.
      - **description** (string) - Description of the environment.
      - **docker_image** (string) - Docker image used.
      - **github_repos** (array) - List of GitHub repositories.
        - **owner** (string) - Repository owner.
        - **repo** (string) - Repository name.
      - **setup_commands** (array) - Setup commands.
  - **created_at** (string) - Timestamp when the schedule was created (RFC3339).
  - **updated_at** (string) - Timestamp when the schedule was last updated (RFC3339).
  - **created_by** (object) - Information about the creator.
    - **type** (string) - Type of the creator (user or service_account).
    - **uid** (string) - Unique identifier of the creator.
    - **display_name** (string) - Display name of the creator.
    - **email** (string) - Email address of the creator.
    - **photo_url** (string) - URL to the creator's photo.
  - **updated_by** (object) - Information about the last updater.
    - **type** (string) - Type of the updater (user or service_account).
    - **uid** (string) - Unique identifier of the updater.
    - **display_name** (string) - Display name of the updater.
    - **email** (string) - Email address of the updater.
    - **photo_url** (string) - URL to the updater's photo.
  - **history** (object) - Scheduler-derived history metadata.
    - **last_ran** (string) - Timestamp of the last successful run (RFC3339).
    - **next_run** (string) - Timestamp of the next scheduled run (RFC3339).
  - **scope** (object) - Ownership scope for the resource.
    - **type** (string) - Type of ownership (User or Team).
    - **uid** (string) - UID of the owning user or team.

#### Response Example
```json
{
  "schedule_id": "sched_abc123",
  "name": "My Updated Scheduled Agent",
  "description": "Updated description.",
  "cron_schedule": "0 0 * * *",
  "run_as": "user:12345",
  "agent_config": {
    "environment": {
      "cloud_environment_config": {
        "name": "My Cloud Env",
        "docker_image": "ubuntu:latest",
        "github_repos": [
          {
            "owner": "my-org",
            "repo": "my-repo"
          }
        ],
        "setup_commands": [
          "apt-get update",
          "pip install -r requirements.txt"
        ]
      }
    },
    "created_at": "2023-10-27T10:00:00Z",
    "updated_at": "2023-10-27T10:30:00Z",
    "created_by": {
      "type": "user",
      "uid": "user:12345",
      "display_name": "John Doe",
      "email": "john.doe@example.com",
      "photo_url": "https://example.com/photo.jpg"
    },
    "updated_by": {
      "type": "user",
      "uid": "user:12345",
      "display_name": "John Doe",
      "email": "john.doe@example.com",
      "photo_url": "https://example.com/photo.jpg"
    },
    "history": {
      "last_ran": "2023-10-27T09:00:00Z",
      "next_run": "2023-10-28T00:00:00Z"
    },
    "scope": {
      "type": "User",
      "uid": "user:12345"
    }
  }
}
```

#### Error Response (400, 404, 500)
- **type** (string) - URI reference that identifies the problem type.
- **title** (string) - Short, human-readable summary of the problem type.
- **status** (integer) - The HTTP status code for this occurrence of the problem.
- **detail** (string) - A human-readable explanation specific to this occurrence of the problem.
- **instance** (string) - The request path that generated this error.
- **error** (string) - Human-readable error message combining title and detail.
- **retryable** (boolean) - Whether the request can be retried.
- **trace_id** (string) - OpenTelemetry trace ID for debugging.
```

--------------------------------

### POST /agent/schedules/{scheduleId}/pause

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Pauses a specific scheduled agent by its ID, preventing it from running until it is manually resumed.

```APIDOC
## POST /agent/schedules/{scheduleId}/pause

### Description
Pause a scheduled agent. The agent will not run until resumed. This sets the enabled flag to false.

### Method
POST

### Endpoint
/agent/schedules/{scheduleId}/pause

### Parameters
#### Path Parameters
- **scheduleId** (string) - Required - The unique identifier of the scheduled agent

### Request Example
{
  "scheduleId": "agent-123-abc"
}

### Response
#### Success Response (200)
- **ScheduledAgentItem** (object) - The updated scheduled agent object.

#### Response Example
{
  "id": "agent-123-abc",
  "enabled": false
}
```

--------------------------------

### Platform Error Categories

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors

Lists and describes common platform-side errors indicating issues within the Warp system.

```APIDOC
## Platform Error Categories

### Description
Platform errors indicate issues originating from the Warp system itself. When encountered, cloud agent tasks transition to the ERROR state. Retryable errors are automatically retried.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
#### Platform Errors
- **`authentication_required`** - Invalid or expired API key.
- **`resource_unavailable`** - Transient infrastructure issue (retryable).
- **`internal_error`** - Unexpected server-side error (retryable).
```

--------------------------------

### PullRequestArtifact Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Represents a PULL_REQUEST artifact generated by an agent run, including the pull request URL and branch.

```APIDOC
## PullRequestArtifact Schema

### Description
An artifact of type PULL_REQUEST produced by an agent run. Contains
the URL and branch name of the pull request opened by the agent.

### Properties
- **artifact_type** (string) - Required - Identifies this artifact as a pull request (enum: PULL_REQUEST).
- **created_at** (string) - Required - Timestamp when the artifact was created (RFC3339).
- **data** (object) - Required - Data payload for a PULL_REQUEST artifact.
  - **url** (string) - Required - URL of the pull request.
  - **branch** (string) - Required - Branch name for the pull request.
```

--------------------------------

### Define RunStatusMessage and PlatformErrorCode schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the RunStatusMessage object for tracking run states and the associated PlatformErrorCode enum. It provides human-readable messages, machine-readable error codes, and retryability indicators for terminal states.

```json
{"type":"object","description":"Status message for a run. For terminal error states, includes structured\nerror code and retryability info from the platform error catalog.\n","required":["message"],"properties":{"message":{"type":"string","description":"Human-readable status message"},"error_code":{"$ref":"#/components/schemas/PlatformErrorCode"},"retryable":{"type":"boolean","description":"Whether the error is transient and the client may retry by submitting\na new run. Only present on terminal error states. When false, retrying\nwithout addressing the underlying cause will not succeed.\n"}}}
```

--------------------------------

### Set Fish as Default Shell on macOS

Source: https://docs.warp.dev/getting-started/supported-shells

This snippet configures fish as the default shell for Warp on macOS. It first adds the fish executable path to the system's shells file and then sets it as the default login shell. This process requires sudo privileges.

```shell
echo $(which fish) | sudo tee -a /etc/shells
chsh -s $(which fish)
```

--------------------------------

### Verifying Compilation with Cargo (Rust)

Source: https://docs.warp.dev/university/developer-workflows/frontend-ui/how-to-replace-a-ui-element-in-warp-rust-codebase

After code modifications, the Warp agent uses 'cargo check' to verify that the Rust codebase compiles successfully. This step is crucial for ensuring the integrity of the changes and identifying any potential compilation errors.

```bash
cargo check
```

--------------------------------

### Set PowerShell (pwsh) as Default Shell on macOS

Source: https://docs.warp.dev/getting-started/supported-shells

This snippet configures PowerShell (pwsh) as the default shell for Warp on macOS. It involves adding the pwsh executable path to the system's shells file and then setting it as the default login shell. This operation requires sudo privileges.

```shell
echo $(which pwsh) | sudo tee -a /etc/shells
chsh -s $(which pwsh)
```

--------------------------------

### Reset MCP Authentication Tokens

Source: https://docs.warp.dev/agent-platform/capabilities/mcp

To reset authentication tokens for MCP servers, delete the local MCP auth files. This action will remove all locally stored tokens, requiring re-authentication. Ensure sensitive information is removed before sharing logs.

```bash
rm -rf ~/.mcp-auth
```

--------------------------------

### Conditionally Disable Configurations for Warp (Bash)

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

This Bash snippet demonstrates how to conditionally disable specific configurations or plugins that might be incompatible with Warp Terminal. It checks if the TERM_PROGRAM environment variable is set to 'WarpTerminal' and only applies the enclosed code if it is not, allowing for targeted debugging.

```bash
# bash (See ~/.bashrc)
if [[ $TERM_PROGRAM != "WarpTerminal" ]]; then
##### WHAT YOU WANT TO DISABLE FOR WARP - BELOW
    # Unsupported plugin/prompt code here, i.e.
##### WHAT YOU WANT TO DISABLE FOR WARP - ABOVE
fi

```

--------------------------------

### Resume Scheduled Agent

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Resumes a paused scheduled agent. This action sets the agent's 'enabled' flag to true, allowing it to run according to its defined cron schedule.

```APIDOC
## POST /schedules/{id}/resume

### Description
Resumes a paused scheduled agent. The agent will start running according to its cron schedule. This sets the enabled flag to true.

### Method
POST

### Endpoint
/schedules/{id}/resume

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the scheduled agent to resume.

### Request Example
(No request body is required for this operation)

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating the agent has been resumed.

#### Response Example
```json
{
  "message": "Scheduled agent resumed successfully."
}
```
```

--------------------------------

### Handle feature_not_available JSON error response

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/feature-not-available

This JSON object represents the standard error response returned by the API when a feature is restricted by the current subscription plan. It includes the error type, status code, and a descriptive message indicating the required plan level.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/feature-not-available",
  "title": "Slack integration requires a Build plan or higher.",
  "status": 403,
  "instance": "/api/v1/agent/tasks",
  "error": "Slack integration requires a Build plan or higher.",
  "retryable": false
}
```

--------------------------------

### Error Handling Response

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Standard error response format used across the Warp Dev API when a resource is not found or a request fails.

```APIDOC
## GET /resource

### Description
Returns a standard error object when the requested resource cannot be located.

### Method
GET

### Endpoint
/resource/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the resource.

### Request Example
GET /resource/123

### Response
#### Error Response (404)
- **message** (string) - Description of the error (e.g., "File not found")

#### Response Example
{
  "message": "File not found"
}
```

--------------------------------

### DeleteScheduledAgentResponse Schema

Source: https://docs.warp.dev/reference/api-and-sdk/models

Defines the confirmation response returned after a scheduled agent is successfully deleted.

```APIDOC
## DeleteScheduledAgentResponse Object

### Description
Confirmation response returned after a scheduled agent is successfully deleted.

### Properties
- **success** (boolean) - Whether the deletion was successful

### Response Example
{
  "success": true
}
```

--------------------------------

### Error Codes

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Machine-readable error codes identifying problem types for user and Warp errors.

```APIDOC
## Error Codes

### Description
Machine-readable error code identifying the problem type. Used in the `type` URI of Error responses and in the `error_code` field of RunStatusMessage.

### User Errors (run transitions to FAILED)
- `insufficient_credits` — Team has no remaining add-on credits
- `feature_not_available` — Required feature not enabled for user's plan
- `external_authentication_required` — User hasn't authorized a required external service
- `not_authorized` — Principal lacks permission for the requested operation
- `invalid_request` — Request is malformed or contains invalid parameters
- `resource_not_found` — Referenced resource does not exist
- `budget_exceeded` — Spending budget limit has been reached
- `integration_disabled` — Integration is disabled and must be enabled
- `integration_not_configured` — Integration setup is incomplete
- `operation_not_supported` — Requested operation not supported for this resource/state
- `environment_setup_failed` — Client-side environment setup failed
- `content_policy_violation` — Prompt or setup commands violated content policy
- `conflict` — Request conflicts with the current state of the resource

### Warp Errors (run transitions to ERROR)
- `authentication_required` — Request lacks valid authentication credentials
- `resource_unavailable` — Transient infrastructure issue (retryable)
- `internal_error` — Unexpected server-side error (retryable)

### Enum
- `insufficient_credits`
- `feature_not_available`
- `external_authentication_required`
- `not_authorized`
- `invalid_request`
- `resource_not_found`
- `budget_exceeded`
- `integration_disabled`
- `integration_not_configured`
- `operation_not_supported`
- `environment_setup_failed`
- `content_policy_violation`
- `conflict`
- `authentication_required`
- `resource_unavailable`
- `internal_error`
```

--------------------------------

### ArtifactItem Schema

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Represents a discriminated union for artifacts produced during an agent run. The type of artifact is determined by the 'artifact_type' field.

```APIDOC
## ArtifactItem Schema

### Description
A discriminated union representing an artifact produced during an agent run.
The artifact_type field determines which variant is present: PLAN, PULL_REQUEST, or SCREENSHOT. Each variant carries a data object with type-specific fields.

### Properties
- **artifact_type** (string) - Required - The type of artifact (PLAN, PULL_REQUEST, or SCREENSHOT).
- **created_at** (string) - Required - Timestamp when the artifact was created (RFC3339).
- **data** (object) - Required - Type-specific data for the artifact.

### Variants
- **PlanArtifact**: An artifact of type PLAN.
  - **data**: Contains `document_uid`, `notebook_uid` (optional), and `title` (optional).
- **PullRequestArtifact**: An artifact of type PULL_REQUEST.
  - **data**: Contains `url` and `branch`.
- **ScreenshotArtifact**: An artifact of type SCREENSHOT.
  - **data**: Contains `artifact_uid`, `mime_type`, and `description` (optional).

### Example
```json
{
  "artifact_type": "PLAN",
  "created_at": "2023-10-27T10:00:00Z",
  "data": {
    "document_uid": "doc-12345",
    "title": "Initial Project Plan"
  }
}
```
```

--------------------------------

### Delete Secret with Confirmation using oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/secrets

Permanently removes a secret after prompting the user for confirmation. This is a safety measure to prevent accidental deletion of critical secrets.

```bash
oz secret delete --team METABASE_API_KEY
```

--------------------------------

### Reset Warp Authentication Credentials

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

Commands to clear stale login tokens and user data across different operating systems. This resolves issues where online features like AI agents or block sharing fail due to authentication errors.

```bash
sudo security delete-generic-password -l "dev.warp.Warp-Stable" $HOME/Library/Keychains/login.keychain
```

```powershell
Remove-Item $env:LOCALAPPDATA\warp\Warp\data\*-User
```

```bash
rm -f ${XDG_STATE_HOME:-$HOME/.local/state}/warp-terminal/*-User
```

--------------------------------

### POST /api/v1/agent/tasks/{task_id}/cancel

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/operation-not-supported

Endpoint for cancelling agent tasks. This endpoint returns an operation_not_supported error if the task is self-hosted, local, or triggered via GitHub Actions.

```APIDOC
## POST /api/v1/agent/tasks/{task_id}/cancel

### Description
Attempts to cancel an agent task. This operation is restricted for certain task types (self-hosted, local, or GitHub Actions), resulting in a 422 error if invoked.

### Method
POST

### Endpoint
/api/v1/agent/tasks/{task_id}/cancel

### Parameters
#### Path Parameters
- **task_id** (string) - Required - The unique identifier of the agent task to cancel.

### Request Example
{}

### Response
#### Error Response (422)
- **type** (string) - A URI reference that identifies the problem type.
- **title** (string) - A short, human-readable summary of the problem.
- **status** (integer) - The HTTP status code (422).
- **instance** (string) - The specific request path that caused the error.
- **error** (string) - Detailed explanation of why the operation is unsupported.
- **retryable** (boolean) - Indicates if the request can be retried (false).

#### Response Example
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/operation-not-supported",
  "title": "Self-hosted agent runs cannot be cancelled with the API.",
  "status": 422,
  "instance": "/api/v1/agent/tasks/abc123/cancel",
  "error": "Self-hosted agent runs cannot be cancelled with the API.",
  "retryable": false
}
```

--------------------------------

### Update Bitbucket API Token Secret with Oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/integrations/bitbucket

This command updates the value of an existing team-scoped secret named BITBUCKET_API_TOKEN using the Oz CLI. This is useful if the API token needs to be refreshed or changed.

```bash
oz secret update --value BITBUCKET_API_TOKEN
```

--------------------------------

### User Error Categories

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors

Lists and describes common user-facing errors that indicate issues the caller needs to resolve.

```APIDOC
## User Error Categories

### Description
User errors are issues originating from the client's request that require correction by the caller. When encountered, cloud agent tasks transition to the FAILED state.

### Method
N/A

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
#### User Errors
- **`insufficient_credits`** - Team has no remaining add-on credits.
- **`feature_not_available`** - Feature not included in your current plan.
- **`external_authentication_required`** - External service authorization needed.
- **`not_authorized`** - Insufficient permissions for the operation.
- **`invalid_request`** - Malformed request or invalid parameters.
- **`resource_not_found`** - Referenced resource does not exist.
- **`budget_exceeded`** - Spending budget limit reached.
- **`integration_disabled`** - Integration is disabled.
- **`integration_not_configured`** - Integration setup is incomplete.
- **`operation_not_supported`** - Operation not supported for this resource or state.
- **`environment_setup_failed`** - Cloud agent environment failed to initialize.
- **`content_policy_violation`** - Task flagged by content policy checks.
- **`conflict`** - Request conflicts with the current resource state (retryable).
```

--------------------------------

### Disable Spaceship prompt async mode

Source: https://docs.warp.dev/terminal/appearance/prompt

Configures the Spaceship prompt to disable asynchronous mode, which resolves typeahead issues within the Warp input editor.

```bash
echo "SPACESHIP_PROMPT_ASYNC=FALSE" >>! ~/.zshrc
```

--------------------------------

### Configure Locale for Chinese Character Rendering

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

Environment variable exports to fix rendering issues with Chinese characters in the terminal. Add these lines to your shell configuration file (e.g., .bashrc or .zshrc).

```bash
export LC_ALL=zh_CN.UTF-8
export LANG=zh_CN.UTF-8
```

--------------------------------

### Disable Background Commands in Remote Sessions (Linux)

Source: https://docs.warp.dev/terminal/warpify/subshells

Disables background commands in remote subshell sessions on Linux by modifying the user preferences JSON file. This ensures features like command corrections do not run in remote environments.

```bash
cd ~/.config/warp-terminal/
jq '.prefs += {"DisableInBandCommands": "true"}' user_preferences.json > tmp.json && mv tmp.json user_preferences.json
```

--------------------------------

### Clear Warp Session Restoration Database (macOS, Windows, Linux)

Source: https://docs.warp.dev/terminal/sessions/session-restoration

These commands are used to delete the SQLite database file containing session restoration data. This action is destructive and will remove all saved session and block history. It is recommended to close Warp before executing these commands.

```bash
rm -f "$HOME/Library/Group Containers/2BBY89MBSN.dev.warp/Library/Application Support/dev.warp.Warp-Stable/warp.sqlite"
```

```powershell
Remove-Item -Force $env:LOCALAPPDATA\warp\Warp\data\warp.sqlite
```

```bash
rm -f "${XDG_STATE_HOME:-$HOME/.local/state}/warp-terminal/warp.sqlite"
```

--------------------------------

### Update Secret Value Interactively with oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/secrets

Updates a secret's value by prompting the user for secure input in the terminal. This command is useful for interactive updates where the new value is not stored in a file.

```bash
oz secret update --team --value METABASE_API_KEY
```

--------------------------------

### Conditionally Disable Configurations for Warp (Zsh)

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/known-issues

This Zsh snippet shows how to conditionally disable configurations or plugins that may conflict with Warp Terminal. It uses an if statement to check if the TERM_PROGRAM variable is not 'WarpTerminal', ensuring that the code within the block is only executed outside of Warp, aiding in troubleshooting.

```zsh
# zsh (See ~/.zshrc)
if [[ $TERM_PROGRAM != "WarpTerminal" ]]; then
##### WHAT YOU WANT TO DISABLE FOR WARP - BELOW
    # Unsupported plugin/prompt code here
##### WHAT YOU WANT TO DISABLE FOR WARP - ABOVE
fi

```

--------------------------------

### POST /agent/runs/{runId}/cancel

Source: https://docs.warp.dev/reference/api-and-sdk/agent

Endpoint to cancel an agent run that is currently queued or in progress.

```APIDOC
## POST /agent/runs/{runId}/cancel

### Description
Cancel an agent run that is currently queued or in progress. Once cancelled, the run will transition to a cancelled state. Note that terminal states, pending states, and specific run types like local or GitHub Actions may return error codes.

### Method
POST

### Endpoint
/agent/runs/{runId}/cancel

### Parameters
#### Path Parameters
- **runId** (string) - Required - The unique identifier of the run to cancel

### Request Example
POST /agent/runs/run_12345/cancel

### Response
#### Success Response (200)
- **runId** (string) - The ID of the cancelled run

#### Response Example
{
  "runId": "run_12345"
}

#### Error Handling
- **400**: Run is in a terminal state or invalid request.
- **401**: Authentication required.
- **403**: No permission to cancel run.
- **404**: Run not found.
- **409**: Run is in PENDING state; retry after a moment.
- **422**: Operation not supported for this run type (e.g., local/GitHub Actions).
```

--------------------------------

### POST /api/v1/agent/tasks/{taskId}/cancel

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/conflict

Endpoint used to cancel a pending or active agent task. May return a 409 Conflict if the task is in a pending state.

```APIDOC
## POST /api/v1/agent/tasks/{taskId}/cancel

### Description
Attempts to cancel a specific agent task. If the task is currently in a 'pending' state, the server will return a 409 Conflict error as pending tasks cannot be cancelled.

### Method
POST

### Endpoint
/api/v1/agent/tasks/{taskId}/cancel

### Parameters
#### Path Parameters
- **taskId** (string) - Required - The unique identifier of the agent task to cancel.

### Request Example
{
  "taskId": "abc123"
}

### Response
#### Error Response (409)
- **type** (string) - URI reference to the error documentation.
- **title** (string) - Human-readable summary of the error.
- **status** (integer) - The HTTP status code (409).
- **instance** (string) - The request path that caused the error.
- **error** (string) - Detailed error message.
- **retryable** (boolean) - Indicates if the operation can be retried.

#### Response Example
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/conflict",
  "title": "Pending agent runs cannot be cancelled, retry after a moment.",
  "status": 409,
  "instance": "/api/v1/agent/tasks/abc123/cancel",
  "error": "Pending agent runs cannot be cancelled, retry after a moment.",
  "retryable": true
}
```

--------------------------------

### Oz Platform API Error Response Structure

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors

Details the standard JSON structure for error responses from the Oz Platform API, adhering to RFC 7807.

```APIDOC
## Error Response Structure

### Description
All error responses from the Oz Platform API adhere to the structure defined by RFC 7807 (Problem Details for HTTP APIs). This structure provides machine-readable error codes and human-readable messages.

### Method
N/A (This describes a response format, not a specific request method)

### Endpoint
N/A (This describes a response format, not a specific endpoint)

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (N/A - This describes error responses)
#### Error Response Structure
- **`type`** (string) - URI identifying the error type, linking to documentation.
- **`title`** (string) - Short, human-readable summary of the problem.
- **`status`** (integer) - The HTTP status code for the response.
- **`detail`** (string) - Optional: Additional context specific to the error occurrence.
- **`instance`** (string) - The request path that produced the error.
- **`error`** (string) - Backward-compatible field combining `title` and `detail`.
- **`retryable`** (boolean) - Indicates if the request can be retried.
- **`trace_id`** (string) - OpenTelemetry trace ID for support reference.

#### Response Example
```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/invalid-request",
  "title": "The request contains invalid or missing parameters.",
  "status": 400,
  "detail": "schedule_id is required",
  "instance": "/api/v1/agent/tasks",
  "error": "The request contains invalid or missing parameters. (schedule_id is required)",
  "retryable": false,
  "trace_id": "abc123def456..."
}
```
```

--------------------------------

### Disable Background Commands in Remote Sessions (Windows)

Source: https://docs.warp.dev/terminal/warpify/subshells

Disables background commands in remote subshell sessions on Windows by updating the registry. This setting prevents features like syntax highlighting and command corrections from functioning in remote sessions.

```powershell
Set-ItemProperty -Path "HKCU:\SOFTWARE\Warp.dev\Warp" -Name DisableInBandCommands -Value true
```

--------------------------------

### DELETE /agent/schedules/{scheduleId}

Source: https://docs.warp.dev/reference/api-and-sdk/schedules

Deletes a specific scheduled agent by its ID, effectively stopping all future scheduled runs.

```APIDOC
## DELETE /agent/schedules/{scheduleId}

### Description
Delete a scheduled agent. This will stop all future scheduled runs.

### Method
DELETE

### Endpoint
/agent/schedules/{scheduleId}

### Parameters
#### Path Parameters
- **scheduleId** (string) - Required - The unique identifier of the scheduled agent

### Request Example
N/A (No request body required)

### Response
#### Success Response (200)
- **success** (boolean) - Whether the deletion was successful

#### Response Example
{
  "success": true
}
```

--------------------------------

### Refresh Linux Package Signing Keys

Source: https://docs.warp.dev/support-and-community/troubleshooting-and-support/updating-warp

Commands to update expired GPG or RPM signing keys for Warp terminal on Debian/Ubuntu, Fedora/RHEL/CentOS, and Arch Linux systems to resolve signature verification errors.

```bash
# Debian / Ubuntu
curl -fsSL https://releases.warp.dev/linux/keys/warp.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/warpdotdev.gpg > /dev/null
sudo apt update && sudo apt install warp-terminal
```

```bash
# Fedora / RHEL / CentOS
sudo rpm --import https://releases.warp.dev/linux/keys/warp.asc
sudo dnf upgrade warp-terminal
```

```bash
# Arch Linux
sudo pacman-key --recv-keys "linux-maintainers@warp.dev" --keyserver hkp://keys.openpgp.org:80
sudo pacman-key --lsign-key "linux-maintainers@warp.dev"
sudo pacman -Syu warp-terminal
```

--------------------------------

### Constrain Agent Scope for Linear Updates

Source: https://docs.warp.dev/university/mcp-servers/linear-mcp-updating-tickets-with-a-lean-build-approach

This prompt provides a safety constraint for the Warp agent, ensuring that modifications are strictly limited to a specified ticket ID to prevent unintended changes to related epics.

```text
Only update the ticket with ID <ticket_number>.
Do not modify other epics or related tickets.
```

--------------------------------

### Disable Background Commands in Remote Sessions (macOS)

Source: https://docs.warp.dev/terminal/warpify/subshells

Disables background commands in remote subshell sessions on macOS by updating the application's default settings. This prevents features like tab completions and syntax highlighting from running in remote environments.

```bash
defaults update dev.warp.Warp-Stable DisableInBandCommands true
```

--------------------------------

### Disable iTerm2 shell integration for Warp

Source: https://docs.warp.dev/terminal/appearance/prompt

Uses a conditional check to prevent iTerm2 shell integration scripts from running in Warp, which otherwise causes conflicts with custom prompts.

```bash
if [[ $TERM_PROGRAM != "WarpTerminal" ]]; then
##### WHAT YOU WANT TO DISABLE FOR WARP - BELOW

test -e "${HOME}/.iterm2_shell_integration.zsh" && source "${HOME}/.iterm2_shell_integration.zsh"

##### WHAT YOU WANT TO DISABLE FOR WARP - ABOVE
fi
```

--------------------------------

### Delete Secret Forcefully using oz CLI

Source: https://docs.warp.dev/agent-platform/cloud-agents/secrets

Permanently removes a secret without prompting for confirmation. Use this command with caution, as it bypasses the safety confirmation step.

```bash
oz secret delete --team --force METABASE_API_KEY
```

--------------------------------

### Warp API Error Response Structure (JSON)

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors

This JSON structure represents a typical error response from the Warp platform API, conforming to RFC 7807. It includes a machine-readable type, human-readable title and detail, HTTP status, instance, a combined error field, retryability status, and a trace ID for support.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/invalid-request",
  "title": "The request contains invalid or missing parameters.",
  "status": 400,
  "detail": "schedule_id is required",
  "instance": "/api/v1/agent/tasks",
  "error": "The request contains invalid or missing parameters. (schedule_id is required)",
  "retryable": false,
  "trace_id": "abc123def456..."
}
```

--------------------------------

### Set Terminal Tab Title via Shell Configuration

Source: https://docs.warp.dev/terminal/windows/tabs

This script allows users to set a custom title for their terminal tab by disabling automatic title updates and sending an escape sequence. It is compatible with both Zsh and Bash environments by hooking into pre-execution or prompt command functions.

```bash
# Set name, where MyTabName would be whatever you want to see in the Tab ( either a fixed string, $PWD, or something else )
function set_name () {
  export WARP_DISABLE_AUTO_TITLE=true
  echo -ne "\033]0;MyTabName\007"
}
# Add the function to the environment variable in either Zsh or Bash
if [ -n "$ZSH_VERSION" ]; then
  preexec_functions+=(set_name)
elif [ -n "$BASH_VERSION" ]; then
  PROMPT_COMMAND='set_name'
fi
```

--------------------------------

### Regex Patterns for Secret Redaction

Source: https://docs.warp.dev/support-and-community/privacy-and-security/secret-redaction

A collection of regular expression patterns used by Warp to identify various types of secrets, including IP addresses, API keys, tokens, and more. These patterns can be used to configure custom secret redaction rules.

```regex
\b((25[0-5]||(2[0-4]||1\d||[1-9]||)\d)\.?\b){4}\b
```

```regex
\b((([0-9A-Fa-f]{1,4}:){1,6}:)||(([0-9A-Fa-f]{1,4}:){7}))([0-9A-Fa-f]{1,4})\b
```

```regex
\bxapp-[0-9]+-[A-Za-z0-9_]+-[0-9]+-[a-f0-9]+\b
```

```regex
\b(\+\d{1,2}\s)?\(?\d{3}\)?[\s.-]\d{3}[\s.-]\d{4}\b
```

```regex
\b(AKIA||A3T||AGPA||AIDA||AROA||AIPA||ANPA||ANVA||ASIA)[A-Z0-9]{12,}\b
```

```regex
\b((([a-zA-z0-9]{2}[-:]){5}([a-zA-z0-9]{2}))||(([a-zA-z0-9]{2}:){5}([a-zA-z0-9]{2})))\b
```

```regex
\bAIza[0-9A-Za-z-_]{35}\b
```

```regex
\b[0-9]+-[0-9A-Za-z_]{32}\.apps\.googleusercontent\.com\b
```

```regex
\bghp_[A-Za-z0-9_]{36}\b
```

```regex
\bgithub_pat_[A-Za-z0-9_]{82}\b
```

```regex
\bgho_[A-Za-z0-9_]{36}\b
```

```regex
\bghu_[A-Za-z0-9_]{36}\b
```

```regex
\bghs_[A-Za-z0-9_]{36}\b
```

```regex
\b(?:r||s)k_(test||live)_[0-9a-zA-Z]{24}\b
```

```regex
\b([a-z0-9-]){1,30}(\.firebaseapp\.com)\b
```

```regex
\b(ey[a-zA-z0-9_\-=]{10,}\.){2}[a-zA-z0-9_\-=]{10,}\b
```

```regex
\bsk-[a-zA-Z0-9]{48}\b
```

```regex
\bsk-ant-api\d{0,2}-[a-zA-Z0-9\-]{80,120}\b
```

```regex
\bfw_[a-zA-Z0-9]{24}\b
```

--------------------------------

### Internal Error JSON Response Structure

Source: https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/internal-error

This JSON object represents the standard error response returned by the Warp API when an unclassified server-side error occurs. It includes a trace_id for debugging and indicates that the error is retryable.

```json
{
  "type": "https://docs.warp.dev/reference/api-and-sdk/troubleshooting/errors/internal-error",
  "title": "An unexpected error occurred. Please try again later. If the issue persists, contact support.",
  "status": 500,
  "instance": "/api/v1/agent/tasks",
  "error": "An unexpected error occurred. Please try again later. If the issue persists, contact support.",
  "retryable": true,
  "trace_id": "abc123..."
}
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.