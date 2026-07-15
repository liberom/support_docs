### Install and Configure macOS PKG Options

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Demonstrates installing a macOS PKG with interactive configuration and then updating installation options using the `defaults` command. This example shows setting a string, boolean, and integer option for a PKG.

```bash
sudo installer -dumplog -verbose -pkg path/to/app.pkg -target LocalSystem
sudo defaults write /Library/Preferences/<the bundle id> MY_STRING_OPTION -string "hello"
sudo defaults write /Library/Preferences/<the bundle id> MY_BOOLEAN_OPTION -boolean YES
sudo defaults write /Library/Preferences/<the bundle id> MY_INTEGER_OPTION -integer 7
```

--------------------------------

### Install Express Dependency for Runner Authorization Service

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

Command to install the Express framework, a necessary dependency for the Node.js runner authorization service example.

```bash
npm install express
```

--------------------------------

### Install MSI with Multiple Custom Options

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Shows how to install an MSI package with multiple custom installation options, including string and integer types.

```bash
msiexec /i path\to\package.msi MY_STRING_OPTION='hello' MY_INTEGER_OPTION=7
```

--------------------------------

### Install Postman Enterprise Windows App (MSI)

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Demonstrates how to install the Postman Enterprise MSI package on Windows. This example shows a system-wide installation to a custom directory using the INSTALLDIR property.

```bash
msiexec /i path/to/package.msi INSTALLDIR=C:\custom
```

--------------------------------

### Install MCP Server Dependencies

Source: https://learning.postman.com/docs/postman-ai/mcp-servers/set-up-start

Installs all the necessary project dependencies for your MCP server. This command reads the 'package.json' file and downloads required packages into the 'node_modules' directory.

```bash
npm install

```

--------------------------------

### Install Postman CLI

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

Command to globally install the Postman CLI using npm, required for managing and starting Postman runners.

```bash
npm install -g postman-cli
```

--------------------------------

### Configure macOS PKG Installation Options (Per-User)

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Sets installation options for a per-user macOS PKG using the `defaults` command. This example sets the `TEAM_IDS` option. Changes can be made before or after installation.

```bash
defaults write <the bundle id> TEAM_IDS -string "1234,5678"
```

--------------------------------

### GET /resources - Response with Examples

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that the response for GET /resources includes multiple examples for consumers.

```APIDOC
## GET /resources

### Description
This endpoint retrieves a list of resources and includes multiple examples for consumers.

### Method
GET

### Endpoint
/resources

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **aProperty** (any) - An example property.

#### Response Example
```json
{
  "aProperty": "example value"
}
```

#### Examples
- **anExample**:
  - summary: An example
  - description: This is an example description
  - value: |
    {
      "aProperty": "example value"
    }
```

--------------------------------

### GET /resources - Response with Example

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that the response for GET /resources includes an example for consumers.

```APIDOC
## GET /resources

### Description
This endpoint retrieves a list of resources and includes an example response.

### Method
GET

### Endpoint
/resources

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **aProperty** (any) - An example property.

#### Response Example
```json
{
  "aProperty": "example"
}
```
```

--------------------------------

### Example Request with Wildcard Variable

Source: https://learning.postman.com/docs/design-apis/mock-apis/matching-algorithm

Demonstrates how to use a wildcard variable in a request URL to capture dynamic URL segments like user IDs. The example shows a GET request to a user endpoint.

```json
GET {{url}}/users/{{userId}}
```

--------------------------------

### Configure macOS PKG Installation Options (System-Wide)

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Sets installation options for a system-wide macOS PKG using the `defaults` command. This example sets the `TEAM_IDS` option. Changes can be made before or after installation.

```bash
sudo defaults write /Library/Preferences/<the bundle id> TEAM_IDS -string "1234,5678"
```

--------------------------------

### Per-User Install Postman Enterprise Windows App

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Shows how to perform a per-user installation of the Postman Enterprise MSI package. This example uses the MSIINSTALLPERUSER=1 property to install for the current user.

```bash
msiexec /i path/to/package.msi MSIINSTALLPERUSER=1
```

--------------------------------

### Enable Verbose Logging for MSI Installation

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Shows how to enable verbose logging during the MSI installation process for debugging. The /l*v option directs detailed logs to a specified file.

```bash
msiexec /i path\to\package.msi /l*v C:\log.txt
```

--------------------------------

### Dockerfile: Install Postman CLI and Start Runner

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

This Dockerfile installs the Postman CLI, sets up a non-root user, and configures the Postman runner to start with the built-in proxy server enabled. It also specifies the authorization service URL. Ensure the necessary environment variables (POSTMAN_RUNNER_ID, POSTMAN_RUNNER_KEY, AUTHORIZATION_SERVICE_URL) are provided when running the container.

```dockerfile
FROM --platform=linux/amd64 node:22-bookworm-slim

# Install CA certificates for SSL/TLS connections and curl for health checks
RUN apt-get update && apt-get install -y ca-certificates curl && rm -rf /var/lib/apt/lists/*

# Install Postman CLI
RUN npm install -g postman-cli

# Set working directory for runner
WORKDIR /app

# Create non-root user and set up directories
# The directory permissions ensure the runner can write logs and cache data
RUN groupadd --system --gid 1001 postman && \
    useradd --system --uid 1001 --gid postman --home-dir /app postman && \
    mkdir -p /.postman/logs \
            /app/.postman/logs \
            /app/.postman/cli \
            /app/.postman-runner-proxy-ca && \
    chown -R postman:postman /app && \
    chown -R postman:postman /.postman && \
    chmod -R 777 /.postman && \
    chmod -R 777 /app/.postman-runner-proxy-ca

# Switch to non-root user for security
USER postman

# Start the Postman runner with the built-in proxy enabled
CMD ["sh", "-c", "postman runner start --id ${POSTMAN_RUNNER_ID} --key ${POSTMAN_RUNNER_KEY} --egress-proxy --egress-proxy-authz-url ${AUTHORIZATION_SERVICE_URL}"]

```

--------------------------------

### Install Postman MCP Server as Gemini CLI Extension

Source: https://learning.postman.com/docs/developer/postman-api/postman-mcp-server/set-up-postman-mcp-server

This command installs the Postman MCP Server as an extension for the Gemini CLI. It uses the `gemini extensions install` command with the GitHub repository URL of the Postman MCP Server.

```bash
gemini extensions install https://github.com/postmanlabs/postman-mcp-server

```

--------------------------------

### Install Postman CLI using npm

Source: https://learning.postman.com/docs/monitoring-your-api/runners/set-up-a-runner-in-your-network

Installs the Postman CLI globally using npm. This is the first step to setting up a runner. Ensure you have Node.js and npm installed on your system.

```bash
npm install -g postman-cli

```

--------------------------------

### Start MCP Server (STDIO)

Source: https://learning.postman.com/docs/postman-ai/mcp-servers/set-up-start

Starts the MCP server using the standard input and output (STDIO) transport layer. This is the default mode for the MCP server.

```bash
node mcpServer.js

```

--------------------------------

### Install Postman Enterprise App with Snap (Linux)

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Installs the Postman Enterprise application from a local snap package file. The `--dangerous` flag is required as the app is not distributed via the Snap store. Ensure the path to the snap file is correct.

```bash
sudo snap install /path/to/postman-enterprise.snap --dangerous

```

--------------------------------

### Example: Import and Use Postman Logger Package

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/package-library

An example illustrating the import of a package named `postman_logger`. It shows how to declare the imported package as a variable (`postmanLogger`) and use it to call a `logger` function. The example also demonstrates using the `pm` object to run a test method.

```javascript
// team domain: postman
// package name: postman_logger
const postmanLogger = pm.require('@postman/postman_logger');

postmanLogger.logger("The test passed")

// output in the Postman Console: Logging information to the console, The test passed
```

--------------------------------

### Start MCP Server (Streamable HTTP)

Source: https://learning.postman.com/docs/postman-ai/mcp-servers/set-up-start

Starts the MCP server using the streamable HTTP transport layer. This option allows for more advanced communication patterns.

```bash
node mcpServer.js --streamable-http

```

--------------------------------

### Navigate to MCP Server Directory

Source: https://learning.postman.com/docs/postman-ai/mcp-servers/set-up-start

Changes the current directory to the root of your MCP server project. This is a prerequisite for running subsequent npm commands and starting the server.

```bash
cd /path/to/your-mcp-server

```

--------------------------------

### Configure Basic Proxy Authentication (Windows)

Source: https://learning.postman.com/docs/getting-started/installation/proxy

This batch script sets the `HTTP_PROXY` and `HTTPS_PROXY` environment variables with basic authentication credentials before starting the Postman desktop application. Replace `USER:PASS@host:port` with your actual proxy server address, port, username, and password. Update `C:\path\to\Postman.exe` to your Postman installation directory.

```batch
set HTTP_PROXY=http://USER:PASS@host:port
set HTTPS_PROXY=https://USER:PASS@host:port
start C:\path\to\Postman.exe

```

--------------------------------

### OpenAPI: Add Examples to Operation Parameters

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet illustrates how to use the 'examples' field for a parameter in an OpenAPI operation, allowing for multiple documented examples. This enhances clarity for API consumers and facilitates mock server generation.

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    get:
      parameters:
        - name: status
          description: Filters resources on their status
          in: query
          examples:
            anExample:
              summary: An example
              description: A description of an example
              value: done
          schema:
            type: string

```

--------------------------------

### Per-User Custom Install Postman Enterprise Windows App

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Illustrates performing a per-user installation to a custom directory. This combines MSIINSTALLPERUSER=1 and INSTALLDIR properties for flexible deployment.

```bash
msiexec /i path/to/package.msi MSIINSTALLPERUSER=1 INSTALLDIR=%USERPROFILE%\custom
```

--------------------------------

### Silent Install Postman Enterprise Windows App

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Demonstrates how to perform a silent installation of the Postman Enterprise MSI package using the /qn flag. This is useful for automated deployments where user interaction should be minimized.

```bash
msiexec /i path\to\package.msi /qn MSIINSTALLPERUSER=1
```

--------------------------------

### List Installed macOS PKG Identifiers

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Retrieves a list of all installed PKG bundle identifiers on a macOS system. Use `--volume / --packages` for system-wide installations and `--volume "$HOME" --packages` for per-user installations. This is a prerequisite for uninstalling PKG installers.

```bash
# For system-wide PKGs
pkgutil --volume / --packages
# For per-user PKGs
pkgutil --volume "$HOME" --packages
```

--------------------------------

### Install Postman Enterprise macOS App (System-Wide)

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Installs the Postman Enterprise PKG package for all users on a macOS system. The `installer` tool is used with the `-dumplog`, `-verbose`, `-pkg`, and `-target LocalSystem` flags. This ensures the app is installed to the system-wide Applications directory and configuration is stored in /Library/Preferences.

```bash
sudo installer -dumplog -verbose -pkg path/to/app.pkg -target LocalSystem
```

--------------------------------

### Install Postman MCP Server in Claude Code

Source: https://learning.postman.com/docs/developer/postman-api/postman-mcp-server/set-up-postman-mcp-server

These commands demonstrate how to add the Postman MCP Server to Claude Code. Each command corresponds to a different mode: Minimal, Code, or Full. It includes setting the POSTMAN_API_KEY environment variable and specifying the desired mode via command-line flags.

```bash
claude mcp add postman --env POSTMAN_API_KEY=YOUR_KEY -- npx @postman/postman-mcp-server@latest

```

```bash
claude mcp add postman --env POSTMAN_API_KEY=YOUR_KEY -- npx @postman/postman-mcp-server@latest  --code

```

```bash
claude mcp add postman --env POSTMAN_API_KEY=YOUR_KEY -- npx @postman/postman-mcp-server@latest --full

```

--------------------------------

### List MCP Server Tools

Source: https://learning.postman.com/docs/postman-ai/mcp-servers/set-up-start

Lists the available tools within your MCP server project, displaying their file names and other relevant information. This helps in identifying and configuring individual tool files.

```bash
npm run list-tools

```

--------------------------------

### Install Postman Enterprise macOS App (Per-User)

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Installs the Postman Enterprise PKG package for the current user on a macOS system. The `installer` tool is used with the `-dumplog`, `-verbose`, `-pkg`, and `-target CurrentUserHomeDirectory` flags. This installs the app to the user's home Applications directory and configuration to $HOME/Library/Preferences.

```bash
installer -dumplog -verbose -pkg path/to/app.pkg -target CurrentUserHomeDirectory
```

--------------------------------

### Example Response for All Environments

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Illustrates the structure of the response returned by the `_pm('_property.get', 'environments')` method, showing an array of environment objects.

```json
[
  {
    "button_index": 0,
    "name": "env1",
    "values": [
      {
        "key": "testKey",
        "value": "testValue",
        "enabled": true
      }
    ]
  }
]
```

--------------------------------

### MCP Tool Example

Source: https://learning.postman.com/docs/postman-ai/mcp-server-flows/create-mcp-server-flow

This snippet shows an example of an MCP tool definition, including parameters for a tool named 'code_review' and its arguments.

```json
Copy"params": {
    "name": "code_review",
    "arguments": {
      "code": "def hello():\n    print('world')"
    }
  }


```

--------------------------------

### Node.js Runner Authorization Service Implementation with Express

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

An example Node.js implementation of a runner authorization service using the Express framework. This code demonstrates how to create a POST /validate endpoint that accepts the specified request format and returns an allowed or blocked status based on custom logic.

```javascript
#!/usr/bin/env node
const express = require("express");
const app = express();
app.use(express.json());

const PORT = process.env.AUTH_SERVER_PORT || 8080;

/**
* Evaluates whether a request from the runner is allowed.
* Customize with your authorization logic based on: url, method, headers, body, queryParams
*/
function evaluateRequest({ url, method }) {
  try {
    console.info('Evaluating authorization request');
    const hostname = new URL(url).hostname;
    const pathname = new URL(url).pathname;

    // Block unsafe methods
    if (["DELETE", "PUT", "PATCH"].includes(method)) {
      console.warn(`Blocked unsafe method: ${method}`);
      return false;
    }

    // Block: Admin paths
    if (pathname.includes("/admin") || pathname.includes("/internal")) {
      console.warn(`Blocked sensitive path: ${method} ${hostname}`);
      return false;
    }

    // Add more policies here

    // Consider blocking by default in production
    console.info(`Request allowed: ${method} ${hostname}`);
    return true;
  } catch {
    return false;
  }
}

app.post("/validate", (req, res) => {
  if (!req.body?.url || !req.body?.method) {
    return res.status(400).json({ allowed: false });
  }

  const allowed = evaluateRequest(req.body);
  res.status(allowed ? 200 : 403).json({ allowed });
});

app.listen(PORT, () =>
  console.log(`Runner authorization service on port ${PORT}`)
);

```

--------------------------------

### MCP Resource Example

Source: https://learning.postman.com/docs/postman-ai/mcp-server-flows/create-mcp-server-flow

Illustrates how to specify a resource with a URI in an MCP prompt, which actions will use to provide context to language models.

```json
Copy{
  "params": {
    "uri": "file:///project/src/main.rs"
  }
}


```

--------------------------------

### Configure Postman Teams During MSI Install

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Illustrates setting specific MSI installation options, such as the TEAM_IDS property, to control which Postman teams can use the Enterprise app.

```bash
msiexec /i path\to\package.msi TEAM_IDS="1234"
```

--------------------------------

### Example Response with Wildcard Variable

Source: https://learning.postman.com/docs/design-apis/mock-apis/matching-algorithm

Illustrates how to use captured wildcard variables in the response body. The example shows a JSON response that includes the captured userId.

```json
{
  "id": {{userId}},
  "name": "Carol"
}
```

--------------------------------

### Install External Newman HTML Reporter

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-custom-reporters

Demonstrates how to install an external reporter, specifically the Newman HTML reporter, using npm. This command installs the reporter package locally.

```bash
npm install newman-reporter-html

```

--------------------------------

### Start Postman Runner with ID and Key

Source: https://learning.postman.com/docs/monitoring-your-api/runners/set-up-a-runner-in-your-network

Starts the Postman runner by providing its unique ID and a secret key. These credentials authenticate the runner with your Postman account. Replace placeholders with your actual runner ID and key.

```bash
postman runner start --id <runner-id> --key <runner-key>

```

--------------------------------

### Run Postman MCP Server in Docker

Source: https://learning.postman.com/docs/developer/postman-api/postman-mcp-server/set-up-postman-mcp-server

This section provides Docker commands for running the Postman MCP Server. It includes a direct `docker run` command for automatic discovery and download, and instructions for manual build and run, with options for Minimal and Full modes. The POSTMAN_API_KEY is passed as an environment variable.

```bash
docker run -i -e POSTMAN_API_KEY="<your-secret-key>" mcp/postman

```

```bash
docker run -i -e POSTMAN_API_KEY="<your-secret-key>" postman-api-mcp-stdio

```

```bash
docker run -i -e POSTMAN_API_KEY="<your-secret-key>" postman-api-mcp-stdio --full

```

--------------------------------

### Unboxed MCP Prompt Example

Source: https://learning.postman.com/docs/postman-ai/mcp-server-flows/create-mcp-server-flow

Demonstrates the 'unboxed' version of an MCP prompt that an action will process, stripping outer elements.

```json
Copy{
    "name": "code_review",
    "arguments": {
      "code": "def hello():\n    print('world')"
    }
}


```

--------------------------------

### OpenAPI: Add Example to Operation Parameters

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet shows how to include an 'example' field for a parameter in an OpenAPI operation. Providing examples helps users understand expected data formats and can aid in generating mock servers.

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    get:
      parameters:
        - name: status
          description: Filters resources on their status
          in: query
          example: done
          schema:
            type: string

```

--------------------------------

### List Files of Installed macOS PKG

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Lists the files associated with a specific installed PKG on macOS, relative to its installation root. Use `--volume / --files <the bundle id>` for system-wide PKGs and `--volume "$HOME" --files <the bundle id>` for per-user PKGs. This information is used to manually uninstall the PKG.

```bash
# For system-wide PKGs
pkgutil --volume / --files <the bundle id>
# For per-user PKGs
pkgutil --volume "$HOME" --files <the bundle id>
```

--------------------------------

### Dockerfile for Postman Runner

Source: https://learning.postman.com/docs/monitoring-your-api/runners/set-up-a-runner-in-your-network

A Dockerfile to create an image for the Postman runner. It installs the Postman CLI, sets up a non-root user, and configures the environment to start the runner using provided credentials as environment variables. This is used for deploying runners in cloud networks.

```dockerfile
FROM --platform=linux/amd64 node:22-bookworm-slim

# Install ca-certificates for SSL/TLS connections
RUN apt-get update && apt-get install -y ca-certificates && rm -rf /var/lib/apt/lists/*

# Install Postman CLI
RUN npm install -g postman-cli

# Create a non-root user
RUN groupadd -r postman && useradd -r -g postman -u 1001 postman

# Set working directory for runner
WORKDIR /app

# Create Postman directories with proper permissions
RUN mkdir -p /home/postman/.postman/logs && \
    chown -R postman:postman /home/postman/.postman && \
    chown -R postman:postman /app

# Switch to non-root user
USER postman

# Run the Postman runner
CMD ["sh", "-c", "postman runner start --id ${POSTMAN_RUNNER_ID} --key ${POSTMAN_RUNNER_KEY}"]

```

--------------------------------

### Use Newman as a Node.js Library

Source: https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman

Integrates Newman into a Node.js project to run Postman collections programmatically. This example demonstrates how to require Newman and execute a collection with a 'cli' reporter.

```javascript
const newman = require('newman'); // require Newman in your project

// call newman.run to pass the `options` object and wait for callback
newman.run({
    collection: require('./sample-collection.json'),
    reporters: 'cli'
}, function (err) {
    if (err) { throw err; }
    console.log('collection run complete!');
});

```

--------------------------------

### Add Examples to OpenAPI Responses

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This rule emphasizes the importance of providing examples for all response objects in your API definition. Examples, whether using the `example` or `examples` property, significantly aid API consumers in understanding the data structure and can facilitate mock server generation.

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    get:
      responses:
        '200':
          description: A success response
          content:
            'application/json':
              schema:
                # ...
              example:
                aProperty: example

```

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    get:
      responses:
        '200':
          description: A success response
          content:
            'application/json':
              schema:
                # ...
              examples:
                anExample:
                  summary: An example
                  description: This is an example description
                  value:
                    aProperty: example value

```

--------------------------------

### Add Examples to All Responses

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Requires that all response objects in API definitions include examples. Response examples help consumers understand the data they will receive and can be used for mock servers.

```yaml
swagger: '2.0'
# ...
paths:
  /resources:
    get:
      responses:
        '200':
          description: A success response
          examples:
            'application/json':
              aProperty: example value

```

--------------------------------

### Install Newman CLI Globally

Source: https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman

Installs the Newman command-line runner globally on your system, making it accessible from any directory. This command requires Node.js and npm to be installed.

```bash
npm install -g newman

```

--------------------------------

### OpenAPI: Add Examples to Request Bodies

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet shows how to use the 'examples' field for a request body in an OpenAPI operation, allowing for multiple documented examples. This enhances clarity for API consumers and facilitates mock server generation.

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    post:
      requestBody:
        content:
          'application/json':
            schema:
              # ...
            examples:
              anExample:
                summary: An example
                description: This is an example description
                value:
                  aProperty: example value

```

--------------------------------

### Test Docker Installation

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-with-docker

Verifies that Docker is installed and running correctly on your system. This is a prerequisite for using Docker and Newman with Docker.

```shell
docker run hello-world
```

--------------------------------

### Get Help for Postman Insights Agent CLI (Bash)

Source: https://learning.postman.com/docs/insights/get-started/ec2

This command displays the help information for the Postman Insights Agent command-line interface, listing available configuration parameters and options.

```bash
postman-insights-agent ec2 --help
```

--------------------------------

### Install Postman CLI on Windows using PowerShell

Source: https://learning.postman.com/docs/postman-cli/postman-cli-installation

Installs the Postman CLI specifically for Windows. This command downloads and executes an install script using PowerShell, setting up the 'postman' binary in the user's AppData directory.

```powershell
powershell.exe -NoProfile -InputFormat None -ExecutionPolicy AllSigned -Command "[System.Net.ServicePointManager]::SecurityProtocol = 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://dl-cli.pstmn.io/install/win64.ps1'))"
```

--------------------------------

### Install Postman Certificate on Ubuntu

Source: https://learning.postman.com/docs/sending-requests/capturing-request-data/capturing-https-traffic

Installs the Postman security certificate on Ubuntu systems. This involves creating a directory, copying the certificate file, and reconfiguring the system's certificate authorities. Requires superuser privileges.

```bash
sudo mkdir -p /usr/share/ca-certificates/extra

```

```bash
sudo cp ~/.config/Postman/proxy/postman-proxy-ca.crt /usr/share/ca-certificates/extra/postman-proxy-ca.crt

```

```bash
sudo dpkg-reconfigure ca-certificates

```

```bash
sudo update-ca-certificates

```

--------------------------------

### Data Parsing Example

Source: https://learning.postman.com/docs/postman-flows/reference/flows-actions-overview

This example demonstrates how a query string is parsed into a structured JSON object by a Flows action. Each field in the query string becomes a key in the JSON object, with its value being an array of strings.

```APIDOC
## Data Parsing in Flows Actions

### Description
Flows actions parse incoming data as a structured data object. Each field in the object maps to a list of string values. This is particularly useful when dealing with data from sources like Slack slash commands or other webhook integrations.

### Method
Not Applicable (This describes data transformation, not a specific HTTP method)

### Endpoint
Not Applicable (This describes data transformation, not a specific endpoint)

### Parameters
This section describes the transformation of incoming data. A typical input is a URL-encoded query string.

#### Incoming Data Example (Query String)
```
token=9XqPLt7mKaRjVh2NbzC4f5Yw&team_id=T91H6Z2LK&team_domain=acme&channel_id=C72DF1XRK9&channel_name=integration-testing&user_id=U18ABZQXPR&user_name=jane.doe&command=%2Fflows&text=status&api_app_id=A45K9L72QM&is_enterprise_install=false&enterprise_id=E55YT9QWKV&enterprise_name=AcmeCorp&response_url=https%3A%2F%2Fhooks.slack.com%2Fcommands%2FT91H6Z2LK%2F3399128457101%2FHgT9yW3aKpLvQ8RbFsXe5JdM&trigger_id=3399128462830.8451991626.a1bc
```

### Parsed Data Example (JSON Object)
When the action receives the data above, it parses it into the following JSON structure:

#### Response Example
```json
{
  "token": ["9XqPLt7mKaRjVh2NbzC4f5Yw"],
  "team_id": ["T91H6Z2LK"],
  "team_domain": ["acme"],
  "channel_id": ["C72DF1XRK9"],
  "channel_name": ["integration-testing"],
  "user_id": ["U18ABZQXPR"],
  "user_name": ["jane.doe"],
  "command": ["/flows"],
  "text": ["status"],
  "api_app_id": ["A45K9L72QM"],
  "is_enterprise_install": ["false"],
  "enterprise_id": ["E55YT9QWKV"],
  "enterprise_name": ["AcmeCorp"],
  "response_url": ["https://hooks.slack.com/commands/T91H6Z2LK/3399128457101/HgT9yW3aKpLvQ8RbFsXe5JdM"],
  "trigger_id": ["3399128462830.8451991626.a1bcde230ab982f3d451f9bce67d041d"]
}
```

### Notes
- Each key in the parsed JSON object corresponds to a parameter name from the original query string.
- The value for each key is always an array of strings, even if there's only one value for that parameter.
```

--------------------------------

### OpenAPI: Add Example to Request Bodies

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet demonstrates how to add an 'example' field to the request body of an OpenAPI operation. Providing examples clarifies the expected data structure for consumers and aids in mock server generation.

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    post:
      requestBody:
        content:
          'application/json':
            schema:
              # ...
            example:
              aProperty: example value

```

--------------------------------

### JavaScript Pre-request Script Example

Source: https://learning.postman.com/collection-format/advanced-concepts/events

An example of a pre-request script written in JavaScript. This script demonstrates setting a text variable and logging it to the console, which would execute before the API request is sent.

```javascript
const text = 'I am a text';
console.log('Text is: ', text)
```

--------------------------------

### Define Bitbucket Pipeline Configuration

Source: https://learning.postman.com/docs/integrations/available-integrations/ci-integrations/bitbucket-pipelines

This snippet shows an example of a `bitbucket-pipelines.yml` file, which defines the structure and steps of your CI/CD pipeline. You specify the build environment, steps for building and testing your API, and deployment configurations.

```yaml
pipelines:
  default:
    - step:
        name: Build and Test API
        image: node:18
        script:
          - npm install
          - npm test
          - postman collection run "my-api-collection.json" --environment "my-api-environment.json"
```

--------------------------------

### Start MCP Server using Node.js

Source: https://learning.postman.com/docs/postman-ai/mcp-servers/interact

This code snippet shows the command to start an MCP server using Node.js. It assumes the server is a JavaScript file located at a specified path. This is used when the communication method is set to STDIO.

```shell
node /path/to/your-mcp-server/mcpServer.js
```

--------------------------------

### View Newman Help and Version

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

These commands are used to display the help information listing all available Newman options or to show the currently installed version of Newman.

```bash
newman run -h

```

```bash
newman run -v

```

--------------------------------

### Get Postman CLI Version

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Displays the version number of the Postman CLI. This is a basic command to verify your installation.

```bash
postman -v
```

--------------------------------

### Add Example to Request Bodies

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that all request bodies defined in API operations include an example. Providing examples aids consumers in understanding the expected data format and can facilitate mock server generation.

```yaml
swagger: '2.0'
# ...
paths:
  /resources:
    post:
      parameters:
        - in: body
          name: body
          schema:
            type: object
            example:
              aProperty: example value

```

--------------------------------

### Configure Postman MCP Server in VS Code

Source: https://learning.postman.com/docs/developer/postman-api/postman-mcp-server/set-up-postman-mcp-server

This configuration sets up the Postman MCP Server to run within Visual Studio Code. It specifies the server type, command to execute, and arguments for different modes (full, code, region). It also includes environment variable configuration for the Postman API key, which is prompted from the user.

```json
{
    "servers": {
        "postman-api-mcp": {
            "type": "stdio",
            "command": "npx",
            "args": [
                "@postman/postman-mcp-server",
                "--full" // (optional) Use this flag to enable full mode.
                "--code" // (optional) Use this flag to enable code mode.
                "--region us" // (optional) Use this flag to specify the Postman API region (us or eu). Defaults to us.
            ],
            "env": {
                "POSTMAN_API_KEY": "${input:postman-api-key}"
            }
        }
    },
    "inputs": [
        {
            "id": "postman-api-key",
            "type": "promptString",
            "description": "Enter your Postman API key"
        }
    ]
}
```

--------------------------------

### Get Kubernetes Deployment Configuration

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/sidecar

This `kubectl` command retrieves all deployments across all namespaces in your Kubernetes cluster. It is used to identify the correct deployment to modify for agent injection.

```bash
kubectl get deployments -A
```

--------------------------------

### Retrieve Configuration Options for a Target Language

Source: https://learning.postman.com/docs/developer/code-generators

This code example shows how to retrieve the available configuration options for a specific language and variant using the `codegen.getOptions` method. This is useful for understanding the parameters that can be passed to the `convert` function. The options are logged to the console if successful.

```javascript
var codegen = require('postman-code-generators'),
  language = 'nodejs',
  variant = 'Request';

codegen.getOptions(language, variant, function (error, options) {
  if (error) {
    // handle error
  }
  console.log(options);
});

```

--------------------------------

### Run Postman Collections via CLI in Bitbucket Pipeline

Source: https://learning.postman.com/docs/integrations/available-integrations/ci-integrations/bitbucket-pipelines

This code example demonstrates how to execute Postman collections as part of your Bitbucket Pipeline using the Postman CLI. It ensures that your API tests are run automatically during the CI process. Ensure the Postman CLI is installed and configured within your pipeline environment.

```bash
# Example within bitbucket-pipelines.yml script section
postman collection run "your_collection_uid" --environment "your_environment_uid" --reporters cli
```

--------------------------------

### Postman Insights Agent ECS Add Command Examples

Source: https://learning.postman.com/docs/insights/reference/agent/ecs-add

Illustrative examples of the `ecs add` command demonstrating various filtering and configuration options. These examples cover capturing traffic by port, interface, path exclusions, host exclusions, host allowances, and path allowances.

```bash
postman-insights-agent ecs add ... --filter "port 80" ...
```

```bash
postman-insights-agent ecs add ... --interfaces "lo,eth0" ...
```

```bash
postman-insights-agent ecs add ... --path-exclusions '.*\.png' --path-exclusions '.*\.jpg' ...
```

```bash
postman-insights-agent ecs add ... --host-exclusions 'deb\.debian\.org' ...
```

```bash
postman-insights-agent ecs add ... --host-allow 'www\.example\.com' ...
```

```bash
postman-insights-agent ecs add ... --path-allow '*/admin/*' ...
```

--------------------------------

### Postman Collection with Markdown Description Example

Source: https://learning.postman.com/collection-format/advanced-concepts/documentation

Illustrates a Postman collection with a Markdown-formatted description for a collection item. This allows for structured and readable documentation within the collection itself.

```json
{
  "info": {
    "name": "Collection showing documentation example",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": {
    "name": "Create a collection",
    "description": {
      "type": "text/markdown",
      "content": "## Postman API\n        The Postman API lets you to programmatically access data stored in your Postman account with ease.\n\n        ## Overview\n        1. You must use a valid API Key to send requests to the API endpoints. You can get your API key from Postman's integrations dashboard.\n        2. The API has access rate limits.\n        3. The API only responds to HTTPS-secured communications. Any requests sent via HTTP return an HTTP 301 redirect to the corresponding HTTPS resources.\n\n        ## ID and UID\n        All items in Postman, such as collections, mocks, workspaces, and APIs, have ID and UIDs:\n\n        - An ID is the unique ID assigned to a Postman item. For example, ec29121c-5203-409f-9e84-e83ffc10f226.\n        - The UID is the full ID of a Postman item. This value is the item's unique ID concatenated with the user ID. For example, in the 12345678-ec29121c-5203-409f-9e84-e83ffc10f226 UID:\n          - 12345678 is the user's ID.\n          - ec29121c-5203-409f-9e84-e83ffc10f226 is the item's ID."
    },
    "request": {
      "description": {
        "type": "text/markdown",
        "content":  "### Create a collection\n      \n                Creates a collection using the [Postman Collection v2 schema format](https://schema.postman.com/json/collection/v2.1.0/docs/index.html). Include a collection object in the request body that contains the following required properties:\n                - `info` -- An *object* that contains the following properties:\n                  - `name` -- A *string* value that contains the collection's name.\n                  - `schema` -- A string that contains a URL to the collection's schema. For example, the `https://schema.getpostman.com/collection/v1` URL.\n                - `item` -- An *object* that contains the HTTP request and response information.\n                  - `request` --  An *object* that contains the collection's request information. For a complete list of values, refer to the `definitions.request` entry in the [collection.json schema file](https://schema.getpostman.com/json/collection/v2.1.0/collection.json). If you pass an empty object for this value, the system defaults to an untitled GET request."
      },
      "url": "https://api.getpostman.com/collections",
      "method": "POST",
       "header": [
        {
          "key": "Content-Type",
          "value": "Application/JSON"
        }
      ],
      "body": {
        "mode": "raw",
        "raw": "{\n    \"collection\": {\n        \"info\": {\n            \"name\": \"Sample Collection\",\n            \"schema\": \"https://schema.getpostman.com/json/collection/v2.1.0/collection.json\"\n        },\n        \"item\": [\n            {\n                \"request\": \"https://postman-echo.com/get\"\n            }\n        ]\n    }\n}",
        "options": {
          "raw": {
            "language": "json"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Install Postman CLI on macOS, Linux, and WSL using curl

Source: https://learning.postman.com/docs/postman-cli/postman-cli-installation

Installs the Postman CLI on macOS, Linux, and Windows Subsystem for Linux (WSL). This command uses curl to download and execute a unified installation script that automatically detects the OS and architecture.

```bash
curl -o- "https://dl-cli.pstmn.io/install/unix.sh" | sh
```

--------------------------------

### Install Local Newman Reporter

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-custom-reporters

Shows the command to install a custom reporter that has been developed locally. This is useful for testing or using reporters not yet published to npm.

```bash
npm install <path/to/local-reporter-directory>

```

--------------------------------

### MCP Tool Definition Resource Template Configuration

Source: https://learning.postman.com/docs/postman-ai/mcp-server-flows/create-mcp-server-flow

Provides an example of how to add resource templates to a toolDefinition scenario for parameterizing MCP server resources.

```json
Copy"resourceTemplates": [
      {
        "uriTemplate": "file:///{path}",
        "name": "Project Files",
        "title": "Project Files",
        "description": "Access files in the project directory",
        "mimeType": "application/octet-stream"
      }
    ]


```

--------------------------------

### Configure Postman MCP Server in Kiro

Source: https://learning.postman.com/docs/developer/postman-api/postman-mcp-server/set-up-postman-mcp-server

This JSON configuration is used to manually set up the Postman MCP Server within Kiro. It defines the server's command, arguments, environment variables (including POSTMAN_API_KEY), and settings for auto-approval of actions like `getAuthenticatedUser`.

```json
{
    "mcpServers": {
        "postman": {
        "command": "npx",
            "args": [
                "@postman/postman-mcp-server"
            ],
            "env": {
                "POSTMAN_API_KEY": "postman-api-key"
            },
            "disabled": false,
            "autoApprove": [
                "getAuthenticatedUser"
           ]
        }
    }
}

```

--------------------------------

### Get Cookie Example in Postman Scripting

Source: https://learning.postman.com/docs/sending-requests/response-data/cookies

This snippet shows how to retrieve a cookie's value for a given domain using Postman's scripting. The `pm.cookies.jar().get()` method is used to fetch the cookie by its name. Ensure the domain is on the allowlist and the cookie exists.

```javascript
let cookieValue = pm.cookies.jar("example.com").get("myCookie");
console.log(cookieValue);
```

--------------------------------

### Get Postman Insights Agent Logs

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/sidecar

This `kubectl` command retrieves the logs specifically from the Postman Insights Agent container within a specified pod and namespace. This is useful for troubleshooting issues with the agent.

```bash
kubectl logs -n <your_namespace> <your_pod> postman-insights-agent
```

--------------------------------

### Get Mock Servers

Source: https://learning.postman.com/docs/design-apis/mock-apis/tutorials/mock-with-api

Retrieves a list of your mock servers. This can be used to find the URL of an existing mock server.

```APIDOC
## GET /mocks

### Description
Retrieves a list of mock servers associated with your account.

### Method
GET

### Endpoint
`https://api.getpostman.com/mocks`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **mocks** (array) - A list of mock server objects.
  - Each object contains `id`, `name`, `mockUrl`, `collection`, and `environment` details.

#### Response Example
```json
{
    "mocks": [
        {
            "id": "your-mock-id-1",
            "name": "testAPImock-1",
            "mockUrl": "https://your-mock-server-url-1.com",
            "collection": {
                "id": "your-collection-id-1",
                "name": "testAPI-1"
            },
            "environment": {
                "id": "your-environment-id-1",
                "name": "testAPI-1"
            }
        },
        {
            "id": "your-mock-id-2",
            "name": "testAPImock-2",
            "mockUrl": "https://your-mock-server-url-2.com",
            "collection": {
                "id": "your-collection-id-2",
                "name": "testAPI-2"
            },
            "environment": null
        }
    ]
}
```
```

--------------------------------

### Create Linux Launcher Icon for Postman

Source: https://learning.postman.com/docs/getting-started/installation/installation-and-updates

Creates a desktop entry file for Postman on Linux to enable launching the application from a system launcher. This involves copying a .desktop file and configuring its properties, including the executable path and icon location.

```bash
install -t ~/.local/share/applications/ /</path/to/file>/Postman/app/resources/Postman.desktop
```

```ini
[Desktop Entry]
Encoding=UTF-8
Name=Postman
Exec=</path/to/file>/Postman/app/Postman %U
Icon=</path/to/file>/Postman/app/resources/app/assets/icon.png
Terminal=false
Type=Application
Categories=Development;
```

--------------------------------

### Check Postman Insights Agent DaemonSet Status

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/daemonset

This command checks the status of the Postman Insights Agent DaemonSet in the 'postman-insights-namespace'. After applying the manifest, you need to ensure all pods assigned to the DaemonSet have started successfully. The 'DESIRED' and 'READY' counts should match, indicating a healthy deployment.

```bash
kubectl get daemonsets -n postman-insights-namespace postman-insights-agent
```

--------------------------------

### Update Postman Enterprise Windows App

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

To upgrade the Postman Enterprise app on Windows, you must reinstall the new MSI package using the same public properties as the original installation. Downgrading is not supported and will result in an error. If a downgrade is necessary, the current version must be manually removed before installing an earlier version.

```batch
INSTALLDIR=C:\custom MSIINSTALLPERUSER=1
```

--------------------------------

### Using Template Helpers for Contextual Mock Responses

Source: https://learning.postman.com/docs/design-apis/mock-apis/create-dynamic-responses

This snippet shows examples of how to use Postman template helpers within a mock server's example response. Helpers like $body, $queryParams, $pathSegments, and $headers allow dynamic inclusion of data from the incoming request into the mock response.

```json
// Example: Return the full request body
{{$body}}

// Example: Return a specific property from the request body
{{$body 'path.to.property'}}

// Example: Return a specific request header
{{$headers 'header-key'}}

// Example: Return a specific query parameter
{{$queryParams 'parameter-key'}}

// Example: Return the second path segment (index 1)
{{$pathSegments '1'}}

// Example: Define a default value for a body property
{{$body 'property' 'default value'}}

// Example: Access a property with a dot in its key name
{{$body 'a\.a'}}
```

--------------------------------

### Example Request to Mock Server - cURL

Source: https://learning.postman.com/docs/design-apis/mock-apis/tutorials/mock-with-api

This cURL command demonstrates how to send a request to a mock server. Replace `{{mockUrl}}` with the actual mock server URL obtained after creation. This is useful for testing integrations or front-end applications against a simulated backend.

```bash
curl -X GET "https://{{mockUrl}}/get?test=123"
```

--------------------------------

### pm.test example for checking HTTP status code

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-test-expect

A basic example of using `pm.test` with `pm.expect` to verify that the HTTP response status code is 200 (OK). It checks the `pm.response.code` property.

```javascript
pm.test("Response status code is 200", function () {
    // value: pm.response.code (a number)
    // Assertion: checks if it equals 200
    pm.expect(pm.response.code).to.eql(200);
});
```

--------------------------------

### Install Postman Collection Transformer

Source: https://learning.postman.com/docs/getting-started/importing-and-exporting/importing-data

This command installs the Postman Collection Transformer globally using npm. This tool is necessary for converting Postman collections from v1 to v2 format. Ensure you have Node.js and npm installed on your system.

```bash
sudo npm install -g postman-collection-transformer

```

--------------------------------

### GET /me - Get Authenticated User

Source: https://learning.postman.com/docs/developer/postman-api/make-postman-api-call

Retrieves information about the user associated with the provided API key. This is a basic GET endpoint that does not modify any data.

```APIDOC
## GET /me

### Description
Retrieves information about the user that owns the API key being used to authenticate the call.

### Method
GET

### Endpoint
/me

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "example": "No request body for this endpoint."
}
```

### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the user.
- **username** (string) - The username of the Postman user.
- **email** (string) - The email address of the Postman user.

#### Response Example
```json
{
  "id": "1234567890abcdef",
  "username": "postman_user",
  "email": "user@example.com"
}
```

### Error Handling
- **401 Unauthorized**: Returned if the API key is missing or invalid.
```

--------------------------------

### Forget Installed macOS PKG

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Notifies macOS that a PKG installer has been removed, preventing future "update available" notifications. Use `--volume / --forget <the bundle id>` for system-wide PKGs and `--volume "$HOME" --forget <the bundle id>` for per-user PKGs. This command should be run after manually deleting the PKG files.

```bash
# For system-wide PKGs
sudo pkgutil --volume / --forget <the bundle id>
# For per-user PKGs
pkgutil --volume "$HOME" --forget <the bundle id>
```

--------------------------------

### Run Postman Collection from URL

Source: https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman

Executes a Postman collection by providing its URL. Replace `<collection-id>` with the actual ID of your collection.

```bash
newman run https://www.postman.com/collections/<collection-id>

```

--------------------------------

### Verify Postman CLI version

Source: https://learning.postman.com/docs/postman-cli/postman-cli-installation

Checks the installed version of the Postman CLI. This command can be used after installation or to verify which version is active, especially when troubleshooting.

```bash
postman --version
```

--------------------------------

### Install Postman on Mac using Homebrew

Source: https://learning.postman.com/docs/getting-started/installation/installation-and-updates

Installs the Postman application on macOS using the Homebrew package manager. This command fetches and installs the latest version of Postman, making it available in your Applications folder.

```bash
brew install --cask postman
```

--------------------------------

### Postman Collection Item Example (JSON)

Source: https://learning.postman.com/collection-format/getting-started/structure-of-a-collection

Illustrates a basic Postman collection item, representing a single HTTP GET request. It includes an ID, name, description, and the request URL.

```json
{
  "id": "my-first-item",
  "name": "My First Item",
  "description": "This is an Item that contains a single HTTP GET request. It doesn't really do much yet!",
  "request": "http://postman-echo.com/get",
  "response": []
}
```

--------------------------------

### Run the Node.js Runner Authorization Service

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

Command to execute the Node.js runner authorization service script. Ensure you replace `<path-to-authorization-service-file>` with the actual file path.

```bash
node <path-to-authorization-service-file>
```

--------------------------------

### Apply injected resources via kubectl

Source: https://learning.postman.com/docs/insights/reference/agent/kube-inject

This example demonstrates piping the output of the `kube inject` command directly to `kubectl apply`. This allows for immediate application of the injected resources (including generated secrets) to a Kubernetes cluster without intermediate file saving.

```bash
postman-insights-agent kube inject -s --project projectId -f in.yml | kubectl apply -f -
```

--------------------------------

### CSV File Format Example

Source: https://learning.postman.com/docs/collections/running-collections/working-with-data-files

This example demonstrates the correct formatting for a CSV file used with Postman collection runs. The first row specifies variable names, and subsequent rows contain data. Ensure Unix-style line endings and consistent column counts per row. Numbers longer than 15 digits may require special formatting as text or explicit data type specification in Postman.

```csv
CopyCity,Ramen Vancouver,100 San Francisco,84 Singapore,79 Austin,66 Los Angeles,65

```

--------------------------------

### Run Newman with Custom Reporter (Command Line)

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-custom-reporters

Illustrates how to execute a Newman collection run and specify a custom reporter using the command-line interface. It includes an example of passing reporter-specific options.

```bash
newman run /path/to/collection.json -r myreporter --reporter-myreporter-<option-name> <option-value> # The option is optional

```

--------------------------------

### Implement Basic Authentication

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This example shows how to implement Basic Authentication for an API operation. It defines the 'BasicAuth' security scheme and applies it to the '/pets' POST operation, ensuring credentials are sent securely.

```yaml
components:
 securitySchemes:
  BasicAuth:
   type: http
   scheme: basic
paths:
 '/pets':
  post:
   operationId: addPet
   servers:
   - url: https://example.com/
     description: Example server
   security:
   - BasicAuth: []
```

--------------------------------

### Importing .proto files with relative paths

Source: https://learning.postman.com/docs/sending-requests/grpc/using-service-definition

Example of import directives within a .proto file that reference other proto files using relative paths. This requires configuring the parent directory of these imported files as an import path in Postman.

```proto
import "enums/NumericEnum.proto"
import "messages/EmptyMessage.proto"
import "messages/HelloResponse.proto"
import "messages/HelloRequest.proto"
```

--------------------------------

### GET /resources

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Retrieves a list of resources. Supports filtering by status.

```APIDOC
## GET /resources

### Description
A GET operation description for retrieving resources.

### Method
GET

### Endpoint
/resources

#### Query Parameters
- **status** (string) - Optional - Filters resources on their status

### Request Example
```json
{
  "example": ""
}
```

### Response
#### Success Response (200)
- **example** (object) - Example response structure

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### JSON File Format Example

Source: https://learning.postman.com/docs/collections/running-collections/working-with-data-files

This example illustrates the required JSON format for data files in Postman. The data should be an array of objects, where each object represents a row of data and its keys correspond to the variable names used in your collection requests. Variable names are case-sensitive.

```json
Copy[
  {
    "City": "Vancouver",
    "Ramen": 100
  },
  {
    "City": "San Francisco",
    "Ramen": 84
  },
  {
    "City": "Singapore",
    "Ramen": 79
  },
  {
    "City": "Austin",
    "Ramen": 66
  },
  {
    "City": "Los Angeles",
    "Ramen": 65
  }
]

```

--------------------------------

### Add Remote Postman MCP Server in Claude Code (Minimal Mode)

Source: https://learning.postman.com/docs/developer/postman-api/postman-mcp-server/set-up-postman-mcp-server

Command to add the Postman MCP Server in Minimal mode to Claude Code. This command specifies the HTTP transport, the server endpoint, and includes the necessary Authorization header with a placeholder for the Postman API key.

```bash
claude mcp add --transport http postman https://mcp.postman.com/minimal --header "Authorization: Bearer <POSTMAN_API_KEY>"

```

--------------------------------

### pm.test examples for response validation

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-test-expect

Demonstrates how to use `pm.test` to validate HTTP responses. Examples include checking if the response is error-free, has a specific JSON body structure, or performs deep comparisons.

```javascript
pm.test("response should be okay to process", function () {
  pm.response.to.not.be.error;
  pm.response.to.have.jsonBody('data') // checks existence of a property in the JSON response
  pm.response.to.have.jsonBody('data', { "id" : 1 }); // Performs deep comparison.
});
```

--------------------------------

### Example JSON Schema for Backing Up Collections

Source: https://learning.postman.com/docs/integrations/available-integrations/microsoft-power-automate

This JSON schema can be used to create an integration that backs up a Postman collection. It defines the structure for a collection object within the payload.

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "definitions": {},
  "id": "http://example.com/example.json",
  "properties": {
    "collection": {
      "id": "/properties/collection",
      "properties": {},
      "type": "object"
    }
  },
  "type": "object"
}
```

--------------------------------

### Configure Remote Postman MCP Server in mcp.json

Source: https://learning.postman.com/docs/developer/postman-api/postman-mcp-server/set-up-postman-mcp-server

This JSON configuration block is used to set up the remote Postman MCP Server in development environments like Cursor or VS Code. It specifies the server type, URL (with options for minimal or full mode), and authorization headers. It also includes an input prompt for the Postman API key.

```json
{
    "servers": {
        "postman-api-http-server": {
            "type": "sse",
            "url": "https://mcp.postman.com/{minimal OR mcp}",
            // Use "https://mcp.postman.com/mcp" for full or "https://mcp.postman.com/minimal" for minimal mode.
            // For the EU server, use the "https://mcp.eu.postman.com" URL.
            "headers": {
                "Authorization": "Bearer ${input:postman-api-key}"
            }
        }
    },
    "inputs": [
        {
            "id": "postman-api-key",
            "type": "promptString",
            "description": "Enter your Postman API key"
        }
    ]
}

```

--------------------------------

### Check active Postman CLI binary on Windows

Source: https://learning.postman.com/docs/postman-cli/postman-cli-installation

Determines which 'postman' binary is currently active in the system's PATH for Windows. This is useful for troubleshooting when multiple installation methods have been used.

```cmd
where postman
```

--------------------------------

### GET /get

Source: https://learning.postman.com/docs/developer/echo-api

The GET endpoint of the Postman Echo API returns a JSON object containing details from the request sent. It's useful for testing GET requests without complex configurations.

```APIDOC
## GET /get

### Description
This endpoint allows you to test GET requests. It echoes back the details of the request, including headers, query parameters, and the URL, in a JSON response.

### Method
GET

### Endpoint
`https://postman-echo.com/get`

### Parameters
#### Query Parameters
This endpoint does not have specific required query parameters, but any query parameters sent will be reflected in the response.

### Request Example
```json
{
  "example": "GET https://postman-echo.com/get?param1=value1&param2=value2"
}
```

### Response
#### Success Response (200)
- **args** (object) - An object containing the query parameters sent with the request.
- **headers** (object) - An object containing the headers sent with the request.
- **url** (string) - The URL that was requested.

#### Response Example
```json
{
  "args": {
    "param1": "value1",
    "param2": "value2"
  },
  "headers": {
    "x-amzn-trace-id": "Root=1-65b8a8b1-1234567890abcdef12345678",
    "host": "postman-echo.com",
    "user-agent": "PostmanRuntime/7.36.0",
    "accept": "*/*",
    "postman-token": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "connection": "keep-alive"
  },
  "url": "https://postman-echo.com/get?param1=value1&param2=value2"
}
```
```

--------------------------------

### Basic Authorization Configuration Example

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Defines the 'basic' authorization type with username and password credentials. This is a common method for authenticating requests.

```json
{
  "type": "basic",
  "basic": [
    {
      "key": "password",
      "value": "your_secure_password",
      "type": "string"
    },
    {
      "key": "username",
      "value": "your_unique_username",
      "type": "string"
    }
  ]
}
```

--------------------------------

### Run Newman with Custom Reporter (Programmatically)

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-custom-reporters

Provides a JavaScript example of how to run a Newman collection and configure a custom reporter programmatically. It shows how to specify the reporter and its options within the `newman.run` configuration object.

```javascript
var newman = require('newman');

newman.run({
   collection: '/path/to/collection.json',
   reporters: 'myreporter',
   reporter: {
     myreporter: {
       'option-name': 'option-value' // this is optional
     }
   }
}, function (err, summary) {
  if (err) { throw err; }
  console.info('collection run complete!');
});

```

--------------------------------

### Define Operation-Specific Basic Authentication in OpenAPI

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This snippet illustrates how to enforce basic authentication for a specific API operation in an OpenAPI 2.0 specification. It addresses scenarios where the operation's security field is missing, empty, or does not specify a scheme, ensuring the endpoint is protected. The example applies 'basicAuth' to the GET /user endpoint.

```yaml
Copyswagger: '2.0'
#...
paths:
  /user:
    get:
      description: 'Returns details about a particular user'
      security:
          - basicAuth: []
      #...
securityDefinitions:
  basicAuth:
    type: basic

```

--------------------------------

### Sample User Endpoint with OAuth2 Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

An example of defining a sample endpoint '/user' with OAuth2 security, specifying required scopes for read and write operations.

```yaml
copypaths:
  /user:
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      operationId: listUser
      security:
      - OAuth2:
        - read
        - write
components:
  securitySchemes:
    OAuth2:
      type: oauth2
      flows:
        authorizationCode:
          scopes:
            read: read objects in your account
            write: write objects to your account

```

--------------------------------

### JSON Path Plus Examples for Postman Rules

Source: https://learning.postman.com/docs/api-governance/configurable-rules/spectral

Illustrates common JSON Path Plus syntaxes for selecting elements within API specifications. These examples are useful for defining 'given' paths in Postman rules to target specific data points.

```jsonpath
$.info.title
```

```jsonpath
$.paths.*.*.responses
```

```jsonpath
$.paths.*[post,patch,put]
```

```jsonpath
$..properties
```

--------------------------------

### Implement OAuth 1.0 Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This example demonstrates how to configure OAuth 1.0 authentication for an API operation. It defines the security scheme and applies it to the '/pets' POST operation, ensuring secure credential transport.

```yaml
paths:
  '/pets':
    post:
      servers:
      - url: https://example.com/
        description: Example server
components:
  securitySchemes:
    OAuth1:
      type: http
      scheme: oauth
security:
  - OAuth1: []
```

--------------------------------

### Extract Substring by Start and Length

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $substring helper function extracts a portion of a string. It takes the original string, a starting index, and an optional length. If the length is omitted, the substring extends to the end of the string. Negative start indices count from the end of the string.

```postman-helper
$substring("hello world", 0, 5) -> "hello"
$substring("hello world", -5, 5) -> "world"
```

--------------------------------

### Capture All Traffic | Postman CLI

Source: https://learning.postman.com/docs/insights/reference/agent/apidump

This example demonstrates how to capture all traffic from a Postman collection and send it to the Insights Agent. It requires a Postman Insights project ID.

```bash
postman-insights-agent apidump --project <projectId>
```

--------------------------------

### Check active Postman CLI binary on macOS/Linux/WSL

Source: https://learning.postman.com/docs/postman-cli/postman-cli-installation

Determines which 'postman' binary is currently active in the system's PATH for macOS, Linux, or WSL. This is useful for troubleshooting when multiple installation methods have been used.

```bash
which postman
```

--------------------------------

### Install Postman Insights Agent on EC2 (Bash)

Source: https://learning.postman.com/docs/insights/get-started/ec2

This command downloads and executes the installation script for the Postman Insights Agent on an EC2 instance. Ensure you have SSH access and root privileges.

```bash
bash -c "$(curl -L https://releases.observability.postman.com/scripts/install-postman-insights-agent.sh)"
```

--------------------------------

### Configure CLI and JSON Reporters with Options

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-built-in-reporters

This example shows how to run a collection with both CLI and JSON reporters and apply a specific option, `silent`, to both reporters. The `--reporter-[reporter-option]` syntax is used to pass options that apply globally to all specified reporters.

```bash
newman run my-collection.json -r cli,json --reporter-silent

```

--------------------------------

### Run Postman Collection with Environment File

Source: https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman

Runs a Postman collection while specifying an environment file using the `-e` flag. This is useful when your collection relies on environment variables.

```bash
newman run my-collection.json -e dev-environment.json

```

--------------------------------

### GET /resources - Success Response

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that GET operations for resources return a 2xx success status code.

```APIDOC
## GET /resources

### Description
This endpoint retrieves a list of resources. It is expected to succeed and return a 2xx HTTP status code.

### Method
GET

### Endpoint
/resources

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **description** (string) - A success response message.

#### Response Example
```json
{
  "message": "Successfully retrieved resources"
}
```
```

--------------------------------

### Example Request Body for Mock Server (JSON)

Source: https://learning.postman.com/docs/design-apis/mock-apis/create-dynamic-responses

An example of a different JSON payload that can be sent to a Postman mock server. This payload demonstrates how changing the 'username' value in the request body will affect the mock server's response when using the `$body` helper.

```json
{
    "username": "s-morgenstern",
    "password": "12345"
}
```

--------------------------------

### Travis CI configuration for Newman

Source: https://learning.postman.com/docs/collections/using-newman-cli/integration-with-travis

This is a sample `.travis.yml` file that configures Travis CI to build a Node.js project. It installs Newman, runs version checks, and then executes the Postman tests using Newman.

```yaml
language: node_js
node_js:
- "16.13.2"

install:
- npm install newman

before_script:
- node --version
- npm --version
- node_modules/.bin/newman --version

script:
- node_modules/.bin/newman run tests/hello_world.postman_collection.json

```

--------------------------------

### Create JWT Auth Method (Vault CLI)

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command creates a JSON Web Token (JWT) authentication method in HashiCorp Vault, named `postman-jwt` in this example. You can choose a different name and must save it for later configuration.

```shell
vault write /sys/auth/postman-jwt type="jwt"
```

--------------------------------

### Filter Host Allowances | Postman CLI

Source: https://learning.postman.com/docs/insights/reference/agent/apidump

This example shows how to allow traffic only to a specific host (www.example.com) using the apidump command's host-allow flag.

```bash
postman-insights-agent apidump ... --host-allow 'www\.example\.com' ...
```

--------------------------------

### GET /resources - Server Error Response

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that GET operations for resources return a 5xx server error HTTP status code when failures occur.

```APIDOC
## GET /resources

### Description
This endpoint retrieves a list of resources. It is expected to return a 5xx server error HTTP status code in case of failure.

### Method
GET

### Endpoint
/resources

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Server Error Response (500)
- **description** (string) - A server error response message.

#### Response Example
```json
{
  "error": "Internal Server Error"
}
```
```

--------------------------------

### JSON Output Example for Postman Spec Lint

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Example of JSON output from the `postman spec lint` command, detailing violations found in an OpenAPI specification. Each violation includes file path, line number, element path, severity level, the issue description, and the issue type (Syntax or Governance).

```json
{
  "violations": [
    {
      "file": "../../../Desktop/test-collections/spacecraft-api/src/main/resources/openapi.yaml",
      "line number": "13",
      "path": "paths./spacecrafts/{spacecraftIds}.parameters.0",
      "severity": "WARNING",
      "issue": "Parameter \"spacecraftId\" must be used in path \"/spacecrafts/{spacecraftIds}\".",
      "issue type": "Syntax"
    },
    {
      "file": "../../../Desktop/test-collections/spacecraft-api/src/main/resources/openapi.yaml",
      "line number": "19",
      "path": "paths./spacecrafts/{spacecraftIds}.get",
      "severity": "WARNING",
      "issue": "Operation must define parameter \"{spacecraftIds}\" as expected by path \"/spacecrafts/{spacecraftIds}\".",
      "issue type": "Syntax"
    },
    {
      "file": "../../../Desktop/test-collections/spacecraft-api/src/main/resources/openapi.yaml",
      "line number": "4",
      "path": "info",
      "severity": "WARNING",
      "issue": "The info object should have a description.",
      "issue type": "Governance"
    },
    {
      "file": "../../../Desktop/test-collections/spacecraft-api/src/main/resources/openapi.yaml",
      "line number": "21",
      "path": "paths./spacecrafts/{spacecraftIds}.get.responses",
      "severity": "WARNING",
      "issue": "Operation should return a 5xx HTTP status code",
      "issue type": "Governance"
    }
  ]
}
```

--------------------------------

### Run Postman Collection from JSON File

Source: https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman

Executes a Postman collection stored as a JSON file using the Newman CLI. This is a basic command to initiate a collection run.

```bash
newman run my-collection.json

```

--------------------------------

### GET /resources - Reusable Schema Reference

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that schema properties in responses reference reusable schemas for consistency and maintainability.

```APIDOC
## GET /resources

### Description
This endpoint retrieves resources using a reusable schema definition.

### Method
GET

### Endpoint
/resources

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **schema** (object) - References the reusable `#/components/schemas/Resources` schema.

#### Response Example
```json
{
  "Resources": {
    "type": "object"
  }
}
```

### Components
#### Schemas
- **Resources**:
  - type: object
```

--------------------------------

### Uninstall Postman CLI with npm

Source: https://learning.postman.com/docs/postman-cli/postman-cli-installation

Uninstalls the Postman CLI when it was initially installed using npm. This command removes the globally installed package and the 'postman' command from the system's PATH.

```bash
npm uninstall -g postman-cli
```

--------------------------------

### CSV Output Example for Postman Spec Lint

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Example of CSV output from the `postman spec lint` command, presenting API specification violations in a comma-separated values format. Columns include file, line number, path, severity, issue description, and issue type.

```csv
file,line number,path,severity,issue,issue type
../../../Desktop/test-collections/spacecraft-api/src/main/resources/openapi.yaml,13,paths./spacecrafts/{spacecraftIds}.parameters.0,WARNING,"Parameter ""spacecraftId"" must be used in path ""/spacecrafts/{spacecraftIds}"".",Syntax
../../../Desktop/test-collections/spacecraft-api/src/main/resources/openapi.yaml,19,paths./spacecrafts/{spacecraftIds}.get,WARNING,"Operation must define parameter ""{spacecraftIds}"" as expected by path ""/spacecrafts/{spacecraftIds}"".",Syntax
../../../Desktop/test-collections/spacecraft-api/src/main/resources/openapi.yaml,4,info,WARNING,The info object should have a description.,Governance
../../../Desktop/test-collections/spacecraft-api/src/main/resources/openapi.yaml,21,paths./spacecrafts/{spacecraftIds}.get.responses,WARNING,Operation should return a 5xx HTTP status code,Governance
```

--------------------------------

### Add Remote Postman MCP Server in Claude Code (Code Mode)

Source: https://learning.postman.com/docs/developer/postman-api/postman-mcp-server/set-up-postman-mcp-server

Command to add the Postman MCP Server in Code mode to Claude Code. This command specifies the HTTP transport, the server endpoint, and includes the necessary Authorization header with a placeholder for the Postman API key. Note: The URL used here is for Full mode, but the description indicates it's for Code mode.

```bash
claude mcp add --transport http postman https://mcp.postman.com/mcp --header "Authorization: Bearer <POSTMAN_API_KEY>"

```

--------------------------------

### Add License Object to OpenAPI Info

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This example shows how to include a license object within the OpenAPI info section. This is crucial for informing API consumers about how the API can be used and distributed.

```yaml
Copyopenapi: '3.0.3'
info:
  title: An API name
  version: '1.0'
  license:
    name: Apache 2.0
    url: https://opensource.org/licenses/Apache-2.0

```

--------------------------------

### Example JSON Schema for Collection and Team Activity Feed

Source: https://learning.postman.com/docs/integrations/available-integrations/microsoft-power-automate

This JSON schema is used to create integrations for posting collection activity and team activity. It outlines the structure of the payload containing details about the event, collection, user, and more.

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "definitions": {},
  "id": "http://example.com/example.json",
  "properties": {
    "action": {
      "id": "/properties/action",
      "type": "string"
    },
    "collection_name": {
      "id": "/properties/collection_name",
      "type": "string"
    },
    "collection_uid": {
      "id": "/properties/collection_uid",
      "type": "string"
    },
    "message": {
      "id": "/properties/message",
      "type": "string"
    },
    "model": {
      "id": "/properties/model",
      "type": "string"
    },
    "model_name": {
      "id": "/properties/model_name",
      "type": "string"
    },
    "model_uid": {
      "id": "/properties/model_uid",
      "type": "string"
    },
    "user_id": {
      "id": "/properties/user_id",
      "type": "string"
    },
    "user_name": {
      "id": "/properties/user_name",
      "type": "string"
    }
  },
  "type": "object"
}
```

--------------------------------

### Inject manifests with secret generation

Source: https://learning.postman.com/docs/insights/reference/agent/kube-inject

This example injects deployment manifests from `resources.yml`, similar to the previous run, and additionally generates and includes any required secrets for the Insights Agent to function. The secrets are embedded directly into the output YAML.

```bash
postman-insights-agent kube inject -s --project projectId -f resources.yml
```

--------------------------------

### Operation Object - Summary

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Requires that every operation (e.g., GET, POST) in the API definition includes a summary.

```APIDOC
## Operation Object - Summary

### Description
Each operation in an API definition must have a summary. This provides a concise overview of what the operation does, aiding consumers in understanding its purpose.

### Method
N/A (Applies to operation objects within paths)

### Endpoint
N/A (Applies to operation objects within paths)

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
```yaml
swagger: '2.0'
# ...
paths:
  /resources:
    get:
      summary: A GET operation summary
      # ...
```
```

--------------------------------

### Get unique values from a JSON array field

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/conditional-data-selection

The $distinct function in FQL returns an array containing only the unique values from a specified field across all objects in an array. This example extracts unique 'amount' values from the 'payments' array, useful for analyzing distinct data points without duplicates.

```FQL
$distinct(payments.amount)
```

--------------------------------

### Encode API Key using Base64

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/daemonset

This command demonstrates how to encode a sensitive API key using the `base64` utility. The output of this command is a base64-encoded string that can be stored in a Kubernetes Secret. This is a common practice for securely handling sensitive credentials.

```bash
echo -n "<your_api_key>" | base64
# Output: UE1BSy1hc2RmZ2hqa2wtcXdlcnR5dTU0MzIx

```

--------------------------------

### Postman Insights Agent CLI Help

Source: https://learning.postman.com/docs/insights/get-started/ecs

This command displays the help menu for the Postman Insights Agent CLI, providing information on available subcommands and configuration options for managing the agent.

```bash
postman-insights-agent ecs --help
```

--------------------------------

### Configure Basic Proxy Authentication (macOS/Linux)

Source: https://learning.postman.com/docs/getting-started/installation/proxy

This shell script configures the `HTTP_PROXY` and `HTTPS_PROXY` environment variables with basic authentication details before executing the Postman application. Users need to replace `USER:PASS@host:port` with their specific proxy server information and `/path/to/postman` with the correct path to the Postman executable.

```bash
HTTP_PROXY=http://USER:PASS@host:port
HTTPS_PROXY=https://USER:PASS@host:port /path/to/postman

```

--------------------------------

### Start Postman Runner for Private API Monitoring

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Initiates a runner from an internal network to monitor and test APIs without public exposure. It requires a runner ID and key, and sends test results to the Postman cloud. Options support proxy configuration, metrics, and custom SSL certificates.

```bash
postman runner start --id 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12 --key 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12
```

```bash
postman runner start --id 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12 --key 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12 --proxy http://example.com:8080
```

```bash
postman runner start --id 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12 --key 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12 --egress-proxy --egress-proxy-authz-url http://authz.example.com
```

```bash
postman runner start --id 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12 --key 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12 --metrics --metrics-port 12044 --ssl-extra-ca-certs /path/to/certs.pem
```

--------------------------------

### Postman Vault: Get, Set, and Unset Secrets

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-vault

Demonstrates the basic usage of Postman Vault methods for retrieving, storing, and deleting secrets. These methods are asynchronous and return Promises, requiring the `await` operator for proper execution. The `get` method retrieves a secret's value, `set` stores a new secret or updates an existing one, and `unset` removes a secret.

```javascript
console.log(await pm.vault.get("secretKey"));
await pm.vault.set("secretKey", "newValue");
await pm.vault.unset("secretKey");
```

--------------------------------

### Get Help for Postman Collection Transformer Convert Command

Source: https://learning.postman.com/docs/getting-started/importing-and-exporting/importing-data

This command displays the help information for the `convert` command of the Postman Collection Transformer. It lists all available options and their descriptions, which can be useful for understanding the full capabilities of the tool.

```bash
postman-collection-transformer convert -h

```

--------------------------------

### Run Postman Monitor using GitHub Actions CLI

Source: https://learning.postman.com/docs/postman-cli/postman-cli-run-monitor

This snippet demonstrates how to automate Postman monitor runs within a GitHub Actions CI/CD pipeline. It installs the Postman CLI, logs in using an API key, and triggers a monitor run using a provided monitor ID. Ensure you configure the POSTMAN_API_KEY secret and MONITOR_ID variable in your GitHub repository settings.

```yaml
name: Automate monitors using Postman CLI

on: push

jobs:
  automated-api-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Install Postman CLI
        run: npm install -g postman-cli

      - name: Login to Postman CLI
        run: postman login --with-api-key ${{ secrets.POSTMAN_API_KEY }}

      - name: Run monitor
        run: postman monitor run ${{ vars.MONITOR_ID }}

```

--------------------------------

### Add Description to API Parameters

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Clarifies the purpose and usage of API parameters for consumers. This example shows how to add a 'description' to a query parameter in an OpenAPI (Swagger) definition.

```yaml
Copyswagger: '2.0'
# ...
paths:
  /resources:
    get:
      parameters:
        - name: status
          description: filters resources on their status
          in: query
          type: string

```

--------------------------------

### Show Timestamps in CLI and JSON Reports

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-built-in-reporters

This example illustrates how to generate collection run reports with both CLI and JSON reporters enabled, and additionally configure the CLI reporter to display timestamps for each request. The `--reporter-cli-show-timestamps` option is used for this purpose.

```bash
newman run my-collection.json -r cli,json --reporter-cli-show-timestamps

```

--------------------------------

### HashiCorp Vault Policy for OIDC Identity Provider Setup

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This HashiCorp Vault policy grants the necessary permissions to set up an OIDC identity provider. It allows read and create capabilities for OIDC clients and providers, sudo/update for auth methods, update/create for auth endpoints, and update for system policies.

```hcl
path "/identity/oidc/client/*" {
    capabilities=["create", "read"]
}

path "/identity/oidc/provider/*" {
    capabilities=["create", "read"]
}

path "/sys/auth/*" {
    capabilities=["sudo", "update"]
}

path "/auth/*" {
    capabilities=["update", "create"]
}

path "/sys/policy/*" {
    capabilities=["update"]
}
```

--------------------------------

### Add Terms of Service URL to OpenAPI Info

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This OpenAPI example shows how to add the URL for an API's Terms of Service to the info object. This is a recommended practice, especially for public APIs, to ensure users understand the service conditions.

```yaml
Copyopenapi: '3.0.3'
info:
  title: An API name
  version: '1.0'
  termsOfService: https://example.com/tos

```

--------------------------------

### GET /user

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Retrieves details about a particular user. This endpoint is secured with OAuth2 authentication.

```APIDOC
## GET /user

### Description
Returns details about a particular user.

### Method
GET

### Endpoint
/user

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **user_details** (object) - Contains the user's information.

#### Response Example
```json
{
  "user_details": {
    "id": "123e4567-e89b-12d3-a456-426614174000",
    "username": "john.doe",
    "email": "john.doe@example.com"
  }
}
```

### Security
- **OAuth2**: Requires scopes 'read' and 'write'.
```

--------------------------------

### Define ConfigMap for Deployment Environment Variables

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/daemonset

This snippet demonstrates how to define a Kubernetes ConfigMap to store environment variables for a deployment. It includes the API version, kind, metadata, and data sections, where key-value pairs for environment variables are specified. This is useful for managing non-sensitive configuration data.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: deployment-service-config
data:
  POSTMAN_INSIGHTS_PROJECT_ID: "svc_xxxxxxxxxx"
  POSTMAN_INSIGHTS_API_KEY: "PMAK_xxxxxxxx"

```

--------------------------------

### HTTP GET Request for Pagination

Source: https://learning.postman.com/docs/postman-flows/build-flows/structure/loops/loops-pagination

This snippet defines an HTTP GET request to the Postman Echo API for paginating responses. It uses a 'pageNumber' query parameter, which will be dynamically updated within the Postman Flow.

```json
{
  "method": "GET",
  "url": "https://postman-echo.com/get?pageNumber={{value}}"
}
```

--------------------------------

### Configure Newman for CI/CD Bail on Error

Source: https://learning.postman.com/docs/collections/using-newman-cli/installing-running-newman

Configures Newman to stop a collection run and exit with a status code of 1 if any test case fails. This is useful for integrating with CI/CD pipelines to fail builds on test errors.

```bash
newman run my-collection.json --bail 1

```

--------------------------------

### Initialize and Run Postman Collection with Runtime Library (Node.js)

Source: https://learning.postman.com/docs/developer/runtime-library

This snippet shows how to initialize the Postman Runtime library and use it to run a Postman collection. It requires the 'postman-runtime' and 'postman-collection-sdk' npm packages. The function accepts a collection object and configuration options, then executes the collection run, providing callbacks for different stages of the process.

```javascript
const runtime = require('postman-runtime');
const sdk = require('postman-collection'); // Assuming Collection SDK is required

var runner = new runtime.Runner();

// Collection object constructed using the Collection SDK
var collection = new sdk.Collection();

runner.run(collection, {
  data: [],
  timeout: {
    request: 30000,
    script: 5000
  },
  iterationCount: 1,
  // other options...

}, function (err, run) {
  // Callbacks to run as the collection runs
  // run.start(callbacks);
  // Example callback structure (actual callbacks depend on use case):
  const callbacks = {
    start: function(err, summary) { console.log('Collection run started'); },
    beforeRequest: function(err, req) { console.log('About to send request: ' + req.url); },
    request: function(err, req, res) { console.log('Request completed'); },
    afterRequest: function(err, req, res) { console.log('After request'); },
    beforeItem: function(err, item) { console.log('Before item: ' + item.name); },
    item: function(err, item) { console.log('Item finished: ' + item.name); },
    beforeprerequest: function(err, script) { console.log('Before prerequest script'); },
    prerequest: function(err, script) { console.log('Prerequest script finished'); },
    beforetest: function(err, script) { console.log('Before test script'); },
    test: function(err, script) { console.log('Test script finished'); },
    beforeIteration: function(err, iteration) { console.log('Before iteration'); },
    iteration: function(err, iteration) { console.log('Iteration finished'); },
    beforeDone: function(err, summary) { console.log('Before done'); },
    done: function(err, summary) { console.log('Collection run finished'); }
  };
  run.start(callbacks);
});

```

--------------------------------

### Test Response Trailers Presence and Value with Postman

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

This script checks for the presence and specific values of response trailers, like 'grpc-status-details-bin'. It demonstrates using `pm.response.to.have.trailer()` and `pm.expect(pm.response.trailers.get()).to.equal()` for trailer validation. This is useful for debugging gRPC services.

```JavaScript
pm.test('"grpc-status-details-bin" is present in response trailers', () => {
  pm.response.to.have.trailer('grpc-status-details-bin');

  // Using pm.expect
  pm.expect(pm.response.trailers.has('grpc-status-details-bin')).to.be.true;
});
```

```JavaScript
pm.test('"grpc-status-details-bin" response trailer is "dummy-value"', () => {
  pm.response.to.have.trailer('grpc-status-details-bin', 'dummy-value');

  // Using pm.expect
  pm.expect(pm.response.trailers.get('grpc-status-details-bin')).to.equal('dummy-value');
});
```

--------------------------------

### Add Description to OpenAPI Info Object (YAML)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This example shows how to add a description to the 'info' object in an OpenAPI specification. A description is crucial for providing API consumers with information about the API's purpose and usage.

```yaml
Copyswagger: '2.0'
info:
  title: An API name
  version: '1.0'
  description: An API description

```

--------------------------------

### Create Placeholder Variable in Postman Request Builder

Source: https://learning.postman.com/docs/sending-requests/variables

This example illustrates how to create a placeholder variable directly within the Postman request builder by using double curly braces. This variable will not have a scope initially and can be used for testing or sharing with API consumers.

```text
{{username}}
```

--------------------------------

### Reference ConfigMap and Secret in Deployment

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/daemonset

This snippet illustrates how a Kubernetes deployment can reference both a ConfigMap and a Secret to provide environment variables to its containers. The `envFrom` section lists both `configMapRef` and `secretRef`, allowing the deployment to consume configuration from both sources. This approach is used to manage a mix of sensitive and non-sensitive data.

```yaml
spec:
  ...
  template:
    ...
    spec:
      containers:
        - name: deployment-service
          image: deployment-service-image
          envFrom:
            - configMapRef:
                name: deployment-service-config
            - secretRef:
                name: deployment-service-secret
  ...
...

```

--------------------------------

### Unsetting Variables in Postman Scripts

Source: https://learning.postman.com/docs/sending-requests/variables/variables

Provides an example of how to remove a variable using the `unset()` method on the respective variable scope (e.g., `pm.environment.unset()`). This action removes the variable from the specified scope.

```javascript
pm.environment.unset("variable_key");
```

--------------------------------

### Time Component Extraction: Hours, Minutes, Seconds, Milliseconds

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Illustrates how to extract hours, minutes, seconds, and milliseconds from a date (using $now() as an example) with their respective functions.

```FQL
$hours($now()) & ":" & $minutes($now()) & ":" & $seconds($now()) & ":" & $milliSeconds($now())
```

--------------------------------

### Postman Item Group Example (JSON)

Source: https://learning.postman.com/collection-format/getting-started/structure-of-a-collection

Demonstrates an Item Group in Postman, used to organize multiple items or other item groups. It has an ID, name, description, and an 'item' array containing its contents.

```json
{
  "id": "my-first-itemgroup",
  "name": "First Folder",
  "description": "This ItemGroup contains two Items.",
  "item": [
    {
      "id": "1",
      "name": "Item A",
      "request": "http://postman-echo.com/get"
    },
    {
      "id": "2",
      "name": "Item B",
      "request": "http://postman-echo.com/headers"
    }
  ]
}
```

--------------------------------

### MCP Tool Definition Resource Configuration

Source: https://learning.postman.com/docs/postman-ai/mcp-server-flows/create-mcp-server-flow

Shows the structure for adding resources to the 'Body' section of a toolDefinition scenario, including URI, name, title, description, and mimeType.

```json
Copy"resources": [
      {
        "uri": "http://example.com/data.json",
        "name": "data.js",
        "title": "Data file",
        "description": "File containing important data",
        "mimeType": "application/json"
      }
    ]


```

--------------------------------

### Filter Path Allowances | Postman CLI

Source: https://learning.postman.com/docs/insights/reference/agent/apidump

This example demonstrates how to allow traffic only for specific admin endpoints using the apidump command's path-allow flag.

```bash
postman-insights-agent apidump ... --path-allow '*/admin/*' ...
```

--------------------------------

### Get Constant Value

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Retrieves predefined mathematical constants by their string name, such as 'e', 'pi', 'ln2', etc. Returns a number.

```Postman Functions
$constant('e') -> 2.718281828459045
```

--------------------------------

### Check, Get, and List Cookies for Requested Domain (Postman)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-cookies

Utilize `pm.cookies` methods to check for a cookie's existence, retrieve its value, or get all cookies for the domain associated with the current request. These methods are synchronous and directly accessible.

```javascript
if (pm.cookies.has("cookieName")) {
  let cookieValue = pm.cookies.get("cookieName");
  console.log(cookieValue);
}

let allCookies = pm.cookies.toObject();
console.log(allCookies);
```

--------------------------------

### Test if Response Body Matches String

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Asserts that the entire response body exactly matches a given string. This is useful for verifying simple text-based responses.

```javascript
pm.test("Body is string", function () {
  pm.response.to.have.body("whole-body-text");
});
```

--------------------------------

### Test Response Cookies

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Verifies the presence of a cookie by name and checks if a specific cookie has a given value. This functionality relies on cookies being set in the HTTP response.

```javascript
pm.test("Cookie isLoggedIn is present", () => {
  pm.expect(pm.cookies.has('isLoggedIn')).to.be.true;
});
```

```javascript
pm.test("Cookie isLoggedIn has value 1", () => {
  pm.expect(pm.cookies.get('isLoggedIn')).to.eql('1');
});
```

--------------------------------

### Define Mock Server Response with $body Helper (JSON)

Source: https://learning.postman.com/docs/design-apis/mock-apis/create-dynamic-responses

This example demonstrates how to construct a mock server response using Postman's `$body` template helper. It dynamically inserts the 'username' value from the incoming request body into the response, alongside a randomly generated UUID.

```json
{
    "username": "{{$body 'username' 'postman'}}",
    "id": "{{$randomUUID}}"
}
```

--------------------------------

### Apply Reporter Options - All Reporters

Source: https://learning.postman.com/docs/postman-cli/postman-cli-reporters

This example shows how to apply an option to all reporters simultaneously. The `--reporter-omitHeaders` flag will cause all configured reporters (in this case, JSON and HTML) to omit headers from their respective reports. Options specified for single reporters will override this setting.

```bash
postman collection run <collection-id> -r json,html --reporter-omitHeaders

```

--------------------------------

### Assert Response Value Against Variable

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Compares a value from the JSON response body against a Postman variable (e.g., environment variable). This requires the response to be JSON and the specified variable to be set.

```javascript
pm.test("Response property matches environment variable", function () {
  pm.expect(pm.response.json().name).to.eql(pm.environment.get("name"));
});
```

--------------------------------

### Filter Host Exclusions | Postman CLI

Source: https://learning.postman.com/docs/insights/reference/agent/apidump

This example demonstrates how to exclude traffic to a specific host (deb.debian.org) from being captured using the apidump command's host-exclusions flag.

```bash
postman-insights-agent apidump ... --host-exclusions 'deb\.debian\.org' ...
```

--------------------------------

### Current Time Retrieval in Different Formats

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Shows how to get the current timestamp in ISO 8601 format using $now() and in Unix milliseconds since the epoch using $millis().

```FQL
$now()
```

```FQL
$millis()
```

--------------------------------

### Reference ConfigMap in Deployment Environment Variables

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/daemonset

This YAML snippet shows how to reference a ConfigMap within a Kubernetes deployment's pod specification to inject environment variables. The `envFrom` field with `configMapRef` allows all key-value pairs from the specified ConfigMap to be added as environment variables to the container. This simplifies environment variable management for containers.

```yaml
spec:
  ...
  template:
    ...
    spec:
      containers:
        - name: deployment-service
          image: deployment-service-image
          envFrom:
            - configMapRef:
                name: deployment-service-config
  ...
...

```

--------------------------------

### Test Common Property in All Messages

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Verifies if a specific property exists across all messages in the response. This is useful for ensuring consistency in message structures.

```javascript
pm.test('All users have "company" in their profile', () => {
  pm.response.messages.to.have.property('isActive');
});
```

--------------------------------

### Specifications API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

The Specs APIs enable you to manage your API specifications created in Postman’s Spec Hub. Programmatically create, update, get definitions, generate collections from specs, or specs from collections, and synchronize collections and specs with their source.

```APIDOC
## Specifications API

### Description
Manages API specifications in Postman's Spec Hub. Supports creating, updating, retrieving specifications, generating collections from specs and vice-versa, and synchronizing with source.

### Method
GET, POST, PUT, DELETE

### Endpoint
/specs

### Parameters
None specified in the provided text.

### Request Example
Not specified in the provided text.

### Response
#### Success Response (200)
Details about API specification operations.

#### Response Example
Not specified in the provided text.
```

--------------------------------

### Test Response Metadata Presence and Value with Postman

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

These scripts verify the presence and specific values of response metadata, such as the 'content-type'. They showcase using `pm.response.to.have.metadata()` and `pm.expect(pm.response.metadata.get()).to.equal()` for checking headers. Similar assertions can be made for request metadata using `pm.request`.

```JavaScript
pm.test('"content-type" is present in response metadata', () => {
  pm.response.to.have.metadata('content-type');

  // Using pm.expect
  pm.expect(pm.response.metadata.has('content-type')).to.be.true;
});
```

```JavaScript
pm.test('"content-type" response metadata is "application/grpc"', () => {
  pm.response.to.have.metadata('content-type', 'application/grpc');

  // Using pm.expect
  pm.expect(pm.response.metadata.get('content-type')).to.equal('application/grpc');
});
```

--------------------------------

### Add Summary to API Operations

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Improves API discoverability by providing a concise summary for each operation. This snippet illustrates adding a 'summary' field to a GET operation in an OpenAPI (Swagger) definition.

```yaml
Copyswagger: '2.0'
# ...
paths:
  /resources:
    get:
      summary: A GET operation summary

```

--------------------------------

### OAuth2 Security - Access Code Flow

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures secure OAuth2 authentication by recommending the 'accessCode' flow over the deprecated 'password' flow. This example shows a typical configuration for the accessCode flow.

```APIDOC
## OAuth2 Security

### Description
This section details the recommended OAuth2 security configuration, emphasizing the use of the 'accessCode' flow for enhanced security.

### Method
N/A (Configuration)

### Endpoint
N/A (Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

#### Success Response (200)
N/A

#### Response Example
N/A

```yaml
swagger: '2.0'
#...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://my.auth.example.com/
    tokenUrl: https://my.token.example.com/
    scopes:
      write: modify data
      read: read data
```
```

--------------------------------

### Apply Reporter Options - Single Reporter

Source: https://learning.postman.com/docs/postman-cli/postman-cli-reporters

This example demonstrates how to apply a specific option to a single reporter when using multiple reporters. The `--reporter-json-omitHeaders` flag ensures that only the JSON reporter will omit headers from the report.

```bash
postman collection run <collection-id> -r json,html --reporter-json-omitHeaders

```

--------------------------------

### Postman Vault Secrets API

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-vault

This section details the methods available for interacting with Postman Vault secrets. These include getting, setting, and unsetting secrets, all of which are asynchronous operations.

```APIDOC
## pm.vault.get(secretKey:String)

### Description
Gets the value of the vault secret with the specified name in your Postman Vault.
Returns the value of the vault secret. You can append a string to the value of a vault secret using the `+` operator before or after the method.

### Method
GET (conceptual, as it's a script method)

### Endpoint
N/A (Script method)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```javascript
console.log(await pm.vault.get("secretKey"));
```

### Response
#### Success Response (200)
- **secretValue** (String) - The value of the vault secret.

#### Response Example
```json
{
  "secretValue": "yourSecretValue"
}
```

## pm.vault.set(secretKey:String, secretValue:*)

### Description
Sets a vault secret with the specified name and value in your Postman Vault. Postman doesn’t support setting the value of vault secrets linked with external vaults.

### Method
POST (conceptual, as it's a script method)

### Endpoint
N/A (Script method)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **secretKey** (String) - Required - The name of the secret to set.
- **secretValue** (*) - Required - The value of the secret.

### Request Example
```javascript
await pm.vault.set("secretKey", "newValue");
```

### Response
#### Success Response (200)
- No explicit response body, operation is confirmed by absence of errors.

#### Response Example
```json
{
  "message": "Secret set successfully"
}
```

## pm.vault.unset(secretKey:String)

### Description
Removes a specified vault secret from your Postman Vault.

### Method
DELETE (conceptual, as it's a script method)

### Endpoint
N/A (Script method)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **secretKey** (String) - Required - The name of the secret to remove.

### Request Example
```javascript
await pm.vault.unset("secretKey");
```

### Response
#### Success Response (200)
- No explicit response body, operation is confirmed by absence of errors.

#### Response Example
```json
{
  "message": "Secret unset successfully"
}
```
```

--------------------------------

### Map Array Values with $map and $string

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $map() function applies a given function to each element of an array. This example uses $string to convert numerical amounts in a payments array to strings.

```FQL
$map(input.payments[].amount,$string)
```

--------------------------------

### Docker: Run Postman Runner Container

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

This command runs a Docker container from the 'postman-runner' image. It sets the necessary environment variables for the runner ID, key, and authorization service URL. The container is configured to be removed upon exit (`--rm`).

```bash
docker run --rm \
  -e POSTMAN_RUNNER_ID="<runner-id>" \
  -e POSTMAN_RUNNER_KEY="<runner-key>" \
  -e AUTHORIZATION_SERVICE_URL="<authorization-service-url>" \
  postman-runner

```

--------------------------------

### Test Response Headers

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Checks for the presence of a specific response header and verifies if a header contains a particular string value. Requires a valid HTTP response with headers.

```javascript
pm.test("Content-Type header is present", () => {
  pm.response.to.have.header("Content-Type");
});
```

```javascript
pm.test("Content-Type header is application/json", () => {
  pm.expect(pm.response.headers.get('Content-Type')).to.include('application/json');
});
```

--------------------------------

### Connect Password Manager Service Interface (Linux)

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Connects the Postman Enterprise snap to the password manager service interface, which is mandatory for securely storing local data. This ensures that sensitive information is encrypted.

```bash
sudo snap connect postman-enterprise:password-manager-service

```

--------------------------------

### Create OIDC Provider (Vault CLI)

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command creates an OIDC provider in HashiCorp Vault. For HCP Vault, the `issuer` must be the public cluster URL. For self-managed Vault, it's the Vault cluster address. If a custom scope was created, include it in `scopes_supported`. Ensure you have the correct OIDC client ID and issuer URL.

```shell
vault write identity/oidc/provider/<oidc-provider-name> allowed_client_ids="<oidc-client-id>" issuer="<vault-cluster-url>" scopes_supported=["<scope-name>"]
```

--------------------------------

### Environment Variables

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-variables

Manage environment variables for your Postman requests. This includes getting, setting, replacing, unsetting, and clearing variables from the active environment.

```APIDOC
## Environment Variables

### `pm.environment.get(variableName:String)`

Gets the value of a variable with the specified name in the active environment.
Returns the value of the environment variable.
> You can append a string to the value of an environment variable using the `+` operator before or after the method.

### `pm.environment.set(variableName:String, variableValue:*)`

Sets a variable with the specified name and value in the active environment.

### `pm.environment.replaceIn(variableName:string)`

Gets the resolved value of a dynamic variable inside a script using the syntax `{{$dynamicVariableName}}`
Returns the value of the dynamic variable.

### `pm.environment.toObject()`

Gets all variables in the active environment.
Returns all environment variables and their values as an object.

### `pm.environment.unset(variableName:String)`

Removes a specified variable from the active environment.

### `pm.environment.clear():function`

Clears all variables from the active environment.
```

--------------------------------

### pm.test example for checking JSON response body

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-test-expect

Demonstrates how to use `pm.test` and `pm.expect` to check if a JSON response body contains a specific boolean value. It parses the response body and checks the `success` property.

```javascript
pm.test("Response body has success = true", function () {
    const jsonData = pm.response.json();
    // value: jsonData.success (a boolean)
    // Assertion: checks if it equals true
    pm.expect(jsonData.success).to.eql(true);
});
```

--------------------------------

### Schema Best Practices

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Guidelines for defining schemas, properties, and array constraints to improve API documentation and usability.

```APIDOC
## Schema Best Practices

### Reusable Schemas
Ensure all reusable schemas in the `definitions` object have a `description` to provide clarity to API consumers.

#### Example
```yaml
swagger: '2.0'
# ...
definitions:
  aReusableSchema:
    description: a reusable schema description
    type: object
```

### Schema Properties
All properties within a schema object must have a `description` to explain their purpose and usage.

#### Example
```yaml
swagger: '2.0'
#...
paths:
  /resources:
    get:
      responses:
        '200':
          description: a success response
          schema:
            properties:
              aProperty:
                description: a property description
                type: string
```

### Array Constraints
Properties of type array must define `minItems` and `maxItems` to set clear boundaries for the number of elements.

#### Example
```yaml
swagger: '2.0'
# ...
definitions:
  anObject:
    properties:
      aList:
        type: array
        minItems: 1
        maxItems: 100
        items:
          type: object
```
```

--------------------------------

### Day of the Week Extraction

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Shows the usage of the $dayOfTheWeek() function to get a numerical representation of the day of the week for a given date.

```FQL
$dayOfTheWeek($now())
```

--------------------------------

### Mapping and Sorting Data with TypeScript in Postman Flows

Source: https://learning.postman.com/docs/postman-flows/build-flows/structure/loops/overview

Demonstrates mapping and sorting data using TypeScript `map()` and `sort()` methods within a Postman Flows 'Evaluate' block. This example transforms well data to include specific fields and orders it by elevation.

```TypeScript
CopywellList = wells.map((row) => ({"Elevation": row["Elevation"],"Status": row["Status of Well"]}));
wellList.sort((a, b) => a.Elevation - b.Elevation);
```

--------------------------------

### URL-encoded Request Body Parameter

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

An example of a single parameter within a URL-encoded request body. It shows the key, value, and optional 'disabled' and 'description' fields.

```json
{
  "key": "name",
  "value": "John Doe",
  "disabled": false,
  "description": ""
}
```

--------------------------------

### Get Distinct Array Elements

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Creates a new array containing only the unique elements from the input array, effectively removing duplicates.

```Postman Functions
$distinct(["a", "b", "b", "c"]) -> ["a", "b", "c"]
```

--------------------------------

### Check Kubernetes Pod Status

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/sidecar

This `kubectl` command lists the pods within a specified namespace. It is used to verify that the Postman Insights Agent sidecar is running correctly alongside your application pods.

```bash
kubectl get pods -n <your_namespace>
```

--------------------------------

### Example Dynamic Mock Server Response

Source: https://learning.postman.com/docs/design-apis/mock-apis/create-dynamic-responses

This JSON object illustrates a typical response generated by a Postman mock server when using dynamic variables. The placeholders like {{$randomFullName}} have been replaced with actual randomized data, showcasing the simulated output.

```json
{
    "name": "Cielo McClure",
    "userName": "Aurelie.Lockman",
    "location": "Kubhaven",
    "company": "Runolfsdottir, Bernhard and Hodkiewicz",
    "jobTitle": "Direct Branding Liaison",
    "updatedAt": "1565088856"
}
```

--------------------------------

### Secure OAuth2 Authorization URL

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This example shows how to configure the authorization URL for OAuth 2.0 using HTTPS. This ensures that authorization credentials are exchanged securely between the client and the authorization server.

```yaml
components:
  securitySchemes:
     OauthScheme:
        type: oauth2
        flows:
          authorizationCode:
            authorizationUrl: https://my.auth.example.com/
```

--------------------------------

### kube helm-fragment Command

Source: https://learning.postman.com/docs/insights/reference/agent/kube-helm-fragment

Prints a container definition for the Postman Insights Agent sidecar to be inserted into a Helm Chart template.

```APIDOC
## kube helm-fragment Command Reference

### Description
The `kube helm-fragment` command generates a container definition that can be inserted into a Helm Chart template to add the Postman Insights Agent as a sidecar container.

### Usage
```bash
postman-insights-agent kube helm-fragment [flags]
```

### Flags

*   **`--filter`** (string) - Used to match packets going to and coming from your API service.
*   **`--host-allow`** (strings) - Allows only HTTP hosts matching regular expressions.
*   **`--host-exclusions`** (strings) - Removes HTTP hosts matching regular expressions.
*   **`--interfaces`** (strings) - List of network interfaces to listen on. Defaults to all interfaces on host.
*   **`--path-allow`** (strings) - Allows only HTTP paths matching regular expressions.
*   **`--path-exclusions`** (strings) - Removes HTTP paths matching regular expressions.
*   **`--rate-limit`** (float) - Number of requests per minute to capture.
*   **`--repro-mode`** - Turns on Repro Mode to send request and response payloads to Postman.
*   **`-h`, `--help`** - Help for `helm-fragment`.

### Global Flags

*   **`--log-format`** (string) - Set to `'color'`, `'plain'` or `'json'` to control the log format.
*   **`--project`** (string) - Your Postman Insights project ID.
*   **`--proxy`** (string) - The domain name, IP address, or URL of an HTTP proxy server to use.
```

--------------------------------

### JSON Data File Example for Newman Iterations

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

This JSON structure defines data to be used across multiple iterations of a Newman collection run. Each object in the array represents a set of variables for a single iteration, allowing for dynamic testing with different inputs.

```json
[
    {
        "url": "http://127.0.0.1:5000",
        "user_id": "1",
        "id": "1",
        "token_id": "123123"
    },
    {
        "url": "http://postman-echo.com",
        "user_id": "2",
        "id": "2",
        "token_id": "899899"
    }
]
```

--------------------------------

### Postman Item with Pre-request and Test Events (JavaScript)

Source: https://learning.postman.com/collection-format/getting-started/structure-of-a-collection

An example of a Postman item configured with both pre-request and test events. These events contain JavaScript code executed before the request is sent and after the response is received, respectively.

```json
{
  "id": "evented-item",
  "name": "Item with Events",
  "description": "This is an Item that contains `test and `prerequest` events.",
  "request": "http://echo.getpostman.com/get",
  "event": [
    {
      "listen": "prerequest",
      "script": {
        "type": "text/javascript",
        "exec": "console.log('We are in the pre-request script, the request has not run yet!')"
      }
    },
    {
      "listen": "test",
      "script": {
        "type": "text/javascript",
        "exec": "console.log('We are using the test script now, and the request was already sent!')"
      }
    }
  ]
}
```

--------------------------------

### Test Messages Against JSON Schema

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Validates that the received messages conform to a defined JSON Schema. This ensures data integrity and structure compliance for all or specific messages.

```javascript
const schema = {
  type: "object",
  properties: {
    username: {
      type: "string",
      pattern: "^[a-z0-9_-]{3,16}$"
    }
  }
};

pm.test('All response messages have correct username', () => {
  pm.response.messages.to.have.jsonSchema(schema);
});

pm.test('Assert on a specific message', () => {
  pm.expect(pm.response.messages.idx(10).data).to.have.jsonSchema(schema);
});
```

--------------------------------

### Check Postman Insights Agent Status/Logs (Bash)

Source: https://learning.postman.com/docs/insights/get-started/ec2

Use this command to monitor the real-time logs and status of the Postman Insights Agent service. This is useful for troubleshooting and verifying the agent is running correctly.

```bash
sudo journalctl -fu postman-insights-agent
```

--------------------------------

### Customizing Mock Server Responses with Headers

Source: https://learning.postman.com/docs/design-apis/mock-apis/tutorials/mock-with-api

This section details how to use optional request headers to influence the behavior of Postman mock servers, enabling specific response matching and delays.

```APIDOC
## Postman Mock Server Custom Headers

Postman mock servers can be customized using optional request headers to control response behavior. These headers allow for precise control over which saved examples are returned, bypassing the default matching algorithm.

### How to Add Custom Headers:
1. Navigate to the **Headers** tab of your collection's request.
2. In the **Key** field, enter the desired custom header name. For a list of available mock server headers, enter `x-mock`.
3. In the **Value** field, provide the corresponding value for the header.

### Available Custom Headers:

#### `x-mock-response-code`
- **Description**: Specifies a particular HTTP response code for the mock server's response. For example, setting this to `500` will return an example with a 500 HTTP status code.
- **Method**: Any (typically POST, PUT, GET, DELETE)
- **Endpoint**: N/A (Header specific)
- **Parameters**: None (Header value)
- **Request Example**: (Header in request)
  ```
  x-mock-response-code: 500
  ```

#### `x-mock-response-name` / `x-mock-response-id`
- **Description**: Selects a specific saved example by matching its `name` or `id`. The example `id` or `name` can be retrieved using the Postman API's GET `/collections/{collectionId}` endpoint.
- **Note**: Ensure unique names for saved examples to avoid ambiguity. Use `x-mock-response-id` for guaranteed accuracy if names are not unique.
- **Method**: Any (typically POST, PUT, GET, DELETE)
- **Endpoint**: N/A (Header specific)
- **Parameters**: None (Header value)
- **Request Example**: (Header in request)
  ```
  x-mock-response-name: "My Specific Response Name"
  ```
  or
  ```
  x-mock-response-id: "a1b2c3d4-e5f6-7890-1234-567890abcdef"
  ```

#### `x-mock-match-request-body`
- **Description**: Enables matching of the saved example based on the request body. Requires the `Content-Type` header to be set in the example and match the request's `Content-Type`.
- **Method**: Any (typically POST, PUT, GET, DELETE)
- **Endpoint**: N/A (Header specific)
- **Parameters**: `true` (boolean)
- **Request Example**: (Header in request)
  ```
  x-mock-match-request-body: true
  ```

#### `x-mock-match-request-headers`
- **Description**: Enables matching of the saved example based on specified request headers. The value should be a comma-separated string of header keys to match (case-insensitive).
- **Method**: Any (typically POST, PUT, GET, DELETE)
- **Endpoint**: N/A (Header specific)
- **Parameters**: Comma-separated string of header keys
- **Request Example**: (Header in request)
  ```
  x-mock-match-request-headers: "Content-Type,Authorization"
  ```

#### `x-mock-response-delay`
- **Description**: Introduces a delay to the mock server response, in milliseconds. Accepts a range from 1 to 180000.
- **Note**: This header takes precedence over any delay configured in the mock server settings.
- **Method**: Any (typically POST, PUT, GET, DELETE)
- **Endpoint**: N/A (Header specific)
- **Parameters**: Milliseconds (integer)
- **Request Example**: (Header in request)
  ```
  x-mock-response-delay: 2000
  ```

### Note on Body and Header Matching:
Body and header matching can also be configured directly within the mock server settings.
```

--------------------------------

### Get Audit Logs

Source: https://learning.postman.com/docs/administration/managing-your-team/audit-logs

Retrieves audit log events for your Postman team. This endpoint allows you to integrate Postman's audit logs with your security information and event management (SIEM) tools.

```APIDOC
## GET /auditlogs

### Description
Retrieves a list of audit log events for your Postman team. This endpoint is useful for integrating Postman's audit trail with external security monitoring systems.

### Method
GET

### Endpoint
/auditlogs

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of audit log events to return per page.
- **cursor** (string) - Optional - A cursor for paginating through results. Use the `nextCursor` from a previous response.
- **startDate** (string) - Optional - The start date for filtering events (YYYY-MM-DD).
- **endDate** (string) - Optional - The end date for filtering events (YYYY-MM-DD).
- **eventType** (string) - Optional - Filters events by a specific event type.
- **actorId** (integer) - Optional - Filters events by the ID of the team member who performed the action.

### Request Example
```json
{
  "example": ""
}
```

### Response
#### Success Response (200)
- **logs** (array) - An array of audit log event objects.
  - **id** (integer) - Unique identifier for the audit log event.
  - **ip** (string) - IP address of the actor.
  - **userAgent** (string) - User agent of the actor.
  - **action** (string) - The type of event that occurred.
  - **timestamp** (string) - ISO 8601 formatted date and time of the action.
  - **message** (string) - Description of the audit log event.
  - **data** (object) - Contains details about the actor, user, team, and variables.
    - **actor** (object) - Information about the team member who performed the action.
      - **name** (string) - Actor's name.
      - **username** (string) - Actor's username.
      - **email** (string) - Actor's email address.
      - **id** (integer) - Actor's unique identifier.
      - **active** (boolean) - Whether the actor's account is active.
    - **user** (object) - Information about the team member affected by the action.
      - **name** (string) - User's name.
      - **username** (string) - User's username.
      - **email** (string) - User's email address.
      - **id** (integer) - User's unique identifier.
    - **team** (object) - Information about the team.
      - **name** (string) - Team's name.
      - **id** (integer) - Team's unique identifier.
    - **variables** (object) - Details about the performed action.
- **nextCursor** (string) - Cursor for the next page of results.

#### Response Example
```json
{
  "logs": [
    {
      "id": 12345,
      "ip": "192.168.1.1",
      "userAgent": "PostmanRuntime/7.28.0",
      "action": "user_signed_in",
      "timestamp": "2023-10-27T10:30:00Z",
      "message": "User John Doe signed in.",
      "data": {
        "actor": {
          "name": "John Doe",
          "username": "johndoe",
          "email": "john.doe@example.com",
          "id": 101,
          "active": true
        },
        "user": {
          "name": "John Doe",
          "username": "johndoe",
          "email": "john.doe@example.com",
          "id": 101
        },
        "team": {
          "name": "Example Team",
          "id": 50
        },
        "variables": {}
      }
    }
  ],
  "nextCursor": "someCursorString"
}
```
```

--------------------------------

### OpenAPI: Secure API Key Transmission with HTTPS

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This example configures an OpenAPI specification to use HTTPS for API key transmission, mitigating the risk of API keys being exposed in plain text over unencrypted channels.

```yaml
servers:
  - url: https://my.api.example.com/
    description: API server
#...
components:
  securitySchemes:
    AuthKeyAuth:
      type: apiKey
      name: api-key
      in: header
#...
security:
  - AuthKeyAuth: []

```

--------------------------------

### Get Substring Before Separator

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $substringBefore helper function returns the part of a string that comes before the first occurrence of a specified separator. It takes the string and the separator as arguments. If the separator is not found, the original string is returned.

```postman-helper
$substringBefore( "john@gmail.com", "@") -> "john"
```

--------------------------------

### Assert Current Environment in Postman Script

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

This script verifies that the currently active environment in Postman matches a specified name. It's useful for ensuring tests are run against the correct environment, such as 'Production'. The `.eql` assertion is used for equality comparison.

```javascript
pm.test("Check the active environment", () => {
  pm.expect(pm.environment.name).to.eql("Production");
});
```

--------------------------------

### pm.test for grouping gRPC messages

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-test-expect

Shows how to use `pm.test` to assert multiple conditions within a single gRPC test. This example checks if a response includes specific update events for different users.

```javascript
pm.test("Should receive update events for both users", function () {
  pm.response.messages.to.include({ action: 'update', userId: 'user1' });
  pm.response.messages.to.include({ action: 'update', userId: 'user2' });
});
```

--------------------------------

### Sort Array Numerically with $sort

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $sort() function sorts an array based on a provided comparison function. This example sorts an array of payment amounts in ascending order.

```FQL
$sort(input.payments[].amount,fn($i, $j){$i < $j})
```

--------------------------------

### Test Response Message Existence

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Asserts that a specific response message with exact properties exists. This is useful for verifying that the expected data structure and values are present in the response.

```javascript
pm.test('Correct user details are received', () => {
  pm.response.to.have.message({
    userId: '123',
    name: 'John Doe',
    email: 'john@example.com',
    phone: '+1-555-555-5555',
    age: 30,
    company: 'XYZ'
  });
});
```

--------------------------------

### Test Common Property Value in All Messages

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Asserts that a common property across all response messages has a specific value. This is useful for validating consistent data points.

```javascript
pm.test('All users are in same company', () => {
  pm.response.messages.to.have.property('company', 'XYZ');
});
```

--------------------------------

### Add Contact Information to OpenAPI Info Object (YAML)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This example demonstrates how to add a 'contact' object, including email and URL, to the 'info' section of an OpenAPI specification. This provides essential contact details for API consumers.

```yaml
Copyswagger: '2.0'
info:
  title: An API name
  version: '1.0'
  contact:
    email: support@example.com
    url: https://example.com/support

```

--------------------------------

### Create Spotify Environment with Credentials

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Creates a new Postman environment named 'Spotify' and populates it with user credentials such as user ID and authorization token. This is useful for onboarding users to authenticated API flows.

```javascript
Copy_pm('env.create', 'Spotify', {
  user_id: 'spotifyuser',
  authorization: 'Bearer 1234xyzd'
});
```

--------------------------------

### Postman POST Request Object Example (JSON)

Source: https://learning.postman.com/collection-format/getting-started/structure-of-a-collection

Shows a detailed JSON object representation of an HTTP POST request within a Postman item. It includes the URL, method, headers, and a URL-encoded request body.

```json
{
  "description": "This is a sample POST request",
  "url": "https://echo.getpostman.com/post",
  "method": "POST",
  "header": [
    {
      "key": "Content-Type",
      "value": "application/json"
    },
    {
      "key": "Host",
      "value": "echo.getpostman.com"
    }
  ],
  "body": {
    "mode": "urlencoded",
    "urlencoded": [
      {
        "key": "my-body-variable",
        "value": "Something Awesome!"
      }
    ]
  }
}
```

--------------------------------

### Audit Logs API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Monitor and analyze Postman Enterprise teams. Team Admins can review audit logs, filter by criteria, and get information about user activity and administrative actions.

```APIDOC
## Audit Logs API

### Description
Use the Audit Logs API to monitor and analyze your Postman Enterprise teams. Team Admins can review audit logs, filter by specific criteria, and get information about:
  * When users were added to, removed from, or invited to your team.
  * Which user performed a specific action—and when they did so.

### Method
GET

### Endpoint
/audit-logs
```

--------------------------------

### Reduce Array to Single Value with $reduce

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $reduce() function applies a function cumulatively to the elements of an array, reducing it to a single value. This example sums all the amount values in a payments array.

```FQL
$reduce(input.payments[].amount,fn($i, $j){$i + $j})
```

--------------------------------

### Referencing Vault Secrets in Postman

Source: https://learning.postman.com/docs/sending-requests/postman-vault/manage-vault-secrets-using-guided-auth

This format demonstrates how to reference vault secrets stored using Guided Auth within Postman. The `vault:` prefix, secret name, and authentication type suffix are essential for correct resolution.

```plaintext
{{vault:postman-api-key:value}}
```

--------------------------------

### Parse JSON Response Body

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Parses the response body as JSON, making it accessible for assertion. This is a fundamental step for validating structured data returned from an API.

```javascript
const responseJson = pm.response.json();
```

--------------------------------

### Get Day of the Week - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Returns the day of the week (0 for Sunday, 6 for Saturday) for a given timestamp. Helpful for weekly analysis or scheduling.

```Postman Script
$dayOftheWeek("2023-02-08") -> 3
$dayOftheWeek("2023-02-07") -> 2
```

--------------------------------

### Configure CLI Reporter Options

Source: https://learning.postman.com/docs/postman-cli/postman-cli-reporters

This example shows how to configure the CLI reporter for a Postman collection run. The `--reporter-cli-silent` option is used to turn off the CLI reporter, meaning no output will be displayed in the terminal.

```shell
postman collection run <collection-id> --reporter-cli-silent
```

--------------------------------

### Parse XML Response Body using xml2js

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Parses an XML response body into a JavaScript object using the 'xml2js' library. This enables programmatic access to XML data for testing purposes.

```javascript
var parseString = require('xml2js').parseString;
parseString(pm.response.text(), function (err, result) {
    console.log(result);
});
```

--------------------------------

### Configure Postman Insights Agent with API Key and Project ID (Bash)

Source: https://learning.postman.com/docs/insights/get-started/ec2

This command sets up the Postman Insights Agent on your EC2 instance using your API key and project ID. The `--repro-mode` flag enables encrypted payload data for rerunning requests. Ensure you replace placeholders with your actual credentials.

```bash
sudo POSTMAN_API_KEY=<your-api-key> postman-insights-agent ec2 setup --project <projectId> --repro-mode
```

--------------------------------

### Postman Package with Logger Function and Response Test

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/package-library

This example shows a Postman package named `postman_logger`. It includes a `logger` function to print messages to the Postman Console and uses the `pm` object to define a test that checks for a 200 status code in the API response. The `logger` function is exported.

```javascript
// package name: postman_logger
function logger (data) {
    console.log(`Logging information to the console, ${data}`)
}

pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});

module.exports = {
    logger
}

```

--------------------------------

### Create Public OIDC Client Application (Vault CLI)

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command creates a public OIDC client application in HashiCorp Vault. It specifies the redirect URIs Postman will use and allows all assignments. Ensure you have the necessary permissions to write to the identity OIDC client endpoint.

```shell
vault write identity/oidc/client/<client-application-name> redirect_uris="http://127.0.0.1:10545/,http://127.0.0.1:10534/" client_type=public assignments=allow_all
```

--------------------------------

### Create New Postman Environment

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Demonstrates the creation of a new Postman environment with specified key-value pairs. It handles potential failures if an environment with the same name already exists.

```javascript
Copy_pm('env.create', 'environment_name', {key: value}, runButtonIndex);
```

--------------------------------

### Apply Postman Insights Agent DaemonSet Manifest

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/daemonset

This command applies the Postman Insights Agent DaemonSet manifest file to your Kubernetes cluster. Ensure you have downloaded the 'postman-insights-agent-daemonset.yaml' file before running this command. This step sets up necessary resources like namespaces, service accounts, roles, and the DaemonSet itself.

```bash
kubectl apply -f postman-insights-agent-daemonset.yaml
```

--------------------------------

### Filter Array Values with $filter

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $filter() function returns elements from an array that satisfy a given condition. This example filters for payment amounts greater than 40.

```FQL
$filter(input.payments[].amount,fn($v,$i,$a) { $v > 40})
```

--------------------------------

### Define Environment Variables Directly in Kubernetes Deployment

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/daemonset

This YAML snippet demonstrates how to define environment variables directly within a Kubernetes container specification. It shows the addition of 'POSTMAN_INSIGHTS_PROJECT_ID' and 'POSTMAN_INSIGHTS_API_KEY' to the 'env' section of a container. These variables are crucial for onboarding your service to Postman Insights.

```yaml
spec:
  ...
  template:
    ...
    spec:
      containers:
        - name: my-container
          image: my-image
          env:
            - name: POSTMAN_INSIGHTS_PROJECT_ID
              value: "svc_xxxxxxxxxx"
            - name: POSTMAN_INSIGHTS_API_KEY
              value: "PMAK_xxxxxxxxxx"
  ...
...
```

--------------------------------

### Filter Path Exclusions | Postman CLI

Source: https://learning.postman.com/docs/insights/reference/agent/apidump

This example shows how to exclude specific file types (PNG and JPG) from being captured during network traffic monitoring using the apidump command's path-exclusions flag.

```bash
postman-insights-agent apidump ... --path-exclusions '.*\.png' --path-exclusions '.*\.jpg' ...
```

--------------------------------

### Create a Mock Server using Postman API

Source: https://learning.postman.com/docs/design-apis/mock-apis/tutorials/mock-with-api

This endpoint allows you to create a mock server by providing a collection and an optional environment ID. You can specify if the mock server should be private or public.

```APIDOC
## POST /mocks

### Description
Creates a mock server based on a Postman collection and environment.

### Method
POST

### Endpoint
`https://api.getpostman.com/mocks`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **mock** (object) - Required - Contains details for the mock server.
  - **name** (string) - Required - The name of the mock server.
  - **collection** (string) - Required - The ID of the collection to mock.
  - **environment** (string) - Optional - The ID of the environment to associate with the mock server.
  - **private** (boolean) - Optional - Set to `true` to create a private mock server. Defaults to `false` (public).

### Request Example
```json
{
    "mock": {
        "name": "testAPImock",
        "collection": "{{collectionId}}",
        "environment": "{{environmentId}}",
        "private": false
    }
}
```

### Response
#### Success Response (200)
- **mock** (object) - Details of the created mock server.
  - **id** (string) - The unique identifier for the mock server.
  - **name** (string) - The name of the mock server.
  - **mockUrl** (string) - The URL of the mock server.
  - **collection** (object) - Information about the associated collection.
  - **environment** (object) - Information about the associated environment.

#### Response Example
```json
{
    "mock": {
        "id": "your-mock-id",
        "name": "testAPImock",
        "mockUrl": "https://your-mock-server-url.com",
        "collection": {
            "id": "your-collection-id",
            "name": "testAPI"
        },
        "environment": {
            "id": "your-environment-id",
            "name": "testAPI"
        }
    }
}
```
```

--------------------------------

### Parse HTML Response Body using Cheerio

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Parses an HTML response body using the Cheerio library, allowing for DOM manipulation and querying similar to jQuery. This is helpful for testing web scraping or front-end related API responses.

```javascript
const $ = require('cheerio').load(pm.response.text());
//output the html for testing
console.log($.html());
```

--------------------------------

### Conditional Logic with $boolean Ternary Operator

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

This example demonstrates conditional logic using the $boolean value and a ternary operator. It evaluates a condition and returns one of two specified outputs based on whether the condition is true or false.

```FQL
$boolean(customer_info.total_value > 250) ? "high-value customer" : "not a high-value customer"
```

--------------------------------

### Prepare Local Collections and Environments for Postman Workspace

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Validates and prepares local Postman collections and environments for synchronization with a Postman workspace. It checks for valid IDs and regenerates them if necessary. Requires a `.postman/config.json` file for configuration.

```bash
postman workspace prepare
```

--------------------------------

### Parse CSV Response Body using csv-parse

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Parses a CSV response body into a JavaScript array using the 'csv-parse/lib/sync' utility. This is useful for testing data returned in CSV format.

```javascript
const parse = require('csv-parse/lib/sync');
const responseJson = parse(pm.response.text());
```

--------------------------------

### Get List of Supported Languages for Code Generation

Source: https://learning.postman.com/docs/developer/code-generators

This snippet utilizes the `codegen.getLanguageList` method to retrieve an array of all supported programming languages for client code generation. The resulting list of supported code generators is then logged to the console.

```javascript
var codegen = require('postman-code-generators'),
  supportedCodegens = codegen.getLanguageList();
  console.log(supportedCodegens);

```

--------------------------------

### Add Description to API Operations

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Provides detailed context about an API operation's purpose and behavior. This snippet demonstrates adding a 'description' field to a GET operation in an OpenAPI (Swagger) definition.

```yaml
Copyswagger: '2.0'
# ...
paths:
  /resources:
    get:
      description: A GET operation description

```

--------------------------------

### Send Request with Tests in Postman Script

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-send-request

Illustrates sending a GET request using `pm.sendRequest` and immediately defining tests to validate the response. It checks for the absence of errors and verifies the status code and status text, facilitating automated validation of responses.

```javascript
pm.sendRequest('https://postman-echo.com/get', (error, response) => {
  if (error) {
    console.log(error);
  }

  pm.test('response should be okay to process', () => {
    pm.expect(error).to.equal(null);
    pm.expect(response).to.have.property('code', 200);
    pm.expect(response).to.have.property('status', 'OK');
  });
});
```

--------------------------------

### Test Request-Response Message Correlation

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Ensures that every request message has a corresponding response message, identified by a common ID. This is crucial for verifying the completeness of message exchanges.

```javascript
pm.test('Every request message should have a corresponding response message', () => {
  pm.request.messages.each((reqMsg) => {
    pm.response.messages.to.include({ id: reqMsg.data.id });
  });
});
```

--------------------------------

### Build Docker Image for Postman Runner

Source: https://learning.postman.com/docs/monitoring-your-api/runners/set-up-a-runner-in-your-network

Builds a Docker image from the specified Dockerfile and tags it as 'postman-runner'. This image can then be used to run Postman runners in containerized environments.

```bash
docker build -t postman-runner .

```

--------------------------------

### Define Security Scheme in OpenAPI Components

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This snippet demonstrates defining reusable security schemes within the 'securityDefinitions' (OpenAPI 2.0) or 'components/securitySchemes' (OpenAPI 3.0) section. It resolves issues where security definitions are not declared, making them unavailable for use in the API's security fields. The example defines a 'basicAuth' scheme.

```yaml
Copyswagger: '2.0'
#...
securityDefinitions:
  basicAuth:
    type: basic

```

--------------------------------

### Test API Response Time with Postman

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

This script asserts that the API response time is below a specified threshold (e.g., 200ms or 300ms). It demonstrates using both `pm.expect().to.be.below()` and `pm.response.to.have.responseTime.not.above()` for validating performance. This is crucial for ensuring API responsiveness.

```JavaScript
pm.test("Response time is less than 200ms", () => {
  pm.expect(pm.response.responseTime).to.be.below(200);

  // or
  pm.response.to.have.responseTime.not.above(200);

  // Using pm.expect
  pm.expect(pm.response.responseTime).to.be.below(300);
});
```

--------------------------------

### Remove Postman Enterprise App (Linux)

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

This command removes the Postman Enterprise application from your Linux system using the snap package manager. Ensure no critical data is lost before execution.

```bash
sudo snap remove postman-enterprise

```

--------------------------------

### Project structure with collection and environment

Source: https://learning.postman.com/docs/collections/using-newman-cli/integration-with-travis

This illustrates the project structure when both a Postman collection and its associated environment are exported as JSON files and placed in the 'tests' folder.

```tree
. 
├── .travis.yml
└── tests
    └── hello_world.postman_collection.json

```

--------------------------------

### Define ConfigMap for Specific Environment Variables

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/daemonset

This snippet defines a Kubernetes ConfigMap containing only the `POSTMAN_INSIGHTS_PROJECT_ID`. This is part of a strategy to separate sensitive and non-sensitive configuration data, where project IDs might be stored in ConfigMaps while API keys are in Secrets.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: deployment-service-config
data:
  POSTMAN_INSIGHTS_PROJECT_ID: "svc_xxxxxxxxxx"

```

--------------------------------

### Runner Authorization Service API Response Format

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

Specifies the JSON response format that the runner authorization service must return to indicate whether a request is allowed or blocked. A 'true' value for 'allowed' permits the request.

```json
{
  "allowed": true
}
```

--------------------------------

### Get Substring After Separator

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $substringAfter helper function returns the part of a string that comes after the first occurrence of a specified separator. It takes the string and the separator as arguments. If the separator is not found, the original string is returned.

```postman-helper
$substringAfter("abc@gmail.com", "@") -> "gmail.com"
```

--------------------------------

### Test Keep-Alive Message Frequency

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Verifies that 'keep-alive' messages are received at a regular interval, within a specified time range. This is useful for monitoring services that send periodic status updates.

```javascript
pm.test('Should receive keep-alive message roughly every 5 seconds', () => {
  const keepAliveMessage = pm.response.messages.filter({
    data: {
      type: 'keep-alive'
    }
  });

  for (let i = 1; i < keepAliveMessage.length; i++) {
    const time1 = keepAliveMessage[i-1].timestamp;
    const time2 = keepAliveMessage[i].timestamp;

    pm.expect(time2-time1).to.be.within(4800, 5200);
  }
});
```

--------------------------------

### Configure RelayState in AD FS web.config

Source: https://learning.postman.com/docs/administration/sso/microsoft-adfs

This snippet shows how to enable the RelayState parameter in the web.config file for Microsoft AD FS 2.0 or 3.0. This is a crucial step for IdP-initiated sign-on.

```xml
<microsoft.identityServer.web>
    ...
    <useRelayStateForIdpInitiatedSignOn enabled="true" />
</microsoft.identityServer.web>
```

--------------------------------

### Postman SOAP Request Header Configuration

Source: https://learning.postman.com/docs/sending-requests/soap/making-soap-requests

This example shows how to configure the necessary headers for a SOAP request in Postman. It highlights overriding the default Content-Type to 'text/xml' and setting the SOAPAction header, which are crucial for many SOAP services.

```postman
{
  "name": "SOAP ISBN Validation Request",
  "request": {
    "method": "POST",
    "header": [
      {
        "key": "Content-Type",
        "value": "text/xml"
      },
      {
        "key": "SOAPAction",
        "value": "#POST"
      }
    ],
    "body": {
      "mode": "raw",
      "raw": "<?xml version=\"1.0\" encoding=\"utf-8\"?>\n<soap:Envelope xmlns:soap=\"http://schemas.xmlsoap.org/soap/envelope/\">
    <soap:Body>
        <IsValidISBN10 xmlns=\"http://webservices.daehosting.com/ISBN\">
            <sISBN>0-19-852663-6</sISBN>
        </IsValidISBN10>
    </soap:Body>
</soap:Envelope>"
    },
    "url": "http://webservices.daehosting.com/services/isbnservice.wso"
  }
}

```

--------------------------------

### Assert Value Against a Set of Options

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Validates if a value from the JSON response is present within a predefined list of acceptable options. Useful for checking enumerated types or status indicators. Requires a JSON response and a list of expected values.

```javascript
/* Response has the following structure:
{
  "type": "Subscriber"
},
*/

pm.test("Value is in valid list", () => {
  pm.expect(pm.response.json().type)
    .to.be.oneOf(["Subscriber", "Customer", "User"]);
});
```

--------------------------------

### Run File Upload Collection with Newman CLI

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-file-uploads

This command demonstrates how to execute a Postman collection file named `file-upload.postman_collection.json` using the Newman CLI. Ensure the collection file and any referenced data files are in the same directory.

```bash
newman run file-upload.postman_collection.json

```

--------------------------------

### OpenAPI: Secure API Server URL with HTTPS for OpenID Connect

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This example shows how to configure an OpenAPI specification to use HTTPS for the API server URL when using OpenID Connect for authentication. This is crucial for protecting credentials transmitted over the network.

```yaml
components:
 securitySchemes:
  OpenIdScheme:
   type: openIdConnect
   openIdConnectUrl: https://example.com/connect
paths:
 '/pets':
  post:
   operationId: addPet
   servers:
   - url: https://example.com/
     description: API server
   security:
   - OpenIdScheme: []

```

--------------------------------

### CSV Data File Example for Newman Iterations

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

This CSV structure defines data to be used across multiple iterations of a Newman collection run. The first row contains headers (variable names), and subsequent rows provide the values for each iteration, similar to the JSON data file format.

```csv
url, user_id, id, token_id
http://127.0.0.1:5000, 1, 1, 123123123
http://postman-echo.com, 2, 2, 899899
```

--------------------------------

### Get Response Data in Postman Visualizer Template (JavaScript)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-visualizer

The `pm.getData` method allows you to retrieve data that was passed to the visualizer template. It accepts a callback function that receives an `error` object and the `data` object.

```javascript
pm.getData(callback):Function
```

```javascript
pm.getData(function (error, data) {
  var value = data.res.info;
});
```

--------------------------------

### Exporting Custom Functions for Spectral Rules (JavaScript)

Source: https://learning.postman.com/docs/api-governance/configurable-rules/spectral

Shows how to export a custom function, named 'myCustomFunction', which can be used in Postman custom rules. It provides examples for both ES6 and CommonJS module formats.

```javascript
function myCustomFunction(targetVal, options, context) { ... }

// ES6 syntax
export default myCustomFunction;
// CommonJS syntax
// module.exports = myCustomFunction;
```

--------------------------------

### Multiple Assertions in a Single Test

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Groups several related assertions within a single Postman test case. If any assertion within the group fails, the entire test fails, promoting organized and comprehensive testing.

```javascript
pm.test("The response has all properties", () => {
    //parse the response JSON and test three properties
    const responseJson = pm.response.json();
    pm.expect(responseJson.type).to.eql('vip');
    pm.expect(responseJson.name).to.be.a('string');
    pm.expect(responseJson.id).to.have.lengthOf(1);
});
```

--------------------------------

### Test if Response Body Contains String

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Checks if the raw response body text includes a specific substring. This is a basic assertion for verifying the presence of certain data points without parsing.

```javascript
pm.test("Body contains string",() => {
  pm.expect(pm.response.text()).to.include("customer_id");
});
```

--------------------------------

### Filter Array Objects with JavaScript .filter()

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

This example uses the JavaScript array.filter() method to select objects from a payments array where the description property matches a specified variable. This offers more complex filtering logic.

```JavaScript
list.payments.filter( (payment) => payment.description === payments );
```

--------------------------------

### Create Cookie Example in Postman Scripting

Source: https://learning.postman.com/docs/sending-requests/response-data/cookies

This snippet demonstrates how to create a cookie for a specific domain using Postman's scripting capabilities. It utilizes the `pm.cookies.jar()` method to add a cookie with a name, value, and expiration date. Domains must be added to the allowlist before cookies can be managed for them.

```javascript
pm.cookies.jar("example.com").set("myCookie", "cookieValue", {
    expires: "Wed, 09 Oct 2024 21:49:26 GMT"
});
```

--------------------------------

### FQL: Get substring before pattern

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Returns the part of a string that appears before the first occurrence of a specified pattern. If the pattern is not found, the entire string is returned. This is helpful for splitting strings at a specific delimiter.

```FQL
$substringBefore(payments[0].description, "subscription")   
```

--------------------------------

### Postman Runner with Custom CA Certificates

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

Specify custom CA certificates for enhanced security when using an external proxy or built-in proxy with an authorization service. This is done by providing the path to a PEM-formatted file containing the certificates. This option is compatible with both `--proxy` and `--egress-proxy` configurations.

```bash
postman runner start --ssl-extra-ca-certs <path-to-pem-file> --proxy <proxy-url> --id <runner-id> --key <runner-key>
```

--------------------------------

### Access Variables in Postman Scripts (JavaScript)

Source: https://learning.postman.com/docs/sending-requests/variables/variables

Provides examples of how to retrieve variable values within Postman scripts using different scope-specific methods. It includes accessing variables from any scope, global, collection, environment, and vault secrets. The `pm.variables.get()` method is highlighted for its ability to retrieve the variable with the highest precedence.

```javascript
Copy//access a variable at any scope including local
pm.variables.get("variable_key");
//access a global variable
pm.globals.get("variable_key");
//access a collection variable
pm.collectionVariables.get("variable_key");
//access an environment variable
pm.environment.get("variable_key");
//access a vault secret
await pm.vault.get("secret_key")
```

--------------------------------

### Configure Newman SSL Options

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

Options for handling SSL client certificates, including specifying certificate files, private keys, passphrases, and a list of certificates for different hosts. Also includes option for extra CA certificates.

```bash
newman run my-collection.json --ssl-client-cert ./client.crt

```

```bash
newman run my-collection.json --ssl-client-key ./client.key

```

```bash
newman run my-collection.json --ssl-client-passphrase "mypass"

```

```bash
newman run my-collection.json --ssl-client-cert-list ./cert-list.json

```

```bash
newman run my-collection.json --ssl-extra-ca-certs ./ca-certs.pem

```

--------------------------------

### Spectral Function Return Statement with Message and Path

Source: https://learning.postman.com/docs/api-governance/configurable-rules/spectral

Demonstrates how to construct a return statement for Spectral custom functions, including the required 'message' property and an optional 'path' property for specifying the location of a rule violation. The example shows how to use the 'context.path' to build custom paths.

```javascript
return [
  // Rule violation with the default targetVal path
  {
    message: `Value must be different from "${values.join(',')}".`,
  },
  // Rule violation with a custom path leveraging the default targetVal path
  {
    message: `Value must be different from "${values.join(',')}".`,
    path: [...context.path, "a", "custom", "path"]
  },
];
```

--------------------------------

### Create Vault Policy for Postman Role (Vault CLI)

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command creates a HashiCorp Vault policy granting `read` capabilities to all secrets engines for users authenticated with the `postman` role. It denies access to `sys/*` and `auth/*` paths. You can customize the policy to restrict access to specific secrets engines.

```shell
vault write sys/policy/<policy-name> policy='path "*" { capabilities=["read"] } path "sys/*" { capabilities=["deny"] } path "auth/*" { capabilities=["deny"] }'
```

--------------------------------

### Assert Object Properties in Response

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Checks for the presence of specific keys or properties within an object in the JSON response. Supports checking for all keys, any keys, or a single property. Applicable to JSON responses containing objects.

```javascript
/* Response has the following structure:
{
  "a": 1,
  "b": 2
},
*/
pm.expect({a: 1, b: 2}).to.have.all.keys('a', 'b');
pm.expect({a: 1, b: 2}).to.have.any.keys('a', 'b');
pm.expect({a: 1, b: 2}).to.not.have.any.keys('c', 'd');
pm.expect({a: 1}).to.have.property('a');
pm.expect({a: 1, b: 2}).to.be.a('object')
  .that.has.all.keys('a', 'b');
```

--------------------------------

### Forks API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Use the Forks endpoints to manage forks of Postman collections and environments. Find all forks for a specific collection or environment, get the current status of a forked collection’s source collection, create or merge forks, and pull source changes.

```APIDOC
## Forks API

### Description
Manages forks of Postman collections and environments. Supports finding forks, checking status, creating, merging, and pulling source changes.

### Method
GET, POST, PUT, DELETE

### Endpoint
/forks

### Parameters
None specified in the provided text.

### Request Example
Not specified in the provided text.

### Response
#### Success Response (200)
Details about fork operations.

#### Response Example
Not specified in the provided text.
```

--------------------------------

### POST /resources

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Creates a new resource by accepting resource details in the request body and returns the created resource upon successful creation.

```APIDOC
## POST /resources

### Description
Creates a new resource.

### Method
POST

### Endpoint
/resources

### Parameters
#### Request Body
- **a resource to create** (object, $ref: '#/definitions/ResourceCreate') - Required - Details of the resource to create.

### Response
#### Success Response (201)
- **a post success response** (object, $ref: '#/definitions/Resource') - Description of the created resource.

### Response Example
{
  "example": "{\"id\": \"resource_id\", \"name\": \"example resource\"}"
}
```

--------------------------------

### Secure OAuth2 Refresh URL

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This example configures the refresh URL for OAuth 2.0 to use HTTPS. This ensures that refresh tokens, used to obtain new access tokens, are transmitted securely, protecting long-term access.

```yaml
components:
  securitySchemes:
    OauthFlow:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: https://my.auth.example.com/
          tokenUrl: https://my.token.example.com/
          refreshUrl: https://my.refresh.example.com/
          scopes:
            write: modify data
            read: read data
```

--------------------------------

### Test Response Message Subset

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Checks if the response messages include an object with specific properties, acting as a subset of the received message data. This is helpful for verifying key fields without needing to match the entire message.

```javascript
pm.test('User details are updated successfully', () => {
  pm.response.messages.to.include({
    action: 'update-user-details',
    status: 'success'
  });
});
```

--------------------------------

### Apply $uppercase to Object Values with $each() in FQL

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $each() function in Postman's FQL iterates over the string values of an object and applies a specified function to each. This example uses $uppercase to convert all string values to uppercase. It takes an object as input and returns an array of the transformed values. No external dependencies are required beyond Postman's FQL.

```FQL
$each({"transaction_id": "inv_80394", "description": "buying 20 units of data"},$uppercase)
```

--------------------------------

### Get Run Button Index from DOM

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Retrieves the index of a specific 'Run in Postman' button element within the page's DOM. This is necessary when 'segregateEnvironments' is enabled to associate actions with the correct button.

```javascript
var runButtons = Array.prototype.slice.call(document.getElementsByClassName('postman-run-button')),
  runButtonIndex = runButtons.indexOf(elem);
```

--------------------------------

### Test Response Status Codes

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Asserts the HTTP status code of the response. Supports checking for a specific code, a list of acceptable codes using 'oneOf', or a status code name string. Requires a valid HTTP response.

```javascript
pm.test("Status code is 201", () => {
  pm.response.to.have.status(201);
});
```

```javascript
pm.test("Successful POST request", () => {
  pm.expect(pm.response.code).to.be.oneOf([201,202]);
});
```

```javascript
pm.test("Status code name has string", () => {
  pm.response.to.have.status("Created");
});
```

--------------------------------

### AD FS Configuration File Paths

Source: https://learning.postman.com/docs/administration/sso/microsoft-adfs

Specifies the configuration file paths for different versions of Microsoft AD FS. These files need to be edited to enable the RelayState parameter.

```text
%systemroot%\inetpub\adfs\ls\web.config
```

```text
%systemroot%\ADFS\Microsoft.IdentityServer.Servicehost.exe.config
```

--------------------------------

### Define Global Basic Authentication in OpenAPI

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This snippet shows how to define and apply basic authentication globally in an OpenAPI 2.0 specification. It resolves issues where the global security field is not defined, ensuring that API operations require authentication. The example defines a 'basicAuth' scheme and applies it.

```yaml
Copyswagger: '2.0'
#...
securityDefinitions:
  basicAuth:
    type: basic
security:
    - basicAuth: []

```

--------------------------------

### Calculate Years Since Milestone using Evaluate Block

Source: https://learning.postman.com/docs/postman-flows/tutorials/beginner/calculate-years-since-milestone

This snippet demonstrates calculating the difference in years between two dates using an Evaluate block. It subtracts the milestone date from the current date (in milliseconds) and divides by the milliseconds per year, then floors the result to get whole years.

```FQL
$floor(
	(now - date) /
	millisecondsPerYear
)
```

```TypeScript
Math.floor((now - date) / millisecondsPerYear)
```

--------------------------------

### Import and Use a Postman Package

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/package-library

Demonstrates how to import a Postman package into your scripts using `pm.require` and assign it to a variable. This allows you to call functions and access objects defined within the imported package. The variable identifier is typically derived from the package name.

```javascript
const variableName = pm.require('@team-domain/package-name');

variableName.functionName()
```

--------------------------------

### Run a Request from a Collection Script - JavaScript

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-execution

This example demonstrates how to use the `pm.execution.runRequest` method to send a request defined in a collection from within a script. It shows how to pass a request ID, override variables, and handle the asynchronous response using `await`. The response status and JSON body are logged, with error handling for failed requests. This method is limited to Postman's execution environment and not supported in Newman or the VS Code extension.

```javascript
try {
  const response = await pm.execution.runRequest(
    "12345678-12345ab-1234-1ab2-1ab2-ab1234112a12",
    {
      variables: {
        base_url: "https://example.com",
        vip: "123"
      }
    }
  );

  console.log("Response received from collection request with status:", response.code, response.json());
}
catch (error) {
  console.error("Failed to send a request from the collection", error);
}

```

--------------------------------

### Comprehensive Response Validation with Postman Tests

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-scripts

This example illustrates multiple assertions within a single Postman test to validate a response. It checks that the response is not an error, has a JSON body, and specifically does not contain an 'error' key within its JSON body. This provides a robust way to ensure the response is in a processable state.

```javascript
pm.test("response should be okay to process", function () {
    pm.response.to.not.be.error;
    pm.response.to.have.jsonBody("");
    pm.response.to.not.have.jsonBody("error");
});
```

--------------------------------

### Using External Libraries in Postman Packages

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/package-library

Illustrates the usage of external library modules within Postman packages. The `require` method is used to incorporate supported libraries such as `cheerio` and `xml2js` into your package code.

```javascript
const cheerio = require('cheerio');
const xml2js = require('xml2js');
```

--------------------------------

### Execute Postman Collection with Newman in Jenkins

Source: https://learning.postman.com/docs/collections/using-newman-cli/integration-with-jenkins

This shell command is used within a Jenkins 'Execute shell' build step to run a Postman collection. It requires Newman to be installed in Jenkins and the collection file to be accessible. The command takes the path to the exported Postman collection JSON file as an argument.

```shell
newman run ~/Desktop/jenkins_demo_postman_collection.json

```

--------------------------------

### Remove Trailing Slashes from API Paths

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures consistent path handling by removing trailing slashes. This example shows a valid path definition without a trailing slash in an OpenAPI (Swagger) specification.

```yaml
Copyswagger: '2.0'
# ...
paths:
  '/resources':


```

--------------------------------

### Checking for API Description Presence with JSON Path Plus

Source: https://learning.postman.com/docs/api-governance/configurable-rules/spectral

Demonstrates two approaches for verifying the presence of an API description. The first approach is incorrect as it fails when the path does not exist. The second, correct approach, targets the parent object and specifies the desired field.

```yaml
# this approach won't work

rules:
  info-description:
    given: $.info.description
    then:
      function: truthy

```

```yaml
# this approach will work

rules:
  info-description:
    given: $.info
    then:
      field: description
      function: truthy

```

--------------------------------

### Postman Runner with External Proxy

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

Configure the Postman runner to route traffic through an external proxy server by specifying its URL. This allows for inspection and policy enforcement of outbound requests. Alternatively, the proxy URL can be set using HTTP_PROXY and HTTPS_PROXY environment variables.

```bash
postman runner start --proxy <proxy-url> --id <runner-id> --key <runner-key>
```

--------------------------------

### Filtering Data with TypeScript in Postman Flows

Source: https://learning.postman.com/docs/postman-flows/build-flows/structure/loops/overview

Shows how to filter a list of JSON objects using the TypeScript `filter()` method within a Postman Flows 'Evaluate' block. This example filters wells based on their elevation range.

```TypeScript
CopytableOfWells.filter(
(row) => row.Elevation >= 700 && row.Elevation <= 960);
```

--------------------------------

### Run a Newman Collection

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

This is the basic command to run a Newman collection from a specified file or URL. Additional options can be appended to customize the run.

```bash
newman run my-collection.json [options]

```

--------------------------------

### Postman Request Header Object Example

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Shows the structure of an individual request header object within a Postman collection. It includes the header key, value, a boolean to disable it, and an optional description. This allows for fine-grained control over request headers.

```json
{
  "key": "Content-Type",
  "value": "application/json",
  "disable": false,
  "description": "Your headers descriptions"
}
```

--------------------------------

### Postman Valid Spectral Document Structure

Source: https://learning.postman.com/docs/api-governance/configurable-rules/spectral

This example shows the required properties for a Spectral document to be valid within Postman. It includes rule description, severity, supported formats, the 'given' property for targeting, and the 'then' property with a specific function and options.

```yaml
rules:
  api-name-doesnt-contain-api:
    description: The API name must not contain the word API
    message: The info.title value "{{value}}" contains the forbidden word API
    severity: error
    formats:
      - oas2
      - oas3
    given:
      - $.info
    then:
      - field: title
        function: pattern
        functionOptions:
          notMatch: /\b(api)\b/i
```

--------------------------------

### Test Response Body Values

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Validates specific key-value pairs within the JSON response body. Assumes the response body is a valid JSON object. No external dependencies are required beyond the Postman testing environment.

```javascript
/* Response has the following structure:
{
  "name": "Jane",
  "age": 23
},
*/
pm.test("Person is Jane", () => {
  const responseJson = pm.response.json();
  pm.expect(responseJson.name).to.eql("Jane");
  pm.expect(responseJson.age).to.eql(23);
});
```

--------------------------------

### Assert Array Properties in Response

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Validates properties of arrays within the JSON response, such as checking if an array is empty, if it includes specific items, or if it contains a set of members. Requires a JSON response containing arrays.

```javascript
/* Response has the following structure:
{
  "errors": [],
  "areas": [ "goods", "services" ],
  "settings": [
    {
      "type": "notification",
      "detail": [ "email", "sms" ]
    },
    {
      "type": "visual",
      "detail": [ "light", "large" ]
    }
  ],
},
*/

const jsonData = pm.response.json();
pm.test("Test array properties", () => {
    //errors array is empty
  pm.expect(jsonData.errors).to.be.empty;
    //areas array includes "goods"
  pm.expect(jsonData.areas).to.include("goods");
    //get the notification settings object
  const notificationSettings = jsonData.settings.find
      (m => m.type === "notification");
  pm.expect(notificationSettings)
    .to.be.an("object", "Could not find the setting");
    //detail array must include "sms"
  pm.expect(notificationSettings.detail).to.include("sms");
    //detail array must include all listed
  pm.expect(notificationSettings.detail)
    .to.have.members(["email", "sms"]);
});
```

--------------------------------

### pm.cookies Methods (Current Domain)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-cookies

Use `pm.cookies` methods to interact with cookies associated with the current request's domain. This includes checking for a cookie's existence, retrieving its value, and getting all cookies as an object.

```APIDOC
## pm.cookies Methods

Use the `pm.cookies` methods in your scripts to access and manipulate cookies for the requested domain.

### `pm.cookies.has(cookieName:String)`

Checks if there is a cookie with the specified name for the requested domain.

**Returns:**
* `true` - The cookie exists for the requested domain.
* `false` - The cookie doesn’t exist for the requested domain.

### `pm.cookies.get(cookieName:String)`

Gets the value of the specified cookie for the requested domain.

**Returns:**
* The value of the cookie. (Can be appended with a string using the `+` operator).

### `pm.cookies.toObject()`

Gets all cookies and their values for the requested domain.

**Returns:**
* All cookies and their values as an object.
```

--------------------------------

### POST /resources

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Creates a new resource. Requires a request body.

```APIDOC
## POST /resources

### Description
A POST operation for creating resources. Requires a request body.

### Method
POST

### Endpoint
/resources

#### Request Body
- **aProperty** (any) - Required - Example property for the request body.

### Request Example
```json
{
  "aProperty": "example value"
}
```

### Response
#### Success Response (200)
- **example** (object) - Example response structure

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Send Request with Plain URL String in Postman Script

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-send-request

Demonstrates sending an asynchronous GET request using a simple URL string with `pm.sendRequest`. It handles potential errors and logs the JSON response. This is useful for basic asynchronous data fetching.

```javascript
try {
    const response = await pm.sendRequest('https://postman-echo.com/get');

    console.log(response.json());
}
catch (error) {
    console.log(error)
}
```

--------------------------------

### POST /validate - Runner Authorization Service

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

This endpoint is called by the built-in proxy server to validate outbound requests from the runner. It accepts a JSON payload with request details and returns a JSON response indicating whether the request is allowed.

```APIDOC
## POST /validate

### Description
Validates outbound requests from the runner. The runner authorization service API exposes this endpoint to allow or block requests based on custom logic.

### Method
POST

### Endpoint
/validate

### Parameters
#### Request Body
- **url** (string) - Required - The destination URL for the request.
- **queryParams** (string) - Optional - Query parameters for the request.
- **body** (string) - Optional - The request body content as a string.
- **headers** (string) - Required - A JSON-encoded string representing the request headers.
- **method** (string) - Required - The HTTP method for the request (e.g., GET, POST, PUT, DELETE).

### Request Example
```json
{
  "url": "https://example.com/api/endpoint?param=value",
  "queryParams": "param1=value1&param2=value2",
  "body": "request body content as string",
  "headers": "{\"content-type\":\"application/json\",\"x-pstmn-outbound-identifier\":\"c9-post\"}",
  "method": "POST"
}
```

### Response
#### Success Response (200)
- **allowed** (boolean) - Required - Returns `true` to allow the request and `false` to block the request.

#### Response Example
```json
{
  "allowed": true
}
```

#### Error Response (400)
Returned if the request body is missing 'url' or 'method'.
```json
{
  "allowed": false
}
```

#### Error Response (403)
Returned if the `evaluateRequest` function returns false.
```json
{
  "allowed": false
}
```
```

--------------------------------

### Travis CI script to run collection with environment

Source: https://learning.postman.com/docs/collections/using-newman-cli/integration-with-travis

This `script` section for the `.travis.yml` file shows how to execute a Postman collection using Newman, including a specified Postman environment JSON file.

```yaml
script:
- node_modules/.bin/newman run tests/hello_world.postman_collection.json -e tests/tests.postman_environment.json

```

--------------------------------

### Dynamic Variables for Mock Server Responses

Source: https://learning.postman.com/docs/design-apis/mock-apis/create-dynamic-responses

This snippet demonstrates the use of dynamic variables within a Postman collection's example response body. These variables, such as $randomFullName and $timestamp, are resolved by the mock server and replaced with randomized data, useful for generating varied data for testing.

```json
{
    "name": "{{$randomFullName}}",
    "userName": "{{$randomUserName}}",
    "location": "{{$randomCity}}",
    "company": "{{$randomCompanyName}}",
    "jobTitle": "{{$randomJobTitle}}",
    "updatedAt": "{{$timestamp}}"
}
```

--------------------------------

### FQL: Extract substring

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Extracts a portion of a string based on a starting offset and a length. It can also handle negative offsets to count from the end of the string. This is useful for parsing or manipulating string data.

```FQL
$substring(payments[0].description, 3, 6)   
```

--------------------------------

### Configure Newman Environment and Globals

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

Options to specify environment and global variables for a Newman collection run. These can be local files or URLs. They help in parameterizing collection runs.

```bash
newman run my-collection.json -e environment.json

```

```bash
newman run my-collection.json -g globals.json

```

--------------------------------

### Postman Request with Multiple Headers

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Demonstrates how to include multiple headers in a Postman collection request. It defines a GET request to a sample URL and includes 'Content-Type', 'Authorization', and 'x-api-key' headers. This showcases the flexibility in setting various request headers.

```json
{
  "description": "Header example",
  "url": "https://postman-echo.com/get",
  "method": "GET",
  "header": [
    {
      "key": "Content-Type",
      "value": "application/json"
    },
    {
      "key": "Authorization",
      "value": "Bearer 12345"
    },
    {
      "key": "x-api-key",
      "value": "slknakliwpojpwsnj"
    }
  ]
}
```

--------------------------------

### Configure HTTP Request for Polling

Source: https://learning.postman.com/docs/postman-flows/build-flows/structure/loops/loops-polling

Sets up an HTTP GET request to poll the Postman Echo API for a random integer. This request will be used within a Postman Flow to generate values for the polling loop.

```json
{
  "info": {
    "_postman_id": "your_collection_id",
    "name": "Random Number Generator",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Random number generator",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "https://postman-echo.com/get?randomNumber={{$randomInt}}",
          "host": [
            "postman-echo",
            "com"
          ],
          "path": [
            "get"
          ],
          "query": [
            {
              "key": "randomNumber",
              "value": "{{$randomInt}}"
            }
          ]
        }
      },
      "response": []
    }
  ]
}
```

--------------------------------

### SCIM API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Supports System for Cross-domain Identity Management (SCIM) for automating team provisioning, allowing scalable deployment and access control via identity providers.

```APIDOC
## SCIM API

### Description
The SCIM API supports SCIM (System for Cross-domain Identity Management), which enables you to automate the provisioning of your team. You can deploy Postman at scale across your organization and control access to it with your identity provider. You can use these endpoints to integrate your onboarding process and automatically provision users and groups.

### Method
GET, POST, PUT, DELETE

### Endpoint
/scim
```

--------------------------------

### Assert Value Types in Response

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

Checks the data type of various properties within the JSON response body, including objects, strings, numbers, arrays, undefined, and null values. Assumes a JSON response structure.

```javascript
/* Response has the following structure:
{
  "name": "Jane",
  "age": 29,
  "hobbies": [
    "skating",
    "painting"
  ],
  "email": null
},
*/
const jsonData = pm.response.json();
pm.test("Test data type of the response", () => {
  pm.expect(jsonData).to.be.an("object");
  pm.expect(jsonData.name).to.be.a("string");
  pm.expect(jsonData.age).to.be.a("number");
  pm.expect(jsonData.hobbies).to.be.an("array");
  pm.expect(jsonData.website).to.be.undefined;
  pm.expect(jsonData.email).to.be.null;
});
```

--------------------------------

### Basic Auth

Source: https://learning.postman.com/docs/sending-requests/authorization/authorization-types

Basic authentication sends a username and password with your request. Postman Base64 encodes these credentials and adds them to the Authorization header.

```APIDOC
## Basic Auth

### Description
Authenticate requests by sending a verified username and password. Postman Base64 encodes these and adds them to the `Authorization` header.

### Method
N/A (Client-side configuration)

### Endpoint
N/A (Applies to individual requests, collections, or folders)

### Parameters
#### Request Body
- **Auth Type** (string) - Required - Must be 'Basic Auth'
- **Username** (string) - Required - Your API username.
- **Password** (string) - Required - Your API password.

### Request Example
```json
{
  "auth": {
    "type": "basic",
    "username": "your_username",
    "password": "your_password"
  }
}
```

### Response
#### Success Response (200)
Depends on the API being called.

#### Response Example
```json
{
  "message": "Success"
}
```

### Note
Postman appends `Basic <Base64 encoded username and password>` to the `Authorization` header.
```

--------------------------------

### Pre-generated Cookie String Format

Source: https://learning.postman.com/docs/sending-requests/response-data/cookies

This example shows a pre-generated cookie string format compliant with HTTP State Management standards, as produced by Postman's cookie manager when adding a new cookie. It includes the cookie name, value, path, and expiration date.

```http
CopyCookie_1=value; Path=/; Expires=Wed, 09 Oct 2024 21:49:26 GMT;
```

--------------------------------

### Inject Postman Insights Agent into Kubernetes Deployment

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/sidecar

This command injects the Postman Insights Agent as a sidecar into a specified Kubernetes deployment. It requires your Postman API key and project ID, and uses `kube inject` to modify the deployment YAML. The output is piped to `kubectl apply` to update the deployment.

```bash
kubectl get -n <namespace> deployment/<deployment> -o yaml \
| POSTMAN_API_KEY=<add-your-api-key-here> postman-insights-agent kube inject --project <projectId> --repro-mode -s=true -f - \
| kubectl apply -f -
```

--------------------------------

### Postman Runner with Built-in Proxy

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

Enable Postman's built-in proxy server, which routes traffic through a configured runner authorization service. This service validates outbound requests based on predefined rules. The authorization service URL can also be set via the POSTMAN_RUNNER_AUTHZ_URL environment variable.

```bash
postman runner start --egress-proxy --egress-proxy-authz-url <authorization-service-url> --id <runner-id> --key <runner-key>
```

--------------------------------

### Postman CLI: Push Workspace (No Prepare)

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Executes the 'postman workspace push' command, skipping the 'prepare' step. This can be used when the workspace is already in a consistent state.

```bash
postman workspace push --no-prepare
```

--------------------------------

### Delete Cookie Example in Postman Scripting

Source: https://learning.postman.com/docs/sending-requests/response-data/cookies

This snippet illustrates how to remove a specific cookie for a domain using Postman's scripting. The `pm.cookies.jar().remove()` method deletes the cookie by its name. This operation requires the domain to be allowlisted.

```javascript
pm.cookies.jar("example.com").remove("myCookie");
```

--------------------------------

### Runner Authorization Service API Request Payload Format

Source: https://learning.postman.com/docs/monitoring-your-api/runners/runners-proxy-server

Defines the JSON payload format expected by the runner authorization service for validating outbound requests. It includes fields for URL, query parameters, request body, headers, and HTTP method.

```json
{
  "url": "https://example.com/api/endpoint?param=value",
  "queryParams": "param1=value1&param2=value2",
  "body": "request body content as string",
  "headers": "{\"content-type\":\"application/json\",\"x-pstmn-outbound-identifier\":\"c9-post\"}",
  "method": "POST"
}
```

--------------------------------

### Setting Postman Variables in Scripts

Source: https://learning.postman.com/docs/sending-requests/variables

Demonstrates how to set global, collection, environment, local, and vault variables using Postman's scripting capabilities. It also shows how to unset variables. Note that vault secrets require the 'await' operator.

```javascript
pm.globals.set("variable_key", "variable_value");
pm.collectionVariables.set("variable_key", "variable_value");
pm.environment.set("variable_key", "variable_value");
pm.variables.set("variable_key", "variable_value");
await pm.vault.set("secret_key", "secret_value");
pm.environment.unset("variable_key");
```

--------------------------------

### FQL: Get string length

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Returns the length of a specified string. This function is useful for validating input or processing text data where character count is important. It takes a string as input and returns its length as a number.

```FQL
$length(payments[0].description)   
```

--------------------------------

### Get All Cookies for a Specific Domain (Postman)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-cookies

Fetch all cookies associated with a particular domain using `pm.cookies.jar().getAll()`. The results, including cookie names and values, are provided through a callback function due to the asynchronous nature of the operation.

```javascript
pm.cookies.jar().getAll("example.com", (error, cookies) => {
    if (error) {
        console.error(`An error occurred: ${error}`);
    } else {
        console.log(`All cookies: ${JSON.stringify(cookies)}`);
    }
});
```

--------------------------------

### Generate JUnit XML Report with Newman CLI

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-built-in-reporters

This command uses Newman to run a Postman collection and generate a JUnit-compatible XML report. The `--reporter-junit-export` option specifies the directory for the output file. If the directory does not exist, it will be created. The reporter will create `collection-run.xml` by default, but a custom filename can also be provided.

```bash
newman run my-collection.json -r cli,junit --reporter-junit-export xml-file-reports
```

--------------------------------

### Postman Collection: Basic API Structure (JSON)

Source: https://learning.postman.com/collection-format/getting-started/defining-a-simple-api

Defines the most basic structure of a Postman API collection, requiring 'info' for metadata and 'item' for a single request. The request defaults to a GET method when only a URL is provided.

```json
{
  "info": {
    "name": "My first collection",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/"
  },
  "item": {
    "name": "This is a request",
    "request": "http://myapi.com/api"
  }
}
```

--------------------------------

### Postman: Environment Variable Management with pm.environment

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-variables

Facilitates the management of variables within the currently active Postman environment. It offers methods to check for variable existence (`has`), retrieve values (`get`), set new values (`set`), and access dynamic variables (`replaceIn`). Editor permissions are required to alter environment variables.

```javascript
// Example usage of pm.environment

// Check if an environment variable exists
if (pm.environment.has('myEnvironmentVar')) {
  console.log('myEnvironmentVar exists');
}

// Get the value of an environment variable
let environmentValue = pm.environment.get('myEnvironmentVar');
console.log('Value of myEnvironmentVar:', environmentValue);

// Set an environment variable
pm.environment.set('newEnvironmentVar', 'Hello Environment!');

// Get a dynamic variable within the environment scope
// let dynamicEnvironmentValue = pm.environment.replaceIn('{{$timestamp}}');
// console.log('Dynamic environment value:', dynamicEnvironmentValue);

// Note: pm.environment also has 'unset' and 'clear' methods, similar to globals and collection variables.
// pm.environment.unset('oldEnvironmentVar');
// pm.environment.clear();

```

--------------------------------

### Generate CLI and JSON Reports with Newman

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-built-in-reporters

This command demonstrates how to run a collection using Newman and generate reports in both the Command Line Interface (CLI) and JSON formats. The `-r` flag specifies the desired reporters.

```bash
newman run my-collection.json -r cli,json

```

--------------------------------

### Test API Status Code with Postman

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

This script tests if the HTTP status code of an API response is 200. It utilizes the `pm.response.to.have.status()` method for direct assertion or `pm.expect(pm.response.code).to.eql()` for a more explicit check. This is fundamental for verifying successful API interactions.

```JavaScript
pm.test("Status code is 200", function () {
  pm.response.to.have.status(200);
});
```

```JavaScript
pm.test("Status code is 200", () => {
  pm.expect(pm.response.code).to.eql(200);
});
```

--------------------------------

### Run Postman Collection

Source: https://learning.postman.com/docs/collections/using-newman-cli/continuous-integration

This section details how to execute a Postman Collection using Newman and the Postman API. It includes the basic command and how to add environment variables.

```APIDOC
## Run Postman Collection using Newman and the Postman API

### Description
Use this command to run a Postman Collection directly from your CI environment using Newman. Replace `collection-id` with your actual collection ID and `postman-api-key` with your generated Postman API key.

### Method
GET (implicitly via Newman)

### Endpoint
`https://api.getpostman.com/collections/{collection-id}`

### Parameters
#### Query Parameters
- **apikey** (string) - Required - Your Postman API key.

### Request Example
```bash
newman run "https://api.getpostman.com/collections/collection-id?apikey=postman-api-key"
```

### Response
Newman will output the test results directly to your console.

## Run Postman Collection with Environment

### Description
This command allows you to run a Postman Collection along with a specified environment. This is useful when your collection tests rely on specific environment variables. Replace `collection-id`, `environment-id`, and `postman-api-key` with your respective IDs and key.

### Method
GET (implicitly via Newman)

### Endpoint
`https://api.getpostman.com/collections/{collection-id}` and `https://api.getpostman.com/environments/{environment-id}`

### Parameters
#### Query Parameters
- **apikey** (string) - Required - Your Postman API key.

#### Request Body
(Not applicable for this command)

### Request Example
```bash
newman run "https://api.getpostman.com/collections/collection-id?apikey=postman-api-key" --environment "https://api.getpostman.com/environments/environment-id?apikey=postman-api-key"
```

### Response
Newman will output the test results, including environment-specific data, to your console.
```

--------------------------------

### pm.expect syntax for assertions

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-test-expect

Explains the `pm.expect` method for writing assertions using ChaiJS BDD syntax. It takes a value to test and returns an Assertion object with chainable methods for various checks.

```javascript
pm.expect(value: *): Assertion
```

--------------------------------

### Document JavaScript functions in Postman pre-request scripts with JSDoc

Source: https://learning.postman.com/docs/writing-scripts/pre-request-scripts

This snippet demonstrates how to document a JavaScript function using JSDoc comments. The documentation explains the function's purpose and details its parameters, including their data types. This documentation is displayed in a popup when the function is called within Postman.

```javascript
/**
 * This function prints a string to the Postman Console.
 * @param {string} data - The text to print to the Postman Console.
 */
function logger (data) {
    console.log(`Logging information to the console, ${data}`)
}
```

--------------------------------

### Uninstall Postman Enterprise Windows App

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

The Postman Enterprise Windows app can be uninstalled using the `msiexec` command-line tool with the `/x` option, specifying the path to the MSI package. Alternatively, it can be removed via the 'Add/Remove Programs' feature in Windows settings.

```batch
msiexec /x path\to\package.msi
```

--------------------------------

### Import a Postman Package (No Variable Declaration)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/package-library

Shows how to import a Postman package when it only contains JavaScript code or `pm` object instances without callable functions or objects. In this case, explicit variable declaration is not necessary.

```javascript
pm.require('@team-domain/package-name');
```

--------------------------------

### Faker Dynamic Variables for Common Data

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/variables-list

This section lists common dynamic variables available through the Faker library in Postman. These variables generate unique identifiers and timestamps, such as GUIDs and UNIX timestamps. They are used directly in Postman requests or within scripts using `pm.variables.replaceIn()`.

```Postman Variables
$guid
$timestamp
$isoTimestamp
$randomUUID
```

--------------------------------

### Run Postman Collections with Reporting Options

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Execute Postman collections from the command line and generate local reports. Supports 'cli', 'json', 'junit', and 'html' report formats. Defaults to 'cli' if no reporter is specified. Refer to Postman documentation for detailed report generation.

```bash
postman collection run /myCollectionFolderName/myCollectionFile.json

postman collection run 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12
```

--------------------------------

### Disable Environment Variables for Postman (Windows)

Source: https://learning.postman.com/docs/getting-started/installation/proxy

This batch script clears common proxy environment variables (`http_proxy`, `https_proxy`, `HTTP_PROXY`, `HTTPS_PROXY`) before launching the Postman desktop application. This is useful when OS-level proxy environment variables interfere with Postman's proxy settings. Ensure the `C:\path\to\Postman.exe` is updated to your actual Postman installation path.

```batch
set HTTP_PROXY=''
set HTTPS_PROXY=''
set http_proxy=''
set https_proxy=''
start C:\path\to\Postman.exe

```

--------------------------------

### Reusable Schema with Description

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that all reusable schemas have descriptions to provide context and information to API consumers.

```APIDOC
## Components

### Schemas
- **aReusableSchema**:
  - description: A reusable schema description
  - type: object
  
### Example Usage
This schema can be referenced in request or response objects for consistency.
```

--------------------------------

### Configure Postman Enterprise Login Policy (Linux)

Source: https://learning.postman.com/docs/administration/enterprise/managing-enterprise-deployment

Sets the login policy for the Postman Enterprise app by specifying allowed team IDs. Users must sign in to one of the listed Postman teams to use the app. Replace '1234,4321' with your actual team IDs.

```bash
sudo snap set postman-enterprise TEAM_IDS="1234,4321"

```

--------------------------------

### Basic Postman Collection Item Structure

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Defines the simplest form of a Postman collection item, containing a name and a request URL. When only a URL is provided, the HTTP method defaults to GET. This serves as a foundational element for organizing API calls.

```json
{
  "item": {
    "name": "Simple API definition",
    "request": "https://postman-echo.com/get"
  }
}
```

--------------------------------

### Get Current Timestamp in ISO 8601 Format with FQL

Source: https://learning.postman.com/docs/postman-flows/build-flows/structure/date-and-time

This snippet demonstrates how to retrieve the current timestamp in ISO 8601 format using the `now` function in Postman Flows Query Language (FQL). This format is widely accepted by many APIs. It directly outputs the current date, time, and UTC offset.

```fql
$now()
```

--------------------------------

### Completion Command Reference

Source: https://learning.postman.com/docs/insights/reference/agent/completion

The `completion` command generates autocompletion scripts for the Postman Insights Agent for different shells (bash, fish, powershell, zsh).

```APIDOC
## POST /websites/learning_postman_com/completion

### Description
Generates the autocompletion script for The Postman Insights Agent in the specified shell.

### Method
POST

### Endpoint
/websites/learning_postman_com/completion

### Parameters
#### Query Parameters
- **command** (string) - Required - The shell for which to generate the autocompletion script (e.g., 'bash', 'fish', 'powershell', 'zsh').
- **--log-format** (string) - Optional - Set to 'color', 'plain' or 'json' to control the log format.
- **--project** (string) - Optional - Your Postman Insights project ID.
- **--proxy** (string) - Optional - The domain name, IP address, or URL of an HTTP proxy server to use.

### Request Example
```json
{
  "command": "bash"
}
```

### Response
#### Success Response (200)
- **script** (string) - The generated autocompletion script for the specified shell.
```

--------------------------------

### Filter Endpoints by IP Address using apidump CLI

Source: https://learning.postman.com/docs/insights/troubleshoot/traffic

This command-line example shows how to exclude API calls to specific IP addresses from the Postman Insights Agent's monitoring. The `--host-exclusions` flag accepts a Go regular expression to filter out traffic directed at IP addresses, useful for removing unnamed infrastructure services. The provided regex targets standard IPv4 dotted-quad notation.

```bash
apidump --project <projectID> –-host-exclusions ^(\d)+\.(\d)+\.(\d)+\.(\d)+$
```

--------------------------------

### Create ECS Task Definition with Postman Insights Agent CLI

Source: https://learning.postman.com/docs/insights/get-started/ecs

This command uses the Postman Insights Agent CLI to generate a task definition for ECS. It requires your Postman API key and project ID. The output can be directly used to update an ECS task definition JSON.

```bash
POSTMAN_API_KEY=PMAK_xxxxxxxx_xxxxxxxx postman-insights-agent ecs task-def --project svc_xxxxxxxxxx --repro-mode

```

--------------------------------

### Create Environment with User-Entered API Keys

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Creates a new Postman environment named 'API Keys' using API keys provided by the user through input fields. This function dynamically fetches values from HTML input elements.

```javascript
function () {
  var stagingKey = document.getElementById('staging-key-input').value,
    productionKey = document.getElementById('production-key-input').value,
    runButtonIndex = 0,
    envData = {
      stagingKey: stagingKey,
      productionKey: productionKey
    };

  _pm('env.create', 'API Keys', envData, runButtonIndex);
}
```

--------------------------------

### Generate CloudFormation Fragment for ECS Insights Agent

Source: https://learning.postman.com/docs/insights/get-started/ecs

This command generates a CloudFormation fragment required to include the Postman Insights Agent in an ECS task definition. It requires your Postman API key and Project ID. The output can be directly integrated into your CloudFormation template.

```bash
POSTMAN_API_KEY=<your-api-key> postman-insights-agent ecs cf-fragment --project <project-id> --repro-mode
```

--------------------------------

### Assert Object Containment in Postman Script

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-examples

This script checks if a specific object is included within the JSON response from an API call. It uses the `.deep.include` assertion for deep comparison of objects. Ensure the response body is valid JSON for this assertion to work correctly.

```javascript
/* Response has the following structure:
{
  "id": "d8893057-3e91-4cdd-a36f-a0af460b6373",
  "created": true,
  "errors": []
},
*/

pm.test("Object is contained", () => {
  const expectedObject = {
    "created": true,
    "errors": []
  };
  pm.expect(pm.response.json()).to.deep.include(expectedObject);
});
```

--------------------------------

### Number Formatting: Convert to Hex or Binary

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Shows how to use the formatBase() function to convert a number into its hexadecimal (base 16) or binary (base 2) representation.

```FQL
$formatBase(3000, 16)
```

--------------------------------

### Define Secret for API Key

Source: https://learning.postman.com/docs/insights/get-started/kubernetes/daemonset

This YAML defines a Kubernetes Secret of type `Opaque` to store sensitive data, specifically the `POSTMAN_INSIGHTS_API_KEY`. The API key should be base64 encoded before being placed in the `data` field. Secrets are designed for sensitive information like passwords, tokens, and keys.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: deployment-service-secret
type: Opaque
data:
  POSTMAN_INSIGHTS_API_KEY: "encoded API key"

```

--------------------------------

### Add Link using Markdown

Source: https://learning.postman.com/docs/publishing-your-api/authoring-your-documentation

This snippet demonstrates how to add a hyperlink to your Postman documentation using Markdown syntax. It requires a link text to display and the URL of the resource. This method is useful for directing users to external resources like repositories or websites.

```markdown
Copy[link text to display](https://your-link-url.com)

```

--------------------------------

### Get Request Path with pm.execution.location

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-execution

The `pm.execution.location` property returns an array representing the full path of a request, including its parent folder and collection. The `pm.execution.location.current` property specifically returns the name of the current item (request, folder, or collection) being executed. These properties are useful for context-aware scripting.

```javascript
console.log(pm.execution.location);

```

```javascript
console.log(pm.execution.location.current);

```

--------------------------------

### Restart IIS and AD FS Service

Source: https://learning.postman.com/docs/administration/sso/microsoft-adfs

Commands to restart IIS for AD FS 2.0 and the Active Directory Federation Services service for both AD FS 2.0 and 3.0. These commands are necessary after configuration changes.

```bash
IISReset
```

```bash
adfssrv
```

--------------------------------

### Push Local Changes to Postman Workspace

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Synchronizes local collections and environments with your Postman workspace in the cloud. This command performs create, update, and delete operations based on your local files. It can optionally skip the preparation step and confirmation prompts.

```bash
postman workspace push
```

```bash
postman workspace push --no-prepare
```

```bash
postman workspace push -y
```

--------------------------------

### Embed Video in Markdown - HTML

Source: https://learning.postman.com/docs/publishing-your-api/authoring-your-documentation

This code snippet demonstrates how to embed a video from YouTube into your Postman documentation using Markdown. It utilizes an HTML video tag with the video source URL and specifies the width and height for the preview. Ensure the video is hosted on YouTube or Vimeo for direct embedding.

```html
<video src="https://www.youtube.com/embed/FeqSWgx6FxY?si=-5pR5tgUQtPN8P6z" alt="View Public Workspace Metrics" width="340" height="170"></video>

```

--------------------------------

### Visualizer API - pm.visualizer.set()

Source: https://learning.postman.com/docs/sending-requests/response-data/visualizer

The pm.visualizer.set() method allows you to programmatically create and display visualizations within Postman based on request responses. It takes a Handlebars HTML template, optional data to bind to the template, and optional compilation options.

```APIDOC
## POST pm.visualizer.set()

### Description
Sets up a visualization using an HTML template and data. Postman renders this in the Visualizer tab.

### Method
`pm.visualizer.set(layout, data, options)`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **layout** (string) - Required - A Handlebars HTML template string that defines the structure, CSS, and JavaScript for the visualization.
- **data** (object) - Optional - An object containing data that can be accessed and bound within the Handlebars template.
- **options** (object) - Optional - An options object for `Handlebars.compile()`, used to control template compilation.

### Request Example
```javascript
pm.visualizer.set(
  "<h1>{{title}}</h1><p>{{content}}</p>",
  { title: "My Visualization", content: "This is some data." },
  { strict: true } 
);
```

### Response
#### Success Response (200)
This method does not return a direct response in the traditional sense. It modifies the Postman application's state to display the visualization in the **Visualization** tab.

#### Response Example
(No direct response body, visualization is rendered in the UI)

### Error Handling
- Errors during template compilation or data binding may be logged in the Postman console or the Visualizer Developer Tools.
```

--------------------------------

### Specify Allowed External Packages

Source: https://learning.postman.com/docs/administration/managing-your-team/manage-team-workspaces

Defines the syntax for allowing specific external packages from registries like npm and JSR. Supports exact versions, version ranges using glob patterns, and wildcards for scopes or entire registries. This feature is available on Postman Enterprise plans.

```plaintext
npm:ajv@8.12.0
```

```plaintext
npm:lodash@4.*
```

```plaintext
jsr:*@*
```

```plaintext
npm:@types/*@*
```

--------------------------------

### Pad String

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $pad helper function returns a copy of a string, padded to a specified length. Padding is added to the end of the string by default. An optional padding string can be provided; if not, spaces are used. If the original string is longer than the target length, it is returned unchanged.

```postman-helper
$pad("example", 5) -> "example  "
$pad("example", 5, "-") -> "example--"
```

--------------------------------

### Postman: Global Variable Management with pm.globals

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-variables

Provides methods to interact with global variables in Postman scripts. This includes checking for existence (`has`), retrieving values (`get`), setting new values (`set`), accessing dynamic variables (`replaceIn`), retrieving all globals (`toObject`), removing a specific global (`unset`), and clearing all globals (`clear`). Editor permissions are required to modify global variables.

```javascript
// Example usage of pm.globals

// Check if a global variable exists
if (pm.globals.has('myGlobalVar')) {
  console.log('myGlobalVar exists');
}

// Get the value of a global variable
let globalValue = pm.globals.get('myGlobalVar');
console.log('Value of myGlobalVar:', globalValue);

// Set a global variable
pm.globals.set('newGlobalVar', 'Hello Globals!');

// Get a dynamic variable
// let dynamicValue = pm.globals.replaceIn('{{$randomEmail}}');
// console.log('Dynamic value:', dynamicValue);

// Get all global variables as an object
// let allGlobals = pm.globals.toObject();
// console.log('All globals:', allGlobals);

// Unset a global variable
// pm.globals.unset('oldGlobalVar');

// Clear all global variables
// pm.globals.clear();

```

--------------------------------

### Run Postman Requests with Various Options

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Test and debug HTTP requests using the Postman CLI. Supports specifying request methods, URLs, authentication, request bodies, headers, environments, and form data. Options for debugging, output redirection, and redirect handling are available.

```bash
postman request GET https://api.example.com/users

postman request POST https://api.example.com/users \
    --body '{"name": "John", "email": "john@example.com"}'

postman request https://api.example.com/data \
    --auth-apikey-key "apikey" \
    --auth-apikey-value "abc123xyz" \
    --auth-apikey-in query
```

--------------------------------

### Setting Environment Variables in Postman Scripts

Source: https://learning.postman.com/docs/sending-requests/variables/variables

Shows how to set an environment variable for the currently active environment using `pm.environment.set()` within Postman scripts. Changes made without Editor access only affect the local value and are not synced.

```javascript
pm.environment.set("variable_key", "variable_value");
```

--------------------------------

### Postman: Collection Variable Management with pm.collectionVariables

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-variables

Enables interaction with variables scoped to the current Postman collection. Functions include checking existence (`has`), retrieving values (`get`), setting new values (`set`), accessing dynamic variables (`replaceIn`), obtaining all collection variables (`toObject`), removing a specific variable (`unset`), and clearing all collection variables (`clear`). Editor permissions are necessary for modification.

```javascript
// Example usage of pm.collectionVariables

// Check if a collection variable exists
if (pm.collectionVariables.has('myCollectionVar')) {
  console.log('myCollectionVar exists');
}

// Get the value of a collection variable
let collectionValue = pm.collectionVariables.get('myCollectionVar');
console.log('Value of myCollectionVar:', collectionValue);

// Set a collection variable
pm.collectionVariables.set('newCollectionVar', 'Hello Collection!');

// Get a dynamic variable within the collection scope
// let dynamicCollectionValue = pm.collectionVariables.replaceIn('{{$guid}}');
// console.log('Dynamic collection value:', dynamicCollectionValue);

// Get all collection variables as an object
// let allCollectionVars = pm.collectionVariables.toObject();
// console.log('All collection vars:', allCollectionVars);

// Unset a collection variable
// pm.collectionVariables.unset('obsoleteCollectionVar');

// Clear all collection variables
// pm.collectionVariables.clear();

```

--------------------------------

### Importing Packages with pm.require

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-require

This section details how to use the `pm.require` method to import packages from your team's Package Library or external package registries. It shows the syntax for importing and using functions or objects from these packages.

```APIDOC
## Importing Packages with pm.require

Use the `pm.require` method to import packages from your team's Package Library or external package registries within scripts in HTTP, gRPC, and GraphQL requests.

### Usage

Declare the `pm.require` method as a variable if you intend to call functions or objects from the package. If the package only contains code or instances of the `pm` object, variable declaration is not necessary.

#### Importing from Package Library

```markdown
const variableName = pm.require('@team-domain/package-name');

variableName.functionName()
```

#### Importing from External Registries

**npm:**

```markdown
// package imported from npm
const npmVariableName = pm.require('npm:package-name@version-number');

npmVariableName.functionName()
```

**jsr:**

```markdown
// package imported from jsr
const jsrVariableName = pm.require('jsr:package-name@version-number');

jsrVariableName.functionName()
```
```

--------------------------------

### URL-Scoped Variables in Postman Query Parameters

Source: https://learning.postman.com/collection-format/advanced-concepts/variables

This example demonstrates variables defined within a URL object in Postman, specifically for use in query parameters. The variables `username` and `email` are declared within the URL's `variable` array and are used in the `query` section. These variables are scoped to this particular URL definition.

```json
{
  "url": {
    "raw": "https://postman-echo.com:443/get/user?username={{username}}&email={{email}}",
    "protocol": "https",
    "host": [
      "postman-echo",
      "com"
    ],
    "port": "443",
    "path": [
      "get",
      "user"
    ],
    "query": [
      {
        "key": "username",
        "value": "{{username}}",
        "disabled": false,
        "description": "Username of this user"
      },
      {
        "key": "email",
        "value": "{{email}}",
        "disabled": false,
        "description": "Email of this user"
      }
    ],
    "variable": [
      {
        "id": "e5b2bde6-15e5-4081-92c9-4ae767433032",
        "key": "username",
        "value": "johndoe"
      },
      {
        "id": "e3t5b2bde6-15e5-4081-92c9-4ae7674332w23",
        "key": "email",
        "value": "john@doe.com"
      }
    ]
  }
}
```

--------------------------------

### Embed Image using Markdown

Source: https://learning.postman.com/docs/publishing-your-api/authoring-your-documentation

This snippet shows how to embed an image hosted online into your Postman documentation using Markdown. It requires alt text for the image and the URL where the image is hosted. This allows for visual content to be included directly in the documentation.

```markdown
Copy![image alt text](https://your-image-location.com)

```

--------------------------------

### Increment loop index with Evaluate block

Source: https://learning.postman.com/docs/postman-flows/tutorials/beginner/create-count-based-loop

This snippet demonstrates how to increment a loop's index in Postman Flows. It takes the current index value from the Repeat block, adds one, and outputs it. This is useful for starting loops with an index of one instead of zero.

```FQL
index + 1
```

--------------------------------

### Configure Insights Agent as Sidecar using `ecs add`

Source: https://learning.postman.com/docs/insights/get-started/ecs

This command configures the Postman Insights Agent as a sidecar container within an AWS ECS service. It requires your Postman API key, project ID, ECS cluster ARN, AWS profile name, AWS region, ECS service ARN, and task name. The `--repro-mode` flag enables the agent to send encrypted payload data for rerunning requests.

```bash
POSTMAN_API_KEY=<add-your-api-key-here> postman-insights-agent ecs add \
--project <projectId> \
--cluster <ECS_cluster_ARN> \
--profile <aws_profile_name> \
--region <aws_region> \
--service <ECS_service_ARN> \
--task <task-name> \
--repro-mode
```

--------------------------------

### Implement API Key Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet illustrates how to secure an API operation using an API key. It defines an API key security scheme that reads the key from the header and applies it to the '/pets' POST operation.

```yaml
paths:
  '/pets':
    post:
      servers:
      - url: https://example.com/
        description: Example server
components:
  securitySchemes:
    AuthKeyAuth:
      type: apiKey
      name: api-key
      in: header
security:
  - AuthKeyAuth: []
```

--------------------------------

### Description Object

Source: https://learning.postman.com/collection-format/advanced-concepts/documentation

Details on how to use the description object within Postman collections to provide rich textual or HTML descriptions for various collection elements.

```APIDOC
## Description Object

### Description
The description object is a flexible way to provide descriptions for collection units. It supports plain text, Markdown, HTML, and other MIME types.

### Structure
Descriptions can be strings or objects. When used as an object, it has the following properties:

- **content** (string) - Required - The actual description content.
- **type** (string) - Required - The MIME type of the content (e.g., `text/plain`, `text/html`, `text/markdown`).
- **version** (string) - Optional - A version identifier for the description.

### Example
```json
{
  "description": {
    "content": "<p>The description you want to provide.</p> ",
    "type": "text/html",
    "version": "1.0"
  }
}
```

### Usage in Collections
The description object can be applied to various parts of a Postman collection, such as the collection itself or individual requests, to provide contextual information.

#### Example in a Collection Item
```json
{
  "item": {
    "name": "Create a collection",
    "description": {
      "type": "text/markdown",
      "content": "## Postman API\n The Postman API lets you programmatically access data stored in your Postman account."
    },
    "request": { ... }
  }
}
```
```

--------------------------------

### Handle script errors using try-catch

Source: https://learning.postman.com/docs/monitoring-your-api/troubleshooting-monitors

This JavaScript code demonstrates how to wrap potentially problematic code within a `try...catch` block. This ensures that if an error occurs within the `try` block, it is caught and handled gracefully by the `catch` block, preventing script execution from halting and allowing for potential error logging or fallback logic.

```javascript
try {
  // Suspicious code goes here
} catch (error) {
  console.error("An error occurred:", error);
  // Handle the error, e.g., by logging or setting a flag
}
```

--------------------------------

### Run in Postman Button Configuration

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Details on configuring the 'Run in Postman' button, including segregation of environments for multiple buttons.

```APIDOC
## Run in Postman Button Configuration

This section details how to configure the 'Run in Postman' button, especially when using multiple buttons on a single page.

### `_pm('_property.set', 'segregateEnvironments', true)`

**Description:** Enables the segregation of environments for multiple 'Run in Postman' buttons on the same page. When enabled, each button will manage its own set of environments.

**Parameters:**
- `propertyName` (string): Must be `'segregateEnvironments'`.
- `value` (boolean): Set to `true` to enable segregation.

**Usage Note:** When `segregateEnvironments` is enabled, the `runButtonIndex` parameter becomes mandatory for all `_pm()` methods that interact with environments to specify which button's environment should be affected.

### Obtaining `runButtonIndex`

If `segregateEnvironments` is enabled, you need to provide a `runButtonIndex` to differentiate between multiple 'Run in Postman' buttons. This index corresponds to the button's position on the page.

**Example using vanilla JavaScript:**
```javascript
var runButtons = Array.prototype.slice.call(document.getElementsByClassName('postman-run-button'));
var runButtonIndex = runButtons.indexOf(elem); // 'elem' is the specific button element
```

**Example using jQuery:**
```javascript
var runButtonIndex = $('postman-run-button').index(elem); // 'elem' is the specific button element
```

This `runButtonIndex` is then passed as the last argument to methods like `env.create`, `env.assign`, `env.replace`, and `env.remove` when `segregateEnvironments` is active.
```

--------------------------------

### Publish API Version

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Publish a version of an API from the Postman API Builder using the Postman CLI. Supports Git-linked repositories.

```APIDOC
## POSTMAN API PUBLISH

### Description
Publishes a snapshot of an API for the given `apiId`. You can specify which elements to publish and provide release notes.

### Method
POST

### Endpoint
`/` (This is a CLI command, not a REST endpoint)

### Parameters
#### Path Parameters
- **apiId** (string) - Required - The ID of the API to publish.

#### Query Parameters
- **--name** (string) - Required - Specifies the name of the version to publish.
- **--release-notes** (string) - Optional - Enter release notes as a string in quotes. Supports Markdown.
- **--collections** (string[]) - Optional - Specifies the collections to publish. If the API is linked with Git, provide the `filePath` instead of the ID.
- **--api-definition** (string | string[]) - Optional - Specifies the API specification to publish. If the API is linked with Git, provide the `schemaDirectoryPath`, `schemaRootFilePath`, or `schemaDirectoryPath`.
- **--do-not-poll** (boolean) - Optional - Specifies not to poll for completion status of the publish action.
- **--suppress-exit-code** (boolean) - Optional - Specifies whether to override the default exit code for the current run.
- **-x** (boolean) - Alias for `--suppress-exit-code`.

### Request Example
#### For repos not linked with Git
```bash
postman api publish <apiId> --name v1 \
--release-notes "# Some release notes information" \
--collections <collectionId1> <collectionId2> \
--api-definition <apiDefinitionId>
```

#### For repos linked with Git (using schema folder)
```bash
postman api publish <apiId> --name v1 \
--release-notes "# Some release notes information" \
--collections <collectionPath1> <collectionPath2> \
--api-definition <schemaDirectoryPath>
```

#### For repos linked with Git (using schema root file)
```bash
postman api publish <apiId> --name v1 \
--release-notes "# Some release notes information" \
--collections <collectionPath1> <collectionPath2> \
--api-definition <schemaRootFilePath>
```

### Response
(CLI command output, not a standard HTTP response)

#### Success Response
- (Output indicates successful publishing or status if `--do-not-poll` is not used)

#### Error Response Example
- `API Definition <file/folder> isn't part of API <apiId>` (If the specified API definition path is incorrect for the linked Git repository setup.)
```

--------------------------------

### Environments and Variables API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

The Environments API enables you to programmatically manage your Postman environments. You can use this API to manage your global variables and collection variables.

```APIDOC
## Environments and Variables API

### Description
Programmatically manages Postman environments and their associated global and collection variables.

### Method
GET, POST, PUT, DELETE

### Endpoint
/environments

### Parameters
None specified in the provided text.

### Request Example
Not specified in the provided text.

### Response
#### Success Response (200)
Details about environment and variable operations.

#### Response Example
Not specified in the provided text.
```

--------------------------------

### Get Cookie Value from Specific Domain (Postman)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-cookies

Retrieve the value of a specific cookie from a designated domain using `pm.cookies.jar().get()`. This is an asynchronous operation, and the cookie value is returned within a callback function.

```javascript
pm.cookies.jar().get("example.com", "cookieName", (error, value) => {
    if (error) {
        console.error(`An error occurred: ${error}`);
    } else {
        console.log(`Cookie value: ${value}`);
    }
});
```

--------------------------------

### Parameter Object - Description

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that all parameters defined for API operations include a description.

```APIDOC
## Parameter Object - Description

### Description
Every parameter defined within an operation object must have a description. This clarifies the purpose and expected format of the parameter for API consumers.

### Method
N/A (Applies to parameter objects within operations)

### Endpoint
N/A (Applies to parameter objects within operations)

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
```yaml
swagger: '2.0'
# ...
paths:
  /resources:
    get:
      parameters:
        - name: status
          description: filters resources on their status
          in: query
          type: string
      # ...
```
```

--------------------------------

### Add Descriptions to Reusable OpenAPI Schemas

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This rule highlights the necessity of providing descriptions for all reusable schema objects within the `components` object. Descriptions offer valuable context to API designers and consumers when schema names alone are insufficient.

```yaml
openapi: '3.0.3'
# ...
components:
  schemas:
    aReusableSchema:
      description: A reusable schema description
      type: object

```

--------------------------------

### Monitors API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

The Monitors API enables you to programmatically run collections, depending on specific events on your CI/CD pipelines. You can also create and run a webhook, which is a special monitor that runs a collection.

```APIDOC
## Monitors API

### Description
Programmatically runs collections based on CI/CD pipeline events. Supports creating and running webhooks as special monitors.

### Method
GET, POST, PUT, DELETE

### Endpoint
/monitors

### Parameters
None specified in the provided text.

### Request Example
Not specified in the provided text.

### Response
#### Success Response (200)
Details about monitor operations.

#### Response Example
Not specified in the provided text.
```

--------------------------------

### API Key

Source: https://learning.postman.com/docs/sending-requests/authorization/authorization-types

API key authentication involves sending a key-value pair to the API either in the request headers or query parameters. Configure this by selecting 'API Key' from the Auth Type list.

```APIDOC
## API Key

### Description
Send a key-value pair to the API in request headers or query parameters. Postman appends this information to your request.

### Method
N/A (Client-side configuration)

### Endpoint
N/A (Applies to individual requests, collections, or folders)

### Parameters
#### Request Body
- **Auth Type** (string) - Required - Must be 'API Key'
- **Key Name** (string) - Required - The name of your API key.
- **Key Value** (string) - Required - The value of your API key.
- **Add to** (string) - Required - Either 'Header' or 'Query Params'. Specifies where the key-value pair is added.

### Request Example
```json
{
  "auth": {
    "type": "apiKey",
    "keyName": "X-API-Key",
    "keyValue": "your_api_key_value",
    "addto": "Header"
  }
}
```

### Response
#### Success Response (200)
Depends on the API being called.

#### Response Example
```json
{
  "message": "Success"
}
```
```

--------------------------------

### Run Postman Runner Container

Source: https://learning.postman.com/docs/monitoring-your-api/runners/set-up-a-runner-in-your-network

Runs a Docker container using the 'postman-runner' image. It passes the runner ID and key as environment variables to the container, which are then used by the runner to connect to Postman.

```bash
docker run --rm -e POSTMAN_RUNNER_ID="<runner-id>" -e POSTMAN_RUNNER_KEY="<runner-key>" postman-runner

```

--------------------------------

### Partition Array

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $partition helper function divides an array into sub-arrays of a specified size. It takes the array and the desired chunk size as arguments. The last sub-array may contain fewer elements if the original array's length is not perfectly divisible by the chunk size.

```postman-helper
$partition([1,2,3,4,5,6,7,8,9,10], 2) -> [[1,2], [3,4], [5,6], [7,8], [9,10]]
$partition([1,2,3,4,5,6,7,8,9,10], 3) -> [[1,2,3], [4,5,6], [7,8,9], [10]]
```

--------------------------------

### User Authentication API

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This section describes the configuration for basic authentication for the user endpoint.

```APIDOC
## GET /user

### Description
Retrieves user information with basic authentication.

### Method
GET

### Endpoint
/user

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **Example** (object) - Example user data

#### Response Example
```json
{
  "userId": "123e4567-e89b-12d3-a456-426614174000",
  "username": "exampleUser"
}
```
```

--------------------------------

### Get Run Button Index using jQuery

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Obtains the index of a 'Run in Postman' button element using jQuery selectors. This provides a concise way to identify the specific button when managing multiple instances on a page.

```javascript
var runButtonIndex = $('postman-run-button').index(elem);
```

--------------------------------

### Define Mock Server Request Body (JSON)

Source: https://learning.postman.com/docs/design-apis/mock-apis/create-dynamic-responses

This snippet shows the JSON structure for the request body when setting up a mock server in Postman. It includes fields like 'username' and 'password' which can be accessed by template helpers in the response.

```json
{
    "username": "postman",
    "password": "12345"
}
```

--------------------------------

### Operation Object - Description

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Requires that every operation in the API definition includes a detailed description.

```APIDOC
## Operation Object - Description

### Description
Each operation in an API definition must have a description. This provides more detailed context about the operation's behavior, especially when the summary, path, and method are insufficient.

### Method
N/A (Applies to operation objects within paths)

### Endpoint
N/A (Applies to operation objects within paths)

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
```yaml
swagger: '2.0'
# ...
paths:
  /resources:
    get:
      description: A GET operation description
      # ...
```
```

--------------------------------

### Configure JWT Auth Method Role (Vault CLI)

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command configures a role named `postman` for the JWT auth method, linking it to the OIDC provider's discovery URL. This sets `postman` as the default role for authentication. Ensure you use the correct OIDC provider URL and a chosen role name.

```shell
vault write auth/postman-jwt/config oidc_discovery_url="<oidc-provider-url>" default_role=postman
```

--------------------------------

### Output injected resources and secrets to separate files

Source: https://learning.postman.com/docs/insights/reference/agent/kube-inject

This command injects deployment manifests from `in.yml`, generates secrets, and outputs the modified resources to `out.yml` and the secrets to `secret.yml`. This separation is useful for managing sensitive information like secrets independently.

```bash
postman-insights-agent kube inject -s="secret.yml" --project projectId -f in.yml -o out.yml
```

--------------------------------

### Publish API Version (Git Linked - Schema Folder) - Postman CLI

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Publishes an API version from a Git-linked repository where the API integration uses a schema folder. Requires providing file paths for collections and the schema directory instead of IDs. Allows specifying version name and release notes.

```bash
postman api publish <apiId> --name v1 \
--release-notes "# Some release notes information" \
--collections <collectionPath1> <collectionPath2> \
--api-definition <schemaDirectoryPath>
```

--------------------------------

### Reporter Configuration Options

Source: https://learning.postman.com/docs/postman-cli/postman-cli-reporters

Details on configuring individual reporters (JSON, JUnit, HTML) with various options to customize report generation.

```APIDOC
## Reporter Configuration Options

### Description
Configure the JSON, JUnit, and HTML reporters to create report files in your working directory. Options can be applied to specific reporters or globally.

### Method
N/A (Configuration options for command-line execution)

### Endpoint
N/A (Command-line tool configuration)

### Parameters
#### Command-line Options
- `--reporter-\<reporter\>-export <path>` (string) - Optional - Specify a path to save the report. Defaults to `/postman-cli-reports`.
- `--reporter-\<reporter\>-omitRequestBodies` (boolean) - Optional (JSON and HTML only) - Remove all request bodies from the report.
- `--reporter-\<reporter\>-omitResponseBodies` (boolean) - Optional (JSON and HTML only) - Remove all response bodies from the report.
- `--reporter-\<reporter\>-omitHeaders` (boolean) - Optional (JSON and HTML only) - Remove all request and response headers from the report.
- `--reporter-\<reporter\>-omitAllHeadersAndBody` (boolean) - Optional (JSON and HTML only) - Remove all request and response headers, and all request and response bodies, from the report.
- `--reporter-json-structure newman` (string) - Optional (JSON only) - Generate a JSON report using the Newman schema. Defaults to native Postman CLI structure.

### Request Example
```bash
postman collection run <collection-id> -r json,html --reporter-json-omitHeaders
postman collection run <collection-id> -r json,html --reporter-omitHeaders
```

### Response
#### Success Response (Output Files)
- Report files (JSON, JUnit XML, HTML) generated in the specified or default directory.

#### Response Example
N/A (CLI output)

### Notes
- Replace `<reporter>` with `json`, `junit`, or `html`.
- When using multiple reporters, options specified for a single reporter take precedence over options specified for all reporters.
```

--------------------------------

### Create OIDC Scope with Custom Claim (Vault CLI)

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command creates a scope in HashiCorp Vault with a custom claim. This allows associating an existing entity with the auth method Postman uses, preventing the creation of new entities for each user. The template maps an alias name to a template parameter. Ensure you save the scope name and claim key name.

```shell
vault write identity/oidc/scope/<scope-name> template='{ "alias_name": {{identity.entity.aliases.<mount-accessor>.name}} }' description="Gets the name of the alias associated with the specified auth method."
```

--------------------------------

### Add Description to OpenAPI Info Object

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This OpenAPI snippet demonstrates how to add a description to the info object, providing essential metadata about the API. This improves clarity for API consumers.

```yaml
Copyopenapi: '3.0.3'
info:
  title: An API name
  version: '1.0'
  description: An API description

```

--------------------------------

### Mathematical Functions: Power and Square Root

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Demonstrates the use of $power() to raise a number to a power and $sqrt() to find the square root of a number.

```FQL
$power(2,3)
```

```FQL
$sqrt(9)
```

--------------------------------

### OpenAPI Info Object - License

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Details the requirement for a license object within the info object, enabling consumers to understand how the API can be used and distributed.

```APIDOC
## Info Object - License

### Description
Includes a license object in the OpenAPI info object to clarify the API's usage terms and conditions for consumers.

### Method
N/A (Configuration)

### Endpoint
N/A (Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

#### Success Response (200)
N/A

#### Response Example
N/A

```yaml
swagger: '2.0'
info:
  title: An API name
  version: '1.0'
  license:
    name: Apache 2.0
    url: https://opensource.org/licenses/Apache-2.0
```
```

--------------------------------

### Define MCP Tools for Postman Flows

Source: https://learning.postman.com/docs/postman-ai/mcp-server-flows/create-mcp-server-flow

Defines MCP tools available to an MCP server within Postman Flows. Each tool has a name, description, and an input schema. Properties in the input schema become arguments for tool calls. This is used within the `toolDefinition` scenario.

```json
{
  "tools": [
    {
      "name": "greeter",
      "description": "Says hello to a person by their first name",
      "inputSchema": {
        "type": "object",
        "properties": {
          "first_name": {
            "type": "string",
            "description": "The person's first name"
          }
        },
        "required": [
          "first_name"
        ]
      }
    }
  ]
}
```

--------------------------------

### Date Component Extraction: Year, Month, Day

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Demonstrates extracting the year, month, and day components from a date string using the $year(), $month(), and $day() functions, and concatenating them.

```FQL
$year("2023-02-11") & "-" & $month("2023-02-11") & "-" & $day("2023-02-11")
```

--------------------------------

### HTTP Request URL for Book Titles

Source: https://learning.postman.com/docs/postman-flows/cookbook/iterate-list-for-block

This HTTP request fetches a list of book titles from the Open Library API. The 'limit' parameter restricts the number of results returned. The response is expected to contain structured data that can be further processed.

```shell
https://openlibrary.org/subjects/love.json?limit=5
```

--------------------------------

### Retrieve All Postman Environments

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Fetches an array containing all currently configured Postman environments associated with 'Run in Postman' buttons on the page. Each environment object includes its index, name, and values.

```javascript
Copy_pm('_property.get', 'environments');
```

--------------------------------

### Partition Array with $partition

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $partition() function divides an array into smaller arrays of a specified size. It returns a list containing these smaller arrays, useful for batch processing.

```FQL
$partition(payments,2)
```

--------------------------------

### Lint API with Postman CLI in Bitbucket Pipeline (Enterprise)

Source: https://learning.postman.com/docs/integrations/available-integrations/ci-integrations/bitbucket-pipelines

For enterprise teams, this snippet shows how to use the Postman CLI's `api lint` command within a Bitbucket Pipeline to enforce API Governance and Security rules. This ensures that your API adheres to defined standards on every pipeline run. This command is only available for enterprise teams.

```bash
# Example within bitbucket-pipelines.yml script section
postman api lint "your_api_id" --workingDir "/path/to/your/api/spec" --reporter cli
```

--------------------------------

### Run Postman Collection with Newman

Source: https://learning.postman.com/docs/collections/using-newman-cli/continuous-integration

Executes a Postman Collection using Newman from the command line. It requires the collection ID and your Postman API key to fetch and run the collection. This is a fundamental step for automating API tests in a CI environment.

```bash
newman run "https://api.getpostman.com/collections/collection-id?apikey=postman-api-key"
```

--------------------------------

### OpenAPI Info Object - License URL

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Emphasizes the inclusion of a license URL within the license object to provide a direct link to detailed license information.

```APIDOC
## Info Object - License URL

### Description
Ensures the license object in the OpenAPI info object contains a URL pointing to the full license details.

### Method
N/A (Configuration)

### Endpoint
N/A (Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

#### Success Response (200)
N/A

#### Response Example
N/A

```yaml
swagger: '2.0'
info:
  title: An API name
  version: '1.0'
  license:
    name: Apache 2.0
    url: https://opensource.org/licenses/Apache-2.0
```
```

--------------------------------

### Using External Libraries with require

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-require

The `require` method in Postman allows you to integrate sandbox built-in library modules into your scripts. This section lists the supported libraries, such as `ajv`, `lodash`, and `uuid`, and also notes deprecated libraries and unsupported functionalities within the `buffer` module.

```APIDOC
## Use External Libraries

The `require` method enables you to use the sandbox built-in library modules. To use a library, call the `require` method, pass the module name as a parameter, and assign the return object from the method to a variable.

### Syntax

```markdown
require(moduleName:String):function
```

### Supported Libraries

The following libraries are available for use in the sandbox:

* ajv
* chai
* cheerio
* csv-parse/lib/sync
* lodash
* moment
* postman-collection
* uuid
* xml2js

> **Deprecated Libraries:**
> * atob (use the `atob` method)
> * btoa (use the `btoa` method)
> * crypto-js (use the Web Crypto objects)
> * tv4 (use the ajv library)

### Supported NodeJS Modules

The following NodeJS modules are also available:

* path
* assert
* buffer
* util
* url
* punycode
* querystring
* string-decoder
* stream
* timers
* events

> **Unsupported `buffer` module features:** isAscii, isUtf8, resolveObjectURL, transcode, and copyBytesFrom.
```

--------------------------------

### Define MCP Prompts for Postman Flows

Source: https://learning.postman.com/docs/postman-ai/mcp-server-flows/create-mcp-server-flow

Adds prompts to an MCP server in Postman Flows, enabling structured messages and instructions for language models. Prompts have a unique name, title, description, and arguments. Clients discover and use prompts by their name, providing arguments as needed.

```json
"prompts": [
  {
    "name": "example-prompt",
    "title": "Request Code Review",
    "description": "Asks the LLM to analyze data file to find anomalies",
    "arguments": [
      {
        "name": "file",
        "description": "The data file to review",
        "required": true
      }
    ]
  }
]
```

--------------------------------

### Publish API Version (Not Git Linked) - Postman CLI

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Publishes a snapshot of an API for a given `apiId` when the repository is not linked with Git. Allows specifying the version name, release notes, associated collections, and the API definition. Does not poll for completion status by default.

```bash
postman api publish <apiId> --name v1 \
--release-notes "# Some release notes information" \
--collections <collectionId1> <collectionId2> \
--api-definition <apiDefinitionId>
```

--------------------------------

### Convert Postman Collection from v1 to v2

Source: https://learning.postman.com/docs/getting-started/importing-and-exporting/importing-data

This command converts a Postman Collection file from v1 to v2 format. It takes the input file path, specifies the output file path, and sets the format versions. The `-P` flag indicates a pretty-print output.

```bash
postman-collection-transformer convert -i <path to the input Postman Collection file> -o <path to the downloaded Postman file> -j 1.0.0 -p 2.0.0 -P

```

--------------------------------

### OpenAPI Info Object - Description

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Highlights the importance of including a description in the OpenAPI info object to provide consumers with essential information about the API's purpose and usage.

```APIDOC
## Info Object - Description

### Description
Ensures the OpenAPI info object includes a description to inform API consumers about the API's functionality and use cases.

### Method
N/A (Configuration)

### Endpoint
N/A (Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

#### Success Response (200)
N/A

#### Response Example
N/A

```yaml
swagger: '2.0'
info:
  title: An API name
  version: '1.0'
  description: An API description
```
```

--------------------------------

### Run a Collection with Multiple Reporters

Source: https://learning.postman.com/docs/postman-cli/postman-cli-reporters

This command shows how to use multiple built-in reporters for a single collection run. Reporters are specified as a comma-separated list. If you want to include the CLI reporter when using other reporters, it must be explicitly listed.

```shell
postman collection run <collection-id> -r cli,json
```

--------------------------------

### Publish API Version (Git Linked - Schema Root File) - Postman CLI

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Publishes an API version from a Git-linked repository where the API integration uses a schema root file (Postman v10.18+). Requires providing file paths for collections and the schema root file instead of IDs. Allows specifying version name and release notes.

```bash
postman api publish <apiId> --name v1 \
--release-notes "# Some release notes information" \
--collections <collectionPath1> <collectionPath2> \
--api-definition <schemaRootFilePath>
```

--------------------------------

### Basic pm.test syntax for HTTP requests

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-test-expect

Defines a test specification for an HTTP request. It requires a test name and a function defining the test logic. Postman outputs test results based on these specifications.

```javascript
pm.test(testName , specFunction)
```

--------------------------------

### Run Postman Collection with Environment using Newman

Source: https://learning.postman.com/docs/collections/using-newman-cli/continuous-integration

Runs a Postman Collection with a specified environment using Newman. This command includes the `--environment` flag, allowing you to pass environment variables necessary for the collection's tests, such as API endpoints or authentication tokens. This is crucial for testing in different deployment stages.

```bash
newman run "https://api.getpostman.com/collections/collection-id?apikey=postman-api-key"
--environment "https://api.getpostman.com/environments/environment-id?apikey=postman-api-key"
```

--------------------------------

### Reference Reusable Schemas in Properties

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Promotes the use of reusable schemas via `$ref` for properties in response objects and body parameters. This enhances design consistency, readability, and maintainability by avoiding duplicated model definitions.

```yaml
swagger: '2.0'

```

--------------------------------

### Mock Servers API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Perform CRUD operations on your mock servers, set mock servers to public or private, list all calls received by a mock server, and manage mock server responses for 5XX errors.

```APIDOC
## Mock Servers API

### Description
Manages mock servers, including CRUD operations, setting visibility (public/private), listing calls, and managing error responses.

### Method
GET, POST, PUT, DELETE

### Endpoint
/mocks

### Parameters
None specified in the provided text.

### Request Example
Not specified in the provided text.

### Response
#### Success Response (200)
Details about mock server operations.

#### Response Example
Not specified in the provided text.
```

--------------------------------

### Create Postman JWT Role

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command creates a role named 'postman' for JWT authentication using the postman-jwt auth method. It binds to specified audiences, uses the 'sub' claim for user identification, and assigns a policy to the role. Ensure you replace placeholders like '<oidc-client-id>' and '<policy-name>'.

```shell
vault write auth/postman-jwt/role/postman bound_audiences="<oidc-client-id>" user_claim=sub token_policies=<policy-name> role_type=jwt
```

--------------------------------

### PATCH /resources

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Partially updates an existing resource. Requires a request body.

```APIDOC
## PATCH /resources

### Description
A PATCH operation for partially updating resources. Requires a request body.

### Method
PATCH

### Endpoint
/resources

#### Request Body
- **partialUpdateField** (any) - Required - Example field for the request body.

### Request Example
```json
{
  "partialUpdateField": "update value"
}
```

### Response
#### Success Response (200)
- **example** (object) - Example response structure

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Sign in to Postman CLI

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Authenticates your session with Postman. The `login` command prompts for browser-based authentication. You can optionally use an API key or specify the EU region for data residency plans.

```bash
postman login
```

```bash
postman login --with-api-key ABCD-1234-1234-1234-1234-1234
```

```bash
postman login --with-api-key ABCD-1234-1234-1234-1234-1234 --region eu
```

--------------------------------

### Postman Sandbox API Reference

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/overview

The Postman Sandbox provides JavaScript APIs through the `pm` object to interact with various aspects of Postman during script execution. This includes accessing request and response data, managing variables, writing tests, sending additional requests, and visualizing results.

```APIDOC
## Postman Sandbox API

### Description
The Postman Sandbox API, accessed via the `pm` object, allows you to programmatically interact with Postman functionalities within your scripts. This includes accessing request and response details, managing variables, sending new HTTP requests, writing test assertions, and utilizing the visualizer.

### Core Objects & Methods

- **`pm.cookies`**: Methods for accessing and manipulating cookies.
- **`pm.request`**: Object to reference request details.
- **`pm.response`**: Object to reference response details.
- **`pm.message`**: Object returned for streaming protocols, similar to request/response.
- **`pm.info`**: Object containing meta information related to the current request and script.
- **`pm.sendRequest`**: Method to send HTTP requests from within your scripts.
- **`pm.execution`**: Object providing context about collection runs, including request status and position.
- **`pm.require`**: Method to import packages from a team's Package Library or external registries.
- **`pm.visualizer`**: Object to create visual representations of API responses.
- **`pm.vault`**: Methods for accessing and managing vault secrets.
- **`pm.test`**: Function to define test specifications.
- **`pm.expect`**: Function used for creating assertions within tests.

### Variables

- **Script Variables**: Access and manipulate different variable types and scopes within your scripts. Refer to "Reference variables in Postman scripts" for detailed usage.

### Example Usage (Conceptual)

```javascript
// Accessing request data
const requestBody = pm.request.body;

// Sending a new request
pm.sendRequest("https://api.example.com/data", function (err, response) {
    if (err) {
        console.log(err);
    } else {
        console.log(JSON.parse(response.text()));
    }
});

// Writing a test assertion
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// Accessing a variable
const userId = pm.variables.get("userId");
```

### Further Resources

- Access cookies in Postman scripts
- Reference requests and responses in scripts
- Use scripts to send requests in Postman
- Reference Postman requests in scripts
- Reference message data in scripts
- Use scripts in collection runs
- Reference variables in Postman scripts
- Script Postman visualizations
- Reference vault secrets in Postman scripts
- Writing tests and assertions in scripts
- Import packages into your scripts
```

--------------------------------

### Request Definition with HTML Description

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Demonstrates how to include a rich HTML description for a request definition. This allows for formatted context about the request.

```json
{
  "url": "https://postman-echo.com/get",
  "method": "GET",
  "description": {
    "content": "<p>The description you want to provide.</p> ",
    "type": "text/html",
    "version": "Description can have versions associated with it. Use this field to specify a version for your description"
  }
}
```

--------------------------------

### Inject deployment manifests to stdout

Source: https://learning.postman.com/docs/insights/reference/agent/kube-inject

This command injects deployment manifests from a specified YAML file and outputs the modified resources to standard output. Each injected deployment will send traffic from the endpoint to the Postman Insights Agent. This is useful for previewing changes before applying them.

```bash
postman-insights-agent kube inject --project projectId -f resources.yml
```

--------------------------------

### Assert Environment Variable in Postman Tests

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-scripts

This code snippet shows how to verify that a specific environment variable in Postman is set to an expected value. It uses `pm.test` to define a test named 'environment to be production' and employs `pm.expect` to assert that the value retrieved by `pm.environment.get("env")` is strictly equal to 'production'. This is useful for ensuring correct environment configurations.

```javascript
pm.test("environment to be production", function () {
    pm.expect(pm.environment.get("env")).to.equal("production");
});
```

--------------------------------

### Run Postman Monitor with CLI

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Executes a Postman monitor in the Postman cloud, useful for CI/CD integration to catch regressions. It polls for completion and returns results, requiring a monitor ID. Options include `--timeout` and `--suppress-exit-code`.

```bash
postman monitor run 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12
```

--------------------------------

### Create Entity Alias for Postman JWT Authentication

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command creates an alias for an existing entity, associating it with the 'postman-jwt' auth method. This is crucial for users authenticating with HashiCorp Vault via Postman, especially when using custom claims. Replace '<entity-id>' and '<postman-jwt-accessor>' with your specific values.

```shell
vault write /identity/entity-alias name="<entity-id>" canonical_id="<entity-id>" mount_accessor="<postman-jwt-accessor>"
```

--------------------------------

### Read and Parse Collection from JSON File using Collection SDK

Source: https://learning.postman.com/docs/developer/collection-sdk

This snippet demonstrates how to use the Postman Collection SDK in Node.js to read a JSON file containing collection data, parse it, and create a Collection object. It requires the 'fs' module for file system operations and the 'postman-collection' module. The output is the JSON representation of the created collection.

```javascript
var fs = require('fs');
  Collection = require('postman-collection').Collection;
  myCollection;

myCollection = new Collection(JSON.parse
  (fs.readFileSync('sample-collection.json').toString()));

console.log(myCollection.toJSON());

```

--------------------------------

### Get Collection Details via Postman API

Source: https://learning.postman.com/docs/postman-api-network/showcase/publish/maintain-public-apis

This snippet demonstrates how to retrieve a collection's details using the Postman API. It requires specifying the collection ID as a path variable and setting up authentication. The API returns the collection as a JSON object.

```http
GET https://api.getpostman.com/collections/:collectionId

---

Params:
  - key: collectionId
    value: "YOUR_TEAM_COLLECTION_ID"

---

Authorization:
  Type: Bearer Token
  Token: "YOUR_POSTMAN_API_KEY"
```

--------------------------------

### PUT /resources

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Updates an existing resource. Requires a request body.

```APIDOC
## PUT /resources

### Description
A PUT operation for updating resources. Requires a request body.

### Method
PUT

### Endpoint
/resources

#### Request Body
- **exampleField** (any) - Required - Example field for the request body.

### Request Example
```json
{
  "exampleField": "example value"
}
```

### Response
#### Success Response (200)
- **example** (object) - Example response structure

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Environment Management

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

This section covers the core methods for managing environments associated with the 'Run in Postman' button.

```APIDOC
## Environment Management

This section covers the core methods for managing environments associated with the 'Run in Postman' button.

### `_pm('env.create', environment_name, data, runButtonIndex)`

**Description:** Creates a new environment. If an environment with the same name already exists, this method will fail.

**Parameters:**
- `environment_name` (string) - The name of the environment to create.
- `data` (object) - An object containing key-value pairs for the environment variables.
- `runButtonIndex` (number, optional) - The index of the 'Run in Postman' button if `segregateEnvironments` is enabled.

**Response:** Returns the total number of environments on success, `false` on failure.

### `_pm('env.assign', environment_name, data, preventOveride, runButtonIndex)`

**Description:** Updates an existing environment. This method cannot create new environments; it only modifies existing ones.

**Parameters:**
- `environment_name` (string) - The name of the environment to update.
- `data` (object) - An object containing key-value pairs to update.
- `preventOveride` (boolean) - If `true`, prevents overriding existing variables.
- `runButtonIndex` (number, optional) - The index of the 'Run in Postman' button if `segregateEnvironments` is enabled.

**Response:** Returns `true` on success, `false` on failure.

### `_pm('env.replace', environment_name, data, runButtonIndex)`

**Description:** Replaces the entire contents of an existing environment with new data. The environment must exist.

**Parameters:**
- `environment_name` (string) - The name of the environment to replace.
- `data` (object) - An object containing the new key-value pairs for the environment.
- `runButtonIndex` (number, optional) - The index of the 'Run in Postman' button if `segregateEnvironments` is enabled.

**Response:** Returns `true` on success, `false` on failure.

### `_pm('env.remove', environment_name, runButtonIndex)`

**Description:** Removes an existing environment. The environment must exist.

**Parameters:**
- `environment_name` (string) - The name of the environment to remove.
- `runButtonIndex` (number, optional) - The index of the 'Run in Postman' button if `segregateEnvironments` is enabled.

**Response:** Returns `true` on success, `false` on failure.

### `_pm('_property.get', 'environments')`

**Description:** Retrieves all environments currently associated with the 'Run in Postman' buttons on the page.

**Response:** An array of environment objects, each containing `button_index`, `name`, and `values`.

**Example Response:**
```json
[
  {
    "button_index": 0,
    "name": "env1",
    "values": [
      {
        "key": "testKey",
        "value": "testValue",
        "enabled": true
      }
    ]
  }
]
```
```

--------------------------------

### Pull Newman Docker Image

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-with-docker

Downloads the latest Newman Docker image from Docker Hub. This image contains Newman and its dependencies, allowing you to run collections in a containerized environment.

```shell
docker pull postman/newman
```

--------------------------------

### Postman: Demonstrate Variable Scope Precedence in Scripts

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-variables

This script illustrates how Postman prioritizes variables when multiple variables with the same name exist across different scopes (collection, environment, local). It shows how `pm.variables.get()` defaults to the most specific scope, while `pm.collectionVariables.get()` and `pm.environment.get()` access specific scopes.

```javascript
// collection var 'score' = 1
// environment var 'score' = 2

// first request run
console.log(pm.variables.get('score')); // outputs 2
console.log(pm.collectionVariables.get('score')); // outputs 1
console.log(pm.environment.get('score')); // outputs 2

// second request run
pm.variables.set('score', 3);// local var
console.log(pm.variables.get('score')); // outputs 3

// third request run
console.log(pm.variables.get('score')); // outputs 2

```

--------------------------------

### Request Object Structure

Source: https://learning.postman.com/collection-format/reference/request

This section details the fields available within a 'Request' object in a Postman Collection, including URL, authentication, method, headers, and body.

```APIDOC
## Request Object

A request object in a Postman Collection represents an HTTP request.

### Description
Defines the details of an HTTP request, including the URL, method, headers, and body.

### Fields

#### Reference Table

| Field Name | Type | Required | Description |
|---|---|---|---|
| url | #url | `false` | The URL of this request. |
| auth | #auth | `false` | The authentication helper that this request uses. |
| proxy | #proxy | `false` | Configure a custom proxy for a particular URL match. |
| certificate | #certificate | `false` | The SSL certificate used in this request. |
| method | `string` | `false` | The standard HTTP method associated with this request. |
| description | #description | `false` | The description of this request and its parameters. |
| header | #header | `false` | The HTTP headers of this request. |
| body | `object` | `false` | The data of the request body. |

### Example

```json
{
  "info": {
    "_postman_id": "a-collection-id",
    "name": "My Collection",
    "schema": "https://schema.pstmn.io/collection/v1"
  },
  "item": [
    {
      "name": "Example Request",
      "request": {
        "method": "GET",
        "header": [],
        "url": {
          "raw": "https://api.example.com/data",
          "protocol": "https",
          "host": [
            "api",
            "example",
            "com"
          ],
          "path": [
            "data"
          ]
        },
        "description": "A sample GET request."
      },
      "response": []
    }
  ]
}
```
```

--------------------------------

### Add License to OpenAPI Info Object (YAML)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This code snippet illustrates how to include a 'license' object within the 'info' section of an OpenAPI specification. This helps consumers understand how the API can be copied and used.

```yaml
Copyswagger: '2.0'
info:
  title: An API name
  version: '1.0'
  license:
    name: Apache 2.0
    url: https://opensource.org/licenses/Apache-2.0

```

--------------------------------

### Configure Newman Output and Reporters

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

Options to control the appearance of CLI output, enable verbose logging, suppress output, and generate reports in various formats like JSON or JUnit.

```bash
newman run my-collection.json --color off

```

```bash
newman run my-collection.json --verbose

```

```bash
newman run my-collection.json -x

```

```bash
newman run my-collection.json --disable-unicode

```

```bash
newman run my-collection.json -r json

```

```bash
newman run my-collection.json -r cli,junit

```

--------------------------------

### Postman CLI: Push Workspace (Default)

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Executes the 'postman workspace push' command with default settings, which includes an automatic 'prepare' step and interactive prompts for confirmation.

```bash
postman workspace push
```

--------------------------------

### Path Syntax - No Trailing Slashes

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that API paths do not have trailing slashes to maintain consistency and prevent potential issues with tooling.

```APIDOC
## Path Syntax - No Trailing Slashes

### Description
API paths should not end with a trailing slash. This prevents inconsistencies where `/path/` and `/path` might be treated as different resources by some tools.

### Method
N/A (Applies to API path definitions)

### Endpoint
N/A (Applies to API path definitions)

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
```yaml
swagger: '2.0'
# ...
paths:
  '/resources':
    # ...
```
```

--------------------------------

### User and Usage Data API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Retrieves information about the authenticated user, including account details and current usage statistics like remaining API requests for the month.

```APIDOC
## Get Authenticated User API

### Description
The Get authenticated user API returns information about the API key’s owner. Use this endpoint to get details about your account and current usage information, such as how many API requests you can perform until the end of the month.

### Method
GET

### Endpoint
/user/me
```

--------------------------------

### Log environment details in Postman scripts

Source: https://learning.postman.com/docs/monitoring-your-api/troubleshooting-monitors

This JavaScript snippet logs the current environment object to the Postman Console. This is useful for debugging to ensure that the correct environment is being used across different runs (local vs. monitor) and to inspect the variables available in the current scope.

```javascript
console.log(environment);
```

--------------------------------

### pm.test for asynchronous functions with done callback

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-test-expect

Illustrates how to test asynchronous functions within Postman scripts using `pm.test` and an optional `done` callback. This is useful for handling operations with delays, like `setTimeout`.

```javascript
pm.test('async test', function (done) {
  setTimeout(() => {
    pm.expect(pm.response.code).to.equal(200);
    done();
  }, 1500);
});
```

--------------------------------

### Attach AWS IAM Policy for ECS Permissions

Source: https://learning.postman.com/docs/insights/get-started/ecs

This JSON policy grants the necessary permissions for the Postman Insights Agent to manage ECS services and task definitions. It allows actions like updating services, registering task definitions, and describing clusters. This policy should be attached to the AWS profile used by the agent.

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ecs:UpdateService",
                "ecs:RegisterTaskDefinition",
                "ecs:DescribeServices",
                "ecs:TagResource",
                "ecs:DescribeTaskDefinition",
                "ecs:DescribeClusters"
                ],
            "Resource": "*"
        }
    ]
}
```

--------------------------------

### Connect to MCP Server via HTTP

Source: https://learning.postman.com/docs/postman-ai/mcp-servers/interact

This code snippet provides the URL format for connecting to an MCP server configured for HTTP communication. It specifies the local host and a default port, which is used when configuring the server's communication method to HTTP.

```http
http://localhost:3001/mcp
```

--------------------------------

### Lint API Definition

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Lint an API definition file using the Postman CLI. This command checks for rule violations based on severity levels.

```APIDOC
## POSTMAN API LINT

### Description
Lints an API definition file to check for rule violations.

### Method
POST

### Endpoint
`/` (This is a CLI command, not a REST endpoint)

### Parameters
#### Path Parameters
- **apiId** (string) - Required - The ID of the API to lint.

#### Query Parameters
- **--fail-severity** (string) - Optional - Triggers an exit failure code for rule violations at or higher than the specified severity level. Options: `HINT`, `INFO`, `WARN`, `ERROR` (default).
- **-f** (string) - Alias for `--fail-severity`.
- **--suppress-exit-code** (boolean) - Optional - Specifies whether to override the default exit code for the current run.
- **-x** (boolean) - Alias for `--suppress-exit-code`.

### Request Example
```bash
postman api lint my-definition-file.json
postman api lint 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12
```

### Response
(CLI command output, not a standard HTTP response)

#### Success Response (0 exit code)
- (No specific output, indicates successful linting with no critical errors)

#### Response Example
(Output will vary based on linting results and severity settings)
```

--------------------------------

### Check if a JSON field contains a specific value

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/conditional-data-selection

The $contains function in FQL checks if a specified field within a JSON object contains a particular substring. This example checks the 'description' of the first item in the 'payments' array for the string 'recurring', returning a boolean true or false. It's useful for validating data content.

```FQL
$contains(payments[0].description, "recurring")
```

--------------------------------

### Run a Collection with a Specific Reporter

Source: https://learning.postman.com/docs/postman-cli/postman-cli-reporters

This command demonstrates how to run a Postman collection and generate a report using a specified built-in reporter. The reporter can be CLI, JSON, JUnit, or HTML. Reports are saved in the 'postman-cli-reports' directory by default.

```shell
postman collection run <collection-id> -r <reporter>
```

--------------------------------

### OpenAPI Info Object - Terms of Service

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Stresses the importance of including a terms of service URL in the info object, especially for public APIs, to outline usage policies.

```APIDOC
## Info Object - Terms of Service

### Description
Requires the OpenAPI info object to include a URL for the API's Terms of Service, crucial for public APIs.

### Method
N/A (Configuration)

### Endpoint
N/A (Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

#### Success Response (200)
N/A

#### Response Example
N/A

```yaml
swagger: '2.0'
info:
  title: An API name
  version: '1.0'
  termsOfService: https://example.com/tos
```
```

--------------------------------

### GraphQL Request Configuration

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Details how to configure GraphQL requests within Postman, including the query and variables.

```APIDOC
## GraphQL Request Configuration

### Description
Enables sending GraphQL requests over HTTP, similar to RESTful APIs. Allows specifying the GraphQL query and its corresponding variables.

### Method
POST (Typically)

### Endpoint
Your GraphQL endpoint

### Parameters
#### Request Body
- **query** (string) - Required - The GraphQL query string.
- **variables** (object/string) - Optional - The variables for the GraphQL query.

### Request Example
```json
{
  "query": "\n      {\n        query(username: $username){\n          name\n          email\n        }\n      }\n    ",
  "variables": "{ 'username': 'johndoe' }"
}
```
```

--------------------------------

### Silence Specific CLI Reporter

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-built-in-reporters

This command demonstrates how to run a collection with multiple reporters (CLI and JSON) while specifically silencing only the CLI reporter. The `--reporter-[reporter-name]-[reporter-option]` syntax is used to target options for individual reporters.

```bash
newman run my-collection.json -r cli,json --reporter-cli-silent

```

--------------------------------

### Produces Field Definition

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Addresses issues related to the `produces` field in Swagger/OpenAPI definitions, ensuring the API clearly defines the MIME types it can return.

```APIDOC
## Produces Field Definition Issues

### Description
These issues concern the `produces` field in the API definition. If not defined or not populated correctly, the API's output format can be ambiguous, potentially leading to security risks or compatibility problems.

### Method
N/A (Configuration issue)

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A

## Scenarios and Resolutions:

### Produces field is not defined
- **Issue:** If the global `produces` field isn’t defined, the API could return any form of data.
- **Fix:** The `produces` field needs to be defined in the schema.
```yaml
swagger: '2.0'
paths: {}
consumes:
  - application/json
produces:
  - application/json
```

### Produces field does not contain any item
- **Issue:** If the `produces` field has an empty array, the API can return any type of data by default.
- **Fix:** The global `produces` field needs at least one item with a valid MIME type in the array.
```yaml
swagger: '2.0'
paths: {}
produces:
  - application/json
```

### Produces field for the operation does not contain any item
- **Issue:** No `produces` field in the operation means that API can return any type of data by default.
- **Fix:** The `produces` field in any operation needs to have at least one item in the array.
```yaml
swagger: '2.0'
paths:
  /user/{userId}:
    get:
      produces:
        - application/json
```

### Operation does not contain produces field
- **Issue:** If both the global `produces` field and operation’s `produces` field for any operation aren’t defined, anyone can exploit your API.
- **Fix:** Define a `produces` field in the operation if not defined at the global level.
```yaml
swagger: '2.0'
paths:
  /user/{userId}:
    get:
      produces:
        - application/json
  ...
...
```
```

--------------------------------

### Add descriptions to schema properties in OpenAPI

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that all properties within an OpenAPI schema object have a 'description'. This provides clarity to API consumers when the schema name and context are insufficient. A well-defined description aids in understanding the purpose and usage of each property.

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    get:
      responses:
        '200':
          description: A success response
          content:
            'application/json':
              schema:
                properties:
                  aProperty:
                    description: A property description
                    type: string

```

--------------------------------

### Full URL Encoding and Decoding

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Demonstrates the use of $encodeUrl() to encode an entire URL, including non-ASCII characters, and $decodeUrl() to revert the encoding.

```FQL
$encodeUrl("https://faketranslatewebsite.com/?phrase=こんにちは")
```

```FQL
$decodeUrl("https://faketranslatewebsite.com/?phrase=%E3%81%93%E3%82%93%E3%81%AB%E3%81%A1%E3%81%AF")
```

--------------------------------

### Export JSON Report to a Specific Directory

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-built-in-reporters

This command shows how to generate collection run reports using the CLI and JSON reporters, and specifically directs the output of the JSON reporter to a designated directory named 'json-file-reports'. The `--reporter-json-export` option is used to control the output path for the JSON file.

```bash
newman run my-collection.json -r cli,json --reporter-json-export json-file-reports

```

--------------------------------

### Setting Environment/Global Variables Programmatically in Postman

Source: https://learning.postman.com/docs/sending-requests/variables/variables

This snippet shows how to set environment or global variables programmatically using Postman's scripting capabilities. These variables are saved for later use within their respective scopes. If issues arise, the Postman Console can be used for debugging.

```javascript
pm.environment.set("variable_name", "variable_value");
pm.globals.set("variable_name", "variable_value");
```

--------------------------------

### Create a Private API Network folder

Source: https://learning.postman.com/docs/collaborating-in-postman/private-api-network/publish-private-network-elements-with-api

This HTTP request creates a folder in your Private API Network. A folder can contain multiple elements, such as workspaces, collections, or APIs.

```APIDOC
## POST /network/private

### Description
Creates a folder in your Private API Network to organize elements like workspaces, collections, or APIs.

### Method
POST

### Endpoint
`https://api.getpostman.com/network/private`

### Parameters
#### Request Body
- **folder** (object) - Required - An object containing folder details.
  - **name** (string) - Required - The name of the folder.
  - **description** (string) - Optional - A description for the folder.

### Request Example
```json
{
    "folder": {
        "name": "Billing",
        "description": "The Billing API."
    }
}
```

### Response
#### Success Response (200)
- **id** (integer) - The unique identifier for the created folder.
- **parentFolderId** (integer) - The ID of the parent folder.
- **updatedAt** (string) - Timestamp of the last update.
- **updatedBy** (integer) - User ID who last updated the folder.
- **createdBy** (integer) - User ID who created the folder.
- **createdAt** (string) - Timestamp of creation.
- **name** (string) - The name of the folder.
- **description** (string) - The description of the folder.
- **type** (string) - The type of element, which is 'folder'.

#### Response Example
```json
{
    "id": 1,
    "parentFolderId": 0,
    "updatedAt": "2023-08-03T13:18:25.000Z",
    "updatedBy": 12345678,
    "createdBy": 12345678,
    "createdAt": "2023-08-03T13:18:25.000Z",
    "name": "Billing",
    "description": "The Billing API.",
    "type": "folder"
}
```
```

--------------------------------

### Workspaces API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Use the Workspaces APIs to manage your Postman workspaces. These endpoints enable you to create temporary workspaces to test, which you can then delete when you’re finished. You can also save a backup of another workspace or specific resources (such as collections or APIs) using the Postman API.

```APIDOC
## Workspaces API

### Description
Manages Postman workspaces, allowing for creation, deletion, and backup of workspaces and their resources.

### Method
GET, POST, PUT, DELETE

### Endpoint
/workspaces

### Parameters
None specified in the provided text.

### Request Example
Not specified in the provided text.

### Response
#### Success Response (200)
Details about workspace operations.

#### Response Example
Not specified in the provided text.
```

--------------------------------

### Add Descriptions to Reusable Schemas (Swagger/OpenAPI)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that all reusable schema objects within the definitions section of an OpenAPI or Swagger specification include a 'description' field. This clarifies the purpose and usage of the schema for API consumers.

```yaml
swagger: '2.0'
# ...
definitions:
  aReusableSchema:
    description: a reusable schema description
    type: object

```

--------------------------------

### Ensure HTTPS for Server URL

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet demonstrates how to specify a server URL using HTTPS. It's crucial for encrypting all communication between the client and the API, protecting sensitive data in transit.

```yaml
get:
  operationId: getPetsById
  servers:
    - url: https://my.api.example.com/
```

--------------------------------

### Project structure with Postman collection

Source: https://learning.postman.com/docs/collections/using-newman-cli/integration-with-travis

This shows the basic file structure required for Travis CI integration. The Postman collection (JSON file) is placed in a 'tests' folder at the root of the project.

```tree
. 
└── tests
    └── hello_world.postman_collection.json

```

--------------------------------

### Proxy Configuration

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Defines how to configure proxy settings for requests.

```APIDOC
## Proxy Configuration

### Description
Allows specifying proxy configuration for requests when a proxy server is in use.

### Method
N/A (Configured within request settings)

### Endpoint
N/A

### Parameters
#### Request Settings (Proxy)
- **match** (string) - The URL match for which the proxy config is defined. Defaults to `http+https://*/*`.
- **host** (string) - The proxy server host.
- **port** (number) - The proxy server port.
- **tunnel** (boolean) - Enables or disables tunneling for the proxy connection.
- **disabled** (boolean) - When set to `true`, ignores this proxy configuration element.
```

--------------------------------

### Handle Complex Objects/Arrays in Postman Environment Variables

Source: https://learning.postman.com/docs/tests-and-scripts/run-tests/test-with-monitors

Demonstrates how to store and retrieve complex data structures like objects and arrays in Postman environment variables by stringifying and parsing them. This is crucial for passing non-atomic values between requests, preventing data loss.

```javascript
Copy// set the value
pm.environment.set('complexObj', JSON.stringify(myComplexObjOrArray, null, 2));

// get the value
var theValue;
try {
    theValue = JSON.parse(pm.environment.get('complexObj'));
}
catch (e) {
    console.error(e);
    theValue = { __parseError: true };
}
if (theValue.__parseError) {
    // handle parse errors here
}
```

--------------------------------

### Specify Newman Folder and Working Directory

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

Options to run specific folders within a collection or to set a working directory for Newman, which affects how relative paths are resolved.

```bash
newman run my-collection.json --folder "My Tests"

```

```bash
newman run my-collection.json --working-dir "/path/to/working/dir"

```

--------------------------------

### Postman Variable Usage in URL Path

Source: https://learning.postman.com/collection-format/advanced-concepts/variables

Demonstrates how to use a variable in a URL path, specifically using a colon prefix for path parameters. The variable 'customerId' is defined separately and referenced in the URL.

```json
{
  "item": {
    "name": "Collection Variable Example",
    "request": "https://postman-echo.com/get/customer/:customerId"
  },
  "variable": [
    {
      "id": "e5b2bde6-15e5-4081-92c9-4ae767433032",
      "key": "customerId",
      "value": "123abc",
      "type": "string",
      "disabled": false
    }
  ]
}
```

--------------------------------

### Import Public Packages from npm and JSR

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/external-package-registries

Demonstrates how to import public packages from npm and JSR registries into Postman scripts. It shows the syntax for using `pm.require` with the package registry, name, and version. The imported package is then used to call its functions.

```javascript
// package imported from npm
const npmVariableName = pm.require('npm:package-name@version-number');

npmVariableName.functionName()

// package imported from jsr
const jsrVariableName = pm.require('jsr:package-name@version-number');

jsrVariableName.functionName()
```

--------------------------------

### Global Server URL Protocol

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures the global server URL uses HTTPS for secure communication.

```APIDOC
## Global Server URL Security

### Description
Configures the global server URL to use HTTPS to prevent unencrypted data transmission.

### Method
N/A (Configuration based)

### Endpoint
N/A (Global server configuration)

### Parameters
None

### Request Example
N/A

### Response
N/A

#### Resolution Example
```yaml
servers:
  - url: https://my.api.example.com/
    description: API server
# ...
components:
  securitySchemes:
    OAuth2:
      type: oauth2
# ...
security:
  - OAuth2:
      - write
      - read
```
```

--------------------------------

### Reference Reusable Schemas in OpenAPI

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This rule promotes the use of reusable schemas via `$ref` for consistency and maintainability in your API definition. By consolidating models in `definitions` (or `components/schemas`), you avoid duplication and improve readability.

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    get:
      responses:
        '200':
          description: a success response
          content:
            'application/json':
              schema:
                $ref: '#/components/schemas/Resources'
components:
  schemas:
    Resources:
      type: object

```

--------------------------------

### Request Descriptions

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Add context to your API definitions using descriptions. These can be strings or objects and support Markdown, HTML, or plain text content.

```APIDOC
## Request Descriptions

### Description
Descriptions provide additional context for your API definitions. They can be simple strings or structured objects.

### Description Object Structure
```json
{
  "content": "Your description content here. Can include Markdown, HTML, or plain text.",
  "type": "text/plain | text/html | application/markdown",
  "version": "Optional version for the description."
}
```

### Example Request Definition with Description
```json
{
  "url": "https://postman-echo.com/get",
  "method": "GET",
  "description": {
    "content": "<p>This endpoint retrieves data and includes a detailed description.</p>",
    "type": "text/html",
    "version": "1.0"
  }
}
```
```

--------------------------------

### Postman Visualizer: Handlebars Template for Response Data

Source: https://learning.postman.com/docs/sending-requests/response-data/visualizer

This snippet demonstrates how to create a Handlebars template string to structure response data into an HTML table. The template iterates over an array of objects, extracting 'name' and 'email' properties for each row. It's designed to be used with Postman's Visualizer.

```javascript
var template = `
    <table bgcolor="#FFFFFF">
        <tr>
            <th>Name</th>
            <th>Email</th>
        </tr>

        {{#each response}}
            <tr>
                <td>{{name}}</td>
                <td>{{email}}</td>
            </tr>
        {{/each}}
    </table>
`;
```

--------------------------------

### Postman Visualizer: Setting Template and Data

Source: https://learning.postman.com/docs/sending-requests/response-data/visualizer

This JavaScript code snippet shows how to use the `pm.visualizer.set()` method in Postman. It takes a Handlebars template string and a data object as arguments. The data object's 'response' property, containing the parsed JSON response, is made available to the template for rendering.

```javascript
// Set visualizer
pm.visualizer.set(template, {
    // Pass the response body parsed as JSON as `data`
    response: pm.response.json()
});
```

--------------------------------

### Loop Request with Iteration Limit

Source: https://learning.postman.com/docs/collections/running-collections/building-workflows

Enables repeating a request multiple times before proceeding. It uses a variable to track iterations and stops the loop by setting the next request to null after a predefined count. This prevents infinite loops.

```javascript
var i = !pm.variables.get("i") ? 1 : pm.variables.get("i");

if (i < 3) {
    console.log("this is run "+i+" for request " + pm.execution.location.current);
    pm.execution.setNextRequest(pm.execution.location.current)
    i++;
    pm.variables.set("i", i);
} else {
    pm.execution.setNextRequest(null);
}

```

--------------------------------

### Compare Date Components with $hasSameDate

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Checks if specified components (years, months, days, etc.) of two timestamps are identical. The units to compare are provided as an array of strings.

```Postman Script
console.log($hasSameDate("23-02-08", "2019-02-08", ["month", "day"])); // Output: true
console.log($hasSameDate("2023-02-01", "2023-02-08", ["month", "year"])); // Output: true
console.log($hasSameDate("23-02-01", "2023-02-08", ["month", "year"])); // Output: true
console.log($hasSameDate("2023-02-01T07:15:54.730Z", "2023-02-01T14:00:22.340Z", ["year","month", "day"])); // Output: true
```

--------------------------------

### Match String Pattern

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $match helper function extracts all substrings from a given string that match a specified pattern (string or regular expression). It returns an array of the matched substrings. This is powerful for data extraction and validation based on patterns.

```postman-helper
$match("ababbabbbcc",/a(b+)/) -> ["ab", "abb", "abbb"]
```

--------------------------------

### Add Workspace to Folder (HTTP)

Source: https://learning.postman.com/docs/collaborating-in-postman/private-api-network/publish-private-network-elements-with-api

This HTTP request adds a workspace to a specified parent folder in your Private API Network. It requires authentication via an x-api-key and a JSON payload containing the workspace ID and its parentFolderId. The response confirms the addition and provides details about the newly added workspace.

```HTTP
POST /network/private HTTP/1.1
Host: api.getpostman.com
Content-Type: application/json
x-api-key: {{postman-api-key}}
Content-Length: 121

{
    "workspace": {
        "id": "1f0df51a-8658-4ee8-a2a1-d2567dfa09a9",
        "parentFolderId": {{folderId}}
    }
}

```

```JSON
{
    "addedAt": "2023-08-03T13:18:25.000Z",
    "addedBy": 12345678,
    "createdBy": 12345678,
    "createdAt": "2023-08-03T13:18:25.000Z",
    "updatedBy": 12345678,
    "updatedAt": "2023-08-03T13:18:25.000Z",
    "type": "workspace",
    "id": "1f0df51a-8658-4ee8-a2a1-d2567dfa09a9",
    "name": "Billing Team Workspace",
    "summary": "The Billing team's workspace.",
    "description": "The Billing team's workspace.",
    "href": "https://api.getpostman.com/workspaces/1f0df51a-8658-4ee8-a2a1-d2567dfa09a9",
    "parentFolderId": 1
}

```

--------------------------------

### Roles APIs

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

APIs to programmatically manage user permissions within Postman elements. This includes managing roles for specific workspaces and collections.

```APIDOC
## Workspace Roles API

### Description
With the Workspace Roles API you can manage user and user group permissions within a specific workspace. Use these endpoints to help you with onboarding or off-boarding, automating role-based workflows, and simplifying compliance and auditing processes by ensuring the right team members have access to sensitive information.

### Method
GET, POST, PUT, DELETE

### Endpoint
/workspaces/{workspace_id}/roles

## Collections Roles API

### Description
The Collections Roles API enables you to manage your collection’s roles. You can use them to view all users, teams, and groups with access to a collection or manage access permissions.

### Method
GET, POST, PUT, DELETE

### Endpoint
/collections/{collection_id}/roles
```

--------------------------------

### Convert Value to String Representation

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $string helper function converts various data types (numbers, objects, arrays, etc.) into their string representation. An optional `$prettify` argument can be used to format the output string for better readability, especially for complex data structures like objects and arrays.

```postman-helper
$string({"a": 1, "b": 2}) -> "{"a":1, "b" : 2}"
$string(5) -> "5"
$string([1,2,3]) -> ["1", "2", "3"]
```

--------------------------------

### Set Visualizer Data with Handlebars Template and Options

Source: https://learning.postman.com/docs/sending-requests/response-data/visualizer

The pm.visualizer.set() method allows you to render custom HTML visualizations within Postman. It accepts a Handlebars HTML template, optional data to bind to the template, and compilation options for Handlebars. The rendered HTML is displayed in the Visualization tab.

```javascript
pm.visualizer.set(
  "<h1>{{title}}</h1><p>{{content}}</p>",
  { title: "My Data", content: "This is some dynamic content." },
  { ignorePartials: true, }*/
);
```

--------------------------------

### Use 'accessCode' OAuth Flow

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Recommends using the OAuth 'accessCode' flow instead of the deprecated 'implicit' flow. The 'accessCode' flow is more secure as it separates the authorization and token granting steps, preventing direct exposure of access tokens.

```yaml
swagger: '2.0'
# ...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    # ...

```

--------------------------------

### Set Postman Visualizer Template and Data (JavaScript)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-visualizer

Use `pm.visualizer.set` to define an HTML template (using Handlebars syntax) and provide data to visualize API response information. The `layout` parameter is a required HTML string, `data` is a JSON object bound to the template, and `options` are for Handlebars compilation.

```javascript
pm.visualizer.set(layout:String, data:Object, options:Object):Function
```

```javascript
var template = `<p>{{res.info}}</p>`;
pm.visualizer.set(template, {
    res: pm.response.json()
});
```

--------------------------------

### FQL Each Object Iteration Function

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The '$each' function applies a provided function to each key/value pair of an object. It iterates through the object's properties, executing the callback for each.

```FQL
"Address": {
    "Street": "Hursley Park",
    "City": "Winchester",
    "Postcode": "SO21 2JN"
}
$each(Address, fn($v, $k) {$k & ": " & $v}) ->
 [
        "Street: Hursley Park",
        "City: Winchester",
        "Postcode: SO21 2JN"
 ]
```

--------------------------------

### Retrieve OIDC Provider Issuer URL (Vault CLI)

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command retrieves the issuer URL of a configured OIDC provider in HashiCorp Vault. This URL is necessary for configuring the JWT auth method's discovery URL. Save this value for later use.

```shell
vault read -field=issuer identity/oidc/provider/<oidc-provider-name>
```

--------------------------------

### Supported Global Objects in Postman Scripts

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-require

Postman provides a wide range of globally accessible JavaScript objects within its scripting environment. This includes standard JavaScript objects, DOM objects, Encoding objects, File objects, URL objects, and Web Crypto objects, enabling powerful client-side scripting capabilities.

```APIDOC
## Use Global Objects

Postman supports the following JavaScript objects globally in your scripts:

### Standard Objects
- AggregateError
- Array
- ArrayBuffer
- Atomics
- BigInt
- BigInt64Array
- BigUint64Array
- Boolean
- DataView
- Date
- Error
- EvalError
- Float32Array
- Float64Array
- Function
- Infinity property
- Int8Array
- Int16Array
- Int32Array
- Intl
- JSON
- Map
- Math
- NaN property
- Number
- Object
- Promise
- Proxy
- RangeError
- ReferenceError
- Reflect
- RegExp
- Set
- SharedArrayBuffer
- String
- Symbol
- SyntaxError
- TypeError
- Uint8Array
- Uint8ClampedArray
- Uint16Array
- Uint32Array
- URIError
- WeakMap
- WeakSet

### Document Object Model (DOM) Objects
- AbortController
- AbortSignal
- DOMException
- Event
- EventTarget

### Encoding Objects
- `atob` method
- `btoa` method
- TextEncoder
- TextEncoderStream
- TextDecoder
- TextDecoderStream

### File Objects
- Blob
- File

### JavaScript Objects
- decodeURI
- decodeURIComponent
- encodeURI
- encodeURIComponent
- escape
- isFinite
- isNaN
- parseFloat
- parseInt
- undefined
- unescape

### HTML DOM Objects
- `structuredClone` method
- `queueMicrotask` method

### Streams Objects
- ByteLengthQueuingStrategy
- CountQueuingStrategy
- CompressionStream
- DecompressionStream
- ReadableByteStreamController
- ReadableStream
- ReadableStreamBYOBReader
- ReadableStreamBYOBRequest
- ReadableStreamDefaultController
- ReadableStreamDefaultReader
- TransformStream
- TransformStreamDefaultController
- WritableStream
- WritableStreamDefaultController
- WritableStreamDefaultWriter

### URL Objects
- URL
- URLSearchParams

### Web Crypto Objects
- Crypto
- CryptoKey
- SubtleCrypto
- `crypto` property
```

--------------------------------

### Configure Newman Iteration Data and Count

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

These options allow for iterative runs of a Newman collection using data from a specified file (JSON or CSV) and controlling the number of iterations.

```bash
newman run my-collection.json -d data.csv -n 5

```

--------------------------------

### apidump Command Usage | Postman CLI

Source: https://learning.postman.com/docs/insights/reference/agent/apidump

This snippet shows the basic usage of the apidump command from the Postman Insights Agent CLI. It outlines the command structure and available flags for controlling network traffic capture.

```bash
postman-insights-agent apidump [flags]
```

--------------------------------

### Trim Whitespace from String

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $trim helper function returns a copy of a string with any leading and trailing whitespace characters (spaces, tabs, newlines) removed. It takes a single string argument.

```postman-helper
$trim(" Hello \n World ") -> "Hello World"
```

--------------------------------

### Define minItems and maxItems for array properties in OpenAPI

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Specifies the minimum and maximum number of items allowed in an array property within an OpenAPI schema. This is crucial for managing API behavior, enabling pagination, and preventing issues with an unbounded number of elements.

```yaml
openapi: '3.0.3'
# ...
components:
  schemas:
    anObject:
      properties:
        aList:
          type: array
          minItems: 1
          maxItems: 100
          items:
            type: object

```

--------------------------------

### Pad String with Characters (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $pad() function adjusts a string's length by adding specified characters to either the beginning or end. This is useful for creating fixed-width fields or aligning text.

```FQL
$pad(customer_info."customer field", 15, "#")
```

--------------------------------

### Operation Level OpenID Connect Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures specific operations using OpenID Connect authentication use HTTPS.

```APIDOC
## Operation Level OpenID Connect Security

### Description
Configures specific API operations to use OpenID Connect authentication securely over HTTPS.

### Method
POST

### Endpoint
/pets

### Parameters
None

### Request Example
```json
{
  "name": "Buddy",
  "tag": "dog"
}
```

### Response
#### Success Response (200)
- **Example** (object) - Details of the added pet.

#### Response Example
```json
{
  "id": 10,
  "name": "Buddy",
  "tag": "dog"
}
```

#### Resolution Example
```yaml
components:
  securitySchemes:
    OpenIdScheme:
      type: openIdConnect
      openIdConnectUrl: https://example.com/connect
paths:
  '/pets':
    post:
      operationId: addPet
      servers:
      - url: https://example.com/
        description: API server
      security:
      - OpenIdScheme: []
```
```

--------------------------------

### Split String by Separator (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $split() function divides a string into an array of substrings based on a specified separator. It can also optionally limit the number of splits performed. Regular expressions can be used as separators.

```FQL
$split(payments[1].description, " ", 2)
```

```FQL
$split(payments[3].description, /\s+/)
```

--------------------------------

### Define MinItems and MaxItems for Arrays (Swagger/OpenAPI)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Requires that array-type properties in schema objects define both 'minItems' and 'maxItems'. This prevents issues with handling an undefined number of elements and helps establish clear boundaries for lists.

```yaml
swagger: '2.0'
# ...
definitions:
  anObject:
    properties:
      aList:
        type: array
        minItems: 1
        maxItems: 100
        items:
          type: object

```

--------------------------------

### Run Newman Collection with JSON Data File

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

This command executes a Newman collection using data from a specified JSON file. The `-d` option indicates the data file, enabling parameterized tests where each iteration can consume different data points defined in the JSON.

```bash
newman run my-collection.json -d data-file.json
```

--------------------------------

### Reduce Array to a Value

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $reduce helper function iterates over an array, applying a function to accumulate a single resulting value. It takes the array, a reducer function (which receives the accumulator and current value), and an optional initial value. The reducer function's return value becomes the accumulator for the next iteration.

```postman-helper
$reduce([1,2,3,4], fn($prev, $cur) { $prev*$cur}) ) -> 24
```

--------------------------------

### Operation Level OAuth Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures specific operations using OAuth authentication use HTTPS.

```APIDOC
## Operation Level OAuth Security

### Description
Configures specific API operations to use OAuth authentication securely over HTTPS.

### Method
POST

### Endpoint
/pets

### Parameters
None

### Request Example
```json
{
  "name": "Buddy",
  "tag": "dog"
}
```

### Response
#### Success Response (200)
- **Example** (object) - Details of the added pet.

#### Response Example
```json
{
  "id": 10,
  "name": "Buddy",
  "tag": "dog"
}
```

#### Resolution Example
```yaml
components:
  securitySchemes:
    OAuth2:
      type: oauth2
      flows:
        implicit:
          authorizationUrl: https://example.com/api/oauth/authorize
          scopes:
            write: modify pets in your account
            read: read your pets
paths:
  '/pets':
    post:
      operationId: addPet
      servers:
      - url: https://my.api.example.com/
        description: API server
      security:
      - OAuth2:
          - write
```
```

--------------------------------

### Split String by Pattern

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $split helper function breaks a string into an array of substrings based on a delimiter pattern (string or regular expression). An optional limit can be provided to control the maximum number of splits. This is useful for parsing delimited data.

```postman-helper
$split("so many words", " ") -> [ "so", "many", "words" ]
$split("so many words", " ", 2) -> [ "so", "many" ]
$split("too much, punctuation. hard; to read", /[ ,.;]+/) -> ["too", "much", "punctuation", "hard", "to", "read"]
```

--------------------------------

### Send Request with Full Configuration in Postman Script

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-send-request

Shows how to send a POST request with custom headers and a raw JSON body using `pm.sendRequest`. It utilizes a callback function to process the response or any errors, allowing for more complex asynchronous operations.

```javascript
const postRequest = {
  url: 'https://postman-echo.com/post',
  method: 'POST',
  header: {
    'Content-Type': 'application/json',
    'X-Foo': 'bar'
  },
  body: {
    mode: 'raw',
    raw: JSON.stringify({ key: 'this is json' })
  }
};
pm.sendRequest(postRequest, (error, response) => {
  console.log(error ? error : response.json());
});
```

--------------------------------

### Date and Time Conversion: Milliseconds to Specific Format

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Details the conversion of a specific date string into Unix epoch milliseconds using $toMillis() and converting Unix epoch milliseconds back into a formatted date string using $fromMillis().

```FQL
$toMillis("10/12/2018 11:39 PM", "[M]/[D]/[Y] [h]:[m] [P]")
```

```FQL
$fromMillis(1539387540000, "[yyyy]-[MM]-[dd] [H]:[m]:[s] [z]")
```

--------------------------------

### Add Summary to OpenAPI Operations

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Requires that each operation object in an OpenAPI definition includes a 'summary' field. This provides a concise description of the operation's purpose, offering essential context beyond the HTTP method and path.

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    get:
      summary: A GET operation summary
```

--------------------------------

### Convert Milliseconds to Date String with $fromMillis

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Converts milliseconds since the epoch to a formatted date string. An optional picture string can be provided for custom formatting according to Unicode standards. If no picture is provided, it defaults to ISO format.

```Postman Script
console.log($fromMillis(1521801216617, "dd/M/yyyy")); // Output: "23/3/2018"
console.log($fromMillis(1522616700000, "E EEEE")); // Output: "7 Sunday"
```

--------------------------------

### Generate Node.js Client Code Snippet from Request Object

Source: https://learning.postman.com/docs/developer/code-generators

This snippet demonstrates how to use the `codegen.convert` function from the `postman-code-generators` module to generate client code for a given `Request` object. It targets Node.js and includes options for indentation and request body trimming. The generated snippet is returned in a callback function.

```javascript
var codegen = require('postman-code-generators'),
  sdk = require('postman-collection'),
  request = new sdk.Request('https://www.google.com'),
  language = 'nodejs',
  variant = 'request',
  options = {
    indentCount: 3,
    indentType: 'Space',
    trimRequestBody: true,
    followRedirect: true
  };
codegen.convert(language, variant, request, options,
  function(error, snippet) {
    if (error) {
      //  handle error
    }
    //  handle snippet..
});

```

--------------------------------

### Replace String Pattern

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $replace helper function returns a new string where all occurrences of a specified pattern (string or regex) are replaced with a given replacement string. It takes the original string, the pattern to find, and the replacement string as arguments.

```postman-helper
$replace("Hello World", "World", "Everyone") -> "Hello Everyone"
$replace("the cat sat on the mat", "at", "it") -> "the cit sit on the mit"
```

--------------------------------

### Reference Variables in Postman Requests

Source: https://learning.postman.com/docs/sending-requests/variables/variables

Demonstrates how to use double curly braces to reference variables within Postman requests, including in URL parameters and request bodies. Postman automatically resolves these variables to their stored values when a request is executed.

```postman
Copy{{username}}
```

```postman
Copyhttps://postman-echo.com/get?customer_id={{cust_id}}
```

```postman
Copy{ "customer_id" : "{{cust_id}}" }
```

--------------------------------

### OpenAPI Info Object - Contact URL or Email

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Stresses the importance of providing either a contact URL or email address within the contact object to facilitate communication with API consumers.

```APIDOC
## Info Object - Contact URL or Email

### Description
Ensures the OpenAPI contact object includes at least a contact URL or email address for consumer communication.

### Method
N/A (Configuration)

### Endpoint
N/A (Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

#### Success Response (200)
N/A

#### Response Example
N/A

```yaml
swagger: '2.0'
info:
  title: An API name
  version: '1.0'
  contact:
    email: support@example.com
    url: https://example.com/support
```
```

--------------------------------

### Configure Newman Request Delays and Timeouts

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

Options to set delays between requests and specify timeout durations for the entire collection run or individual requests and scripts.

```bash
newman run my-collection.json --delay-request 500

```

```bash
newman run my-collection.json --timeout 120000

```

```bash
newman run my-collection.json --timeout-request 30000

```

```bash
newman run my-collection.json --timeout-script 10000

```

--------------------------------

### Retrieve OIDC Client ID (Vault CLI)

Source: https://learning.postman.com/docs/sending-requests/postman-vault/hashicorp-vault

This command retrieves the client ID of a previously created OIDC client application in HashiCorp Vault. The client ID is essential for configuring the OIDC provider and should be saved for later use.

```shell
vault read -field=client_id identity/oidc/client/<client-application-name>
```

--------------------------------

### Private API Network API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Programmatically manage your Private API Network, automate documentation management, integrate with CI/CD, and handle requests to add elements to the network.

```APIDOC
## Private API Network API

### Description
The Private API Network API enables you to programmatically manage your Private API Network. Use these endpoints to automate the management of your team’s internal documentation, integrate it with CI/CD, and ensure that the documentation is always up-to-date. This API also enables you to get all user requests to add elements to your Private API Network and approve or reject them.

### Method
GET, POST, PUT, DELETE

### Endpoint
/private-api-network
```

--------------------------------

### Join Array of Strings (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $join() function concatenates elements of a string array into a single string. It's useful for combining array data into a readable format.

```FQL
$join(customer_info.associated_usernames)
```

--------------------------------

### Log response body and headers in Postman scripts

Source: https://learning.postman.com/docs/monitoring-your-api/troubleshooting-monitors

These JavaScript snippets are used within Postman's pre-request or test scripts to log the entire response body and headers to the Postman Console. This helps in debugging unexpected API responses. Ensure you are within a context where `responseBody` and `responseHeaders` are available.

```javascript
console.log(JSON.stringify(responseBody, null, 2));
console.log(JSON.stringify(responseHeaders, null, 2));
```

--------------------------------

### Create Collection API

Source: https://learning.postman.com/collection-format/advanced-concepts/documentation

This endpoint allows you to create a new collection using the Postman Collection v2 schema format. It requires a collection object in the request body with 'info' and 'item' properties.

```APIDOC
## POST /collections

### Description
Creates a collection using the [Postman Collection v2 schema format](https://schema.postman.com/json/collection/v2.1.0/docs/index.html). Include a collection object in the request body that contains the following required properties:
- `info` -- An *object* that contains the following properties:
  - `name` -- A *string* value that contains the collection's name.
  - `schema` -- A string that contains a URL to the collection's schema. For example, the `https://schema.getpostman.com/collection/v1` URL.
- `item` -- An *object* that contains the HTTP request and response information.
  - `request` --  An *object* that contains the collection's request information. For a complete list of values, refer to the `definitions.request` entry in the [collection.json schema file](https://schema.postman.com/json/collection/v2.1.0/collection.json). If you pass an empty object for this value, the system defaults to an untitled GET request.

### Method
POST

### Endpoint
`https://api.getpostman.com/collections`

### Parameters
#### Headers
- **Content-Type** (string) - Required - `Application/JSON`

#### Request Body
- **collection** (object) - Required - The collection object to create.
  - **info** (object) - Required - Contains collection metadata.
    - **name** (string) - Required - The name of the collection.
    - **schema** (string) - Required - The URL of the collection schema.
  - **item** (array) - Required - An array of items within the collection.
    - Each item can be a request object or a folder object.
    - Example item with request: `{ "request": "https://postman-echo.com/get" }`

### Request Example
```json
{
    "collection": {
        "info": {
            "name": "Sample Collection",
            "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
        },
        "item": [
            {
                "request": "https://postman-echo.com/get"
            }
        ]
    }
}
```

### Response
#### Success Response (200)
- **collection** (object) - The created collection object.

#### Response Example
```json
{
    "collection": {
        "info": {
            "name": "Sample Collection",
            "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
        },
        "item": [
            {
                "request": "https://postman-echo.com/get"
            }
        ],
        "id": "a1b2c3d4-e5f6-7890-1234-567890abcdef"
    }
}
```
```

--------------------------------

### Mock Server Response with Dynamic Username (JSON)

Source: https://learning.postman.com/docs/design-apis/mock-apis/create-dynamic-responses

This JSON output represents the response from a Postman mock server after receiving a request with a specific body. It shows the 'username' field populated with the value from the request body, demonstrating the functionality of the `$body` template helper.

```json
{
    "username": "s-morgenstern",
    "id": "1ad6b425-5ebf-4864-98e0-7bb44c318bac"
}
```

--------------------------------

### Spread Object Properties into Array

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $spread helper function takes an object and returns an array of objects, where each object in the array contains a single key-value pair corresponding to a property from the original object. This is useful for transforming object structures.

```postman-helper
$spread({ "a": 1, "b": 2}) -> [ { "a" : 1}, {"b": 2}]
```

--------------------------------

### Lint API Specification with Postman CLI

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

The `postman spec lint` command performs syntax validation and governance rule checks on API specifications. It accepts local file paths or Spec Hub IDs for OpenAPI 2.0, 3.0, or 3.1 formats. Options include controlling failure severity, output format (JSON, CSV, or table), and specifying a workspace for governance rules.

```bash
postman spec lint openapi.yaml --workspace-id 987654321-54321ef-4321-1ab2-1ab2-ab1234112a12
postman spec lint 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12
```

--------------------------------

### OAuth Implicit Flow Deprecation

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Recommends migrating from the deprecated OAuth implicit flow to the more secure accessCode flow to prevent token interception.

```APIDOC
## OAuth Implicit Flow Deprecation

### Description
In OAuth implicit flow, the authorization server issues access tokens directly in the authorization request's response. This makes access tokens vulnerable to interception by attackers monitoring network traffic.

### Method
N/A (Configuration issue)

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A

## Resolution
It’s recommended to use the accessCode flow. Ensure that the OAuth authentication scheme is not using the implicit flow. Refer to the OAuth 2.0 specification for recommended flows.

*Example of recommended flow configuration (conceptual):
```yaml
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://example.com/authorize
    tokenUrl: https://example.com/token
    scopes: {}
```
```

--------------------------------

### Implement OAuth 2.0 Authorization Code Flow (Replace Password Flow)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This code snippet resolves the issue of using the deprecated OAuth password grant flow. It illustrates the recommended approach using the authorizationCode flow, which is more secure as it does not rely on user credentials for token retrieval.

```yaml
Copycomponents:
  securitySchemes:
    OauthFlow:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: https://my.auth.example.com/
          tokenUrl: https://my.token.example.com/
          scopes:
            write: modify data
            read: read data



```

--------------------------------

### pm.message Object Reference

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-message

Details on the properties available within the `pm.message` object for accessing server response data in 'On message' scripts.

```APIDOC
## pm.message Properties

The `pm.message` object provides access to the data returned in the message that’s received from the server. This object is only available in **On message** scripts.

### Properties

*   **`pm.message`** (`PropertyList<{ data: any, timestamp: Date }>`) - Represents an individual message. It's a `PropertyList` object containing `data` and `timestamp`.
    *   **`data`** (`any`) - The content of the received message.
    *   **`timestamp`** (`Date`) - The time the message was received, represented as a JavaScript `Date` object.
```

--------------------------------

### Update Environment with User-Entered API Keys

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Updates an existing Postman environment named 'API Keys' with new API keys entered by the user. It prevents overriding existing values if specified and requires the environment to exist.

```javascript
function () {
  var stagingKey = document.getElementById('staging-key-input').value,
    productionKey = document.getElementById('production-key-input').value,
    preventOveride = true,
    runButtonIndex = 0,
    envData = {
      stagingKey: stagingKey,
      productionKey: productionKey
    };

  _pm('env.assign', 'API Keys', envData, preventOveride, runButtonIndex);
}
```

--------------------------------

### Migrate from OAuth 1.0 to OAuth 2.0 Authorization Code Flow

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This code demonstrates the resolution for using a deprecated OAuth 1.0 scheme. It updates the security scheme to use OAuth 2.0 with the recommended authorizationCode flow, enhancing security by avoiding deprecated methods.

```yaml
Copycomponents:
  securitySchemes:
    OauthFlow:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: https://my.auth.example.com/
          tokenUrl: https://my.token.example.com/
          scopes:
            write: modify data
            read: read data

```

--------------------------------

### Require External Library (Postman)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-require

Use the `require` method to import supported external libraries within the Postman sandbox. Assign the returned module object to a variable for usage in your scripts.

```javascript
require(moduleName:String):function
```

--------------------------------

### Add Descriptions to Schema Properties (Swagger/OpenAPI)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Validates that individual properties within schema objects in an API definition have a 'description'. This provides essential context for each property, making the API easier to understand and consume.

```yaml
swagger: '2.0'
#...
paths:
  /resources:
    get:
      responses:
        '200':
          description: a success response
          schema:
            properties:
              aProperty:
                description: a property description
                type: string

```

--------------------------------

### OpenAPI: Add Description to Operation Parameters

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet demonstrates how to add a 'description' field to parameter objects within an OpenAPI operation. This is crucial for clarifying the purpose of each parameter to API consumers.

```yaml
openapi: '3.0.3'
# ...
paths:
  /resources:
    get:
      parameters:
        - name: status
          description: Filters resources on their status
          in: query
          schema:
            type: string

```

--------------------------------

### DELETE /resources - No Content Response

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that DELETE operations for resources with a 204 status code do not define a response body.

```APIDOC
## DELETE /resources

### Description
This endpoint deletes a resource. A 204 status code indicates success with no content, and thus no response body is defined.

### Method
DELETE

### Endpoint
/resources

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (204)
- **description** (string) - A success response with no content.

#### Response Example
None
```

--------------------------------

### Postman CLI: Push Workspace (Auto Confirm)

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Executes the 'postman workspace push' command with the '--yes' flag, automatically confirming all prompts. This is useful for CI/CD pipelines where interactive input is not possible.

```bash
postman workspace push --yes
```

--------------------------------

### Configure JSON Reporter Options

Source: https://learning.postman.com/docs/postman-cli/postman-cli-reporters

This command illustrates how to configure the JSON reporter with specific options to customize the output. Here, 'omitHeaders' and 'omitResponseBodies' are used to exclude header and response body details from the JSON report.

```shell
postman collection run <collection-id> -r json --reporter-json-omitHeaders --reporter-json-omitResponseBodies
```

--------------------------------

### Setting Global Variables in Postman Scripts

Source: https://learning.postman.com/docs/sending-requests/variables/variables

Demonstrates how to set a global variable using the `pm.globals.set()` method within Postman scripts. This variable will be accessible across all requests in your workspace. Ensure you have appropriate permissions to modify global variables.

```javascript
pm.globals.set("variable_key", "variable_value");
```

--------------------------------

### Replace Entire Postman Environment

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Replaces the complete contents of an existing Postman environment with a new set of key-value pairs. This operation will fail if the specified environment does not exist.

```javascript
Copy_pm('env.replace', 'environment_name', {key: value}, runButtonIndex);
```

--------------------------------

### pm.request.headers

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-request

Provides methods to add, remove, or upsert headers for the current request within Postman scripts.

```APIDOC
## pm.request.headers.add

### Description
Adds a header with the given name and value for the current request.

### Method
`pm.request.headers.add(header: Header): function`

### Parameters
*   **header** (Object) - An object containing `key` (String) and `value` (String) for the header.

### Request Example
```javascript
pm.request.headers.add({
  key: "client-id",
  value: "abcdef"
});
```

## pm.request.headers.remove

### Description
Deletes the request header with the given name.

### Method
`pm.request.headers.remove(headerName: String): function`

### Parameters
*   **headerName** (String) - The name of the header to remove.

## pm.request.headers.upsert

### Description
Inserts the given header name and value if the header doesn’t exist. If it exists, the existing header updates with the given value.

### Method
`pm.request.headers.upsert({key: headerName: String, value: headerValue: String}): function`

### Parameters
*   **header** (Object) - An object containing `key` (String) and `value` (String) for the header.

```

--------------------------------

### Basic Authentication Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that basic authentication credentials are not transmitted in plain text by recommending the use of HTTPS.

```APIDOC
## Basic Authentication Security

### Description
This section addresses the vulnerability of basic authentication credentials being sent in plain text. It emphasizes the use of HTTPS for secure data transmission.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Configuration focused)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
components:
 securitySchemes:
  BasicAuth:
   type: http
   scheme: basic
paths:
 '/pets':
  post:
   operationId: addPet
   servers:
   - url: https://example.com/
     description: Example server
   security:
   - BasicAuth: []
```

### Response
#### Success Response (200)
N/A (Configuration focused)

#### Response Example
N/A (Configuration focused)
```

--------------------------------

### Documenting Postman Package Functions with JSDoc

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/package-library

This snippet illustrates how to add JSDoc comments to a JavaScript function within a Postman package. The JSDoc comments provide a description of the function's purpose and detail its parameters, including their type and meaning. This documentation will appear when the function is called in Postman.

```javascript
/**
 * This function prints a string to the Postman Console.
 * @param {string} data - The text to print to the Postman Console.
 */
function logger (data) {
    console.log(`Logging information to the console, ${data}`)
}

module.exports = {
    logger
}

```

--------------------------------

### Embed 'Run in Postman' button in Markdown

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/creating-run-button

This code snippet generates a 'Run in Postman' button compatible with Markdown documents. It uses an image and a link structure, allowing users to fork a specified Postman collection. The `:collection_id` and `:collection_url` are placeholders for the actual collection details. This format is suitable for README files and other Markdown-based content.

```markdown
[center class="width: 128px; margin: auto;"]
[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;" role="img">](https://god.gw.postman.com/run-collection/:collection_id?action=collection%2Ffork&source=rip_markdown&:collection_url)
[/center]

```

--------------------------------

### Accessing Package Exports in Postman Scripts

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/external-package-registries

Demonstrates the correct syntax for accessing both default and named exports from external npm packages within Postman scripts. This is crucial for packages that utilize mixed export styles.

```javascript
const fooDefaultExport = pm.require("npm:foo").default

const { fooNamedExport } = pm.require("npm:foo")
```

--------------------------------

### Create Mock Server Request Body - Postman API

Source: https://learning.postman.com/docs/design-apis/mock-apis/tutorials/mock-with-api

This JSON payload is used to create a mock server via the Postman API. It specifies the name of the mock server, the collection ID to be mocked, and optionally, the environment ID.

```json
{
    "mock": {
        "name": "testAPImock",
        "collection": "{{collectionId}}",
        "environment": "{{environmentId}}" // Optional
    }
}
```

--------------------------------

### Create Custom Newman Reporter Structure

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-custom-reporters

Defines the basic structure for a custom Newman reporter Node.js module. It requires exporting a function that accepts emitter, reporterOptions, and collectionRunOptions.

```javascript
function CustomNewmanReporter (emitter, reporterOptions, collectionRunOptions) {
  // emitter is is an event emitter that triggers the following events: https://github.com/postmanlabs/newman#newmanrunevents
  // reporterOptions is an object of the reporter specific options. The usage examples below have more details.
  // collectionRunOptions is an object of all the collection run options: https://github.com/postmanlabs/newman#newmanrunoptions-object--callback-function--run-eventemitter
}
module.exports = CustomNewmanReporter

```

--------------------------------

### Operation Object - Summary No Period

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that operation summaries do not end with a period, as they are often used as titles.

```APIDOC
## Operation Object - Summary No Period

### Description
Operation summaries should not terminate with a period. Since summaries are frequently utilized as titles in documentation or UI elements, a trailing period can appear visually unappealing or grammatically incorrect.

### Method
N/A (Applies to operation object summaries)

### Endpoint
N/A (Applies to operation object summaries)

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
```yaml
swagger: '2.0'
# ...
paths:
  /resources:
    get:
      summary: A GET operation summary
      # ...
```
```

--------------------------------

### Convert String to Uppercase

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $uppercase helper function converts a given string to its uppercase representation. It takes a single string argument and returns the modified string. This is useful for standardizing text or case-sensitive operations.

```postman-helper
$uppercase("hello") -> "HELLO"
```

--------------------------------

### Log Variable Values in Postman Console

Source: https://learning.postman.com/docs/sending-requests/variables/variables

This snippet demonstrates how to log the value of a Postman variable to the Postman Console during request execution. Ensure the Postman Console is open to view the output. This functionality is useful for debugging and understanding variable states.

```javascript
console.log(pm.variables.get("variable_key"));
```

--------------------------------

### API Security: Global Schemes

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that the global server configuration for an API defines HTTPS as the default scheme, protecting all communications.

```APIDOC
## API Security: Global Schemes

### Description
This addresses the vulnerability where the global server configuration allows unencrypted HTTP connections. It recommends setting the default scheme to HTTPS to ensure all API traffic is encrypted.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Global configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

### Resolution

```yaml
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
#...
```
```

--------------------------------

### APIs API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Use the Postman API endpoints to manage your APIs and integrate with your CI/CD systems and automate the publication of new API versions. Update or change your API definition, create and publish new versions, and manage collections attached to an API.

```APIDOC
## APIs API

### Description
Manages Postman APIs, enabling integration with CI/CD systems, automation of API version publication, updating API definitions, and managing associated collections. Note: Postman API v9 APIs are deprecated.

### Method
GET, POST, PUT, DELETE

### Endpoint
/apis

### Parameters
None specified in the provided text.

### Request Example
Not specified in the provided text.

### Response
#### Success Response (200)
Details about API management operations.

#### Response Example
Not specified in the provided text.
```

--------------------------------

### Create a Private API Network Folder (HTTP)

Source: https://learning.postman.com/docs/collaborating-in-postman/private-api-network/publish-private-network-elements-with-api

This HTTP request demonstrates how to create a new folder within your Postman Private API Network. Sensitive data like API keys should be stored in the Postman Vault. The request includes the folder name and description.

```HTTP
POST /network/private HTTP/1.1
Host: api.getpostman.com
Content-Type: application/json
X-API-Key: {{postman-api-key}}
Content-Length: 94

{
    "folder": {
        "name": "Billing",
        "description": "The Billing API."
    }
}
```

--------------------------------

### Log Variable and Response Data with Postman Console

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/troubleshoot-tests

Use console.log(), console.info(), console.warn(), and console.error() to inspect variable values and response properties within Postman. This helps in understanding the state of your data during test execution. The console.clear() method can also be used to clear the console output.

```javascript
console.log(pm.collectionVariables.get("name"));
console.log(pm.response.json().name);
```

```javascript
console.log(typeof pm.response.json().id);
```

```javascript
if (pm.response.json().id) {
  console.log("id was found!");
  // do something
} else {
  console.log("no id ...");
  //do something else
}
```

--------------------------------

### apidump Command Usage

Source: https://learning.postman.com/docs/insights/reference/agent/apidump

The `apidump` command captures and stores a sequence of requests and responses to a service by observing network traffic. Use `-h` or `--help` for assistance.

```APIDOC
## apidump Command Usage

The `apidump` command captures and stores a sequence of requests and responses to a service by observing network traffic. For help, use `-h` or `--help`.

### Usage
```
postman-insights-agent apidump [flags]
```

### Flags
* `--filter string` - Match the packets going to and coming from the API service.
* `--host-allow strings` - Allow only the HTTP hosts matching the regular expressions.
* `--host-exclusions strings` - Remove the HTTP hosts matching the regular expressions.
* `--interfaces strings` - List of network interfaces to listen on. Default: All interfaces on host.
* `--path-allow strings` - Allow only the HTTP paths matching the regular expressions.
* `--path-exclusions strings` - Remove the HTTP paths matching the regular expressions.
* `--project string` - The Postman Insights project ID.
* `--rate-limit float` - Number of requests per minute to capture. Default: 1000.

### Global flags
* `--log-format string` - Set to `color`, `plain`, or `json` to control the log format.
* `--proxy string` - The domain name, IP address, or URL of an HTTP proxy server to use.

### Examples

* Capture all traffic from your collection and send it to the Insights Agent.
```
postman-insights-agent apidump --project <projectId>
```

* Filter out requests fetching files with `.png` or `.jpg` extensions.
```
postman-insights-agent apidump ... --path-exclusions '.*\.png' --path-exclusions '.*\.jpg' ...
```

* Filter out requests having host `deb.debian.org`.
```
postman-insights-agent apidump ... --host-exclusions 'deb\.debian\.org' ...
```

* Only allow requests having host `www.example.com`.
```
postman-insights-agent apidump ... --host-allow 'www\.example\.com' ...
```

* Only allow requests related to the admin endpoints.
```
postman-insights-agent apidump ... --path-allow '*/admin/*' ...
```
```

--------------------------------

### pm.execution.runRequest Method

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-execution

Use the `pm.execution.runRequest` method in a pre-request or post-response script to send HTTP requests stored in your collections. This method allows you to run a 'referenced request' from a 'root request' or collection script.

```APIDOC
## POST /runRequest (via script)

### Description
Runs a referenced HTTP request from a pre-request or post-response script within a collection run. The referenced request will execute with its own configurations, including parameters, headers, variables, and test scripts.

### Method
`pm.execution.runRequest(requestId, options)`

### Endpoint
This method is invoked within a Postman script context, not a direct HTTP endpoint.

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

#### Script Arguments
- **requestId** (string) - Required - The ID of the request to be referenced and run.
- **options** (object) - Optional - An object that can override variables referenced in the request. This object can contain a `variables` property:
  - **variables** (object) - Optional - Key-value pairs for overriding variables during the execution of the referenced request.

### Request Example
```javascript
try {
  const response = await pm.execution.runRequest(
    "12345678-12345ab-1234-1ab2-1ab2-ab1234112a12",
    {
      variables: {
        base_url: "https://example.com",
        vip: "123"
      }
    }
  );

  console.log("Response received from collection request with status:", response.code, response.json());
}
catch (error) {
  console.error("Failed to send a request from the collection", error);
}
```

### Response
#### Success Response
The `runRequest` method returns a Promise that resolves with a response object upon successful execution of the referenced request. The response object contains details similar to a standard Postman response, including `code`, `json()`, `text()`, etc.

#### Response Example
```json
{
  "code": 200,
  "json": () => ({ /* parsed JSON body */ }),
  "text": () => "Response Body"
}
```

### Notes
- This method is asynchronous and returns a Promise. Use `await` to handle the response.
- `pm.execution.runRequest` is not supported with Newman or the Postman VS Code extension.
- `pm.execution.setNextRequest` and `pm.visualizer` methods will not run in the referenced request.
- If the referenced request uses `pm.execution.skipRequest` in its pre-request script, `runRequest` will return `null`.
- Variable resolution order: Global < Root Collection < Referenced Collection < Environment < Data < Local < Overrides.
```

--------------------------------

### Configure formdata with File

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Defines formdata with a file, including its key, base64 encoded value, and content type. It also supports using 'src' for file paths.

```json
{
    "key": "image",
    "value": "data:image/png;base64,R0lGODlhDAAMAKIFAF5LAP/zxAAAANyuAP/gaP///wAAAAAAACH5BAEAAAUALAAAAAAMAAwAAAMlWLPcGjDKFYi9lxKBOaGcF35DhWHamZUW0K4mAbiwWtuf0uxFAgA7",
    "disabled": false,
    "type": "String",
    "contentType": "file",
    "description": "form data image example"
  }
```

```json
{
    "key": "image",
    "description": "Some text emoji",
    "type": "file",
    "src": "/path/to/emoji.png"
  }
```

--------------------------------

### Format Number to String in Different Bases - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Converts a number to its string representation in a specified base (defaulting to base 10). This is useful for data serialization or displaying numbers in non-decimal formats.

```Postman Script
formatBase(100, 2) -> "1100100"
```

--------------------------------

### Users and User Groups API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Endpoints for managing users and user groups within a team, providing basic information about team members and their associated user groups.

```APIDOC
## Users and Groups API

### Description
Use the Users and Groups endpoints to manage user and user groups. These endpoints enable you to get basic information about your team’s users or your team’s user groups.

### Method
GET, POST, PUT, DELETE

### Endpoint
/users, /groups
```

--------------------------------

### Basic Request Object Structure

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Demonstrates the fundamental structure of a Postman request object, including URL, method, headers, and body.

```APIDOC
## POST /post

### Description
This is a sample POST request to demonstrate the request object structure.

### Method
POST

### Endpoint
https://postman-echo.com/post

### Parameters
#### Request Body
- **some-variable** (string) - Required - The value for the variable.

### Request Example
```json
{
  "description": "This is a sample POST request",
  "url": "https://postman-echo.com/post",
  "method": "POST",
  "header": [
    {
      "key": "Content-Type",
      "value": "Application/JSON"
    },
    {
      "key": "host",
      "value": "postman-echo.com"
    }
  ],
  "body": {
    "mode": "urlencoded",
    "urlencoded": [
      {
        "key": "some-variable",
        "value": "Something awesome!"
      }
    ]
  }
}
```

### Response
#### Success Response (200)
- **json** (object) - The JSON response from the server.
- **headers** (object) - The headers received in the response.
- **url** (string) - The URL that was requested.

#### Response Example
```json
{
  "args": {},
  "data": "",
  "files": {},
  "form": {
    "some-variable": "Something awesome!"
  },
  "headers": {
    "Accept": "*/*",
    "Content-Type": "application/x-www-form-urlencoded",
    "Host": "postman-echo.com",
    "User-Agent": "PostmanRuntime/7.33.0",
    "X-Amzn-Trace-Id": "Root=1-65e3a3c1-787711f54870692a53893102"
  },
  "json": null,
  "url": "https://postman-echo.com/post"
}
```
```

--------------------------------

### File Upload Configuration

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Specifies how to upload a file directly as the request body.

```APIDOC
## File Upload Configuration

### Description
Allows specifying a file directly as the request body.

### Method
POST/PUT (Implied for requests with file body)

### Endpoint
N/A (Configured within the request body)

### Parameters
#### Request Body
- **file** (object) - Required - Contains file upload configuration.
  - **src** (string) - Required - Path to the file to be uploaded.

### Request Example
```json
{
  "file": {
    "src": "/path/to/emoji.png"
  }
}
```
```

--------------------------------

### OpenAPI Info Object - Contact Information

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Details the necessity of a contact object within the info object, providing consumers with a designated point of contact for the API.

```APIDOC
## Info Object - Contact Information

### Description
Mandates the inclusion of a contact object in the OpenAPI info object to supply contact details for API consumers.

### Method
N/A (Configuration)

### Endpoint
N/A (Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

#### Success Response (200)
N/A

#### Response Example
N/A

```yaml
swagger: '2.0'
info:
  title: An API name
  version: '1.0'
  contact:
    email: support@example.com
    url: https://example.com/support
```
```

--------------------------------

### Run Postman Monitors

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Trigger Postman monitor runs from your CI/CD pipeline or execute organization's APIs from your internal network. This command is used to initiate scheduled collection runs configured in Postman.

```bash
postman monitor run

postman runner start
```

--------------------------------

### Use Dynamic Variables in Postman Scripts

Source: https://learning.postman.com/docs/sending-requests/variables/variables

Shows how to utilize dynamic variables within Postman scripts for generating random or time-based data. The `pm.variables.replaceIn()` method is used to substitute dynamic variable placeholders with their generated values.

```javascript
Copypm.variables.replaceIn('{{$randomFirstName}}')
```

--------------------------------

### Exporting JavaScript Functions and Objects in Postman Packages

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/package-library

This snippet demonstrates how to define a JavaScript function and export it from a Postman package using `module.exports`. The exported name must match the function declaration. This allows the function to be called from other scripts within Postman.

```javascript
function functionName {
    return result
}

module.exports = {
    functionName
}

```

--------------------------------

### Configure Request Body as File

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Specifies a file to be used directly as the request body using its source path.

```json
{
  "file": {
    "src": "/path/to/emoji.png"
  }
}
```

--------------------------------

### API Security: API Key Authentication

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Secures API key authentication by preventing API keys from being sent in plain text over unencrypted networks.

```APIDOC
## API Security: API Key Authentication

### Description
This section addresses the security risk of API keys being transmitted in plain text. It emphasizes the use of HTTPS to encrypt API key transmissions.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Global and Operation specific)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

### Resolution

```yaml
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
securityDefinitions:
  apiKeyAuth:
    type: apiKey
    name: api_key
    in: header
security:
  - apiKeyAuth: []
```

**Note:** For specific operations, ensure the `schemes` array within the operation definition also includes `https`.
```

--------------------------------

### Setting Local Variables Programmatically in Postman

Source: https://learning.postman.com/docs/sending-requests/variables/variables

This snippet demonstrates how to set a local variable programmatically within a Postman pre-request script. This is useful for dynamically setting variable values that are then used in the request. The variable will appear as 'Resolved via script' in the variables pane if it's also referenced in the request.

```javascript
pm.variables.set("variable_name", "variable_value");
```

--------------------------------

### Postman Collection JSON for File Upload

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-file-uploads

This JSON defines a Postman collection with a single POST request designed to upload a file named `sample-file.txt` as form data. It includes test scripts to verify the upload status and content.

```json
// the filename is sample-file.txt
{
	"info": {
		"_postman_id": "9dbfcf22-fdf4-f328-e440-95dbd8e4cfbb",
		"name": "file-upload",
		"description": "A set of `POST` requests to upload files as form data fields",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
	},
	"item": [
		{
			"name": "Form data upload",
			"event": [
				{
					"listen": "test",
					"script": {
						"exec": [
							"const uploadedFile = pm.response.json()?.files['sample-file.txt']";
							"",
							"pm.test(\"Status code is 200\", () => pm.response.to.have.status(200))";
							"pm.test('File was uploaded correctly', () => pm.expect(uploadedFile).to.match(/^data:application\/octet-stream;base64/))"
						],
						"type": "text/javascript",
						"packages": {}
					}
				}
			],
			"request": {
				"method": "POST",
				"header": [],
				"body": {
					"mode": "formdata",
					"formdata": [
						{
							"key": "file",
							"type": "file",
							"src": "sample-file.txt"
						}
					]
				},
				"url": {
					"raw": "https://postman-echo.com/post",
					"protocol": "https",
					"host": [
						"postman-echo",
						"com"
					],
					"path": [
						"post"
					]
				},
				"description": "Uploads a file as a form data field to `https://postman-echo.com/post` using a `POST` request."
			},
			"response": []
		}
	]
}

```

--------------------------------

### Define Global 'produces' Field with Items

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures the global 'produces' field in the OpenAPI schema contains at least one valid MIME type. An empty array would allow the API to return any data type by default, posing a security risk.

```yaml
swagger: '2.0'
paths: {}
produces:
  - application/json
...

```

--------------------------------

### Request Body Configuration

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Configure request bodies with different modes: raw, urlencoded, formdata, file, and graphql. Each mode has specific fields for data representation.

```APIDOC
## Request Body Configuration

### Description
Postman supports multiple request body types, allowing flexibility in how you send data to your API.

### Supported Request Body Modes
- `raw`
- `urlencoded`
- `formdata`
- `file`
- `graphql`

### Request Body Fields
- **mode** (string) - Required. Specifies the type of request body (`raw`, `urlencoded`, `formdata`, `file`, or `graphql`).
- **raw** (string) - Used when `mode` is `raw`. Contains the serialized payload (e.g., JSON, XML, HTML, plain text).
- **urlencoded** (object) - Used when `mode` is `urlencoded`. Contains key-value pairs for URL-encoded data.
- **formdata** (array) - Used when `mode` is `formdata`. Represents multipart/formdata, supporting text and file uploads.
- **file** (object) - Used when `mode` is `file`. Specifies a file to be sent as the request body.
- **graphql** (object) - Used when `mode` is `graphql`. Represents a GraphQL schema.
- **options** (object) - Optional. Provides extra constraints or data for the request body.
- **disabled** (boolean) - Optional. If `true`, prevents the request body from being sent.

### Example Request Body (Raw JSON)
```json
{
  "mode": "raw",
  "raw": "{\"message\": \"Hello, World!\"}"
}
```

### Example Request Body (URL Encoded)
```json
{
  "mode": "urlencoded",
  "urlencoded": [
    {
      "key": "name",
      "value": "John Doe",
      "disabled": false,
      "description": "User's full name"
    }
  ]
}
```

### Mode Details
- **raw**: Suitable for sending JSON, XML, HTML, or plain text payloads directly.
- **urlencoded**: Use for sending data as `application/x-www-form-urlencoded`.
- **formdata**: Ideal for sending data that includes files, using `multipart/formdata`.
```

--------------------------------

### Run Newman Collection with Bail Option

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

This command runs a Newman collection and enables the `--bail` option, which stops the collection run immediately if any test script fails. This is useful for CI/CD pipelines where early failure detection is critical.

```bash
newman run my-collection.json -e dev-environment.json --bail
```

--------------------------------

### Extract Minutes from Timestamp with $minutes

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Extracts the minutes component from a given timestamp and returns it as a number. The input can be a string or a number.

```Postman Script
console.log($minutes("2023-02-08T07:56:14.747+00:00")); // Output: 56
```

--------------------------------

### Postman CLI Configuration

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Defines the structure of the `.postman/config.json` file used to configure Postman CLI workspace operations. It specifies the schema version, workspace ID, and paths to collection and environment files.

```json
{
  "schemaVersion": "1",
  "workspace": {
    "id": "your-workspace-id"
  },
  "entities": {
    "collections": ["./collections/collection-name.postman_collection.json"],
    "environments": ["./environments/environment-name.postman_environment.json"]
  }
}
```

--------------------------------

### Add an API to a folder

Source: https://learning.postman.com/docs/collaborating-in-postman/private-api-network/publish-private-network-elements-with-api

Adds an API to your Private API Network folder. The API in the Private API Network is a link to the original element and must have a published version.

```APIDOC
## POST /network/private

### Description
Adds an existing API as an element to a specified folder in your Private API Network. The API must have a published version.

### Method
POST

### Endpoint
`https://api.getpostman-beta.com/network/private`

### Parameters
#### Request Body
- **api** (object) - Required - An object containing API details.
  - **id** (string) - Required - The unique identifier of the API to add.
  - **parentFolderId** (integer) - Required - The ID of the folder where the API will be added. This is typically obtained from the `id` returned when creating a folder.

### Request Example
```json
{
    "api": {
        "id": "5360b75f-447e-467c-9299-12fd6c92450d",
        "parentFolderId": {{folderId}}
    }
}
```

### Response
#### Success Response (200)
- **addedAt** (string) - Timestamp when the element was added.
- **addedBy** (integer) - User ID who added the element.
- **createdBy** (integer) - User ID who created the original element.
- **createdAt** (string) - Timestamp of the original element's creation.
- **updatedBy** (integer) - User ID who last updated the original element.
- **updatedAt** (string) - Timestamp of the original element's last update.
- **type** (string) - The type of element, which is 'api'.
- **id** (string) - The unique identifier of the API.
- **name** (string) - The name of the API.
- **summary** (string) - The summary of the API.
- **description** (string) - The description of the API (can be null).
- **href** (string) - URL to the API resource.
- **parentFolderId** (integer) - The ID of the parent folder.

#### Response Example
```json
{
    "addedAt": "2023-08-03T13:18:25.000Z",
    "addedBy": 12345678,
    "createdBy": 12345678,
    "createdAt": "2023-08-03T13:18:25.000Z",
    "updatedBy": 12345678,
    "updatedAt": "2023-08-03T13:18:25.000Z",
    "type": "api",
    "id": "5360b75f-447e-467c-9299-12fd6c92450d",
    "name": "Billing API",
    "summary": "The payments and account services API.",
    "description": null,
    "href": "https://api.getpostman.com/apis/5360b75f-447e-467c-9299-12fd6c92450d",
    "parentFolderId": 1
}
```
```

--------------------------------

### Lint API Definition using Postman CLI

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Lints an API definition file or uses an API ID to check for rule violations. Supports severity level filtering and exit code suppression. The default severity level for failures is ERROR.

```bash
postman api lint my-definition-file.json
postman api lint 12345678-12345ab-1234-1ab2-1ab2-ab1234112a12
```

--------------------------------

### Info Object Reference Table

Source: https://learning.postman.com/collection-format/reference/info

A table outlining the fields within the 'info' object of a Postman collection, including their type, whether they are required, and a description.

```APIDOC
## Info Object Reference Table

| Field Name | Type  | Required | Description  
---|---|---|---
name | `string` | `true` | A collection's human-friendly name is defined by this field. Set this field to a value that lets you to identify this collection, such as highlighting its usage or content.  
_postman_id | `string` | `false` | The Postman unique identifier for this collection.  
description | #description | `false` | The description of this collection.  
version | #description | `false` | The version info of this collection.  
schema | `string` | `true` | Holds a link to the Postman schema that's used to validate this collection. For example, `https://schema.postman.com/collection/json/v2.1.0/draft-07/collection.json`.
```

--------------------------------

### Setting Vault Secrets in Postman Scripts

Source: https://learning.postman.com/docs/sending-requests/variables/variables

Demonstrates how to securely set a vault secret using `await pm.vault.set()` in Postman scripts. The `await` operator is mandatory for vault operations. Ensure vault access is enabled in your Postman settings.

```javascript
await pm.vault.set("secret_key", "secret_value");
```

--------------------------------

### Contact Information - URL

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that the API definition includes a contact URL, typically for support or more detailed information.

```APIDOC
## Contact Information - URL

### Description
An API definition should provide a contact URL, which can lead consumers to support pages, documentation, or company websites.

### Method
N/A (Applies to API definition metadata)

### Endpoint
N/A (Applies to API definition metadata)

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
```yaml
swagger: '2.0'
info:
  title: An API name
  version: '1.0'
  contact:
    url: https://example.com/support
```
```

--------------------------------

### Enable Segregated Environments for Multiple Buttons

Source: https://learning.postman.com/docs/publishing-your-api/run-in-postman/customize-run-button

Enables the 'segregateEnvironments' property to allow each 'Run in Postman' button on a page to manage its own distinct environment. This requires using 'runButtonIndex' to reference specific buttons.

```javascript
Copy_pm('_property.set', 'segregateEnvironments', true);
```

--------------------------------

### Excessive Data Exposure - API Key

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Addresses the vulnerability where API keys are sent in plain text.

```APIDOC
## API Key Security

### Description
Ensures that API keys are transmitted securely, typically in headers, using HTTPS.

### Method
N/A (Configuration based)

### Endpoint
N/A (Global or specific server configuration)

### Parameters
None

### Request Example
N/A

### Response
N/A

#### Resolution Example
```yaml
servers:
  - url: https://my.api.example.com/
    description: API server
components:
  securitySchemes:
    AuthKeyAuth:
      type: apiKey
      name: api-key
      in: header
security:
  - AuthKeyAuth: []
```
```

--------------------------------

### Update to OpenID Connect Security Scheme

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet shows how to update an OpenAPI definition to use the OpenID Connect security scheme. It replaces deprecated schemes with a modern, secure alternative.

```yaml
Copycomponents:
  securitySchemes:
    OpenIdScheme:
      type: openIdConnect
      openIdConnectUrl: https://example.com/connect
#...
security:
- OpenIdScheme: []

```

--------------------------------

### Convert String to Uppercase (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $uppercase() function converts all characters in a given string to their uppercase equivalents. This is commonly used for standardizing text data or for case-insensitive comparisons.

```FQL
$uppercase(payments[0].description)
```

--------------------------------

### URL Component Encoding and Decoding

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Covers the functions $encodeUrlComponent() for encoding specific characters in a URL component and $decodeUrlComponent() for reversing the process.

```FQL
$encodeUrlComponent("?city=melbourne")
```

```FQL
$decodeUrlComponent("%3Fcity%3Dmelbourne")
```

--------------------------------

### Control Newman File Reading and Output

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-options

Options to control file reading security and to export collection, environment, or global variables after a run.

```bash
newman run my-collection.json --no-insecure-file-read

```

```bash
newman run my-collection.json --export-environment ./env.json

```

```bash
newman run my-collection.json --export-collection ./collection.json

```

--------------------------------

### Trim Whitespace and Special Characters (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $trim() function cleans up strings by removing leading/trailing whitespace, converting newline/tab characters to spaces, and reducing multiple spaces to single spaces. It standardizes string formats for easier processing.

```FQL
$trim(customer_info.unformatted_customer_field)
```

--------------------------------

### POST Method - Request Body

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Requires that POST operations include a request body, as they typically involve sending data to the server.

```APIDOC
## POST Method - Request Body

### Description
POST operation objects should include a request body. While technically permissible to have POST requests without a body, it often indicates a potential design issue or misunderstanding of the HTTP POST method's typical usage.

### Method
POST

### Endpoint
Example: `/resources`

### Parameters
N/A

### Request Example
```yaml
# ...
paths:
  /resources:
    post:
      parameters:
        - in: body
          name: body
          schema:
            type: object
            # ... schema definition ...
      # ...
```

### Response
#### Success Response (200 or 201)
Depends on the operation.

#### Response Example
```json
{
  "message": "Resource created successfully"
}
```
```

--------------------------------

### Postman Description Object Structure

Source: https://learning.postman.com/collection-format/advanced-concepts/documentation

Defines the structure of a description object in Postman collections. It can contain content, specify its MIME type, and optionally include a version.

```json
{
  "description": {
    "content": "<p>The description you want to provide.</p> ",
    "type": "text/html",
    "version": "A description can have versions associated with it. Use this field to specify a version for your description."
  }
}
```

--------------------------------

### Postman Monitor Run Results JSON Schema

Source: https://learning.postman.com/docs/integrations/available-integrations/microsoft-power-automate

Defines the structure for reporting Postman monitor run results. It includes details about the collection, environment, and various performance metrics like test outcomes and latency. This schema is essential for applications that need to ingest or submit monitoring data.

```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "definitions": {},
  "id": "http://example.com/example.json",
  "properties": {
    "collection_name": {
      "id": "/properties/collection_name",
      "type": "string"
    },
    "collection_uid": {
      "id": "/properties/collection_uid",
      "type": "string"
    },
    "environment_name": {
      "id": "/properties/environment_name",
      "type": "string"
    },
    "environment_uid": {
      "id": "/properties/environment_uid",
      "type": "string"
    },
    "metrics": {
      "id": "/properties/metrics",
      "properties": {
        "errors": {
          "id": "/properties/metrics/properties/errors",
          "type": "integer"
        },
        "failedTests": {
          "id": "/properties/metrics/properties/failedTests",
          "type": "integer"
        },
        "passedTests": {
          "id": "/properties/metrics/properties/passedTests",
          "type": "integer"
        },
        "requestCount": {
          "id": "/properties/metrics/properties/requestCount",
          "type": "integer"
        },
        "totalLatency": {
          "id": "/properties/metrics/properties/totalLatency",
          "type": "integer"
        },
        "warnings": {
          "id": "/properties/metrics/properties/warnings",
          "type": "integer"
        }
      },
      "type": "object"
    },
    "monitor_name": {
      "id": "/properties/monitor_name",
      "type": "string"
    },
    "monitor_uid": {
      "id": "/properties/monitor_uid",
      "type": "string"
    },
    "user_id": {
      "id": "/properties/user_id",
      "type": "string"
    },
    "user_name": {
      "id": "/properties/user_name",
      "type": "string"
    }
  },
  "type": "object"
}
```

--------------------------------

### API Key Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Mitigates the risk of API keys being exposed by ensuring they are transmitted over HTTPS connections.

```APIDOC
## API Key Security

### Description
This section focuses on securing API keys by ensuring they are transmitted over encrypted channels (HTTPS).

### Method
N/A (Configuration focused)

### Endpoint
N/A (Configuration focused)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
paths:
  '/pets':
    post:
      servers:
      - url: https://example.com/
        description: Example server
components:
  securitySchemes:
    AuthKeyAuth:
      type: apiKey
      name: api-key
      in: header
security:
  - AuthKeyAuth: []
```

### Response
#### Success Response (200)
N/A (Configuration focused)

#### Response Example
N/A (Configuration focused)
```

--------------------------------

### Faker Dynamic Variables for Names

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/variables-list

This snippet presents Faker dynamic variables for generating various components of a person's name. It includes variables for first names, last names, full names, and common name prefixes and suffixes, useful for creating realistic user data.

```Postman Variables
$randomFirstName
$randomLastName
$randomFullName
$randomNamePrefix
$randomNameSuffix
```

--------------------------------

### Postman CLI: Run Collection

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

Executes a Postman collection using the 'postman collection run' command. This command sends the run results to the Postman cloud. The collection can be specified by its file path or Collection ID.

```bash
postman collection run <collection-path-or-id>
```

--------------------------------

### Setting Local Variables in Postman Scripts

Source: https://learning.postman.com/docs/sending-requests/variables/variables

Explains how to set a local variable using `pm.variables.set()` in Postman scripts. Local variables are scoped to the execution context of the script and are not persisted or shared.

```javascript
pm.variables.set("variable_key", "variable_value");
```

--------------------------------

### Persist Data to JSONbin.io via HTTP POST

Source: https://learning.postman.com/docs/postman-flows/cookbook/persist-data-outside-flow

This snippet shows how to send data to JSONbin.io using an HTTP POST request to persist it. It includes the endpoint URL and the requirement for an 'x-master-key' header for authentication.

```text
https://api.jsonbin.io/v3/b
```

--------------------------------

### Map Array Elements with a Function

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $map helper function transforms each element of an array by applying a provided function. It accepts an array and a function (which can optionally use the element's index and the original array) and returns a new array containing the transformed elements. This is ideal for data transformation tasks.

```postman-helper
$map([1,2,3,4,5], fn($e){ $e *2}) -> [2,4,6,8,10]
```

--------------------------------

### API Security: Operation Schemes

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that individual API operations are configured to use HTTPS, even if the global scheme is set to HTTP, to protect sensitive data within specific endpoints.

```APIDOC
## API Security: Operation Schemes

### Description
This section highlights the risk of specific API operations supporting unencrypted HTTP connections. It mandates the use of HTTPS for individual operations to protect data exchanged during those specific API calls.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Operation specific)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

### Resolution

```yaml
swagger: '2.0'
#...
host: 'example.com'
paths:
  '/user':
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      schemes:
          - https
      #...
```
```

--------------------------------

### Extract Substring After Pattern (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $substringAfter() function finds the first occurrence of a specified pattern in a string and returns the portion of the string that follows it. This is useful for parsing data where a specific delimiter or keyword is present.

```FQL
$substringAfter(payments[0].description, "recurring")
```

--------------------------------

### Define OAuth2 Scopes in OpenAPI 3 Security and Components

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet demonstrates how to correctly define OAuth2 scopes in both the global security field and the securitySchemes component in an OpenAPI 3 definition. This ensures that scopes used in security requirements are properly declared and understood, preventing potential security vulnerabilities related to undefined scopes.

```yaml
security:
  - OAuth2:
    - read
    - write
components:
  securitySchemes:
    OAuth2:
      type: oauth2
      flows:
        authorizationCode:
          scopes:
            read: read objects in your account
            write: write objects to your account

```

--------------------------------

### Sort Array Elements

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Sorts an array using a provided swap function to determine the order. The swap function dictates whether elements should be swapped based on a comparison.

```Postman Functions
$sort([13,2,8,6,15], fn($l, $r) { $l > $r }) -> [2,6,8,13,15]
$sort([13,2,8,6,15], fn($l, $r) { $l < $r }) -> [15,13,8,6,2]
```

--------------------------------

### Verify Response Body and Format with Postman Tests

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/test-scripts

This Postman test snippet validates several aspects of an API response, focusing on its body and format. It asserts that the response is 'ok' (typically meaning a 2xx status code), has a body (`pm.response.to.be.withBody`), and is specifically a JSON response (`pm.response.to.be.json`). This is ideal for ensuring the API returns expected data structures.

```javascript
pm.test("response must be valid and have a body", function () {
     pm.response.to.be.ok;
     pm.response.to.be.withBody;
     pm.response.to.be.json;
});
```

--------------------------------

### Implicit Grant Type

Source: https://learning.postman.com/docs/sending-requests/authorization/oauth-20

Configure Postman to use the Implicit grant type, which directly returns an access token without an authorization code step. This method is less secure but simpler for certain applications.

```APIDOC
## Implicit Grant Type

### Description
Implicit grant type returns an access token to the client without requiring the extra auth code step. This is generally less secure.

### Method
GET (typically initiated via UI)

### Endpoint
N/A (UI configuration)

### Parameters
#### Auth Details (UI)
- **Callback URL** (string) - Required - The URL registered with the API provider where the user will be redirected after authorization.
- **Auth URL** (string) - Required - The authorization server's URL to initiate the OAuth flow.
- **Client ID** (string) - Required - The identifier for your registered application.

### Request Example
(This grant type is typically configured through Postman's UI and does not have a direct request body example in this context.)

### Response
#### Success Response (Implicit Token)
- **access_token** (string) - The obtained access token.
- **token_type** (string) - The type of token (e.g., Bearer).
- **expires_in** (integer) - The token's validity period in seconds.

#### Response Example
```json
{
  "access_token": "your_access_token_here",
  "token_type": "Bearer",
  "expires_in": 3600
}
```
```

--------------------------------

### Define Custom Function with JSON Schema Options (JavaScript)

Source: https://learning.postman.com/docs/api-governance/configurable-rules/spectral

This snippet demonstrates how to define a custom function using `createRulesetFunction` with JSON Schemas for both input and options parameters. It shows the structure for validating `targetVal` and `options` passed to a custom Spectral rule. The JSON Schema defines the expected structure and types for these parameters.

```javascript
import { createRulesetFunction } from "@stoplight/spectral-core";

function myCustomFunction(targetVal, options, context) { /* ... function logic ... */ }

export default createRulesetFunction(
  {
    // JSON Schema for the targetVal parameter
    input: {
      type: "string"
    },
    // JSON Schema for the options parameter
    options: {
      type: "object",
      additionalProperties: false,
      properties: {
        values: {
          type: "array"
        }
      },
      required: ["values"],
    },
  },
  myCustomFunction
);
```

```javascript
const { createRulesetFunction } = require("@stoplight/spectral-core");

function myCustomFunction(targetVal, options, context) { /* ... function logic ... */ }

module.exports = createRulesetFunction(
  {
    // JSON Schema for the targetVal parameter
    input: {
      type: "string"
    },
    // JSON Schema for the options parameter
    options: {
      type: "object",
      additionalProperties: false,
      properties: {
        values: {
          type: "array"
        }
      },
      required: ["values"],
    },
  },
  myCustomFunction
);
```

--------------------------------

### Compare Timestamps - Date Equality - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Verifies if two timestamps represent the exact same date and time. Crucial for exact matching and record reconciliation.

```Postman Script
$dateEquals("2023-02-08", "2023-02-08") -> true
$dateEquals("2023-02-08", "2023-02-07") -> false
```

--------------------------------

### Configure Basic Authentication with HTTPS

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures basic authentication credentials are sent securely over HTTPS. This prevents credentials from being exposed in plain text over unencrypted networks, protecting against man-in-the-middle attacks. The solution involves setting the 'schemes' to 'https'.

```yaml
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
securityDefinitions:
  basicAuth:
    type: basic
security:
 - basicAuth: []

```

```yaml
swagger: '2.0'
#...
host: 'example.com'
paths:
  '/user':
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      schemes:
          - https
      security:
          - BasicAuth: []
      #...
securityDefinitions:
  BasicAuth:
    type: basic

```

--------------------------------

### OpenID Connect Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that the OpenID Connect URL uses HTTPS to prevent credentials from being transferred as plain text.

```APIDOC
## OpenID Connect Security

### Description
This section details how to secure OpenID Connect configurations by enforcing the use of HTTPS for the OpenID Connect URL.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Configuration focused)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
components:
  securitySchemes:
    OpenIdScheme:
      type: openIdConnect
      openIdConnectUrl: https://my.api.openidconnect.example.com/
```

### Response
#### Success Response (200)
N/A (Configuration focused)

#### Response Example
N/A (Configuration focused)
```

--------------------------------

### Setting Collection Variables in Postman Scripts

Source: https://learning.postman.com/docs/sending-requests/variables/variables

Illustrates how to set a collection variable using the `pm.collectionVariables.set()` method in Postman scripts. This variable is specific to the collection it's defined in. Editor access is required to set or update collection variables.

```javascript
pm.collectionVariables.set("variable_key", "variable_value");
```

--------------------------------

### Client Credentials Grant Type

Source: https://learning.postman.com/docs/sending-requests/authorization/oauth-20

Configure Postman to use the Client Credentials grant type. This is suitable for accessing data associated with the client application itself, rather than user data.

```APIDOC
## Client Credentials Grant Type

### Description
Client credentials grant type is typically not used to access user data but instead for data associated with the client application.

### Method
POST

### Endpoint
[Access Token URL]

### Parameters
#### Request Body
- **grant_type** (string) - Required - Set to `client_credentials`.
- **client_id** (string) - Required - The identifier for your registered application.
- **client_secret** (string) - Required - The secret for your registered application.

### Request Example
```json
{
  "grant_type": "client_credentials",
  "client_id": "your_client_id",
  "client_secret": "your_client_secret"
}
```

### Response
#### Success Response (200)
- **access_token** (string) - The obtained access token.
- **token_type** (string) - The type of token (e.g., Bearer).
- **expires_in** (integer) - The token's validity period in seconds.

#### Response Example
```json
{
  "access_token": "your_access_token_here",
  "token_type": "Bearer",
  "expires_in": 7200
}
```
```

--------------------------------

### JSON Schema for URL Definition

Source: https://learning.postman.com/collection-format/reference/url

This snippet defines the JSON schema for representing a URL in Postman. It allows for a URL to be represented as a simple string or a detailed object with properties for protocol, host, path, port, query, hash, and variables. The host and path properties offer flexibility by accepting either strings or arrays.

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "description": "If object, contains the complete broken-down URL for this request. If string, contains the literal request URL.",
  "$id": "#/definitions/url",
  "title": "Url",
  "oneOf": [
    {
      "type": "object",
      "properties": {
        "raw": {
          "type": "string",
          "description": "The string representation of the request URL, including the protocol, host, path, hash, query parameter(s) and path variable(s)."
        },
        "protocol": {
          "type": "string",
          "description": "The protocol associated with the request, E.g: 'http'"
        },
        "host": {
          "title": "Host",
          "description": "The host for the URL, E.g: api.yourdomain.com. Can be stored as a string or as an array of strings.",
          "oneOf": [
            {
              "type": "string"
            },
            {
              "type": "array",
              "items": {
                "type": "string"
              },
              "description": "The host, split into subdomain strings."
            }
          ]
        },
        "path": {
          "oneOf": [
            {
              "type": "string"
            },
            {
              "type": "array",
              "description": "The complete path of the current url, broken down into segments. A segment could be a string, or a path variable.",
              "items": {
                "oneOf": [
                  {
                    "type": "string"
                  },
                  {
                    "type": "object",
                    "properties": {
                      "type": {
                        "type": "string"
                      },
                      "value": {
                        "type": "string"
                      }
                    }
                  }
                ]
              }
            }
          ]
        },
        "port": {
          "type": "string",
          "description": "The port number present in this URL. An empty value implies 80/443 depending on whether the protocol field contains http/https."
        },
        "query": {
          "type": "array",
          "description": "An array of QueryParams, which is basically the query string part of the URL, parsed into separate variables",
          "items": {
            "type": "object",
            "title": "QueryParam",
            "properties": {
              "key": {
                "type": [
                  "string",
                  "null"
                ]
              },
              "value": {
                "type": [
                  "string",
                  "null"
                ]
              },
              "disabled": {
                "type": "boolean",
                "default": false,
                "description": "If set to true, the current query parameter will not be sent with the request."
              },
              "description": {
                "$ref": "#/definitions/description"
              }
            }
          }
        },
        "hash": {
          "description": "Contains the URL fragment (if any). Usually this is not transmitted over the network, but it could be useful to store this in some cases.",
          "type": "string"
        },
        "variable": {
          "type": "array",
          "description": "Postman supports path variables with the syntax '/path/:variableName/to/somewhere'. These variables are stored in this field.",
          "items": {
            "$ref": "#/definitions/variable"
          }
        }
      }
    },
    {
      "type": "string"
    }
  ]
}
```

--------------------------------

### Random Number Generation and String Concatenation

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Illustrates generating a random whole number using $random() and $round(), then concatenating it with a string to form an invoice number.

```FQL
"Invoice number " & $round($random()*1000)
```

--------------------------------

### Post monitoring results webhook

Source: https://learning.postman.com/docs/integrations/webhooks

Configure a webhook to receive real-time monitoring results. This allows you to track performance metrics, errors, and test failures automatically.

```APIDOC
## POST /webhook/monitoring_results

### Description
This endpoint receives monitoring results from Postman monitors.

### Method
POST

### Endpoint
`/webhook/monitoring_results`

### Request Body
#### Schema
```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "definitions": {},
  "id": "http://example.com/example.json",
  "properties": {
    "collection_name": {
      "id": "/properties/collection_name",
      "type": "string"
    },
    "collection_uid": {
      "id": "/properties/collection_uid",
      "type": "string"
    },
    "environment_name": {
      "id": "/properties/environment_name",
      "type": "string"
    },
    "environment_uid": {
      "id": "/properties/environment_uid",
      "type": "string"
    },
    "metrics": {
      "id": "/properties/metrics",
      "properties": {
        "errors": {
          "id": "/properties/metrics/properties/errors",
          "type": "integer"
        },
        "failedTests": {
          "id": "/properties/metrics/properties/failedTests",
          "type": "integer"
        },
        "passedTests": {
          "id": "/properties/metrics/properties/passedTests",
          "type": "integer"
        },
        "requestCount": {
          "id": "/properties/metrics/properties/requestCount",
          "type": "integer"
        },
        "totalLatency": {
          "id": "/properties/metrics/properties/totalLatency",
          "type": "integer"
        },
        "warnings": {
          "id": "/properties/metrics/properties/warnings",
          "type": "integer"
        }
      },
      "type": "object"
    },
    "monitor_name": {
      "id": "/properties/monitor_name",
      "type": "string"
    },
    "monitor_uid": {
      "id": "/properties/monitor_uid",
      "type": "string"
    },
    "user_id": {
      "id": "/properties/user_id",
      "type": "string"
    },
    "user_name": {
      "id": "/properties/user_name",
      "type": "string"
    }
  },
  "type": "object"
}
```

### Response
#### Success Response (200 OK)
Indicates that the webhook received and processed the monitoring results successfully.

#### Response Example
No specific response body is detailed for success, typically an empty 200 OK is returned.
```

--------------------------------

### Add Terms of Service URL to OpenAPI Info Object (YAML)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This code snippet shows how to add a 'termsOfService' URL to the 'info' object in an OpenAPI specification. This is often mandatory for public APIs and recommended for private ones.

```yaml
Copyswagger: '2.0'
info:
  title: An API name
  version: '1.0'
  termsOfService: https://example.com/tos

```

--------------------------------

### Convert String to Lowercase

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $lowercase helper function converts a given string to its lowercase representation. It takes a single string argument and returns the modified string. This is useful for case-insensitive comparisons or formatting.

```postman-helper
$lowercase("Hello World") -> "hello world"
```

--------------------------------

### Calculate Milliseconds Per Year using Evaluate Block

Source: https://learning.postman.com/docs/postman-flows/tutorials/beginner/calculate-years-since-milestone

This snippet shows how to use an Evaluate block to calculate the average number of milliseconds in a year, accounting for leap years. This value is crucial for converting millisecond differences into years.

```FQL
1000 * 60 * 60 * 24 * 365.25
```

--------------------------------

### Access Environment Variable in Postman Scripts

Source: https://learning.postman.com/docs/sending-requests/variables/managing-environments

Access the value of an environment variable within Postman's Pre-request or Post-response scripts using the `pm.environment.get()` method. This allows for dynamic request modification and response handling based on environment settings.

```javascript
pm.environment.get("variable_name");

```

--------------------------------

### Script Object

Source: https://learning.postman.com/collection-format/reference/script

Defines the structure of a script object, including its properties like id, type, exec, src, and name.

```APIDOC
## Script Object Schema

### Description
Represents a script snippet used for performing setup or teardown operations on a request or response. It can be defined by inline code or an external source URL.

### Properties

#### id
- **Type**: `string`
- **Required**: `false`
- **Description**: A unique, user-defined identifier for referencing the script from requests.

#### type
- **Type**: `string`
- **Required**: `false`
- **Description**: The type of the script, e.g., `text/javascript`.

#### exec
- **Type**: `array` of `string` or `string`
- **Required**: `false`
- **Description**: An array of strings, where each string is a line of code, or a single string representing the entire script. This allows for tracking changes line by line.

#### src
- **Type**: `url`
- **Required**: `false`
- **Description**: A URL pointing to an external script file. (Note: The schema uses a reference '#/definitions/url' for this.)

#### name
- **Type**: `string`
- **Required**: `false`
- **Description**: The name of the script.

### Example Request Body
```json
{
  "id": "my-script-1",
  "type": "text/javascript",
  "exec": [
    "console.log('Hello, world!');",
    "pm.test('Status code is 200', function () {
      pm.response.to.have.status(200);
    });"
  ],
  "name": "Example Script"
}
```

### Example Response Body (Success)
```json
{
  "id": "my-script-1",
  "type": "text/javascript",
  "exec": [
    "console.log('Hello, world!');",
    "pm.test('Status code is 200', function () {
      pm.response.to.have.status(200);
    });"
  ],
  "name": "Example Script"
}
```
```

--------------------------------

### Generate Alphabet List with TypeScript

Source: https://learning.postman.com/docs/postman-flows/tutorials/beginner/create-list-based-loop

This TypeScript code snippet generates a list of all lowercase letters of the alphabet. It initializes an empty array, then uses a for loop to push each character into the array by converting character codes. The resulting array is then returned.

```TypeScript
const alphabet = []

for (let i = 0; i < 26; i++) {
	alphabet.push(String.fromCharCode(97 + i))
}

alphabet
```

--------------------------------

### Lint API Specification with Postman CLI

Source: https://learning.postman.com/docs/postman-cli/postman-cli-options

The `postman api lint` command validates API specifications against governance and security rules. It accepts specifications from a Postman config file, a local file, or a UUID. A warning is issued if the API ID cannot be found to send data back to Postman.

```bash
postman api lint
```

--------------------------------

### Add Contact Object to OpenAPI Info

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures the 'info' object in an OpenAPI definition includes a 'contact' object with essential contact details like email, URL, or name. This improves discoverability and provides users with a way to reach the API owner.

```yaml
openapi: '3.0.3'
info:
  title: An API name
  version: '1.0'
  contact:
    email: support@example.com
    url: https://example.com/support
```

```yaml
openapi: '3.0.3'
info:
  title: An API name
  version: '1.0'
  contact:
    name: A contact name
```

```yaml
openapi: '3.0.3'
info:
  title: An API name
  version: '1.0'
  contact:
    email: contact@example.com
```

```yaml
openapi: '3.0.3'
info:
  title: An API name
  version: '1.0'
  contact:
    url: https://example.com/support
```

```yaml
openapi: '3.0.3'
info:
  title: An API name
  version: '1.0'
  contact:
    email: support@example.com
```

```yaml
openapi: '3.0.3'
info:
  title: An API name
  version: '1.0'
  contact:
    url: https://example.com/support
```

--------------------------------

### Append to Array or String with $append

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $append() function combines two arrays, an array and a single value, or two strings into a single array or string. It's useful for concatenating collections or text.

```FQL
$append([1,2,3], [4,5,6])
```

--------------------------------

### Compare Dates with $hasSameDate

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $hasSameDate() function compares specified date components (e.g., month, year) of two or more dates. It returns true if the specified components match, and false otherwise. It accepts dates in 'YYYY-MM-DD' format.

```FQL
$hasSameDate("2023-02-01", "2023-02-08", ["month", "year"])
```

--------------------------------

### Header Object Reference

Source: https://learning.postman.com/collection-format/reference/header

This section details the fields available for defining a header object in a Postman Collection, including key, value, disabled status, and description.

```APIDOC
## Header Object

### Description
Represents a single HTTP Header that can be included in requests within a Postman Collection.

### Fields

#### Reference Table
| Field Name | Type   | Required | Description                                                                 |
|------------|--------|----------|-----------------------------------------------------------------------------|
| `key`      | string | true     | The name of the HTTP header (e.g., `Content-Type`, `X-Custom-Header`).      |
| `value`    | string | true     | The value of the HTTP header (e.g., `application/json`, `my-value`).        |
| `disabled` | boolean| false    | If `true`, this header will not be sent with requests. Defaults to `false`. |
| `description`| string | false    | A description for the header.                                               |

### Schema
```json
{
  "type": "object",
  "title": "Header",
  "$id": "#/definitions/header",
  "description": "Represents a single HTTP Header",
  "properties": {
    "key": {
      "description": "This holds the LHS of the HTTP Header, e.g \"Content-Type\" or \"X-Custom-Header\"",
      "type": "string"
    },
    "value": {
      "type": "string",
      "description": "The value (or the RHS) of the Header is stored in this field."
    },
    "disabled": {
      "type": "boolean",
      "default": false,
      "description": "If set to true, the current header will not be sent with requests."
    },
    "description": {
      "type": "string"
    }
  },
  "required": [
    "key",
    "value"
  ]
}
```
```

--------------------------------

### Add a Collection to a Private API Network Folder (HTTP)

Source: https://learning.postman.com/docs/collaborating-in-postman/private-api-network/publish-private-network-elements-with-api

This HTTP request shows how to add an existing Postman collection to a folder in your Private API Network. It requires the collection's ID and the parent folder ID, which can be obtained from a previous folder creation request.

```HTTP
POST /network/private HTTP/1.1
Host: api.getpostman.com
Content-Type: application/json
x-api-key: {{postman-api-key}}
Content-Length: 131

{
    "collection": {
        "id": "12345678-12ece9e1-2abf-4edc-8e34-de66e74114d2",
        "parentFolderId": {{folderId}}
    }
}
```

--------------------------------

### Parse URL-Encoded Data to JSON Object

Source: https://learning.postman.com/docs/postman-flows/reference/flows-actions-overview

This snippet illustrates the conversion of a URL-encoded string into a structured JSON object. Each key in the JSON object corresponds to a parameter in the URL-encoded string, and its value is an array containing the parameter's value as a string. This is a common pattern for handling query parameters or form data.

```json
{
  "token": ["9XqPLt7mKaRjVh2NbzC4f5Yw"],
  "team_id": ["T91H6Z2LK"],
  "team_domain": ["acme"],
  "channel_id": ["C72DF1XRK9"],
  "channel_name": ["integration-testing"],
  "user_id": ["U18ABZQXPR"],
  "user_name": ["jane.doe"],
  "command": ["/flows"],
  "text": ["status"],
  "api_app_id": ["A45K9L72QM"],
  "is_enterprise_install": ["false"],
  "enterprise_id": ["E55YT9QWKV"],
  "enterprise_name": ["AcmeCorp"],
  "response_url": ["https://hooks.slack.com/commands/T91H6Z2LK/3399128457101/HgT9yW3aKpLvQ8RbFsXe5JdM"],
  "trigger_id": ["3399128462830.8451991626.a1bcde230ab982f3d451f9bce67d041d"]
}
```

--------------------------------

### Convert String to Lowercase (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $lowercase() function converts all characters in a given string to their lowercase equivalents. This is useful for normalizing text data to ensure consistent formatting.

```FQL
$lowercase(customer_info."customer field")
```

--------------------------------

### Define Global 'produces' Field

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Defines the global 'produces' field in the OpenAPI schema to specify the MIME types the API can return. This prevents the API from returning arbitrary data, enhancing security and predictability.

```yaml
swagger: '2.0'
paths: {}
consumes:
  - application/json
produces:
  - application/json

```

--------------------------------

### Add a collection to a folder

Source: https://learning.postman.com/docs/collaborating-in-postman/private-api-network/publish-private-network-elements-with-api

Adds a collection to your Private API Network folder. The collection in the Private API Network is a link to the original element.

```APIDOC
## POST /network/private

### Description
Adds an existing collection as an element to a specified folder in your Private API Network.

### Method
POST

### Endpoint
`https://api.getpostman.com/network/private`

### Parameters
#### Request Body
- **collection** (object) - Required - An object containing collection details.
  - **id** (string) - Required - The unique identifier of the collection to add.
  - **parentFolderId** (integer) - Required - The ID of the folder where the collection will be added. This is typically obtained from the `id` returned when creating a folder.

### Request Example
```json
{
    "collection": {
        "id": "12345678-12ece9e1-2abf-4edc-8e34-de66e74114d2",
        "parentFolderId": {{folderId}}
    }
}
```

### Response
#### Success Response (200)
- **addedAt** (string) - Timestamp when the element was added.
- **addedBy** (integer) - User ID who added the element.
- **createdBy** (integer) - User ID who created the original element.
- **createdAt** (string) - Timestamp of the original element's creation.
- **updatedBy** (integer) - User ID who last updated the original element.
- **updatedAt** (string) - Timestamp of the original element's last update.
- **type** (string) - The type of element, which is 'collection'.
- **id** (string) - The unique identifier of the collection.
- **name** (string) - The name of the collection.
- **summary** (string) - The summary of the collection (can be null).
- **description** (string) - The description of the collection.
- **href** (string) - URL to the collection resource.
- **parentFolderId** (integer) - The ID of the parent folder.

#### Response Example
```json
{
    "addedAt": "2023-08-03T13:18:25.000Z",
    "addedBy": 12345678,
    "createdBy": 12345678,
    "createdAt": "2023-08-03T13:18:25.000Z",
    "updatedBy": 12345678,
    "updatedAt": "2023-08-03T13:18:25.000Z",
    "type": "collection",
    "id": "12345678-12ece9e1-2abf-4edc-8e34-de66e74114d2",
    "name": "Billing API Collection",
    "summary": null,
    "description": "The Billing API collection.",
    "href": "https://api.getpostman.com/collections/12345678-12ece9e1-2abf-4edc-8e34-de66e74114d2",
    "parentFolderId": 1
}
```
```

--------------------------------

### API Security: Basic Authentication

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Protects basic authentication credentials by ensuring they are sent over an encrypted HTTPS connection, preventing interception.

```APIDOC
## API Security: Basic Authentication

### Description
This section focuses on securing basic authentication credentials, which are often sent as plain text. The recommendation is to enforce HTTPS to encrypt these credentials during transmission.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Global and Operation specific)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

### Resolution

```yaml
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
securityDefinitions:
  basicAuth:
    type: basic
security:
 - basicAuth: []
```

**Note:** For specific operations, ensure the `schemes` array within the operation definition also includes `https`.
```

--------------------------------

### Deprecated Endpoints

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Information regarding deprecated Postman API endpoints. These endpoints are unsupported, may not receive updates, and will eventually be removed. It is not recommended to use them.

```APIDOC
## Deprecated Endpoints

### Description
Deprecated Postman API endpoints reside in the DEPRECATED folder of the Postman API collection. In the Postman API OpenAPI definition, they’re marked by the `deprecated: true` property or, in some cases, removed from the definition. Deprecated endpoints are unsupported and don’t receive any updates. At a future time they will be removed and no longer be available. **It’s recommended that you don’t use deprecated endpoints.**
```

--------------------------------

### Configure OpenID Connect Security Scheme

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet shows how to configure an OpenID Connect security scheme in an OpenAPI specification. It specifies the type and the OpenID Connect URL, which should ideally use HTTPS for secure communication.

```yaml
components:
  securitySchemes:
    OpenIdScheme:
      type: openIdConnect
      openIdConnectUrl: https://my.api.openidconnect.example.com/
```

--------------------------------

### FQL Join Array Function

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The '$join' function concatenates all elements of an array into a single string, optionally using a specified separator between elements. It can handle arrays of numbers and strings.

```FQL
$join(["hello", "world"]) -> "helloworld"
$join(["hello", "world"], "-") → "hello-world"
$join([1,2,3], "..") -> "1..2..3"
```

--------------------------------

### Proxy Configuration API

Source: https://learning.postman.com/collection-format/reference/proxy

This API allows you to define custom proxy settings for your Postman requests. You can specify URL patterns to match, the proxy server's host and port, and whether to use tunneling or disable the proxy configuration.

```APIDOC
## POST /proxy/config

### Description
Configure a custom proxy into Postman for a particular URL match.

### Method
POST

### Endpoint
/proxy/config

### Parameters
#### Request Body
- **match** (string) - Optional - The URL match the proxy config is defined for.
- **host** (string) - Optional - The proxy server host.
- **port** (integer) - Optional - The proxy server port.
- **tunnel** (boolean) - Optional - The tunneling details for the proxy config.
- **disabled** (boolean) - Optional - When set to `true`, ignores this proxy configuration element.

### Request Example
```json
{
  "match": "http+https://*/*",
  "host": "proxy.example.com",
  "port": 8080,
  "tunnel": false,
  "disabled": false
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the proxy configuration was updated.

#### Response Example
```json
{
  "message": "Proxy configuration updated successfully."
}
```
```

--------------------------------

### Request Headers

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Details on how to define and use request headers within a Postman collection.

```APIDOC
## GET /get

### Description
This example demonstrates how to include custom headers in a GET request.

### Method
GET

### Endpoint
https://postman-echo.com/get

### Parameters
#### Query Parameters
- **param1** (string) - Optional - A sample query parameter.

### Request Example
```json
{
  "description": "Header example",
  "url": "https://postman-echo.com/get",
  "method": "GET",
  "header": [
    {
      "key": "Content-Type",
      "value": "application/json"
    },
    {
      "key": "Authorization",
      "value": "Bearer 12345"
    },
    {
      "key": "x-api-key",
      "value": "slknakliwpojpwsnj"
    }
  ]
}
```

### Response
#### Success Response (200)
- **headers** (object) - The headers received in the response.
- **url** (string) - The URL that was requested.

#### Response Example
```json
{
  "args": {},
  "headers": {
    "Accept": "*/*",
    "Accept-Encoding": "gzip, deflate, br",
    "Authorization": "Bearer 12345",
    "Host": "postman-echo.com",
    "Ocp-Apim-Subscription-Key": "slknakliwpojpwsnj",
    "User-Agent": "PostmanRuntime/7.33.0",
    "X-Amzn-Trace-Id": "Root=1-65e3a3c2-18d5d1f257a811554c720e8c"
  },
  "url": "https://postman-echo.com/get"
}
```
```

--------------------------------

### Postman Console Log Statements for Debugging

Source: https://learning.postman.com/docs/sending-requests/response-data/troubleshooting-api-requests

This snippet shows the various console logging methods available in Postman for debugging pre-request or post-request scripts. These logs are stored locally and help in understanding script execution flow and identifying errors. They are useful for inspecting variable values and the outcomes of asynchronous operations.

```javascript
console.log("This is an informational message.");
console.info("This is an info message.");
console.warn("This is a warning message.");
console.error("This is an error message.");
console.clear();
```

--------------------------------

### Postman Script: Replace Dynamic Variables

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/variables-list

This snippet demonstrates how to use `pm.variables.replaceIn()` in Postman scripts to insert dynamically generated data from the Faker library. It shows the syntax for replacing a variable like `$randomFirstName` with its generated value. Ensure variable names are used with double curly braces and are case-sensitive.

```javascript
pm.variables.replaceIn('{{$randomFirstName}}')
```

--------------------------------

### OpenAPI Info Object - Contact Name

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Emphasizes the value of including a contact name within the contact object to clearly identify the API's owner.

```APIDOC
## Info Object - Contact Name

### Description
Recommends adding a contact name to the OpenAPI contact object for clear API ownership identification.

### Method
N/A (Configuration)

### Endpoint
N/A (Configuration)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

#### Success Response (200)
N/A

#### Response Example
N/A

```yaml
swagger: '2.0'
info:
  title: An API name
  version: '1.0'
  contact:
    name: A contact name
```
```

--------------------------------

### Send team activity feed to custom webhooks

Source: https://learning.postman.com/docs/integrations/webhooks

Configure a webhook to receive real-time updates about team activities, such as changes to collections and team events. This helps in tracking collaboration and modifications within your workspace.

```APIDOC
## POST /webhook/team_activity

### Description
This endpoint receives team activity updates from Postman.

### Method
POST

### Endpoint
`/webhook/team_activity`

### Parameters
#### Query Parameters
- **nickname** (string) - Required - A nickname for the integration.
- **url** (string) - Required - The webhook URL to send team updates to.

### Request Body
#### Schema
```json
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "definitions": {},
  "id": "http://example.com/example.json",
  "properties": {
    "action": {
      "id": "/properties/action",
      "type": "string"
    },
    "collection_name": {
      "id": "/properties/collection_name",
      "type": "string"
    },
    "collection_uid": {
      "id": "/properties/collection_uid",
      "type": "string"
    },
    "message": {
      "id": "/properties/message",
      "type": "string"
    },
    "model": {
      "id": "/properties/model",
      "type": "string"
    },
    "model_name": {
      "id": "/properties/model_name",
      "type": "string"
    },
    "model_uid": {
      "id": "/properties/model_uid",
      "type": "string"
    },
    "user_id": {
      "id": "/properties/user_id",
      "type": "string"
    },
    "user_name": {
      "id": "/properties/user_name",
      "type": "string"
    }
  },
  "type": "object"
}
```

### Response
#### Success Response (200 OK)
Indicates that the webhook received and processed the team activity update successfully.

#### Response Example
No specific response body is detailed for success, typically an empty 200 OK is returned.
```

--------------------------------

### Configure GraphQL Request

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Defines a GraphQL request by specifying the query schema and its corresponding variables.

```json
{
    "query": "
      {
        query(username: $username){
          name
          email
        }
      }
    ",
    "variables": "{ 'username': 'johndoe' }"
  }
```

--------------------------------

### Contact Information - Email

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that the API definition includes a contact email for consumers to reach out for support or inquiries.

```APIDOC
## Contact Information - Email

### Description
An API definition should provide a contact email address so that consumers have a direct channel to communicate with the API provider.

### Method
N/A (Applies to API definition metadata)

### Endpoint
N/A (Applies to API definition metadata)

### Parameters
N/A

### Request Example
N/A

### Response
#### Success Response (200)
N/A

#### Response Example
```yaml
swagger: '2.0'
info:
  title: An API name
  version: '1.0'
  contact:
    email: contact@example.com
```
```

--------------------------------

### Set Next Request in Postman Script

Source: https://learning.postman.com/docs/collections/running-collections/building-workflows

Specifies which request Postman should execute immediately after the current one completes. This is done by providing the name or ID of the target request as an argument to the `pm.execution.setNextRequest()` function within a post-response script.

```javascript
pm.execution.setNextRequest("request_name");

```

--------------------------------

### Bearer Token Authorization in a Request

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Shows how to set up 'bearer' authorization with a token directly within a collection request definition. This is frequently used for token-based authentication.

```json
{
  "description": "Header example",
  "url": "https://postman-echo.com/get",
  "method": "GET",
  "header": [
    {
      "key": "Content-Type",
      "value": "application/json"
    },
    {
      "key": "Authorization",
      "value": "Bearer 12345"
    }
  ],
  "auth": {
    "type": "bearer",
    "bearer": [
      {
        "key": "token",
        "value": "Bearer your_authorization_token",
        "type": "String"
      }
    ]
  }
}
```

--------------------------------

### Reference Environment Variable in Request

Source: https://learning.postman.com/docs/sending-requests/variables/managing-environments

Reference an environment variable in a Postman request by enclosing its name in double curly braces. This can be done in URLs, parameters, headers, and body data. Hovering over the variable shows its current value.

```Postman
{{base_url}}
```

--------------------------------

### FQL: Append string and group/sum results by description

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Appends 'annual cost' to each description in the payments array and calculates 12 times the amount for each. Results are then grouped by the modified description. This FQL operation is useful for data aggregation and transformation.

```FQL
payments.{description & " annual cost" : amount*12}  
```

--------------------------------

### Data Type Conversion: Number to String

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

Explains how to convert a numerical value, retrieved from a JSON object's key, into a string format using the $string() function.

```FQL
$string(payments[0].amount)
```

--------------------------------

### pm.cookies.jar Methods (Specific Domain)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-cookies

The `pm.cookies.jar()` methods allow you to manage cookies for any specified domain. You must add the domain to an allowlist before accessing these methods. Note that these functions run asynchronously and require callbacks.

```APIDOC
## pm.cookies.jar Methods

Use the `pm.cookies.jar()` methods to specify a domain and access and manipulate its cookies. Add a domain to the allowlist first.

> Function calls run asynchronously. Use a callback function to ensure functions run in sequence.

### `pm.cookies.jar().set(URL:String, cookieName:String, cookieValue:String, callback(error, cookie))`

Sets a cookie with the specified name and value to a domain.

**Example:**
```javascript
pm.cookies.jar().set("example.com", "session-id", "abc123", (error, cookie) => {
    if (error) {
      console.error(`An error occurred: ${error}`);
      } else {
        console.log(`Cookie saved: ${cookie}`);
        }
});
```

### `pm.cookies.jar().set(URL:String, { name:String, value:String, httpOnly:Bool }, callback(error, cookie))`

Sets a cookie using a Cookie object.

**Example:**
```javascript
var Cookie = require('postman-collection').Cookie,
    myCookie = new Cookie({
        name: 'session-id',
        value: 'abc123e',
        httpOnly: true
    });

pm.cookies.jar().set("example.com", myCookie, (error, cookie) => {
    if (error) {
      console.error(`An error occurred: ${error}`);
      } else {
        console.log(`Cookie saved: ${cookie}`);
        }
});
```

### `pm.cookies.jar().get(URL:String, cookieName:String, callback(error, value))`

Gets the value of a cookie at the specified domain.

**Returns:**
* The value of the cookie available in the callback function.

### `pm.cookies.jar().getAll(URL:String, callback(error, cookies))`

Gets all cookies for a specified domain.

**Returns:**
* The name and value of all cookies available in the callback function.

### `pm.cookies.jar().unset(URL:String, cookieName:String, callback(error))`

Removes a specified cookie from the domain.

### `pm.cookies.jar().clear(URL:String, callback(error))`

Clears all cookies from the specified domain.

**Example:**
```javascript
pm.cookies.jar().clear("example.com", (error) => {
    pm.cookies.jar().set("example.com", "session-id", "jkl456p", (error, cookie) => {
        if (error) {
          console.error(`An error occurred: ${error}`);
        } else {
          console.log(`Cookie saved: ${cookie}`);
        }
    })
});
```
```

--------------------------------

### Iterating Message Template

Source: https://learning.postman.com/docs/postman-flows/build-flows/structure/loops/loops-pagination

This template string is used in a Postman Flow's 'Template' block to display the current page number during loop iteration. It indicates the page being processed and that the next page is being prepared.

```postman-flow-template
We are now on page {{onPage}}. Turning the page ...
```

--------------------------------

### Compare Timestamps - Before Date - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Determines if the first timestamp occurs before the second timestamp. Essential for ordering events or validating time ranges.

```Postman Script
$beforeDate("2023-02-07", "2023-02-08") -> true
$beforeDate("2023-02-08", "2023-02-08") -> false
```

--------------------------------

### Faker Dynamic Variables for Internet and IP Addresses

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/variables-list

This section details Faker dynamic variables for generating network-related data, including IP addresses (IPv4 and IPv6), MAC addresses, passwords, user agents, and protocols. These are useful for simulating network traffic or generating realistic API request payloads.

```Postman Variables
$randomIP
$randomIPV6
$randomMACAddress
$randomPassword
$randomLocale
$randomUserAgent
$randomProtocol
```

--------------------------------

### Set Environment Variable using Postman Script

Source: https://learning.postman.com/docs/sending-requests/variables/environment-variables

This script demonstrates how to set an environment variable within the active Postman environment. It uses the `pm.environment.set` method, which is accessible in both pre-request and post-response scripts. The variable key and value can be dynamically determined by your script logic. Ensure you have appropriate editor access to the environment for changes to be shared.

```javascript
pm.environment.set("variable_key", "variable_value");

```

--------------------------------

### Define Operation-Specific 'produces' Field

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Specifies the 'produces' field for a specific API operation to define the MIME types it can return. This is necessary if the global 'produces' field is not defined or if a specific operation has different output requirements.

```yaml
swagger: '2.0'
paths:
  /user/{userId}:
    get:
      produces:
        - application/json

```

--------------------------------

### Configure Complex URL Object

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Represents a URL with its various components defined as an object, including protocol, host, port, path, and query parameters.

```json
{
  "description": "This is a sample GET request",
  "url": {
    "raw": "https://postman-echo.com:443/get/user?username=johndoe&email=john@doe.com",
    "protocol": "https",
    "host": [
      "postman-echo",
      "com"
    ],
    "port": "443",
    "path": [
      "get",
      "user"
    ],
    "query": [
      {
        "key": "username",
        "value": "johndoe",
        "disabled": false,
        "description": "Username of this user"
      },
      {
        "key": "email",
        "value": "john@doe.com",
        "disabled": false,
        "description": "Email of this user"
      }
    ]
  }
}
```

--------------------------------

### Update OAuth2 Security Definitions to Access Code Flow (YAML)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This snippet demonstrates how to update the securityDefinitions in an OpenAPI specification to use the recommended 'accessCode' flow for OAuth2 authentication, replacing the deprecated 'password' flow. It includes authorization and token URLs, along with scope definitions.

```yaml
Copyswagger: '2.0'
#...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://my.auth.example.com/
    tokenUrl: https://my.token.example.com/
    scopes:
      write: modify data
      read: read data

```

--------------------------------

### Import Private npm Packages

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/packages/external-package-registries

Illustrates how to import private npm packages into Postman scripts, available for Professional and Enterprise plan users. It specifies the `pm.require` syntax for private packages, including the scope, package name, and version.

```javascript
// package imported from npm
const npmVariableName = pm.require('npm:@scope/package-name@version-number');

npmVariableName.functionName()
```

--------------------------------

### Calculate Base-2 Logarithm - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Computes the base-2 logarithm of a number. This function is fundamental in computer science for analyzing algorithms and data structures.

```Postman Script
$log2(16) -> 4
```

--------------------------------

### pm.execution.location

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-execution

Retrieves the full path of a request, including its parent folder and collection, in an array format. Also provides access to the current item's name.

```APIDOC
## pm.execution.location

### Description
The `pm.execution.location` property enables you to get a request’s complete path, including its parent folder and collection, in array format. You can use `pm.execution.location.current` to get the name of the current item.

### Properties
- **`pm.execution.location`** (Array): Returns an array representing the path (e.g., `["Collection Name", "Folder Name", "Request Name"]`).
- **`pm.execution.location.current`** (String): Returns the name of the current item being executed (request, folder, or collection).

### Usage
- Understand the current location within your API testing or collection structure.
- Implement tailored logic and actions in your scripts based on the execution context.

### Examples
1. **Get Full Path:**
   For a request named **R1** in folder **F1** in the **C1** collection, the following post-response script code returns the `["C1", "F1", "R1"]` array:
   ```javascript
   console.log(pm.execution.location);
   ```

2. **Get Current Item Name:**
   If you add the following code to the pre-request script of a folder named **F1**, it returns `F1`:
   ```javascript
   console.log(pm.execution.location.current);
   ```
```

--------------------------------

### Compare Timestamps - After Date - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Checks if the first timestamp occurs after the second timestamp. Useful for validating chronological order in data.

```Postman Script
$afterDate("2023-02-09", "2023-02-08") -> true
$afterDate("2023-02-08", "2023-02-08") -> false
```

--------------------------------

### Add an API to a Private API Network Folder (HTTP)

Source: https://learning.postman.com/docs/collaborating-in-postman/private-api-network/publish-private-network-elements-with-api

This HTTP request illustrates how to add a published API to a folder within your Postman Private API Network. The API must have a published version. The request requires the API's ID and the parent folder ID.

```HTTP
POST /network/private HTTP/1.1
Host: api.getpostman-beta.com
Content-Type: application/json
x-api-key: {{postman-api-key}}
Content-Length: 115

{
    "api": {
        "id": "5360b75f-447e-467c-9299-12fd6c92450d",
        "parentFolderId": {{folderId}}
    }
}
```

--------------------------------

### Ceiling Function

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Returns the smallest integer that is greater than or equal to the input number.

```Postman Functions
$ceil(3.4) -> 4
```

--------------------------------

### OAuth 1.0 Authentication Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Addresses the vulnerability where OAuth 1.0 authentication tokens are transmitted in plain text, potentially leading to interception.

```APIDOC
## OAuth 1.0 Authentication Security

### Description
This section addresses the security risk of OAuth 1.0 tokens being sent in plain text. It recommends using HTTPS to ensure secure transport.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Configuration focused)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
paths:
  '/pets':
    post:
      servers:
      - url: https://example.com/
        description: Example server
components:
  securitySchemes:
    OAuth1:
      type: http
      scheme: oauth
security:
  - OAuth1: []
```

### Response
#### Success Response (200)
N/A (Configuration focused)

#### Response Example
N/A (Configuration focused)
```

--------------------------------

### Calculate Power of a Number - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Raises a number to a specified exponent. This is a core mathematical operation used in many algorithms and financial calculations.

```Postman Script
$power(2, 3) -> 8
$power(3,4) -> 81
```

--------------------------------

### Define Security Scheme in OpenAPI Components

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Declares reusable security schemes within the 'components.securitySchemes' object. This allows different parts of the API to reference these schemes for authentication.

```yaml
components:
  securitySchemes:
    testAuth:
      type: http
      scheme: basic

```

```yaml
components:
  securitySchemes:
    BasicAuth:
      type: http
      scheme: basic

```

```yaml
components:
  securitySchemes:
    myAuth:
      type: http
      scheme: basic

```

--------------------------------

### Calculate Base-10 Logarithm - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Calculates the base-10 logarithm of a number. This is frequently used in fields like signal processing and information theory.

```Postman Script
$log10(16) -> 1.2041199826559248
```

--------------------------------

### Enforce HTTPS for Global API Schemes

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Addresses the vulnerability where the server globally supports unencrypted HTTP connections. By ensuring the 'schemes' array includes 'https', all API traffic is protected, preventing eavesdropping and data tampering.

```yaml
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
#...

```

--------------------------------

### No Auth

Source: https://learning.postman.com/docs/sending-requests/authorization/authorization-types

Postman does not send authorization details with a request unless an auth type is specified. Select 'No Auth' if your request does not require authorization.

```APIDOC
## No Auth

### Description
Select 'No Auth' from the 'Auth Type' dropdown if your request does not require any authorization.

### Method
N/A (Client-side configuration)

### Endpoint
N/A (Applies to individual requests, collections, or folders)

### Parameters
None
```

--------------------------------

### Configure API Key Authentication with HTTPS

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Secures API key transmission by enforcing HTTPS. This mitigates the risk of API keys being intercepted during network communication, especially on unsecured networks. The fix requires updating the 'schemes' to 'https'.

```yaml
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
securityDefinitions:
  apiKeyAuth:
    type: apiKey
    name: api_key
    in: header
security:
  - apiKeyAuth: []

```

```yaml
swagger: '2.0'
#...
host: 'example.com'
paths:
  '/user':
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      schemes:
          - https
      security:
          - apiKeyAuth: []
      #...
securityDefinitions:
  apiKeyAuth:
    type: apiKey
    name: api_key
    in: header

```

--------------------------------

### Basic Loop with Repeat Block in Postman Flows

Source: https://learning.postman.com/docs/postman-flows/build-flows/structure/loops/overview

Demonstrates a basic loop structure using the 'Repeat' block in Postman Flows. This loop iterates a specified number of times and collects the results. There is no direct way to break out of this loop.

```Postman Flows

```

--------------------------------

### Define Global OAuth2 Security in OpenAPI

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This snippet demonstrates how to define global OAuth2 security for an API in an OpenAPI 2.0 specification. It includes the security scheme definition and its application to an endpoint. This ensures that all requests to endpoints without explicit security settings will require OAuth2 authentication.

```yaml
Copyswagger: '2.0'
#...
paths:
  '/user':
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      operationId: listUser
      security:
        - OAuth2:
          - read
          - write
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    scopes:
      read: read object
      write: writes object
    authorizationUrl: https://example.com/authorize
    tokenUrl: https://example.com/token

```

--------------------------------

### Configure OAuth2 Authentication with HTTPS

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures OAuth2 access tokens are transmitted securely over HTTPS. This prevents attackers from intercepting tokens by monitoring network traffic on public Wi-Fi. The configuration involves setting the 'schemes' to 'https' at either the global or operation level.

```yaml
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://my.auth.example.com/
    tokenUrl: https://my.token.example.com/
security:
 - OAuth2: []

```

```yaml
swagger: '2.0'
#...
host: 'example.com'
paths:
  '/user':
    get:
      summary: 'Sample endpoint: Returns details about a particular user'
      schemes:
          - https
      security:
          - OAuth2: []
      #...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://my.auth.example.com/
    tokenUrl: https://my.token.example.com/

```

--------------------------------

### Cube Root

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Calculates the cube root of a given number.

```Postman Functions
$cbrt(27) -> 3
```

--------------------------------

### OpenAPI: Secure API Server URL with HTTPS for OAuth 1.0

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet illustrates how to ensure an API server URL uses HTTPS when implementing OAuth 1.0 authentication in an OpenAPI specification. It addresses the risk of authentication tokens being intercepted in plain text.

```yaml
servers:
  - url: https://my.api.example.com/
    description: API server
#...
components:
  securitySchemes:
    OAuth1:
      type: http
      scheme: oauth
#...
security:
  - OAuth1: []

```

--------------------------------

### Calculate Hyperbolic Sine - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Computes the hyperbolic sine of a number. This function appears in various areas of physics and engineering, particularly in wave mechanics.

```Postman Script
$sinh(1) -> 1.1752011936438014
```

--------------------------------

### Run Postman Collection via Docker

Source: https://learning.postman.com/docs/collections/using-newman-cli/newman-with-docker

Executes a Postman Collection stored remotely using its collection ID and an API key. The collection runs within the Newman Docker container, and the output is displayed in the terminal. This command utilizes the Newman Docker image to run specified collections.

```shell
docker run -t postman/newman run "https://api.getpostman.com/collections/<collection-id>?apikey=<your-api-key>"
```

--------------------------------

### Broken Object Level Authorization

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This section covers warnings related to broken object-level authorization, specifically when OAuth scopes are not correctly defined in security schemes.

```APIDOC
## Broken Object Level Authorization

### Scope for OAuth scheme used in security field is not defined in the securityScheme declaration

#### Description
The OAuth2 scopes used in the global security field are not defined in the security schemes field. This can allow an attacker to introduce their scopes and exploit the system.

#### Method
(Implicitly relates to OpenAPI schema definition)

#### Endpoint
N/A

#### Parameters
N/A

#### Request Body
N/A

### Request Example
```yaml
security:
  - OAuth2:
    - read
    - write
components:
  securitySchemes:
    OAuth2:
      type: oauth2
      flows:
        authorizationCode:
          scopes:
            read: read objects in your account
            write: write objects to your account
```

### Response
#### Success Response (200)
N/A

#### Response Example
N/A

---

### Scope for OAuth scheme used is not defined in the securityScheme declaration

#### Description
The OAuth2 scopes used in the security field of an operation are not defined in the security schemes field. Similar to the global scope issue, this can be exploited by attackers.

#### Method
(Implicitly relates to OpenAPI schema definition)

#### Endpoint
N/A

#### Parameters
N/A

#### Request Body
N/A

### Request Example
(Refer to the previous example, focusing on the operation-level security context)

### Response
#### Success Response (200)
N/A

#### Response Example
N/A
```

--------------------------------

### Excessive Data Exposure - OpenID Connect Authentication

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Addresses the vulnerability where OpenID Connect credentials are sent in plain text.

```APIDOC
## OpenID Connect Authentication Security

### Description
Ensures that OpenID Connect credentials are transmitted securely using HTTPS.

### Method
N/A (Configuration based)

### Endpoint
N/A (Global or specific server configuration)

### Parameters
None

### Request Example
N/A

### Response
N/A

#### Resolution Example
```yaml
components:
  securitySchemes:
    OpenIdScheme:
      type: openIdConnect
      openIdConnectUrl: https://example.com/connect
paths:
  '/pets':
    post:
      operationId: addPet
      servers:
      - url: https://example.com/
        description: API server
      security:
      - OpenIdScheme: []
```
```

--------------------------------

### Reference Vault Secret in Postman

Source: https://learning.postman.com/docs/sending-requests/postman-vault/manage-vault-secrets

Demonstrates the syntax for referencing a vault secret within Postman. This format can be used in various fields like URLs, parameters, headers, and request bodies. Ensure the secret name is correctly appended with the `vault:` prefix and enclosed in double curly braces.

```text
{{vault:postman-api-key}}
```

--------------------------------

### Add STDIO Request for Local MCP Server

Source: https://learning.postman.com/docs/postman-ai/mcp-servers/promote

This code snippet demonstrates how to add a Standard Input/Output (STDIO) request for a locally run MCP server within a Postman collection. Ensure all necessary environment variables are included.

```json
{
  "name": "My AI Service MCP Server",
  "item": [
    {
      "name": "Local MCP Server Request",
      "request": {
        "method": "POST",
        "header": [],
        "body": {
          "mode": "raw",
          "raw": "",
          "options": {
            "raw": {
              "language": "json"
            }
          }
        },
        "url": {
          "raw": "localhost:port",
          "host": [
            "localhost"
          ],
          "port": "port"
        },
        "event": [
          {
            "listen": "prerequest",
            "script": {
              "exec": [
                "// Command to run the local MCP server",
                "const command = 'npx -y @mycompany/mycompany-mcp-server';",
                "// Add necessary environment variables here if not set globally"
              ],
              "type": "text/javascript"
            }
          }
        ]
      }
    }
  ]
}
```

--------------------------------

### Logging Debugging Information in Postman Monitors

Source: https://learning.postman.com/docs/monitoring-your-api/faqs-monitors

You can use built-in console methods like `console.log()` and `console.warn()` to output custom debugging information within your Postman monitor runs. The `console.clear()` method can be used to clear the console output. Note that Postman does not log request/response bodies or headers for security and privacy reasons.

```javascript
console.log("Starting monitor run...");
// Your request logic here
console.warn("Potential issue detected in response.");
// Further logic
// console.clear(); // Uncomment to clear console before next run
```

--------------------------------

### Define OAuth2 Scopes in OpenAPI 2 Security Definitions

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This snippet demonstrates how to correctly define OAuth2 scopes within the `security` and `securityDefinitions` sections of an OpenAPI 2.0 specification. It ensures that scopes used in the global security field are properly declared, preventing potential authorization bypasses.

```yaml
swagger: '2.0'
#...
security:
  - OAuth2:
    - read
    - write
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    scopes:
      read: read object
      write: writes object
    authorizationUrl: https://example.com/authorize
    tokenUrl: https://example.com/token

```

--------------------------------

### Determine Value Type

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $type helper function returns a string indicating the data type of the provided value. It supports common types like 'string', 'number', 'object', 'array', and 'null'. This is helpful for type checking and conditional logic.

```postman-helper
$type("hello") -> "string"
$type(1) -> "number"
$type({}) -> "object"
$type([]) -> "array"
$type(null) -> "null"
```

--------------------------------

### Convert Date String to Milliseconds with $toMillis

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Converts a date string to milliseconds since the epoch. An optional picture string can be provided to specify the format of the input date string. If no picture is provided, it defaults to ISO format.

```Postman Script
console.log($toMillis("1970-01-01T00:00:00.001Z")); // Output: 1
console.log($toMillis("2018-03-27", "yyyy-MM-dd")); // Output: 1522108800000
console.log($toMillis("21 August 2017", "dd MMMM yyyy")); // Output: 1503273600000
```

--------------------------------

### Monitor API Response Latency in Postman

Source: https://learning.postman.com/docs/tests-and-scripts/run-tests/test-with-monitors

This Postman post-response script checks the response time of an API request, ensuring it is within an acceptable threshold (e.g., less than or equal to 1000 milliseconds). This helps monitor API performance and identify potential bottlenecks.

```javascript
Copypm.test("Response latency is acceptable", function () {
    // responseTime is in milliseconds
    pm.expect(pm.response.responseTime).to.be.lte(1000);
});
```

--------------------------------

### Collection Version Schema

Source: https://learning.postman.com/collection-format/reference/version

Defines the structure for versioning Postman collections, including major, minor, patch, identifier, and meta fields. It supports both object and string representations for versioning.

```APIDOC
## Collection Version Schema

### Description
This schema defines the structure for versioning Postman collections. It allows for detailed version management with major, minor, and patch increments, a human-friendly identifier, and optional metadata. The version can be represented as an object with specific fields or as a simple string.

### Method
N/A (Schema Definition)

### Endpoint
N/A (Schema Definition)

### Parameters
#### Request Body
- **major** (integer) - Required - Increment this number for backward-incompatible changes.
- **minor** (integer) - Required - Increment this number for backward-compatible changes.
- **patch** (integer) - Required - Increment this number for patch-level changes.
- **identifier** (string) - Optional - A human-friendly identifier for the version (e.g., 'beta-3'). Max length 10.
- **meta** (object) - Optional - Any additional information related to the version.

### Request Example
```json
{
  "major": 1,
  "minor": 2,
  "patch": 0,
  "identifier": "rc-1",
  "meta": {
    "release_date": "2024-07-26"
  }
}
```

### Response
#### Success Response (200)
- **version** (object or string) - The version information of the collection.

#### Response Example
```json
{
  "major": 1,
  "minor": 2,
  "patch": 0,
  "identifier": "rc-1",
  "meta": {
    "release_date": "2024-07-26"
  }
}
```

### Error Handling
- **404 Not Found**: If the requested collection version or URL is not found.
- **Invalid Schema**: If the provided version data does not conform to the schema.
```

--------------------------------

### Excessive Data Exposure - OAuth Authentication

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Addresses the vulnerability where OAuth access tokens are sent in plain text.

```APIDOC
## OAuth Authentication Security

### Description
Ensures that OAuth 2.0 authentication tokens are transmitted securely using HTTPS.

### Method
N/A (Configuration based)

### Endpoint
N/A (Global or specific server configuration)

### Parameters
None

### Request Example
N/A

### Response
N/A

#### Resolution Example
```yaml
servers:
  - url: https://my.api.example.com/
    description: API server
components:
  securitySchemes:
    OAuth2:
      type: oauth2
      flows:
        implicit:
          authorizationUrl: https://example.com/api/oauth/authorize
          scopes:
            write: modify pets in your account
            read: read your pets
security:
  - OAuth2:
      - write
      - read
```
```

--------------------------------

### ecs task-def Command Reference

Source: https://learning.postman.com/docs/insights/reference/agent/ecs-task-def

The `ecs task-def` command prints a task definition to be added to an ECS cluster to run the Postman Insights Agent as a daemon in host-networking mode on every EC2 instance in the cluster. Use `-h` or `--help` for assistance.

```APIDOC
## `ecs task-def` Command Reference

### Description
Generates an ECS task definition for the Postman Insights Agent to run as a daemon with host-networking mode on every EC2 instance in the cluster.

### Usage
```bash
postman-insights-agent ecs task-def [flags]
```

### Flags
#### Query Parameters
- **`--cluster`** (string) - The name or ARN of the ECS cluster.
- **`--dry-run`** (boolean) - Perform a dry run: Show what will be done, but don’t change ECS.
- **`--log-format`** (string) - Set to `color`, `plain`, or `json` to control the log format.
- **`--profile`** (string) - Which of the AWS profiles to use to access ECS.
- **`--project`** (string) - The Postman Insights project ID.
- **`--proxy`** (string) - The domain name, IP address, or URL of an HTTP proxy server to use.
- **`--region`** (string) - The AWS region in which the ECS cluster resides.
- **`--service`** (string) - The name or ARN of the ECS service.
- **`--task`** (string) - The name of the ECS task definition to change.
```

--------------------------------

### Extract Seconds from Timestamp with $seconds

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Extracts the local seconds component from a given timestamp and returns it as a number. The input can be a string or a number.

```Postman Script
console.log($seconds("2023-02-08T07:56:14.747+00:00")); // Output: 14
```

--------------------------------

### API Security: OAuth2 Authentication

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures OAuth2 authentication tokens are not sent in plain text by enforcing HTTPS for all API communication.

```APIDOC
## API Security: OAuth2 Authentication

### Description
This section details how to secure OAuth2 authentication by ensuring that access tokens are transmitted over an encrypted channel (HTTPS) rather than plain text.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Global and Operation specific)

### Parameters
N/A

### Request Example
N/A

### Response
N/A

### Resolution

```yaml
swagger: '2.0'
#...
host: 'example.com'
schemes:
  - https
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    authorizationUrl: https://my.auth.example.com/
    tokenUrl: https://my.token.example.com/
security: 
 - OAuth2: []
```

**Note:** For specific operations, ensure the `schemes` array within the operation definition also includes `https`.
```

--------------------------------

### Form Data Configuration

Source: https://learning.postman.com/collection-format/advanced-concepts/request-definition

Defines how to specify formdata for requests, including text and file types. Supports base64 encoded data or file paths.

```APIDOC
## Form Data Configuration

### Description
Allows defining `multipart/form-data` for requests, supporting text, files, and base64 encoded data.

### Method
POST (Implied for requests with form data)

### Endpoint
N/A (Configured within the request body)

### Parameters
#### Request Body (Form Data Fields)
- **key** (string) - Required - The name of the form field.
- **value** (string) - Optional - The text or base64 encoded file content.
- **src** (string) - Optional - Path to a file (use instead of `value` for files).
- **disabled** (boolean) - Optional - Whether the field is disabled.
- **type** (string) - Optional - 'String' for text, 'File' for files.
- **contentType** (string) - Optional - 'file' when sending files.
- **description** (string) - Optional - Description for the field.

### Request Example (Base64 Encoded File)
```json
{
  "key": "image",
  "value": "data:image/png;base64,R0lGODlhDAAMAKIFAF5LAP/zxAAAANyuAP/gaP///wAAAAAAACH5BAEAAAUALAAAAAAMAAwAAAMlWLPcGjDKFYi9lxKBOaGcF35DhWHamZUW0K4mAbiwWtuf0uxFAgA7",
  "disabled": false,
  "type": "String",
  "contentType": "file",
  "description": "form data image example"
}
```

### Request Example (File Path)
```json
{
  "key": "image",
  "description": "Some text emoji",
  "type": "file",
  "src": "/path/to/emoji.png"
}
```
```

--------------------------------

### Other Protocols

Source: https://learning.postman.com/docs/developer/echo-api

The Postman Echo service also supports other protocols besides REST, including GraphQL, gRPC, WebSocket, SocketIO, and MCP.

```APIDOC
## Other Protocols

### Description
Postman Echo provides endpoints for testing various protocols beyond standard RESTful HTTP requests.

### Protocols Supported

*   **GraphQL**
    *   Endpoint: `graphql.postman-echo.com/graphql`
*   **gRPC**
    *   Endpoint: `grpc.postman-echo.com`
*   **WebSocket**
    *   Endpoint: `wss://ws.postman-echo.com/raw`
*   **SocketIO**
    *   Endpoint: `wss://ws.postman-echo.com/socketio`
*   **MCP**
    *   Endpoint: `https://postman-echo-mcp.fly.dev/`

### Usage
Refer to the specific documentation for each protocol to understand how to structure your requests and interpret the responses.
```

--------------------------------

### Tags API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Manage Postman tags programmatically, allowing you to add or remove tags from collections, APIs, and workspaces, and retrieve elements matching a specific tag.

```APIDOC
## Tags API

### Description
Use the Tags APIs to manage your Postman tags programmatically. You can use these endpoints to add or remove tags from Postman collections, APIs, and workspaces. You can also use this API to get all Postman elements that match a given tag and then operate on them programmatically.

### Method
GET, POST, PUT, DELETE

### Endpoint
/tags
```

--------------------------------

### JWT Bearer

Source: https://learning.postman.com/docs/sending-requests/authorization/authorization-types

Postman supports generating JWT bearer tokens for authorization. You can specify payload, algorithm, and signing keys.

```APIDOC
## JWT Bearer

### Description
Generate and use JWT bearer tokens for API authentication. Configure payload, algorithm, and signing details.

### Method
N/A (Client-side configuration)

### Endpoint
N/A (Applies to individual requests, collections, or folders)

### Parameters
#### Request Body
- **Auth Type** (string) - Required - Must be 'JWT Bearer'
- **Add JWT token to** (string) - Required - 'Request Header' or 'Query Param'.
- **Algorithm** (string) - Required - Signing algorithm (e.g., 'HS', 'RS', 'ES', 'PS').
- **Secret** (string) - Required if Algorithm is 'HS' - The secret key for HMAC-SHA.
- **Secret Base64 encoded** (boolean) - Optional - True if the secret is Base64 encoded.
- **Private key** (string) - Required if Algorithm is 'RS', 'ES', 'PS' - The private key for signing.
- **Payload** (object) - Required - JSON object representing the JWT payload.

#### Advanced Configuration (Optional)
- **Request header prefix** (string) - Optional prefix for headers.
- **JWT headers** (object) - Optional custom headers for the JWT token.

### Request Example
```json
{
  "auth": {
    "type": "jwt",
    "jwt": {
      "addTokenTo": "Header",
      "algorithm": "HS256",
      "secret": "your_secret",
      "payload": {
        "sub": "1234567890",
        "name": "John Doe",
        "iat": 1516239022
      }
    }
  }
}
```

### Response
#### Success Response (200)
Depends on the API being called.

#### Response Example
```json
{
  "message": "Success"
}
```
```

--------------------------------

### Set Local Variable Programmatically in Postman

Source: https://learning.postman.com/docs/sending-requests/variables

This snippet demonstrates how to set a local variable programmatically within a Postman pre-request script. Local variables set this way will appear as 'Resolved via script' if referenced in the request. Other variable types like environment or global variables can also be set programmatically and are saved for future use.

```javascript
pm.variables.set("local_variable_name", "variable_value");
pm.environment.set("environment_variable_name", "variable_value");
pm.globals.set("global_variable_name", "variable_value");
```

--------------------------------

### Inverse Hyperbolic Sine

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Computes the inverse hyperbolic sine of a number, returning the result in radians. The result ranges from -infinity to +infinity.

```Postman Functions
$asinh(1) -> 1.5707963267948966
```

--------------------------------

### Replace Substring in String (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $replace() function finds occurrences of a substring within a string and replaces them with another specified string. The replacement can be limited to a certain number of occurrences, and regular expressions can be used for pattern matching.

```FQL
$replace(payments[0].description,"recurring", "renewing", 1)
```

--------------------------------

### Password Credentials Grant Type

Source: https://learning.postman.com/docs/sending-requests/authorization/oauth-20

Configure Postman to use the Password Credentials grant type. This involves sending the user's username and password directly to the access token URL. Use with caution, especially for third-party data.

```APIDOC
## Password Credentials Grant Type

### Description
OAuth 2.0 Password grant type involves sending username and password directly from the client and is therefore not recommended if you’re dealing with third-party data.

### Method
POST

### Endpoint
[Access Token URL]

### Parameters
#### Request Body
- **grant_type** (string) - Required - Set to `password`.
- **username** (string) - Required - The user's username.
- **password** (string) - Required - The user's password.
- **client_id** (string) - Optional - The client ID, if required by the provider.
- **client_secret** (string) - Optional - The client secret, if required by the provider.

### Request Example
```json
{
  "grant_type": "password",
  "username": "user@example.com",
  "password": "your_password",
  "client_id": "your_client_id",
  "client_secret": "your_client_secret"
}
```

### Response
#### Success Response (200)
- **access_token** (string) - The obtained access token.
- **token_type** (string) - The type of token (e.g., Bearer).
- **expires_in** (integer) - The token's validity period in seconds.
- **refresh_token** (string) - Optional - A token to obtain a new access token when the current one expires.

#### Response Example
```json
{
  "access_token": "your_access_token_here",
  "token_type": "Bearer",
  "expires_in": 3600,
  "refresh_token": "your_refresh_token_here"
}
```
```

--------------------------------

### FQL Object Keys Function

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The '$keys' function returns an array containing all the keys (property names) of a given object. This is useful for iterating over or inspecting object properties.

```FQL
"Product": [
    {
        "Product Name": "Bowler Hat",
        "ProductID": 858383,
        "SKU": "0406654608",
        "Description": {
            "Colour": "Purple",
            "Width": 300,
            "Height": 200,
            "Depth": 210,
            "Weight": 0.75
        },
        "Price": 34.45,
        "Quantity": 2
    }
]
$keys(Product) -> ["Product Name","ProductID","SKU","Description","Price","Quantity"]
```

--------------------------------

### Persisting Variables Between Monitor Runs with Postman API

Source: https://learning.postman.com/docs/monitoring-your-api/faqs-monitors

While global and environment variables in Postman Monitors revert to their original values after a run, you can persist changes by using the Postman API to update your environment after each monitor run. This allows subsequent runs to utilize the updated variable values.

```bash
POST {{postman_api_url}}/collections/{{collection_uid}}/monitors/{{monitor_id}}/runs

# In the monitor's pre-request script or a separate script:
# pm.sendRequest({
#     url: '{{postman_api_url}}/environments/{{environment_id}}',
#     method: 'PUT',
#     headers: {
#         'Content-Type': 'application/json',
#         'Authorization': 'Bearer {{api_key}}'
#     },
#     body: {
#         mode: 'raw',
#         raw: JSON.stringify({
#             values: [
#                 {
#                     key: 'myVariable',
#                     value: 'newValue',
#                     enabled: true
#                 }
#             ]
#         })
#     }
# }, function (err, response) {
#     if (err) {
#         console.log(err);
#     } else {
#         console.log('Environment updated successfully');
#     }
# });
```

--------------------------------

### Control Request Workflow with pm.execution.setNextRequest

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-execution

The `pm.execution.setNextRequest` method allows dynamic control over the sequence of requests when running a collection using the Collection Runner or Newman. It overrides the default or specified run order by indicating which request should execute next. This method has no effect when requests are run individually using 'Send'.

```javascript
pm.execution.setNextRequest(requestName:String):Function
```

```javascript
//script in another request calls:
//pm.environment.set('next', pm.info.requestId)
pm.execution.setNextRequest(pm.environment.get('next'));

```

--------------------------------

### Excessive Data Exposure - Basic Authentication

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Addresses the vulnerability where basic authentication credentials are sent in plain text.

```APIDOC
## Basic Authentication Security

### Description
Ensures that basic authentication credentials are transmitted securely using HTTPS.

### Method
N/A (Configuration based)

### Endpoint
N/A (Global or specific server configuration)

### Parameters
None

### Request Example
N/A

### Response
N/A

#### Resolution Example
```yaml
servers:
- url: https://example.com/
  description: Example server
components:
  securitySchemes:
    BasicAuth:
      type: http
      scheme: basic
security:
- BasicAuth: []
```
```

--------------------------------

### Calculate Sum of Numeric Array

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $sum helper function calculates the total sum of all numeric values within a given array. It takes a single numeric array as input and returns the sum. This is useful for aggregations.

```postman-helper
$sum([1,2,3,4]) -> 10
```

--------------------------------

### JSON Schema for Postman Proxy Configuration

Source: https://learning.postman.com/collection-format/reference/proxy

This JSON schema defines the structure and constraints for a proxy configuration object within a Postman collection. It specifies properties like 'match', 'host', 'port', 'tunnel', and 'disabled' with their respective types, descriptions, and default values. This schema ensures valid proxy configurations are used.

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "#/definitions/proxy-config",
  "title": "Proxy Config",
  "description": "Using the Proxy, you can configure your custom proxy into the postman for particular url match",
  "type": "object",
  "properties": {
    "match": {
      "default": "http+https://*/*",
      "description": "The Url match for which the proxy config is defined",
      "type": "string"
    },
    "host": {
      "type": "string",
      "description": "The proxy server host"
    },
    "port": {
      "type": "integer",
      "minimum": 0,
      "default": 8080,
      "description": "The proxy server port"
    },
    "tunnel": {
      "description": "The tunneling details for the proxy config",
      "default": false,
      "type": "boolean"
    },
    "disabled": {
      "type": "boolean",
      "default": false,
      "description": "When set to true, ignores this proxy configuration entity"
    }
  }
}
```

--------------------------------

### Termination Message Template

Source: https://learning.postman.com/docs/postman-flows/build-flows/structure/loops/loops-pagination

This template string is used in a Postman Flow's 'Template' block to display a message when the pagination loop terminates. It shows the last page number reached before stopping.

```postman-flow-template
Stopping! We got to page {{lastPage}}.
```

--------------------------------

### Billing API

Source: https://learning.postman.com/docs/developer/postman-api/intro-api

Enables retrieval of information about your Postman billing account, useful for account management, compliance, and integration with internal systems.

```APIDOC
## Billing API

### Description
The Billing API enables you to get information about your Postman billing account. You can use these endpoints to help with account and compliance. You can also use these endpoints to integrate with your internal systems, such as SAP.

### Method
GET

### Endpoint
/billing
```

--------------------------------

### POST /network/private

Source: https://learning.postman.com/docs/collaborating-in-postman/private-api-network/publish-private-network-elements-with-api

Adds a workspace to your Private API Network folder. This endpoint allows you to organize your workspaces within folders in your Private API Network.

```APIDOC
## POST /network/private

### Description
Adds a workspace to your Private API Network folder.

### Method
POST

### Endpoint
/network/private

### Parameters
#### Request Body
- **workspace** (object) - Required - Contains workspace details.
  - **id** (string) - Required - The ID of the workspace to add.
  - **parentFolderId** (integer) - Required - The ID of the folder to add the workspace to.

### Request Example
```json
{
    "workspace": {
        "id": "1f0df51a-8658-4ee8-a2a1-d2567dfa09a9",
        "parentFolderId": {{folderId}}
    }
}
```

### Response
#### Success Response (200)
- **addedAt** (string) - The timestamp when the workspace was added.
- **addedBy** (integer) - The ID of the user who added the workspace.
- **createdBy** (integer) - The ID of the user who created the workspace.
- **createdAt** (string) - The timestamp when the workspace was created.
- **updatedBy** (integer) - The ID of the user who last updated the workspace.
- **updatedAt** (string) - The timestamp when the workspace was last updated.
- **type** (string) - The type of the added item (e.g., "workspace").
- **id** (string) - The ID of the workspace.
- **name** (string) - The name of the workspace.
- **summary** (string) - A summary of the workspace.
- **description** (string) - A description of the workspace.
- **href** (string) - A URL to the workspace.
- **parentFolderId** (integer) - The ID of the parent folder.

#### Response Example
```json
{
    "addedAt": "2023-08-03T13:18:25.000Z",
    "addedBy": 12345678,
    "createdBy": 12345678,
    "createdAt": "2023-08-03T13:18:25.000Z",
    "updatedBy": 12345678,
    "updatedAt": "2023-08-03T13:18:25.000Z",
    "type": "workspace",
    "id": "1f0df51a-8658-4ee8-a2a1-d2567dfa09a9",
    "name": "Billing Team Workspace",
    "summary": "The Billing team's workspace.",
    "description": "The Billing team's workspace.",
    "href": "https://api.getpostman.com/workspaces/1f0df51a-8658-4ee8-a2a1-d2567dfa09a9",
    "parentFolderId": 1
}
```
```

--------------------------------

### Excessive Data Exposure - OAuth 1.0 Authentication

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Addresses the vulnerability where OAuth 1.0 tokens are sent in plain text.

```APIDOC
## OAuth 1.0 Authentication Security

### Description
Ensures that OAuth 1.0 authentication tokens are transmitted securely using HTTPS.

### Method
N/A (Configuration based)

### Endpoint
N/A (Global or specific server configuration)

### Parameters
None

### Request Example
N/A

### Response
N/A

#### Resolution Example
```yaml
servers:
  - url: https://my.api.example.com/
    description: API server
components:
  securitySchemes:
    OAuth1:
      type: http
      scheme: oauth
      bearerFormat: '1.0'
security:
  - OAuth1: []
```
```

--------------------------------

### Script Variables

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-variables

Manage local variables within your Postman scripts using `pm.variables`. This section covers checking for variable existence, retrieving values from the narrowest scope, setting local variables, and resolving dynamic variables.

```APIDOC
## Script Variables

Use the `pm.variables` methods in your scripts to access and manipulate variables in the narrowest scope and local variables. To learn more, see Variable scope precedence.
> Postman doesn’t support using `pm.variables` to access and manipulate vault secrets. Use the pm.vault methods.

### `pm.variables.has(variableName:String)`

Checks if there is a variable with the specified name in any of the scopes, such as the collection or environment scope.
Returns one of the following:
  * `true` - The variable exists in one of the scopes.
  * `false` - The global variable doesn’t exist in any of the scopes.


### `pm.variables.get(variableName:String)`

Gets the value of a variable with the specified name in the narrowest scope.
Returns the value of the variable in the narrowest scope. For example, if a variable with the same name exists in the collection and environment scopes, Postman returns the value in the active environment.
> You can append a string to the value of a variable using the `+` operator before or after the method.

### `pm.variables.set(variableName:String, variableValue:*)`

Sets a local variable with the specified name and value.

### `pm.variables.replaceIn(variableName:string)`

Gets the resolved value of a dynamic variable inside a script using the syntax `{{$dynamicVariableName}}`
Returns the value of the dynamic variable.

### `pm.variables.toObject()`

Gets all variables in the active environment.
Based on the order of precedence, returns all variables and their values as an object. The object will contain variables from multiple scopes. For example, if there’s a variable in the open collection and globals, the object will include both variables.
```

--------------------------------

### Logical NOT Operation

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $not helper function returns the boolean opposite of its input. It evaluates to true if the input is falsey (false, null, 0, "", undefined) and false if the input is truthy (true, non-zero numbers, non-empty strings, objects, arrays).

```postman-helper
$not(true) -> false
$not(false) -> true
$not(null) -> true
$not(0) -> true
$not(100) -> false
$not("") -> true
$not("hello") -> false
```

--------------------------------

### Increment Page Number Logic

Source: https://learning.postman.com/docs/postman-flows/build-flows/structure/loops/loops-pagination

This TypeScript expression is used within a Postman Flow's 'Evaluate' block to increment the current page number. It takes the 'pageBeforeTurning' value, converts it to a number, and adds 1.

```typescript
Number(pageBeforeTurning) + 1
```

--------------------------------

### JSON Schema for Custom Function Options

Source: https://learning.postman.com/docs/api-governance/configurable-rules/spectral

This JSON Schema defines the structure and validation rules for the options parameter of a custom Postman function. It specifies that the 'options' must be an object with a required 'values' property, which should be an array. `additionalProperties: false` prevents any properties other than 'values' from being included.

```json
{
    "input": {
      "type": "string"
    },
    "options": {
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "values": {
          "type": "array"
        }
      },
      "required": ["values"],
    },
  }
```

--------------------------------

### OpenAPI: Secure API Server URL with HTTPS for Basic Authentication

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

This snippet shows how to configure an OpenAPI specification to use HTTPS for the API server URL when Basic Authentication is used. This protects credentials from being intercepted in plain text.

```yaml
servers:
- url: https://example.com/
  description: Example server
components:
 securitySchemes:
  BasicAuth:
   type: http
   scheme: basic
security:
- BasicAuth: []

```

--------------------------------

### pm.execution.setNextRequest

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-execution

Enables the creation of request workflows by specifying the next request to be executed, primarily used with the Collection Runner or Newman.

```APIDOC
## pm.execution.setNextRequest

### Description
You can use the `pm.execution.setNextRequest` method for building request workflows when you use the Collection Runner or Newman.

> `setNextRequest` has no effect when you run requests using **Send**. It only has an effect when you run a collection.

### Method
```javascript
pm.execution.setNextRequest(requestName:String):Function
pm.execution.setNextRequest(requestId:String):Function
```

### Usage
- Overrides the default or specified run order when running a collection.
- Specify the name or ID of the next request to execute.

### Examples
1. **Run by Request Name:**
   ```javascript
   // Assuming 'requestName' is the name of the next request, e.g., "Get customers"
pm.execution.setNextRequest(requestName)
   ```

2. **Run by Request ID:**
   ```javascript
   // Script in another request calls:
   // pm.environment.set('next', pm.info.requestId)
pm.execution.setNextRequest(pm.environment.get('next'))
   ```
```

--------------------------------

### Protocol Profile Behavior Schema Definition

Source: https://learning.postman.com/collection-format/reference/protocol-profile-behavior

Defines the structure for protocol profile behavior configurations. This JSON schema specifies the properties and types for settings that alter the default request sending behavior in Postman. It includes a schema version, object type, and a descriptive title and ID.

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "title": "Protocol Profile Behavior",
  "$id": "#/definitions/protocol-profile-behavior",
  "description": "Set of configurations used to alter the usual behavior of sending the request"
}
```

--------------------------------

### FQL String Length Function

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The '$length' function returns the number of characters in a given string. It accepts a string as input and returns a number representing its length.

```FQL
$length("abc") -> 3
$length("") -> 0
```

--------------------------------

### Spectral Custom Function Structure (JavaScript)

Source: https://learning.postman.com/docs/api-governance/configurable-rules/spectral

Provides a basic structure for a custom governance function in JavaScript compatible with Spectral. It includes the required `targetVal` parameter and demonstrates how to define custom logic within the function.

```javascript
function myCustomFunction(targetVal, options, context) { ... }

```

--------------------------------

### FQL Object Lookup Function

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The '$lookup' function retrieves the value associated with a specific key from an object. It takes the object and the key name as arguments and returns the corresponding value.

```FQL
($o := { "name" : "John", "email": "john@gmail.com"}; $lookup($o, "name")) -> "John"
```

--------------------------------

### Base64 Encode String (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $base64encode() function converts a given string into its Base64 encoded representation. This is often used for data transmission or simple obfuscation.

```FQL
$base64encode("some data here")
```

--------------------------------

### Shuffle Array Elements

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Returns a new array with the elements of the original array randomly reordered.

```Postman Functions
$shuffle([1,2,3,4]) -> [3,1,4,2]
```

--------------------------------

### Add Min/Max Length to String Schema

Source: https://learning.postman.com/docs/design-apis/collections/add-properties-to-body-data

Set minimum and maximum character length constraints for a string property using 'minLength' and 'maxLength'. Postman will flag strings that do not meet these length requirements.

```json
{
    "baseUrl": {
        "type": "string",
        "format": "uri",
        "minLength": 15,
        "maxLength": 25
    }
}
```

--------------------------------

### Extract Day from Timestamp - Postman Script

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Retrieves the day component (1-31) from a given timestamp. Useful for daily reporting or scheduling tasks.

```Postman Script
$day("2023-02-08") -> 8
```

--------------------------------

### Count Array Elements

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Returns the total number of elements present in an array. An empty array will return 0.

```Postman Functions
$count([1,2,3,4,5]) -> 5
$count([]) -> 0
```

--------------------------------

### Round Number Down (Floor) (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The floor() function rounds a given number down to the nearest whole number. This is useful for scenarios where you need to truncate fractional parts, such as calculating completed units.

```FQL
$floor(3.99)
```

--------------------------------

### Postman Collection: Nested Folders (JSON)

Source: https://learning.postman.com/collection-format/getting-started/defining-a-simple-api

Illustrates structuring a Postman API collection with nested folders. This allows for hierarchical organization of related API requests, enhancing manageability.

```json
{
  "info": {
    "name": "My collection with multiple requests",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/"
  },
  "item": [
    {
      "item": [
        {
          "name": "Request 1a",
          "request": "https://postman-echo.com/get",
          "description": "This request is in a Folder nested inside another folder"
        },
        {
          "name": "Request 1b",
          "request": "https://postman-echo.com/get",
          "description": "This request is in a Folder nested inside another folder"
        }
      ]
    },
    {
      "name": "Request 2",
      "request": "https://postman-echo.com/get",
      "description": "This request is in a single folder"
    }
  ]
}
```

--------------------------------

### Define Global 'consumes' Field with Items

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures the global 'consumes' field in the OpenAPI schema contains at least one valid MIME type. An empty array would allow the API to accept any input type by default, increasing vulnerability.

```yaml
swagger: '2.0'
paths: {}
consumes:
  - application/json
...

```

--------------------------------

### Timestamp Output Format

Source: https://learning.postman.com/docs/postman-flows/reference/blocks/schedule

The Timestamp output from the Schedule block provides the date and time when the action was triggered in a JSON key/value pair format. This output can be connected to other blocks to utilize the trigger time.

```json
{
    "startTime": "YYYY-MM-DDTHH:MM:SS.SSSZ"
}
```

--------------------------------

### Consumes Field Definition

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Addresses issues related to the `consumes` field in Swagger/OpenAPI definitions, ensuring the API clearly specifies the MIME types it accepts as input for operations.

```APIDOC
## Consumes Field Definition Issues

### Description
These issues relate to the `consumes` field in the API definition. Proper definition of `consumes` is crucial for preventing unexpected input data that could lead to security vulnerabilities such as SQL injection or buffer overflows.

### Method
N/A (Configuration issue)

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A

## Scenarios and Resolutions:

### Consumes field is not defined
- **Issue:** If the global `consumes` field isn’t defined, the API could accept any form of data as input. This could open your API to any number of potential attacks, like buffer overflow, decoding errors, or SQL injection attacks.
- **Fix:** The `consumes` field needs to be defined in the schema.
```yaml
swagger: '2.0'
paths: {}
consumes:
  - application/json
```

### Consumes field does not contain any item
- **Issue:** If the `consumes` field has an empty array, the API can accept any type of input by default.
- **Fix:** The global `consumes` field needs at least one item with valid MIME type in the array.
```yaml
swagger: '2.0'
paths: {}
consumes:
  - application/json
...
```

### Consumes field for the operation does not contain any item
- **Issue:** No `consumes` field in the operation means that API can accept any type of input by default.
- **Fix:** The `consumes` field in `PUT`/`PATCH`/`POST` operations needs to have at least one item in the array.
```yaml
swagger: '2.0'
paths:
  /user/{userId}:
    put:
      consumes:
        - application/json
```

### Operation does not contain consumes field
- **Issue:** If both the global `consumes` field and operation’s `consumes` field (for `PUT`/`PATCH`/`POST`) aren’t defined, anyone can exploit your API.
- **Fix:** Define a `consumes` field in the operation if not defined at the global level.
```yaml
swagger: '2.0'
paths:
  /user/{userId}:
    put:
      consumes:
        - application/json
  ...
...
```
```

--------------------------------

### Extract Month from Timestamp with $month

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Extracts the month component from a given timestamp and returns it as a number. The input can be a string or a number.

```Postman Script
console.log($month("2023-02-08")); // Output: 2
```

--------------------------------

### Add 'description' to JSON Schema Properties - Postman

Source: https://learning.postman.com/docs/design-apis/collections/add-properties-to-body-data

Include descriptive text for properties within a JSON schema. This documentation is displayed as tooltips in Postman when hovering over body properties, improving clarity for users working with the API request.

```json
{
    "baseUrl": {
        "type": "string",
        "format": "uri",
        "description": "The base URL of the service"
    }
}
```

--------------------------------

### Find Maximum Value in Numeric Array

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The $max helper function calculates and returns the largest number from a given numeric array. It takes a single array of numbers as input. This is useful for identifying peak values in datasets.

```postman-helper
$max([9,2,17,3]) -> 17
```

--------------------------------

### Postman Insights Agent ECS Add Command Usage

Source: https://learning.postman.com/docs/insights/reference/agent/ecs-add

The basic usage of the `ecs add` command to deploy the Postman Insights Agent to an ECS task. This command requires specific flags to configure the agent's behavior and integration with ECS.

```bash
postman-insights-agent ecs add [flags]
```

--------------------------------

### Item Object Structure

Source: https://learning.postman.com/collection-format/reference/item

This section details the structure of an 'Item' object in Postman, which represents a single API request and its associated responses.

```APIDOC
## Item Object Structure

### Description
An item is the basic building block of a Postman collection, containing a request and its corresponding responses.

### Fields

#### Reference Table

| Field Name            | Type        | Required | Description                                                          |
|---------------------|-------------|----------|----------------------------------------------------------------------|
| `id`                | `string`    | `false`  | A unique ID used to identify collections internally.                 |
| `name`              | `string`    | `false`  | A human-readable identifier for the current item.                    |
| `description`       | `description` | `false`  | The description of this item.                                        |
| `variable`          | `variable-list` | `false`  | Variables scoped to this item.                                       |
| `event`             | `event-list`  | `false`  | Events that this item listens to.                                    |
| `request`           | `request`     | `true`   | Carries all necessary information about this HTTP call.              |
| `response`          | `response`    | `false`  | Represents any type of response received from your HTTP request.     |
| `protocolProfileBehavior` | `protocol-profile-behavior` | `false` | Configurations to change the usual behavior of sending the request. |

#### Schema
```json
{
  "type": "object",
  "title": "Item",
  "$id": "#/definitions/item",
  "description": "Items are entities which contain an actual HTTP request, and sample responses attached to it.",
  "properties": {
    "id": {
      "type": "string",
      "description": "A unique ID that is used to identify collections internally"
    },
    "name": {
      "type": "string",
      "description": "A human readable identifier for the current item."
    },
    "description": {
      "$ref": "#/definitions/description"
    },
    "variable": {
      "$ref": "#/definitions/variable-list"
    },
    "event": {
      "$ref": "#/definitions/event-list"
    },
    "request": {
      "$ref": "#/definitions/request"
    },
    "response": {
      "type": "array",
      "title": "Responses",
      "items": {
        "$ref": "#/definitions/response"
      }
    },
    "protocolProfileBehavior": {
      "$ref": "#/definitions/protocol-profile-behavior"
    }
  },
  "required": [
    "request"
  ]
}
```
```

--------------------------------

### Define Operation 'produces' Field if Global is Missing

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that a 'produces' field is defined for an operation if it's not defined globally. This prevents the API from returning any type of data by default when neither the global nor operation-level 'produces' fields are set.

```yaml
swagger: '2.0'
paths:
  /user/{userId}:
    get:
      produces:
        - application/json
  ...
...

```

--------------------------------

### pm.execution.skipRequest

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-execution

Allows you to stop the execution of a request from a pre-request script. When invoked, the request is not sent, and subsequent scripts or tests are skipped.

```APIDOC
## pm.execution.skipRequest

### Description
The `pm.execution.skipRequest` method enables you to stop the run of a request from a pre-request script.

### Method
```javascript
pm.execution.skipRequest()
```

### Usage
- Can be used in the **Pre-request** tab of a request, collection, or folder.
- When `pm.execution.skipRequest()` is encountered, the request is not sent.
- Any remaining scripts in the **Pre-request** tab are skipped, and no tests are run.
- In Collection Runner, Newman, and Postman CLI, the request is skipped, and the run proceeds to the next request.
- Results will show no response and no tests for the skipped request.

> **Note:** This method is not supported in the **Post-response** tab and will result in a `TypeError`.
```

--------------------------------

### pm.request Properties

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-request

Access various properties of the current request object within Postman scripts.

```APIDOC
## pm.request Properties

### Description
The `pm.request` object contains the following properties, allowing access to request configuration details within Postman scripts.

### Properties
*   **`pm.request.url`** (Url) - The request’s URL.
*   **`pm.request.headers`** (HeaderList) - The list of headers for the current request.
*   **`pm.request.method`** (String) - The HTTP request’s method (e.g., GET, POST).
*   **`pm.request.methodPath`** (String) - The package, service, and method name in `packageName.serviceName.methodName` format.
*   **`pm.request.body`** (RequestBody) - The request body’s data. This object is immutable and can’t be modified from scripts.
*   **`pm.request.auth`** - The request’s authentication details.
*   **`pm.request.metadata`** (PropertyList<{ key: string, value: string }>) - The list of metadata sent with the request. Each item contains `key` and `value` properties.
*   **`pm.request.messages`** (PropertyList) - The list of outgoing messages. Each message object has `data` and `timestamp` properties. For unary and server streaming methods, `pm.request.messages` contains a single message at index `0` accessible via `pm.request.messages.idx(0)`.

### Note
Request mutation isn’t supported in the `pm` object.
```

--------------------------------

### Info Object Schema Definition

Source: https://learning.postman.com/collection-format/reference/info

The JSON schema defining the structure and constraints for the 'info' object within a Postman collection.

```APIDOC
## Info Object Schema Definition

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "#/definitions/info",
  "title": "Information",
  "description": "Detailed description of the info block",
  "type": "object",
  "properties": {
    "name": {
      "type": "string",
      "title": "Name of the collection",
      "description": "A collection's friendly name is defined by this field. You would want to set this field to a value that would allow you to easily identify this collection among a bunch of other collections, as such outlining its usage or content."
    },
    "_postman_id": {
      "type": "string",
      "description": "Every collection is identified by the unique value of this field. The value of this field is usually easiest to generate using a UID generator function. If you already have a collection, it is recommended that you maintain the same id since changing the id usually implies that is a different collection than it was originally.\n *Note: This field exists for compatibility reasons with Collection Format V1.*"
    },
    "description": {
      "$ref": "#/definitions/description"
    },
    "version": {
      "$ref": "#/definitions/version"
    },
    "schema": {
      "description": "This should ideally hold a link to the Postman schema that is used to validate this collection. E.g: https://schema.getpostman.com/collection/v1",
      "type": "string"
    }
  },
  "required": [
    "name",
    "schema"
  ]
}
```
```

--------------------------------

### Postman Collection: Multiple Requests (JSON)

Source: https://learning.postman.com/collection-format/getting-started/defining-a-simple-api

Demonstrates defining a Postman API collection with multiple requests. This is achieved by using an 'item' array, where each element represents a distinct request.

```json
{
  "info": {
    "name": "My collection with multiple requests",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/"
  },
  "item": [
    {
      "name": "This is request one",
      "request": "http://myapi.com/api/1"
    },
    {
      "name": "This is request two",
      "request": "http://myapi.com/api/2"
    }
  ]
}
```

--------------------------------

### Sum Numerical Values (FQL)

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/data-manipulation

The $sum() function calculates the total of all numerical values found for a specified key within an array or object. It's used for aggregating data, like calculating totals from a list of transactions.

```FQL
$sum(payments.amount)
```

--------------------------------

### Token URL uses HTTP Protocol

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that OAuth authentication tokens are not transmitted over an unencrypted channel by mandating the use of HTTPS for the token URL.

```APIDOC
## Token URL uses HTTP Protocol

### Description
OAuth authentication tokens are transported over an unencrypted channel. Anyone listening to the network traffic while the token is being sent can intercept it.

### Method
N/A (Configuration issue)

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A

## Resolution
Make sure that the token URL is a valid URL and follows HTTPS protocol.

```yaml
swagger: '2.0'
#...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    #...
    tokenUrl: https://example.com/token
```
```

--------------------------------

### Add Contact Name to OpenAPI Contact Object (YAML)

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

This code snippet illustrates adding a 'name' to the 'contact' object within the 'info' section of an OpenAPI specification. Including a contact name clarifies API ownership for consumers.

```yaml
Copyswagger: '2.0'
info:
  title: An API name
  version: '1.0'
  contact:
    name: A contact name

```

--------------------------------

### Import External Package (Postman)

Source: https://learning.postman.com/docs/tests-and-scripts/write-scripts/postman-sandbox-reference/pm-require

Import packages from external registries like npm or jsr into your Postman scripts. Specify the package name and optionally a version number. Assign the imported package to a variable to call its functions.

```javascript
// package imported from npm
const npmVariableName = pm.require('npm:package-name@version-number');

npmVariableName.functionName()
```

```javascript
// package imported from jsr
const jsrVariableName = pm.require('jsr:package-name@version-number');

jsrVariableName.functionName()
```

--------------------------------

### FQL Assert Function

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The '$assert' function throws an error with a specified message if a given condition is false. It's primarily used for validation within FQL expressions.

```FQL
$assert(user.age <18, "error: user can't vote!")
```

--------------------------------

### Authorization URL uses HTTP Protocol

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Ensures that OAuth authorization credentials are not transferred over an unencrypted channel by enforcing the use of HTTPS.

```APIDOC
## Authorization URL uses HTTP Protocol

### Description
OAuth authorization credentials are transported over an unencrypted channel. Anyone listening to the network traffic while the calls are being made can intercept them.

### Method
N/A (Configuration issue)

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A

## Resolution
Make sure that the authorization URL is a valid URL and follows HTTPS protocol.

```yaml
swagger: '2.0'
#...
securityDefinitions:
  OAuth2:
    type: oauth2
    flow: accessCode
    #...
    authorizationUrl: https://example.com/authorize
```
```

--------------------------------

### Reverse Array Elements

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Returns a new array with the order of elements from the original array reversed.

```Postman Functions
$reverse([1,2,3,4,5]) -> [5,4,3,2,1]
```

--------------------------------

### Disable Environment Variables for Postman (macOS/Linux)

Source: https://learning.postman.com/docs/getting-started/installation/proxy

This shell script unsets common proxy environment variables (`http_proxy`, `https_proxy`, `HTTP_PROXY`, `HTTPS_PROXY`) before launching the Postman application. This is a workaround for situations where OS-level proxy environment variables override Postman's proxy configurations. Replace `/path/to/postman` with the actual path to your Postman executable.

```bash
http_proxy=''
https_proxy=''
HTTP_PROXY=''
HTTPS_PROXY=''
/path/to/postman

```

--------------------------------

### Ensure 5xx HTTP Status Code for Operations

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi2

Validates that API operations include a 5xx HTTP status code in their responses, accounting for potential server-side failures. This rule ensures proper error handling is defined.

```yaml
swagger: '2.0'
# ...
paths:
  /resources:
    get:
      responses:
        '500':
          description: A server error response

```

--------------------------------

### OAuth Refresh URL Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that the OAuth refresh URL uses HTTPS to protect refresh tokens from being intercepted.

```APIDOC
## OAuth Refresh URL Security

### Description
This section addresses the security risk of OAuth refresh URLs using HTTP. It recommends HTTPS to ensure refresh tokens are transmitted securely.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Configuration focused)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
components:
  securitySchemes:
    OauthFlow:
      type: oauth2
      flows:
        authorizationCode:
          authorizationUrl: https://my.auth.example.com/
          tokenUrl: https://my.token.example.com/
          refreshUrl: https://my.refresh.example.com/
          scopes:
            write: modify data
            read: read data
```

### Response
#### Success Response (200)
N/A (Configuration focused)

#### Response Example
N/A (Configuration focused)
```

--------------------------------

### Floor Function

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Returns the largest integer that is less than or equal to the input number.

```Postman Functions
$floor(3.4) -> 3
```

--------------------------------

### HTTPS Protocol Enforcement

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that API operations use the HTTPS protocol to prevent data interception during transmission.

```APIDOC
## HTTPS Protocol Enforcement

### Description
This section highlights the importance of using HTTPS for all API operations to ensure data is transmitted securely and is not vulnerable to interception.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Configuration focused)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
get:
  operationId: getPetsById
  servers:
    - url: https://my.api.example.com/
```

### Response
#### Success Response (200)
N/A (Configuration focused)

#### Response Example
N/A (Configuration focused)
```

--------------------------------

### FQL Logical OR Operator

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

The 'or' operator returns true if at least one of the provided conditions is true. It is useful for checking multiple possible states.

```FQL
value1 < 18 or value1 < 100 -> true
value1 < 18 or value1 > 100 -> false
```

--------------------------------

### OAuth Authorization URL Security

Source: https://learning.postman.com/docs/api-governance/api-definition/openapi3

Ensures that the OAuth authorization URL uses HTTPS to prevent credentials from being transferred as plain text.

```APIDOC
## OAuth Authorization URL Security

### Description
This section addresses the security risk associated with OAuth authorization URLs using HTTP. It recommends using HTTPS to protect credentials during transfer.

### Method
N/A (Configuration focused)

### Endpoint
N/A (Configuration focused)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
components:
  securitySchemes:
     OauthScheme:
        type: oauth2
        flows:
          authorizationCode:
            authorizationUrl: https://my.auth.example.com/
```

### Response
#### Success Response (200)
N/A (Configuration focused)

#### Response Example
N/A (Configuration focused)
```

--------------------------------

### Extract Milliseconds from Timestamp with $milliSeconds

Source: https://learning.postman.com/docs/postman-flows/flows-query-language/function-reference

Extracts the milliseconds component from a given timestamp and returns it as a number. The input can be a string or a number.

```Postman Script
console.log($milliSeconds("2023-02-08T07:56:14.747+00:00")); // Output: 747
```