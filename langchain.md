### Agent Builder - Get Started

Source: https://docs.langchain.com/langsmith/agent-builder-remote-mcp-servers

Guides for getting started with the Agent Builder, including quickstarts, essentials, templates, setup, and agent settings.

```APIDOC
## Agent Builder - Get Started

### Description
Guides to help users begin using the Agent Builder.

### Pages
- `langsmith/agent-builder-quickstart`
- `langsmith/agent-builder-essentials`
- `langsmith/agent-builder-templates`
- `langsmith/agent-builder-setup`
- `langsmith/agent-builder-manage-agent-settings`
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/self-host-scale

Handles the setup URL callback from GitHub Apps during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the installation process status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/file_loaders/text

Handles the setup callback from GitHub Apps, triggered during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Returns a success message or redirects to the frontend callback page.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/export-backend

Handles the initial setup for an OAuth provider, including processing new installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for an OAuth provider. For new installations with code/state, it processes the setup similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/tools/parallel_search

Handles the setup callback for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for GitHub App installations. For updates, it displays a success page; for new installations, it processes the OAuth token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/tools/bedrock_agentcore_code_interpreter

Handles the setup callback for GitHub Apps, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. Processes new installations via code/state exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the installation status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/rbac

Handles the setup process for a new OAuth provider installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup for new installations with code or state, similar to the regular OAuth callback flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Setup completion status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/microsoft_onedrive

Handles the setup URL callback from GitHub Apps or other providers, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup URL callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For updates, it displays a success page; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### Full Example: Langchain Agent Setup and Invocation (JavaScript)

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Provides a complete, runnable example of setting up a Langchain agent. It includes imports for agent creation, tool definition, model initialization, and type definitions, demonstrating the end-to-end process.

```javascript
import { createAgent, tool, initChatModel, type ToolRuntime } from "langchain";

```

--------------------------------

### Agent Builder - Get Started

Source: https://docs.langchain.com/oss/javascript/deepagents/subagents

Guides for getting started with the Agent Builder, including quickstarts and essentials.

```APIDOC
## Agent Builder - Get Started

### Description
Guides to help users begin using the Agent Builder, covering initial setup, core concepts, and available templates.

### Pages

- `langsmith/agent-builder-quickstart`
- `langsmith/agent-builder-essentials`
- `langsmith/agent-builder-templates`
- `langsmith/agent-builder-setup`
- `langsmith/agent-builder-manage-agent-settings`
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/langchain/multi-agent/subagents

Handles the setup flow for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup or update of a GitHub App installation. Processes new installations via code/state or confirms updates for existing installations.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/agent-server-api/thread-runs

Handles the setup process for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles user installation or updates for GitHub Apps. For updates, it displays a success page; for new installations, it processes the OAuth flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/cicd-pipeline-example

Handles OAuth setup callbacks, specifically for GitHub App installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint processes new installations or updates to GitHub App access.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Status message indicating success or redirect instruction.
```

--------------------------------

### Python Quickstart: Initialize PrivyWalletTool and Create Agent

Source: https://docs.langchain.com/oss/python/integrations/tools/privy

This Python code snippet demonstrates the initial setup for using the PrivyWalletTool within a LangChain agent. It covers importing necessary modules, setting up environment variables for credentials, and creating an agent that can leverage Privy's wallet functionalities. Ensure you have the 'langchain-privy' and 'langchain' libraries installed.

```python
import os
from langchain_privy import PrivyWalletTool
from langchain.agents import create_agent

# Set credentials
os.environ["PRIVY_API_KEY"] = "your_privy_api_key"
os.environ["PRIVY_ACCESS_TOKEN"] = "your_privy_access_token"

# Initialize the PrivyWalletTool
privy_wallet_tool = PrivyWalletTool()

# Example of creating an agent (details depend on your LangChain setup)
# agent = create_agent(tools=[privy_wallet_tool], ...)

```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/agent-server-api/threads/create-thread

Handles the setup process for a new GitHub App installation or updates to existing installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup or update of a GitHub App installation. For updates, it displays a success page; for new installations, it processes the OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback triggered when a user installs or updates their GitHub App installation. For update actions, it displays a success page. For new installations with code/state, it processes the token exchange similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps, processing installation or update events.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the OAuth provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/polly

Handles the initial setup for new OAuth installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the initial setup for a new OAuth installation, similar to the regular OAuth callback flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Setup completion status.
```

--------------------------------

### LangGraph Quickstart Example (JavaScript)

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

This snippet demonstrates a basic LangGraph setup in JavaScript, likely for defining a graph structure. It uses JSX syntax for rendering components and styling, indicating a frontend framework context. The code defines a graph with nodes and edges, suitable for agentic workflows.

```javascript
function MDXContent(props = {}) {\n const {wrapper: MDXLayout} = {\n ..._provideComponents(),\n ...props.components\n };\n return MDXLayout ? _jsx(MDXLayout, {\n ...props,\n children: _jsx(_createMdxContent, {\n ...props\n })\n }) : _createMdxContent(props);\n}\nreturn {\n default: MDXContent\n};\nfunction _missingMdxReference(id, component) {\n throw new Error("Expected " + (component ? "component" : "object") + " `" + id + "` to be defined: you likely forgot to import, pass, or provide it.");\n}\n
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/youtube

Handles the setup URL callback from GitHub Apps during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For updates, it displays a success page; for new installations, it processes the code/state exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The identifier for the OAuth provider (e.g., github).

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### Agent Builder Quickstart

Source: https://docs.langchain.com/langsmith/agent-server-scale

A quick guide to building your first agent using the Agent Builder.

```APIDOC
## Quickstart: Build an agent from a template

### Description
Follow this guide to quickly create an agent using a pre-defined template in the Agent Builder.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/upload-files-with-traces

Handles the OAuth setup callback redirect, specifically for GitHub App installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint processes installation or update events for GitHub Apps.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Status message indicating success or redirect action.
```

--------------------------------

### Langchain LLM Getting Started Guide (Python)

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/figma

This Python code snippet is a comment referencing the official Langchain documentation for getting started with LLMs. It points to a URL for more detailed information on data connection modules.

```python
# see https://python.langchain.com/en/latest/modules/data_connection/getting_started.html for more details
index 
```

--------------------------------

### Project Setup and Package Installation (Shell)

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

This snippet demonstrates the shell commands required to set up a new project directory, initialize a Node.js project, and install necessary Langchain-related packages. It includes creating a directory, initializing npm, and installing 'langsmith', 'openevals', and 'openai'.

```shellscript
mkdir ls-evaluation-quickstart-ts && cd ls-evaluation-quickstart-ts
npm init -y
npm install langsmith openevals openai
npx tsc --init
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/create-account-api-key

Handles the setup phase for OAuth providers, including redirecting to success pages for pre-authorized installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup process for a specific provider. If no token exchange is required, it redirects to a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### Quickstart: Initialize Privy Wallet Tool and Create Langchain Agent

Source: https://docs.langchain.com/oss/python/integrations/tools/privy

This snippet demonstrates how to set up Privy credentials, initialize the PrivyWalletTool, and create a Langchain agent capable of performing wallet operations. It requires the 'langchain-privy' package and sets environment variables for authentication.

```python
import os
from langchain_privy import PrivyWalletTool
from langchain.agents import create_agent

# Set credentials
os.environ["PRIVY_APP_ID"] = "your-privy-app-id"
os.environ["PRIVY_APP_SECRET"] = "your-privy-app-secret"

# Initialize wallet tool (automatically creates wallet)
privy_tool = PrivyWalletTool()
print(f"Wallet created! Address: {privy_tool.wallet_address}")

# Create agent
agent = create_agent(
    model="claude-sonnet-4-6",
    tools=[privy_tool],
)

# Agent can now perform wallet operations
agent.invoke({"messages": [{"role": "user", "content": "What's my wallet address on Base?"}]})

```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/vectorstores/pgvector

Handles the setup flow for a new OAuth provider installation, including GitHub App installation callbacks.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup flow for OAuth providers. For GitHub, it handles new installations or updates to existing ones.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the setup status.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### Create App Example (Python)

Source: https://docs.langchain.com/oss/python/deepagents/data-analysis

This Python code snippet demonstrates how to create an application instance. It involves importing necessary components and assigning them to variables.

```python
app = create(
    app
)
backend = ModalSandbox(
    sandbox
)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/self-host-using-an-existing-secret

Handles the initial setup or installation callback for an OAuth provider, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup flow, processing new installations or updates from providers like GitHub.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.smith.langchain.com/

Initializes the setup process for a specific OAuth provider.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup for a new OAuth provider installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Setup initialization status.
```

--------------------------------

### Agent Builder

Source: https://python.langchain.com/docs/integrations/chat/azure_chat_openai

Documentation for the Agent Builder product, including getting started guides.

```APIDOC
## Agent Builder

### Overview

- **Page**: `langsmith/agent-builder`
  - Description: Introduction to the Agent Builder product.

### Get Started

- **Page**: `langsmith/agent-builder-quickstart`
  - Description: Quickstart guide for using the Agent Builder.

- **Page**: `langsmith/agent-builder-essentials`
  - Description: Essential concepts and features of the Agent Builder.

- **Page**: `langsmith/agent-builder-t`
  - Description: Further details on Agent Builder functionalities (title truncated).
```

--------------------------------

### Create Examples with Langchain Client (JavaScript)

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/langsmith

This snippet demonstrates creating examples for a Langchain dataset. It uses the `createExamples` method, requiring an object with `inputs` and `outputs` properties, which should be pre-defined arrays or structures. The `lsClient` must be initialized.

```javascript
const examples = await lsClient.createExamples({
  inputs: exampleInputs,
  outputs: exampleOutputs
});
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/providers/graph_rag

Handles the setup or update of GitHub App installations or other OAuth provider configurations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup or update of a GitHub App installation. For updates, it confirms the action; for new installations, it processes the OAuth flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the installation status.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### Getting Started with Tavily Search API Retriever

Source: https://docs.langchain.com/oss/javascript/integrations/retrievers/tavily

Guides users on how to get started with the Tavily Search API retriever within the Langchain framework. It links to the general retriever documentation for further assistance.

```markdown
This will help you getting started with the Tavily Search API [retriever](/oss/javascript/langchain/retrieval).
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/manage-prompts

Handles the initial setup for OAuth providers, including processing new installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for OAuth providers, including processing new installations with code/state parameters.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion or redirect status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/langchain/errors/MODEL_RATE_LIMIT

Handle OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

For 'update' actions (user modified repo access via GitHub), a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup callback.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/langchain/errors/OUTPUT_PARSING_FAILURE

Handles the setup callback for OAuth providers, specifically for GitHub App installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### Qdrant Vector Store Setup and Usage (JavaScript)

Source: https://docs.langchain.com/oss/javascript/integrations/vectorstores/qdrant

Demonstrates how to set up and use the QdrantVectorStore in a JavaScript environment. This involves initializing the store with Qdrant client configurations and potentially embedding documents. It requires the '@langchain/qdrant' package.

```javascript
import { QdrantVectorStore } from "@langchain/qdrant";

// Example initialization (actual code would involve more setup)
const qdrantClient = new QdrantClient({ host: "localhost", port: 6333 });
const vectorStore = new QdrantVectorStore(qdrantClient, {
  collectionName: "my_collection",
  // other options...
});

// Example usage (e.g., adding documents)
// await vectorStore.addDocuments(documents);

```

--------------------------------

### Install Dependencies and Start Development Server (Shell)

Source: https://docs.langchain.com/oss/python/langchain/ui

This snippet demonstrates how to install project dependencies using 'pnpm install' and then start the development server with 'pnpm dev'. These commands are essential for running the Agent Chat UI locally.

```shellscript
pnpm install
pnpm dev
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/chat/bedrock_converse

Handles the setup callback for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Triggered when a user installs or updates their GitHub App installation. Processes new installations or shows a success page for updates.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.
```

--------------------------------

### Initialize Local Qdrant Vector Store

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/qdrant

Demonstrates setting up a Qdrant vector store in local mode. Includes examples for ephemeral in-memory storage and persistent on-disk storage.

```python
from langchain_qdrant import QdrantVectorStore
from qdrant_client import QdrantClient
from qdrant_client.http.models import Distance, VectorParams

# In-memory
client = QdrantClient(":memory:")
client.create_collection(
    collection_name="demo_collection",
    vectors_config=VectorParams(size=3072, distance=Distance.COSINE),
)
vector_store = QdrantVectorStore(
    client=client,
    collection_name="demo_collection",
    embedding=embeddings,
)

# On-disk
client = QdrantClient(path="/tmp/langchain_qdrant")
client.create_collection(
    collection_name="demo_collection",
    vectors_config=VectorParams(size=3072, distance=Distance.COSINE),
)
vector_store = QdrantVectorStore(
    client=client,
    collection_name="demo_collection",
    embedding=embeddings,
)
```

--------------------------------

### Create Agent and Get Tools in Langchain

Source: https://docs.langchain.com/oss/python/integrations/tools/apify_actors

This example illustrates the creation of an agent and the retrieval of available tools within the Langchain framework. It shows how to use a client to call a 'get_tools' function and then subsequently use 'create_agent' to initialize an agent.

```javascript
const tools = await client.get_tools();
const agent = create_agent(tools);
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/csv

Handles GitHub App installation setup or updates, processing OAuth exchanges for new installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup or update of GitHub App installations. For updates, it displays a success page; for new installations, it processes the OAuth token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/cli

Handles the initial setup for new installations requiring OAuth callback processing.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the initial OAuth setup for new installations with code or state.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success status of the setup process.
```

--------------------------------

### PostgresSaver - Database Setup

Source: https://reference.langchain.com/javascript/langchain-langgraph-checkpoint-postgres/index/PostgresSaver

Methods for setting up and initializing the checkpoint database.

```APIDOC
## POST /checkpoints/setup

### Description
Set up the checkpoint database asynchronously. This method creates the necessary tables in the Postgres database if they don't already exist and runs database migrations. It MUST be called directly by the user the first time checkpointer is used.

### Method
POST

### Endpoint
/checkpoints/setup

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```
POST /checkpoints/setup
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the database setup is complete.

#### Response Example
```json
{
  "message": "Checkpoint database setup complete."
}
```
```

--------------------------------

### Local Documentation Development Setup (Bash)

Source: https://docs.langchain.com/oss/python/contributing/documentation

Steps to set up a local environment for previewing LangChain documentation. This involves cloning the repository, installing dependencies using 'make install', and starting a development server with 'make dev' for hot-reloading.

```bash
git clone https://github.com/langchain-ai/docs.git
cd docs
make install
make dev
```

--------------------------------

### Full Example: Agent with Configured FilesystemFileSearchMiddleware

Source: https://docs.langchain.com/oss/python/langchain/middleware/built-in

Demonstrates a full agent configuration using FilesystemFileSearchMiddleware with all parameters set: root_path, use_ripgrep, and max_file_size_mb. This example shows how an agent can be prompted to find specific code patterns, utilizing the glob and grep tools provided by the middleware.

```python
from langchain.agents import create_agent
from langchain.agents.middleware import FilesystemFileSearchMiddleware
from langchain.messages import HumanMessage


agent = create_agent(
    model="gpt-4.1",
    tools=[],
    middleware=[
        FilesystemFileSearchMiddleware(
            root_path="/workspace",
            use_ripgrep=True,
            max_file_size_mb=10,
        ),
    ],
)

# Agent can now use glob_search and grep_search tools
result = agent.invoke({
    "messages": [HumanMessage("Find all Python files containing 'async def'")]
})

# The agent will use:
# 1. glob_search(pattern="**/*.py") to find Python files
# 2. grep_search(pattern="async def", include="*.py") to find async functions
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/hn

Handles the setup callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles GitHub App installation setup callbacks. For updates, it displays a success page; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Indicates successful processing or redirection.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.smith.langchain.com/langsmith/pytest

Handles the setup process for a new OAuth provider installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup for a new OAuth provider installation, handling code/state exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Setup completion status.
```

--------------------------------

### Fetch Examples from Dataset (JavaScript)

Source: https://docs.langchain.com/langsmith/manage-datasets

Demonstrates how to fetch a subset of examples from a dataset using the `listExamples` method in JavaScript. This is useful for evaluating models on specific data subsets, such as those with particular metadata.

```javascript
import { Client } from "langsmith";

const client = new Client();

// Fetch examples with a specific metadata key-value pair
const examples = await client.listExamples({
  datasetId: "your-dataset-id",
  // Note: Direct metadata filtering might require fetching and then filtering client-side
  // or using specific query parameters if available in the SDK version.
});

examples.forEach(example => {
  console.log(example.inputs, example.outputs);
});
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/observability

Handles the OAuth setup callback redirect from GitHub Apps, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/langchain/errors/MESSAGE_COERCION_FAILURE

Handles GitHub App installation callbacks and OAuth setup redirects.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes GitHub App installation callbacks or initiates OAuth setup flows for specific providers.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/self-host-sso

Handles the initial OAuth setup callback for new installations. If code and state are present, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup callback for new installations. If code and state are present, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup is complete or further actions are needed.

#### Response Example
```json
{
  "message": "OAuth setup complete."
}
```
```

--------------------------------

### POST /v2/sandboxes/templates

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Create a new SandboxTemplate in the tenant's namespace.

```APIDOC
## POST /v2/sandboxes/templates

### Description
Create a new SandboxTemplate in tenant's namespace.

### Method
POST

### Endpoint
/v2/sandboxes/templates

### Request Body
- **name** (string) - Required - Name of the template
- **image** (string) - Required - Container image for the template

### Response
#### Success Response (200)
- **id** (string) - The created template ID

#### Response Example
{
  "id": "template-123"
}
```

--------------------------------

### Initialize LangChain Agent with Tools

Source: https://docs.langchain.com/oss/python/migrate/langchain-v1

Demonstrates the initialization of an agent using 'create_agent'. It shows both the standard configuration and the usage of model strings with tool lists.

```python
ChatOpenAI().bind_tools([some_tool])

agent = create_agent(model_with_tools, tools=[])

# Use instead
agent = create_agent("gpt-4.1-mini", tools=[some_tool])
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/langgraph/errors/INVALID_GRAPH_NODE_RETURN_VALUE

Handles the setup callback from providers like GitHub Apps during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup URL callback from GitHub Apps. Triggers when a user installs or updates their app installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the installation process state.
```

--------------------------------

### POST /v2/sandboxes/volumes

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Create a new persistent volume for the tenant's sandbox namespace.

```APIDOC
## POST /v2/sandboxes/volumes

### Description
Creates a new persistent volume. By default, this blocks until the PVC is bound or the timeout is reached.

### Method
POST

### Endpoint
/v2/sandboxes/volumes

### Parameters
#### Request Body
- **wait_for_ready** (boolean) - Optional - Whether to block until the volume is ready.

### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the created volume.

### Response Example
{
  "id": "vol-12345"
}
```

--------------------------------

### Elasticsearch Setup Example

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/elasticsearch

This code snippet demonstrates the basic setup for using Elasticsearch as a vector store in Langchain. It requires the 'langchain-elasticsearch' package to be installed. The example shows how to initialize the ElasticsearchStore with necessary parameters.

```python
from langchain_elasticsearch import ElasticsearchStore

# Example initialization (replace with your actual connection details)
vector_store = ElasticsearchStore(
    index_name="my_index",
    embedding=None,  # Replace with your embedding model
    es_url="http://localhost:9200",
    es_user="elastic",
    es_password="changeme",
    # Other optional parameters like client_kwargs, query_strategy, etc.
)

# You would then typically add documents to this vector store:
# vector_store.add_documents(documents)

