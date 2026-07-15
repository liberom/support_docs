### Install AgentMail SDK and dotenv

Source: https://docs.agentmail.to/get-started/quickstart

Installs the AgentMail SDK and the python-dotenv library for managing environment variables. This is a prerequisite for authenticating with the AgentMail API.

```bash
pip install agentmail python-dotenv
```

--------------------------------

### AgentMail Setup and Flask Server (`main.py`)

Source: https://docs.agentmail.to/webhook-agent

This Python script initializes the AgentMail client, sets up an inbox and webhook idempotently, starts an ngrok tunnel for public access, and configures a Flask web server. It includes environment variable loading and basic error handling for critical setup steps. The agent's instructions are defined within this script, specifying its role and interaction scenarios.

```python
# main.py
from dotenv import load_dotenv
load_dotenv()

import os
import asyncio
from threading import Thread
import time

import ngrok
from flask import Flask, request, Response

from agentmail import AgentMail
from agentmail_toolkit.openai import AgentMailToolkit
from agents import WebSearchTool, Agent, Runner

port = 8080
domain = os.getenv("WEBHOOK_DOMAIN")
inbox_username = os.getenv("INBOX_USERNAME")
inbox = f"{inbox_username}@agentmail.to"

target_github_repo = os.getenv("TARGET_GITHUB_REPO")
if not target_github_repo:
  print("\nWARNING: The TARGET_GITHUB_REPO environment variable is not set.")
  print("The agent will not have a specific GitHub repository to focus on.")
  print("Please set it in your .env file (e.g., TARGET_GITHUB_REPO='owner/repository_name')\n")

demo_target_email = os.getenv("DEMO_TARGET_EMAIL")
if not demo_target_email:
  print("\nWARNING: The DEMO_TARGET_EMAIL environment variable is not set.")
  print("The agent will not have a specific email to send the 'top starrer' outreach to.")
  print("Please set it in your .env file (e.g., DEMO_TARGET_EMAIL='your.email@example.com')\n")

# Determine the target email, with a fallback if the environment variable is not set.

# The fallback is less ideal for a real demo but prevents the agent from having no target.

actual_demo_target_email = demo_target_email if demo_target_email else "fallback.email@example.com"

# Use a fallback for target_github_repo as well for the instructions string construction

actual_target_github_repo = target_github_repo if target_github_repo else "example/repo"

# --- AgentMail and Web Server Setup ---

# 1. Initialize the AgentMail client

client = AgentMail()

# 2. Idempotently create the inbox for the agent

# Using a deterministic client_id ensures we don't create duplicate inboxes

# if the script is run multiple times.

inbox_client_id = f"inbox-for-{inbox_username}"
print(f"Attempting to create or retrieve inbox '{inbox}' with client_id: {inbox_client_id}")
try:
  client.inboxes.create(
  username=inbox_username,
  client_id=inbox_client_id
  )
  print("Inbox creation/retrieval successful.")
except Exception as e:
  print(f"Error creating/retrieving inbox: {e}") # Depending on the desired behavior, you might want to exit here # if the inbox is critical for the agent's function.

# 3. Start the ngrok tunnel to get a public URL

print("Starting ngrok tunnel...")
listener = ngrok.forward(port, domain=domain, authtoken_from_env=True)
print(f"ngrok tunnel started: {listener.url()}")

# 4. Idempotently create the webhook pointing to our new public URL

webhook_url = f"{listener.url()}/webhooks"
webhook_client_id = f"webhook-for-{inbox_username}"
print(f"Attempting to create or retrieve webhook for URL: {webhook_url}")
try:
  client.webhooks.create(
  url=webhook_url,
  client_id=webhook_client_id,
  )
  print("Webhook creation/retrieval successful.")
except Exception as e:
  print(f"Error creating/retrieving webhook: {e}")

# 5. Initialize the Flask App

app = Flask(__name__)

instructions = f"""
You are a GitHub Repository Evangelist Agent. Your name is AgentMail. Your email address is {inbox}.
Your primary focus is the GitHub repository: '{actual_target_github_repo}'.
Your goal is to engage the user at {actual_demo_target_email} about the potential of '{actual_target_github_repo}' for building AI agents, using rich HTML emails.

**You operate in two main scenarios:**

**Scenario 1: Proactive Outreach (Triggered by internal monitor for '{actual_target_github_repo}')**

- You will receive a direct instruction when a new (simulated) star is detected for '{actual_target_github_repo}'.
- This instruction will explicitly ask you to:
    1.  Use the WebSearchTool to find fresh, compelling information or talking points about '{actual_target_github_repo}' (e.g., new features, use cases for agent development, benefits). You should synthesize this information, not just copy it.
    2.  Use the 'send_message' tool to send a NEW email to {actual_demo_target_email}.
        - The email should start by mentioning something like: "Hello! We noticed you recently showed interest in (or starred) our repository, '{actual_target_github_repo}'! We're excited to share some insights..."
        - You must craft an engaging 'subject' for this email.
        - You must craft an informative 'html' (body) for this email in HTML format, based on your synthesized web search findings. **Do NOT include raw URLs or direct links from your web search in the email body.** Instead, discuss the concepts or information you found.
"""
```

--------------------------------

### Run Quickstart Script

Source: https://docs.agentmail.to/get-started/quickstart

Executes the Python quickstart script from the terminal to create an inbox and send an email using the AgentMail API.

```bash
python quickstart.py
```

--------------------------------

### List Drafts via HTTP GET Request (Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/drafts/list

Provides examples of how to list drafts by making a direct HTTP GET request to the AgentMail API. These examples cover Go, Ruby, Java, PHP, C#, and Swift, requiring an API key for authorization.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/drafts"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/drafts")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/drafts")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/drafts', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/drafts");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/drafts")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Agent Running Output Example

Source: https://docs.agentmail.to/documentation/examples/smart-labeling-agent

This is an example of the expected output when the AgentMail agent starts successfully. It shows the agent's readiness and the local URL it's running on.

```text
SMART EMAIL LABELING AGENT

Ready: smart-labels@agentmail.to

Waiting for emails...

 * Running on http://127.0.0.1:8080
```

--------------------------------

### Install Ngrok on macOS

Source: https://docs.agentmail.to/webhook-setup

Provides instructions for installing the ngrok tool on macOS using Homebrew. Ngrok is used to create secure public URLs for local development servers.

```bash
brew install ngrok
```

--------------------------------

### List Threads via HTTP GET Request (Go)

Source: https://docs.agentmail.to/api-reference/threads/list

Provides a Go example for fetching threads by making a direct HTTP GET request to the AgentMail API. Includes setting the Authorization header.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/threads"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Install AgentMail and Flask Packages

Source: https://docs.agentmail.to/webhook-setup

Installs the necessary Python packages for AgentMail integration and creating a web server. Ensure Python 3.8+ and pip are installed.

```bash
pip install agentmail flask ngrok
```

--------------------------------

### Install Dependencies with requirements.txt

Source: https://docs.agentmail.to/webhook-agent

This snippet shows the content of a requirements.txt file, listing Python packages necessary for the project. These include agentmail, agentmail-toolkit, openai, openai-agents, python-dotenv, flask, and ngrok.

```txt
agentmail
agentmail-toolkit
openai
openai-agents
python-dotenv
flask
ngrok
```

--------------------------------

### List Threads via HTTP GET Request (Java)

Source: https://docs.agentmail.to/api-reference/threads/list

A Java example using the Unirest library to make an HTTP GET request to fetch threads. It demonstrates setting the Authorization header.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/threads")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Fetch Draft via HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/drafts/get

Illustrates making a direct HTTP GET request to the AgentMail API to fetch a draft. This example uses Go's standard `net/http` package and does not rely on a specific SDK.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/drafts/draft_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Install Dependencies - Pip Command (Bash)

Source: https://docs.agentmail.to/sales-agent-websocket

Demonstrates how to install the required Python packages for the project using pip. It shows two common methods: installing from a `requirements.txt` file or installing directly from a `pyproject.toml` file.

```bash
pip install -r requirements.txt
# or with pyproject.toml
pip install .
```

--------------------------------

### List Threads via HTTP GET Request (Ruby)

Source: https://docs.agentmail.to/api-reference/threads/list

Illustrates how to retrieve threads using Ruby's Net::HTTP library. This example sends a GET request with the necessary Authorization header.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/threads")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Main Execution Block and Initialization (Python)

Source: https://docs.agentmail.to/webhook-agent

This block defines the main entry point for the application. It prints the inbox ID, checks for necessary configuration variables (TARGET_GITHUB_REPO, DEMO_TARGET_EMAIL), starts a background thread for polling GitHub stargazers, and then launches the Flask web server.

```python
if __name__ == "__main__":
  print(f"Inbox: {inbox}\n")
  if not target_github_repo or target_github_repo == "example/repo":
  print("WARNING: TARGET_GITHUB_REPO not set or is default. Poller will not be effective.")
  if not demo_target_email:
  print("WARNING: DEMO_TARGET_EMAIL not set or is default. Poller will not be effective.")

  polling_thread = Thread(target=poll_github_stargazers)
  polling_thread.daemon = True # So it exits when the main thread exits
  polling_thread.start()

  print(f"ngrok tunnel started: {listener.url()}")

  app.run(port=port)
```

--------------------------------

### Fetch Pod Information using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/pods/get

Demonstrates how to fetch pod information using the AgentMail SDK. This involves initializing the client with an API key and calling the get method for a specific pod. Ensure you have the agentmail library installed.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.get("pod_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.get(
    pod_id="pod_id"
)
```

--------------------------------

### Fetch Threads using HTTP Request (Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/pods/threads/get

Examples of fetching threads from a specific pod using direct HTTP GET requests. These snippets cover various languages and demonstrate how to set the 'Authorization' header with an API key and process the response.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/threads/thread_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/threads/thread_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id/threads/thread_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/pods/pod_id/threads/thread_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id/threads/thread_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id/threads/thread_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Fetch Inbox Data with AgentMail SDK

Source: https://docs.agentmail.to/api-reference/pods/inboxes/get

Examples show how to initialize the AgentMail client and retrieve inbox data using the SDK. This typically involves providing an API key and specifying pod and inbox IDs. Ensure the AgentMail SDK is installed for your respective language.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.inboxes.get("pod_id", "inbox_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.inboxes.get(
    pod_id="pod_id",
    inbox_id="inbox_id"
)
```

--------------------------------

### Webhook Server Setup with Flask and ngrok

Source: https://docs.agentmail.to/webhook-agent

Sets up a local web server using Flask to receive incoming webhooks from AgentMail. It also configures ngrok to create a public URL that forwards traffic to the local server. The webhook endpoint listens for POST requests.

```python
from flask import Flask
import ngrok

app = Flask(__name__)

@app.route("/webhooks", methods=["POST"])
def listener():
    # ... (webhook processing logic)
    return "", 200

# Forward traffic to the local Flask server
public_url = ngrok.forward(8080, "your_webhook_domain")
print(f"Ngrok tunnel established at: {public_url}")

if __name__ == "__main__":
    app.run(port=8080)
```

--------------------------------

### List API Keys via HTTP Request (PHP)

Source: https://docs.agentmail.to/api-reference/api-keys/list

A PHP example using the Guzzle HTTP client to make a GET request to the AgentMail API for listing API keys. Ensure the GuzzleHttp client is installed via Composer.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/api-keys', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### Create an inbox and send an email with AgentMail API

Source: https://docs.agentmail.to/quickstart

Initializes the AgentMail client using an API key from environment variables, creates a new email inbox, and sends a test email. Requires the AGENTMAIL_API_KEY to be set in a .env file.

```python
import os
from dotenv import load_dotenv
from agentmail import AgentMail

# Load the API key from the .env file
load_dotenv()
api_key = os.getenv("AGENTMAIL_API_KEY")

# Initialize the client
client = AgentMail(api_key=api_key)

# Create an inbox
print("Creating inbox...")
inbox = client.inboxes.create() # domain is optional
print("Inbox created successfully!")
print(inbox)

# Send Email

client.inboxes.messages.send(
inbox_id="your-email@example.com",
to="contact@agentmail.to",
subject="Hello from AgentMail!",
text="This is my first email sent with the AgentMail API."

)
```

```typescript
import { AgentMailClient } from "agentmail";
import "dotenv/config"; // loads .env file

async function main() {
  // Initialize the client
  const client = new AgentMailClient({
    apiKey: process.env.AGENTMAIL_API_KEY,
  });

  // Create an inbox
  console.log("Creating inbox...");
  const inbox = await client.inboxes.create(); // domain is optional
  console.log("Inbox created successfully!");
  console.log(inbox);

  // Send an email from the new inbox
  console.log("Sending email...");
  await client.inboxes.messages.send(inbox.inboxId, {
    to: "your-email@example.com",
    subject: "Hello from AgentMail!",
    text: "This is my first email sent with the AgentMail API.",
  });
  console.log("Email sent successfully!");
}

main();
```

--------------------------------

### Fetch Inbox Metrics via HTTP GET Request (Go)

Source: https://docs.agentmail.to/api-reference/inboxes/metrics/get

Provides a Go example for fetching inbox metrics using a direct HTTP GET request. It constructs the URL with parameters and includes the 'Authorization' header with a Bearer token. This method does not require an SDK but involves manual HTTP handling.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Custom AgentMail Skill Setup

Source: https://docs.agentmail.to/integrations/openclaw

Guide to setting up a custom AgentMail skill for Openclaw, including API endpoints and usage examples.

```APIDOC
## Custom AgentMail Skill Setup

### Description
Create and configure a custom AgentMail skill for Openclaw to gain more control over the email integration. This involves creating a skill directory and a `SKILL.md` file with API interaction instructions.

### Skill Directory Creation

Create a new skill directory in your Openclaw workspace:

```bash
mkdir -p ~/.openclaw/skills/agentmail
```

### Skill File (`SKILL.md`)

Create `~/.openclaw/skills/agentmail/SKILL.md` with the following content:

```markdown
---
name: agentmail
description: Send and receive emails using AgentMail
requires:
  env:
    - AGENTMAIL_API_KEY
---

# AgentMail Skill

You can send and receive emails using the AgentMail API. Use the `exec` tool to run curl commands against the AgentMail API.

## API Base URL

```
https://api.agentmail.to/v0
```

## Authentication

Include your API key in the Authorization header:

```
Authorization: Bearer $AGENTMAIL_API_KEY
```

## Common Operations

### List inboxes

```bash
curl -s -H "Authorization: Bearer $AGENTMAIL_API_KEY" \
  https://api.agentmail.to/v0/inboxes
```

### Create an inbox

```bash
curl -s -X POST -H "Authorization: Bearer $AGENTMAIL_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"display_name": "My Agent"}' \
  https://api.agentmail.to/v0/inboxes
```

### Send an email

```bash
curl -s -X POST -H "Authorization: Bearer $AGENTMAIL_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "to": ["recipient@example.com"],
    "subject": "Hello from Openclaw",
    "text": "This email was sent by my AI assistant."
  }' \
  https://api.agentmail.to/v0/inboxes/{inbox_id}/messages
```

### List messages in an inbox

```bash
curl -s -H "Authorization: Bearer $AGENTMAIL_API_KEY" \
  https://api.agentmail.to/v0/inboxes/{inbox_id}/messages
```

### Reply to a message

```bash
curl -s -X POST -H "Authorization: Bearer $AGENTMAIL_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"text": "Thanks for your email!"}' \
  https://api.agentmail.to/v0/inboxes/{inbox_id}/messages/{message_id}/reply
```
```

### Configuration

Add your AgentMail API key to the skill configuration in `~/.openclaw/openclaw.json`:

```json
{
  "skills": {
    "entries": {
      "agentmail": {
        "enabled": true,
        "env": {
          "AGENTMAIL_API_KEY": "your-api-key-here"
        }
      }
    }
  }
}
```

### Verification

Check that the skill is loaded:

```bash
openclaw skills list --eligible
```

You should see `agentmail` in the list of available skills.

```
--------------------------------

### Start Ngrok Tunnel

Source: https://docs.agentmail.to/webhook-setup

Starts an ngrok tunnel to expose a local development server running on port 3000 to the internet. This allows external services like AgentMail to send webhooks to your local machine.

```bash
ngrok http 3000
```

--------------------------------

### Illustrative Pod Structures for SaaS, Agencies, and AI Agents (TypeScript)

Source: https://docs.agentmail.to/documentation/core-concepts/pods

Provides conceptual examples of how pods can be structured in a multi-tenant SaaS application, for agency client management, and for an AI agent platform. These examples illustrate the organizational isolation provided by pods.

```typescript
// Customer A's workspace
Pod: "Acme Corp"
├── Inbox: support@acme.com
├── Inbox: sales@acme.com
└── Domain: acme.com

// Customer B's workspace
Pod: "TechStart Inc"
├── Inbox: hello@techstart.io
├── Inbox: team@techstart.io
└── Domain: techstart.io
```

```typescript
// Client 1
Pod: "Client - Retail Co"
├── Inbox: info@retailco.com
└── Domain: retailco.com

// Client 2
Pod: "Client - FinTech"
├── Inbox: support@fintech.ai
└── Domain: fintech.ai
```

```typescript
// Agent 1: Customer Support Agent
Pod: "Support-Agent"
├── Inbox: support@mycompany.com
├── Inbox: help@mycompany.com
└── Inbox: tickets@mycompany.com

// Agent 2: Sales Outreach Agent
Pod: "Sales-Agent"
├── Inbox: sales@mycompany.com
├── Inbox: outreach@mycompany.com
└── Inbox: leads@mycompany.com

// Agent 3: Marketing Agent
Pod: "Marketing-Agent"
├── Inbox: newsletter@mycompany.com
├── Inbox: campaigns@mycompany.com
└── Inbox: events@mycompany.com
```

--------------------------------

### Get List Entry API Request Example

Source: https://docs.agentmail.to/api-reference/lists/get

This example demonstrates how to make a GET request to the Agentmail.to API to retrieve a list entry. It requires specifying the direction, type, and entry identifier in the URL path, along with an Authorization header.

```HTTP
GET https://api.agentmail.to/v0/lists/{direction}/{type}/{entry} \
  -H "Authorization: Bearer YOUR_API_KEY"
```

--------------------------------

### Run Python Webhook Receiver

Source: https://docs.agentmail.to/webhook-setup

Command to execute the Python webhook receiver script. This assumes the script is saved as `webhook_receiver.py` and that Python is installed and accessible in the system's PATH.

```bash
python webhook_receiver.py
```

--------------------------------

### Create Pod via HTTP POST Request (Swift)

Source: https://docs.agentmail.to/api-reference/pods/create

This Swift example shows how to create a pod by making an HTTP POST request using URLSession. It defines the necessary headers, prepares the request with the correct HTTP method and body, and sends it asynchronously. The response or any errors are logged.

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Register Webhook with AgentMail using Python

Source: https://docs.agentmail.to/webhook-setup

Registers a webhook endpoint with AgentMail, specifying the URL where notifications should be sent. This example uses a placeholder ngrok URL and a `client_id` for idempotency.

```python
# Using the ngrok URL you copied
webhook_url = "https://your-subdomain.ngrok-free.app/webhooks"

webhook = client.webhooks.create(
    url=webhook_url,
    client_id="webhook-demo-webhook"  # Ensures idempotency
)

print(f"Webhook created: {webhook.webhook_id}")
```

--------------------------------

### Fetch Draft via HTTP Request (C#)

Source: https://docs.agentmail.to/api-reference/drafts/get

Demonstrates making an HTTP GET request to the AgentMail API to fetch a draft using C#. This example utilizes the RestSharp library.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/drafts/draft_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### List API Keys via HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/api-keys/list

Provides a Go example for making a GET request to the AgentMail API to list API keys. This method uses the standard Go `net/http` package and requires manual header management.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/api-keys"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### List Pod Threads via HTTP (Go)

Source: https://docs.agentmail.to/api-reference/pods/threads/list

Provides a Go example for listing threads in a pod using direct HTTP requests. It constructs a GET request to the AgentMail API endpoint, including the necessary Authorization header with a Bearer token.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/threads"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### List Threads via HTTP GET Request (C#)

Source: https://docs.agentmail.to/api-reference/threads/list

An example in C# using the RestSharp library to send an HTTP GET request to the AgentMail API for threads. It shows how to add the Authorization header.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/threads");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### GET /v0/drafts/{draft_id}

Source: https://docs.agentmail.to/api-reference/drafts/get

This endpoint retrieves a specific draft using its ID. The examples demonstrate how to make a GET request with an API key for authentication.

```APIDOC
## GET /v0/drafts/{draft_id}

### Description
Retrieves a specific draft by its unique identifier.

### Method
GET

### Endpoint
/v0/drafts/{draft_id}

### Parameters
#### Path Parameters
- **draft_id** (string) - Required - The unique identifier of the draft to retrieve.

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
curl -X GET \
  'https://api.agentmail.to/v0/drafts/draft_id' \
  -H 'Authorization: Bearer <api_key>'
```

### Response

#### Success Response (200)

- **body** (object) - The content of the draft.

#### Response Example

```json
{
  "id": "draft_id",
  "subject": "Example Subject",
  "body": "This is the content of the draft."
}
```

```
--------------------------------

### Create Inbox and Send Email with AgentMail API (Python)

Source: https://docs.agentmail.to/get-started/quickstart

Initializes the AgentMail client using an API key from a .env file, creates a new email inbox, and sends a test email. Requires the 'agentmail' and 'python-dotenv' libraries.

```python
import os
from dotenv import load_dotenv
from agentmail import AgentMail

# Load the API key from the .env file
load_dotenv()
api_key = os.getenv("AGENTMAIL_API_KEY")

# Initialize the client
client = AgentMail(api_key=api_key)

# Create an inbox
print("Creating inbox...")
inbox = client.inboxes.create() # domain is optional
print("Inbox created successfully!")
print(inbox)

# Send Email

client.inboxes.messages.send(
    inbox_id="your-email@example.com",
    to="contact@agentmail.to",
    subject="Hello from AgentMail!",
    text="This is my first email sent with the AgentMail API."

)
```

--------------------------------

### List Pod Threads via HTTP (Java)

Source: https://docs.agentmail.to/api-reference/pods/threads/list

An example in Java using the Unirest library to make an HTTP GET request to list pod threads. It configures the request with the correct URL and the 'Authorization' header.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id/threads")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Create Domain via HTTP POST (Go)

Source: https://docs.agentmail.to/api-reference/domains/create

Illustrates creating a new domain by making a direct HTTP POST request to the AgentMail API. This example uses Go's standard net/http package. It constructs the request with necessary headers and JSON payload.

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/domains"

    payload := strings.NewReader("{\n  \"domain\": \"domain\",\n  \"feedback_enabled\": true\n}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Get Zone File using Agentmail API (PHP)

Source: https://docs.agentmail.to/api-reference/domains/get-zone-file

PHP example using GuzzleHttp to call the Agentmail API and get a zone file. It demonstrates setting the Authorization header for authentication.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/domains/%3Adomain_id/zone-file', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### GET /v0/pods/{pod_id}/inboxes/{inbox_id}

Source: https://docs.agentmail.to/api-reference/pods/inboxes/get

This endpoint retrieves a specific inbox within a pod. The examples demonstrate how to make a GET request using different SDKs and libraries.

```APIDOC
## GET /v0/pods/{pod_id}/inboxes/{inbox_id}

### Description
Retrieves a specific inbox within a pod.

### Method
GET

### Endpoint
`/v0/pods/{pod_id}/inboxes/{inbox_id}`

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The ID of the pod.
- **inbox_id** (string) - Required - The ID of the inbox.

#### Query Parameters
None

#### Request Body
None

### Request Example
```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.inboxes.get("pod_id", "inbox_id");
}
main();
```

### Response

#### Success Response (200)

- **(structure depends on API response)**

#### Response Example

```json
{
  "example": "response body"
}
```

```
--------------------------------

### Fetch Draft via HTTP Request (Swift)

Source: https://docs.agentmail.to/api-reference/drafts/get

Provides a Swift example for fetching a draft by making an HTTP GET request to the AgentMail API. This code uses `URLSession` for network operations.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/drafts/draft_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Configure Environment Variables with .env

Source: https://docs.agentmail.to/webhook-agent

This example displays a .env file used for storing sensitive API keys and configuration settings. It includes placeholders for AgentMail API Key, OpenAI API Key, ngrok authtoken, and project-specific details like inbox username, webhook domain, target email, and GitHub repository.

```env
AGENTMAIL_API_KEY="your_agentmail_api_key"
OPENAI_API_KEY="your_openai_api_key"

NGROK_AUTHTOKEN="your_ngrok_authtoken"
INBOX_USERNAME="github-star-agent"
WEBHOOK_DOMAIN="your-ngrok-subdomain.ngrok-free.app"
DEMO_TARGET_EMAIL="your-email@example.com"
TARGET_GITHUB_REPO="YourGitHub/YourRepo"
```

--------------------------------

### Get Zone File using Agentmail API (Go)

Source: https://docs.agentmail.to/api-reference/domains/get-zone-file

Provides a Go code example for making a GET request to the Agentmail API to retrieve a zone file. It includes manual HTTP request construction with Authorization header.

```go
package main

import (
    "fmt"
    "io"
    "net/http"
)

func main() {

    url := "https://api.agentmail.to/v0/domains/%3Adomain_id/zone-file"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### List Threads via HTTP GET Request (PHP)

Source: https://docs.agentmail.to/api-reference/threads/list

This PHP code snippet uses the Guzzle HTTP client to perform a GET request for threads, including the required Authorization header. Assumes Guzzle is installed via Composer.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/threads', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### Fetch Inbox Metrics via HTTP GET Request (Java)

Source: https://docs.agentmail.to/api-reference/inboxes/metrics/get

An example in Java using the Unirest library to make an HTTP GET request for inbox metrics. It sets the 'Authorization' header and retrieves the response as a string. Ensure Unirest is included as a dependency.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Start Agent Execution (Bash)

Source: https://docs.agentmail.to/sales-agent-websocket

Command to start the AgentMail agent. This script initiates the agent process, which then connects to the AgentMail WebSocket to listen for incoming emails.

```bash
python main.py
```

--------------------------------

### Create Pod via HTTP POST Request (Ruby)

Source: https://docs.agentmail.to/api-reference/pods/create

This Ruby example illustrates creating a pod by sending an HTTP POST request to the AgentMail API. It configures the request with the correct URL, headers (Authorization and Content-Type), and an empty JSON body. The response body is then printed.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{}"

response = http.request(request)
puts response.read_body
```

--------------------------------

### Fetch Draft using AgentMail Library (Python)

Source: https://docs.agentmail.to/api-reference/drafts/get

Shows how to instantiate the AgentMail client and retrieve a draft using its ID with the Python library. Ensure the 'agentmail' library is installed.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.drafts.get(
    draft_id="draft_id"
)
```

--------------------------------

### Create Domain in Pod using HTTP Request (Swift)

Source: https://docs.agentmail.to/api-reference/pods/domains/create

This Swift example demonstrates how to create a domain in a pod by making an HTTP POST request. It configures the request with necessary headers and the JSON body containing domain details, then sends it using URLSession.

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [
  "domain": "domain",
  "feedback_enabled": true
] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id/domains")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Fetch Inbox Metrics via HTTP GET Request (C#)

Source: https://docs.agentmail.to/api-reference/inboxes/metrics/get

A C# example using the RestSharp library to perform an HTTP GET request for inbox metrics. It configures the client, adds the 'Authorization' header, and executes the request, storing the response.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### Fetch Draft via HTTP Request (PHP)

Source: https://docs.agentmail.to/api-reference/drafts/get

Shows how to retrieve a draft by sending an HTTP GET request to the AgentMail API using PHP. This example relies on the Guzzle HTTP client.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/drafts/draft_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### Fetch Draft via HTTP Request (Java)

Source: https://docs.agentmail.to/api-reference/drafts/get

Provides an example of fetching a draft using an HTTP GET request to the AgentMail API in Java. This snippet utilizes the `mashape-unirest` library for making HTTP requests.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/drafts/draft_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Organizations API - GET

Source: https://docs.agentmail.to/api-reference/organizations/get

This endpoint retrieves a list of organizations. Examples are provided in TypeScript, Python, Go, Ruby, Java, PHP, C#, and Swift.

```APIDOC
## GET /v0/organizations

### Description
Retrieves a list of organizations associated with the API key.

### Method
GET

### Endpoint
/v0/organizations

### Parameters
#### Query Parameters
None

#### Request Body
None

### Request Example
(See language-specific examples below)

### Response
#### Success Response (200)
- **organizations** (array) - A list of organization objects.
  - **id** (string) - The unique identifier for the organization.
  - **name** (string) - The name of the organization.

#### Response Example
```json
[
  {
    "id": "org_123",
    "name": "Example Organization"
  }
]
```

## SDK Code Examples

### TypeScript

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.organizations.get();
}
main();
```

### Python

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.organizations.get()
```

### Go

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/organizations"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))
}
```

### Ruby

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/organizations")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

### Java

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/organizations")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

### PHP

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/organizations', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

### C#

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/organizations");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

### Swift

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/organizations")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

```
--------------------------------

### Create Draft via HTTP Request (Ruby)

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/create

A Ruby example demonstrating how to create a draft by sending an HTTP POST request to the AgentMail API. It configures the request with necessary headers like Authorization and Content-Type.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/drafts")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{}"

response = http.request(request)
puts response.read_body
```

--------------------------------

### Make HTTP GET Request for Inbox Data

Source: https://docs.agentmail.to/api-reference/pods/inboxes/get

These examples demonstrate how to make a direct HTTP GET request to the AgentMail API endpoint for fetching inbox data. They show how to set up the request, include the necessary Authorization header with an API key, and handle the response. These snippets are useful if you are not using the official SDK or need to interact with the API at a lower level.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/inboxes/inbox_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/inboxes/inbox_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id/inboxes/inbox_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/pods/pod_id/inboxes/inbox_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id/inboxes/inbox_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id/inboxes/inbox_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### List Pods via HTTP GET Request (Java)

Source: https://docs.agentmail.to/api-reference/pods/list

An example in Java using the Unirest library to make an HTTP GET request to the AgentMail API for listing pods. It demonstrates setting the Authorization header for authentication.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Retrieve List Entry Allow - C# SDK

Source: https://docs.agentmail.to/api-reference/lists/get

A C# example using the RestSharp library to get list entry allowance. It configures a GET request with the Authorization header and executes it against the Agentmail.to API. Requires the RestSharp NuGet package.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/lists/send/allow/entry");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### AgentMail Initialization and Setup (Python)

Source: https://docs.agentmail.to/documentation/examples/smart-labeling-agent

Initializes the Flask web server, AgentMail client, and OpenAI client. Sets up the AgentMail inbox with idempotency and starts an ngrok tunnel to expose the local Flask application to the internet for receiving webhooks.

```python
# Load environment variables first
load_dotenv()

# Initialize three clients
app = Flask(__name__)
client = AgentMail()            # AgentMail SDK
openai_client = OpenAI()        # OpenAI for AI classification

# Create inbox with idempotency
inbox = client.inboxes.create(
    username=INBOX_USERNAME,
    client_id=f"{INBOX_USERNAME}-inbox"  # Prevents duplicates
)

# Start ngrok tunnel (localhost → public URL)
listener = ngrok.forward(PORT, domain=WEBHOOK_DOMAIN)
```

--------------------------------

### Get Zone File using Agentmail API (Swift)

Source: https://docs.agentmail.to/api-reference/domains/get-zone-file

Swift code example for fetching a zone file from the Agentmail API using URLSession. It shows how to configure the request with the Authorization header.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/domains/%3Adomain_id/zone-file")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Fetch Inbox Data using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/inboxes/get

Demonstrates how to fetch inbox data using the AgentMail SDK. This involves initializing the client with an API key and calling the get method for a specific inbox. Ensure you have the agentmail library installed.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.get("inbox_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.get(
    inbox_id="inbox_id"
)
```

--------------------------------

### Create Domain via HTTP POST (Swift)

Source: https://docs.agentmail.to/api-reference/domains/create

Illustrates creating a new domain using an HTTP POST request in Swift. This example utilizes URLSession and NSMutableURLRequest to construct and send the request, including setting authorization headers and the JSON body.

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [
  "domain": "domain",
  "feedback_enabled": true
] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/domains")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### List API Keys via HTTP Request (Swift)

Source: https://docs.agentmail.to/api-reference/api-keys/list

An example in Swift showing how to make an HTTP GET request to the AgentMail API to retrieve API keys. It uses `URLSession` and `NSMutableURLRequest` for network communication.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/api-keys")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### List Inbox Messages via HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/list

This Go example shows how to make a direct HTTP GET request to the AgentMail API to list messages from an inbox. It includes setting the Authorization header with a Bearer token. No external SDK is used.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/messages"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Verify API Key and List Inboxes (Python)

Source: https://docs.agentmail.to/sales-agent-websocket

This snippet demonstrates how to initialize the AgentMail client with an API key and list available inboxes to verify a successful connection. It requires the agentmail library to be installed.

```python
client = AsyncAgentMail(api_key="your-key")
print(await client.inboxes.list())  # Should succeed
```

--------------------------------

### List Pods via HTTP GET Request (C#)

Source: https://docs.agentmail.to/api-reference/pods/list

A C# example using the RestSharp library to perform an HTTP GET request to the AgentMail API for listing pods. The code illustrates adding the necessary Authorization header.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### Create Domain and Get DNS Records via Python SDK

Source: https://docs.agentmail.to/custom-domains

This Python code snippet demonstrates how to create a domain and fetch its DNS records using the AgentMail SDK. It shows both default creation and creation with feedback forwarding disabled. The response includes domain details and the necessary DNS records.

```python
from agentmail import AgentMail

client = AgentMail(api_key="YOUR_API_KEY")

# Create domain with default settings
domain = client.domains.create("your-domain.com")

# Or with custom feedback forwarding
domain = client.domains.create(
  "your-domain.com",
  feedback_enabled=False
)

print("Domain created:", domain)
print("DNS Records:", domain.records)
```

--------------------------------

### Fetch Organizations using HTTP Request (PHP)

Source: https://docs.agentmail.to/api-reference/organizations/get

This PHP example utilizes the GuzzleHttp client to make an HTTP GET request to fetch organization data. It requires the GuzzleHttp library and correctly sets the Authorization header.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/organizations', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### List Inbox Threads using AgentMail API (Go)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/list

Provides a Go example for fetching inbox threads directly via the AgentMail API. This involves making an HTTP GET request with appropriate headers, including the Bearer token.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/threads"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### List Pods via HTTP GET Request (Ruby)

Source: https://docs.agentmail.to/api-reference/pods/list

Shows how to retrieve a list of pods by sending an HTTP GET request to the AgentMail API using Ruby's Net::HTTP library. This example includes setting the necessary Authorization header.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Create Domain in Pod using AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/pods/domains/create

This Python example demonstrates how to create a domain within a pod using the AgentMail SDK. It requires an API key for authentication and specifies the pod ID, domain name, and feedback enabled status.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.domains.create(
    pod_id="pod_id",
    domain="domain",
    feedback_enabled=True
)
```

--------------------------------

### Create Draft via HTTP Request (Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/create

A Swift example demonstrating how to create a draft by making an HTTP POST request using URLSession. It sets up the request headers and body for the AgentMail API endpoint.

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/drafts")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Download Attachment via C# RestSharp

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

Provides a C# example using the RestSharp library to download a message attachment from AgentMail. It configures a GET request with the necessary 'Authorization' header and executes it, capturing the response.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/attachments/attachment_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### Fetch Inbox Message using HTTP Client (Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get

Illustrates fetching a specific message from an inbox using standard HTTP client libraries in Ruby, Java, PHP, C#, and Swift. These examples require an API key and specific inbox/message IDs, and demonstrate making a GET request with an Authorization header.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Create Webhook using AgentMail SDK (TypeScript, Python, Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/webhooks/create

Demonstrates how to create a webhook subscription using the AgentMail SDK. This involves initializing the client with an API key and specifying the URL and event types for the webhook. The examples cover multiple programming languages, showing the equivalent API calls.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.webhooks.create({
        url: "url",
        eventTypes: [
            "message.received",
            "message.received",
        ],
    });
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.webhooks.create(
    url="url",
    event_types=[
        "message.received",
        "message.received"
    ]
)
```

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/webhooks"

    payload := strings.NewReader("{\n  \"url\": \"url\",\n  \"event_types\": [\n    \"message.received\",\n    \"message.received\"\n  ]\n}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/webhooks")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{\n  \"url\": \"url\",\n  \"event_types\": [\n    \"message.received\",\n    \"message.received\"\n  ]\n}"

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.post("https://api.agentmail.to/v0/webhooks")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .body("{\n  \"url\": \"url\",\n  \"event_types\": [\n    \"message.received\",\n    \"message.received\"\n  ]\n}")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/webhooks', [
  'body' => '{
  "url": "url",
  "event_types": [
    "message.received",
    "message.received"
  ]
}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/webhooks");
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer <api_key>");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"url\": \"url\",\n  \"event_types\": [\n    \"message.received\",\n    \"message.received\"\n  ]\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [
  "url": "url",
  "event_types": ["message.received", "message.received"]
] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/webhooks")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Get Zone File using Agentmail API (TypeScript)

Source: https://docs.agentmail.to/api-reference/domains/get-zone-file

Example of how to retrieve a domain's zone file using the Agentmail SDK for TypeScript. Requires an API key for authentication and the domain ID as a parameter.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.domains.getZoneFile(":domain_id");
}
main();
```

--------------------------------

### Fetch Organizations using HTTP Request (Swift)

Source: https://docs.agentmail.to/api-reference/organizations/get

This Swift example demonstrates making an HTTP GET request to fetch organization data from the AgentMail API using URLSession. It includes setting up the request with the necessary Authorization header.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/organizations")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Install OpenAI Library

Source: https://docs.agentmail.to/documentation/examples/auto-reply-agent

Installs the OpenAI Python library using pip. This is a prerequisite for using OpenAI's services in your project.

```bash
pip install openai
```

--------------------------------

### Fetch Threads using AgentMail SDK (TypeScript, Python)

Source: https://docs.agentmail.to/api-reference/pods/threads/get

Examples of fetching threads from a specific pod using the AgentMail SDK. Requires an API key for authentication. These examples demonstrate client initialization and the call to retrieve thread data.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.threads.get("pod_id", "thread_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.threads.get(
    pod_id="pod_id",
    thread_id="thread_id"
)
```

--------------------------------

### Fetch Inbox Message using AgentMail SDK (TypeScript, Python, Go)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get

Demonstrates fetching a specific message from an inbox using the AgentMail SDK in TypeScript and Python, and a direct HTTP GET request in Go. These examples require API keys and specific inbox/message IDs.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.messages.get("inbox_id", "message_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.messages.get(
    inbox_id="inbox_id",
    message_id="message_id"
)
```

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Create Pod using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/pods/create

Demonstrates how to create a new pod using the AgentMail TypeScript SDK. It initializes the client with an API key and calls the create method on the pods object. Ensure you have the 'agentmail' package installed.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.create({});
}
main();
```

--------------------------------

### Get Draft Attachment - AgentMail SDK Examples

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/get-attachment

These examples show how to retrieve an attachment from a draft within an inbox using the AgentMail SDK or direct HTTP requests. They require an API key and specific IDs for the inbox, draft, and attachment. Ensure you replace placeholders like 'YOUR_TOKEN_HERE', 'inbox_id', 'draft_id', and 'attachment_id' with your actual values.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.drafts.getAttachment("inbox_id", "draft_id", "attachment_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.drafts.get_attachment(
    inbox_id="inbox_id",
    draft_id="draft_id",
    attachment_id="attachment_id"
)
```

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/attachments/attachment_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/attachments/attachment_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/attachments/attachment_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/attachments/attachment_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/attachments/attachment_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/attachments/attachment_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### List Drafts - Go

