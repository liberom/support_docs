# QMD - Query Markup Documents

QMD is an on-device hybrid search engine for markdown files, notes, meeting transcripts, and documentation. It combines BM25 full-text search, vector semantic search, and LLM re-ranking—all running locally via node-llama-cpp with GGUF models. QMD indexes your documents and provides fast keyword search, semantic similarity search, and intelligent hybrid queries that fuse multiple search signals for best results.

The system uses a content-addressable storage architecture with SQLite, supporting multiple document collections with hierarchical context annotations. QMD exposes both a CLI tool and an MCP (Model Context Protocol) server for AI agent integration, plus a TypeScript SDK for programmatic access. Documents are chunked using smart boundary detection to keep semantic units together, then embedded for vector search with configurable models including EmbeddingGemma and Qwen3.

## Installation

```bash
# Install globally
npm install -g @tobilu/qmd
# or
bun install -g @tobilu/qmd

# Run directly without installation
npx @tobilu/qmd ...
bunx @tobilu/qmd ...
```

## CLI: Create and Manage Collections

Collections are directories of documents that QMD indexes. Add collections to start searching your knowledge base.

```bash
# Create collections for your notes, docs, and meeting transcripts
qmd collection add ~/notes --name notes
qmd collection add ~/Documents/meetings --name meetings
qmd collection add ~/work/docs --name docs --mask "**/*.md"

# List all collections
qmd collection list

# Remove a collection
qmd collection remove myproject

# Rename a collection
qmd collection rename old-name new-name

# List files in a collection
qmd ls notes
qmd ls notes/subfolder
```

## CLI: Add Context to Collections

Context adds descriptive metadata that improves search relevance and is returned alongside results.

```bash
# Add context to a collection using qmd:// virtual paths
qmd context add qmd://notes "Personal notes and ideas"
qmd context add qmd://docs/api "API documentation"

# Add context from within a collection directory
cd ~/notes && qmd context add "Personal notes and ideas"
cd ~/notes/work && qmd context add "Work-related notes"

# Add global context (applies to all collections)
qmd context add / "Knowledge base for my projects"

# List all contexts
qmd context list

# Remove context
qmd context rm qmd://notes/old
```

## CLI: Index and Embed Documents

Re-index collections and generate vector embeddings for semantic search capabilities.

```bash
# Re-index all collections (scan filesystem for changes)
qmd update

# Re-index with git pull first (for remote repos)
qmd update --pull

# Generate embeddings for semantic search (900 tokens/chunk, 15% overlap)
qmd embed

# Force re-embed everything
qmd embed -f

# Show index status
qmd status
```

## CLI: BM25 Keyword Search

Fast full-text search using BM25 algorithm with SQLite FTS5. Supports exact phrases and negation.

```bash
# Basic keyword search
qmd search "authentication flow"

# Search with minimum score threshold
qmd search "API design patterns" --min-score 0.3

# Limit results
qmd search "error handling" -n 10

# Search within a specific collection
qmd search "API" -c notes

# Output as JSON for scripting
qmd search "quarterly reports" --json

# Output as markdown for LLM context
qmd search --md --full "error handling"

# Show all matches with file paths
qmd search "API" --all --files --min-score 0.3
```

## CLI: Vector Semantic Search

Semantic similarity search using embeddings. Finds documents by meaning, not just exact keywords.

```bash
# Semantic search (requires embeddings)
qmd vsearch "how to deploy"

# Vector search with options
qmd vsearch "user authentication process" -n 10 --min-score 0.5
```

## CLI: Hybrid Search with Query Expansion and Reranking

The `query` command provides the highest quality results by combining BM25 + vector search with LLM query expansion and reranking.

```bash
# Hybrid search with re-ranking (best quality)
qmd query "user authentication"

# With intent for disambiguation
qmd query --intent "web performance and latency" "performance"

# Multi-line structured query with typed sub-queries
qmd query $'lex: rate limiter algorithm\nvec: how does rate limiting work in the API'

# With hypothetical document (hyde)
qmd query $'lex: keywords\nvec: question\nhyde: hypothetical answer passage...'

# Inspect how results were scored
qmd query --json --explain "quarterly reports"

# Get 10 results with minimum score
qmd query -n 10 --min-score 0.3 "API design patterns"
```

## CLI: Document Retrieval

Retrieve specific documents by path, docid, or glob pattern.

```bash
# Get document by filepath
qmd get notes/meeting.md

# Get document by docid (from search results)
qmd get "#abc123"

# Get document starting at line 50, max 100 lines
qmd get notes/meeting.md:50 -l 100

# Get multiple documents by glob pattern
qmd multi-get "journals/2025-05*.md"

# Get multiple documents by comma-separated list
qmd multi-get "doc1.md, doc2.md, #abc123"

# Limit multi-get to files under 20KB
qmd multi-get "docs/*.md" --max-bytes 20480

# Output multi-get as JSON
qmd multi-get "docs/*.md" --json
```