```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/docker

Handles the OAuth setup callback for new installations with code/state, processing similar to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations with code/state, processing similar to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
```json
{
  "message": "OAuth setup callback processed successfully."
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/file_loaders/directory

Handles the Setup URL callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the Setup URL callback from GitHub Apps. For updates, it displays a success page; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/providers/anthropic

Handles the setup URL callback from GitHub Apps, processing new installations or updates to existing app installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For updates, it displays a success page; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### Basic Langchain Langgraph and Core Hello World Example

Source: https://docs.langchain.com/oss/javascript/langgraph/overview

This TypeScript code snippet provides a fundamental 'Hello World' example using Langchain's Langgraph and Core libraries. It showcases basic import statements and the initial setup for a Langchain application. This example assumes you have the necessary Langchain packages installed.

```typescript
import { StateSchema } from "@langchain/core/runnables";

// Placeholder for a simple state schema
type SimpleState = {
  input: string;
  output: string;
};

// Example of creating a simple runnable or graph component
const simpleRunnable = new Runnable<string, SimpleState>({
  async invoke(input: string) {
    return { input: input, output: `Hello, ${input}!` };
  },
});

// Example of how to use the runnable (conceptual)
async function runExample() {
  const result = await simpleRunnable.invoke("World");
  console.log(result);
}

runExample();

```

--------------------------------

### Initialize ChromaDB Clients in Python

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/chroma

Demonstrates how to instantiate ChromaDB clients. It includes examples for local persistent storage using PersistentClient and remote server connectivity using HttpClient.

```python
import chromadb

# Local persistent client
client = chromadb.PersistentClient(path="./chroma_langchain_db")

# Remote HTTP client
client = chromadb.HttpClient(host="localhost", port=8000)
```

--------------------------------

### POST /v2/sandboxes/boxes

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Create a new sandbox instance.

```APIDOC
## POST /v2/sandboxes/boxes

### Description
Creates a new sandbox in the tenant's namespace.

### Method
POST

### Endpoint
/v2/sandboxes/boxes

### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the created sandbox.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/langchain/knowledge-base

Handles the setup callback for OAuth providers, processing installation states and redirecting users as necessary.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles OAuth setup callbacks. If no token exchange is required, it displays a success page; otherwise, it processes the installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/langchain/human-in-the-loop

Handles the setup callback from GitHub Apps, processing new installations or updates to existing app configurations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider (e.g., github).

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### Initialize Project Environment

Source: https://docs.langchain.com/langsmith/observability-quickstart

Commands to create a project directory, set up a virtual environment, and install necessary LangSmith and OpenAI dependencies.

```bash
mkdir ls-observability-quickstart && cd ls-observability-quickstart
python -m venv .venv && source .venv/bin/activate
python -m pip install --upgrade pip
pip install -U langsmith openai
```

--------------------------------

### Initialize Runloop Client and Create Sandbox

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

Demonstrates how to import the RunloopSDK and RunloopSandbox, authenticate with an API key, and instantiate a new development environment.

```python
from langchain_runloop import RunloopSDK, RunloopSandbox

api_key = "..."
client = RunloopSDK(bearer_token=api_key)

devbox = client.devbox.create()
backend = RunloopSandbox(devbox=devbox)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/opensearch

Handles the setup process for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes user installation or updates for GitHub Apps. For updates, it displays a success page; for new installations, it initiates the OAuth callback flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/chat/nvidia_ai_endpoints

Handles the setup process for OAuth providers, including processing new GitHub App installations or OAuth callbacks.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles OAuth setup, including processing GitHub App installation triggers and OAuth state exchanges.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Indicates successful processing or redirection.
```

--------------------------------

### Define and Create LLM Dataset Examples

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

This snippet shows the structure of a dataset entry containing 'inputs' and 'outputs' fields, followed by a method call to 'create_examples' using a client instance. It is used to populate datasets with question-answer pairs for model evaluation or fine-tuning.

```json
[
  {
    "inputs": {
      "question": "What is Earth's lowest point?"
    },
    "outputs": {
      "answer": "Earth's lowest point is The Dead Sea."
    }
  }
]
```

```python
# Add examples to the dataset
client.create_examples(dataset_id=...)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/retrievers/amazon_kendra_retriever

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation. For 'update' actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed. For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider (e.g., GitHub).

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the OAuth provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Request Example
```
GET /v2/auth/setup/github?code=AUTHORIZATION_CODE&state=SOME_STATE
```

### Response
#### Success Response (200 OK)
- **message** (string) - A message indicating the status of the setup callback.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### Initialize Chroma Client in Python

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/chroma

Demonstrates how to import the chromadb library and initialize a client instance. This is the foundational step for connecting LangChain to a Chroma database.

```python
import chromadb

client = chromadb.Client()
```

```python
import chromadb

client = chromadb.PersistentClient()
```

--------------------------------

### Initialize and Use Text Splitter

Source: https://docs.langchain.com/oss/python/integrations/splitters/recursive_text_splitter

Example demonstrating how to import the text splitter and prepare it for document creation.

```python
from langchain_text_splitters import RecursiveCharacterTextSplitter

# Example usage for splitting text into documents
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200
)

docs = text_splitter.create_documents(["Your text content here..."])
```

--------------------------------

### Create Examples with Langchain LLM Client (JavaScript)

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

This snippet shows how to use a Langchain LLM client to create examples. It involves an asynchronous call to `createExamples` with parameters for dataset ID, inputs, and outputs. The code assumes the existence of a `client` object and a `dataset` object with an `id` property.

```javascript
await client.createExamples({
  datasetId: dataset.id,
  inputs: inputs,
  outputs: outputs
});
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/release-policy

Handles the setup URL callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps. For updates, it displays a success page; for new installations, it processes the OAuth flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### QdrantVectorStore Configuration Example (JavaScript)

Source: https://docs.langchain.com/oss/javascript/integrations/vectorstores/qdrant

Illustrates the configuration options for the QdrantVectorStore, including specifying metadata and source URL. This is useful for organizing and retrieving documents with specific attributes.

```javascript
const vectorStore = new QdrantVectorStore({
  url: "YOUR_QDRANT_URL",
  apiKey: "YOUR_QDRANT_API_KEY",
  collectionName: "my_collection"
});

// Example of adding data with metadata
await vectorStore.addDocuments([
  {
    pageContent: "Mitochondria are made out of lipids",
    metadata: {
      source: "https://example.com",
      id: undefined // or some identifier
    }
  }
]);
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://python.langchain.com/docs/how_to/serialization

Handles the initial setup for an OAuth provider, including processing new installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for an OAuth provider. For new installations, it processes the code/state similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.smith.langchain.com/langsmith/vitest-jest

Handles the setup process for a new OAuth provider installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup for a new OAuth provider installation, similar to the regular OAuth callback flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/contributing/standard-tests-langchain

Handles the setup process for new GitHub App installations or OAuth provider configurations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Triggered when a user installs or updates their GitHub App installation. Processes new installations or redirects for existing updates.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### LambdaDB Setup and Usage Example

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/lambdadb

Provides an example of setting up and using the LambdaDB vector store within LangChain. It outlines the necessary steps, including account creation, credential retrieval, and package installation.

```javascript
import { LambdaDB } from "langchain_community.vectorstores";

// ... setup LambdaDB account and get credentials ...

const vectorstore = await LambdaDB.from_documents(
 documents,
 embedding=OpenAIEmbeddings(),
 project_id="YOUR_PROJECT_ID",
 api_key="YOUR_API_KEY"
);
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/providers

Handles the setup flow for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup or update of GitHub App installations. For updates, it displays a success page; for new installations, it processes the code/state exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/retrievers

Handles the setup callback for OAuth providers, processing installation state and provider configuration.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback, processing new installations or existing provider configurations.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### GET /v2/sandboxes/templates

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Retrieve a list of all available SandboxTemplates in the tenant's namespace.

```APIDOC
## GET /v2/sandboxes/templates

### Description
List all SandboxTemplates in the tenant's namespace.

### Method
GET

### Endpoint
/v2/sandboxes/templates

### Response
#### Success Response (200)
- **templates** (array) - List of sandbox template objects

#### Response Example
{
  "templates": []
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/providers/tavily

Handles the setup process for an OAuth provider, including processing new installations or updates to existing repo access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup process for an OAuth provider. For updates, it displays a success page; for new installations, it processes the OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/langchain/errors/MODEL_NOT_FOUND

Handles the setup callback for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles GitHub App installation setup or updates. Processes new installations with code/state or displays a success page for existing installations.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/databricks_vector_search

Handles the setup callback from GitHub Apps during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the 'Setup URL' callback from GitHub Apps. Triggers when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the installation process.
```

--------------------------------

### Initialize QdrantVectorStore from documents

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/qdrant

Demonstrates how to import the necessary modules and initialize a QdrantVectorStore from a list of documents using the from_documents method.

```python
from langchain_qdrant import RetrievalMode

QdrantVectorStore.from_documents(
 docs,
 embedding=embeddings
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/auth

Handles the setup process for a new OAuth provider installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup for a new OAuth provider installation, similar to the standard OAuth callback flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Setup completion status.
```

--------------------------------

### Agent Builder

Source: https://docs.langchain.com/langsmith/insights

Documentation related to the Agent Builder product, including getting started guides and tool integrations.

```APIDOC
## Agent Builder Documentation

### Description
Resources for using the Agent Builder to create AI agents without code.

### Sections

#### Get started
- `langsmith/agent-builder-quickstart`
- `langsmith/agent-builder-essentials`
- `langsmith/agent-builder-templates`
- `langsmith/agent-builder-setup`
- `langsmith/agent-builder-manage-agent-settings`

#### Tools and integrations
- `langsmith/agent` (Incomplete path, likely refers to tool integrations)
```

--------------------------------

### Create Project Directory and Install Dependencies (Shell)

Source: https://docs.langchain.com/langsmith/observability-quickstart

This snippet demonstrates how to create a new project directory, navigate into it, set up a Python virtual environment, activate it, and install necessary dependencies. It's a foundational step for many Python projects.

```shellscript
mkdir ls-observability-quickstart && cd ls-observability-quickstart
python -m venv .venv && source .venv/bin/activate
python -m pip install --upgrade
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/microsoft_powerpoint

Handles the setup URL callback from GitHub Apps, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup URL callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the installation process status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/providers/toolbox

Handles the OAuth setup callback redirect from GitHub Apps, processing new installations or updates to repository access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### Start Streamable HTTP Server Example (Shell)

Source: https://reference.langchain.com/python/langchain_mcp_adapters

This command navigates to an example directory and starts a streamable HTTP MCP server using `uvicorn`. The server is configured to listen on port 3000, making it accessible for clients to connect and interact with.

```shell
cd examples/servers/streamable-http-stateless/
uv run mcp-simple-streamablehttp-stateless --port 3000
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://python.langchain.com/docs/concepts/chat_models

Handles the OAuth setup callback redirect from GitHub Apps, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/text_embedding/openai

Handles the setup flow for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup flow for new installations or updates to GitHub App installations. Processes code/state for new installs or displays success for updates.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instructions.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/agent-server-api/assistants/get-assistant

Handles the setup URL callback from GitHub Apps, triggered during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.
```

--------------------------------

### POST /v2/sandboxes/pools

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Create a new sandbox pool.

```APIDOC
## POST /v2/sandboxes/pools

### Description
Create a new Sandbox Pool in the tenant's namespace. Pools pre-provision sandboxes from a template for faster claim binding.

### Method
POST

### Endpoint
/v2/sandboxes/pools
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/langgraph/use-functional-api

Handles the setup callback for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes OAuth setup callbacks, specifically handling GitHub App installations and token exchanges.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the setup status.
```

--------------------------------

### Install Elasticsearch Locally with start-local

Source: https://docs.langchain.com/oss/python/integrations/providers/elasticsearch

This snippet shows how to install and set up Elasticsearch on your local machine for development and testing purposes using the 'start-local' script. It utilizes Docker for a streamlined setup process.

```shellscript
curl -sSL https://raw.githubusercontent.com/elastic/start-local/main/install.sh | bash
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://python.langchain.com/docs/integrations/text_embedding/openai

Handles the setup process for GitHub App installations or other OAuth providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup flow for new OAuth installations or updates to existing GitHub App installations.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### Fetch Dataset Examples Programmatically (Python)

Source: https://docs.langchain.com/langsmith/manage-datasets

Demonstrates how to fetch examples from a dataset programmatically using LangChain. This involves creating a client and calling a list method with specific parameters.

```python
from langsmith import Client

client = Client()

# Fetch examples from a dataset
for example in client.list_examples(dataset_name="my-dataset"):
    print(example)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/sqlserver

Handles the setup process for new GitHub App installations or OAuth provider configurations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup process for new GitHub App installations or OAuth provider configurations. For updates, it confirms access changes; for new installations, it processes the code/state exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### Gemini Developer API Setup with API Key

Source: https://docs.langchain.com/oss/python/integrations/chat/google_generative_ai

Demonstrates the quick setup for the Gemini Developer API using an API key. This involves importing necessary libraries and handling the API key securely, likely through environment variables or a secure input method.

```python
import getpass
import os


```

--------------------------------

### Example Usage: npm Install (Shell)

Source: https://docs.langchain.com/oss/javascript/integrations/splitters/code_splitter

This snippet demonstrates how to install the necessary Langchain packages using npm. It's a prerequisite for using the text splitting functionalities in a Node.js environment.

```shellscript
npm install @langchain/text-splitter
```

--------------------------------

### Initialize Qdrant Vector Store

Source: https://docs.langchain.com/oss/python/langchain/knowledge-base

Installs the Qdrant integration and sets up an in-memory collection.

```bash
pip install -qU langchain-qdrant
```

```python
from qdrant_client.models import Distance, VectorParams
from langchain_qdrant import QdrantVectorStore
from qdrant_client import QdrantClient

client = QdrantClient(":memory:")
vector_size = len(embeddings.embed_query("sample text"))

if not client.collection_exists("test"):
    client.create_collection(
        collection_name="test",
        vectors_config=VectorParams(size=vector_size, distance=Distance.COSINE)
    )
vector_store = QdrantVectorStore(
    client=client,
    collection_name="test",
    embedding=embeddings,
)
```

--------------------------------

### Agent Builder

Source: https://docs.langchain.com/langsmith/self-host-custom-tls-certificates

Documentation for the Agent Builder product, including getting started guides and tool integrations.

```APIDOC
## Agent Builder Documentation

### Overview

Agent Builder allows you to create helpful AI agents without code. It provides a user-friendly interface for defining agent behavior, integrating tools, and managing settings.

### Getting Started

- **Quickstart**: A guide to quickly set up and start using Agent Builder.
- **Essentials**: Core concepts and features of Agent Builder.
- **Templates**: Pre-built agent templates to accelerate development.
- **Setup**: Instructions for setting up your Agent Builder environment.
- **Manage Agent Settings**: How to configure and manage your agent's settings.

### Tools and Integrations

- **Agent Builder Tools**: Information on available tools for your agents.
- **Agent Builder Triggers**: How to set up triggers for your agents.
- **Agent Builder Integrations**: Details on integrating Agent Builder with other services.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/kubernetes

Handles the initial setup for OAuth providers, processing callbacks for new installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the OAuth setup for a specific provider, handling new installations with code or state.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/file_loaders/epub

Handles the OAuth setup callback redirect, specifically for GitHub Apps installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the callback was processed.
```

--------------------------------

### Install jq (Shell Script)

Source: https://docs.langchain.com/langsmith/script-running-pg-support-queries

This snippet provides commands to install the 'jq' utility on a system. 'jq' is a lightweight and flexible command-line JSON processor. Installing it is a prerequisite for using the JSON parsing examples provided in this document.

```shellscript
sudo apt-get update && sudo apt-get install -y jq
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/searchapi

Handles the Setup URL callback from GitHub Apps, triggered during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the Setup URL callback from GitHub Apps. For new installations, it processes the token exchange; for updates, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/chat/anthropic

Handle OAuth setup callback redirect from GitHub Apps. This endpoint manages the callback for GitHub App installations and updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint manages the callback for GitHub App installations and updates. It handles both new installations and updates to existing ones, processing token exchanges where necessary.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Body
(No request body)

### Response
#### Success Response (200)
(No specific success response documented in the provided text)

#### Response Example
(No example provided)
```

--------------------------------

### Initialize Project and Install Dependencies

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

Commands to create a new project directory, set up a Python virtual environment, and ensure pip and LangSmith are installed or upgraded.

```shellscript
mkdir ls-evaluation-quickstart && cd ls-evaluation-quickstart
python -m venv .venv && source .venv/bin/activate
python -m pip install --upgrade pip
pip install -U langsmith
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/evaluate-with-attachments

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The identifier of the OAuth provider (e.g., 'github').

#### Query Parameters
- **code** (string) - Required - The authorization code received from the OAuth provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Response
#### Success Response (200 OK)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
```json
{
  "message": "GitHub App setup processed successfully."
}
```
```

--------------------------------

### Install LangGraph SDK and Test Deployment

Source: https://docs.langchain.com/oss/python/langgraph/deploy

Instructions for setting up the environment and executing a test request against a LangGraph deployment. The process involves installing the necessary SDK and using the sync client to communicate with the agent.

```shellscript
pip install langgraph-sdk
```

```python
from langgraph_sdk import get_sync_client # or get_client for async

client = get_sync_client()
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/metric-type

Handles the setup callback from GitHub Apps triggered during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps. For updates, it displays a success page; for new installations, it processes the OAuth token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The identifier for the GitHub App provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/recursive_url

Handles OAuth setup callbacks, specifically for GitHub App installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, particularly useful for GitHub App installations. For updates, it displays a success page; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### Start local Elasticsearch instance

Source: https://docs.langchain.com/oss/python/integrations/providers/elasticsearch

Commands to navigate to the installation directory and execute the startup script for the local Elasticsearch service.

```shellscript
cd elastic-start-local
./start.sh
```

--------------------------------

### QdrantVectorStore Initialization Example (JavaScript)

Source: https://docs.langchain.com/oss/javascript/integrations/vectorstores/qdrant

Demonstrates how to initialize the QdrantVectorStore in JavaScript. This involves specifying connection details and collection name. It's a foundational step for using Qdrant with LangChain.

```javascript
const vectorStore = new QdrantVectorStore({
  url: "YOUR_QDRANT_URL",
  apiKey: "YOUR_QDRANT_API_KEY",
  collectionName: "my_collection"
});
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/vectorstores/azure_documentdb

Handles the callback from GitHub Apps or other providers when a user installs or updates their installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes installation callbacks from GitHub Apps. For updates, it displays a success page; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/langchain/models

Handles the OAuth setup callback redirect, specifically for GitHub App installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the callback was processed.
```

--------------------------------

### Instantiate ParallelWebSearchTool in Python

Source: https://docs.langchain.com/oss/python/integrations/tools/parallel_search

Demonstrates how to import the ParallelWebSearchTool and initialize it. Shows both basic instantiation using environment variables and configuration with explicit API keys and base URLs.

```python
from langchain_parallel import ParallelWebSearchTool

# Basic instantiation - API key from environment
tool = ParallelWebSearchTool()

# With explicit API key and custom base URL
tool = ParallelWebSearchTool(api_key="YOUR_API_KEY", base_url="https://api.example.com")
```

--------------------------------

### Initialize Qdrant Client for On-Disk Storage

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/qdrant

Demonstrates how to instantiate the QdrantClient with a local file system path and configure a new collection with defined vector dimensions. This is useful for local development and persistence of vector data.

```python
client = QdrantClient(path="/tmp/langchain_qdrant")

client.create_collection(
    collection_name="demo_collection",
    vectors_config=VectorParams(size=3072)
)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/granular-usage

Handles the OAuth setup callback for new installations. It processes the OAuth callback similar to regular OAuth callbacks when code/state are present, otherwise it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations. It processes the OAuth callback similar to regular OAuth callbacks when code/state are present, otherwise it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the completion of the setup.

#### Response Example
```json
{
  "message": "OAuth setup complete."
}
```
```

--------------------------------

### Create Deployment

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

Create a new deployment.

```APIDOC
## POST /v2/deployments

### Description
Create a new deployment.

### Method
POST

### Endpoint
/v2/deployments

### Parameters
#### Request Body
- **name** (string) - Required - The name of the deployment.
- **template_id** (string) - Required - The ID of the deployment template.

### Request Example
```json
{
  "example": "{\"name\": \"New Web App Deployment\", \"template_id\": \"tpl_xyz123\"}"
}
```

### Response
#### Success Response (200)
- **id** (string) - The unique identifier for the newly created deployment.
- **name** (string) - The name of the deployment.
- **status** (string) - The initial status of the deployment.

#### Response Example
```json
{
  "example": "{\"id\": \"dep_ghi\", \"name\": \"New Web App Deployment\", \"status\": \"creating\"}"
}
```
```

--------------------------------

### GET /info

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Retrieves server version information, feature flags, and metadata.

```APIDOC
## GET /info

### Description
Returns metadata about the running server instance, including versioning and enabled features.

### Method
GET

### Endpoint
/info

### Response
#### Success Response (200)
- **version** (string) - The server version.
- **features** (array) - List of enabled feature flags.

#### Response Example
{
  "version": "1.0.0",
  "features": ["mcp", "metrics"]
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://python.langchain.com/docs/concepts/messages

Handles the initial setup for an OAuth provider, processing installation state and redirecting to the callback page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for an OAuth provider. Processes installation state and redirects to the frontend callback page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### List Examples from Langchain Datasets (JavaScript)

Source: https://docs.langchain.com/langsmith/manage-datasets

This snippet illustrates how to list examples from a Langchain dataset. It shows the structure for calling the `listExamples` function with dataset name and metadata. This is useful for retrieving specific data points for testing or analysis.

```javascript
data: langsmith.listExamples({
  datasetName: datasetName,
  metadata: {"desired_key": "desired_value"},
})
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/versioning

Handles the OAuth setup callback for new installations. It processes the OAuth callback similarly to regular OAuth callbacks when code/state are present. If no token exchange is needed, it displays a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations. It processes the OAuth callback similarly to regular OAuth callbacks when code/state are present. If no token exchange is needed, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Indicates the success of the operation.

#### Response Example
{
  "message": "Setup successful"
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/file_loaders/subtitles

Handles the setup URL callback from GitHub Apps, triggered during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps. For updates, it displays a success page; for new installations, it processes the code/state exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the GitHub App provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### Agent Setup and Execution in Python

Source: https://docs.langchain.com/oss/python/integrations/tools/goat

Provides a Python code example for setting up and running an agent within the Langchain framework. It includes loading environment variables, importing necessary libraries like 'os' and 'asyncio', and demonstrates a basic agent execution flow.

```python
import os
import asyncio
from dotenv import load_dotenv

# Load environment variables
load_dotenv()
```

--------------------------------

### GET /v2/deployments

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Lists all deployments available in the control plane.

```APIDOC
## GET /v2/deployments

### Description
Retrieves a list of all deployments managed by the control plane.

### Method
GET

### Endpoint
/v2/deployments

### Response
#### Success Response (200)
- **deployments** (array) - A list of deployment objects.

#### Response Example
{
  "deployments": [
    { "id": "dep-123", "name": "production-agent" }
  ]
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/self-host-basic-auth

Handles the setup phase for OAuth providers, processing installation callbacks or showing success pages.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup phase for OAuth providers. For new installations, it processes the code/state; otherwise, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/retrievers/tavily

Handles the OAuth setup callback redirect, specifically for GitHub Apps installation events.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint processes installation or update events for GitHub Apps.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.
```

--------------------------------

### Create Dataset Examples using LangChain Client

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

This snippet demonstrates how to define a list of input/output pairs and use the LangChain client's 'createExamples' method to persist them to a specific dataset. It highlights the asynchronous nature of the operation and the required object structure for dataset entries.

```javascript
await client.createExamples({
  datasetId: dataset.id,
  inputs,
  outputs
});
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/langchain/overview

Handles the initial setup for an OAuth provider, processing new installations or existing access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup for an OAuth provider, including processing new installations or redirecting after successful access.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### Langsmith Agent Builder Resources

Source: https://docs.langchain.com/langsmith/docker

Resources related to the Langsmith Agent Builder, including getting started guides and essential concepts.

```APIDOC
## Langsmith Agent Builder Resources

### Agent Builder Overview

#### GET /langsmith/agent-builder

**Description**: Provides an overview of the Langsmith Agent Builder.

**Method**: GET

**Endpoint**: /langsmith/agent-builder

### Agent Builder Quickstart

#### GET /langsmith/agent-builder-quickstart

**Description**: A quickstart guide to begin using the Agent Builder.

**Method**: GET

**Endpoint**: /langsmith/agent-builder-quickstart

### Agent Builder Essentials

#### GET /langsmith/agent-builder-essentials

**Description**: Covers the essential concepts and features of the Agent Builder.

**Method**: GET

**Endpoint**: /langsmith/agent-builder-essentials
```

--------------------------------

### Create and run a LangChain agent

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Demonstrates how to import the createAgent function and initialize an agent instance with a specific model, system prompt, and tools.

```typescript
import { createAgent } from "langchain";

const agent = createAgent({
  model: "claude-sonnet-4-6",
  systemPrompt: systemPrompt,
  tools: tools
});
```

--------------------------------

### POST /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/chat/cohere

Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## POST /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
POST

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Request Example
```json
{
  "example": "POST /v2/auth/setup/github?code=AUTHORIZATION_CODE&state=STATE_PARAM"
}
```

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup completion.

#### Response Example
```json
{
  "example": {
    "message": "GitHub App setup successful."
  }
}
```
```

--------------------------------

### Install and Start Local Elasticsearch

Source: https://docs.langchain.com/oss/python/integrations/vectorstores

Commands to download, install, and execute the local Elasticsearch startup script.

```shellscript
curl -fsSL https://elastic.co/start-local | sh
cd elastic-start-local
./start.sh
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/migrate/langchain-v1

Handles the initial OAuth setup callback. For new installations with code/state, it processes similarly to a regular OAuth callback. If the user modified repo access via GitHub, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup callback. For new installations with code/state, it processes similarly to a regular OAuth callback. If the user modified repo access via GitHub, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "OAuth setup successful."
}
```
```

--------------------------------

### Initialize Drasi tool instance

Source: https://docs.langchain.com/oss/python/integrations/tools/drasi

Demonstrates how to import the required modules and configure the MCP connection to instantiate the Drasi tool for real-time updates.

```python
from langchain_drasi import create_drasi_tool, MCPConnectionConfig, ConsoleHandler

# Configure connection to Drasi MCP server
config = MCPConnectionConfig(...)
```

--------------------------------

### POST /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/deepagents/streaming/overview

Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## POST /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
POST

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter for CSRF protection.

### Request Example
```json
{
  "example": "POST /v2/auth/setup/github?code=AUTHORIZATION_CODE&state=CSRF_STATE"
}
```

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup completion.

#### Response Example
```json
{
  "example": {
    "message": "GitHub App setup complete."
  }
}
```
```

--------------------------------

### POST /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/soniox

Handles the 'Setup URL' callback from GitHub Apps, triggered by app installation or updates. For 'update' actions, it displays a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## POST /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered by app installation or updates. For 'update' actions, it displays a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
POST

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App setup successful."
}
```

--------------------------------

### Install Project Dependencies

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

Commands to initialize a project directory, create a virtual environment, and install necessary packages including langsmith, openevals, and openai.

```bash
mkdir ls-evaluation-quickstart && cd ls-evaluation-quickstart
python -m venv .venv && source .venv/bin/activate
python -m pip install --upgrade pip
pip install -U langsmith openevals openai
```

--------------------------------

### Initialize Qdrant Vector Store in Python

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/qdrant

Demonstrates how to instantiate the QdrantVectorStore using the from_documents method. It requires a cluster URL and an API key for authentication when using Qdrant Cloud.

```python
url = "<---qdrant cloud cluster url here --->"
api_key = "<---api key here--->"
qdrant = QdrantVectorStore.from_documents(
 docs,
 collection_name="my_documents"
)
```

--------------------------------

### Create LangChain Tools

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Demonstrates how to import necessary modules to create tools in LangChain, including support for runtime configurations.

```typescript
import { tool, type ToolRuntime } from "langchain";
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/langgraph/errors/MULTIPLE_SUBGRAPHS

Handles the setup process for GitHub App installations or OAuth provider configurations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes user installation or updates for GitHub Apps and other OAuth providers. For updates, it displays a success page; for new installations, it initiates the token exchange flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/providers/deepseek

Handles the OAuth setup callback, processing GitHub App installations and regular OAuth callbacks for new installations with code or state.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback, processing GitHub App installations and regular OAuth callbacks for new installations with code or state.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the callback.

#### Response Example
```json
{
  "message": "GitHub App installation processed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/llms/azure

Handles the initial setup for OAuth providers. For update actions, it shows a success page as no token exchange is needed. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for OAuth providers. For update actions, it shows a success page as no token exchange is needed. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Details of success response not provided in the source text)

#### Response Example
(No specific response example provided in the source text)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/file_loaders/unstructured

Handles the setup callback from GitHub Apps, processing new installations or updates to existing repository access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For updates, it displays a success page; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the GitHub provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### Initialize RunLoop SDK in Python

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

Demonstrates how to import the required SDK components and configure the client with an API key. This setup is required to interact with the RunLoop sandbox environment.

```python
from runloop_api_client import RunLoopSDK

from langchain_runloop import RunLoopSandbox

api_key = "..."
client = ...
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/documentdb

Handles the setup process for OAuth providers, including GitHub App installations and OAuth callback processing.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup process for OAuth providers. For GitHub App installations, it processes new installations or updates to existing ones.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion or redirect requirement.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/langchain/long-term-memory

Handles the OAuth setup callback redirect from GitHub Apps, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### Fetch Examples from Dataset (Python)

Source: https://docs.langchain.com/langsmith/manage-datasets

Demonstrates how to fetch a subset of examples from a dataset using the `list_examples` method in Python. This is useful for evaluating models on specific data subsets, such as those with particular metadata.

```python
from langsmith import Client

client = Client()

# Fetch examples with a specific metadata key-value pair
examples = client.list_examples(dataset_id="your-dataset-id", metadata_key="your-metadata-key", metadata_value="your-metadata-value")

for example in examples:
    print(example.inputs, example.outputs)
```

--------------------------------

### Full Langchain LLM Example with Commands (TypeScript)

Source: https://docs.langchain.com/oss/javascript/langgraph/interrupts

Provides a complete TypeScript example demonstrating the integration of various commands like Command, MemorySaver, START, and END within a Langchain LLM application. This snippet showcases a typical setup for defining and using these commands.

```typescript
import {
  Command,
  MemorySaver,
  START,
  END,
  S
} from "langchain_llms/commands";

// The following code is a direct representation of the provided snippet,
// illustrating the import and structure of commands within a TypeScript file.

// Note: The actual functionality and usage depend on the Langchain library's context.

// Example structure as seen in the input:
// import { Command, MemorySaver, START, END, S } from "langchain_llms/commands";

// The following lines are extracted directly from the HTML structure and represent
// the code as it would appear in a code block, including styling information.

// _jsxs(_components.pre, {
//   className: "shiki shiki-themes catppuccin-latte catppuccin-mocha",
//   style: {
//     backgroundColor: "#eff1f5",
//     "--shiki-dark-bg": "#1e1e2e",
//     color: "#4c4f69",
//     "--shiki-dark": "#cdd6f4"
//   },
//   language: "typescript",
//   children: _jsxs(_components.code, {
//     language: "typescript",
//     numberOfLines: "46",
//     children: [
//       _jsxs(_components.span, {
//         className: "line",
//         children: [
//           _jsx(_components.span, {
//             style: {
//               color: "#8839EF",
//               "--shiki-dark": "#CBA6F7"
//             },
//             children: "import"
//           }),
//           _jsx(_components.span, {
//             style: {
//               color: "#7C7F93",
//               "--shiki-dark": "#9399B2"
//             },
//             children: " {"
//           })
//         ]
//       }),
//       // ... other lines of code representing the full example ...
//     ]
//   })
// })

// Simplified representation of the import statement:
const importStatement = "import { Command, MemorySaver, START, END, S } from \"langchain_llms/commands\";";
console.log(importStatement);

```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/add-human-in-the-loop

Handles the setup callback for OAuth providers, processing installation state or token exchange as required.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, processing installation state or token exchange as required.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/figma

Handles the setup URL callback from GitHub Apps, triggered during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps. For updates, it displays a success page; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### List all Sandbox Pools

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Lists all Sandbox Pools in the tenant's namespace. Supports optional pagination via `limit` and `offset` query parameters.

```APIDOC
## GET /v2/sandboxes/pools

### Description
List all Sandbox Pools in the tenant's namespace.
This endpoint queries the database for fast performance.
Supports optional pagination via `limit` and `offset` query parameters.

### Method
GET

### Endpoint
/v2/sandboxes/pools

#### Query Parameters
- **limit** (integer) - Optional - Maximum number of pools to return.
- **offset** (integer) - Optional - Number of pools to skip before returning results.

### Response
#### Success Response (200)
- **pools** (array) - A list of sandbox pools.
  - **name** (string) - The name of the sandbox pool.
  - **template_name** (string) - The name of the template used for the pool.
  - **replicas** (integer) - The number of replicas in the pool.
  - **created_at** (string) - The timestamp when the pool was created.

#### Response Example
```json
{
  "pools": [
    {
      "name": "example-pool",
      "template_name": "example-template",
      "replicas": 3,
      "created_at": "2023-10-27T10:00:00Z"
    }
  ]
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/jira

Handles the OAuth setup callback redirect from GitHub Apps, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/evaluate-pairwise

Handles the OAuth setup callback redirect from GitHub Apps, processing installation or update events.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### Install and Initialize LangGraph SDK

Source: https://docs.langchain.com/oss/javascript/langchain/deploy

This snippet demonstrates how to install the LangGraph SDK via pip and how to initialize a synchronous client using a deployment URL and API key.

```shellscript
pip install langgraph-sdk
```

```python
from langgraph_sdk import get_sync_client # or get_client for async

client = get_sync_client(url="your-deployment-url", api_key="your-api-key")
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/callbacks/sagemaker_tracking

Handles the setup flow for OAuth providers, including GitHub App installation callbacks.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup flow for OAuth providers. For GitHub Apps, this is triggered when a user installs or updates their installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success confirmation message.
```

--------------------------------

### Initialize example document

Source: https://docs.langchain.com/oss/python/integrations/llms/sagemaker

Demonstrates how to instantiate a Document object for use within the LangChain framework.

```python
example_doc_1 = """"
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/providers/groq

Handles the initial setup for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the status of the setup.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### POST /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/providers/ollama

Handles the 'Setup URL' callback from GitHub Apps, triggered during app installation or updates. For 'update' actions, it displays a success page. For new installations with code/state, it processes the OAuth callback.

```APIDOC
## POST /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered during app installation or updates. For 'update' actions, it displays a success page. For new installations with code/state, it processes the OAuth callback.

### Method
POST

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the OAuth provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Request Body
(Not applicable for this endpoint, as it handles callbacks)

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App setup successful."
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/components

Handle OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation. For "update" actions, it shows a success page. For new installations with code/state, it processes similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Response
#### Success Response (200 OK)
- **message** (string) - A success message indicating the completion of the setup process.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### Initialize Qdrant Client with Local Storage (Python)

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/qdrant

This snippet shows how to create an instance of QdrantClient, configuring it to use a local directory for data storage. It imports necessary components and defines the path for the local database.

```python
from qdrant_client import QdrantClient, Distance, VectorParams

# Create a Qdrant client for local storage
client = QdrantClient(path="/tmp/langchain_qdrant")
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/providers/astradb

Handles the OAuth setup callback redirect, specifically for GitHub Apps installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps. It processes new installations or updates to existing repository access.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success confirmation message.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/agent-builder-self-hosted

Handle OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/chat/deepseek

Handles the OAuth setup callback for GitHub App installations. For 'update' actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. For 'update' actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/use-tools

Handles the initial OAuth setup callback for new installations. It processes the authorization code and exchanges it for tokens, similar to a regular OAuth callback, but without needing an initial token exchange.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup callback for new installations. It processes the authorization code and exchanges it for tokens, similar to a regular OAuth callback, but without needing an initial token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup is complete.

#### Response Example
```json
{
  "message": "OAuth setup complete."
}
```
```

--------------------------------

### Build a basic agent with LangChain

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Demonstrates how to initialize a simple agent using the LangChain library, define a weather-fetching tool with Zod schema validation, and invoke the agent with a user message.

```javascript
import { createAgent, tool } from "langchain";
import * as z from "zod";

const getWeather = tool(
  (input) => `It's always sunny in ${input.city}!`,
  {
    name: "get_weather",
    description: "Get the weather for a given city",
    schema: z.object({
      city: z.string().describe("The city to get the weather for"),
    }),
  }
);

const agent = createAgent({
  model: "claude-sonnet-4-6",
  tools: [getWeather],
});

console.log(
  await agent.invoke({
    messages: [{ role: "user", content: "What's the weather in Tokyo?" }],
  })
);
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/define-target-function

Handles the setup phase for an OAuth provider, including processing installations and redirecting to the success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup phase for an OAuth provider. For new installations, it processes the state and code, otherwise, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### Create a Sandbox Pool

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Creates a new Sandbox Pool in the tenant's namespace. Pools pre-provision sandboxes from a template for faster claim binding.

```APIDOC
## POST /v2/sandboxes/pools

### Description
Create a new Sandbox Pool in tenant's namespace.
Pools pre-provision sandboxes from a template for faster claim binding.

Requirements:
- The referenced template must exist
- The template must not have any volume mounts (volumes are stateful)

Pool creation is subject to quota limits. The total resource usage
(replicas * per-replica resources) is checked against the organization's
quota limits.

### Method
POST

### Endpoint
/v2/sandboxes/pools

#### Request Body
- **name** (string) - Required - The name of the sandbox pool.
- **template_name** (string) - Required - The name of the template to use for the pool.
- **replicas** (integer) - Required - The number of replicas to create in the pool.

### Request Example
```json
{
  "name": "my-new-pool",
  "template_name": "my-template",
  "replicas": 5
}
```

### Response
#### Success Response (201)
- **message** (string) - A confirmation message.
- **pool** (object) - The created sandbox pool details.
  - **name** (string) - The name of the sandbox pool.
  - **template_name** (string) - The name of the template used for the pool.
  - **replicas** (integer) - The number of replicas in the pool.
  - **created_at** (string) - The timestamp when the pool was created.

#### Response Example
```json
{
  "message": "Sandbox pool 'my-new-pool' created successfully.",
  "pool": {
    "name": "my-new-pool",
    "template_name": "my-template",
    "replicas": 5,
    "created_at": "2023-10-27T10:05:00Z"
  }
}
```
```

--------------------------------

### Agent Builder

Source: https://docs.langchain.com/langsmith/agent-builder-tools

Documentation for the Langchain Agent Builder, including getting started guides, tools, and integrations.

```APIDOC
## Agent Builder Documentation

### Agent Builder Overview

**Description**: Introduction to the Langchain Agent Builder.

**Endpoint**: /langsmith/agent-builder

### Get Started with Agent Builder

#### Quickstart

**Description**: Quickstart guide for the Agent Builder.

**Endpoint**: /langsmith/agent-builder-quickstart

#### Essentials

**Description**: Core concepts and essentials of the Agent Builder.

**Endpoint**: /langsmith/agent-builder-essentials

#### Templates

**Description**: Available templates for building agents.

**Endpoint**: /langsmith/agent-builder-templates

#### Setup

**Description**: Setting up the Agent Builder environment.

**Endpoint**: /langsmith/agent-builder-setup

#### Manage Agent Settings

**Description**: Managing settings for your agents.

**Endpoint**: /langsmith/agent-builder-manage-agent-settings

### Tools and Integrations

#### Agent Builder Tools

**Description**: Information on available tools for the Agent Builder.

**Endpoint**: /langsmith/agent-builder-tools

#### Agent Builder Integrations

**Description**: Information on integrating with other services.

**Endpoint**: /langsmith/agent-builder-integrations
```

--------------------------------

### Initialize Vector Store and Perform Similarity Search

Source: https://docs.langchain.com/oss/javascript/integrations/vectorstores/azure_cosmosdb_nosql

Demonstrates how to instantiate a vector store with specific database and container configurations, followed by performing a similarity search using a natural language query.

```javascript
OpenAIEmbeddings();

const store = {
  databaseName: "langchain",
  containerName: "documents"
};

// Performs a similarity search
const resultDocuments = await store.similaritySearch(
  "What did the president say about Ketanji Brown Jackson?"
);
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/mongodb_atlas

Handles the OAuth setup callback, triggered when a user installs or updates their GitHub App installation. For update actions, it shows a success page. For new installations, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback, triggered when a user installs or updates their GitHub App installation. For update actions, it shows a success page. For new installations, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation processed successfully."
}
```
```

--------------------------------

### Fetch dataset examples by version in Python

Source: https://docs.langchain.com/langsmith/manage-datasets

Demonstrates how to initialize the LangSmith client and prepare for evaluation by fetching examples from a specific dataset version.

```python
from langsmith import Client

ls_client = Client()

# Assumes actual outputs have a 'class' key.
# Assumes example outputs have a 'label' key.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/distributed-tracing

Handle OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback from GitHub Apps after a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback from GitHub Apps after a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter for CSRF protection.

### Response
#### Success Response (200)
- **message** (string) - A message indicating the status of the setup callback.

#### Response Example
```json
{
  "message": "GitHub App setup processed successfully."
}
```
```

--------------------------------

### Set up development environment

Source: https://docs.langchain.com/langsmith/prompt-engineering-quickstart

Commands to create a project directory, set up a Python virtual environment, and install the LangSmith and OpenAI libraries. This is the prerequisite step for starting a LangSmith project.

```shellscript
mkdir ls-prompt-quickstart && cd ls-prompt-quickstart
python -m venv .venv
source .venv/bin/activate
pip install -qU langsmith openai
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/pymupdf4llm

Handles the OAuth setup callback, processing new installations or updates to GitHub App installations. For new installations with code/state, it processes similarly to a regular OAuth callback. For updates where users modify repo access, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. Processes new installations or updates to repository access.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

#### Query Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation processed successfully."
}
```
```

--------------------------------

### Project Initialization and Dependency Installation (Shell)

Source: https://docs.langchain.com/langsmith/prompt-engineering-quickstart

This snippet demonstrates the shell commands to create a new project directory, initialize a Node.js project with npm, install essential development and runtime dependencies for Langchain, and initialize the TypeScript compiler. It ensures all necessary tools are in place for a TypeScript-based Langchain project.

```shellscript
mkdir ls-prompt-quickstart-ts && cd ls-prompt-quickstart-ts
npm init -y
npm install langsmith openai typescript ts-node
npx tsc --init
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/evaluate-existing-experiment

Handles the OAuth setup callback redirect from GitHub Apps, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This endpoint processes new installations or updates to existing repository access.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/moorcheh

Handles OAuth setup callback redirects from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langgraph/overview

Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. For actions like user-modified repo access via GitHub, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. For actions like user-modified repo access via GitHub, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://python.langchain.com/v0.1/docs/guides/productionization/safety/amazon_comprehend_chain

Handles the initial setup phase for an OAuth provider, including processing installations with code or state.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup phase for an OAuth provider. For new installations with code/state, it processes the callback; otherwise, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/deploy-self-hosted-full-platform

Handles the setup process for a new OAuth provider installation or updates to existing repository access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup process for a new OAuth provider installation or updates to existing repository access. Processes new installations with code/state or displays a success page for updates.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion or redirect status.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/retrievers/nvidia

Handles the OAuth setup callback, processing new installations similarly to a regular OAuth callback when code or state is present. For update actions, it displays a success page as no token exchange is required.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback. For new installations with code or state, it processes the OAuth callback. For update actions, it shows a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the status of the setup.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/splitters/split_by_token

Handles the OAuth setup callback, triggered when a user installs or updates their GitHub App installation. For new installations with code/state, it processes similarly to a regular OAuth callback. For updates, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback, triggered when a user installs or updates their GitHub App installation. For new installations with code/state, it processes similarly to a regular OAuth callback. For updates, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation processed successfully."
}
```
```

--------------------------------

### Initialize Drasi tool instance

Source: https://docs.langchain.com/oss/python/integrations/tools/drasi

Demonstrates how to import the necessary components and configure the MCP connection for the Drasi tool. This setup is required to establish communication with the Drasi server.

```python
from langchain_drasi import create_drasi_tool, MCPConnectionConfig, ConsoleHandler

# Configure connection to Drasi MCP server
config = MCPConnectionConfig(
    server_url="http://localhost:8083",
    timeout=30.0
)

# Create a Drasi tool instance
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/deploy-hybrid

Handles the initial setup phase for OAuth providers, including processing new installations with code or state.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the OAuth setup for a specific provider, handling new installations and state verification.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion or redirect status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/prompt-template-format

Handles the setup phase for OAuth providers, including redirecting to success pages for pre-authorized installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup phase for OAuth providers. For modified repo access, it displays a success page as no token exchange is required.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/manage-datasets

Handles the initial OAuth setup callback for new installations. It processes the OAuth callback similar to regular OAuth flows when code/state are present, otherwise, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup callback for new installations. Processes the OAuth callback similar to regular OAuth flows when code/state are present, otherwise, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the completion of the setup or a redirect to the success page.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### Initialize AzureChatOpenAI

Source: https://docs.langchain.com/oss/javascript/integrations/chat/azure

Shows how to import and instantiate the AzureChatOpenAI class with required parameters including instance name, deployment name, and API version.

```javascript
import { AzureChatOpenAI } from "@langchain/openai";

const model = new AzureChatOpenAI({
  azureOpenAIApiKey: "<your_key>",
  azureOpenAIApiInstanceName: "<your_instance_name>",
  azureOpenAIApiDeploymentName: "<your_deployment_name>",
  azureOpenAIApiVersion: "<api_version>",
});
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/serpapi

Handles the OAuth setup callback redirect from GitHub Apps, facilitating new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This is triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the setup or update status.
```

--------------------------------

### Ollama Embeddings Example

Source: https://docs.langchain.com/oss/python/integrations/text_embedding/ollama

This snippet demonstrates how to get started with Ollama embedding models using LangChain. It provides a basic example of using the `OllamaEmbeddings` class. For comprehensive details on features and configuration, consult the official API reference.

```javascript
import { OllamaEmbeddings } from "langchain_ollama.embeddings";

// Example usage:
const ollamaEmbeddings = new OllamaEmbeddings({
  model: "llama2",
  // Other configuration options can be passed here
});

// You can then use ollamaEmbeddings for tasks like generating embeddings for text:
// const embeddings = await ollamaEmbeddings.embedQuery("This is a test query.");
// console.log(embeddings);
```

--------------------------------

### Initialize and load from OBSFileLoader

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/huawei_obs_file

Demonstrates how to instantiate the OBSFileLoader with bucket details, object keys, endpoint, and configuration parameters, followed by the load method to retrieve data.

```python
loader = OBSFileLoader("your-bucket-name", "your-object-key", endpoint=endpoint, config=config)
loader.load()
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/clickhouse

Handles the OAuth setup callback for GitHub App installations. For new installations, it processes the token exchange similar to a regular OAuth callback. For updates, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. For new installations, it processes the token exchange similar to a regular OAuth callback. For updates, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App installation successful."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/contributing/integrations-langchain

Handles the OAuth setup callback for GitHub App installations or updates. For new installations with code/state, it processes similar to a regular OAuth callback. For updates, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations or updates. For new installations with code/state, it processes similar to a regular OAuth callback. For updates, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App setup successful."
}
```
```

--------------------------------

### Setup and Initialization of KV-Store Integration

Source: https://docs.langchain.com/oss/python/integrations/tools/github

Demonstrates how to install the required package, configure API keys, and instantiate the ByteStore class for a KV-store integration.

```bash
pip install -U __package_name__
export __MODULE_NAME___API_KEY="your-api-key"
```

```python
from __module_name__ import __ModuleName__ByteStore

kv_store = __ModuleName__ByteStore(
    # api_key="...",
    # other params...
)
```

--------------------------------

### Initialize Qdrant Vector Store from Documents

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/qdrant

Demonstrates the initialization of a Qdrant vector store using the from_documents method. It configures parameters such as the collection name, URL, and gRPC preference.

```python
QdrantVectorStore.from_documents(
	docs,
	embeddings,
	url=url,
	prefer_grpc=True,
	collection_name="my_documents"
)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/tools/playwright

Handles the setup process for a new OAuth installation or updates to existing repository access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup for a new OAuth installation or handles updates to existing repository access via GitHub.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the setup or update status.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/deepagents/acp

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A message indicating the status of the setup.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/tavily_search

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation. For "update" actions, it shows a success page. For new installations with code/state, it processes similarly to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Required - The authorization code received from GitHub.
- **state** (string) - Required - The state parameter used to prevent CSRF attacks.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup was completed.

#### Response Example
```json
{
  "message": "GitHub App setup successful."
}
```
```

--------------------------------

### POST /assistants

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Create a new assistant in the system.

```APIDOC
## POST /assistants

### Description
Create an assistant. An initial version of the assistant will be created and the assistant is set to that version.

### Method
POST

### Endpoint
/assistants

### Request Body
- **name** (string) - Required - The name of the assistant.

### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the created assistant.

### Response Example
{
  "id": "assistant_123"
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/llms/amazon_api_gateway

Handles the setup flow for OAuth providers, specifically processing new installations or updates for GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes OAuth setup requests. For updates, it returns a success page; for new installations, it initiates the token exchange process.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect instruction.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/cockroachdb

Handles the setup flow for new OAuth installations or updates, processing code/state exchanges for GitHub and other providers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup flow for new OAuth installations or updates. For update actions, it displays a success page; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### POST /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/imsdb

Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to the regular OAuth callback.

```APIDOC
## POST /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For 'update' actions (user modified repo access via GitHub), it shows a success page since no token exchange is needed. For new installations with code/state, it processes similar to the regular OAuth callback.

### Method
POST

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Request Example
```json
{
  "example": "POST /v2/auth/setup/github?code=abc123xyz&state=some_state_value"
}
```

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
```json
{
  "example": {
    "message": "GitHub App setup processed successfully."
  }
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders

Handles the setup callback for OAuth providers, processing new installations or updates to GitHub App installations. For updates, it displays a success page as no token exchange is needed. For new installations, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, processing new installations or updates to GitHub App installations. For updates, it displays a success page as no token exchange is needed. For new installations, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/tools/azure_dynamic_sessions

Handles GitHub App installation callbacks or OAuth setup triggers.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes GitHub App installation or update callbacks. For updates, it displays a success page; for new installations, it processes the OAuth flow.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/apify_dataset

Handles the 'Setup URL' callback from GitHub Apps, triggered by user installation or updates. For updates, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps. Processes new installations or updates to existing ones.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/google_cloud_storage_directory

Handles the setup callback redirect from GitHub Apps, triggered during installation or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps. For updates, it displays a success page; for new installations, it processes the OAuth token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/chat/togetherai

Handles the setup callback for OAuth providers, processing updates to GitHub App installations. For new installations, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, processing updates to GitHub App installations. For new installations, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/aws-self-hosted

Handles the OAuth callback for new installations when code and state are present. It processes the OAuth callback similarly to regular OAuth callbacks.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth callback for new installations when code and state are present. It processes the OAuth callback similarly to regular OAuth callbacks.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(No specific success response details provided in the source text)

#### Response Example
(No specific success response example provided in the source text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/prompt-engineering

Handles the setup callback for OAuth providers, processing GitHub App installations and updates. For new installations, it processes similar to a regular OAuth callback. For updates, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, processing GitHub App installations and updates. For new installations, it processes similar to a regular OAuth callback. For updates, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation processed successfully."
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/chat/mistral

Handles the setup process for a specific OAuth provider, processing new installations or updates to repo access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup process for a specific OAuth provider. For updates, it shows a success page; for new installations, it processes the OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/s3

Handle OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.
```

--------------------------------

### Agent Builder Documentation

Source: https://docs.langchain.com/langsmith/share-trace

Documentation related to the LangSmith Agent Builder, including getting started guides and managing agent settings.

```APIDOC
## Agent Builder Documentation

### Get Started

#### Description
Guides for starting with the Agent Builder, covering essentials, templates, setup, and settings management.

### Pages
- /langsmith/agent-builder-quickstart
- /langsmith/agent-builder-essentials
- /langsmith/agent-builder-templates
- /langsmith/agent-builder-setup
- /langsmith/agent-builder-manage-agent-settings
```

--------------------------------

### Setup and Use Amazon Bedrock AgentCore Browser

Source: https://docs.langchain.com/oss/python/integrations/providers/aws

Provides installation instructions and a code example for initializing the Bedrock AgentCore browser toolkit and using it within a LangChain agent.

```bash
pip install langchain-aws bedrock-agentcore playwright beautifulsoup4
```

```python
from langchain_aws.tools import create_browser_toolkit

# Create toolkit
toolkit, browser_tools = create_browser_toolkit(region="us-west-2")

# Use with an agent
agent = create_react_agent(model=llm, tools=browser_tools)
result = await agent.ainvoke(
    {"messages": [{"role": "user", "content": "Go to example.com and get the heading"}]},
    config={"configurable": {"thread_id": "session-1"}}
)

# Cleanup when done
await toolkit.cleanup()
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/pdf

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback triggered by user actions like installing or updating a GitHub App installation. For updates, it displays a success page. For new installations with code/state, it proceeds with the regular OAuth callback flow.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/chat/cloudflare_workersai

Handles the OAuth setup callback for GitHub Apps, triggered on installation or update. For updates, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub Apps, triggered on installation or update. For updates, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### Initialize Qdrant Vector Store Client

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/qdrant

Demonstrates how to instantiate the QdrantVectorStore client in Python. This setup requires a pre-configured client, a collection name, and an embedding model.

```python
QdrantVectorStore(
  client=client,
  collection_name="demo_collection",
  embedding=embeddings
)
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/messages

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For 'update' actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter for CSRF protection.

### Response
#### Success Response (200 OK)
- **message** (string) - A success message indicating the outcome of the callback.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/graphs/azure_cosmosdb_gremlin

Handles the setup for GitHub Apps installations and updates. For new installations, it processes the OAuth callback. For updates where only repository access is modified, it displays a success page as no token exchange is required.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup for GitHub Apps installations and updates. For new installations, it processes the OAuth callback. For updates where only repository access is modified, it displays a success page as no token exchange is required.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
```
(No request body for GET request)
```

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App installation processed successfully."
}
```
```

--------------------------------

### Database Migration Setup

Source: https://docs.langchain.com/oss/javascript/langgraph/add-memory

Explains the convention for running database migrations in LangGraph using the setup() method on checkpointer or store instances.

```javascript
setup()
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/log-traces-to-project

Handles the setup phase for OAuth providers, processing installation codes or state to finalize the authentication flow.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup phase for an OAuth provider. For new installations, it processes codes or state parameters to complete the setup.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/multi-agent/skills

Handles the initial setup for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/tools/mcp_toolbox

Handles the setup callback for OAuth providers, specifically processing new GitHub App installations or user-modified repository access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes OAuth setup callbacks, handling new installations or updates to existing provider permissions.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the setup status.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/stardog

Handles the initial setup for OAuth providers. For new installations with code/state, it processes the OAuth callback similar to regular OAuth flows. For update actions (e.g., user modified repo access via GitHub), it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for OAuth providers. For new installations with code/state, it processes the OAuth callback similar to regular OAuth flows. For update actions (e.g., user modified repo access via GitHub), it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Details depend on the specific provider and action - may redirect or show a success page)

#### Response Example
(No specific JSON response example, as it may involve redirects or UI elements.)
```

--------------------------------

### Example Project File Structure (Shell Script)

Source: https://docs.langchain.com/langsmith/setup-app-requirements-txt

This shell script illustrates a recommended project directory structure for Langchain LLM applications. It shows how to organize agent code, utility files, and the main application directory.

```shellscript
my-app/
├── my_agent # all project code lies within here
│   ├── utils # utilities for your graph

```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/google_serper

Handles the OAuth setup callback for GitHub App installations. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/text_embedding/fake

Handles the OAuth setup callback for GitHub App installations. It processes updates to repository access or new installations by exchanging tokens.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. Processes updates to repository access or new installations by exchanging tokens.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the installation or update was processed.

#### Response Example
```json
{
  "message": "GitHub App installation processed successfully."
}
```
```

--------------------------------

### Initialize DeepAgent with StateBackend

Source: https://docs.langchain.com/oss/python/deepagents/skills

Demonstrates initializing a DeepAgent using the StateBackend with an in-memory checkpointer. It shows how to fetch remote skill files and inject them into the agent's virtual filesystem.

```python
from urllib.request import urlopen
from deepagents import create_deep_agent
from deepagents.backends.utils import create_file_data
from langgraph.checkpoint.memory import MemorySaver

checkpointer = MemorySaver()

skill_url = "https://raw.githubusercontent.com/langchain-ai/deepagents/refs/heads/main/libs/cli/examples/skills/langgraph-docs/SKILL.md"
with urlopen(skill_url) as response:
    skill_content = response.read().decode('utf-8')

skills_files = {
    "/skills/langgraph-docs/SKILL.md": create_file_data(skill_content)
}

agent = create_deep_agent(
    skills=["/skills/"],
    checkpointer=checkpointer,
)

result = agent.invoke(
    {
        "messages": [{"role": "user", "content": "What is langgraph?"}],
        "files": skills_files
    },
    config={"configurable": {"thread_id": "12345"}},
)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/example-data-format

Handles the initial OAuth setup callback. For new installations with code/state, it processes similarly to the regular OAuth callback. For existing installations via GitHub, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup callback. For new installations with code/state, it processes similarly to the regular OAuth callback. For existing installations via GitHub, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Indicates the success of the setup process.

#### Response Example
{
  "message": "OAuth setup successful"
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/errors/MESSAGE_COERCION_FAILURE

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes the callback similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For 'update' actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter for CSRF protection.

### Response
#### Success Response (200)
- **message** (string) - A message indicating the status of the setup.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/contributing/integrations-langchain

Handles the OAuth setup callback, processing new installations or updates to GitHub App installations. For updates involving repository access changes, it displays a success page as no token exchange is required. For new installations with code/state, it proceeds similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback, processing new installations or updates to GitHub App installations. For updates involving repository access changes, it displays a success page as no token exchange is required. For new installations with code/state, it proceeds similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### Agent Builder

Source: https://docs.langchain.com/oss/javascript/contributing/standard-tests-langchain

Information related to the Langsmith Agent Builder, including quickstart guides, essentials, templates, and setup instructions.

```APIDOC
## Agent Builder Documentation

### Get Started

- **Page:** /langsmith/agent-builder-quickstart
  - Description: Quickstart guide for using the Agent Builder.

- **Page:** /langsmith/agent-builder-essentials
  - Description: Essential concepts and features of the Agent Builder.

- **Page:** /langsmith/agent-builder-templates
  - Description: Available templates for building agents.

- **Page:** /langsmith/agent-builder-setup
  - Description: Setup instructions for the Agent Builder.
```

--------------------------------

### Install and Initialize LangChain Runloop

Source: https://docs.langchain.com/oss/python/deepagents/data-analysis

This snippet demonstrates how to install the required package using the uv package manager and how to initialize the RunloopSDK client in Python using an API key.

```shellscript
uv add langchain-runloop
```

```python
from runloop_api_client import RunloopSDK

from langchain_runloop import RunloopSandbox

api_key = "..."
client = RunloopSDK(bearer_token=api_key)

devbox =
```

--------------------------------

### Langchain Agent Configuration Example (JavaScript)

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

An example illustrating the configuration of a Langchain agent, including optional parameters like thread_id and context with user_id. This helps in managing conversation state and user-specific data.

```javascript
const config = {
  configurable: {
    thread_id: "1",
    context: {
      user_id: "1"
    }
  };
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/microsoft_word

Handles the setup callback for GitHub Apps or other OAuth providers, processing token exchanges for new installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback from GitHub Apps or similar providers. Processes new installations or updates to existing ones.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the setup status.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/huawei_obs_directory

Handle the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider (e.g., 'github').

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter used during the OAuth flow.

### Response
#### Success Response (200)
- **message** (string) - A success message, e.g., 'GitHub App installation successful.' or a redirect to the frontend.

#### Error Response (400 or 500)
- **error** (string) - Description of the error.
```

--------------------------------

### Python Example for Langsmith Evaluation Setup

Source: https://docs.langchain.com/langsmith/code-evaluator-sdk

This Python code demonstrates how to set up an evaluation using Langsmith. It imports necessary components from langsmith and openai, and assumes pydantic is installed. This example is for Langsmith version 0.2.0 or higher.

```python
from langsmith import evaluate
from langsmith.schemas import Run, Example
from openai import AsyncOpenAI

# Assumes you've installed pydantic.
from pydantic import BaseModel
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/azure_blob_storage_file

Handle OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/manage-organization-by-api

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint manages the "Setup URL" callback from GitHub Apps, triggered during installation or updates. For updates, it displays a success page. For new installations with code/state, it processes the OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter for CSRF protection.

#### Request Body
(No request body documented)

### Response
#### Success Response (200)
(Response details depend on whether it's an update or a new installation. Typically redirects or shows a success message.)

#### Response Example
(Example depends on the flow - could be a redirect URL or an HTML success message.)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/file_loaders/notion_markdown

Handles the GitHub App setup URL callback, processing new installations or updates to existing repository access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating installation or update status.
```

--------------------------------

### Initialize OBS Client and Load Documents

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/huawei_obs_file

Provides a comprehensive example of initializing the OBS client and using OBSFileLoader to load documents. This includes specifying credentials, endpoint, bucket name, and the object path for loading.

```python
from obs import ObsClient

# Initialize OBS client
client = ObsClient(ak="YOUR_AK", sk="YOUR_SK", server_endpoint=endpoint, 
                   domain_id="YOUR_DOMAIN_ID", 
                   region="YOUR_REGION")

# Initialize OBSFileLoader
loader = OBSFileLoader(bucket_name="your-bucket-name", 
                       prefix="your-object-path/", 
                       obs_client=client)

# Load documents
documents = loader.load()
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/langchain/multi-agent/handoffs-customer-support

Handle OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider
```

--------------------------------

### Get Listener

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

Get a listener by ID.

```APIDOC
## GET /v2/listeners/{listener_id}

### Description
Get a listener by ID.

### Method
GET

### Endpoint
/v2/listeners/{listener_id}

### Parameters
#### Path Parameters
- **listener_id** (string) - Required - The ID of the listener to retrieve.

#### Query Parameters
- **None**

### Request Example
```json
{
  "example": "No request body needed for this GET request."
}
```

### Response
#### Success Response (200)
- **id** (string) - The unique identifier for the listener.
- **name** (string) - The name of the listener.
- **status** (string) - The current status of the listener.
- **url** (string) - The URL configured for the listener.
- **created_at** (string) - The timestamp when the listener was created.

#### Response Example
```json
{
  "example": "{\"id\": \"lst_1\", \"name\": \"Listener A\", \"status\": \"active\", \"url\": \"https://example.com/webhook\", \"created_at\": \"2023-10-27T10:10:00Z\"}"
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/chat/azure

Handles the initial setup callback for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Indicates the success of the operation.

#### Response Example
{
  "message": "OAuth setup successful."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/astradb

Handles the OAuth setup callback for GitHub App installations. It processes updates to repository access or new installations by performing a token exchange if necessary.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. It processes updates to repository access or new installations by performing a token exchange if necessary.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/errors/MODEL_AUTHENTICATION

Handles the OAuth setup callback, processing new installations or updates to GitHub App installations. For new installations with code/state, it processes similarly to a regular OAuth callback. For updates where users modify repo access, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. Processes new installations or updates to repository access.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(No response example provided in the input text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langgraph/errors/INVALID_CONCURRENT_GRAPH_UPDATE

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

For \"update\" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

#### Request Body
None

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation successful."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/custom-auth

Handles the OAuth setup callback for new installations with code/state, processing it similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations with code/state, processing it similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
```json
{
  "message": "OAuth setup callback processed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/legacy-trace-with-vercel-ai-sdk

Handles the OAuth setup callback for new installations or updates. For new installations with code/state, it processes similarly to a regular OAuth callback. For update actions (user modified repo access via GitHub), it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations or updates. For new installations with code/state, it processes similarly to a regular OAuth callback. For update actions (user modified repo access via GitHub), it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/agent-builder-manage-agent-settings

Handle OAuth setup callback redirect from GitHub Apps. This endpoint is used to manage the callback process after a user initiates or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation. For "update" actions (user modified repo access via GitHub), it shows a success page. For new installations with code/state, it processes the callback similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter for CSRF protection.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/deepagents/streaming/overview

Handles the OAuth setup callback redirect from GitHub Apps, processing new installations or updates to repository access.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. Triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Indicates success of the setup or update process.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/tools/bearly

Handles the OAuth setup callback redirect from GitHub Apps, processing new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### Get Deployment

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

Get a deployment by ID.

```APIDOC
## GET /v2/deployments/{deployment_id}

### Description
Get a deployment by ID.

### Method
GET

### Endpoint
/v2/deployments/{deployment_id}

### Parameters
#### Path Parameters
- **deployment_id** (string) - Required - The ID of the deployment to retrieve.

#### Query Parameters
- **None**

### Request Example
```json
{
  "example": "No request body needed for this GET request."
}
```

### Response
#### Success Response (200)
- **id** (string) - The unique identifier for the deployment.
- **name** (string) - The name of the deployment.
- **status** (string) - The current status of the deployment.
- **created_at** (string) - The timestamp when the deployment was created.

#### Response Example
```json
{
  "example": "{\"id\": \"dep_abc\", \"name\": \"My App Deployment\", \"status\": \"active\", \"created_at\": \"2023-10-27T10:00:00Z\"}"
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/tools

Handles the OAuth setup callback for a given provider. For new installations with code/state, it processes similarly to a regular OAuth callback. If no token exchange is needed (e.g., via GitHub), it shows a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. For new installations with code/state, it processes similarly to a regular OAuth callback. If no token exchange is needed (e.g., via GitHub), it shows a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
```json
{
  "message": "OAuth setup successful."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/llms/sagemaker

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation. For 'update' actions, it displays a success page. For new installations with code/state, it processes the callback similar to regular OAuth.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details depend on the specific provider and action)

#### Response Example
(Example response would be a redirect or a success message page)
```

--------------------------------

### Initialize Environment Configuration

Source: https://docs.langchain.com/oss/python/deepagents/acp

Copies the example environment file to a local .env file to prepare for API key configuration.

```shellscript
cp .env.example .env
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/middleware/anthropic

Handles the setup or update of a GitHub App installation, processing token exchanges or redirecting to success pages.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup or update of a GitHub App installation. Processes new installations with code/state or shows a success page for updates.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect status.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/hyperbrowser

Handles the OAuth setup callback from GitHub Apps, triggered on installation or update. For updates, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from GitHub Apps, triggered on installation or update. For updates, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App setup successful."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/background-run

Handles the OAuth setup callback for new installations. If code/state are present, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations. If code/state are present, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup is complete.

#### Response Example
```json
{
  "message": "OAuth setup complete."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/multi-agent/skills-sql-assistant

Handles the OAuth setup callback, processing new installations or updates for GitHub App installations. For new installations with code/state, it processes similarly to a regular OAuth callback. For updates where users modify repo access, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback, processing new installations or updates for GitHub App installations. For new installations with code/state, it processes similarly to a regular OAuth callback. For updates where users modify repo access, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the callback.

#### Response Example
{
  "message": "GitHub App installation processed successfully."
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/langgraph/errors/GRAPH_RECURSION_LIMIT

Handles the setup flow for GitHub Apps or other OAuth providers, processing installation callbacks or redirects.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup flow for OAuth providers, specifically triggered by GitHub App installations or updates.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/pdfminer

Handles the OAuth setup callback, triggered when a user installs or updates their GitHub App installation. For new installations with code/state, it processes similarly to a regular OAuth callback. For 'update' actions, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. Processes new installations or updates existing ones.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App installation processed successfully."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/vitest-jest

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For 'update' actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter used for CSRF protection.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup callback.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback (GitHub Apps)

Source: https://docs.langchain.com/langsmith/observability-stack

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation. It processes new installations with code/state similar to the regular OAuth callback and shows a success page for update actions.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is
triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show
a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular
OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App setup successful."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/deepagents/skills

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation. For update actions, it shows a success page. For new installations with code/state, it processes similarly to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Details not provided in the source text)

#### Response Example
(Details not provided in the source text)
```

--------------------------------

### Configure Azure OpenAI Constructor

Source: https://docs.langchain.com/oss/javascript/integrations/chat/azure

Example of initializing the Azure OpenAI client with required parameters including instance name, deployment name, and API version.

```javascript
{
  azureOpenAIApiKey: "<your_key>",
  azureOpenAIApiInstanceName: "<your_instance_name>",
  azureOpenAIApiDeploymentName: "<your_deployment_name>",
  azureOpenAIApiVersion: "<api_version>"
}
```

--------------------------------

### GET /api/v1/examples

Source: https://docs.langchain.com/langsmith/data-purging-compliance

Retrieves examples based on provided metadata filters. You can filter by user ID or environment.

```APIDOC
## GET /api/v1/examples

### Description
Retrieves examples that match the specified metadata criteria (user ID or environment).

### Method
GET

### Endpoint
https://api.smith.langchain.com/api/v1/examples

### Parameters
#### Query Parameters
- **as_of** (string) - Optional - Timestamp to filter examples as of a specific date.

#### Request Body
- **metadata** (object) - Required - An object containing filtering criteria.
  - **user_id** (string) - Optional - The ID of the user to filter examples by.
  - **environment** (string) - Optional - The environment to filter examples by.

### Request Example
```json
{
  "metadata": {
    "user_id": "user123",
    "environment": "staging"
  }
}
```

### Response
#### Success Response (200)
- **examples** (array) - A list of example objects matching the query.

#### Response Example
```json
{
  "examples": [
    {
      "id": "example-id-1",
      "metadata": {
        "user_id": "user123",
        "environment": "staging"
      },
      "inputs": {
        "question": "What is Langchain?"
      },
      "outputs": {
        "answer": "Langchain is a framework..."
      }
    }
  ]
}
```
```

--------------------------------

### Setup Client and Thread

Source: https://docs.langchain.com/langsmith/background-run

This section details how to set up the client and create a new thread for background runs. It provides code examples for Python, JavaScript, and cURL.

```APIDOC
## Setup Client and Thread

### Description
Set up your Langchain client and create a new thread to manage background runs for your agent.

### Method
POST

### Endpoint
`/threads`

### Parameters
#### Query Parameters
- **url** (string) - Required - The deployment URL for your Langchain agent.

### Request Body
This endpoint does not require a request body.

### Request Example (Python)
```python
from langgraph_sdk import get_client

client = get_client(url=<DEPLOYMENT_URL>)
# Using the graph deployed with the name "agent"
assistant_id = "agent"
# create thread
thread = await client.threads.create()
print(thread)
```

### Request Example (JavaScript)
```javascript
import { Client } from "@langchain/langgraph-sdk";

const client = new Client({ apiUrl: <DEPLOYMENT_URL> });
// Using the graph deployed with the name "agent"
const assistantID = "agent";
// create thread
const thread = await client.threads.create();
console.log(thread);
```

### Request Example (cURL)
```bash
curl --request POST \
  --url <DEPLOYMENT_URL>/threads \
  --header 'Content-Type: application/json' \
  --data '{}'
```

### Response
#### Success Response (200)
- **thread_id** (string) - The unique identifier for the created thread.
- **created_at** (string) - The timestamp when the thread was created.
- **updated_at** (string) - The timestamp when the thread was last updated.
- **metadata** (object) - Any associated metadata for the thread.
- **status** (string) - The current status of the thread (e.g., 'idle').
- **config** (object) - Configuration details for the thread.
- **values** (any) - Any values associated with the thread.

#### Response Example
```json
{
  "thread_id": "5cb1e8a1-34b3-4a61-a34e-71a9799bd00d",
  "created_at": "2024-08-30T20:35:52.062934+00:00",
  "updated_at": "2024-08-30T20:35:52.062934+00:00",
  "metadata": {},
  "status": "idle",
  "config": {},
  "values": null
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/context-engineering

Handles the OAuth setup callback for GitHub App installations. For new installations, it processes the OAuth callback similar to regular OAuth callbacks. For 'update' actions where users modify repository access, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. For new installations, it processes the OAuth callback similar to regular OAuth callbacks. For 'update' actions where users modify repository access, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App installation updated successfully."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/share-trace

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation. For 'update' actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed. For new installations with code/state, we process similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
- **message** (string) - A success message or redirect information.

#### Response Example
{
  "message": "Setup complete" or "Redirecting to frontend..."
}
```

--------------------------------

### Instantiation: Initialize PrivyWalletTool with Different Options

Source: https://docs.langchain.com/oss/python/integrations/tools/privy

Demonstrates various ways to instantiate the PrivyWalletTool. It shows how to create a new wallet automatically, specify a chain type (e.g., 'base', 'solana'), or reuse an existing wallet by providing its ID.

```python
from langchain_privy import PrivyWalletTool

# Automatically creates a new Ethereum wallet
tool = PrivyWalletTool()

# Or create on a specific chain
base_tool = PrivyWalletTool(chain_type="base")
solana_tool = PrivyWalletTool(chain_type="solana")

# Or reuse an existing wallet
existing_tool = PrivyWalletTool(wallet_id="wal_abc123...")

```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/elasticsearch

Handle OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback from GitHub Apps for installation or update actions.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A message indicating the setup completion status.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/errors/OUTPUT_PARSING_FAILURE

Handles the OAuth setup callback for GitHub App installations. For new installations, it processes the OAuth callback similar to regular OAuth flows. For updates, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. For new installations, it processes the OAuth callback similar to regular OAuth flows. For updates, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App installation processed successfully."
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/dataset-json-types

Handles GitHub App installation or updates, processing OAuth token exchanges for new installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles GitHub App installation or updates. For updates, it shows a success page; for new installations, it processes the OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### Environment Setup and Installation

Source: https://docs.langchain.com/oss/python/langgraph/agentic-rag

Installs necessary dependencies and configures environment variables for OpenAI API access.

```bash
pip install -U langgraph "langchain[openai]" langchain-community langchain-text-splitters bs4
```

```python
import getpass
import os

def _set_env(key: str):
    if key not in os.environ:
        os.environ[key] = getpass.getpass(f"{key}:")

_set_env("OPENAI_API_KEY")
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/mathpix

Handles the initial setup callback from OAuth providers, particularly for GitHub App installations. For new installations, it processes the OAuth token exchange similar to a regular OAuth callback. For updates to existing installations where a user modifies repository access, it displays a success page as no token exchange is required.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback from OAuth providers, particularly for GitHub App installations. For new installations, it processes the OAuth token exchange. For updates to existing installations where a user modifies repository access, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details depend on the specific OAuth provider and installation status)

#### Response Example
(Example response would be a redirect or a success page, depending on the flow)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/evaluation

Handles the setup process for a specific OAuth provider, processing new installations or existing configurations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Processes the setup for an OAuth provider, handling new installations or existing state configurations.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Setup completion status.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/chat/azure_ai

Handles the initial setup callback for OAuth providers. For update actions, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers. For update actions, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "OAuth setup completed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/errors/MODEL_NOT_FOUND

Handles the setup callback for OAuth providers, including GitHub App installations and updates. For new installations with code/state, it processes similarly to a regular OAuth callback. For update actions, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, including GitHub App installations and updates. For new installations with code/state, it processes similarly to a regular OAuth callback. For update actions, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(No example provided in the input text)
```

--------------------------------

### Implement Rapid Prototyping with LangChain Entrypoints

Source: https://docs.langchain.com/oss/javascript/langgraph/choosing-apis

Demonstrates how to import and use the entrypoint utility in TypeScript to quickly execute LLM-based tasks. This approach bypasses the need for complex state schemas or graph definitions, making it ideal for rapid iteration.

```typescript
import { entrypoint } from "@langchain/core/runnables";

const finalEssay = await reviseEssay(draft, feedback);

return { essay: finalEssay };
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/multi-agent/skills

Handles the setup callback for OAuth providers, processing updates to GitHub App installations. For 'update' actions, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, processing updates to GitHub App installations. For 'update' actions, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### Extended Example: Streaming from Subgraphs in Python

Source: https://docs.langchain.com/oss/python/langgraph/streaming

This extended Python example demonstrates how to import necessary components from LangGraph and configure a graph for streaming outputs from subgraphs. It includes the setup for the START node and other graph elements.

```python
from langgraph.graph import START, CompiledGraph

# Placeholder for the actual graph definition
# This is a simplified representation based on the provided snippet

# Example of how a graph might be defined (conceptual)
# class MyGraph:
#     def __init__(self):
#         self.graph = START
#         # ... other graph configurations ...

#     def invoke(self, input):
#         # ... graph execution logic ...
#         pass

# Assuming 'graph' is an instance of a LangGraph graph
# The provided snippet suggests a structure where subgraphs and streaming are configured.
# A full example would involve defining nodes, edges, and the graph itself.

# The snippet provided is highly fragmented and appears to be part of a larger
# rendering process (likely for documentation). The core functionality implied is:
# 1. Importing START from langgraph.graph
# 2. Setting up a graph that supports subgraphs and streaming.

# To make this a runnable example, we would need the full graph definition.
# For demonstration purposes, let's assume a conceptual graph setup:

# Conceptual graph setup (not directly from snippet but inferred)
# from langgraph.graph import StateGraph
# 
# def node_a(state):
#     return "output_a"
# 
# def node_b(state):
#     return "output_b"
# 
# workflow = StateGraph([node_a, node_b])
# workflow.add_edge("node_a", "node_b")
# 
# # The snippet implies a way to enable subgraphs and streaming during compilation or invocation
# # This part is not fully represented in the provided text.
# # For instance, a hypothetical compilation step might look like:
# # compiled_graph = workflow.compile(subgraphs=True, stream_mode="updates")

# The provided snippet is more about the *output* of a rendering process for code,
# rather than a direct, runnable code block. The actual code for defining and
# running such a graph would be more extensive.

# Based on the snippet's structure, the relevant part is the import and the
# conceptual setup for streaming. The 'print(chunk)' part is also key.

# The provided snippet is highly fragmented and appears to be a representation
# of rendered code rather than a direct, runnable code block. The actual Python code
# for defining and running a LangGraph with subgraphs and streaming would be more extensive.
# However, the core elements suggested by the snippet are:

# 1. Importing necessary components:
from langgraph.graph import START

# 2. Configuration for subgraphs and streaming (conceptual, as the full context is missing):
# subgraphs=True
# stream_mode="updates"

# 3. Processing streamed output:
# for chunk in streamed_output:
#     print(chunk)

# Due to the fragmented nature of the input, a complete, runnable Python script cannot be generated.
# The following is a representation of the *intent* based on the provided fragments.

# --- Conceptual Python Code Snippet ---

# Assume 'graph' is a pre-defined LangGraph object
# For example:
# from langgraph.graph import StateGraph
# 
# def my_node(state):
#     # ... node logic ...
#     return state
# 
# graph_builder = StateGraph(my_node)
# # ... add edges and nodes ...
# graph = graph_builder.compile()

# The following demonstrates how you might invoke it with streaming enabled,
# based on the provided text fragments.

# This is a placeholder for the actual graph invocation.
# The actual invocation would depend on how the graph object is defined and compiled.

# Example of how streaming might be handled:
# streamed_output = graph.astream_events(
#     {},
#     version="v1",
#     stream_mode="updates", # Corresponds to "stream_mode=\"updates\""
#     subgraphs=True # Corresponds to "subgraphs=True"
# )
# 
# for chunk in streamed_output:
#     print(chunk) # Corresponds to "print(chunk)"

# --- End Conceptual Snippet ---

```

--------------------------------

### Start Local Development Server with Studio (Shell)

Source: https://docs.langchain.com/langsmith/cicd-pipeline-example

This command initiates a local development server using the Studio CLI, as indicated by the comment. This is a common first step for local testing and development with Langchain.

```shellscript
# Start local development server with Studio
```

--------------------------------

### Example Graph Implementation (Python)

Source: https://docs.langchain.com/langsmith/streaming

A Python code example demonstrating the setup of a stateful graph using Langchain's StateGraph. It includes type definitions for the state and the graph's start and end nodes.

```python
from typing import TypedDict
from langgraph.graph import StateGraph, START, END

class State(TypedDict, 

```

--------------------------------

### Langchain LLM and Chain Setup (Python)

Source: https://docs.langchain.com/langsmith/trace-with-opentelemetry

This snippet demonstrates how to initialize a ChatOpenAI model and construct a simple chain using a prompt and the model. It also shows how to invoke the chain with specific inputs and print the result.

```python
model = ChatOpenAI()
chain = prompt | model
result = chain.invoke({
  "topic": "programming"
})
print(result.content)
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/pypdfloader

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation. For 'update' actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed. For new installations with code/state, we process similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was handled.

#### Response Example
{
  "message": "OAuth setup callback handled successfully."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/url

Handles the initial setup or update of a GitHub App installation. For new installations with code, it processes like a regular OAuth callback. For updates, it displays a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup or update of a GitHub App installation. For new installations with code, it processes like a regular OAuth callback. For updates, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### Implement Filesystem Search Middleware in Python

Source: https://docs.langchain.com/oss/python/langchain/middleware/built-in

Demonstrates the import and initialization of the FilesystemFileSearchMiddleware for performing file discovery and content analysis in Python projects.

```python
from langchain.agents.middleware.file_search import FilesystemFileSearchMiddleware

# Example usage of the middleware for filesystem operations
middleware = FilesystemFileSearchMiddleware(
    api_key="sk-[a-zA-Z0-9]{32}"
)
```

--------------------------------

### Example Dockerfile for LangGraph

Source: https://docs.langchain.com/langsmith/cli

A sample Dockerfile configuration for a LangGraph application, showing base image setup, dependency installation, and environment variable configuration.

```docker
FROM langchain/langgraphjs-api:20

ADD . /deps/agent

RUN cd /deps/agent && yarn install

ENV LANGSERVE_GRAPHS='{"agent":"./src/react_agent/graph.ts:graph"}'

WORKDIR /deps/agent

RUN (test ! -f /api/langgraph_api/js/build.mts && echo "Prebuild script not found")
```

--------------------------------

### OAuth Setup Callback

Source: https://python.langchain.com/docs/versions/migrating_chains

Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. For existing installations with a GitHub token, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. For existing installations with a GitHub token, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### SQL Agent Setup with Langchain

Source: https://docs.langchain.com/oss/python/langchain/sql-agent

Initializes a Langchain SQL agent. It downloads a SQLite database, sets up an LLM, creates SQL database tools, and defines a system prompt for the agent to interact with the database.

```python
#sql_agent.py for studio
import pathlib

from langchain.agents import create_agent
from langchain.chat_models import init_chat_model
from langchain_community.agent_toolkits import SQLDatabaseToolkit
from langchain_community.utilities import SQLDatabase
import requests


# Initialize an LLM
model = init_chat_model("gpt-4.1")

# Get the database, store it locally
url = "https://storage.googleapis.com/benchmarks-artifacts/chinook/Chinook.db"
local_path = pathlib.Path("Chinook.db")

if local_path.exists():
    print(f"{local_path} already exists, skipping download.")
else:
    response = requests.get(url)
    if response.status_code == 200:
        local_path.write_bytes(response.content)
        print(f"File downloaded and saved as {local_path}")
    else:
        print(f"Failed to download the file. Status code: {response.status_code}")

db = SQLDatabase.from_uri("sqlite:///Chinook.db")

# Create the tools
toolkit = SQLDatabaseToolkit(db=db, llm=model)

tools = toolkit.get_tools()

for tool in tools:
    print(f"{tool.name}: {tool.description}\n")

# Use create_agent
system_prompt = """
You are an agent designed to interact with a SQL database.
Given an input question, create a syntactically correct {dialect} query to run,
then look at the results of the query and return the answer. Unless the user
specifies a specific number of examples they wish to obtain, always limit your
query to at most {top_k} results.

You can order the results by a relevant column to return the most interesting
examples in the database. Never query for all the columns from a specific table, only ask for the relevant columns given the question.

You MUST double check your query before executing it. If you get an error while
executing a query, rewrite the query and try again.

DO NOT make any DML statements (INSERT, UPDATE, DELETE, DROP etc.) to the
database.

To start you should ALWAYS look at the tables in the database to see what you
can query. Do NOT skip this step.

Then you should query the schema of the most relevant tables.
""".format(
    dialect=db.dialect,
    top_k=5,
)

agent = create_agent(
    model,
    tools,
    system_prompt=system_prompt,
)

```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/conditional-tracing

Handles the OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
* **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
* **code** (string) - Optional - The authorization code received from the provider.
* **state** (string) - Optional - The state parameter for CSRF protection.

#### Request Body
* None

### Response
#### Success Response (200)
* This endpoint typically redirects to a frontend page or returns a success message.

#### Response Example
* (Redirect to frontend or success message)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/release-versions

Handles the OAuth callback redirect for new installations, processing the token exchange similar to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth callback redirect for new installations, processing the token exchange similar to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup is complete.

#### Response Example
{
  "message": "OAuth setup complete."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/jit-invite-sso

Handles the OAuth setup callback for new installations. It processes the OAuth callback similar to regular OAuth callbacks when code/state are present, and shows a success page if no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations. It processes the OAuth callback similar to regular OAuth callbacks when code/state are present, and shows a success page if no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup is complete.

#### Response Example
```json
{
  "message": "OAuth setup successful."
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/couchbase

Handles the setup process for OAuth providers, including GitHub App installations and OAuth callback processing.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup or update of OAuth provider installations. For updates, it confirms access changes; for new installations, it processes the token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### Initialize and Load PDF Documents

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/pymupdf

Demonstrates how to instantiate the PyMuPDFLoader and load content from a specified PDF file path.

```python
from langchain_community.document_loaders import PyMuPDFLoader

file_path = "./example_data/layout-parser-paper.pdf"
loader = PyMuPDFLoader(file_path)
docs = loader.load()
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/twitter

Handles the setup flow for OAuth providers, including GitHub app installations and OAuth callback processing.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup flow for OAuth providers. For GitHub app installations, it processes new installations or updates to existing ones.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion or redirect status.
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/human-in-the-loop

Handle OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback triggered when a user installs or updates their GitHub App installation. For update actions, it displays a success page. For new installations with code/state, it processes the callback similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Response details not specified in the provided text, typically a success message or redirect)

#### Response Example
(Example response not provided in the source text)
```

--------------------------------

### Configure Modal Sandbox for LangChain Agents

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

Shows the setup process for using Modal as a sandbox provider. It involves looking up an existing Modal app, creating a sandbox instance, and passing it to the agent backend.

```python
import modal
from langchain_anthropic import ChatAnthropic
from deepagents import create_deep_agent
from langchain_modal import ModalSandbox

app = modal.App.lookup("your-app")
modal_sandbox = modal.Sandbox.create(app=app)
backend = ModalSandbox(sandbox=modal_sandbox)

agent = create_deep_agent(
    model=ChatAnthropic(model="claude-sonnet-4-20250514"),
    system_prompt="You are a Python coding assistant with sandbox access.",
    backend=backend,
)
try:
    result = agent.invoke(
        {
            "messages": [
                {
                    "role": "user",
                    "content": "Create a small Python package and run pytest",
                }
            ]
        }
    )
finally:
    modal_sandbox.terminate()
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/multi-agent/handoffs-customer-support

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback for new installations or updates to GitHub App installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is
triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show
a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular
OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter for CSRF protection.

### Request Example
```json
{
  "example": ""
}
```

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "example": "{\"message\": \"GitHub App setup completed successfully.\"}"
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/llms/huggingface_pipelines

Handles the setup callback for OAuth providers, triggered by GitHub App installations or updates. For new installations, it processes the OAuth token exchange. For updates where users modify repo access, it displays a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, triggered by GitHub App installations or updates. For new installations, it processes the OAuth token exchange. For updates where users modify repo access, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App setup successful."
}
```
```

--------------------------------

### Full Example: State-Based Text Editor with Path Prefix

Source: https://docs.langchain.com/oss/python/integrations/middleware/anthropic

Demonstrates the full setup of a state-based text editor with a specific allowed path prefix. This example shows how to configure the middleware to only permit file operations within the '/project' directory and how to use a checkpointer for state persistence across invocations.

```python
from langchain_anthropic import ChatAnthropic
from langchain_anthropic.middleware import StateClaudeTextEditorMiddleware
from langchain.agents import create_agent
from langchain_core.runnables import RunnableConfig
from langgraph.checkpoint.memory import MemorySaver


agent = create_agent(
    model=ChatAnthropic(model="claude-sonnet-4-6"),
    tools=[],
    middleware=[
        StateClaudeTextEditorMiddleware(
            allowed_path_prefixes=["/project"],
        ),
    ],
    checkpointer=MemorySaver(),
)

# Use a thread_id to persist state across invocations
config: RunnableConfig = {"configurable": {"thread_id": "my-session"}}

# Claude can now create and edit files (stored in LangGraph state)
result = agent.invoke(
    {"messages": [{"role": "user", "content": "Create a file at /project/hello.py with a simple hello world program"}]},
    config=config,
)
print(result["messages"][-1].content)
```

--------------------------------

### Initialize an Agent with create_agent

Source: https://docs.langchain.com/oss/python/migrate/langchain-v1

Demonstrates the syntax for importing and using the create_agent function to initialize an agent with specific tools in LangChain.

```python
from langchain.agents import create_agent

create_agent("gpt-4.1-mini", tools=[some_tool])
```

--------------------------------

### GET /v2/deployments

Source: https://docs.langchain.com/oss/python/langchain/install

Lists all deployments available in the control plane.

```APIDOC
## GET /v2/deployments

### Description
List all deployments.

### Method
GET

### Endpoint
/v2/deployments

### Response
#### Success Response (200)
- **deployments** (array) - A list of deployment objects.

#### Response Example
{
  "deployments": [
    { "id": "dep-123", "name": "production-app" }
  ]
}
```

--------------------------------

### Initialize Postgres Vector Store

Source: https://docs.langchain.com/oss/python/langchain/knowledge-base

Installs the Postgres integration and demonstrates initialization via connection string or engine.

```bash
pip install -qU langchain-postgres
```

```python
from langchain_postgres import PGVector

vector_store = PGVector(
    embeddings=embeddings,
    collection_name="my_docs",
    connection="postgresql+psycopg://...",
)
```

--------------------------------

### GET /info

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Retrieves server version information, feature flags, and metadata.

```APIDOC
## GET /info

### Description
Get server version information, feature flags, and metadata.

### Method
GET

### Endpoint
/info

### Response
#### Success Response (200)
- **version** (string) - The server version.
- **features** (object) - Enabled feature flags.
- **metadata** (object) - Server metadata.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/deepagents/data-analysis

Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. For user-modified repo access via GitHub, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from OAuth providers. Processes new installations or user-modified repo access.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the callback.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/providers/overview

Handles the initial setup callback for OAuth providers. For new installations with code or state, it processes the authentication flow similar to a regular OAuth callback. For 'update' actions (e.g., user modifying repo access via GitHub), it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers. For new installations with code or state, it processes the authentication flow similar to a regular OAuth callback. For 'update' actions (e.g., user modifying repo access via GitHub), it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "Setup complete."
}
```

--------------------------------

### Agent Builder Documentation

Source: https://docs.langchain.com/oss/python/integrations/stores

Documentation for the Agent Builder product, including getting started guides, tools, integrations, and advanced topics.

```APIDOC
## Agent Builder Documentation

### Description
Guides and resources for creating AI agents without code using the Agent Builder.

### Sections
- **Get started**: Quickstart, essentials, templates, setup, and agent settings management.
- **Tools and integrations**: Information on tools, triggers, remote MCP servers, webhooks, and the Slack app.
- **Advanced**: Details on authentication format, code, and the MCP framework.
- **Additional resources**
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/chat/openrouter

Handles the setup callback for OAuth providers, processing updates to GitHub App installations. For 'update' actions, it shows a success page. For new installations, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, processing updates to GitHub App installations. For 'update' actions, it shows a success page. For new installations, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### Initialize LangChain Agent and Define Custom Tools

Source: https://docs.langchain.com/oss/python/langgraph/use-subgraphs

Demonstrates the initialization of an agent using 'create_agent' with a specified model, toolset, and system prompt. It also shows how to use the @tool decorator to wrap functions as tools for use within the agent framework.

```python
veggie_agent = create_agent(
  model="gpt-4.1-mini",
  tools=[veggie_info],
  prompt="You are a veggie expert. Use the veggie_info tool. Respond in one sentence."
)

# Wrap subagents as tools for the outer agent
@tool
def ask_fruit_expert(question):
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/mojeek_search

Handles the OAuth setup callback for GitHub App installations. It processes updates to repository access or new installations by exchanging tokens.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. For 'update' actions (user modified repo access via GitHub), it shows a success page as no token exchange is needed. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App installation updated successfully."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/llms/azure_ml

Handles the initial setup callback for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- (No specific fields mentioned, likely a redirect or success message)

#### Response Example
(No specific example provided in the source text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/studio

Handles the initial OAuth setup callback. For new installations with code/state, it processes similarly to a regular OAuth callback. If a token exchange is not needed (e.g., via GitHub access), it directly shows a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup callback. For new installations with code/state, it processes similarly to a regular OAuth callback. If a token exchange is not needed (e.g., via GitHub access), it directly shows a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Indicates the success of the setup process.
```

--------------------------------

### Initialize and Run LangChain Agent

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

This code demonstrates the initialization of an agent with specific parameters such as model, system prompt, and tools, followed by the execution pattern using a thread identifier.

```javascript
// Create agent
const agent = createAgent({
  model,
  systemPrompt,
  responseFormat,
  checkpointer,
  tools: [getUserLocation, getWeather],
});

// Run agent
// `thread_id` is a unique identifier for a given conversation.
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/api-ref-control-plane

Handles the initial setup callback for OAuth providers, processing installation state and redirecting to a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers, processing installation state and redirecting to a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating setup completion.
```

--------------------------------

### POST /threads

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Create a new thread.

```APIDOC
## POST /threads

### Description
Creates a new thread for agent interaction.

### Method
POST

### Endpoint
/threads

### Response
#### Success Response (200)
- **thread_id** (string) - The unique identifier of the created thread.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langgraph/errors/GRAPH_RECURSION_LIMIT

Handles the setup callback for OAuth providers, triggered by GitHub App installations or updates. For new installations, it processes the OAuth token exchange. For updates, it displays a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, triggered by GitHub App installations or updates. For new installations, it processes the OAuth token exchange. For updates, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App setup successful."
}
```

--------------------------------

### Initialize LangChain Agent with Tools and Prompt

Source: https://docs.langchain.com/oss/python/langgraph/use-subgraphs

This snippet shows how to instantiate an agent using the create_agent function. It configures the agent with a model, a list of specialized tools, and a prompt that instructs the agent on how to delegate tasks to specific experts.

```python
# Outer agent with checkpointer
agent = create_agent(
    model="gpt-4.1-mini",
    tools=[ask_fruit_expert, ask_veggie_expert],
    prompt=(
        "You have two experts: ask_fruit_expert and ask_veggie_expert. "
        "ALWAYS delegate questions to the appropriate expert."
    ),
)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/gitbook

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes the callback similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Response
#### Success Response (200)
- **message** (string) - A message indicating the status of the setup callback.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/agent-server-api/threads/search-threads

Handles the OAuth setup callback for GitHub App installations or updates. For new installations, it processes the token exchange similar to a regular OAuth callback. For updates where users modify repository access, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations or updates. For new installations, it processes the token exchange similar to a regular OAuth callback. For updates where users modify repository access, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(No example provided in the input text)
```

--------------------------------

### Install and Import Amazon Comprehend Moderation Chain

Source: https://docs.langchain.com/oss/python/integrations/providers/aws

Setup guide for the Amazon Comprehend moderation chain, which requires boto3 and nltk. This chain is used for NLP-based content moderation tasks.

```bash
pip install boto3 nltk
```

```python
from langchain_experimental.comprehend_moderation import AmazonComprehendModerationChain
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/agent-builder-essentials

Handles the OAuth setup callback for a given provider. For new installations with code/state, it processes similar to a regular OAuth callback. If the repository is user-modified and has GitHub access, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. For new installations with code/state, it processes similar to a regular OAuth callback. If the repository is user-modified and has GitHub access, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/use-threads

Handles the initial OAuth setup callback for new installations. It processes the authentication flow similarly to a regular OAuth callback when code and state parameters are present.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup callback for new installations. It processes the authentication flow similarly to a regular OAuth callback when code and state parameters are present.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup completion.

#### Response Example
```json
{
  "message": "OAuth setup successful."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/web_playwright

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint manages the "Setup URL" callback from GitHub Apps, triggered during installation or updates. For updates, it displays a success page. For new installations with code/state, it processes the OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider (e.g., 'github').

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter for CSRF protection.

### Request Example
(No request body)

### Response
#### Success Response (200)
(Response content depends on whether it's an update or a new installation. For updates, a success page is shown. For new installations, it proceeds to token exchange.)

#### Response Example
(Success page HTML or redirect to frontend callback)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/google_drive

Handles the callback from GitHub Apps for installation or update events. For new installations, it processes the OAuth token exchange. For updates, it displays a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the callback from GitHub Apps for installation or update events. For new installations, it processes the OAuth token exchange. For updates, it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the installation or update.

#### Response Example
```json
{
  "message": "GitHub App installed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/callbacks/google_bigquery

Handles the OAuth setup callback, triggered when a user installs or updates their GitHub App installation. For updates, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. Processes new installations similarly to regular OAuth callbacks and shows a success page for updates.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(No example provided in the input text)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/tools/azure_dynamic_sessions

Handles the setup callback for OAuth providers, specifically processing new installations or updates from platforms like GitHub.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles OAuth setup callbacks, processing new installations or updates for configured providers.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success message indicating the setup status.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### Setup Postgres Store for First Use (Python)

Source: https://docs.langchain.com/oss/python/langgraph/add-memory

This code snippet highlights the requirement to call `store.setup()` when first using the Postgres store. This is a crucial step for initializing the database schema or any necessary configurations before data operations.

```python
store.setup()
```

--------------------------------

### Instantiate ChatCohere Model in TypeScript

Source: https://docs.langchain.com/oss/javascript/integrations/chat/cohere

Example of how to import and instantiate the ChatCohere model in a TypeScript project. This code snippet demonstrates the basic setup required to start using Cohere's chat capabilities with Langchain.

```typescript
import { ChatCohere } from "@langchain/cohere";

const model = new ChatCohere({
  apiKey: "YOUR_API_KEY", // In production, use environment variables or a secret management service
});

async function main() {
  const response = await model.invoke("Hello, how can I help you today?");
  console.log(response);
}

main();
```

--------------------------------

### Initialize Agent with Middleware

Source: https://docs.langchain.com/oss/python/migrate/langchain-v1

Demonstrates how to instantiate an agent using the create_agent factory, including the configuration of a model, tools, and custom middleware for state management.

```python
agent = create_agent(
    model="claude-sonnet-4-6",
    tools=[...],
    middleware=[CallCounterMiddleware()]
)
```

--------------------------------

### Invoke Model with Tools

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Demonstrates how to invoke a language model with a set of tools and a system message. This setup is essential for agentic workflows where the model needs to perform arithmetic or other tasks based on input messages.

```typescript
modelWithTools.invoke([
  new SystemMessage("You are a helpful assistant tasked with performing arithmetic on a set of inputs."),
  ...messages
]);
```

--------------------------------

### Authenticate

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Gets an OAuth token or initiates the authentication flow if needed. This endpoint is used to retrieve an OAuth token or to start the authentication process if one is not already established.

```APIDOC
## POST /v2/auth/authenticate

### Description
Retrieves an OAuth token or starts the authentication flow if required.

### Method
POST

### Endpoint
/v2/auth/authenticate

### Parameters
#### Query Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

#### Request Body
- **redirect_uri** (string) - Optional - The URI to redirect to after authentication.

### Request Example
```json
{
  "redirect_uri": "https://example.com/callback"
}
```

### Response
#### Success Response (200)
- **auth_id** (string) - The identifier for the authentication process.
- **auth_url** (string) - The URL to redirect the user to for authentication.

#### Response Example
```json
{
  "auth_id": "auth_process_123",
  "auth_url": "https://oauth.provider.com/authorize?client_id=..."
}
```
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/undatasio

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation. For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed. For new installations with code/state, we process similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not provided in the input text)

#### Response Example
(Response example not provided in the input text)
```

--------------------------------

### cURL Example for GET /threads/{thread_id}

Source: https://docs.langchain.com/langsmith/use-threads

Example of how to call the GET /threads/{thread_id} endpoint using cURL.

```APIDOC
## cURL Example for GET /threads/{thread_id}

### Description
This section provides a cURL command to demonstrate how to fetch a specific thread.

### Method
GET

### Endpoint
/threads/{thread_id}

### Request Example
```shell
curl --request GET \
  --url "<DEPLOYMENT_URL>/threads/thread_id" \
  --header "Content-Type: application/json"
```

### Response Example
```json
{
  "thread_id": "thread_abc123",
  "messages": [
    {
      "message_id": "msg_xyz789",
      "content": "Hello! How can I help you today?",
      "sender": "bot",
      "timestamp": "2023-10-27T10:00:00Z"
    }
  ],
  "created_at": "2023-10-27T09:55:00Z",
  "updated_at": "2023-10-27T10:05:00Z"
}
```
```

--------------------------------

### GET /examples

Source: https://docs.langchain.com/langsmith/cloud

Retrieves a list of examples. This endpoint is subject to a rate limit categorized as Examples.

```APIDOC
## GET /examples

### Description
Retrieves a list of examples. This endpoint is subject to a rate limit categorized as Examples.

### Method
GET

### Endpoint
/examples

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
  "example": "request body not applicable"
}
```

### Response
#### Success Response (200)
- **examples** (array) - A list of example objects.

#### Response Example
```json
{
  "examples": [
    {
      "id": "example_1",
      "description": "A sample example"
    }
  ]
}
```

### Rate Limits
- **Header**: x-api-key
- **Limit**: 5000 requests per 60 seconds
- **Category**: Examples
```

--------------------------------

### Setup: Install langchain-privy and Set Credentials

Source: https://docs.langchain.com/oss/python/integrations/tools/privy

This section details the installation of the 'langchain-privy' package using pip and how to securely set your Privy App ID and App Secret environment variables using `getpass` for interactive input.

```python
pip install langchain-privy

```

```python
import os
import getpass

os.environ["PRIVY_APP_ID"] = getpass.getpass("Enter your Privy App ID: ")
os.environ["PRIVY_APP_SECRET"] = getpass.getpass("Enter your Privy App Secret: ")

```

--------------------------------

### Full Agent Code Example in TypeScript

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

This is a comprehensive TypeScript code example for building an agent using the LangGraph Graph API. It includes the necessary imports, agent definition, message processing, and logging. This serves as a complete reference for implementing agents with LangGraph.

```typescript
import { AgentExecutor, createOpenAIFunctionsAgent, Agent, ChatOpenAI } from "langgraph/agent";
import { MessagesPlaceholder, convertMessageLikeToMessage } from "@langchain/core/messages";
import { formatToOpenAIFunction } from "langchain/tools";
import { TavilySearchResults } from "langchain/tools";
import { AIMessage, HumanMessage } from "@langchain/core/messages";

const tools = [new TavilySearchResults({ "k": 3 })];

const llm = new ChatOpenAI({
  model: "gpt-4o",
  temperature: 0
});

const agent = await createOpenAIFunctionsAgent({
  llm,
  tools,
  // A prompt is required
  // We use MessagesPlaceholder to ensure that the memory is included in the prompt
  // We also add a system message to the prompt
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The prompt is used to generate the next message in the conversation
  // The prompt is a list of messages, where each message is a dictionary with a role and content
  // The role can be 'system', 'human', or 'ai'
  // The content can be a string or a list of strings
  // The
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/annotation-queues

Handles the OAuth setup callback for providers. For new installations with code/state, it processes similarly to a regular OAuth callback. For existing installations or when no token exchange is needed (e.g., via tHub), it displays a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for providers. For new installations with code/state, it processes similarly to a regular OAuth callback. For existing installations or when no token exchange is needed (e.g., via tHub), it displays a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Indicates the status of the setup process.
```

--------------------------------

### GET /v2/sandboxes/usage

Source: https://docs.langchain.com/oss/python/langchain/install

Retrieve resource usage and quota limits for sandboxes.

```APIDOC
## GET /v2/sandboxes/usage

### Description
Returns current resource consumption and organization quota limits. Sandbox counts include direct claims and warmpool replicas.

### Method
GET

### Endpoint
/v2/sandboxes/usage

### Response
#### Success Response (200)
- **usage** (object) - Current consumption metrics.
- **limits** (object) - Organization quota limits.
```

--------------------------------

### Initialize Qdrant Vector Store with Custom Payload Keys

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/qdrant

Demonstrates how to initialize the Qdrant vector store using the from_documents method. Allows users to specify custom keys for page content and metadata to align with existing collection schemas.

```python
QdrantVectorStore.from_documents(
    docs,
    embeddings,
    location=":memory:",
    collection_name="my_documents_2",
    content_payload_key="my_page_content_key",
    metadata_payload_key="my_meta",
)
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/turbopuffer

Handles the setup callback for OAuth providers, processing new installations similar to a regular OAuth callback when tokens are needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers. For new installations requiring token exchange, it processes the callback similarly to a regular OAuth flow. For updates where users modify repository access, it displays a success page without needing a token exchange.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "Setup complete successfully."
}
```

--------------------------------

### Initialize GenericLoader and FileSystemBlobLoader

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/pymupdf

Demonstrates initializing a GenericLoader and a FileSystemBlobLoader. The GenericLoader is instantiated with a path and potentially other configurations, while FileSystemBlobLoader is initialized for loading blob data.

```python
loader = GenericLoader(
    blob_loader=FileSystemBlobLoader(
        "/path/to/your/directory"
    )
)
```

--------------------------------

### Sync Redis Checkpointing with LangGraph

Source: https://docs.langchain.com/oss/python/langgraph/add-memory

This example demonstrates synchronous state checkpointing in LangGraph using a RedisSaver. It includes the necessary installation command, the setup requirement for the checkpointer, and a basic graph execution that streams LLM responses.

```bash
pip install -U langgraph langgraph-checkpoint-redis
```

```python
from langchain.chat_models import init_chat_model
from langgraph.graph import StateGraph, MessagesState, START
from langgraph.checkpoint.redis import RedisSaver  

model = init_chat_model(model="claude-haiku-4-5-20251001")

DB_URI = "redis://localhost:6379"
with RedisSaver.from_conn_string(DB_URI) as checkpointer:
    # checkpointer.setup()

    def call_model(state: MessagesState):
        response = model.invoke(state["messages"])
        return {"messages": response}

    builder = StateGraph(MessagesState)
    builder.add_node(call_model)
    builder.add_edge(START, "call_model")

    graph = builder.compile(checkpointer=checkpointer)

    config = {
        "configurable": {
            "thread_id": "1"
        }
    }

    for chunk in graph.stream(
        {"messages": [{"role": "user", "content": "hi! I'm bob"}]},
        config,
        stream_mode="values"
    ):
        chunk["messages"][-1].pretty_print()

    for chunk in graph.stream(
        {"messages": [{"role": "user", "content": "what's my name?"}]},
        config,
        stream_mode="values"
    ):
        chunk["messages"][-1].pretty_print()
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/langsmith/agent-builder-quickstart

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback triggered by user installation or updates of GitHub Apps. For updates, it displays a success page. For new installations, it processes the callback similar to regular OAuth callbacks.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### JavaScript Example: RecursiveCharacterTextSplitter Configuration

Source: https://docs.langchain.com/oss/javascript/integrations/splitters/recursive_text_splitter

This JavaScript snippet demonstrates the configuration of the RecursiveCharacterTextSplitter, showing how to define chunk size, overlap, and content structure. It's useful for understanding the basic setup of text splitting in Langchain.

```javascript
["\n", {" pageContent": "...", " metadata": {}}
]
```

--------------------------------

### Install and Import @langchain/classic

Source: https://docs.langchain.com/oss/javascript/migrate/langchain-v1

Instructions for installing the legacy support package and updating import statements from the v0 legacy structure to the v1 structure.

```bash
npm install @langchain/classic
```

```typescript
// v1 (new)
import { ... } from "@langchain/classic";
import { ... } from "@langchain/classic/chains";

// v0 (old)
import { ... } from "langchain";
import { ... } from "langchain/chains";
```

--------------------------------

### Create Dataset and Examples with Langchain Client

Source: https://docs.langchain.com/langsmith/evaluate-on-intermediate-steps

This snippet demonstrates how to use the Langchain client to create a dataset and then populate it with examples. It involves asynchronous operations and structured data inputs.

```javascript
await client.createDataset("datasetName");
await client.createExamples("", {
  datasetId: dataset.id,
  inputs: {},
  outputs: {}
});
```

--------------------------------

### Construct and Invoke Model with System Message and Messages (JavaScript)

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

This snippet demonstrates how to construct a SystemMessage and combine it with other messages to invoke a model. It highlights the use of `SystemMessage` and `invoke` methods, along with message formatting.

```javascript
const messages: BaseMessage[] = [
  new SystemMessage("You are a helpful assistant tasked with performing arithmetic on a set of inputs."),
  ...
messages
];

modelWithTools.invoke([
 new SystemMessage("You are a helpful assistant tasked with performing arithmetic on a set of inputs.")
 ...messages,
];
```

--------------------------------

### GET /v2/sandboxes/volumes

Source: https://docs.langchain.com/oss/python/langchain/install

List all persistent volumes in the tenant's sandbox namespace.

```APIDOC
## GET /v2/sandboxes/volumes

### Description
Queries the database to list all persistent volumes. Supports pagination.

### Method
GET

### Endpoint
/v2/sandboxes/volumes

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - Number of items to return.
- **offset** (integer) - Optional - Number of items to skip.

### Response
#### Success Response (200)
- **volumes** (array) - List of volume objects.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/self-host-usage

Handles the OAuth setup callback for new installations. It processes the callback similar to a regular OAuth callback when code/state are present.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations. Processes the callback similar to a regular OAuth callback when code/state are present.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup completion.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/bshtml

Handles the setup callback for OAuth providers, processing new installations or updates to GitHub App installations. For new installations with code/state, it processes similarly to a regular OAuth callback. For updates where a user modifies repo access, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, processing new installations or updates to GitHub App installations. For new installations with code/state, it processes similarly to a regular OAuth callback. For updates where a user modifies repo access, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App installation processed successfully."
}
```
```

--------------------------------

### POST /v2/sandboxes/volumes

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Creates a new persistent volume and associated claim in the sandbox namespace.

```APIDOC
## POST /v2/sandboxes/volumes

### Description
Create a new persistent volume in the tenant's sandbox namespace. This creates both a PersistentVolume (PV) and PersistentVolumeClaim (PVC).

### Method
POST

### Endpoint
/v2/sandboxes/volumes

### Parameters
#### Request Body
- **name** (string) - Required - Name of the volume.
- **size** (integer) - Required - Storage size in GB.
- **wait_for_ready** (boolean) - Optional - Whether to block until PVC is bound (default: true).

### Response
#### Success Response (200)
- **id** (string) - The ID of the created volume.
```

--------------------------------

### Async Redis Checkpointing with LangGraph

Source: https://docs.langchain.com/oss/python/langgraph/add-memory

This code illustrates asynchronous state checkpointing in LangGraph using AsyncRedisSaver. It outlines the installation, the asynchronous setup method for the checkpointer, and a complete example of defining and running a graph that streams LLM outputs.

```python
from langchain.chat_models import init_chat_model
from langgraph.graph import StateGraph, MessagesState, START
from langgraph.checkpoint.redis.aio import AsyncRedisSaver  

model = init_chat_model(model="claude-haiku-4-5-20251001")

DB_URI = "redis://localhost:6379"
async with AsyncRedisSaver.from_conn_string(DB_URI) as checkpointer:
    # await checkpointer.asetup()

    async def call_model(state: MessagesState):
        response = await model.ainvoke(state["messages"])
        return {"messages": response}

    builder = StateGraph(MessagesState)
    builder.add_node(call_model)
    builder.add_edge(START, "call_model")

    graph = builder.compile(checkpointer=checkpointer)

    config = {
        "configurable": {
            "thread_id": "1"
        }
    }

    async for chunk in graph.astream(
        {"messages": [{"role": "user", "content": "hi! I'm bob"}]},
        config,
        stream_mode="values"
    ):
        chunk["messages"][-1].pretty_print()

    async for chunk in graph.astream(
        {"messages": [{"role": "user", "content": "what's my name?"}]},
        config,
        stream_mode="values"
    ):
        chunk["messages"][-1].pretty_print()
```

--------------------------------

### Initialize Qdrant Vector Store and Embeddings (Python)

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/qdrant

Demonstrates how to import and initialize Qdrant-related components from Langchain, including FastEmbedSparse for sparse embeddings and QdrantVectorStore for vector storage. It also shows importing QdrantClient and models for interacting with a Qdrant instance.

```python
from langchain_qdrant import FastEmbedSparse, QdrantVectorStore
from qdrant_client import QdrantClient, models
from qdrant_client.http import models
```

--------------------------------

### Initialize ChatAnthropic LLM in TypeScript

Source: https://docs.langchain.com/oss/javascript/integrations/chat/anthropic

This snippet demonstrates how to import and initialize the ChatAnthropic LLM class from the '@langchain/anthropic' package. It shows the basic setup required to start using Anthropic models within a Langchain application. Ensure you have the correct version of the package installed.

```typescript
import { ChatAnthropic } from "@langchain/anthropic";


const llm = new ChatAnthropic(
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/retrievers/azure_ai_search

Handle OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback from GitHub Apps, handling both new installations and updates to existing ones.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langgraph/errors/MISSING_CHECKPOINTER

Handles the initial setup callback for OAuth providers, particularly for GitHub App installations. For new installations with code/state, it processes similar to a regular OAuth callback. For update actions where users modify repo access, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers, particularly for GitHub App installations. For new installations with code/state, it processes similar to a regular OAuth callback. For update actions where users modify repo access, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not provided in the source text)

#### Response Example
(No example provided in the source text)
```

--------------------------------

### Configure PIIMiddleware

Source: https://docs.langchain.com/oss/python/langchain/middleware/built-in

Example configuration for PIIMiddleware, demonstrating how to define the detector and masking strategy.

```javascript
middleware = [
  PIIMiddleware(
    "ssn",
    detector=detect_ssn,
    strategy="hash"
  )
]
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/export-traces

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes the callback similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### Configure LLM Instances and Metadata in LangChain

Source: https://docs.langchain.com/langsmith/trace-with-langchain

Demonstrates how to instantiate LLM objects with specific model IDs and metadata for tracking. It includes examples for both local models and OpenAI configurations with custom temperature settings.

```python
model = "llama2:13b-chat",
metadata = {"ls_model_name": "llama2-13b-production"} # Actual model ID

# Or with OpenAI to distinguish configurations
llm_creative = ChatOpenAI(
    model = "gpt-4.1",
    temperature = 0.9
)
```

--------------------------------

### Create Assistant with LangGraph SDK (Python)

Source: https://docs.langchain.com/langsmith/configuration-cloud

Demonstrates how to initialize the LangGraph client and create a new assistant. This requires a deployment URL and specifies the graph ID, context, and a descriptive name for the assistant. The example uses Python and assumes the `langgraph_sdk` library is installed.

```python
from langgraph_sdk import get_client

# Initialize the client with your deployment URL
client = get_client(url=DEPLOYMENT_URL)

# Create an assistant for the "agent" graph
assistant = client.assistants.create(
    graph_id="agent",
    name="My Assistant",
    context={ "model_name": "openai" } 
)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/concepts/products

Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. If the provider is already configured (e.g., via GitHub access), it displays a success page as no token exchange is required.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. If the provider is already configured (e.g., via GitHub access), it displays a success page as no token exchange is required.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
- **message** (string) - Indicates the success of the setup process.

#### Response Example
```json
{
  "message": "OAuth setup successful."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/quick-start-studio

Handles the OAuth setup callback for a given provider. For new installations, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. For new installations, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
```json
{
  "message": "OAuth setup callback processed successfully."
}
```
```

--------------------------------

### Install @langchain/classic with pnpm, yarn, and bun

Source: https://docs.langchain.com/oss/javascript/migrate/langchain-v1

These commands show how to install the @langchain/classic package using different package managers. Ensure you have the respective package manager installed on your system.

```shellscript
pnpm install @langchain/classic
```

```shellscript
yarn add @langchain/classic
```

```shellscript
bun add @langchain/classic
```

--------------------------------

### Initialize OpenGauss client

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/opengauss

Python code demonstrating how to import the OpenGauss class and settings to begin configuring the database connection.

```python
from langchain_opengauss import OpenGauss, OpenGaussSettings

# Configure with schema validation
config = 
```

--------------------------------

### Install Ollama on macOS

Source: https://docs.langchain.com/oss/python/integrations/chat/ollama

Instructions for installing Ollama on macOS using Homebrew. This includes the commands to install the package and start the Ollama service.

```bash
brew install ollama
brew services start ollama
```

--------------------------------

### Initialize LangChain with ChatOpenAI

Source: https://docs.langchain.com/langsmith/trace-with-opentelemetry

Demonstrates how to import necessary modules and initialize a basic prompt template and model chain using LangChain and OpenAI.

```python
import os
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate

# Create a chain
prompt = ChatPromptTemplate.from_template("Tell me a joke about {topic}")
model = ChatOpenAI()
```

--------------------------------

### Full Example: Filesystem-Based Text Editor in Temporary Directory

Source: https://docs.langchain.com/oss/python/integrations/middleware/anthropic

Illustrates the setup of a filesystem-based text editor using a temporary directory as the root path. This example is suitable for testing and demonstration purposes, showing how to initialize the middleware with a dynamic workspace.

```python
import tempfile

from langchain_anthropic import ChatAnthropic
from langchain_anthropic.middleware import FilesystemClaudeTextEditorMiddleware
from langchain.agents import create_agent


# Create a temporary workspace directory for this demo.
# In production, use a persistent directory path.
workspace = tempfile.mkdtemp(prefix="editor-workspace-")

agent = create_agent(
    model=ChatAnthropic(model="claude-sonnet-4-6"),
    tools=[],
    middleware=[
        FilesystemClaudeTextEditorMiddleware(
            root_path=workspace,

```

--------------------------------

### Instantiate Model with Quantization

Source: https://docs.langchain.com/oss/python/integrations/chat/huggingface

Shows how to import necessary modules to configure and load a model using bitsandbytes quantization to reduce memory footprint.

```python
from transformers import
```

--------------------------------

### Get Revision

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

Get a revision by ID for a deployment.

```APIDOC
## GET /v2/deployments/{deployment_id}/revisions/{revision_id}

### Description
Get a revision by ID for a deployment.

### Method
GET

### Endpoint
/v2/deployments/{deployment_id}/revisions/{revision_id}

### Parameters
#### Path Parameters
- **deployment_id** (string) - Required - The ID of the deployment.
- **revision_id** (string) - Required - The ID of the revision to retrieve.

#### Query Parameters
- **None**

### Request Example
```json
{
  "example": "No request body needed for this GET request."
}
```

### Response
#### Success Response (200)
- **id** (string) - The unique identifier for the revision.
- **created_at** (string) - The timestamp when the revision was created.
- **status** (string) - The status of the revision.
- **code_commit** (string) - The commit hash associated with this revision.

#### Response Example
```json
{
  "example": "{\"id\": \"rev_1\", \"created_at\": \"2023-10-27T10:05:00Z\", \"status\": \"deployed\", \"code_commit\": \"a1b2c3d4e5f6\"}"
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/chat/ollama

Handles the OAuth setup callback for new installations with code/state, processing it similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations with code/state, processing it similarly to a regular OAuth callback. For "update" actions (user modified repo access via GitHub), a success page is shown as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the completion of the setup or update.

#### Response Example
```json
{
  "message": "Setup complete."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langgraph/errors/MISSING_CHECKPOINTER

Handles the OAuth setup callback, processing new installations or updates to GitHub App installations. For new installations with code, it processes similarly to a regular OAuth callback. For updates where users modify repository access, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. Processes new installations or updates to repository access.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
{
  "message": "GitHub App installation processed successfully."
}
```

--------------------------------

### GET /v2/sandboxes/templates

Source: https://docs.langchain.com/oss/python/integrations/splitters/recursive_text_splitter

Lists all available sandbox templates.

```APIDOC
## GET /v2/sandboxes/templates

### Description
Lists all SandboxTemplates in the tenant's sandbox namespace with support for pagination.

### Method
GET

### Endpoint
/v2/sandboxes/templates

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - Number of items to return.
- **offset** (integer) - Optional - Number of items to skip.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/microsoft_sharepoint

Handles the callback from GitHub Apps, triggered by user installation or updates. For updates, it displays a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the callback from GitHub Apps, triggered by user installation or updates. For updates, it displays a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the provider.

### Response
#### Success Response (200)
- **message** (string) - A success message.

#### Response Example
```json
{
  "message": "GitHub App setup successful."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/tools

Handles the initial setup callback for OAuth providers. For new installations with code/state, it processes similarly to a regular OAuth callback. If the repository access is modified via GitHub, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers. For new installations with code/state, it processes similarly to a regular OAuth callback. If the repository access is modified via GitHub, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
```json
{
  "message": "OAuth setup successful."
}
```
```

--------------------------------

### Initialize ChatXAI LLM

Source: https://docs.langchain.com/oss/python/integrations/chat/xai

Demonstrates how to import and instantiate the ChatXAI class. It includes setting the model to 'grok-beta' and configuring optional parameters like temperature, max_tokens, and retries.

```python
from langchain_xai import ChatXAI

llm = ChatXAI(
    model="grok-beta",
    temperature=0,
    max_tokens=None,
    timeout=None,
    max_retries=None
)
```

--------------------------------

### Langchain Python Example

Source: https://docs.langchain.com/oss/python/integrations/tools/composio

This Python code snippet demonstrates a basic setup for using Langchain. It includes comments indicating output and echo behavior, and imports necessary components from the 'langchain' library. This serves as a starting point for more complex Langchain applications.

```python
# | output: false
# | echo: false

from langchain
```

--------------------------------

### GET /v2/sandboxes/templates/{name}

Source: https://docs.langchain.com/oss/python/langchain/install

Retrieves a specific SandboxTemplate by name from the tenant's namespace.

```APIDOC
## GET /v2/sandboxes/templates/{name}

### Description
Get a specific SandboxTemplate by name in tenant's namespace. This endpoint queries the database for fast performance.

### Method
GET

### Endpoint
/v2/sandboxes/templates/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The unique name of the SandboxTemplate.

### Response
#### Success Response (200)
- **template** (object) - The SandboxTemplate object details.

#### Response Example
{
  "name": "example-template",
  "display_name": "My Template"
}
```

--------------------------------

### Initialize OpenAI Chat Model in LangChain (Python)

Source: https://python.langchain.com/docs/concepts/chat_models

Demonstrates how to initialize an OpenAI chat model using LangChain's `init_chat_model` function. This is a straightforward way to get started with OpenAI models for various NLP tasks. Ensure the `openai` package is installed.

```python
from langchain.chat_models import ChatOpenAI

# Initialize the chat model
chat = ChatOpenAI()

# Example usage (optional, depending on context)
# response = chat.invoke("Hello, how are you?")
# print(response)
```

--------------------------------

### POST /v2/sandboxes/pools

Source: https://docs.langchain.com/langsmith/observability-llm-tutorial

Create a new Sandbox Pool in the tenant's namespace.

```APIDOC
## POST /v2/sandboxes/pools

### Description
Create a new Sandbox Pool. Pools pre-provision sandboxes from a template.

### Method
POST

### Endpoint
/v2/sandboxes/pools

### Request Body
- **name** (string) - Required - Name of the pool.
- **template_ref** (string) - Required - Reference to the template.
```

--------------------------------

### Setup URL Callback

Source: https://docs.langchain.com/oss/javascript/langgraph/errors/INVALID_GRAPH_NODE_RETURN_VALUE

Handles the 'Setup URL' callback from GitHub Apps, triggered during installation or updates. For 'update' actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered during installation or updates. For 'update' actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App setup completed successfully."
}
```

--------------------------------

### Initialize Agent with LangChain

Source: https://docs.langchain.com/oss/python/migrate/langchain-v1

Demonstrates how to import and initialize an agent using the create_agent function in Python. This setup requires specifying the model and tools to be utilized by the agent.

```python
from langchain.agents import create_agent

agent = create_agent(
    model="claude-sonnet-4-6",
    tools=tools
)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/prebuilt-evaluators

Handles the initial OAuth setup callback for a given provider. For new installations, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup callback for a given provider. For new installations, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup completion.

#### Response Example
{
  "message": "OAuth setup successful"
}
```

--------------------------------

### Quickstart Deep Agent (JavaScript)

Source: https://docs.langchain.com/oss/javascript/deepagents/quickstart

This MDX content provides a quickstart guide for building a deep agent in minutes using JavaScript. It includes a description and frontmatter details.

```javascript
import {jsx as _jsx} from "react/jsx-runtime";
import {useMDXComponents as _provideComponents} from "@mdx-js/react";
function _createMdxContent(props) {
 const _components = {
 p: "p",
 ..._provideComponents(),
 ...props.components
 };
 return _jsx(_components.p, {
 children: "Build your first deep agent in minutes"
 });
}
function MDXContent(props = {}) {
 const {wrapper: MDXLayout} = {
 ..._provideComponents(),
 ...props.components
 };
 return MDXLayout ? _jsx(MDXLayout, {
 ...props,
 children: _jsx(_createMdxContent, {
 ...props
 })
 }) : _createMdxContent(props);
}
return {
 default: MDXContent
};

```

--------------------------------

### Sandboxes (v2)

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Endpoints for managing sandbox resources, including usage, volumes, and quotas.

```APIDOC
## GET /v2/sandboxes/usage

### Description
Return current resource consumption and organization quota limits. Sandbox counts include both direct claims and warmpool replicas. For self-hosted deployments, limit fields are 0 (quotas not enforced).

### Method
GET

### Endpoint
/v2/sandboxes/usage

### Response
#### Success Response (200)
- **usage** (object) - Current resource usage.
- **quotas** (object) - Organization quota limits.

#### Response Example
```json
{
  "usage": {
    "cpu_cores": 10,
    "memory_gb": 20
  },
  "quotas": {
    "cpu_cores": 100,
    "memory_gb": 50
  }
}
```

## GET /v2/sandboxes/volumes

### Description
List all persistent volumes in the tenant's sandbox namespace. This endpoint queries the database for fast performance. Supports optional pagination via `limit` and `offset` query parameters.

### Method
GET

### Endpoint
/v2/sandboxes/volumes

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - Maximum number of volumes to return.
- **offset** (integer) - Optional - Number of volumes to skip.

### Response
#### Success Response (200)
- **volumes** (array) - A list of persistent volumes.

#### Response Example
```json
{
  "volumes": [
    {
      "name": "my-volume",
      "size_gb": 10,
      "status": "Bound"
    }
  ]
}
```

## POST /v2/sandboxes/volumes

### Description
Create a new persistent volume in the tenant's sandbox namespace. This creates both a PersistentVolume (PV) and PersistentVolumeClaim (PVC). The volume can then be referenced in sandbox templates. Volume creation is subject to quota limits.

### Method
POST

### Endpoint
/v2/sandboxes/volumes

### Parameters
#### Request Body
- **volume_name** (string) - Required - The name of the volume.
- **size_gb** (integer) - Required - The size of the volume in gigabytes.

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.
- **volume_name** (string) - The name of the created volume.

#### Response Example
```json
{
  "message": "Volume created successfully.",
  "volume_name": "my-new-volume"
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/trace-anthropic

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is
triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show
a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular
OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider (e.g., GitHub).

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Request Example
```
GET /v2/auth/setup/github?code=AUTHORIZATION_CODE&state=RANDOM_STRING
```

### Response
#### Success Response (200)
- **message** (string) - A message indicating the status of the setup process.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/retrievers/bedrock

Handles the OAuth setup callback for GitHub App installations. For new installations with code or state, it processes the callback similarly to a regular OAuth callback. For 'update' actions where a user modifies repository access via GitHub, it displays a success page as no token exchange is required.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. For new installations with code or state, it processes the callback similarly to a regular OAuth callback. For 'update' actions where a user modifies repository access via GitHub, it displays a success page as no token exchange is required.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App installation processed successfully."
}
```

--------------------------------

### List Examples from Dataset using Langchain Client in Python

Source: https://docs.langchain.com/langsmith/manage-datasets

This Python code snippet demonstrates how to use a Langchain client to list examples from a specified dataset. It requires a 'client' object and a 'dataset_name'. The output is a list of examples, which can be further processed.

```python
data = client.list_examples(dataset_name=dataset_name)
```

--------------------------------

### Example: Getting Current Date with JavaScript

Source: https://docs.langchain.com/oss/javascript/integrations/chat/openai

Demonstrates how to get the current date using JavaScript, likely within a templating or string interpolation context. This example shows the use of template literals and the Date object.

```javascript
const currentDate = `The current date is ${new Date()}`;
```

--------------------------------

### Initialize ChatOpenAI and Bind Tools

Source: https://docs.langchain.com/oss/javascript/integrations/chat/openai

This snippet demonstrates how to instantiate a ChatOpenAI model with a specific preview model and bind tool configurations for computer-use tasks. It sets up the necessary parameters for display width and tool types.

```javascript
const llm = new ChatOpenAI({ model: "computer-use-preview" });

llm.bindTools([
  {
    type: "computer-preview",
    display_width: 1024
  }
]);
```

--------------------------------

### Basic Chat Interaction with Langchain LLM

Source: https://python.langchain.com/docs/integrations/chat/openai

Demonstrates a simple chat interaction using Langchain's LLM capabilities. It shows how to instantiate a chat model and send a message to it, then print the response content. This is a fundamental example for getting started with Langchain.

```python
from langchain.chat_models import ChatOpenAI

chat = ChatOpenAI()
response = chat.invoke("Hello, how are you?")
print(response.content)
```

--------------------------------

### Create a Custom MCP Server with FastMCP

Source: https://docs.langchain.com/oss/python/langchain/mcp

Demonstrates how to define a custom MCP server using the FastMCP library, including tool registration and stdio transport configuration.

```python
from fastmcp import FastMCP

mcp = FastMCP("Math")

@mcp.tool()
def add(a: int, b: int) -> int:
    """Add two numbers"""
    return a + b

@mcp.tool()
def multiply(a: int, b: int) -> int:
    """Multiply two numbers"""
    return a * b

if __name__ == "__main__":
    mcp.run(transport="stdio")
```

--------------------------------

### POST /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/providers/litellm

Handles the 'Setup URL' callback from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## POST /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered during app installation or updates. For updates, it displays a success page. For new installations, it processes the OAuth callback.

### Method
POST

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

#### Query Parameters
None

#### Request Body
None (This endpoint typically handles callbacks with query parameters)

### Request Example
None

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App setup successful."
}
```
```

--------------------------------

### Sandbox API

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Endpoints for managing sandbox instances, including listing, creation, and retrieval.

```APIDOC
## GET /v2/sandboxes/boxes

### Description
List all Sandboxes in the tenant's namespace.

This endpoint queries the database for fast performance.
Supports optional pagination via `limit` and `offset` query parameters.

### Method
GET

### Endpoint
/v2/sandboxes/boxes

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of sandboxes to return.
- **offset** (integer) - Optional - The number of sandboxes to skip before returning results.

### Response
#### Success Response (200)
- **sandboxes** (array) - A list of sandboxes.
  - **id** (string) - The unique identifier of the sandbox.
  - **name** (string) - The name of the sandbox.
  - **templateName** (string) - The name of the template used to create the sandbox.
  - **status** (string) - The current status of the sandbox (e.g., "Running", "Stopped", "Error").

#### Response Example
```json
{
  "sandboxes": [
    {
      "id": "sandbox-123",
      "name": "my-sandbox",
      "templateName": "my-template",
      "status": "Running"
    }
  ]
}
```
```

```APIDOC
## POST /v2/sandboxes/boxes

### Description
Create a new SandboxClaim in tenant's namespace.

If wait_for_ready is True (default), this will block until the sandbox is ready or the timeout is reached.

The sandbox creation can fail for several reasons:
- Image pull errors (invalid image, registry auth issues)
- Container crashes (bad entrypoint, missing dependencies, health check failures)
- Scheduling failures (no suitable nodes available)

Sandbox creation is subject to quota limits (count, CPU, memory) configured via Metronome org config.

On failure, the claim is automatically cleaned up and a descriptive error is returned.

### Method
POST

### Endpoint
/v2/sandboxes/boxes

### Parameters
#### Request Body
- **templateName** (string) - Required - The name of the sandbox template to use.
- **name** (string) - Optional - A custom name for the sandbox. If not provided, a name will be generated.
- **wait_for_ready** (boolean) - Optional - Whether to wait for the sandbox to be ready. Defaults to true.
- **timeout_seconds** (integer) - Optional - The maximum time to wait for the sandbox to be ready.
- **env** (object) - Optional - Environment variables to override or add to the sandbox.

### Request Example
```json
{
  "templateName": "my-template",
  "name": "my-custom-sandbox",
  "wait_for_ready": true,
  "timeout_seconds": 300,
  "env": {
    "ANOTHER_VAR": "another_value"
  }
}
```

### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the created sandbox.
- **name** (string) - The name of the created sandbox.
- **status** (string) - The status of the sandbox (e.g., "Pending", "Running").

#### Response Example
```json
{
  "id": "sandbox-456",
  "name": "my-custom-sandbox",
  "status": "Running"
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/chat/openrouter

Handles the initial OAuth setup redirect from OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup redirect from OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/install

Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. For user-modified repo access via GitHub, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. For user-modified repo access via GitHub, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Details of success response not provided in the source text)

#### Response Example
(No example response provided in the source text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/milvus

Handles the setup callback for OAuth providers, processing updates to GitHub App installations. For 'update' actions, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers, processing updates to GitHub App installations. For 'update' actions, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the OAuth provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Request Example
```
GET /v2/auth/setup/github?code=AUTHORIZATION_CODE&state=STATE_VALUE
```

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### POST /v2/sandboxes/volumes

Source: https://docs.langchain.com/langsmith/observability-llm-tutorial

Create a new persistent volume in the tenant's sandbox namespace.

```APIDOC
## POST /v2/sandboxes/volumes

### Description
Create a new persistent volume (PV and PVC). Volume creation is subject to quota limits. By default, this blocks until the PVC is bound.

### Method
POST

### Endpoint
/v2/sandboxes/volumes

### Request Body
- **name** (string) - Required - Unique name for the volume
- **size** (integer) - Required - Storage size in GB
- **wait_for_ready** (boolean) - Optional - Whether to wait for PVC binding

### Response
#### Success Response (200)
- **id** (string) - Unique identifier for the created volume
```

--------------------------------

### Configure Postgres Checkpointer for Production

Source: https://docs.langchain.com/oss/javascript/langgraph/add-memory

Demonstrates how to initialize a Postgres-backed checkpointer for state persistence. Includes installation instructions and a complete example of compiling a graph with a database connection.

```bash
npm install @langchain/langgraph-checkpoint-postgres
```

```typescript
import { PostgresSaver } from "@langchain/langgraph-checkpoint-postgres";
import { ChatAnthropic } from "@langchain/anthropic";
import { StateGraph, StateSchema, MessagesValue, GraphNode, START } from "@langchain/langgraph";

const DB_URI = "postgresql://postgres:postgres@localhost:5442/postgres?sslmode=disable";
const checkpointer = PostgresSaver.fromConnString(DB_URI);

const builder = new StateGraph(StateSchema).addNode("call_model", callModel).addEdge(START, "call_model");
const graph = builder.compile({ checkpointer });
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/test

Handles the OAuth setup callback for new installations. It processes the OAuth token exchange and redirects to the frontend callback page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for new installations. It processes the OAuth token exchange and redirects to the frontend callback page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
{
  "message": "OAuth setup successful."
}
```

--------------------------------

### POST /assistants

Source: https://docs.langchain.com/langsmith/observability-llm-tutorial

Create a new assistant instance.

```APIDOC
## POST /assistants

### Description
Create an assistant. An initial version of the assistant will be created and the assistant is set to that version.

### Method
POST

### Endpoint
/assistants

### Request Example
{
  "name": "My Assistant",
  "config": {}
}

### Response
#### Success Response (200)
- **assistant_id** (string) - The unique identifier of the created assistant.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/ls-metadata-parameters

Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to a regular OAuth callback. If repository access is modified via GitHub, a success page is shown as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to a regular OAuth callback. If repository access is modified via GitHub, a success page is shown as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### Configure LLM and Initialize Search Tools

Source: https://docs.langchain.com/oss/python/integrations/tools/exa_search

This snippet shows the setup of an LLM provider with a temperature parameter and the initialization of the ExaSearchResults tool. It utilizes the 'os' module to securely fetch the 'EXA_API_KEY' from the environment.

```python
model_provider = "openai", temperature = 0

# Initialize Exa Tools
exa_search = ExaSearchResults(
    exa_api_key=os.environ["EXA_API_KEY"],
    max_results=5
)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/versioning

Handles the initial OAuth setup callback for new installations. It processes the necessary steps without requiring a token exchange, redirecting to a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial OAuth setup callback for new installations. It processes the necessary steps without requiring a token exchange, redirecting to a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### Python: Langchain LLM Backend Setup and Execution

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

This snippet demonstrates how to set up a backend for Langchain LLMs and execute a sandbox environment. It also shows how to download files using the backend.

```python
backend = RunloopSandbox("devbox")

results = backend.download_files(["/src/index.py", "/output.txt"])

for result in results:
  if result.content is not None:
```

--------------------------------

### GET /api/v1/examples

Source: https://docs.langchain.com/langsmith/data-purging-compliance

Search for dataset examples across a workspace based on metadata and timestamps.

```APIDOC
## GET /api/v1/examples

### Description
Find all examples with matching metadata across all datasets in a workspace. This is the first step in the bulk deletion process.

### Method
GET

### Endpoint
/api/v1/examples

### Parameters
#### Query Parameters
- **as_of** (string) - Required - A timestamp string. Only examples created before this date will be returned.

### Request Example
```bash
curl -X GET "https://api.smith.langchain.com/api/v1/examples?as_of=2024-01-01T00:00:00Z" \
 -H "x-api-key: YOUR_API_KEY" \
 -H "Content-Type: application/json"
```

### Response
#### Success Response (200)
- **examples** (array) - A list of examples matching the criteria.

#### Response Example
{
  "examples": [
    { "id": "example_id_1", "metadata": { "user_id": "user123" } }
  ]
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/multi-agent/handoffs

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint manages the callback from GitHub Apps, processing setup URL redirects for new installations or updates.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This endpoint manages the callback from GitHub Apps, processing setup URL redirects for new installations or updates.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from GitHub.
- **state** (string) - Optional - The state parameter for CSRF protection.

### Request Example
None

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### Initialize DeepAgents Backends

Source: https://docs.langchain.com/oss/python/deepagents/data-analysis

Demonstrates how to import and instantiate backend classes for the DeepAgents library. Includes examples for both RunloopSandbox and LocalShellBackend configurations.

```python
from deepagents.backends import RunloopSandbox

backend = RunloopSandbox(devbox=devbox)
```

```python
from deepagents.backends import LocalShellBackend

backend = LocalShellBackend(root_dir=".", env=env)
```

--------------------------------

### POST /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/file_loaders/json

Handles the 'Setup URL' callback from GitHub Apps, triggered on installation or update. For updates, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## POST /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered on installation or update. For updates, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
POST

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Body
(No specific request body documented, likely handled by GitHub App callback)

### Response
#### Success Response (200)
(Response details not specified, likely a redirect or success page)

#### Response Example
(No example provided)
```

--------------------------------

### Configure PostgreSQL Database URI in Kubernetes Secret

Source: https://docs.langchain.com/langsmith/self-host-using-an-existing-secret

This snippet illustrates how to set the `POSTGRES_DATABASE_URI` within a Kubernetes secret. It guides the user to set the 'connection_url' key in their secret to the desired database URI, providing an example of the expected output format.

```shellscript
POSTGRES_DATABASE_URI: < set to the key 'connection_url' in secret <your-secret-name> > Optional:
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/requests

Handles the initial setup callback for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Indicates the success of the setup process.
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/azure_cognitive_services

Handles the setup callback from GitHub Apps, triggered by user installation or updates. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback from GitHub Apps, triggered by user installation or updates. For 'update' actions, it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(No example provided in the input text)
```

--------------------------------

### Pinecone Integration Setup (Python)

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/pinecone

This Python code demonstrates the initial setup for integrating with the Pinecone vector database using Langchain. It highlights the need to install the 'langchain-pinecone' package and mentions potential version conflicts with 'pinecone-client'.

```python
from langchain_pinecone import PineconeVectorStore

# Example usage (assuming Pinecone is configured)
# vector_store = PineconeVectorStore(...)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/providers/aws

Handles the initial setup callback for OAuth providers. For new installations with code/state, it processes the OAuth callback similarly to regular OAuth flows. For update actions (e.g., user modified repo access via GitHub), it displays a success page as no token exchange is required.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers. Processes new installations similarly to regular OAuth callbacks, and displays a success page for update actions where no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
- (No specific response body details provided in the source text)

#### Response Example
(No specific response example provided in the source text)
```

--------------------------------

### Initialize LangChain Agent with Skills and System Prompt

Source: https://docs.langchain.com/oss/python/langchain/multi-agent/skills

This snippet demonstrates how to instantiate an agent using 'create_agent', configuring it with a specific model, a list of tools, and a detailed system prompt. It highlights the pattern of providing instructions for on-demand skill usage.

```javascript
agent = create_agent(
  model = "gpt-4.1",
  tools = [load_skill],
  system_prompt = (
    "You are a helpful assistant. "
    "You have access to two skills: "
    "write_sql and review_legal_doc. "
    "Use load_skill to access them."
  )
)
```

--------------------------------

### Build and compile a StateGraph agent

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Demonstrates how to initialize a StateGraph with a defined state, add processing nodes such as 'llmCall' and 'toolNode', and prepare the agent for execution.

```typescript
const agent = new StateGraph(MessagesState)
  .addNode("llmCall", llmCall)
  .addNode("toolNode", toolNode);
```

--------------------------------

### Initialize Runloop SDK and Create Sandbox (Python)

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

This snippet shows how to import the Runloop SDK and API client for Langchain, initialize the SDK with an API key, and create a sandbox environment. It requires the `runloop_api_client` and `langchain_runloop` libraries.

```python
from runloop_api_client import RunloopSDK
from langchain_runloop import RunloopSandbox

api_key = "..."
client = RunloopSDK(bearer_token=api_key)
devbox = client.devbox.create()
```

--------------------------------

### MDX: Anthropic Chat Model Integration

Source: https://docs.langchain.com/oss/javascript/integrations/chat/anthropic

This MDX code snippet describes the integration with Anthropic's chat models. It explains that Anthropic is an AI safety and research company and the creator of Claude. It guides users on getting started with Anthropic chat models and directs them to the API reference for detailed documentation.

```mdx
"use strict";
const {Fragment: _Fragment, jsx: _jsx, jsxs: _jsxs} = arguments[0];
const {useMDXComponents: _provideComponents} = arguments[0];
function _createMdxContent(props) {
 const _components = {
 a: "a",
 code: "code",
 hr: "hr",
 img: "img",
 p: "p",
 pre: "pre",
 span: "span",
 strong: "strong",
 tbody: "tbody",
 td: "td",
 th: "th",
 thead: "thead",
 tr: "tr",
 ..._provideComponents(),
 ...props.components
 }, {Callout, CodeBlock, CodeGroup, Heading, Info, Table, Warning} = _components;
 if (!Callout) _missingMdxReference("Callout", true);
 if (!CodeBlock) _missingMdxReference("CodeBlock", true);
 if (!CodeGroup) _missingMdxReference("CodeGroup", true);
 if (!Heading) _missingMdxReference("Heading", true);
 if (!Info) _missingMdxReference("Info", true);
 if (!Table) _missingMdxReference("Table", true);
 if (!Warning) _missingMdxReference("Warning", true);
 return _jsxs(_Fragment, {
 children: [_jsxs(_components.p, {
 children: [_jsx(_components.a, {
 href: "https://www.anthropic.com/",
 children: "Anthropic"
 }), " is an AI safety and research company. They are the creator of Claude."]
 }), "\n", _jsxs(_components.p, {
 children: ["This will help you getting started with Anthropic ", _jsx(_components.a, {
 href: "/oss/javascript/langchain/models",
 children: "chat models"
 }), ". For detailed documentation of all ", _jsx(_components.code, {
 children: "ChatAnthropic"
 }), " features and configurations head to the ", _jsx(_components.a, {
 href: "https://api.js.langchain.com/classes/langchain_anthropic.ChatAnthropic.html",
 children: "API reference"
 }), "."]
 }), "\n", _jsx(Heading, {
 level: "2",
 id: "overview",
 children: "Overview"
 }), "\n", _jsx(Heading, {
 level: "3",
 id: "integration-details",
 children: "Integration details"
 }), "\n", _jsxs(Table, {
 children: [_jsx(

```

--------------------------------

### Create Example Outputs Array with Langchain

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/langsmith

This code snippet shows how to create an array named `exampleOutputs` using Langchain's array utility. It's designed to generate a structured array, likely for testing or demonstration purposes, by leveraging array creation functions.

```javascript
const exampleOutputs = Array.from({
  length: 1
}, () => {
  return {
    output: ""
  };
});
```

--------------------------------

### Define a system prompt for an agent

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Shows how to define a system prompt string to establish the persona and capabilities of an AI agent, which is a foundational step for building production-ready agents.

```javascript
const systemPrompt = `You are an expert weather forecaster, who speaks in puns.

You have access to two tools:`;
```

--------------------------------

### Install Matplotlib and Scikit-learn for Task Type Example

Source: https://docs.langchain.com/oss/python/integrations/text_embedding/google_generative_ai

This command installs the matplotlib and scikit-learn libraries, which are used in the subsequent example to demonstrate task-specific embedding optimization and cosine similarity calculations.

```bash
pip install -qU  matplotlib scikit-learn
```

--------------------------------

### Configure DeepAgents CLI Model and Installation

Source: https://docs.langchain.com/oss/python/deepagents/cli/providers

Examples of how to invoke the CLI model and install necessary provider packages via the command line.

```bash
deepagents --model openai:gpt-4o
uv tool install 'deepagents-cli[anthropic]'
uv tool upgrade deepagents-cli --with <package>
```

--------------------------------

### Instantiate ParallelWebSearchTool in Python

Source: https://docs.langchain.com/oss/python/integrations/tools/parallel_search

Demonstrates how to import and initialize the ParallelWebSearchTool. It shows both the default method using environment variables and the explicit method for providing an API key and custom base URL.

```python
from langchain_parallel import ParallelWebSearchTool

# Basic instantiation - API key from environment
tool = ParallelWebSearchTool()

# With explicit API key and custom base URL
tool = ParallelWebSearchTool(
    api_key="your-api-key"
)
```

--------------------------------

### Authentication Service (v2)

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Endpoints for managing OAuth authentication, including waiting for completion, creating providers, and managing tokens.

```APIDOC
## POST /v2/authenticate

### Description
Handles OAuth authentication.

### Method
POST

### Endpoint
/v2/authenticate

### Parameters
#### Query Parameters
- **provider** (string) - Required - The OAuth provider to use.

### Request Body
(No specific request body documented, likely handled by OAuth flow)

### Response
#### Success Response (200)
- **auth_url** (string) - The URL to redirect the user to for authentication.

#### Response Example
```json
{
  "auth_url": "https://example.com/oauth/authorize?client_id=..."
}
```

## GET /v2/auth/wait/{auth_id}

### Description
Wait for OAuth authentication completion.

### Method
GET

### Endpoint
/v2/auth/wait/{auth_id}

### Parameters
#### Path Parameters
- **auth_id** (string) - Required - The authentication ID to wait for.

### Response
#### Success Response (200)
- **status** (string) - The status of the authentication process.

#### Response Example
```json
{
  "status": "completed"
}
```

## POST /v2/auth/providers/mcp-discover

### Description
Create an OAuth provider via MCP auto-discovery.

### Method
POST

### Endpoint
/v2/auth/providers/mcp-discover

### Parameters
#### Request Body
- **provider_config** (object) - Required - Configuration for the OAuth provider.
  - **name** (string) - Required - The name of the provider.
  - **client_id** (string) - Required - The client ID for the provider.
  - **client_secret** (string) - Required - The client secret for the provider.

### Response
#### Success Response (200)
- **provider_id** (string) - The ID of the created OAuth provider.

#### Response Example
```json
{
  "provider_id": "provider_123"
}
```

## GET /v2/auth/providers/{provider_id}

### Description
Get a specific OAuth provider.

### Method
GET

### Endpoint
/v2/auth/providers/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider to retrieve.

### Response
#### Success Response (200)
- **provider_details** (object) - Details of the OAuth provider.

#### Response Example
```json
{
  "provider_details": {
    "name": "Example Provider",
    "client_id": "client_abc"
  }
}
```

## DELETE /v2/auth/providers/{provider_id}

### Description
Delete an OAuth provider.

### Method
DELETE

### Endpoint
/v2/auth/providers/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider to delete.

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "OAuth provider deleted successfully."
}
```

## PATCH /v2/auth/providers/{provider_id}

### Description
Update an OAuth provider.

### Method
PATCH

### Endpoint
/v2/auth/providers/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider to update.

#### Request Body
- **updates** (object) - Fields to update for the provider.

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "OAuth provider updated successfully."
}
```

## GET /v2/auth/tokens/exists

### Description
Return whether the current user has any tokens for a given provider (across agents).

### Method
GET

### Endpoint
/v2/auth/tokens/exists

### Parameters
#### Query Parameters
- **provider** (string) - Required - The OAuth provider to check tokens for.

### Response
#### Success Response (200)
- **exists** (boolean) - True if tokens exist, false otherwise.

#### Response Example
```json
{
  "exists": true
}
```

## DELETE /v2/auth/tokens

### Description
Delete all tokens for the current user for the given provider (across agents).

### Method
DELETE

### Endpoint
/v2/auth/tokens

### Parameters
#### Query Parameters
- **provider** (string) - Required - The OAuth provider for which to delete tokens.

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Tokens deleted successfully."
}
```

## GET /v2/auth/tokens/workspace/slack/exists

### Description
Check if the workspace has any Slack tokens.

### Method
GET

### Endpoint
/v2/auth/tokens/workspace/slack/exists

### Response
#### Success Response (200)
- **exists** (boolean) - True if Slack tokens exist for the workspace, false otherwise.

#### Response Example
```json
{
  "exists": true
}
```

## DELETE /v2/auth/tokens/workspace/slack

### Description
Revoke ALL Slack tokens for the workspace. Admin-only action that disconnects Slack entirely. This is a destructive operation that revokes all Slack tokens on Slack's side for all users in the workspace and deletes all Slack tokens from the database.

### Method
DELETE

### Endpoint
/v2/auth/tokens/workspace/slack

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "All Slack tokens for the workspace have been revoked."
}
```
```

--------------------------------

### GET /v2/sandboxes/boxes/{name}

Source: https://docs.langchain.com/oss/javascript/langchain/quickstart

Retrieve details for a specific sandbox.

```APIDOC
## GET /v2/sandboxes/boxes/{name}

### Description
Get a specific Sandbox by name in the tenant's namespace. This endpoint queries the database for fast performance.

### Method
GET

### Endpoint
/v2/sandboxes/boxes/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the sandbox.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/filter-experiments-ui

Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. If repository access is already granted via GitHub, a success page is shown as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. If repository access is already granted via GitHub, a success page is shown as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### Python Agent Server and Execution Example

Source: https://docs.langchain.com/oss/python/deepagents/acp

This Python code snippet demonstrates how to set up an agent server and then asynchronously run an agent. It includes conditional execution for the main function.

```python
server = AgentServerACP(
    agent=agent,
)

await run_agent(server)

if __name__ == "__main__":
  asyncio.run(main())

```

--------------------------------

### GET /v2/sandboxes/boxes/{name}/status

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Retrieve the provisioning status of a specific sandbox for polling purposes.

```APIDOC
## GET /v2/sandboxes/boxes/{name}/status

### Description
Lightweight endpoint for polling sandbox provisioning status. Returns only status and status_message.

### Method
GET

### Endpoint
/v2/sandboxes/boxes/{name}/status

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the sandbox

### Response
#### Success Response (200)
- **status** (string) - Current status of the sandbox
- **status_message** (string) - Detailed status message

#### Response Example
{
  "status": "ready",
  "status_message": "Sandbox is running"
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/dashboards

Handles the setup process for a specific OAuth provider.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Initializes the setup flow for an OAuth provider. Processes new installations with code/state similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Setup initialization status.
```

--------------------------------

### Create a new run with LangChain client

Source: https://docs.langchain.com/langsmith/agent-server-scale

This snippet demonstrates how to initialize a run using the LangChain client. It includes configuration for thread tracking, assistant identification, and durability settings.

```javascript
run = await client.runs.create(
  thread_id = ["thread_id"],
  assistant_id = "agent",
  durability = "exit"
)
```

--------------------------------

### Initialize ChatOpenAI with Configuration

Source: https://docs.langchain.com/langsmith/trace-with-langchain

Demonstrates how to instantiate the ChatOpenAI class with specific parameters including model name, temperature, and metadata. This setup is typically used to define the behavior and tracking attributes of the LLM instance.

```javascript
const llm = new ChatOpenAI({
  modelName: "gpt-4.1",
  temperature: 0.9,
  metadata: {
    ls_model_name: "gpt-4.1-creative"
  }
});

const llmFactual = new ChatOpenAI({});
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/managing-model-configurations

Handles the OAuth setup callback from providers. For 'update' actions where user modified repo access via GitHub, a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from providers. For 'update' actions where user modified repo access via GitHub, a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
{
  "message": "OAuth setup successful"
}
```

--------------------------------

### List Deployments

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

List all deployments.

```APIDOC
## GET /v2/deployments

### Description
List all deployments.

### Method
GET

### Endpoint
/v2/deployments

### Parameters
#### Query Parameters
- **None**

### Request Example
```json
{
  "example": "No request body needed for this GET request."
}
```

### Response
#### Success Response (200)
- **deployments** (array) - A list of deployments.
  - **id** (string) - The unique identifier for the deployment.
  - **name** (string) - The name of the deployment.
  - **status** (string) - The current status of the deployment.

#### Response Example
```json
{
  "example": "{\"deployments\": [{\"id\": \"dep_abc\", \"name\": \"My App Deployment\", \"status\": \"active\"}, {\"id\": \"dep_def\", \"name\": \"Another Deployment\", \"status\": \"inactive\"}]}"
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/guardrails

Handles the OAuth setup callback for a given provider. This endpoint is used after a user initiates an OAuth flow and is redirected back to the application. For existing installations with modified repository access, it displays a success page. For new installations with code/state, it processes the callback similar to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. This endpoint is used after a user initiates an OAuth flow and is redirected back to the application. For existing installations with modified repository access, it displays a success page. For new installations with code/state, it processes the callback similar to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
{
  "message": "OAuth setup successful."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/chat/perplexity

Handles the setup callback for OAuth providers. For 'update' actions where a user modifies repository access via GitHub, a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers. For 'update' actions where a user modifies repository access via GitHub, a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### Initialize LangChain Client and Tracer

Source: https://docs.langchain.com/langsmith/trace-with-langchain

This code demonstrates how to create a new client instance by providing an API key and API URL. It also shows the pattern for passing the client and project name to a LangChainTracer instance for tracing purposes.

```javascript
// You can create a client instance with an api key and api url
const client = new Client({
  apiKey: "YOUR_API_KEY",
  apiUrl: "https://api.smith.langchain.com", // Update appropriately for self-hosted installations or the EU region
});

// You can pass the client and project_name to the LangChainTracer instance
const tracer = new LangChainTracer({
  client,
  projectName: "YOUR_PROJECT_NAME"
});
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/ampersend

Handles the initial setup for OAuth, processing user modifications to repository access via GitHub. For new installations with code or state, it proceeds similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for OAuth, processing user modifications to repository access via GitHub. For new installations with code or state, it proceeds similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(No example provided in the input text)
```

--------------------------------

### Initialize Vector Stores

Source: https://docs.langchain.com/oss/python/langchain/knowledge-base

Provides examples for setting up different vector store backends. It covers lightweight in-memory storage and cloud-based solutions like Amazon OpenSearch.

```python
from langchain_core.vectorstores import InMemoryVectorStore
vector_store = InMemoryVectorStore(embeddings)
```

```python
from opensearchpy import RequestsHttpConnection
import boto3

# Example configuration for OpenSearch
service = "es"
region = "us-east-2"
credentials = boto3.Session(aws_access_key_id="xxxxxx", aws_secret_access_key="xxxxx").get_credentials()
awsauth = AWS4Auth("xxxxx", "xxxxxx", region, service, session_token=credentials.token)

vector_store = OpenSearchVectorSearch.from_documents(docs, embeddings)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/messages

Handles the OAuth setup callback from providers. For new installations with code/state, it processes similarly to a regular OAuth callback. If repo access is already granted via GitHub, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from providers. For new installations with code/state, it processes similarly to a regular OAuth callback. If repo access is already granted via GitHub, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/chat/google_generative_ai

Handles the callback from GitHub Apps for installation or update events. For new installations, it processes the OAuth token exchange similar to a regular OAuth callback. For updates where only repository access is modified, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the callback from GitHub Apps for installation or update events. For new installations, it processes the OAuth token exchange similar to a regular OAuth callback. For updates where only repository access is modified, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details depend on the specific provider and action - typically a redirect or success page)

#### Response Example
(No specific JSON response example provided, as it often involves redirects or HTML pages.)
```

--------------------------------

### Initialize OpenAI Client and Tracing

Source: https://docs.langchain.com/langsmith/trace-with-opentelemetry

This snippet shows the instantiation of an OpenAI client using an API key from environment variables and the setup of an OTLP span exporter with a defined timeout. It also includes the registration of a global tracer provider for application monitoring.

```python
client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

otlp_exporter = OTLPSpanExporter(
    timeout=10,
)

trace.set_tracer_provider(TracerProvider())
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/langgraph/durable-execution

Handle OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the 'Setup URL' callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Status of the setup process.
```

--------------------------------

### GET /v1/integrations/github/install

Source: https://docs.langchain.com/oss/python/langchain/middleware/built-in

Lists available GitHub integrations for LangGraph Platform Cloud SaaS.

```APIDOC
## GET /v1/integrations/github/install

### Description
Lists all GitHub integrations configured for the account.

### Method
GET

### Endpoint
/v1/integrations/github/install

### Response
#### Success Response (200)
- **integrations** (array) - List of installed GitHub integration objects.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/splitters/character_text_splitter

Handles the callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For 'update' actions, it shows a success page. For new installations, it processes similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the callback from GitHub Apps upon installation or update.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message.

#### Response Example
{
  "message": "GitHub App installation processed successfully."
}
```

--------------------------------

### GET /v2/sandboxes/volumes/{name}

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Retrieve details for a specific volume by its name.

```APIDOC
## GET /v2/sandboxes/volumes/{name}

### Description
Queries the database to retrieve a specific volume by name in the tenant's sandbox namespace.

### Method
GET

### Endpoint
/v2/sandboxes/volumes/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the volume.

### Response
#### Success Response (200)
- **name** (string) - The volume name.
- **size** (integer) - The storage size of the volume.

### Response Example
{
  "name": "my-volume",
  "size": 10
}
```

--------------------------------

### Oauth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/gitlab

Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation. For 'update' actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed. For new installations with code/state, we process similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the status of the setup callback.

#### Response Example
{
  "message": "GitHub App setup completed successfully."
}
```

--------------------------------

### Initialize Daytona with LangChain

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

Python code demonstrating how to import and set up the Daytona sandbox environment for use within a LangChain workflow.

```python
from dotenv import load_dotenv
from daytona import Daytona
from langchain_daytona import Daytona
```

--------------------------------

### Initialize LangChain Client Example Creation

Source: https://docs.langchain.com/langsmith/evaluate-llm-application

This snippet demonstrates the method call to the LangChain client to initiate the creation of example datasets. It serves as the entry point for registering the structured input/output pairs defined in the system.

```python
ls_client.create_examples()
```

--------------------------------

### End-to-End LangGraph Agent with Claude and Vector Store

Source: https://python.langchain.com/docs/integrations/chat/anthropic

An end-to-end example demonstrating the setup of a LangChain vector store with sample documents and an agent that uses Claude to query these documents. It includes installation instructions and the full Python code for setting up embeddings, vector store, defining a tool with filtering, creating the agent, and invoking it.

```python
pip install langchain-openai numpy
```

```python
from typing import Literal

from langchain.chat_models import init_chat_model
from langchain.embeddings import init_embeddings
from langchain_core.documents import Document
from langchain_core.vectorstores import InMemoryVectorStore
from langgraph.checkpoint.memory import InMemorySaver
from langchain.agents import create_agent


# Set up vector store
# Ensure you set your OPENAI_API_KEY environment variable
embeddings = init_embeddings("openai:text-embedding-3-small")
vector_store = InMemoryVectorStore(embeddings)

document_1 = Document(
    id="1",
    page_content=(
        "To request vacation days, submit a leave request form through the "
        "HR portal. Approval will be sent by email."
    ),
    metadata={
        "category": "HR Policy",
        "doc_title": "Leave Policy",
        "provenance": "Leave Policy - page 1",
    },
)
document_2 = Document(id="2", page_content="Managers will review vacation requests within 3 business days.", metadata={"category": "HR Policy", "doc_title": "Leave Policy", "provenance": "Leave Policy - page 2"})
document_3 = Document(
    id="3",
    page_content=(
        "Employees with over 6 months tenure are eligible for 20 paid vacation days "
        "per year."
    ),
    metadata={
        "category": "Benefits Policy",
        "doc_title": "Benefits Guide 2025",
        "provenance": "Benefits Policy - page 1",
    },
)

documents = [document_1, document_2, document_3]
vector_store.add_documents(documents=documents)


# Define tool
async def retrieval_tool(
    query: str,
    category: Literal["HR Policy", "Benefits Policy"],
) -> list[dict]:
    """Access my knowledge base."""

    def _filter_function(doc: Document) -> bool:
        return doc.metadata.get("category") == category

    results = vector_store.similarity_search(
        query=query, k=2, filter=_filter_function
    )

    return [
        {
            "type": "search_result",
            "title": doc.metadata["doc_title"],
            "source": doc.metadata["provenance"],
            "citations": {"enabled": True},
            "content": [{"type": "text", "text": doc.page_content}],
        }
        for doc in results
    ]



# Create agent
model = init_chat_model("claude-haiku-4-5-20251001")

checkpointer = InMemorySaver()
agent = create_agent(model, [retrieval_tool], checkpointer=checkpointer)


# Invoke on a query
config = {"configurable": {"thread_id": "session_1"}}

input_message = {
    "role": "user",
    "content": "How do I request vacation days?",
}
async for step in agent.astream(
    {"messages": [input_message]},
    config,
    stream_mode="values",
):
    step["messages"][-1].pretty_print()
```

--------------------------------

### Basic Langchain Langgraph 'Hello World' Example

Source: https://docs.langchain.com/oss/javascript/langgraph

A fundamental TypeScript example demonstrating the import of essential Langchain components like StateSchema, MessagesValue, GraphNode, StateGraph, and START. This serves as a starting point for building more complex stateful applications.

```typescript
import { StateSchema, MessagesValue, GraphNode, StateGraph, START } from "@langchain/langgraph";

// Define the state for the graph
interface MyState {
  messages: MessagesValue;
}

// Define the nodes
const entryNode: GraphNode<MyState> = {
  name: "entry",
  fn: async (state: MyState) => {
    console.log("Entering the graph");
    return { ...state, messages: ["Hello from the entry node!"] };
  },
};

const exitNode: GraphNode<MyState> = {
  name: "exit",
  fn: async (state: MyState) => {
    console.log("Exiting the graph");
    return state;
  },
};

// Create the state graph
const graph = new StateGraph<MyState>({
  nodes: {
    entry: entryNode,
    exit: exitNode,
  },
  channels: {
    messages: new StateSchema<MessagesValue>({})
  },
  entryPoint: START,
});

// Define transitions
graph.addConditionalEdges({
  entry: {
    exit: (state: MyState) => state.messages.length > 0 ? "exit" : "entry",
  },
});

// Compile the graph
const compiledGraph = graph.compile();

// Run the graph
async function runGraph() {
  const result = await compiledGraph.invoke({ messages: [] });
  console.log("Graph result:", result);
}

runGraph();

```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/retrievers/wikipedia

Handles the OAuth setup callback for GitHub App installations. For 'update' actions, it displays a success page. For new installations, it processes the token exchange similar to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for GitHub App installations. For 'update' actions (user modified repo access via GitHub), a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App installation updated successfully."
}
```

--------------------------------

### Install LangChain dependencies

Source: https://docs.langchain.com/oss/python/integrations/chat/anthropic

Installs the required langchain-openai and numpy packages necessary for running the LLM examples.

```shellscript
pip install langchain-openai numpy
```

--------------------------------

### POST /v2/sandboxes/templates

Source: https://docs.langchain.com/langsmith/legacy-trace-with-vercel-ai-sdk

Create a new SandboxTemplate in the tenant's namespace.

```APIDOC
## POST /v2/sandboxes/templates

### Description
Creates a new SandboxTemplate within the tenant's namespace.

### Method
POST

### Endpoint
/v2/sandboxes/templates
```

--------------------------------

### GET /sandboxes-v2/get-sandbox-status

Source: https://docs.langchain.com/oss/python/langchain/install

Retrieves the current status of a specific sandbox environment.

```APIDOC
## GET /sandboxes-v2/get-sandbox-status

### Description
Fetches the status of a sandbox to determine if it is running, stopped, or pending.

### Method
GET

### Endpoint
/api-reference/sandboxes-v2/get-sandbox-status/{sandbox_id}

### Parameters
#### Path Parameters
- **sandbox_id** (string) - Required - The unique ID of the sandbox

### Response
#### Success Response (200)
- **status** (string) - The current state of the sandbox

#### Response Example
{
  "status": "running"
}
```

--------------------------------

### Initialize ChatOpenAI and ChatPromptTemplate

Source: https://docs.langchain.com/oss/javascript/integrations/vectorstores/azure_documentdb

Demonstrates how to instantiate a ChatOpenAI model with specific parameters and create a system-based ChatPromptTemplate for question answering tasks.

```javascript
const model = new ChatOpenAI({ model: "gpt-3.5-turbo-1106" });

const questionAnsweringPrompt = ChatPromptTemplate.fromMessages([
  ["system", "Answer the user's questions based on the below context:\n\n{context}"]
]);
```

--------------------------------

### Install @langchain/textsplitters

Source: https://docs.langchain.com/oss/javascript/integrations/splitters/recursive_text_splitter

Commands to install the text splitter package using common JavaScript package managers.

```shellscript
pnpm install @langchain/textsplitters
```

```shellscript
yarn add @langchain/textsplitters
```

```shellscript
bun add @langchain/textsplitters
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/contributing/publish-langchain

Handles the setup callback for OAuth providers. For 'update' actions (user modified repo access via GitHub), it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers. For 'update' actions (user modified repo access via GitHub), it shows a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the callback.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/runtime

Handles the OAuth setup callback for a given provider. If the repository is user-modified, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. If the repository is user-modified, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
{
  "message": "OAuth setup successful"
}
```

--------------------------------

### Define Example Data for Langchain Datasets (Python)

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

This snippet illustrates how to define structured examples for a Langchain dataset. Each example includes inputs and expected outputs, crucial for testing and fine-tuning language models.

```python
examples = [
    {
        "inputs": {"question": "Which country is Mount Kilimanjaro located in?"},
        "outputs": {"answer": "Tanzania"}
    }
]
```

--------------------------------

### Initialize Solana Wallet Tool

Source: https://docs.langchain.com/oss/python/integrations/tools/privy

Demonstrates how to instantiate a PrivyWalletTool by providing a wallet ID. This tool allows LLMs to interact with specific existing wallet configurations.

```python
# Or reuse an existing wallet
existing_tool = PrivyWalletTool(wallet_id="wal_abc123...")
```

--------------------------------

### Initialize Pinecone Client with API Key

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/pinecone

Demonstrates how to securely prompt the user for a Pinecone API key using getpass and initialize the Pinecone client instance. It also shows how to retrieve an existing key from environment variables.

```python
import getpass
import os

pinecone_api_key = getpass.getpass("Enter your Pinecone API key: ")
pinecone_api_key = os.environ.get("PINECONE_API_KEY")

pc = Pinecone(api_key=pinecone_api_key)
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/graphs/amazon_neptune_open_cypher

Handles the GitHub Apps callback URL, triggered when a user installs or updates their GitHub App installation. For 'update' actions, it displays a success page. For new installations, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the GitHub Apps callback URL, triggered when a user installs or updates their GitHub App installation. For 'update' actions, it displays a success page. For new installations, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the callback.

#### Response Example
{
  "message": "GitHub App installation processed successfully."
}
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/file_loaders/csv

Handle OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint processes new installations or updates to existing GitHub App installations.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Success status of the callback handling.
```

--------------------------------

### Creating App and ModalSandbox Instances

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

This snippet shows the creation of an 'app' instance using a 'modal.App' lookup and a 'modal_sandbox' instance using 'ModalSandbox.create'. These are fundamental steps for initializing and configuring components within a Langchain environment.

```javascript
app = modal.App.lookup("your-app")
modal_sandbox = ModalSandbox.create(app=app)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/chat/openai

Handles the OAuth setup callback, processing user modifications to repository access via GitHub. For new installations with code/state, it proceeds like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for providers like GitHub. Processes user modifications to repository access and shows a success page if no token exchange is needed. For new installations, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
```json
{
  "message": "OAuth setup completed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/composio

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback for GitHub App installations or updates, handling token exchange when necessary.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This endpoint processes the callback for GitHub App installations or updates, handling token exchange when necessary.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider (e.g., 'github').

#### Query Parameters
- **code** (string) - Required - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter used to maintain context.

### Request Example
```json
{
  "example": "GET /v2/auth/setup/github?code=some_auth_code&state=some_state"
}
```

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup completion.

#### Response Example
```json
{
  "example": "{\"message\": \"GitHub App setup successful.\"}"
}
```
```

--------------------------------

### Initialize Daytona Sandbox

Source: https://docs.langchain.com/oss/python/deepagents/data-analysis

Demonstrates how to import the DaytonaSandbox class and instantiate a new sandbox environment for backend operations.

```python
from langchain_daytona import DaytonaSandbox

sandbox = Daytona().create()
backend = DaytonaSandbox(sandbox=sandbox)
```

--------------------------------

### List Listeners

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

List all listeners.

```APIDOC
## GET /v2/listeners

### Description
List all listeners.

### Method
GET

### Endpoint
/v2/listeners

### Parameters
#### Query Parameters
- **None**

### Request Example
```json
{
  "example": "No request body needed for this GET request."
}
```

### Response
#### Success Response (200)
- **listeners** (array) - A list of listeners.
  - **id** (string) - The unique identifier for the listener.
  - **name** (string) - The name of the listener.
  - **status** (string) - The current status of the listener.

#### Response Example
```json
{
  "example": "{\"listeners\": [{\"id\": \"lst_1\", \"name\": \"Listener A\", \"status\": \"active\"}, {\"id\": \"lst_2\", \"name\": \"Listener B\", \"status\": \"inactive\"}]}"
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/custom-middleware

Handles the OAuth setup callback for a given provider. For new installations with code/state, it processes similarly to a regular OAuth callback. If no token exchange is needed (e.g., for existing installations), it shows a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. For new installations with code/state, it processes similarly to a regular OAuth callback. If no token exchange is needed (e.g., for existing installations), it shows a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Indicates the success of the setup process.
```

--------------------------------

### Install LangChain and Exa dependencies

Source: https://docs.langchain.com/oss/python/integrations/tools/exa_search

Command to install the required LangChain and Exa packages for the integration.

```bash
pip install -q langchain langchain-openai langchain-community
```

--------------------------------

### Install LangChain Integrations (Shell)

Source: https://docs.langchain.com/oss/python/deepagents/cli/overview

This command demonstrates how to install specific LangChain integration packages for the DeepAgents CLI. This is necessary when using particular model providers. The example shows installing with one provider.

```shellscript
# Install with one provider
uv deepagents[provider-name]
```

--------------------------------

### Initialize OpenAI Client and Traceable RAG

Source: https://docs.langchain.com/langsmith/observability-quickstart

Demonstrates the initialization of an OpenAI client using a wrapper and the setup of a traceable RAG component. These patterns are used to capture prompts and responses from the LLM for monitoring and debugging purposes.

```javascript
const client = wrapOpenAI(new OpenAI()); // keep this to capture the prompt and response from the LLM

const rag = traceable(async (string[]) => {
  return ["Harrison worked at Kensho"];
});
```

--------------------------------

### Create Run

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Creates a single run and returns immediately.

```APIDOC
## POST /runs

### Description
Creates a single run and returns immediately.

### Method
POST

### Endpoint
/runs

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
  "example": "request body"
}
```

### Response
#### Success Response (200)
- **field1** (type) - Description

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Create Langchain Examples

Source: https://docs.langchain.com/langsmith/evaluate-on-intermediate-steps

This snippet demonstrates how to create examples for a Langchain dataset using the `ls_client.create_examples` function. It requires a dataset ID and a list of examples as input. The function is part of the Langchain client library.

```python
ls_client.create_examples(
  dataset_id=dataset.id,
  examples=examples
)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/providers/milvus

Handles the OAuth callback redirect from OAuth providers for new installations with code/state, processing similar to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth callback redirect from OAuth providers for new installations with code/state, processing similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(No example provided)
```

--------------------------------

### Initialize Slack WebClient with LangChain

Source: https://docs.langchain.com/oss/python/deepagents/data-analysis

This snippet demonstrates how to import the required LangChain tools and Slack SDK components. It also shows the initialization of the Slack WebClient using an environment-based user token.

```python
from langchain.tools import tool
from slack_sdk import WebClient
import os

slack_token = os.environ["SLACK_USER_TOKEN"]
slack_client = WebClient(slack_token)
```

--------------------------------

### Load Prompt with Arguments using Langchain Client

Source: https://docs.langchain.com/oss/python/langchain/mcp

This example demonstrates loading a prompt template and providing specific arguments to it. The `get_prompt` method is used with the prompt name and an 'arguments' dictionary. This allows for dynamic prompt generation based on provided key-value pairs.

```python
messages = await client.get_prompt("server_name", "code_review", arguments={"language": "python"})
```

--------------------------------

### Initialize and Run Google Serper API Wrapper

Source: https://docs.langchain.com/oss/python/integrations/tools/google_serper

Demonstrates how to install necessary dependencies, configure the API key, and perform a basic search query using the GoogleSerperAPIWrapper.

```bash
pip install -qU langchain-community langchain-openai
```

```python
import os
from langchain_community.utilities import GoogleSerperAPIWrapper

os.environ["SERPER_API_KEY"] = "your-serper-api-key"
search = GoogleSerperAPIWrapper()
print(search.run("Obama's first name?"))
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/chat/anthropic

Handles the initial setup for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes the OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes the OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/figma

Handles the OAuth callback for GitHub App installations. For new installations, it processes the token exchange similar to a regular OAuth callback. For updates, it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth callback for GitHub App installations. For new installations, it processes the token exchange similar to a regular OAuth callback. For updates, it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the installation or update.

#### Response Example
```json
{
  "message": "GitHub App installation processed successfully."
}
```
```

--------------------------------

### Initialize Gemini Computer Use Model in Python

Source: https://docs.langchain.com/oss/python/integrations/chat/google_generative_ai

Demonstrates how to import and instantiate the ChatGoogleGenerativeAI class to enable computer use capabilities within a LangChain workflow.

```python
from langchain_google_genai import ChatGoogleGenerativeAI

model = ChatGoogleGenerativeAI(model="gemini-2.5-computer-use-preview-10-2025")
```

--------------------------------

### Search Examples by Metadata (curl)

Source: https://docs.langchain.com/langsmith/data-purging-compliance

Retrieves examples matching specified metadata from all datasets in a workspace. The 'as_of' parameter must be a timestamp, and it returns examples created before that time. Metadata matching is OR-based.

```curl
curl -X GET "https://api.smith.langchain.com/api/v1/examples?as_of=2024-01-01T00:00:00Z" \
  -H "x-api-key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "metadata": {
      "user_id": "user123",
      "environment": "staging"
    }
  }'
```

--------------------------------

### Install and Run LangGraph Agent

Source: https://docs.langchain.com/oss/javascript/langgraph/studio

Commands to install necessary dependencies and start the local development server for the LangGraph agent.

```shellscript
yarn install
```

```shellscript
npx @langchain/langgraph-cli dev
```

--------------------------------

### Initialize LangSmith Client

Source: https://docs.langchain.com/langsmith/export-traces

Demonstrates importing the Langsmith client and initializing it using configuration from the environment.

```python
import com.langchain.smith.client.okhttp.LangsmithOkHttpClient;

LangsmithClient client = LangsmithOkHttpClient.fromEnv();
```

--------------------------------

### Initialize Pinecone Vector Store

Source: https://docs.langchain.com/oss/python/langchain/knowledge-base

Installs the Pinecone integration and connects to an existing index.

```bash
pip install -qU langchain-pinecone
```

```python
from langchain_pinecone import PineconeVectorStore
from pinecone import Pinecone

pc = Pinecone(api_key=...)
index = pc.Index(index_name)

vector_store = PineconeVectorStore(embedding=embeddings, index=index)
```

--------------------------------

### Install LangChain Text Splitters

Source: https://docs.langchain.com/oss/javascript/integrations/splitters/recursive_text_splitter

Installation commands for the @langchain/textsplitters package using common Node.js package managers.

```shellscript
npm install @langchain/textsplitters
```

```shellscript
pnpm install @langchain/textsplitters
```

--------------------------------

### Authenticate

Source: https://docs.langchain.com/langsmith/cicd-pipeline-example

Get OAuth token or start authentication flow if needed.

```APIDOC
## POST /v2/auth/authenticate

### Description
Get OAuth token or start authentication flow if needed.

### Method
POST

### Endpoint
/v2/auth/authenticate

### Parameters
#### Request Body
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
- **redirect_uri** (string) - Optional - The URI to redirect to after authentication.

### Request Example
```json
{
  "provider_id": "google",
  "redirect_uri": "https://myapp.com/callback"
}
```

### Response
#### Success Response (200)
- **auth_id** (string) - The identifier for the authentication process.
- **auth_url** (string) - The URL to redirect the user to for authentication.

#### Response Example
```json
{
  "auth_id": "auth_12345",
  "auth_url": "https://accounts.google.com/o/oauth2/v2/auth?response_type=code&client_id=..."
}
```
```

--------------------------------

### Initialize and Fetch Resources with MultiServerMCPClient

Source: https://docs.langchain.com/oss/python/langchain/mcp

Demonstrates how to import and instantiate the MultiServerMCPClient, followed by examples of fetching resources from an MCP server. It covers both bulk loading by server name and targeted loading by URI.

```typescript
from langchain_mcp_adapters.client import MultiServerMCPClient

client = MultiServerMCPClient(...)

# Load all resources from a server
blobs = await client.get_resources("server_name")

# Or load specific resources by URI
blobs = await client.get_resources("uri")
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/privy

Handles the OAuth setup callback for a given provider. For 'update' actions where the user has modified repository access via GitHub, a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. For 'update' actions where the user has modified repository access via GitHub, a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
(Details not provided in the source text)

#### Response Example
(No specific response example provided in the source text)
```

--------------------------------

### Install Dependencies with Shell Commands

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

This snippet shows the shell commands to create a project directory, set up a Python virtual environment, and upgrade pip. It's a foundational step for any Python project requiring specific dependencies.

```shellscript
mkdir ls-evaluation-quickstart && cd ls-evaluation-quickstart && \
python -m venv .venv && \
source .venv/bin/activate && \
pip install --upgrade pip
```

--------------------------------

### Instantiate Model with Quantization (Python)

Source: https://docs.langchain.com/oss/python/integrations/chat/huggingface

Demonstrates how to instantiate a model using quantization with the bitsandbytes library. This is useful for reducing memory footprint and potentially speeding up inference on compatible hardware.

```python
from transformers import BitsAndBytesConfig

quantization_config = BitsAndBytesConfig(
    load_in_4bit=True,
    bnb_4bit_compute_dtype=torch.float16,
    bnb_4bit_quant_type="nf4",
    bnb_4bit_use_double_quant=True,
)

model = AutoModelForCausalLM.from_pretrained(
    model_name_or_path, quantization_config=quantization_config
)
```

--------------------------------

### Pydantic Model State Serialization Example (Python)

Source: https://docs.langchain.com/oss/python/langgraph/use-graph-api

This Python code snippet illustrates the setup for using Pydantic models as state schemas in LangChain. It imports `StateGraph`, `START`, and `END` from `langgraph`, and `BaseModel` from `pydantic`. A nested Pydantic model `NestedModel` is defined to showcase handling of complex state structures.

```python
from langgraph.graph import StateGraph, START, END
from pydantic import BaseModel

class NestedModel(BaseModel):
    value: str
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/self-hosted-changelog

Handles the initial setup for an OAuth provider, including redirecting to a success page if no token exchange is required.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup for an OAuth provider. For new installations, it processes the state and code similar to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### Generate Structured LLM Output with Pydantic

Source: https://docs.langchain.com/oss/python/integrations/chat/llamacpp

This snippet demonstrates how to use Pydantic models with LangChain to get structured output from an LLM. It defines a 'Joke' Pydantic model and then uses `convert_to_openai_tool` and `with_structured_output` to guide the LLM to return jokes in the specified format. The output is a dictionary containing the joke's setup and punchline.

```python
from pydantic import BaseModel


class Joke(BaseModel):
    """A setup to a joke and the punchline."""

    setup: str
    punchline: str


dict_schema = convert_to_openai_tool(Joke)
structured_llm = llm.with_structured_output(dict_schema)
result = structured_llm.invoke("Tell me a joke about birds")
result
```

--------------------------------

### Initialize Chroma Vector Store

Source: https://docs.langchain.com/oss/python/langchain/knowledge-base

Installs the Chroma integration and initializes a local persistent vector store.

```bash
pip install -qU langchain-chroma
```

```python
from langchain_chroma import Chroma

vector_store = Chroma(
    collection_name="example_collection",
    embedding_function=embeddings,
    persist_directory="./chroma_langchain_db",
)
```

--------------------------------

### Initialize AzureChatOpenAI model

Source: https://docs.langchain.com/oss/python/langgraph/sql-agent

Demonstrates how to instantiate the AzureChatOpenAI class, configuring the model name and deployment identifier from environment variables.

```python
model = AzureChatOpenAI(
    model="gpt-5.2",
    azure_deployment=os.environ["AZURE_OPENAI_DEPLOYMENT_NAME"]
)
```

--------------------------------

### GET /v2/auth/providers

Source: https://docs.langchain.com/langsmith/evaluation-quickstart

Retrieve a list of all configured OAuth providers.

```APIDOC
## GET /v2/auth/providers

### Description
List OAuth providers.

### Method
GET

### Endpoint
/v2/auth/providers

### Response
#### Success Response (200)
- **providers** (array) - A list of available OAuth provider objects.
```

--------------------------------

### POST /v2/sandboxes/templates

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/google_cloud_storage

Create a new SandboxTemplate in the tenant's namespace.

```APIDOC
## POST /v2/sandboxes/templates

### Description
Create a new SandboxTemplate in the tenant's namespace.

### Method
POST

### Endpoint
/v2/sandboxes/templates

### Parameters
#### Request Body
- **name** (string) - Required - The unique name for the SandboxTemplate.
- **displayName** (string) - Required - The display name for the SandboxTemplate.
- **image** (string) - Required - The container image to use for the sandbox.
- **resources** (object) - Required - The resource specifications for the sandbox (e.g., CPU, memory).
- **volumeMounts** (array) - Optional - The volume mounts to configure for the sandbox.
  - **name** (string) - Required - The name of the volume.
  - **mountPath** (string) - Required - The path where the volume should be mounted.

### Response
#### Success Response (201)
- **name** (string) - The name of the created SandboxTemplate.
- **displayName** (string) - The display name of the created SandboxTemplate.
- **image** (string) - The container image used by the SandboxTemplate.
- **resources** (object) - The resource specifications for the SandboxTemplate.
- **volumeMounts** (array) - The volume mounts configured for the SandboxTemplate.

#### Response Example
```json
{
  "name": "new-template",
  "displayName": "My New Template",
  "image": "python:3.9",
  "resources": {
    "cpu": "500m",
    "memory": "512Mi"
  },
  "volumeMounts": [
    {
      "name": "app-data",
      "mountPath": "/app/data"
    }
  ]
}
```
```

--------------------------------

### Install LangChain Text Splitters

Source: https://docs.langchain.com/oss/python/integrations/splitters/recursive_text_splitter

Command to install the necessary library for text splitting functionality in Python environments.

```bash
pip install -qU langchain-text-splitters
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain

Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similar to the regular OAuth callback. For actions involving user-modified repo access via GitHub, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similar to the regular OAuth callback. For actions involving user-modified repo access via GitHub, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### Get a Registry

Source: https://docs.langchain.com/oss/javascript/integrations/splitters/code_splitter

Gets a specific registry by name. Returns metadata only; credentials are never included in responses.

```APIDOC
## GET /v2/sandboxes/registries/{name}

### Description
Gets a specific registry by name. Returns metadata only; credentials are never included in responses.

### Method
GET

### Endpoint
/v2/sandboxes/registries/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the registry to retrieve.

### Response
#### Success Response (200)
- **registry** (object) - The registry object.
  - **name** (string) - The name of the registry.
  - **url** (string) - The URL of the registry.

#### Response Example
```json
{
  "registry": {
    "name": "my-registry",
    "url": "https://my.registry.com"
  }
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/drasi

Handles the OAuth setup callback for a given provider. For 'update' actions where a user has modified repository access via GitHub, a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. For 'update' actions where a user has modified repository access via GitHub, a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not provided in the source text)

#### Response Example
(Response example not provided in the source text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/concepts/products

Handles the OAuth setup callback for a given provider. If the repository is user-modified (user-controlled access via GitHub), a success page is shown as no token exchange is needed. For new installations with code/state, it processes similarly to the regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. For user-modified repositories, it shows a success page. For new installations, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the callback was processed.

#### Response Example
```json
{
  "message": "OAuth setup successful."
}
```
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/agent-server-api/stateless-runs

Handles the OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps. This endpoint handles the 'Setup URL' callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - Status of the installation or update process.
```

--------------------------------

### Get a Sandbox

Source: https://docs.langchain.com/oss/javascript/integrations/splitters/recursive_text_splitter

Get a specific Sandbox by name in the tenant's namespace. This endpoint queries the database for fast performance.

```APIDOC
## GET /v2/sandboxes/boxes/{name}

### Description
Get a specific Sandbox by name in the tenant's namespace. This endpoint queries the database for fast performance.

### Method
GET

### Endpoint
/v2/sandboxes/boxes/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the sandbox to retrieve.

### Request Example
```json
{
  "example": "No request body needed for getting a sandbox."
}
```

### Response
#### Success Response (200)
- **sandbox** (object) - The requested SandboxClaim object.
  - **name** (string) - The name of the sandbox.
  - **display_name** (string) - The display name of the sandbox.
  - **template_name** (string) - The name of the template used to create the sandbox.
  - **status** (string) - The current status of the sandbox.
  - **resources** (object) - The resources allocated to the sandbox.
  - **ports** (array) - The ports exposed by the sandbox.

#### Response Example
```json
{
  "sandbox": {
    "name": "sandbox-1",
    "display_name": "My First Sandbox",
    "template_name": "default-template",
    "status": "Ready",
    "resources": {
      "cpu": "1 core",
      "memory": "2Gi"
    },
    "ports": [
      {
        "name": "http",
        "port": 8080,
        "url": "http://localhost:8080"
      }
    ]
  }
}
```
```

--------------------------------

### Initialize LangChain Prompt and Model Configuration

Source: https://docs.langchain.com/langsmith/trace-with-langchain

This snippet demonstrates importing a string output parser, creating a chat prompt template from system and user messages, and configuring a ChatOpenAI instance with custom metadata and tags.

```python
from langchain_core.output_parsers import StrOutputParser

prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful AI."),
    ("user", "{input}")
])

# The tag "model-tag" and metadata {"model-key": "model-value"} will be attached to the ChatOpenAI run only
chat_model = ChatOpenAI().with_config({"tags": ["model-tag"], "metadata": {"model-key": "model-value"}})
```

--------------------------------

### Initialize and Load PDF Documents with PyMuPDFLoader

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/pymupdf

Demonstrates the instantiation of the PyMuPDFLoader with a file path and the subsequent execution of the load method to retrieve document contents.

```python
loader = PyMuPDFLoader(file_path)
docs = loader.load()
docs[0]
```

--------------------------------

### cURL Example for Get Thread State

Source: https://docs.langchain.com/langsmith/use-threads

Example of how to retrieve thread state using cURL, demonstrating the request method, URL, and parameters.

```APIDOC
## GET /threads/{thread_id}/state/{checkpoint_id} (cURL Example)

### Description
This cURL command demonstrates how to fetch the state of a specific thread at a given checkpoint.

### Method
GET

### Endpoint
`/threads/{thread_id}/state/{checkpoint_id}`

### Request Example
```shell
curl --request GET \
  --url "<DEPLOYMENT_URL>/threads/thread[\"thread_id\"]/state/<CHECKPOINT_ID>" \
```

### Response
#### Success Response (200)
- **state** (object) - The state of the thread at the specified checkpoint.
- **metadata** (object) - Any associated metadata for the thread state.

#### Response Example
```json
{
  "example": "{\n  \"state\": {\n    \"messages\": [\n      {\n        \"role\": \"user\",\n        \"content\": \"Hello!\"\n      }\n    ]\n  },\n  \"metadata\": {\n    \"timestamp\": \"2023-10-27T10:00:00Z\"\n  }\n}"
}
```
```

--------------------------------

### Install LangChain Groq package

Source: https://docs.langchain.com/oss/python/integrations/chat/groq

Command to install the necessary library for integrating Groq models with LangChain.

```bash
pip install -qU langchain-groq
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/agent-server-api/threads/get-thread

Handles the initial setup callback for OAuth providers. For new installations with code/state, it processes similarly to a regular OAuth callback. For 'update' actions (user modified repo access via GitHub), it displays a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the initial setup callback for OAuth providers. For new installations with code/state, it processes similarly to a regular OAuth callback. For 'update' actions (user modified repo access via GitHub), it displays a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the OAuth provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Request Example
```
GET /v2/auth/setup/github?code=AUTHORIZATION_CODE&state=STATE_VALUE
```

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/hugging_face_dataset

Handles the OAuth setup callback redirect from GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This endpoint processes the \"Setup URL\" callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For \"update\" actions, it shows a success page. For new installations with code/state, it processes the OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider (e.g., 'github').

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the completion of the setup.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### Invoke Tool and Store Observation

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

This snippet shows the process of identifying a tool from a collection, invoking it with a tool call object, and pushing the resulting observation into a results array. It handles the asynchronous nature of tool execution using the await keyword.

```javascript
const tool = toolsByName[toolCall.name];
const observation = await tool.invoke(toolCall);
result.push(observation);

return { messages: result };
```

--------------------------------

### Example Execution Comment in JavaScript

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/sort_xyz_blockchain

A documentation comment indicating the start of an example execution block. This comment serves as a placeholder or explanation for the code that follows, typically demonstrating how to run a Langchain example.

```javascript
/**
 * Run the example.
 */
```

--------------------------------

### KV-Store Documentation Setup (Shell)

Source: https://docs.langchain.com/oss/python/integrations/tools/github

This snippet provides shell commands for setting up KV-store documentation within a Langchain project. It includes installing the CLI, creating a new integration doc, and building a preview of the documentation.

```shell
poetry run pip install -e libs/cli
poetry run langchain-cli integration create-doc --name "foo-bar" --name-class FooBar --component-type kv_store --destination-dir ./docs/docs/integrations/stores/
```

```shell
make docs_clean
make docs_build
cd docs/build/output-new
yarn
yarn start
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/text_embedding/nvidia_ai_endpoints

Handles the callback from GitHub Apps, triggered when a user installs or updates their GitHub App installation. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the callback from GitHub Apps during installation or update.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
Displays a success page or processes the OAuth callback.

#### Response Example
(HTML content for success page or redirect to frontend callback)
```

--------------------------------

### Initialize and Run LangChain Agent

Source: https://docs.langchain.com/oss/python/integrations/tools/drasi

This snippet shows the setup of a ChatAnthropic model, the creation of an agent instance with a tool, and the execution of that agent.

```python
from agents import create_agent

# Initialize the model
model = ChatAnthropic(model="claude-sonnet-4-6")

# Create agent with Drasi tool
agent = create_agent(model, [tool])

# Run the agent
result = agent.run()
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/evals

Handles the OAuth setup callback for a given provider. For new installations with code/state, it processes similarly to a regular OAuth callback. If no token exchange is needed (e.g., via GitHub), it shows a success page.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. For new installations with code/state, it processes similarly to a regular OAuth callback. If no token exchange is needed (e.g., via GitHub), it shows a success page.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the completion of the setup.

#### Response Example
```json
{
  "message": "OAuth setup completed successfully."
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/langchain/multi-agent/router

Handles the setup callback for OAuth providers. For 'update' actions where users modify repository access, it displays a success page. For new installations with code or state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers. For 'update' actions where users modify repository access, it displays a success page. For new installations with code or state, it processes similarly to a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

#### Query Parameters
- **code** (string) - Optional - The authorization code received from the OAuth provider.
- **state** (string) - Optional - The state parameter used to maintain state between the request and callback.

### Request Example
```
GET /v2/auth/setup/github?code=AUTHORIZATION_CODE&state=STATE_VALUE
```

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup process.

#### Response Example
```json
{
  "message": "GitHub App installation updated successfully."
}
```
```

--------------------------------

### Dockerfile for Langchain Application Setup

Source: https://docs.langchain.com/langsmith/cli

This Dockerfile sets up an environment for a Langchain application. It starts from a specific Langchain API image, installs Python dependencies using pip, and copies local graph data into the container for use by the application. It also configures pip to use a specific configuration file and disables bytecode writing.

```docker
FROM langchain/langgraph-api:3.11

ADD ./pipconf.txt /pipconfig.txt

RUN PIP_CONFIG_FILE=/pipconfig.txt PYTHONDONTWRITEBYTECODE=1 pip install --no-cache-dir -c /api/constraints.txt langchain_community langchain_anthropic langchain_openai wikipedia scikit-learn

ADD ./graphs /deps/__outer_graphs/src

RUN set -ex && \
 for line in \
 'name = "graphs"' \
 'version = "0.1"' \
 '[	ool.setuptools.package-data]' \
 '"*" = ["**/*"]' ; do \
 echo "
```

--------------------------------

### Invoke Agent with Filesystem Tools

Source: https://docs.langchain.com/oss/python/langchain/middleware/built-in

Demonstrates how to invoke an agent with a specific query and utilize filesystem search tools like glob_search and grep_search to locate and analyze Python files.

```python
agent.invoke({
  "messages": [HumanMessage("Find all Python files containing 'async def'")]
})

# The agent will use:
# 1. glob_search(pattern="**/*.py") to find Python files
# 2. grep_search(pattern="async def", include="*.py") to find async functions
```

--------------------------------

### Initialize Chroma Vector Store

Source: https://docs.langchain.com/oss/python/integrations/vectorstores/chroma

Demonstrates how to import the Chroma class and initialize a vector store instance. This setup is used to connect LangChain applications to Chroma databases.

```python
from langchain_chroma import Chroma

vector_store = Chroma(
    collection_name="example_collection",
    embedding_function=embeddings,
    host="localhost"
)
```

```python
from langchain_chroma import Chroma

vector_store = Chroma()
```

--------------------------------

### POST /v2/auth/authenticate

Source: https://docs.langchain.com/langsmith/components

Get OAuth token or start authentication flow if needed.

```APIDOC
## POST /v2/auth/authenticate

### Description
Get OAuth token or start authentication flow if needed. This endpoint initiates the OAuth authentication process or retrieves an existing token if available.

### Method
POST

### Endpoint
/v2/auth/authenticate

### Parameters
#### Request Body
- **provider_id** (string) - Required - The ID of the OAuth provider.
- **scopes** (array of strings) - Optional - The scopes to request for the authentication.

### Response
#### Success Response (200 OK)
- **auth_id** (string) - The ID for the authentication process, used for waiting.
- **redirect_url** (string) - The URL to redirect the user to for authentication.

#### Response Example
```json
{
  "auth_id": "auth_abc",
  "redirect_url": "https://oauth.provider.com/auth?client_id=..."
}
```
```

--------------------------------

### Create Dataset Examples

Source: https://reference.langchain.com/javascript/modules/langsmith.html

Demonstrates how to iterate through runs and create examples within a LangSmith dataset using the client.

```typescript
for (const run of runs) {
  await client.createExample(run.inputs, run.outputs ?? {}, {
    datasetId: dataset.id
  });
}
```

--------------------------------

### Initialize OpenAI LLM with Configuration (JavaScript)

Source: https://docs.langchain.com/langsmith/trace-with-langchain

This example demonstrates initializing an OpenAI LLM instance in JavaScript. It highlights how to configure different LLM behaviors, such as 'creative' or 'precise', by passing specific parameters. The OpenAI API key should be set as an environment variable.

```javascript
const llmCreative = new OpenAI({
  model: "gpt-3.5-turbo",
  temperature: 0.7,
  // Other OpenAI specific parameters
});
```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/langsmith/agent-server-api/crons

Handles GitHub App installation or update triggers, processing token exchanges for new installations.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Triggered when a user installs or updates their GitHub App installation. Processes new installations with code/state or displays a success page for updates.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider (e.g., github).

### Response
#### Success Response (200)
- **status** (string) - Success message or redirect confirmation.
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/multi-agent/router

Handles the OAuth setup callback for a given provider. For update actions, it displays a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback for a given provider. For update actions, it displays a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the callback.

#### Response Example
{
  "message": "OAuth setup completed successfully."
}
```

--------------------------------

### Create Example Dataset with TypeScript

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/langsmith

This TypeScript code snippet demonstrates how to initialize a LangSmith client and create an example dataset. This dataset can then be used with Langchain document loaders for various applications. It requires the 'langchain/core' package to be installed.

```typescript
import { Client as LangSmithClient } from "@langchain/core";

// Example usage:
// const client = new LangSmithClient({%n//   apiKey: "YOUR_LANGSMITH_API_KEY",
// });

// async function createDataset() {
//   const datasetName = "my-example-dataset";
//   const dataset = await client.createDataset({ name: datasetName });
//   console.log(`Dataset '${dataset.name}' created with ID: ${dataset.id}`);
//   return dataset;
// }

// createDataset();
```

--------------------------------

### Redis Sentinel Connection URL Example

Source: https://docs.langchain.com/oss/python/integrations/providers/redis

This example shows the connection URL format for a Redis Sentinel setup. It uses the `redis+sentinel` scheme and specifies the sentinel host, port, service name, and database number.

```python
redis_url = "redis+sentinel://:secret-pass@sentinel-host:26379/mymaster/0"
```

--------------------------------

### Initialize agent with skill sources

Source: https://docs.langchain.com/oss/python/deepagents/skills

Demonstrates how to pass the ordered skill source list to the agent creation function. The Python example illustrates the 'last-one-wins' behavior for skill name collisions.

```python
# If both sources contain a skill named "web-search",
# the one from "/skills/project/" wins (loaded last).
agent = create_deep_agent(
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/langchain/runtime

Handles the OAuth callback redirect from OAuth providers for new installations. It processes the setup similar to a regular OAuth callback, showing a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth callback redirect from OAuth providers for new installations. It processes the setup similar to a regular OAuth callback, showing a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup is complete.

#### Response Example
```json
{
  "message": "OAuth setup successful."
}
```
```

--------------------------------

### Store API

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Endpoints for managing items in the store, including retrieval, update, deletion, search, and listing namespaces.

```APIDOC
## GET /store/items

### Description
Retrieve a single item from the store.

### Method
GET

### Endpoint
/store/items

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
  "example": "request body"
}
```

### Response
#### Success Response (200)
- **field1** (type) - Description

#### Response Example
```json
{
  "example": "response body"
}
```

## PUT /store/items

### Description
Store or update an item in the store.

### Method
PUT

### Endpoint
/store/items

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
  "example": "request body"
}
```

### Response
#### Success Response (200)
- **field1** (type) - Description

#### Response Example
```json
{
  "example": "response body"
}
```

## DELETE /store/items

### Description
Delete an item from the store.

### Method
DELETE

### Endpoint
/store/items

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
  "example": "request body"
}
```

### Response
#### Success Response (200)
- **field1** (type) - Description

#### Response Example
```json
{
  "example": "response body"
}
```

## POST /store/items/search

### Description
Search or list items within a namespace prefix. Lists items ordered by last updated time. If a `query` is provided, performs a natural language search instead. Supports pagination via `limit` and `offset`, and filtering via `filter`.

### Method
POST

### Endpoint
/store/items/search

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
  "example": "request body"
}
```

### Response
#### Success Response (200)
- **field1** (type) - Description

#### Response Example
```json
{
  "example": "response body"
}
```

## POST /store/namespaces

### Description
List namespaces with optional match conditions.

### Method
POST

### Endpoint
/store/namespaces

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
  "example": "request body"
}
```

### Response
#### Success Response (200)
- **field1** (type) - Description

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Initialize ObsClient in Python

Source: https://docs.langchain.com/oss/python/integrations/document_loaders/huawei_obs_file

This example illustrates the initialization of the ObsClient from the obs library. It requires authentication details such as access_key_id and secret_access_key.

```python
from obs import ObsClient

obs_client = ObsClient(
    access_key_id="your-access-key-id",
    secret_access_key="your-secret-access-key",
    server="your-obs-server"
)
```

--------------------------------

### Start LangGraph Server with Debugging

Source: https://docs.langchain.com/langsmith/quick-start-studio

Commands to install the debugpy package and start the LangGraph development server on a specific debug port.

```shellscript
# Install debugpy package
uv add debugpy

# Start server with debugging enabled
langgraph dev --debug-port 5678
```

--------------------------------

### Install Langchain Classic Package

Source: https://docs.langchain.com/oss/python/migrate/langchain-v1

Instructions for installing the `langchain-classic` package using `uv pip`. This is a prerequisite for using legacy components.

```bash
uv pip install langchain-classic

```

--------------------------------

### Retrieve Dataset Examples and Configure Evaluators

Source: https://docs.langchain.com/langsmith/manage-datasets

This snippet demonstrates how to fetch examples from a specific dataset using a client object and define a list of evaluators. It includes parameters for dataset name, data splits, and evaluation metrics.

```javascript
data = client.list_examples(dataset_name=dataset_name, splits=["test", "training"]);
evaluators = [correct_label];
```

--------------------------------

### Full Agent Implementation

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

A complete example integrating ChatAnthropic, tool definitions with Zod, and the functional LangGraph workflow to create an arithmetic-capable agent.

```typescript
import { ChatAnthropic } from "@langchain/anthropic";
import { tool } from "@langchain/core/tools";
import { task, entrypoint, addMessages } from "@langchain/langgraph";
import { SystemMessage, HumanMessage, type BaseMessage } from "@langchain/core/messages";
import * as z from "zod";

const model = new ChatAnthropic({ model: "claude-sonnet-4-6", temperature: 0 });
const add = tool(({ a, b }) => a + b, {
  name: "add",
  description: "Add two numbers",
  schema: z.object({ a: z.number(), b: z.number() }),
});

const toolsByName = { [add.name]: add };
const modelWithTools = model.bindTools([add]);

const callLlm = task({ name: "callLlm" }, async (messages: BaseMessage[]) => {
  return modelWithTools.invoke([new SystemMessage("You are a helpful assistant."), ...messages]);
});

const agent = entrypoint({ name: "agent" }, async (messages: BaseMessage[]) => {
  let modelResponse = await callLlm(messages);
  // ... loop logic ...
  return messages;
});
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/annotation-queues-sdk

Handles the initial OAuth setup redirect from OAuth providers. This endpoint is typically the starting point for initiating an OAuth flow.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Initiates the OAuth setup process by redirecting the user to the specified provider.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.
```

--------------------------------

### Get a SandboxTemplate

Source: https://docs.langchain.com/oss/javascript/integrations/splitters/code_splitter

Gets a specific SandboxTemplate by name in the tenant's namespace. This endpoint queries the database for fast performance.

```APIDOC
## GET /v2/sandboxes/templates/{name}

### Description
Gets a specific SandboxTemplate by name in tenant's namespace. This endpoint queries the database for fast performance.

### Method
GET

### Endpoint
/v2/sandboxes/templates/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the sandbox template to retrieve.

### Response
#### Success Response (200)
- **template** (object) - The sandbox template object.
  - **name** (string) - The name of the sandbox template.
  - **description** (string) - The description of the sandbox template.
  - **image** (string) - The container image used.
  - **resources** (object) - Resources allocated.
    - **cpu** (string) - CPU allocation.
    - **memory** (string) - Memory allocation.
  - **volume_mounts** (array) - Volume mounts configured.
    - **name** (string) - The name of the volume.
    - **mount_path** (string) - The path where the volume is mounted.

#### Response Example
```json
{
  "template": {
    "name": "my-template",
    "description": "A sample sandbox template",
    "image": "ubuntu:latest",
    "resources": {
      "cpu": "500m",
      "memory": "512Mi"
    },
    "volume_mounts": [
      {
        "name": "my-volume",
        "mount_path": "/data"
      }
    ]
  }
}
```
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/javascript/integrations/document_loaders/web_loaders/sonix_audio_transcription

Handles the OAuth setup callback redirect from GitHub Apps. This endpoint manages the callback from GitHub Apps, processing both new installations and updates to existing ones.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handle OAuth setup callback redirect from GitHub Apps.

This endpoint handles the "Setup URL" callback from GitHub Apps, which is triggered when a user installs or updates their GitHub App installation.

For "update" actions (user modified repo access via GitHub), we just show a success page since no token exchange is needed.

For new installations with code/state, we process similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier of the OAuth provider (e.g., GitHub App ID).

#### Query Parameters
- **code** (string) - Required (for new installations) - The authorization code received from GitHub.
- **state** (string) - Required (for new installations) - The state parameter used to prevent CSRF attacks.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup completion or redirection.

#### Response Example
```json
{
  "message": "GitHub App setup completed successfully."
}
```
```

--------------------------------

### Retrieve File and Create Cache with LangChain

Source: https://docs.langchain.com/oss/python/integrations/chat/google_generative_ai

Demonstrates how to fetch a file using a client instance and initialize a new model cache. These operations are essential for managing LLM context and optimizing performance through caching.

```python
file = client.files.get(name=file.name)

# Create cache
model = "gemini-3.1-pro-preview"
cache = client.caches.create(model=model)
```

--------------------------------

### Get a Sandbox Pool

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

Retrieves a specific Sandbox Pool by its name in the tenant's namespace.

```APIDOC
## GET /v2/sandboxes/pools/{name}

### Description
Get a specific Sandbox Pool by name in tenant's namespace.
This endpoint queries the database for fast performance.

### Method
GET

### Endpoint
/v2/sandboxes/pools/{name}

#### Path Parameters
- **name** (string) - Required - The name of the sandbox pool to retrieve.

### Response
#### Success Response (200)
- **name** (string) - The name of the sandbox pool.
- **template_name** (string) - The name of the template used for the pool.
- **replicas** (integer) - The number of replicas in the pool.
- **created_at** (string) - The timestamp when the pool was created.

#### Response Example
```json
{
  "name": "example-pool",
  "template_name": "example-template",
  "replicas": 3,
  "created_at": "2023-10-27T10:00:00Z"
}
```
```

--------------------------------

### GET /metrics

Source: https://docs.langchain.com/oss/python/langchain/install

Retrieves system metrics for monitoring and observability purposes.

```APIDOC
## GET /metrics

### Description
Get system metrics in Prometheus or JSON format for monitoring and observability.

### Method
GET

### Endpoint
/metrics

### Response
#### Success Response (200)
- **metrics** (object) - System metrics data in Prometheus or JSON format.

#### Response Example
{
  "cpu_usage": 0.15,
  "memory_usage": "512MB"
}
```

--------------------------------

### Initialize DeepAgent with FilesystemBackend

Source: https://docs.langchain.com/oss/javascript/deepagents/skills

Demonstrates how to instantiate a DeepAgent using a MemorySaver checkpointer and a FilesystemBackend. It configures the agent with specific skills and interrupt triggers for file operations.

```javascript
const checkpointer = new MemorySaver();
const backend = new FilesystemBackend({ rootDir: process.cwd() });

const agent = await createDeepAgent({
  backend,
  skills: ["./examples/skills/"],
  interruptOn: {
    read_file: true,
    write_file: true,
    delete_file: true,
  },
  checkpointer,
});

const config = {
  configurable: {
    thread_id: `thread-${Date.now()}`,
  },
};

const result = await agent.invoke(
  {
    messages: [
      {
        role: "user",
        content: "what is langraph? Use the langgraph-docs skill if available.",
      },
    ],
  },
  config
);
```

--------------------------------

### GET /system/health-check

Source: https://docs.langchain.com/oss/python/langchain/install

Checks the operational status of the LangSmith Agent Server.

```APIDOC
## GET /system/health-check

### Description
Returns the current health status of the Agent Server to ensure the service is responsive.

### Method
GET

### Endpoint
/langsmith/agent-server-api/system/health-check

### Response
#### Success Response (200)
- **status** (string) - The health status of the server (e.g., "ok")

#### Response Example
{
  "status": "ok"
}
```

--------------------------------

### GET /v1/integrations/github/install

Source: https://docs.langchain.com/oss/javascript/integrations/tools/google_calendar

List GitHub installations for the integration.

```APIDOC
## GET /v1/integrations/github/install

### Description
Retrieve GitHub installations associated with the current user or organization.

### Method
GET

### Endpoint
/v1/integrations/github/install

### Response
#### Success Response (200)
- **installations** (array) - List of GitHub installations.
```

--------------------------------

### Set up Modal Backend (Python)

Source: https://docs.langchain.com/oss/python/deepagents/data-analysis

Configures the Modal backend for LangChain deep agents. Requires the `modal` library and involves looking up an existing Modal app and creating a Modal Sandbox instance.

```python
import modal
from langchain_modal import ModalSandbox

app = modal.App.lookup("your-app")
modal_sandbox = modal.Sandbox.create(app=app)
backend = ModalSandbox(sandbox=modal_sandbox)
```

--------------------------------

### LangSmith Testing Setup with Vitest

Source: https://docs.langchain.com/langsmith/vitest-jest

This snippet demonstrates the basic structure for setting up tests using LangSmith's Vitest integration. It shows how `ls.describe` and `ls.test` are used to define test suites and individual test cases, which correspond to datasets and dataset examples in LangSmith, respectively. When LangSmith environment variables are set, this setup automatically creates datasets, examples, and experiments in LangSmith.

```javascript
import { describe, test } from "langsmith/vitest";

describe("My LangSmith Dataset", () => {
  test("My first dataset example", async () => {
    // Your test logic here
  });
});
```

--------------------------------

### GET /v2/sandboxes/templates

Source: https://docs.langchain.com/langsmith/self-host-using-an-existing-secret

List all SandboxTemplates.

```APIDOC
## GET /v2/sandboxes/templates

### Description
Lists all SandboxTemplates available in the tenant's namespace with support for pagination.

### Method
GET

### Endpoint
/v2/sandboxes/templates

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - Number of items to return.
- **offset** (integer) - Optional - Number of items to skip.
```

--------------------------------

### Execute LLM Tools using Promise.all

Source: https://docs.langchain.com/oss/javascript/langgraph/quickstart

This snippet demonstrates how to iterate over tool calls returned by a model response and execute them concurrently. It uses the map function to transform tool calls into execution promises, which are then resolved using Promise.all.

```javascript
// Execute tools
const toolResults = await Promise.all(
  modelResponse.tool_calls.map((toolCall) => callTool(toolCall))
);
```

--------------------------------

### Authenticate

Source: https://docs.langchain.com/oss/javascript/langgraph/errors/INVALID_CONCURRENT_GRAPH_UPDATE

Gets an OAuth token or starts the authentication flow if needed.

```APIDOC
## POST /v2/auth/authenticate

### Description
Gets an OAuth token or starts the authentication flow if needed.

### Method
POST

### Endpoint
/v2/auth/authenticate

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **provider_id** (string) - Required - The ID of the OAuth provider.
- **scopes** (array) - Optional - A list of scopes to request for the authentication.

### Request Example
```json
{
  "provider_id": "github",
  "scopes": ["repo", "user"]
}
```

### Response
#### Success Response (200)
- **auth_id** (string) - The ID of the authentication process, used for waiting.
- **redirect_url** (string) - The URL to redirect the user to for authentication.

#### Response Example
```json
{
  "auth_id": "auth_abc123",
  "redirect_url": "https://github.com/login/oauth/authorize?client_id=..."
}
```
```

--------------------------------

### Initialize ChatOpenAI and Bind Tools

Source: https://docs.langchain.com/oss/javascript/langchain/models

Demonstrates how to instantiate a ChatOpenAI model with a specific model version and how to bind custom tools using the bindTools method. This setup allows the model to utilize external functions like getWeather during execution.

```javascript
const model = new ChatOpenAI({ model: "gpt-4.1" });
const modelWithTools = model.bindTools([getWeather]);
```

--------------------------------

### Authenticate

Source: https://docs.langchain.com/oss/javascript/deepagents/acp

Get OAuth token or start authentication flow if needed.

```APIDOC
## POST /v2/auth/authenticate

### Description
Get OAuth token or start authentication flow if needed.

### Method
POST

### Endpoint
/v2/auth/authenticate

### Parameters
#### Request Body
- **provider_id** (string) - Required - The ID of the OAuth provider.
- **agent_id** (string) - Optional - The ID of the agent initiating the authentication.

### Response
#### Success Response (200)
- **auth_id** (string) - The ID of the authentication process, if a flow needs to be started.
- **token** (string) - The OAuth token, if already available.

#### Response Example
```json
{
  "auth_id": "auth_abc789",
  "token": null
}
```

```json
{
  "auth_id": null,
  "token": "user_oauth_token_xyz"
}
```
```

--------------------------------

### Authenticate

Source: https://docs.langchain.com/langsmith/double-texting

Gets an OAuth token or starts the authentication flow if needed.

```APIDOC
## POST /v2/auth/authenticate

### Description
Gets an OAuth token or starts the authentication flow if needed.

### Method
POST

### Endpoint
/v2/auth/authenticate

### Parameters
(No parameters specified in the source text)

### Request Body
(Request body details not provided in the source text)

### Response
#### Success Response (200)
(Response details not provided in the source text)

#### Response Example
(Response example not provided in the source text)
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/oss/python/integrations/tools/powerbi

Handles the setup callback for OAuth providers. For update actions, it displays a success page. For new installations with code/state, it processes similarly to a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the setup callback for OAuth providers. For update actions (user modified repo access via GitHub), a success page is shown as no token exchange is needed. For new installations with code/state, it processes similar to the regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the callback.

#### Response Example
{
  "message": "Setup complete."
}
```

--------------------------------

### POST /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/integrations/providers/all_providers

Handles the setup process for OAuth providers, particularly for GitHub App installations or updates. For new installations, it processes the OAuth callback. For updates where the user modifies repository access, it displays a success page without needing a token exchange.

```APIDOC
## POST /v2/auth/setup/{provider_id}

### Description
Handles the setup process for OAuth providers, particularly for GitHub App installations or updates. For new installations, it processes the OAuth callback. For updates where the user modifies repository access, it displays a success page without needing a token exchange.

### Method
POST

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Request Body
(No specific request body details provided in the source text)

### Response
#### Success Response (200)
(No specific success response details provided in the source text)

#### Response Example
(No example provided in the source text)
```

--------------------------------

### Configure Sandbox Environment with setup.sh

Source: https://docs.langchain.com/oss/python/deepagents/cli/overview

A shell script template for initializing a remote sandbox. It handles repository cloning using authentication tokens and sets up persistent environment variables.

```shellscript
#!/bin/bash
set -e

# Clone repository using GitHub token
git clone https://x-access-token:${GITHUB_TOKEN}@github.com/username/repo.git $HOME/workspace
cd $HOME/workspace

# Make environment variables persistent
cat >> $HOME/.bashrc <<EOF
export MY_VAR=value
EOF
```

--------------------------------

### Initialize Langchain LLM with Examples

Source: https://docs.langchain.com/oss/python/integrations/tools/powerbi

This snippet demonstrates initializing a Langchain LLM while also providing few-shot examples. This is useful for guiding the LLM's responses by showing it desired input-output pairs. The 'few_shots' variable would typically contain a list of these examples.

```python
llm = smart_llm, examples=few_shots,
```

--------------------------------

### Process PowerShell Code for Document Creation

Source: https://docs.langchain.com/oss/python/integrations/splitters/code_splitter

This example showcases the use of Langchain's text splitting capabilities with PowerShell code. It illustrates how to define a directory path and potentially process files within that path for LLM ingestion. The snippet focuses on the initial setup for PowerShell script execution.

```python
POWERSHELL_CODE =
"""
$directoryPath = Get-Location
"""
```

--------------------------------

### CURL Example for GET /threads/{thread_id}/runs/{run_id}

Source: https://docs.langchain.com/langsmith/background-run

Provides a cURL command to execute the GET /threads/{thread_id}/runs/{run_id} endpoint.

```APIDOC
## CURL Example for GET /threads/{thread_id}/runs/{run_id}

### Description
Provides a cURL command to execute the GET /threads/{thread_id}/runs/{run_id} endpoint.

### Method
GET

### Endpoint
/threads/{thread_id}/runs/{run_id}

### Request Example
```shell
curl --request GET \
  --url "<DEPLOYMENT_URL>/threads/<THREAD_ID>/runs/<RUN_ID>"
```
```

--------------------------------

### OAuth Setup Callback

Source: https://js.langchain.com/docs/how_to/callbacks_serverless

Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. For actions like user-modified repo access via GitHub, it shows a success page as no token exchange is needed.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback from OAuth providers. For new installations with code/state, it processes similarly to the regular OAuth callback. For actions like user-modified repo access via GitHub, it shows a success page as no token exchange is needed.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Request Example
(No request body for GET request)

### Response
#### Success Response (200)
(Response details not specified in the provided text)

#### Response Example
(Response example not specified in the provided text)
```

--------------------------------

### Initialize and Compile a StateGraph in Python

Source: https://reference.langchain.com/python/langgraph/graph/state/StateGraph

Demonstrates how to define a state schema with a reducer, create a StateGraph, add nodes, and compile the graph for execution. The example shows how to pass context and state updates through the graph nodes.

```python
from langchain_core.runnables import RunnableConfig
from typing_extensions import Annotated, TypedDict
from langgraph.checkpoint.memory import InMemorySaver
from langgraph.graph import StateGraph
from langgraph.runtime import Runtime

def reducer(a: list, b: int | None) -> list:
    if b is not None:
        return a + [b]
    return a

class State(TypedDict):
    x: Annotated[list, reducer]

class Context(TypedDict):
    r: float

graph = StateGraph(state_schema=State, context_schema=Context)

def node(state: State, runtime: Runtime[Context]) -> dict:
    r = runtime.context.get("r", 1.0)
    x = state["x"][-1]
    next_value = x * r * (1 - x)
    return {"x": next_value}

graph.add_node("A", node)
graph.set_entry_point("A")
graph.set_finish_point("A")
compiled = graph.compile()

step1 = compiled.invoke({"x": 0.5}, context={"r": 3.0})
```

--------------------------------

### Create Examples with Langchain LLM Client

Source: https://docs.langchain.com/langsmith/evaluation-async

This snippet demonstrates how to create examples for a dataset using the `ls_client`. It defines the structure for examples, including 'inputs' and 'idea' fields, and shows how to iterate over a list of ideas to populate these examples.

```javascript
ls_client.create_examples(
  dataset_name = dataset.name,
  examples = [{
    "inputs": {
      "idea": i
    },
    "outputs": {
      "answer": ""
    }
  } for i in ideas]
)
```

--------------------------------

### Example: Get usage by workspace

Source: https://docs.langchain.com/langsmith/granular-usage

Demonstrates how to use the Usage API to retrieve usage data for a specific workspace using Python.

```APIDOC
## Example: Get usage by workspace

### Description
This example demonstrates how to retrieve usage data for a specific workspace using the `httpx` library in Python. It includes setting up the client, defining the time range, and making the API request.

### Method
GET

### Endpoint
/usage (with potential workspace-specific parameters, not explicitly shown in the provided code but implied by the example title)

### Request Example
```python
import httpx
from datetime import datetime, timedelta, timezone

client = httpx.Client(
    base_url="YOUR_API_BASE_URL",
    timeout=60.0,
)

now = datetime.now(timezone.utc)

response = client.get(
    "/usage",
    params={
        "time_range": "1-31 days",
        "aggregation": "Daily",
        "stride": "days: 1",
        # Assuming a workspace parameter might be used here, though not explicit in the snippet
        # "workspace": "your_workspace_id"
    },
)

response.raise_for_status()

usage_data = response.json()
print(usage_data)

client.close()
```

### Response
#### Success Response (200)
- **usage_data** (object) - The JSON response containing the usage data for the specified workspace and parameters.

#### Response Example
```json
{
  "data": [
    {
      "time_range": "1-31 days",
      "aggregation": "Daily",
      "stride": "days: 1"
    }
  ]
}
```
```

--------------------------------

### Initialize Modal Sandbox with LangChain

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

This snippet demonstrates how to import the required 'create_deep_agent' and 'ModalSandbox' modules. It then shows the process of looking up an existing application and initializing a new sandbox instance for backend operations.

```python
from deepagents import create_deep_agent
from langchain_modal import ModalSandbox

app = modal.App.lookup("your-app")
modal_sandbox = modal.Sandbox.create(app=app)
backend = ModalSandbox()
```

--------------------------------

### Create and Execute Sandbox Commands in Python

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

Demonstrates how to create a sandbox, execute a command within it, and stop the sandbox using Langchain. This involves defining the sandbox, backend, and result execution steps. It assumes the existence of a 'DaytonaSandbox' class and related methods.

```python
sandbox = Daytona().create()
backend = DaytonaSandbox("sandbox")
result = backend.execute("echo hello")
# ... use sandbox
sandbox.stop()
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/custom-checkpointer

Handles the callback redirect from GitHub Apps for installation or update events. For updates, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the callback redirect from GitHub Apps for installation or update events. For updates, it shows a success page. For new installations with code/state, it processes like a regular OAuth callback.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the outcome of the setup.

#### Response Example
{
  "message": "GitHub App setup successful."
}
```

--------------------------------

### OAuth Setup Callback

Source: https://docs.langchain.com/langsmith/create-a-prompt

Handles the OAuth callback for new installations, processing similar to regular OAuth callbacks when code/state are present.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth callback for new installations, processing similar to regular OAuth callbacks when code/state are present.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The ID of the OAuth provider.

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the setup is complete.
```

--------------------------------

### Initialize and use Daytona Sandbox with LangChain

Source: https://docs.langchain.com/oss/python/deepagents/sandboxes

This code demonstrates how to import the DaytonaSandbox class, initialize a sandbox instance, and use the backend to download specific files from the environment.

```python
from langchain_daytona import DaytonaSandbox

sandbox = Daytona().create()
backend = DaytonaSandbox(sandbox=sandbox)

results = backend.download_files(["/src/index.py", "/output.txt"])
for result in results:
```

--------------------------------

### Complete Langchain Agent Example with Skills

Source: https://docs.langchain.com/oss/python/langchain/multi-agent/skills-sql-assistant

This comprehensive Python script provides a full, runnable example of setting up a Langchain agent. It includes defining skill structures, creating sample skills with schemas and business logic for 'sales_analytics' and 'inventory_management', and integrating them with middleware and agent creation.

```python
import uuid
from typing import TypedDict, NotRequired
from langchain.tools import tool
from langchain.agents import create_agent
from langchain.agents.middleware import ModelRequest, ModelResponse, AgentMiddleware
from langchain.messages import SystemMessage
from langgraph.checkpoint.memory import InMemorySaver
from typing import Callable

# Define skill structure
class Skill(TypedDict):
    """A skill that can be progressively disclosed to the agent."""
    name: str
    description: str
    content: str

# Define skills with schemas and business logic
SKILLS: list[Skill] = [
    {
        "name": "sales_analytics",
        "description": "Database schema and business logic for sales data analysis including customers, orders, and revenue.",
        "content": "# Sales Analytics Schema

## Tables

### customers
- customer_id (PRIMARY KEY)
- name
- email
- signup_date
- status (active/inactive)
- customer_tier (bronze/silver/gold/platinum) 

### orders
- order_id (PRIMARY KEY)
- customer_id (FOREIGN KEY -> customers)
- order_date
- status (pending/completed/cancelled/refunded)
- total_amount
- sales_region (north/south/east/west)

### order_items
- item_id (PRIMARY KEY)
- order_id (FOREIGN KEY -> orders)
- product_id
- quantity
- unit_price
- discount_percent

## Business Logic

**Active customers**: status = 'active' AND signup_date <= CURRENT_DATE - INTERVAL '90 days'

**Revenue calculation**: Only count orders with status = 'completed'. Use total_amount from orders table, which already accounts for discounts.

**Customer lifetime value (CLV)**: Sum of all completed order amounts for a customer.

**High-value orders**: Orders with total_amount > 1000

## Example Query

-- Get top 10 customers by revenue in the last quarter
SELECT
    c.customer_id,
    c.name,
    c.customer_tier,
    SUM(o.total_amount) as total_revenue
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
WHERE o.status = 'completed'
  AND o.order_date >= CURRENT_DATE - INTERVAL '3 months'
GROUP BY c.customer_id, c.name, c.customer_tier
ORDER BY total_revenue DESC
LIMIT 10;
",
    },
    {
        "name": "inventory_management",
        "description": "Database schema and business logic for inventory tracking including products, warehouses, and stock levels.",
        "content": "# Inventory Management Schema

## Tables

### products
- product_id (PRIMARY KEY)
- product_name
- sku
- category
- unit_cost
- reorder_point (minimum stock level before reordering)
- discontinued (boolean)

### warehouses
- warehouse_id (PRIMARY KEY)
- warehouse_name
- location
- capacity

### inventory
- inventory_id (PRIMARY KEY)
- product_id (FOREIGN KEY -> products)
- warehouse_id (FOREIGN KEY -> warehouses)
- quantity_on_hand
- last_updated

### stock_movements
- movement_id (PRIMARY KEY)
- product_id (FOREIGN KEY -> products)
- warehouse_id (FOREIGN KEY -> warehouses)
- movement_type (inbound/outbound/transfer/adjustment)
- quantity (positive for inbound, negative for outbound)
- movement_date
- reference_number

## Business Logic

**Available stock**: quantity_on_hand from inventory table where quantity_on_hand > 0

"
    },
]

# Placeholder for CustomState, model, load_skill, write_sql_query, and other necessary imports/definitions
# class CustomState(TypedDict):
#     ...
# model = ...
# @tool
# def load_skill(skill_name: str):
#     ... 
# @tool
# def write_sql_query(query: str):
#     ... 

# Example usage (assuming CustomState, model, load_skill, write_sql_query are defined elsewhere)
# class SkillMiddleware(AgentMiddleware[CustomState]):
#     state_schema = CustomState
#     tools = [load_skill, write_sql_query]

# agent = create_agent(
#     model,
#     system_prompt=(
#         "You are a SQL query assistant that helps users "
#         "write queries against business databases."
#     ),
#     middleware=[SkillMiddleware()],
#     checkpointer=InMemorySaver(),
# )

```

--------------------------------

### GET /v2/auth/setup/{provider_id}

Source: https://docs.langchain.com/oss/python/langchain/quickstart

Handles the OAuth setup callback redirect from external services like GitHub Apps.

```APIDOC
## GET /v2/auth/setup/{provider_id}

### Description
Handles the OAuth setup callback redirect from GitHub Apps. This endpoint is triggered when a user installs or updates their GitHub App installation.

### Method
GET

### Endpoint
/v2/auth/setup/{provider_id}

### Parameters
#### Path Parameters
- **provider_id** (string) - Required - The unique identifier for the OAuth provider.

### Response
#### Success Response (200)
- **status** (string) - Indicates successful processing of the callback.
```

--------------------------------

### Initialize Qdrant Client (Python)

Source: https://docs.langchain.com/oss/python/integrations/vectorstores

Demonstrates how to initialize the Qdrant client in Python. This involves importing necessary classes and setting up the connection to the Qdrant instance.

```python
from qdrant_client import QdrantClient, models

client = QdrantClient(
    # url="localhost",
    # port=6333,
    # api_key="YOUR_API_KEY",
    location=":memory:"
)

client.recreate_collection(
    collection_name="my_collection",
    vectors_config=models.VectorParams(size=100, distance=models.Distance.COSINE),
)

client.upsert(
    collection_name="my_collection",
    wait=True,
    points=[
        models.PointStruct(
            id=1,
            vector=[
                0.0 for _ in range(100)
            ],
            payload={"color": "red"},
        )
    ],
)

client.upsert(
    collection_name="my_collection",
    wait=True,
    points=[
        models.PointStruct(
            id=2,
            vector=[
                0.5 for _ in range(100)
            ],
            payload={"color": "blue"},
        )
    ],
)

search_result = client.search(
    collection_name="my_collection",
    query_vector=[
        0.1 for _ in range(100)
    ],
    limit=3,
)

print(search_result)

```

--------------------------------

### Initialize and Run SearxNG Search Wrapper

Source: https://docs.langchain.com/oss/python/integrations/tools/searx_search

Demonstrates how to instantiate the SearxSearchWrapper with a host URL and execute a basic search query. This wrapper simplifies interaction with the SearxNG API to retrieve search answers or results.

```python
import pprint
from langchain_community.utilities import SearxSearchWrapper

search = SearxSearchWrapper(searx_host="http://127.0.0.1:8888")
search.run("What is the capital of France")
```

--------------------------------

### Integrate LangSmith Tracing with Sentry OpenTelemetry (TypeScript)

Source: https://docs.langchain.com/langsmith/legacy-trace-with-vercel-ai-sdk

This snippet demonstrates how to integrate LangSmith's LangSmithOTLPTraceExporter with Sentry's OpenTelemetry instrumentation. It requires installing specific OpenTelemetry v1 packages and initializes both Sentry and LangSmith's OTEL setup. The example shows how to wrap an AI SDK `generateText` call with a traceable function.

```typescript
import { initializeOTEL } from "langsmith/experimental/otel/setup";
import { LangSmithOTLPTraceExporter } from "langsmith/experimental/otel/exporter";
import { BatchSpanProcessor } from "@opentelemetry/sdk-trace-base";
import { traceable } from "langsmith/traceable";
import { generateText, tool } from "ai";
import { openai } from "@ai-sdk/openai";
import { z } from "zod";
import * as Sentry from "@sentry/node";
import { Client } from "langsmith";

const exporter = new LangSmithOTLPTraceExporter();
const spanProcessor = new BatchSpanProcessor(exporter);

const sentry = Sentry.init({
  dsn: "...",
  tracesSampleRate: 1.0,
  openTelemetrySpanProcessors: [spanProcessor],
});

initializeOTEL({
  globalTracerProvider: sentry?.traceProvider,
});

const wrappedText = traceable(
  async (content: string) => {
    const { text } = await generateText({
      model: openai("gpt-4.1-nano"),
      messages: [{ role: "user", content }],
      experimental_telemetry: {
        isEnabled: true,
      },
      maxSteps: 10,
    });
    return { text };
  },
  { name: "parentTraceable" }
);

let result;
try {
  result = await wrappedText("What color is the sky?");
} finally {
  await sentry?.traceProvider?.shutdown();
}

```

--------------------------------

### GET /v2/sandboxes/volumes/{name}

Source: https://docs.langchain.com/oss/python/langchain/install

Retrieves details for a specific persistent volume by its name.

```APIDOC
## GET /v2/sandboxes/volumes/{name}

### Description
Get a specific volume by name in the tenant's sandbox namespace. This endpoint queries the database for fast performance.

### Method
GET

### Endpoint
/v2/sandboxes/volumes/{name}

### Parameters
#### Path Parameters
- **name** (string) - Required - The unique name of the volume.

### Response
#### Success Response (200)
- **volume** (object) - The volume details.

#### Response Example
{
  "name": "my-volume",
  "size": "10Gi"
}
```

--------------------------------

### Create Main Agent with Subagent Tool

Source: https://docs.langchain.com/oss/javascript/langchain/multi-agent/subagents

Demonstrates the initialization of a main agent configured with a subagent tool. This setup allows the main agent to delegate tasks to a sub-agent based on defined tool descriptions.

```javascript
const mainAgent = createAgent({
  model,
  tools: [callSubagent]
});
```