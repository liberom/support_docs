### Setup and Build n8n Development Environment

Source: https://docs.n8n.io/embed/white-labelling

Commands to clone the n8n repository, install necessary dependencies, and start the development server for local customization.

```bash
git clone https://github.com/<your-organization>/n8n.git n8n
cd n8n
npm install
npm run build
npm run start
```

--------------------------------

### Setup n8n Node Project

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Commands to clone the n8n node starter repository and install the necessary project dependencies.

```bash
git clone https://github.com/<your-organization>/<your-repo-name>.git n8n-nodes-nasa-pics
cd n8n-nodes-nasa-pics
npm i
```

--------------------------------

### Start n8n with Docker Compose

Source: https://docs.n8n.io/hosting/installation/server-setups/docker-compose

This command initiates the Docker containers defined in the `compose.yaml` file in detached mode. Ensure that your `.env` file is correctly configured and that Docker is installed and running on your system.

```bash
sudo docker compose up -d
```

--------------------------------

### Install and Publish Node

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Commands to install the n8n CLI globally and publish the custom node locally for testing purposes.

```bash
npm install n8n -g
```

```bash
npm run build
npm link
```

--------------------------------

### Install a Community Node using npm

Source: https://docs.n8n.io/integrations/community-nodes/installation/manual-install

Installs a specified community node package from the npm registry into your n8n environment. Ensure you have navigated to the correct directory first.

```bash
npm i n8n-nodes-nodeName
```

--------------------------------

### Create and Navigate to n8n Nodes Directory

Source: https://docs.n8n.io/integrations/community-nodes/installation/manual-install

This command sequence creates the necessary directory for custom n8n nodes if it does not exist and then navigates into it. This is where you will install community nodes.

```bash
mkdir ~/.n8n/nodes
cd ~/.n8n/nodes
```

--------------------------------

### Start n8n Instance

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Command to initialize the n8n application after linking custom nodes.

```bash
n8n start
```

--------------------------------

### Authenticate API requests using cURL

Source: https://docs.n8n.io/api/authentication

Demonstrates how to retrieve active workflows by sending a GET request with the X-N8N-API-KEY header. The example covers both self-hosted instances and n8n Cloud environments.

```bash
# For a self-hosted n8n instance
curl -X 'GET' \
  '<N8N_HOST>:<N8N_PORT>/<N8N_PATH>/api/v<version-number>/workflows?active=true' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'

# For n8n Cloud
curl -X 'GET' \
  '<your-cloud-instance>/api/v<version-number>/workflows?active=true' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'
```

--------------------------------

### Run n8n with Tunnel (Services Only)

Source: https://docs.n8n.io/hosting/installation/docker

This approach involves running n8n locally and cloudflared as a separate service. It requires two terminals: one to start the cloudflared tunnel pointing to your local n8n instance, and another to start n8n. This method also sets up necessary environment variables for webhook functionality.

```bash
# Terminal 1: Start the cloudflared tunnel service
pnpm --filter n8n-containers services --services cloudflared

# Terminal 2: Start n8n locally
pnpm dev
```

--------------------------------

### Initialize n8n Node Project

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

Commands to clone the n8n node starter repository and install necessary project dependencies.

```bash
git clone https://github.com/<your-organization>/<your-repo-name>.git n8n-nodes-friendgrid
cd n8n-nodes-friendgrid
npm i
```

--------------------------------

### Build and link n8n nodes locally

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

Commands to install n8n globally, build the custom node package, and link it to the local n8n installation directory for testing.

```bash
npm install n8n -g

# In your node directory
npm run build
npm link

# In the nodes directory within your n8n installation
npm link <node-package-name>

n8n start
```

--------------------------------

### Example of Input Parameters Reference in n8n

Source: https://docs.n8n.io/data/expressions-for-transformation

This JSON example shows how to reference input parameters within an n8n workflow. The error 'Can't get data for expression' can occur if this step is tested without being connected to a preceding node that provides the necessary input data.

```json
{
  "my_field_1": {{ $input.params }}
}
```

--------------------------------

### Trigger Webhook Node using curl

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.webhook/common-issues

Examples of using the curl command-line tool to interact with n8n Webhook nodes. These examples demonstrate GET and POST requests, including sending data bodies, headers, and files.

```bash
curl --request GET https://your-n8n.url/webhook/path
```

```bash
curl --request POST https://your-n8n.url/webhook/path --data 'key=value'
```

```bash
curl --request GET https://your-n8n.url/webhook/path --header 'key=value'
```

```bash
curl --request POST https://your-n8n.url/webhook/path --form 'key=@/path/to/file'
```

--------------------------------

### Install a Specific Version of a Community Node

Source: https://docs.n8n.io/integrations/community-nodes/installation/manual-install

Installs a particular version of a community node package from the npm registry. This is useful for downgrading or pinning to a stable version.

```bash
npm install n8n-nodes-nodeName@version
```

--------------------------------

### Configure OAuth Scopes for Google API

Source: https://docs.n8n.io/integrations/builtin/credentials/google/oauth-generic

Example of a space-separated list of OAuth scopes required for Gmail API operations within an n8n credential configuration.

```text
https://www.googleapis.com/auth/gmail.labels https://www.googleapis.com/auth/gmail.addons.current.action.compose
```

--------------------------------

### Initialize PostgreSQL Database and User

Source: https://docs.n8n.io/hosting/configuration/supported-databases-settings

SQL commands to create a dedicated database and user for n8n, granting the necessary privileges for schema management.

```sql
CREATE DATABASE n8n-db;
CREATE USER n8n-user WITH PASSWORD 'random-password';
GRANT ALL PRIVILEGES ON DATABASE n8n-db TO n8n-user;
```

--------------------------------

### Initialize Custom Directory

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Troubleshooting commands to manually create the custom directory and initialize an npm project if it does not exist in the n8n installation path.

```bash
mkdir custom
cd custom
npm init
```

--------------------------------

### Manage Docker Compose Services

Source: https://docs.n8n.io/hosting/installation/server-setups/digital-ocean

Commands to start and stop the n8n and Caddy services defined in the Docker Compose file.

```bash
sudo docker compose up -d
```

```bash
sudo docker compose stop
```

--------------------------------

### Fetch Lead Form Responses from LinkedIn API

Source: https://docs.n8n.io/integrations/builtin/credentials/linkedin

An example GET request to retrieve lead form responses from the LinkedIn API. This is used after setting up webhook notifications to fetch the actual lead data.

```http
GET https://api.linkedin.com/rest/leadFormResponses?owner=(organization:urn%3Ali%3Aorganization%3A123456)&leadType=(leadType:SPONSORED)&q=owner
```

--------------------------------

### Install n8n custom node via npm

Source: https://docs.n8n.io/integrations/community-nodes/installation/manual-install

This command installs a specific version of an n8n node package from the npm registry. Replace the placeholder version number with the desired release version.

```bash
npm install n8n-nodes-nodeName@2.1.0
```

--------------------------------

### Using Expressions in n8n Customer Messenger Node

Source: https://docs.n8n.io/try-it-out/quickstart

This snippet demonstrates how to use expressions within the n8n Customer Messenger node to dynamically populate message content. It maps customer ID and constructs a personalized message using variables from the previous node's output. This is useful for creating dynamic and personalized communication within workflows.

```javascript
Hi {{ $json.customer_name }}. Your description is: {{ $json.customer_description }}
```

--------------------------------

### GET /credentials

Source: https://docs.n8n.io/release-notes

Retrieves a paginated list of all credentials across the n8n instance, providing visibility into which project each credential belongs to.

```APIDOC
## GET /credentials

### Description
Returns a paginated list of all credentials across the instance, including the project they belong to, to assist in security auditing.

### Method
GET

### Endpoint
/credentials

### Parameters
#### Query Parameters
- **page** (integer) - Optional - The page number for pagination.
- **limit** (integer) - Optional - Number of items per page.

### Response
#### Success Response (200)
- **credentials** (array) - List of all credentials in the instance.
- **total** (integer) - Total count of credentials.

#### Response Example
{
  "credentials": [
    { "id": "cred_1", "name": "AWS", "projectId": "proj_A" }
  ],
  "total": 1
}
```

--------------------------------

### Install Node into n8n Instance

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Linking the local node package into the n8n custom extensions directory. Replace <node-package-name> with the actual name defined in your package.json.

```bash
cd ~/.n8n/custom/
npm link <node-package-name>
```

--------------------------------

### Get Workflows with Pagination (cURL)

Source: https://docs.n8n.io/api/pagination

This snippet shows how to retrieve active workflows using cURL, specifying a limit of 150 results per page. It includes examples for both self-hosted and n8n Cloud instances, requiring an API key for authentication. The response contains a 'nextCursor' if more pages are available.

```shell
# For a self-hosted n8n instance
curl -X 'GET' \
  '<N8N_HOST>:<N8N_PORT>/<N8N_PATH>/api/v<version-number>/workflows?active=true&limit=150' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'

# For n8n Cloud
curl -X 'GET' \
  '<your-cloud-instance>/api/v<version-number>/workflows?active=true&limit=150' \
  -H 'accept: application/json' \
  -H 'X-N8N-API-KEY: <your-api-key>'
```

--------------------------------

### Dockerfile for Custom n8n Image

Source: https://docs.n8n.io/integrations/creating-nodes/deploy/install-private-nodes

A Dockerfile configuration that installs n8n, necessary system dependencies, and fonts. It sets up the environment to support custom node integration by defining the entry point and working directories.

```dockerfile
FROM node:16-alpine

ARG N8N_VERSION

RUN if [ -z "$N8N_VERSION" ] ; then echo "The N8N_VERSION argument is missing!" ; exit 1; fi

# Update everything and install needed dependencies
RUN apk add --update graphicsmagick tzdata git tini su-exec

# Set a custom user to not have n8n run as root
USER root

# Install n8n and the packages it needs to build it correctly.
RUN apk --update add --virtual build-dependencies python3 build-base ca-certificates && \
	npm config set python "$(which python3)" && \
	npm_config_user=root npm install -g full-icu n8n@${N8N_VERSION} && \
	apk del build-dependencies \
	&& rm -rf /root /tmp/* /var/cache/apk/* && mkdir /root;


# Install fonts
RUN apk --no-cache add --virtual fonts msttcorefonts-installer fontconfig && \
	update-ms-fonts && \
	fc-cache -f && \
	apk del fonts && \
	find  /usr/share/fonts/truetype/msttcorefonts/ -type l -exec unlink {} \; \
	&& rm -rf /root /tmp/* /var/cache/apk/* && mkdir /root

ENV NODE_ICU_DATA /usr/local/lib/node_modules/full-icu

WORKDIR /data

COPY docker-entrypoint.sh /docker-entrypoint.sh
ENTRYPOINT ["tini", "--", "/docker-entrypoint.sh"]

EXPOSE 5678/tcp
```

--------------------------------

### Run n8n with Tunnel (Full Stack)

Source: https://docs.n8n.io/hosting/installation/docker

This command starts n8n and the cloudflared tunnel service together in Docker containers. The tunnel URL will be printed on startup, and all necessary configurations for webhook access will be handled automatically. This is intended for local development and testing only.

```bash
pnpm stack --tunnel
```

--------------------------------

### GET /.well-known/openid-configuration

Source: https://docs.n8n.io/user-management/oidc/setup

Retrieves the OpenID Connect discovery document from an identity provider to automate configuration of authentication settings.

```APIDOC
## GET /.well-known/openid-configuration

### Description
Fetches the OpenID Connect discovery document, which contains metadata about the identity provider's endpoints, supported scopes, and public keys.

### Method
GET

### Endpoint
`/.well-known/openid-configuration`

### Parameters
#### Path Parameters
- **tenant-id** (string) - Required (for Azure AD) - The unique identifier for the Azure AD tenant.
- **region** (string) - Required (for Cognito) - The AWS region where the user pool is hosted.
- **user-pool-id** (string) - Required (for Cognito) - The unique identifier for the Amazon Cognito user pool.

### Request Example
GET https://accounts.google.com/.well-known/openid-configuration

### Response
#### Success Response (200)
- **issuer** (string) - The issuer URL of the identity provider.
- **authorization_endpoint** (string) - The URL for the authorization request.
- **token_endpoint** (string) - The URL for the token exchange request.
- **jwks_uri** (string) - The URL for the JSON Web Key Set.

#### Response Example
{
  "issuer": "https://accounts.google.com",
  "authorization_endpoint": "https://accounts.google.com/o/oauth2/v2/auth",
  "token_endpoint": "https://oauth2.googleapis.com/token",
  "jwks_uri": "https://www.googleapis.com/oauth2/v3/certs"
}
```

--------------------------------

### n8n Workflow: Convert JSON to Binary File

Source: https://docs.n8n.io/courses/level-two/chapter-2

This n8n workflow demonstrates how to fetch JSON data from an API, convert it into a binary file, write that file to the disk, and then read it back. It utilizes the HTTP Request, Convert to File, and Read/Write Files from Disk nodes. The workflow starts with a manual trigger and ends with reading the created file.

```json
{
	"name": "JSON to file and Read-Write",
	"nodes": [
		{
		"parameters": {},
		"id": "78639a25-b69a-4b9c-84e0-69e045bed1a3",
		"name": "When clicking \"Execute Workflow\"",
		"type": "n8n-nodes-base.manualTrigger",
		"typeVersion": 1,
		"position": [
			480,
			520
		]
		},
		{
		"parameters": {
			"url": "https://poetrydb.org/random/1",
			"options": {}
		},
		"id": "a11310df-1287-4e9a-b993-baa6bd4265a6",
		"name": "HTTP Request",
		"type": "n8n-nodes-base.httpRequest",
		"typeVersion": 4.1,
		"position": [
			680,
			520
		]
		},
		{
		"parameters": {
			"operation": "toJson",
			"options": {}
		},
		"id": "06be18f6-f193-48e2-a8d9-35f4779d8324",
		"name": "Convert to File",
		"type": "n8n-nodes-base.convertToFile",
		"typeVersion": 1,
		"position": [
			880,
			520
		]
		},
		{
		"parameters": {
			"operation": "write",
			"fileName": "/tmp/poetrydb.json",
			"options": {}
		},
		"id": "f2048e5d-fa8f-4708-b15a-d07de359f2e5",
		"name": "Read/Write Files from Disk",
		"type": "n8n-nodes-base.readWriteFile",
		"typeVersion": 1,
		"position": [
			1080,
			520
		]
		},
		{
		"parameters": {
			"fileSelector": "={{ $json.fileName }}",
			"options": {}
		},
		"id": "d630906c-09d4-49f4-ba14-416c0f4de1c8",
		"name": "Read/Write Files from Disk1",
		"type": "n8n-nodes-base.readWriteFile",
		"typeVersion": 1,
		"position": [
			1280,
			520
		]
		}
	],
	"pinData": {},
	"connections": {
		"When clicking \"Execute Workflow\"": {
		"main": [
			[
			{
				"node": "HTTP Request",
				"type": "main",
				"index": 0
			}
			]
		]
		},
		"HTTP Request": {
		"main": [
			[
			{
				"node": "Convert to File",
				"type": "main",
				"index": 0
			}
			]
		]
		},
		"Convert to File": {
		"main": [
			[
			{
				"node": "Read/Write Files from Disk",
				"type": "main",
				"index": 0
			}
			]
		]
		},
		"Read/Write Files from Disk": {
		"main": [
			[
			{
				"node": "Read/Write Files from Disk1",
				"type": "main",
				"index": 0
			}
			]
		]
		}
	}
}
```

--------------------------------

### HashiCorp Vault KV v1 Policy Example

Source: https://docs.n8n.io/external-secrets

This example shows a simplified Vault policy for a KV v1 mount at the 'kv/' path. It grants both read and list capabilities for secrets stored under this path, suitable for older KV versions.

```hcl
# Read and list secrets at the "kv/" KV v1 mount
path "kv/*" {
  capabilities = ["read", "list"]
}
```

--------------------------------

### GET /webhook (Challenge Verification)

Source: https://docs.n8n.io/integrations/builtin/credentials/linkedin

Handles the initial webhook registration challenge request from LinkedIn to verify the endpoint ownership.

```APIDOC
## GET /webhook

### Description
Responds to LinkedIn's webhook registration challenge request. Must respond within 3 seconds.

### Method
GET

### Endpoint
/webhook

### Parameters
#### Query Parameters
- **challengeCode** (string) - Required - The unique code sent by LinkedIn for verification.

### Response
#### Success Response (200)
- **challengeCode** (string) - The original code received.
- **challengeResponse** (string) - HMAC-SHA256 hash of the challenge code using the Client Secret.

### Response Example
{
  "challengeCode": "890e4665-4dfe-4ab1-b689-ed553bceeed0",
  "challengeResponse": "27b1d19678542072a7f1d0ce845d0c78cec22567f413697e25648f44fa3d1514"
}
```

--------------------------------

### GET /healthz/readiness

Source: https://docs.n8n.io/hosting/logging-monitoring/monitoring

The /healthz/readiness endpoint is similar to /healthz, but it returns an HTTP status code of 200 only if the database is connected and migrated, indicating the instance is ready to accept traffic.

```APIDOC
## GET /healthz/readiness

### Description
Checks if the n8n instance is ready to accept traffic, including database connection and migration status.

### Method
GET

### Endpoint
`<your-instance-url>/healthz/readiness`

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **status** (string) - Indicates the instance is ready.

#### Response Example
```json
{
  "status": "ok"
}
```
```

--------------------------------

### n8n Workflow Structure Example

Source: https://docs.n8n.io/embed/managing-workflows

This is an example of the JSON structure returned when fetching a workflow. It includes details about the workflow's nodes, parameters, and positions, representing a typical n8n workflow definition.

```json
{
  "data": {
    "id": "1012",
    "name": "Nathan's Workflow",
    "active": false,
    "nodes": [
      {
        "parameters": {},
        "name": "Start",
        "type": "n8n-nodes-base.start",
        "typeVersion": 1,
        "position": [
          130,
          640
        ]
      },
      {
        "parameters": {
          "authentication": "headerAuth",
          "url": "https://internal.users.n8n.cloud/webhook/custom-erp",
          "options": {
            "splitIntoItems": true
          },
          "headerParametersUi": {
            "parameter": [
              {
                "name": "unique_id",
                "value": "recLhLYQbzNSFtHNq"
              }
            ]
          }
        },
        "name": "HTTP Request",
        "type": "n8n-nodes-base.httpRequest",
        "typeVersion": 1,
        "position": [
          430,
          300
        ],
        "credentials": {
          "httpHeaderAuth": "beginner_course"
        }
      },
      {
        "parameters": {
          "operation": "append",
          "application": "appKBGQfbm6NfW6bv",
          "table": "processingOrders",
          "options": {}
        },
        "name": "Airtable",
        "type": "n8n-nodes-base.airtable",
        "typeVersion": 1,
        "position": [
          990,
          210
        ],
        "credentials": {
          "airtableApi": "Airtable"
        }
      },
      {
        "parameters": {
          "conditions": {
            "string": [
              {
                "value1": "={{$json["orderStatus"]}}",
                "value2": "processing"
              }
            ]
          }
        },
        "name": "IF",
        "type": "n8n-nodes-base.if",
        "typeVersion": 1,
        "position": [
          630,
          300
        ]
      },
      {
        "parameters": {
          "keepOnlySet": true,
          "values": {
            "number": [
              {
                "name": "=orderId",
                "value": "={{$json["orderID"]}}"
              }
            ],
            "string": [
              {
                "name": "employeeName",
                "value": "={{$json["employeeName"]}}"
              }
            ]
          },
          "options": {}
        },
        "name": "Set",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": [
          800,
          210
        ]
      },
      {
        "parameters": {
          "functionCode": "let totalBooked = items.length;\nlet bookedSum = 0;\n\nfor(let i=0; i < items.length; i++) {\n  bookedSum = bookedSum + items[i].json.orderPrice;\n}\nreturn [{json:{totalBooked, bookedSum}}]\n"
        },
        "name": "Function",
        "type": "n8n-nodes-base.function",
        "typeVersion": 1,
        "position": [
          800,
          400
        ]
      },
      {
        "parameters": {
          "webhookUri": "https://discord.com/api/webhooks/865213348202151968/oD5_WPDQwtr22Vjd_82QP3-_4b_lGhAeM7RynQ8Js5DzyXrQEnj0zeAQIA6fki1JLtXE",
          "text": "=This week we have {{$json["totalBooked"]}} booked orders with a total value of {{$json["bookedSum"]}}. My Unique ID: {{ $("HTTP Request").params.headerParameters.parameters[0].value }}"
        },
        "name": "Discord",
        "type": "n8n-nodes-base.discord",
        "typeVersion": 1,
        "position": [
          1000,
          400
        ]
      },
      {
        "parameters": {
          "triggerTimes": {
            "item": [
              {
                "mode": "everyWeek",
                "hour": 9
              }
            ]
          }
        },
        "name": "Cron",
        "type": "n8n-nodes-base.cron",
        "typeVersion": 1,
        "position": [
          220,
          300
        ]
      }
    ]
  }
}
```

--------------------------------

### GET /templates/categories

Source: https://docs.n8n.io/embed/workflow-templates

Retrieves a list of available template categories.

```APIDOC
## GET /templates/categories

### Description
Returns a list of all template categories available in the n8n library.

### Method
GET

### Endpoint
/templates/categories

### Response
#### Success Response (200)
- **categories** (array) - List of category objects

#### Response Example
{
  "categories": [
    {
      "id": 1,
      "name": "Automation"
    }
  ]
}
```

--------------------------------

### GET /templates/collections

Source: https://docs.n8n.io/embed/workflow-templates

Retrieves a list of template collections.

```APIDOC
## GET /templates/collections

### Description
Returns a list of curated template collections.

### Method
GET

### Endpoint
/templates/collections

### Response
#### Success Response (200)
- **collections** (array) - List of collection objects

#### Response Example
{
  "collections": [
    {
      "id": 1,
      "rank": 1,
      "name": "Featured",
      "totalViews": 1000,
      "createdAt": "2023-01-01T00:00:00Z",
      "workflows": [{"id": 123}],
      "nodes": []
    }
  ]
}
```

--------------------------------

### HashiCorp Vault KV v2 Policy Example

Source: https://docs.n8n.io/external-secrets

This example demonstrates a minimal Vault policy required for a KV v2 mount at the 'secret/' path. It grants read access to secrets and read/list access to metadata, ensuring secure access to secrets stored in the vault.

```hcl
# Read and list secrets at the "secret/" KV v2 mount
path "secret/data/*" {
  capabilities = ["read"]
}
path "secret/metadata/*" {
  capabilities = ["read", "list"]
}
```

--------------------------------

### GET /drives

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive/shared-drive-operations

Retrieves a list of shared drives based on optional query filters and pagination settings.

```APIDOC
## GET /drives

### Description
Retrieves multiple shared drives. Supports filtering via query strings and pagination.

### Method
GET

### Endpoint
/drives

### Parameters
#### Query Parameters
- **returnAll** (boolean) - Optional - Whether to return all results.
- **limit** (integer) - Optional - Maximum number of items to return.
- **q** (string) - Optional - Query string to filter shared drives.
- **useDomainAdminAccess** (boolean) - Optional - Whether to issue the request as a domain administrator.

### Response
#### Success Response (200)
- **drives** (array) - A list of shared drive objects.

### Response Example
{
  "drives": [
    { "id": "1", "name": "Drive A" },
    { "id": "2", "name": "Drive B" }
  ]
}
```

--------------------------------

### Simplify Node Authentication Setup with Generic Interface

Source: https://docs.n8n.io/release-notes/0-x

This code demonstrates the new generic authentication setup for n8n nodes. It uses the `IAuthenticateGeneric` interface to define how credentials are used in requests, supporting methods like bearer and basic auth by passing data in headers, body, or query strings. This approach is not suitable for complex multi-call authentication like OAuth.

```typescript
import {
	IAuthenticateGeneric,
	ICredentialType,
	INodeProperties,
} from 'n8n-workflow';

export class AsanaApi implements ICredentialType {
	name = 'asanaApi';
	displayName = 'Asana API';
	documentationUrl = 'asana';
	properties: INodeProperties[] = [
		{
			displayName: 'Access Token',
			name: 'accessToken',
			type: 'string',
			default: '',
		},
	];

	authenticate: IAuthenticateGeneric = {
		type: 'generic',
		properties: {
			headers: {
				Authorization: '=Bearer {{$credentials.accessToken}}',
			},
		},
	};
}
```

--------------------------------

### Configure Weaviate Search Filters

Source: https://docs.n8n.io/integrations/builtin/cluster-nodes/root-nodes/n8n-nodes-langchain.vectorstorezep

Demonstrates the JSON structure for applying conditional filters in Weaviate queries. This example uses the 'OR' operator to match documents based on specific metadata source values.

```JSON
{
  "OR": [
    {
        "path": ["source"],
        "operator": "Equal",
        "valueString": "source1"
    },
    {
        "path": ["source"],
        "operator": "Equal",
        "valueString": "source1"
    }
  ]
}
```

--------------------------------

### Schedule Trigger Configuration in n8n

Source: https://docs.n8n.io/courses/level-two/chapter-2

Sets up a 'Schedule Trigger' node to run the workflow at a defined interval. This example configures the trigger to run every 30 minutes.

```json
{
	"parameters": {
		"rule": {
		"interval": [
			{
			"field": "minutes",
			"minutesInterval": 30
			}
		]
		}
	},
	"id": "6e8e4308-d0e0-4d0d-bc29-5131b57cf061",
	"name": "Schedule Trigger",
	"type": "n8n-nodes-base.scheduleTrigger",
	"typeVersion": 1.1,
	"position": [
		620,
		480
	]
}
```

--------------------------------

### Set NASA Node Start Date with Expression

Source: https://docs.n8n.io/try-it-out/tutorial-first-workflow

This snippet demonstrates how to use an n8n expression to set the start date for the NASA node to one week prior to the current date. It utilizes the Luxon library's date manipulation capabilities, specifically the `$today.minus()` method.

```n8n Expression
{{ $today.minus(7, 'days') }}
```

--------------------------------

### Set up sample data using JavaScript Code node for n8n

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.removeduplicates/templates-and-examples

This JavaScript code snippet is used within an n8n Code node to generate sample data. It creates an array of objects, each representing a person with an ID, name, job, and last updated timestamp. This data is intended to be used with the Remove Duplicates node to demonstrate its functionality. The 'Run Once for Each Item' mode and 'JavaScript' language should be selected in the Code node.

```javascript
let data =[];

return {
  data: [
    { id: 1, name: 'Taylor Swift', job: 'Pop star', last_updated: '2024-09-20T10:12:43.493Z' },
    { id: 2, name: 'Ed Sheeran', job: 'Singer-songwriter', last_updated: '2024-10-05T08:30:59.493Z' },
    { id: 3, name: 'Adele', job: 'Singer-songwriter', last_updated: '2024-10-07T14:15:59.493Z' },
    { id: 4, name: 'Bruno Mars', job: 'Singer-songwriter', last_updated: '2024-08-25T17:45:12.493Z' },
    { id: 1, name: 'Taylor Swift', job: 'Pop star', last_updated: '2024-09-20T10:12:43.493Z' },  // duplicate
    { id: 5, name: 'Billie Eilish', job: 'Singer-songwriter', last_updated: '2024-09-10T09:30:12.493Z' },
    { id: 6, name: 'Katy Perry', job: 'Pop star', last_updated: '2024-10-08T12:30:45.493Z' },
    { id: 2, name: 'Ed Sheeran', job: 'Singer-songwriter', last_updated: '2024-10-05T08:30:59.493Z' },  // duplicate
    { id: 7, name: 'Lady Gaga', job: 'Pop star', last_updated: '2024-09-15T14:45:30.493Z' },
    { id: 8, name: 'Rihanna', job: 'Pop star', last_updated: '2024-10-01T11:50:22.493Z' },
    { id: 3, name: 'Adele', job: 'Singer-songwriter', last_updated: '2024-10-07T14:15:59.493Z' },  // duplicate
    //{ id: 9, name: 'Tom Hanks', job: 'Actor', last_updated: '2024-10-17T13:58:31.493Z' },
    //{ id: 0, name: 'Madonna', job: 'Pop star', last_updated: '2024-10-17T17:11:38.493Z' },
    //{ id: 15, name: 'Bob Dylan', job: 'Folk singer', last_updated: '2024-09-24T08:03:16.493Z'},
    //{ id: 10, name: 'Harry Nilsson', job: 'Singer-songwriter', last_updated: '2020-10-17T17:11:38.493Z' },
    //{ id: 11, name: 'Kylie Minogue', job: 'Pop star', last_updated: '2024-10-24T08:03:16.493Z'}
  ]
}
```

--------------------------------

### Access Docker Shell for n8n

Source: https://docs.n8n.io/integrations/community-nodes/installation/manual-install

This command allows you to access the Docker shell of your running n8n instance. This is a prerequisite for managing community nodes via npm.

```bash
docker exec -it n8n sh
```

--------------------------------

### Wait Node Configuration in n8n

Source: https://docs.n8n.io/courses/level-two/chapter-2

Sets up a 'Wait' node to pause workflow execution for a specified duration. This example configures a wait of 1 minute, which can be useful for rate limiting or synchronizing with external systems.

```json
{
	"parameters": {
		"amount": 1,
		"unit": "minutes"
	},
	"id": "5aa860b7-c73c-4df0-ad63-215850166f13",
	"name": "Wait",
	"type": "n8n-nodes-base.wait",
	"typeVersion": 1.1,
	"position": [
		1480,
		260
	],
	"webhookId": "be78732e-787d-463e-9210-2c7e8239761e"
}
```

--------------------------------

### Configure UI Elements (JSON, HTML, Notice, Hints)

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

Configuration objects for standard n8n UI components. Includes setup for JSON editors, HTML templates, notice boxes, and parameter-level hints.

```javascript
{
	displayName: 'Content (JSON)',
	name: 'content',
	type: 'json',
	default: '',
	displayOptions: {
		show: {
			resource: [],
			operation: []
		}
	}
}

{
	displayName: 'HTML Template',
	name: 'html',
	type: 'string',
	typeOptions: {
		editor: 'htmlEditor'
	},
	default: placeholder,
	noDataExpression: true,
	description: 'HTML template to render'
}

{
	displayName: 'Your text here',
	name: 'notice',
	type: 'notice',
	default: ''
}

{
	displayName: 'URL',
	name: 'url',
	type: 'string',
	hint: 'Enter a URL'
}
```

--------------------------------

### Custom Auth - Sending Two Headers

Source: https://docs.n8n.io/integrations/builtin/credentials/httprequest

Example of configuring Custom Auth to send two custom headers. This is useful when an API requires specific headers for authentication.

```json
{
	"headers": {
		"X-AUTH-USERNAME": "username",
		"X-AUTH-PASSWORD": "password"
	}
}
```

--------------------------------

### GET /health

Source: https://docs.n8n.io/embed/workflow-templates

Checks the health status of the API.

```APIDOC
## GET /health

### Description
Returns the current health status of the n8n API service.

### Method
GET

### Endpoint
/health

### Response
#### Success Response (200)
- **status** (string) - The health status (e.g., "ok")
```

--------------------------------

### Custom Auth - Sending Query String Parameters

Source: https://docs.n8n.io/integrations/builtin/credentials/httprequest

Example of configuring Custom Auth to send authentication details as query string parameters. This is useful for APIs that accept authentication tokens or keys in the URL.

```json
{
	"qs": {
		"appid": "123456",
		"apikey": "my-api-key"
	}
}
```

--------------------------------

### Making HTTP Requests with n8n Helper

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/http-helpers

Demonstrates how to use the n8n `httpRequest` helper within the `execute` function. It shows examples for making requests with and without authentication, utilizing the `this.helpers.httpRequest` and `this.helpers.httpRequestWithAuthentication` methods respectively.

```javascript
// If no auth needed
const response = await this.helpers.httpRequest(options);

// If auth needed
const response = await this.helpers.httpRequestWithAuthentication.call(
	this, 
	'credentialTypeName', // For example: pipedriveApi
	options,
);

```

--------------------------------

### GET /rest/leadFormResponses

Source: https://docs.n8n.io/integrations/builtin/credentials/linkedin

Retrieves the actual lead data after receiving a notification via the webhook.

```APIDOC
## GET /rest/leadFormResponses

### Description
Fetches lead form responses for a specific owner and lead type.

### Method
GET

### Endpoint
https://api.linkedin.com/rest/leadFormResponses

### Parameters
#### Query Parameters
- **owner** (string) - Required - The URN of the organization or account.
- **leadType** (string) - Required - The type of lead to filter by.
- **q** (string) - Required - Query parameter set to 'owner'.
```

--------------------------------

### Configure PostgreSQL Environment Variables for n8n

Source: https://docs.n8n.io/hosting/configuration/supported-databases-settings

Sets the required environment variables to connect n8n to a PostgreSQL database instance. Includes optional TLS configuration for secure connections.

```bash
export DB_TYPE=postgresdb
export DB_POSTGRESDB_DATABASE=n8n
export DB_POSTGRESDB_HOST=postgresdb
export DB_POSTGRESDB_PORT=5432
export DB_POSTGRESDB_USER=n8n
export DB_POSTGRESDB_PASSWORD=n8n
export DB_POSTGRESDB_SCHEMA=n8n

# optional:
export DB_POSTGRESDB_SSL_CA=$(pwd)/ca.crt
export DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false

n8n start
```

--------------------------------

### Create an Assistant

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/assistant-operations

Creates a new assistant with specified configurations, including model, name, description, instructions, and optional tools like code interpreter and knowledge retrieval.

```APIDOC
## POST /assistants

### Description
Use this operation to create a new assistant.

### Method
POST

### Endpoint
/assistants

### Parameters
#### Request Body
- **credential** (object) - Required - OpenAI credential to connect with.
- **resource** (string) - Required - Must be 'Assistant'.
- **operation** (string) - Required - Must be 'Create an Assistant'.
- **model** (string) - Required - The model that the assistant will use (e.g., `gpt-4o`, `gpt-4o-mini`).
- **name** (string) - Required - The name of the assistant. Max length: 256 characters.
- **description** (string) - Optional - The description of the assistant. Max length: 512 characters.
- **instructions** (string) - Optional - The system instructions that the assistant uses. Max length: 32,768 characters.
- **codeInterpreter** (boolean) - Optional - Enable the code interpreter for the assistant.
- **knowledgeRetrieval** (boolean) - Optional - Enable knowledge retrieval for the assistant.
  - **files** (array) - Optional - A list of files to upload for your external knowledge source.

### Options
- **outputRandomnessTemperature** (number) - Optional - Adjust the randomness of the response. Range: 0.0 to 1.0. Defaults to 1.0.
- **outputRandomnessTopP** (number) - Optional - Adjust the Top P setting to control diversity. Defaults to 1.0.
- **failIfAssistantAlreadyExists** (boolean) - Optional - If enabled, the operation will fail if an assistant with the same name already exists.

### Request Example
```json
{
  "credential": {"id": "your_credential_id"},
  "resource": "Assistant",
  "operation": "Create an Assistant",
  "model": "gpt-4o",
  "name": "My Virtual Assistant",
  "description": "A virtual assistant that helps users with daily tasks.",
  "instructions": "Always respond in a friendly and engaging manner.",
  "codeInterpreter": true,
  "knowledgeRetrieval": false,
  "outputRandomnessTemperature": 0.7,
  "failIfAssistantAlreadyExists": true
}
```

### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the created assistant.
- **name** (string) - The name of the assistant.
- **description** (string) - The description of the assistant.
- **model** (string) - The model used by the assistant.
- **instructions** (string) - The instructions for the assistant.
- **tools** (array) - The tools enabled for the assistant (e.g., code_interpreter, retrieval).

#### Response Example
```json
{
  "id": "asst_abc123",
  "name": "My Virtual Assistant",
  "description": "A virtual assistant that helps users with daily tasks.",
  "model": "gpt-4o",
  "instructions": "Always respond in a friendly and engaging manner.",
  "tools": [
    {
      "type": "code_interpreter"
    }
  ],
  "created_at": 1677652000
}
```
```

--------------------------------

### GET /drives/{driveId}

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive/shared-drive-operations

Retrieves the details of a specific shared drive by its ID, URL, or selection from a list.

```APIDOC
## GET /drives/{driveId}

### Description
Retrieves metadata for a specific shared drive.

### Method
GET

### Endpoint
/drives/{driveId}

### Parameters
#### Path Parameters
- **driveId** (string) - Required - The unique identifier of the shared drive.

#### Query Parameters
- **useDomainAdminAccess** (boolean) - Optional - Whether to issue the request as a domain administrator.

### Response
#### Success Response (200)
- **id** (string) - The ID of the shared drive.
- **name** (string) - The name of the shared drive.

### Response Example
{
  "id": "0AN-123456789",
  "name": "Project Team Drive"
}
```

--------------------------------

### Generic Authentication with Query String Parameter (TypeScript)

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/credentials-files

This example demonstrates how to configure generic authentication in n8n to send a token as a query string parameter. The code is written in TypeScript and uses the `IAuthenticateGeneric` interface.

```typescript
authenticate: IAuthenticateGeneric = {
	type: 'generic',
	properties: {
		qs: {
			token: '={{$credentials.token}}',
		},
	},
};
```

--------------------------------

### Add Filters to Pipedrive Organization: Get All Operation

Source: https://docs.n8n.io/release-notes/0-x

The Pipedrive node now supports filters for the 'Organization: Get All' operation. This enhancement allows users to retrieve specific organization data based on defined filter criteria, improving data selection efficiency.

```javascript
Pipedrive node: adds support for filters to the Organization: Get All operation.
```

--------------------------------

### Set Subtitle Based on Parameter Values

Source: https://docs.n8n.io/integrations/creating-nodes/plan/node-ui-design

This example demonstrates how to dynamically set a subtitle for a node based on the values of its parameters. It uses an expression to concatenate the 'operation' and 'resource' parameter values, separated by a colon.

```javascript
subtitle: '={{$parameter["operation"] + ": " + $parameter["resource"]}}'
```

--------------------------------

### GET /workflows/templates/{id}

Source: https://docs.n8n.io/embed/workflow-templates

Retrieves a workflow template with a flat structure. The response directly contains the workflow definition without nested metadata.

```APIDOC
## GET /workflows/templates/{id}

### Description
Retrieves a workflow template with a flat structure. The response directly contains the workflow definition without nested metadata.

### Method
GET

### Endpoint
/workflows/templates/{id}

### Parameters
#### Path Parameters
- **id** (number) - Required - The ID of the workflow template to retrieve.

### Response
#### Success Response (200)
- **id** (number) - The ID of the workflow.
- **name** (string) - The name of the workflow.
- **workflow** (object) - The actual workflow definition.
  - **nodes** (array) - An array of nodes in the workflow.
  - **connections** (object) - The connections between nodes in the workflow.

#### Response Example
```json
{
  "id": 123,
  "name": "...",
  "workflow": {
    "nodes": [...],
    "connections": {}
  }
}
```
```

--------------------------------

### GET /templates/workflows/{id}

Source: https://docs.n8n.io/embed/workflow-templates

Retrieves a workflow template with a wrapped structure. The response includes template metadata and the workflow definition nested within a 'workflow' key.

```APIDOC
## GET /templates/workflows/{id}

### Description
Retrieves a workflow template with a wrapped structure. The response includes template metadata and the workflow definition nested within a 'workflow' key.

### Method
GET

### Endpoint
/templates/workflows/{id}

### Parameters
#### Path Parameters
- **id** (number) - Required - The ID of the workflow template to retrieve.

### Response
#### Success Response (200)
- **workflow** (object) - Contains the workflow template data, including metadata and the nested workflow definition.
  - **id** (number) - The ID of the workflow.
  - **name** (string) - The name of the workflow.
  - **totalViews** (number) - The total number of views for the workflow.
  - **price** (any) - The price of the workflow (if applicable).
  - **purchaseUrl** (any) - The URL to purchase the workflow (if applicable).
  - **recentViews** (number) - The number of recent views for the workflow.
  - **createdAt** (string) - The creation date of the workflow.
  - **user** (object) - Information about the user who created the workflow.
    - **username** (string) - The username of the creator.
    - **verified** (boolean) - Indicates if the user is verified.
  - **workflow** (object) - The actual workflow definition.
    - **nodes** (array) - An array of nodes in the workflow.
    - **connections** (object) - The connections between nodes in the workflow.

#### Response Example
```json
{
  "workflow": {
    "id": 123,
    "name": "...",
    "totalViews": 1000,
    "workflow": {
      "nodes": [...],
      "connections": {}
    }
  }
}
```
```

--------------------------------

### Get Specific Template Collection

Source: https://docs.n8n.io/workflows/templates

Retrieves details for a specific collection of workflow templates.

```APIDOC
## GET /templates/collections/<id>

### Description
Gets a specific template collection.

### Method
GET

### Endpoint
`/templates/collections/<id>`

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the template collection.

### Response
#### Success Response (200)
- **collection** (object) - Information about the template collection.
  - **id** (string) - The collection ID.
  - **name** (string) - The name of the collection.
  - **description** (string) - A description of the collection.
  - **templates** (array) - A list of templates within the collection.

#### Response Example
```json
{
  "id": "collection-abc",
  "name": "Featured Templates",
  "description": "A curated list of popular and useful templates.",
  "templates": [
    {
      "id": "workflow-123",
      "name": "Data Processing Workflow"
    }
  ]
}
```
```

--------------------------------

### Enable Google Cloud APIs and Environment Variables

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

Configures the required Google Cloud services and sets project-specific environment variables for the deployment process.

```bash
gcloud auth login

gcloud services enable run.googleapis.com
gcloud services enable sqladmin.googleapis.com
gcloud services enable secretmanager.googleapis.com

export PROJECT_ID=your-project
export REGION=region-where-you-want-this-deployed
```

--------------------------------

### Get License Information (n8n CLI)

Source: https://docs.n8n.io/release-notes/0-x

This command retrieves information about licenses for self-hosted n8n users. It is a command-line interface tool provided by n8n.

```bash
n8n license:info
```

--------------------------------

### Initialize custom directory for n8n

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

Commands to manually create the custom directory within the n8n configuration folder if it does not exist.

```bash
# In ~/.n8n directory run
mkdir custom 
cd custom 
npm init
```

--------------------------------

### Get a message

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/message-operations

Retrieves a single Gmail message, with an option for a simplified or raw data response.

```APIDOC
## Get a message

### Description
Use this operation to get a single message. You can choose to return a simplified version or the raw data.

### Method
GET

### Endpoint
/users.messages/{id}

### Parameters
#### Path Parameters
- **userId** (string) - Required - The ID of the user's mailbox. Use 'me' to refer to the authenticated user.
- **id** (string) - Required - The ID of the message to retrieve.

#### Query Parameters
- **format** (string) - Optional - The format to return the message in. Can be 'full' or 'metadata'. Defaults to 'metadata' (simplified).
- **metadataHeaders** (string) - Optional - When specified, the value of this field is used as a prefix to the labels that are returned in the metadata.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **id** (string) - The unique ID of the message.
- **threadId** (string) - The unique ID of the thread associated with the message.
- **labelIds** (array) - The list of IDs of labels associated with this message.
- **snippet** (string) - The snippet of the message's content.
- **payload** (object) - The message's content and headers (if format is 'full').

#### Response Example
```json
{
  "id": "17a8b3a4c5d6e7f8",
  "threadId": "17a8b3a4c5d6e7f8",
  "labelIds": [
    "INBOX",
    "UNREAD"
  ],
  "snippet": "This is a sample snippet of the message content.",
  "payload": {
    "partId": "0",
    "mimeType": "text/plain",
    "filename": "",
    "headers": [
      {
        "name": "Date",
        "value": "Tue, 15 Aug 2023 10:00:00 +0000"
      },
      {
        "name": "From",
        "value": "Sender Name <sender@example.com>"
      }
    ],
    "body": {
      "size": 123,
      "data": "SGVsbG8sIHRoaXMgaXMgYSBzYW1wbGUgYm9keS4="
    }
  }
}
```
```

--------------------------------

### GET /metrics

Source: https://docs.n8n.io/hosting/logging-monitoring/monitoring

The /metrics endpoint provides detailed information about the current status of the n8n instance. This endpoint is not available on n8n Cloud and is disabled by default for self-hosted instances.

```APIDOC
## GET /metrics

### Description
Provides detailed metrics about the n8n instance status. Not available on n8n Cloud.

### Method
GET

### Endpoint
`<your-instance-url>/metrics`

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **metrics** (object) - Contains various metrics about the instance.

#### Response Example
```json
{
  "process_version": "1.35.0",
  "event_queue_length": 0,
  "webhook_queue_length": 0,
  "active_workflows": 5,
  "active_nodes": 10
}
```
```

--------------------------------

### GET /projects/{projectId}/users

Source: https://docs.n8n.io/release-notes

Retrieves a list of all members associated with a specific project, including their assigned roles for auditing purposes.

```APIDOC
## GET /projects/{projectId}/users

### Description
Returns all members of a project including their assigned role to facilitate project access auditing.

### Method
GET

### Endpoint
/projects/{projectId}/users

### Parameters
#### Path Parameters
- **projectId** (string) - Required - The unique identifier of the project.

### Response
#### Success Response (200)
- **users** (array) - List of project members with their roles.

#### Response Example
{
  "users": [
    { "userId": "123", "role": "owner" },
    { "userId": "456", "role": "editor" }
  ]
}
```

--------------------------------

### GET /workflows (Paginated)

Source: https://docs.n8n.io/api/pagination

Retrieves a list of workflows with support for pagination using limit and cursor parameters.

```APIDOC
## GET /workflows

### Description
Retrieves a list of workflows. Supports pagination via the 'limit' query parameter and 'cursor' for subsequent pages.

### Method
GET

### Endpoint
/api/v<version-number>/workflows

### Parameters
#### Query Parameters
- **active** (boolean) - Optional - Filter by active status.
- **limit** (integer) - Optional - Number of results per page (Default: 100, Max: 250).
- **cursor** (string) - Optional - The cursor value from the previous response to fetch the next page.

### Request Example
curl -X 'GET' 'https://n8n.example.com/api/v1/workflows?active=true&limit=150' -H 'X-N8N-API-KEY: <your-api-key>'

### Response
#### Success Response (200)
- **data** (array) - List of workflow objects.
- **nextCursor** (string) - The cursor string to use for the next page request.

#### Response Example
{
  "data": [
    { "id": "1", "name": "Workflow A" }
  ],
  "nextCursor": "MTIzZTQ1NjctZTg5Yi0xMmQzLWE0NTYtNDI2NjE0MTc0MDA"
}
```

--------------------------------

### Get Many messages

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/message-operations

Retrieves multiple Gmail messages with various filtering and sorting options.

```APIDOC
## Get Many messages

### Description
Use this operation to get two or more messages. You can specify various filters to refine the results.

### Method
GET

### Endpoint
/users.messages

### Parameters
#### Path Parameters
- **userId** (string) - Required - The ID of the user's mailbox. Use 'me' to refer to the authenticated user.

#### Query Parameters
- **maxResults** (integer) - Optional - The maximum number of messages to return. Defaults to 100.
- **pageToken** (string) - Optional - Page token to retrieve the next page of results.
- **q** (string) - Optional - Gmail search refine filters, like `from:`, to filter the messages returned.
- **labelIds** (string) - Optional - Only return messages with the specified label IDs.
- **includeSpamTrash** (boolean) - Optional - Whether to include messages from Spam and Trash folders. Defaults to false.
- **format** (string) - Optional - The format to return the message in. Can be 'full' or 'metadata'. Defaults to 'metadata' (simplified).
- **metadataHeaders** (string) - Optional - When specified, the value of this field is used as a prefix to the labels that are returned in the metadata.
- **processForLabel** (string) - Optional - Specifies whether the messages should be processed for a label.
- **after** (string) - Optional - Return only those emails received after the specified date and time (ISO 8601 format or milliseconds timestamp).
- **before** (string) - Optional - Return only those emails received before the specified date and time (ISO 8601 format or milliseconds timestamp).
- **sender** (string) - Optional - Enter an email or a part of a sender name to return messages from only that sender.
- **unread** (string) - Optional - Filters messages based on read status. Can be 'true' (unread only), 'false' (read only), or omitted (all).

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **messages** (array) - A list of message resources.
  - **id** (string) - The unique ID of the message.
  - **threadId** (string) - The unique ID of the thread associated with the message.
  - **labelIds** (array) - The list of IDs of labels associated with this message.
  - **snippet** (string) - The snippet of the message's content.
- **nextPageToken** (string) - Token to retrieve the next page of results.
- **resultSizeEstimate** (integer) - An estimate of the number of messages that would match the query.

#### Response Example
```json
{
  "messages": [
    {
      "id": "17a8b3a4c5d6e7f8",
      "threadId": "17a8b3a4c5d6e7f8",
      "labelIds": [
        "INBOX",
        "UNREAD"
      ],
      "snippet": "This is a sample snippet of the first message."
    },
    {
      "id": "17a8b3a4c5d6e7f9",
      "threadId": "17a8b3a4c5d6e7f9",
      "labelIds": [
        "INBOX"
      ],
      "snippet": "This is a sample snippet of the second message."
    }
  ],
  "nextPageToken": "CAEQAA",
  "resultSizeEstimate": 2
}
```
```

--------------------------------

### Provision Postgres Database and User

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

Creates a Cloud SQL Postgres instance, initializes the database, and creates a dedicated user for n8n.

```bash
gcloud sql instances create n8n-db \
    --database-version=POSTGRES_13 \
    --tier=db-f1-micro \
    --region=$REGION \
    --root-password="change-this-password" \
    --storage-size=10GB \
    --availability-type=ZONAL \
    --no-backup \
    --storage-type=HDD

gcloud sql databases create n8n --instance=n8n-db

gcloud sql users create n8n-user \
    --instance=n8n-db \
    --password="change-this-password"
```

--------------------------------

### Create Lead Notification Subscription via LinkedIn API

Source: https://docs.n8n.io/integrations/builtin/credentials/linkedin

An example API call to create a webhook subscription for lead notifications using the LinkedIn Lead Sync API. This allows n8n to receive real-time lead data.

```http
POST https://api.linkedin.com/rest/leadNotifications
{
  "webhook": "https://your-n8n-instance.com/webhook/linkedin-leads",
  "owner": {"organization": "urn:li:organization:123456"},
  "leadType": "SPONSORED"
}
```

--------------------------------

### Configure Claude Desktop for n8n MCP

Source: https://docs.n8n.io/advanced-ai/accessing-n8n-mcp-server

Configuration for the claude_desktop_config.json file to enable the n8n MCP server using an access token. Requires Node.js and the supergateway package.

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": [
        "-y",
        "supergateway",
        "--streamableHttp",
        "https://<your-n8n-domain>/mcp-server/http",
        "--header",
        "authorization:Bearer <YOUR_N8N_MCP_TOKEN>"
      ]
    }
  }
}
```

--------------------------------

### Configure n8n Docker container with host access

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.mysql/common-issues

Command to start an n8n container on Linux with the host-gateway flag. This allows the n8n instance to resolve the host machine's services via host.docker.internal.

```bash
docker run -it --rm --add-host host.docker.internal:host-gateway --name n8n -p 5678:5678 -v n8n_data:/home/node/.n8n docker.n8n.io/n8nio/n8n
```

--------------------------------

### POST /api/v1/source-control/pull

Source: https://docs.n8n.io/source-control-environments/using/copy-work

This endpoint allows you to automatically pull changes into your n8n instance. It is designed to be called after merging changes, for example, from a CI/CD pipeline.

```APIDOC
## POST /api/v1/source-control/pull

### Description
Automatically pulls changes into the n8n instance. This is useful for integrating with CI/CD pipelines to update a production instance after code merges.

### Method
POST

### Endpoint
`/api/v1/source-control/pull`

### Parameters
#### Request Body
- **force** (boolean) - Optional - If set to `true`, forces the pull operation, potentially overwriting local changes.

### Request Example
```json
{
  "force": true
}
```

### Response
#### Success Response (200)
This endpoint typically returns a 200 OK status upon successful execution. The response body may be empty or contain a confirmation message.

#### Response Example
(No specific response body example provided in the source text, but a 200 OK status is expected.)
```

--------------------------------

### Using $fromAI() Function for Dynamic Parameter Values

Source: https://docs.n8n.io/advanced-ai/examples/using-the-fromai-function

The $fromAI() function allows AI to dynamically fill parameters for tools connected to the AI Agent node. It takes a 'key' and optional 'description', 'type', and 'defaultValue' to guide the AI. This function is not compatible with the Code tool or other non-tool cluster sub-nodes.

```javascript
 {{ $fromAI('email') }}
```

```javascript
$fromAI("name", "The commenter's name", "string", "Jane Doe")
```

```javascript
$fromAI("name")
```

```javascript
$fromAI("numItemsInStock", "Number of items in stock", "number", 5)
```

```javascript
Generated by AI: {{ $fromAI("subject") }}
```

--------------------------------

### Extend n8nio/runners Image with Custom Dependencies

Source: https://docs.n8n.io/hosting/configuration/task-runners

This Dockerfile extends the official `n8nio/runners` image to include additional npm and pip packages. It first switches to the root user to install dependencies using `pnpm` for JavaScript and `uv pip` for Python, then copies a custom configuration file, and finally switches back to the runner user. Ensure you are using version `1.121.0` or later.

```dockerfile
FROM n8nio/runners:1.121.0
USER root
RUN cd /opt/runners/task-runner-javascript && pnpm add moment uuid
RUN cd /opt/runners/task-runner-python && uv pip install numpy pandas
COPY n8n-task-runners.json /etc/n8n-task-runners.json
USER runner
```

--------------------------------

### Update a Community Node to the Latest Version

Source: https://docs.n8n.io/integrations/community-nodes/installation/manual-install

Updates a specified community node package to its latest available version from the npm registry. Use with caution due to potential breaking changes.

```bash
npm update n8n-nodes-nodeName
```

--------------------------------

### Configure loadOptions for dynamic GUI parameters

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/declarative-style-parameters

The loadOptions object defines how to query an external service to populate dynamic fields in the n8n GUI. It includes routing for the API request and output processing to transform, filter, or sort the returned data.

```JavaScript
methods : {
	loadOptions: {
		routing: {
			request: {
				url: '/webhook/example-option-parameters',
				method: 'GET',
			},
			output: {
				postReceive: [
					{
						type: 'rootProperty',
						properties: {
							property: 'responseData',
						},
					},
					{
						type: 'setKeyValue',
						properties: {
							name: '={{$responseItem.key}} ({{$responseItem.value}})',
							value: '={{$responseItem.value}}',
						},
					},
					{
						type: 'sort',
						properties: {
							key: 'name',
						},
					},
				],
			},
		},
	}
}
```

--------------------------------

### Fetch Active Workflows via n8n Cloud API (cURL)

Source: https://docs.n8n.io/api/pagination

This snippet demonstrates how to fetch a list of active workflows from your n8n Cloud instance using a cURL command. It requires your cloud instance URL, API version, and an authentication token (implicitly handled by headers in this example). The output is in JSON format.

```bash
curl -X 'GET' \
  '<your-cloud-instance>/api/v<version-number>/workflows?active=true&limit=150&cursor=MTIzZTQ1NjctZTg5Yi0xMmQzLWE0NTYtNDI2NjE0MTc0MDA' \
  -H 'accept: application/json'
```

--------------------------------

### Generic Authentication with Request Body (TypeScript)

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/credentials-files

This code example shows how to configure generic authentication for an n8n node where credentials (username and password) are sent in the request body. It uses TypeScript and the `IAuthenticateGeneric` interface.

```typescript
authenticate: IAuthenticateGeneric = {
	type: 'generic',
	properties: {
		body: {
			username: '={{$credentials.username}}',
			password: '={{$credentials.password}}',
		},
	},
};
```

--------------------------------

### Custom Auth - Sending Credentials in Body

Source: https://docs.n8n.io/integrations/builtin/credentials/httprequest

Example of configuring Custom Auth to send authentication credentials within the request body. This is common for APIs that expect authentication details in a JSON payload.

```json
{
	 "body" : {
		"user": "username",
		"pass": "password"
	}
}
```

--------------------------------

### Get Year from DateTime

Source: https://docs.n8n.io/data/expression-reference/datetime

Extracts the year from a DateTime object. This property is part of the Luxon library.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.year //=> 2024
```

--------------------------------

### Load Gmail Labels using loadOptions in Programmatic Nodes

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/programmatic-style-parameters

Demonstrates how to use the `loadOptions` method within `methods` to fetch user-specific data, such as Gmail labels. This data is then rendered in the GUI for user selection. It requires access to a Google API and assumes helper functions like `googleApiRequestAllItems` are available.

```typescript
methods = {
		loadOptions: {
			// Get all the labels and display them
			async getLabels(
				this: ILoadOptionsFunctions,
			): Promise<INodePropertyOptions[]> {
				const returnData: INodePropertyOptions[] = [];
				const labels = await googleApiRequestAllItems.call(
					this,
					'labels',
					'GET',
					'/gmail/v1/users/me/labels',
				);
				for (const label of labels) {
					const labelName = label.name;
					const labelId = label.id;
					returnData.push({
						name: labelName,
						value: labelId,
					});
				}
				return returnData;
			},
		},
	};
```

--------------------------------

### Round DateTime units

Source: https://docs.n8n.io/data/expression-reference/datetime

Rounds the DateTime object down to the beginning of a specified unit, such as the start of a month.

```javascript
// dt = "2024-03-20T18:49".toDateTime()
dt.startOf('month') // => 2024-03-01T00:00
```

--------------------------------

### Standard JMESPath library implementation

Source: https://docs.n8n.io/data/specific-data-types/jmespath

This example demonstrates the equivalent functionality using the standard JMESPath library. This approach is typically used in standard Node.js environments rather than n8n expression fields.

```JavaScript
var jmespath = require('jmespath');
jmespath.search(object, searchString);
```

--------------------------------

### Manage n8n Docker Container

Source: https://docs.n8n.io/hosting/installation/docker

These commands are used to manage your n8n Docker container after pulling a new image. First, find the container ID, then stop and remove the old container before starting a new one with the updated image. Replace `<container_id>` and `<container_name>` with your specific values.

```bash
# Find your container ID
docker ps -a

# Stop the container with the <container_id>
docker stop <container_id>

# Remove the container with the <container_id>
docker rm <container_id>

# Start the container
docker run --name=<container_name> [options] -d docker.n8n.io/n8nio/n8n
```

--------------------------------

### Configure Kubernetes persistent storage zone

Source: https://docs.n8n.io/hosting/installation/server-setups/google-kubernetes-engine

Example snippet for defining the storage zone in the storage.yaml manifest to ensure persistent data availability for the Postgres database.

```yaml
allowedTopologies:
  - matchLabelExpressions:
      - key: failure-domain.beta.kubernetes.io/zone
        values:
          - us-central1-b
          - us-central1-c
```

--------------------------------

### Generate RSA Key Pair using OpenSSL

Source: https://docs.n8n.io/integrations/builtin/credentials/wise

This snippet demonstrates how to generate an RSA private and public key pair using the OpenSSL command-line tool. The private key is used for authentication, and the public key is added to the Wise account settings.

```bash
$ openssl genrsa -out private.pem 2048 
$ openssl rsa -pubout -in private.pem -out public.pem
```

--------------------------------

### Import workflows and credentials via n8n CLI

Source: https://docs.n8n.io/hosting/cli-commands

Imports workflows and credentials from JSON files or directories. Supports single file imports or bulk imports from a directory using the --separate flag.

```bash
n8n import:workflow --input=file.json
n8n import:workflow --separate --input=backups/latest/
n8n import:credentials --input=file.json
n8n import:credentials --separate --input=backups/latest/
```

--------------------------------

### Get Current Datetime and Date with Luxon in n8n

Source: https://docs.n8n.io/data/specific-data-types/luxon

Demonstrates how to access the current timestamp and the current date using Luxon's built-in `$now` and `$today` objects within n8n. It shows variations in output when these objects are used in expressions versus the Code node, and across JavaScript and Python.

```javascript
// Expressions (JavaScript)
{{$now}}
// n8n displays the ISO formatted timestamp
// For example 2022-03-09T14:02:37.065+00:00
{{"Today's date is " + $now}}
// n8n displays "Today's date is <unix timestamp>"
// For example "Today's date is 1646834498755"

```

```javascript
// Code node (JavaScript)
$now
// n8n displays <ISO formatted timestamp>
// For example 2022-03-09T14:00:25.058+00:00
let rightNow = "Today's date is " + $now
// n8n displays "Today's date is <unix timestamp>"
// For example "Today's date is 1646834498755"

```

```python
# Code node (Python)
_now
# n8n displays <ISO formatted timestamp>
# For example 2022-03-09T14:00:25.058+00:00
rightNow = "Today's date is " + str(_now)
# n8n displays "Today's date is <unix timestamp>"
# For example "Today's date is 1646834498755"

```

--------------------------------

### Configure Google Cloud CLI and Services

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

Commands to authenticate with Google Cloud and enable the Cloud Run API required for deployment.

```bash
gcloud auth login
gcloud services enable run.googleapis.com
```

--------------------------------

### Get Minute from DateTime - Luxon

Source: https://docs.n8n.io/data/expression-reference/datetime

Retrieves the minute component (0-59) from a DateTime object. A standard property access for time extraction.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.minute //=> 49
```

--------------------------------

### Connect Google ADK Agent to n8n MCP

Source: https://docs.n8n.io/advanced-ai/accessing-n8n-mcp-server

This Python code demonstrates how to initialize a Google ADK agent with an n8n MCP toolset. It uses StreamableHTTPServerParams to establish a secure connection using the instance URL and authorization token.

```python
from google.adk.agents import Agent
from google.adk.tools.mcp_tool import McpToolset
from google.adk.tools.mcp_tool.mcp_session_manager import StreamableHTTPServerParams

N8N_INSTANCE_URL = "https://localhost:5678"
N8N_MCP_TOKEN = "YOUR_N8N_MCP_TOKEN"

root_agent = Agent(
    model="gemini-2.5-pro",
    name="n8n_agent",
    instruction="Help users manage and execute workflows in n8n",
    tools=[
        McpToolset(
            connection_params=StreamableHTTPServerParams(
                url=f"{N8N_INSTANCE_URL}/mcp-server/http",
                headers={
                    "Authorization": f"Bearer {N8N_MCP_TOKEN}",
                },
            ),
        )
    ],
)
```

--------------------------------

### Get Month from DateTime - Luxon

Source: https://docs.n8n.io/data/expression-reference/datetime

Returns the month as a number (1-12) from a DateTime object. This is a direct numerical representation of the month.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.month //=> 3
```

--------------------------------

### GET /rest/workflows/{workflow_id}

Source: https://docs.n8n.io/embed/managing-workflows

Fetches the JSON data of a specific template workflow using its unique ID.

```APIDOC
## GET /rest/workflows/{workflow_id}

### Description
Fetches the JSON data of a specific template workflow using its unique ID.

### Method
GET

### Endpoint
`https://<n8n-domain>/rest/workflows/<workflow_id>`

### Parameters
#### Path Parameters
- **workflow_id** (string) - Required - The unique identifier of the workflow to retrieve.

### Request Example
```
GET https://<n8n-domain>/rest/workflows/1012
```

### Response
#### Success Response (200)
- **data** (object) - Contains the JSON data of the workflow.
  - **id** (string) - The workflow's ID.
  - **name** (string) - The workflow's name.
  - **active** (boolean) - Indicates if the workflow is active.
  - **nodes** (array) - An array of node objects representing the workflow structure.

#### Response Example
```json
{
  "data": {
    "id": "1012",
    "name": "Nathan's Workflow",
    "active": false,
    "nodes": [
      {
        "parameters": {},
        "name": "Start",
        "type": "n8n-nodes-base.start",
        "typeVersion": 1,
        "position": [
          130,
          640
        ]
      },
      {
        "parameters": {
          "authentication": "headerAuth",
          "url": "https://internal.users.n8n.cloud/webhook/custom-erp",
          "options": {
            "splitIntoItems": true
          },
          "headerParametersUi": {
            "parameter": [
              {
                "name": "unique_id",
                "value": "recLhLYQbzNSFtHNq"
              }
            ]
          }
        },
        "name": "HTTP Request",
        "type": "n8n-nodes-base.httpRequest",
        "typeVersion": 1,
        "position": [
          430,
          300
        ],
        "credentials": {
          "httpHeaderAuth": "beginner_course"
        }
      },
      {
        "parameters": {
          "operation": "append",
          "application": "appKBGQfbm6NfW6bv",
          "table": "processingOrders",
          "options": {}
        },
        "name": "Airtable",
        "type": "n8n-nodes-base.airtable",
        "typeVersion": 1,
        "position": [
          990,
          210
        ],
        "credentials": {
          "airtableApi": "Airtable"
        }
      },
      {
        "parameters": {
          "conditions": {
            "string": [
              {
                "value1": "={{$json["orderStatus"]}}",
                "value2": "processing"
              }
            ]
          }
        },
        "name": "IF",
        "type": "n8n-nodes-base.if",
        "typeVersion": 1,
        "position": [
          630,
          300
        ]
      },
      {
        "parameters": {
          "keepOnlySet": true,
          "values": {
            "number": [
              {
                "name": "=orderId",
                "value": "={{$json["orderID"]}}"
              }
            ],
            "string": [
              {
                "name": "employeeName",
                "value": "={{$json["employeeName"]}}"
              }
            ]
          },
          "options": {}
        },
        "name": "Set",
        "type": "n8n-nodes-base.set",
        "typeVersion": 1,
        "position": [
          800,
          210
        ]
      },
      {
        "parameters": {
          "functionCode": "let totalBooked = items.length;\nlet bookedSum = 0;\n\nfor(let i=0; i < items.length; i++) {\n  bookedSum = bookedSum + items[i].json.orderPrice;\n}\nreturn [{json:{totalBooked, bookedSum}}]\n"
        },
        "name": "Function",
        "type": "n8n-nodes-base.function",
        "typeVersion": 1,
        "position": [
          800,
          400
        ]
      },
      {
        "parameters": {
          "webhookUri": "https://discord.com/api/webhooks/865213348202151968/oD5_WPDQwtr22Vjd_82QP3-_4b_lGhAeM7RynQ8Js5DzyXrQEnj0zeAQIA6fki1JLtXE",
          "text": "=This week we have {{$json["totalBooked"]}} booked orders with a total value of {{$json["bookedSum"]}}. My Unique ID: {{ $(\"HTTP Request\").params.headerParameters.parameters[0].value }}"
        },
        "name": "Discord",
        "type": "n8n-nodes-base.discord",
        "typeVersion": 1,
        "position": [
          1000,
          400
        ]
      },
      {
        "parameters": {
          "triggerTimes": {
            "item": [
              {
                "mode": "everyWeek",
                "hour": 9
              }
            ]
          }
        },
        "name": "Cron",
        "type": "n8n-nodes-base.cron",
        "typeVersion": 1,
        "position": [
          220,
          300
        ]
      }
    ]
  }
}
```
```

--------------------------------

### Get Hour from DateTime - Luxon

Source: https://docs.n8n.io/data/expression-reference/datetime

Retrieves the hour component (0-23) from a DateTime object. This is a direct property access.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.hour //=> 18
```

--------------------------------

### Programmatic Node Creation in n8n (TypeScript)

Source: https://docs.n8n.io/integrations/creating-nodes/plan/choose-node-method

Demonstrates building an n8n node using a programmatic TypeScript approach. This method involves defining node properties and the execution logic directly in code, including making HTTP requests. It requires the 'n8n-workflow' package for types and helpers.

```typescript
import {
	IExecuteFunctions,
	INodeExecutionData,
	INodeType,
	INodeTypeDescription,
	IRequestOptions,
} from 'n8n-workflow';

// Create the FriendGrid class
export class FriendGrid implements INodeType {
  description: INodeTypeDescription = {
    displayName: 'FriendGrid',
    name: 'friendGrid',
    . . .
    properties: [
      {
        displayName: 'Resource',
        . . .
      },
      {
        displayName: 'Operation',
        name: 'operation',
        type: 'options',
        displayOptions: {
          show: {
              resource: [
              'contact',
              ],
          },
        },
        options: [
          {
            name: 'Create',
            value: 'create',
            description: 'Create a contact',
          },
        ],
        default: 'create',
        description: 'The operation to perform.',
      },
      {
        displayName: 'Email',
        name: 'email',
        . . .
      },
      {
        displayName: 'Additional Fields',
        // Sets up optional fields
      },
    ],
};

  async execute(this: IExecuteFunctions): Promise<INodeExecutionData[][]> {
    let responseData;
    const resource = this.getNodeParameter('resource', 0) as string;
    const operation = this.getNodeParameter('operation', 0) as string;
    //Get credentials the user provided for this node
    const credentials = await this.getCredentials('friendGridApi') as IDataObject;

    if (resource === 'contact') {
      if (operation === 'create') {
      // Get email input
      const email = this.getNodeParameter('email', 0) as string;
      // Get additional fields input
      const additionalFields = this.getNodeParameter('additionalFields', 0) as IDataObject;
      const data: IDataObject = {
          email,
      };

      Object.assign(data, additionalFields);

      // Make HTTP request as defined in https://sendgrid.com/docs/api-reference/
      const options: IRequestOptions = {
        headers: {
            'Accept': 'application/json',
            'Authorization': `Bearer ${credentials.apiKey}`,
        },
        method: 'PUT',
        body: {
            contacts: [
            data,
            ],
        },
        url: `https://api.sendgrid.com/v3/marketing/contacts`,
        json: true,
      };
      responseData = await this.helpers.httpRequest(options);
      }
    }
    // Map data to n8n data
    return [this.helpers.returnJsonArray(responseData)];
  }
}

```

--------------------------------

### Build Custom n8n Docker Image

Source: https://docs.n8n.io/integrations/creating-nodes/deploy/install-private-nodes

Command to build the customized n8n Docker image using a specific version argument. This command assumes the Dockerfile and necessary node files are present in the build context.

```bash
# Replace <n8n-version-number> with the n8n release version number. 
# For example, N8N_VERSION=0.177.0
docker build --build-arg N8N_VERSION=<n8n-version-number> --tag=customizedn8n .
```

--------------------------------

### Expose Local Server with ngrok

Source: https://docs.n8n.io/integrations/builtin/credentials/getresponse

This command uses ngrok to expose a local server running on port 5678 to the internet. ngrok provides a public URL that can be used as a callback URL for OAuth2 services that do not accept 'localhost'.

```bash
ngrok http 5678
```

--------------------------------

### GET /api/v<version-number>/workflows

Source: https://docs.n8n.io/api/pagination

Retrieves a list of workflows from your n8n Cloud instance. You can filter by active status and specify the number of results and a cursor for pagination.

```APIDOC
## GET /api/v<version-number>/workflows

### Description
Retrieves a list of workflows, with options to filter by active status and control pagination.

### Method
GET

### Endpoint
`/api/v<version-number>/workflows`

### Query Parameters
- **active** (boolean) - Optional - Filters workflows to only include active ones.
- **limit** (integer) - Optional - Specifies the maximum number of workflows to return per page.
- **cursor** (string) - Optional - A cursor for fetching the next page of results.

### Request Example
```bash
curl -X 'GET' \
  '<your-cloud-instance>/api/v<version-number>/workflows?active=true&limit=150&cursor=MTIzZTQ1NjctZTg5Yi0xMmQzLWE0NTYtNDI2NjE0MTc0MDA' \
  -H 'accept: application/json'
```

### Response
#### Success Response (200)
- **data** (array) - A list of workflow objects.
  - **id** (string) - The unique identifier of the workflow.
  - **name** (string) - The name of the workflow.
  - **active** (boolean) - Indicates if the workflow is active.
  - **createdAt** (string) - The timestamp when the workflow was created.
  - **updatedAt** (string) - The timestamp when the workflow was last updated.

#### Response Example
```json
{
  "data": [
    {
      "id": "123e4567-e89b-12d3-a456-426614174000",
      "name": "My First Workflow",
      "active": true,
      "createdAt": "2023-01-01T10:00:00Z",
      "updatedAt": "2023-01-01T10:00:00Z"
    }
  ],
  "nextCursor": "another_cursor_string"
}
```
```

--------------------------------

### Declarative Node Creation in n8n (TypeScript)

Source: https://docs.n8n.io/integrations/creating-nodes/plan/choose-node-method

Illustrates building an n8n node using a declarative TypeScript approach. This method defines node structure and request configurations within the `description` object, simplifying the `execute` method. It leverages `requestDefaults` and `routing` for request handling and `output` for response processing.

```typescript
import { INodeType, INodeTypeDescription } from 'n8n-workflow';

// Create the FriendGrid class
export class FriendGrid implements INodeType {
  description: INodeTypeDescription = {
    displayName: 'FriendGrid',
    name: 'friendGrid',
    . . .
    // Set up the basic request configuration
    requestDefaults: {
      baseURL: 'https://api.sendgrid.com/v3/marketing'
    },
    properties: [
      {
        displayName: 'Resource',
        . . .
      },
      {
        displayName: 'Operation',
        name: 'operation',
        type: 'options',
        displayOptions: {
          show: {
            resource: [
              'contact',
            ],
          },
        },
        options: [
          {
            name: 'Create',
            value: 'create',
            description: 'Create a contact',
            // Add the routing object
            routing: {
              request: {
                method: 'POST',
                url: '=/contacts',
                send: {
                  type: 'body',
                  properties: {
                    email: {{$parameter["email"]}}
                  }
                }
              }
            },
            // Handle the response to contact creation
            output: {
              postReceive: [
                {
                  type: 'set',
                  properties: {
                    value: '={{ { "success": $response } }}'
                  }
                }
              ]
            }
          },
        ],
        default: 'create',
        description: 'The operation to perform.',
      },
      {

```

--------------------------------

### Get first element of Array in n8n

Source: https://docs.n8n.io/data/expression-reference/array

A custom n8n utility method that returns the first element of an array.

```JavaScript
const arr = ['quick', 'brown', 'fox'];
arr.first(); // => 'quick'
```

--------------------------------

### Get Millisecond from DateTime - Luxon

Source: https://docs.n8n.io/data/expression-reference/datetime

Extracts the millisecond component (0-999) of a second from a DateTime object. Useful for high-precision time tracking.

```javascript
// dt = "2024-03-30T18:49:07.234".toDateTime()
dt.millisecond //=> 234
```

--------------------------------

### Uninstall a Community Node using npm

Source: https://docs.n8n.io/integrations/community-nodes/installation/manual-install

Removes a specified community node package from your n8n environment using npm. This is useful for removing nodes or before upgrading/downgrading.

```bash
npm uninstall n8n-nodes-nodeName
```

--------------------------------

### Create and Configure n8n Service Account

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

Sets up a dedicated service account with the necessary IAM permissions to access secrets and Cloud SQL instances.

```bash
gcloud iam service-accounts create n8n-service-account \
    --display-name="n8n Service Account"

gcloud secrets add-iam-policy-binding n8n-db-password \
    --member="serviceAccount:n8n-service-account@$PROJECT_ID.iam.gserviceaccount.com" \
    --role="roles/secretmanager.secretAccessor"

gcloud secrets add-iam-policy-binding n8n-encryption-key \
    --member="serviceAccount:n8n-service-account@$PROJECT_ID.iam.gserviceaccount.com" \
    --role="roles/secretmanager.secretAccessor"

gcloud projects add-iam-policy-binding $PROJECT_ID \
    --member="serviceAccount:n8n-service-account@$PROJECT_ID.iam.gserviceaccount.com" \
    --role="roles/cloudsql.client"
```

--------------------------------

### Verify LinkedIn Notification Signature

Source: https://docs.n8n.io/integrations/builtin/credentials/linkedin

Illustrates the process of verifying the authenticity of incoming notifications from LinkedIn by comparing the X-LI-Signature header with a locally computed HMAC-SHA256 hash of the request body.

```javascript
// Assume 'requestBody' is the JSON-encoded POST body
// Assume 'clientSecret' is your LinkedIn app's client secret

const crypto = require('crypto');

const signature = crypto.createHmac('sha256', clientSecret)
                        .update(requestBody)
                        .digest('hex');

// Compare 'signature' with the 'X-LI-Signature' header from the request
```

--------------------------------

### Get Locale from DateTime - Luxon

Source: https://docs.n8n.io/data/expression-reference/datetime

Retrieves the locale string (e.g., 'en-US') associated with a DateTime object. This locale influences formatting.

```javascript
$now.locale //=> 'en-US'
```

--------------------------------

### Configure Caddy Reverse Proxy

Source: https://docs.n8n.io/hosting/installation/server-setups/digital-ocean

Commands and configuration syntax for setting up the Caddyfile to route traffic to the n8n service.

```bash
nano caddy_config/Caddyfile
```

```text
n8n.<domain>.<suffix> {
    reverse_proxy n8n:5678 {
      flush_interval -1
    }
}
```

--------------------------------

### Query Auth Configuration

Source: https://docs.n8n.io/integrations/builtin/credentials/httprequest

Configures authentication by passing a single key/value query parameter. Requires a query parameter key (Name) and its corresponding Value.

```text
Name: [Query Parameter Key]
Value: [Query Parameter Value]
```

--------------------------------

### Convert Date String to Luxon DateTime in n8n

Source: https://docs.n8n.io/data/specific-data-types/luxon

Illustrates how to parse date strings into Luxon `DateTime` objects in n8n, emphasizing the need for explicit format specification unlike native JavaScript `Date`. It shows examples for ISO 8601 format using `fromISO()`.

```javascript
// Expressions (JavaScript) using fromISO:
{{DateTime.fromISO('2019-06-23T00:00:00.00')}}

```

```javascript
// Code node (JavaScript) using fromISO:
let luxonDateTime = DateTime.fromISO('2019-06-23T00:00:00.00')

```

--------------------------------

### Get all custom execution data

Source: https://docs.n8n.io/data/expression-reference/customdata

Retrieves all key-value pairs stored within the current execution context. Returns an object containing all custom data entries.

```javascript
$execution.customData.getAll() //=> {"user_email": "me@example.com", "id": 1234}
```

--------------------------------

### Get Array Length in JavaScript

Source: https://docs.n8n.io/data/expression-reference/array

The `length` property returns the number of elements in an array. It is a built-in JavaScript property.

```javascript
// names = ["Bob", "Bill", "Nat"];
names.length //=> 3
```

--------------------------------

### Get Day of Month from DateTime

Source: https://docs.n8n.io/data/expression-reference/datetime

Extracts the day of the month (1-31) from a DateTime object. This is a direct property access provided by the Luxon type.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.day //=> 30
```

--------------------------------

### Get Week Number of Year

Source: https://docs.n8n.io/data/expression-reference/datetime

Retrieves the week number of the year, typically ranging from 1 to 52. This property is part of the Luxon library.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.weekNumber //=> 13
```

--------------------------------

### Get last element of Array in n8n

Source: https://docs.n8n.io/data/expression-reference/array

A custom n8n utility method that returns the last element of an array.

```JavaScript
const arr = ['quick', 'brown', 'fox'];
arr.last(); // => 'fox'
```

--------------------------------

### Get Weekday Number

Source: https://docs.n8n.io/data/expression-reference/datetime

Retrieves the day of the week as a number, where 1 represents Monday and 7 represents Sunday. This property is part of the Luxon library.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.weekday //=> 6
```

--------------------------------

### Get Node Data with $()

Source: https://docs.n8n.io/data/expression-reference/root

Retrieves the data of a specified node by its name. This function is part of n8n's custom functionality and returns NodeData.

```javascript
function getNodeData(nodeName) {
  // Example usage: retrieve data for a node named 'myNode'
  return $(nodeName);
}
```

--------------------------------

### GET /healthz

Source: https://docs.n8n.io/hosting/logging-monitoring/monitoring

The /healthz endpoint returns a standard HTTP status code. A 200 status code indicates that the instance is reachable. This endpoint does not verify the database status. It is available for both self-hosted and n8n Cloud users.

```APIDOC
## GET /healthz

### Description
Checks if the n8n instance is reachable.

### Method
GET

### Endpoint
`<your-instance-url>/healthz`

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **status** (string) - Indicates the instance is reachable.

#### Response Example
```json
{
  "status": "ok"
}
```
```

--------------------------------

### Make HTTP Request with n8n

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/let_your_ai_call_an_api.json

Sends an HTTP request to a specified URL, allowing for query parameters and custom options. This node is commonly used to interact with external APIs, such as the Bored API in this example.

```json
{
  "url": "http://www.boredapi.com/api/activity/",
  "sendQuery": true,
  "queryParameters": {
    "parameters": [
      {
        "name": "type",
        "value": "={{ $json.output.type.data }}"
      },
      {
        "name": "participants",
        "value": "={{ $json.output.participants }}"
      }
    ]
  },
  "options": {}
}
```

--------------------------------

### Get Object Keys (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/object

The `keys()` method returns an array containing all the field names (keys) of the object. This functionality is equivalent to JavaScript's native `Object.keys(obj)`. This is a custom n8n functionality.

```javascript
// obj = {'name': 'Mr Nathan', age: 42 }
obj.keys() //=> ['name', 'age']
```

--------------------------------

### Enabling Metrics for Self-Hosted n8n

Source: https://docs.n8n.io/hosting/logging-monitoring/monitoring

To enable the /metrics endpoint for self-hosted n8n instances, set the `N8N_METRICS` environment variable to `true`.

```APIDOC
## Enabling Metrics for Self-Hosted n8n

### Description
Enables the `/metrics` endpoint for self-hosted n8n instances.

### Method
Environment Variable Configuration

### Endpoint
N/A

### Parameters
#### Environment Variables
- **N8N_METRICS** (boolean) - Set to `true` to enable the metrics endpoint.

### Request Example
```
N8N_METRICS=true
```

### Response
N/A
```

--------------------------------

### Configure n8n Persistent Volume Mount

Source: https://docs.n8n.io/hosting/installation/server-setups/azure

Example snippet showing how to mount a persistent volume claim within the n8n deployment manifest to ensure data persistence for binary files and encryption keys.

```yaml
volumes:
  - name: n8n-claim0
    persistentVolumeClaim:
      claimName: n8n-claim0
```

--------------------------------

### Clean up n8n Tunnel Services

Source: https://docs.n8n.io/hosting/installation/docker

This command is used to clean up the resources and configurations set up by the `pnpm --filter n8n-containers services` command. It should be run after you are finished with the local tunnel setup to revert any changes made to environment files or running services.

```bash
pnpm --filter n8n-containers services:clean
```

--------------------------------

### Define Options and Multi-Options Parameters

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

The 'options' type allows users to select a single value from a predefined list, while 'multiOptions' enables the selection of multiple values. Both are essential for resource or event selection within nodes.

```JavaScript
{
	displayName: 'Resource',
	name: 'resource',
	type: 'options',
	options: [
		{ name: 'Image', value: 'image' },
		{ name: 'Template', value: 'template' },
	],
	default: 'image',
	description: 'Resource to consume',
	displayOptions: { show: { resource: [], operation: [] } }
}
```

```JavaScript
{
	displayName: 'Events',
	name: 'events',
	type: 'multiOptions',
	options: [
		{ name: 'Plan Created', value: 'planCreated' },
		{ name: 'Plan Deleted', value: 'planDeleted' },
	],
	default: [],
	description: 'The events to be monitored',
	displayOptions: { show: { resource: [], operation: [] } }
}
```

--------------------------------

### Get Random Array Item (n8n)

Source: https://docs.n8n.io/data/expression-reference/array

The `randomItem()` method returns a randomly selected element from the array. This is a custom n8n functionality.

```javascript
// arr = ['quick', 'brown', 'fox']
arr.randomItem() //=> 'brown'
arr.randomItem() //=> 'quick'
```

--------------------------------

### Configure Package Details

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Updates the package.json file to register the n8n node, link credential and node files, and define package metadata such as version, license, and repository information.

```json
{
	"name": "n8n-nodes-nasapics",
	"version": "0.1.0",
	"description": "n8n node to call NASA's APOD and Mars Rover Photo services.",
	"keywords": [
		"n8n-community-node-package"
	],
	"license": "MIT",
	"homepage": "https://n8n.io",
	"author": {
		"name": "Test",
		"email": "test@example.com"
	},
	"repository": {
		"type": "git",
		"url": "git+<your-repo-url>"
	},
	"main": "index.js",
	"files": [
		"dist"
	],
	"n8n": {
		"n8nNodesApiVersion": 1,
		"credentials": [
			"dist/credentials/NasaPicsApi.credentials.js"
		],
		"nodes": [
		    "dist/nodes/NasaPics/NasaPics.node.js"
		]
	}
}
```

--------------------------------

### Constructing Human Review Approval Messages

Source: https://docs.n8n.io/advanced-ai/human-in-the-loop-tools

An example of using the $tool variable within an n8n expression to generate a descriptive message for a human reviewer. This includes the tool name and a formatted JSON string of the parameters the AI intends to use.

```n8n-expression
The AI wants to use {{ $tool.name }} with the following parameters:
{{ JSON.stringify($tool.parameters, null, 2) }}
```

--------------------------------

### Get Short Weekday Name

Source: https://docs.n8n.io/data/expression-reference/datetime

Returns the abbreviated textual name of the weekday (e.g., 'Wed'). It defaults to the system's locale if no locale has been explicitly set. This property is part of the Luxon library.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.weekdayShort //=> 'Sat'

// dt = "2024-03-30T18:49".toDateTime()
dt.setLocale('fr-FR').weekdayShort //=> 'sam.'
```

--------------------------------

### Get Full Month Name from DateTime - Luxon

Source: https://docs.n8n.io/data/expression-reference/datetime

Retrieves the full, textual name of the month (e.g., 'March') from a DateTime object. Defaults to the system's locale.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.monthLong //=> 'March'

// dt = "2024-03-30T18:49".toDateTime()
dt.setLocale('de-DE').monthLong //=> 'März'
```

--------------------------------

### Get Abbreviated Month Name from DateTime - Luxon

Source: https://docs.n8n.io/data/expression-reference/datetime

Returns the abbreviated, textual name of the month (e.g., 'Mar') from a DateTime object. Defaults to the system's locale.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.monthShort //=> 'Mar'

// dt = "2024-03-30T18:49".toDateTime()
dt.setLocale('de-DE').monthShort //=> 'Mär'
```

--------------------------------

### Execute complex JavaScript with IIFE in n8n

Source: https://docs.n8n.io/data/expressions-for-transformation

Shows how to perform multi-line JavaScript operations within an n8n expression by wrapping code in an Immediately Invoked Function Expression (IIFE). This example uses the Luxon library to calculate the difference between two dates in months.

```javascript
{{(()=>{
  let end = DateTime.fromISO('2017-03-13');
  let start = DateTime.fromISO('2017-02-13');
  let diffInMonths = end.diff(start, 'months');
  return diffInMonths.toObject();
})()}}
```

--------------------------------

### Create a Data Table

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.datatable/tables

Creates a new data table with specified columns and options.

```APIDOC
## POST /api/tables

### Description
Creates a new data table with specified columns and options.

### Method
POST

### Endpoint
/api/tables

### Parameters
#### Request Body
- **name** (string) - Required - The name for the data table.
- **columns** (array) - Required - An array of column definitions.
  - **name** (string) - Required - The name for the column.
  - **type** (string) - Required - The data type for the column (Boolean, Date, Number, String).
- **reuseExistingTables** (boolean) - Optional - Enable to return an existing table if one exists with the same name, without throwing an error.

### Request Example
```json
{
  "name": "MyDataTable",
  "columns": [
    {
      "name": "ID",
      "type": "Number"
    },
    {
      "name": "Name",
      "type": "String"
    }
  ],
  "reuseExistingTables": true
}
```

### Response
#### Success Response (200)
- **id** (string) - The ID of the created data table.
- **name** (string) - The name of the created data table.
- **columns** (array) - The columns of the created data table.

#### Response Example
```json
{
  "id": "table_123",
  "name": "MyDataTable",
  "columns": [
    {
      "name": "ID",
      "type": "Number"
    },
    {
      "name": "Name",
      "type": "String"
    }
  ]
}
```
```

--------------------------------

### Update n8n with Docker Compose

Source: https://docs.n8n.io/hosting/installation/docker

This sequence of commands updates n8n when managed by Docker Compose. It involves navigating to your compose file directory, pulling the latest image, stopping and removing the current services, and then starting them again with the updated image.

```bash
# Navigate to the directory containing your docker compose file
cd </path/to/your/compose/file/directory>

# Pull latest version
docker compose pull

# Stop and remove older version
docker compose down

# Start the container
docker compose up -d
```

--------------------------------

### Import entities via n8n CLI

Source: https://docs.n8n.io/hosting/cli-commands

Imports entities from a previous export into a database. Supports SQLite and Postgres, and allows for table truncation before import.

```bash
n8n import:entities --inputDir ./outputs --truncateTables true
```

--------------------------------

### Extract string fragments with slice()

Source: https://docs.n8n.io/data/expression-reference/string

Extracts a fragment of a string based on start and optional end positions. Supports negative indices to count from the end of the string.

```javascript
'Hello from n8n'.slice(0, 5);
'Hello from n8n'.slice(6);
'Hello from n8n'.slice(-3);
```

--------------------------------

### Configure Codex CLI for n8n MCP

Source: https://docs.n8n.io/advanced-ai/accessing-n8n-mcp-server

This configuration snippet adds the n8n MCP server to the Codex CLI configuration file. It uses npx to execute the supergateway and requires the n8n instance URL and a valid MCP token.

```toml
[mcp_servers.n8n_mcp]
command = "npx"
args = [
    "-y",
    "supergateway",
    "--streamableHttp",
    "https://<your-n8n-domain>/mcp-server/http",
    "--header",
    "authorization:Bearer <YOUR_N8N_MCP_TOKEN>"
]
```

--------------------------------

### Retrieve Recent Google Drive File using n8n

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive/common-issues

This workflow demonstrates how to get the most recent file from Google Drive. It uses a Google Drive node to search for files, a Sort node to order them by modification time in descending order, and a Limit node to select only the top result. Finally, another Google Drive node is used to access the identified file by its ID.

```json
{
  "name": "Get Recent Google Drive File",
  "nodes": [
    {
      "parameters": {
        "resource": "file",
        "operation": "search",
        "returnAll": true,
        "whatToSearch": "files",
        "options": {
          "fields": "all"
        }
      },
      "name": "Google Drive Search",
      "type": "n8n-nodes-base.googleDrive",
      "id": "node-1"
    },
    {
      "parameters": {
        "sortType": "simple",
        "fieldsToSortBy": [
          {
            "fieldName": "modifiedTime",
            "order": "descending"
          }
        ]
      },
      "name": "Sort by Modification Time",
      "type": "n8n-nodes-base.sort",
      "id": "node-2",
      "addEdge": [
        {
          "node": "node-1"
        }
      ]
    },
    {
      "parameters": {
        "maxItems": 1
      },
      "name": "Limit to 1",
      "type": "n8n-nodes-base.limit",
      "id": "node-3",
      "addEdge": [
        {
          "node": "node-2"
        }
      ]
    },
    {
      "parameters": {
        "resource": "file",
        "operation": "get",
        "fileSelection": {
          "mode": "byID",
          "expression": "{{ $json.id }}"
        }
      },
      "name": "Get Recent File",
      "type": "n8n-nodes-base.googleDrive",
      "id": "node-4",
      "addEdge": [
        {
          "node": "node-3"
        }
      ]
    }
  ],
  "connections": {
    "node-1": [
      {
        "node": "node-2",
        "type": "main",
        "index": 0
      }
    ],
    "node-2": [
      {
        "node": "node-3",
        "type": "main",
        "index": 0
      }
    ],
    "node-3": [
      {
        "node": "node-4",
        "type": "main",
        "index": 0
      }
    ]
  }
}
```

--------------------------------

### Get Absolute Value of a Number (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/number

Returns the absolute value of a number, effectively removing any negative sign. This is a custom n8n functionality for Number types.

```javascript
// x = -1.7
x.abs() //=> 1.7
```

--------------------------------

### Get DateTime Zone Information (Luxon)

Source: https://docs.n8n.io/data/expression-reference/datetime

Retrieves the time zone information associated with a DateTime object using the Luxon library. This property returns an object containing the zone name and validity status.

```javascript
$now.zone //=> {"zoneName": "Europe/Berlin", "valid": true}
```

--------------------------------

### Calculate Days to Christmas using JavaScript Code Node

Source: https://docs.n8n.io/data/specific-data-types/luxon

This JavaScript code snippet performs the same Christmas countdown calculation as the expression example. It uses Luxon's DateTime and diff methods within a JavaScript code node in n8n. The result is stored in a variable and formatted into a user-friendly string indicating the remaining days.

```javascript
let daysToChristmas = "There are " + $today.diff(DateTime.fromISO($today.year + '-12-25'), 'days').toObject().days.toString().substring(1) + " days to Christmas!";

console.log(daysToChristmas);
```

--------------------------------

### String indexOf() - Find first occurrence of substring

Source: https://docs.n8n.io/data/expression-reference/string

Returns the index of the first occurrence of a substring within a string. It is case-sensitive and returns -1 if the substring is not found. An optional start position can be specified.

```javascript
'steam'.indexOf('tea') //=> 1
'steam'.indexOf('i') //=> -1 
'STEAM'.indexOf('tea') //=> -1
'STEAM'.toLowerCase().indexOf('tea') //=> 1
```

--------------------------------

### Configure n8n environment variables using external files

Source: https://docs.n8n.io/hosting/configuration/configuration-methods

This snippet demonstrates how to map sensitive configuration fields to file paths. By appending _FILE to the variable name, n8n will read the value from the specified file path at runtime.

```shell
CREDENTIALS_OVERWRITE_DATA_FILE=/path/to/credentials_data
DB_TYPE_FILE=/path/to/db_type
DB_POSTGRESDB_DATABASE_FILE=/path/to/database_name
DB_POSTGRESDB_HOST_FILE=/path/to/database_host
DB_POSTGRESDB_PORT_FILE=/path/to/database_port
DB_POSTGRESDB_USER_FILE=/path/to/database_user
DB_POSTGRESDB_PASSWORD_FILE=/path/to/database_password
DB_POSTGRESDB_SCHEMA_FILE=/path/to/database_schema
DB_POSTGRESDB_SSL_CA_FILE=/path/to/ssl_ca
DB_POSTGRESDB_SSL_CERT_FILE=/path/to/ssl_cert
DB_POSTGRESDB_SSL_KEY_FILE=/path/to/ssl_key
DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED_FILE=/path/to/ssl_reject_unauth
```

--------------------------------

### Get Long Weekday Name

Source: https://docs.n8n.io/data/expression-reference/datetime

Returns the full textual name of the weekday (e.g., 'Wednesday'). It defaults to the system's locale if no locale has been explicitly set. This property is part of the Luxon library.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.weekdayLong //=> 'Saturday'

// dt = "2024-03-30T18:49".toDateTime()
dt.setLocale('de-DE').weekdayLong //=> 'Samstag'
```

--------------------------------

### String length - Get the number of characters

Source: https://docs.n8n.io/data/expression-reference/string

Retrieves the total number of characters within a string. This is a property that returns a numeric value representing the string's length.

```javascript
"hello".length //=> 5
```

--------------------------------

### Referencing Secrets in n8n Credentials

Source: https://docs.n8n.io/external-secrets

This example illustrates how to reference a secret stored in an external vault within an n8n credential field. It uses a specific expression format to access secrets by their vault and secret name.

```javascript
{{ $secrets.<vault-name>.<secret-name> }}
```

--------------------------------

### Get specific custom execution data

Source: https://docs.n8n.io/data/expression-reference/customdata

Retrieves a specific value associated with a key from the execution's custom data store. It returns a string value corresponding to the provided key.

```javascript
// Get the user's email (which was previously stored)
$execution.customData.get("user_email") //=> "me@example.com"
```

--------------------------------

### Generating SFTP Private Key (OpenSSH)

Source: https://docs.n8n.io/integrations/builtin/credentials/ftp

This code snippet demonstrates how to generate a private key in OpenSSH format using the `ssh-keygen` command. This is typically used for key-based authentication with SFTP servers. The `-o` parameter ensures the key is in OpenSSH format, `-a 100` specifies the number of KDF (Key Derivation Function) rounds for passphrase protection, and `-t ed25519` selects the Ed25519 algorithm.

```bash
ssh-keygen -o -a 100 -t ed25519
```

--------------------------------

### Create Nested Contact Data with Code Node (JavaScript)

Source: https://docs.n8n.io/courses/level-two/chapter-1

This example shows how to create a more complex data set of contacts using the n8n Code node. It defines an array of objects, with each object containing nested email properties (personal and work).

```javascript
var myContacts = [
	{
		json: {
			name: 'Alice',
			email: {
				personal: 'alice@home.com',
				work: 'alice@wonderland.org'
			},
		}
	},
	{
		json: {
			name: 'Bob',
			email: {
				personal: 'bob@mail.com',
				work: 'contact@thebuilder.com'
				},
		}
	},
];

return myContacts;
```

--------------------------------

### Get Item Index with $itemIndex

Source: https://docs.n8n.io/data/expression-reference/root

Returns the position of the item currently being processed within the list of input items. This function returns a Number and is part of n8n's custom functionality.

```javascript
function getItemIndex() {
  // Example usage: get the index of the current item
  return $itemIndex;
}
```

--------------------------------

### Manage users and authentication via n8n CLI

Source: https://docs.n8n.io/hosting/cli-commands

Provides utilities to reset user management, disable Multi-Factor Authentication (MFA) for specific users, and reset LDAP configurations.

```bash
n8n user-management:reset
n8n mfa:disable --email=johndoe@example.com
n8n ldap:reset
```

--------------------------------

### Slice Array Portions

Source: https://docs.n8n.io/data/expression-reference/array

Returns a shallow copy of a portion of an array into a new array object selected from start to end. Supports negative indexing to count from the end of the array.

```JavaScript
// arr = [1, 2, 3, 4, 5]
arr.slice(2, 4) //=> [3, 4]
arr.slice(2) //=> [3, 4, 5]
arr.slice(-2) //=> [4, 5]
```

--------------------------------

### Build and Link Custom Node Package

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Commands to compile the node package and create a symbolic link in the local development environment. This allows n8n to recognize the local node package during development.

```bash
npm run build
npm link
```

--------------------------------

### Get Minimum Value in Array (n8n)

Source: https://docs.n8n.io/data/expression-reference/array

The `min()` method returns the smallest number in the array. This is a custom n8n functionality and throws an error if the array contains non-numeric values.

```javascript
// arr = [12, 1, 5]
arr.min() //=> 1
```

--------------------------------

### Fetch Workflow Data to Import

Source: https://docs.n8n.io/workflows/templates

Retrieves the full workflow data for a specific template, intended for importing onto the canvas.

```APIDOC
## GET /workflows/templates/<id>

### Description
Fetches workflow data to import onto the canvas.

### Method
GET

### Endpoint
`/workflows/templates/<id>`

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the template.

### Response
#### Success Response (200)
- **workflow** (object) - The complete workflow definition.
  - **nodes** (array) - An array of workflow nodes.
  - **connections** (array) - An array of connections between nodes.
  - **settings** (object) - Workflow settings.

#### Response Example
```json
{
  "name": "Imported Workflow",
  "nodes": [
    {
      "id": "1",
      "type": "trigger",
      "name": "Manual Trigger"
    }
  ],
  "connections": [],
  "settings": {}
}
```
```

--------------------------------

### Update Docker container permissions for n8n v1.0

Source: https://docs.n8n.io/1-0-migration-checklist

This command updates the file ownership of the n8n data directory to the 'node' user, which is required after the security update that changed the default container user from root to node.

```bash
docker run --rm -it --user root -v ~/.n8n:/home/node/.n8n --entrypoint chown n8nio/base:16 -R node:node /home/node/.n8n
```

--------------------------------

### Apply Kubernetes Manifests

Source: https://docs.n8n.io/hosting/installation/server-setups/azure

Applies all Kubernetes deployment and service manifests to the cluster. This command is used to create the n8n and PostgreSQL resources. If a namespace error occurs, apply the namespace manifest first.

```bash
kubectl apply -f .

# Or to apply namespace first:
kubectl apply -f namespace.yaml
```

--------------------------------

### Deploy n8n to Cloud Run

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

Deploys the n8n container image to Cloud Run with environment variables, secret mappings, and Cloud SQL connectivity.

```bash
gcloud run deploy n8n \
    --image=n8nio/n8n:latest \
    --command="/bin/sh" \
    --args="-c,sleep 5;n8n start" \
    --region=$REGION \
    --allow-unauthenticated \
    --port=5678 \
    --memory=2Gi \
    --no-cpu-throttling \
    --set-env-vars="N8N_PORT=5678,N8N_PROTOCOL=https,N8N_ENDPOINT_HEALTH=health,DB_TYPE=postgresdb,DB_POSTGRESDB_DATABASE=n8n,DB_POSTGRESDB_USER=n8n-user,DB_POSTGRESDB_HOST=/cloudsql/$PROJECT_ID:$REGION:n8n-db,DB_POSTGRESDB_PORT=5432,DB_POSTGRESDB_SCHEMA=public,GENERIC_TIMEZONE=UTC,QUEUE_HEALTH_CHECK_ACTIVE=true" \
    --set-secrets="DB_POSTGRESDB_PASSWORD=n8n-db-password:latest,N8N_ENCRYPTION_KEY=n8n-encryption-key:latest" \
    --add-cloudsql-instances=$PROJECT_ID:$REGION:n8n-db \
    --service-account=n8n-service-account@$PROJECT_ID.iam.gserviceaccount.com
```

--------------------------------

### Get Maximum Value in Array (n8n)

Source: https://docs.n8n.io/data/expression-reference/array

The `max()` method returns the largest number in the array. This is a custom n8n functionality and throws an error if the array contains non-numeric values.

```javascript
// arr = [1, 12, 5]
arr.max() //=> 12
```

--------------------------------

### Respect Time Parameter in Wise Node Exchange Rate

Source: https://docs.n8n.io/release-notes/0-x

The Wise node now respects the time parameter when fetching exchange rates using 'get: exchangeRate'. This allows for more precise retrieval of historical exchange rate data.

```javascript
Wise node: respect the time parameter on `get: exchangeRate`.
```

--------------------------------

### Extract URL from String - JavaScript

Source: https://docs.n8n.io/data/expression-reference/string

Extracts the first full URL (starting with http) found in a string. Returns undefined if no URL is detected. This function is part of n8n's custom string utilities.

```javascript
"Check out http://n8n.io".extractUrl() //=> 'http://n8n.io'
```

--------------------------------

### Implement dynamic hint in n8n programmatic node

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

This code demonstrates how to return a NodeExecutionOutput object containing a dynamic message. It checks for specific conditions, such as multiple items and execution settings, before providing feedback to the user in the output pane.

```TypeScript
if (operation === 'select' && items.length > 1 && !node.executeOnce) {
    // Expects two parameters: NodeExecutionData and an array of hints
	return new NodeExecutionOutput(
		[returnData],
		[
			{
				message: `This node ran ${items.length} times, once for each input item. To run for the first item only, enable <b>Execute once</b> in the node settings.`,
				location: 'outputPane',
			},
		],
	);
}
return [returnData];
```

--------------------------------

### Fetch Workflow JSON via API

Source: https://docs.n8n.io/embed/managing-workflows

This snippet shows how to fetch the JSON data of a specific workflow using the n8n REST API. It requires the n8n domain and the workflow ID. The GET request returns the complete workflow structure.

```http
GET https://<n8n-domain>/rest/workflows/1012
```

--------------------------------

### Extract Part of a DateTime

Source: https://docs.n8n.io/data/expression-reference/datetime

Extracts a specific part of a DateTime object, such as the month, day, or hour, as a number. This method is useful for getting individual components of a date or time. For textual representations, use the `format()` method.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.extract('month') //=> 3
```

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.extract('hour') //=> 18
```

--------------------------------

### Configure Secret Manager for Sensitive Data

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

Stores database credentials and encryption keys securely in Google Secret Manager.

```bash
gcloud secrets create n8n-db-password \
    --data-file=/your/password/file \
    --replication-policy="automatic"

openssl rand -base64 -out my-encryption-key 42

gcloud secrets create n8n-encryption-key \
    --data-file=my-encryption-key \
    --replication-policy="automatic"
```

--------------------------------

### Increment Page Number for Pagination in HTTP Request

Source: https://docs.n8n.io/code/cookbook/http-node/pagination

Set up the HTTP Request node to paginate by incrementing a query parameter that specifies the page number. This method is suitable for APIs that allow direct access to pages via a numbered parameter. The '$pageCount' variable is used to dynamically increase the page number for each subsequent request, starting from page one.

```javascript
{{ $pageCount + 1 }}
```

--------------------------------

### Get Binary Data Buffer in n8n (JavaScript)

Source: https://docs.n8n.io/code/cookbook/code-node/get-binary-data-buffer

Retrieves the binary data buffer for a specific item and property name. This function is essential for performing operations on binary data within n8n workflows. It takes an item index and the binary property name as input and returns the binary data buffer. Note: This function is not available when using Python.

```javascript
/* 
* itemIndex: number. The index of the item in the input data.
* binaryPropertyName: string. The name of the binary property. 
* The default in the Read/Write File From Disk node is 'data'. 
*/
let binaryDataBufferItem = await this.helpers.getBinaryDataBuffer(itemIndex, binaryPropertyName);
```

```javascript
let binaryDataBufferItem = await this.helpers.getBinaryDataBuffer(0, 'data');
// Returns the data in the binary buffer for the first input item
```

--------------------------------

### Implement manual item linking in n8n nodes

Source: https://docs.n8n.io/data/data-mapping/data-item-linking/item-linking-node-building

Demonstrates how to define the 'pairedItem' property when returning items from a programmatic node. This allows developers to either pass through existing item lineage or manually assign an index to maintain data context.

```JavaScript
// Use the pairedItem information of the incoming item
newItem = {
	"json": { . . . },
	"pairedItem": {
		"item": item.pairedItem,
		// Optional: choose the input to use
		// Set this if your node combines multiple inputs
		"input": 0
	}
};

// Or set the index manually
newItem = {
	"json": { . . . },
	"pairedItem": {
		"item": i,
		// Optional: choose the input to use
		// Set this if your node combines multiple inputs
		"input": 0
	}
};
```

--------------------------------

### Dynamically Populate SQL IN Groups with Parameters in Postgres

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.postgres/common-issues

Demonstrates how to use n8n expressions and query parameters to dynamically populate SQL `IN` groups. This method sanitizes input and automatically creates the correct number of prepared statement placeholders.

```sql
SELECT color, shirt_size FROM shirts WHERE shirt_size IN ('small', 'medium', 'large');
```

```sql
SELECT color, shirt_size FROM shirts WHERE shirt_size IN ();
```

```sql
SELECT color, shirt_size FROM shirts WHERE shirt_size IN ({{ $json.input_shirt_sizes.map((i, pos) => "$" + (pos+1)).join(', ') }});
```

--------------------------------

### Configure AI Agent Node in n8n

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/ask_a_human.json

This node configures an AI agent, likely for natural language processing tasks. It includes options for system messages that guide the AI's behavior, such as answering questions or using specific tools when unsure.

```json
{
  "options": {
    "systemMessage": "Try to answer the user's question. When you can't answer, or you're not confident of the answer, use the appropriate tool. When you use the dont_know_tool, respond with the message from the tool."
  }
}
```

--------------------------------

### Configure Cron Expression for Gmail Trigger

Source: https://docs.n8n.io/integrations/builtin/trigger-nodes/n8n-nodes-base.gmailtrigger/poll-mode-options

Examples of Cron expressions used to schedule the Gmail Trigger node. These expressions define specific execution times based on seconds, minutes, hours, days, months, and weekdays.

```Cron
30 8 4 * * *
```

```Cron
8 4 * * *
```

--------------------------------

### Get End of Unit for DateTime

Source: https://docs.n8n.io/data/expression-reference/datetime

Rounds a DateTime object up to the end of a specified unit (e.g., end of the month, end of the year). It accepts units like 'year', 'month', 'day', and optional options for locale-specific week calculations.

```javascript
// dt = "2024-03-20T18:49".toDateTime()
dt.endOf('month') //=> 2024-03-31T23:59
```

--------------------------------

### Clone and Navigate n8n Hosting Configuration

Source: https://docs.n8n.io/hosting/installation/server-setups/azure

Commands to download the official n8n Kubernetes configuration repository and enter the directory containing the manifest files.

```bash
git clone https://github.com/n8n-io/n8n-hosting.git
cd n8n-hosting/kubernetes
```

--------------------------------

### API Endpoints Overview

Source: https://docs.n8n.io/workflows/templates

Provides links to interactively explore n8n's API endpoints.

```APIDOC
## API Endpoints Overview

### Description
Explore n8n's API endpoints interactively.

### Available Endpoints
- **Categories**: https://api.n8n.io/templates/categories
- **Collections**: https://api.n8n.io/templates/collections
- **Search**: https://api.n8n.io/templates/search
- **Health Check**: https://api.n8n.io/health
```

--------------------------------

### Transform Specific Field Array (JavaScript)

Source: https://docs.n8n.io/courses/level-two/chapter-1

Processes an array within a specific field of the input item, creating a new item for each element in that array. This example targets the 'workEmail' field, assuming it contains an array of email objects. It allows targeted data manipulation without affecting other fields.

```javascript
let items = $input.all();
return items[0].json.workEmail.map(item => {
	return {
		json: item
	}
});
```

--------------------------------

### Create New List of Names with Python Code Node

Source: https://docs.n8n.io/data/specific-data-types/jmespath

This Python code snippet for an n8n Code node uses the `_jmespath` function to extract first and last names from the 'people' array, similar to the JavaScript example. It returns the transformed data in a dictionary under the key 'newList'. Ensure the input JSON has a 'people' array for this to work correctly.

```python
newList = _jmespath(_json.body.people, "[].[first, last]")
return {"newList":newList}
"""
Returns:
[
	{
		"newList": [
			[
				"James",
				"Green"
			],
			[
				"Jacob",
				"Jones"
			],
			[
				"Jayden",
				"Smith"
			]
		]
	}
]"""
```

--------------------------------

### Configure Allowed Packages in n8n-task-runners.json

Source: https://docs.n8n.io/hosting/configuration/task-runners

This JSON configuration file specifies environment variables for the task runners, allowing you to control which external packages and built-in modules can be used by the Code node. It includes settings for both JavaScript and Python runners, defining comma-separated lists for allowed Node.js built-ins, third-party JS packages, Python standard library modules, and third-party Python packages.

```json
{
  "task-runners": [
    {
      "runner-type": "javascript",
      "env-overrides": {
        "NODE_FUNCTION_ALLOW_BUILTIN": "crypto",         // <-- allowlist Node.js builtin modules here
        "NODE_FUNCTION_ALLOW_EXTERNAL": "moment,uuid",   // <-- allowlist third-party JS packages here
      }
    },
    {
      "runner-type": "python",
      "env-overrides": {
        "PYTHONPATH": "/opt/runners/task-runner-python",
        "N8N_RUNNERS_STDLIB_ALLOW": "json",              // <-- allowlist Python standard library packages here
        "N8N_RUNNERS_EXTERNAL_ALLOW": "numpy,pandas"     // <-- allowlist third-party Python packages here
      }
    }
  ]
}
```

--------------------------------

### Request Next Page of Workflows with Cursor (cURL)

Source: https://docs.n8n.io/api/pagination

This cURL command demonstrates how to fetch the next page of active workflows by appending the 'cursor' parameter obtained from a previous response. This allows for sequential retrieval of paginated data. It's applicable to both self-hosted and n8n Cloud environments.

```shell
# For a self-hosted n8n instance
curl -X 'GET' \
  '<N8N_HOST>:<N8N_PORT>/<N8N_PATH>/api/v<version-number>/workflows?active=true&limit=150&cursor=MTIzZTQ1NjctZTg5Yi0xMmQzLWE0NTYtNDI2NjE0MTc0MDA' \
  -H 'accept: application/json'
```

--------------------------------

### Build Custom n8nio/runners Docker Image

Source: https://docs.n8n.io/hosting/configuration/task-runners

This command builds a custom Docker image for the n8n runners using `docker buildx`. It specifies the Dockerfile to use (`docker/images/runners/Dockerfile`) and tags the resulting image as `n8nio/runners:custom`. This command should be executed from the root of the n8n repository.

```bash
docker buildx build \
  -f docker/images/runners/Dockerfile \
  -t n8nio/runners:custom \
  .
```

--------------------------------

### n8n Workflow Configuration (JSON)

Source: https://docs.n8n.io/_workflows//advanced-ai/tutorials/chat_complete.json

The complete n8n workflow configuration in JSON format. This defines the nodes, their parameters, connections, and settings for an AI tutorial.

```json
{
    "name": "AI tutorial",
    "nodes": [
      {
        "parameters": {
          "options": {}
        },
        "type": "@n8n/n8n-nodes-langchain.chatTrigger",
        "typeVersion": 1.1,
        "position": [
          -300,
          -40
        ],
        "id": "a2d42e1f-36df-4a6a-a3b4-99a162074d11",
        "name": "When chat message received",
        "webhookId": "97c1a41f-8ef0-4d63-a924-92eb634384d3"
      },
      {
        "parameters": {
          "options": {}
        },
        "type": "@n8n/n8n-nodes-langchain.agent",
        "typeVersion": 1.7,
        "position": [
          -80,
          -40
        ],
        "id": "0f61a10f-668f-42f7-b835-cf3efb60082a",
        "name": "AI Agent"
      },
      {
        "parameters": {
          "model": {
            "__rl": true,
            "mode": "list",
            "value": "gpt-4o-mini"
          },
          "options": {}
        },
        "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
        "typeVersion": 1.2,
        "position": [
          -100,
          160
        ],
        "id": "b8129c6d-f201-4378-8f66-ce9a6cfd5f3b",
        "name": "OpenAI Chat Model",
        "credentials": {
          "openAiApi": {
            "id": "jiPPcYV9I70iKapN",
            "name": "OpenAi account 37"
          }
        }
      },
      {
        "parameters": {},
        "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
        "typeVersion": 1.3,
        "position": [
          20,
          180
        ],
        "id": "afbab05c-1e87-4f7a-9d66-c86f9db1ec64",
        "name": "Simple Memory"
      }
    ],
    "pinData": {},
    "connections": {
      "When chat message received": {
        "main": [
          [
            {
              "node": "AI Agent",
              "type": "main",
              "index": 0
            }
          ]
        ]
      },
      "OpenAI Chat Model": {
        "ai_languageModel": [
          [
            {
              "node": "AI Agent",
              "type": "ai_languageModel",
              "index": 0
            }
          ]
        ]
      },
      "Simple Memory": {
        "ai_memory": [
          [
            {
              "node": "AI Agent",
              "type": "ai_memory",
              "index": 0
            }
          ]
        ]
      }
    },
    "active": false,
    "settings": {
      "executionOrder": "v1"
    },
    "versionId": "b1641385-c6b0-48a8-8e26-20d1f6bd7fda",
    "meta": {
      "templateCredsSetupCompleted": true,
      "instanceId": "cb484ba7b742928a2048bf8829668bed5b5ad9787579adea888f05980292a4a7"
    },
    "id": "l05TkWXXYbOiuL4o",
    "tags": []
  }
```

--------------------------------

### POST /files

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive/file-operations

Uploads a new file to a specific folder or drive in Google Drive.

```APIDOC
## POST /files

### Description
Uploads a new file to Google Drive, allowing specification of parent folders or drives.

### Method
POST

### Endpoint
/files

### Parameters
#### Request Body
- **name** (string) - Required - The name to use for the new file.
- **binaryData** (binary) - Required - The binary content of the file.
- **parentId** (string) - Optional - The ID of the parent folder or drive.
- **ocrLanguage** (string) - Optional - ISO 639-1 language code for OCR processing.

### Request Example
{
  "name": "new_upload.txt",
  "parentId": "folder_id_123",
  "ocrLanguage": "en"
}

### Response
#### Success Response (200)
- **id** (string) - The ID of the newly created file.
- **name** (string) - The name of the created file.

#### Response Example
{
  "id": "2def456...",
  "name": "new_upload.txt"
}
```

--------------------------------

### Edit Docker Compose Configuration

Source: https://docs.n8n.io/hosting/installation/server-setups/digital-ocean

Opens the docker-compose.yml file for viewing or modification using the nano text editor.

```bash
nano docker-compose.yml
```

--------------------------------

### Configure n8n and Traefik with Docker Compose

Source: https://docs.n8n.io/hosting/installation/server-setups/docker-compose

This Docker Compose configuration defines services for n8n and Traefik. Traefik handles SSL certificates and routing, while n8n is configured with environment variables and volume mounts for data persistence and local file access. It relies on environment variables like SUBDOMAIN, DOMAIN_NAME, and GENERIC_TIMEZONE for customization.

```yaml
services:
  traefik:
    image: "traefik"
    restart: always
    command:
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entrypoints.web.address=:80"
      - "--entrypoints.web.http.redirections.entryPoint.to=websecure"
      - "--entrypoints.web.http.redirections.entrypoint.scheme=https"
      - "--entrypoints.websecure.address=:443"
      - "--certificatesresolvers.mytlschallenge.acme.tlschallenge=true"
      - "--certificatesresolvers.mytlschallenge.acme.email=${SSL_EMAIL}"
      - "--certificatesresolvers.mytlschallenge.acme.storage=/letsencrypt/acme.json"
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - traefik_data:/letsencrypt
      - /var/run/docker.sock:/var/run/docker.sock:ro

  n8n:
    image: docker.n8n.io/n8nio/n8n
    restart: always
    ports:
      - "127.0.0.1:5678:5678"
    labels:
      - traefik.enable=true
      - traefik.http.routers.n8n.rule=Host(`${SUBDOMAIN}.${DOMAIN_NAME}`)
      - traefik.http.routers.n8n.tls=true
      - traefik.http.routers.n8n.entrypoints=web,websecure
      - traefik.http.routers.n8n.tls.certresolver=mytlschallenge
      - traefik.http.middlewares.n8n.headers.SSLRedirect=true
      - traefik.http.middlewares.n8n.headers.STSSeconds=315360000
      - traefik.http.middlewares.n8n.headers.browserXSSFilter=true
      - traefik.http.middlewares.n8n.headers.contentTypeNosniff=true
      - traefik.http.middlewares.n8n.headers.forceSTSHeader=true
      - traefik.http.middlewares.n8n.headers.SSLHost=${DOMAIN_NAME}
      - traefik.http.middlewares.n8n.headers.STSIncludeSubdomains=true
      - traefik.http.middlewares.n8n.headers.STSPreload=true
      - traefik.http.routers.n8n.middlewares=n8n@docker
    environment:
      - N8N_ENFORCE_SETTINGS_FILE_PERMISSIONS=true
      - N8N_HOST=${SUBDOMAIN}.${DOMAIN_NAME}
      - N8N_PORT=5678
      - N8N_PROTOCOL=https
      - N8N_RUNNERS_ENABLED=true
      - NODE_ENV=production
      - WEBHOOK_URL=https://${SUBDOMAIN}.${DOMAIN_NAME}/
      - GENERIC_TIMEZONE=${GENERIC_TIMEZONE}
      - TZ=${GENERIC_TIMEZONE}
    volumes:
      - n8n_data:/home/node/.n8n
      - ./local-files:/files

volumes:
  n8n_data:
  traefik_data:
```

--------------------------------

### Use Large Language Models with $fromAI()

Source: https://docs.n8n.io/data/expression-reference/root

Integrates large language models to provide values for node parameters. It supports specifying a key, description, type, and default value for better results. Returns any type.

```javascript
// Ask the model to provide a name, and use it here
$fromAI('name')
```

```javascript
// Ask the model to provide the age of the person (as a number with a default value of 18), and use it here
$fromAI('age', 'The age of the person', 'number', 18)
```

```javascript
// Ask the model to provide a boolean signifying whether the person is a student (with default value false), and use it here
$fromAI('isStudent', 'Is the person a student', 'boolean', false)
```

--------------------------------

### Answer Query

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/callback-operations

Sends answers to callback queries initiated from inline keyboards using the Bot API's answerCallbackQuery method.

```APIDOC
## POST /api/telegram/answerCallbackQuery

### Description
Sends answers to callback queries from inline keyboards.

### Method
POST

### Endpoint
/api/telegram/answerCallbackQuery

### Parameters
#### Request Body
- **credential** (string) - Required - Credential to connect with Telegram.
- **resource** (string) - Required - Must be 'Callback'.
- **operation** (string) - Required - Must be 'Answer Query'.
- **queryId** (string) - Required - The unique identifier of the query to answer.
- **results** (string) - Required - A JSON-serialized array of results for the query.
- **cacheTime** (integer) - Optional - Maximum time in seconds the client can cache the result. Defaults to 0.
- **showAlert** (boolean) - Optional - Whether to display the answer as an alert. Defaults to false.
- **text** (string) - Optional - Up to 200 characters of text to display with the answer.
- **url** (string) - Optional - A URL to be opened by the user's client.

### Request Example
```json
{
  "credential": "your_telegram_credential",
  "resource": "Callback",
  "operation": "Answer Query",
  "queryId": "query_12345",
  "results": "[\"result1\", \"result2\"]",
  "cacheTime": 300,
  "showAlert": true,
  "text": "This is an important update!",
  "url": "https://example.com"
}
```

### Response
#### Success Response (200)
- **status** (string) - Indicates the success of the operation.

#### Response Example
```json
{
  "status": "success"
}
```
```

--------------------------------

### Set Webhook URL Environment Variable

Source: https://docs.n8n.io/integrations/builtin/credentials/getresponse

This command sets the WEBHOOK_URL environment variable to the ngrok URL obtained in the previous step. This variable is used by applications to direct webhooks to the locally running server.

```bash
export WEBHOOK_URL=<YOUR-NGROK-URL>
```

--------------------------------

### Check string prefixes with startsWith()

Source: https://docs.n8n.io/data/expression-reference/string

Determines whether a string begins with the characters of a specified string. This method is case-sensitive.

```javascript
'team'.startsWith('tea');
'team'.startsWith('Tea');
'Team'.toLowerCase().startsWith('tea');
```

--------------------------------

### Mount Custom Launcher Config in Runners Container

Source: https://docs.n8n.io/hosting/configuration/task-runners

This snippet demonstrates how to mount a custom launcher configuration file into the runners container. This allows for modifications to the default configuration, such as allowlisting modules. The custom configuration file should be placed at `/etc/task-runners.json` within the container.

```dockerfile
path/to/n8n-task-runners.json:/etc/n8n-task-runners.json
```

--------------------------------

### Update an Assistant

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/assistant-operations

Update the details of an existing assistant. This includes modifying its description, instructions, tools, model, and other configuration options.

```APIDOC
## Update an Assistant

### Description
Use this operation to update the details of an existing assistant.

### Method
POST

### Endpoint
/assistants/{assistant_id}

### Parameters
#### Path Parameters
- **assistant_id** (string) - Required - The ID of the assistant to update.

#### Query Parameters
None

#### Request Body
- **credential** (object) - Required - Credential to connect with OpenAI.
  - **resource** (string) - Required - Must be 'Assistant'.
  - **operation** (string) - Required - Must be 'Update an Assistant'.
  - **assistant** (string) - Required - The assistant you want to update.

### Options
- **Code Interpreter** (boolean) - Optional - Enable code interpreter for the assistant.
- **Description** (string) - Optional - Description of the assistant (max 512 characters).
- **Instructions** (string) - Optional - System instructions for the assistant (max 32,768 characters).
- **Knowledge Retrieval** (boolean) - Optional - Enable knowledge retrieval for the assistant.
- **Files** (array) - Optional - Select files to upload for external knowledge source.
- **Model** (string) - Optional - The model the assistant will use (e.g., `gpt-4o`, `gpt-4o-mini`).
- **Name** (string) - Optional - The name of the assistant (max 256 characters).
- **Remove All Custom Tools (Functions)** (boolean) - Optional - Turn on to remove all custom tools.
- **Output Randomness (Temperature)** (number) - Optional - Adjust randomness of the response (0.0 to 1.0). Defaults to 1.0.
- **Output Randomness (Top P)** (number) - Optional - Adjust Top P setting to control diversity (0.0 to 1.0). Defaults to 1.0.

### Request Example
```json
{
  "credential": {
    "resource": "Assistant",
    "operation": "Update an Assistant",
    "assistant": "asst_abc123"
  },
  "options": {
    "name": "My Updated Assistant",
    "description": "An assistant that helps with coding tasks.",
    "model": "gpt-4o",
    "codeInterpreter": true,
    "knowledgeRetrieval": true,
    "outputRandomnessTemperature": 0.7
  }
}
```

### Response
#### Success Response (200)
- **id** (string) - The ID of the updated assistant.
- **name** (string) - The name of the assistant.
- **description** (string) - The description of the assistant.
- **model** (string) - The model used by the assistant.

#### Response Example
```json
{
  "id": "asst_abc123",
  "name": "My Updated Assistant",
  "description": "An assistant that helps with coding tasks.",
  "model": "gpt-4o",
  "instructions": "You are a helpful assistant.",
  "tools": [
    {"type": "code_interpreter"},
    {"type": "retrieval"}
  ],
  "created_at": 1677652220,
  "updated_at": 1677652220,
  "temperature": 0.7,
  "top_p": 1.0,
  "code_interpreter": {
    "enabled": true
  },
  "retrieval": {
    "enabled": true
  }
}
```
```

--------------------------------

### Configure Node Description Metadata

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

Defines the display properties for the n8n node, such as display name, icon, and input/output connections.

```typescript
displayName: 'FriendGrid',
name: 'friendGrid',
icon: 'file:friendGrid.svg',
group: ['transform'],
version: 1,
description: 'Consume SendGrid API',
defaults: {
	name: 'FriendGrid',
},
inputs: [NodeConnectionTypes.Main],
outputs: [NodeConnectionTypes.Main],
usableAsTool: true,
credentials: [
	{
		name: 'friendGridApi',
		required: true,
	},
],
```

--------------------------------

### Workflow Endpoint Response Schemas (JSON)

Source: https://docs.n8n.io/embed/workflow-templates

Compares the JSON response structures for two n8n.io workflow endpoints: `/templates/workflows/{id}` (wrapped) and `/workflows/templates/{id}` (flat). The wrapped response includes a top-level 'workflow' key, while the flat response directly provides the workflow definition.

```json
{
  "workflow": {
    "id": 123,
    "name": "...",
    "totalViews": 1000,
    "workflow": {    // actual workflow definition
      "nodes": [...],
      "connections": {}
    }
  }
}
```

```json
{
  "id": 123,
  "name": "...",
  "workflow": {      // actual workflow definition
    "nodes": [...],
    "connections": {}
  }
}
```

--------------------------------

### Handle Empty Values with $ifEmpty()

Source: https://docs.n8n.io/data/expression-reference/root

Returns the first parameter if it's not empty, otherwise returns the second parameter. Empty values include "", [], {}, null, and undefined. Returns any type.

```javascript
"Hi " + $ifEmpty(name, "there") // e.g. "Hi Nathan" or "Hi there"
```

--------------------------------

### Manage n8n license via CLI

Source: https://docs.n8n.io/hosting/cli-commands

Commands to clear the current license or display information about the active license. Clearing the license resets n8n to default features.

```bash
n8n license:clear
n8n license:info
```

--------------------------------

### Connect Claude Code to n8n MCP

Source: https://docs.n8n.io/advanced-ai/accessing-n8n-mcp-server

Methods to connect Claude Code to an n8n instance, either via CLI command or by updating the claude.json configuration file.

```bash
claude mcp add --transport http n8n-mcp https://<your-n8n-domain>/mcp-server/http \
  --header "Authorization: Bearer <YOUR_N8N_MCP_TOKEN>"
```

```json
{
    "mcpServers": {
        "n8n-local": {
            "type": "http",
            "url": "https://<your-n8n-domain>/mcp-server/http",
            "headers": {
                "Authorization": "Bearer <YOUR_N8N_MCP_TOKEN>"
            }
        }
    }
}
```

--------------------------------

### Define API Operations and Routing

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Defines specific operations for resources, including HTTP request routing and conditional UI display logic. It demonstrates how to use 'displayOptions' to show fields based on the selected resource and how to construct dynamic URLs using expressions.

```TypeScript
{
	displayName: 'Operation',
	name: 'operation',
	type: 'options',
	noDataExpression: true,
	displayOptions: {
		show: {
			resource: ['astronomyPictureOfTheDay'],
		},
	},
	options: [
		{
			name: 'Get',
			value: 'get',
			action: 'Get the APOD',
			description: 'Get the Astronomy Picture of the day',
			routing: {
				request: {
					method: 'GET',
					url: '/planetary/apod',
				},
			},
		},
	],
	default: 'get',
},
{
	displayName: 'Rover name',
	description: 'Choose which Mars Rover to get a photo from',
	required: true,
	name: 'roverName',
	type: 'options',
	options: [
		{name: 'Curiosity', value: 'curiosity'},
		{name: 'Opportunity', value: 'opportunity'},
		{name: 'Perseverance', value: 'perseverance'},
		{name: 'Spirit', value: 'spirit'},
	],
	routing: {
		request: {
			url: '=/mars-photos/api/v1/rovers/{{$value}}/photos',
		},
	},
	default: 'curiosity',
	displayOptions: {
		show: {
			resource: ['marsRoverPhotos'],
		},
	},
}
```

--------------------------------

### List All Template Categories

Source: https://docs.n8n.io/workflows/templates

Retrieves a list of all available categories for workflow templates.

```APIDOC
## GET /templates/categories

### Description
Lists all template categories.

### Method
GET

### Endpoint
`/templates/categories`

### Response
#### Success Response (200)
- **categories** (array) - A list of available template categories.
  - **id** (string) - The category ID.
  - **name** (string) - The name of the category.

#### Response Example
```json
{
  "categories": [
    {
      "id": "data",
      "name": "Data Processing"
    },
    {
      "id": "automation",
      "name": "Automation"
    }
  ]
}
```
```

--------------------------------

### Enable Google Workspace APIs using gcloud

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

This snippet demonstrates how to enable various Google Workspace APIs required for n8n integration. Ensure you enable the specific APIs for the services you intend to use, such as Gmail, Drive, Sheets, Docs, and Calendar. Note that enabling Drive API is not sufficient for Sheets and Docs; their respective APIs must also be enabled.

```bash
gcloud services enable gmail.googleapis.com
gcloud services enable drive.googleapis.com
gcloud services enable sheets.googleapis.com
gcloud services enable docs.googleapis.com
gcloud services enable calendar-json.googleapis.com
```

--------------------------------

### Simulate Node Output with Array of Objects (JavaScript)

Source: https://docs.n8n.io/courses/level-two/chapter-1

Demonstrates how to create a basic data set in the n8n Code node. It returns an array containing a single object, where the object has a 'json' key. This structure is expected by n8n for data items.

```javascript
return [
	{
		json: {
			apple: 'beets',
		}
	}
];
```

--------------------------------

### Define Node Hints in n8n.io

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

This snippet demonstrates how to define hints within a node's description in n8n.io. Hints provide contextual information to users, such as warnings about many input items or specific operation conditions. They can include customizable messages, types, display locations, and conditions for when to show them.

```typescript
description: INodeTypeDescription = {
	...
	hints: [
		{
			// The hint message. You can use HTML.
			message: "This node has many input items. Consider enabling <b>Execute Once</b> in the node\'s settings.",
			// Choose from: info, warning, danger. The default is 'info'.
			// Changes the color. info (grey), warning (yellow), danger (red)
			type: 'info',
			// Choose from: inputPane, outputPane, ndv. By default n8n displays the hint in both the input and output panels.
			location: 'outputPane',
			// Choose from: always, beforeExecution, afterExecution. The default is 'always'
			whenToDisplay: 'beforeExecution',
			// Optional. An expression. If it resolves to true, n8n displays the message. Defaults to true.
			displayCondition: '={{ $parameter["operation"] === "select" && $input.all().length > 1 }}'
		}
	]
	...
}
```

--------------------------------

### Search Workflow Templates

Source: https://docs.n8n.io/workflows/templates

Searches for workflow templates based on provided query parameters.

```APIDOC
## GET /templates/search

### Description
Searches for workflow templates.

### Method
GET

### Endpoint
`/templates/search`

### Parameters
#### Query Parameters
- **page** (integer) - Optional - The page of results to return.
- **rows** (integer) - Optional - The maximum number of results to return per page.
- **category** (string) - Optional - A comma-separated list of categories to search within.
- **search** (string) - Optional - The search query string.

### Response
#### Success Response (200)
- **templates** (array) - A list of matching workflow templates.
  - **id** (string) - The template ID.
  - **name** (string) - The template name.
  - **description** (string) - A brief description of the template.
  - **categories** (array) - A list of categories the template belongs to.

#### Response Example
```json
{
  "templates": [
    {
      "id": "workflow-123",
      "name": "Data Processing Workflow",
      "description": "Processes incoming data and generates reports.",
      "categories": ["data", "reporting"]
    }
  ]
}
```
```

--------------------------------

### Configure HTTP Headers and Query Parameters in n8n

Source: https://docs.n8n.io/integrations/builtin/credentials/httprequest

This JSON object defines the structure for passing custom headers and query string parameters to an HTTP request node. The 'headers' object is used for metadata like API versions, while the 'qs' object handles URL query parameters such as API keys.

```json
{
	"headers": {
		"api-version": "202404"
	},
	"qs": {
		"apikey": "my-api-key"
	}
}
```

--------------------------------

### Enable Concurrency Control with Environment Variable

Source: https://docs.n8n.io/hosting/scaling/concurrency-control

This snippet demonstrates how to enable concurrency control in self-hosted n8n by setting the N8N_CONCURRENCY_PRODUCTION_LIMIT environment variable. This variable defines the maximum number of production executions allowed to run concurrently. Executions exceeding this limit will be queued.

```shell
export N8N_CONCURRENCY_PRODUCTION_LIMIT=20
```

--------------------------------

### Constructing n8n API Documentation URL

Source: https://docs.n8n.io/api/using-api-playground

Defines the URL structure for accessing the Swagger UI playground. It requires the host, port, path, and API version number to generate the correct endpoint.

```text
N8N_HOST:N8N_PORT/N8N_PATH/api/v<api-version-number>/docs
```

--------------------------------

### Manually Set pairedItem in Programmatic Nodes (JavaScript)

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/paired-items

Demonstrates how to manually set the 'pairedItem' property for each item returned by a programmatic node in n8n. This is crucial for ensuring that subsequent nodes can correctly access data from preceding items. It shows how to reference the incoming item's 'pairedItem' or manually set the index and optionally specify the input if the node combines multiple inputs.

```javascript
newItem = {
	"json": { . . . },
	"pairedItem": {
		"item": item.pairedItem,
		// Optional: choose the input to use
		// Set this if your node combines multiple inputs
		"input": 0
	};

// Or set the index manually
newItem = {
		"json": { . . . }
		"pairedItem": {
			"item": i,
			// Optional: choose the input to use
			// Set this if your node combines multiple inputs
			"input": 0
		},
};
```

--------------------------------

### Configure Node Credentials

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Implements the credential type for the NASA API. It defines the API key input field and sets up a generic authentication method using query string parameters, along with a test request endpoint.

```typescript
import {
	IAuthenticateGeneric,
	ICredentialTestRequest,
	ICredentialType,
	INodeProperties,
} from 'n8n-workflow';

export class NasaPicsApi implements ICredentialType {
	name = 'NasaPicsApi';
	displayName = 'NASA Pics API';
	documentationUrl = 'https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node/';
	properties: INodeProperties[] = [
		{
			displayName: 'API Key',
			name: 'apiKey',
			type: 'string',
			default: '',
		},
	];
	authenticate: IAuthenticateGeneric = {
		type: 'generic',
		properties: {
			qs: {
				'api_key': '={{$credentials.apiKey}}'
			}
		},
	};
	test: ICredentialTestRequest = {
		request: {
			baseURL: 'https://api.nasa.gov',
			url: '/apod',
		},
	};
}
```

--------------------------------

### List Assistants

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/assistant-operations

Retrieves a list of all assistants available in your OpenAI organization.

```APIDOC
## GET /assistants

### Description
Use this operation to retrieve a list of assistants in your organization.

### Method
GET

### Endpoint
/assistants

### Parameters
#### Request Body
- **credential** (object) - Required - OpenAI credential to connect with.
- **resource** (string) - Required - Must be 'Assistant'.
- **operation** (string) - Required - Must be 'List Assistants'.

### Options
- **simplifyOutput** (boolean) - Optional - Turn on to return a simplified version of the response. Enabled by default.

### Request Example
```json
{
  "credential": {"id": "your_credential_id"},
  "resource": "Assistant",
  "operation": "List Assistants"
}
```

### Response
#### Success Response (200)
- **data** (array) - A list of assistant objects.
  - **id** (string) - The unique identifier of the assistant.
  - **name** (string) - The name of the assistant.
  - **description** (string) - The description of the assistant.
  - **model** (string) - The model used by the assistant.

#### Response Example
```json
{
  "data": [
    {
      "id": "asst_abc123",
      "name": "My Virtual Assistant",
      "description": "A virtual assistant that helps users with daily tasks.",
      "model": "gpt-4o"
    },
    {
      "id": "asst_def456",
      "name": "Code Helper",
      "description": "Assists with code generation and debugging.",
      "model": "gpt-3.5-turbo"
    }
  ]
}
```
```

--------------------------------

### Define Node Metadata (Codex)

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Provides the JSON configuration for node metadata, including node versioning, categories, and documentation URLs for credentials and primary resources.

```json
{
	"node": "n8n-nodes-base.NasaPics",
	"nodeVersion": "1.0",
	"codexVersion": "1.0",
	"categories": [
		"Miscellaneous"
	],
	"resources": {
		"credentialDocumentation": [
			{
				"url": ""
			}
		],
		"primaryDocumentation": [
			{
				"url": ""
			}
		]
	}
}
```

--------------------------------

### Configure n8n Logging via Environment Variables

Source: https://docs.n8n.io/hosting/logging-monitoring/logging

Set environment variables to control n8n's logging behavior. This includes log level, output destination (console or file), log file location, maximum file size, and the maximum number of log files to retain. These settings are crucial for debugging and monitoring n8n instances.

```bash
# Set the logging level to 'debug'
export N8N_LOG_LEVEL=debug

# Set log output to both console and a log file
export N8N_LOG_OUTPUT=console,file

# Set a save location for the log file
export N8N_LOG_FILE_LOCATION=/home/jim/n8n/logs/n8n.log

# Set a 50 MB maximum size for each log file
export N8N_LOG_FILE_SIZE_MAX=50

# Set 60 as the maximum number of log files to be kept
export N8N_LOG_FILE_COUNT_MAX=60
```

--------------------------------

### Retrieve all users via n8n Public API

Source: https://docs.n8n.io/api/api-reference

Fetches a list of users from the n8n instance. This operation requires an X-N8N-API-KEY header and supports pagination via cursor and filtering by role or project.

```Shell
curl https://your-instance-name.app.n8n.cloud/api/v1/users \
  --header 'X-N8N-API-KEY: YOUR_SECRET_TOKEN'
```

--------------------------------

### Credential Schema Endpoint

Source: https://docs.n8n.io/api/using-api-playground

The API provides documentation about credential formats through the `/credentials/schema/{credentialTypeName}` endpoint. This helps in understanding the structure required for different credential types.

```APIDOC
## Retrieving Credential Schema

### Description
This endpoint provides the schema for different credential types, which is useful for understanding the required fields when setting up credentials within n8n.

### Method
GET

### Endpoint
`N8N_HOST:N8N_PORT/N8N_PATH/api/v<api-version-number>/credentials/schema/{credentialTypeName}`

### Parameters
#### Path Parameters
- **credentialTypeName** (string) - Required - The type name of the credential for which to retrieve the schema. For example, `googleDriveOAuth2Api`.

### How to Find `credentialTypeName`
To determine the `credentialTypeName`, download your n8n workflow as a JSON file and inspect the `credentials` object. The key within this object corresponds to the `credentialTypeName`.

### Request Example (Illustrative)
To get the schema for Google Drive credentials:
`GET http://localhost:5678/api/v1/credentials/schema/googleDriveOAuth2Api`

### Response Example (Illustrative Structure)
```json
{
  "name": "Google Drive OAuth2",
  "description": "Credentials for Google Drive API",
  "properties": {
    "clientId": {
      "type": "string",
      "description": "Client ID"
    },
    "clientSecret": {
      "type": "string",
      "description": "Client Secret"
    }
    // ... other credential fields
  },
  "required": ["clientId", "clientSecret"]
}
```
```

--------------------------------

### Mount Custom Certificates via Docker CLI

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/custom-certificate-authority

Uses the -v flag to map a local directory containing certificates to the container's internal certificate storage path.

```bash
docker run -it --rm \
 --name n8n \
 -p 5678:5678 \
 -v ./pki:/opt/custom-certificates \
 docker.n8n.io/n8nio/n8n
```

--------------------------------

### Environment Variable Configuration

Source: https://docs.n8n.io/embed/workflow-templates

Configuration options for managing workflow templates within an embedded n8n environment using environment variables.

```APIDOC
## Disable Workflow Templates

### Description
To disable the default n8n workflow templates library, set the `N8N_TEMPLATES_ENABLED` environment variable to `false`.

### Environment Variable
`N8N_TEMPLATES_ENABLED`

### Value
`false`

## Use Your Own Workflow Templates Library

### Description
To use a custom workflow templates library, set the `N8N_TEMPLATES_HOST` environment variable to the base URL of your custom API.

### Environment Variable
`N8N_TEMPLATES_HOST`

### Value
`"http://your-custom-api.com/api"`
```

--------------------------------

### POST /rest/leadNotifications

Source: https://docs.n8n.io/integrations/builtin/credentials/linkedin

Creates a new webhook subscription to receive lead notifications for specific owners or forms.

```APIDOC
## POST /rest/leadNotifications

### Description
Registers a webhook URL to receive notifications when new leads are submitted to LinkedIn forms.

### Method
POST

### Endpoint
https://api.linkedin.com/rest/leadNotifications

### Request Body
- **webhook** (string) - Required - The public HTTPS URL of your n8n webhook.
- **owner** (object) - Required - The URN of the organization or account (e.g., {"organization": "urn:li:organization:123456"}).
- **leadType** (string) - Required - Type of lead (SPONSORED, COMPANY, EVENT, ORGANIZATION_PRODUCT).

### Request Example
{
  "webhook": "https://your-n8n-instance.com/webhook/linkedin-leads",
  "owner": {"organization": "urn:li:organization:123456"},
  "leadType": "SPONSORED"
}
```

--------------------------------

### Convert PDF to JSON Workflow (n8n)

Source: https://docs.n8n.io/courses/level-two/chapter-2

This n8n workflow demonstrates how to convert a PDF file to JSON. It uses an HTTP Request node to fetch the PDF and an Extract From File node to perform the conversion. The workflow is triggered manually.

```JSON
{
	"name": "Binary to JSON",
	"nodes": [
		{
		"parameters": {},
		"id": "78639a25-b69a-4b9c-84e0-69e045bed1a3",
		"name": "When clicking \"Execute Workflow\"",
		"type": "n8n-nodes-base.manualTrigger",
		"typeVersion": 1,
		"position": [
			480,
			520
		]
		},
		{
		"parameters": {
			"url": "https://media.kaspersky.com/pdf/Kaspersky_Lab_Whitepaper_Anti_blocker.pdf",
			"options": {}
		},
		"id": "a11310df-1287-4e9a-b993-baa6bd4265a6",
		"name": "HTTP Request",
		"type": "n8n-nodes-base.httpRequest",
		"typeVersion": 4.1,
		"position": [
			700,
			520
		]
		},
		{
		"parameters": {
			"operation": "pdf",
			"options": {}
		},
		"id": "88697b6b-fb02-4c3d-a715-750d60413e9f",
		"name": "Extract From File",
		"type": "n8n-nodes-base.extractFromFile",
		"typeVersion": 1,
		"position": [
			920,
			520
		]
		}
	],
	"pinData": {},
	"connections": {
		"When clicking \"Execute Workflow\"": {
		"main": [
			[
			{
				"node": "HTTP Request",
				"type": "main",
				"index": 0
			}
			]
		]
		},
		"HTTP Request": {
		"main": [
			[
			{
				"node": "Extract From File",
				"type": "main",
				"index": 0
			}
			]
		]
		}
	}
}

```

--------------------------------

### Implement Frontend Hook Files

Source: https://docs.n8n.io/embed/configuration

Defines the structure for frontend hooks using the window.n8nExternalHooks object. These hooks allow developers to execute custom logic when specific UI events occur.

```javascript
window.n8nExternalHooks = {
  nodeView: {
    mount: [
      function (store, meta) {
        // do something
      },
    ],
    createNodeActiveChanged: [
      function (store, meta) {
        // do something
      },
      function (store, meta) {
        // do something else
      },
    ],
    addNodeButton: [
      function (store, meta) {
        // do something
      },
    ],
  },
};
```

--------------------------------

### List All Template Collections

Source: https://docs.n8n.io/workflows/templates

Retrieves a list of all available template collections, with optional filtering and searching.

```APIDOC
## GET /templates/collections

### Description
Lists all template collections.

### Method
GET

### Endpoint
`/templates/collections`

### Parameters
#### Query Parameters
- **category** (string) - Optional - A comma-separated list of categories to filter collections by.
- **search** (string) - Optional - A search query to filter collections by name or description.

### Response
#### Success Response (200)
- **collections** (array) - A list of template collections.
  - **id** (string) - The collection ID.
  - **name** (string) - The name of the collection.
  - **description** (string) - A description of the collection.

#### Response Example
```json
{
  "collections": [
    {
      "id": "collection-abc",
      "name": "Featured Templates",
      "description": "A curated list of popular and useful templates."
    },
    {
      "id": "collection-xyz",
      "name": "Integration Templates",
      "description": "Templates for common integrations."
    }
  ]
}
```
```

--------------------------------

### Swagger UI Playground Access

Source: https://docs.n8n.io/api/using-api-playground

The n8n API includes a built-in Swagger UI playground for self-hosted versions, allowing interactive API request testing. The access path is constructed using environment variables.

```APIDOC
## Accessing the Swagger UI Playground

### Description
The Swagger UI playground provides interactive documentation for the n8n API, allowing you to test requests directly. This feature is available for all self-hosted pricing tiers but not on n8n Cloud.

### Endpoint Structure
The path to access the playground depends on your n8n hosting configuration and is constructed using environment variables:

`N8N_HOST:N8N_PORT/N8N_PATH/api/v<api-version-number>/docs`

### API Version
The current API version number is `1`. Multiple versions may be available in the future.

### Usage
Navigate to the constructed URL in your browser. You can select 'Authorize' and enter your API key to interact with your live data. Be cautious when modifying or deleting data.

### Example Path (Illustrative)
If `N8N_HOST` is `localhost`, `N8N_PORT` is `5678`, and `N8N_PATH` is empty, the path would be:
`/api/v1/docs`
```

--------------------------------

### Automate n8n Pulls with GitHub Actions

Source: https://docs.n8n.io/source-control-environments/create-environments

This GitHub Action automates the process of pulling changes into your n8n production instance whenever new work is pushed to the production or main branch. It utilizes cURL to interact with the n8n API, requiring instance URL and API key to be stored as GitHub secrets.

```yaml
name: CI
on:
  # Trigger the workflow on push or pull request events for the "production" branch
  push:
    branches: [ "production" ]
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:
jobs:
  run-pull:
    runs-on: ubuntu-latest
    steps:
      - name: PULL
				# Use GitHub secrets to protect sensitive information
        run: >
          curl --location '${{ secrets.INSTANCE_URL }}/version-control/pull' --header
          'Content-Type: application/json' --header 'X-N8N-API-KEY: ${{ secrets.INSTANCE_API_KEY }}'
```

--------------------------------

### n8n Workflow Template Schema Comparison

Source: https://docs.n8n.io/workflows/templates

Compares the JSON response structures for fetching workflow templates from n8n. The '/templates/workflows/{id}' endpoint returns a 'workflow' object containing the template metadata and the actual workflow definition. In contrast, '/workflows/templates/{id}' returns a flat structure where the workflow definition is directly accessible.

```json
// GET /templates/workflows/{id} returns (wrapped):
{
  "workflow": {
    "id": 123,
    "name": "...",
    "totalViews": 1000,
    // ... see full workflow item schema below
    "workflow": {    // actual workflow definition
      "nodes": [...],
      "connections": {}
    }
  }
}

// GET /workflows/templates/{id} returns (flat):
{
  "id": 123,
  "name": "...",
  "workflow": {      // actual workflow definition
    "nodes": [...],
    "connections": {}
  }
}
```

--------------------------------

### Access Binary Input Data with $binary

Source: https://docs.n8n.io/data/expression-reference/root

Provides access to any binary input data for the current item in the node. It's a shorthand for $input.item.binary and returns an Array.

```javascript
function getBinaryData() {
  // Example usage: access binary data
  return $binary;
}
```

--------------------------------

### Automate n8n Pull with GitHub Actions

Source: https://docs.n8n.io/source-control-environments/using/copy-work

A YAML configuration for a GitHub Action that triggers an n8n pull request on push events to the production branch. It utilizes GitHub Secrets for secure credential management.

```yaml
name: CI
on:
  push:
    branches: [ "production" ]
  workflow_dispatch:
jobs:
  run-pull:
    runs-on: ubuntu-latest
    steps:
      - name: PULL
        run: >
          curl --location '${{ secrets.INSTANCE_URL }}/version-control/pull' --header
          'Content-Type: application/json' --header 'X-N8N-API-KEY: ${{ secrets.INSTANCE_API_KEY }}'
```

--------------------------------

### Calculate Dates N Days From Today with Luxon

Source: https://docs.n8n.io/data/specific-data-types/luxon

Calculate a date that is a specified number of days before or after the current date using the `$today` variable and the `minus()` or `plus()` methods. This is useful for setting relative date fields. The `$today` variable is a convenience equivalent to `DateTime.now().set({ hour: 0, minute: 0, second: 0, millisecond: 0 }).minus({days: 7})`.

```javascript
{{$today.minus({days: 7})}}
```

```javascript
let sevenDaysAgo = $today.minus({days: 7})
```

--------------------------------

### Parse Non-Standard Date Strings with Luxon

Source: https://docs.n8n.io/data/specific-data-types/luxon

Use Luxon's `fromFormat()` function to parse date strings that do not follow standard formats. This requires providing both the date string and a format string that describes its structure. Be aware of Luxon's limitations when using ad-hoc parsing.

```javascript
DateTime.fromFormat("23-06-2019", "dd-MM-yyyy")
```

```javascript
let newFormat = DateTime.fromFormat("23-06-2019", "dd-MM-yyyy")
```

--------------------------------

### Configuring Batching in HTTP Request Node

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/common-issues

Illustrates how to configure the batching option within the HTTP Request node to manage API rate limits. This involves setting the number of items per batch and the interval between batches.

```javascript
// Example configuration for batching
// Items per Batch: 10
// Batch Interval (ms): 1000
```

--------------------------------

### Access All Node Items with `all()` in JavaScript and Python

Source: https://docs.n8n.io/code/cookbook/builtin/all

This function allows you to retrieve all items from the current or parent nodes. You can specify the branch index and run index to filter the results. If no parameters are provided, it returns all items from the current node.

```javascript
// Returns all the items of the given node and current run
let allItems = $("<node-name>").all();

// Returns all items the node "IF" outputs (index: 0 which is Output "true" of its most recent run)
let allItems = $("IF").all();

// Returns all items the node "IF" outputs (index: 0 which is Output "true" of the same run as current node)
let allItems = $("IF").all(0, $runIndex);

// Returns all items the node "IF" outputs (index: 1 which is Output "false" of run 0 which is the first run)
let allItems = $("IF").all(1, 0);
```

```python
# Returns all the items of the given node and current run
allItems = _("<node-name>").all()

# Returns all items the node "IF" outputs (index: 0 which is Output "true" of its most recent run)
allItems = _("IF").all()

# Returns all items the node "IF" outputs (index: 0 which is Output "true" of the same run as current node)
allItems = _("IF").all(0, _runIndex)

# Returns all items the node "IF" outputs (index: 1 which is Output "false" of run 0 which is the first run)
allItems = _("IF").all(1, 0);
```

--------------------------------

### Implement Backend Hook Files

Source: https://docs.n8n.io/embed/configuration

Defines the structure for backend hooks using module.exports. These hooks allow modification of settings and validation of workflow states via database access.

```javascript
module.exports = {
    "frontend": {
        "settings": [
            async function (settings) {
                settings.oauthCallbackUrls.oauth1 = 'https://n8n.example.com/oauth1/callback';
                settings.oauthCallbackUrls.oauth2 = 'https://n8n.example.com/oauth2/callback';
            }
        ]
    },
    "workflow": {
        "activate": [
            async function (workflowData) {
                const activeWorkflows = await this.dbCollections.Workflow.count({ active: true });

                if (activeWorkflows > 1) {
                    throw new Error(
                        'Active workflow limit reached.'
                    );
                }
            }
        ]
    }
}
```

--------------------------------

### Define DateTime and Boolean UI Elements

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

Configuration for date picker inputs and toggle switches for boolean values.

```JSON
{
	displayName: 'Modified Since',
	name: 'modified_since',
	type: 'dateTime',
	default: '',
	description: 'The date and time when the file was last modified',
	displayOptions: {
		show: {
			resource: [],
			operation: []
		}
	}
}
```

```JSON
{
	displayName: 'Wait for Image',
	name: 'waitForImage',
	type: 'boolean',
	default: true,
	description: 'Whether to wait for the image or not',
	displayOptions: {
		show: {
			resource: [],
			operation: []
		}
	}
}
```

--------------------------------

### POST /sendDocument

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/message-operations

Sends a document to a specified chat, supporting both binary files and file IDs/URLs.

```APIDOC
## POST /sendDocument

### Description
Sends a document file to a chat. Supports binary file uploads or referencing existing files via file_id or URL.

### Method
POST

### Endpoint
/sendDocument

### Parameters
#### Request Body
- **chatId** (string) - Required - The Chat ID or username.
- **document** (string) - Required - file_id or HTTP URL of the document.
- **caption** (string) - Optional - Caption text (max 1024 chars).
- **disableNotification** (boolean) - Optional - Send silently if true.
- **parseMode** (string) - Optional - 'HTML', 'Markdown', or 'MarkdownV2'.

### Request Example
{
  "chatId": "@channelusername",
  "document": "file_id_or_url",
  "caption": "Here is your document"
}

### Response
#### Success Response (200)
- **message_id** (integer) - The ID of the sent message.

#### Response Example
{
  "ok": true,
  "result": { "message_id": 12345 }
}
```

--------------------------------

### Configure MySQL Docker container

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.mysql/common-issues

Command to run a MySQL container while exposing the default port 3306 to the host machine. This ensures the database is accessible to external services like n8n.

```bash
docker run -p 3306:3306 --name my-mysql -d mysql:latest
```

--------------------------------

### Set Certificate Permissions

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/custom-certificate-authority

Updates the ownership of the mounted certificate directory to the n8n user (UID 1000) to ensure the application can read the files.

```bash
docker exec --user 0 n8n chown -R 1000:1000 /opt/custom-certificates
```

--------------------------------

### Generate Mock Data with JavaScript in n8n

Source: https://docs.n8n.io/_workflows/ai-code/reference-incoming-data-explicitly.json

This code snippet, used within an n8n code node, generates mock data. It returns an array of objects, each containing personal and work information. This is useful for testing or simulating incoming data.

```javascript
return [
  {
   "id": 0001,
   "personal_info": {
    "first_name": "Natalie",
    "surname": "Berlin"
   },
   "work_info": {
    "job_title": "Automation engineer"
   }
  },
  {
    "id": 0002,
    "personal_info": {
     "first_name": "Nathan",
     "surname": "Berlin"
    },
    "work_info": {
     "job_title": "Automation designer"
    }
   }
]
```

--------------------------------

### Define String Input UI Elements

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

Configuration objects for standard string inputs, including password fields and multi-line text areas. These elements support conditional display based on resource and operation selection.

```JSON
{
	displayName: 'Name',
	name: 'name',
	type: 'string',
	required: true,
	default: 'n8n',
	description: 'The name of the user',
	displayOptions: {
		show: {
			resource: [],
			operation: []
		}
	}
}
```

```JSON
{
	displayName: 'Password',
	name: 'password',
	type: 'string',
	required: true,
	typeOptions: {
		password: true
	},
	default: '',
	description: "User's password",
	displayOptions: {
		show: {
			resource: [],
			operation: []
		}
	}
}
```

```JSON
{
	displayName: 'Description',
	name: 'description',
	type: 'string',
	required: true,
	typeOptions: {
		rows: 4
	},
	default: '',
	description: 'Description',
	displayOptions: {
		show: {
			resource: [],
			operation: []
		}
	}
}
```

--------------------------------

### Format DateTime to Localized String (Luxon)

Source: https://docs.n8n.io/data/expression-reference/datetime

Returns a localized string representation of a DateTime object, using the language and format corresponding to its locale. Defaults to the system's locale if none is specified. Supports various formatting options.

```javascript
$now.toLocaleString() //=> '4/30/2024'
$now.toLocaleString({'dateStyle':'medium', 'timeStyle':'short'}) //=> 'Apr 30, 2024, 10:00 PM'
// (if in US English locale)
```

```javascript
$now.setLocale('de-DE').toLocaleString() //=> '30.4.2024'
```

```javascript
$now.toLocaleString({'dateStyle':'short'}) //=> '4/30/2024'
$now.toLocaleString({'dateStyle':'medium'}) //=> 'Apr 30, 2024'
$now.toLocaleString({'dateStyle':'long'}) //=> 'April 30, 2024'
$now.toLocaleString({'dateStyle':'full'}) //=> 'Tuesday, April 30, 2024'
// (if in US English locale)
```

```javascript
$now.toLocaleString({'year':'numeric', 'month':'numeric', 'day':'numeric'}) //=> '4/30/2024'
$now.toLocaleString({'year':'2-digit', 'month':'2-digit', 'day':'2-digit'}) //=> '04/30/24'
$now.toLocaleString({'month':'short', 'weekday':'short', 'day':'numeric'}) //=> 'Tue, Apr 30'
$now.toLocaleString({'month':'long', 'weekday':'long', 'day':'numeric'}) //=> 'Tuesday, April 30'
// (if in US English locale)
```

```javascript
$now.toLocaleString({'timeStyle':'short'}) //=> '10:00 PM'
$now.toLocaleString({'timeStyle':'medium'}) //=> '10:00:58 PM'
$now.toLocaleString({'timeStyle':'long'}) //=> '10:00:58 PM GMT+2'
$now.toLocaleString({'timeStyle':'full'}) //=> '10:00:58 PM Central European Summer Time'
// (if in US English locale)
```

```javascript
$now.toLocaleString({'hour':'numeric', 'minute':'numeric', hourCycle:'h24'}) //=> '22:00'
$now.toLocaleString({'hour':'2-digit', 'minute':'2-digit', hourCycle:'h12'}) //=> '10:00 PM'
// (if in US English locale)
```

--------------------------------

### Node Icon Configuration (SVG/PNG)

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/standard-parameters

Defines how to specify an icon for an n8n node. It supports using a single SVG or PNG file for both light and dark modes, or separate files for each mode using an object structure. Recommended icon resolution for PNG is 60x60px.

```typescript
icon: 'file:exampleNodeIcon.svg'
```

```typescript
icon: {
  light: 'file:exampleNodeIcon.svg',
  dark: 'file:exampleNodeIcon.dark.svg'
}
```

--------------------------------

### POST /message/send-and-wait

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/message-operations

Sends a message and pauses workflow execution until a user interaction (Approval, Free Text, or Custom Form) is received.

```APIDOC
## POST /message/send-and-wait

### Description
Sends a message and waits for a response from the user. Supports Approval buttons, Free Text input, or complex Custom Forms.

### Method
POST

### Parameters
#### Request Body
- **chatId** (string) - Required - Target chat ID.
- **message** (string) - Required - The prompt message.
- **responseType** (string) - Required - 'Approval', 'FreeText', or 'CustomForm'.
- **limitWaitTime** (string) - Optional - Timeout duration for the workflow to resume.

### Request Example
{
  "chatId": "12345678",
  "message": "Please approve this request",
  "responseType": "Approval"
}

### Response
#### Success Response (200)
- **status** (string) - The outcome of the user interaction.
- **data** (object) - The submitted response data.

#### Response Example
{
  "status": "approved",
  "data": { "confirmed": true }
```

--------------------------------

### Message an Assistant

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/assistant-operations

Send a message to an assistant and receive a response. This operation allows for configuring various parameters like credentials, assistant selection, prompt definition, and advanced options such as base URL, retries, and timeouts.

```APIDOC
## Message an Assistant

### Description
Use this operation to send a message to an assistant and receive a response.

### Method
POST

### Endpoint
/assistants/{assistant_id}/messages

### Parameters
#### Path Parameters
- **assistant_id** (string) - Required - The ID of the assistant to message.

#### Query Parameters
None

#### Request Body
- **credential** (object) - Required - Credential to connect with OpenAI.
  - **resource** (string) - Required - Must be 'Assistant'.
  - **operation** (string) - Required - Must be 'Message an Assistant'.
  - **assistant** (string) - Required - The assistant you want to message.
  - **prompt** (string or object) - Required - The text prompt or message to send.
    - **connectedChatTriggerNode** (string) - Use input from a previous node's `chatInput` field.
    - **defineBelow** (string) - Manually define the prompt.

### Options
- **Base URL** (string) - Optional - The base URL for API requests.
- **Max Retries** (integer) - Optional - The number of times to retry an operation on failure.
- **Timeout** (integer) - Optional - The maximum time in milliseconds to wait for a response.
- **Preserve Original Tools** (boolean) - Optional - Turn off to remove original tools associated with the assistant.

### Request Example
```json
{
  "credential": {
    "resource": "Assistant",
    "operation": "Message an Assistant",
    "assistant": "asst_abc123",
    "prompt": {
      "defineBelow": "What is the weather today?"
    }
  },
  "options": {
    "baseUrl": "https://api.openai.com/v1",
    "maxRetries": 3,
    "timeout": 60000,
    "preserveOriginalTools": false
  }
}
```

### Response
#### Success Response (200)
- **id** (string) - The ID of the message.
- **content** (array) - The content of the message.
- **role** (string) - The role of the message sender (e.g., 'assistant').

#### Response Example
```json
{
  "id": "msg_xyz789",
  "content": [
    {
      "type": "text",
      "text": {
        "value": "The weather today is sunny with a high of 75 degrees Fahrenheit.",
        "annotations": []
      }
    }
  ],
  "role": "assistant"
}
```
```

--------------------------------

### Declarative-Style Node Structure Outline

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/structure

This code snippet provides a basic outline for a declarative-style node in n8n. It includes the necessary import statements and the structure for the node class and its description object, which defines properties for resources and operations.

```typescript
import { INodeType, INodeTypeDescription } from 'n8n-workflow';

export class ExampleNode implements INodeType {
	description: INodeTypeDescription = {
		// Basic node details here
		properties: [
			// Resources and operations here
		]
	};
}
```

--------------------------------

### Basic Authentication using 'auth' property (TypeScript)

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/credentials-files

This TypeScript code snippet shows how to implement Basic Authentication for an n8n node. It configures the `authenticate` object to use the `auth` type, providing username and password from credentials.

```typescript
authenticate: IAuthenticateGeneric = {
	type: 'generic',
	properties: {
		auth: {
			username: '={{$credentials.username}}',
			password: '={{$credentials.password}}',
		},
	},
};
```

--------------------------------

### Uninstall community nodes and credentials via n8n CLI

Source: https://docs.n8n.io/hosting/cli-commands

Removes community nodes or specific credentials from the n8n instance. Requires the package name or credential type identifier.

```bash
n8n community-node --uninstall --package n8n-nodes-evolution-api
n8n community-node --uninstall --credential evolutionApi --userId 1234
```

--------------------------------

### Generic Authentication with Request Header (TypeScript)

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/credentials-files

This TypeScript snippet illustrates setting up generic authentication for an n8n node, sending an authorization token in the request header. It utilizes the `IAuthenticateGeneric` interface for configuration.

```typescript
authenticate: IAuthenticateGeneric = {
	type: 'generic',
	properties: {
		header: {
			Authorization: '=Bearer {{$credentials.authToken}}',
		},
	},
};
```

--------------------------------

### Display Text Content with n8n Sticky Note

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/let_your_ai_call_an_api.json

Allows for displaying rich text content, such as instructions or links, within an n8n workflow canvas using a sticky note. Customizable with height, width, and color.

```json
{
  "content": "## Try it out\n\nSelect **Chat** at the bottom and enter:\n\n_Hi! Please suggest something to do. I feel like learning something new._",
  "height": 214.8397420554627,
  "width": 185.9375,
  "color": 4
}
```

```json
{
  "content": "## Next steps\n\nLearn more about [Advanced AI in n8n](https://docs.n8n.io/advanced-ai/)",
  "height": 144.50520156238127
}
```

--------------------------------

### Rate Limit Calculation

Source: https://docs.n8n.io/integrations/builtin/credentials/twitter

Information on how rate limits are calculated based on authentication methods.

```APIDOC
## Rate Limit Calculation

### Description
This section explains how rate limits are calculated for API requests, differentiating between user rate limits and app rate limits based on the authentication method used.

### Authentication Methods and Rate Limits

- **Deprecated OAuth Method**: If you are using the deprecated OAuth method, **user rate limits** apply. You will have one limit per time window for each set of users' access tokens.
- **OAuth2 Method**: If you are using OAuth2, **app rate limits** apply. You will have a limit per time window for requests made by your app.

### Independent Calculation

X calculates user rate limits and app rate limits independently. Refer to X's Rate limits and authentication methods for more information about these rate limit types.
```

--------------------------------

### List Data Tables

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.datatable/tables

Lists existing data tables with options for filtering, sorting, and limiting results.

```APIDOC
## GET /api/tables

### Description
Lists existing data tables. You can return all tables, all tables up to a defined limit, or filter for tables to return.

### Method
GET

### Endpoint
/api/tables

### Parameters
#### Query Parameters
- **returnAll** (boolean) - Optional - Enable to return all matching tables.
- **limit** (integer) - Optional - The maximum number of tables to return (used when returnAll is false).
- **filterByName** (string) - Optional - Enter a value or expression to return data tables whose names contain the specified text. Matching is case-insensitive.
- **sortField** (string) - Optional - Select a field to sort results on.
- **sortDirection** (string) - Optional - Select whether to sort results in Ascending or Descending direction.

### Request Example
(No request body needed for listing)

### Response
#### Success Response (200)
- **tables** (array) - An array of data table objects.
  - **id** (string) - The ID of the data table.
  - **name** (string) - The name of the data table.
  - **columns** (array) - The columns of the data table.

#### Response Example
```json
{
  "tables": [
    {
      "id": "table_123",
      "name": "MyDataTable",
      "columns": [
        {
          "name": "ID",
          "type": "Number"
        }
      ]
    },
    {
      "id": "table_456",
      "name": "AnotherTable",
      "columns": [
        {
          "name": "Name",
          "type": "String"
        }
      ]
    }
  ]
}
```
```

--------------------------------

### Fetch Template Metadata

Source: https://docs.n8n.io/workflows/templates

Retrieves metadata for a specific workflow template, typically used for preview or browsing purposes.

```APIDOC
## GET /templates/workflows/<id>

### Description
Fetches template metadata for preview/browsing.

### Method
GET

### Endpoint
`/templates/workflows/<id>`

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the template.

### Response
#### Success Response (200)
- **template_metadata** (object) - Contains metadata about the template.
  - **name** (string) - The name of the template.
  - **description** (string) - A brief description of the template.
  - **categories** (array) - A list of categories the template belongs to.
  - **imageUrl** (string) - URL to an image representing the template.

#### Response Example
```json
{
  "name": "Example Workflow",
  "description": "A sample workflow demonstrating basic functionality.",
  "categories": ["example", "getting-started"],
  "imageUrl": "https://example.com/images/template.png"
}
```
```

--------------------------------

### HTTP Request Options Object

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/http-helpers

Defines the structure and possible fields for the `options` object used in the n8n `httpRequest` helper. This object allows customization of the request, including URL, headers, method, body, query parameters, authentication, and more.

```typescript
{
	url: string;
	headers?: object;
	method?: 'GET' | 'POST' | 'PUT' | 'DELETE' | 'HEAD';
	body?: FormData | Array | string | number | object | Buffer | URLSearchParams;
	qs?: object;
	arrayFormat?: 'indices' | 'brackets' | 'repeat' | 'comma';
	auth?: {
		username: string,
		password: string,
	};
	disableFollowRedirect?: boolean;
	encoding?: 'arraybuffer' | 'blob' | 'document' | 'json' | 'text' | 'stream';
	skipSslCertificateValidation?: boolean;
	returnFullResponse?: boolean;
	proxy?: {
		host: string;
		port: string | number;
		auth?: {
			username: string;
			password: string;
		},
		protocol?: string;
	};
	timeout?: number;
	json?: boolean;
}	

```

--------------------------------

### Format Salesforce Private Key for n8n

Source: https://docs.n8n.io/integrations/builtin/credentials/salesforce

The private key must be provided in standard PEM format when configuring Salesforce credentials in n8n. Ensure the key data is placed between the BEGIN and END headers.

```text
-----BEGIN PRIVATE KEY-----
KEY DATA GOES HERE
-----END PRIVATE KEY-----
```

--------------------------------

### Docker Compose for External Task Runner Mode

Source: https://docs.n8n.io/hosting/configuration/task-runners

This Docker Compose configuration sets up n8n and its task runners in external mode. It ensures the task runner image version matches the n8n image version and that n8n is version 1.111.0 or higher. Key environment variables for enabling external mode, setting authentication tokens, and specifying broker URIs are included.

```yaml
services:
  n8n:
    image: n8nio/n8n:1.111.0
    container_name: n8n-main
    environment:
      - N8N_RUNNERS_ENABLED=true
      - N8N_RUNNERS_MODE=external
      - N8N_RUNNERS_BROKER_LISTEN_ADDRESS=0.0.0.0
      - N8N_RUNNERS_AUTH_TOKEN=your-secret-here
      - N8N_NATIVE_PYTHON_RUNNER=true
    ports:
      - "5678:5678"
    volumes:
      - n8n_data:/home/node/.n8n
    # etc.

  task-runners:
    image: n8nio/runners:1.111.0
    container_name: n8n-runners
    environment:
      - N8N_RUNNERS_TASK_BROKER_URI=http://n8n-main:5679
      - N8N_RUNNERS_AUTH_TOKEN=your-secret-here
      # etc.
    depends_on:
      - n8n

volumes:
  n8n_data:

```

--------------------------------

### Light Versioning Configuration in n8n Nodes

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-versioning

Configures light versioning for an n8n node by making the 'version' parameter an array and using '@version' in displayOptions to control visibility for specific versions. This allows for minor version increments without code duplication.

```typescript
{
    displayName: 'NASA Pics',
    name: 'NasaPics',
    icon: 'file:nasapics.svg',
    // List the available versions
    version: [1,2,3],
    // More basic parameters here
    properties: [
        // Add a resource that's only displayed for version2
        {
            displayName: 'Resource name',
            // More resource parameters
            displayOptions: {
                show: {
                    '@version': 2,
                },
            },
        },
    ],
}
```

--------------------------------

### Programmatic Node Structure in TypeScript

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/structure

This snippet outlines the basic structure of a programmatic-style node in n8n using TypeScript. It includes the necessary imports, the node class definition with its description (properties), and the asynchronous execute method for processing data. This serves as a template for creating custom n8n nodes.

```typescript
import { IExecuteFunctions } from 'n8n-core';
import { INodeExecutionData, INodeType, INodeTypeDescription } from 'n8n-workflow';

export class ExampleNode implements INodeType {
  description: INodeTypeDescription = {
    // Basic node details here
    properties: [
      // Resources and operations here
    ]
  };

  async execute(this: IExecuteFunctions): Promise<INodeExecutionData[][]> {
    // Process data and return
  }
};
```

--------------------------------

### Running Ollama in Docker

Source: https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.lmchatollama/common-issues

Command to run the Ollama Docker container, publishing port 11434 and mounting a volume for persistent data. This is used when Ollama is in Docker and n8n is not, or when both are in separate Docker containers.

```bash
docker run -d -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

--------------------------------

### Register Frontend Hooks

Source: https://docs.n8n.io/embed/configuration

Demonstrates how to include a custom frontend hook script in the n8n editor UI by adding a script tag to the index.html file.

```html
<script src="frontend-hooks.js"></script>
```

--------------------------------

### Replacing 'import' with 'require' in n8n Code Node

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.code/common-issues

Demonstrates how to replace unsupported 'import' statements with the 'require' function for loading modules within the n8n Code node's JavaScript sandbox. This is necessary because 'import' and 'export' are not allowed at the top level.

```javascript
// Original code:
// import express from "express";
// New code:
const express = require("express");
```

--------------------------------

### Configure SameSite Cookie Behavior in n8n

Source: https://docs.n8n.io/hosting/configuration/environment-variables/security

Controls how cookies are sent with cross-site requests. Options include 'strict', 'lax', and 'none'. 'lax' is the default, balancing security and usability. 'none' requires HTTPS.

```bash
# Example: Set SameSite cookie to strict
N8N_SAMESITE_COOKIE=strict
```

--------------------------------

### Node Data Access Methods

Source: https://docs.n8n.io/data/data-mapping/referencing-other-nodes

Methods to retrieve items, parameters, and context from specific nodes in an n8n workflow.

```APIDOC
## GET Node Data Access

### Description
Methods provided by the n8n runtime to interact with data outputs from other nodes in a workflow.

### Methods
- **all(branchIndex?, runIndex?)**: Returns all items from a given node.
- **first(branchIndex?, runIndex?)**: Returns the first item output by the node.
- **last(branchIndex?, runIndex?)**: Returns the last item output by the node.
- **item**: The linked item used to produce the current item.
- **params**: Object containing query settings and operation configurations of the node.
- **context**: Boolean indicating processing state (specifically for Loop Over Items nodes).
- **itemMatching(currentNodeInputIndex)**: Traces back from an input item in the Code node.

### Parameters
#### Path Parameters
- **node-name** (string) - Required - The name of the node to retrieve data from.

#### Optional Parameters
- **branchIndex** (number) - Optional - The specific output branch to target.
- **runIndex** (number) - Optional - The specific execution run index.

### Request Example
// Accessing all items from a node named 'HTTP Request'
$("HTTP Request").all();

### Response
#### Success Response (200)
- **data** (Array/Object) - The requested items or node metadata.
```

--------------------------------

### Specify Custom Node Locations with Environment Variable

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/custom-nodes-location

This snippet demonstrates how to set the N8N_CUSTOM_EXTENSIONS environment variable to define multiple directories for custom n8n nodes. This allows n8n to load nodes from user-defined locations on startup. Ensure the paths are correctly formatted and separated by semicolons.

```shell
export N8N_CUSTOM_EXTENSIONS="/home/jim/n8n/custom-nodes;/data/n8n/nodes"
```

--------------------------------

### Create multiple users via n8n Public API

Source: https://docs.n8n.io/api/api-reference

Creates one or more users by sending an array of user objects in the request body. Requires the X-N8N-API-KEY header and Content-Type set to application/json.

```Shell
curl https://your-instance-name.app.n8n.cloud/api/v1/users \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'X-N8N-API-KEY: YOUR_SECRET_TOKEN' \
  --data '[
  {
    "email": "",
    "role": "global:member"
  }
]'
```

--------------------------------

### Format Dates into Human-Readable Strings with Luxon

Source: https://docs.n8n.io/data/specific-data-types/luxon

Convert Luxon date objects into human-readable formats using the `toLocaleString()` function. You can specify various options to control the output format, such as the month's name, day, and year. This is useful for presenting dates in a user-friendly way.

```javascript
{{$today.minus({days: 7}).toLocaleString()}}
```

```javascript
let readableSevenDaysAgo = $today.minus({days: 7}).toLocaleString()
```

```javascript
{{$today.minus({days: 7}).toLocaleString({month: 'long', day: 'numeric', year: 'numeric'})}}
```

```javascript
let readableSevenDaysAgo = $today.minus({days: 7}).toLocaleString({month: 'long', day: 'numeric', year: 'numeric'})
```

--------------------------------

### Configure package.json for n8n nodes

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

Defines the structure for a custom n8n node package. It includes mandatory fields like the n8n object for linking credentials and node files, and the n8n-community-node-package keyword.

```json
{
	"name": "n8n-nodes-friendgrid",
	"version": "0.1.0",
	"description": "n8n node to create contacts in SendGrid",
	"keywords": [
		"n8n-community-node-package"
	],
	"license": "MIT",
	"homepage": "https://n8n.io",
	"author": {
		"name": "Test",
		"email": "test@example.com"
	},
	"repository": {
		"type": "git",
		"url": "git+<your-repo-url>"
	},
	"main": "index.js",
	"files": [
		"dist"
	],
	"n8n": {
		"n8nNodesApiVersion": 1,
		"credentials": [
			"dist/credentials/FriendGridApi.credentials.js"
		],
		"nodes": [
			"dist/nodes/FriendGrid/FriendGrid.node.js"
		]
	}
}
```

--------------------------------

### JavaScript: Define Node Display Options

Source: https://docs.n8n.io/integrations/creating-nodes/plan/choose-node-method

This JavaScript code defines display options for a node, including its display name and additional fields. It's part of a larger system, likely for defining workflow nodes in a visual programming environment. No execute method is needed as it's a configuration object.

```javascript
displayName: 'Email',
. . .
},
{
  displayName: 'Additional Fields',
  // Sets up optional fields
},
],
}
// No execute method needed
```

--------------------------------

### Update MySQL rows with composite keys

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.mysql/common-issues

Demonstrates how to perform an update operation on a table using a composite key by executing a raw SQL query. This bypasses the limitations of the standard Update node which only supports single-column matching.

```sql
UPDATE orders SET quantity = 3 WHERE customer_id = 538 AND product_id = 800;
```

--------------------------------

### Deploy n8n to Google Cloud Run

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

Commands to deploy the n8n container to Cloud Run. Includes setting the N8N_ENDPOINT_HEALTH variable to avoid path conflicts and configuring memory and scaling settings.

```bash
gcloud run deploy n8n \
    --image=n8nio/n8n \
    --region=us-west1 \
    --allow-unauthenticated \
    --port=5678 \
    --no-cpu-throttling \
    --memory=2Gi \
    --set-env-vars="N8N_ENDPOINT_HEALTH=health"
```

```bash
gcloud run deploy n8n \
    --image=n8nio/n8n \
    --region=us-west1 \
    --allow-unauthenticated \
    --port=5678 \
    --no-cpu-throttling \
    --memory=2Gi \
    --scaling=1 \
    --set-env-vars="N8N_ENDPOINT_HEALTH=health"
```

--------------------------------

### Accessing and Managing Node-Specific Static Data

Source: https://docs.n8n.io/code/cookbook/builtin/get-workflow-static-data

Demonstrates how to retrieve and manipulate static data scoped exclusively to a specific node. Only the node that initializes or updates this data can access it.

```JavaScript
// Get the static data of the node
const nodeStaticData = $getWorkflowStaticData('node');

// Access its data
const lastExecution = nodeStaticData.lastExecution;

// Update its data
nodeStaticData.lastExecution = new Date().getTime();

// Delete data
delete nodeStaticData.lastExecution;
```

```Python
# Get the static data of the node
nodeStaticData = _getWorkflowStaticData('node')

# Access its data
lastExecution = nodeStaticData.lastExecution

# Update its data
nodeStaticData.lastExecution = new Date().getTime()

# Delete data
delete nodeStaticData.lastExecution
```

--------------------------------

### Define n8n API Credentials with Generic Authentication (TypeScript)

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/credentials-files

This snippet demonstrates how to define API credentials for an n8n node using TypeScript. It includes properties for API key and domain, and configures generic authentication to send the API key in the query string. The `test` object specifies the base URL and endpoint for testing the credentials.

```typescript
import {
	IAuthenticateGeneric,
	ICredentialTestRequest,
	ICredentialType,
	INodeProperties,
} from 'n8n-workflow';

export class ExampleNode implements ICredentialType {
	name = 'exampleNodeApi';
	displayName = 'Example Node API';
	documentationUrl = '';
	properties: INodeProperties[] = [
		{
			displayName: 'API Key',
			name: 'apiKey',
			type: 'string',
			default: '',
		},
	];
	authenticate: IAuthenticateGeneric = {
		type: 'generic',
		properties: {
    		// Can be body, header, qs or auth
			qs: {
        		// Use the value from `apiKey` above
				'api_key': '={{$credentials.apiKey}}'
			}

		},
	};
	test: ICredentialTestRequest = {
		request: {
			baseURL: '={{$credentials?.domain}}',
			url: '/bearer',
		},
	};
}
```

--------------------------------

### Set execution custom data in n8n

Source: https://docs.n8n.io/data/expression-reference/customdata

The setAll method allows you to store multiple key-value pairs as custom data for an execution. This is useful for tagging executions with metadata like user emails or IDs to facilitate easier filtering within the n8n interface.

```JavaScript
$execution.customData.setAll({"user_email": "me@example.com", "id": 1234});
```

--------------------------------

### Trigger n8n Source Control Pull via API

Source: https://docs.n8n.io/source-control-environments/using/copy-work

A cURL command to trigger a pull operation on an n8n instance. It requires an API key and the instance URL to authenticate and execute the update.

```bash
curl --request POST \
	--location '<YOUR-INSTANCE-URL>/api/v1/source-control/pull' \
	--header 'Content-Type: application/json' \
	--header 'X-N8N-API-KEY: <YOUR-API-KEY>' \
	--data '{"force": true}'
```

--------------------------------

### Verify Node Execution Status in n8n

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/common-issues

Use the .isExecuted property to check if a specific node has successfully completed its execution before attempting to access its output. This is useful for conditional logic in custom JavaScript nodes.

```JavaScript
$("<node-name>").isExecuted
```

--------------------------------

### Define API routing and request defaults

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/declarative-style-parameters

The routing object specifies the details of an API call within a node operation. It works alongside requestDefaults to establish base URLs and headers for consistent service communication.

```TypeScript
description: INodeTypeDescription = {
  requestDefaults: {
			baseURL: 'https://api.nasa.gov',
			url: '',
			headers: {
				Accept: 'application/json',
				'Content-Type': 'application/json',
			},
		},
    properties: [
      {
        displayName: 'Operation',
        options: [
          {
            name: 'Get',
            value: 'get',
            routing: {
              request: {
                method: 'GET',
                url: '/planetary/apod'
              }
            }
          }
        ]
      }
    ]
}
```

--------------------------------

### Add HTML Formatting Option to Pushover Node

Source: https://docs.n8n.io/release-notes/0-x

This enhancement adds an HTML formatting option to the Pushover node, allowing users to send messages with rich text formatting. It also includes the addition of a credential test for the Pushover node to ensure secure and correct authentication.

```javascript
Pushover node: adds an HTML formatting option, and a credential test.
```

--------------------------------

### Enable n8n Execution Pruning with Custom Age and Count (npm)

Source: https://docs.n8n.io/hosting/scaling/execution-data

This configuration enables execution pruning in n8n and sets custom values for the maximum age of finished executions (in hours) and the maximum number of finished executions to keep. Pruning is enabled by default but can be explicitly turned on.

```bash
# Enable executions pruning
export EXECUTIONS_DATA_PRUNE=true

# How old (hours) a finished execution must be to qualify for soft-deletion
export EXECUTIONS_DATA_MAX_AGE=168

# Max number of finished executions to keep. May not strictly prune back down to the exact max count. Set to `0` for unlimited.
export EXECUTIONS_DATA_PRUNE_MAX_COUNT=50000
```

--------------------------------

### Define API Resources for n8n Node

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Configures the 'resource' property in an n8n node to provide a dropdown selection for API endpoints. This uses the 'options' type to allow users to choose between different API categories.

```TypeScript
properties: [
	{
		displayName: 'Resource',
		name: 'resource',
		type: 'options',
		noDataExpression: true,
		options: [
			{
				name: 'Astronomy Picture of the Day',
				value: 'astronomyPictureOfTheDay',
			},
			{
				name: 'Mars Rover Photos',
				value: 'marsRoverPhotos',
			},
		],
		default: 'astronomyPictureOfTheDay',
	},
]
```

--------------------------------

### Configure Theme Colors via SCSS Tokens

Source: https://docs.n8n.io/embed/white-labelling

Modifying primary theme colors by updating HSL values within the SCSS mixin tokens.

```scss
@mixin theme {
	--color-primary-h: 204;
	--color-primary-s: 100%;
	--color-primary-l: 50%;
}
```

--------------------------------

### Configure n8n node metadata

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

The codex JSON file defines node identity, versioning, and documentation links for the n8n editor.

```JSON
{
	"node": "n8n-nodes-base.FriendGrid",
	"nodeVersion": "1.0",
	"codexVersion": "1.0",
	"categories": ["Miscellaneous"],
	"resources": {
		"credentialDocumentation": [{ "url": "" }],
		"primaryDocumentation": [{ "url": "" }]
	}
}
```

--------------------------------

### Process User Input with n8n Langchain LLM Node

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/let_your_ai_call_an_api.json

Processes user input using a Langchain LLM chain. It takes the input from a workflow trigger and passes it to the language model for processing. This is often used for natural language understanding tasks.

```json
{
  "prompt": "={{ $('Execute Workflow Trigger').item.json.chatInput }}"
}
```

--------------------------------

### NodeOutputData Methods

Source: https://docs.n8n.io/data/expression-reference/nodeoutputdata

Methods for accessing node output items and execution metadata.

```APIDOC
## GET $().all()

### Description
Returns an array of all output items from the node.

### Parameters
#### Query Parameters
- **branchIndex** (Number) - Optional - The output branch of the node to use. Defaults to 0.
- **runIndex** (Number) - Optional - The run of the node to use. Defaults to 0.

### Response
- **Returns** (Array) - An array of output items.

---

## GET $().first()

### Description
Returns the first item output by the node.

### Parameters
#### Query Parameters
- **branchIndex** (Number) - Optional - The output branch of the node to use. Defaults to 0.
- **runIndex** (Number) - Optional - The run of the node to use. Defaults to 0.

### Response
- **Returns** (Item) - The first item object.

---

## GET $().isExecuted

### Description
Checks if the node has been executed.

### Response
- **Returns** (Boolean) - True if the node has executed, false otherwise.

---

## GET $().item

### Description
Returns the matching item used to produce the current item in the current node.

### Response
- **Returns** (Item) - The matching item object.

---

## GET $().itemMatching()

### Description
Returns the matching item used to produce the item in the current node at the specified index.

### Parameters
#### Query Parameters
- **currentItemIndex** (Number) - Required - The index of the item in the current node to be matched with.

### Response
- **Returns** (Item) - The matching item object.

---

## GET $().last()

### Description
Returns the last item output by the node.

### Parameters
#### Query Parameters
- **branchIndex** (Number) - Optional - The output branch of the node to use. Defaults to 0.
- **runIndex** (Number) - Optional - The run of the node to use. Defaults to 0.

### Response
- **Returns** (Item) - The last item object.
```

--------------------------------

### Check if Object is Empty (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/object

The `isEmpty()` method returns `true` if the object has no keys or if the object is `null`. Otherwise, it returns `false`. This is a custom n8n functionality.

```javascript
// obj = {'name': 'Nathan'}
obj.isEmpty() //=> false

// obj = {}
obj.isEmpty() //=> true
```

--------------------------------

### Configure n8n Service URL for OAuth

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

This snippet shows how to set the n8n service URL as an environment variable. This is a crucial step when re-deploying n8n on Cloud Run, especially when setting up OAuth for Google Workspace services, as it defines the callback URL for authentication.

```bash
export SERVICE_URL="your-n8n-service-URL"
```

--------------------------------

### Manage API Workflow Execution

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/let_your_ai_call_an_api.json

Handles the sequence of API calls and response setting within the n8n workflow. It links activity analysis to the final API response assignment.

```json
{
  "Call_the_API": {
    "main": [{"node": "Set 'response' value", "type": "main", "index": 0}]
  },
  "Work_out_activity_type": {
    "main": [{"node": "Call the API", "type": "main", "index": 0}]
  }
}
```

--------------------------------

### Summarize submission data for Slack notifications

Source: https://docs.n8n.io/code/ai-code

This script processes a list of submissions to count occurrences of ideas, features, and bugs. It also identifies the top 5 submissions by vote count and formats the results into a Slack-compatible markdown string.

```javascript
const submissions = $input.all();

// Count the number of ideas, features, and bugs
let ideaCount = 0;
let featureCount = 0;
let bugCount = 0;

submissions.forEach((submission) => {
  switch (submission.json.property_type[0]) {
    case "Idea":
      ideaCount++;
      break;
    case "Feature":
      featureCount++;
      break;
    case "Bug":
      bugCount++;
      break;
  }
});

// Sort submissions by votes and take the top 5
const topSubmissions = submissions
  .sort((a, b) => b.json.property_votes - a.json.property_votes)
  .slice(0, 5);

let topSubmissionText = "";
topSubmissions.forEach((submission) => {
  topSubmissionText += `<${submission.json.url}|${submission.json.name}> with ${submission.json.property_votes} votes\n`;
});

// Construct the Slack message
const slackMessage = `*Summary of Submissions*\n
Ideas: ${ideaCount}\n
Features: ${featureCount}\n
Bugs: ${bugCount}\n
Top 5 Submissions:\n
${topSubmissionText}`;

return [{ json: { slackMessage } }];
```

--------------------------------

### Configure AI Language Model Nodes

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/let_your_ai_call_an_api.json

Defines the integration of GPT-4 models within n8n workflows. These nodes are used for processing activity types, calculating participant counts, and managing auto-fixing output parsing.

```json
{
  "GPT4_Model_2": {
    "ai_languageModel": [{"node": "Work out activity type and number of people", "type": "ai_languageModel", "index": 0}]
  },
  "GPT4_Model_3": {
    "ai_languageModel": [{"node": "Auto-fixing Output Parser", "type": "ai_languageModel", "index": 0}]
  }
}
```

--------------------------------

### Convert DateTime to String Representation (Luxon)

Source: https://docs.n8n.io/data/expression-reference/datetime

Returns a string representation of the DateTime object, similar to `toISO()`. For more advanced formatting, use `format()` or `toLocaleString()`.

```javascript
$now.toString() //=> 2024-04-05T18:44:55.525+02:00
```

--------------------------------

### Answer Inline Query

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/callback-operations

Sends answers to callback queries initiated from inline queries using the Bot API's answerInlineQuery method.

```APIDOC
## POST /api/telegram/answerInlineQuery

### Description
Sends answers to callback queries from inline queries.

### Method
POST

### Endpoint
/api/telegram/answerInlineQuery

### Parameters
#### Request Body
- **credential** (string) - Required - Credential to connect with Telegram.
- **resource** (string) - Required - Must be 'Callback'.
- **operation** (string) - Required - Must be 'Answer Inline Query'.
- **queryId** (string) - Required - The unique identifier of the query to answer.
- **results** (string) - Required - A JSON-serialized array of results for the query (max 50 results).
- **cacheTime** (integer) - Optional - Maximum time in seconds the client can cache the result. Defaults to 0.
- **isPersonal** (boolean) - Optional - Whether the results are personal to the user. Defaults to false.
- **nextOffset** (string) - Optional - If more results are available, specify the offset for the next query.
- **switchPmText** (string) - Optional - If set, sends a message to the user to switch to inline mode.
- **switchPmParameter** (string) - Optional - Parameter for the switchPmText message.

### Request Example
```json
{
  "credential": "your_telegram_credential",
  "resource": "Callback",
  "operation": "Answer Inline Query",
  "queryId": "inline_query_67890",
  "results": "[\"inline_result_1\", \"inline_result_2\"]",
  "cacheTime": 60,
  "isPersonal": true,
  "nextOffset": "offset_abc",
  "switchPmText": "Try this feature!",
  "switchPmParameter": "feature_xyz"
}
```

### Response
#### Success Response (200)
- **status** (string) - Indicates the success of the operation.

#### Response Example
```json
{
  "status": "success"
}
```
```

--------------------------------

### Enable n8n Execution Pruning with Custom Age and Count (Docker)

Source: https://docs.n8n.io/hosting/scaling/execution-data

This Docker command enables execution pruning in n8n and configures custom values for the maximum age of finished executions and the maximum number of finished executions to retain. It maps the n8n port and sets the pruning-related environment variables.

```bash
docker run -it --rm \
 --name n8n \
 -p 5678:5678 \
 -e EXECUTIONS_DATA_PRUNE=true \
 -e EXECUTIONS_DATA_MAX_AGE=168 \
 docker.n8n.io/n8nio/n8n
```

--------------------------------

### Join Usernames with Commas and Quotes (JavaScript)

Source: https://docs.n8n.io/code/ai-code

This code snippet transforms an array of items into a single string containing all usernames, each enclosed in double quotes and separated by a comma. It utilizes the `map` function to format each username and `join` to create the final comma-separated string. The result is returned within a JSON object under the key 'usernames'.

```javascript
const items = $input.all();
const usernames = items.map((item) => `"${item.json.username}"`);
const result = usernames.join(", ");
return [{ json: { usernames: result } }];
```

--------------------------------

### Define Assignment Collection Parameter

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

The 'assignmentCollection' type facilitates a drag-and-drop interface, allowing users to pre-fill name and value pairs efficiently.

```JavaScript
{
	displayName: 'Fields to Set',
	name: 'assignments',
	type: 'assignmentCollection',
	default: {},
}
```

--------------------------------

### Retrieving Credential Schema Endpoint

Source: https://docs.n8n.io/api/using-api-playground

Defines the URL structure for querying specific credential schemas. Users must replace the placeholder with the specific credential type name found in their workflow configuration.

```text
N8N_HOST:N8N_PORT/N8N_PATH/api/v<api-version-number>/credentials/schema/{credentialTypeName}
```

--------------------------------

### Implement Node Versioning in n8n

Source: https://docs.n8n.io/release-notes/0-x

This code snippet demonstrates how to implement node versioning in n8n. By changing the 'version' parameter to an array and including existing versions, you can manage multiple versions of a node. This allows for incremental updates without code duplication and enables querying the current version within the 'execute' function.

```javascript
change the `version` parameter in your node to an array, and add your version numbers, including your existing version. You can then access the version parameter with `@version` in your `displayOptions` (to control which version n8n displays). You can also query the version in your `execute` function using `const nodeVersion = this.getNode().typeVersion;`.
```

--------------------------------

### Configure Nginx location block for n8n MCP

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-langchain.mcptrigger

This Nginx configuration snippet disables proxy buffering, gzip compression, and chunked transfer encoding for the /mcp/ endpoint. These settings are required to ensure proper handling of SSE and streamable HTTP traffic for the n8n MCP Server Trigger.

```nginx
location /mcp/ {
    proxy_http_version          1.1;
    proxy_buffering             off;
    gzip                        off;
    chunked_transfer_encoding   off;

    proxy_set_header            Connection '';

    # The rest of your proxy headers and settings
    # . . .
}
```

--------------------------------

### Define Color Selector Parameter

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

The 'color' type provides a color picker interface for users. It is typically used for UI-related configurations like background colors.

```JavaScript
{
	displayName: 'Background Color',
	name: 'backgroundColor',
	type: 'color',
	default: '',
	displayOptions: {
		show: {
			resource: [],
			operation: []
		}
	},
}
```

--------------------------------

### POST /sendChatAction

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/message-operations

Notifies the user that the bot is performing a specific action, such as typing or recording.

```APIDOC
## POST /sendChatAction

### Description
Use this operation to inform the user that the bot is performing an action. The status remains active for 5 seconds or less.

### Method
POST

### Endpoint
/sendChatAction

### Parameters
#### Request Body
- **chatId** (string) - Required - The Chat ID or username of the channel.
- **action** (string) - Required - The action to broadcast (e.g., 'typing', 'recording_audio', 'uploading_document').

### Request Example
{
  "chatId": "@channelusername",
  "action": "typing"
}

### Response
#### Success Response (200)
- **ok** (boolean) - Indicates success.
- **result** (boolean) - Returns true if the action was sent successfully.
```

--------------------------------

### Structure AI Output with n8n Structured Output Parser

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/let_your_ai_call_an_api.json

Parses AI model output into a structured JSON format based on a provided JSON schema. This node is useful for enforcing specific data structures from language models, particularly within the Langchain integration.

```json
{
  "jsonSchema": "{\n  \"type\": \"object\",\n  \"properties\": {\n    \"type\": {\n      \"type\": \"object\",\n      \"properties\": {\n        \"data\": {\n          \"enum\": [\"education\",\"recreational\",\"social\",\"diy\",\"charity\",\"cooking\",\"relaxation\",\"music\",\"busywork\"]\n        }\n      }\n    }\n    \"participants\": {\n      \"type\": \"number\"\n    }\n  }\n}"
}
```

--------------------------------

### Define Node Resource and Operations in n8n

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

Configures the resource and operation properties for an n8n node. These objects define the UI dropdowns and conditional logic required to map user input to specific API endpoints.

```javascript
{
	displayName: 'Resource',
	name: 'resource',
	type: 'options',
	options: [
		{
			name: 'Contact',
			value: 'contact',
		},
	],
	default: 'contact',
	noDataExpression: true,
	required: true,
	description: 'Create a new contact',
},
{
	displayName: 'Operation',
	name: 'operation',
	type: 'options',
	displayOptions: {
		show: {
			resource: [
				'contact',
			],
		},
	},
	options: [
		{
			name: 'Create',
			value: 'create',
			description: 'Create a contact',
			action: 'Create a contact',
		},
	],
	default: 'create',
	noDataExpression: true,
},
{
	displayName: 'Email',
	name: 'email',
	type: 'string',
	required: true,
	displayOptions: {
		show: {
			operation: [
				'create',
			],
			resource: [
				'contact',
			],
		},
	},
	default:'',
	placeholder: 'name@email.com',
	description:'Primary email for the contact',
}
```

--------------------------------

### Convert JavaScript Dates to Luxon in n8n

Source: https://docs.n8n.io/data/specific-data-types/luxon

Provides methods for converting native JavaScript `Date` objects into Luxon `DateTime` objects within n8n. It covers usage in expressions using `.toDateTime()` and in the Code node using `DateTime.fromJSDate()`.

```javascript
// In expressions:
{{ (new Date()).toDateTime() }}

```

```javascript
// In the Code node:
let luxondate = DateTime.fromJSDate(new Date())

```

--------------------------------

### Enable Credential Overwrite Persistence (Bash)

Source: https://docs.n8n.io/embed/configuration

This snippet shows how to enable persistence for credential overwrites by setting the `CREDENTIALS_OVERWRITE_PERSISTENCE` environment variable to `true`. When enabled, overwrites are stored in the database and propagated to all workers.

```bash
export CREDENTIALS_OVERWRITE_PERSISTENCE=true
```

--------------------------------

### Retrieve Postgres Server Address

Source: https://docs.n8n.io/integrations/builtin/credentials/postgres

SQL query to identify the current database server's IP address or host.

```SQL
SELECT inet_server_addr();
```

--------------------------------

### Implement Rate Limiting with SplitInBatches and Wait Nodes

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/common-issues

This JSON workflow configuration demonstrates how to use the 'Loop Over Items' (SplitInBatches) node combined with a 'Wait' node to throttle requests to the OpenAI API. This pattern prevents hitting rate limits by processing data in smaller chunks with configurable delays.

```json
{
    "nodes": [
    {
        "parameters": {},
        "id": "35d05920-ad75-402a-be3c-3277bff7cc67",
        "name": "When clicking ‘Execute workflow’",
        "type": "n8n-nodes-base.manualTrigger",
        "typeVersion": 1,
        "position": [
        880,
        400
        ]
    },
    {
        "parameters": {
        "batchSize": 500,
        "options": {}
        },
        "id": "ae9baa80-4cf9-4848-8953-22e1b7187bf6",
        "name": "Loop Over Items",
        "type": "n8n-nodes-base.splitInBatches",
        "typeVersion": 3,
        "position": [
        1120,
        420
        ]
    },
    {
        "parameters": {
        "resource": "chat",
        "options": {},
        "requestOptions": {}
        },
        "id": "a519f271-82dc-4f60-8cfd-533dec580acc",
        "name": "OpenAI",
        "type": "n8n-nodes-base.openAi",
        "typeVersion": 1,
        "position": [
        1380,
        440
        ]
    },
    {
        "parameters": {
        "unit": "minutes"
        },
        "id": "562d9da3-2142-49bc-9b8f-71b0af42b449",
        "name": "Wait",
        "type": "n8n-nodes-base.wait",
        "typeVersion": 1,
        "position": [
        1620,
        440
        ],
        "webhookId": "714ab157-96d1-448f-b7f5-677882b92b13"
    }
    ],
    "connections": {
    "When clicking ‘Execute workflow’": {
        "main": [
        [
            {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
            }
        ]
        ]
    },
    "Loop Over Items": {
        "main": [
        null,
        [
            {
            "node": "OpenAI",
            "type": "main",
            "index": 0
            }
        ]
        ]
    },
    "OpenAI": {
        "main": [
        [
            {
            "node": "Wait",
            "type": "main",
            "index": 0
            }
        ]
        ]
    },
    "Wait": {
        "main": [
        [
            {
            "node": "Loop Over Items",
            "type": "main",
            "index": 0
            }
        ]
        ]
    }
    },
    "pinData": {}
}
```

--------------------------------

### Mount Custom Certificates via Docker Compose

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/custom-certificate-authority

Configures volume mapping within a docker-compose.yml file to persist and mount custom certificates into the n8n service.

```yaml
name: n8n
services:
    n8n:
        volumes:
            - ./pki:/opt/custom-certificates
        container_name: n8n
        ports:
            - 5678:5678
        image: docker.n8n.io/n8nio/n8n
```

--------------------------------

### Find Notion User ID from Slack Email (JavaScript)

Source: https://docs.n8n.io/code/ai-code

This snippet demonstrates how to find a Notion user's ID by matching their email with a Slack user's email. It accesses data from a 'Mock Slack' node and the input data from preceding nodes. The function handles cases where the 'person' property (containing the email) might be null in the Notion data. It returns an array containing the notionId if a match is found, otherwise an empty array.

```javascript
const slackUser = $("Mock Slack").all()[0];
const notionUsers = $input.all();
const slackUserEmail = slackUser.json.email;

const notionUser = notionUsers.find(
  (user) => user.json.person && user.json.person.email === slackUserEmail
);

return notionUser ? [{ json: { notionId: notionUser.json.id } }] : [];
```

--------------------------------

### Executions API

Source: https://docs.n8n.io/release-notes/1-x

This section details updates to the n8n Executions API, including new fields in the execution details endpoint, a new endpoint for retrying failed executions, and additional filtering capabilities.

```APIDOC
## GET /executions

### Description
Retrieves details for executions. This endpoint now includes `status` and `workflow_name` in the response.

### Method
GET

### Endpoint
/executions

### Query Parameters
- **status** (string) - Optional - Filter executions by running or canceled status.

### Response
#### Success Response (200)
- **status** (string) - The current status of the execution.
- **workflow_name** (string) - The name of the workflow associated with the execution.

#### Response Example
```json
{
  "data": [
    {
      "id": "123e4567-e89b-12d3-a456-426614174000",
      "workflow_name": "My Workflow",
      "status": "running",
      "started_at": "2025-09-19T10:00:00Z",
      "finished_at": null
    }
  ]
}
```
```

```APIDOC
## POST /executions/{id}/retry

### Description
Retries a failed execution.

### Method
POST

### Endpoint
/executions/{id}/retry

### Path Parameters
- **id** (string) - Required - The ID of the execution to retry.

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the execution has been retried.

#### Response Example
```json
{
  "message": "Execution 123e4567-e89b-12d3-a456-426614174000 has been retried."
}
```
```

--------------------------------

### Create and Activate n8n Workflow via REST API

Source: https://docs.n8n.io/embed/managing-workflows

Demonstrates the API endpoints for creating a new workflow and updating its status to active. The creation process requires a JSON payload representing the workflow structure, while the activation process uses a PATCH request.

```HTTP
POST https://<n8n-domain>/rest/workflows/
```

```HTTP
PATCH https://<n8n-domain>/rest/workflows/1012
```

```JSON
// ...
"active":true,
"settings": {},
"staticData": null,
"tags": []
```

--------------------------------

### Implement execute method for n8n node

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

The execute method processes incoming data and performs API requests. It iterates through input items, retrieves node parameters, and uses helper methods to execute authenticated HTTP requests.

```TypeScript
const items = this.getInputData();
let responseData;
const returnData: INodeExecutionData[] = [];
const resource = this.getNodeParameter('resource', 0);
const operation = this.getNodeParameter('operation', 0);

for (let i = 0; i < items.length; i++) {
	try {
		if (resource === 'contact') {
			if (operation === 'create') {
				const email = this.getNodeParameter('email', i);
				const additionalFields = this.getNodeParameter('additionalFields', i);
				const data: IDataObject = { email };
				Object.assign(data, additionalFields);

				const options: IHttpRequestOptions = {
					headers: { 'Accept': 'application/json' },
					method: 'PUT',
					body: { contacts: [data] },
					url: 'https://api.sendgrid.com/v3/marketing/contacts',
					json: true,
				};
				responseData = await this.helpers.httpRequestWithAuthentication.call(this, 'friendGridApi', options);
				const executionData = this.helpers.constructExecutionMetaData(
					this.helpers.returnJsonArray(responseData as IDataObject),
					{ itemData: { item: i } },
				);
				returnData.push.apply(returnData, executionData);
			}
		}
	} catch (error) {
		if (this.continueOnFail()) {
			const executionData = this.helpers.constructExecutionMetaData(
				this.helpers.returnJsonArray({ error: error.message }),
				{ itemData: { item: i } },
			);
			returnData.push.apply(returnData, executionData);
			continue;
		}
		throw error;
	}
}
return [returnData];
```

--------------------------------

### JMESPath Query Methods

Source: https://docs.n8n.io/code/builtin/jmespath

Methods used to execute JMESPath queries against JSON data structures within n8n code nodes.

```APIDOC
## $jmespath() / _jmespath()

### Description
These methods allow you to perform a search or query on a JSON object using the JMESPath library syntax. They are primarily used within n8n Code nodes to extract or filter data from complex JSON structures.

### Method
Internal Function Call

### Parameters
#### Request Body
- **jsonObject** (object) - Required - The JSON object to query.
- **expression** (string) - Required - The JMESPath query string.

### Request Example
```javascript
// Example usage in a Code node
const data = { "people": [{ "name": "John" }, { "name": "Jane" }] };
const result = $jmespath(data, "people[*].name");
```

### Response
#### Success Response (200)
- **result** (any) - The data extracted based on the provided JMESPath expression.

#### Response Example
```json
["John", "Jane"]
```
```

--------------------------------

### Workflow Diff Enhancements

Source: https://docs.n8n.io/release-notes/1-x

Details on improvements made to the workflow diff functionality, including enhanced viewing in Code and Stickies nodes, and the ability to enable/disable sync in the viewport.

```APIDOC
## Workflow Diff Viewing

### Description
Enhancements to how workflow differences are displayed, providing more granular insights.

### Details
- **Line-by-line highlighting**: Changes in Code nodes and Stickies are now highlighted per line, improving readability.
- **Viewport sync control**: Users can now enable or disable sync in the viewport, allowing for independent comparison of workflow changes.
```

--------------------------------

### Set n8n Reverse Proxy Environment Variables

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/webhook-url

Configure n8n to work behind a reverse proxy by setting the `WEBHOOK_URL` and `N8N_PROXY_HOPS` environment variables. `WEBHOOK_URL` manually sets the webhook URL, and `N8N_PROXY_HOPS` enables proxy hop support.

```bash
export WEBHOOK_URL=https://n8n.example.com/
export N8N_PROXY_HOPS=1
```

--------------------------------

### Pull and Update n8n Docker Image

Source: https://docs.n8n.io/hosting/installation/docker

This snippet shows how to pull the latest 'next' version of the n8n Docker image. After pulling, you need to stop and restart your existing n8n container to use the updated image.

```bash
docker pull docker.n8n.io/n8nio/n8n:next
```

--------------------------------

### Customize Sidebar Logo Styles

Source: https://docs.n8n.io/embed/white-labelling

Adjusting the CSS/SCSS styles for logo components within the Vue.js frontend to accommodate custom branding assets.

```scss
.logoItem {
	display: flex;
	justify-content: space-between;
	height: $header-height;
	line-height: $header-height;
	margin: 0 !important;
	border-radius: 0 !important;
	border-bottom: var(--border-width-base) var(--border-style-base) var(--color-background-xlight);
	cursor: default;

	&:hover, &:global(.is-active):hover {
		background-color: initial !important;
	}

	* { vertical-align: middle; }
	.icon {
		height: 18px;
		position: relative;
		left: 6px;
	}
}
```

--------------------------------

### Configure GPT-4 Language Model with n8n

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/let_your_ai_call_an_api.json

Configures the GPT-4 language model for use within n8n workflows. It specifies the model name and allows for additional options. This node is part of the Langchain integration.

```json
{
  "model": "gpt-4",
  "options": {}
}
```

--------------------------------

### Fix KoBoToolbox Node Query and Sort

Source: https://docs.n8n.io/release-notes/0-x

The KoBoToolbox Node has been fixed to correctly handle query and sort parameters. It also now uses the question name in attachments, improving data retrieval and organization.

```javascript
KoBoToolbox Node: Fix query and sort + use question name in attachments.
```

--------------------------------

### Define Resource Mapper Interfaces

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

Interfaces for configuring resource mapper behavior and defining the schema fields returned by the mapper method. These are essential for nodes that support dynamic field mapping.

```typescript
export interface ResourceMapperTypeOptions {
	resourceMapperMethod: string;
	mode: 'add' | 'update' | 'upsert';
	fieldWords?: { singular: string; plural: string };
	addAllFields?: boolean;
	noFieldsError?: string;
	multiKeyMatch?: boolean;
	supportAutoMap?: boolean;
	matchingFieldsLabels?: {
		title?: string;
		description?: string;
		hint?: string;
	};
}

interface ResourceMapperField {
	id: string;
	displayName: string;
	defaultMatch: boolean;
	canBeUsedToMatch?: boolean;
	required: boolean;
	display: boolean;
	type?: FieldType;
	removed?: boolean;
	options?: INodePropertyOptions[];
}
```

--------------------------------

### Manage LangChain Node Data and Execution

Source: https://docs.n8n.io/code/builtin/langchain-methods

Methods for populating, retrieving, and controlling data flow within the LangChain Code node. These functions allow for mocking input/output data and handling execution cancellation signals.

```javascript
// Populate non-main input data
this.addInputData("ai_agent", data);

// Populate non-main output data
this.addOutputData("ai_chain", data);

// Get data from a specific non-main input
const inputData = this.getInputConnectionData("ai_document", 0);

// Get data from the main input
const mainData = this.getInputData();

// Retrieve current node and output configuration
const node = this.getNode();
const outputs = this.getNodeOutputs();

// Handle execution cancellation
const signal = this.getExecutionCancelSignal();
```

--------------------------------

### Configure Resource Locator in n8n

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

Defines a resource locator element that allows users to select resources using IDs, URLs, or prepopulated lists. It supports validation via regex and custom search methods for list-based selections.

```typescript
{
	displayName: 'Card',
	name: 'cardID',
	type: 'resourceLocator',
	default: '',
	description: 'Get a card',
	modes: [
		{
			displayName: 'ID',
			name: 'id',
			type: 'string',
			hint: 'Enter an ID',
			validation: [
				{
					type: 'regex',
					properties: {
						regex: '^[0-9]',
						errorMessage: 'The ID must start with a number',
					},
				},
			],
			placeholder: '12example',
			url: '=http://api-base-url.com/?id={{$value}}',
		},
		{
			displayName: 'URL',
			name: 'url',
			type: 'string',
			hint: 'Enter a URL',
			validation: [
				{
					type: 'regex',
					properties: {
						regex: '^http',
						errorMessage: 'Invalid URL',
					},
				},
			],
			placeholder: 'https://example.com/card/12example/',
			extractValue: {
				type: 'regex',
				regex: 'example.com/card/([0-9]*.*)/',
			},
		},
		{
			displayName: 'List',
			name: 'list',
			type: 'list',
			typeOptions: {
				searchListMethod: 'searchMethod',
				searchable: true,
				searchFilterRequired: true,
			},
		},
	],
	displayOptions: {
		show: {
			resource: [],
			operation: [],
		},
	},
}
```

--------------------------------

### String match() - Find matches against a regular expression

Source: https://docs.n8n.io/data/expression-reference/string

Searches a string for matches against a regular expression. It returns an array of matches, or null if no matches are found. The 'g' flag finds all matches, while its absence finds only the first.

```javascript
// Match all words starting with 'r'
"rock and roll".match(/r[^ ]*/g) //=> ['rock', 'roll']

// Match first word starting with 'r' (no 'g' flag)
"rock and roll".match(/r[^ ]*/) //=> ['rock']

// For case-insensitive, add 'i' flag
"ROCK and roll".match(/r[^ ]*/ig) //=> ['ROCK', 'roll']
```

--------------------------------

### Join Array elements into a string

Source: https://docs.n8n.io/data/expression-reference/array

Creates and returns a new string by concatenating all of the elements in an array, separated by a specified separator string.

```JavaScript
const arr = ['Wind', 'Water', 'Fire'];
arr.join(" + "); // => 'Wind + Water + Fire'
arr.join(); // => 'Wind,Water,Fire'
```

--------------------------------

### Workflow Templates API Endpoints

Source: https://docs.n8n.io/embed/workflow-templates

This section details the available endpoints for interacting with the workflow templates API when embedding n8n. It includes endpoints for fetching template metadata, workflow data, searching templates, managing collections, and a health check.

```APIDOC
## GET /templates/workflows/<id>

### Description
Fetch template metadata for preview/browsing.

### Method
GET

### Endpoint
/templates/workflows/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the template.

### Response
#### Success Response (200)
- **template_metadata** (object) - Contains metadata for the template.
- **workflow** (object) - The workflow definition for the template.

#### Response Example
```json
{
  "template_metadata": {
    "id": "example_id",
    "name": "Example Workflow Template",
    "description": "A sample workflow template."
  },
  "workflow": {
    "nodes": [],
    "connections": {}
  }
}
```
```

```APIDOC
## GET /workflows/templates/<id>

### Description
Fetch workflow data to import onto the canvas.

### Method
GET

### Endpoint
/workflows/templates/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the template.

### Response
#### Success Response (200)
- **workflow** (object) - The workflow definition to be imported.

#### Response Example
```json
{
  "nodes": [],
  "connections": {}
}
```
```

```APIDOC
## GET /templates/search

### Description
Search for workflow templates based on various criteria.

### Method
GET

### Endpoint
/templates/search

### Parameters
#### Query Parameters
- **page** (integer) - Optional - The page of results to return.
- **rows** (integer) - Optional - The maximum number of results to return per page.
- **category** (string) - Optional - A comma-separated list of categories to search within.
- **search** (string) - Optional - The search query string.

### Response
#### Success Response (200)
- **templates** (array) - A list of matching workflow templates.

#### Response Example
```json
{
  "templates": [
    {
      "id": "example_id_1",
      "name": "Template One",
      "description": "First sample template."
    },
    {
      "id": "example_id_2",
      "name": "Template Two",
      "description": "Second sample template."
    }
  ]
}
```
```

```APIDOC
## GET /templates/collections/<id>

### Description
Get a specific template collection.

### Method
GET

### Endpoint
/templates/collections/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The unique identifier of the collection.

### Response
#### Success Response (200)
- **collection** (object) - The details of the template collection.

#### Response Example
```json
{
  "id": "collection_id",
  "name": "Example Collection",
  "description": "A collection of example templates.",
  "templates": []
}
```
```

```APIDOC
## GET /templates/collections

### Description
List all available template collections.

### Method
GET

### Endpoint
/templates/collections

### Parameters
#### Query Parameters
- **category** (string) - Optional - A comma-separated list of categories to filter collections by.
- **search** (string) - Optional - The search query string for collection names or descriptions.

### Response
#### Success Response (200)
- **collections** (array) - A list of template collections.

#### Response Example
```json
{
  "collections": [
    {
      "id": "collection_id_1",
      "name": "Collection A"
    },
    {
      "id": "collection_id_2",
      "name": "Collection B"
    }
  ]
}
```
```

```APIDOC
## GET /templates/categories

### Description
List all available template categories.

### Method
GET

### Endpoint
/templates/categories

### Response
#### Success Response (200)
- **categories** (array) - A list of template categories.

#### Response Example
```json
{
  "categories": [
    "Automation",
    "Data Processing",
    "Webhooks"
  ]
}
```
```

```APIDOC
## GET /health

### Description
Health check endpoint to verify the API is operational.

### Method
GET

### Endpoint
/health

### Response
#### Success Response (200)
- **status** (string) - Indicates the health status (e.g., "ok").

#### Response Example
```json
{
  "status": "ok"
}
```
```

--------------------------------

### Accessing and Managing Global Workflow Static Data

Source: https://docs.n8n.io/code/cookbook/builtin/get-workflow-static-data

Demonstrates how to retrieve, read, update, and delete global static data that is accessible by all nodes within a workflow. This data persists across executions, provided the workflow is active and triggered correctly.

```JavaScript
// Get the global workflow static data
const workflowStaticData = $getWorkflowStaticData('global');

// Access its data
const lastExecution = workflowStaticData.lastExecution;

// Update its data
workflowStaticData.lastExecution = new Date().getTime();

// Delete data
delete workflowStaticData.lastExecution;
```

```Python
# Get the global workflow static data
workflowStaticData = _getWorkflowStaticData('global')

# Access its data
lastExecution = workflowStaticData.lastExecution

# Update its data
workflowStaticData.lastExecution = new Date().getTime()

# Delete data
delete workflowStaticData.lastExecution
```

--------------------------------

### Mock Notion User Data with n8n Code Node

Source: https://docs.n8n.io/_workflows/ai-code/find-a-piece-of-data.json

This snippet generates a mock array of Notion user objects. It provides a simplified schema including user IDs, names, and nested email addresses for testing integration logic.

```javascript
return [
{
"object": "user",
"id": "1234",
"name": "Nathan Berlin",
"avatar_url": "https://example.jpeg",
"type": "person",
"person": {
"email": "nathan@example.io"
}
},
{
"object": "user",
"id": "5678",
"name": "Natalie Berlin",
"avatar_url": "https://example.jpeg",
"type": "person",
"person": {
"email": "natalie@example.io"
}
}
]
```

--------------------------------

### User Operations API

Source: https://docs.n8n.io/api/api-reference

This section details operations related to users within the n8n instance, including retrieving, creating, and managing user roles.

```APIDOC
## GET /users

### Description
Retrieve all users from your instance. Only available for the instance owner.

### Method
GET

### Endpoint
https://{instance}.app.n8n.cloud/api/v1/users

### Parameters
#### Query Parameters
- **limit** (number) - Optional - The maximum number of items to return. Max: 250, Default: 100.
- **cursor** (string) - Optional - Paginate by setting the cursor parameter to the nextCursor attribute returned by the previous request's response. Default value fetches the first "page" of the collection.
- **includeRole** (boolean) - Optional - Whether to include the user's role or not. Default: false.
- **projectId** (string) - Optional - Filters users by the specified project ID.

### Request Example
```curl
curl https://your-instance-name.app.n8n.cloud/api/v1/users \
  --header 'X-N8N-API-KEY: YOUR_SECRET_TOKEN'
```

### Response
#### Success Response (200)
- **data** (array object) - List of users.
  - **id** (string) - Unique identifier for the user.
  - **email** (string) - User's email address.
  - **firstName** (string) - User's first name.
  - **lastName** (string) - User's last name.
  - **isPending** (boolean) - Indicates if the user account is pending.
  - **createdAt** (string) - Timestamp when the user was created.
  - **updatedAt** (string) - Timestamp when the user was last updated.
  - **role** (string) - User's role within the instance.
- **nextCursor** (string) - Cursor for paginating to the next set of results.

#### Response Example
```json
{
  "data": [
    {
      "id": "123e4567-e89b-12d3-a456-426614174000",
      "email": "john.doe@company.com",
      "firstName": "john",
      "lastName": "Doe",
      "isPending": true,
      "createdAt": "2026-03-21T22:09:17.407Z",
      "updatedAt": "2026-03-21T22:09:17.407Z",
      "role": "global:owner"
    }
  ],
  "nextCursor": "MTIzZTQ1NjctZTg5Yi0xMmQzLWE0NTYtNDI2NjE0MTc0MDA"
}
```

#### Error Response (401)
Unauthorized.

## POST /users

### Description
Create one or more users.

### Method
POST

### Endpoint
https://{instance}.app.n8n.cloud/api/v1/users

### Parameters
#### Request Body
- **users** (array object[]) - Required - Array of users to be created.
  - **email** (string) - Required - User's email address.
  - **role** (string) - Optional - User's role. Default: "global:member".

### Request Example
```curl
curl https://your-instance-name.app.n8n.cloud/api/v1/users \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'X-N8N-API-KEY: YOUR_SECRET_TOKEN' \
  --data \
  '[{"email": "new.user@example.com", "role": "global:member"}]'
```

### Response
#### Success Response (200)
- **user** (object) - Details of the created user.
  - **id** (string) - Unique identifier for the user.
  - **email** (string) - User's email address.
  - **inviteAcceptUrl** (string) - URL to accept the invitation.
  - **emailSent** (boolean) - Indicates if the invitation email was sent.
- **error** (string) - Error message if creation failed.

#### Response Example
```json
{
  "user": {
    "id": "string",
    "email": "string",
    "inviteAcceptUrl": "string",
    "emailSent": true
  },
  "error": "string"
}
```

#### Error Response (401)
Unauthorized.

#### Error Response (403)
Forbidden.

## GET /users/{id}

### Description
Retrieve a specific user by their ID.

### Method
GET

### Endpoint
https://{instance}.app.n8n.cloud/api/v1/users/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the user to retrieve.

### Response
#### Success Response (200)
- **id** (string) - Unique identifier for the user.
- **email** (string) - User's email address.
- **firstName** (string) - User's first name.
- **lastName** (string) - User's last name.
- **isPending** (boolean) - Indicates if the user account is pending.
- **createdAt** (string) - Timestamp when the user was created.
- **updatedAt** (string) - Timestamp when the user was last updated.
- **role** (string) - User's role within the instance.

#### Error Response (401)
Unauthorized.

#### Error Response (404)
User not found.

## DELETE /users/{id}

### Description
Delete a user by their ID.

### Method
DELETE

### Endpoint
https://{instance}.app.n8n.cloud/api/v1/users/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the user to delete.

### Response
#### Success Response (200)
Operation successful.

#### Error Response (401)
Unauthorized.

#### Error Response (403)
Forbidden.

#### Error Response (404)
User not found.

## PATCH /users/{id}/role

### Description
Update the role of a specific user.

### Method
PATCH

### Endpoint
https://{instance}.app.n8n.cloud/api/v1/users/{id}/role

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the user whose role to update.
#### Request Body
- **role** (string) - Required - The new role for the user (e.g., "global:member", "global:admin").

### Response
#### Success Response (200)
Operation successful.

#### Error Response (401)
Unauthorized.

#### Error Response (403)
Forbidden.

#### Error Response (404)
User not found.
```

--------------------------------

### Define Number Input UI Element

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

Configuration for numeric inputs with validation constraints such as minimum/maximum values and decimal precision.

```JSON
{
	displayName: 'Amount',
	name: 'amount',
	type: 'number',
	required: true,
	typeOptions: {
		maxValue: 10,
		minValue: 0,
		numberPrecision: 2
	},
	default: 10.00,
	description: 'Your current amount',
	displayOptions: {
		show: {
			resource: [],
			operation: []
		}
	}
}
```

--------------------------------

### Initialize NodeApiError

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/error-handling

Instantiate NodeApiError for API-related errors. It requires the node instance, the error response from an API, and optional configuration for message and description.

```typescript
new NodeApiError(node: INode, errorResponse: JsonObject, options?: NodeApiErrorOptions)
```

--------------------------------

### Set Credential Overwrite Endpoint (Bash)

Source: https://docs.n8n.io/embed/configuration

This snippet demonstrates how to set the environment variable `CREDENTIALS_OVERWRITE_ENDPOINT` to activate a custom REST endpoint for loading credential overwrites. This is the recommended method for applying credential overwrites.

```bash
export CREDENTIALS_OVERWRITE_ENDPOINT=send-credentials
```

--------------------------------

### PATCH /files/{fileId}

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive/file-operations

Updates an existing file's metadata or content in Google Drive.

```APIDOC
## PATCH /files/{fileId}

### Description
Updates the properties, content, or metadata of an existing file in Google Drive.

### Method
PATCH

### Endpoint
/files/{fileId}

### Parameters
#### Path Parameters
- **fileId** (string) - Required - The unique identifier of the file to update.

#### Request Body
- **name** (string) - Optional - The new name for the file.
- **binaryData** (binary) - Optional - New binary content to replace existing data.
- **properties** (object) - Optional - Key-value pairs visible to all apps.
- **appProperties** (object) - Optional - Private key-value pairs for the requesting app.
- **keepRevisionForever** (boolean) - Optional - Whether to set the keepForever field for binary content.

### Request Example
{
  "name": "updated_document.pdf",
  "properties": {
    "status": "final"
  }
}

### Response
#### Success Response (200)
- **id** (string) - The ID of the updated file.
- **name** (string) - The updated name of the file.

#### Response Example
{
  "id": "1abc123...",
  "name": "updated_document.pdf"
}
```

--------------------------------

### Map Array Elements in JavaScript

Source: https://docs.n8n.io/data/expression-reference/array

The `map()` method creates a new array by applying a function to each element of the original array. It accepts a callback function and an optional `thisValue`. The callback function receives the element, index, and the array itself.

```javascript
// Double all numbers (using arrow function notation):
// nums = [12, 33, 16]
nums.map(num => num*2) //=> [24, 66, 32]
```

```javascript
// Convert elements to uppercase (using arrow function notation):
// words = ['hello', 'old', 'chap']
words.map(word => word.toUpperCase()) //=> ['HELLO', 'OLD', 'CHAP']]

// Or using traditional function notation:
words.map(function(word){return word.toUpperCase()}) //=> ['HELLO', 'OLD', 'CHAP']]
```

--------------------------------

### Generate URL Encoded String from Object

Source: https://docs.n8n.io/data/expression-reference/object

The urlEncode() method transforms an Object into a URL parameter string. It processes only top-level keys and values, returning a string formatted for URL query parameters.

```javascript
// obj = {'name':'Mr Nathan', 'city':'hanoi'}
obj.urlEncode() //=> 'name=Mr+Nathan&city=hanoi'
```

--------------------------------

### Mock Data Generation using JavaScript in n8n

Source: https://docs.n8n.io/_workflows/ai-code/summarize-data.json

This JavaScript code snippet is used within an n8n 'code' node to generate mock data. It returns an array of objects, each representing a feature, bug, or idea with properties like id, name, url, type, and votes. This is useful for testing or simulating data.

```javascript
return [
{
"id":
"0001",
"name":
"Example feature 1",
"url": "example.com",
"property_tags":
[
],
"property_type":
[
"Feature"
],
"property_votes":
2
},
{
"id":
"0002",
"name":
"Example feature 2",
"url": "example.com",
"property_type":
[
"Feature"
],
"property_votes":
3
},
{
"id":
"0003",
"name":
"Example feature 3",
"url": "example.com",
"property_type":
[
"Feature"
],
"property_votes":
1
},
{
"id":
"0004",
"name":
"Example bug 1",
"url": "example.com",
"property_type":
[
"Bug"
],
"property_votes":
0
},
{
"id":
"0005",
"name":
"Example idea 1",
"url": "example.com",
"property_type":
[
"Idea"
],
"property_votes":
4
}
]
```

--------------------------------

### Configure Content Security Policy (CSP) in n8n

Source: https://docs.n8n.io/hosting/configuration/environment-variables/security

Sets Content-Security-Policy headers using helmet.js nested directives. This helps mitigate cross-site scripting (XSS) and other code injection attacks. The configuration is provided as a JSON object.

```json
{
  "frame-ancestors": ["http://localhost:3000"]
}
```

--------------------------------

### Manage Execution Metadata with $execution

Source: https://docs.n8n.io/data/expression-reference/root

Allows retrieval or setting of metadata for the current execution. This function returns ExecData and is part of n8n's custom functionality.

```javascript
function manageExecutionMetadata() {
  // Example usage: retrieve execution metadata
  return $execution;
}
```

--------------------------------

### Convert JsProxy to Python Dict in n8n

Source: https://docs.n8n.io/code/cookbook/code-node/console-log

This snippet demonstrates how to convert a JsProxy object, commonly encountered when accessing n8n node data, into a native Python dictionary. This is essential for processing data from previous nodes in a workflow. It assumes the `_` function is available for node data retrieval.

```python
previousNodeData = _("<node-name>").all()
for item in previousNodeData:
	# item is of type <class 'pyodide.ffi.JsProxy'>
	# You need to convert it to a Dict
	itemDict = item.json.to_py()
	print(itemDict)
```

--------------------------------

### Define Optional Node Fields

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Defines an 'Additional Fields' collection in the n8n node properties. This allows users to input a date parameter which is dynamically converted to an ISO string for API query requests.

```typescript
{
	displayName: 'Additional Fields',
	name: 'additionalFields',
	type: 'collection',
	default: {},
	placeholder: 'Add Field',
	displayOptions: {
		show: {
			resource: [
				'astronomyPictureOfTheDay',
			],
			operation: [
				'get',
			],
		},
	},
	options: [
		{
			displayName: 'Date',
			name: 'apodDate',
			type: 'dateTime',
			default: '',
			routing: {
				request: {
					qs: {
						date: '={{ new Date($value).toISOString().substr(0,10) }}',
					},
				},
			},
		},
	],									
}
```

--------------------------------

### Convert Date to Luxon DateTime with n8n

Source: https://docs.n8n.io/data/expression-reference/date

This snippet demonstrates how to convert a JavaScript Date object to a Luxon DateTime object using the custom `toDateTime()` method provided by n8n. The resulting DateTime object offers more advanced manipulation options, such as adding days. This function is part of n8n's custom functionality.

```javascript
date = new Date("2024-03-30T18:49")
date.toDateTime().plus(5, 'days') //=> 2024-05-05T18:49
```

--------------------------------

### Compare DateTime Equality with Unit - Luxon

Source: https://docs.n8n.io/data/expression-reference/datetime

Checks if two DateTime objects are the same down to a specified unit. Time zones are ignored, so UTC conversion might be necessary. Accepts another DateTime object and a unit string ('year', 'month', 'day', etc.) as parameters.

```javascript
// dt1 = "2024-03-20".toDateTime()
// dt2 = "2024-03-18".toDateTime()
dt1.hasSame(dt2, 'month') //=> true

// dt1 = "1982-03-20".toDateTime()
// dt2 = "2024-03-18".toDateTime()
dt1.hasSame(dt2, 'month') //=> false
```

--------------------------------

### Retrieve MySQL Connection Metadata

Source: https://docs.n8n.io/integrations/builtin/credentials/mysql

SQL queries used to identify specific database server properties such as the hostname, database list, port number, and connection timeout settings required for n8n credential configuration.

```sql
SHOW VARIABLES WHERE Variable_name = 'hostname';
SHOW DATABASES;
SHOW VARIABLES WHERE Variable_name = 'port';
SHOW VARIABLES WHERE Variable_name = 'connect_timeout';
```

--------------------------------

### Mock Slack User Data with n8n Code Node

Source: https://docs.n8n.io/_workflows/ai-code/find-a-piece-of-data.json

This snippet defines a JavaScript object structure that mimics a Slack user profile. It returns an array of objects containing user details like name, email, and avatar information to be used as mock input for downstream nodes.

```javascript
return [
{
"title": "",
"phone": "",
"skype": "",
"real_name": "Nathan Berlin",
"email": "nathan@example.io",
"real_name_normalized": "Nathan Berlin",
"display_name": "Nathan Berlin",
"display_name_normalized": "Nathan Berlin",
"fields": {},
"status_text": "",
"status_emoji": "",
"status_emoji_display_info": [],
"status_expiration": 0,
"avatar_hash": "0856f5fbbd43",
"image_original": "https://example.png",
"is_custom_image": true,
"huddle_state": "default_unset",
"huddle_state_expiration_ts": 0,
"first_name": "Nathan",
"last_name": "Berlin",
"image_24": "https://example.png",
"image_32": "https://example.png",
"image_48": "https://example.png",
"image_72": "https://example.png",
"image_192": "https://example.png",
"image_512": "https://example.png",
"image_1024": "https://example.png",
"status_text_canonical": ""
}
]
```

--------------------------------

### OAuth2 Client Credentials Grant Type Configuration

Source: https://docs.n8n.io/integrations/builtin/credentials/httprequest

Configures OAuth2 using the Client Credentials grant type for applications accessing their own resources. Requires an Access Token URL, Client ID, Client Secret, and optionally Scopes and Authentication type (Header or Body). SSL issues can be ignored.

```text
Access Token URL: [URL]
Client ID: [ID]
Client Secret: [Secret]
Scope: [Scope(s)] (Optional)
Authentication: Header or Body
Ignore SSL Issues: true or false (Optional)
```

--------------------------------

### Add Region Selection to Google Cloud Realtime Database Node

Source: https://docs.n8n.io/release-notes/0-x

Users can now select a region for the Google Cloud Realtime Database node. This enhancement allows for better performance and data locality by choosing the most appropriate region for database operations.

```javascript
Google Cloud Realtime Database node: you can now select a region.
```

--------------------------------

### Define n8n Node Class and Metadata

Source: https://docs.n8n.io/integrations/creating-nodes/build/declarative-style-node

Implementation of the node class using TypeScript, including the required INodeType interface and the description object that configures node behavior and UI properties.

```typescript
import { NodeConnectionTypes } from 'n8n-workflow';
import type { INodeType, INodeTypeDescription } from 'n8n-workflow';

export class NasaPics implements INodeType {
	description: INodeTypeDescription = {
		displayName: 'NASA Pics',
		name: 'nasaPics',
		icon: 'file:nasapics.svg',
		group: ['transform'],
		version: 1,
		subtitle: '={{$parameter["operation"] + ": " + $parameter["resource"]}}',
		description: 'Get data from NASAs API',
		defaults: {
			name: 'NASA Pics',
		},
		usableAsTool: true,
		inputs: [ NodeConnectionTypes.Main ],
		outputs: [ NodeConnectionTypes.Main ],
		credentials: [
			{
				name: 'NasaPicsApi',
				required: true,
			},
		],
		requestDefaults: {
			baseURL: 'https://api.nasa.gov',
			headers: {
				Accept: 'application/json',
				'Content-Type': 'application/json',
			},
		},
		properties: []
	};
}
```

--------------------------------

### n8n Workflow JSON for RSS Feed Processing

Source: https://docs.n8n.io/courses/level-two/chapter-3

This JSON represents a complete n8n workflow designed to read RSS feeds. It includes a manual trigger, a Code node for generating URLs, a Loop Over Items node for batch processing, and an RSS Read node for fetching feed content. This structure allows for automated fetching and processing of multiple RSS feed items.

```json
{
"meta": {
	"templateCredsSetupCompleted": true,
	"instanceId": "cb484ba7b742928a2048bf8829668bed5b5ad9787579adea888f05980292a4a7"
},
"nodes": [
	{
	"parameters": {},
	"id": "ed8dc090-ae8c-4db6-a93b-0fa873015c25",
	"name": "When clicking \"Execute workflow\"",
	"type": "n8n-nodes-base.manualTrigger",
	"typeVersion": 1,
	"position": [
		460,
		460
	]
	},
	{
	"parameters": {
		"jsCode": "let urls = [\n  {\n    json: {\n      url: 'https://medium.com/feed/n8n-io'\n    }\n  },\n  {\n   json: {\n     url: 'https://dev.to/feed/n8n'\n   } \n  }\n]\n\nreturn urls;"
	},
	"id": "1df2a9bf-f970-4e04-b906-92dbbc9e8d3a",
	"name": "Code",
	"type": "n8n-nodes-base.code",
	"typeVersion": 2,
	"position": [
		680,
		460
	]
	},
	{
	"parameters": {
		"options": {}
	},
	"id": "3cce249a-0eab-42e2-90e3-dbdf3684e012",
	"name": "Loop Over Items",
	"type": "n8n-nodes-base.splitInBatches",
	"typeVersion": 3,
	"position": [
		900,
		460
	]
	},
	{
	"parameters": {
		"url": "={{ $json.url }}",
		"options": {}
	},
	"id": "50e1c1dc-9a5d-42d3-b7c0-accc31636aa6",
	"name": "RSS Read",
	"type": "n8n-nodes-base.rssFeedRead",
	"typeVersion": 1,
	"position": [
		1120,
		460
	]
	}
],
"connections": {
	"When clicking \"Execute workflow\"": {
	"main": [
		[
		{
			"node": "Code",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"Code": {
	"main": [
		[
		{
			"node": "Loop Over Items",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"Loop Over Items": {
	"main": [
		null,
		[
		{
			"node": "RSS Read",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"RSS Read": {
	"main": [
		[
		{
			"node": "Loop Over Items",
			"type": "main",
			"index": 0
		}
		]
	]
	}
},
"pinData": {}
}
```

--------------------------------

### Create User Credentials API

Source: https://docs.n8n.io/embed/managing-workflows

This API endpoint allows for the creation of new service credentials for a user within n8n. It is an alternative to using the Editor UI for credential management.

```APIDOC
## POST /rest/credentials

### Description
Creates new service credentials for a user in n8n.

### Method
POST

### Endpoint
`https://<n8n-domain>/rest/credentials`

### Parameters
#### Request Body
- **name** (string) - Required - A name for the credentials.
- **type** (string) - Required - The type of credential (e.g., "airtableApi").
- **nodesAccess** (array) - Required - An array of objects specifying which nodes can access these credentials.
  - **nodeType** (string) - Required - The type of the node (e.g., "n8n-nodes-base.airtable").
- **data** (object) - Required - An object containing the actual credential data.
  - **apiKey** (string) - Required - The API key for the service (example).

### Request Example
```json
{
   "name":"MyAirtable",
   "type":"airtableApi",
   "nodesAccess":[
      {
         "nodeType":"n8n-nodes-base.airtable"
      }
   ],
   "data":{
      "apiKey":"q12we34r5t67yu"
   }
}
```

### Response
#### Success Response (200)
- **data** (object) - Contains the details of the newly created credentials.
  - **name** (string) - The name of the credentials.
  - **type** (string) - The type of the credential.
  - **data** (object) - The credential data.
  - **nodesAccess** (array) - Nodes that have access to these credentials.
  - **id** (string) - The unique identifier for the credentials.
  - **createdAt** (string) - Timestamp when the credentials were created.
  - **updatedAt** (string) - Timestamp when the credentials were last updated.

#### Response Example
```json
{
   "data":{
      "name":"MyAirtable",
      "type":"airtableApi",
      "data":{
         "apiKey":"q12we34r5t67yu"
      },
      "nodesAccess":[
         {
            "nodeType":"n8n-nodes-base.airtable",
            "date":"2021-09-10T07:41:27.770Z"
         }
      ],
      "id":"29",
      "createdAt":"2021-09-10T07:41:27.777Z",
      "updatedAt":"2021-09-10T07:41:27.777Z"
   }
}
```
```

--------------------------------

### n8n Workflow JSON Configuration

Source: https://docs.n8n.io/_workflows/try-it-out/quickstart/tutorial.json

This JSON object defines the complete n8n workflow, including nodes for scheduling, NASA API integration, conditional logic, and external HTTP requests via PostBin. It requires valid NASA credentials and a configured PostBin ID to function correctly.

```json
{
  "name": "Tutorial-workflow",
  "nodes": [
    {
      "parameters": {
        "rule": {
          "interval": [
            {
              "field": "weeks",
              "triggerAtDay": [1],
              "triggerAtHour": 9
            }
          ]
        }
      },
      "type": "n8n-nodes-base.scheduleTrigger",
      "name": "Schedule Trigger"
    },
    {
      "parameters": {
        "resource": "donkiSolarFlare",
        "additionalFields": {
          "startDate": "={{ $today.minus(7, 'days') }}"
        }
      },
      "type": "n8n-nodes-base.nasa",
      "name": "NASA"
    },
    {
      "parameters": {
        "conditions": {
          "conditions": [
            {
              "leftValue": "={{ $json.classType }}",
              "rightValue": "C",
              "operator": { "type": "string", "operation": "contains" }
            }
          ]
        }
      },
      "type": "n8n-nodes-base.if",
      "name": "If"
    }
  ]
}
```

--------------------------------

### POST /rest/workflows

Source: https://docs.n8n.io/embed/managing-workflows

Creates a new workflow in the n8n instance using a JSON workflow definition.

```APIDOC
## POST /rest/workflows

### Description
Creates a new workflow by submitting a JSON object representing the workflow structure, nodes, and connections.

### Method
POST

### Endpoint
https://<n8n-domain>/rest/workflows

### Request Body
- **nodes** (array) - Required - The list of nodes and their configurations.
- **connections** (object) - Required - The mapping of node connections.
- **settings** (object) - Optional - Workflow settings.

### Request Example
{
  "nodes": [],
  "connections": {},
  "settings": {}
}

### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the created workflow.

#### Response Example
{
  "id": "1012"
}
```

--------------------------------

### Update n8n Docker Container

Source: https://docs.n8n.io/hosting/installation/server-setups/digital-ocean

A sequence of commands to pull the latest image, remove the existing container, and restart the service to apply updates.

```bash
cd </path/to/your/compose/file/directory>
docker compose pull
docker compose down
docker compose up -d
```

--------------------------------

### Test Credential Request Object (TypeScript)

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/credentials-files

Defines a `request` object for testing n8n credentials. It includes the base URL and the specific endpoint for the test request. The `baseURL` can dynamically reference credential values like `$credentials?.domain`.

```typescript
test: ICredentialTestRequest = {
		request: {
			baseURL: '={{$credentials?.domain}}',
			url: '/bearer',
		},
	};
```

--------------------------------

### Check if Object is Not Empty (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/object

The `isNotEmpty()` method returns `true` if the object has at least one key. Otherwise, it returns `false`. This is a custom n8n functionality.

```javascript
// obj = {'name': 'Nathan'}
obj.isNotEmpty() //=> true

// obj = {}
obj.isNotEmpty() //=> false
```

--------------------------------

### PATCH /drives/{driveId}

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive/shared-drive-operations

Updates the properties of an existing shared drive.

```APIDOC
## PATCH /drives/{driveId}

### Description
Updates the metadata of a specified shared drive.

### Method
PATCH

### Endpoint
/drives/{driveId}

### Parameters
#### Path Parameters
- **driveId** (string) - Required - The ID of the drive to update.

#### Request Body
- **name** (string) - Optional - The new name for the shared drive.

### Request Example
{
  "name": "Updated Project Drive"
}

### Response
#### Success Response (200)
- **id** (string) - The ID of the updated drive.
- **name** (string) - The updated name.
```

--------------------------------

### Configure File-Based Environment Variables in n8n

Source: https://docs.n8n.io/hosting/configuration/environment-variables/security

Allows sensitive configuration to be stored in separate files by appending `_FILE` to environment variable names. This enhances security by keeping credentials out of direct environment variable lists. Refer to 'Keeping sensitive data in separate files' for more details.

```bash
# Example: Store N8N_API_KEY in a file
N8N_API_KEY_FILE=/path/to/your/n8n_api_key.txt
```

--------------------------------

### Make HTTP Request with Headers (n8n)

Source: https://docs.n8n.io/_workflows//courses/level-one/chapter-5/chapter-5.6.json

Configures an HTTP request node to send data to a specified URL. It supports authentication via HTTP headers and allows custom header parameters to be included in the request. This node is crucial for integrating with external APIs.

```json
{
  "parameters": {
    "url": "https://internal.users.n8n.cloud/webhook/custom-erp",
    "authentication": "genericCredentialType",
    "genericAuthType": "httpHeaderAuth",
    "sendHeaders": true,
    "headerParameters": {
      "parameters": [
        {
          "name": "unique_id",
          "value": "<YOUR_UNIQUE_ID_HERE>"
        }
      ]
    },
    "options": {}
  },
  "type": "n8n-nodes-base.httpRequest",
  "typeVersion": 4.2,
  "position": [
    300,
    -520
  ],
  "id": "ada6becf-c320-41a7-bdca-a842ea3ee769",
  "name": "HTTP Request1",
  "credentials": {
    "httpHeaderAuth": {
      "id": "sMuanZ4xGobAurzY",
      "name": "Nathan's ABCorp data warehouse account"
    }
  }
}
```

--------------------------------

### Output to Browser Console with print() (Python)

Source: https://docs.n8n.io/code/cookbook/code-node/console-log

Utilize the print() function in the n8n Code node to display variable contents or debug messages in the browser console when working with Python. Set the Code node's language to Python before executing.

```python
a = "apple"
print(a)
```

--------------------------------

### Support Temporary Credentials in AWS Nodes

Source: https://docs.n8n.io/release-notes/0-x

All AWS nodes now support AWS temporary credentials. This improves security and flexibility by allowing the use of short-lived credentials for accessing AWS services, which is a best practice for managing access in cloud environments.

```javascript
All AWS nodes now support AWS temporary credentials.
```

--------------------------------

### n8n Workflow Connections

Source: https://docs.n8n.io/courses/level-two/chapter-2

Defines the execution flow and connections between nodes in an n8n workflow. This JSON structure illustrates how different nodes are linked together to form a complete automated process.

```json
{
	"pinData": {},
	"connections": {
	"When clicking \"Execute workflow\"": {
	"main": [
		[
		{
			"node": "Customer Datastore (n8n training)",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"Customer Datastore (n8n training)": {
	"main": [
		[
		{
			"node": "Date & Time",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"Date & Time": {
	"main": [
		[
		{
			"node": "If",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"If": {
	"main": [
		[
		{
			"node": "Wait",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"Wait": {
	"main": [
		[
		{
			"node": "Edit Fields",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"Schedule Trigger": {
	"main": [
		[
		{
			"node": "Customer Datastore (n8n training)",
			"type": "main",
			"index": 0
		}
		]
	]
	}
}
}
```

--------------------------------

### Retrieve Postgres Server Port

Source: https://docs.n8n.io/integrations/builtin/credentials/postgres

SQL query to identify the port number currently being used by the database server.

```SQL
SELECT inet_server_port();
```

--------------------------------

### Retrieve Linked Items via itemMatching in n8n

Source: https://docs.n8n.io/data/data-mapping/itemmatching

Demonstrates how to iterate through input items and fetch corresponding data from a specific upstream node using the itemMatching method. This approach is essential for restoring or enriching data that was filtered or transformed in intermediate nodes.

```JavaScript
for(let i=0; i<$input.all().length; i++) {
	$input.all()[i].json.restoreEmail = $('Customer Datastore (n8n training)').itemMatching(i).json.email;
}
return $input.all();
```

```Python
for i,item in enumerate(_input.all()):
	_input.all()[i].json.restoreEmail = _('Customer Datastore (n8n training)').itemMatching(i).json.email

return _input.all();
```

--------------------------------

### Use Response URL for Pagination in HTTP Request

Source: https://docs.n8n.io/code/cookbook/http-node/pagination

Configure the HTTP Request node to use a URL provided in the API response to fetch the next page. This is useful when the API dynamically provides the link to the subsequent data set. Ensure the 'Response Contains Next URL' pagination mode is selected and the 'Next URL' expression correctly extracts the URL from the response body.

```javascript
{{ $response.body["next-page"] }}
```

--------------------------------

### Merge Data with n8n Workflow JSON

Source: https://docs.n8n.io/courses/level-two/chapter-3

This JSON represents an n8n workflow designed to merge data. It includes a manual trigger, a Customer Datastore node to fetch data, a Code node to generate data, and a Merge node to combine them. The Merge node is configured to combine data based on the 'name' field.

```json
{
"meta": {
	"templateCredsSetupCompleted": true,
	"instanceId": "cb484ba7b742928a2048bf8829668bed5b5ad9787579adea888f05980292a4a7"
},
"nodes": [
	{
	"parameters": {
		"mode": "combine",
		"mergeByFields": {
		"values": [
			{
			"field1": "name",
			"field2": "name"
			}
		]
		},
		"options": {}
	},
	"id": "578365f3-26dd-4fa6-9858-f0a5fdfc413b",
	"name": "Merge",
	"type": "n8n-nodes-base.merge",
	"typeVersion": 2.1,
	"position": [
		720,
		580
	]
	},
	{
	"parameters": {},
	"id": "71aa5aad-afdf-4f8a-bca0-34450eee8acc",
	"name": "When clicking \"Execute workflow\"",
	"type": "n8n-nodes-base.manualTrigger",
	"typeVersion": 1,
	"position": [
		260,
		560
	]
	},
	{
	"parameters": {
		"operation": "getAllPeople"
	},
	"id": "497174fe-3cab-4160-8103-78b44efd038d",
	"name": "Customer Datastore (n8n training)",
	"type": "n8n-nodes-base.n8nTrainingCustomerDatastore",
	"typeVersion": 1,
	"position": [
		500,
		460
	]
	},
	{
	"parameters": {
		"jsCode": "return [\n  {\n    'name': 'Jay Gatsby',\n    'language': 'English',\n    'country': {\n      'code': 'US',\n      'name': 'United States'\n    }\n    \n  }\n  \n];"
	},
	"id": "387e8a1e-e796-4f05-8e75-7ce25c786c5f",
	"name": "Code",
	"type": "n8n-nodes-base. n8n-nodes-base.code",
	"typeVersion": 2,
	"position": [
		500,
		720
	]
	}
],
"connections": {
	"When clicking \"Execute workflow\"": {
	"main": [
		[
		{
			"node": "Customer Datastore (n8n training)",
			"type": "main",
			"index": 0
		},
		{
			"node": "Code",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"Customer Datastore (n8n training)": {
	"main": [
		[
		{
			"node": "Merge",
			"type": "main",
			"index": 0
		}
		]
	]
	},
	"Code": {
	"main": [
		[
		{
			"node": "Merge",
			"type": "main",
			"index": 1
		}
		]
	]
	}
},
"pinData": {}
}
```

--------------------------------

### Execute JavaScript Code in n8n

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/ask_a_human.json

This node allows for custom JavaScript execution within an n8n workflow. It takes a 'jsCode' parameter which is a string containing the JavaScript code to be executed. The output is assigned to a 'response' variable.

```javascript
response = {"response": "Thank you for getting in touch. I've messaged a human to help."}
return response;
```

--------------------------------

### Extend Default Blocked IP Ranges for SSRF Protection

Source: https://docs.n8n.io/hosting/securing/ssrf-protection

This configuration allows extending the default list of blocked IP ranges for SSRF protection. You can add additional ranges to the `N8N_SSRF_BLOCKED_IP_RANGES` environment variable, separated by commas. The `default` keyword includes the pre-defined RFC 1918, loopback, link-local, and reserved ranges.

```environment
N8N_SSRF_BLOCKED_IP_RANGES=default,100.0.0.0/8
```

--------------------------------

### Define Filter and Collection Parameters

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

The 'filter' type is used for evaluating incoming data, often paired with a 'collection' type to allow users to configure specific filter behaviors like case sensitivity or type validation.

```JavaScript
{
	displayName: 'Conditions',
	name: 'conditions',
	placeholder: 'Add Condition',
	type: 'filter',
	default: {},
	typeOptions: {
		filter: {
			caseSensitive: '={{!$parameter.options.ignoreCase}}',
			typeValidation: '={{$parameter.options.looseTypeValidation ? "loose" : "strict"}}',
		},
	},
},
{
	displayName: 'Options',
	name: 'options',
	type: 'collection',
	placeholder: 'Add option',
	default: {},
	options: [
		{ displayName: 'Ignore Case', name: 'ignoreCase', type: 'boolean', default: true },
		{ displayName: 'Less Strict Type Validation', name: 'looseTypeValidation', type: 'boolean', default: true },
	],
}
```

--------------------------------

### Convert DateTime to Relative Time String (Luxon)

Source: https://docs.n8n.io/data/expression-reference/datetime

Returns a textual representation of the time relative to the current moment, such as 'in two days'. Rounds down by default. Options can specify the unit or locale for the output.

```javascript
$now.plus(1, 'day').toRelative() //=> "in 1 day"
```

```javascript
$now.plus(1, 'day').toRelative({unit:'hours'}) //=> "in 24 hours"
```

```javascript
$now.plus(1, 'day').toRelative({locale:'es'}) //=> "dentro de 1 día"
```

--------------------------------

### Define Node Resources and Operations in TypeScript

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/code-standards

Demonstrates the standard structure for defining a node's resources and operations using TypeScript. It utilizes displayOptions to conditionally show operations based on the selected resource.

```TypeScript
export const ExampleNode implements INodeType {
    description: {
        displayName: 'Example Node',
        ... 
        properties: [
            {
                displayName: 'Resource',
                name: 'resource',
                type: 'options',
                options: [
                    {
                        name: 'Resource One',
                        value: 'resourceOne'
                    },
                    {
                        name: 'Resource Two',
                        value: 'resourceTwo'
                    }
                ],
                default: 'resourceOne'
            },
            {
                displayName: 'Operation',
                name: 'operation',
                type: 'options',
                displayOptions: {
                    show: {
                        resource: [
                            'resourceOne'
                        ]
                    }
                },
                options: [
                    {
                        name: 'Create',
                        value: 'create',
                        description: 'Create an instance of Resource One'
                    }
                ]
            }
        ]
    }
}
```

--------------------------------

### LangChain Code Node Methods

Source: https://docs.n8n.io/code/builtin/langchain-methods

Methods available for use within expressions in the LangChain Code node to interact with node inputs, outputs, and execution lifecycle.

```APIDOC
## [METHOD] this.addInputData(inputName, data)

### Description
Populate the data of a specified non-main input. Useful for mocking data.

### Parameters
- **inputName** (string) - Required - Must be one of: ai_agent, ai_chain, ai_document, ai_embedding, ai_languageModel, ai_memory, ai_outputParser, ai_retriever, ai_textSplitter, ai_tool, ai_vectorRetriever, ai_vectorStore
- **data** (object) - Required - The data structure to be added.

---

## [METHOD] this.addOutputData(outputName, data)

### Description
Populate the data of a specified non-main output. Useful for mocking data.

### Parameters
- **outputName** (string) - Required - Must be one of: ai_agent, ai_chain, ai_document, ai_embedding, ai_languageModel, ai_memory, ai_outputParser, ai_retriever, ai_textSplitter, ai_tool, ai_vectorRetriever, ai_vectorStore
- **data** (object) - Required - The data structure to be added.

---

## [METHOD] this.getInputConnectionData(inputName, itemIndex, inputIndex?)

### Description
Get data from a specified non-main input.

### Parameters
- **inputName** (string) - Required - Connection type.
- **itemIndex** (number) - Required - Should always be 0.
- **inputIndex** (number) - Optional - Use if there is more than one node connected to the specified input.

---

## [METHOD] this.getExecutionCancelSignal()

### Description
Use this to stop the execution of a function when the workflow stops. Essential for custom chains or agents to handle cancellation signals.
```

--------------------------------

### Configure Resource Mapper in n8n

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

Implements a resource mapper component to handle data mapping and matching for insert/update operations. It supports automatic field mapping and custom matching logic.

```typescript
{
	displayName: 'Columns',
	name: 'columns',
	type: 'resourceMapper',
	default: {
		mappingMode: 'defineBelow',
		value: null,
	},
	required: true,
	typeOptions: {
		resourceMapper: {
			resourceMapperMethod: 'getMappingColumns',
			mode: 'update',
			fieldWords: {
				singular: 'column',
				plural: 'columns',
			},
			addAllFields: true,
			multiKeyMatch: true,
			supportAutoMap: true,
			matchingFieldsLabels: {
				title: 'Custom matching columns title',
				description: 'Help text for custom matching columns',
				hint: 'Below-field hint for custom matching columns',
			},
		},
	},
}
```

--------------------------------

### Set VUE_APP_URL_BASE_API Environment Variable

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/base-url

This snippet demonstrates how to set the VUE_APP_URL_BASE_API environment variable to configure the base URL for the n8n front-end to connect to the back-end REST API. This is typically done in a shell environment before building the UI. It requires a manual build of the n8n-editor-ui package.

```shell
export VUE_APP_URL_BASE_API=https://n8n.example.com/
```

--------------------------------

### Define Airtable Create Operation

Source: https://docs.n8n.io/_workflows//courses/level-one/chapter-5/chapter-5.5.json

This snippet shows the configuration for an Airtable node set to the 'create' operation. It maps input data fields 'orderID' and 'employeeName' to a specific table within an Airtable base.

```json
{
  "operation": "create",
  "base": { "value": "app9nOVsRxdypoknP" },
  "table": { "value": "tblTIOsm4BLJD9Tql" },
  "columns": {
    "mappingMode": "autoMapInputData"
  }
}
```

--------------------------------

### Access environment variables in n8n

Source: https://docs.n8n.io/code/cookbook/builtin/vars

Demonstrates how to retrieve a specific variable value using the $vars object. This syntax is applicable within expressions or code nodes in n8n workflows.

```javascript
// Access a variable
$vars.<variable-name>
```

--------------------------------

### Fix Ghost Node Post Tags and Add Credential Tests

Source: https://docs.n8n.io/release-notes/0-x

The Ghost Node has been fixed to correctly handle post tags. Additionally, credential tests have been added to the Ghost Node to improve authentication reliability and security.

```javascript
Ghost Node: Fix post tags and add credential tests.
```

--------------------------------

### Configure OpenAI GPT-4 Model in n8n

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/ask_a_human.json

This node configures the OpenAI GPT-4 model for use within an n8n workflow. It specifies the model name and allows for setting generation parameters such as 'temperature' to control the randomness of the output.

```json
{
  "model": "gpt-4",
  "options": {
    "temperature": 0.2
  }
}
```

--------------------------------

### Airtable Node Configuration for Data Creation

Source: https://docs.n8n.io/_workflows//courses/level-one/finished.json

Configures an Airtable node to create records in a specified base and table. It maps input data to Airtable columns, allowing for structured data storage. Requires Airtable API credentials.

```json
{
  "parameters": {
    "operation": "create",
    "base": {
      "__rl": true,
      "value": "app9nOVsRxdypoknP",
      "mode": "list",
      "cachedResultName": "beginner course"
    },
    "table": {
      "__rl": true,
      "value": "tblTIOsm4BLJD9Tql",
      "mode": "list",
      "cachedResultName": "processingOrders"
    },
    "columns": {
      "mappingMode": "autoMapInputData",
      "value": {},
      "matchingColumns": [],
      "schema": [
        {
          "id": "orderID",
          "displayName": "orderID",
          "required": false,
          "defaultMatch": false,
          "canBeUsedToMatch": true,
          "display": true,
          "type": "number",
          "readOnly": false,
          "removed": false
        },
        {
          "id": "employeeName",
          "displayName": "employeeName",
          "required": false,
          "defaultMatch": false,
          "canBeUsedToMatch": true,
          "display": true,
          "type": "string",
          "readOnly": false,
          "removed": false
        }
      ],
      "attemptToConvertTypes": false,
      "convertFieldsToString": false
    },
    "options": {}
  },
  "type": "n8n-nodes-base.airtable",
  "typeVersion": 2.1,
  "position": [
    880,
    -140
  ],
  "id": "5cef2ef7-98a6-4dc6-bc30-667eba06fd7b",
  "name": "Airtable",
  "credentials": {
    "airtableTokenApi": {
      "id": "UT32NHUYnp4pn1H3",
      "name": "Airtable Personal Access Token account"
    }
  }
}
```

--------------------------------

### Create Multiple Items from One Item (JavaScript)

Source: https://docs.n8n.io/courses/level-two/chapter-1

Transforms a single input item containing an array into multiple output items. Assumes the input item has a 'data' key set to an array. Each element in the array becomes a new item. This is useful when an incoming node provides a list within a single data object.

```javascript
return $input.first().json.data.map(item => {
    return {
        json: item
    }
});
```

--------------------------------

### Format Number with Locale and Options - JavaScript

Source: https://docs.n8n.io/data/expression-reference/number

Illustrates formatting a number with both a specific locale ('fr-FR') and formatting options, such as currency style, using Number.toLocaleString(). The 'options' object allows for detailed customization.

```javascript
let num = 500000.125;
console.log(num.toLocaleString('fr-FR', {style:'currency', currency:'EUR'})); //=> '500 000,13 €'
```

--------------------------------

### Perform HTTP Requests with n8n Helpers

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/code-standards

Demonstrates how to execute standard HTTP requests and authenticated requests using the built-in n8n helper methods. These methods utilize the Axios library internally to handle network communication.

```javascript
// If no auth needed
const response = await this.helpers.httpRequest(options);

// If auth needed
const response = await this.helpers.httpRequestWithAuthentication.call(
	this, 
	'credentialTypeName', // For example: pipedriveApi
	options,
);
```

--------------------------------

### Define AI Output Parser

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/let_your_ai_call_an_api.json

Configures the Auto-fixing Output Parser node to structure AI responses into JSON format. This ensures consistent data output for downstream workflow nodes.

```json
{
  "Structure_as_JSON": {
    "ai_outputParser": [{"node": "Auto-fixing Output Parser", "type": "ai_outputParser", "index": 0}]
  }
}
```

--------------------------------

### Convert DateTime to Local Timezone (Luxon)

Source: https://docs.n8n.io/data/expression-reference/datetime

Converts a DateTime object to the workflow's local time zone. The DateTime object still represents the same moment in time. The workflow's time zone can be configured in the workflow settings.

```javascript
dt.toLocal() //=> 2024-01-01T01:00:00.000+01:00, if time zone is Europe/Berlin
```

--------------------------------

### Update Google Cloud Run Service for n8n

Source: https://docs.n8n.io/hosting/installation/server-setups/google-cloud-run

This command updates a Google Cloud Run service named 'n8n' in a specified region. It configures essential environment variables for n8n, including N8N_HOST, WEBHOOK_URL, and N8N_EDITOR_BASE_URL, using the service's URL. Ensure the REGION variable is set before execution.

```bash
gcloud run services update n8n \
    --region=$REGION \
    --update-env-vars="N8N_HOST=$(echo $SERVICE_URL | sed 's/https:\/\///'),WEBHOOK_URL=$SERVICE_URL,N8N_EDITOR_BASE_URL=$SERVICE_URL"
```

--------------------------------

### Define API credentials for n8n node

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

Defines the credential structure for the node, including the API key input field and the authentication header configuration for API requests.

```TypeScript
import { IAuthenticateGeneric, ICredentialTestRequest, ICredentialType, INodeProperties } from 'n8n-workflow';

export class FriendGridApi implements ICredentialType {
	name = 'friendGridApi';
	displayName = 'FriendGrid API';
	properties: INodeProperties[] = [
		{ displayName: 'API Key', name: 'apiKey', type: 'string', default: '' },
	];

	authenticate: IAuthenticateGeneric = {
		type: 'generic',
		properties: {
			headers: { Authorization: '=Bearer {{$credentials.apiKey}}' },
		},
	};

	test: ICredentialTestRequest = {
		request: { baseURL: 'https://api.sendgrid.com/v3', url: '/marketing/contacts' },
	};
}
```

--------------------------------

### Add Optional Fields to n8n Node

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

Implements a 'collection' type property in n8n to group optional fields under an 'Additional Fields' UI element. This allows users to provide extra parameters like first and last names conditionally.

```javascript
{
	displayName: 'Additional Fields',
	name: 'additionalFields',
	type: 'collection',
	placeholder: 'Add Field',
	default: {},
	displayOptions: {
		show: {
			resource: [
				'contact',
			],
			operation: [
				'create',
			],
		},
	},
	options: [
		{
			displayName: 'First Name',
			name: 'firstName',
			type: 'string',
			default: '',
		},
		{
			displayName: 'Last Name',
			name: 'lastName',
			type: 'string',
			default: '',
		},
	],
}
```

--------------------------------

### Using '@feature' in n8n DisplayOptions for Parameter Visibility

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-versioning

Controls parameter visibility in n8n nodes based on defined feature flags using '@feature' within 'displayOptions'. This allows parameters to be shown only when specific features are enabled or disabled.

```typescript
{
    displayName: 'New API Field',
    name: 'newApiField',
    type: 'string',
    displayOptions: {
        show: {
            '@feature': ['useNewApi'],
        },
    },
}
```

```typescript
displayOptions: {
    show: {
        '@feature': [{ _cnd: { not: 'useNewApi' } }],
    },
}
```

```typescript
displayOptions: {
    show: {
        resource: ['myResource'],
        '@feature': [{ _cnd: { eq: 'useNewApi' } }],
    },
}
```

--------------------------------

### Allowlist Hostnames for SSRF Protection

Source: https://docs.n8n.io/hosting/securing/ssrf-protection

This configuration allows specifying hostnames that are permitted to be accessed, even if they fall within a blocked IP range. Hostname allowlists take precedence over IP blocklists. Wildcards are supported for pattern matching.

```environment
N8N_SSRF_ALLOWED_HOSTNAMES=*.n8n.internal,*.company.local
```

--------------------------------

### Convert DateTime to Seconds Timestamp (Luxon)

Source: https://docs.n8n.io/data/expression-reference/datetime

Returns a Unix timestamp in seconds, representing the number of seconds elapsed since January 1, 1970.

```javascript
$now.toSeconds() //=> 1712334442.372
```

--------------------------------

### Encode strings for URLs using urlEncode()

Source: https://docs.n8n.io/data/expression-reference/string

The urlEncode() method converts a string into a URL-safe format by replacing special characters with %XX codes. It accepts an optional boolean parameter 'allChars' to determine whether to encode reserved URI syntax characters like '=' or '?'.

```n8n
"name=Nathan Automat".urlEncode() // => "name%3DNathan%20Automat"
"name=Nathan Automat".urlEncode(true) // => "name=Nathan%20Automat"
```

--------------------------------

### Enable all nodes by clearing exclusion list

Source: https://docs.n8n.io/hosting/securing/blocking-nodes

To allow access to all nodes, including those blocked by default, set the NODES_EXCLUDE environment variable to an empty array. This removes all restrictions on node usage.

```environment
NODES_EXCLUDE: "[]"
```

--------------------------------

### Allow Specific Built-in Modules in n8n Code Node (Shell)

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/modules-in-code-node

This configuration enables the n8n Code node to import specific built-in Node.js modules, enhancing security by limiting the available modules. The `NODE_FUNCTION_ALLOW_BUILTIN` environment variable is set to a comma-separated list of allowed modules, such as 'crypto' or 'crypto,fs'.

```shell
# Allows usage of only crypto
export NODE_FUNCTION_ALLOW_BUILTIN=crypto
```

```shell
# Allows usage of only crypto and fs
export NODE_FUNCTION_ALLOW_BUILTIN=crypto,fs
```

--------------------------------

### Define Collection UI Element

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

Configuration for collection types used to group optional fields or provide nested options within a node interface.

```JSON
{
	displayName: 'Filters',
	name: 'filters',
	type: 'collection',
	placeholder: 'Add Field',
	default: {},
	options: [
		{
			displayName: 'Type',
			name: 'type',
			type: 'options',
			options: [
				{ name: 'Automated', value: 'automated' },
				{ name: 'Past', value: 'past' },
				{ name: 'Upcoming', value: 'upcoming' }
			],
			default: ''
		}
	],
	displayOptions: {
		show: {
			resource: [],
			operation: []
		}
	}
}
```

--------------------------------

### Split strings into arrays with split()

Source: https://docs.n8n.io/data/expression-reference/string

Divides a string into an array of substrings using a specified separator or regular expression. The separator is excluded from the resulting array.

```javascript
"wind,fire,water".split(",");
"me and you and her".split("and");
"me? you, and her".split(/[ ,?]+/);
```

--------------------------------

### Remove Empty Fields from Object (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/object

The `compact()` method removes all fields from an object that have empty values (null or empty string). It returns the modified object. This is a custom n8n functionality.

```javascript
// obj = {'x':null, 'y':2, 'z':''}
obj.compact() //=> {'y':2}
```

--------------------------------

### POST /message/send

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/message-operations

Sends a standard message to a Telegram chat with optional formatting and notification settings.

```APIDOC
## POST /message/send

### Description
Sends a message to a specified Telegram chat. Includes support for n8n attribution, silent notifications, and custom parse modes.

### Method
POST

### Parameters
#### Request Body
- **chatId** (string) - Required - The unique identifier or username of the target chat.
- **text** (string) - Required - The message content to send.
- **appendAttribution** (boolean) - Optional - Whether to append 'This message was sent automatically with n8n'.
- **disableNotification** (boolean) - Optional - If true, sends the message silently.
- **disableWebPagePreview** (boolean) - Optional - Disables link previews.
- **parseMode** (string) - Optional - Formatting style: HTML, Markdown, or MarkdownV2.
- **replyToMessageId** (integer) - Optional - ID of the message to reply to.
- **messageThreadId** (integer) - Optional - Target forum topic ID.

### Request Example
{
  "chatId": "@mychannel",
  "text": "Hello world!",
  "parseMode": "HTML"
}

### Response
#### Success Response (200)
- **messageId** (integer) - The ID of the sent message.

#### Response Example
{
  "messageId": 12345
}
```

--------------------------------

### Stop n8n with Docker Compose

Source: https://docs.n8n.io/hosting/installation/server-setups/docker-compose

This command gracefully stops the running Docker containers managed by Docker Compose. It ensures that all services defined in the `compose.yaml` file are shut down.

```bash
sudo docker compose stop
```

--------------------------------

### Send Credential Overwrites via cURL (Bash)

Source: https://docs.n8n.io/embed/configuration

This command uses `curl` to send a local JSON file containing credential overwrites to the configured REST endpoint. It sets the `Content-Type` header to `application/json` and uses the `--data` flag to specify the JSON file.

```bash
curl -H "Content-Type: application/json" --data @oauth-credentials.json http://localhost:5678/send-credentials
```

--------------------------------

### Allow All Built-in Modules in n8n Code Node (Shell)

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/modules-in-code-node

This configuration allows the n8n Code node to import all built-in Node.js modules. It is achieved by setting the `NODE_FUNCTION_ALLOW_BUILTIN` environment variable to '*'. This setting should be used with caution due to potential security implications.

```shell
# Allows usage of all builtin modules
export NODE_FUNCTION_ALLOW_BUILTIN=*
```

--------------------------------

### Send Credential Overwrites with Auth Token via cURL (Bash)

Source: https://docs.n8n.io/embed/configuration

This `curl` command demonstrates sending credential overwrites to a REST endpoint that is secured with an authorization token. It includes an `Authorization` header with a `Bearer` token.

```bash
curl -H "Content-Type: application/json" -H "Authorization: Bearer secure-token" --data @oauth-credentials.json http://localhost:5678/send-credentials
```

--------------------------------

### Number.format()

Source: https://docs.n8n.io/data/expression-reference/number

Formats a number into a string based on locale and options.

```APIDOC
## Number.format()

### Description
Returns a formatted string representing the number. Useful for formatting for a specific language or currency. The same as Intl.NumberFormat().

### Syntax
Number.format(locale?, options?)

### Parameters
- **locale** (String) - Optional - A locale tag for formatting the number, e.g. fr-FR, en-GB, pr-BR
- **options** (Object) - Optional - Configuration options for number formatting.

### Response Example
// number = 123456.789;
number.format('de-DE') //=> 123.456,789
```

--------------------------------

### Configure Discord Embeds via Raw JSON

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.discord/common-issues

This JSON object demonstrates how to define advanced embed fields like 'footer' and 'fields' that are not available through the standard n8n Discord node UI. It is intended for use within the 'Value' parameter when the 'Input Method' is set to 'Raw JSON'.

```json
{
    "author": "My Name",
	"url": "https://discord.js.org",
	"fields": [
		{
			"name": "Regular field title",
			"value": "Some value here"
		}
	],
	"footer": {
		"text": "Some footer text here",
		"icon_url": "https://i.imgur.com/AfFp7pu.png"
	}
}
```

--------------------------------

### Define Kubernetes Pod Resource Limits

Source: https://docs.n8n.io/hosting/installation/server-setups/azure

Specifies the minimum and maximum memory resources for n8n application containers within a Kubernetes pod. This helps manage resource consumption and ensures stability. The values can be adjusted based on specific needs and n8n cloud offering tiers.

```yaml
resources:
  requests:
    memory: "250Mi"
  limits:
    memory: "500Mi"
```

--------------------------------

### Make Notion Heading Toggleable via HTTP Request

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.notion/common-issues

This sequence of HTTP requests allows you to create a toggleable heading in Notion. It involves creating a regular heading, then querying it to enable the `is_toggleable` property, and finally updating the block. This is necessary because the Notion node does not directly support creating toggleable headings.

```http
1. Create a heading using the Notion node (Page, Database Page, or Block resource).
2. Use an HTTP Request node (GET method) to fetch the block details: https://api.notion.com/v1/blocks/<block_ID>
3. Use an Edit Fields (Set) node to add `heading_X.is_toggleable` as a Boolean field set to `true`.
4. Use a second HTTP Request node (PATCH method) to update the block: https://api.notion.com/v1/blocks/{{ $json.id }}
   Set parameter Name to `heading_X` and Value to `{{ $json.heading_X }}`.
```

--------------------------------

### Disable n8n Telemetry and External Services

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/isolation

Configures environment variables to disable diagnostics, version notifications, and template access. These settings prevent the n8n instance from sending data to or fetching content from n8n's servers.

```bash
N8N_DIAGNOSTICS_ENABLED=false
N8N_VERSION_NOTIFICATIONS_ENABLED=false
N8N_TEMPLATES_ENABLED=false
```

--------------------------------

### Add Support for Service Account Authentication in GoogleBigQuery

Source: https://docs.n8n.io/release-notes/0-x

The GoogleBigQuery node now supports service account authentication. This allows for more secure and flexible access to Google BigQuery data by using service accounts, which is a common practice in cloud environments.

```javascript
GoogleBigQuery: added support for service account authentication.
```

--------------------------------

### Create Single Item from Multiple Items (JavaScript)

Source: https://docs.n8n.io/courses/level-two/chapter-1

Combines multiple input items into a single output item. The 'data_object' field in the output will contain an array of all input items. This is useful for aggregating results from different branches of a workflow into one consolidated item.

```javascript
return [
	{
    	json: {
    		data_object: $input.all().map(item => item.json)
    	}
    }
];
```

--------------------------------

### Array.chunk()

Source: https://docs.n8n.io/data/expression-reference/array

Splits the array into an array of sub-arrays, each with the given length.

```APIDOC
## Array.chunk()

### Description
Splits the array into an array of sub-arrays, each with the given length.

### Method
Array.chunk(length)

### Parameters
#### Path Parameters
- **length** (Number) - Required - The number of elements in each chunk

### Request Example
```json
{
  "example": "// arr = [1, 2, 3, 4, 5, 6]\narr.chunk(2) //=> [ [1,2], [3,4], [5,6] ]"
}
```

### Response
#### Success Response (200)
- **Array** (Array) - An array of sub-arrays, each with the specified length.

#### Response Example
```json
{
  "example": "[ [1,2], [3,4], [5,6] ]"
}
```
```

--------------------------------

### Convert Object to JSON String

Source: https://docs.n8n.io/data/expression-reference/object

The toJsonString() method converts an Object into a JSON-formatted string. It functions similarly to the native JavaScript JSON.stringify() method and returns a string representation of the object.

```javascript
// obj = {'name':'Nathan', age:42}
obj.toJsonString() //=> '{"name":"Nathan","age":42}'
```

--------------------------------

### Array.compact()

Source: https://docs.n8n.io/data/expression-reference/array

Removes any empty values from the array. `null`, `""` and `undefined` count as empty.

```APIDOC
## Array.compact()

### Description
Removes any empty values from the array. `null`, `""` and `undefined` count as empty.

### Method
Array.compact()

### Request Example
```json
{
  "example": "// arr = [2, null, 1, \"\"]\narr.compact() //=> [2, 1]"
}
```

### Response
#### Success Response (200)
- **Array** (Array) - The array with empty values removed.

#### Response Example
```json
{
  "example": "[2, 1]"
}
```
```

--------------------------------

### Restrict File Access in n8n

Source: https://docs.n8n.io/hosting/configuration/environment-variables/security

Controls which directories n8n can access files from. By default, access might be broader, but this variable allows for explicit limitation. Multiple directories can be specified using a semicolon-separated list.

```bash
# Example: Limit file access to /data and /shared
N8N_RESTRICT_FILE_ACCESS_TO=/data;/shared
```

--------------------------------

### Add Label to a message

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/message-operations

Adds one or more labels to a specified Gmail message.

```APIDOC
## Add Label to a message

### Description
Use this operation to add one or more labels to a message.

### Method
POST

### Endpoint
/users.messages.modify

### Parameters
#### Path Parameters
- **userId** (string) - Required - The ID of the user's mailbox. Use 'me' to refer to the authenticated user.

#### Query Parameters
- **format** (string) - Optional - The format to return the message in.
- **metadataHeaders** (string) - Optional - When specified, the value of this field is used as a prefix to the labels that are returned in the metadata. 

#### Request Body
- **addLabelIds** (array) - Required - The IDs of labels to add to this message.
- **removeLabelIds** (array) - Optional - The IDs of labels to remove from this message.

### Request Example
```json
{
  "addLabelIds": [
    "Label_1"
  ],
  "removeLabelIds": [
    "Label_2"
  ]
}
```

### Response
#### Success Response (200)
- **id** (string) - The unique ID of the message.
- **threadId** (string) - The unique ID of the thread associated with the message.
- **labelIds** (array) - The list of IDs of labels associated with this message.

#### Response Example
```json
{
  "id": "17a8b3a4c5d6e7f8",
  "threadId": "17a8b3a4c5d6e7f8",
  "labelIds": [
    "INBOX",
    "UNREAD",
    "Label_1"
  ]
}
```
```

--------------------------------

### Conditional Logic with $if()

Source: https://docs.n8n.io/data/expression-reference/root

Returns one of two values based on a condition, similar to JavaScript's ternary operator. It takes a condition, a value if true, and a value if false. Returns any type.

```javascript
// Return "Good day" if time is before 5pm, otherwise "Good evening"
$if($now.hour < 17, "Good day", "Good evening")
```

```javascript
// $if() calls can be combined:
// Return "Good morning" if time is before 10am, "Good day" it's before 5pm, otherwise "Good evening"
$if($now.hour < 10, "Good morning", $if($now.hour < 17, "Good day", "Good evening"))
```

--------------------------------

### Retrieve SQL Domain Name

Source: https://docs.n8n.io/integrations/builtin/credentials/microsoftsql

This SQL query retrieves the default domain name for the SQL Server connection. It's used when users from multiple domains access the database.

```sql
SELECT DEFAULT_DOMAIN()[DomainName];
```

--------------------------------

### Enable External OAuth Connections in n8n

Source: https://docs.n8n.io/release-notes/0-x

This enhancement allows n8n to support external OAuth connections. This feature enables users to connect OAuth applications without requiring direct access to n8n's internal configuration, simplifying the integration process for third-party services.

```javascript
allow external OAuth connection. This enhancement adds support for connecting OAuth apps without access to n8n.
```

--------------------------------

### Disable n8n Version Notifications

Source: https://docs.n8n.io/hosting/securing/telemetry-opt-out

Configures the environment variable to prevent the n8n instance from checking for new software versions. Set this variable to false to disable automatic update notifications.

```bash
export N8N_VERSION_NOTIFICATIONS_ENABLED=false
```

--------------------------------

### Set Maximum Workflow Execution Time (Shell)

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/execution-timeout

Sets the maximum execution time in seconds for individual workflows. This provides a granular control over how long a specific workflow is allowed to run before being canceled. The default value is -1 (no maximum limit).

```shell
export EXECUTIONS_TIMEOUT_MAX=7200
```

--------------------------------

### Check if Array is empty

Source: https://docs.n8n.io/data/expression-reference/array

Custom n8n utility methods to verify if an array contains no elements (isEmpty) or contains at least one element (isNotEmpty).

```JavaScript
const arr = [];
arr.isEmpty(); // => true
arr.isNotEmpty(); // => false
```

--------------------------------

### Delete Kubernetes Resources

Source: https://docs.n8n.io/hosting/installation/server-setups/azure

Removes all resources created by the Kubernetes manifests. This command is used to clean up the deployed n8n and PostgreSQL applications from the cluster.

```bash
kubectl delete -f .
```

--------------------------------

### Define Collection Item Schema

Source: https://docs.n8n.io/embed/workflow-templates

Defines the structure for a collection object, including metadata like rank, views, and creation date, along with arrays of associated workflows and nodes.

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "id": {
      "type": "number"
    },
    "rank": {
      "type": "number"
    },
    "name": {
      "type": "string"
    },
    "totalViews": {},
    "createdAt": {
      "type": "string"
    },
    "workflows": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {
            "type": "number"
          }
        },
        "required": [
          "id"
        ]
      }
    },
    "nodes": {
      "type": "array",
      "items": {}
    }
  },
  "required": [
    "id",
    "rank",
    "name",
    "totalViews",
    "createdAt",
    "workflows",
    "nodes"
  ]
}
```

--------------------------------

### Add Custom Log Messages in n8n Workflows

Source: https://docs.n8n.io/hosting/logging-monitoring/logging

Implement custom log messages within n8n workflows using the LoggerProxy class. This allows for detailed debugging information to be recorded, including workflow context like name and ID. Ensure the LoggerProxy is initialized before use, typically handled by the start.ts file.

```typescript
// You have to import the LoggerProxy. We rename it to Logger to make it easier

import {
	LoggerProxy as Logger
} from 'n8n-workflow';

// Info-level logging of a trigger function, with workflow name and workflow ID as additional metadata properties

Logger.info(`Polling trigger initiated for workflow "${workflow.name}"`, {workflowName: workflow.name, workflowId: workflow.id});

```

--------------------------------

### Allowlist IP Ranges for SSRF Protection

Source: https://docs.n8n.io/hosting/securing/ssrf-protection

This configuration allows specifying specific IP ranges that are permitted to be accessed, overriding the blocklists. IP allowlists are checked after hostname allowlists. Individual IPs can be specified using /32 notation.

```environment
N8N_SSRF_ALLOWED_IP_RANGES=10.0.1.0/24,10.0.2.50/32
```

--------------------------------

### Access Input Data with $input

Source: https://docs.n8n.io/data/expression-reference/root

Provides access to the input data of the current node. This function returns NodeData and is part of n8n's custom functionality.

```javascript
function getInputData() {
  // Example usage: access input data
  return $input;
}
```

--------------------------------

### PATCH /rest/workflows/{id}

Source: https://docs.n8n.io/embed/managing-workflows

Updates an existing workflow, typically used to activate or publish the workflow.

```APIDOC
## PATCH /rest/workflows/{id}

### Description
Updates the properties of an existing workflow, such as setting the 'active' status to true to publish it.

### Method
PATCH

### Endpoint
https://<n8n-domain>/rest/workflows/{id}

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID of the workflow to update.

#### Request Body
- **active** (boolean) - Optional - Set to true to activate/publish the workflow.
- **settings** (object) - Optional - Workflow settings.

### Request Example
{
  "active": true,
  "settings": {}
}

### Response
#### Success Response (200)
- **message** (string) - Confirmation of the update.
```

--------------------------------

### Create Airtable Records (n8n)

Source: https://docs.n8n.io/_workflows//courses/level-one/chapter-5/chapter-5.6.json

Configures an Airtable node to create new records in a specified table. It supports mapping input data to table columns and allows for schema definition to ensure data integrity. This node is used for writing data into Airtable.

```json
{
  "parameters": {
    "operation": "create",
    "base": {
      "__rl": true,
      "value": "app9nOVsRxdypoknP",
      "mode": "list",
      "cachedResultName": "beginner course"
    },
    "table": {
      "__rl": true,
      "value": "tblTIOsm4BLJD9Tql",
      "mode": "list",
      "cachedResultName": "processingOrders"
    },
    "columns": {
      "mappingMode": "autoMapInputData",
      "value": {},
      "matchingColumns": [],
      "schema": [
        {
          "id": "orderID",
          "displayName": "orderID",
          "required": false,
          "defaultMatch": false,
          "canBeUsedToMatch": true,
          "display": true,
          "type": "number",
          "readOnly": false,
          "removed": false
        },
        {
          "id": "employeeName",
          "displayName": "employeeName",
          "required": false,
          "defaultMatch": false,
          "canBeUsedToMatch": true,
          "display": true,
          "type": "string",
          "readOnly": false,
          "removed": false
        }
      ],
      "attemptToConvertTypes": false,
      "convertFieldsToString": false
    },
    "options": {}
  },
  "type": "n8n-nodes-base.airtable",
  "typeVersion": 2.1,
  "position": [
    1020,
    -600
  ],
  "id": "5e60ca72-d773-439c-b39a-4b14c54f795b",
  "name": "Airtable1",
  "credentials": {
    "airtableTokenApi": {
      "id": "UT32NHUYnp4pn1H3",
      "name": "Airtable Personal Access Token account"
    }
  }
}
```

--------------------------------

### Create n8n Credentials via API

Source: https://docs.n8n.io/embed/managing-workflows

This snippet demonstrates how to create n8n credentials for a user programmatically using a POST request to the n8n API. It requires specifying the credential name, type, nodes that will access it, and the actual credential data. The response includes the ID of the newly created credential.

```HTTP
POST https://<n8n-domain>/rest/credentials
```

```JSON
{
   "name":"MyAirtable",
   "type":"airtableApi",
   "nodesAccess":[
      {
         "nodeType":"n8n-nodes-base.airtable"
      }
   ],
   "data":{
      "apiKey":"q12we34r5t67yu"
   }
}
```

```JSON
{
   "data":{
      "name":"MyAirtable",
      "type":"airtableApi",
      "data":{
         "apiKey":"q12we34r5t67yu"
      },
      "nodesAccess":[
         {
            "nodeType":"n8n-nodes-base.airtable",
            "date":"2021-09-10T07:41:27.770Z"
         }
      ],
      "id":"29",
      "createdAt":"2021-09-10T07:41:27.777Z",
      "updatedAt":"2021-09-10T07:41:27.777Z"
   }
}
```

--------------------------------

### Enhance PagerDuty Node with More Incident Details

Source: https://docs.n8n.io/release-notes/0-x

The PagerDuty node has been updated to support more detailed incident information. This allows users to access and utilize a richer set of data when interacting with PagerDuty incidents for monitoring and alerting purposes.

```javascript
PagerDuty node: now supports more detail in incidents.
```

--------------------------------

### Calculate Days to Christmas using n8n Expression (JavaScript)

Source: https://docs.n8n.io/data/specific-data-types/luxon

This n8n expression calculates the number of days until Christmas of the current year. It leverages Luxon's DateTime and diff methods, along with JMESPath for object property access and string manipulation to format the output. The expression dynamically uses the current year to ensure it works for any year.

```javascript
{{"There are " + $today.diff(DateTime.fromISO($today.year + '-12-25'), 'days').toObject().days.toString().substring(1) + " days to Christmas!"}}
```

--------------------------------

### Define n8n Node Class and Imports

Source: https://docs.n8n.io/integrations/creating-nodes/build/programmatic-style-node

The essential TypeScript imports and class structure required to implement a custom node in n8n, including the INodeType interface.

```typescript
import type {
	IDataObject,
	IExecuteFunctions,
	IHttpRequestOptions,
	INodeExecutionData,
	INodeType,
	INodeTypeDescription,
} from 'n8n-workflow';
import { NodeConnectionTypes } from 'n8n-workflow';

export class FriendGrid implements INodeType {
	description: INodeTypeDescription = {
		// Basic node details will go here
		properties: [
			// Resources and operations will go here
		],
	};
	// The execute method will go here
	async execute(this: IExecuteFunctions): Promise<INodeExecutionData[][]> {
	}
}
```

--------------------------------

### HTTP Request Node Configuration

Source: https://docs.n8n.io/_workflows//courses/level-one/finished.json

Configures an HTTP request to an internal webhook. It uses generic HTTP header authentication and sends custom headers. This node is crucial for initiating data flow from an external source.

```json
{
  "parameters": {
    "url": "https://internal.users.n8n.cloud/webhook/custom-erp",
    "authentication": "genericCredentialType",
    "genericAuthType": "httpHeaderAuth",
    "sendHeaders": true,
    "headerParameters": {
      "parameters": [
        {
          "name": "unique_id",
          "value": "4d259ec5241587a0d2820670fc048f0d"
        }
      ]
    },
    "options": {}
  },
  "type": "n8n-nodes-base.httpRequest",
  "typeVersion": 4.2,
  "position": [
    220,
    -40
  ],
  "id": "e1fb70b3-0212-4e78-9976-cb77c69f1a92",
  "name": "HTTP Request",
  "credentials": {
    "httpHeaderAuth": {
      "id": "sMuanZ4xGobAurzY",
      "name": "Nathan's ABCorp data warehouse account"
    }
  }
}
```

--------------------------------

### Update Drive Fields

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googledrive/shared-drive-operations

This endpoint allows you to update various fields of a shared drive, including its name, color, and restrictions.

```APIDOC
## PUT /drive/v3/drives/{driveId}

### Description
Updates the specified shared drive. This method supports patch semantics. 

### Method
PUT

### Endpoint
`/drive/v3/drives/{driveId}`

### Parameters
#### Path Parameters
- **driveId** (string) - Required - The ID of the shared drive.

#### Query Parameters
- **fields** (string) - Optional - A selector specifying a subset of fields to include in the response.
- **useDomainAdminAccess** (boolean) - Optional - Whether to use domain admin privileges.

#### Request Body
- **colorRgb** (string) - Optional - The color of this shared drive as an RGB hex string.
- **name** (string) - Optional - The updated name for the shared drive.
- **restrictions** (object) - Optional - Restrictions for this shared drive.
  - **adminManagedRestrictions** (boolean) - Optional - When enabled, restrictions here will override the similarly named fields to true for any file inside of this shared drive.
  - **copyRequiresWriterPermission** (boolean) - Optional - Whether the options to copy, print, or download files inside this shared drive should be disabled for readers and commenters.
  - **domainUsersOnly** (boolean) - Optional - Whether to restrict access to this shared drive and items inside this shared drive to users of the domain to which this shared drive belongs.
  - **driveMembersOnly** (boolean) - Optional - Whether to restrict access to items inside this shared drive to its members.

### Request Example
```json
{
  "name": "New Drive Name",
  "colorRgb": "#aabbcc",
  "restrictions": {
    "adminManagedRestrictions": true,
    "copyRequiresWriterPermission": false
  }
}
```

### Response
#### Success Response (200)
- **id** (string) - The ID of the drive.
- **name** (string) - The name of the drive.
- **colorRgb** (string) - The color of the drive as an RGB hex string.
- **restrictions** (object) - Restrictions for this drive.
  - **adminManagedRestrictions** (boolean) - Whether the Admin managed restrictions are enabled.
  - **copyRequiresWriterPermission** (boolean) - Whether copy requires writer permission.
  - **domainUsersOnly** (boolean) - Whether the drive is restricted to domain users only.
  - **driveMembersOnly** (boolean) - Whether the drive is restricted to members only.

#### Response Example
```json
{
  "id": "drive123",
  "name": "New Drive Name",
  "colorRgb": "#aabbcc",
  "restrictions": {
    "adminManagedRestrictions": true,
    "copyRequiresWriterPermission": false,
    "domainUsersOnly": false,
    "driveMembersOnly": false
  }
}
```
```

--------------------------------

### n8n Workflow JSON Configuration

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/ask_a_human.json

This JSON structure defines the nodes and parameters for the n8n workflow, including the Chat Trigger, Memory Buffer, and Tool Workflow nodes. It serves as the blueprint for the AI agent's interaction logic.

```json
{
  "name": "Ask a human",
  "nodes": [
    {
      "parameters": {},
      "id": "a60c8572-56c1-4bf3-8352-a6419a475887",
      "name": "Simple Memory",
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.1
    },
    {
      "parameters": {
        "name": "dont_know_tool",
        "description": "Use this tool if you don't know the answer...",
        "workflowId": "={{ $workflow.id}}"
      },
      "id": "b4f2e26c-903b-46b8-bd8b-110fd64de9e4",
      "name": "Not sure?",
      "type": "@n8n/n8n-nodes-langchain.toolWorkflow"
    }
  ]
}
```

--------------------------------

### Smart Join Array of Objects

Source: https://docs.n8n.io/data/expression-reference/array

Transforms an array of objects into a single object by mapping specific fields as keys and values. Useful for converting key-value pair structures into a single flat object.

```n8n
// arr => [{'field':'age','value':2},{'field':'city','value':'Berlin'}]
arr.smartJoin('field','value') //=> {"age": 2, "city": "Berlin"}
```

--------------------------------

### Set custom execution data

Source: https://docs.n8n.io/data/expression-reference/customdata

Stores a key-value pair in the execution's custom data store. This is useful for tagging executions to allow for easier filtering and retrieval later.

```javascript
// Store the user's email, to easily retrieve all execs related to that user later
$execution.customData.set("user_email", "me@example.com")
```

--------------------------------

### Array.average()

Source: https://docs.n8n.io/data/expression-reference/array

Returns the average of the numbers in the array. Throws an error if there are any non-numbers.

```APIDOC
## Array.average()

### Description
Returns the average of the numbers in the array. Throws an error if there are any non-numbers.

### Method
Array.average()

### Response
#### Success Response (200)
- **Number** (Number) - The average of the numbers in the array

### Request Example
```json
{
  "example": "// arr = [12, 1, 5]\narr.average() //=> 6"
}
```
```

--------------------------------

### Find element in Array using JavaScript

Source: https://docs.n8n.io/data/expression-reference/array

Returns the first element in an array that satisfies a provided testing function. Returns undefined if no element matches the condition.

```JavaScript
// Find first age over 18
const ages = [12, 33, 16, 40];
ages.find(age => (age > 18)); // => 33

// Find first name under 5 letters long
const names = ['Nathan', 'Bob', 'Sebastian'];
names.find(name => name.length < 5); // => 'Bob'
```

--------------------------------

### Format Number with Locale and Options (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/number

Returns a formatted string representation of a number, suitable for specific locales or currencies. It mirrors the functionality of `Intl.NumberFormat()`. Accepts optional locale and formatting options.

```javascript
// number = 123456.789;
number.format('de-DE') //=> 123.456,789
```

```javascript
// number = 123456.789;
number.format('de-DE', {'style': 'currency', 'currency': 'EUR'}) //=> 123.456,79 €
```

--------------------------------

### Convert strings to DateTime objects with toDateTime()

Source: https://docs.n8n.io/data/expression-reference/string

A custom n8n method that parses strings into DateTime objects. Supports ISO 8601, HTTP, RFC2822, SQL, and Unix timestamp formats.

```javascript
"2024-03-29T18:06:31.798+01:00".toDateTime();
"Fri, 29 Mar 2024 18:08:01 +0100".toDateTime();
"20240329".toDateTime();
"1711732132990".toDateTime();
```

--------------------------------

### Define Additional Fields Object for n8n

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-base-files/standard-parameters

This object structure is used to define optional parameters in n8n integrations. It includes metadata for the UI element and displayOptions to control when the field appears based on selected resources or operations.

```JavaScript
displayName: 'Additional Fields',
name: 'additionalFields',
// The UI element type
type: '',
placeholder: 'Add Field',
default: {},
displayOptions: {
  // Set which resources and operations this field is available for
  show: {
    resource: [
      // Resource names
    ],
    operation: [
      // Operation names
    ]
  },
}
```

--------------------------------

### Valid JSON Formatting for HTTP Request Node

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.httprequest/common-issues

Demonstrates how to correctly format JSON data within an expression for the HTTP Request node. Ensures proper syntax, including nested objects and arrays, to avoid 'JSON parameter need to be an valid JSON' errors.

```javascript
{
    "myjson":
    {
        "name1": "value1",
        "name2": "value2",
        "array1":
            ["value1","value2"]
    }
}
```

--------------------------------

### Format Number with Default Locale - JavaScript

Source: https://docs.n8n.io/data/expression-reference/number

Demonstrates using Number.toLocaleString() with the default system locale to format a number. This method takes optional 'locales' and 'options' arguments for customization.

```javascript
let num = 500000.125;
console.log(num.toLocaleString()); //=> '500,000.125' (if in US English locale)
```

--------------------------------

### String isEmpty() - Check if string is empty or null

Source: https://docs.n8n.io/data/expression-reference/string

Checks if a string is either empty (contains no characters) or is explicitly null. It returns true for empty or null strings and false otherwise.

```javascript
"".isEmpty() // => true
"hello".isEmpty() // => false
```

--------------------------------

### Identifying Credential Type Name in Workflow JSON

Source: https://docs.n8n.io/api/using-api-playground

Demonstrates how to locate the credential type name within an exported n8n workflow JSON file. This identifier is necessary for querying the credential schema API.

```json
{
    ...,
    "credentials": {
        "googleDriveOAuth2Api": {
        "id": "9",
        "name": "Google Drive"
        }
    }
}
```

--------------------------------

### Access and log node data in n8n

Source: https://docs.n8n.io/code/cookbook/builtin/all

Retrieves all items from a specified previous node and iterates through them to log their JSON content. This is a common pattern for debugging or transforming data within n8n workflow nodes.

```JavaScript
previousNodeData = $("<node-name>").all();
for(let i=0; i<previousNodeData.length; i++) {
	console.log(previousNodeData[i].json);
}
```

```Python
previousNodeData = _("<node-name>").all()
for item in previousNodeData:
	# item is of type <class 'pyodide.ffi.JsProxy'>
	# You need to convert it to a Dict
	itemDict = item.json.to_py()
	print(itemDict)
```

--------------------------------

### Define Fixed Collection Parameter

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/ui-elements

The 'fixedCollection' type is used to group semantically related fields, allowing for structured data input like metadata key-value pairs.

```JavaScript
{
	displayName: 'Metadata',
	name: 'metadataUi',
	placeholder: 'Add Metadata',
	type: 'fixedCollection',
	default: '',
	typeOptions: { multipleValues: true },
	options: [
		{
			name: 'metadataValues',
			displayName: 'Metadata',
			values: [
				{ displayName: 'Name', name: 'name', type: 'string', default: '' },
				{ displayName: 'Value', name: 'value', type: 'string', default: '' },
			],
		},
	],
}
```

--------------------------------

### Customizing Health Check Endpoints

Source: https://docs.n8n.io/hosting/logging-monitoring/monitoring

You can customize the path for the health check endpoints using the `N8N_ENDPOINT_HEALTH` environment variable.

```APIDOC
## Customizing Health Check Endpoints

### Description
Allows customization of the health check endpoint path.

### Method
Environment Variable Configuration

### Endpoint
N/A

### Parameters
#### Environment Variables
- **N8N_ENDPOINT_HEALTH** (string) - The custom path for health check endpoints.

### Request Example
```
N8N_ENDPOINT_HEALTH=/custom/health
```

### Response
N/A
```

--------------------------------

### Add Support for Blocks in Slack Message Update

Source: https://docs.n8n.io/release-notes/0-x

The Slack node now supports using 'blocks' for updating Slack messages. This enables the creation of more interactive and visually appealing messages within Slack, leveraging Slack's Block Kit UI framework.

```javascript
Slack node: added support for blocks in Slack message update.
```

--------------------------------

### Fix Pagination Issue in QuickBooks Node

Source: https://docs.n8n.io/release-notes/0-x

A pagination issue within the QuickBooks node has been resolved. This fix ensures that data retrieval from QuickBooks is handled correctly across multiple pages, preventing data loss or incomplete results.

```javascript
QuickBooks node: fixed a pagination issue.
```

--------------------------------

### Format DateTime to ISO

Source: https://docs.n8n.io/data/expression-reference/datetime

Converts the DateTime object into an ISO 8601-compliant string.

```javascript
$now.toISO() // => 2024-04-05T18:44:55.525+02:00
```

--------------------------------

### Array.sum()

Source: https://docs.n8n.io/data/expression-reference/array

Calculates the total sum of all numbers within an array.

```APIDOC
## Array.sum()

### Description
Returns the total of all the numbers in the array. Throws an error if there are any non-numbers.

### Method
N/A (Custom n8n Method)

### Response
- **Returns** (Number) - The sum of the array elements.

### Response Example
```javascript
[12, 1, 5].sum() // 18
```
```

--------------------------------

### Set General Workflow Timeout (Shell)

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/execution-timeout

Sets the general timeout for workflows in seconds. If a workflow runs in the main process, a soft timeout occurs. If it runs in its own process, n8n attempts a soft timeout, then kills the process after a fifth of the timeout duration. The default value is -1 (no timeout).

```shell
export EXECUTIONS_TIMEOUT=3600
```

--------------------------------

### Conditional Logic

Source: https://docs.n8n.io/data/expression-reference

Helpers and standard operators to evaluate conditions and return values accordingly. Includes n8n-specific helpers like $ifEmpty for handling null or undefined data.

```n8n-expression
$if(condition, "true", "false")
condition ? true : false
$ifEmpty(value, defaultValue)
```

--------------------------------

### Check Boolean Emptiness with isEmpty()

Source: https://docs.n8n.io/data/expression-reference/boolean

The isEmpty() method checks if a boolean value is null. It returns false for true or false values and true if the input is null.

```javascript
// bool = true
bool.isEmpty(); // => false

// bool = false
bool.isEmpty(); // => false

// bool = null
bool.isEmpty(); // => true
```

--------------------------------

### Extract values from objects using JMESPath

Source: https://docs.n8n.io/data/specific-data-types/jmespath

Demonstrates object projection to extract specific properties from a dictionary/object structure. Useful for aggregating values from nested keys.

```javascript
{{$jmespath($json.body.dogs, "*.age")}}
```

```javascript
let dogsAges = $jmespath($json.body.dogs, "*.age");
return {dogsAges};
```

```python
dogsAges = _jmespath(_json.body.dogs, "*.age")
return {"dogsAges": dogsAges}
```

--------------------------------

### Update Brand Name via Localization

Source: https://docs.n8n.io/embed/white-labelling

Updating the English internationalization JSON file to replace default n8n branding with custom brand names using Vue I18n keys.

```json
{
	"_brand.name": "My Brand",
	"about.aboutN8n": "About @:_brand.name",
	"about.n8nVersion": "@:_brand.name Version"
}
```

--------------------------------

### Slice a collection using JMESPath

Source: https://docs.n8n.io/data/specific-data-types/jmespath

Uses slice projection to retrieve a subset of elements from a list based on index range. Applicable in expressions and code nodes.

```javascript
{{$jmespath($json.body.people, "[:2].first")}}
```

```javascript
let firstTwoNames = $jmespath($json.body.people, "[:2].first");
return {firstTwoNames};
```

```python
firstTwoNames = _jmespath(_json.body.people, "[:2].first" )
return {"firstTwoNames":firstTwoNames}
```

--------------------------------

### Convert Boolean to String in JavaScript

Source: https://docs.n8n.io/data/expression-reference/boolean

The toString() method converts a boolean value (true or false) into its corresponding string representation ('true' or 'false'). It requires no arguments and returns a string.

```javascript
// bool = true
bool.toString(); // => 'true'

// bool = false
bool.toString(); // => 'false'
```

--------------------------------

### Handle item-level errors in n8n loops

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/error-handling

Shows how to process multiple items in a loop while handling potential errors. It supports the 'continue on fail' setting by catching errors and returning them as part of the output data, or throwing a NodeOperationError if the failure should stop the execution.

```TypeScript
for (let i = 0; i < items.length; i++) {
	try {
		// Process item
		const result = await processItem(items[i]);
		returnData.push(result);
	} catch (error) {
		if (this.continueOnFail()) {
			returnData.push({
				json: { error: error.message },
				pairedItem: { item: i },
			});
			continue;
		}

		throw new NodeOperationError(this.getNode(), error as Error, {
			description: error.description,
			itemIndex: i,
		});
	}
}
```

--------------------------------

### Convert String to Title Case

Source: https://docs.n8n.io/data/expression-reference/string

Converts a string to title case, capitalizing the first letter of each word while leaving other letters unchanged. Short prepositions and conjunctions are not capitalized. This is a custom n8n functionality.

```javascript
"quick a brown FOX".toTitleCase() //=> "Quick a Brown Fox"
```

--------------------------------

### Output to Browser Console with console.log() (JavaScript)

Source: https://docs.n8n.io/code/cookbook/code-node/console-log

Use console.log() within the n8n Code node to output variable values or messages to the browser's developer console. This is useful for debugging JavaScript code. Ensure the Code node is configured for JavaScript execution.

```javascript
let a = "apple";
console.log(a);
```

--------------------------------

### Array.difference()

Source: https://docs.n8n.io/data/expression-reference/array

Compares two arrays. Returns all elements in the base array that aren't present in `otherArray`.

```APIDOC
## Array.difference()

### Description
Compares two arrays. Returns all elements in the base array that aren't present in `otherArray`.

### Method
Array.difference(otherArray)

### Parameters
#### Path Parameters
- **otherArray** (Array) - Required - The array to compare to the base array

### Request Example
```json
{
  "example": "// arr = [1, 2, 3]\narr.difference([2, 3]) //=> [1]"
}
```

### Response
#### Success Response (200)
- **Array** (Array) - An array containing elements from the base array not present in `otherArray`.

#### Response Example
```json
{
  "example": "[1]"
}
```
```

--------------------------------

### OAuth2 Authorization Code Grant Type Configuration

Source: https://docs.n8n.io/integrations/builtin/credentials/httprequest

Configures OAuth2 using the Authorization Code grant type to exchange an authorization code for an access token. Requires an Authorization URL, Access Token URL, Client ID, Client Secret, and optionally Scopes, Auth URI Query Parameters, and Authentication type (Header or Body). SSL issues can be ignored.

```text
Authorization URL: [URL]
Access Token URL: [URL]
Client ID: [ID]
Client Secret: [Secret]
Scope: [Scope(s)] (Optional)
Auth URI Query Parameters: [Parameters] (Optional)
Authentication: Header or Body
Ignore SSL Issues: true or false (Optional)
```

--------------------------------

### Discord Node for Notifications

Source: https://docs.n8n.io/_workflows//courses/level-one/finished.json

Configures a Discord node to send a notification message. The message content is dynamically generated using expressions to include the total booked orders, total value, and a unique ID from the HTTP Request node. Requires Discord webhook authentication.

```json
{
  "parameters": {
    "authentication": "webhook",
    "content": "=This week we've {{$json["totalBooked"]}} booked orders with a total value of {{$json["bookedSum"]}}. My Unique ID: {{ $('HTTP Request').params["headerParameters"]["parameters"][0]["value"] }}",
    "options": {}
  },
  "type": "n8n-nodes-base.discord",
  "typeVersion": 1,
  "position": [
    880,
    60
  ],
  "id": "17834072-1a46-4604-872a-1d06477c914a",
  "name": "Discord"
}
```

--------------------------------

### Retrieve custom execution data in n8n

Source: https://docs.n8n.io/workflows/executions/custom-executions-data

This snippet demonstrates how to access a specific value from the execution context's custom data store. It uses the _execution object to retrieve a value associated with a provided key.

```JavaScript
customData = _execution.customData.get("key");
```

--------------------------------

### Access All Custom Data Object (Python)

Source: https://docs.n8n.io/workflows/executions/custom-executions-data

Retrieves the entire custom data object as it currently exists during the workflow execution. This allows access to all previously set custom data. The data is returned as a Python dictionary.

```python
# Access the current state of the object during the execution
customData = _execution.customData.getAll();
```

--------------------------------

### Set All Custom Execution Data (Python)

Source: https://docs.n8n.io/workflows/executions/custom-executions-data

Overwrites the entire custom data object for the current workflow execution with a new set of key-value pairs. Each value must be a string, keys have a max length of 50 characters, and values have a max length of 255 characters. n8n supports a maximum of 10 items.

```python
_execution.customData.setAll({"key1": "value1", "key2": "value2"})
```

--------------------------------

### Conditional Logic with If Node (n8n)

Source: https://docs.n8n.io/_workflows//courses/level-one/chapter-5/chapter-5.6.json

Implements conditional branching in a workflow using an 'If' node. It evaluates conditions based on input data and routes the workflow execution accordingly. This node is essential for creating dynamic and responsive workflows.

```json
{
  "parameters": {
    "conditions": {
      "options": {
        "caseSensitive": true,
        "leftValue": "",
        "typeValidation": "strict",
        "version": 2
      },
      "conditions": [
        {
          "id": "526cb30c-0f90-4f66-8f98-b64ceb2e52f2",
          "leftValue": "={{ $json.orderStatus }}",
          "rightValue": "processing",
          "operator": {
            "type": "string",
            "operation": "equals"
          }
        }
      ],
      "combinator": "and"
    },
    "options": {}
  },
  "type": "n8n-nodes-base.if",
  "typeVersion": 2.2,
  "position": [
    520,
    -520
  ],
  "id": "70e4db65-f827-4e4f-8673-b405b7986d6e",
  "name": "If1"
}
```

--------------------------------

### Send Slack Message with User Input in n8n

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/ask_a_human.json

This node sends a message to a specified Slack channel. It constructs the message text to include a user's input that the bot couldn't answer. It requires configuration of the 'channelId' and the message 'text'.

```json
{
  "select": "channel",
  "channelId": {
    "__rl": true,
    "value": "",
    "mode": "name"
  },
  "text": "={{ "A user had a question the bot couldn't answer. Here's their message: " + $('Execute Workflow Trigger').item.json.chatInput }}",
  "otherOptions": {}
}
```

--------------------------------

### Transform nested JSON data structures

Source: https://docs.n8n.io/code/ai-code

This script demonstrates how to extract specific fields from nested JSON objects within an n8n workflow. It maps input items to a new structure containing only the required first name and job title fields.

```javascript
const items = $input.all();
const newItems = items.map((item) => {
  const firstName = item.json.personal_info.first_name;
  const jobTitle = item.json.work_info.job_title;
  return {
    json: {
      firstName,
      jobTitle,
    },
  };
});
return newItems;
```

--------------------------------

### n8n Workflow Item Data Schema (JSON)

Source: https://docs.n8n.io/embed/workflow-templates

A detailed JSON schema defining the structure of a workflow item in n8n. This schema is used by the `/templates/workflows/{id}` endpoint and includes metadata like ID, name, views, price, user information, and the nested workflow definition with nodes and connections.

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Generated schema for Root",
  "type": "object",
  "properties": {
    "id": {
      "type": "number"
    },
    "name": {
      "type": "string"
    },
    "totalViews": {
      "type": "number"
    },
    "price": {},
    "purchaseUrl": {},
    "recentViews": {
      "type": "number"
    },
    "createdAt": {
      "type": "string"
    },
    "user": {
      "type": "object",
      "properties": {
        "username": {
          "type": "string"
        },
        "verified": {
          "type": "boolean"
        }
      },
      "required": [
        "username",
        "verified"
      ]
    },
    "nodes": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {
            "type": "number"
          },
          "icon": {
            "type": "string"
          },
          "name": {
            "type": "string"
          },
          "codex": {
            "type": "object",
            "properties": {
              "data": {
                "type": "object",
                "properties": {
                  "details": {
                    "type": "string"
                  },
                  "resources": {
                    "type": "object",
                    "properties": {
                      "generic": {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "url": {
                              "type": "string"
                            },
                            "icon": {
                              "type": "string"
                            },
                            "label": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "url",
                            "label"
                          ]
                        }
                      },
                      "primaryDocumentation": {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "url": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "url"
                          ]
                        }
                      }
                    },
                    "required": [
                      "primaryDocumentation"
                    ]
                  },
                  "categories": {
                    "type": "array",
                    "items": {
                      "type": "string"
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
}
```

--------------------------------

### Credential Overwrite JSON Structure (JSON)

Source: https://docs.n8n.io/embed/configuration

This JSON structure defines the format for credential overwrites. It maps credential names (e.g., `asanaOAuth2Api`, `githubOAuth2Api`) to their respective parameters that need to be overwritten, such as `clientId` and `clientSecret`.

```json
{
    "asanaOAuth2Api": {
        "clientId": "<id>",
        "clientSecret": "<secret>"
    },
    "githubOAuth2Api": {
        "clientId": "<id>",
        "clientSecret": "<secret>"
    }
}
```

--------------------------------

### Enable Drag and Drop Nodes in Editor

Source: https://docs.n8n.io/release-notes/0-x

The n8n editor now supports dragging and dropping nodes directly from the nodes panel onto the canvas. This enhancement provides a more intuitive and efficient user experience for building workflows.

```javascript
editor : you can now drag and drop nodes from the nodes panel onto the canvas.
```

--------------------------------

### Send Media Group

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/message-operations

Sends a group of photos and/or videos using the Bot API's sendMediaGroup method. Requires a Telegram credential and specifies the chat ID and media details.

```APIDOC
## POST /sendMediaGroup

### Description
Use this operation to send a group of photos and/or videos using the Bot API sendMediaGroup method.

### Method
POST

### Endpoint
/sendMediaGroup

### Parameters
#### Request Body
- **credential** (object) - Required - Credential to connect with Telegram.
- **chatId** (string) - Required - The Chat ID or username of the channel you wish to send the media group to in the format `@channelusername`.
- **media** (array) - Required - Use 'Add Media' to add different media types to your media group. Each item should include:
  - **type** (string) - Required - The type of media. Choose from 'Photo' and 'Video'.
  - **mediaFile** (string) - Required - Enter the media file to send. Pass a `file_id` or an HTTP URL.
  - **caption** (string) - Optional - Enter a caption text for the file, max of 1024 characters.
  - **parseMode** (string) - Optional - Enter the parser to use for any related text. Options include 'HTML' (default), 'Markdown (Legacy)', 'MarkdownV2'.

### Request Example
```json
{
  "credential": "<your_credential_id>",
  "chatId": "@channelusername",
  "media": [
    {
      "type": "Photo",
      "mediaFile": "AgADBAADzKcxG9_y_Vf458_Z_Vf458_Z",
      "caption": "Beautiful sunset"
    },
    {
      "type": "Video",
      "mediaFile": "http://example.com/video.mp4"
    }
  ]
}
```

### Response
#### Success Response (200)
- **result** (array) - An array of sent message objects.

#### Response Example
```json
{
  "result": [
    {
      "message_id": 12346,
      "chat": {
        "id": 123456789,
        "type": "private"
      },
      "photo": [
        {
          "file_id": "AgADBAADzKcxG9_y_Vf458_Z_Vf458_Z",
          "file_unique_id": "...",
          "width": 320,
          "height": 240,
          "file_size": 10000
        }
      ],
      "caption": "Beautiful sunset",
      "date": 1678886401
    },
    {
      "message_id": 12347,
      "chat": {
        "id": 123456789,
        "type": "private"
      },
      "video": {
        "file_id": "...",
        "file_unique_id": "...",
        "width": 640,
        "height": 480,
        "duration": 10,
        "file_size": 50000
      },
      "date": 1678886402
    }
  ]
}
```

### Additional Fields
- **disableNotification** (boolean) - Optional - Choose whether to send the notification silently (turned on) or with a standard notification (turned off).
- **replyToMessageId** (integer) - Optional - If the message is a reply, enter the ID of the message it's replying to.
- **messageThreadId** (integer) - Optional - Enter a unique identifier for the target message thread (topic) of the forum; for forum supergroups only.
```

--------------------------------

### PATCH /v1/blocks/{block_id}

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.notion/common-issues

Updates the properties of a block, such as enabling the toggleable feature for heading blocks.

```APIDOC
## PATCH /v1/blocks/<block_id>

### Description
Updates the configuration of a specific block. Used here to set the `is_toggleable` property to true for heading blocks.

### Method
PATCH

### Endpoint
https://api.notion.com/v1/blocks/<block_id>

### Parameters
#### Path Parameters
- **block_id** (string) - Required - The unique identifier of the block.

#### Request Body
- **heading_1** (object) - Required - The heading block object containing the updated `is_toggleable` field.

### Request Example
{
	"heading_1": {
		"is_toggleable": true
	}
}
```

--------------------------------

### Access Custom Data in n8n Execution

Source: https://docs.n8n.io/code/cookbook/builtin/execution

This snippet demonstrates how to retrieve a specific value from the custom data set during an n8n workflow execution. It uses the `_execution.customData.get()` method, expecting a 'key' as input and returning the associated value. Ensure the key exists in the custom data to avoid errors.

```javascript
customData = _execution.customData.get("key")
```

--------------------------------

### Calculate Time Difference Between Two Dates with Luxon

Source: https://docs.n8n.io/data/specific-data-types/luxon

Determine the duration between two dates using Luxon's `diff()` method. This method subtracts one `DateTime` object from another and returns a duration object, which can then be converted to a plain object using `toObject()`. You can specify the unit of time for the difference (e.g., 'months', 'days', 'hours').

```javascript
{{DateTime.fromISO('2019-06-23').diff(DateTime.fromISO('2019-05-23'), 'months').toObject()}}
```

```javascript
let monthsBetweenDates = DateTime.fromISO('2019-06-23').diff(DateTime.fromISO('2019-05-23'), 'months').toObject()
```

--------------------------------

### Generate RSS Feed URLs with JavaScript Code Node

Source: https://docs.n8n.io/courses/level-two/chapter-3

This JavaScript code snippet is designed for an n8n Code node. It generates a list of objects, each containing a URL for an RSS feed from Medium and dev.to. This node should be configured to 'Run Once for All Items'. The output serves as input for subsequent nodes in the workflow.

```javascript
let urls = [
	{
		json: {
		url: 'https://medium.com/feed/n8n-io'
		}
	},
	{
	json: {
		url: 'https://dev.to/feed/n8n'
	}
	}
]
return urls;
```

--------------------------------

### Convert strings to booleans with toBoolean()

Source: https://docs.n8n.io/data/expression-reference/string

A custom n8n method that converts strings to boolean values. It treats '0', 'false', and 'no' as false, while all other values resolve to true.

```javascript
"true".toBoolean();
"false".toBoolean();
"0".toBoolean();
"hello".toBoolean();
```

--------------------------------

### Manage Custom Execution Data

Source: https://docs.n8n.io/code/cookbook/builtin/execution

Provides methods to store and retrieve custom data associated with a workflow execution within a Code node. Supports setting individual keys, bulk objects, and retrieving stored values.

```JavaScript
// Set a single piece of custom execution data
$execution.customData.set("key", "value");

// Set the custom execution data object
$execution.customData.setAll({"key1": "value1", "key2": "value2"})

// Access the current state of the object during the execution
var customData = $execution.customData.getAll()

// Access a specific value set during this execution
var customData = $execution.customData.get("key")
```

```Python
# Set a single piece of custom execution data
_execution.customData.set("key", "value");

# Set the custom execution data object
_execution.customData.setAll({"key1": "value1", "key2": "value2"})

# Access the current state of the object during the execution
customData = _execution.customData.getAll()
```

--------------------------------

### Handle LinkedIn Webhook Challenge Request

Source: https://docs.n8n.io/integrations/builtin/credentials/linkedin

Responds to LinkedIn's webhook challenge request with a JSON payload containing the original challenge code and its HMAC-SHA256 hash. This is crucial for validating the webhook endpoint.

```json
{
  "challengeCode": "890e4665-4dfe-4ab1-b689-ed553bceeed0",
  "challengeResponse": "27b1d19678542072a7f1d0ce845d0c78cec22567f413697e25648f44fa3d1514"
}
```

--------------------------------

### Delete an Assistant

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-langchain.openai/assistant-operations

Deletes an existing assistant from your OpenAI account.

```APIDOC
## DELETE /assistants/{assistant_id}

### Description
Use this operation to delete an existing assistant from your account.

### Method
DELETE

### Endpoint
/assistants/{assistant_id}

### Parameters
#### Path Parameters
- **assistant_id** (string) - Required - The ID of the assistant to delete.

#### Request Body
- **credential** (object) - Required - OpenAI credential to connect with.
- **resource** (string) - Required - Must be 'Assistant'.
- **operation** (string) - Required - Must be 'Delete an Assistant'.

### Request Example
```json
{
  "credential": {"id": "your_credential_id"},
  "resource": "Assistant",
  "operation": "Delete an Assistant"
}
```

### Response
#### Success Response (200)
- **id** (string) - The ID of the deleted assistant.
- **deleted** (boolean) - Indicates if the assistant was successfully deleted.

#### Response Example
```json
{
  "id": "asst_abc123",
  "deleted": true
}
```
```

--------------------------------

### Replace String Patterns in n8n

Source: https://docs.n8n.io/data/expression-reference/string

Replaces occurrences of a pattern with a replacement string or function. Use replace() for the first occurrence and replaceAll() for all occurrences.

```JavaScript
'Red or blue or green'.replace('or', 'and');
let text = "Mr Blue has a blue house and a blue car";
text.replace(/blue/gi, "red");
text.replaceAll(/blue|car/gi, x => x.toUpperCase());
```

--------------------------------

### JavaScript Data Transformation in n8n Code Node

Source: https://docs.n8n.io/_workflows/ai-code/data-transformation.json

This snippet shows how to use JavaScript within an n8n code node to transform and structure data. It takes an array of objects as input and returns a new array of objects with specified fields. This is useful for cleaning, reformatting, or enriching data before it's passed to subsequent nodes. The code assumes the input data is implicitly available and returns the transformed data.

```javascript
return [
{
"user_id":
"0001",
"username":
"nathan",
"date":
"2023-08-10",
"variant":
"control",
"data_exec_success":
"TRUE"
},
{
"user_id":
"0002",
"username":
"natalie",
"date":
"2023-08-10",
"variant":
"control",
"data_exec_success":
"TRUE"
},
{
"user_id":
"0003",
"username":
"nadia",
"date":
"2023-08-10",
"variant":
"control",
"data_exec_success":
"FALSE"
},
{
"user_id":
"naomi",
"username":
"hkhjk",
"date":
"2023-08-10",
"variant":
"control",
"data_exec_success":
"FALSE"
},
{
"user_id":
"0005",
"username":
"nolan",
"date":
"2023-08-10",
"variant":
"control",
"data_exec_success":
"FALSE"
}
]
```

--------------------------------

### String isDomain() - Check if string is a domain

Source: https://docs.n8n.io/data/expression-reference/string

Determines if the given string represents a valid domain name. It returns true for domain names and false for strings that include protocols or are not valid domain formats.

```javascript
"n8n.io".isDomain() //=> true
"http://n8n.io".isDomain() //=> false
"hello".isDomain() //=> false
```

--------------------------------

### Format Number with Specific Locale - JavaScript

Source: https://docs.n8n.io/data/expression-reference/number

Shows how to format a number using a specific locale, such as French ('fr-FR'), with Number.toLocaleString(). The 'locales' parameter accepts a string or an array of strings.

```javascript
let num = 500000.125;
console.log(num.toLocaleString('fr-FR')); //=> '500 000,125'
```

--------------------------------

### Category Item Data Schema

Source: https://docs.n8n.io/workflows/templates

Schema definition for a category item within the n8n API.

```APIDOC
## Category Item Data Schema

### Description
This schema defines the structure of a category item.

### Method
GET

### Endpoint
/templates/categories

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **id** (number) - The unique identifier for the category.
- **name** (string) - The name of the category.

### Response Example
```json
{
  "id": 1,
  "name": "Data & Databases"
}
```
```

--------------------------------

### Set All Custom Execution Data (JavaScript)

Source: https://docs.n8n.io/workflows/executions/custom-executions-data

Overwrites the entire custom data object for the current workflow execution with a new set of key-value pairs. Each value must be a string, keys have a max length of 50 characters, and values have a max length of 255 characters. n8n supports a maximum of 10 items.

```javascript
$execution.customData.setAll({"key1": "value1", "key2": "value2"})
```

--------------------------------

### Hash String - JavaScript

Source: https://docs.n8n.io/data/expression-reference/string

Returns a hashed version of the input string using a specified algorithm, defaulting to MD5. Supports various algorithms like SHA variants and RIPEMD160.

```javascript
"hello".hash() //=> '5d41402abc4b2a76b9719d911017c592'
```

--------------------------------

### Convert DateTime to Milliseconds Timestamp (Luxon)

Source: https://docs.n8n.io/data/expression-reference/datetime

Returns a Unix timestamp in milliseconds, representing the number of milliseconds elapsed since January 1, 1970.

```javascript
$now.toMillis() //=> 1712334324677
```

--------------------------------

### Array.concat()

Source: https://docs.n8n.io/data/expression-reference/array

Joins one or more arrays onto the end of the base array.

```APIDOC
## Array.concat()

### Description
Joins one or more arrays onto the end of the base array.

### Method
Array.concat(array2, array3?, ... arrayN?)

### Parameters
#### Path Parameters
- **array2** (Array) - Required - The first array to be joined on the end of the base array
- **array3** (Array) - Optional - The second array to be joined on to the end of the base array
- **arrayN** (Array) - Optional - The Nth array to be joined on to the end of the base array

### Request Example
```json
{
  "example": "// arr1 = ['Nathan', 'Jan']\narr1.concat(['Steve', 'Bill']) // ['Nathan', 'Jan', 'Steve', 'Bill']"
}
```

### Response
#### Success Response (200)
- **Array** (Array) - The joined array.

#### Response Example
```json
{
  "example": "['Nathan', 'Jan', 'Steve', 'Bill']"
}
```
```

--------------------------------

### Enhance Microsoft Teams Node Functionality

Source: https://docs.n8n.io/release-notes/0-x

Several enhancements have been made to the Microsoft Teams node. These include options to limit group retrieval to 'member of', fetch all tasks from a plan (not just a group member), and autocompletion for various fields in task update operations.

```javascript
Microsoft Teams node: adds several enhancements:
    * An option to limit groups to "member of", rather than retrieving the whole directory.
    * An option to get all tasks from a plan instead of just a group member.
    * Autocompletion for plans, buckets, labels, and members in update fields for tasks.
```

--------------------------------

### Feature-Based Versioning Definition in n8n Nodes

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-versioning

Defines features for an n8n node using a 'features' object, where each feature is tied to specific node versions using '@version' conditions. This enables conditional logic and parameter visibility based on enabled features.

```typescript
{
    version: [2, 2.1, 2.2, 2.3, 2.4],
    features: {
        useNewApi: { '@version': [{ _cnd: { gte: 2.2 } }] },
        useLegacyAuth: { '@version': [{ _cnd: { lte: 2.1 } }] },
        useSpecialMode: { '@version': [2] },
    },
    // More basic parameters here
}
```

--------------------------------

### Configure NODES_EXCLUDE environment variable

Source: https://docs.n8n.io/hosting/securing/blocking-nodes

Use the NODES_EXCLUDE environment variable to define an array of node identifiers that should be restricted. This configuration prevents users from searching for or utilizing the specified nodes within the n8n interface.

```environment
NODES_EXCLUDE: "[\"n8n-nodes-base.executeCommand\", \"n8n-nodes-base.readWriteFile\"]"
```

--------------------------------

### OIDC SSO Error: State Parameter Not Supported

Source: https://docs.n8n.io/user-management/oidc/troubleshooting

This snippet illustrates the error message received when an OIDC provider enforces the 'state' parameter, which n8n's current implementation does not support. This typically results in an authorization response error from the server.

```text
{"code":0,"message":"authorization response from the server is an error"}
```

--------------------------------

### Send Discord Notification (n8n)

Source: https://docs.n8n.io/_workflows//courses/level-one/chapter-5/chapter-5.6.json

Configures a Discord node to send messages to a Discord channel. It supports dynamic content generation using expressions that reference workflow data, including values calculated by other nodes. This node is used for real-time alerts and reporting.

```json
{
  "parameters": {
    "authentication": "webhook",
    "content": "=This week we've {{$json["totalBooked"]}} booked orders with a total value of {{$json["bookedSum"]}}. My Unique ID: {{ $('HTTP Request1').params["headerParameters"]["parameters"][0]["value"] }}",
    "options": {}
  },
  "type": "n8n-nodes-base.discord",
  "typeVersion": 1,
  "position": [
    1020,
    -420
  ],
  "id": "c9a1221c-010f-4189-819a-143471210147",
  "name": "Discord1"
}
```

--------------------------------

### Convert String to Sentence Case

Source: https://docs.n8n.io/data/expression-reference/string

Transforms a string into sentence case, capitalizing the first letter of each sentence and lowercasing the rest. This is a custom n8n functionality.

```javascript
"quick! brown FOX".toSentenceCase() //=> "Quick! Brown fox"
```

--------------------------------

### Access All Custom Data Object (JavaScript)

Source: https://docs.n8n.io/workflows/executions/custom-executions-data

Retrieves the entire custom data object as it currently exists during the workflow execution. This allows access to all previously set custom data. The data is returned as a JavaScript object.

```javascript
// Access the current state of the object during the execution
const customData = $execution.customData.getAll();
```

--------------------------------

### Add Markdown to HTML Conversion Node

Source: https://docs.n8n.io/release-notes/0-x

A new Markdown node has been introduced, enabling conversion between Markdown and HTML formats. This node provides a convenient way to process and transform text content within n8n workflows.

```javascript
Markdown node: added a new Markdown node to convert between Markdown and HTML.
```

--------------------------------

### Set Single Custom Execution Data (Python)

Source: https://docs.n8n.io/workflows/executions/custom-executions-data

Sets a single key-value pair of custom data for the current workflow execution. The value must be a string and has a maximum length of 255 characters. The key has a maximum length of 50 characters. This method is part of the n8n execution context.

```python
_execution.customData.set("key", "value");
```

--------------------------------

### Date and Time Formatting

Source: https://docs.n8n.io/data/expression-reference

Expressions to retrieve current temporal data and format it into specific string representations. Useful for logging, file naming, or API timestamps.

```n8n-expression
$now
$today
$now.toFormat("yyyy-MM-dd")
```

--------------------------------

### Define AI Fallback Response with JavaScript

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/ask_a_human.json

This code snippet uses an n8n Code node to return a structured JSON response. It is triggered when the AI agent cannot answer a query, prompting the user to provide an email address for further assistance.

```javascript
response = {"response":"I'm sorry I don't know the answer. Please repeat your question and include your email address so I can request help."};
return response;
```

--------------------------------

### Prepare Data Output with JavaScript

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/chat_with_google_sheets_docs_version.json

This snippet uses the n8n Code node to transform input data into a JSON-stringified format. It maps all incoming JSON objects and returns them as a single string under the 'response' key.

```javascript
return {
  'response': JSON.stringify($input.all().map(x => x.json))
}
```

--------------------------------

### Unset n8n Diagnostics Configuration

Source: https://docs.n8n.io/hosting/configuration/configuration-examples/isolation

Clears specific environment variables related to frontend and backend diagnostic hooks. This ensures that no diagnostic reporting endpoints are configured for the instance.

```bash
EXTERNAL_FRONTEND_HOOKS_URLS=
N8N_DIAGNOSTICS_CONFIG_FRONTEND=
N8N_DIAGNOSTICS_CONFIG_BACKEND=
```

--------------------------------

### Handle JSON Path Headers in Google Sheets Node

Source: https://docs.n8n.io/release-notes/0-x

The Google Sheets node has been enhanced to handle header names formatted as JSON paths. This allows for more flexible and structured data mapping when interacting with Google Sheets, improving compatibility with complex data formats.

```javascript
Google Sheets node: n8n now handles header names formatted as JSON paths.
```

--------------------------------

### Convert String to Number

Source: https://docs.n8n.io/data/expression-reference/string

Converts a string representation of a number into an actual number. It throws an error if the string does not begin with a valid numerical format. This is a custom n8n functionality.

```javascript
"123".toNumber() //=> 123
"1.23E10".toNumber() //=> 12300000000
```

--------------------------------

### Retrieve DateTime units

Source: https://docs.n8n.io/data/expression-reference/datetime

Accesses specific components of the DateTime object, such as the quarter of the year or the current second.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.quarter // => 1

// dt = "2024-03-30T18:49:07.234".toDateTime()
dt.second // => 7
```

--------------------------------

### Number.floor()

Source: https://docs.n8n.io/data/expression-reference/number

Rounds a number down to the nearest whole number.

```APIDOC
## Number.floor()

### Description
Rounds the number down to the nearest whole number.

### Syntax
Number.floor()

### Returns
Number

### Response Example
// x = 1.234
x.floor() //=> 1
```

--------------------------------

### Check for Email Format using Regex in n8n

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/ask_a_human.json

This 'if' node checks if a user's input contains a valid email address using a regular expression. It performs a strict, case-sensitive comparison. The input is taken from the 'chatInput' of the 'Execute Workflow Trigger'.

```json
{
  "conditions": {
    "options": {
      "caseSensitive": true,
      "leftValue": "",
      "typeValidation": "strict"
    },
    "conditions": [
      {
        "id": "5e21e7c5-db60-4111-bb17-c289ae0fc159",
        "leftValue": "={{ $('Execute Workflow Trigger').item.json.chatInput }}",
        "rightValue": "/([a-zA-Z0-9._-]+@[a-zA-Z0-9._-]+\.[a-zA-Z0-9_-]+)/gi",
        "operator": {
          "type": "string",
          "operation": "regex"
        }
      }
    ],
    "combinator": "and"
  },
  "options": {}
}
```

--------------------------------

### Extract substrings with substring()

Source: https://docs.n8n.io/data/expression-reference/string

Returns a subset of a string between two specified indices. Similar to slice, but does not support negative indices.

```javascript
'Hello from n8n'.substring(0, 5);
'Hello from n8n'.substring(6);
```

--------------------------------

### Convert Number to String with Radix (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/number

Converts a number to its string representation using a specified radix (base). The radix must be an integer between 2 and 36. This is commonly used for binary, octal, or hexadecimal conversions.

```javascript
let num = 500000.125;
console.log(num.toString(16)); // Output: '7a120.2'
```

--------------------------------

### Configure Error Workflow with Slack Notification

Source: https://docs.n8n.io/courses/level-two/chapter-4

A JSON representation of an n8n workflow that uses the Error Trigger node to capture failures and send a notification to Slack. This workflow extracts the failed workflow name and execution URL from the trigger data.

```json
{
	"nodes": [
		{
			"parameters": {},
			"name": "Error Trigger",
			"type": "n8n-nodes-base.errorTrigger",
			"typeVersion": 1,
			"position": [
				720,
				-380
			]
		},
		{
			"parameters": {
				"channel": "channelname",
				"text": "=This workflow {{$(\"Error Trigger\").item.json[\"workflow\"][\"name\"]}}failed.\nHave a look at it here: {{$(\"Error Trigger\").item.json[\"execution\"][\"url\"]}}",
				"attachments": [],
				"otherOptions": {}
			},
			"name": "Slack",
			"type": "n8n-nodes-base.slack",
			"position": [
				900,
				-380
			],
			"typeVersion": 1,
			"credentials": {
				"slackApi": {
					"id": "17",
					"name": "slack_credentials"
				}
			}
		}
	],
	"connections": {
		"Error Trigger": {
			"main": [
				[
					{
						"node": "Slack",
						"type": "main",
						"index": 0
					}
				]
			]
		}
	}
}
```

--------------------------------

### Pass Data to Embedded Chat Trigger Node (JavaScript)

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-langchain.chattrigger/common-issues

Demonstrates how to pass arbitrary data from a website to an embedded Chat Trigger node. This is achieved by including a `metadata` object within the `createChat` function call. The data in `metadata` will be available in the Chat Trigger's output for further processing in n8n.

```javascript
createChat({
	webhookUrl: 'YOUR_PRODUCTION_WEBHOOK_URL',
	metadata: {
		'YOUR_KEY': 'YOUR_DATA'
	}
});
```

--------------------------------

### Merge Two Objects (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/object

The `merge(otherObject)` method merges the current object with `otherObject`. If a key exists in both objects, the value from the first (base) object is retained. It returns the merged object. This is a custom n8n functionality.

```javascript
// obj1 = {'name':'Nathan', 'age': 42}
// obj2 = {'name':'Jan', 'city': 'hanoi'}
obj1.merge(obj2) //=> {'name':'Jan', 'city': 'hanoi', 'age':42}
```

--------------------------------

### Health Check

Source: https://docs.n8n.io/workflows/templates

A simple endpoint to check the health status of the API.

```APIDOC
## GET /health

### Description
Health check endpoint.

### Method
GET

### Endpoint
`/health`

### Response
#### Success Response (200)
- **status** (string) - The health status of the API (e.g., "OK").

#### Response Example
```json
{
  "status": "OK"
}
```
```

--------------------------------

### Fix Filtering Executions by Waiting Status

Source: https://docs.n8n.io/release-notes/0-x

A fix has been implemented for filtering the executions list by waiting status. This ensures that users can accurately filter and view workflow executions based on their current waiting status.

```javascript
**core** : a fix for filtering the executions list by waiting status.
```

--------------------------------

### Manually link output items to input items in n8n

Source: https://docs.n8n.io/data/data-mapping/data-item-linking/item-linking-code-node

When returning new items from a Code node, you can explicitly link them to a specific input item by setting the 'pairedItem' property. This allows subsequent nodes to reference the original input data via the item linking mechanism.

```json
[
	{
		"json": {
			"key": "value"
		},
		"pairedItem": 0
	}
]
```

--------------------------------

### Calculate Difference Between Two DateTimes

Source: https://docs.n8n.io/data/expression-reference/datetime

Calculates the difference between two DateTime objects in specified units. It accepts ISO date strings or Luxon DateTime objects for the comparison and can return the difference in various units like days, months, or years.

```javascript
// dt1 = "2024-03-30T18:49:07.234".toDateTime()
dt1.diffTo('2025-01-01', 'days') //=> 276.21
```

```javascript
// dt1 = "2024-03-30T18:49:07.234".toDateTime()
// dt2 = "2025-01-01T00:00:00.000".toDateTime()
dt1.diffTo(dt2, ['months', 'days']) //=> {'months':, 'days':}
```

--------------------------------

### Correct Data Structure for Code Node Output

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.code/common-issues

Ensures data returned from the Code node follows the expected n8n format, which is an array of objects, each containing a 'json' key that holds another object with your data. This is crucial for proper data flow between nodes.

```javascript
[
  {
    "json": {
	  // your data goes here
	}
  }
]
```

--------------------------------

### Conditional Date Check in n8n 'If' Node

Source: https://docs.n8n.io/courses/level-two/chapter-2

Configures an 'If' node to check if a 'new-date' value from JSON is after a specific date ('1960-01-01T00:00:00'). This is useful for implementing conditional logic based on date comparisons within a workflow.

```json
{
	"leftValue": "={{ $json['new-date'] }}",
	"rightValue": "1960-01-01T00:00:00",
	"operator": {
		"type": "dateTime",
		"operation": "after"
	}
}
```

--------------------------------

### Execute JMESPath query in n8n

Source: https://docs.n8n.io/data/specific-data-types/jmespath

The jmespath() method allows for searching JSON objects using the JMESPath query language. Note that the parameter order is (object, searchString), which differs from the standard JMESPath library specification.

```JavaScript
$jmespath(object, searchString)
```

```Python
_jmespath(object, searchString)
```

--------------------------------

### Send Discord Messages via HTTP Request

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.discord/common-issues

This snippet provides the API endpoint and the required JSON body structure for sending messages with embeds directly to the Discord API. This approach is recommended when the standard Discord node does not support specific API features.

```text
https://discord.com/api/v10/channels/<CHANNEL_ID>/messages
```

```json
{
	"content": "Test",
	"embeds": [
		{
			"author": "My Name",
			"url": "https://discord.js.org",
			"fields": [
				{
					"name": "Regular field title",
					"value": "Some value here"
				}
			],
			"footer": {
				"text": "Some footer text here",
				"icon_url": "https://i.imgur.com/AfFp7pu.png"
			}
		}
	]
}
```

--------------------------------

### String isNotEmpty() - Check if string has content

Source: https://docs.n8n.io/data/expression-reference/string

Determines if a string contains at least one character. It returns true for strings with content and false for empty or null strings.

```javascript
"hello".isNotEmpty() // => true
"".isNotEmpty() // => false
```

--------------------------------

### Number.toDateTime()

Source: https://docs.n8n.io/data/expression-reference/number

Converts a numerical timestamp into a DateTime object.

```APIDOC
## Number.toDateTime()

### Description
Converts a numerical timestamp into a DateTime. The format of the timestamp must be specified if it’s not in milliseconds.

### Syntax
Number.toDateTime(format?)

### Parameters
- **format** (String) - Optional - The type of timestamp: 'ms' (milliseconds), 's' (seconds), or 'excel' (days since 1900).

### Response Example
// ts = 1708695471
ts.toDateTime('s') //=> 2024-02-23T14:37:51+01:00
```

--------------------------------

### Generate New Items with PairedItem in JavaScript

Source: https://docs.n8n.io/data/data-mapping/data-item-linking/item-linking-code-node

This JavaScript code snippet demonstrates how to generate new items from existing ones, adding a new field and crucially, including a 'pairedItem' property. The 'pairedItem' property links the newly created item back to its original source item, enabling traceability. This is useful for maintaining relationships between data in workflows.

```javascript
newItems = [];
for(let i=0; i<items.length; i++){
  newItems.push(
    {
      "json":
        {
          "name": items[i].json.name,
				"aBrandNewField": "New data for item " + i
        },
      "pairedItem": i
    }    
  )
}
return newItems;
```

--------------------------------

### Error Trigger Data Structure (n8n)

Source: https://docs.n8n.io/flow-logic/error-handling

This JSON structure represents the default error data received by the Error Trigger in n8n when an execution fails. It includes details about the execution, workflow, and the specific error encountered. Note that 'execution.id' and 'execution.url' are not always present, and 'execution.retryOf' is only present during retries.

```json
[
	{
		"execution": {
			"id": "231",
			"url": "https://n8n.example.com/execution/231",
			"retryOf": "34",
			"error": {
				"message": "Example Error Message",
				"stack": "Stacktrace"
			},
			"lastNodeExecuted": "Node With Error",
			"mode": "manual"
		},
		"workflow": {
			"id": "1",
			"name": "Example Workflow"
		}
	}
]
```

--------------------------------

### Set Single Custom Execution Data (JavaScript)

Source: https://docs.n8n.io/workflows/executions/custom-executions-data

Sets a single key-value pair of custom data for the current workflow execution. The value must be a string and has a maximum length of 255 characters. The key has a maximum length of 50 characters. This method is part of the n8n execution context.

```javascript
$execution.customData.set("key", "value");
```

--------------------------------

### Audit Log API

Source: https://docs.n8n.io/api/api-reference

Endpoint for generating audit logs within the n8n instance.

```APIDOC
## POST /audit

### Description
Generate an audit log entry for specific actions or events within the instance.

### Method
POST

### Endpoint
https://{instance}.app.n8n.cloud/api/v1/audit

### Parameters
#### Request Body
- **additionalOptions** (object) - Optional - Additional options for audit generation.
  - **daysAbandonedWorkflow** (number) - Optional - Number of days to consider for abandoned workflows.
  - **categories** (array string) - Optional - Categories to include in the audit log (e.g., "credentials").

### Request Example
```curl
curl https://your-instance-name.app.n8n.cloud/api/v1/audit \
  --request POST \
  --header 'Content-Type: application/json' \
  --header 'X-N8N-API-KEY: YOUR_SECRET_TOKEN' \
  --data '{ "additionalOptions": { "daysAbandonedWorkflow": 1, "categories": [ "credentials" ] }}'
```

### Response
#### Success Response (200)
Operation successful. (Specific response body may vary based on implementation)

#### Error Response (401)
Unauthorized.

#### Error Response (403)
Forbidden.
```

--------------------------------

### Check Data Type in Python for '[object Object]' Output

Source: https://docs.n8n.io/code/cookbook/code-node/console-log

When encountering '[object Object]' in the console output for Python, use print(type(myData)) to inspect the data type of your variable. This helps in identifying the need for data conversion.

```python
print(type(myData))
```

--------------------------------

### Array Filtering (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/array

Creates a new array with all elements that pass the test implemented by the provided function. The function is called for each element and should return `true` to keep the element or `false` otherwise.

```javascript
// Keep ages over 18 (using arrow function notation):
// ages = [12, 33, 16, 40]
ages.filter(age => (age > 18)) //=> [33, 40]
```

```javascript
// Keep names under 5 letters long (using arrow function notation):
// names = ['Nathan', 'Bob', 'Sebastian']
ages.filter(age => (age.length < 5)) //=> ["Bob"]

// Or using traditional function notation:
ages.filter(function(age){return age.length < 5}) //=> ["Bob"]
```

```javascript
// Keep numbers at odd indexes
// nums = [1, 7, 3, 10, 5]
ages.filter((num, index) => {return index%2 != 0}) //=> [7, 10]
```

--------------------------------

### Validate user inputs with NodeOperationError in n8n

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/error-handling

Demonstrates how to validate node parameters and throw a NodeOperationError when input data is invalid. This provides specific feedback to the user, including the item index for better debugging.

```TypeScript
const email = this.getNodeParameter("email", itemIndex);

if (email.indexOf("@") === -1) {
	const description = `The email address '${email}' in the 'email' field isn't valid`;
	throw new NodeOperationError(this.getNode(), "Invalid email address", {
		description,
		itemIndex,
	});
}
```

--------------------------------

### Count items returned by previous node

Source: https://docs.n8n.io/code/cookbook/code-node/number-items-last-node

Calculates the length of the items array from the previous node. It checks if the input is empty to return a result of 0, otherwise it returns the total count of items.

```JavaScript
if (Object.keys(items[0].json).length === 0) {
	return [
		{
			json: {
				results: 0,
			}
		}
	]
}
return [
	{
		json: {
			results: items.length,
		}
	}
];
```

```Python
if len(items[0].json) == 0:
	return [
		{
			"json": {
				"results": 0,
			}
		}
	]
else:
	return [
		{
			"json": {
				"results": items.length,
			}
		}
	]
```

--------------------------------

### Initialize NodeOperationError

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/error-handling

Instantiate NodeOperationError for non-API related issues such as validation failures, configuration problems, or workflow logic errors. It accepts the node instance, an error object or string, and optional configuration.

```typescript
new NodeOperationError(node: INode, error: Error | string | JsonObject, options?: NodeOperationErrorOptions)
```

--------------------------------

### Create New List of Names with JavaScript Code Node

Source: https://docs.n8n.io/data/specific-data-types/jmespath

This JavaScript code snippet, intended for an n8n Code node, utilizes JMESPath to extract first and last names from the 'people' array and returns them as a new list named 'newList'. It demonstrates programmatic data transformation within n8n. The input is expected to be a JSON object with a 'people' array.

```javascript
let newList = $jmespath($json.body.people, "[].[first, last]");
return {newList};
/* Returns:
[
	{
		"newList": [
			[
				"James",
				"Green"
			],
			[
				"Jacob",
				"Jones"
			],
			[
				"Jayden",
				"Smith"
			]
		]
	}
]
*/
```

--------------------------------

### Edit Fields Node Configuration in n8n

Source: https://docs.n8n.io/courses/level-two/chapter-2

Configures an 'Edit Fields' node to set or update a field named 'outputValue' with the value of 'new-date' from the JSON input. It also includes an option to include other fields from the input.

```json
{
	"parameters": {
		"assignments": {
		"assignments": [
			{
			"id": "e058832a-2461-4c6d-b584-043ecc036427",
			"name": "outputValue",
			"value": "={{ $json['new-date'] }}",
			"type": "string"
			}
		]
		},
		"includeOtherFields": true,
		"options": {}
	},
	"id": "be034e9e-3cf1-4264-9d15-b6760ce28f91",
	"name": "Edit Fields",
	"type": "n8n-nodes-base.set",
	"typeVersion": 3.3,
	"position": [
		1700,
		260
	]
}
```

--------------------------------

### Send Location

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/message-operations

Sends a geolocation to a chat using the Bot API's sendLocation method. Requires a Telegram credential and specifies the chat ID, latitude, and longitude.

```APIDOC
## POST /sendLocation

### Description
Use this operation to send a geolocation to the chat using the Bot API sendLocation method.

### Method
POST

### Endpoint
/sendLocation

### Parameters
#### Request Body
- **credential** (object) - Required - Credential to connect with Telegram.
- **chatId** (string) - Required - The Chat ID or username of the channel you wish to send the location to in the format `@channelusername`.
- **latitude** (number) - Required - The latitude of the location.
- **longitude** (number) - Required - The longitude of the location.
- **replyMarkup** (object) - Optional - Use this parameter to set more interface options.

### Request Example
```json
{
  "credential": "<your_credential_id>",
  "chatId": "@channelusername",
  "latitude": 40.7128,
  "longitude": -74.0060,
  "replyMarkup": {}
}
```

### Response
#### Success Response (200)
- **result** (object) - The sent message object.

#### Response Example
```json
{
  "result": {
    "message_id": 12345,
    "chat": {
      "id": 123456789,
      "type": "private"
    },
    "location": {
      "latitude": 40.7128,
      "longitude": -74.0060
    },
    "date": 1678886400
  }
}
```

### Additional Fields
- **disableNotification** (boolean) - Optional - Choose whether to send the notification silently (turned on) or with a standard notification (turned off).
- **replyToMessageId** (integer) - Optional - If the message is a reply, enter the ID of the message it's replying to.
- **messageThreadId** (integer) - Optional - Enter a unique identifier for the target message thread (topic) of the forum; for forum supergroups only.
```

--------------------------------

### Rebrand n8n Window Title

Source: https://docs.n8n.io/embed/white-labelling

Updates the application's HTML title tag and the TypeScript constants used by the document title composable to reflect custom branding.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<!-- Replace html title attribute -->
	<title>My Brand - Workflow Automation</title>
</head>
```

```typescript
import { useSettingsStore } from '@/stores/settings.store';

// replace n8n
const DEFAULT_TITLE = 'My Brand';
const DEFAULT_TAGLINE = 'Workflow Automation';
```

--------------------------------

### Fix Call to /executions-current with Unsaved Workflow

Source: https://docs.n8n.io/release-notes/0-x

This bug fix addresses an issue where calls to the '/executions-current' endpoint failed when a workflow was unsaved. The fix ensures that the endpoint functions correctly even in scenarios with unsaved workflow states.

```javascript
**core:** Fix call to `/executions-current` with unsaved workflow.
```

--------------------------------

### Add Support for Querying Chat Administrators in Telegram Node

Source: https://docs.n8n.io/release-notes/0-x

The Telegram node now includes functionality to query chat administrators. This enhancement allows users to retrieve information about administrators within a Telegram chat, which can be useful for various automation and management tasks.

```javascript
Telegram node: add support for querying chat administrators.
```

--------------------------------

### Reduce Array to Single Value with JavaScript

Source: https://docs.n8n.io/data/expression-reference/array

Reduces an array to a single value by applying a callback function to each element. It supports both arrow function and traditional function notation for accumulating results.

```JavaScript
// Sum numbers (using arrow function notation):
// nums = [12, 33, 16]
nums.reduce((result, num) => (result+num), 0) //=> 61

// Join letters and uppercase (using arrow function notation):
// chars = ['a', 'b', 'c']
chars.reduce((result, char) => (result+char.toUpperCase()), '') //=> 'ABC'

// Or using traditional function notation:
chars.reduce(function(result, char){return result+char.toUpperCase()}, '') //=> 'ABC'
```

--------------------------------

### Extract URL Path from String - JavaScript

Source: https://docs.n8n.io/data/expression-reference/string

Returns the path component of a URL string. Returns undefined if no URL is found. This is a custom n8n function for URL parsing.

```javascript
"http://n8n.io/workflows".extractUrlPath() //=> '/workflows'
```

```javascript
"Check out http://n8n.io/workflows".extractUrl().extractUrlPath() //=> '/workflows'
```

--------------------------------

### Extract object values using Object.values() in n8n

Source: https://docs.n8n.io/data/expression-reference/object

This method returns an array containing all the values of the fields present in an object. It is a custom implementation within n8n that mirrors the behavior of the standard JavaScript Object.values() function.

```JavaScript
// obj = {'name': 'Mr Nathan', age: 42 }
obj.values() //=> ['Mr Nathan', 42]
```

--------------------------------

### Set DateTime values

Source: https://docs.n8n.io/data/expression-reference/datetime

Assigns new values to specific units of a DateTime object using an object map of units to values.

```javascript
// dt = "2024-03-30T18:49".toDateTime()
dt.set({year:1982, month:10}) // => 1982-10-20T18:49
```

--------------------------------

### Fix Edit Image Node Binary Data Mode

Source: https://docs.n8n.io/release-notes/0-x

The Edit Image node now works correctly with the binary-data-mode 'filesystem'. This fix ensures proper handling of binary data when using the filesystem mode for image editing operations.

```javascript
Edit Image node: node now works correctly with the binary-data-mode 'filesystem'.
```

--------------------------------

### Format strings for JSON with toJsonString()

Source: https://docs.n8n.io/data/expression-reference/string

A custom n8n method that escapes quotes and special characters within a string to prepare it for insertion into a JSON object.

```javascript
let str = 'The "best" colours: red\nbrown';
str.toJsonString();
```

--------------------------------

### Define JSON Data Structure in n8n Code Node

Source: https://docs.n8n.io/data/specific-data-types/jmespath

This snippet shows the standard format for returning data from an n8n Code node. It returns an array of objects, where each object contains a 'json' property holding the actual data fields.

```javascript
return[
  {
    "json": {      
      "num_categories": "0",
      "num_products": "45",
      "category_id": 5529735,
      "parent_id": 1407340,
      "pos_enabled": 1,
      "pos_favorite": 0,
      "name": "HP",
      "description": "",
      "image": ""
    }
  },
  {
    "json": {
      "num_categories": "0",
      "num_products": "86",
      "category_id": 5529740,
      "parent_id": 1407340,
      "pos_enabled": 1,
      "pos_favorite": 0,
      "name": "Lenovo",
      "description": "",
      "image": ""
    }
  }  
];
```

--------------------------------

### Compare Two DateTimes for Equality

Source: https://docs.n8n.io/data/expression-reference/datetime

Checks if two DateTime objects represent the exact same moment in time and are in the same time zone. For a less strict comparison, the `hasSame()` method should be used.

```javascript
// dt1 = "2024-03-20T18:49+01:00".toDateTime()
// dt2 = "2024-03-20T19:49+02:00".toDateTime()
dt1.equals(dt2) //=> false
```

--------------------------------

### String isUrl() - Check if string is a valid URL

Source: https://docs.n8n.io/data/expression-reference/string

Verifies if a string represents a valid URL, typically requiring a protocol like 'http' or 'https'. It returns true for valid URLs and false for strings that are not properly formatted URLs.

```javascript
"https://n8n.io".isUrl() //=> true
"n8n.io".isUrl() //=> false
"hello".isUrl() //=> false
```

--------------------------------

### Configure n8n to Save Only Error Executions (npm)

Source: https://docs.n8n.io/hosting/scaling/execution-data

This configuration reduces saved data by only storing n8n executions that result in an error. It also disables saving successful executions, node progress, and manually launched executions.

```bash
# Save executions ending in errors
export EXECUTIONS_DATA_SAVE_ON_ERROR=all

# Don't save successful executions
export EXECUTIONS_DATA_SAVE_ON_SUCCESS=none

# Don't save node progress for each execution
export EXECUTIONS_DATA_SAVE_ON_PROGRESS=false

# Don't save manually launched executions
export EXECUTIONS_DATA_SAVE_MANUAL_EXECUTIONS=false
```

--------------------------------

### Convert Number to String (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/number

Converts a number to its default string representation. This is useful for displaying numbers as text. The default radix is 10.

```javascript
let num = 500000.125;
console.log(num.toString()); // Output: '500000.125'
```

--------------------------------

### Set Variable with n8n Set Node

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/let_your_ai_call_an_api.json

Assigns values to variables within an n8n workflow. This node allows for setting specific fields, such as a 'response' field, from other node outputs or expressions.

```json
{
  "assignments": {
    "assignments": [
      {
        "id": "e37e64f6-64e7-4fbd-9ea1-e9d3ef99b39c",
        "name": "response",
        "value": "={{ $json.activity }}",
        "type": "string"
      }
    ]
  },
  "options": {}
}
```

--------------------------------

### Array.sort()

Source: https://docs.n8n.io/data/expression-reference/array

Reorders the elements of an array based on a comparison function or default string conversion.

```APIDOC
## Array.sort()

### Description
Reorders the elements of the array. For sorting strings alphabetically, no parameter is required. For sorting numbers or Objects, a compare function is required.

### Method
N/A (JavaScript Method)

### Parameters
- **compareFunction** (function) - Optional - A function to compare two array elements (a, b).

### Request Example
```javascript
// Sort numbers
[4, 2, 1, 3].sort((a, b) => (a - b)) // [1, 2, 3, 4]
```

### Response
- **Returns** (Array) - The sorted array.
```

--------------------------------

### Array.append()

Source: https://docs.n8n.io/data/expression-reference/array

Adds new elements to the end of the array. Similar to `push()`, but returns the modified array. Consider using spread syntax instead.

```APIDOC
## Array.append()

### Description
Adds new elements to the end of the array. Similar to `push()`, but returns the modified array. Consider using spread syntax instead.

### Method
Array.append(elem1, elem2?, ..., elemN?)

### Parameters
#### Path Parameters
- **elem1** (any) - Required - The first element to append
- **elem2** (any) - Optional - The second element to append
- **elemN** (any) - Optional - The Nth element to append

### Request Example
```json
{
  "example": "// arr = ['forget', 'me']\narr.append('not') //=> arr = ['forget', 'me', 'not']"
}
```

### Response
#### Success Response (200)
- **Array** (Array) - The modified array

#### Response Example
```json
{
  "example": "['forget', 'me', 'not']"
}
```
```

--------------------------------

### Workflow Item Data Schema

Source: https://docs.n8n.io/workflows/templates

Detailed schema for the workflow item data, used by the `/templates/workflows/{id}` endpoint.

```APIDOC
## Workflow Item Data Schema

### Description
This schema describes the metadata and definition of a workflow template. It is used by the `/templates/workflows/{id}` endpoint and is nested within the `workflow` key of the response. It includes information for displaying templates in search or browse interfaces, along with the nested `workflow` property containing the actual importable workflow definition.

### Schema
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Generated schema for Root",
  "type": "object",
  "properties": {
    "id": {
      "type": "number"
    },
    "name": {
      "type": "string"
    },
    "totalViews": {
      "type": "number"
    },
    "price": {},
    "purchaseUrl": {},
    "recentViews": {
      "type": "number"
    },
    "createdAt": {
      "type": "string"
    },
    "user": {
      "type": "object",
      "properties": {
        "username": {
          "type": "string"
        },
        "verified": {
          "type": "boolean"
        }
      },
      "required": [
        "username",
        "verified"
      ]
    },
    "nodes": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {
            "type": "number"
          },
          "icon": {
            "type": "string"
          },
          "name": {
            "type": "string"
          },
          "codex": {
            "type": "object",
            "properties": {
              "data": {
                "type": "object",
                "properties": {
                  "details": {
                    "type": "string"
                  },
                  "resources": {
                    "type": "object",
                    "properties": {
                      "generic": {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "url": {
                              "type": "string"
                            },
                            "icon": {
                              "type": "string"
                            },
                            "label": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "url",
                            "label"
                          ]
                        }
                      },
                      "primaryDocumentation": {
                        "type": "array",
                        "items": {
                          "type": "object",
                          "properties": {
                            "url": {
                              "type": "string"
                            }
                          },
                          "required": [
                            "url"
                          ]
                        }
                      }
                    },
                    "required": [
                      "primaryDocumentation"
                    ]
                  },
                  "categories": {
                    "type": "array",
                    "items": {
                      "type": "string"
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
}
```
```

--------------------------------

### Filter Supabase Metadata using Postgres Operators

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.supabase/common-issues

Use the Postgres ->> operator to query JSON metadata fields in Supabase. The syntax follows the format metadata->>{property}={operator}.{value}.

```Postgres
metadata->>{your-property}={comparison-operator}.{comparison-value}
```

```Postgres
metadata->>age=gte.21
```

--------------------------------

### Collection Item Data Schema

Source: https://docs.n8n.io/workflows/templates

Schema definition for a collection item within the n8n API.

```APIDOC
## Collection Item Data Schema

### Description
This schema defines the structure of a collection item, which groups related workflows.

### Method
GET

### Endpoint
/templates/collections

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **id** (number) - The unique identifier for the collection.
- **rank** (number) - The ranking of the collection.
- **name** (string) - The name of the collection.
- **totalViews** (object) - Information about the total views for the collection.
- **createdAt** (string) - The timestamp when the collection was created.
- **workflows** (array) - A list of workflows within the collection.
  - **id** (number) - The ID of a workflow.
- **nodes** (array) - Information about nodes associated with the collection.

### Response Example
```json
{
  "id": 1,
  "rank": 1,
  "name": "Popular Templates",
  "totalViews": {},
  "createdAt": "2023-01-01T10:00:00Z",
  "workflows": [
    { "id": 101 },
    { "id": 102 }
  ],
  "nodes": []
}
```
```

--------------------------------

### Fix Issue with FixedCollection Default Values

Source: https://docs.n8n.io/release-notes/0-x

A bug related to 'fixedCollection' having all default values has been resolved. This ensures that 'fixedCollection' behaves as expected and does not erroneously apply default values when not intended.

```javascript
**core:** Fix issue with fixedCollection having all default values.
```

--------------------------------

### If Node for Conditional Logic

Source: https://docs.n8n.io/_workflows//courses/level-one/finished.json

Implements conditional logic based on the 'orderStatus' field. It checks if the order status is 'processing' using a strict string comparison. This node routes the workflow based on the condition's outcome.

```json
{
  "parameters": {
    "conditions": {
      "options": {
        "caseSensitive": true,
        "leftValue": "",
        "typeValidation": "strict",
        "version": 2
      },
      "conditions": [
        {
          "id": "526cb30c-0f90-4f66-8f98-b64ceb2e52f2",
          "leftValue": "={{ $json.orderStatus }}",
          "rightValue": "processing",
          "operator": {
            "type": "string",
            "operation": "equals"
          }
        }
      ],
      "combinator": "and"
    },
    "options": {}
  },
  "type": "n8n-nodes-base.if",
  "typeVersion": 2.2,
  "position": [
    440,
    -40
  ],
  "id": "448b2e3c-569d-42e6-a4b9-57c08b2cac1a",
  "name": "If"
}
```

--------------------------------

### Array Compact Functionality (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/array

Removes all 'empty' values from an array, including `null`, empty strings (`""`), and `undefined`. Returns a new array with only the defined and non-empty values.

```javascript
// arr = [2, null, 1, ""]
arr.compact() //=> [2, 1]
```

--------------------------------

### Retrieve list of elements using JMESPath

Source: https://docs.n8n.io/data/specific-data-types/jmespath

Extracts a specific field from a list of objects using the list projection operator. This works across JavaScript expressions, Code nodes, and Python nodes.

```javascript
{{$jmespath($json.body.people, "[*].first" )}}
```

```javascript
let firstNames = $jmespath($json.body.people, "[*].first" );
return {firstNames};
```

```python
firstNames = _jmespath(_json.body.people, "[*].first" )
return {"firstNames":firstNames}
```

--------------------------------

### Rename Object Keys in Array

Source: https://docs.n8n.io/data/expression-reference/array

Changes matching keys (field names) for all objects within an array. Supports renaming multiple keys by providing pairs of arguments.

```n8n
// arr = [{'name':'bob'},{'name':'meg'}]
arr.renameKeys('name', 'x') //=> [{"x": "bob"},{"x": "meg"}]]
```

--------------------------------

### Calculate Array Sum

Source: https://docs.n8n.io/data/expression-reference/array

Returns the total of all numbers in an array. Throws an error if non-numeric values are present.

```JavaScript
const total = [12, 1, 5].sum();
```

--------------------------------

### Array.union()

Source: https://docs.n8n.io/data/expression-reference/array

Concatenates two arrays and removes duplicates.

```APIDOC
## Array.union()

### Description
Concatenates two arrays and then removes any duplicates.

### Parameters
- **otherArray** (Array) - Required - The array to union with the base array.

### Response
- **Returns** (Array) - The combined array without duplicates.

### Response Example
```javascript
[1, 2].union([2, 3]) // [1, 2, 3]
```
```

--------------------------------

### Define n8n Form Node Configuration

Source: https://docs.n8n.io/_workflows/integrations/builtin/core-nodes/n8n-nodes-base.form/multiple-branch-execution.json

This JSON structure defines an n8n form node, including parameters for form fields, completion messages, and node metadata like position and unique identifiers. These nodes are used to collect user input and display final completion screens in a workflow.

```json
{
  "parameters": {
    "operation": "completion",
    "completionTitle": "Thank you for answering our romance film questions!",
    "options": {}
  },
  "type": "n8n-nodes-base.form",
  "typeVersion": 1,
  "position": [700, -20],
  "id": "cd7bc8d0-a143-4733-be84-320c88ef241b",
  "name": "Romance questions"
}
```

--------------------------------

### JavaScript Code for Data Aggregation

Source: https://docs.n8n.io/_workflows//courses/level-one/finished.json

A JavaScript code snippet that calculates the total number of booked orders and the sum of their prices. It iterates through the input items, accessing the 'orderPrice' from each item's JSON. The output is an object containing 'totalBooked' and 'bookedSum'.

```javascript
let items = $input.all();
let totalBooked = items.length;
let bookedSum = 0;

for (let i=0; i < items.length; i++) {
  bookedSum = bookedSum + items[i].json.orderPrice;
}

return [{ json: {totalBooked, bookedSum} }];
```

--------------------------------

### Define Category Item Schema

Source: https://docs.n8n.io/embed/workflow-templates

Defines the structure for a category object, requiring an integer ID and a string name. This schema is used to validate category data returned by the n8n API.

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "id": {
      "type": "number"
    },
    "name": {
      "type": "string"
    }
  },
  "required": [
    "id",
    "name"
  ]
}
```

--------------------------------

### Configure HTTP Request Node

Source: https://docs.n8n.io/_workflows//courses/level-one/chapter-5/chapter-5.5.json

This configuration defines an HTTP Request node in n8n, set up to perform a request to a custom ERP webhook. It includes authentication via HTTP headers and a unique identifier parameter.

```json
{
  "url": "https://internal.users.n8n.cloud/webhook/custom-erp",
  "authentication": "genericCredentialType",
  "genericAuthType": "httpHeaderAuth",
  "sendHeaders": true,
  "headerParameters": {
    "parameters": [
      {
        "name": "unique_id",
        "value": "<YOUR_UNIQUE_ID_HERE>"
      }
    ]
  }
}
```

--------------------------------

### Configure n8n Form Trigger and Conditional Routing

Source: https://docs.n8n.io/_workflows/integrations/builtin/core-nodes/n8n-nodes-base.form/multiple-branch-execution.json

This JSON configuration defines a form trigger node with a multi-select dropdown field and a subsequent routing logic structure. It uses n8n expression syntax to evaluate array contents against specific genre strings to determine branch execution.

```json
{
  "type": "n8n-nodes-base.formTrigger",
  "parameters": {
    "formTitle": "Form that may execute multiple branches",
    "formFields": {
      "values": [{
        "fieldLabel": "What are your favorite film genres",
        "fieldType": "dropdown",
        "multiselect": true
      }]
    }
  }
},
{
  "type": "n8n-nodes-base.if",
  "parameters": {
    "conditions": {
      "conditions": [{
        "leftValue": "={{ $json['What are your favorite film genres'] }}",
        "rightValue": "Documentary",
        "operator": {
          "type": "array",
          "operation": "contains"
        }
      }]
    }
  }
}
```

--------------------------------

### Check String Inclusion - JavaScript

Source: https://docs.n8n.io/data/expression-reference/string

Determines if a string contains a specified substring. The search is case-sensitive. This is a standard JavaScript String method.

```javascript
'team'.includes('tea') //=> true
'team'.includes('i') //=> false
```

```javascript
// Returns false if the case doesn't match, so consider using .toLowerCase() first
'team'.includes('Tea') //=> false
'Team'.toLowerCase().includes('tea') //=> true
```

--------------------------------

### Send Message

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/message-operations

Sends a text message to a chat using the Bot API's sendMessage method. Requires a Telegram credential and specifies the chat ID and the text content.

```APIDOC
## POST /sendMessage

### Description
Use this operation to send a message to the chat using the Bot API sendMessage method.

### Method
POST

### Endpoint
/sendMessage

### Parameters
#### Request Body
- **credential** (object) - Required - Credential to connect with Telegram.
- **chatId** (string) - Required - The Chat ID or username of the channel you wish to send the message to in the format `@channelusername`.
- **text** (string) - Required - Enter the text to send, max 4096 characters after entities parsing.

### Request Example
```json
{
  "credential": "<your_credential_id>",
  "chatId": "@channelusername",
  "text": "Hello, this is a test message!"
}
```

### Response
#### Success Response (200)
- **result** (object) - The sent message object.

#### Response Example
```json
{
  "result": {
    "message_id": 12348,
    "chat": {
      "id": 123456789,
      "type": "private"
    },
    "text": "Hello, this is a test message!",
    "date": 1678886403
  }
}
```

### Limits
Telegram limits the number of messages you can send to 30 per second. If you expect to hit this limit, refer to Send more than 30 messages per second for a suggested workaround.
```

--------------------------------

### Search String with Regex in n8n

Source: https://docs.n8n.io/data/expression-reference/string

Finds the index of the first occurrence of a regular expression pattern within a string. Returns -1 if no match is found.

```JavaScript
"Neat n8n node".search(/n[^ ]*/); // => 5
"Neat n8n node".search(/n[^ ]*/i); // => 0
```

--------------------------------

### Convert Array to String

Source: https://docs.n8n.io/data/expression-reference/array

Converts an array to a comma-separated string representation.

```JavaScript
const str = ['make', 'my', 'day'].toString();
```

--------------------------------

### Configure n8n to Save Only Error Executions (Docker)

Source: https://docs.n8n.io/hosting/scaling/execution-data

This Docker command configures n8n to save only error executions and disable saving of successful executions, node progress, and manually launched executions. It maps the n8n port and sets the relevant environment variables.

```bash
docker run -it --rm \
 --name n8n \
 -p 5678:5678 \
 -e EXECUTIONS_DATA_SAVE_ON_ERROR=all \
 -e EXECUTIONS_DATA_SAVE_ON_SUCCESS=none \
 -e EXECUTIONS_DATA_SAVE_ON_PROGRESS=true \
 -e EXECUTIONS_DATA_SAVE_MANUAL_EXECUTIONS=false \
 docker.n8n.io/n8nio/n8n
```

--------------------------------

### Disable n8n Telemetry Events

Source: https://docs.n8n.io/hosting/securing/telemetry-opt-out

Configures the environment variable to stop n8n from sending anonymous diagnostic telemetry data. Set this variable to false to opt out of event collection.

```bash
export N8N_DIAGNOSTICS_ENABLED=false
```

--------------------------------

### Convert Array to JSON String

Source: https://docs.n8n.io/data/expression-reference/array

Serializes an array into a JSON-formatted string, equivalent to JSON.stringify().

```JavaScript
const jsonString = ['quick', 'brown', 'fox'].toJsonString();
```

--------------------------------

### Array Difference Calculation (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/array

Compares the base array with another array and returns a new array containing elements present in the base array but not in the `otherArray`.

```javascript
// arr = [1, 2, 3]
arr.difference([2, 3]) //=> [1]
```

--------------------------------

### Calculate intersection of two Arrays

Source: https://docs.n8n.io/data/expression-reference/array

A custom n8n utility that returns an array containing elements present in both the base array and the provided comparison array.

```JavaScript
const arr = [1, 2];
arr.intersection([2, 3]); // => [2]
```

--------------------------------

### Access Specific Custom Data Value (JavaScript)

Source: https://docs.n8n.io/workflows/executions/custom-executions-data

Retrieves a specific value from the custom data object during the workflow execution using its key. This allows targeted access to individual pieces of custom data that were previously set.

```javascript
// Access a specific value set during this execution
const customData = $execution.customData.get("key");
```

--------------------------------

### n8n Workflow Node Configuration

Source: https://docs.n8n.io/_workflows/advanced-ai/examples/chat_with_google_sheets_docs_version.json

A collection of JSON-based node definitions for an n8n workflow. These snippets define the parameters for AI agents, memory management, and tool-based sub-workflow execution.

```json
{
  "id": "8f2a4854-2177-4ac8-9501-fa36cf2a3d73",
  "name": "AI Agent",
  "type": "@n8n/n8n-nodes-langchain.agent",
  "parameters": {
    "text": "={{ $json.chatInput }}",
    "options": {
      "maxIterations": 10
    }
  }
},
{
  "id": "c3d20569-1374-4f8d-8779-23b98952d124",
  "name": "Simple Memory",
  "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
  "parameters": {}
},
{
  "id": "2b8c8a67-a4df-4f5c-8c13-3cb2d25d2c5f",
  "name": "GPT4 Model",
  "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
  "parameters": {
    "model": "gpt-4",
    "options": {
      "temperature": 0
    }
  }
}
```

--------------------------------

### Convert String to Snake Case

Source: https://docs.n8n.io/data/expression-reference/string

Converts a string to snake case by replacing spaces and dashes with underscores, removing symbols, and lowercasing all letters. This is a custom n8n functionality.

```javascript
"quick brown $FOX".toSnakeCase() //=> "quick_brown_fox"
```

--------------------------------

### Format DateTime to String

Source: https://docs.n8n.io/data/expression-reference/datetime

Converts a DateTime object into a string representation based on a specified format. It supports various formatting tokens and locale settings for internationalization. Common formats can also be achieved using `toLocaleString()`.

```javascript
// dt = "2024-04-30T18:49".toDateTime()
dt.format('dd/LL/yyyy') //=> '30/04/2024'
```

```javascript
// dt = "2024-04-30T18:49".toDateTime()
dt.format('dd LLL yy') //=> '30 Apr 24'
dt.setLocale('fr').format('dd LLL yyyy') //=> '30 avr. 2024'
dt.format("HH 'hours and' mm 'minutes'") //=> '18 hours and 49 minutes'
```

--------------------------------

### Delete a Data Table

Source: https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.datatable/tables

Permanently deletes an existing data table.

```APIDOC
## DELETE /api/tables/{tableId}

### Description
Permanently deletes an existing data table. This action can't be undone.

### Method
DELETE

### Endpoint
/api/tables/{tableId}

### Parameters
#### Path Parameters
- **tableId** (string) - Required - The ID or name of the data table to delete.

### Request Example
(No request body needed for deletion by ID)

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating the table was deleted.

#### Response Example
```json
{
  "message": "Data table 'MyDataTable' deleted successfully."
}
```
```

--------------------------------

### Number.abs()

Source: https://docs.n8n.io/data/expression-reference/number

Returns the absolute value of a number, effectively removing any negative sign.

```APIDOC
## Number.abs()

### Description
Returns the number’s absolute value, i.e. removes any minus sign.

### Syntax
Number.abs()

### Returns
Number

### Response Example
// x = -1.7
x.abs() //=> 1.7
```

--------------------------------

### Add Additional Fields to Discord Node Message Sending

Source: https://docs.n8n.io/release-notes/0-x

The Discord node now provides additional fields when sending a message. This allows for more customization and control over the content and appearance of messages sent to Discord.

```javascript
Discord node: additional fields now available when sending a message to Discord.
```

--------------------------------

### Convert String to Lower Case

Source: https://docs.n8n.io/data/expression-reference/string

Converts all letters in a given string to lower case. This is a standard JavaScript string method.

```javascript
"I'm SHOUTing".toLowerCase() //=> "i'm shouting"
```

--------------------------------

### Array Chunking Functionality (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/array

Splits an array into multiple sub-arrays, each containing a specified number of elements. The last sub-array may contain fewer elements if the total count is not evenly divisible by the chunk length.

```javascript
// arr = [1, 2, 3, 4, 5, 6]
arr.chunk(2) //=> [ [1,2], [3,4], [5,6] ]
```

--------------------------------

### Select Names using JMESPath Expression

Source: https://docs.n8n.io/data/specific-data-types/jmespath

This snippet demonstrates how to use a JMESPath expression to select the 'first' and 'last' names from a 'people' array within a JSON body. It's a concise way to transform JSON data directly in n8n expressions. No external dependencies are required beyond the n8n environment.

```jmespath
{{$jmespath($json.body.people, "[].[first, last]"}} // Returns [["James","Green"],["Jacob","Jones"],["Jayden","Smith"]]
```

--------------------------------

### Add New Property from Existing Data in Code Node (JavaScript)

Source: https://docs.n8n.io/courses/level-two/chapter-1

This snippet illustrates how to reference and manipulate data from a previous node within the n8n Code node. It accesses the input data, adds a new 'workEmail' property by extracting it from the nested 'email.work' structure, and returns the modified data.

```javascript
let items = $input.all();
items[0].json.workEmail = items[0].json.email['work'];
return items;
```

--------------------------------

### Number.round()

Source: https://docs.n8n.io/data/expression-reference/number

Rounds the number to the nearest whole number or specified decimal places.

```APIDOC
## Number.round()

### Description
Returns the number rounded to the nearest whole number (or specified number of decimal places).

### Syntax
Number.round(decimalPlaces?)

### Parameters
- **decimalPlaces** (Number) - Optional - The number of decimal places to round to.

### Response Example
// number = 1.256
number.round(1) //=> 1.3
```

--------------------------------

### POST /channels/{channel_id}/messages

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.discord/common-issues

Sends a message with optional rich embeds to a specific Discord channel using the Discord REST API.

```APIDOC
## POST /channels/<CHANNEL_ID>/messages

### Description
Sends a message to a Discord channel. This endpoint supports rich embeds for advanced formatting, including authors, footers, and custom fields.

### Method
POST

### Endpoint
https://discord.com/api/v10/channels/<CHANNEL_ID>/messages

### Parameters
#### Path Parameters
- **CHANNEL_ID** (string) - Required - The unique identifier of the Discord channel.

#### Request Body
- **content** (string) - Optional - The text content of the message.
- **embeds** (array) - Optional - An array of embed objects containing rich content.

### Request Example
{
	"content": "Test",
	"embeds": [
		{
			"author": "My Name",
			"url": "https://discord.js.org",
			"fields": [
				{
					"name": "Regular field title",
					"value": "Some value here"
				}
			],
			"footer": {
				"text": "Some footer text here",
				"icon_url": "https://i.imgur.com/AfFp7pu.png"
			}
		}
	]
}

### Response
#### Success Response (200)
- **id** (string) - The ID of the created message.
- **channel_id** (string) - The ID of the channel the message was sent to.

#### Response Example
{
	"id": "123456789012345678",
	"channel_id": "876543210987654321",
	"content": "Test"
}
```

--------------------------------

### Skip Credentials Checks for Disabled Nodes

Source: https://docs.n8n.io/release-notes/0-x

n8n now skips credentials checks for disabled nodes. This optimization prevents unnecessary credential validation for nodes that are not actively being used in a workflow.

```javascript
**core** : n8n now skips credentials checks for disabled nodes.
```

--------------------------------

### Checking Feature Status in n8n Node Code

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/node-versioning

Checks if a specific feature is enabled within the execution context of an n8n node using the 'this.isNodeFeatureEnabled()' method. This allows for conditional logic based on feature flags.

```typescript
if (this.isNodeFeatureEnabled('useNewApi')) {
    // Process with new API
} else {
    // Process with legacy API
}
```

--------------------------------

### Convert DateTime to UTC

Source: https://docs.n8n.io/data/expression-reference/datetime

Converts a DateTime object to the Coordinated Universal Time (UTC) timezone. The moment in time remains the same unless specific options are used. This method is part of the Luxon library.

```javascript
// dt = "2024-01-01T00:00:00.000+02:00".toDateTime()
dt.toUTC() //=> 2023-12-31T22:00:00.000Z
```

--------------------------------

### Convert String to Upper Case

Source: https://docs.n8n.io/data/expression-reference/string

Converts all letters in a given string to upper case. This is a standard JavaScript string method.

```javascript
"I'm not angry".toUpperCase() //=> "I'M NOT ANGRY"
```

--------------------------------

### Extract Domain from String - JavaScript

Source: https://docs.n8n.io/data/expression-reference/string

Extracts the domain name from an email address or URL string. Returns undefined if no domain is found. This is a custom n8n function.

```javascript
"me@example.com".extractDomain() //=> 'example.com'
```

```javascript
"http://n8n.io/workflows".extractDomain() //=> 'n8n.io'
```

```javascript
"It's me@example.com".extractEmail().extractDomain() //=> 'example.com'
```

--------------------------------

### Access Execution ID

Source: https://docs.n8n.io/code/cookbook/builtin/execution

Retrieves the unique identifier for the current workflow execution. This property is used to track or log specific workflow instances.

```JavaScript
let executionId = $execution.id;
```

```Python
executionId = _execution.id
```

--------------------------------

### Subscribe to Page Updates using Graph API

Source: https://docs.n8n.io/integrations/builtin/trigger-nodes/n8n-nodes-base.facebooktrigger/page

This code snippet demonstrates how to subscribe to updates for a Facebook page using the Graph API. It requires the page ID and is used to configure the trigger to receive specific events.

```bash
1
{
page-id
}/subscribed_apps?subscribed_fields=feed
```

--------------------------------

### Array Append Functionality (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/array

Adds new elements to the end of an array, returning the modified array. Similar to `push()`, but returns the array. Consider using spread syntax for a more modern approach.

```javascript
// arr = ['forget', 'me']
arr.append('not') //=> arr = ['forget', 'me', 'not']
```

```javascript
// arr = [9, 0, 2]
arr.append(1, 0) //=> [9, 0, 2, 1, 0]

// Consider using spread syntax instead
[...arr, 1, 0]  //=> [9, 0, 2, 1, 0]
```

--------------------------------

### Find index of element in Array

Source: https://docs.n8n.io/data/expression-reference/array

Returns the first index at which a given element can be found in the array, or -1 if it is not present.

```JavaScript
const names = ["Bob", "Bill", "Nat"];
names.indexOf("Nat"); // => 2
names.indexOf("Nathan"); // => -1
```

--------------------------------

### Configure n8n to Save Only Error Executions (Docker Compose)

Source: https://docs.n8n.io/hosting/scaling/execution-data

This Docker Compose configuration sets environment variables for n8n to save only error executions and disable saving of successful executions, node progress, and manually launched executions.

```yaml
n8n:
    environment:
      - EXECUTIONS_DATA_SAVE_ON_ERROR=all
      - EXECUTIONS_DATA_SAVE_ON_SUCCESS=none
      - EXECUTIONS_DATA_SAVE_ON_PROGRESS=true
      - EXECUTIONS_DATA_SAVE_MANUAL_EXECUTIONS=false
```

--------------------------------

### Trim Whitespace from String

Source: https://docs.n8n.io/data/expression-reference/string

Removes leading and trailing whitespace, including new lines and tabs, from a string. This is a standard JavaScript string method.

```javascript
'   lonely   '.trim() //=> 'lonely'
```

--------------------------------

### Check if Object Has a Specific Field (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/object

The `hasField(name)` method checks if an object contains a top-level key with the specified name. The comparison is case-sensitive. It returns a boolean value. This is a custom n8n functionality.

```javascript
// obj = {'name':'Nathan', 'age':42}
obj.hasField('name') //=> true

// obj = {'name':'Nathan', 'age':42}
obj.hasField('Name') //=> false
obj.hasField('inventedField') //=> false
```

--------------------------------

### Base64 Encode String - JavaScript

Source: https://docs.n8n.io/data/expression-reference/string

Converts a plain text string to its base64-encoded representation. This is a custom n8n functionality for string encoding.

```javascript
"hello".base64Encode() //=> "aGVsbG8="
```

--------------------------------

### Check Node Execution Status in JavaScript (n8n)

Source: https://docs.n8n.io/data/expressions-for-transformation

This JavaScript snippet demonstrates how to check if a specific node has been executed within an n8n workflow. It's useful for preventing errors when an expression relies on data from a preceding node that might not have run.

```javascript
1
$('<node-name>').isExecuted
```

--------------------------------

### Define RSS Feed URLs in n8n Code Node

Source: https://docs.n8n.io/_workflows/integrations/builtin/core-nodes/n8n-nodes-base.splitinbatches/rss-feed-example.json

This JavaScript snippet is used within an n8n Code node to output an array of objects, each containing a URL. These URLs are subsequently used by downstream nodes to fetch RSS feed data.

```javascript
return [
	{
		json: {
			url: 'https://medium.com/feed/n8n-io',
		}
	},
	{
		json: {
			url: 'https://dev.to/feed/n8n',
		}
	}
];
```

--------------------------------

### Quote String in n8n

Source: https://docs.n8n.io/data/expression-reference/string

Wraps a string in quotation marks and escapes existing quotes. This is useful for formatting data for JSON or SQL injection.

```JavaScript
'Nathan says "hi"'.quote() // => '"Nathan says \"hi\""'
```

--------------------------------

### Decode URL-Encoded String

Source: https://docs.n8n.io/data/expression-reference/string

Decodes a URL-encoded string, replacing %XX character codes with their corresponding characters. An optional parameter `allChars` can be set to true to decode URI syntax characters. This is a custom n8n functionality.

```javascript
"name%3DNathan%20Automat".urlDecode() //=> "name=Nathan Automat"
"name%3DNathan%20Automat".urlDecode(true) //=> "name%3DNathan Automat"
```

--------------------------------

### Generate New Items without PairedItem in JavaScript

Source: https://docs.n8n.io/data/data-mapping/data-item-linking/item-linking-code-node

This JavaScript code snippet illustrates the process of generating new items from an input array. It iterates through the input 'items', extracts the 'name' property, and adds a new field 'aBrandNewField' with associated data. However, it does not include the 'pairedItem' property, meaning the generated items will not have a direct link back to their original source.

```javascript
newItems = [];
for(let i=0; i<items.length; i++){
  newItems.push(
    {
    "json":
      {
        "name": items[i].json.name,
				"aBrandNewField": "New data for item " + i
      }
    }
  )
}

return newItems;
```

--------------------------------

### Edit Fields with Set Node (n8n)

Source: https://docs.n8n.io/_workflows//courses/level-one/chapter-5/chapter-5.6.json

Utilizes the 'Set' node to modify or add fields to the workflow data. It allows for dynamic assignment of values to fields based on expressions or static data. This node is commonly used for data transformation and preparation.

```json
{
  "parameters": {
    "assignments": {
      "assignments": [
        {
          "id": "20d37948-763a-4d7b-b725-e65f3802af03",
          "name": "orderID",
          "value": "={{ $json.orderID }}",
          "type": "number"
        },
        {
          "id": "9df108a7-6b13-42ab-a6dd-9ca582ba8b49",
          "name": "employeeName",
          "value": "={{ $json.employeeName }}",
          "type": "string"
        }
      ]
    },
    "options": {}
  },
  "type": "n8n-nodes-base.set",
  "typeVersion": 3.4,
  "position": [
    800,
    -600
  ],
  "id": "a3d3dc53-32f1-4f44-bf95-50bc5450d601",
  "name": "Edit Fields1"
}
```

--------------------------------

### Add Support for Regions in Microsoft Dynamics CRM Node

Source: https://docs.n8n.io/release-notes/0-x

This update extends the Microsoft Dynamics CRM node to support regions other than North America. This broadens the applicability of the node for users operating in different geographical locations, ensuring better integration with their Dynamics CRM instances.

```javascript
Microsoft Dynamics CRM node: add support for regions other than North America.
```

--------------------------------

### Set Node for Field Editing

Source: https://docs.n8n.io/_workflows//courses/level-one/finished.json

Configures a 'Set' node to assign values to specific fields, 'orderID' and 'employeeName'. It uses expressions to map data from the input JSON. This node is used for data transformation and preparation.

```json
{
  "parameters": {
    "assignments": {
      "assignments": [
        {
          "id": "20d37948-763a-4d7b-b725-e65f3802af03",
          "name": "orderID",
          "value": "={{ $json.orderID }}",
          "type": "number"
        },
        {
          "id": "9df108a7-6b13-42ab-a6dd-9ca582ba8b49",
          "name": "employeeName",
          "value": "={{ $json.employeeName }}",
          "type": "string"
        }
      ]
    },
    "options": {}
  },
  "type": "n8n-nodes-base.set",
  "typeVersion": 3.4,
  "position": [
    660,
    -140
  ],
  "id": "7e2a8092-fb0f-4260-84e8-d796cf14d309",
  "name": "Edit Fields"
}
```

--------------------------------

### Handle Basic API Request Failures with NodeApiError

Source: https://docs.n8n.io/integrations/creating-nodes/build/reference/error-handling

Wrap potential API request errors in NodeApiError to provide structured feedback. This pattern is useful for general HTTP request failures.

```typescript
try {
	const response = await this.helpers.httpRequestWithAuthentication.call(
		this,
		credentialType,
		options
	);
	return response;
} catch (error) {
	throw new NodeApiError(this.getNode(), error as JsonObject);
}
```

--------------------------------

### Concatenate Strings - JavaScript

Source: https://docs.n8n.io/data/expression-reference/string

Joins one or more strings to the end of a base string. This functionality is available as a JavaScript method or can be achieved using the '+' operator.

```javascript
'sea'.concat('food') //=> 'seafood'
'sea' + 'food' //=> 'seafood'
```

```javascript
'work'.concat('a', 'holic') //=> 'workaholic'
```

--------------------------------

### Extract JSON field value in n8n

Source: https://docs.n8n.io/data/expressions-for-transformation

Demonstrates how to access nested JSON data from a previous node's output using n8n's expression syntax. It shows both dot notation and bracket notation for accessing the 'city' field from a webhook body.

```n8n-expression
{{$json.body.city}}
```

```n8n-expression
{{$json['body']['city']}}
```

--------------------------------

### PATCH /v1/pages/{page_id}

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.notion/common-issues

Updates a page's properties, specifically useful for modifying one-way relationship properties that are not supported by the standard Notion node.

```APIDOC
## PATCH /v1/pages/<page_id>

### Description
Updates the properties of a specific Notion page. This is primarily used to update one-way relationship properties.

### Method
PATCH

### Endpoint
https://api.notion.com/v1/pages/<page_id>

### Parameters
#### Path Parameters
- **page_id** (string) - Required - The unique identifier of the Notion page.

#### Request Body
- **properties** (object) - Required - The properties to update on the page.

### Request Example
{
	"properties": {
		"Account": {
			"relation": [
				{
					"id": "<your_relation_ID>"
				}
			]
		}
	}
}
```

--------------------------------

### Extract data with $jmespath

Source: https://docs.n8n.io/data/expression-reference/root

The $jmespath function allows for querying and transforming complex, nested JSON objects using JMESPath expressions. It takes an object or array as input and returns the filtered result, or undefined if the expression is invalid.

```javascript
data = {
  "people": [
    { "age": 20, "other": "foo", "name": "Bob" },
    { "age": 25, "other": "bar", "name": "Fred" },
    { "age": 30, "other": "baz", "name": "George" }
  ]
};

// Get all names in an array
$jmespath(data, '[*].name');

// Get names and ages of everyone over 20
$jmespath(data, '[?age > `20`].[name, age]');

// Complex nested query
$jmespath(data, 'reservations[].guests[?requirements.room==`double`].name');
```

--------------------------------

### Enable SSRF Protection in n8n

Source: https://docs.n8n.io/hosting/securing/ssrf-protection

This configuration enables Server-Side Request Forgery (SSRF) protection in n8n. When enabled, n8n validates all outbound HTTP requests from user-controllable nodes against configured blocked and allowed ranges.

```environment
N8N_SSRF_PROTECTION_ENABLED=true
```

--------------------------------

### Set DateTime locale

Source: https://docs.n8n.io/data/expression-reference/datetime

Configures the locale for the DateTime object, affecting how it is formatted into strings.

```javascript
$now.setLocale('de-DE').toLocaleString({'dateStyle':'long'}) // => 5. Oktober 2024
$now.setLocale('fr-FR').toLocaleString({'dateStyle':'long'}) // => 5 octobre 2024
```

--------------------------------

### Add Upsert Support to Google Sheets Node

Source: https://docs.n8n.io/release-notes/0-x

The Google Sheets node has been updated to include 'upsert' support. This functionality allows for both inserting new rows and updating existing ones in a Google Sheet based on specified criteria, streamlining data management operations.

```javascript
Google Sheets node: Added upsert support.
```

--------------------------------

### IAM Role Trust Policy for STS AssumeRole

Source: https://docs.n8n.io/integrations/builtin/credentials/aws

This JSON policy defines the trust relationship for an IAM role, allowing a specific AWS account root to assume the role with a condition based on an external ID. This is crucial for secure role assumption in n8n.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::SOURCE-ACCOUNT:root"
      },
      "Action": "sts:AssumeRole",
      "Condition": {
        "StringEquals": {
          "sts:ExternalId": "your-unique-external-id"
        }
      }
    }
  ]
}
```

--------------------------------

### Fix Editor UI Bug with Node Versioning

Source: https://docs.n8n.io/release-notes/0-x

A bug in the editor UI related to node versioning has been fixed. This ensures a smoother user experience when working with different versions of nodes within the n8n editor.

```javascript
Fixes a bug in the editor UI related to node versioning.
```

--------------------------------

### Parse Dates Using Dot Notation in MongoDB Node

Source: https://docs.n8n.io/release-notes/0-x

The MongoDB node now supports parsing dates using dot notation. This feature simplifies the process of accessing and manipulating date fields within MongoDB documents, especially when dealing with nested structures.

```javascript
MongoDB node: you can now parse dates using dot notation.
```

--------------------------------

### Format Postgres DATE as string using TO_CHAR

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.postgres/common-issues

Uses the Postgres TO_CHAR function to cast a date column into a specific string format. This ensures the output is a simple date string (YYYY-MM-DD) instead of an ISO 8601 datetime object.

```sql
SELECT TO_CHAR(date_col, 'YYYY-MM-DD') AS date_col_as_date FROM table_with_date_col
```

--------------------------------

### Remove Markdown and HTML Tags in n8n

Source: https://docs.n8n.io/data/expression-reference/string

Cleans strings by stripping away Markdown syntax or HTML/XML tags. These methods return a plain text representation of the input string.

```JavaScript
"*bold*, [link]()".removeMarkdown(); // => "bold, link"
"<b>bold</b>, <a>link</a>".removeTags(); // => "bold, link"
```

--------------------------------

### Array.filter()

Source: https://docs.n8n.io/data/expression-reference/array

Returns an array with only the elements satisfying a condition. The condition is a function that returns `true` or `false`.

```APIDOC
## Array.filter()

### Description
Returns an array with only the elements satisfying a condition. The condition is a function that returns `true` or `false`.

### Method
Array.filter(function(element, index?, array?), thisValue?)

### Parameters
#### Path Parameters
- **function()** (function) - Required - A function to run for each array element. If it returns `true`, the element will be kept. Consider using arrow function notation to save space.
  - **element** (any) - The value of the current element
  - **index** (Number) - Optional - The position of the current element in the array (starting at 0)
  - **array** (Array) - Optional - The array being processed. Rarely needed.
- **thisValue** (any) - Optional - A value passed to the function as its `this` value. Rarely needed.

### Request Example
```json
{
  "example": "// Keep ages over 18 (using arrow function notation):\n// ages = [12, 33, 16, 40]\nages.filter(age => (age > 18)) //=> [33, 40]"
}
```

### Response
#### Success Response (200)
- **Array** (Array) - An array containing only the elements that satisfy the condition.

#### Response Example
```json
{
  "example": "[33, 40]"
}
```
```

--------------------------------

### Number.ceil()

Source: https://docs.n8n.io/data/expression-reference/number

Rounds a number up to the next whole number.

```APIDOC
## Number.ceil()

### Description
Rounds the number up to the next whole number.

### Syntax
Number.ceil()

### Returns
Number

### Response Example
// x = 1.234
x.ceil() //=> 2
```

--------------------------------

### Array Concatenation (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/array

Joins one or more arrays to the end of the base array, creating a new, combined array. This function does not modify the original arrays.

```javascript
// arr1 = ['Nathan', 'Jan']
arr1.concat(['Steve', 'Bill']) // ['Nathan', 'Jan', 'Steve', 'Bill']
```

```javascript
// arr1 = [5, 4]
// arr2 = [100, 101]
// arr3 = ['a', 'b']
arr1.concat(arr2, arr3) // [5, 4, 100, 101, 'a', 'b']
```

--------------------------------

### Error Trigger Data Structure (Trigger Node Error) (n8n)

Source: https://docs.n8n.io/flow-logic/error-handling

This JSON structure represents the error data received by the Error Trigger when the failure originates from the main workflow's trigger node. It contains less information in the 'execution' object and more detailed error information within the 'trigger' object, including context, error name, cause, timestamp, and the node configuration.

```json
{
  "trigger": {
    "error": {
      "context": {},
      "name": "WorkflowActivationError",
      "cause": {
        "message": "",
        "stack": ""
      },
      "timestamp": 1654609328787,
      "message": "",
      "node": {
        . . .
      }
    },
    "mode": "trigger"
  },
  "workflow": {
    "id": "",
    "name": ""
  }
}
```

--------------------------------

### Fix Discord Node Icon Name

Source: https://docs.n8n.io/release-notes/0-x

A bug related to the Discord node's icon name has been fixed. This ensures the correct icon is displayed for the Discord node in the n8n interface.

```javascript
Fixes a bug with the Discord node icon name.
```

--------------------------------

### Calculate Difference to Now from DateTime

Source: https://docs.n8n.io/data/expression-reference/datetime

Calculates the difference between a DateTime object and the current moment in specified units. This is useful for determining how long ago or in the future a specific date is. It supports returning the difference in multiple units.

```javascript
// dt = "2023-03-30T18:49:07.234".toDateTime()
dt.diffToNow('days') //=> 371.9
```

```javascript
// dt = "2023-03-30T18:49:07.234".toDateTime()
dt.diffToNow(['months', 'days']) //=> {"months":12, "days":5.9}
```

--------------------------------

### Accessing Node Data

Source: https://docs.n8n.io/data/expression-reference

Methods to retrieve data from the current item or reference specific items from previous nodes in the workflow. These expressions are fundamental for passing data between nodes.

```n8n-expression
$json
$json.fieldName
$binary
$("NodeName").first()
$("NodeName").item
$("NodeName").all()
$("NodeName").last()
```

--------------------------------

### Improve Google Calendar Node with Public Calendars

Source: https://docs.n8n.io/release-notes/0-x

The Google Calendar node has been improved to work with public calendars and has undergone code cleanup. This enhancement broadens its usability for accessing and managing public calendar data.

```javascript
Google Calendar Node: Make it work with public calendars and clean up.
```

--------------------------------

### Fix Pipedrive Node Multi Option Field Resolution

Source: https://docs.n8n.io/release-notes/0-x

The Pipedrive Node has been fixed to correctly resolve properties when using a multi-option field. This ensures accurate data handling for fields that allow multiple selections in Pipedrive.

```javascript
Pipedrive Node: Fix resolve properties when using multi option field.
```

--------------------------------

### Representing Nested JSON Data

Source: https://docs.n8n.io/data/data-structure

A JSON array containing objects with nested properties. This structure is used to demonstrate how n8n maps hierarchical data fields into its user interface.

```json
[
  {
    "name": "First item",
    "nested": {
      "example-number-field": 1,
      "example-string-field": "apples"
    }
  },
  {
    "name": "Second item",
    "nested": {
      "example-number-field": 2,
      "example-string-field": "oranges"
    }
  }
]
```

--------------------------------

### Pluck Field Values from Array Objects (n8n)

Source: https://docs.n8n.io/data/expression-reference/array

The `pluck()` method returns an array containing the values of specified fields from each object within an array. It ignores elements that are not objects or lack the specified keys. Multiple field names can be provided.

```javascript
// arr = [{'name':'Nathan','age':42},{'name':'Jan','city':'Berlin'}]
arr.pluck('name') //=> ["Nathan", "Jan"]
```

```javascript
// arr = [{'name':'Nathan','age':42},{'name':'Jan','city':'Berlin'}]
arr.pluck('age') //=> [42]
```

--------------------------------

### Update Google Calendar Event

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.googlecalendar/event-operations

Updates an existing event in a specified Google Calendar. This operation supports modifying various event attributes, including recurrence, reminders, attendees, and visibility.

```APIDOC
## POST /google-calendar/events/update

### Description
Updates an existing event in a Google Calendar. You can modify various aspects of the event, such as its summary, description, start/end times, attendees, recurrence rules, and more.

### Method
POST

### Endpoint
/google-calendar/events/update

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **credential** (object) - Required - Google Calendar credentials.
- **resource** (string) - Required - Must be 'Event'.
- **operation** (string) - Required - Must be 'Update'.
- **calendar** (string) - Required - The ID or title of the calendar to update the event in.
- **eventId** (string) - Required - The ID of the event to update.
- **modify** (string) - Optional - For recurring events, specifies whether to update the 'recurring event' or a 'single instance'.
- **useDefaultReminders** (boolean) - Optional - Whether to use the calendar's default reminders.
- **updateFields** (object) - Optional - An object containing the fields to update.
  - **allDay** (boolean) - Optional - Whether the event is an all-day event.
  - **attendees** (array) - Optional - List of attendees to invite or replace.
  - **colorNameOrId** (string) - Optional - The color of the event.
  - **description** (string) - Optional - A description for the event.
  - **end** (object) - Optional - The end time of the event. Example: `{"dateTime": "2024-12-31T23:59:59-07:00", "timeZone": "America/Los_Angeles"}`
  - **guestsCanInviteOthers** (boolean) - Optional - Whether guests can invite others.
  - **guestsCanModify** (boolean) - Optional - Whether guests can modify the event.
  - **guestsCanSeeOtherGuests** (boolean) - Optional - Whether guests can see other attendees.
  - **id** (string) - Optional - The opaque identifier of the event.
  - **location** (string) - Optional - The geographic location of the event.
  - **repeatFrequency** (string) - Optional - The repetition interval for recurring events (e.g., 'DAILY', 'WEEKLY').
  - **repeatHowManyTimes** (integer) - Optional - The number of instances to create for recurring events.
  - **repeatUntil** (string) - Optional - The date until which recurring events should stop (ISO 8601 format).
  - **rrule** (string) - Optional - Recurrence rule (RFC 5545 format). Overrides repeatFrequency, repeatHowManyTimes, and repeatUntil.
  - **sendUpdates** (string) - Optional - Whether to send notifications about the event update ('all', 'externalOnly', 'none').
  - **showMeAs** (string) - Optional - Whether the event blocks time on the calendar ('free', 'busy', 'tentative').
  - **start** (object) - Optional - The start time of the event. Example: `{"dateTime": "2024-12-31T09:00:00-07:00", "timeZone": "America/Los_Angeles"}`
  - **summary** (string) - Optional - The title of the event.
  - **visibility** (string) - Optional - The visibility of the event ('public', 'private', 'confidential', 'default').

### Request Example
```json
{
  "credential": {
    "id": "your_credential_id"
  },
  "resource": "Event",
  "operation": "Update",
  "calendar": "primary",
  "eventId": "your_event_id",
  "updateFields": {
    "summary": "Updated Event Title",
    "description": "This is an updated description.",
    "start": {
      "dateTime": "2024-12-31T10:00:00-07:00",
      "timeZone": "America/Los_Angeles"
    },
    "end": {
      "dateTime": "2024-12-31T11:00:00-07:00",
      "timeZone": "America/Los_Angeles"
    }
  }
}
```

### Response
#### Success Response (200)
- **id** (string) - The ID of the updated event.
- **status** (string) - The status of the update operation.

#### Response Example
```json
{
  "id": "your_event_id",
  "status": "success"
}
```
```

--------------------------------

### Union Two Arrays

Source: https://docs.n8n.io/data/expression-reference/array

Concatenates two arrays while removing duplicate entries.

```JavaScript
const result = [1, 2].union([2, 3]);
```

--------------------------------

### Round Number to Decimal Places (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/number

Rounds a number to the nearest whole number or to a specified number of decimal places. This is a custom n8n functionality.

```javascript
// number = 1.256
number.round() //=> 1
```

```javascript
// number = 1.256
number.round(1) //=> 1.3
number.round(2) //=> 1.26
```

--------------------------------

### Convert Number to Boolean (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/number

Converts a number to a boolean value. `0` is converted to `false`, and any other number (including negative numbers) is converted to `true`. This is a custom n8n functionality.

```javascript
// number = 12
number.toBoolean() //=> true
```

```javascript
// number = 0
number.toBoolean() //=> false
```

--------------------------------

### String isEmail() - Check if string is an email address

Source: https://docs.n8n.io/data/expression-reference/string

Validates if a string conforms to the typical structure of an email address. It returns true for valid email formats and false for strings that do not match the pattern, including those with leading text.

```javascript
"me@example.com".isEmail() //=> true
"It's me@example.com".isEmail() //=> false
"hello".isEmail() //=> false
```

--------------------------------

### Convert Number Timestamp to DateTime (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/number

Converts a numerical timestamp into a DateTime object. The format of the timestamp (milliseconds, seconds, or Excel date) must be specified if it's not in milliseconds. Uses the timezone configured in n8n or workflow settings. This is a custom n8n functionality.

```javascript
// ts = 1708695471
ts.toDateTime('s') //=> 2024-02-23T14:37:51+01:00
```

```javascript
// ts = 1708695471000
ts.toDateTime('ms') //=> 2024-02-23T14:37:51+01:00
```

```javascript
// ts = 45345
ts.toDateTime('excel') //=> 2024-02-23T01:00:00+01:00
```

--------------------------------

### Extract Email from String - JavaScript

Source: https://docs.n8n.io/data/expression-reference/string

Extracts the first email address found within a string. Returns undefined if no email address is detected. This is a custom n8n functionality.

```javascript
"My email is me@example.com".extractEmail() //=> 'me@example.com'
```

--------------------------------

### Check if DateTime is in Daylight Saving Time - Luxon

Source: https://docs.n8n.io/data/expression-reference/datetime

A boolean property that indicates whether the DateTime object falls within a Daylight Saving Time period.

```javascript
// Example usage would involve checking the boolean value returned by the property.
```

--------------------------------

### Fix HubSpot Node Search Operators

Source: https://docs.n8n.io/release-notes/0-x

A fix has been implemented for the HubSpot node's search operators. This ensures that search queries using operators in HubSpot are executed correctly, providing accurate results.

```javascript
HubSpot node: fix for search operators.
```

--------------------------------

### Improve Webhook Error Messages

Source: https://docs.n8n.io/release-notes/0-x

Webhook error messages in n8n have been improved for clarity and helpfulness. This enhancement aids users in diagnosing and resolving issues related to webhook configurations and data reception.

```javascript
**core** : improved webhook error messages.
```

--------------------------------

### Sort Array Elements

Source: https://docs.n8n.io/data/expression-reference/array

Reorders array elements. Uses default string comparison or a custom compare function for numbers and objects.

```JavaScript
arr.sort();
arr.sort((a, b) => (a - b));
arr.sort((a, b) => b.localeCompare(a));
arr.sort((a, b) => a.name.localeCompare(b.name));
```

--------------------------------

### Reverse Array Elements

Source: https://docs.n8n.io/data/expression-reference/array

Reverses the order of elements in an array using the standard JavaScript reverse method.

```JavaScript
// arr = ['dog', 'bites', 'man']
arr.reverse() //=> ['man', 'bites', 'dog']
```

--------------------------------

### Delete a message

Source: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.gmail/message-operations

Immediately and permanently deletes a specified Gmail message.

```APIDOC
## Delete a message

### Description
Use this operation to immediately and permanently delete a message. This operation can't be undone.

### Method
DELETE

### Endpoint
/users.messages/{id}

### Parameters
#### Path Parameters
- **userId** (string) - Required - The ID of the user's mailbox. Use 'me' to refer to the authenticated user.
- **id** (string) - Required - The ID of the message to delete.

#### Query Parameters
- **format** (string) - Optional - The format to return the message in.
- **metadataHeaders** (string) - Optional - When specified, the value of this field is used as a prefix to the labels that are returned in the metadata. 

### Response
#### Success Response (204)
No content is returned upon successful deletion.

#### Response Example
(No content)
```

--------------------------------

### Array Average Calculation (JavaScript)

Source: https://docs.n8n.io/data/expression-reference/array

Calculates and returns the average of numbers within an array. Throws an error if the array contains any non-numeric values.

```javascript
// arr = [12, 1, 5]
arr.average() //=> 6
```

--------------------------------

### Filter Data with JMESPath Expression

Source: https://docs.n8n.io/data/specific-data-types/jmespath

This snippet demonstrates how to use the $jmespath expression in n8n to query data from a previous node. It filters the items to find those where the name is 'Lenovo' and returns the corresponding category ID.

```jmespath
{{ $jmespath($("Code").all(), "[?json.name=='Lenovo'].json.category_id") }}
```