## SDK: Create and Configure Store

Use QMD as a library in Node.js or Bun applications. The SDK provides programmatic access to all search and indexing features.

```typescript
import { createStore } from '@tobilu/qmd'

// Mode 1: Inline config (no files needed besides the DB)
const store = await createStore({
  dbPath: './my-index.sqlite',
  config: {
    collections: {
      docs: { path: '/path/to/docs', pattern: '**/*.md' },
      notes: { path: '/path/to/notes' },
    },
  },
})

// Mode 2: YAML config file
const store2 = await createStore({
  dbPath: './index.sqlite',
  configPath: './qmd.yml',
})

// Mode 3: DB-only (reopen previously configured store)
const store3 = await createStore({ dbPath: './index.sqlite' })

// Always close when done
await store.close()
```

## SDK: Search with Query Expansion

The unified `search()` method handles both simple queries and pre-expanded structured queries with optional LLM reranking.

```typescript
import { createStore } from '@tobilu/qmd'

const store = await createStore({
  dbPath: './index.sqlite',
  config: { collections: { docs: { path: './docs' } } },
})

// Simple query (auto-expanded via LLM, then BM25 + vector + reranking)
const results = await store.search({ query: "authentication flow" })
console.log(results.map(r => `${r.title} (${Math.round(r.score * 100)}%)`))

// With options
const results2 = await store.search({
  query: "rate limiting",
  intent: "API throttling and abuse prevention",
  collection: "docs",
  limit: 5,
  minScore: 0.3,
  explain: true,  // Include retrieval score traces
})

// Pre-expanded queries (skip auto-expansion, control each sub-query)
const results3 = await store.search({
  queries: [
    { type: 'lex', query: '"connection pool" timeout -redis' },
    { type: 'vec', query: 'why do database connections time out under load' },
  ],
  collections: ["docs", "notes"],
})

// Skip reranking for faster results
const fast = await store.search({ query: "auth", rerank: false })

await store.close()
```

## SDK: Direct BM25 and Vector Search

Access the underlying search backends directly for fine-grained control.

```typescript
import { createStore } from '@tobilu/qmd'

const store = await createStore({
  dbPath: './index.sqlite',
  config: { collections: { docs: { path: './docs' } } },
})

// BM25 keyword search (fast, no LLM)
const lexResults = await store.searchLex("auth middleware", { limit: 10 })
console.log('BM25 results:', lexResults.map(r => r.displayPath))

// Vector similarity search (embedding model, no reranking)
const vecResults = await store.searchVector("how users log in", { limit: 10 })
console.log('Vector results:', vecResults.map(r => r.displayPath))

// Manual query expansion for full control
const expanded = await store.expandQuery("auth flow", { intent: "user login" })
console.log('Expanded queries:', expanded)
// => [{ type: 'lex', query: 'auth login' }, { type: 'vec', query: 'user authentication' }, ...]

// Use expanded queries
const results = await store.search({ queries: expanded })

await store.close()
```

## SDK: Document Retrieval

Retrieve documents by path, docid, or glob pattern with optional line slicing.

```typescript
import { createStore } from '@tobilu/qmd'

const store = await createStore({
  dbPath: './index.sqlite',
  config: { collections: { docs: { path: './docs' } } },
})

// Get a document by path or docid
const doc = await store.get("docs/readme.md")
const byId = await store.get("#abc123")

if (!("error" in doc)) {
  console.log(doc.title, doc.displayPath, doc.context)
  console.log('Docid:', doc.docid)  // Short 6-char hash for quick reference
}

// Get document body with line range
const body = await store.getDocumentBody("docs/readme.md", {
  fromLine: 50,
  maxLines: 100,
})

// Batch retrieve by glob or comma-separated list
const { docs, errors } = await store.multiGet("docs/**/*.md", {
  maxBytes: 20480,  // Skip files larger than 20KB
})

for (const result of docs) {
  if (!result.skipped) {
    console.log(result.doc.displayPath, result.doc.title)
  }
}

await store.close()
```

## SDK: Collection Management

Add, remove, rename, and list collections programmatically.