Source: https://docs.agentmail.to/api-reference/drafts/list

Example of how to list drafts using a direct HTTP request in Go.

```APIDOC
## GET /v0/drafts

### Description
Retrieves a list of all drafts.

### Method
GET

### Endpoint
/v0/drafts

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of drafts to return.
- **offset** (integer) - Optional - The number of drafts to skip before returning results.

### Request Example
```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/drafts"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

### Response

#### Success Response (200)

- **drafts** (array) - A list of draft objects.
   - **id** (string) - The unique identifier of the draft.
   - **subject** (string) - The subject line of the draft.
   - **createdAt** (string) - The timestamp when the draft was created.

#### Response Example

```json
{
  "drafts": [
    {
      "id": "draft_123",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z"
    }
  ]
}
```

```
--------------------------------

### Fetch Organizations using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/organizations/get

This example shows how to initialize the AgentMail client with an API key and fetch organization data using the TypeScript SDK. It requires the 'agentmail' package.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.organizations.get();
}
main();
```

--------------------------------

### List Inbox Threads using AgentMail API (Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/list

A Swift example for fetching inbox threads from the AgentMail API. It uses URLSession to make an HTTP GET request and includes the necessary Authorization header.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/threads")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Retrieve Drafts using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/pods/drafts/get

Demonstrates how to retrieve a draft from a specific pod using the AgentMail SDK. This involves initializing the client with an API key and calling the get method on the drafts resource. Ensure you have the agentmail SDK installed.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.drafts.get("pod_id", "draft_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.drafts.get(
    pod_id="pod_id",
    draft_id="draft_id"
)
```

--------------------------------

### Allow List Entry via Agentmail.to API (Python, JavaScript, Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/pods/lists/get

Demonstrates how to make a GET request to the Agentmail.to API to allow an entry into a list. This requires an API key for authorization. The examples cover common HTTP client libraries in each language.

```python
import requests

url = "https://api.agentmail.to/v0/pods/pod_id/lists/send/allow/entry"

headers = {"Authorization": "Bearer <api_key>"}

response = requests.get(url, headers=headers)

print(response.json())
```

```javascript
const url = 'https://api.agentmail.to/v0/pods/pod_id/lists/send/allow/entry';
const options = {method: 'GET', headers: {Authorization: 'Bearer <api_key>'}};

try {
  const response = await fetch(url, options);
  const data = await response.json();
  console.log(data);
} catch (error) {
  console.error(error);
}
```

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/lists/send/allow/entry"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/lists/send/allow/entry")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id/lists/send/allow/entry")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/pods/pod_id/lists/send/allow/entry', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
?>
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id/lists/send/allow/entry");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id/lists/send/allow/entry")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Retrieve List Entry Allow - JavaScript SDK

Source: https://docs.agentmail.to/api-reference/lists/get

Shows how to retrieve list entry allowance using the JavaScript fetch API. This example makes an asynchronous GET request to the Agentmail.to API, including an Authorization header. Handles potential errors during the fetch operation.

```javascript
const url = 'https://api.agentmail.to/v0/lists/send/allow/entry';
const options = {method: 'GET', headers: {Authorization: 'Bearer <api_key>'}};

try {
  const response = await fetch(url, options);
  const data = await response.json();
  console.log(data);
} catch (error) {
  console.error(error);
}
```

--------------------------------

### Fetch Organizations using AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/organizations/get

This example demonstrates fetching organization data by initializing the AgentMail client with an API key in Python. It relies on the 'agentmail' Python package.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.organizations.get()
```

--------------------------------

### Create Domain using AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/domains/create

Shows how to create a new domain using the AgentMail Python SDK. Requires the 'agentmail' library. Initializes the client with an API key and invokes the domains.create method.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.domains.create(
    domain="domain",
    feedback_enabled=True
)
```

--------------------------------

### Authenticate Ngrok

Source: https://docs.agentmail.to/webhook-setup

Authenticates the ngrok client with your ngrok account using an authtoken. The authtoken can be found in your ngrok dashboard.

```bash
ngrok config add-authtoken YOUR_AUTHTOKEN
```

--------------------------------

### Fetch Organizations using HTTP Request (Ruby)

Source: https://docs.agentmail.to/api-reference/organizations/get

This Ruby example shows how to perform an HTTP GET request to retrieve organization data from the AgentMail API. It utilizes Ruby's built-in Net::HTTP library and requires setting the Authorization header.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/organizations")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Create Domain in Pod using HTTP Request (Ruby)

Source: https://docs.agentmail.to/api-reference/pods/domains/create

This Ruby example demonstrates creating a domain in a pod via an HTTP POST request to the AgentMail API. It sets the necessary headers, including Authorization and Content-Type, and sends the domain details in the request body.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/domains")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{\n  \"domain\": \"domain\",\n  \"feedback_enabled\": true\n}"

response = http.request(request)
puts response.read_body
```

--------------------------------

### Fetch Metrics via HTTP Request (Swift)

Source: https://docs.agentmail.to/api-reference/metrics/list

This Swift example demonstrates fetching metrics by making an HTTP GET request to the AgentMail API using URLSession. It shows how to configure the request with headers and handle the response. The API key must be manually provided.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Retrieve List Entry Allow - Java SDK

Source: https://docs.agentmail.to/api-reference/lists/get

A Java example using the Unirest library to fetch list entry allowance. It performs a GET request to the Agentmail.to API, including the required Authorization header. Note: Requires the Unirest library to be added as a dependency.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/lists/send/allow/entry")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Reply to a Message using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/inboxes/messages/reply

Demonstrates how to reply to a specific message within an inbox using the AgentMail SDK. This functionality requires an API key for authentication and the inbox and message IDs to target the correct message. The examples show basic setup and the reply action.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.messages.reply("inbox_id", "message_id", {});
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.messages.reply(
    inbox_id="inbox_id",
    message_id="message_id"
)
```

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/reply"

    payload := strings.NewReader("{}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/reply")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{}"

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.post("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/reply")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .body("{}")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/reply', [
  'body' => '{}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/reply");
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer <api_key>");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/reply")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Send Draft using AgentMail SDK (TypeScript, Python, Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/send

Examples of sending a draft email using the AgentMail SDK. These snippets cover initializing the client, specifying inbox and draft IDs, and making the API call. Dependencies include the respective AgentMail SDKs or HTTP client libraries for each language.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.drafts.send("inbox_id", "draft_id", {});
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.drafts.send(
    inbox_id="inbox_id",
    draft_id="draft_id"
)
```

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/send"

    payload := strings.NewReader("{}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/send")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{}"

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.post("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/send")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .body("{}")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/send', [
  'body' => '{}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/send");
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer <api_key>");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id/send")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Create Project Directory (Bash)

Source: https://docs.agentmail.to/documentation/examples/smart-labeling-agent

This snippet demonstrates the command-line steps to create a new directory for the smart labeling agent project and navigate into it. It's a fundamental setup step for the project.

```bash
mkdir smart-labeling-agent
cd smart-labeling-agent
```

--------------------------------

### Install Dependencies and Run Webhook Server (Python)

Source: https://docs.agentmail.to/webhook-verification

This command installs the necessary Python packages (Flask, python-dotenv, svix) and then runs the webhook server script. Ensure you have Python and pip installed.

```bash
pip install flask python-dotenv svix
python webhook_server.py
```

--------------------------------

### List Inbox Messages via HTTP Request (Ruby)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/list

This Ruby example illustrates making an HTTP GET request to the AgentMail API to fetch inbox messages. It manually constructs the request, including the 'Authorization' header. This method does not rely on a specific SDK.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/messages")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Create AgentMail Inbox using Python

Source: https://docs.agentmail.to/webhook-setup

Demonstrates how to create a dedicated inbox for receiving webhook notifications using the AgentMail Python SDK. It utilizes a `client_id` for idempotency to prevent duplicate inboxes.

```python
from agentmail import AgentMail

client = AgentMail()

# Create an inbox for your webhook agent
inbox = client.inboxes.create(
    username="webhook-demo",
    client_id="webhook-demo-inbox"  # Ensures idempotency
)

print(f"Inbox created: {inbox.inbox_id}")
```

--------------------------------

### List Inbox Messages via HTTP Request (Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/list

This Swift example shows how to construct and execute an HTTP GET request using URLSession to fetch inbox messages from the AgentMail API. It includes setting the 'Authorization' header. Error handling for the network request is also included.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/messages")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Download Message Attachment with Ruby HTTP Client

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

Illustrates how to download a message attachment using Ruby's Net::HTTP library. This example makes a direct HTTP GET request to the AgentMail API, setting the necessary Authorization header. It then prints the response body, which contains the attachment content.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/attachments/attachment_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Create Inbox using AgentMail SDK (TypeScript, Python, Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/create

Examples of creating a new inbox using the AgentMail SDK. These snippets demonstrate the basic setup and API call for inbox creation in different programming languages. Ensure you replace placeholder API keys with your actual token.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.create();
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.create()
```

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes"

    req, _ := http.NewRequest("POST", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.post("https://api.agentmail.to/v0/inboxes")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/inboxes', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes");
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer <api_key>");
request.AddHeader("Content-Type", "application/json");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Retrieve List Entry Allow - PHP SDK

Source: https://docs.agentmail.to/api-reference/lists/get

This PHP snippet demonstrates fetching list entry allowance using the Guzzle HTTP client. It sends a GET request to the Agentmail.to API with the Authorization header. Ensure the Guzzle HTTP client is installed via Composer.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/lists/send/allow/entry', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### GET /v0

Source: https://docs.agentmail.to/api-reference/websockets/websockets

Establishes a connection to the Agentmail.to service.

```APIDOC
## GET /v0

### Description
Establishes a connection to the Agentmail.to service.

### Method
GET

### Endpoint
/v0

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
- **message** (string) - A confirmation message indicating a successful connection.

#### Response Example
{
  "message": "Connected successfully"
}
```

--------------------------------

### List Drafts - Python

Source: https://docs.agentmail.to/api-reference/drafts/list

Example of how to list drafts using the AgentMail Python SDK.

```APIDOC
## GET /v0/drafts

### Description
Retrieves a list of all drafts.

### Method
GET

### Endpoint
/v0/drafts

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of drafts to return.
- **offset** (integer) - Optional - The number of drafts to skip before returning results.

### Request Example
```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.drafts.list()
```

### Response

#### Success Response (200)

- **drafts** (array) - A list of draft objects.
   - **id** (string) - The unique identifier of the draft.
   - **subject** (string) - The subject line of the draft.
   - **createdAt** (string) - The timestamp when the draft was created.

#### Response Example

```json
{
  "drafts": [
    {
      "id": "draft_123",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z"
    }
  ]
}
```

```
--------------------------------

### List Inbox Messages via HTTP Request (C#)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/list

This C# example uses the RestSharp library to perform an HTTP GET request to the AgentMail API for listing messages. It demonstrates adding the 'Authorization' header. Make sure RestSharp is added as a NuGet package.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/messages");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### Start the Agent Script

Source: https://docs.agentmail.to/documentation/examples/smart-labeling-agent

This command starts the AgentMail agent by executing the main Python script. Ensure you are in the correct directory before running.

```bash
python agent.py
```

--------------------------------

### Fetch Metrics via HTTP Request (PHP)

Source: https://docs.agentmail.to/api-reference/metrics/list

This PHP example demonstrates fetching metrics by making an HTTP GET request to the AgentMail API using GuzzleHttp. It includes setting the Authorization header and echoing the response body. The API key must be manually provided.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### List Threads using AgentMail Library (Python)

Source: https://docs.agentmail.to/api-reference/threads/list

Shows how to instantiate the AgentMail client and call the threads.list() method using the Python library. Requires the 'agentmail' package.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.threads.list()
```

--------------------------------

### List Webhooks via HTTP Request (Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/webhooks/list

Demonstrates how to list webhooks by making direct HTTP GET requests to the AgentMail API endpoint. These examples cover different programming languages and their respective HTTP client libraries. Authentication is handled via a Bearer token in the Authorization header.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/webhooks"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/webhooks")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/webhooks")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/webhooks', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/webhooks");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/webhooks")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Fetch Metrics via HTTP Request (Ruby)

Source: https://docs.agentmail.to/api-reference/metrics/list

This Ruby example demonstrates fetching metrics by making an HTTP GET request to the AgentMail API. It utilizes the Net::HTTP library to set the URL, headers including authorization, and retrieve the response body. The API key must be manually provided.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Handle Incoming Webhooks (Python)

Source: https://docs.agentmail.to/webhook-agent

This Flask route handles incoming POST requests to the /webhooks endpoint. It logs the received payload and starts a new thread to process the webhook data asynchronously using the process_webhook function. This prevents blocking the main request thread.

```python
@app.route("/webhooks", methods=["POST"])
def receive_webhook():
  print(f"[/webhooks] Received webhook. Payload keys: {list(request.json.keys()) if request.is_json else 'Not JSON or empty'}")
  Thread(target=process_webhook, args=(request.json,)).start()
  return Response(status=200)
```

--------------------------------

### Install Dependencies and Run Webhook Server (TypeScript)

Source: https://docs.agentmail.to/webhook-verification

This command installs the necessary Node.js packages (express, svix, dotenv) and then runs the webhook server script using ts-node. Ensure you have Node.js and npm installed.

```bash
npm install express svix dotenv
npx ts-node webhook_server.ts
```

--------------------------------

### List Metrics using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/metrics/list

This example shows how to initialize the AgentMail client and list metrics within a specified time range using the TypeScript SDK. It requires the 'agentmail' package and an API key for authentication.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.metrics.list({
        startTimestamp: new Date("2024-01-15T09:30:00Z"),
        endTimestamp: new Date("2024-01-15T09:30:00Z"),
    });
}
main();
```

--------------------------------

### List Inbox Messages via HTTP Request (PHP)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/list

This PHP example utilizes the Guzzle HTTP client to make a GET request to the AgentMail API for retrieving inbox messages. It shows how to add the 'Authorization' header. The 'vendor/autoload.php' must be included.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/messages', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### Create Pod via HTTP POST Request (PHP)

Source: https://docs.agentmail.to/api-reference/pods/create

This PHP example utilizes the Guzzle HTTP client to send a POST request for creating a pod. It specifies the API endpoint, sets the required Authorization and Content-Type headers, and includes an empty JSON body. The response body is then echoed.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/pods', [
  'body' => '{}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

--------------------------------

### Create Domain and Get DNS Records via TypeScript SDK

Source: https://docs.agentmail.to/custom-domains

This TypeScript code snippet illustrates creating a domain and retrieving its DNS records using the AgentMail SDK. It covers both default creation and customization of feedback forwarding. The output provides domain information and the required DNS records.

```typescript
import { AgentMailClient } from "agentmail";

const client = new AgentMailClient({
  apiKey: "YOUR_API_KEY",
});

// Create domain with default settings
const domain = await client.domains.create("your-domain.com");

// Or with custom feedback forwarding
const domain = await client.domains.create("your-domain.com", {
  feedback_enabled: false
});

console.log("Domain created:", domain);
console.log("DNS Records:", domain.records);
```

--------------------------------

### Connect and Subscribe to Email Events via WebSockets (Python)

Source: https://docs.agentmail.to/websockets/quickstart

Establishes a WebSocket connection to AgentMail, subscribes to an inbox, and processes incoming events like 'Subscribed' and 'MessageReceivedEvent'. Requires the 'agentmail' package.

```python
from agentmail import AgentMail, MessageReceivedEvent, Subscribe, Subscribed

client = AgentMail()

with client.websockets.connect() as socket:
    socket.send_subscribe(Subscribe(inbox_ids=["my-agent@agentmail.to"]))

    for event in socket:
        if isinstance(event, Subscribed):
            print(f"Subscribed to {event.inbox_ids}")
        elif isinstance(event, MessageReceivedEvent):
            msg = event.message
            print(f"Received message from: {msg.from_}")
```

--------------------------------

### Fetch Inbox Threads via HTTP Request

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Illustrates how to fetch threads from an inbox by making direct HTTP GET requests to the AgentMail API. These examples use standard HTTP libraries for each language and require an API key passed in the Authorization header. They handle constructing the URL, setting headers, and processing the response.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### List Drafts - Java

Source: https://docs.agentmail.to/api-reference/drafts/list

Example of how to list drafts using the Unirest library in Java.

```APIDOC
## GET /v0/drafts

### Description
Retrieves a list of all drafts.

### Method
GET

### Endpoint
/v0/drafts

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of drafts to return.
- **offset** (integer) - Optional - The number of drafts to skip before returning results.

### Request Example
```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/drafts")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

### Response

#### Success Response (200)

- **drafts** (array) - A list of draft objects.
   - **id** (string) - The unique identifier of the draft.
   - **subject** (string) - The subject line of the draft.
   - **createdAt** (string) - The timestamp when the draft was created.

#### Response Example

```json
{
  "drafts": [
    {
      "id": "draft_123",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z"
    }
  ]
}
```

```
--------------------------------

### List Drafts - Swift

Source: https://docs.agentmail.to/api-reference/drafts/list

Example of how to list drafts using URLSession in Swift.

```APIDOC
## GET /v0/drafts

### Description
Retrieves a list of all drafts.

### Method
GET

### Endpoint
/v0/drafts

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of drafts to return.
- **offset** (integer) - Optional - The number of drafts to skip before returning results.

### Request Example
```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/drafts")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

### Response

#### Success Response (200)

- **drafts** (array) - A list of draft objects.
   - **id** (string) - The unique identifier of the draft.
   - **subject** (string) - The subject line of the draft.
   - **createdAt** (string) - The timestamp when the draft was created.

#### Response Example

```json
{
  "drafts": [
    {
      "id": "draft_123",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z"
    }
  ]
}
```

```
--------------------------------

### List Inbox Messages using AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/list

This Python example demonstrates how to instantiate the AgentMail client and retrieve messages from an inbox. It depends on the 'agentmail' library and requires an API key.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.messages.list(
    inbox_id="inbox_id"
)
```

--------------------------------

### Create Pod via HTTP POST Request (Go)

Source: https://docs.agentmail.to/api-reference/pods/create

This Go code snippet demonstrates how to create a pod by making a direct HTTP POST request to the AgentMail API. It sets up the request with the necessary headers, including Authorization and Content-Type, and sends an empty JSON body. It prints the response status and body.

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods"

    payload := strings.NewReader("{}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Fetch Draft via HTTP Request (Ruby)

Source: https://docs.agentmail.to/api-reference/drafts/get

Demonstrates how to fetch a draft by making an HTTP GET request to the AgentMail API using Ruby's built-in `net/http` library. No external SDK is required for this approach.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/drafts/draft_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Create Domain using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/domains/create

Demonstrates how to create a new domain using the AgentMail TypeScript SDK. Requires the 'agentmail' package. Initializes the client with an API key and calls the domains.create method.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.domains.create({
        domain: "domain",
        feedbackEnabled: true,
    });
}
main();
```

--------------------------------

### Simulating GitHub Star Detection

Source: https://docs.agentmail.to/webhook-agent

This function simulates the detection of a new GitHub star for demonstration purposes. It runs in a background thread and triggers an agent outreach workflow. In a real application, this would be replaced with actual GitHub API calls.

```python
def poll_github_stargazers():
    # Simulate finding a new star every 13 seconds
    while True:
        time.sleep(13)
        # Construct prompt and call agent for outreach
        # ... (actual API call simulation logic here)
```

--------------------------------

### Create API Key via HTTP Request (Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/api-keys/create

Examples demonstrating how to create an API key by making direct HTTP POST requests to the AgentMail API. These snippets cover different languages and their respective HTTP client libraries. Remember to replace '<api_key>' with your actual API key.

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/api-keys"


payload := strings.NewReader("{\n  \"name\": \"name\"\n}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/api-keys")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{\n  \"name\": \"name\"\n}"

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.post("https://api.agentmail.to/v0/api-keys")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .body("{\n  \"name\": \"name\"\n}")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/api-keys', [
  'body' => '{
  "name": "name"
}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/api-keys");
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer <api_key>");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{\n  \"name\": \"name\"\n}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = ["name": "name"] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/api-keys")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### List Inboxes via HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/pods/inboxes/list

Provides a Go example for listing inboxes by making a direct HTTP GET request to the AgentMail API. It includes setting the Authorization header and reading the response body. Requires an API key and pod ID.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/inboxes"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### List Drafts - PHP

Source: https://docs.agentmail.to/api-reference/drafts/list

Example of how to list drafts using Guzzle HTTP client in PHP.

```APIDOC
## GET /v0/drafts

### Description
Retrieves a list of all drafts.

### Method
GET

### Endpoint
/v0/drafts

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of drafts to return.
- **offset** (integer) - Optional - The number of drafts to skip before returning results.

### Request Example
```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/drafts', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

### Response

#### Success Response (200)

- **drafts** (array) - A list of draft objects.
   - **id** (string) - The unique identifier of the draft.
   - **subject** (string) - The subject line of the draft.
   - **createdAt** (string) - The timestamp when the draft was created.

#### Response Example

```json
{
  "drafts": [
    {
      "id": "draft_123",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z"
    }
  ]
}
```

```
--------------------------------

### List Threads using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/threads/list

Demonstrates how to initialize the AgentMail client and list threads using the TypeScript SDK. Requires the 'agentmail' package.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.threads.list({});
}
main();
```

--------------------------------

### HTTP GET Request for AgentMail Drafts

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/get

Demonstrates making a direct HTTP GET request to the AgentMail API to retrieve draft information. This approach is useful when not using the official SDK or for understanding the underlying API interaction. It requires constructing the URL, setting the Authorization header with an API key, and handling the response.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Create Pod using AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/pods/create

Shows how to create a pod using the AgentMail Python library. This involves initializing the AgentMail client with your API key and then calling the create method for pods. The library handles the underlying HTTP requests.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.create()
```

--------------------------------

### Create Draft with AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/create

Example of creating a draft using the AgentMail TypeScript SDK. Requires the 'agentmail' package and an API key for authentication. It sends a POST request to the drafts endpoint.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.drafts.create("inbox_id", {});
}
main();
```

--------------------------------

### Retrieve Draft Attachment via HTTP Request (Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/drafts/get-attachment

Provides examples of how to retrieve an attachment from a draft using direct HTTP requests. This method requires constructing the request with the correct URL, HTTP method (GET), and authorization header. It's suitable when the SDK is not available or for lower-level control. Input includes the API key, draft ID, and attachment ID.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/drafts/draft_id/attachments/attachment_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/drafts/draft_id/attachments/attachment_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/drafts/draft_id/attachments/attachment_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/drafts/draft_id/attachments/attachment_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/drafts/draft_id/attachments/attachment_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/drafts/draft_id/attachments/attachment_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Install Dependencies (Bash)

Source: https://docs.agentmail.to/documentation/examples/smart-labeling-agent

Installs the required Python packages for the AgentMail email labeling agent using pip and a requirements.txt file. Ensures all necessary libraries like Flask, ngrok, and OpenAI are available.

```bash
pip install -r requirements.txt
```

--------------------------------

### Retrieve Attachment using AgentMail SDK (TypeScript, Python)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get-attachment

Examples show how to fetch an attachment from a specific thread within an inbox using the AgentMail SDK. Requires an API key and the IDs for the inbox, thread, and attachment.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.threads.getAttachment("inbox_id", "thread_id", "attachment_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.threads.get_attachment(
    inbox_id="inbox_id",
    thread_id="thread_id",
    attachment_id="attachment_id"
)
```

--------------------------------

### List Inboxes via HTTP Request (C#)

Source: https://docs.agentmail.to/api-reference/pods/inboxes/list

A C# example using the RestSharp library to perform an HTTP GET request for listing inboxes. It shows how to add the Authorization header and execute the request. Requires an API key and pod ID.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id/inboxes");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### Install Talon Library

Source: https://docs.agentmail.to/talon-reply-extraction

Install the Talon library using pip. A workaround for the cchardet dependency is required for Python 3.11+.

```bash
pip install talon
```

--------------------------------

### GET /pods

Source: https://docs.agentmail.to/changelog

Lists all pods within your organization.

```APIDOC
## GET /pods

### Description
Lists all pods in your organization.

### Method
GET

### Endpoint
/pods

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
(Details not provided in the source text)

#### Response Example
```json
{
  "example": "response body"
}
```

```
--------------------------------

### List Pod Domains via HTTP Request (Java)

Source: https://docs.agentmail.to/api-reference/pods/domains/list

An example in Java showing how to fetch pod domains using an HTTP GET request. This snippet utilizes the Unirest library to simplify HTTP client operations, including setting the 'Authorization' header.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id/domains")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Create Domain in Pod using HTTP Request (PHP)

Source: https://docs.agentmail.to/api-reference/pods/domains/create

This PHP example demonstrates creating a domain in a pod using the Guzzle HTTP client. It sends a POST request to the AgentMail API, including the necessary authorization and content type headers, and the domain details in the request body.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/pods/pod_id/domains', [
  'body' => '{
  "domain": "domain",
  "feedback_enabled": true
}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

--------------------------------

### List Drafts - Ruby

Source: https://docs.agentmail.to/api-reference/drafts/list

Example of how to list drafts using a direct HTTP request in Ruby.

```APIDOC
## GET /v0/drafts

### Description
Retrieves a list of all drafts.

### Method
GET

### Endpoint
/v0/drafts

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of drafts to return.
- **offset** (integer) - Optional - The number of drafts to skip before returning results.

### Request Example
```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/drafts")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

### Response

#### Success Response (200)

- **drafts** (array) - A list of draft objects.
   - **id** (string) - The unique identifier of the draft.
   - **subject** (string) - The subject line of the draft.
   - **createdAt** (string) - The timestamp when the draft was created.

#### Response Example

```json
{
  "drafts": [
    {
      "id": "draft_123",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z"
    }
  ]
}
```

```
--------------------------------

### Create Domain via HTTP POST (PHP)

Source: https://docs.agentmail.to/api-reference/domains/create

Shows a PHP example of creating a new domain by sending an HTTP POST request to the AgentMail API. This code uses the GuzzleHttp client to manage the request, including setting authorization headers and the JSON payload.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/domains', [
  'body' => '{
  "domain": "domain",
  "feedback_enabled": true
}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

--------------------------------

### Simulate GitHub Stargazer Events and Trigger Email Notifications (Python)

Source: https://docs.agentmail.to/webhook-agent

This Python code simulates new stars appearing on a GitHub repository and triggers an AI agent to send a personalized HTML email. It uses a polling loop with a delay and global variables to track simulated stars. The agent is instructed to first search the web for relevant information and then compose an HTML email without direct links, including a specific call to action.

```python
import time

# Assume Agent, AgentMailToolkit, WebSearchTool, and other necessary imports are defined elsewhere

# --- Configuration (Replace with actual values or load from environment)
actual_demo_target_email = "fallback.email@example.com"
actual_target_github_repo = "example/repo"
inbox = "default_inbox"

# --- Agent Initialization ---
# instructions = "Your agent instructions here"
# client = "Your client object here"
# agent = Agent(
#     name="GitHub Agent",
#     instructions=instructions,
#     tools=AgentMailToolkit(client).get_tools() + [WebSearchTool()],
# )

# messages = []

# --- GitHub Polling Logic ---
simulated_stargazer_count = 0
MAX_SIMULATED_STARS = 1 # single star even
stars_found_so_far = 0

