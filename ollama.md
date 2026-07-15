# Ollama

Ollama is a powerful, open-source tool for running large language models (LLMs) locally on your machine. It provides a simple way to download, run, and interact with various AI models like Llama 3, Gemma, Mistral, and many others without requiring cloud services. Ollama handles model management, inference optimization, and provides both a CLI interface and REST API for seamless integration into applications.

The core functionality includes model pulling from the Ollama library, custom model creation via Modelfiles, streaming text generation, multi-turn chat conversations, embeddings generation, and vision/multimodal capabilities. Ollama also provides OpenAI-compatible API endpoints, making it easy to integrate with existing applications that use the OpenAI API. The project supports multiple platforms (macOS, Windows, Linux, Docker) and offers official client libraries for Python and JavaScript.

---

## CLI Commands

### Run a Model

Execute a model and start an interactive chat session. The model will be automatically downloaded if not present locally.

```shell
# Run the default tag of a model
ollama run llama3.2

# Run a specific model size
ollama run llama3.2:1b

# Run with a prompt directly
ollama run llama3.2 "Summarize this file: $(cat README.md)"

# Run a multimodal model with an image
ollama run llava "What's in this image? /path/to/image.png"
```

### Pull a Model

Download a model from the Ollama library without running it.

```shell
# Pull the latest version
ollama pull llama3.2

# Pull a specific version/size
ollama pull llama3.2:70b

# Update an existing model (only downloads the diff)
ollama pull llama3.2
```

### List Models

Display all locally available models and their details.

```shell
# List all local models
ollama list

# Show currently loaded/running models
ollama ps

# Show detailed model information
ollama show llama3.2

# Show the Modelfile of a model
ollama show --modelfile llama3.2
```

### Create Custom Model

Create a customized model from an existing base model using a Modelfile.

```shell
# Create a model from a Modelfile
ollama create mario -f ./Modelfile

# Copy an existing model with a new name
ollama cp llama3.2 my-model

# Delete a model
ollama rm llama3.2
```

### Start the Server

Start the Ollama API server for programmatic access.

```shell
# Start the server (default: http://localhost:11434)
ollama serve

# The server runs automatically when using the desktop app
```

---

## REST API Endpoints

### Generate Completion

Generate text completions from a prompt. Supports streaming responses and various model parameters.

```shell
# Basic streaming generation
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "Why is the sky blue?"
}'

# Non-streaming with full response
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "Why is the sky blue?",
  "stream": false
}'

# With custom parameters
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "Write a haiku about coding",
  "stream": false,
  "options": {
    "temperature": 0.7,
    "top_p": 0.9,
    "seed": 42,
    "num_ctx": 4096
  }
}'

# JSON mode with structured output
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "List 3 colors in JSON format",
  "format": "json",
  "stream": false
}'

# Structured output with JSON schema
curl -X POST http://localhost:11434/api/generate -H "Content-Type: application/json" -d '{
  "model": "llama3.1:8b",
  "prompt": "Ollama is 22 years old and is busy saving the world. Respond using JSON",
  "stream": false,
  "format": {
    "type": "object",
    "properties": {
      "age": { "type": "integer" },
      "available": { "type": "boolean" }
    },
    "required": ["age", "available"]
  }
}'

# Response structure:
# {
#   "model": "llama3.2",
#   "created_at": "2023-08-04T19:22:45.499127Z",
#   "response": "The sky appears blue due to Rayleigh scattering...",
#   "done": true,
#   "total_duration": 5043500667,
#   "load_duration": 5025959,
#   "prompt_eval_count": 26,
#   "prompt_eval_duration": 325953000,
#   "eval_count": 290,
#   "eval_duration": 4709213000
# }
```

### Chat Completion

Generate conversational responses with message history and tool support.