```typescript
import { createStore } from '@tobilu/qmd'

const store = await createStore({
  dbPath: './index.sqlite',
  config: { collections: {} },
})

// Add a collection
await store.addCollection("myapp", {
  path: "/src/myapp",
  pattern: "**/*.ts",
  ignore: ["node_modules/**", "*.test.ts"],
})

// List collections with document stats
const collections = await store.listCollections()
for (const col of collections) {
  console.log(`${col.name}: ${col.active_count} docs, pattern: ${col.glob_pattern}`)
}

// Get names of collections included in queries by default
const defaults = await store.getDefaultCollectionNames()

// Rename collection
await store.renameCollection("old-name", "new-name")

// Remove collection
await store.removeCollection("myapp")

await store.close()
```

## SDK: Context Management

Add descriptive metadata to collections and paths to improve search relevance.

```typescript
import { createStore } from '@tobilu/qmd'

const store = await createStore({
  dbPath: './index.sqlite',
  config: { collections: { docs: { path: './docs' } } },
})

// Add context for a path within a collection
await store.addContext("docs", "/api", "REST API reference documentation")
await store.addContext("docs", "/guides", "Step-by-step tutorials")

// Set global context (applies to all collections)
await store.setGlobalContext("Internal engineering documentation")

// Get global context
const globalCtx = await store.getGlobalContext()

// List all contexts
const contexts = await store.listContexts()
for (const ctx of contexts) {
  console.log(`${ctx.collection}${ctx.path}: ${ctx.context}`)
}

// Remove context
await store.removeContext("docs", "/api")
await store.setGlobalContext(undefined)  // Clear global

await store.close()
```

## SDK: Indexing and Embedding

Re-index collections and generate vector embeddings with progress callbacks.

```typescript
import { createStore } from '@tobilu/qmd'

const store = await createStore({
  dbPath: './index.sqlite',
  config: { collections: { docs: { path: './docs' } } },
})

// Re-index collections by scanning the filesystem
const indexResult = await store.update({
  collections: ["docs"],  // Optional, defaults to all
  onProgress: ({ collection, file, current, total }) => {
    console.log(`[${collection}] ${current}/${total} ${file}`)
  },
})
console.log(`Indexed: ${indexResult.indexed}, Updated: ${indexResult.updated}`)
console.log(`Needs embedding: ${indexResult.needsEmbedding}`)

// Generate vector embeddings
const embedResult = await store.embed({
  force: false,  // true to re-embed everything
  onProgress: ({ chunksEmbedded, totalChunks, bytesProcessed, totalBytes }) => {
    const pct = Math.round((chunksEmbedded / totalChunks) * 100)
    console.log(`Embedding ${pct}% (${chunksEmbedded}/${totalChunks} chunks)`)
  },
})
console.log(`Embedded ${embedResult.chunksEmbedded} chunks in ${embedResult.durationMs}ms`)

await store.close()
```

## SDK: Index Health and Status

Check index health and document statistics.

```typescript
import { createStore } from '@tobilu/qmd'

const store = await createStore({ dbPath: './index.sqlite' })

// Get index status (document counts, collections, embedding state)
const status = await store.getStatus()
console.log(`Total documents: ${status.totalDocuments}`)
console.log(`Needs embedding: ${status.needsEmbedding}`)
console.log(`Vector index: ${status.hasVectorIndex}`)
for (const col of status.collections) {
  console.log(`  ${col.name}: ${col.documents} docs`)
}

// Get index health info (stale embeddings, etc.)
const health = await store.getIndexHealth()
console.log(`Needs embedding: ${health.needsEmbedding}/${health.totalDocs}`)
if (health.daysStale !== null) {
  console.log(`Index is ${health.daysStale} days stale`)
}

await store.close()
```

## MCP Server: Configuration

QMD exposes an MCP server for AI agent integration. Configure it in Claude Desktop or Claude Code.

```json
// Claude Desktop: ~/Library/Application Support/Claude/claude_desktop_config.json
{
  "mcpServers": {
    "qmd": {
      "command": "qmd",
      "args": ["mcp"]
    }
  }
}
```

```json
// Claude Code: ~/.claude/settings.json
{
  "mcpServers": {
    "qmd": {
      "command": "qmd",
      "args": ["mcp"]
    }
  }
}
```

```bash
# Or install the plugin for Claude Code (recommended)
claude plugin marketplace add tobi/qmd
claude plugin install qmd@qmd
```

## MCP Server: HTTP Transport

Run a shared HTTP server that avoids repeated model loading across clients.

```bash
# Foreground server (Ctrl-C to stop)
qmd mcp --http                    # localhost:8181
qmd mcp --http --port 8080        # Custom port

# Background daemon
qmd mcp --http --daemon           # Start, writes PID to ~/.cache/qmd/mcp.pid
qmd mcp stop                      # Stop via PID file
qmd status                        # Shows "MCP: running (PID ...)" when active
```

## MCP/HTTP: Query Tool

Search the knowledge base using typed sub-queries combined for best recall.