def poll_github_stargazers():
    global simulated_stargazer_count, stars_found_so_far
    print(f"GitHub polling thread started for top 20 repositories related to AI agents...")

    # Give the Flask app a moment to start up if run concurrently
    time.sleep(3)

    while stars_found_so_far < MAX_SIMULATED_STARS:
        time.sleep(13) # Poll every 30 seconds for the demo

        # Simulate a new star appearing
        new_star_detected = False
        # For demo, let's just add a star each time for the first few polls
        if stars_found_so_far < MAX_SIMULATED_STARS: # Check again inside loop
            simulated_stargazer_count += 1
            stars_found_so_far += 1
            new_star_detected = True
            print(f"[POLLER] New star! Total: {simulated_stargazer_count}")

        if new_star_detected and actual_target_github_repo != "example/repo" and actual_demo_target_email != "fallback.email@example.com":
            prompt_for_agent = f"""
            URGENT TASK: A new star has been detected for the repository '{actual_target_github_repo}' (simulated count: {simulated_stargazer_count}).
            Your goal is to use the 'send_message' tool to notify {actual_demo_target_email} with an HTML email that does not contain direct web links in its body and has a specific call to action.

            Thought: I need to perform two steps: first, gather information using WebSearchTool, and second, synthesize this information into an HTML email and send it using the send_message tool.

            Step 1: Gather Information.
            Use the WebSearchTool to find ONE fresh, compelling piece of information or talking point about '{actual_target_github_repo}' relevant to AI agent development.
            Your output for this step should be an action call to WebSearchTool. For example:
            Action: WebSearchTool("key features of {actual_target_github_repo} for AI agents")

            (After you receive the observation from WebSearchTool, you will proceed to Step 2 in your next turn)

            Step 2: Formulate and Send HTML Email.
            Based on the information from WebSearchTool, you MUST call the 'send_message' tool.
            The email should start by acknowledging the user's interest, e.g., \"<p>Hello! We noticed you recently showed interest in (or starred) our repository, <strong>{actual_target_github_repo}</strong>! We're excited to share some insights...</p>\"
            The email body should discuss the information you found but **MUST NOT include any raw URLs or direct hyperlinks from the web search results.** Synthesize the information.
            The email MUST end with a call to action like: \"<p>I'm an AI assistant for '{actual_target_github_repo}', and I'm here to help answer any questions you might have. Feel free to reply to this email with your thoughts or if there's anything specific you'd like to know!</p>\"

            The parameters for the 'send_message' tool call should be:
                - 'to': ['{actual_demo_target_email}']
                - 'inbox_id': '{inbox}'
                - 'subject': An engaging subject based on the web search findings (e.g., "Insights on {actual_target_github_repo} for Your AI Projects!").
                - 'html': An email body in HTML format, adhering to all the above content and formatting rules (mention star, no direct links, specific CTA).

            Your output for this step MUST be an action call to 'send_message' with the tool input formatted as a valid JSON string, ensuring you use the 'html' field for the body. For example:
            Action: send_message(```
            {{
              "inbox_id": "{inbox}",
              "to": ["{actual_demo_target_email}"],
              "subject": "Following Up on Your Interest in {actual_target_github_repo}!",
              "html": "<p>Hello! We noticed you recently showed interest in <strong>{actual_target_github_repo}</strong>!</p><p>We've been developing some exciting capabilities within it, particularly around [synthesized information from web search, e.g., its new modular design for agent development]. This allows for more flexible integration of AI components.</p><p>I'm an AI assistant for \'{actual_target_github_repo}\', and I'm here to help answer any questions you might have. Feel free to reply to this email with your thoughts or if there's anything specific you'd like to know!</p>"
            }}
            ```)
            """
            # In a real scenario, you would pass prompt_for_agent to the agent
            # agent.run(prompt_for_agent)
            print(f"[SIMULATOR] Agent would be prompted with:\n{prompt_for_agent}")

# Example of how to start the polling (in a real application, this would likely be in a separate thread)
# poll_github_stargazers()
```

--------------------------------

### List Inboxes via HTTP Request (Java)

Source: https://docs.agentmail.to/api-reference/pods/inboxes/list

An example in Java using the Unirest library to make an HTTP GET request to list inboxes. It includes setting the Authorization header and retrieving the response as a string. Requires an API key and pod ID.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id/inboxes")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### List Drafts - C#

Source: https://docs.agentmail.to/api-reference/drafts/list

Example of how to list drafts using RestSharp in C#.

```APIDOC
## GET /v0/drafts

### Description
Retrieves a list of all drafts.

### Method
GET

### Endpoint
/v0/drafts

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of drafts to return.
- **offset** (integer) - Optional - The number of drafts to skip before returning results.

### Request Example
```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/drafts");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

### Response

#### Success Response (200)

- **drafts** (array) - A list of draft objects.
   - **id** (string) - The unique identifier of the draft.
   - **subject** (string) - The subject line of the draft.
   - **createdAt** (string) - The timestamp when the draft was created.

#### Response Example

```json
{
  "drafts": [
    {
      "id": "draft_123",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z"
    }
  ]
}
```

```
--------------------------------

### List Pod Domains via HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/pods/domains/list

Provides a Go example for fetching a list of domains within a pod by making a direct HTTP GET request to the AgentMail API. This method requires manual construction of the request, including the Authorization header with your API key.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/domains"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### List Pod Domains via HTTP Request (C#)

Source: https://docs.agentmail.to/api-reference/pods/domains/list

A C# example using the RestSharp library to make an HTTP GET request to the AgentMail API for listing pod domains. It shows how to configure the RestClient, create a request, and add the necessary 'Authorization' header.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id/domains");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### List API Keys using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/api-keys/list

Demonstrates how to initialize the AgentMail client with an API key and list available API keys using the TypeScript SDK. Requires the 'agentmail' package.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.apiKeys.list({});
}
main();
```

--------------------------------

### Connect and Subscribe to Email Events via WebSockets (TypeScript)

Source: https://docs.agentmail.to/websockets/quickstart

Connects to AgentMail WebSockets, subscribes to a specific inbox, and logs received messages. Requires the 'agentmail' package. Handles 'subscribed' and 'message.received' event types.

```typescript
import { AgentMailClient } from "agentmail";

const client = new AgentMailClient();

async function main() {
  const socket = await client.websockets.connect();

  socket.on("message", async (event) => {
    if (event.type === "subscribed") {
      console.log("Subscribed to", event.inboxIds);
    } else if (
      event.type === "event" &&
      event.eventType === "message.received"
    ) {
      console.log(`Received message from: ${event.message.from}`);
    }
  });

  await socket.waitForOpen();

  socket.sendSubscribe({
    type: "subscribe",
    inboxIds: ["my-agent@agentmail.to"],
  });
}

main();
```

--------------------------------

### Run Main Function - Asyncio Event Loop (Python)

Source: https://docs.agentmail.to/sales-agent-websocket

Provides a simple entry point to run the asynchronous `main` function using `asyncio.run()`. It includes a try-except block to catch `KeyboardInterrupt` for a clean shutdown.

```python
def run():
      """Run the main function"""
      try:
          asyncio.run(main())
      except KeyboardInterrupt:
          print("\n✓ Shutdown complete")
```

--------------------------------

### List Drafts - TypeScript

Source: https://docs.agentmail.to/api-reference/drafts/list

Example of how to list drafts using the AgentMail TypeScript SDK.

```APIDOC
## GET /v0/drafts

### Description
Retrieves a list of all drafts.

### Method
GET

### Endpoint
/v0/drafts

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of drafts to return.
- **offset** (integer) - Optional - The number of drafts to skip before returning results.

### Request Example
```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.drafts.list({});
}
main();
```

### Response

#### Success Response (200)

- **drafts** (array) - A list of draft objects.
   - **id** (string) - The unique identifier of the draft.
   - **subject** (string) - The subject line of the draft.
   - **createdAt** (string) - The timestamp when the draft was created.

#### Response Example

```json
{
  "drafts": [
    {
      "id": "draft_123",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z"
    }
  ]
}
```

```
--------------------------------

### List Inbox Messages using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/list

This TypeScript example shows how to initialize the AgentMail client and list messages from a specific inbox. It requires the 'agentmail' package and an API key for authentication.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.messages.list("inbox_id", {});
}
main();
```

--------------------------------

### Example OpenAI Prompt for Email Analysis

Source: https://docs.agentmail.to/documentation/examples/smart-labeling-agent

This is an example prompt sent to the OpenAI API to classify an email. It clearly defines the subject, content, and the desired classification dimensions with their possible values, instructing the API to return only valid JSON.

```text
Analyze this email across 4 dimensions:

Subject: Product keeps crashing!
Content: Your software is terrible. Fix it ASAP!

Classify into:
1. sentiment: positive | neutral | negative
2. category: question | complaint | feature-request | bug-report | praise
3. priority: urgent | high | normal | low
4. department: sales | support | billing | technical

Return ONLY valid JSON...
```

--------------------------------

### HTTP GET Request for Thread Attachment

Source: https://docs.agentmail.to/api-reference/threads/get-attachment

Shows how to make a direct HTTP GET request to retrieve a thread attachment. This method requires manual construction of the request, including setting the Authorization header with a Bearer token. It's suitable when not using the official SDK.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/threads/thread_id/attachments/attachment_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/threads/thread_id/attachments/attachment_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/threads/thread_id/attachments/attachment_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/threads/thread_id/attachments/attachment_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/threads/thread_id/attachments/attachment_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/threads/thread_id/attachments/attachment_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Fetch Threads using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/threads/get

Demonstrates how to fetch thread data using the AgentMail SDK. Requires an API key for authentication. This example shows the basic structure for retrieving a single thread by its ID.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.threads.get("thread_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.threads.get(
    thread_id="thread_id"
)
```

--------------------------------

### Create Domain in Pod using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/pods/domains/create

This example shows how to create a new domain within a specified pod using the AgentMail TypeScript SDK. It requires an API key for authentication and takes the pod ID, domain name, and feedback enabled status as input.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.domains.create("pod_id", {
        domain: "domain",
        feedbackEnabled: true,
    });
}
main();
```

--------------------------------

### Official AgentMail Skill Installation

Source: https://docs.agentmail.to/integrations/openclaw

Instructions for installing the official AgentMail skill for Openclaw using the CLI or ClawHub.

```APIDOC
## Official AgentMail Skill Installation

### Description
Install the official AgentMail skill for Openclaw to enable email functionality for your agent.

### Installation Methods

**Using Openclaw CLI:**
```bash
openclaw skills install agentmail-to/agentmail-skills/agentmail
```

**Using ClawHub:**

```bash
npx clawhub@latest install agentmail
```

### Configuration

Add your AgentMail API key to the skill configuration in `~/.openclaw/openclaw.json`:

```json
{
  "skills": {
    "entries": {
      "agentmail": {
        "enabled": true,
        "env": {
          "AGENTMAIL_API_KEY": "your-api-key-here"
        }
      }
    }
  }
}
```

Get your API key from the [AgentMail Console](https://console.agentmail.to).

### Verification

Check that the skill is loaded:

```bash
openclaw skills list --eligible
```

You should see `agentmail` in the list of available skills.

```
--------------------------------

### GET /metrics

Source: https://docs.agentmail.to/changelog

Retrieves comprehensive email delivery and performance metrics across all your inboxes. This endpoint is useful for getting a high-level overview of your campaign's success.

```APIDOC
## GET /metrics

### Description
Get comprehensive metrics across all your inboxes.

### Method
GET

### Endpoint
/metrics

### Parameters
#### Query Parameters
None

#### Request Body
None

### Response
#### Success Response (200)
- **metrics** (object) - An object containing various delivery and error metrics.
  - **sent** (integer) - The total number of emails sent.
  - **delivered** (integer) - The total number of emails successfully delivered.
  - **bounced** (integer) - The total number of emails that bounced.
  - **rejected** (integer) - The total number of emails rejected.
  - **complaints** (integer) - The total number of spam complaints.
  - **spam_reports** (integer) - The total number of spam reports.
  - **timestamps** (array) - An array of timestamps for the collected metrics.

#### Response Example
```json
{
  "metrics": {
    "sent": 10000,
    "delivered": 9500,
    "bounced": 300,
    "rejected": 200,
    "complaints": 50,
    "spam_reports": 20,
    "timestamps": [
      "2023-10-26T10:00:00Z",
      "2023-10-26T11:00:00Z"
    ]
  }
}
```

```
--------------------------------

### Create Domain via HTTP POST (Java)

Source: https://docs.agentmail.to/api-reference/domains/create

Provides a Java code example for creating a new domain using an HTTP POST request to the AgentMail API. This snippet utilizes the Unirest library for making HTTP requests, including setting headers and the JSON request body.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.post("https://api.agentmail.to/v0/domains")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .body("{\n  \"domain\": \"domain\",\n  \"feedback_enabled\": true\n}")
  .asString();
```

--------------------------------

### Install AgentMail Dependencies

Source: https://docs.agentmail.to/documentation/examples/auto-reply-agent

Command to install necessary Python packages for AgentMail, typically found in a 'requirements.txt' file. Includes instructions for activating a virtual environment on macOS/Linux and Windows.

```bash
pip install -r requirements.txt

source venv/bin/activate  # macOS/Linux
virtualenv\Scripts\activate     # Windows
```

--------------------------------

### Local Development with ngrok

Source: https://docs.agentmail.to/webhook-verification

Instructions for setting up a local webhook server and exposing it to the internet using ngrok for testing.

```APIDOC
## Local Development Setup

### Step 1: Save Your Webhook Server
Create a webhook server file (e.g., `webhook_server.py` or `webhook_server.ts`) with the provided code examples.

### Step 2: Install Dependencies and Run the Server

**Python:**
```bash
pip install flask python-dotenv svix
python webhook_server.py
```

**TypeScript:**

```bash
npm install express svix dotenv
npx ts-node webhook_server.ts
```

### Step 3: Start ngrok

In a new terminal window, run:

```bash
ngrok http 3000
```

Copy the `https://` forwarding URL provided by ngrok (e.g., `https://<your-ngrok-subdomain>.ngrok.app`).

### Step 4: Add the URL to AgentMail Console

1. Navigate to **Webhooks** in the AgentMail Console.
2. Click **Create Webhook**.
3. Paste your ngrok URL with the `/webhooks` path (e.g., `https://<your-ngrok-subdomain>.ngrok.app/webhooks`).
4. Select the events you want to receive.
5. Save the webhook.
6. Copy the signing secret and add it to your `.env` file as `AGENTMAIL_WEBHOOK_SECRET`.
   
   ```
   
   ```

--------------------------------

### HTTP GET Request to Retrieve Attachment

Source: https://docs.agentmail.to/api-reference/pods/threads/get-attachment

Illustrates how to retrieve an attachment by making a direct HTTP GET request to the AgentMail API. This method requires manual construction of the request, including setting the Authorization header with an API key.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/threads/thread_id/attachments/attachment_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/threads/thread_id/attachments/attachment_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id/threads/thread_id/attachments/attachment_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/pods/pod_id/threads/thread_id/attachments/attachment_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id/threads/thread_id/attachments/attachment_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id/threads/thread_id/attachments/attachment_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Fetch Draft using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/drafts/get

Demonstrates how to initialize the AgentMail client and fetch a draft by its ID using the TypeScript SDK. Requires the 'agentmail' package.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.drafts.get("draft_id");
}
main();
```

--------------------------------

### Install AgentMail Skill (CLI)

Source: https://docs.agentmail.to/integrations/skills

Commands to install the AgentMail skill using the command-line interface for different AI assistants. This allows the AI to interact with AgentMail's email functionalities.

```bash
moltbot skills install agentmail-to/agentmail-skills/agentmail
```

```bash
clawdhub install agentmail
```

```bash
claude-code skills install agentmail-to/agentmail-skills/agentmail
```

```bash
cursor skills install agentmail-to/agentmail-skills/agentmail
```

--------------------------------

### Fetch Inbox Threads (Go)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Example of how to fetch threads from a specific inbox using a direct HTTP request in Go.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}

### Description
Retrieves a specific thread from a given inbox.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/threads/{thread_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox.
- **thread_id** (string) - Required - The ID of the thread to retrieve.

#### Headers
- **Authorization** (string) - Required - Bearer token for authentication. Example: `Bearer <api_key>`

### Request Example
```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

### Response

#### Success Response (200)

- **(object)** - Details of the requested thread.

#### Response Example

```json
{
  "id": "thread_id",
  "inbox_id": "inbox_id",
  "subject": "Example Subject",
  "snippet": "This is a snippet of the thread content.",
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### Python Flask Webhook Receiver

Source: https://docs.agentmail.to/webhook-setup

A Python Flask application that sets up a web server to receive and process webhook events from AgentMail. It includes a status page and an endpoint for handling incoming POST requests containing event data. Dependencies include Flask. It outputs received event details to the console.

```python
from flask import Flask, request, Response

app = Flask(__name__)

@app.route('/')
def home():
    """Status page to verify server is running"""
    return """
    <html>
    <body style="font-family: sans-serif; max-width: 800px; margin: 50px auto; padding: 20px;">
        <h1>AgentMail Webhook Receiver</h1>
        <div style="background: #4CAF50; color: white; padding: 10px 20px;
                    border-radius: 4px; display: inline-block; margin: 20px 0;">
            Server is running
        </div>
        <div style="background: #e3f2fd; padding: 15px; border-radius: 4px;
                    border-left: 4px solid #2196F3;">
            <h3>Webhook Endpoint Ready</h3>
            <p>Your webhook endpoint is listening at: <code>POST /webhooks</code></p>
        </div>
        <h3>How to use:</h3>
        <ul>
            <li>Start ngrok: <code>ngrok http 3000</code></li>
            <li>Register your webhook with AgentMail using the ngrok URL</li>
            <li>Send a test email to your AgentMail inbox</li>
            <li>Watch the console for incoming webhook events</li>
        </ul>
    </body>
    </html>
    """

@app.route('/webhooks', methods=['POST'])
def receive_webhook():
    """Receives webhook events from AgentMail"""
    payload = request.json

    event_type = payload.get('event_type')
    message = payload.get('message', {})

    print(f"\nWebhook received: {event_type}")
    print(f"From: {message.get('from_')}")
    print(f"Subject: {message.get('subject')}\n")

    return Response(status=200)

if __name__ == '__main__':
    print("Starting webhook receiver on http://127.0.0.1:3000")
    app.run(port=3000)
```

--------------------------------

### List Pods via HTTP GET Request (Go)

Source: https://docs.agentmail.to/api-reference/pods/list

Demonstrates how to list pods by making a direct HTTP GET request to the AgentMail API endpoint using Go's standard library. This method requires manual construction of the request, including headers for authorization.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Verify AgentMail Skill Installation in Openclaw

Source: https://docs.agentmail.to/integrations/openclaw

Lists the eligible skills loaded by Openclaw to verify that the AgentMail skill has been successfully installed and recognized.

```bash
openclaw skills list --eligible
```

--------------------------------

### Create Draft with AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/create

Demonstrates creating a draft using the AgentMail Python SDK. It requires the 'agentmail' library and an API key. The code sends a POST request to create a new draft.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.drafts.create(
    inbox_id="inbox_id"
)
```

--------------------------------

### Retrieve Message Attachment using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

Demonstrates how to retrieve an attachment from a specific message within an inbox using the AgentMail SDK. Requires an API key for authentication and specifies inbox, message, and attachment IDs as parameters. The TypeScript example initializes the client and calls the getAttachment method.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.messages.getAttachment("inbox_id", "message_id", "attachment_id");
}
main();
```

--------------------------------

### List Metrics API Endpoint (OpenAPI)

Source: https://docs.agentmail.to/api-reference/metrics/list

This snippet details the OpenAPI 3.1.0 specification for the 'List Metrics' GET endpoint. It outlines the required and optional query parameters such as event types, start and end timestamps, and the necessary Bearer authentication header. The response schema includes successful (200) and error (404) structures.

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/metrics:
    get:
      operationId: list
      summary: List Metrics
      tags:
        - subpackage_metrics
      parameters:
        - name: event_types
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/type_metrics:MetricEventTypes'
        - name: start_timestamp
          in: query
          required: true
          schema:
            $ref: '#/components/schemas/type_metrics:MetricStartTimestamp'
        - name: end_timestamp
          in: query
          required: true
          schema:
            $ref: '#/components/schemas/type_metrics:MetricEndTimestamp'
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_metrics:ListMetricsResponse'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_metrics:MetricEventType:
      type: string
      enum:
        - message.sent
        - message.delivered
        - message.bounced
        - message.delayed
        - message.rejected
        - message.complained
        - message.received
      description: Type of metric event.
      title: MetricEventType
    type_metrics:MetricEventTypes:
      type: array
      items:
        $ref: '#/components/schemas/type_metrics:MetricEventType'
      description: List of metric event types to filter by.
      title: MetricEventTypes
    type_metrics:MetricStartTimestamp:
      type: string
      format: date-time
      description: Start timestamp for the metrics query range.
      title: MetricStartTimestamp
    type_metrics:MetricEndTimestamp:
      type: string
      format: date-time
      description: End timestamp for the metrics query range.
      title: MetricEndTimestamp
    type_metrics:MetricTimestamp:
      type: string
      format: date-time
      description: Timestamp when the metric event occurred.
      title: MetricTimestamp
    type_metrics:MessageMetrics:
      type: object
      properties:
        sent:
          type: array
          items:
            $ref: '#/components/schemas/type_metrics:MetricTimestamp'
          description: Timestamps when messages were sent.
        delivered:
          type: array
          items:
            $ref: '#/components/schemas/type_metrics:MetricTimestamp'
          description: Timestamps when messages were delivered.
        bounced:
          type: array
          items:
            $ref: '#/components/schemas/type_metrics:MetricTimestamp'
          description: Timestamps when messages bounced.
        delayed:
          type: array
          items:
            $ref: '#/components/schemas/type_metrics:MetricTimestamp'
          description: Timestamps when messages were delayed.
        rejected:
          type: array
          items:
            $ref: '#/components/schemas/type_metrics:MetricTimestamp'
          description: Timestamps when messages were rejected.
        complained:
          type: array
          items:
            $ref: '#/components/schemas/type_metrics:MetricTimestamp'
          description: Timestamps when messages received complaints.
        received:
          type: array
          items:
            $ref: '#/components/schemas/type_metrics:MetricTimestamp'
          description: Timestamps when messages were received.
      title: MessageMetrics
    type_metrics:ListMetricsResponse:
      type: object
      properties:
        message:
          $ref: '#/components/schemas/type_metrics:MessageMetrics'
          description: Message metrics grouped by event type.
      title: ListMetricsResponse
    type_:ErrorName:
      type: string
      description: Name of error.
      title: ErrorName
    type_:ErrorMessage:
      type: string
      description: Error message.
      title: ErrorMessage
    type_:ErrorResponse:
      type: object
      properties:
        name:
          $ref: '#/components/schemas/type_:ErrorName'
        message:
          $ref: '#/components/schemas/type_:ErrorMessage'
      required:
        - name
        - message
      title: ErrorResponse
  securitySchemes:
    Bearer:
      type: http
      scheme: bearer
```

--------------------------------

### Install Official AgentMail Skill for Openclaw

Source: https://docs.agentmail.to/integrations/openclaw

Installs the official AgentMail skill for Openclaw using the command-line interface. This is the recommended method for integrating email capabilities.

```bash
openclaw skills install agentmail-to/agentmail-skills/agentmail
```

```bash
npx clawhub@latest install agentmail
```

--------------------------------

### Create Draft via HTTP Request (PHP)

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/create

A PHP example using GuzzleHttp to create a draft via an HTTP POST request to the AgentMail API. It configures the request with the Authorization header and JSON content type.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/inboxes/inbox_id/drafts', [
  'body' => '{}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

--------------------------------

### List API Keys using AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/api-keys/list

Shows how to instantiate the AgentMail client with an API key and retrieve a list of API keys using the Python SDK. Requires the 'agentmail' package.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.api_keys.list()
```

--------------------------------

### List Inbox Drafts - Go

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/list

Example of how to list drafts for a specific inbox using a direct HTTP request in Go.

```APIDOC
## GET /v0/inboxes/{inbox_id}/drafts

### Description
Retrieves a list of drafts for a specified inbox.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/drafts

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox to retrieve drafts from.

#### Query Parameters
None

### Request Example
```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/drafts"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

### Response

#### Success Response (200)

- **(object)** - A list of draft objects.

#### Response Example

```json
{
  "example": "[Draft objects]"
}
```

```
--------------------------------

### List Threads via HTTP GET Request (Swift)

Source: https://docs.agentmail.to/api-reference/threads/list

This Swift code demonstrates fetching threads by constructing an NSMutableURLRequest and sending it via URLSession. It includes setting the Authorization header.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/threads")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Fetch Inbox Threads (Java)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Example of how to fetch threads from a specific inbox using the Unirest library in Java.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}