```shell
# Basic chat
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.2",
  "messages": [
    { "role": "user", "content": "why is the sky blue?" }
  ]
}'

# Non-streaming chat
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.2",
  "messages": [
    { "role": "user", "content": "why is the sky blue?" }
  ],
  "stream": false
}'

# Multi-turn conversation with history
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.2",
  "messages": [
    { "role": "system", "content": "You are a helpful assistant." },
    { "role": "user", "content": "why is the sky blue?" },
    { "role": "assistant", "content": "Due to Rayleigh scattering." },
    { "role": "user", "content": "How is that different from Mie scattering?" }
  ],
  "stream": false
}'

# Chat with tools (function calling)
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.2",
  "messages": [
    { "role": "user", "content": "What is the weather today in Paris?" }
  ],
  "stream": false,
  "tools": [
    {
      "type": "function",
      "function": {
        "name": "get_current_weather",
        "description": "Get the current weather for a location",
        "parameters": {
          "type": "object",
          "properties": {
            "location": {
              "type": "string",
              "description": "The location to get the weather for, e.g. San Francisco, CA"
            },
            "format": {
              "type": "string",
              "description": "The format to return the weather in",
              "enum": ["celsius", "fahrenheit"]
            }
          },
          "required": ["location", "format"]
        }
      }
    }
  ]
}'

# Tool call response:
# {
#   "message": {
#     "role": "assistant",
#     "content": "",
#     "tool_calls": [
#       {
#         "function": {
#           "name": "get_current_weather",
#           "arguments": { "format": "celsius", "location": "Paris, FR" }
#         }
#       }
#     ]
#   },
#   "done": true
# }

# Continue conversation with tool result
curl http://localhost:11434/api/chat -d '{
  "model": "llama3.2",
  "messages": [
    { "role": "user", "content": "what is the weather in Toronto?" },
    { "role": "assistant", "content": "", "tool_calls": [{"function": {"name": "get_weather", "arguments": {"city": "Toronto"}}}] },
    { "role": "tool", "content": "11 degrees celsius", "tool_name": "get_weather" }
  ],
  "stream": false,
  "tools": [...]
}'
```

### Chat with Images (Vision)

Send images to multimodal models for visual analysis.

```shell
# Vision request with base64 image
curl http://localhost:11434/api/chat -d '{
  "model": "llava",
  "messages": [
    {
      "role": "user",
      "content": "what is in this image?",
      "images": ["iVBORw0KGgoAAAANSUhEUgAAAAUA...base64_encoded_image..."]
    }
  ]
}'

# Generate with image
curl http://localhost:11434/api/generate -d '{
  "model": "llava",
  "prompt": "What is in this picture?",
  "stream": false,
  "images": ["iVBORw0KGgoAAAANSUhEUgAAAAUA...base64_encoded_image..."]
}'
```

### Generate Embeddings

Generate vector embeddings from text for semantic search and RAG applications.

```shell
# Single text embedding
curl http://localhost:11434/api/embed -d '{
  "model": "all-minilm",
  "input": "Why is the sky blue?"
}'

# Multiple texts embedding
curl http://localhost:11434/api/embed -d '{
  "model": "all-minilm",
  "input": ["Why is the sky blue?", "Why is the grass green?"]
}'

# Response:
# {
#   "model": "all-minilm",
#   "embeddings": [
#     [0.010071029, -0.0017594862, 0.05007221, ...],
#     [-0.0098027075, 0.06042469, 0.025257962, ...]
#   ],
#   "total_duration": 14143917,
#   "load_duration": 1019500,
#   "prompt_eval_count": 8
# }
```

### Model Management

Create, list, copy, and delete models programmatically.

```shell
# List local models
curl http://localhost:11434/api/tags
# Response:
# {
#   "models": [
#     {
#       "name": "llama3.2:latest",
#       "model": "llama3.2:latest",
#       "size": 2019393189,
#       "digest": "a80c4f17acd5...",
#       "details": { "family": "llama", "parameter_size": "3.2B", "quantization_level": "Q4_K_M" }
#     }
#   ]
# }

# Show model information
curl http://localhost:11434/api/show -d '{"model": "llama3.2"}'

# Pull a model
curl http://localhost:11434/api/pull -d '{"model": "llama3.2"}'

# Create a custom model
curl http://localhost:11434/api/create -d '{
  "model": "mario",
  "from": "llama3.2",
  "system": "You are Mario from Super Mario Bros."
}'

# Copy a model
curl http://localhost:11434/api/copy -d '{
  "source": "llama3.2",
  "destination": "llama3-backup"
}'

# Delete a model
curl -X DELETE http://localhost:11434/api/delete -d '{"model": "llama3:13b"}'

# List running models
curl http://localhost:11434/api/ps

# Get server version
curl http://localhost:11434/api/version
# Response: {"version": "0.5.1"}
```

### Load/Unload Models

Control model memory management for optimal resource usage.