```json
// POST http://localhost:8181/query
{
  "searches": [
    { "type": "lex", "query": "\"connection pool\" timeout -redis" },
    { "type": "vec", "query": "why do database connections time out under load" },
    { "type": "hyde", "query": "Connection pool exhaustion occurs when all connections are in use..." }
  ],
  "collections": ["docs"],
  "limit": 10,
  "minScore": 0.3,
  "intent": "database performance troubleshooting"
}
```

```bash
# Example with curl
curl -X POST http://localhost:8181/query \
  -H "Content-Type: application/json" \
  -d '{
    "searches": [
      {"type": "lex", "query": "CAP theorem"},
      {"type": "vec", "query": "consistency vs availability tradeoff"}
    ],
    "limit": 5
  }'

# Response format:
# {
#   "results": [
#     {
#       "docid": "#abc123",
#       "file": "distributed-systems/cap.md",
#       "title": "CAP Theorem",
#       "score": 0.87,
#       "context": "Distributed systems documentation",
#       "snippet": "@@ -15,4 @@ (14 before, 20 after)\n15: The CAP theorem states..."
#     }
#   ]
# }
```

## Query Syntax: Lex (BM25 Keywords)

Lex queries support special syntax for precise keyword matching with phrase and negation support.

```
# Prefix match (default)
lex: perf                         # Matches "performance", "performing", etc.

# Exact phrase (must appear verbatim)
lex: "machine learning"

# Exclude term
lex: performance -sports

# Exclude phrase
lex: "machine learning" -"deep learning"

# Combined
lex: "rate limiter" algorithm -redis -memcached
lex: auth middleware typescript -test -mock
```

## Query Syntax: Vec and Hyde (Semantic)

Vec queries are natural language questions. Hyde queries are hypothetical answer passages (50-100 words).

```
# Vec: Write what you're looking for as a question
vec: how does the rate limiter handle burst traffic
vec: what is the tradeoff between consistency and availability

# Hyde: Write what you expect the answer to look like
hyde: The rate limiter uses a token bucket algorithm. When a client exceeds 100 requests per minute, subsequent requests return 429 Too Many Requests until the window resets.

hyde: Connection pool exhaustion occurs when all database connections are in use and new requests must wait. This typically happens under high concurrency when queries run longer than expected.
```

## Query Syntax: Multi-Line Structured Queries

Combine multiple query types for best results. First query gets 2x weight in RRF fusion.

```
# CLI: Multi-line with bash $'...' syntax
qmd query $'lex: CAP theorem consistency\nvec: what is the tradeoff between consistency and availability'

# With intent for disambiguation
qmd query $'intent: web performance optimization\nlex: performance\nvec: how to improve page load times'

# Full structured query
qmd query $'intent: API rate limiting\nlex: "rate limiter" algorithm\nvec: how does rate limiting work\nhyde: The API uses a sliding window rate limiter that tracks requests per client over a 60-second window...'
```

## Utility Functions

QMD exports utility functions for working with search results and document content.

```typescript
import { extractSnippet, addLineNumbers, DEFAULT_MULTI_GET_MAX_BYTES } from '@tobilu/qmd'

// Extract a relevant snippet from document text
const body = "# Guide\n\nThis section covers authentication...\n\nLogin flow starts here..."
const { line, snippet, linesBefore, linesAfter } = extractSnippet(body, "authentication", 300)
console.log(`Best match at line ${line}`)
console.log(snippet)
// Output: @@ -3,2 @@ (2 before, 1 after)
//         This section covers authentication...

// Add line numbers to text
const numbered = addLineNumbers("line one\nline two\nline three", 10)
console.log(numbered)
// Output:
// 10: line one
// 11: line two
// 12: line three

// Default max bytes for multi-get (10KB)
console.log(`Default max bytes: ${DEFAULT_MULTI_GET_MAX_BYTES}`)
```

## Summary

QMD provides a complete local search solution for markdown knowledge bases, combining fast BM25 keyword search with semantic vector search and LLM reranking. The hybrid search pipeline uses Reciprocal Rank Fusion (RRF) to merge results from multiple query types (lex, vec, hyde), with position-aware score blending that protects high-confidence retrieval results while allowing the reranker to surface relevant content that pure keyword matching might miss.

Integration patterns include: CLI for interactive use and shell scripts, SDK for Node.js/Bun applications with full programmatic control, MCP server for AI agent integration via Claude Desktop or Claude Code, and HTTP REST endpoints for language-agnostic access. Documents are organized into collections with hierarchical context annotations that improve both search relevance and result interpretation. The content-addressable storage architecture enables efficient deduplication and change detection, while smart chunking preserves semantic boundaries when embedding long documents.