### Description
Retrieves a specific thread from a given inbox.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/threads/{thread_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox.
- **thread_id** (string) - Required - The ID of the thread to retrieve.

#### Headers
- **Authorization** (string) - Required - Bearer token for authentication. Example: `Bearer <api_key>`

### Request Example
```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

### Response

#### Success Response (200)

- **(object)** - Details of the requested thread.

#### Response Example

```json
{
  "id": "thread_id",
  "inbox_id": "inbox_id",
  "subject": "Example Subject",
  "snippet": "This is a snippet of the thread content.",
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### Webhook Processing Logic

Source: https://docs.agentmail.to/webhook-agent

Handles incoming webhook requests by processing the payload in a separate thread. It parses the email content, constructs a prompt for the agent, runs the agent, and sends the agent's HTML output as a reply. Returning a 200 OK status immediately is a best practice.

```python
import threading

def receive_webhook(request):
    # Start processing in a new thread to return 200 OK quickly
    thread = threading.Thread(target=process_webhook, args=(request.json,))
    thread.start()
    return "", 200

def process_webhook(payload):
    # Parse JSON payload
    email_content = payload.get('content')
    # Construct prompt
    prompt = f"New email received: {email_content}"
    # Run agent
    agent_response = agent.run(prompt)
    # Reply to the email
    client.messages.reply(message_id=payload.get('message_id'), html_content=agent_response)
```

--------------------------------

### Example AI Response for Email Classification

Source: https://docs.agentmail.to/documentation/examples/smart-labeling-agent

This is an example JSON response from the OpenAI API after analyzing an email. It provides the classification for sentiment, category, priority, and department based on the email's content.

```json
{
  "sentiment": "negative",
  "category": "complaint",
  "priority": "urgent",
  "department": "support"
}
```

--------------------------------

### Create API Key using AgentMail SDK (TypeScript, Python)

Source: https://docs.agentmail.to/api-reference/api-keys/create

Examples of creating an API key using the AgentMail SDK. These snippets demonstrate initializing the client and making the API call to create a new API key. Ensure you replace 'YOUR_TOKEN_HERE' with your actual API key.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.apiKeys.create({
        name: "name",
    });
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.api_keys.create(
    name="name"
)
```

--------------------------------

### List Webhooks using AgentMail SDK (TypeScript, Python)

Source: https://docs.agentmail.to/api-reference/webhooks/list

Examples of listing webhooks using the official AgentMail SDK. Requires the agentmail package and an API key for authentication. These snippets demonstrate basic client initialization and the webhook listing function.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.webhooks.list({});
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.webhooks.list()
```

--------------------------------

### OpenAPI Specification for Get List Entry

Source: https://docs.agentmail.to/api-reference/lists/get

The OpenAPI 3.1.0 specification for the 'Get List Entry' operation. This defines the request parameters (path and header), response schemas for success (200) and error (404), and the structure of list entry objects.

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/lists/{direction}/{type}/{entry}:
    get:
      operationId: get
      summary: Get List Entry
      tags:
        - subpackage_lists
      parameters:
        - name: direction
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_lists:Direction'
        - name: type
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_lists:ListType'
        - name: entry
          in: path
          description: Email address or domain.
          required: true
          schema:
            type: string
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_lists:ListEntry'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_lists:Direction:
      type: string
      enum:
        - send
        - receive
      description: Direction of list entry.
      title: Direction
    type_lists:ListType:
      type: string
      enum:
        - allow
        - block
      description: Type of list entry.
      title: ListType
    type_:OrganizationId:
      type: string
      description: ID of organization.
      title: OrganizationId
    type_lists:EntryType:
      type: string
      enum:
        - email
        - domain
      description: Whether the entry is an email address or domain.
      title: EntryType
    type_lists:ListEntry:
      type: object
      properties:
        entry:
          type: string
          description: Email address or domain of list entry.
        organization_id:
          $ref: '#/components/schemas/type_:OrganizationId'
        reason:
          type: string
          description: Reason for adding the entry.
        direction:
          $ref: '#/components/schemas/type_lists:Direction'
        list_type:
          $ref: '#/components/schemas/type_lists:ListType'
        entry_type:
          $ref: '#/components/schemas/type_lists:EntryType'
        created_at:
          type: string
          format: date-time
          description: Time at which entry was created.
      required:
        - entry
        - organization_id
        - direction
        - list_type
        - entry_type
        - created_at
      title: ListEntry
    type_:ErrorName:
      type: string
      description: Name of error.
      title: ErrorName
    type_:ErrorMessage:
      type: string
      description: Error message.
      title: ErrorMessage
    type_:ErrorResponse:
      type: object
      properties:
        name:
          $ref: '#/components/schemas/type_:ErrorName'
        message:
          $ref: '#/components/schemas/type_:ErrorMessage'
      required:
        - name
        - message
      title: ErrorResponse
  securitySchemes:
    Bearer:
      type: http
      scheme: bearer
```

--------------------------------

### GET /metrics

Source: https://docs.agentmail.to/changelog/2025/8/13

Retrieves comprehensive metrics across all inboxes.

```APIDOC
## GET /metrics

### Description
Retrieves comprehensive metrics across all your inboxes. This endpoint provides an overview of email deliverability and agent performance data aggregated from all sources.

### Method
GET

### Endpoint
/metrics

### Parameters
#### Query Parameters
- **start_time** (integer) - Optional - The start of the time range for the metrics in Unix epoch time.
- **end_time** (integer) - Optional - The end of the time range for the metrics in Unix epoch time.

### Request Example
```json
{
  "example": "GET /metrics?start_time=1678886400&end_time=1678972800"
}
```

### Response

#### Success Response (200)

- **sent** (integer) - The total number of emails sent.
- **delivered** (integer) - The total number of emails successfully delivered.
- **bounced** (integer) - The total number of emails that bounced.
- **rejected** (integer) - The total number of emails that were rejected.
- **complaints** (integer) - The total number of spam complaints received.
- **spam_reports** (integer) - The total number of spam reports received.

#### Response Example

```json
{
  "example": {
    "sent": 10000,
    "delivered": 9800,
    "bounced": 150,
    "rejected": 50,
    "complaints": 20,
    "spam_reports": 10
  }
}
```

```
--------------------------------

### List Pod Threads via HTTP (Ruby)

Source: https://docs.agentmail.to/api-reference/pods/threads/list

A Ruby script demonstrating how to list threads in a pod by making an HTTP GET request to the AgentMail API. It sets up the URL, HTTP client, and includes the 'Authorization' header with a Bearer token.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/threads")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Poll GitHub Stargazers and Trigger Agent (Python)

Source: https://docs.agentmail.to/webhook-agent

This function polls GitHub for new stargazers on a specified repository. If a new star is detected and necessary configuration (TARGET_GITHUB_REPO, DEMO_TARGET_EMAIL) is present, it triggers an agent to send a proactive email. It includes error handling and logging for the agent's execution. If configuration is missing, it logs a warning and skips the agent trigger.

```python
def poll_github_stargazers():
    global new_star_detected
    # ... (rest of the polling logic)
    elif new_star_detected:
        print("[POLLER] Simulated new star, but TARGET_GITHUB_REPO or DEMO_TARGET_EMAIL is not properly set. Skipping agent trigger.")

# ... (within the main execution block)
    polling_thread = Thread(target=poll_github_stargazers)
    polling_thread.daemon = True # So it exits when the main thread exits
    polling_thread.start()
```

--------------------------------

### Create Pod via HTTP POST Request (Java)

Source: https://docs.agentmail.to/api-reference/pods/create

This Java code snippet uses the Unirest library to make an HTTP POST request to create a pod. It sets the endpoint URL, Authorization and Content-Type headers, and provides an empty JSON payload. The response is captured as a String.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.post("https://api.agentmail.to/v0/pods")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .body("{}")
  .asString();
```

--------------------------------

### Forward Message via HTTP API (Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/forward

This Swift example demonstrates forwarding a message using URLSession to make an HTTP POST request to the AgentMail API. It sets up the request headers and body for the operation.

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/forward")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Fetch Inbox Threads (Python)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Example of how to fetch threads from a specific inbox using the AgentMail Python SDK.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}

### Description
Retrieves a specific thread from a given inbox.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/threads/{thread_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox.
- **thread_id** (string) - Required - The ID of the thread to retrieve.

### Request Example
```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.threads.get(
    inbox_id="inbox_id",
    thread_id="thread_id"
)
```

### Response

#### Success Response (200)

- **(object)** - Details of the requested thread.

#### Response Example

```json
{
  "id": "thread_id",
  "inbox_id": "inbox_id",
  "subject": "Example Subject",
  "snippet": "This is a snippet of the thread content.",
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### Get Last Message ID from Thread (TypeScript)

Source: https://docs.agentmail.to/sending-receiving-email

This TypeScript snippet fetches detailed thread information to access its associated messages. It determines the last message in the thread's message array and extracts its unique identifier. This message ID is essential for directing the agent's reply accurately.

```typescript
// Get the full thread object to access its messages
const threadDetails = await client.threads.get('thread_id');

// The last message in the array is the one we want to reply to
const lastMessage = threadDetails.messages[threadDetails.messages.length - 1];
const messageIdToReplyTo = lastMessage.message_id;
```

--------------------------------

### GET /v0/domains/{domain_id}

Source: https://docs.agentmail.to/api-reference/domains/get

Retrieves the details of a specific domain, including its verification status and required DNS records.

```APIDOC
## GET /v0/domains/{domain_id}

### Description
Retrieves the details of a specific domain, including its verification status and required DNS records.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/domains/{domain_id}

### Parameters
#### Path Parameters
- **domain_id** (string) - Required - The name of the domain (e.g., "your-domain.com").

#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Response
#### Success Response (200)
- **pod_id** (string) - ID of the pod.
- **domain_id** (string) - The name of the domain.
- **status** (string) - The verification status of the domain (e.g., NOT_STARTED, PENDING, VERIFIED).
- **feedback_enabled** (boolean) - Indicates if bounce and complaint notifications are enabled.
- **records** (array) - A list of DNS records required to verify the domain.
  - **type** (string) - The type of the DNS record (e.g., TXT, CNAME, MX).
  - **name** (string) - The name or host of the record.
  - **value** (string) - The value of the record.
  - **status** (string) - The verification status of this specific record (e.g., MISSING, INVALID, VALID).
  - **priority** (integer) - The priority of the MX record (if applicable).
- **client_id** (string) - Client ID of the domain.
- **updated_at** (string) - Time at which the domain was last updated (ISO 8601 format).
- **created_at** (string) - Time at which the domain was created (ISO 8601 format).

#### Error Response (404)
- **name** (string) - Name of the error.
- **message** (string) - Error message.

### Request Example
(No request body for GET requests)

### Response Example (200 OK)
```json
{
  "pod_id": "pod_abc123",
  "domain_id": "example.com",
  "status": "VERIFIED",
  "feedback_enabled": true,
  "records": [
    {
      "type": "TXT",
      "name": "_agentmail.example.com",
      "value": "agentmail-verification-code",
      "status": "VALID",
      "priority": null
    },
    {
      "type": "MX",
      "name": "example.com",
      "value": "mx.agentmail.to",
      "status": "VALID",
      "priority": 10
    }
  ],
  "client_id": "client_xyz789",
  "updated_at": "2023-10-27T10:00:00Z",
  "created_at": "2023-10-26T09:00:00Z"
}
```

### Response Example (404 Not Found)

```json
{
  "name": "DomainNotFound",
  "message": "The specified domain was not found."
}
```

```
--------------------------------

### Fetch Inbox Threads using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Demonstrates how to retrieve threads from a specific inbox using the AgentMail SDK. Requires an API key for authentication and specifies the inbox and thread IDs as parameters. The examples show client initialization and the method call to fetch thread data.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.threads.get("inbox_id", "thread_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.threads.get(
    inbox_id="inbox_id",
    thread_id="thread_id"
)
```

--------------------------------

### Get Last Message ID from Thread (Python)

Source: https://docs.agentmail.to/sending-receiving-email

This Python code retrieves the full details of a specific thread to access its messages. It then identifies the most recent message within that thread by accessing the last element in the messages list and extracts its ID. This message ID is necessary for replying to the correct conversation.

```python
# Get the full thread object to access its messages
thread_details = client.threads.get(thread_to_reply_to.thread_id)

# The last message in the list is the one we want to reply to
last_message = thread_details.messages[-1]
message_id_to_reply_to = last_message.message_id
```

--------------------------------

### Check Python Version (Bash)

Source: https://docs.agentmail.to/sales-agent-websocket

A command-line instruction to display the installed Python version. This is important for ensuring compatibility, as AgentMail requires Python 3.11 or newer for proper asyncio functionality.

```bash
python --version
```

--------------------------------

### Update Draft - Go

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/update

Example of updating a draft in an inbox using raw HTTP requests in Go.

```APIDOC
## PATCH /v0/inboxes/{inbox_id}/drafts/{draft_id}

### Description
Updates a specific draft within an inbox.

### Method
PATCH

### Endpoint
`/v0/inboxes/{inbox_id}/drafts/{draft_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox containing the draft.
- **draft_id** (string) - Required - The ID of the draft to update.

#### Request Body
- **{}** (object) - Optional - An empty JSON object, indicating no specific fields are being updated in this example. The actual payload would contain fields to modify.

### Request Example
```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id"

    payload := strings.NewReader("{}")

    req, _ := http.NewRequest("PATCH", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

### Response

#### Success Response (200)

- **(object)** - Details of the updated draft. The exact structure depends on the API response for a successful update.
  
  ```
  
  ```

--------------------------------

### Fetch Inbox Threads (Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Example of how to fetch threads from a specific inbox using URLSession in Swift.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}

### Description
Retrieves a specific thread from a given inbox.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/threads/{thread_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox.
- **thread_id** (string) - Required - The ID of the thread to retrieve.

#### Headers
- **Authorization** (string) - Required - Bearer token for authentication. Example: `Bearer <api_key>`

### Request Example
```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

### Response

#### Success Response (200)

- **(object)** - Details of the requested thread.

#### Response Example

```json
{
  "id": "thread_id",
  "inbox_id": "inbox_id",
  "subject": "Example Subject",
  "snippet": "This is a snippet of the thread content.",
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### Get Zone File using Agentmail API (Java)

Source: https://docs.agentmail.to/api-reference/domains/get-zone-file

Java code snippet using the Unirest library to make a GET request to the Agentmail API for retrieving a zone file. It shows how to set the Authorization header.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/domains/%3Adomain_id/zone-file")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Manually Clone AgentMail Skills Repository

Source: https://docs.agentmail.to/integrations/skills

Instructions for manually cloning the AgentMail skills repository to a local directory. This method is useful for custom installations or when direct CLI installation is not preferred.

```bash
git clone https://github.com/agentmail-to/agentmail-skills.git ~/.skills/agentmail
```

--------------------------------

### Download Zone File

Source: https://docs.agentmail.to/changelog

Downloads the DNS zone file for a specific domain, which can be used for easy DNS setup.

```APIDOC
## GET /domains/{domain_id}/zone-file

### Description
Downloads the DNS zone file for a specific domain, which can be used for easy DNS setup.

### Method
GET

### Endpoint
/domains/{domain_id}/zone-file

### Parameters
#### Path Parameters
- **domain_id** (string) - Required - The unique identifier of the domain.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **zone_file** (string) - The content of the DNS zone file.

#### Response Example
"@ IN SOA ns1.example.com. admin.example.com. (
        2023010101 ; serial
        3600       ; refresh
        1800       ; retry
        604800     ; expire
        600        ; minimum TTL
)

@ IN NS ns1.example.com.
@ IN NS ns2.example.com.

@ IN A 192.0.2.1

mail IN MX 10 mail.example.com.

mail IN A 192.0.2.2"
```

--------------------------------

### List Inbox Drafts - Python

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/list

Example of how to list drafts for a specific inbox using the AgentMail Python SDK.

```APIDOC
## GET /v0/inboxes/{inbox_id}/drafts

### Description
Retrieves a list of drafts for a specified inbox.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/drafts

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox to retrieve drafts from.

#### Query Parameters
None

### Request Example
```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.drafts.list(
    inbox_id="inbox_id"
)
```

### Response

#### Success Response (200)

- **(object)** - A list of draft objects.

#### Response Example

```json
{
  "example": "[Draft objects]"
}
```

```
--------------------------------

### HTTP GET Request to Retrieve Draft Attachment

Source: https://docs.agentmail.to/api-reference/pods/drafts/get-attachment

Shows how to retrieve an attachment from a draft using a direct HTTP GET request to the AgentMail API. This method requires manual construction of the request, including headers for authentication.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/drafts/draft_id/attachments/attachment_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/drafts/draft_id/attachments/attachment_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id/drafts/draft_id/attachments/attachment_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/pods/pod_id/drafts/draft_id/attachments/attachment_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id/drafts/draft_id/attachments/attachment_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id/drafts/draft_id/attachments/attachment_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### List Inbox Drafts - Java

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/list

Example of how to list drafts for a specific inbox using the Unirest library in Java.

```APIDOC
## GET /v0/inboxes/{inbox_id}/drafts

### Description
Retrieves a list of drafts for a specified inbox.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/drafts

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox to retrieve drafts from.

#### Query Parameters
None

### Request Example
```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id/drafts")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

### Response

#### Success Response (200)

- **(object)** - A list of draft objects.

#### Response Example

```json
{
  "example": "[Draft objects]"
}
```

```
--------------------------------

### Forward Message via HTTP API (Ruby)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/forward

This Ruby example shows how to forward a message by sending an HTTP POST request to the AgentMail API. It configures the request with the appropriate URL, headers, and body.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/forward")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{}"

response = http.request(request)
puts response.read_body
```

--------------------------------

### Retrieve List Entry Allow - Ruby SDK

Source: https://docs.agentmail.to/api-reference/lists/get

Illustrates how to get list entry allowance using Ruby's Net::HTTP library. This code makes a GET request to the Agentmail.to API, setting the Authorization header and printing the response body. It handles HTTPS connections.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/lists/send/allow/entry")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### JavaScript: Install TalonJS Package

Source: https://docs.agentmail.to/talon-reply-extraction

A simple bash command to install the TalonJS library using npm, the Node Package Manager. This is the first step for integrating Talon's email parsing functionality into a TypeScript or JavaScript project.

```bash
npm install talonjs
```

--------------------------------

### Install AgentMail Python Packages

Source: https://docs.agentmail.to/integrate-livekit-agents

Installs the necessary Python packages for integrating AgentMail and its toolkit with LiveKit agents. These packages provide the core functionality for email operations and LiveKit agent interactions.

```shell
pip install agentmail agentmail-toolkit
```

--------------------------------

### List Pods via HTTP GET Request (Swift)

Source: https://docs.agentmail.to/api-reference/pods/list

This Swift code demonstrates how to list pods by making an HTTP GET request to the AgentMail API using URLSession. It includes setting up the request with the required Authorization header.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Python: Create and List Agentmail Pods and Inboxes

Source: https://docs.agentmail.to/changelog

This Python snippet demonstrates how to interact with the Agentmail API to create a 'pod' for a sales team, create an inbox within that pod, and then list all existing pods. It requires the 'agentmail' library and an API key.

```python
from agentmail import AgentMail

client = AgentMail(api_key="your-api-key")

# create a pod for your sales team
pod = client.pods.create(
    name="Sales Team",
    description="Shared resources for sales agents")


# create an inbox in the pod
inbox = client.pods.inboxes.create(
    pod_id=pod.pod_id,
    inbox_id="salesExample.com")


# list all pods
pods = client.pods.list()
for pod in pods.pods:
    print(f"Pod: {pod.name} ({len(pod.inbox_ids)} inboxes)")
```

--------------------------------

### TypeScript: Create, Get, and Verify Domain with Agentmail API

Source: https://docs.agentmail.to/changelog

This TypeScript snippet shows how to use the Agentmail API for domain management, including creation, fetching verification details, and initiating verification. It requires an API key and uses asynchronous operations.

```typescript
import { AgentMail } from "agentmail";

const client = new AgentMail({ api_key: "your-api-key" });

// create a domain
const domain = await client.domains.create({
  domain: "mail.example.com",
  feedbackEnabled: true,
});

// get verification records and status
const domainDetails = await client.domains.get(domain.domainId);
for (const record of domainDetails.records) {
  console.log(`$${record.type} $${record.name}: $${record.status}`);
}

// trigger verification after updating DNS
await client.domains.verify(domain.domainId);
```

--------------------------------

### Get Zone File using Agentmail API (C#)

Source: https://docs.agentmail.to/api-reference/domains/get-zone-file

C# code using the RestSharp library to make a GET request to the Agentmail API for a zone file. Includes setting the Authorization header.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/domains/%3Adomain_id/zone-file");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### Fetch Domain Information using HTTP Request

Source: https://docs.agentmail.to/api-reference/domains/get

Shows how to make a direct HTTP GET request to the AgentMail API to fetch domain information. Requires an API key for authentication. Parses the response body.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/domains/domain_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/domains/domain_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/domains/domain_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/domains/domain_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/domains/domain_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/domains/domain_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### List Pod Threads using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/pods/threads/list

Demonstrates how to list threads in a pod using the AgentMail TypeScript SDK. Requires an API key for authentication. Initializes the client and calls the threads.list method.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.threads.list("pod_id", {});
}
main();
```

--------------------------------

### Get Message Details via OpenAPI

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get

This snippet defines the GET endpoint for retrieving a specific message from an inbox. It requires inbox and message IDs as path parameters and Bearer authentication. The response includes the message details or an error if the message is not found.

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/inboxes/{inbox_id}/messages/{message_id}:
    get:
      operationId: get
      summary: Get Message
      tags:
        - subpackage_inboxes.subpackage_inboxes/messages
      parameters:
        - name: inbox_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_inboxes:InboxId'
        - name: message_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_messages:MessageId'
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_messages:Message'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_inboxes:InboxId:
      type: string
      description: ID of inbox.
      title: InboxId
    type_messages:MessageId:
      type: string
      description: ID of message.
      title: MessageId
    type_threads:ThreadId:
      type: string
      description: ID of thread.
      title: ThreadId
    type_messages:MessageLabels:
      type: array
      items:
        type: string
      description: Labels of message.
      title: MessageLabels
    type_messages:MessageTimestamp:
      type: string
      format: date-time
      description: Time at which message was sent or drafted.
      title: MessageTimestamp
    type_messages:MessageFrom:
      type: string
      description: >-
        Address of sender. In format `username@domain.com` or `Display Name
        <username@domain.com>`.
      title: MessageFrom
    type_messages:MessageTo:
      type: array
      items:
        type: string
      description: >-
        Addresses of recipients. In format `username@domain.com` or `Display
        Name <username@domain.com>`.
      title: MessageTo
    type_messages:MessageCc:
      type: array
      items:
        type: string
      description: >-
        Addresses of CC recipients. In format `username@domain.com` or `Display
        Name <username@domain.com>`.
      title: MessageCc
    type_messages:MessageBcc:
      type: array
      items:
        type: string
      description: >-
        Addresses of BCC recipients. In format `username@domain.com` or `Display
        Name <username@domain.com>`.
      title: MessageBcc
    type_messages:MessageSubject:
      type: string
      description: Subject of message.
      title: MessageSubject
    type_messages:MessagePreview:
      type: string
      description: Text preview of message.
      title: MessagePreview
    type_messages:MessageText:
      type: string
      description: Plain text body of message.
      title: MessageText
    type_messages:MessageHtml:
      type: string
      description: HTML body of message.
      title: MessageHtml
    type_attachments:AttachmentId:
      type: string
      description: ID of attachment.
      title: AttachmentId
    type_attachments:AttachmentFilename:
      type: string
      description: Filename of attachment.
      title: AttachmentFilename
    type_attachments:AttachmentSize:
      type: integer
      description: Size of attachment in bytes.
      title: AttachmentSize
    type_attachments:AttachmentContentType:
      type: string
      description: Content type of attachment.
      title: AttachmentContentType
    type_attachments:AttachmentContentDisposition:
      type: string
      enum:
        - inline
        - attachment
      description: Content disposition of attachment.
      title: AttachmentContentDisposition
    type_attachments:AttachmentContentId:
      type: string
      description: Content ID of attachment.
      title: AttachmentContentId
    type_attachments:Attachment:
      type: object
      properties:
        attachment_id:
          $ref: '#/components/schemas/type_attachments:AttachmentId'
        filename:
          $ref: '#/components/schemas/type_attachments:AttachmentFilename'
        size:
          $ref: '#/components/schemas/type_attachments:AttachmentSize'
        content_type:
          $ref: '#/components/schemas/type_attachments:AttachmentContentType'
        content_disposition:
          $ref: '#/components/schemas/type_attachments:AttachmentContentDisposition'
        content_id:
          $ref: '#/components/schemas/type_attachments:AttachmentContentId'
      required:
        - attachment_id
        - size
```

--------------------------------

### Create Domain via HTTP POST (Ruby)

Source: https://docs.agentmail.to/api-reference/domains/create

Demonstrates creating a new domain by sending an HTTP POST request to the AgentMail API using Ruby's Net::HTTP library. The code sets up the URL, headers, and JSON body for the request.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/domains")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{\n  \"domain\": \"domain\",\n  \"feedback_enabled\": true\n}"

response = http.request(request)
puts response.read_body
```

--------------------------------

### Update Draft - Java

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/update

Example of updating a draft in an inbox using the Unirest library in Java.

```APIDOC
## PATCH /v0/inboxes/{inbox_id}/drafts/{draft_id}

### Description
Updates a specific draft within an inbox.

### Method
PATCH

### Endpoint
`/v0/inboxes/{inbox_id}/drafts/{draft_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox containing the draft.
- **draft_id** (string) - Required - The ID of the draft to update.

#### Request Body
- **{}** (object) - Optional - An empty JSON object, indicating no specific fields are being updated in this example. The actual payload would contain fields to modify.

### Request Example
```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.patch("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .body("{}")
  .asString();
```

### Response

#### Success Response (200)

- **(object)** - Details of the updated draft. The exact structure depends on the API response for a successful update.
  
  ```
  
  ```

--------------------------------

### List Inbox Drafts - Ruby

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/list

Example of how to list drafts for a specific inbox using Ruby's Net::HTTP.

```APIDOC
## GET /v0/inboxes/{inbox_id}/drafts

### Description
Retrieves a list of drafts for a specified inbox.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/drafts

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox to retrieve drafts from.

#### Query Parameters
None

### Request Example
```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/drafts")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

### Response

#### Success Response (200)

- **(object)** - A list of draft objects.

#### Response Example

```json
{
  "example": "[Draft objects]"
}
```

```
--------------------------------

### List Pod Threads using AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/pods/threads/list

Shows how to list threads in a pod using the AgentMail Python SDK. Requires an API key for authentication. Initializes the client and calls the pods.threads.list method.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.threads.list(
    pod_id="pod_id"
)
```

--------------------------------

### List Inbox Drafts - Swift

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/list

Example of how to list drafts for a specific inbox using URLSession in Swift.

```APIDOC
## GET /v0/inboxes/{inbox_id}/drafts

### Description
Retrieves a list of drafts for a specified inbox.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/drafts

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox to retrieve drafts from.

#### Query Parameters
None

### Request Example
```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/drafts")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

### Response

#### Success Response (200)

- **(object)** - A list of draft objects.

#### Response Example

```json
{
  "example": "[Draft objects]"
}
```

```
--------------------------------

### Create Domain and Get DNS Records via cURL

Source: https://docs.agentmail.to/custom-domains

Use this cURL command to create a domain and retrieve its DNS records via the AgentMail API. Ensure you replace 'YOUR_API_KEY' with your actual API key and 'your-domain.com' with your desired domain.

```bash
curl -X POST https://api.agentmail.to/domains/your-domain.com \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

--------------------------------

### GET /v0/organizations

Source: https://docs.agentmail.to/api-reference/organizations/get

Retrieves the details of the current organization, including inbox and domain counts, limits, and billing information.

```APIDOC
## GET /v0/organizations

### Description
Retrieves the details of the current organization, including inbox and domain counts, limits, and billing information.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/organizations

### Parameters
#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Request Example
```json
{
  "example": "No request body for this endpoint."
}
```

### Response

#### Success Response (200)

- **organization_id** (string) - ID of the organization.
- **inbox_count** (integer) - Current number of inboxes.
- **domain_count** (integer) - Current number of domains.
- **inbox_limit** (integer) - Maximum number of inboxes allowed.
- **domain_limit** (integer) - Maximum number of domains allowed.
- **billing_id** (string) - Provider-agnostic billing customer ID.
- **billing_type** (string) - Billing provider type (e.g. "stripe").
- **billing_subscription_id** (string) - Active billing subscription ID.
- **authentication_id** (string) - Provider-agnostic authentication ID.
- **authentication_type** (string) - Authentication provider type.
- **updated_at** (string) - Time at which organization was last updated.
- **created_at** (string) - Time at which organization was created.

#### Response Example

```json
{
  "organization_id": "org_12345",
  "inbox_count": 5,
  "domain_count": 2,
  "inbox_limit": 10,
  "domain_limit": 5,
  "billing_id": "cus_abcde",
  "billing_type": "stripe",
  "billing_subscription_id": "sub_fghij",
  "authentication_id": "auth_klmno",
  "authentication_type": "google",
  "updated_at": "2023-10-27T10:00:00Z",
  "created_at": "2023-01-15T09:00:00Z"
}
```

```
--------------------------------

### Create Domain in Pod using HTTP Request (Java)

Source: https://docs.agentmail.to/api-reference/pods/domains/create

This Java code snippet shows how to create a domain within a pod by making an HTTP POST request using the Unirest library. It configures the request with the appropriate URL, headers, and JSON body.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.post("https://api.agentmail.to/v0/pods/pod_id/domains")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .body("{\n  \"domain\": \"domain\",\n  \"feedback_enabled\": true\n}")
  .asString();
```

--------------------------------

### Get Attachment API Endpoint

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

This snippet shows the GET request to retrieve a specific attachment from a message within an inbox. It requires the inbox ID, message ID, and attachment ID as path parameters, along with Bearer authentication.

```http
GET https://api.agentmail.to/v0/inboxes/{inbox_id}/messages/{message_id}/attachments/{attachment_id}
```

--------------------------------

### Webhook Server Implementation

Source: https://docs.agentmail.to/webhook-verification

Example implementations of a webhook server in Python and TypeScript to handle incoming AgentMail events.

```APIDOC
## POST /webhooks

### Description
This endpoint receives webhook events from AgentMail. It verifies the incoming payload using a shared secret and processes the event.

### Method
POST

### Endpoint
/webhooks

### Parameters
#### Request Body
- **payload** (bytes) - Required - The raw request body containing the event data.

### Headers
- **svix-id** (string) - Required - The ID of the event.
- **svix-timestamp** (string) - Required - The timestamp of the event.
- **svix-signature** (string) - Required - The signature of the event, used for verification.

### Request Example (Python)
```python
import os
from dotenv import load_dotenv
from flask import Flask, request
from svix.webhooks import Webhook, WebhookVerificationError

load_dotenv()

app = Flask(__name__)

secret = os.environ.get("AGENTMAIL_WEBHOOK_SECRET")

@app.route('/webhooks', methods=['POST'])
def webhook_handler():
    headers = request.headers
    payload = request.get_data()

    try:
        wh = Webhook(secret)
        msg = wh.verify(payload, headers)
        print(f"Received event: {msg}")
    except WebhookVerificationError as e:
        print(f"Verification failed: {e}")
        return ('', 400)

    # Do something with the message...

    return ('', 204)

if __name__ == '__main__':
    app.run(port=3000)
```

### Request Example (TypeScript)

```typescript
import "dotenv/config";
import express, { Request, Response } from "express";
import { Webhook } from "svix";

const app = express();
const port = 3000;

const secret = process.env.AGENTMAIL_WEBHOOK_SECRET;

if (!secret) {
  throw new Error("AGENTMAIL_WEBHOOK_SECRET environment variable is required");
}

app.post(
  "/webhooks",
  express.raw({ type: "application/json" }),
  (req: Request, res: Response) => {
    const payload = req.body;
    const headers = req.headers as Record<string, string>;

    try {
      const wh = new Webhook(secret);
      const msg = wh.verify(payload, headers);

      // Do something with the message...
      console.log("Webhook verified:", msg);

      res.status(204).send();
    } catch (err) {
      console.error("Webhook verification failed:", err);
      res.status(400).send();
    }
  }
);

app.listen(port, () => {
  console.log(`Webhook server listening on port ${port}`);
});
```

### Response

#### Success Response (204)

Indicates that the webhook was received and processed successfully.

#### Error Response (400)

Indicates that the webhook verification failed.

```
--------------------------------

### Get Domain Details via API (OpenAPI)

Source: https://docs.agentmail.to/api-reference/domains/get

This snippet shows the OpenAPI specification for the GET /v0/domains/{domain_id} endpoint. It defines the request parameters, including the domain ID and Authorization header, and the structure of the successful response (200) containing domain details, as well as the error response (404).

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/domains/{domain_id}:
    get:
      operationId: get
      summary: Get Domain
      tags:
        - subpackage_domains
      parameters:
        - name: domain_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_domains:DomainId'
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_domains:Domain'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_domains:DomainId:
      type: string
      description: The name of the domain. (e.g., " your-domain.com")
      title: DomainId
    type_pods:PodId:
      type: string
      description: ID of pod.
      title: PodId
    type_domains:VerificationStatus:
      type: string
      enum:
        - NOT_STARTED
        - PENDING
        - INVALID
        - FAILED
        - VERIFYING
        - VERIFIED
      title: VerificationStatus
    type_domains:FeedbackEnabled:
      type: boolean
      description: Bounce and complaint notifications are sent to your inboxes.
      title: FeedbackEnabled
    type_domains:RecordType:
      type: string
      enum:
        - TXT
        - CNAME
        - MX
      title: RecordType
    type_domains:RecordStatus:
      type: string
      enum:
        - MISSING
        - INVALID
        - VALID
      title: RecordStatus
    type_domains:VerificationRecord:
      type: object
      properties:
        type:
          $ref: '#/components/schemas/type_domains:RecordType'
          description: The type of the DNS record.
        name:
          type: string
          description: The name or host of the record.
        value:
          type: string
          description: The value of the record.
        status:
          $ref: '#/components/schemas/type_domains:RecordStatus'
          description: The verification status of this specific record.
        priority:
          type: integer
          description: The priority of the MX record.
      required:
        - type
        - name
        - value
        - status
      title: VerificationRecord
    type_domains:ClientId:
      type: string
      description: Client ID of domain.
      title: ClientId
    type_domains:Domain:
      type: object
      properties:
        pod_id:
          $ref: '#/components/schemas/type_pods:PodId'
        domain_id:
          $ref: '#/components/schemas/type_domains:DomainId'
        status:
          $ref: '#/components/schemas/type_domains:VerificationStatus'
          description: The verification status of the domain.
        feedback_enabled:
          $ref: '#/components/schemas/type_domains:FeedbackEnabled'
        records:
          type: array
          items:
            $ref: '#/components/schemas/type_domains:VerificationRecord'
          description: A list of DNS records required to verify the domain.
        client_id:
          $ref: '#/components/schemas/type_domains:ClientId'
        updated_at:
          type: string
          format: date-time
          description: Time at which the domain was last updated.
        created_at:
          type: string
          format: date-time
          description: Time at which the domain was created.
      required:
        - domain_id
        - status
        - feedback_enabled
        - records
        - updated_at
        - created_at
      title: Domain
    type_:ErrorName:
      type: string
      description: Name of error.
      title: ErrorName
    type_:ErrorMessage:
      type: string
      description: Error message.
      title: ErrorMessage
    type_:ErrorResponse:
      type: object
      properties:
        name:
          $ref: '#/components/schemas/type_:ErrorName'
        message:
          $ref: '#/components/schemas/type_:ErrorMessage'
      required:
        - name
        - message
      title: ErrorResponse
  securitySchemes:
    Bearer:
      type: http
      scheme: bearer
```

--------------------------------

### Update Draft - Python

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/update

Example of updating a draft in an inbox using the AgentMail Python SDK.

```APIDOC
## PATCH /v0/inboxes/{inbox_id}/drafts/{draft_id}

### Description
Updates a specific draft within an inbox.

### Method
PATCH

### Endpoint
`/v0/inboxes/{inbox_id}/drafts/{draft_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox containing the draft.
- **draft_id** (string) - Required - The ID of the draft to update.

#### Request Body
- **{}** (object) - Optional - An empty JSON object, indicating no specific fields are being updated in this example. The actual payload would contain fields to modify.

### Request Example
```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.drafts.update(
    inbox_id="inbox_id",
    draft_id="draft_id"
)
```

### Response

#### Success Response (200)

- **(object)** - Details of the updated draft. The exact structure depends on the API response for a successful update.
  
  ```
  
  ```

--------------------------------

### Get Inbox

Source: https://docs.agentmail.to/api-reference/inboxes/get

This endpoint retrieves a specific inbox. It requires an inbox ID and an API key for authentication.

```APIDOC
## GET /v0/inboxes/{inbox_id}

### Description
Retrieves a specific inbox using its unique identifier.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The unique identifier of the inbox to retrieve.

#### Query Parameters
None

#### Request Body
None

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **inbox_data** (object) - Contains the details of the retrieved inbox.

#### Response Example
```json
{
  "id": "inbox_id",
  "email_address": "example@agentmail.to",
  "created_at": "2023-10-27T10:00:00Z"
}
```

```
--------------------------------

### GET /v0/pods/{pod_id}/lists/send/allow/entry

Source: https://docs.agentmail.to/api-reference/pods/lists/get

This endpoint allows an entry to be sent to a specific list within a pod. It requires an API key for authentication.

```APIDOC
## GET /v0/pods/{pod_id}/lists/send/allow/entry

### Description
Allows an entry to be sent to a specific list within a pod. Requires API key authentication.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/lists/send/allow/entry

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The ID of the pod.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **message** (string) - A success message indicating the entry was allowed.

#### Response Example
```json
{
  "message": "Entry allowed successfully."
}
```

```
--------------------------------

### List Domains using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/domains/list

Examples of how to list domains using the AgentMail SDK. These snippets demonstrate initializing the client with an API key and making a request to the domains endpoint. Ensure you replace 'YOUR_TOKEN_HERE' or '<api_key>' with your actual AgentMail API key.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.domains.list({});
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.domains.list()
```

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/domains"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/domains")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/domains")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/domains', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/domains");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/domains")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### POST /pods

Source: https://docs.agentmail.to/changelog

Creates a new pod, which serves as a team workspace.

```APIDOC
## POST /pods

### Description
Creates a new pod (team workspace).

### Method
POST

### Endpoint
/pods

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
(Details not provided in the source text)

### Request Example
```json
{
  "example": "request body"
}
```

### Response

#### Success Response (200)

(Details not provided in the source text)

#### Response Example

```json
{
  "example": "response body"
}
```

```
--------------------------------

### Fetch Inbox Metrics via HTTP GET Request (Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/metrics/get

This Swift code demonstrates fetching inbox metrics using URLSession. It sets up an NSMutableURLRequest with the 'Authorization' header and initiates a data task to execute the GET request. Error handling and response printing are included.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Update AgentMail Draft (Go)

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/update

Provides a Go example for updating an AgentMail draft. This code directly uses the `net/http` package to make a PATCH request to the AgentMail API. It requires an API key and the relevant inbox and draft IDs. The request body is an empty JSON object.

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id"

    payload := strings.NewReader("{}")

    req, _ := http.NewRequest("PATCH", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Fetch Inbox Metrics via HTTP GET Request (Ruby)

Source: https://docs.agentmail.to/api-reference/inboxes/metrics/get

This Ruby code snippet demonstrates fetching inbox metrics using Net::HTTP. It constructs the request URL, sets the 'Authorization' header, and sends a GET request to the AgentMail API. It prints the response body.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### GET /v0/drafts/{draft_id}/attachments/{attachment_id}

Source: https://docs.agentmail.to/api-reference/drafts/get-attachment

Retrieves a specific attachment from a draft. Requires authentication with a Bearer token.

```APIDOC
## GET /v0/drafts/{draft_id}/attachments/{attachment_id}

### Description
Retrieves a specific attachment associated with a draft email. This endpoint allows you to get details and download links for attachments.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/drafts/{draft_id}/attachments/{attachment_id}

### Parameters
#### Path Parameters
- **draft_id** (string) - Required - The unique identifier for the draft.
- **attachment_id** (string) - Required - The unique identifier for the attachment.

#### Query Parameters
None

#### Header Parameters
- **Authorization** (string) - Required - Bearer token for authentication.

### Request Example
```json
{
  "example": "GET /v0/drafts/draft_123/attachments/attach_abc HTTP/1.1\nHost: api.agentmail.to\nAuthorization: Bearer YOUR_API_TOKEN"
}
```

### Response

#### Success Response (200)

- **attachment_id** (string) - The ID of the attachment.
- **filename** (string) - The name of the attachment file.
- **size** (integer) - The size of the attachment in bytes.
- **content_type** (string) - The MIME type of the attachment.
- **content_disposition** (string) - The content disposition (e.g., 'inline', 'attachment').
- **content_id** (string) - The content ID of the attachment.
- **download_url** (string) - A URL to download the attachment.
- **expires_at** (string) - The date and time when the download URL expires.

#### Response Example

```json
{
  "attachment_id": "attach_abc",
  "filename": "document.pdf",
  "size": 102400,
  "content_type": "application/pdf",
  "content_disposition": "attachment",
  "content_id": "<cid_xyz>",
  "download_url": "https://cdn.agentmail.to/attachments/xyz/document.pdf?expires=...",
  "expires_at": "2023-10-27T10:00:00Z"
}
```

#### Error Response (404)

- **name** (string) - The name of the error.
- **message** (string) - A descriptive message about the error.

#### Error Response Example

```json
{
  "name": "NotFoundError",
  "message": "Attachment not found."
}
```

```
--------------------------------

### List Pod Threads via HTTP (Swift)

Source: https://docs.agentmail.to/api-reference/pods/threads/list

Demonstrates how to list threads in a pod using Swift's URLSession. It constructs an NSMutableURLRequest with the GET method, sets the 'Authorization' header, and sends the request.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id/threads")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Get Draft Endpoint - OpenAPI Specification

Source: https://docs.agentmail.to/api-reference/drafts/get

Defines the GET endpoint for retrieving a draft by its ID. It includes path parameters, header authentication, and specifies the success (200) and error (404) responses with their respective schemas.

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/drafts/{draft_id}:
    get:
      operationId: get
      summary: Get Draft
      tags:
        - subpackage_drafts
      parameters:
        - name: draft_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_drafts:DraftId'
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_drafts:Draft'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_drafts:DraftId:
      type: string
      description: ID of draft.
      title: DraftId
    type_inboxes:InboxId:
      type: string
      description: ID of inbox.
      title: InboxId
    type_threads:ThreadId:
      type: string
      description: ID of thread.
      title: ThreadId
    type_drafts:DraftClientId:
      type: string
      description: Client ID of draft.
      title: DraftClientId
    type_drafts:DraftLabels:
      type: array
      items:
        type: string
      description: Labels of draft.
      title: DraftLabels
    type_drafts:DraftReplyTo:
      type: array
      items:
        type: string
      description: >-
        Reply-to addresses. In format `username@domain.com` or `Display Name
        <username@domain.com>`.
      title: DraftReplyTo
    type_drafts:DraftTo:
      type: array
      items:
        type: string
      description: >-
        Addresses of recipients. In format `username@domain.com` or `Display
        Name <username@domain.com>`.
      title: DraftTo
    type_drafts:DraftCc:
      type: array
      items:
        type: string
      description: >-
        Addresses of CC recipients. In format `username@domain.com` or `Display
        Name <username@domain.com>`.
      title: DraftCc
    type_drafts:DraftBcc:
      type: array
      items:
        type: string
      description: >-
        Addresses of BCC recipients. In format `username@domain.com` or `Display
        Name <username@domain.com>`.
      title: DraftBcc
    type_drafts:DraftSubject:
      type: string
      description: Subject of draft.
      title: DraftSubject
    type_drafts:DraftPreview:
      type: string
      description: Text preview of draft.
      title: DraftPreview
    type_drafts:DraftText:
      type: string
      description: Plain text body of draft.
      title: DraftText
    type_drafts:DraftHtml:
      type: string
      description: HTML body of draft.
      title: DraftHtml
    type_attachments:AttachmentId:
      type: string
      description: ID of attachment.
      title: AttachmentId
    type_attachments:AttachmentFilename:
      type: string
      description: Filename of attachment.
      title: AttachmentFilename
    type_attachments:AttachmentSize:
      type: integer
      description: Size of attachment in bytes.
      title: AttachmentSize
    type_attachments:AttachmentContentType:
      type: string
      description: Content type of attachment.
      title: AttachmentContentType
    type_attachments:AttachmentContentDisposition:
      type: string
      enum:
        - inline
        - attachment
      description: Content disposition of attachment.
      title: AttachmentContentDisposition
    type_attachments:AttachmentContentId:
      type: string
      description: Content ID of attachment.
      title: AttachmentContentId
    type_attachments:Attachment:
      type: object
      properties:
        attachment_id:
          $ref: '#/components/schemas/type_attachments:AttachmentId'
        filename:
          $ref: '#/components/schemas/type_attachments:AttachmentFilename'
        size:
          $ref: '#/components/schemas/type_attachments:AttachmentSize'
        content_type:
          $ref: '#/components/schemas/type_attachments:AttachmentContentType'
        content_disposition:
          $ref: '#/components/schemas/type_attachments:AttachmentContentDisposition'
        content_id:
          $ref: '#/components/schemas/type_attachments:AttachmentContentId'
      required:
        - attachment_id
        - size
      title: Attachment
    type_drafts:DraftAttachments:
      type: array
      items:
        $ref: '#/components/schemas/type_attachments:Attachment'
      description: Attachments in draft.
      title: DraftAttachments
    type_drafts:DraftInReplyTo:
      type: string
```

--------------------------------

### Fetch Inbox Threads (Ruby)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Example of how to fetch threads from a specific inbox using a direct HTTP request in Ruby.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}

### Description
Retrieves a specific thread from a given inbox.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/threads/{thread_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox.
- **thread_id** (string) - Required - The ID of the thread to retrieve.

#### Headers
- **Authorization** (string) - Required - Bearer token for authentication. Example: `Bearer <api_key>`

### Request Example
```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

### Response

#### Success Response (200)

- **(object)** - Details of the requested thread.

#### Response Example

```json
{
  "id": "thread_id",
  "inbox_id": "inbox_id",
  "subject": "Example Subject",
  "snippet": "This is a snippet of the thread content.",
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### List Pods using AgentMail SDK (TypeScript, Python)

Source: https://docs.agentmail.to/api-reference/pods/list

Examples of listing pods using the official AgentMail SDKs in TypeScript and Python. These snippets require the 'agentmail' package and an API key for authentication.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.list({});
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.list()
```

--------------------------------

### Get Inbox Details (OpenAPI)

Source: https://docs.agentmail.to/api-reference/inboxes/get

This OpenAPI specification defines the GET endpoint for retrieving inbox details. It requires an `inbox_id` path parameter and an `Authorization` header for Bearer authentication. Successful responses return inbox details, while errors return a standard error response.

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/inboxes/{inbox_id}:
    get:
      operationId: get
      summary: Get Inbox
      tags:
        - subpackage_inboxes
      parameters:
        - name: inbox_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_inboxes:InboxId'
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_inboxes:Inbox'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_inboxes:InboxId:
      type: string
      description: ID of inbox.
      title: InboxId
    type_pods:PodId:
      type: string
      description: ID of pod.
      title: PodId
    type_inboxes:DisplayName:
      type: string
      description: 'Display name: `Display Name <username@domain.com>`.'
      title: DisplayName
    type_inboxes:ClientId:
      type: string
      description: Client ID of inbox.
      title: ClientId
    type_inboxes:Inbox:
      type: object
      properties:
        pod_id:
          $ref: '#/components/schemas/type_pods:PodId'
        inbox_id:
          $ref: '#/components/schemas/type_inboxes:InboxId'
        display_name:
          $ref: '#/components/schemas/type_inboxes:DisplayName'
        client_id:
          $ref: '#/components/schemas/type_inboxes:ClientId'
        updated_at:
          type: string
          format: date-time
          description: Time at which inbox was last updated.
        created_at:
          type: string
          format: date-time
          description: Time at which inbox was created.
      required:
        - pod_id
        - inbox_id
        - updated_at
        - created_at
      title: Inbox
    type_:ErrorName:
      type: string
      description: Name of error.
      title: ErrorName
    type_:ErrorMessage:
      type: string
      description: Error message.
      title: ErrorMessage
    type_:ErrorResponse:
      type: object
      properties:
        name:
          $ref: '#/components/schemas/type_:ErrorName'
        message:
          $ref: '#/components/schemas/type_:ErrorMessage'
      required:
        - name
        - message
      title: ErrorResponse
  securitySchemes:
    Bearer:
      type: http
      scheme: bearer
```

--------------------------------

### Get Message Attachment using PHP Guzzle Client

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

This PHP snippet shows how to retrieve a message attachment using the Guzzle HTTP client. It sends a GET request to the AgentMail API, setting the 'Authorization' header with the API key. The response body is then echoed.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/attachments/attachment_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### Get Domain Details

Source: https://docs.agentmail.to/changelog

Retrieves detailed information and verification records for a specific domain.

```APIDOC
## GET /domains/{domain_id}

### Description
Retrieves detailed information and verification records for a specific domain.

### Method
GET

### Endpoint
/domains/{domain_id}

### Parameters
#### Path Parameters
- **domain_id** (string) - Required - The unique identifier of the domain.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **id** (string) - The unique identifier for the domain.
- **name** (string) - The domain name.
- **verification_status** (string) - The current verification status of the domain.
- **dns_records** (array) - A list of DNS records required for verification.
  - **type** (string) - The type of DNS record (e.g., 'TXT', 'CNAME', 'MX').
  - **name** (string) - The name or host for the DNS record.
  - **value** (string) - The value of the DNS record.

#### Response Example
{
  "id": "domain_123",
  "name": "example.com",
  "verification_status": "verified",
  "dns_records": [
    {
      "type": "TXT",
      "name": "_dmarc",
      "value": "v=DMARC1; p=none"
    }
  ]
}
```

--------------------------------

### Initialize AgentMail and OpenAI Clients in Python

Source: https://docs.agentmail.to/sales-agent-websocket

Initializes the necessary clients for interacting with AgentMail and OpenAI. It loads API keys from environment variables using `dotenv`. Ensure AGENTMAIL_API_KEY and OPENAI_API_KEY are set in your .env file.

```python
import asyncio
import os
import re
from dotenv import load_dotenv
from agentmail import AsyncAgentMail, Subscribe, Subscribed, MessageReceivedEvent
from openai import AsyncOpenAI

# Load environment variables
load_dotenv()

# Initialize clients
agentmail = AsyncAgentMail(api_key=os.getenv("AGENTMAIL_API_KEY"))
openai = AsyncOpenAI(api_key=os.getenv("OPENAI_API_KEY"))

# Simple conversation history (thread_id -> messages)
conversations = {}

# Store manager email for notifications
manager_email = None
```

--------------------------------

### OpenAPI Specification for Get Raw Message

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-raw

This OpenAPI 3.1.0 specification defines the 'Get Raw Message' operation. It outlines the endpoint path, HTTP method, parameters (inbox_id, message_id, Authorization), and possible responses (200 for success with binary data, 404 for not found).

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/inboxes/{inbox_id}/messages/{message_id}/raw:
    get:
      operationId: get-raw
      summary: Get Raw Message
      tags:
        - subpackage_inboxes.subpackage_inboxes/messages
      parameters:
        - name: inbox_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_inboxes:InboxId'
        - name: message_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_messages:MessageId'
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/octet-stream:
              schema:
                type: string
                format: binary
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_inboxes:InboxId:
      type: string
      description: ID of inbox.
      title: InboxId
    type_messages:MessageId:
      type: string
      description: ID of message.
      title: MessageId
    type_:ErrorName:
      type: string
      description: Name of error.
      title: ErrorName
    type_:ErrorMessage:
      type: string
      description: Error message.
      title: ErrorMessage
    type_:ErrorResponse:
      type: object
      properties:
        name:
          $ref: '#/components/schemas/type_:ErrorName'
        message:
          $ref: '#/components/schemas/type_:ErrorMessage'
      required:
        - name
        - message
      title: ErrorResponse
  securitySchemes:
    Bearer:
      type: http
      scheme: bearer
```

--------------------------------

### Get Raw Message API Endpoint

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-raw

This snippet shows the HTTP GET request to retrieve the raw content of a message. It requires the inbox ID and message ID as path parameters and an Authorization header for authentication. The response is typically binary data or an error object.

```HTTP
GET https://api.agentmail.to/v0/inboxes/{inbox_id}/messages/{message_id}/raw
Authorization: Bearer YOUR_API_KEY
```

--------------------------------

### Update Draft - Swift

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/update

Example of updating a draft in an inbox using URLSession in Swift.

```APIDOC
## PATCH /v0/inboxes/{inbox_id}/drafts/{draft_id}

### Description
Updates a specific draft within an inbox.

### Method
PATCH

### Endpoint
`/v0/inboxes/{inbox_id}/drafts/{draft_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox containing the draft.
- **draft_id** (string) - Required - The ID of the draft to update.

#### Request Body
- **{}** (object) - Optional - An empty JSON object, indicating no specific fields are being updated in this example. The actual payload would contain fields to modify.

### Request Example
```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "PATCH"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

### Response

#### Success Response (200)

- **(object)** - Details of the updated draft. The exact structure depends on the API response for a successful update.
  
  ```
  
  ```

--------------------------------

### Fetch Inbox Metrics via HTTP GET Request (PHP)

Source: https://docs.agentmail.to/api-reference/inboxes/metrics/get

This PHP snippet uses the Guzzle HTTP client to fetch inbox metrics. It sends a GET request with the necessary 'Authorization' header and outputs the response body. Make sure to include Guzzle via Composer.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### Update LiveKit Agent Entrypoint with EmailAssistant

Source: https://docs.agentmail.to/integrate-livekit-agents

Modifies the `entrypoint` function in the LiveKit agent script to use the newly defined `EmailAssistant` class. This ensures that the agent starts with email capabilities enabled.

```python
await session.start(
    room=ctx.room,
    agent=EmailAssistant(),  # Replace Assistant with EmailAssistant.
    room_input_options=RoomInputOptions(
        noise_cancellation=noise_cancellation.BVC()
    ),
)
```

--------------------------------

### Fetch Organizations using HTTP Request (Java)

Source: https://docs.agentmail.to/api-reference/organizations/get

This Java code snippet demonstrates fetching organization data via an HTTP GET request using the Unirest library. It includes setting the necessary Authorization header for the request.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/organizations")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Update Draft - Ruby

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/update

Example of updating a draft in an inbox using Ruby's Net::HTTP.

```APIDOC
## PATCH /v0/inboxes/{inbox_id}/drafts/{draft_id}

### Description
Updates a specific draft within an inbox.

### Method
PATCH

### Endpoint
`/v0/inboxes/{inbox_id}/drafts/{draft_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox containing the draft.
- **draft_id** (string) - Required - The ID of the draft to update.

#### Request Body
- **{}** (object) - Optional - An empty JSON object, indicating no specific fields are being updated in this example. The actual payload would contain fields to modify.

### Request Example
```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Patch.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{}"

response = http.request(request)
puts response.read_body
```

### Response

#### Success Response (200)

- **(object)** - Details of the updated draft. The exact structure depends on the API response for a successful update.
  
  ```
  
  ```

--------------------------------

### List Inbox Drafts - PHP

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/list

Example of how to list drafts for a specific inbox using Guzzle HTTP client in PHP.

```APIDOC
## GET /v0/inboxes/{inbox_id}/drafts

### Description
Retrieves a list of drafts for a specified inbox.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/drafts

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox to retrieve drafts from.

#### Query Parameters
None

### Request Example
```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/drafts', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

### Response

#### Success Response (200)

- **(object)** - A list of draft objects.

#### Response Example

```json
{
  "example": "[Draft objects]"
}
```

```
--------------------------------

### GET /pods/{pod_id}

Source: https://docs.agentmail.to/changelog

Retrieves detailed information about a specific pod.

```APIDOC
## GET /pods/{pod_id}

### Description
Gets pod details.

### Method
GET

### Endpoint
/pods/{pod_id}

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The unique identifier of the pod.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
(Details not provided in the source text)

#### Response Example
```json
{
  "example": "response body"
}
```

```
--------------------------------

### Retrieve Attachment using HTTP Client (Swift)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get-attachment

This Swift code demonstrates how to retrieve an attachment using URLSession. It creates an NSMutableURLRequest, sets the HTTP method to GET, and includes the API key in the Authorization header.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id/attachments/attachment_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Fetch Inbox Threads (TypeScript)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Example of how to fetch threads from a specific inbox using the AgentMail TypeScript SDK.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}

### Description
Retrieves a specific thread from a given inbox.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/threads/{thread_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox.
- **thread_id** (string) - Required - The ID of the thread to retrieve.

### Request Example
```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.threads.get("inbox_id", "thread_id");
}
main();
```

### Response

#### Success Response (200)

- **(object)** - Details of the requested thread.

#### Response Example

```json
{
  "id": "thread_id",
  "inbox_id": "inbox_id",
  "subject": "Example Subject",
  "snippet": "This is a snippet of the thread content.",
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### Get Zone File using Agentmail API (Python)

Source: https://docs.agentmail.to/api-reference/domains/get-zone-file

Demonstrates fetching a domain's zone file with the Agentmail Python SDK. Authentication is handled via an API key, and the domain ID is a required argument.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.domains.get_zone_file(
    domain_id=":domain_id"
)
```

--------------------------------

### GET /pods/{pod_id}/metrics

Source: https://docs.agentmail.to/changelog

Retrieves metrics for a specified pod.

```APIDOC
## GET /pods/{pod_id}/metrics

### Description
Gets metrics for a pod.

### Method
GET

### Endpoint
/pods/{pod_id}/metrics

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The unique identifier of the pod.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
(Details not provided in the source text)

#### Response Example
```json
{
  "example": "response body"
}
```

```
--------------------------------

### List Drafts using AgentMail SDK (TypeScript, Python)

Source: https://docs.agentmail.to/api-reference/drafts/list

Demonstrates how to list drafts using the AgentMail SDK in TypeScript and Python. Requires the agentmail package and an API key for authentication.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.drafts.list({});
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.drafts.list()
```

--------------------------------

### DKIM Record Examples for Email Signing

Source: https://docs.agentmail.to/email-protocols

DKIM (DomainKeys Identified Mail) uses CNAME records in your DNS to associate your domain with a public key, allowing for digital signing of emails. These examples show how AgentMail uses CNAME records to manage DKIM keys automatically for your domain.

```text
CNAME | b4w..._domainkey.payment... | b4w...dkim.agentmail.com
```

```text
CNAME | 32c..._domainkey.payment... | 32c...dkim.agentmail.com
```

```text
CNAME | xl4..._domainkey.payment... | xl4...dkim.agentmail.com
```

--------------------------------

### Fetch Inbox Threads (PHP)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Example of how to fetch threads from a specific inbox using Guzzle HTTP client in PHP.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}

### Description
Retrieves a specific thread from a given inbox.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/threads/{thread_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox.
- **thread_id** (string) - Required - The ID of the thread to retrieve.

#### Headers
- **Authorization** (string) - Required - Bearer token for authentication. Example: `Bearer <api_key>`

### Request Example
```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

### Response

#### Success Response (200)

- **(object)** - Details of the requested thread.

#### Response Example

```json
{
  "id": "thread_id",
  "inbox_id": "inbox_id",
  "subject": "Example Subject",
  "snippet": "This is a snippet of the thread content.",
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### GET /v0/inboxes/{inbox_id}/threads/{thread_id}/attachments/{attachment_id}

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get-attachment

Retrieves details of a specific attachment within a thread in an inbox. Requires authentication.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}/attachments/{attachment_id}

### Description
Retrieves details of a specific attachment within a thread in an inbox. Requires authentication.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/inboxes/{inbox_id}/threads/{thread_id}/attachments/{attachment_id}

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - ID of inbox.
- **thread_id** (string) - Required - ID of thread.
- **attachment_id** (string) - Required - ID of attachment.

#### Query Parameters
None

#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Request Example
```

GET https://api.agentmail.to/v0/inboxes/inbox123/threads/thread456/attachments/attachment789
Authorization: Bearer YOUR_API_TOKEN

```
### Response
#### Success Response (200)
- **attachment_id** (string) - The ID of the attachment.
- **filename** (string) - The filename of the attachment.
- **size** (integer) - The size of the attachment in bytes.
- **content_type** (string) - The content type of the attachment.
- **content_disposition** (string) - The content disposition of the attachment (inline or attachment).
- **content_id** (string) - The content ID of the attachment.
- **download_url** (string) - A URL to download the attachment.
- **expires_at** (string) - The time at which the download URL expires.

#### Response Example (200)
```json
{
  "attachment_id": "attachment789",
  "filename": "document.pdf",
  "size": 102400,
  "content_type": "application/pdf",
  "content_disposition": "attachment",
  "content_id": "cid:part1.0001@example.com",
  "download_url": "https://api.agentmail.to/download/attachment789?expires=...",
  "expires_at": "2023-10-27T10:00:00Z"
}
```

#### Error Response (404)

- **name** (string) - The name of the error.
- **message** (string) - A descriptive error message.

#### Response Example (404)

```json
{
  "name": "NotFoundError",
  "message": "Attachment not found."
}
```

```
--------------------------------

### List API Keys via HTTP Request (Ruby)

Source: https://docs.agentmail.to/api-reference/api-keys/list

A Ruby script demonstrating how to fetch API keys from AgentMail by making an HTTP GET request. It utilizes Ruby's built-in `net/http` and `uri` libraries for handling the request.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/api-keys")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Pod Lifecycle and Resource Management

Source: https://docs.agentmail.to/documentation/core-concepts/pods

Understand the lifecycle of pods, including the default pod creation and the inability to delete pods with existing child resources. Learn about creating and listing resources scoped to a pod.

```APIDOC
## Pod Lifecycle and Resource Management

### Pod Lifecycle

- Upon signup, a `Default Pod` is automatically created. All initially created resources (Inboxes, Domains) are associated with this pod.
- A `Pod` cannot be deleted if it contains existing child resources (Inboxes, Domains). These resources must be deleted first.

### Managing Resources within Pods

#### Creating Resources

Resources can be created **within** a pod:

- **Inboxes**: Individual email accounts.
- **Domains**: Custom domains associated with the pod.

<Callout>
  NOTE: Domains can currently only be scoped to one pod or all pods. Scoping to multiple, but not all, pods is not supported.
</Callout>

<Tip>
  TIP: Specify a `client_id` when creating a `Pod` for a unique identifier. This allows you to use your internal ID to access the resource, eliminating the need for a separate mapping table.
</Tip>

#### Listing Resources Scoped to a Pod

The following resources can be listed **scoped to** a specific pod:

- **Inboxes**: `GET /pods/{pod_id}/inboxes` - View all inboxes within a pod.
- **Threads**: `GET /pods/{pod_id}/threads` - View all email conversations across all inboxes in the pod.
- **Drafts**: `GET /pods/{pod_id}/drafts` - View all draft emails across all inboxes in the pod.
- **Domains**: `GET /pods/{pod_id}/domains` - View all custom domains within the pod.

This provides a consolidated view of activity within a customer's workspace, facilitating features like unified unread email counts or listing all threads for a specific customer.
```

--------------------------------

### GET /v0/pods/{pod_id}/threads/{thread_id}

Source: https://docs.agentmail.to/api-reference/pods/threads/get

Fetches a specific thread from a pod. Requires the pod ID and the thread ID as path parameters.

```APIDOC
## GET /v0/pods/{pod_id}/threads/{thread_id}

### Description
Retrieves a specific email thread from a given pod using its unique identifiers.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/threads/{thread_id}

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The unique identifier of the pod.
- **thread_id** (string) - Required - The unique identifier of the thread.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **thread_id** (string) - The unique identifier of the thread.
- **subject** (string) - The subject line of the email thread.
- **snippet** (string) - A short preview of the thread's content.
- **history_id** (string) - The identifier for the thread's history.
- **messages** (array) - A list of messages within the thread.
  - **message_id** (string) - The unique identifier of the message.
  - **from** (object) - Information about the sender.
    - **name** (string) - The name of the sender.
    - **email** (string) - The email address of the sender.
  - **to** (array) - A list of recipients.
    - **name** (string) - The name of the recipient.
    - **email** (string) - The email address of the recipient.
  - **date** (string) - The timestamp when the message was sent (ISO 8601 format).
  - **payload** (string) - The content of the message.

#### Response Example
```json
{
  "thread_id": "th_abc123",
  "subject": "Meeting Follow-up",
  "snippet": "Hi team, regarding our meeting yesterday...",
  "history_id": "hist_xyz789",
  "messages": [
    {
      "message_id": "msg_12345",
      "from": {
        "name": "Alice",
        "email": "alice@example.com"
      },
      "to": [
        {
          "name": "Bob",
          "email": "bob@example.com"
        }
      ],
      "date": "2023-10-27T10:00:00Z",
      "payload": "Hello Bob, ..."
    }
  ]
}
```

```
--------------------------------

### Modify Intent Keywords (Python)

Source: https://docs.agentmail.to/sales-agent-websocket

Example of how to customize the intent detection by modifying the `intent_keywords` dictionary within the `handle_customer_email` function. New intents and keywords can be added.

```python
intent_keywords = {
    'interested': ['interested', 'demo', 'meeting', 'pricing', 'sign up'],
    'not_interested': ['not interested', 'unsubscribe', 'remove me'],
    'question': ['?', 'how', 'what', 'when', 'can you'],
    'urgent': ['urgent', 'asap', 'immediately']  # Add new intent
}
```

--------------------------------

### SPF Record Example for Email Sending Authorization

Source: https://docs.agentmail.to/email-protocols

The SPF (Sender Policy Framework) record is a TXT record in your DNS that lists authorized servers for sending emails on behalf of your domain. This example shows how to authorize AgentMail to send emails for the 'mail.domain.com' subdomain.

```text
TXT | mail.domain.com | v=spf1 include:agentmail.com -all
```

--------------------------------

### Fetch Pod Information via HTTP Request

Source: https://docs.agentmail.to/api-reference/pods/get

Shows how to retrieve pod information by making a direct HTTP GET request to the AgentMail API. This method requires manual construction of the request, including setting the Authorization header. It's useful when the SDK is not available or preferred.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/pods/pod_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Update Draft - C#

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/update

Example of updating a draft in an inbox using RestSharp in C#.

```APIDOC
## PATCH /v0/inboxes/{inbox_id}/drafts/{draft_id}

### Description
Updates a specific draft within an inbox.

### Method
PATCH

### Endpoint
`/v0/inboxes/{inbox_id}/drafts/{draft_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox containing the draft.
- **draft_id** (string) - Required - The ID of the draft to update.

#### Request Body
- **{}** (object) - Optional - An empty JSON object, indicating no specific fields are being updated in this example. The actual payload would contain fields to modify.

### Request Example
```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id");
var request = new RestRequest(Method.PATCH);
request.AddHeader("Authorization", "Bearer <api_key>");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{{}}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

### Response

#### Success Response (200)

- **(object)** - Details of the updated draft. The exact structure depends on the API response for a successful update.
  
  ```
  
  ```

--------------------------------

### GET /v0/pods/{pod_id}/drafts/{draft_id}/attachments/{attachment_id}

Source: https://docs.agentmail.to/api-reference/pods/drafts/get-attachment

Retrieves a specific attachment from a draft within a pod. This endpoint allows you to get details about an attachment, including its filename, size, content type, and a download URL.

```APIDOC
## GET /v0/pods/{pod_id}/drafts/{draft_id}/attachments/{attachment_id}

### Description
Retrieves a specific attachment from a draft within a pod. This endpoint allows you to get details about an attachment, including its filename, size, content type, and a download URL.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/drafts/{draft_id}/attachments/{attachment_id}

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - ID of pod.
- **draft_id** (string) - Required - ID of draft.
- **attachment_id** (string) - Required - ID of attachment.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **attachment_id** (string) - ID of the attachment.
- **filename** (string) - Filename of the attachment.
- **size** (integer) - Size of the attachment in bytes.
- **content_type** (string) - Content type of the attachment.
- **content_disposition** (string) - Content disposition of the attachment (inline or attachment).
- **content_id** (string) - Content ID of the attachment.
- **download_url** (string) - URL to download the attachment.
- **expires_at** (string) - Time at which the download URL expires.

#### Response Example
```json
{
  "attachment_id": "att_abc123",
  "filename": "document.pdf",
  "size": 102400,
  "content_type": "application/pdf",
  "content_disposition": "attachment",
  "content_id": "cid:unique_content_id",
  "download_url": "https://api.agentmail.to/v0/download/att_abc123?token=xyz789",
  "expires_at": "2023-10-27T10:00:00Z"
}
```

#### Error Response (404)

- **name** (string) - Name of the error.
- **message** (string) - Error message.

#### Error Response Example

```json
{
  "name": "NotFoundError",
  "message": "Attachment not found."
}
```

```
--------------------------------

### List Pod Drafts using HTTP Request

Source: https://docs.agentmail.to/api-reference/pods/drafts/list

Shows how to list drafts for a specific pod by making a direct HTTP GET request to the AgentMail API. This method requires manual construction of the request and handling of the response. It is useful when an official SDK is not available or preferred.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/drafts"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/drafts")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id/drafts")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/pods/pod_id/drafts', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id/drafts");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id/drafts")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### GET /pods/{pod_id}/threads

Source: https://docs.agentmail.to/changelog

Lists all threads within a specified pod.

```APIDOC
## GET /pods/{pod_id}/threads

### Description
Lists threads within a pod.

### Method
GET

### Endpoint
/pods/{pod_id}/threads

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The unique identifier of the pod.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
(Details not provided in the source text)

#### Response Example
```json
{
  "example": "response body"
}
```

```
--------------------------------

### GET /v0/inboxes/{inbox_id}/messages/{message_id}/attachments/{attachment_id}

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

Retrieves a specific attachment from a message within an inbox. Requires authentication with an API key.

```APIDOC
## GET /v0/inboxes/{inbox_id}/messages/{message_id}/attachments/{attachment_id}

### Description
Retrieves a specific attachment from a message within an inbox. Requires authentication with an API key.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/messages/{message_id}/attachments/{attachment_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox.
- **message_id** (string) - Required - The ID of the message.
- **attachment_id** (string) - Required - The ID of the attachment.

#### Query Parameters
None

#### Request Body
None

### Request Example
```http
GET /v0/inboxes/inbox_id/messages/message_id/attachments/attachment_id HTTP/1.1
Host: api.agentmail.to
Authorization: Bearer <api_key>
```

### Response

#### Success Response (200)

- **attachment_data** (binary) - The content of the attachment.

#### Response Example

(Binary data representing the attachment)

```
--------------------------------

### Create Domain in Pod using HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/pods/domains/create

This Go code snippet illustrates how to create a domain within a pod by making a direct HTTP POST request to the AgentMail API. It includes setting the Authorization header with a bearer token and the Content-Type header, along with the JSON payload.

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/domains"

    payload := strings.NewReader("{\n  \"domain\": \"domain\",\n  \"feedback_enabled\": true\n}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Access Message Attachment in Swift

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

This Swift code demonstrates how to fetch a message attachment using URLSession. It constructs an HTTP GET request, sets the 'Authorization' header, and sends the request asynchronously. The response includes HTTP status and potential errors.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/attachments/attachment_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### GET /v0/domains/{domain_id}/zone-file

Source: https://docs.agentmail.to/api-reference/domains/get-zone-file

Retrieves the zone file for a specified domain. This endpoint is useful for accessing DNS records associated with your domain.

```APIDOC
## GET /v0/domains/{domain_id}/zone-file

### Description
Retrieves the zone file for a specified domain. This endpoint is useful for accessing DNS records associated with your domain.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/domains/{domain_id}/zone-file

### Parameters
#### Path Parameters
- **domain_id** (string) - Required - The name of the domain (e.g., "your-domain.com").

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **zone_file** (binary) - The content of the domain's zone file.

#### Response Example
```

$TTL 3600
@ IN SOA ns1.agentmail.to. admin.agentmail.to. (
 2023010101 ; serial
 7200       ; refresh
 3600       ; retry
 1209600    ; expire
 60         ; minimum TTL
)

@ IN NS ns1.agentmail.to.
@ IN NS ns2.agentmail.to.
@ IN A 192.0.2.1
www IN CNAME @

```
#### Error Response (404)
- **name** (string) - The name of the error.
- **message** (string) - A descriptive message about the error.

#### Error Response Example
```json
{
  "name": "DomainNotFound",
  "message": "The specified domain could not be found."
}
```

```
--------------------------------

### Retrieve List Entry Allow - Python SDK

Source: https://docs.agentmail.to/api-reference/lists/get

Demonstrates how to fetch list entry allowance status using the Python requests library. It sends a GET request to the specified API endpoint with an authorization header. Requires the 'requests' library.

```python
import requests

url = "https://api.agentmail.to/v0/lists/send/allow/entry"

headers = {"Authorization": "Bearer <api_key>"}

response = requests.get(url, headers=headers)

print(response.json())
```

--------------------------------

### GET /v0/drafts

Source: https://docs.agentmail.to/api-reference/drafts/list

Retrieves a list of drafts with optional filtering and pagination parameters.

```APIDOC
## GET /v0/drafts

### Description
Retrieves a list of drafts. Supports filtering by labels, date ranges, and sorting options. Includes pagination capabilities.

### Method
GET

### Endpoint
/v0/drafts

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - Limit of number of items returned.
- **page_token** (string) - Optional - Page token for pagination.
- **labels** (array of strings) - Optional - Labels to filter by.
- **before** (string) - Optional - Timestamp before which to filter by (ISO 8601 format).
- **after** (string) - Optional - Timestamp after which to filter by (ISO 8601 format).
- **ascending** (boolean) - Optional - Sort in ascending temporal order.

#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Request Example
```http
GET /v0/drafts?limit=10&labels=inbox&ascending=true HTTP/1.1
Host: api.agentmail.to
Authorization: Bearer YOUR_API_TOKEN
```

### Response

#### Success Response (200)

- **drafts** (array) - List of draft objects.
   - **id** (string) - ID of the draft.
   - **labels** (array of strings) - Labels associated with the draft.
   - **to** (array of strings) - Recipient addresses.
   - **cc** (array of strings) - CC recipient addresses.
   - **bcc** (array of strings) - BCC recipient addresses.
   - **subject** (string) - Subject of the draft.
   - **preview** (string) - Text preview of the draft.
   - **created_at** (string) - Timestamp when the draft was created.
   - **modified_at** (string) - Timestamp when the draft was last modified.
- **next_page_token** (string) - Token for fetching the next page of results.

#### Response Example

```json
{
  "drafts": [
    {
      "id": "draft_123",
      "labels": ["important"],
      "to": ["recipient@example.com"],
      "cc": [],
      "bcc": [],
      "subject": "Meeting Follow-up",
      "preview": "Hi team, following up on our meeting...",
      "created_at": "2023-10-27T10:00:00Z",
      "modified_at": "2023-10-27T10:05:00Z"
    }
  ],
  "next_page_token": "page_token_abc"
}
```

#### Error Response (404)

- **error** (object) - Error details.
   - **code** (integer) - Error code.
   - **message** (string) - Error message.

#### Error Response Example

```json
{
  "error": {
    "code": 404,
    "message": "Not Found"
  }
}
```

```
--------------------------------

### Create Inbox using HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/pods/inboxes/create

Provides a Go example for creating an inbox via an HTTP POST request to the AgentMail API. It constructs the request with necessary headers and payload. Requires an API key and pod ID.

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id/inboxes"

    payload := strings.NewReader("{}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### List Inbox Drafts - TypeScript

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/list

Example of how to list drafts for a specific inbox using the AgentMail TypeScript SDK.

```APIDOC
## GET /v0/inboxes/{inbox_id}/drafts

### Description
Retrieves a list of drafts for a specified inbox.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/drafts

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox to retrieve drafts from.

#### Query Parameters
None

### Request Example
```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.drafts.list("inbox_id", {});
}
main();
```

### Response

#### Success Response (200)

- **(object)** - A list of draft objects.

#### Response Example

```json
{
  "example": "[Draft objects]"
}
```

```
--------------------------------

### Retrieve List Entry Allow - Go SDK

Source: https://docs.agentmail.to/api-reference/lists/get

Provides a Go code snippet to fetch list entry allowance status. It constructs an HTTP GET request, adds the necessary Authorization header, and prints the response status and body. Uses standard Go libraries for HTTP requests.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/lists/send/allow/entry"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### List Pod Drafts using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/pods/drafts/list

Demonstrates how to list drafts for a specific pod using the AgentMail SDK. Requires an API key and the pod ID. Handles API requests and responses.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.drafts.list("pod_id", {});
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.drafts.list(
    pod_id="pod_id"
)
```

--------------------------------

### GET /v0/inboxes/{inbox_id}

Source: https://docs.agentmail.to/api-reference/inboxes/get

Retrieves details for a specific inbox using its unique ID. This endpoint is useful for fetching all information associated with a particular inbox.

```APIDOC
## GET /v0/inboxes/{inbox_id}

### Description
Retrieves details for a specific inbox using its unique ID. This endpoint is useful for fetching all information associated with a particular inbox.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/inboxes/{inbox_id}

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - ID of the inbox.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **pod_id** (string) - ID of the pod.
- **inbox_id** (string) - ID of the inbox.
- **display_name** (string) - Display name in the format `Display Name <username@domain.com>`.
- **client_id** (string) - Client ID of the inbox.
- **updated_at** (string) - Time at which the inbox was last updated (ISO 8601 format).
- **created_at** (string) - Time at which the inbox was created (ISO 8601 format).

#### Response Example
```json
{
  "pod_id": "pod_abc123",
  "inbox_id": "inbox_xyz789",
  "display_name": "Support Team <support@example.com>",
  "client_id": "client_456def",
  "updated_at": "2023-10-27T10:00:00Z",
  "created_at": "2023-10-26T09:00:00Z"
}
```

#### Error Response (404)

- **name** (string) - The name of the error.
- **message** (string) - A descriptive message for the error.

#### Error Response Example

```json
{
  "name": "NotFoundError",
  "message": "Inbox with ID 'inbox_nonexistent' not found."
}
```

```
--------------------------------

### Retrieve Drafts using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/get

Examples of how to retrieve drafts from an inbox using the AgentMail SDK. These snippets demonstrate API calls to fetch draft details, requiring an API key and specific inbox and draft IDs.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.drafts.get("inbox_id", "draft_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.drafts.get(
    inbox_id="inbox_id",
    draft_id="draft_id"
)
```

--------------------------------

### GET /v0/inboxes/{inbox_id}/messages/{message_id}/attachments/{attachment_id}

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

Retrieves a specific attachment from a message within an inbox. Requires authentication via Bearer token.

```APIDOC
## GET /v0/inboxes/{inbox_id}/messages/{message_id}/attachments/{attachment_id}

### Description
Retrieves a specific attachment from a message within an inbox. Requires authentication via Bearer token.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/inboxes/{inbox_id}/messages/{message_id}/attachments/{attachment_id}

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - ID of inbox.
- **message_id** (string) - Required - ID of message.
- **attachment_id** (string) - Required - ID of attachment.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **attachment_id** (string) - ID of attachment.
- **filename** (string) - Filename of attachment.
- **size** (integer) - Size of attachment in bytes.
- **content_type** (string) - Content type of attachment.
- **content_disposition** (string) - Content disposition of attachment. (inline or attachment)
- **content_id** (string) - Content ID of attachment.
- **download_url** (string) - URL to download the attachment.
- **expires_at** (string) - Time at which the download URL expires.

#### Response Example
```json
{
  "attachment_id": "att_abc123",
  "filename": "document.pdf",
  "size": 102400,
  "content_type": "application/pdf",
  "content_disposition": "attachment",
  "content_id": "cid:part1.0001@example.com",
  "download_url": "https://api.agentmail.to/v0/download/att_abc123?token=...",
  "expires_at": "2023-10-27T10:00:00Z"
}
```

#### Error Response (404)

- **name** (string) - Name of error.
- **message** (string) - Error message.

#### Response Example

```json
{
  "name": "NotFoundError",
  "message": "Attachment not found."
}
```

```
--------------------------------

### Fetch Inbox Threads (C#)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Example of how to fetch threads from a specific inbox using RestSharp in C#.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}

### Description
Retrieves a specific thread from a given inbox.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/threads/{thread_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox.
- **thread_id** (string) - Required - The ID of the thread to retrieve.

#### Headers
- **Authorization** (string) - Required - Bearer token for authentication. Example: `Bearer <api_key>`

### Request Example
```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id/threads/thread_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

### Response

#### Success Response (200)

- **(object)** - Details of the requested thread.

#### Response Example

```json
{
  "id": "thread_id",
  "inbox_id": "inbox_id",
  "subject": "Example Subject",
  "snippet": "This is a snippet of the thread content.",
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### Merge SPF Records for AgentMail

Source: https://docs.agentmail.to/custom-domains

This example demonstrates how to merge an existing SPF record with AgentMail's SPF include to avoid 'Too many SPF records' errors. Ensure only one 'v=spf1' and one ending mechanism (~all or -all) are present.

```text
# Before
v=spf1 include:_spf.other-domain.com ~all

# After
v=spf1 include:_spf.other-domain.com include:spf.agentmail.to ~all
```

--------------------------------

### Run AgentMail Auto-Reply Agent (Bash)

Source: https://docs.agentmail.to/documentation/examples/auto-reply-agent

This bash command starts the AgentMail auto-reply agent. It executes the main Python script (`agent.py`) which sets up the necessary infrastructure like inboxes and webhooks, and then begins listening for incoming emails.

```bash
python agent.py
```

--------------------------------

### POST /domains

Source: https://docs.agentmail.to/custom-domains

Create a new domain and retrieve the necessary DNS records for verification. The API supports both default settings and custom feedback forwarding configurations.

```APIDOC
## POST /domains

### Description
Creates a new domain registration and returns the DNS records required for verification. Supports optional feedback forwarding configuration.

### Method
POST

### Endpoint
`/domains`

### Parameters
#### Query Parameters
- **your-domain.com** (string) - Required - The domain name to register.
- **feedback_enabled** (boolean) - Optional - If set to `false`, bounce and complaint notifications will not be sent to your domain. Defaults to `true`.
- **client_id** (string) - Optional - A unique identifier to make the request idempotent.

### Request Body
This endpoint does not require a request body. Parameters are passed as query parameters or path parameters.

### Request Example
```bash
curl -X POST https://api.agentmail.to/domains/your-domain.com \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json"
```

```python
from agentmail import AgentMail

client = AgentMail(api_key="YOUR_API_KEY")

# Create domain with default settings
domain = client.domains.create("your-domain.com")

# Or with custom feedback forwarding
domain = client.domains.create(
  "your-domain.com",
  feedback_enabled=False
)

print("Domain created:", domain)
print("DNS Records:", domain.records)
```

```typescript
import { AgentMailClient } from "agentmail";

const client = new AgentMailClient({
  apiKey: "YOUR_API_KEY",
});

// Create domain with default settings
const domain = await client.domains.create("your-domain.com");

// Or with custom feedback forwarding
const domain = await client.domains.create("your-domain.com", {
  feedback_enabled: false,
});

console.log("Domain created:", domain);
console.log("DNS Records:", domain.records);
```

### Response

#### Success Response (200)

- **domain** (object) - Details of the created domain.
   - **id** (string) - Unique identifier for the domain.
   - **name** (string) - The registered domain name.
   - **status** (string) - The current status of the domain (e.g., `pending`, `verified`).
   - **records** (array) - An array of DNS records required for verification.
      - **name** (string) - The name of the DNS record.
      - **type** (string) - The type of the DNS record (e.g., `TXT`, `CNAME`).
      - **value** (string) - The value of the DNS record.
      - **priority** (integer) - The priority of the DNS record (if applicable).

#### Response Example

```json
{
  "domain": {
    "id": "d-12345",
    "name": "your-domain.com",
    "status": "pending",
    "records": [
      {
        "name": "_domainkey",
        "type": "CNAME",
        "value": "selector1._domainkey.dkim.agentmail.to",
        "priority": null
      },
      {
        "name": "@",
        "type": "TXT",
        "value": "v=spf1 include:spf.agentmail.to ~all",
        "priority": null
      }
    ]
  }
}
```

```
--------------------------------

### Fetch Organizations using HTTP Request (C#)

Source: https://docs.agentmail.to/api-reference/organizations/get

This C# code snippet shows how to retrieve organization data using an HTTP GET request with the RestSharp library. It involves creating a RestClient, a RestRequest, and adding the Authorization header.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/organizations");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### GET /v0/pods/{pod_id}/threads/{thread_id}/attachments/{attachment_id}

Source: https://docs.agentmail.to/api-reference/pods/threads/get-attachment

Retrieves detailed information about a specific attachment within a thread in a pod. This includes metadata such as filename, size, content type, and download URL.

```APIDOC
## GET /v0/pods/{pod_id}/threads/{thread_id}/attachments/{attachment_id}

### Description
Retrieves detailed information about a specific attachment within a thread in a pod. This includes metadata such as filename, size, content type, and download URL.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/threads/{thread_id}/attachments/{attachment_id}

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - ID of the pod.
- **thread_id** (string) - Required - ID of the thread.
- **attachment_id** (string) - Required - ID of the attachment.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **attachment_id** (string) - The unique identifier for the attachment.
- **filename** (string) - The name of the attachment file.
- **size** (integer) - The size of the attachment in bytes.
- **content_type** (string) - The MIME type of the attachment (e.g., 'application/pdf').
- **content_disposition** (string) - Indicates whether the attachment should be displayed inline or as a download ('inline' or 'attachment').
- **content_id** (string) - The content ID of the attachment, if applicable.
- **download_url** (string) - A URL from which the attachment can be downloaded.
- **expires_at** (string) - The date and time when the download URL will expire.

#### Response Example
```json
{
  "attachment_id": "att_123abc",
  "filename": "document.pdf",
  "size": 102400,
  "content_type": "application/pdf",
  "content_disposition": "attachment",
  "content_id": "cid:part1.2345@example.com",
  "download_url": "https://api.agentmail.to/v0/download/att_123abc?token=xyz",
  "expires_at": "2023-10-27T10:00:00Z"
}
```

#### Error Response (404)

- **name** (string) - The name of the error (e.g., 'NotFound').
- **message** (string) - A descriptive message explaining the error.

#### Error Response Example

```json
{
  "name": "NotFound",
  "message": "Attachment not found."
}
```

```
--------------------------------

### List Drafts for a Pod

Source: https://docs.agentmail.to/api-reference/pods/drafts/list

This endpoint retrieves a list of drafts within a specified pod. Examples are provided for TypeScript, Python, Go, Ruby, Java, PHP, C#, and Swift.

```APIDOC
## GET /v0/pods/{pod_id}/drafts

### Description
Retrieves a list of drafts for a given pod.

### Method
GET

### Endpoint
`/v0/pods/{pod_id}/drafts`

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The unique identifier of the pod.

#### Query Parameters
None

#### Request Body
None

### Request Example
```

GET /v0/pods/pod_id/drafts
Authorization: Bearer <api_key>

```
### Response
#### Success Response (200)
- **drafts** (array) - A list of draft objects.
- **id** (string) - The unique identifier of the draft.
- **subject** (string) - The subject of the draft.
- **createdAt** (string) - The timestamp when the draft was created.

#### Response Example
```json
{
  "drafts": [
    {
      "id": "draft_id_1",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z"
    },
    {
      "id": "draft_id_2",
      "subject": "Project Update",
      "createdAt": "2023-10-26T15:30:00Z"
    }
  ]
}
```

```
--------------------------------

### GET /v0/threads

Source: https://docs.agentmail.to/api-reference/threads/list

Retrieves a list of threads, with options for filtering, pagination, and sorting. Requires Bearer authentication.

```APIDOC
## GET /v0/threads

### Description
Retrieves a list of threads. Supports filtering by labels, date ranges, and inclusion of spam or blocked threads. Pagination is handled via `page_token` and `limit`.

### Method
GET

### Endpoint
/v0/threads

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of items to return.
- **page_token** (string) - Optional - Token for pagination, used to retrieve the next page of results.
- **labels** (array of strings) - Optional - Filters threads by the specified labels.
- **before** (string) - Optional - Filters threads sent or received before this ISO 8601 timestamp.
- **after** (string) - Optional - Filters threads sent or received after this ISO 8601 timestamp.
- **ascending** (boolean) - Optional - If true, sorts threads in ascending temporal order; otherwise, descending.
- **include_spam** (boolean) - Optional - If true, includes spam threads in the results.
- **include_blocked** (boolean) - Optional - If true, includes blocked threads in the results.

#### Header Parameters
- **Authorization** (string) - Required - Bearer token for authentication. Example: `Bearer YOUR_API_TOKEN`

### Response
#### Success Response (200)
- **items** (array) - A list of thread objects.
  - **id** (string) - The unique identifier for the thread.
  - **labels** (array of strings) - Labels associated with the thread.
  - **received_timestamp** (string) - ISO 8601 timestamp of the last received message.
  - **sent_timestamp** (string) - ISO 8601 timestamp of the last sent message.
  - **subject** (string) - The subject of the thread.
  - **preview** (string) - A text preview of the last message in the thread.
  - **senders** (array of strings) - Senders in the thread (e.g., `username@domain.com` or `Display Name <username@domain.com>`)
  - **recipients** (array of strings) - Recipients in the thread (e.g., `username@domain.com` or `Display Name <username@domain.com>`)
- **next_page_token** (string) - Token for retrieving the next page of results, if available.

#### Error Response (404)
- **code** (integer) - The error code.
- **message** (string) - A description of the error.

### Request Example
```http
GET /v0/threads?limit=20&labels=inbox&ascending=true HTTP/1.1
Host: api.agentmail.to
Authorization: Bearer YOUR_API_TOKEN
Accept: application/json
```

### Response Example (200)

```json
{
  "items": [
    {
      "id": "thread_123",
      "labels": ["inbox", "important"],
      "received_timestamp": "2023-10-27T10:00:00Z",
      "sent_timestamp": "2023-10-27T10:05:00Z",
      "subject": "Meeting Update",
      "preview": "Hi team, please find the updated meeting minutes attached.",
      "senders": ["sender@example.com"],
      "recipients": ["recipient@example.com"]
    }
  ],
  "next_page_token": "page_token_abc"
}
```

### Response Example (404)

```json
{
  "code": 404,
  "message": "Resource not found"
}
```

```
--------------------------------

### Create Project Directory (Bash)

Source: https://docs.agentmail.to/documentation/examples/auto-reply-agent

This command creates a new directory for the auto-reply agent and navigates into it. It's the initial step for setting up the project environment.

```bash
mkdir auto-reply-agent
cd auto-reply-agent
```

--------------------------------

### Update Draft - TypeScript

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/update

Example of updating a draft in an inbox using the AgentMail TypeScript SDK.

```APIDOC
## PATCH /v0/inboxes/{inbox_id}/drafts/{draft_id}

### Description
Updates a specific draft within an inbox.

### Method
PATCH

### Endpoint
`/v0/inboxes/{inbox_id}/drafts/{draft_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox containing the draft.
- **draft_id** (string) - Required - The ID of the draft to update.

#### Request Body
- **{}** (object) - Optional - An empty JSON object, indicating no specific fields are being updated in this example. The actual payload would contain fields to modify.

### Request Example
```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.drafts.update("inbox_id", "draft_id", {{}});
}
main();
```

### Response

#### Success Response (200)

- **(object)** - Details of the updated draft. The exact structure depends on the API response for a successful update.
  
  ```
  
  ```

--------------------------------

### Fetch Inbox Metrics with AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/inboxes/metrics/get

Shows how to fetch inbox metrics using the AgentMail Python SDK. This requires the 'agentmail' library and an API key. The function retrieves metrics for a specific inbox between a start and end timestamp.

```python
from agentmail import AgentMail
from datetime import datetime

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.metrics.get(
    inbox_id="inbox_id",
    start_timestamp=datetime.fromisoformat("2024-01-15T09:30:00Z"),
    end_timestamp=datetime.fromisoformat("2024-01-15T09:30:00Z")
)
```

--------------------------------

### Update Draft - PHP

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/update

Example of updating a draft in an inbox using Guzzle HTTP client in PHP.

```APIDOC
## PATCH /v0/inboxes/{inbox_id}/drafts/{draft_id}

### Description
Updates a specific draft within an inbox.

### Method
PATCH

### Endpoint
`/v0/inboxes/{inbox_id}/drafts/{draft_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox containing the draft.
- **draft_id** (string) - Required - The ID of the draft to update.

#### Request Body
- **{}** (object) - Optional - An empty JSON object, indicating no specific fields are being updated in this example. The actual payload would contain fields to modify.

### Request Example
```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('PATCH', 'https://api.agentmail.to/v0/inboxes/inbox_id/drafts/draft_id', [
  'body' => '{}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

### Response

#### Success Response (200)

- **(object)** - Details of the updated draft. The exact structure depends on the API response for a successful update.
  
  ```
  
  ```

--------------------------------

### Send Data to Agentmail.to List - Python

Source: https://docs.agentmail.to/api-reference/pods/lists/create

This Python snippet demonstrates how to send data to a specific list within a pod using the Agentmail.to API. It utilizes the `requests` library for making the HTTP POST request. Ensure you have the `requests` library installed (`pip install requests`).

```python
import requests

url = "https://api.agentmail.to/v0/pods/pod_id/lists/send/allow"

payload = { "entry": "entry" }
headers = {
    "Authorization": "Bearer <api_key>",
    "Content-Type": "application/json"
}

response = requests.post(url, json=payload, headers=headers)

print(response.json())
```

--------------------------------

### Get Zone File using Agentmail API (Ruby)

Source: https://docs.agentmail.to/api-reference/domains/get-zone-file

A Ruby script to fetch a domain's zone file from the Agentmail API using Net::HTTP. It demonstrates setting the Authorization header with a bearer token.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/domains/%3Adomain_id/zone-file")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### Fetch Organizations using HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/organizations/get

This Go code snippet illustrates how to make a direct HTTP GET request to the AgentMail organizations endpoint, including setting the Authorization header. It uses standard Go libraries for HTTP requests.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/organizations"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### GET /v0/inboxes/{inbox_id}/messages/{message_id}/raw

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-raw

Retrieves the raw content of a specific email message from a given inbox. This endpoint is useful for accessing the full, unparsed email data.

```APIDOC
## GET /v0/inboxes/{inbox_id}/messages/{message_id}/raw

### Description
Retrieves the raw content of a specific email message from a given inbox. This endpoint is useful for accessing the full, unparsed email data.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/inboxes/{inbox_id}/messages/{message_id}/raw

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - ID of inbox.
- **message_id** (string) - Required - ID of message.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **binary** (string) - The raw content of the email message.

#### Response Example
```

(Raw email content will be returned here)

```
#### Error Response (404)
- **name** (string) - Name of the error.
- **message** (string) - Error message.

#### Error Response Example
```json
{
  "name": "ErrorName",
  "message": "ErrorMessage"
}
```

```
--------------------------------

### Get Organization Details (OpenAPI)

Source: https://docs.agentmail.to/api-reference/organizations/get

This OpenAPI specification defines the endpoint for retrieving organization details. It requires Bearer authentication and returns organization information including IDs, counts, limits, billing details, and timestamps.

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/organizations:
    get:
      operationId: get
      summary: Get Organization
      description: Get the current organization.
      tags:
        - subpackage_organizations
      parameters:
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_organizations:Organization'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_:OrganizationId:
      type: string
      description: ID of organization.
      title: OrganizationId
    type_organizations:Organization:
      type: object
      properties:
        organization_id:
          $ref: '#/components/schemas/type_:OrganizationId'
        inbox_count:
          type: integer
          description: Current number of inboxes.
        domain_count:
          type: integer
          description: Current number of domains.
        inbox_limit:
          type: integer
          description: Maximum number of inboxes allowed.
        domain_limit:
          type: integer
          description: Maximum number of domains allowed.
        billing_id:
          type: string
          description: Provider-agnostic billing customer ID.
        billing_type:
          type: string
          description: Billing provider type (e.g. "stripe").
        billing_subscription_id:
          type: string
          description: Active billing subscription ID.
        authentication_id:
          type: string
          description: Provider-agnostic authentication ID.
        authentication_type:
          type: string
          description: Authentication provider type.
        updated_at:
          type: string
          format: date-time
          description: Time at which organization was last updated.
        created_at:
          type: string
          format: date-time
          description: Time at which organization was created.
      required:
        - organization_id
        - inbox_count
        - domain_count
        - updated_at
        - created_at
      description: Organization details with usage limits and counts.
      title: Organization
  securitySchemes:
    Bearer:
      type: http
      scheme: bearer
```

--------------------------------

### GET /v0/pods/{pod_id}/drafts/{draft_id}

Source: https://docs.agentmail.to/api-reference/pods/drafts/get

Retrieves a specific draft associated with a pod. Requires authentication.

```APIDOC
## GET /v0/pods/{pod_id}/drafts/{draft_id}

### Description
Retrieves a specific draft using its pod ID and draft ID. This endpoint is used to fetch the content and metadata of a draft.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/drafts/{draft_id}

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - ID of the pod.
- **draft_id** (string) - Required - ID of the draft.

#### Query Parameters
None

#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Request Example
None (GET request with path parameters)

### Response
#### Success Response (200)
- **Draft** (object) - Contains the details of the draft, including fields like `draft_id`, `pod_id`, `inbox_id`, `thread_id`, `client_id`, `labels`, `reply_to`, `to`, `cc`, `bcc`, `subject`, `preview`, `text`, `html`, and `attachments`.

#### Response Example
```json
{
  "draft_id": "drf_abc123",
  "pod_id": "pod_xyz789",
  "inbox_id": "inb_def456",
  "thread_id": "thr_ghi789",
  "client_id": "cli_jkl012",
  "labels": ["important", "work"],
  "reply_to": ["support@example.com"],
  "to": ["recipient@example.com"],
  "cc": [],
  "bcc": [],
  "subject": "Meeting Follow-up",
  "preview": "Following up on our meeting...",
  "text": "Hello,\n\nFollowing up on our meeting...\n\nBest regards,",
  "html": "<p>Hello,</p><p>Following up on our meeting...</p><p>Best regards,</p>",
  "attachments": [
    {
      "attachment_id": "att_mno345",
      "filename": "report.pdf",
      "size": 102400,
      "content_type": "application/pdf",
      "content_disposition": "attachment",
      "content_id": null
    }
  ]
}
```

#### Error Response (404)

- **ErrorResponse** (object) - Contains error details when the draft or pod is not found.

#### Error Response Example

```json
{
  "error": {
    "code": "NOT_FOUND",
    "message": "Draft not found."
  }
}
```

```
--------------------------------

### Handle Customer Email with Intent Detection (Python)

Source: https://docs.agentmail.to/sales-agent-websocket

Processes incoming customer emails, tracks conversation history, detects customer intent via keyword matching, generates an AI response, and optionally notifies a manager. It uses a dictionary for intent keywords and a default intent of 'question'.

```python
async def handle_customer_email(inbox_id, message_id, thread_id, from_email, subject, body):
    # Track conversation history per thread
    if thread_id not in conversations:
        conversations[thread_id] = []
    conversations[thread_id].append({"role": "user", "content": body})

    # Detect intent with keyword matching
    intent_keywords = {
        'interested': ['interested', 'demo', 'meeting', 'tell me more'],
        'not_interested': ['not interested', 'no thank', 'maybe later'],
        'question': ['?', 'how', 'what', 'when', 'why']
    }

    intent = 'question'  # default
    for key, keywords in intent_keywords.items():
        if any(kw in body.lower() for kw in keywords):
            intent = key
            break

    # Generate contextual AI response using conversation history
    response = await get_ai_response(conversations[thread_id], system_prompt)

    # Reply to customer
    await reply_to_email(inbox_id, message_id, from_email, response)

    # Notify manager of strong signals
    if manager_email and intent in ['interested', 'not_interested']:
        await send_email(inbox_id, manager_email, f"Update: {from_email}",
            f"Customer is {intent}.\n\nTheir message:\n{body}")
```

--------------------------------

### GET /v0/lists/{direction}/{type}/{entry}

Source: https://docs.agentmail.to/api-reference/lists/get

Retrieves a specific list entry based on direction, type, and entry identifier. This endpoint is useful for checking if an email address or domain is present in your allow or block lists.

```APIDOC
## GET /v0/lists/{direction}/{type}/{entry}

### Description
Retrieves a specific list entry based on direction, type, and entry identifier. This endpoint is useful for checking if an email address or domain is present in your allow or block lists.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/lists/{direction}/{type}/{entry}

### Parameters
#### Path Parameters
- **direction** (string) - Required - Direction of list entry. Enum: `send`, `receive`.
- **type** (string) - Required - Type of list entry. Enum: `allow`, `block`.
- **entry** (string) - Required - Email address or domain.

#### Query Parameters
None

#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Request Example
```

GET https://api.agentmail.to/v0/lists/send/allow/example.com
Authorization: Bearer YOUR_API_TOKEN

```
### Response
#### Success Response (200)
- **entry** (string) - Email address or domain of list entry.
- **organization_id** (string) - ID of organization.
- **reason** (string) - Reason for adding the entry.
- **direction** (string) - Direction of list entry. Enum: `send`, `receive`.
- **list_type** (string) - Type of list entry. Enum: `allow`, `block`.
- **entry_type** (string) - Whether the entry is an email address or domain. Enum: `email`, `domain`.
- **created_at** (string) - Time at which entry was created.

#### Response Example
```json
{
  "entry": "example.com",
  "organization_id": "org_12345",
  "reason": "Spam domain",
  "direction": "send",
  "list_type": "block",
  "entry_type": "domain",
  "created_at": "2023-10-27T10:00:00Z"
}
```

#### Error Response (404)

- **name** (string) - Name of error.
- **message** (string) - Error message.

#### Error Response Example

```json
{
  "name": "NotFound",
  "message": "List entry not found."
}
```

```
--------------------------------

### Update Webhook via HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/webhooks/update

This Go code example demonstrates how to update a webhook by making a direct HTTP PATCH request to the AgentMail API. It includes setting the Authorization header with a Bearer token and the Content-Type to application/json. The payload is an empty JSON object.

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/webhooks/webhook_id"

    payload := strings.NewReader("{}")

    req, _ := http.NewRequest("PATCH", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Idempotent Inbox Creation with `client_id`

Source: https://docs.agentmail.to/webhook-agent

Ensures that creating an inbox or webhook is idempotent by using a `client_id`. If the operation has been performed before with the same `client_id`, the API returns the existing resource instead of creating a duplicate. This makes scripts robust and safe to re-run.

```python
client.inboxes.create(client_id="your_unique_client_id")
```

--------------------------------

### List API Keys via HTTP Request (C#)

Source: https://docs.agentmail.to/api-reference/api-keys/list

This C# code demonstrates how to fetch API keys from AgentMail using an HTTP GET request with the RestSharp library. It includes setting the necessary authorization header.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/api-keys");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

--------------------------------

### GET /v0/pods/{pod_id}/threads/{thread_id}/attachments/{attachment_id}

Source: https://docs.agentmail.to/api-reference/pods/threads/get-attachment

This endpoint retrieves a specific attachment from a thread within a pod. It requires the pod ID, thread ID, and attachment ID as path parameters, and an API key for authentication.

```APIDOC
## GET /v0/pods/{pod_id}/threads/{thread_id}/attachments/{attachment_id}

### Description
Retrieves a specific attachment from a thread within a pod.

### Method
GET

### Endpoint
`/v0/pods/{pod_id}/threads/{thread_id}/attachments/{attachment_id}`

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The ID of the pod.
- **thread_id** (string) - Required - The ID of the thread.
- **attachment_id** (string) - Required - The ID of the attachment.

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

- **body** (binary) - The content of the attachment.

#### Response Example

```json
{
  "example": "Binary content of the attachment."
}
```

```
--------------------------------

### GET /v0/pods

Source: https://docs.agentmail.to/api-reference/pods/list

Retrieves a list of pods. Supports pagination and filtering.

```APIDOC
## GET /v0/pods

### Description
Retrieves a list of pods. Supports pagination and filtering.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/pods

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - Limit of number of items returned.
- **page_token** (string) - Optional - Page token for pagination.

#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Request Example
```json
{
  "example": ""
}
```

### Response

#### Success Response (200)

- **count** (integer) - Number of items returned.
- **limit** (integer) - Limit of number of items returned.
- **next_page_token** (string) - Page token for the next page of results.
- **pods** (array) - Ordered by `created_at` descending. Contains a list of pod objects.
   - **pod_id** (string) - ID of pod.
   - **name** (string) - Name of pod.
   - **updated_at** (string) - Time at which pod was last updated.
   - **created_at** (string) - Time at which pod was created.
   - **client_id** (string) - Client ID of pod.

#### Response Example

```json
{
  "count": 10,
  "limit": 10,
  "next_page_token": "some_token",
  "pods": [
    {
      "pod_id": "pod_123",
      "name": "My First Pod",
      "updated_at": "2023-10-27T10:00:00Z",
      "created_at": "2023-10-26T09:00:00Z",
      "client_id": "client_abc"
    }
  ]
}
```

```
--------------------------------

### GET /inboxes/{inbox_id}/metrics

Source: https://docs.agentmail.to/changelog/2025/8/13

Retrieves metrics for a specific inbox.

```APIDOC
## GET /inboxes/{inbox_id}/metrics

### Description
Retrieves metrics for a specific inbox. This endpoint allows you to monitor the performance and deliverability of emails sent through a particular inbox.

### Method
GET

### Endpoint
/inboxes/{inbox_id}/metrics

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox to retrieve metrics for.

#### Query Parameters
- **start_time** (integer) - Optional - The start of the time range for the metrics in Unix epoch time.
- **end_time** (integer) - Optional - The end of the time range for the metrics in Unix epoch time.

### Request Example
```json
{
  "example": "GET /inboxes/in_abc123/metrics?start_time=1678886400&end_time=1678972800"
}
```

### Response

#### Success Response (200)

- **sent** (integer) - The total number of emails sent from this inbox.
- **delivered** (integer) - The total number of emails successfully delivered from this inbox.
- **bounced** (integer) - The total number of emails that bounced from this inbox.
- **rejected** (integer) - The total number of emails that were rejected from this inbox.
- **complaints** (integer) - The total number of spam complaints received for this inbox.
- **spam_reports** (integer) - The total number of spam reports received for this inbox.

#### Response Example

```json
{
  "example": {
    "sent": 5000,
    "delivered": 4900,
    "bounced": 75,
    "rejected": 25,
    "complaints": 10,
    "spam_reports": 5
  }
}
```

```
--------------------------------

### GET /v0/pods/{pod_id}/drafts

Source: https://docs.agentmail.to/api-reference/pods/drafts/list

Fetches a list of all draft emails for a specified pod. This is useful for managing and reviewing unsent emails.

```APIDOC
## GET /v0/pods/{pod_id}/drafts

### Description
Retrieves a list of draft emails associated with a specific pod.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/drafts

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The unique identifier of the pod.

### Request Example
```

GET https://api.agentmail.to/v0/pods/your_pod_id/drafts

```
### Response
#### Success Response (200)
- **drafts** (array) - A list of draft email objects.
  - **id** (string) - The unique identifier of the draft.
  - **subject** (string) - The subject line of the draft email.
  - **createdAt** (string) - The timestamp when the draft was created.
  - **updatedAt** (string) - The timestamp when the draft was last updated.

#### Response Example
```json
{
  "drafts": [
    {
      "id": "draft_abc123",
      "subject": "Meeting Follow-up",
      "createdAt": "2023-10-27T10:00:00Z",
      "updatedAt": "2023-10-27T10:30:00Z"
    },
    {
      "id": "draft_def456",
      "subject": "New Project Proposal",
      "createdAt": "2023-10-26T15:00:00Z",
      "updatedAt": "2023-10-26T15:15:00Z"
    }
  ]
}
```

```
--------------------------------

### Retrieve List Entry Allow - Swift SDK

Source: https://docs.agentmail.to/api-reference/lists/get

This Swift code demonstrates how to retrieve list entry allowance using URLSession. It sets up an NSMutableURLRequest for a GET method, includes the Authorization header, and initiates a data task to communicate with the Agentmail.to API. Error handling for network requests is included.

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/lists/send/allow/entry")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### Create Draft via HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/create

This Go code snippet shows how to create a draft by making a direct HTTP POST request to the AgentMail API. It includes setting the Authorization header with a Bearer token and Content-Type to application/json.

```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/drafts"

    payload := strings.NewReader("{}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Authorization", "Bearer <api_key>")
    req.Header.Add("Content-Type", "application/json")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Send Data to Agentmail.to API (Python)

Source: https://docs.agentmail.to/api-reference/lists/create

This Python snippet uses the 'requests' library to send a POST request to the Agentmail.to API. It includes setting the API key in the Authorization header and the JSON payload. Ensure you have the 'requests' library installed (`pip install requests`).

```python
import requests

url = "https://api.agentmail.to/v0/lists/send/allow"

payload = { "entry": "entry" }
headers = {
    "Authorization": "Bearer <api_key>",
    "Content-Type": "application/json"
}

response = requests.post(url, json=payload, headers=headers)

print(response.json())
```

--------------------------------

### Check AgentMail Version (Bash)

Source: https://docs.agentmail.to/sales-agent-websocket

Command to check the installed version of the agentmail Python package. Ensures that the version meets the minimum requirement for WebSocket support.

```bash
pip show agentmail
```

--------------------------------

### Fetch Domain Information using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/domains/get

Demonstrates how to retrieve domain details using the AgentMail client. Requires an API key for authentication. Handles API requests and responses.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.domains.get("domain_id");
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.domains.get(
    domain_id="domain_id"
)
```

--------------------------------

### GET /v0/threads/{thread_id}/attachments/{attachment_id}

Source: https://docs.agentmail.to/api-reference/threads/get-attachment

Retrieves a specific attachment from a given thread. Requires authentication.

```APIDOC
## GET /v0/threads/{thread_id}/attachments/{attachment_id}

### Description
Retrieves a specific attachment from a given thread. This endpoint requires authentication via a Bearer token.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/threads/{thread_id}/attachments/{attachment_id}

### Parameters
#### Path Parameters
- **thread_id** (string) - Required - ID of the thread.
- **attachment_id** (string) - Required - ID of the attachment.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **attachment_id** (string) - The ID of the attachment.
- **filename** (string) - The filename of the attachment.
- **size** (integer) - The size of the attachment in bytes.
- **content_type** (string) - The content type of the attachment.
- **content_disposition** (string) - The content disposition of the attachment (inline or attachment).
- **content_id** (string) - The content ID of the attachment.
- **download_url** (string) - A URL to download the attachment.
- **expires_at** (string) - The time at which the download URL expires (ISO 8601 format).

#### Response Example
```json
{
  "attachment_id": "att_abc123",
  "filename": "document.pdf",
  "size": 102400,
  "content_type": "application/pdf",
  "content_disposition": "attachment",
  "content_id": "cid:part1.0001@example.com",
  "download_url": "https://api.agentmail.to/download/att_abc123?token=...",
  "expires_at": "2023-10-27T10:30:00Z"
}
```

#### Error Response (404)

- **name** (string) - The name of the error.
- **message** (string) - A descriptive message for the error.

```json
{
  "name": "NotFoundError",
  "message": "Attachment not found."
}
```

```
--------------------------------

### Forward Message using AgentMail SDK (TypeScript)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/forward

Demonstrates how to forward a message using the AgentMail TypeScript SDK. It initializes the client with an API key and calls the forward method on the messages resource.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.messages.forward("inbox_id", "message_id", {});
}
main();
```

--------------------------------

### Send Data to Agentmail.to API (JavaScript)

Source: https://docs.agentmail.to/api-reference/lists/create

This JavaScript example uses the `fetch` API to send a POST request to the Agentmail.to API. It demonstrates setting the API key in the Authorization header and the JSON payload. This code is suitable for browser or Node.js environments that support `fetch`.

```javascript
const url = 'https://api.agentmail.to/v0/lists/send/allow';
const options = {
  method: 'POST',
  headers: {Authorization: 'Bearer <api_key>', 'Content-Type': 'application/json'},
  body: '{"entry":"entry"}'
};

try {
  const response = await fetch(url, options);
  const data = await response.json();
  console.log(data);
} catch (error) {
  console.error(error);
}
```

--------------------------------

### Forward Message via HTTP API (PHP)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/forward

This PHP example uses the Guzzle HTTP client to forward a message by making a POST request to the AgentMail API. It configures the request with headers and the JSON body.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('POST', 'https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/forward', [
  'body' => '{}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

--------------------------------

### GET /v0/pods/{pod_id}/drafts/{draft_id}

Source: https://docs.agentmail.to/api-reference/pods/drafts/get

Fetches a specific draft email from a pod. You need to provide both the pod ID and the draft ID to identify the draft.

```APIDOC
## GET /v0/pods/{pod_id}/drafts/{draft_id}

### Description
Retrieves a specific draft email within a pod using its ID.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/drafts/{draft_id}

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The unique identifier for the pod.
- **draft_id** (string) - Required - The unique identifier for the draft email.

### Request Example
```

GET https://api.agentmail.to/v0/pods/your_pod_id/drafts/your_draft_id

```
### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the draft.
- **pod_id** (string) - The identifier of the pod the draft belongs to.
- **subject** (string) - The subject line of the draft email.
- **body** (string) - The HTML content of the draft email.
- **created_at** (string) - Timestamp when the draft was created.
- **updated_at** (string) - Timestamp when the draft was last updated.

#### Response Example
```json
{
  "id": "draft_abc123",
  "pod_id": "pod_xyz789",
  "subject": "Meeting Follow-up",
  "body": "<p>Hi Team,</p><p>Following up on our meeting...</p>",
  "created_at": "2023-10-27T10:00:00Z",
  "updated_at": "2023-10-27T10:30:00Z"
}
```

```
--------------------------------

### List Inboxes using AgentMail SDK

Source: https://docs.agentmail.to/api-reference/inboxes/list

Demonstrates how to list inboxes using the AgentMail SDK. Requires the agentmail library. Handles API key authentication and makes a GET request to the inboxes endpoint.

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.inboxes.list({});
}
main();
```

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.list()
```

--------------------------------

### Fetch Inbox Data via HTTP Request

Source: https://docs.agentmail.to/api-reference/inboxes/get

Shows how to fetch inbox data by making a direct HTTP GET request to the AgentMail API endpoint. This method requires manual construction of the request, including setting the Authorization header. It's useful when an official SDK is not available or preferred.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/inboxes/inbox_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/inboxes/inbox_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/inboxes/inbox_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### GET /v0/pods/{pod_id}/lists/{direction}/{type}/{entry}

Source: https://docs.agentmail.to/api-reference/pods/lists/get

Retrieves a specific list entry from a pod based on direction, type, and entry identifier. This endpoint is useful for checking the status or details of an email address or domain within a specific list.

```APIDOC
## GET /v0/pods/{pod_id}/lists/{direction}/{type}/{entry}

### Description
Retrieves a specific list entry from a pod based on direction, type, and entry identifier. This endpoint is useful for checking the status or details of an email address or domain within a specific list.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/pods/{pod_id}/lists/{direction}/{type}/{entry}

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - ID of pod.
- **direction** (string) - Required - Direction of list entry. Enum: `send`, `receive`.
- **type** (string) - Required - Type of list entry. Enum: `allow`, `block`.
- **entry** (string) - Required - Email address or domain.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **entry** (string) - Email address or domain of list entry.
- **organization_id** (string) - ID of organization.
- **reason** (string) - Reason for adding the entry.
- **direction** (string) - Direction of list entry.
- **list_type** (string) - Type of list entry.
- **entry_type** (string) - Whether the entry is an email address or domain.
- **created_at** (string) - Time at which entry was created.
- **pod_id** (string) - ID of pod.
- **inbox_id** (string) - ID of inbox, if entry is inbox-scoped.

#### Response Example
```json
{
  "entry": "example.com",
  "organization_id": "org_12345",
  "reason": "Spam",
  "direction": "receive",
  "list_type": "block",
  "entry_type": "domain",
  "created_at": "2023-10-27T10:00:00Z",
  "pod_id": "pod_abcde",
  "inbox_id": "inbox_fghij"
}
```

#### Error Response (404)

- **name** (string) - Name of error.
- **message** (string) - Error message.

#### Error Response Example

```json
{
  "name": "NotFound",
  "message": "List entry not found."
}
```

```
--------------------------------

### OpenAPI Specification for Get Attachment

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

This OpenAPI 3.1.0 specification defines the 'get-attachment' operation. It outlines the request parameters (inbox_id, message_id, attachment_id, Authorization header) and the possible responses (200 OK with attachment details, 404 Not Found with error details).

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/inboxes/{inbox_id}/messages/{message_id}/attachments/{attachment_id}:
    get:
      operationId: get-attachment
      summary: Get Attachment
      tags:
        - subpackage_inboxes.subpackage_inboxes/messages
      parameters:
        - name: inbox_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_inboxes:InboxId'
        - name: message_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_messages:MessageId'
        - name: attachment_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_attachments:AttachmentId'
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_attachments:AttachmentResponse'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_inboxes:InboxId:
      type: string
      description: ID of inbox.
      title: InboxId
    type_messages:MessageId:
      type: string
      description: ID of message.
      title: MessageId
    type_attachments:AttachmentId:
      type: string
      description: ID of attachment.
      title: AttachmentId
    type_attachments:AttachmentFilename:
      type: string
      description: Filename of attachment.
      title: AttachmentFilename
    type_attachments:AttachmentSize:
      type: integer
      description: Size of attachment in bytes.
      title: AttachmentSize
    type_attachments:AttachmentContentType:
      type: string
      description: Content type of attachment.
      title: AttachmentContentType
    type_attachments:AttachmentContentDisposition:
      type: string
      enum:
        - inline
        - attachment
      description: Content disposition of attachment.
      title: AttachmentContentDisposition
    type_attachments:AttachmentContentId:
      type: string
      description: Content ID of attachment.
      title: AttachmentContentId
    type_attachments:AttachmentResponse:
      type: object
      properties:
        attachment_id:
          $ref: '#/components/schemas/type_attachments:AttachmentId'
        filename:
          $ref: '#/components/schemas/type_attachments:AttachmentFilename'
        size:
          $ref: '#/components/schemas/type_attachments:AttachmentSize'
        content_type:
          $ref: '#/components/schemas/type_attachments:AttachmentContentType'
        content_disposition:
          $ref: '#/components/schemas/type_attachments:AttachmentContentDisposition'
        content_id:
          $ref: '#/components/schemas/type_attachments:AttachmentContentId'
        download_url:
          type: string
          description: URL to download the attachment.
        expires_at:
          type: string
          format: date-time
          description: Time at which the download URL expires.
      required:
        - attachment_id
        - size
        - download_url
        - expires_at
      title: AttachmentResponse
    type_:ErrorName:
      type: string
      description: Name of error.
      title: ErrorName
    type_:ErrorMessage:
      type: string
      description: Error message.
      title: ErrorMessage
    type_:ErrorResponse:
      type: object
      properties:
        name:
          $ref: '#/components/schemas/type_:ErrorName'
        message:
          $ref: '#/components/schemas/type_:ErrorMessage'
      required:
        - name
        - message
      title: ErrorResponse
  securitySchemes:
    Bearer:
      type: http
      scheme: bearer
```

--------------------------------

### Retrieve Message Attachment with Java HTTP Client

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

Demonstrates fetching a message attachment from AgentMail using Java's Unirest library. This code performs an HTTP GET request to the API endpoint, including the required 'Authorization' header. The response is captured as a String.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/attachments/attachment_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### GET /v0/drafts/{draft_id}

Source: https://docs.agentmail.to/api-reference/drafts/get

Fetches the details of a specific draft email. You need to provide the `draft_id` in the URL path.

```APIDOC
## GET /v0/drafts/{draft_id}

### Description
Retrieves the content and metadata of a specific draft email.

### Method
GET

### Endpoint
/v0/drafts/{draft_id}

### Parameters
#### Path Parameters
- **draft_id** (string) - Required - The unique identifier of the draft email to retrieve.

### Request Example
```

GET https://api.agentmail.to/v0/drafts/your_draft_id_here

```
### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the draft.
- **subject** (string) - The subject line of the draft email.
- **body** (string) - The HTML content of the draft email.
- **to** (array of strings) - A list of recipient email addresses.
- **cc** (array of strings) - A list of CC recipient email addresses.
- **bcc** (array of strings) - A list of BCC recipient email addresses.
- **createdAt** (string) - The timestamp when the draft was created.
- **updatedAt** (string) - The timestamp when the draft was last updated.

#### Response Example
```json
{
  "id": "draft_abc123",
  "subject": "Meeting Follow-up",
  "body": "<p>Hi team,</p><p>Following up on our meeting...</p>",
  "to": ["recipient@example.com"],
  "cc": [],
  "bcc": [],
  "createdAt": "2023-10-27T10:00:00Z",
  "updatedAt": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### Get Webhook Information (API Reference)

Source: https://docs.agentmail.to/api-reference/webhooks/get

This snippet shows the HTTP GET request to retrieve a specific webhook's details using its ID. It requires an Authorization header with a Bearer token. The response includes webhook configuration such as URL, event types, and creation/update timestamps.

```http
GET https://api.agentmail.to/v0/webhooks/{webhook_id}
Authorization: Bearer YOUR_API_TOKEN
```

--------------------------------

### POST /v0/pods/{pod_id}/domains

Source: https://docs.agentmail.to/api-reference/pods/domains/create

Creates a new domain for a given pod. Requires authentication and provides details about the created domain upon success.

```APIDOC
## POST /v0/pods/{pod_id}/domains

### Description
Creates a new domain associated with a specific pod. This endpoint is used to register a new domain and configure its feedback settings.

### Method
POST

### Endpoint
/v0/pods/{pod_id}/domains

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The ID of the pod to which the domain will be added.

#### Header Parameters
- **Authorization** (string) - Required - Bearer token for authentication.

#### Request Body
- **domain** (string) - Required - The name of the domain to create (e.g., "example.com").
- **feedback_enabled** (boolean) - Required - Specifies whether bounce and complaint notifications should be sent to your inboxes.

### Request Example
```json
{
  "domain": "example.com",
  "feedback_enabled": true
}
```

### Response

#### Success Response (200)

- **pod_id** (string) - The ID of the pod.
- **domain_id** (string) - The unique identifier for the created domain.
- **status** (string) - The verification status of the domain (e.g., NOT_STARTED, PENDING, VERIFIED).
- **feedback_enabled** (boolean) - Indicates if feedback notifications are enabled.
- **records** (array) - A list of DNS records required for domain verification.
   - **type** (string) - The type of the DNS record (e.g., TXT, CNAME, MX).
   - **name** (string) - The name or host of the record.
   - **value** (string) - The value of the record.
   - **status** (string) - The verification status of this specific record (e.g., MISSING, INVALID, VALID).
   - **priority** (integer) - The priority of the MX record (if applicable).
- **client_id** (string) - The client ID associated with the domain.
- **updated_at** (string) - The timestamp when the domain was last updated.
- **created_at** (string) - The timestamp when the domain was created.

#### Response Example

```json
{
  "pod_id": "your-pod-id",
  "domain_id": "your-domain-id",
  "status": "VERIFIED",
  "feedback_enabled": true,
  "records": [
    {
      "type": "TXT",
      "name": "_domainkey",
      "value": "v=DKIM1; k=rsa; p=...",
      "status": "VALID",
      "priority": null
    }
  ],
  "client_id": "your-client-id",
  "updated_at": "2023-10-27T10:00:00Z",
  "created_at": "2023-10-27T09:00:00Z"
}
```

#### Error Response (400)

- **name** (string) - The name of the error.
- **errors** (object) - A detailed object containing validation errors.

#### Error Response Example

```json
{
  "name": "ValidationError",
  "errors": {
    "domain": "Domain is already registered."
  }
}
```

```
--------------------------------

### Retrieve Draft Attachment (OpenAPI)

Source: https://docs.agentmail.to/api-reference/drafts/get-attachment

This OpenAPI specification defines the GET endpoint for retrieving a specific attachment from an email draft. It outlines the required path parameters (draft_id, attachment_id), authentication headers, and the structure of the successful response (AttachmentResponse) and error response (ErrorResponse).

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/drafts/{draft_id}/attachments/{attachment_id}:
    get:
      operationId: get-attachment
      summary: Get Attachment
      tags:
        - subpackage_drafts
      parameters:
        - name: draft_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_drafts:DraftId'
        - name: attachment_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_attachments:AttachmentId'
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_attachments:AttachmentResponse'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_drafts:DraftId:
      type: string
      description: ID of draft.
      title: DraftId
    type_attachments:AttachmentId:
      type: string
      description: ID of attachment.
      title: AttachmentId
    type_attachments:AttachmentFilename:
      type: string
      description: Filename of attachment.
      title: AttachmentFilename
    type_attachments:AttachmentSize:
      type: integer
      description: Size of attachment in bytes.
      title: AttachmentSize
    type_attachments:AttachmentContentType:
      type: string
      description: Content type of attachment.
      title: AttachmentContentType
    type_attachments:AttachmentContentDisposition:
      type: string
      enum:
        - inline
        - attachment
      description: Content disposition of attachment.
      title: AttachmentContentDisposition
    type_attachments:AttachmentContentId:
      type: string
      description: Content ID of attachment.
      title: AttachmentContentId
    type_attachments:AttachmentResponse:
      type: object
      properties:
        attachment_id:
          $ref: '#/components/schemas/type_attachments:AttachmentId'
        filename:
          $ref: '#/components/schemas/type_attachments:AttachmentFilename'
        size:
          $ref: '#/components/schemas/type_attachments:AttachmentSize'
        content_type:
          $ref: '#/components/schemas/type_attachments:AttachmentContentType'
        content_disposition:
          $ref: '#/components/schemas/type_attachments:AttachmentContentDisposition'
        content_id:
          $ref: '#/components/schemas/type_attachments:AttachmentContentId'
        download_url:
          type: string
          description: URL to download the attachment.
        expires_at:
          type: string
          format: date-time
          description: Time at which the download URL expires.
      required:
        - attachment_id
        - size
        - download_url
        - expires_at
      title: AttachmentResponse
    type_:ErrorName:
      type: string
      description: Name of error.
      title: ErrorName
    type_:ErrorMessage:
      type: string
      description: Error message.
      title: ErrorMessage
    type_:ErrorResponse:
      type: object
      properties:
        name:
          $ref: '#/components/schemas/type_:ErrorName'
        message:
          $ref: '#/components/schemas/type_:ErrorMessage'
      required:
        - name
        - message
      title: ErrorResponse
  securitySchemes:
    Bearer:
      type: http
      scheme: bearer
```

--------------------------------

### Fetch Metrics via HTTP Request (Go)

Source: https://docs.agentmail.to/api-reference/metrics/list

This Go code snippet shows how to fetch metrics by making a direct HTTP GET request to the AgentMail API. It includes setting the Authorization header and reading the response body. The API key needs to be manually inserted.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/metrics?start_timestamp=2024-01-15T09%3A30%3A00Z&end_timestamp=2024-01-15T09%3A30%3A00Z"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### Create Pod via HTTP POST Request (C#)

Source: https://docs.agentmail.to/api-reference/pods/create

This C# code uses the RestSharp library to perform an HTTP POST request to create a pod. It configures the RestClient with the API endpoint, sets the POST method, adds the Authorization and Content-Type headers, and specifies the request body. The response is then executed.

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods");
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer <api_key>");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("application/json", "{}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

--------------------------------

### Delete Domain with Go HTTP Client

Source: https://docs.agentmail.to/api-reference/domains/delete

This Go code example shows how to delete a domain using the standard net/http package. It constructs the DELETE request, sets the Authorization header, and sends the request to the Agentmail API.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/domains/domain_id"

    req, _ := http.NewRequest("DELETE", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### GET /v0/inboxes/{inbox_id}/drafts/{draft_id}

Source: https://docs.agentmail.to/api-reference/inboxes/drafts/get

Retrieves a specific draft from an inbox. Requires authentication with an API key.

```APIDOC
## GET /v0/inboxes/{inbox_id}/drafts/{draft_id}

### Description
Retrieves a specific draft from an inbox using its unique IDs. This endpoint is used to fetch the content and metadata of a draft email.

### Method
GET

### Endpoint
`/v0/inboxes/{inbox_id}/drafts/{draft_id}`

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The ID of the inbox containing the draft.
- **draft_id** (string) - Required - The ID of the draft to retrieve.

#### Query Parameters
None

#### Request Body
None

### Request Example
```

GET /v0/inboxes/inbox_id/drafts/draft_id HTTP/1.1
Host: api.agentmail.to
Authorization: Bearer <api_key>

```
### Response
#### Success Response (200)
- **content** (string) - The content of the draft email.
- **subject** (string) - The subject line of the draft.
- **to** (array of strings) - Recipients of the draft.
- **cc** (array of strings) - CC recipients of the draft.
- **bcc** (array of strings) - BCC recipients of the draft.
- **createdAt** (string) - Timestamp when the draft was created.
- **updatedAt** (string) - Timestamp when the draft was last updated.

#### Response Example
```json
{
  "content": "<html><body><p>This is a draft email.</p></body></html>",
  "subject": "Meeting Follow-up",
  "to": ["recipient@example.com"],
  "cc": [],
  "bcc": [],
  "createdAt": "2023-10-27T10:00:00Z",
  "updatedAt": "2023-10-27T10:05:00Z"
}
```

```
--------------------------------

### List Inbox Threads using AgentMail API (PHP)

Source: https://docs.agentmail.to/api-reference/inboxes/threads/list

A PHP example using the Guzzle HTTP client to fetch inbox threads from the AgentMail API. It sets the Authorization header for authentication.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/inboxes/inbox_id/threads', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### GET /v0/threads/{thread_id}/attachments/{attachment_id}

Source: https://docs.agentmail.to/api-reference/threads/get-attachment

Retrieves a specific attachment from a thread. Requires authentication with a Bearer token.

```APIDOC
## GET /v0/threads/{thread_id}/attachments/{attachment_id}

### Description
Retrieves a specific attachment from a thread using its unique thread ID and attachment ID.

### Method
GET

### Endpoint
`/v0/threads/{thread_id}/attachments/{attachment_id}`

### Parameters
#### Path Parameters
- **thread_id** (string) - Required - The unique identifier for the thread.
- **attachment_id** (string) - Required - The unique identifier for the attachment.

#### Query Parameters
None

#### Request Body
None

### Request Example
```

GET /v0/threads/thread_id/attachments/attachment_id HTTP/1.1
Host: api.agentmail.to
Authorization: Bearer <api_key>

```
### Response
#### Success Response (200)
- **body** (binary) - The content of the attachment.

#### Response Example
(Binary data representing the attachment)
```

--------------------------------

### Create and Manage Pods using AgentMail SDK

Source: https://docs.agentmail.to/changelog/2025/6/15

Demonstrates how to use the AgentMail SDK to create a new pod, add an inbox to it, and list all existing pods. This requires an API key for authentication. The SDK handles the communication with the AgentMail API.

```python
from agentmail import AgentMail

client = AgentMail(api_key="your-api-key")

# create a pod for your sales team
pod = client.pods.create(
    name="Sales Team",
    description="Shared resources for sales agents"
)

# create an inbox in the pod
inbox = client.pods.inboxes.create(
    pod_id=pod.pod_id,
    inbox_id="sales@example.com"
)

# list all pods
pods = client.pods.list()
for pod in pods.pods:
    print(f"Pod: {pod.name} ({len(pod.inbox_ids)} inboxes)")
```

```typescript
import { AgentMail } from "agentmail";

const client = new AgentMail({ apiKey: "your-api-key" });

// create a pod for your sales team
const pod = await client.pods.create({
  name: "Sales Team",
  description: "Shared resources for sales agents",
});

// create an inbox in the pod
await client.pods.inboxes.create(pod.podId, "sales@example.com");

// list all pods
const { pods } = await client.pods.list();
for (const p of pods) {
  console.log(`Pod: ${p.name} (${p.inboxIds?.length ?? 0} inboxes)`);
}
```

--------------------------------

### List Pod Threads via HTTP (PHP)

Source: https://docs.agentmail.to/api-reference/pods/threads/list

This PHP snippet uses the Guzzle HTTP client to fetch threads from a pod. It sends a GET request to the AgentMail API endpoint, including the necessary Bearer token in the Authorization header.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/pods/pod_id/threads', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

--------------------------------

### Update Webhook via HTTP Request (Swift)

Source: https://docs.agentmail.to/api-reference/webhooks/update

This Swift code example demonstrates updating a webhook using URLSession. It constructs an NSMutableURLRequest with the PATCH method, sets the required headers, and includes an empty JSON body. The request is then executed asynchronously.

```swift
import Foundation

let headers = [
  "Authorization": "Bearer <api_key>",
  "Content-Type": "application/json"
]
let parameters = [] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/webhooks/webhook_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "PATCH"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### GET /v0/pods/{pod_id}/inboxes/{inbox_id}

Source: https://docs.agentmail.to/api-reference/pods/inboxes/get

Retrieves details for a specific inbox within a pod. Requires authentication.

```APIDOC
## GET /v0/pods/{pod_id}/inboxes/{inbox_id}

### Description
Retrieves details for a specific inbox within a pod. This endpoint allows you to fetch information about an existing inbox, including its ID, display name, client ID, and timestamps.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/inboxes/{inbox_id}

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - ID of the pod.
- **inbox_id** (string) - Required - ID of the inbox.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **pod_id** (string) - The ID of the pod.
- **inbox_id** (string) - The ID of the inbox.
- **display_name** (string) - The display name of the inbox in the format `Display Name <username@domain.com>`.
- **client_id** (string) - The client ID associated with the inbox.
- **updated_at** (string) - The time at which the inbox was last updated (ISO 8601 format).
- **created_at** (string) - The time at which the inbox was created (ISO 8601 format).

#### Response Example
```json
{
  "pod_id": "pod_abc123",
  "inbox_id": "inbox_xyz789",
  "display_name": "Support Team <support@example.com>",
  "client_id": "client_def456",
  "updated_at": "2023-10-27T10:00:00Z",
  "created_at": "2023-10-26T09:00:00Z"
}
```

#### Error Response (404)

- **name** (string) - The name of the error.
- **message** (string) - A descriptive message about the error.

#### Error Response Example

```json
{
  "name": "NotFoundError",
  "message": "Inbox not found."
}
```

### Headers

- **Authorization** (string) - Required - Bearer token for authentication.
  
  ```
  
  ```

--------------------------------

### List API Keys via HTTP Request (Java)

Source: https://docs.agentmail.to/api-reference/api-keys/list

This Java code snippet shows how to retrieve API keys using an HTTP GET request to the AgentMail API. It utilizes the Unirest library for simplified HTTP calls.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/api-keys")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### GET /v0/threads

Source: https://docs.agentmail.to/api-reference/threads/list

Retrieves a list of all threads associated with the authenticated account. This endpoint is useful for fetching an overview of all conversations.

```APIDOC
## GET /v0/threads

### Description
Retrieves a list of all threads associated with the authenticated account.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/threads

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of threads to return.
- **offset** (integer) - Optional - The number of threads to skip before starting to collect the result set.
- **sort** (string) - Optional - The field to sort the threads by. Possible values: `created_at`, `updated_at`.
- **order** (string) - Optional - The order of sorting. Possible values: `asc`, `desc`. Defaults to `desc`.

### Request Example
```

GET https://api.agentmail.to/v0/threads?limit=10&sort=updated_at&order=asc

```
### Response
#### Success Response (200)
- **threads** (array) - A list of thread objects.
  - **id** (string) - The unique identifier for the thread.
  - **subject** (string) - The subject line of the thread.
  - **created_at** (string) - The timestamp when the thread was created.
  - **updated_at** (string) - The timestamp when the thread was last updated.
  - **last_message_id** (string) - The ID of the last message in the thread.
  - **participant_ids** (array) - A list of participant IDs in the thread.

#### Response Example
```json
{
  "threads": [
    {
      "id": "thread_abc123",
      "subject": "Inquiry about product features",
      "created_at": "2023-10-27T10:00:00Z",
      "updated_at": "2023-10-27T11:30:00Z",
      "last_message_id": "msg_xyz789",
      "participant_ids": ["user_1", "agent_a"]
    }
  ]
}
```

```
--------------------------------

### GET /v0/pods/{pod_id}/threads

Source: https://docs.agentmail.to/api-reference/pods/threads/list

Retrieves a list of threads associated with a specific pod. Supports filtering, sorting, and pagination.

```APIDOC
## GET /v0/pods/{pod_id}/threads

### Description
Retrieves a list of threads associated with a specific pod. This endpoint allows for filtering threads by labels, time range, and inclusion of spam or blocked messages. It also supports pagination and sorting.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/threads

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - ID of the pod.

#### Query Parameters
- **limit** (integer) - Optional - Limit of number of items returned.
- **page_token** (string) - Optional - Page token for pagination.
- **labels** (array of strings) - Optional - Labels to filter by.
- **before** (string) - Optional - Timestamp before which to filter by (ISO 8601 format).
- **after** (string) - Optional - Timestamp after which to filter by (ISO 8601 format).
- **ascending** (boolean) - Optional - Sort in ascending temporal order.
- **include_spam** (boolean) - Optional - Include spam in results.
- **include_blocked** (boolean) - Optional - Include blocked in results.

#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Request Example
```

GET /v0/pods/your_pod_id/threads?limit=20&labels=important&ascending=true
Authorization: Bearer YOUR_ACCESS_TOKEN

```
### Response
#### Success Response (200)
- **threads** (array) - List of threads.
  - **id** (string) - ID of the thread.
  - **labels** (array of strings) - Labels of the thread.
  - **subject** (string) - Subject of the thread.
  - **sent_timestamp** (string) - Timestamp of the last sent message.
  - **received_timestamp** (string) - Timestamp of the last received message.
  - **senders** (array of strings) - Senders in the thread.
  - **recipients** (array of strings) - Recipients in the thread.
- **next_page_token** (string) - Token for the next page of results.

#### Error Response (404)
- **code** (integer) - Error code.
- **message** (string) - Error message.

#### Response Example (200)
```json
{
  "threads": [
    {
      "id": "thread_abc123",
      "labels": ["inbox", "important"],
      "subject": "Meeting Update",
      "sent_timestamp": "2023-10-27T10:00:00Z",
      "received_timestamp": "2023-10-27T10:05:00Z",
      "senders": ["sender@example.com"],
      "recipients": ["recipient@example.com"]
    }
  ],
  "next_page_token": "next_token_xyz789"
}
```

#### Response Example (404)

```json
{
  "code": 404,
  "message": "Pod not found."
}
```

```
--------------------------------

### DMARC Record Example for Email Policy and Reporting

Source: https://docs.agentmail.to/email-protocols

The DMARC (Domain-based Message Authentication, Reporting, and Conformance) record is a TXT record that defines a policy for handling emails failing SPF or DKIM checks. This example sets the policy to 'reject' and specifies an email address for receiving aggregate reports.

```text
TXT | _dmarc.domain.com | v=DMARC1; p=reject; rua=mailto:dmarc@agentmail.to
```

--------------------------------

### GET /v0/inboxes/{inbox_id}/threads/{thread_id}

Source: https://docs.agentmail.to/api-reference/inboxes/threads/get

Fetches a specific email thread from a given inbox. You need to provide both the inbox ID and the thread ID to identify the thread.

```APIDOC
## GET /v0/inboxes/{inbox_id}/threads/{thread_id}

### Description
Retrieves a specific email thread from a specified inbox. This endpoint requires both the `inbox_id` and `thread_id` to uniquely identify the thread.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/threads/{thread_id}

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The unique identifier for the inbox.
- **thread_id** (string) - Required - The unique identifier for the thread within the inbox.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the thread.
- **subject** (string) - The subject line of the email thread.
- **snippet** (string) - A short preview of the latest message in the thread.
- **from** (object) - Information about the sender of the latest message.
  - **name** (string) - The name of the sender.
  - **email** (string) - The email address of the sender.
- **to** (array) - A list of recipients.
  - **name** (string) - The name of the recipient.
  - **email** (string) - The email address of the recipient.
- **date** (string) - The timestamp of the latest message in the thread (ISO 8601 format).
- **has_attachments** (boolean) - Indicates if the latest message has attachments.
- **is_read** (boolean) - Indicates if the thread has been read.
- **is_starred** (boolean) - Indicates if the thread is starred.
- **labels** (array) - A list of labels applied to the thread.
  - **id** (string) - The ID of the label.
  - **name** (string) - The name of the label.

#### Response Example
```json
{
  "id": "thread_abc123",
  "subject": "Meeting Follow-up",
  "snippet": "Hi team, here are the notes from our meeting.",
  "from": {
    "name": "Alice",
    "email": "alice@example.com"
  },
  "to": [
    {
      "name": "Bob",
      "email": "bob@example.com"
    }
  ],
  "date": "2023-10-27T10:30:00Z",
  "has_attachments": false,
  "is_read": false,
  "is_starred": true,
  "labels": [
    {
      "id": "label_xyz",
      "name": "Urgent"
    }
  ]
}
```

```
--------------------------------

### GET /v0/inboxes/{inbox_id}/metrics

Source: https://docs.agentmail.to/api-reference/inboxes/metrics/get

Fetches various metrics for a specified inbox, such as open rates, click-through rates, and delivery statistics.

```APIDOC
## GET /v0/inboxes/{inbox_id}/metrics

### Description
Retrieves performance metrics for a specific inbox.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/inboxes/{inbox_id}/metrics

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The unique identifier of the inbox.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **opens** (integer) - The total number of times emails from this inbox have been opened.
- **clicks** (integer) - The total number of clicks on links within emails from this inbox.
- **deliveries** (integer) - The total number of emails successfully delivered from this inbox.
- **unsubscribes** (integer) - The total number of users who unsubscribed from this inbox.

#### Response Example
```json
{
  "opens": 1500,
  "clicks": 300,
  "deliveries": 2000,
  "unsubscribes": 15
}
```

```
--------------------------------

### Handle Manager Emails and Generate Sales Pitch (Python)

Source: https://docs.agentmail.to/sales-agent-websocket

Processes emails identified as coming from a manager. It extracts customer information, generates a sales pitch using an AI model, sends the pitch to the customer, and confirms the action back to the manager.

```python
async def handle_manager_email(inbox_id, message_id, from_email, subject, body):
    global manager_email
    manager_email = from_email  # Remember for notifications

    # Extract customer email using regex (assuming extract_customer_info is defined elsewhere)
    customer_email = extract_customer_info(body)

    if not customer_email:
        await reply_to_email(inbox_id, message_id, from_email,
            "I couldn't find a customer email. Please include it.")
        return

    # Generate AI sales pitch (assuming get_ai_response is defined elsewhere)
    sales_pitch = await get_ai_response(
        [{"role": "user", "content": f"Create a sales email based on: {body}"}],
        "You are a helpful sales agent. Generate a brief, professional email..."
    )

    # Send to customer (assuming send_email is defined elsewhere)
    await send_email(inbox_id, customer_email, f"Introduction: {subject}", sales_pitch)

    # Confirm to manager (assuming reply_to_email is defined elsewhere)
    await reply_to_email(inbox_id, message_id, from_email,
        f"✓ Sent email to {customer_email}.\n\nContent:\n{sales_pitch}")
```

--------------------------------

### Update Webhook via HTTP Request (PHP)

Source: https://docs.agentmail.to/api-reference/webhooks/update

This PHP example uses the Guzzle HTTP client to update a webhook. It sends a PATCH request with the appropriate headers and an empty JSON body. The response body is then echoed.

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('PATCH', 'https://api.agentmail.to/v0/webhooks/webhook_id', [
  'body' => '{}',
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
    'Content-Type' => 'application/json',
  ],
]);

echo $response->getBody();
```

--------------------------------

### List Drafts Endpoint Definition (OpenAPI)

Source: https://docs.agentmail.to/api-reference/drafts/list

Defines the GET /v0/drafts endpoint for listing drafts. It includes parameters for filtering and pagination, authentication via Bearer token, and specifies success (200) and error (404) responses with JSON content.

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/drafts:
    get:
      operationId: list
      summary: List Drafts
      tags:
        - subpackage_drafts
      parameters:
        - name: limit
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/type_:Limit'
        - name: page_token
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/type_:PageToken'
        - name: labels
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/type_:Labels'
        - name: before
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/type_:Before'
        - name: after
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/type_:After'
        - name: ascending
          in: query
          required: false
          schema:
            $ref: '#/components/schemas/type_:Ascending'
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_drafts:ListDraftsResponse'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_:Limit:
      type: integer
      description: Limit of number of items returned.
      title: Limit
    type_:PageToken:
      type: string
      description: Page token for pagination.
      title: PageToken
    type_:Labels:
      type: array
      items:
        type: string
      description: Labels to filter by.
      title: Labels
    type_:Before:
      type: string
      format: date-time
      description: Timestamp before which to filter by.
      title: Before
    type_:After:
      type: string
      format: date-time
      description: Timestamp after which to filter by.
      title: After
    type_:Ascending:
      type: boolean
      description: Sort in ascending temporal order.
      title: Ascending
    type_:Count:
      type: integer
      description: Number of items returned.
      title: Count
    type_inboxes:InboxId:
      type: string
      description: ID of inbox.
      title: InboxId
    type_threads:ThreadId:
      type: string
      description: ID of thread.
      title: ThreadId
    type_drafts:DraftId:
      type: string
      description: ID of draft.
      title: DraftId
    type_drafts:DraftLabels:
      type: array
      items:
        type: string
      description: Labels of draft.
      title: DraftLabels
    type_drafts:DraftTo:
      type: array
      items:
        type: string
      description: >-
        Addresses of recipients. In format `username@domain.com` or `Display
        Name <username@domain.com>`.
      title: DraftTo
    type_drafts:DraftCc:
      type: array
      items:
        type: string
      description: >-
        Addresses of CC recipients. In format `username@domain.com` or `Display
        Name <username@domain.com>`.
      title: DraftCc
    type_drafts:DraftBcc:
      type: array
      items:
        type: string
      description: >-
        Addresses of BCC recipients. In format `username@domain.com` or `Display
        Name <username@domain.com>`.
      title: DraftBcc
    type_drafts:DraftSubject:
      type: string
      description: Subject of draft.
      title: DraftSubject
    type_drafts:DraftPreview:
      type: string
      description: Text preview of draft.
      title: DraftPreview
    type_attachments:AttachmentId:
      type: string
      description: ID of attachment.
      title: AttachmentId
    type_attachments:AttachmentFilename:
      type: string
      description: Filename of attachment.
      title: AttachmentFilename
    type_attachments:AttachmentSize:
      type: integer
      description: Size of attachment in bytes.
      title: AttachmentSize
    type_attachments:AttachmentContentType:
      type: string
      description: Content type of attachment.
      title: AttachmentContentType
    type_attachments:AttachmentContentDisposition:
      type: string
      enum:
        - inline
        - attachment
      description: Content disposition of attachment.
      title: AttachmentContentDisposition
    type_attachments:AttachmentContentId:
      type: string
      description: Content ID of attachment.
      title: AttachmentContentId
    type_attachments:Attachment:
```

--------------------------------

### Create Inbox using HTTP Request (Ruby)

Source: https://docs.agentmail.to/api-reference/pods/inboxes/create

Illustrates how to create an inbox using Ruby's Net::HTTP library. This example sends a POST request to the AgentMail API endpoint, including authentication and content type headers.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/inboxes")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Post.new(url)
request["Authorization"] = 'Bearer <api_key>'
request["Content-Type"] = 'application/json'
request.body = "{}"

response = http.request(request)
puts response.read_body
```

--------------------------------

### Configure Ngrok Authentication Globally

Source: https://docs.agentmail.to/documentation/examples/auto-reply-agent

Command to set your ngrok authentication token globally, which is an alternative to setting it in the '.env' file. Replace 'YOUR_TOKEN' with your actual ngrok auth token.

```bash
ngrok config add-authtoken YOUR_TOKEN
```

--------------------------------

### Delete List Entry via API (Python, JavaScript, Go, Ruby, Java, PHP, C#, Swift)

Source: https://docs.agentmail.to/api-reference/lists/delete

These examples demonstrate how to delete an entry from a list using the Agentmail.to API. They cover various programming languages and utilize their respective HTTP client libraries. Ensure you replace '<api_key>' with your actual API key for authentication. The output typically includes the API response, which may contain status codes and confirmation messages.

```python
import requests

url = "https://api.agentmail.to/v0/lists/send/allow/entry"

headers = {"Authorization": "Bearer <api_key>"}

response = requests.delete(url, headers=headers)

print(response.json())
```

```javascript
const url = 'https://api.agentmail.to/v0/lists/send/allow/entry';
const options = {method: 'DELETE', headers: {Authorization: 'Bearer <api_key>'}};

try {
  const response = await fetch(url, options);
  const data = await response.json();
  console.log(data);
} catch (error) {
  console.error(error);
}
```

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/lists/send/allow/entry"

    req, _ := http.NewRequest("DELETE", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/lists/send/allow/entry")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Delete.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.delete("https://api.agentmail.to/v0/lists/send/allow/entry")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('DELETE', 'https://api.agentmail.to/v0/lists/send/allow/entry', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/lists/send/allow/entry");
var request = new RestRequest(Method.DELETE);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/lists/send/allow/entry")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "DELETE"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

--------------------------------

### GET /v0/inboxes/{inbox_id}/messages/{message_id}

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get

Retrieves a specific message from a given inbox. Requires authentication.

```APIDOC
## GET /v0/inboxes/{inbox_id}/messages/{message_id}

### Description
Retrieves a specific message from a given inbox. Requires authentication.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/messages/{message_id}

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - ID of inbox.
- **message_id** (string) - Required - ID of message.

#### Query Parameters
None

#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Request Example
None (GET request with path parameters and headers)

### Response
#### Success Response (200)
- **message_id** (string) - ID of the message.
- **inbox_id** (string) - ID of the inbox the message belongs to.
- **thread_id** (string) - ID of the thread the message belongs to.
- **labels** (array of strings) - Labels associated with the message.
- **timestamp** (string) - Time at which the message was sent or drafted (ISO 8601 format).
- **from** (string) - Sender's email address.
- **to** (array of strings) - Recipients' email addresses.
- **cc** (array of strings) - CC recipients' email addresses.
- **bcc** (array of strings) - BCC recipients' email addresses.
- **subject** (string) - Subject of the message.
- **preview** (string) - A short preview of the message content.
- **text_body** (string) - The plain text body of the message.
- **html_body** (string) - The HTML body of the message.
- **attachments** (array of objects) - List of attachments associated with the message.
  - **attachment_id** (string) - ID of the attachment.
  - **filename** (string) - Filename of the attachment.
  - **size** (integer) - Size of the attachment in bytes.
  - **content_type** (string) - MIME type of the attachment.
  - **content_disposition** (string) - Content disposition (e.g., 'inline', 'attachment').
  - **content_id** (string) - Content ID of the attachment (if applicable).

#### Error Response (404)
- **code** (integer) - Error code.
- **message** (string) - Error message.

#### Response Example (200)
```json
{
  "message_id": "msg_abc123",
  "inbox_id": "inb_xyz789",
  "thread_id": "thr_def456",
  "labels": ["INBOX", "READ"],
  "timestamp": "2023-10-27T10:00:00Z",
  "from": "sender@example.com",
  "to": ["recipient@example.com"],
  "cc": [],
  "bcc": [],
  "subject": "Test Email",
  "preview": "This is a test email...",
  "text_body": "This is the plain text body.",
  "html_body": "<p>This is the <strong>HTML</strong> body.</p>",
  "attachments": [
    {
      "attachment_id": "att_ghi012",
      "filename": "document.pdf",
      "size": 102400,
      "content_type": "application/pdf",
      "content_disposition": "attachment",
      "content_id": null
    }
  ]
}
```

#### Response Example (404)

```json
{
  "code": 404,
  "message": "Message not found."
}
```

```
--------------------------------

### GET /v0/pods/{pod_id}

Source: https://docs.agentmail.to/api-reference/pods/get

Retrieves a specific pod using its ID. This endpoint is demonstrated across multiple SDKs.

```APIDOC
## GET /v0/pods/{pod_id}

### Description
Retrieves a specific pod using its unique identifier.

### Method
GET

### Endpoint
/v0/pods/{pod_id}

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The unique identifier of the pod to retrieve.

#### Query Parameters
None

#### Request Body
None

### Request Example
(See SDK examples below for language-specific request construction)

### Response
#### Success Response (200)
- **pod_data** (object) - Contains the details of the requested pod.

#### Response Example
```json
{
  "pod_id": "pod_id",
  "name": "Example Pod",
  "created_at": "2023-10-27T10:00:00Z"
}
```

### SDK Examples

**TypeScript**

```typescript
import { AgentMailClient } from "agentmail";

async function main() {
    const client = new AgentMailClient({
        apiKey: "YOUR_TOKEN_HERE",
    });
    await client.pods.get("pod_id");
}
main();
```

**Python**

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.pods.get(
    pod_id="pod_id"
)
```

**Go**

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/pods/pod_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

**Ruby**

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

**Java**

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/pods/pod_id")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

**PHP**

```php
<?php
require_once('vendor/autoload.php');

$client = new \GuzzleHttp\Client();

$response = $client->request('GET', 'https://api.agentmail.to/v0/pods/pod_id', [
  'headers' => [
    'Authorization' => 'Bearer <api_key>',
  ],
]);

echo $response->getBody();
```

**C#**

```csharp
using RestSharp;

var client = new RestClient("https://api.agentmail.to/v0/pods/pod_id");
var request = new RestRequest(Method.GET);
request.AddHeader("Authorization", "Bearer <api_key>");
IRestResponse response = client.Execute(request);
```

**Swift**

```swift
import Foundation

let headers = ["Authorization": "Bearer <api_key>"]

let request = NSMutableURLRequest(url: NSURL(string: "https://api.agentmail.to/v0/pods/pod_id")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "GET"
request.allHTTPHeaderFields = headers

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error as Any)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```

```
--------------------------------

### GET /v0/pods/{pod_id}/drafts

Source: https://docs.agentmail.to/api-reference/pods/drafts/list

Retrieves a list of drafts associated with a specific pod. Supports filtering and pagination.

```APIDOC
## GET /v0/pods/{pod_id}/drafts

### Description
Retrieves a list of drafts associated with a specific pod. Supports filtering and pagination.

### Method
GET

### Endpoint
/v0/pods/{pod_id}/drafts

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - ID of pod.

#### Query Parameters
- **limit** (integer) - Optional - Limit of number of items returned.
- **page_token** (string) - Optional - Page token for pagination.
- **labels** (array of strings) - Optional - Labels to filter by.
- **before** (string) - Optional - Timestamp before which to filter by (ISO 8601 format).
- **after** (string) - Optional - Timestamp after which to filter by (ISO 8601 format).
- **ascending** (boolean) - Optional - Sort in ascending temporal order.

#### Header Parameters
- **Authorization** (string) - Required - Bearer authentication token.

### Response
#### Success Response (200)
- **drafts** (array) - List of drafts.
  - **id** (string) - ID of draft.
  - **labels** (array of strings) - Labels of draft.
  - **to** (array of strings) - Addresses of recipients.
  - **cc** (array of strings) - Addresses of CC recipients.
  - **bcc** (array of strings) - Addresses of BCC recipients.
  - **subject** (string) - Subject of draft.
  - **preview** (string) - Text preview of draft.
  - **created_at** (string) - Timestamp of draft creation.
  - **updated_at** (string) - Timestamp of draft last update.
- **next_page_token** (string) - Token for the next page of results.
- **total_count** (integer) - Total number of drafts available.

#### Error Response (404)
- **code** (integer) - Error code.
- **message** (string) - Error message.

### Response Example
```json
{
  "drafts": [
    {
      "id": "draft_abc123",
      "labels": ["important", "work"],
      "to": ["recipient@example.com"],
      "cc": [],
      "bcc": [],
      "subject": "Meeting Follow-up",
      "preview": "Hi team, following up on our meeting...",
      "created_at": "2023-10-27T10:00:00Z",
      "updated_at": "2023-10-27T10:05:00Z"
    }
  ],
  "next_page_token": "page_token_xyz789",
  "total_count": 10
}
```

```
--------------------------------

### GET /v0/webhooks

Source: https://docs.agentmail.to/api-reference/webhooks/list

Retrieves a list of all configured webhooks. Supports pagination using `limit` and `page_token` query parameters. Requires Bearer authentication.

```APIDOC
## GET /v0/webhooks

### Description
Retrieves a list of all configured webhooks. Supports pagination using `limit` and `page_token` query parameters. Requires Bearer authentication.

### Method
GET

### Endpoint
https://api.agentmail.to/v0/webhooks

### Parameters
#### Query Parameters
- **limit** (integer) - Optional - The maximum number of items to return per page.
- **page_token** (string) - Optional - A token to retrieve the next page of results.

#### Header Parameters
- **Authorization** (string) - Required - Bearer token for authentication. Example: `Bearer YOUR_API_TOKEN`

### Response
#### Success Response (200)
- **count** (integer) - The total number of webhooks returned in this response.
- **limit** (integer) - The limit applied to the number of items returned.
- **next_page_token** (string) - A token to retrieve the next page of results, if available.
- **webhooks** (array) - An array of webhook objects, ordered by `created_at` descending.
  - **webhook_id** (string) - The unique identifier for the webhook.
  - **url** (string) - The URL of the webhook endpoint.
  - **event_types** (array of strings) - The event types for which this webhook will receive notifications.
  - **pod_ids** (array of strings) - The Pod IDs for which this webhook will send events (maximum 10).
  - **inbox_ids** (array of strings) - The Inbox IDs for which this webhook will send events (maximum 10).
  - **secret** (string) - The secret used for webhook signature verification.
  - **enabled** (boolean) - Indicates if the webhook is currently enabled.
  - **updated_at** (string) - The timestamp when the webhook was last updated.
  - **created_at** (string) - The timestamp when the webhook was created.
  - **client_id** (string) - The client ID associated with the webhook.

#### Response Example
```json
{
  "count": 1,
  "limit": 10,
  "next_page_token": "some_token_for_next_page",
  "webhooks": [
    {
      "webhook_id": "wh_abc123",
      "url": "https://example.com/webhook",
      "event_types": [
        "message.received",
        "message.sent"
      ],
      "pod_ids": [],
      "inbox_ids": [],
      "secret": "whsec_abcdef123456",
      "enabled": true,
      "updated_at": "2023-10-27T10:00:00Z",
      "created_at": "2023-10-26T09:00:00Z",
      "client_id": "cl_xyz789"
    }
  ]
}
```

```
--------------------------------

### List Inbox Messages via HTTP Request (Java)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/list

This Java code snippet demonstrates how to use the Unirest library to send an HTTP GET request to the AgentMail API for listing messages. It includes setting the 'Authorization' header. Ensure the Unirest library is included in your project dependencies.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.get("https://api.agentmail.to/v0/inboxes/inbox_id/messages")
  .header("Authorization", "Bearer <api_key>")
  .asString();
```

--------------------------------

### Fetch Message Attachment via HTTP Request

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get-attachment

Provides Go code to retrieve a message attachment by making a direct HTTP GET request to the AgentMail API. It includes setting the Authorization header with a Bearer token and reading the response body. This method bypasses the SDK and interacts directly with the API endpoint.

```go
package main

import (
    "fmt"
    "net/http"
    "io"
)

func main() {

    url := "https://api.agentmail.to/v0/inboxes/inbox_id/messages/message_id/attachments/attachment_id"

    req, _ := http.NewRequest("GET", url, nil)

    req.Header.Add("Authorization", "Bearer <api_key>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := io.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

--------------------------------

### GET /v0/inboxes/{inbox_id}/messages/{message_id}

Source: https://docs.agentmail.to/api-reference/inboxes/messages/get

Fetches a specific message from a given inbox. You need to provide the unique identifier for both the inbox and the message.

```APIDOC
## GET /v0/inboxes/{inbox_id}/messages/{message_id}

### Description
Retrieves a specific message from an inbox using its ID.

### Method
GET

### Endpoint
/v0/inboxes/{inbox_id}/messages/{message_id}

### Parameters
#### Path Parameters
- **inbox_id** (string) - Required - The unique identifier of the inbox.
- **message_id** (string) - Required - The unique identifier of the message.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **id** (string) - The unique identifier of the message.
- **inbox_id** (string) - The identifier of the inbox the message belongs to.
- **subject** (string) - The subject line of the message.
- **from** (string) - The sender's email address.
- **to** (string) - The recipient's email address.
- **body** (string) - The content of the message.
- **created_at** (string) - The timestamp when the message was created.

#### Response Example
```json
{
  "id": "msg_abc123xyz",
  "inbox_id": "inb_def456uvw",
  "subject": "Meeting Follow-up",
  "from": "sender@example.com",
  "to": "recipient@agentmail.to",
  "body": "Hi team, \n\nFollowing up on our meeting today...",
  "created_at": "2023-10-27T10:00:00Z"
}
```

```
--------------------------------

### GET /v0/metrics

Source: https://docs.agentmail.to/api-reference/metrics/list

Retrieves metrics data within a specified time range. Requires an API key for authentication.

```APIDOC
## GET /v0/metrics

### Description
Retrieves metrics data within a specified time range. Requires an API key for authentication.

### Method
GET

### Endpoint
/v0/metrics

### Query Parameters
- **start_timestamp** (string) - Required - The start of the time range for the metrics (ISO 8601 format).
- **end_timestamp** (string) - Required - The end of the time range for the metrics (ISO 8601 format).

### Headers
- **Authorization** (string) - Required - Bearer token with your API key (e.g., `Bearer YOUR_TOKEN_HERE`).

### Request Example
```

GET /v0/metrics?start_timestamp=2024-01-15T09:30:00Z&end_timestamp=2024-01-15T09:30:00Z
Authorization: Bearer YOUR_TOKEN_HERE

```
### Response
#### Success Response (200)
- **metrics_data** (object) - An object containing various metrics.

#### Response Example
```json
{
  "metrics_data": {
    "emails_sent": 1000,
    "open_rate": 0.25,
    "click_rate": 0.05
  }
}
```

#### Error Response (401)

- **error** (string) - Authentication failed. Invalid or missing API key.

#### Error Response (400)

- **error** (string) - Bad Request. Invalid query parameters.
  
  ```
  
  ```

--------------------------------

### Process Webhook Payload and Send Reply (Python)

Source: https://docs.agentmail.to/webhook-agent

This function processes the JSON payload received from a webhook, typically an email. It extracts email details, constructs a prompt for the agent, runs the agent with the prompt and conversation history, and then sends a reply to the original email using the agent's output. It also updates the conversation history.

```python
def process_webhook(payload):
  global messages

  email = payload["message"]
  print(f"[process_webhook] Processing email from: {email.get('from')}, subject: {email.get('subject')}, id: {email.get('message_id')}")

  prompt = f"""
          From: {email["from"]}
          Subject: {email["subject"]}
          Body:\n{email["text"]} """
  print("Prompt:\n\n", prompt, "\n")

  response = asyncio.run(Runner.run(agent, messages + [{"role": "user", "content": prompt}]))
  print("Response:\n\n", response.final_output, "\n")

  print(f"[process_webhook] Attempting to send reply to message_id: {email['message_id']} via inbox: {inbox}")
  client.inboxes.messages.reply(inbox_id=inbox, message_id=email["message_id"], html=response.final_output)
  print(f"[process_webhook] Reply call made for message_id: {email['message_id']}.")

  messages = response.to_input_list()
  print(f"[process_webhook] Updated message history. New length: {len(messages)}\n")
```

--------------------------------

### Subscribe to Multiple Inboxes (Python)

Source: https://docs.agentmail.to/sales-agent-websocket

Demonstrates how to subscribe the agent to multiple email inboxes simultaneously using the `send_subscribe` method with a list of inbox IDs.

```python
await socket.send_subscribe(Subscribe(inbox_ids=[
    "sales-agent@agentmail.to",
    "support-agent@agentmail.to",
    "info@yourdomain.com"
]))
```

--------------------------------

### Get List Entry using OpenAPI Specification

Source: https://docs.agentmail.to/api-reference/pods/lists/get

This snippet demonstrates how to retrieve a list entry from Agentmail.to using its OpenAPI specification. It requires the pod ID, direction, type, and the specific entry (email or domain) as path parameters, along with an Authorization header for authentication. The response includes details about the entry, its organization, reason, creation time, and associated pod/inbox IDs.

```yaml
openapi: 3.1.0
info:
  title: api
  version: 1.0.0
paths:
  /v0/pods/{pod_id}/lists/{direction}/{type}/{entry}:
    get:
      operationId: get
      summary: Get List Entry
      tags:
        - subpackage_pods.subpackage_pods/lists
      parameters:
        - name: pod_id
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_pods:PodId'
        - name: direction
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_lists:Direction'
        - name: type
          in: path
          required: true
          schema:
            $ref: '#/components/schemas/type_lists:ListType'
        - name: entry
          in: path
          description: Email address or domain.
          required: true
          schema:
            type: string
        - name: Authorization
          in: header
          description: Bearer authentication
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Response with status 200
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_lists:PodListEntry'
        '404':
          description: Error response with status 404
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/type_:ErrorResponse'
servers:
  - url: https://api.agentmail.to
  - url: https://x402.api.agentmail.to
  - url: https://mpp.api.agentmail.to
  - url: https://api.agentmail.eu
components:
  schemas:
    type_pods:PodId:
      type: string
      description: ID of pod.
      title: PodId
    type_lists:Direction:
      type: string
      enum:
        - send
        - receive
      description: Direction of list entry.
      title: Direction
    type_lists:ListType:
      type: string
      enum:
        - allow
        - block
      description: Type of list entry.
      title: ListType
    type_:OrganizationId:
      type: string
      description: ID of organization.
      title: OrganizationId
    type_lists:EntryType:
      type: string
      enum:
        - email
        - domain
      description: Whether the entry is an email address or domain.
      title: EntryType
    type_lists:PodListEntry:
      type: object
      properties:
        entry:
          type: string
          description: Email address or domain of list entry.
        organization_id:
          $ref: '#/components/schemas/type_:OrganizationId'
        reason:
          type: string
          description: Reason for adding the entry.
        direction:
          $ref: '#/components/schemas/type_lists:Direction'
        list_type:
          $ref: '#/components/schemas/type_lists:ListType'
        entry_type:
          $ref: '#/components/schemas/type_lists:EntryType'
        created_at:
          type: string
          format: date-time
          description: Time at which entry was created.
        pod_id:
          type: string
          description: ID of pod.
        inbox_id:
          type: string
          description: ID of inbox, if entry is inbox-scoped.
      required:
        - entry
        - organization_id
        - direction
        - list_type
        - entry_type
        - created_at
        - pod_id
      title: PodListEntry
    type_:ErrorName:
      type: string
      description: Name of error.
      title: ErrorName
    type_:ErrorMessage:
      type: string
      description: Error message.
      title: ErrorMessage
    type_:ErrorResponse:
      type: object
      properties:
        name:
          $ref: '#/components/schemas/type_:ErrorName'
        message:
          $ref: '#/components/schemas/type_:ErrorMessage'
      required:
        - name
        - message
      title: ErrorResponse
  securitySchemes:
    Bearer:
      type: http
      scheme: bearer
```

--------------------------------

### Forward Message using AgentMail SDK (Python)

Source: https://docs.agentmail.to/api-reference/inboxes/messages/forward

Shows how to forward a message with the AgentMail Python SDK. It initializes the AgentMail client with an API key and uses it to forward a specific message from an inbox.

```python
from agentmail import AgentMail

client = AgentMail(
    api_key="YOUR_TOKEN_HERE"
)

client.inboxes.messages.forward(
    inbox_id="inbox_id",
    message_id="message_id"
)
```

--------------------------------

### Connect to AgentMail Inbox using TypeScript IMAP

Source: https://docs.agentmail.to/imap-smtp

This TypeScript example shows how to establish an IMAP connection to AgentMail using the 'imap' library. It requires your inbox email and API key (from environment variable) for authentication, connects to the IMAP server over TLS, and opens the INBOX folder. Error handling for connection issues is included.

```typescript
import Imap from "imap";

// Your credentials from AgentMail Console
const inboxEmail = "myinbox@agentmail.to"; // From Dashboard → Inboxes
const apiKey = process.env.AGENTMAIL_API_KEY!; // From Dashboard → API Keys

const imap = new Imap({
  user: inboxEmail,
  password: apiKey,
  host: "imap.agentmail.to",
  port: 993,
  tls: true, // SSL required
});

imap.once("ready", () => {
  imap.openBox("INBOX", false, (err, box) => {
    if (err) throw err;
    console.log(`${box.messages.total} messages in INBOX`);
    imap.end();
  });
});

imap.once("error", (err: Error) => {
  console.error("IMAP error:", err.message);
});

imap.connect();
```

--------------------------------

### List Inboxes via HTTP Request (Ruby)

Source: https://docs.agentmail.to/api-reference/pods/inboxes/list

Demonstrates how to list inboxes for a pod by making an HTTP GET request using Ruby's Net::HTTP library. It sets the Authorization header and prints the response body. Requires an API key and pod ID.

```ruby
require 'uri'
require 'net/http'

url = URI("https://api.agentmail.to/v0/pods/pod_id/inboxes")

http = Net::HTTP.new(url.host, url.port)
http.use_ssl = true

request = Net::HTTP::Get.new(url)
request["Authorization"] = 'Bearer <api_key>'

response = http.request(request)
puts response.read_body
```

--------------------------------

### GET /v0/pods/{pod_id}/domains

Source: https://docs.agentmail.to/api-reference/pods/domains/list

Retrieves a list of domains associated with a specific pod. Supports pagination and filtering.

```APIDOC
## GET /v0/pods/{pod_id}/domains

### Description
Retrieves a list of domains associated with a specific pod. This endpoint allows you to list all domains configured for a given pod, with options for pagination.

### Method
GET

### Endpoint
`/v0/pods/{pod_id}/domains`

### Parameters
#### Path Parameters
- **pod_id** (string) - Required - The unique identifier of the pod.

#### Query Parameters
- **limit** (integer) - Optional - The maximum number of items to return per page.
- **page_token** (string) - Optional - A token to retrieve the next page of results.

#### Header Parameters
- **Authorization** (string) - Required - Bearer token for authentication.

### Request Example
```json
{
  "example": ""
}
```

### Response

#### Success Response (200)

- **count** (integer) - The total number of domains returned.
- **limit** (integer) - The limit applied to the number of items returned.
- **next_page_token** (string) - A token for fetching the next page of results, if available.
- **domains** (array) - An array of domain objects, ordered by creation date descending.
   - **pod_id** (string) - The ID of the pod the domain belongs to.
   - **domain_id** (string) - The name of the domain.
   - **feedback_enabled** (boolean) - Indicates if bounce and complaint notifications are enabled.
   - **client_id** (string) - The client ID associated with the domain.
   - **updated_at** (string) - The timestamp when the domain was last updated.
   - **created_at** (string) - The timestamp when the domain was created.

#### Response Example

```json
{
  "count": 2,
  "limit": 10,
  "next_page_token": "some_token",
  "domains": [
    {
      "pod_id": "your_pod_id",
      "domain_id": "example.com",
      "feedback_enabled": true,
      "client_id": "your_client_id",
      "updated_at": "2023-10-27T10:00:00Z",
      "created_at": "2023-10-26T09:00:00Z"
    }
  ]
}
```

#### Error Response (404)

- **name** (string) - The name of the error.
- **message** (string) - A descriptive message for the error.

#### Error Response Example

```json
{
  "name": "PodNotFound",
  "message": "The specified pod was not found."
}
```

```
--------------------------------

### Handle Customer Email - Track, Detect Intent, Notify Manager (Python)

Source: https://docs.agentmail.to/sales-agent-websocket

Processes incoming customer emails by tracking conversation history, detecting user intent using keywords, generating an AI response via OpenAI, replying to the customer, and notifying a manager if a strong intent signal is detected. It relies on external functions like `get_ai_response`, `reply_to_email`, and `send_email`.

```python
async def handle_customer_email(inbox_id, message_id, thread_id, from_email, subject, body):
      """Handle email from customer - track conversation, detect intent, and notify manager"""
      print(f"\n📧 Email from CUSTOMER: {from_email}")

      # Track conversation history
      if thread_id not in conversations:
          conversations[thread_id] = []
      conversations[thread_id].append({"role": "user", "content": body})

      # Detect customer intent
      intent_keywords = {
          'interested': ['interested', 'demo', 'meeting', 'tell me more', 'sounds good'],
          'not_interested': ['not interested', 'no thank', 'not right now', 'maybe later'],
          'question': ['?', 'how', 'what', 'when', 'why', 'can you']
      }

      body_lower = body.lower()
      intent = 'question'  # default
      for key, keywords in intent_keywords.items():
          if any(keyword in body_lower for keyword in keywords):
              intent = key
              break

      # Generate AI response
      system_prompt = """You are a helpful sales agent. Answer customer questions professionally
      and helpfully. Keep responses brief (under 100 words). Be friendly but professional."""

      response = await get_ai_response(conversations[thread_id], system_prompt)

      # Reply to customer
      await reply_to_email(inbox_id, message_id, from_email, response)

      # Notify manager if strong intent signal
      if manager_email and intent in ['interested', 'not_interested']:
          status = "showing interest" if intent == 'interested' else "not interested at this time"
          await send_email(
              inbox_id,
              manager_email,
              f"Update: {from_email}",
              f"Customer {from_email} is {status}.\n\nTheir message:\n{body}\n\nMy response:\n{response}"
          )
          print(f"→ Notified manager about customer's {intent}")

      # Update conversation history
      conversations[thread_id].append({"role": "assistant", "content": response})
```

--------------------------------

### AI Response Generation in Python

Source: https://docs.agentmail.to/sales-agent-websocket

Generates responses using the OpenAI API. This function takes a list of messages and a system prompt to guide the AI's output. It's designed to handle sales conversations and generate professional email content.

```python
async def get_ai_response(messages, system_prompt):
    """Get response from OpenAI"""
    try:
        response = await openai.chat.completions.create(
            model="gpt-4o-mini",
            messages=[
                {"role": "system", "content": system_prompt},
                *messages
            ],
            temperature=0.7,
        )
        return response.choices[0].message.content
    except Exception as e:
        print(f"Error getting AI response: {e}")
        return "I apologize, but I encountered an error. Please try again."
```

--------------------------------

### Send Data to Agentmail.to API (Java)

Source: https://docs.agentmail.to/api-reference/lists/create

This Java example utilizes the Unirest library to send a POST request to the Agentmail.to API. It shows how to set the API key in the Authorization header, the Content-Type, and the JSON request body. Ensure you have the Unirest dependency added to your project.

```java
import com.mashape.unirest.http.HttpResponse;
import com.mashape.unirest.http.Unirest;

HttpResponse<String> response = Unirest.post("https://api.agentmail.to/v0/lists/send/allow")
  .header("Authorization", "Bearer <api_key>")
  .header("Content-Type", "application/json")
  .body("{\n  \"entry\": \"entry\"\n}")
  .asString();
```