```shell
# Pre-load a model into memory
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2"
}'

# Unload a model from memory
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "keep_alive": 0
}'

# Set custom keep_alive duration (default: 5m)
curl http://localhost:11434/api/generate -d '{
  "model": "llama3.2",
  "prompt": "Hello",
  "keep_alive": "10m"
}'
```

---

## OpenAI-Compatible API

### Chat Completions

Use existing OpenAI client libraries with Ollama's OpenAI-compatible endpoints.

```python
# Python example using OpenAI SDK
from openai import OpenAI

client = OpenAI(
    base_url='http://localhost:11434/v1/',
    api_key='ollama',  # required but ignored
)

# Basic chat completion
chat_completion = client.chat.completions.create(
    messages=[
        {'role': 'user', 'content': 'Say this is a test'}
    ],
    model='llama3.2',
)
print(chat_completion.choices[0].message.content)

# Streaming chat completion
stream = client.chat.completions.create(
    messages=[{'role': 'user', 'content': 'Tell me a story'}],
    model='llama3.2',
    stream=True,
)
for chunk in stream:
    if chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end='')

# Vision with OpenAI SDK
response = client.chat.completions.create(
    model='llava',
    messages=[
        {
            'role': 'user',
            'content': [
                {'type': 'text', 'text': "What's in this image?"},
                {'type': 'image_url', 'image_url': 'data:image/png;base64,...'},
            ],
        }
    ],
    max_tokens=300,
)
print(response.choices[0].message.content)
```

```javascript
// JavaScript example using OpenAI SDK
import OpenAI from "openai";

const openai = new OpenAI({
  baseURL: "http://localhost:11434/v1/",
  apiKey: "ollama", // required but ignored
});

const chatCompletion = await openai.chat.completions.create({
  messages: [{ role: "user", content: "Say this is a test" }],
  model: "llama3.2",
});

console.log(chatCompletion.choices[0].message.content);
```

```shell
# cURL example
curl -X POST http://localhost:11434/v1/chat/completions \
-H "Content-Type: application/json" \
-d '{
  "model": "llama3.2",
  "messages": [{ "role": "user", "content": "Say this is a test" }]
}'
```

### Embeddings (OpenAI-Compatible)

Generate embeddings using the OpenAI-compatible endpoint.

```shell
curl -X POST http://localhost:11434/v1/embeddings \
-H "Content-Type: application/json" \
-d '{
  "model": "all-minilm",
  "input": "Hello world"
}'
```

---

## Go Client Library

### Basic Generation

Use the Go client library to interact with Ollama programmatically.

```go
package main

import (
    "context"
    "fmt"
    "log"

    "github.com/ollama/ollama/api"
)

func main() {
    client, err := api.ClientFromEnvironment()
    if err != nil {
        log.Fatal(err)
    }

    req := &api.GenerateRequest{
        Model:  "llama3.2",
        Prompt: "How many planets are there?",
        Stream: new(bool), // set to false for non-streaming
    }

    ctx := context.Background()
    respFunc := func(resp api.GenerateResponse) error {
        fmt.Println(resp.Response)
        return nil
    }

    err = client.Generate(ctx, req, respFunc)
    if err != nil {
        log.Fatal(err)
    }
}
```

### Chat with History

Maintain conversation context using the Chat API.

```go
package main

import (
    "context"
    "fmt"
    "log"

    "github.com/ollama/ollama/api"
)

func main() {
    client, err := api.ClientFromEnvironment()
    if err != nil {
        log.Fatal(err)
    }

    messages := []api.Message{
        {Role: "system", Content: "Provide very brief, concise responses"},
        {Role: "user", Content: "Name some unusual animals"},
        {Role: "assistant", Content: "Monotreme, platypus, echidna"},
        {Role: "user", Content: "Which of these is the most dangerous?"},
    }

    ctx := context.Background()
    req := &api.ChatRequest{
        Model:    "llama3.2",
        Messages: messages,
    }

    respFunc := func(resp api.ChatResponse) error {
        fmt.Print(resp.Message.Content)
        return nil
    }

    err = client.Chat(ctx, req, respFunc)
    if err != nil {
        log.Fatal(err)
    }
}
```

### Model Management in Go

List, pull, and manage models using the Go client.

```go
package main

import (
    "context"
    "fmt"
    "log"

    "github.com/ollama/ollama/api"
)

func main() {
    client, err := api.ClientFromEnvironment()
    if err != nil {
        log.Fatal(err)
    }

    ctx := context.Background()

    // List local models
    list, err := client.List(ctx)
    if err != nil {
        log.Fatal(err)
    }
    for _, model := range list.Models {
        fmt.Printf("Model: %s, Size: %d\n", model.Name, model.Size)
    }

    // Pull a model with progress
    err = client.Pull(ctx, &api.PullRequest{Model: "llama3.2"}, func(resp api.ProgressResponse) error {
        fmt.Printf("Status: %s, Completed: %d/%d\n", resp.Status, resp.Completed, resp.Total)
        return nil
    })
    if err != nil {
        log.Fatal(err)
    }

    // Show model info
    info, err := client.Show(ctx, &api.ShowRequest{Model: "llama3.2"})
    if err != nil {
        log.Fatal(err)
    }
    fmt.Printf("Model family: %s\n", info.Details.Family)

    // Generate embeddings
    embedResp, err := client.Embed(ctx, &api.EmbedRequest{
        Model: "all-minilm",
        Input: "Hello world",
    })
    if err != nil {
        log.Fatal(err)
    }
    fmt.Printf("Embeddings: %v\n", embedResp.Embeddings)
}
```

---

## Modelfile Reference

### Basic Modelfile

Create custom models by defining parameters, system prompts, and templates.

```dockerfile
# Modelfile for a Mario assistant
FROM llama3.2

# Set model parameters
PARAMETER temperature 1
PARAMETER num_ctx 4096
PARAMETER top_p 0.9

# Define the system message
SYSTEM You are Mario from Super Mario Bros, acting as an assistant.

# Custom template (optional)
TEMPLATE """{{ if .System }}<|im_start|>system
{{ .System }}<|im_end|>
{{ end }}{{ if .Prompt }}<|im_start|>user
{{ .Prompt }}<|im_end|>
{{ end }}<|im_start|>assistant
"""
```

```shell
# Create and use the model
ollama create mario -f ./Modelfile
ollama run mario
```

### Modelfile with Message History

Pre-configure conversation examples to guide model behavior.

```dockerfile
FROM llama3.2

SYSTEM You are a helpful geography assistant.

# Example conversation to guide responses
MESSAGE user Is Toronto in Canada?
MESSAGE assistant yes
MESSAGE user Is Sacramento in Canada?
MESSAGE assistant no
MESSAGE user Is Ontario in Canada?
MESSAGE assistant yes
```

### Modelfile from GGUF

Import models from GGUF files for custom model deployment.

```dockerfile
# Import from a local GGUF file
FROM ./my-model.gguf

# Configure the imported model
PARAMETER temperature 0.7
PARAMETER num_ctx 8192

SYSTEM You are a helpful assistant.
```

### Available Parameters

Configure model behavior with these parameters in your Modelfile.

```dockerfile
FROM llama3.2

# Context window size (default: 2048)
PARAMETER num_ctx 4096

# Temperature for creativity (default: 0.8)
PARAMETER temperature 0.7

# Top-p nucleus sampling (default: 0.9)
PARAMETER top_p 0.9

# Top-k sampling (default: 40)
PARAMETER top_k 40

# Min-p sampling (default: 0.0)
PARAMETER min_p 0.05

# Repetition penalty (default: 1.1)
PARAMETER repeat_penalty 1.2

# How far back to look for repetition (default: 64)
PARAMETER repeat_last_n 64

# Random seed for reproducibility (default: 0)
PARAMETER seed 42

# Max tokens to generate (default: -1, infinite)
PARAMETER num_predict 500

# Stop sequences (can specify multiple)
PARAMETER stop "<|end|>"
PARAMETER stop "User:"
```

---

## Summary

Ollama provides a comprehensive platform for running LLMs locally, offering multiple integration paths: CLI for interactive use, REST API for custom applications, OpenAI-compatible endpoints for drop-in replacement, and native Go client library for programmatic access. Key use cases include local AI development and testing, building privacy-focused applications that keep data on-premise, creating custom fine-tuned models via Modelfiles, embedding generation for RAG applications, and tool/function calling for agentic workflows.

Integration patterns typically involve starting with the CLI for model exploration, then moving to the REST API or client libraries for application integration. The OpenAI compatibility layer enables easy migration of existing applications, while Modelfiles provide flexibility for creating domain-specific assistants. For production deployments, consider running Ollama as a service with `ollama serve`, managing model lifecycle with keep_alive parameters, and using streaming for responsive user interfaces.
