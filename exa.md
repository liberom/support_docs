### Install Exa SDK

Source: https://exa.ai/docs/reference/contents-quickstart

Commands to install the required Exa SDK packages for Python and JavaScript environments.

```bash
pip install exa-py
```

```bash
npm install exa-js
```

--------------------------------

### Quick Start and Configuration

Source: https://exa.ai/docs/reference/vercel

Examples demonstrating how to initialize a web search tool within the Vercel AI SDK generateText function, including basic and advanced search configurations.

```typescript
import { generateText, stepCountIs } from "ai";
import { webSearch } from "@exalabs/ai-sdk";
import { openai } from "@ai-sdk/openai";

const { text } = await generateText({
  model: openai('gpt-5-nano'),
  prompt: 'Tell me the latest developments in AI',
  system: "Only use web search once per turn. Answer based on the information you have.",
  tools: {
    webSearch: webSearch(),
  },
  stopWhen: stepCountIs(3),
});

console.log(text);
```

```typescript
const { text } = await generateText({
  model: openai('gpt-5-nano'),
  prompt: 'Find the top AI companies in Europe founded after 2018',
  tools: {
    webSearch: webSearch({
      type: "auto",
      numResults: 6,
      category: "company",
      contents: {
        text: { maxCharacters: 1000 },
        livecrawl: "preferred",
        summary: true,
      },
    }),
  },
  stopWhen: stepCountIs(5),
});

console.log(text);
```

--------------------------------

### Fetch Website Content with Exa

Source: https://exa.ai/docs/reference/contents-quickstart

Demonstrates how to initialize the Exa client and retrieve content highlights from a specific URL. Requires a valid API key from the Exa Dashboard.

```python
from exa_py import Exa

exa = Exa(api_key="your-api-key")

result = exa.get_contents(
  ["tesla.com"],
  highlights={"max_characters": 4000}
)
```

```javascript
import Exa from "exa-js";

const exa = new Exa("your-api-key");

const result = await exa.getContents(["tesla.com"], {
  highlights: {
    maxCharacters: 4000,
  },
});
```

```bash
curl -X POST https://api.exa.ai/contents \
  --header "content-type: application/json" \
  --header "x-api-key: your-api-key" \
  --data '{
      "ids": ["tesla.com"],
      "highlights": {
        "maxCharacters": 4000
      }
    }'
```

--------------------------------

### Perform Search Request with Exa

Source: https://exa.ai/docs/reference/search-quickstart

Demonstrates how to initialize the Exa client and execute a search query with content highlights. Requires a valid API key obtained from the Exa Dashboard.

```python
from exa_py import Exa

exa = Exa(api_key="your-api-key")

result = exa.search(
  "blog post about artificial intelligence",
  type="auto",
  contents={
    "highlights": {
      "max_characters": 4000
    }
  }
)
```

```javascript
import Exa from "exa-js";

const exa = new Exa("your-api-key");

const result = await exa.search(
  "blog post about artificial intelligence",
  {
    type: "auto",
    contents: {
      highlights: {
        maxCharacters: 4000
      }
    }
  }
);
```

```bash
curl --request POST \
  --url https://api.exa.ai/search \
  --header "accept: application/json" \
  --header "content-type: application/json" \
  --header "x-api-key: your-api-key" \
  --data '{
    "query": "blog post about artificial intelligence",
    "type": "auto",
    "contents": {
      "highlights": {
        "maxCharacters": 4000
      }
    }
  }'
```

--------------------------------

### Install Exa AI SDK

Source: https://exa.ai/docs/reference/vercel

Command to install the Exa AI SDK package via npm.

```bash
npm install @exalabs/ai-sdk
```

--------------------------------

### Install Exa and OpenAI LangChain libraries

Source: https://exa.ai/docs/reference/langchain

Install the necessary Python packages to enable Exa search capabilities and OpenAI integration within the LangChain framework.

```Bash
pip install langchain-openai langchain-exa
```

--------------------------------

### Install Dependencies

Source: https://exa.ai/docs/reference/anthropic-tool-calling

Install the required Python packages for Anthropic API interaction, Exa search, and console output formatting.

```bash
pip install anthropic exa_py rich
```

--------------------------------

### Install Required Libraries

Source: https://exa.ai/docs/reference/openai-tool-calling

Installs the necessary Python packages including OpenAI, Exa, and Rich for API interaction and output formatting.

```shell
pip install openai exa_py rich
```

--------------------------------

### Environment Variable Setup

Source: https://exa.ai/docs/reference/vercel

Instructions for configuring the Exa API key in a project environment file.

```bash
EXA_API_KEY=your-api-key-here
```

--------------------------------

### JavaScript: Tool Description Examples

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Illustrates good and bad examples of tool descriptions for LLMs, focusing on providing clear usage guidance and context. The 'Good' example includes specific instructions on how to use categories and when not to use them.

```javascript
// Bad — leaves the LLM guessing
"Search the internet"

// Good — tells the LLM exactly how to use the tool
"Search the web via Exa. Write queries as natural language.\n" +
"CATEGORIES - Use sparingly:\n" +
"- company: ONLY for 'what does X company do'\n" +
"- people: ONLY for non-public figures\n" +
"For news, sports, general facts - DO NOT use a category."
```

```javascript
// Bad
"Performs a web search"

// Good
"Use this for deep investigation when keyword search isn't enough — it runs " +
"a multi-step research pipeline that searches, reads pages, and synthesizes " +
"findings. Especially useful for finding contradicting evidence, alternative " +
"approaches, or version-specific caveats."
```

```javascript
// Bad
{ "description": "The query" }

// Good
{ "description": "The search query. Write descriptive, natural language queries for best results." }
```

--------------------------------

### JavaScript: Referential Query Expansion Examples

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Illustrates how to expand vague, referential queries in multi-turn conversations with LLMs. The 'Good' examples provide more context and specificity.

```javascript
```diff  theme={null}
- "competitors" (after discussing Stripe)
+ "Stripe competitors in payment processing"

- "how do I set it up"
+ "how to set up Exa web search integration in a Python project"
```
```

--------------------------------

### POST /context

Source: https://exa.ai/docs/reference/context

Searches for and retrieves relevant code snippets and examples based on a given query. This endpoint is useful for finding practical code examples for framework usage, API syntax, development setup, library implementation, and best practices.

```APIDOC
## POST /context

### Description
Searches for and retrieves relevant code snippets and examples based on a given query. This endpoint is useful for finding practical code examples for framework usage, API syntax, development setup, library implementation, and best practices.

### Method
POST

### Endpoint
`https://api.exa.ai/context`

### Parameters
#### Request Body
- **query** (string) - Required - Search query to find relevant code snippets. Min Length: 1 character, Max Length: 2000 characters.
- **tokensNum** (integer or "dynamic") - Optional - The number of tokens to return. If set to "dynamic", the API will attempt to return a suitable number of tokens based on the query. Defaults to a reasonable number if not specified.

### Request Example
```json
{
  "query": "how to use React hooks for state management",
  "tokensNum": 5000
}
```

### Response
#### Success Response (200)
- **requestId** (string) - A unique identifier for the request.
- **query** (string) - The original search query.
- **response** (string) - Formatted code snippets and contextual examples.
- **resultsCount** (integer) - The number of results found.
- **costDollars** (object or string) - The cost of the request in dollars. Can be an object detailing costs or a string representing the total cost.
- **searchTime** (float) - The time taken for the search in seconds.
- **outputTokens** (integer) - The number of output tokens generated.

#### Response Example
```json
{
  "requestId": "req_12345",
  "query": "how to use React hooks for state management",
  "response": "## State Management with useState Hook in React\n\nhttps://www.geeksforgeeks.org/reactjs/state-management-with-usestate-hook-in-react/\n\n```\nimport React, {\n  useState\n} from 'react';\n\nfunction InputField() {\n  const [name, setName] = useState('');\n\n  const handleChange = (event) => {\n    setName(event.target.value);\n  }\n\n  return (\n    <div>\n      Name:\n      <input onChange={handleChange} />\n      Entered name: {name}\n    </div>\n  );\n}\n\nexport default InputField;\n```\n\n...(response continues with more code examples)",
  "resultsCount": 502,
  "costDollars": {"total":1,"search":{"neural":1}},
  "searchTime": 3112.290825000033,
  "outputTokens": 4805
}
```
```

--------------------------------

### JavaScript: Query Style Examples

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Demonstrates the difference between keyword-style and semantic, natural language queries for LLMs. The 'Good' examples are more descriptive and specific, leading to better search results.

```javascript
```diff  theme={null}
- "TSLA stock price"
+ "Tesla current stock performance and price"

- "AI startups"
+ "AI startups founded in 2025 that have raised Series A funding in the healthcare space"
```
```

--------------------------------

### Find Similar Links using Exa API (Bash, Python, JavaScript)

Source: https://exa.ai/docs/reference/find-similar-links

This snippet demonstrates how to find links similar to a given URL using the Exa Search API. It includes examples for Bash, Python, and JavaScript, showing how to make the POST request and handle the response. Ensure you have the necessary libraries installed for Python and JavaScript, and replace 'YOUR_EXA_API_KEY' with your actual API key.

```bash
curl -X POST 'https://api.exa.ai/findSimilar' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "url": "https://arxiv.org/abs/2307.06435",
    "contents": {
      "text": true
    }
  }'
```

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

results = exa.find_similar_and_contents(
    url="https://arxiv.org/abs/2307.06435",
    text=True
)

print(results)
```

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const results = await exa.findSimilarAndContents(
    'https://arxiv.org/abs/2307.06435',
    { text: true }
);

console.log(results);
```

--------------------------------

### Exa Research API - Python Example

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

Example of how to use the Exa Research API with Python to get research summaries.

```APIDOC
## POST /responses

### Description
This endpoint allows you to query Exa's research models to get summarized information on a given topic.

### Method
POST

### Endpoint
https://api.exa.ai/responses

### Parameters
#### Query Parameters
None

#### Request Body
- **input** (string) - Required - The research query or topic.
- **model** (string) - Required - The research model to use (e.g., `exa-research`, `exa-research-pro`).

### Request Example
```json
{
  "input": "Summarize the impact of CRISPR on gene therapy with recent developments",
  "model": "exa-research"
}
```

### Response
#### Success Response (200)
- **output** (string) - The research summary generated by the model.

#### Response Example
```json
{
  "output": "CRISPR technology has revolutionized gene therapy by enabling precise gene editing. Recent developments include advancements in delivery methods and the application of CRISPR for treating genetic disorders like sickle cell anemia and cystic fibrosis, although ethical considerations and long-term effects are still under investigation."
}
```
```

--------------------------------

### X/Twitter Search Agent Skill Setup

Source: https://exa.ai/docs/reference/x-search-claude-skill

Instructions for installing Exa MCP and adding the Claude skill for searching tweets.

```APIDOC
## Exa MCP Installation

### Description
Install or update Exa MCP in your MCP configuration.

### Method
Terminal Command

### Endpoint
N/A

### Parameters
N/A

### Request Example
```bash
claude mcp add --transport http exa "https://mcp.exa.ai/mcp?tools=web_search_advanced_exa"
```

### Response
N/A

---

## Claude Skill Addition

### Description
Add the `web-search-advanced-tweet` Claude skill to your configuration.

### Method
Claude Code Configuration

### Endpoint
N/A

### Parameters
N/A

### Request Example
```yaml
---
name: web-search-advanced-tweet
description: Search tweets and Twitter/X content using Exa advanced search. Limited filter support - text and domain filters are NOT supported. Use when searching for tweets, Twitter/X discussions, or social media sentiment.
context: fork
---

# Web Search Advanced - Tweet Category

## Tool Restriction (Critical)
ONLY use `web_search_advanced_exa` with `category: "tweet"`. Do NOT use other categories or tools.

## Filter Restrictions (Critical)
The `tweet` category has **LIMITED filter support**. The following parameters are **NOT supported** and will cause 400 errors:

- `includeText` - NOT SUPPORTED
- `excludeText` - NOT SUPPORTED
- `includeDomains` - NOT SUPPORTED
- `excludeDomains` - NOT SUPPORTED
- `moderation` - NOT SUPPORTED (causes 500 server error)

## Supported Parameters

### Core
- `query` (required)
- `numResults`
- `type` ("auto", "fast", "deep", "neural")

### Date filtering (ISO 8601) - Use these instead of text filters!
- `startPublishedDate` / `endPublishedDate`
- `startCrawlDate` / `endCrawlDate`

### Content extraction
- `textMaxCharacters` / `contextMaxCharacters`
- `enableHighlights` / `highlightsNumSentences` / `highlightsPerUrl` / `highlightsQuery`
- `enableSummary` / `summaryQuery`

### Additional
- `additionalQueries` - useful for hashtag variations
- `livecrawl` / `livecrawlTimeout` - use "preferred" for recent tweets

## Token Isolation (Critical)
Never run Exa searches in main context. Always spawn Task agents:
- Agent calls `web_search_advanced_exa` with `category: "tweet"`
- Agent merges + deduplicates results before presenting
- Agent returns distilled output (brief markdown or compact JSON)
- Main context stays clean regardless of search volume

## When to Use

Use this category when you need:
- Social discussions on a topic
- Product announcements from company accounts
- Developer opinions and experiences
- Trending topics and community sentiment
- Expert takes and threads

## Examples

Recent tweets on a topic:
```
web_search_advanced_exa {
  "query": "Claude Code MCP experience",
  "category": "tweet",
  "startPublishedDate": "2025-01-01",
  "numResults": 20,
  "type": "auto",
  "livecrawl": "preferred"
}
```

Search with specific keywords (put keywords in query, not includeText):
```
web_search_advanced_exa {
  "query": "launching announcing new open source release",
  "category": "tweet",
  "startPublishedDate": "2025-12-01",
  "numResults": 15,
  "type": "auto"
}
```

Developer sentiment (use specific query terms instead of excludeText):
```
web_search_advanced_exa {
  "query": "developer experience DX frustrating painful",
  "category": "tweet",
  "numResults": 20,
  "type": "deep",
  "livecrawl": "preferred"
}
```

## Output Format

Return:
1) Results (tweet content, author handle, date, engagement if visible)
2) Sources (Tweet URLs)
3) Notes (sentiment summary, notable accounts, threads vs single tweets)

Important: Be aware that tweet content can be informal, sarcastic, or context-dependent.
```

### Response
N/A

---

### Restart Claude Code

### Description
Ask the user to restart Claude Code for the configuration changes to take effect.

### Method
User Instruction

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A
```

--------------------------------

### Install Exa and CrewAI dependencies

Source: https://exa.ai/docs/reference/crewai

Installs the core CrewAI framework, built-in tools, and the Exa Python SDK required for semantic search capabilities.

```Bash
pip install crewai 'crewai[tools]' exa_py
```

--------------------------------

### Install Exa AI and LlamaIndex Libraries

Source: https://exa.ai/docs/reference/llamaindex

Installs the required Python libraries for Exa AI integration with LlamaIndex. This includes the core LlamaIndex libraries and the Exa-specific tools. OpenAI dependencies are managed within the core library.

```Python
pip install llama-index llama-index-core llama-index-tools-exa
```

--------------------------------

### Exa Research API - JavaScript Example

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

Example of how to use the Exa Research API with JavaScript to get research summaries.

```APIDOC
## POST /responses (JavaScript)

### Description
This endpoint allows you to query Exa's research models to get summarized information on a given topic using JavaScript.

### Method
POST

### Endpoint
https://api.exa.ai/responses

### Parameters
#### Query Parameters
None

#### Request Body
- **input** (string) - Required - The research query or topic.
- **model** (string) - Required - The research model to use (e.g., `exa-research`, `exa-research-pro`).

### Request Example
```javascript
{
  "input": "Summarize the impact of CRISPR on gene therapy with recent developments",
  "model": "exa-research"
}
```

### Response
#### Success Response (200)
- **output** (string) - The research summary generated by the model.

#### Response Example
```json
{
  "output": "CRISPR technology has revolutionized gene therapy by enabling precise gene editing. Recent developments include advancements in delivery methods and the application of CRISPR for treating genetic disorders like sickle cell anemia and cystic fibrosis, although ethical considerations and long-term effects are still under investigation."
}
```
```

--------------------------------

### Exa Research API - cURL Example

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

Example of how to use the Exa Research API with cURL to get research summaries.

```APIDOC
## POST /responses (cURL)

### Description
This endpoint allows you to query Exa's research models to get summarized information on a given topic using cURL.

### Method
POST

### Endpoint
https://api.exa.ai/responses

### Parameters
#### Query Parameters
None

#### Request Body
- **input** (string) - Required - The research query or topic.
- **model** (string) - Required - The research model to use (e.g., `exa-research`, `exa-research-pro`).

### Request Example
```bash
curl --location 'https://api.exa.ai/responses' \
--header 'x-api-key: YOUR_EXA_API_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "input": "Summarize the impact of CRISPR on gene therapy with recent developments",
    "model": "exa-research"
}'
```

### Response
#### Success Response (200)
- **output** (string) - The research summary generated by the model.

#### Response Example
```json
{
  "output": "CRISPR technology has revolutionized gene therapy by enabling precise gene editing. Recent developments include advancements in delivery methods and the application of CRISPR for treating genetic disorders like sickle cell anemia and cystic fibrosis, although ethical considerations and long-term effects are still under investigation."
}
```
```

--------------------------------

### List Research Tasks using JavaScript

Source: https://exa.ai/docs/reference/research/list-tasks

This JavaScript code snippet demonstrates how to list research tasks using the exa-js library. Install the library (`npm install exa-js`) and replace 'YOUR_EXA_API_KEY' with your valid API key.

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const tasks = await exa.research.listTasks({ limit: 10 });
console.log(tasks);
```

--------------------------------

### Execute Exa Search Example

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

An asynchronous wrapper function to execute a search query and handle the resulting response, suitable for Node.js environments.

```javascript
async function runExaSearchExample() {
  const userQuery = process.argv[2] || "What's the latest news about AI?";
  const result = await run_exa_search(userQuery);
  return result;
}

if (require.main === module) {
  runExaSearchExample().catch(console.error);
}
```

--------------------------------

### JavaScript: Category Usage Examples

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Provides examples of appropriate and inappropriate category usage in LLM queries. It highlights when to use categories like 'company' or 'research paper' and when to omit them.

```javascript
```diff  theme={null}
- category="news" for "latest AI developments"       (just search without category)
- category="people" for "Elon Musk interview"        (public figure, don't use people)
+ category="company" for "what does Stripe do"        (company research)
+ category="research paper" for "transformer attention mechanisms arxiv"
```
```

--------------------------------

### JavaScript: Query Year Correction Example

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Shows how to correct LLM queries that might use outdated years. The 'Good' example specifies the current year for more relevant results.

```javascript
```diff  theme={null}
- "NFL draft picks"
+ "2026 NFL draft projections and mock drafts"
```
```

--------------------------------

### POST /search

Source: https://exa.ai/docs/reference/search

Perform a search with an Exa prompt-engineered query and retrieve a list of relevant results. Optionally get contents.

```APIDOC
## POST /search

### Description
Perform a search with an Exa prompt-engineered query and retrieve a list of relevant results. Optionally get contents.

### Method
POST

### Endpoint
/search

### Parameters
#### Request Body
- **query** (string) - Required - The query string for the search.
- **additionalQueries** (array of strings) - Optional - Additional query variations for deep search. Only works with type="deep" or type="deep-reasoning". When provided, these queries are used alongside the main query for comprehensive results.
- **outputSchema** (object) - Optional - JSON schema for deep search structured output mode. When provided, the output.content field is returned as structured JSON matching this schema.
- **type** (string) - Optional - The type of search. Supported values: neural, fast, auto, deep, deep-reasoning, instant. Defaults to 'auto'.
- **category** (string) - Optional - A data category to focus on. Supported values: company, research paper, news, tweet, personal site, financial report, people.
- **userLocation** (string) - Optional - The two-letter ISO country code of the user, e.g. US.

### Request Example
```json
{
  "query": "Latest developments in LLM capabilities",
  "type": "auto",
  "category": "research paper"
}
```

### Response
#### Success Response (200)
- **results** (array) - A list of search results.
- **autoprompt** (string) - The autoprompt used for the search.
- **usedQuery** (string) - The actual query used for the search.

#### Response Example
```json
{
  "results": [
    {
      "title": "Example Research Paper",
      "url": "http://example.com/paper",
      "score": 0.95,
      "publishedDate": "2023-10-27",
      "author": "Dr. AI Researcher",
      "text": "This paper discusses the latest advancements..."
    }
  ],
  "autoprompt": "Latest developments in LLM capabilities",
  "usedQuery": "Latest developments in LLM capabilities"
}
```
```

--------------------------------

### Example: Search Tweets with Keywords

Source: https://exa.ai/docs/reference/x-search-claude-skill

Shows an example of searching for tweets using specific keywords within the `query` parameter, suitable for finding announcements or launch-related discussions.

```json
web_search_advanced_exa {
  "query": "launching announcing new open source release",
  "category": "tweet",
  "startPublishedDate": "2025-12-01",
  "numResults": 15,
  "type": "auto"
}
```

--------------------------------

### Exa Search API

Source: https://exa.ai/docs/reference/search-quickstart

This endpoint allows you to search for content using Exa's powerful search engine. You can specify search queries, content types, and desired output formats.

```APIDOC
## POST /search

### Description
Searches for content based on the provided query and parameters.

### Method
POST

### Endpoint
https://api.exa.ai/search

### Parameters
#### Query Parameters
None

#### Request Body
- **query** (string) - Required - The search query string.
- **type** (string) - Optional - The type of search to perform (e.g., 'auto', 'web'). Defaults to 'auto'.
- **contents** (object) - Optional - Specifies the content to retrieve and format.
  - **highlights** (object) - Optional - Configuration for content highlights.
    - **max_characters** (integer) - Optional - Maximum characters for highlights. (Note: In JS SDK, this is camelCased as `maxCharacters`)

### Request Example
```json
{
  "query": "blog post about artificial intelligence",
  "type": "auto",
  "contents": {
    "highlights": {
      "maxCharacters": 4000
    }
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - A list of search results.
  - Each result object may contain fields like 'title', 'url', 'text', 'author', 'date', etc.

#### Response Example
```json
{
  "results": [
    {
      "title": "The Future of Artificial Intelligence",
      "url": "https://example.com/ai-future",
      "text": "An in-depth look at the advancements in AI...",
      "author": "Jane Doe",
      "date": "2023-10-27"
    }
  ]
}
```
```

--------------------------------

### Summary Configuration Options

Source: https://exa.ai/docs/reference/get-contents

Configures the generation of webpage summaries. Supports custom queries for summarization and provides a schema for structured output. The 'schema' property allows defining the expected structure of the summary.

```yaml
summary:
  type: object
  description: Summary of the webpage
  properties:
    query:
      type: string
      description: Custom query for the LLM-generated summary.
      example: Main developments
    schema:
      type: object
      description: >
        JSON schema for structured output from summary. 

        See https://json-schema.org/overview/what-is-jsonschema for JSON
        Schema documentation.
      example:
        $schema: http://json-schema.org/draft-07/schema#
        title: Title
        type: object
        properties:
          Property 1:
            type: string
            description: Description
          Property 2:
            type: string
            enum:
              - option 1
              - option 2
              - option 3
            description: Description
        required:
          - Property 1
```

--------------------------------

### Configure RAG Pipeline with LangChain

Source: https://exa.ai/docs/reference/langchain

Initializes the OpenAI LLM and constructs a LangChain RunnableParallel chain. This setup integrates user queries with context retrieved from an Exa retriever and processes the output through a string parser.

```Python
llm = ChatOpenAI(api_key=os.getenv("OPENAI_API_KEY"))
output_parser = StrOutputParser()

chain = RunnableParallel({
    "query": RunnablePassthrough(),
    "context": retrieval_chain,
}) | generation_prompt | llm | output_parser
```

--------------------------------

### POST /contents

Source: https://exa.ai/docs/reference/livecrawling-contents

Retrieves the content of specified web pages. Supports fine-grained control over content freshness via the maxAgeHours parameter.

```APIDOC
## POST /contents

### Description
Fetches the content for a list of provided URLs. Use the `maxAgeHours` parameter to determine whether to serve cached content or perform a live crawl.

### Method
POST

### Endpoint
https://api.exa.ai/contents

### Parameters
#### Request Body
- **ids** (array of strings) - Required - A list of URLs to retrieve content from.
- **maxAgeHours** (number) - Optional - Sets the maximum acceptable age (in hours) for cached content. 0 = always livecrawl, -1 = never livecrawl, omit = default fallback behavior.
- **livecrawlTimeout** (number) - Optional - Timeout in milliseconds for livecrawl operations.

### Request Example
{
  "ids": ["https://www.apple.com"],
  "maxAgeHours": 1,
  "livecrawlTimeout": 12000
}

### Response
#### Success Response (200)
- **results** (array) - List of objects containing the content and metadata for the requested URLs.

#### Response Example
{
  "results": [
    {
      "id": "https://www.apple.com",
      "text": "...content...",
      "title": "Apple"
    }
  ]
}
```

--------------------------------

### Create a research task using Exa API

Source: https://exa.ai/docs/reference/research/create-a-task

Demonstrates how to initiate an asynchronous research task by providing instructions and selecting a research model. The examples show implementation across different environments including HTTP requests and official SDKs.

```bash
curl -X POST 'https://api.exa.ai/research/v1' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "instructions": "Summarize the latest developments in AI safety research",
    "model": "exa-research"
  }'
```

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

task = exa.research.create_task(
    instructions="Summarize the latest developments in AI safety research",
    model="exa-research"
)

print(task)
```

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const task = await exa.research.createTask({
  instructions: "Summarize the latest developments in AI safety research",
  model: "exa-research"
});

console.log(task);
```

--------------------------------

### Fetch Webpage Content with Exa.js

Source: https://exa.ai/docs/reference/get-contents

This snippet demonstrates how to use the exa-js library to fetch detailed content from a given URL. It shows how to initialize the Exa client with an API key and make a request to the getContents method, specifying various options for text extraction, highlights, and summaries. The results are then logged to the console.

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const results = await exa.getContents(
    ["https://arxiv.org/abs/2307.06435"],
    {
        text: {
            maxCharacters: 1000,
            includeHtmlTags: false
        },
        highlights: {
            maxCharacters: 2000,
            query: "Key findings"
        },
        summary: {
            query: "Main research contributions"
        },
        subpages: 1,
        subpageTarget: "references",
        extras: {
            links: 2,
            imageLinks: 1
        }
    }
);

console.log(results);
```

--------------------------------

### Search for code context using Exa API

Source: https://exa.ai/docs/reference/context

Demonstrates how to perform a POST request to the Exa Context API to retrieve code examples based on a natural language query. Requires an API key and a JSON payload specifying the search query and token constraints.

```bash
curl -X POST 'https://api.exa.ai/context' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": "how to use React hooks for state management",
    "tokensNum": 5000
  }'
```

```bash
curl -X POST 'https://api.exa.ai/context' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": "pandas dataframe filtering and groupby operations",
    "tokensNum": "dynamic"
  }'
```

```bash
curl -X POST 'https://api.exa.ai/context' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": "Next.js 14 app router with TypeScript configuration",
    "tokensNum": "dynamic"
  }'
```

--------------------------------

### List Research Tasks using Python

Source: https://exa.ai/docs/reference/research/list-tasks

This Python code snippet shows how to list research tasks using the exa-py library. Ensure you have installed the library (`pip install exa-py`) and replace 'YOUR_EXA_API_KEY' with your actual API key.

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

tasks = exa.research.list_tasks(limit=10)
print(tasks)
```

--------------------------------

### Install Exa MCP

Source: https://exa.ai/docs/reference/financial-report-search-claude-skill

Command to install or update the Exa MCP in your Claude MCP configuration. This command adds the Exa MCP with advanced web search capabilities.

```bash
claude mcp add --transport http exa "https://mcp.exa.ai/mcp?tools=web_search_advanced_exa"
```

--------------------------------

### POST /research/v1

Source: https://exa.ai/docs/reference/exa-research

Initiates a research task using the Exa AI API. This endpoint allows you to specify instructions for the AI and an optional output schema to structure the results. The example provided demonstrates how to compare flagship GPUs from major manufacturers.

```APIDOC
## POST /research/v1

### Description
Initiates a research task using the Exa AI API. This endpoint allows you to specify instructions for the AI and an optional output schema to structure the results. The example provided demonstrates how to compare flagship GPUs from major manufacturers.

### Method
POST

### Endpoint
https://api.exa.ai/research/v1

### Parameters
#### Query Parameters
None

#### Request Body
- **instructions** (string) - Required - The instructions for the research task.
- **outputSchema** (object) - Optional - A JSON schema defining the desired structure of the output.

### Request Example
```json
{
  "instructions": "Compare the current flagship GPUs from NVIDIA, AMD and Intel. Return a table of model name, MSRP USD, TDP watts, and launch date. Include citations for each cell.",
  "outputSchema": {
    "type": "object",
    "required": ["gpus"],
    "properties": {
      "gpus": {
        "type": "array",
        "items": {
          "type": "object",
          "required": ["manufacturer", "model", "msrpUsd", "tdpWatts", "launchDate"],
          "properties": {
            "manufacturer": {"type": "string"},
            "model": {"type": "string"},
            "msrpUsd": {"type": "number"},
            "tdpWatts": {"type": "integer"},
            "launchDate": {"type": "string"}
          }
        }
      }
    },
    "additionalProperties": false
  }
}
```

### Response
#### Success Response (200)
- **researchId** (string) - The ID of the initiated research task.

#### Response Example
```json
{
  "researchId": "res_abcdef1234567890"
}
```
```

--------------------------------

### Example: Risk Factors Analysis

Source: https://exa.ai/docs/reference/financial-report-search-claude-skill

Example Exa MCP call to analyze risk factors related to cybersecurity. It uses `includeText` to filter for relevant content and enables highlights with a specific query.

```json
web_search_advanced_exa {
  "query": "risk factors cybersecurity",
  "category": "financial report",
  "includeText": ["cybersecurity"],
  "numResults": 10,
  "enableHighlights": true,
  "highlightsQuery": "What are the main cybersecurity risks?"
}
```

--------------------------------

### Execute Personal Site Search Queries

Source: https://exa.ai/docs/reference/personal-site-search-claude-skill

Examples of JSON payloads for the web_search_advanced_exa tool, demonstrating how to filter by category, date, and domain to retrieve specific personal content.

```json
web_search_advanced_exa {
  "query": "building production LLM applications lessons learned",
  "category": "personal site",
  "numResults": 15,
  "type": "deep",
  "enableSummary": true
}
```

```json
web_search_advanced_exa {
  "query": "Rust async runtime comparison",
  "category": "personal site",
  "startPublishedDate": "2025-01-01",
  "numResults": 10,
  "type": "auto"
}
```

```json
web_search_advanced_exa {
  "query": "startup founder lessons",
  "category": "personal site",
  "excludeDomains": ["medium.com", "substack.com"],
  "numResults": 15,
  "type": "auto"
}
```

--------------------------------

### GET /contents

Source: https://exa.ai/docs/reference/get-contents

Retrieves the content and metadata for a specified list of document IDs or URLs.

```APIDOC
## GET /contents

### Description
Retrieves the full content and metadata for documents identified by their IDs or URLs. This endpoint returns the results along with the status of each fetch operation.

### Method
GET

### Endpoint
/contents

### Parameters
#### Query Parameters
- **ids** (array) - Required - A list of document IDs or URLs to fetch content for.

### Request Example
GET /contents?ids=https://arxiv.org/abs/2307.06435

### Response
#### Success Response (200)
- **requestId** (string) - Unique identifier for the request.
- **results** (array) - List of document objects containing content, author, and metadata.
- **statuses** (array) - Status information for each requested URL including success/error states.
- **costDollars** (number) - The cost associated with the request.

#### Response Example
{
  "requestId": "e492118ccdedcba5088bfc4357a8a125",
  "results": [
    {
      "id": "https://arxiv.org/abs/2307.06435",
      "author": "Humza Naveed, University of Engineering and Technology (UET), Lahore, Pakistan",
      "publishedDate": "2023-11-16T01:36:32.547Z"
    }
  ],
  "statuses": [
    {
      "id": "https://arxiv.org/abs/2307.06435",
      "status": "success"
    }
  ],
  "costDollars": 0.001
}
```

--------------------------------

### Get Contents API

Source: https://exa.ai/docs/reference/get-contents

Fetches and processes content from specified URLs, allowing for detailed configuration of text extraction, highlights, summaries, and subpage analysis.

```APIDOC
## POST /search/grids

### Description
This endpoint allows you to retrieve and process content from a list of URLs. You can specify detailed options for text extraction, generating highlights, creating summaries, and exploring subpages.

### Method
POST

### Endpoint
`/search/grids`

### Parameters
#### Query Parameters
- **query** (string) - Required - The search query to find relevant documents.
- **numResults** (integer) - Optional - The number of results to return.
- **useAutocorrect** (boolean) - Optional - Whether to use autocorrection for the query.

#### Request Body
- **contents** (object) - Required - Configuration for content retrieval.
  - **urls** (array of strings) - Required - A list of URLs to process.
  - **text** (object or boolean) - Optional - Configuration for text extraction.
    - **maxCharacters** (integer) - Optional - Maximum character limit for the full page text.
    - **includeHtmlTags** (boolean) - Optional - Whether to include HTML tags.
    - **verbosity** (string) - Optional - Verbosity level (compact, standard, full).
    - **includeSections** (array of strings) - Optional - Sections to include.
    - **excludeSections** (array of strings) - Optional - Sections to exclude.
  - **highlights** (object or boolean) - Optional - Configuration for highlight extraction.
    - **maxCharacters** (integer) - Optional - Maximum character limit for highlights.
    - **query** (string) - Optional - Query to generate highlights.
  - **summary** (object or boolean) - Optional - Configuration for summary generation.
    - **query** (string) - Optional - Query to generate summary.
  - **subpages** (integer) - Optional - Number of subpages to explore.
  - **subpageTarget** (string) - Optional - Target for subpage exploration (e.g., "references").
  - **extras** (object) - Optional - Additional options.
    - **links** (integer) - Optional - Number of links to include.
    - **imageLinks** (integer) - Optional - Number of image links to include.

### Request Example
```json
{
  "contents": {
    "urls": ["https://arxiv.org/abs/2307.06435"],
    "text": {
      "maxCharacters": 1000,
      "includeHtmlTags": false
    },
    "highlights": {
      "maxCharacters": 2000,
      "query": "Key findings"
    },
    "summary": {
      "query": "Main research contributions"
    },
    "subpages": 1,
    "subpageTarget": "references",
    "extras": {
      "links": 2,
      "imageLinks": 1
    }
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - A list of processed content objects, each containing details like text, highlights, and summary based on the request.

#### Response Example
```json
{
  "results": [
    {
      "url": "https://arxiv.org/abs/2307.06435",
      "text": "The full text of the page...",
      "highlights": "Key findings from the page...",
      "summary": "Main research contributions...",
      "subpages": [
        {
          "url": "https://example.com/subpage1",
          "text": "Content from subpage 1..."
        }
      ],
      "extras": {
        "links": [
          "http://link1.com",
          "http://link2.com"
        ],
        "imageLinks": [
          "http://image1.com"
        ]
      }
    }
  ]
}
```
```

--------------------------------

### Example Research Request Data

Source: https://exa.ai/docs/reference/research/get-a-task

Sample JSON objects representing research requests in different lifecycle stages, such as running or completed.

```json
{
  "researchId": "01jszdfs0052sg4jc552sg4jc5",
  "model": "exa-research",
  "instructions": "What species of ant are similar to honeypot ants?",
  "status": "completed",
  "output": "Melophorus bagoti"
}
```

--------------------------------

### Install Websets MCP via Claude CLI

Source: https://exa.ai/docs/reference/websets-mcp

Command to add the Websets MCP server using the Claude command-line interface. This command registers the HTTP transport for the websets MCP.

```bash
claude mcp add --transport http websets "https://websetsmcp.exa.ai/mcp?exaApiKey=YOUR_EXA_API_KEY"
```

--------------------------------

### Install Websets MCP for Cursor

Source: https://exa.ai/docs/reference/websets-mcp

Configuration for integrating Websets MCP with the Cursor IDE. This involves adding the MCP server details to the `~/.cursor/mcp.json` file.

```json
{
  "mcpServers": {
    "websets": {
      "url": "https://websetsmcp.exa.ai/mcp?exaApiKey=YOUR_EXA_API_KEY"
    }
  }
}
```

--------------------------------

### Install Websets MCP for VS Code

Source: https://exa.ai/docs/reference/websets-mcp

Configuration for integrating Websets MCP with VS Code. This involves adding the MCP server details to the `.vscode/mcp.json` file.

```json
{
  "servers": {
    "websets": {
      "type": "http",
      "url": "https://websetsmcp.exa.ai/mcp?exaApiKey=YOUR_EXA_API_KEY"
    }
  }
}
```

--------------------------------

### Common Research and Analysis Use Cases

Source: https://exa.ai/docs/reference/exa-for-sheets

Practical examples for tracking research, performing competitor analysis, and automating content discovery workflows using Exa AI functions.

```Google Sheets Formula
=EXA_SEARCH("latest research on " & A2 & " 2024", 3)
```

```Google Sheets Formula
=EXA_SEARCH(A2 & " " & B2 & " market analysis", 5, "neural")
```

```Google Sheets Formula
=EXA_FINDSIMILAR(A2, 10)
```

```Google Sheets Formula
=EXA_CONTENTS(B2)
```

--------------------------------

### Configure Content Modes for Token Efficiency

Source: https://exa.ai/docs/reference/search-best-practices

Examples of requesting specific content modes like highlights for agentic workflows or full text for deep research. These configurations help manage token consumption by limiting character counts in the API response.

```json
{
  "query": "What is the current Fed interest rate?",
  "contents": {
    "highlights": { "maxCharacters": 4000 }
  },
  "maxAgeHours": 0
}
```

```json
{
  "query": "detailed analysis of transformer architecture innovations",
  "contents": {
    "text": { "maxCharacters": 15000 }
  },
  "numResults": 5
}
```

--------------------------------

### API Error Codes Reference

Source: https://exa.ai/docs/reference/error-codes

A reference guide for interpreting HTTP status codes returned by the Exa AI API.

```APIDOC
## API Error Handling

### Description
This section details the standard HTTP error codes returned by the API. Use these codes to debug integration issues and handle request failures gracefully.

### Error Reference Table

| Code | Overview | Solution |
| :--- | :--- | :--- |
| 400 | Bad Request: Invalid parameters or JSON | Check request body and parameters |
| 401 | Unauthorized: Missing/Invalid API key | Verify API key and authentication headers |
| 402 | Payment Required: Credits exhausted | Top up credits at dashboard.exa.ai |
| 403 | Forbidden: Insufficient permissions | Check plan features and content policies |
| 404 | Not Found: Resource does not exist | Verify resource identifier/URL |
| 409 | Conflict: Resource already exists | Use a different identifier or update existing |
| 422 | Unprocessable Entity: Logic error | Check error message; verify URL accessibility |
| 429 | Too Many Requests: Rate limit exceeded | Implement exponential backoff |
| 500 | Internal Server Error | Retry request after a brief wait |
| 501 | Not Implemented: Model unable to answer | Rephrase query or adjust parameters |
| 502 | Bad Gateway | Retry request after a brief delay |
| 503 | Service Unavailable | Retry after maintenance or delay |

### Error Response Example
{
  "error": "Unauthorized",
  "message": "Invalid API key provided.",
  "code": 401
}
```

--------------------------------

### Install Websets MCP for Windsurf

Source: https://exa.ai/docs/reference/websets-mcp

Configuration for integrating Websets MCP with Windsurf. This involves adding the MCP server details to the `~/.codeium/windsurf/mcp_config.json` file.

```json
{
  "mcpServers": {
    "websets": {
      "serverUrl": "https://websetsmcp.exa.ai/mcp?exaApiKey=YOUR_EXA_API_KEY"
    }
  }
}
```

--------------------------------

### Example: Search for SEC Filings

Source: https://exa.ai/docs/reference/financial-report-search-claude-skill

Example Exa MCP call to search for a specific company's SEC filing (S-1). It specifies the query, category, number of results, and search type.

```json
web_search_advanced_exa {
  "query": "Anthropic SEC filing S-1",
  "category": "financial report",
  "numResults": 10,
  "type": "auto"
}
```

--------------------------------

### Initialize OpenAI and Exa Clients and Console

Source: https://exa.ai/docs/reference/openai-tool-calling

This code snippet initializes the necessary clients and objects for the search agent. It loads environment variables for API keys, creates instances of the OpenAI and Exa clients, and sets up the rich console for enhanced output. Dependencies include 'os', 'dotenv', 'openai', 'exa_py', and 'rich'.

```python
import json
import os

from dotenv import load_dotenv
from typing import Any, Dict
from exa_py import Exa
from openai import OpenAI
from rich.console import Console
from rich.markdown import Markdown
from rich.prompt import Prompt

# Load environment variables from .env file
load_dotenv()

# create the openai client
openai = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))

# create the exa client
exa = Exa(api_key=os.getenv("EXA_API_KEY"))

# create the rich console
console = Console()

# define the system message (primer) of your agent
SYSTEM_MESSAGE = {
    "role": "system",
    "content": "You are the world's most advanced search engine. Please provide the user with the information they are looking for by using the tools provided.",
}
```

--------------------------------

### Install Websets MCP for Claude Desktop

Source: https://exa.ai/docs/reference/websets-mcp

Configuration for integrating Websets MCP with Claude Desktop. This involves adding the MCP server details to the `claude_desktop_config.json` file.

```json
{
  "mcpServers": {
    "websets": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://websetsmcp.exa.ai/mcp?exaApiKey=YOUR_EXA_API_KEY"]
    }
  }
}
```

--------------------------------

### Example: Search for Specific Filing Type

Source: https://exa.ai/docs/reference/financial-report-search-claude-skill

Example Exa MCP call to search for 10-K annual reports from AI companies, filtering by domain (sec.gov) and publication date. It also specifies the number of results and search type.

```json
web_search_advanced_exa {
  "query": "10-K annual report AI companies",
  "category": "financial report",
  "includeDomains": ["sec.gov"],
  "startPublishedDate": "2025-01-01",
  "numResults": 15,
  "type": "deep"
}
```

--------------------------------

### Initialize API Clients

Source: https://exa.ai/docs/reference/anthropic-tool-calling

Import required libraries and initialize the Anthropic and Exa clients using environment variables.

```python
import anthropic
import os
from dotenv import load_dotenv
from exa_py import Exa

load_dotenv()

claude = anthropic.Anthropic(api_key=os.getenv("ANTHROPIC_API_KEY"))
exa = Exa(api_key=os.getenv("EXA_API_KEY"))
```

--------------------------------

### Example: Search for Recent Earnings Reports

Source: https://exa.ai/docs/reference/financial-report-search-claude-skill

Example Exa MCP call to find recent earnings reports for a specific industry. It includes a date range and specifies the number of results and search type.

```json
web_search_advanced_exa {
  "query": "Q4 2025 earnings report technology",
  "category": "financial report",
  "startPublishedDate": "2025-10-01",
  "numResults": 20,
  "type": "auto"
}
```

--------------------------------

### Initialize Exa and OpenAI Clients

Source: https://exa.ai/docs/reference/openai-tool-calling

Initializes the OpenAI and Exa client instances using environment variables.

```python
from dotenv import load_dotenv
from exa_py import Exa
from openai import OpenAI
import os

load_dotenv()

openai = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))
exa = Exa(api_key=os.getenv("EXA_API_KEY"))
```

--------------------------------

### Highlight Configuration Options

Source: https://exa.ai/docs/reference/get-contents

Defines how text highlights are generated and retrieved from web pages. Includes options for maximum characters, deprecated sentence count, and custom queries. The 'highlightsPerUrl' option is deprecated and ignored in favor of 'maxCharacters'.

```yaml
highlightsPerUrl:
  type: integer
  minimum: 1
  deprecated: true
  description: >-
    Deprecated and will be removed in a future release.
    Currently ignored. Use maxCharacters instead.
  example: 1
query:
  type: string
  description: Custom query to direct the LLM's selection of highlights.
  example: Key advancements
maxCharacters:
  type: integer
  minimum: 1
  description: >-
    Maximum number of characters to return for highlights. Controls
    the total length of highlight text returned per URL.
  example: 2000
numSentences:
  type: integer
  minimum: 1
  description: >-
    Deprecated and will be removed in a future release. Currently
    mapped to a character budget (1 sentence ≈ 1333 characters). Use
    maxCharacters instead.
  example: 1
  deprecated: true
```

--------------------------------

### Search Configuration Parameters

Source: https://exa.ai/docs/reference/get-contents

Defines the configuration options for processing search results, including highlight extraction, summarization, and crawl freshness.

```APIDOC
## POST /search/configure

### Description
Configures how search results are processed, including text highlights, LLM-generated summaries, and cache freshness policies.

### Method
POST

### Endpoint
/search/configure

### Request Body
- **highlights** (object) - Optional - Configuration for text snippets.
  - **maxCharacters** (integer) - Required - Maximum characters per URL.
  - **query** (string) - Optional - Custom query for LLM selection.
- **summary** (object) - Optional - Configuration for webpage summaries.
  - **query** (string) - Optional - Custom query for summary.
  - **schema** (object) - Optional - JSON schema for structured output.
- **maxAgeHours** (integer) - Optional - Cache freshness control (0: always live, -1: never live).
- **livecrawlTimeout** (integer) - Optional - Timeout in milliseconds (default 10000).
- **subpages** (integer) - Optional - Number of subpages to crawl.
- **subpageTarget** (string/array) - Optional - Terms to identify specific subpages.

### Request Example
{
  "highlights": {
    "maxCharacters": 2000,
    "query": "Key advancements"
  },
  "maxAgeHours": 24,
  "subpages": 1
}

### Response
#### Success Response (200)
- **status** (string) - Confirmation of configuration update.

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### Define Search Tool and System Message

Source: https://exa.ai/docs/reference/anthropic-tool-calling

Define the tool definition for the search function and set the system message to guide Claude's behavior.

```python
TOOLS = [
    {
        "name": "exa_search",
        "description": "Perform a search query on the web, and retrieve the most relevant URLs/web data.",
        "input_schema": {
            "type": "object",
            "properties": {
                "query": {
                    "type": "string",
                    "description": "The search query to perform."
                }
            },
            "required": ["query"]
        }
    }
]

SYSTEM_MESSAGE = "You are an agent that has access to an advanced search engine. Please provide the user with the information they are looking for by using the search tool provided."
```

--------------------------------

### Run the search agent application

Source: https://exa.ai/docs/reference/anthropic-tool-calling

Command-line instructions to execute the Python script after setting up the required environment variables.

```bash
python claude_search.py
```

--------------------------------

### Contents API - Get Highlights

Source: https://exa.ai/docs/reference/contents-best-practices

Extracts key excerpts from the page that are most relevant to a query. These are extractive and not generated.

```APIDOC
## GET /v1/contents

### Description
Fetches key excerpts from the page relevant to a specific query.

### Method
GET

### Endpoint
/v1/contents

### Parameters
#### Query Parameters
- **ids** (string[]) - Required - List of URLs to extract content from.
- **highlights** (bool/obj) - Optional - Return key excerpts most relevant to a query. Can specify `maxCharacters` and custom `query`.
- **maxAgeHours** (int) - Optional - Maximum age of indexed content in hours. `0` = always livecrawl, `-1` = never livecrawl.
- **livecrawlTimeout** (int) - Optional - Timeout in milliseconds for live crawling.
- **subpages** (int) - Optional - Maximum number of subpages to crawl from each URL.
- **subpageTarget** (string[]) - Optional - Keywords to prioritize when selecting subpages.

### Request Example
```json
{
  "ids": ["https://example.com/research-paper"],
  "highlights": {
    "query": "methodology and results",
    "maxCharacters": 2000
  }
}
```

### Response
#### Success Response (200)
- **content** (string) - The extracted highlights.

#### Response Example
```json
{
  "content": "The methodology involved... The results indicated..."
}
```
```

--------------------------------

### Exa MCP HTTP Server Configuration

Source: https://exa.ai/docs/reference/code-search-claude-skill

JSON configuration for Exa MCP's HTTP server, specifying the URL for the 'get_code_context_exa' tool.

```json
{
  "servers": {
    "exa": {
      "type": "http",
      "url": "https://mcp.exa.ai/mcp?tools=get_code_context_exa"
    }
  }
}
```

--------------------------------

### Contents API - Get Summary

Source: https://exa.ai/docs/reference/contents-best-practices

Generates an LLM-based summary of the page content. Supports custom queries and JSON schema for structured extraction.

```APIDOC
## GET /v1/contents

### Description
Generates an LLM-based summary of the page content.

### Method
GET

### Endpoint
/v1/contents

### Parameters
#### Query Parameters
- **ids** (string[]) - Required - List of URLs to extract content from.
- **summary** (bool/obj) - Optional - Return LLM-generated summary. Can specify custom `query` and JSON `schema`.
- **maxAgeHours** (int) - Optional - Maximum age of indexed content in hours. `0` = always livecrawl, `-1` = never livecrawl.
- **livecrawlTimeout** (int) - Optional - Timeout in milliseconds for live crawling.
- **subpages** (int) - Optional - Maximum number of subpages to crawl from each URL.
- **subpageTarget** (string[]) - Optional - Keywords to prioritize when selecting subpages.

### Request Example
```json
{
  "ids": ["https://example.com/article"],
  "summary": {
    "query": "Key takeaways"
  }
}
```

### Response
#### Success Response (200)
- **content** (string) - The generated summary.

#### Response Example
```json
{
  "content": "The article discusses the impact of AI on the job market, highlighting potential benefits and challenges."
}
```
```

--------------------------------

### Exa MCP Configuration

Source: https://exa.ai/docs/reference/research-paper-search-claude-skill

Command to install or update the Exa MCP in your Claude environment.

```APIDOC
## Install or Update Exa MCP

### Description
Installs or updates the Exa MCP configuration for advanced web search capabilities.

### Command
```bash
claude mcp add --transport http exa "https://mcp.exa.ai/mcp?tools=web_search_advanced_exa"
```

### Usage
Run this command in your terminal to add the Exa MCP to your Claude environment.
```

--------------------------------

### Instantiate ExaToolSpec with API Key

Source: https://exa.ai/docs/reference/llamaindex

Imports the ExaToolSpec from the llama_index.tools.exa library and initializes it using the EXA_API_KEY environment variable. This sets up the connection to the Exa AI service.

```Python
from llama_index.tools.exa import ExaToolSpec
import os

exa_tool = ExaToolSpec(
    api_key=os.environ["EXA_API_KEY"],
)
```

--------------------------------

### Fetch Fresh Content with Exa AI (cURL, Python, TypeScript)

Source: https://exa.ai/docs/reference/livecrawling-contents

Demonstrates how to fetch fresh content from a given URL using the Exa AI API. It sets `maxAgeHours` to 1 for near real-time data and `livecrawlTimeout` to 12000 milliseconds. This is useful for applications requiring up-to-date information.

```bash
curl -X POST 'https://api.exa.ai/contents' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "ids": ["https://www.apple.com"],
    "maxAgeHours": 1,
    "livecrawlTimeout": 12000
  }'
```

```python
result = exa.get_contents(
    ["https://www.apple.com"],
    max_age_hours=1,
    livecrawl_timeout=12000
)
```

```typescript
const result = await exa.getContents(
    ["https://www.apple.com"],
    {
        maxAgeHours: 1,
        livecrawlTimeout: 12000
    }
);
```

--------------------------------

### GET /contents

Source: https://exa.ai/docs/reference/contents-best-practices

Retrieves content for a list of URLs and provides status information for each request to handle potential crawl errors.

```APIDOC
## GET /contents

### Description
Retrieves content for specified URLs. The API returns a statuses array to indicate the success or failure of each individual URL request.

### Method
GET

### Endpoint
/contents

### Parameters
#### Query Parameters
- **urls** (array) - Required - List of URLs to retrieve content for.

### Request Example
{
  "urls": ["https://example.com", "https://example.com/broken"]
}

### Response
#### Success Response (200)
- **results** (array) - List of retrieved content objects.
- **statuses** (array) - List of status objects for each requested URL.

#### Response Example
{
  "results": [...],
  "statuses": [
    {
      "id": "https://example.com",
      "status": "success"
    },
    {
      "id": "https://example.com/broken",
      "status": "error",
      "error": {
        "tag": "CRAWL_NOT_FOUND",
        "httpStatusCode": 404
      }
    }
  ]
}

### Error Tags
- **CRAWL_NOT_FOUND**: Content not found (404)
- **CRAWL_TIMEOUT**: Target page timed out (408)
- **CRAWL_LIVECRAWL_TIMEOUT**: livecrawlTimeout limit reached
- **SOURCE_NOT_AVAILABLE**: Access forbidden (403)
- **CRAWL_UNKNOWN_ERROR**: Other errors (500+)
```

--------------------------------

### Search Results with Content

Source: https://exa.ai/docs/reference/get-contents

Retrieves search results including full content text, highlights, and summaries.

```APIDOC
## GET /websites/exa_ai

### Description
Retrieves search results with detailed content, including text, highlights, and summaries.

### Method
GET

### Endpoint
/websites/exa_ai

### Parameters
#### Query Parameters
- **links** (integer) - Optional - Number of URLs to return from each webpage. Default: 0.
- **imageLinks** (integer) - Optional - Number of images to return for each result. Default: 0.
- **context** (boolean or object) - Optional - Deprecated. Use highlights or text instead. Returns page contents as a combined context string.
  - If boolean: `true` to return context.
  - If object: `{ "maxCharacters": integer }` to specify maximum characters for the context string.

### Response
#### Success Response (200)
- **text** (string) - The full content text of the search result.
- **highlights** (array of strings) - Array of highlights extracted from the search result content.
- **highlightScores** (array of floats) - Array of cosine similarity scores for each highlighted section.
- **summary** (string) - Summary of the webpage.
- **subpages** (array of objects) - Array of subpages for the search result, each containing id, url, title, author, publishedDate, text, and summary.

#### Response Example
```json
{
  "text": "Abstract Large Language Models (LLMs) have recently demonstrated remarkable capabilities...",
  "highlights": [
    "Such requirements have limited their adoption..."
  ],
  "highlightScores": [
    0.4600165784358978
  ],
  "summary": "This overview paper on Large Language Models (LLMs) highlights key developments...",
  "subpages": [
    {
      "id": "https://arxiv.org/abs/2303.17580",
      "url": "https://arxiv.org/pdf/2303.17580.pdf",
      "title": "HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face",
      "author": "Yongliang Shen, Microsoft Research Asia, Kaitao Song, Microsoft Research Asia, Xu Tan, Microsoft Research Asia, Dongsheng Li, Microsoft Research Asia, Weiming Lu, Microsoft Research Asia, Yueting Zhuang, Microsoft Research Asia, yzhuang@zju.edu.cn, Zhejiang University, Microsoft Research Asia, Microsoft Research, Microsoft Research Asia",
      "publishedDate": "2023-11-16T01:36:20.486Z",
      "text": "HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face Date Published: 2023-05-25 Authors: Yongliang Shen, Microsoft Research Asia Kaitao Song, Microsoft Research Asia Xu Tan, Microsoft Research Asia Dongsheng Li, Microsoft Research Asia Weiming Lu, Microsoft Research Asia Yueting Zhuang, Microsoft Research Asia, yzhuang@zju.edu.cn Zhejiang University, Microsoft Research Asia Microsoft Research, Microsoft Research Asia Abstract Solving complicated AI tasks with different domains and modalities is a key step toward artificial general intelligence. While there are abundant AI models available for different domains and modalities, they cannot handle complicated AI tasks. Considering large language models (LLMs) have exhibited exceptional ability in language understanding, generation, interaction, and reasoning, we advocate that LLMs could act as a controller to manage existing AI models to solve complicated AI tasks and language could be a generic interface to empower t",
      "summary": "HuggingGPT is a framework using ChatGPT as a central controller to orchestrate various AI models from Hugging Face to solve complex tasks. ChatGPT plans the task, selects"
    }
  ]
}
```
```

--------------------------------

### GET /research/{researchId}

Source: https://exa.ai/docs/reference/research/list-tasks

Retrieves the status and details of a specific research request, including real-time events or final output.

```APIDOC
## GET /research/{researchId}

### Description
Retrieves the current status and results of a research request. Use query parameters to toggle real-time event logs or detailed output.

### Method
GET

### Endpoint
/research/{researchId}

### Parameters
#### Path Parameters
- **researchId** (string) - Required - Unique identifier for the research request.

#### Query Parameters
- **stream** (boolean) - Optional - If true, enables live updates for running research.
- **events** (boolean) - Optional - If true, includes detailed event logs for completed research.

### Request Example
GET /research/res_12345?events=true

### Response
#### Success Response (200)
- **researchId** (string) - Unique identifier.
- **status** (string) - Current status (running, completed).
- **output** (object) - Final results containing content and parsed JSON.
- **costDollars** (object) - Breakdown of total cost, searches, pages, and tokens.

#### Response Example
{
  "researchId": "res_12345",
  "status": "completed",
  "output": {
    "content": "Research summary text...",
    "parsed": { "key": "value" }
  },
  "costDollars": {
    "total": 0.05,
    "numSearches": 2,
    "numPages": 5,
    "reasoningTokens": 150
  }
}
```

--------------------------------

### Example: Search Developer Sentiment on Twitter

Source: https://exa.ai/docs/reference/x-search-claude-skill

Illustrates how to search for developer sentiment on Twitter/X by using descriptive keywords in the `query` parameter, focusing on terms related to developer experience.

```json
web_search_advanced_exa {
  "query": "developer experience DX frustrating painful",
  "category": "tweet",
  "numResults": 20,
  "type": "deep",
  "livecrawl": "preferred"
}
```

--------------------------------

### GET /findSimilar

Source: https://exa.ai/docs/reference/find-similar-links

Retrieves similar search results based on provided criteria, returning a list of documents with metadata and associated costs.

```APIDOC
## GET /findSimilar

### Description
Retrieves a list of search results similar to a target document. Returns metadata such as title, URL, published date, author, and document ID.

### Method
GET

### Endpoint
/findSimilar

### Parameters
#### Query Parameters
- **x-api-key** (string) - Required - API key provided in the header.

### Request Example
{
  "query": "https://arxiv.org/abs/2307.06435"
}

### Response
#### Success Response (200)
- **requestId** (string) - Unique identifier for the request.
- **results** (array) - List of search result objects.
- **costDollars** (object) - Breakdown of costs for the request.

#### Response Example
{
  "requestId": "c6958155d5c89ffa0663b7c90c407396",
  "results": [
    {
      "title": "A Comprehensive Overview of Large Language Models",
      "url": "https://arxiv.org/pdf/2307.06435.pdf",
      "id": "https://arxiv.org/abs/2307.06435"
    }
  ],
  "costDollars": {
    "contentHighlight": 0.001,
    "contentSummary": 0.001
  }
}
```

--------------------------------

### Configure Environment Variables

Source: https://exa.ai/docs/reference/anthropic-tool-calling

Set up your API keys in a .env file to securely authenticate with Anthropic and Exa services.

```bash
API_KEY=insert your Anthropic API key here, without the quotes
EXA_API_KEY=insert your Exa API key here, without the quotes
```

--------------------------------

### GET /research/{researchId}

Source: https://exa.ai/docs/reference/research/create-a-task

Retrieves the status and details of a specific research request, including output, cost, and event logs.

```APIDOC
## GET /research/{researchId}

### Description
Retrieves the current state of a research request. Use the events query parameter to include detailed logs.

### Method
GET

### Endpoint
/research/{researchId}

### Parameters
#### Path Parameters
- **researchId** (string) - Required - The unique identifier for the research request.

#### Query Parameters
- **events** (boolean) - Optional - If set to true, includes the detailed log of operations performed during research.

### Request Example
GET /research/01jszdfs0052sg4jc552sg4jc5?events=true

### Response
#### Success Response (200)
- **researchId** (string) - Unique identifier.
- **status** (string) - Current status (running, completed, canceled, failed).
- **model** (string) - The model used (exa-research, exa-research-fast, exa-research-pro).
- **output** (object) - The research results, if available.
- **costDollars** (object) - Detailed cost breakdown for billing.

#### Response Example
{
  "researchId": "01jszdfs0052sg4jc552sg4jc5",
  "model": "exa-research",
  "status": "completed",
  "output": "Melophorus bagoti",
  "costDollars": {
    "total": 0.05,
    "numSearches": 2,
    "numPages": 5,
    "reasoningTokens": 150
  }
}
```

--------------------------------

### Fetch Content with Daily Freshness (cURL, Python, TypeScript)

Source: https://exa.ai/docs/reference/livecrawling-contents

Shows how to retrieve content with a daily freshness requirement using the Exa AI API. It configures `maxAgeHours` to 24, meaning cached content up to 24 hours old is used, otherwise a live crawl is performed. Includes `livecrawlTimeout` for robustness in production applications.

```bash
curl -X POST 'https://api.exa.ai/contents' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "ids": ["https://www.apple.com"],
    "maxAgeHours": 24,
    "livecrawlTimeout": 12000
  }'
```

```python
result = exa.get_contents(
    ["https://www.apple.com"],
    max_age_hours=24,
    livecrawl_timeout=12000
)
```

```typescript
const result = await exa.getContents(
    ["https://www.apple.com"],
    {
        maxAgeHours: 24,
        livecrawlTimeout: 12000
    }
);
```

--------------------------------

### Initialize and Use Exa OpenAI Wrapper

Source: https://exa.ai/docs/reference/openai-sdk

Demonstrates how to initialize the Exa client and wrap an existing OpenAI client instance to enable automated RAG features. The wrapped client functions identically to the standard OpenAI client for chat completions.

```python
from openai import OpenAI
from exa_py import Exa

# Initialize clients
openai = OpenAI(api_key='OPENAI_API_KEY')
exa = Exa('EXA_API_KEY')

# Wrap the OpenAI client
exa_openai = exa.wrap(openai)

# Use exactly like the normal OpenAI client
completion = exa_openai.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "What is the latest climate tech news?"}]
)

print(completion.choices[0].message.content)
```

--------------------------------

### GET /research/{researchId}

Source: https://exa.ai/docs/reference/research/get-a-task

Retrieves the current status and details of a specific research request, including real-time events and final output.

```APIDOC
## GET /research/{researchId}

### Description
Retrieves the status, event logs, and final output of a research request. Use the `stream` or `events` query parameters to control the verbosity of the response.

### Method
GET

### Endpoint
/research/{researchId}

### Parameters
#### Path Parameters
- **researchId** (string) - Required - The unique identifier for the research request.

#### Query Parameters
- **stream** (boolean) - Optional - If true, provides live updates for running research.
- **events** (boolean) - Optional - If true, includes detailed operation logs for debugging.

### Request Example
GET /research/res_12345?events=true

### Response
#### Success Response (200)
- **researchId** (string) - Unique identifier.
- **status** (string) - Current state (running, completed).
- **output** (object) - Final research results (content and parsed JSON).
- **costDollars** (object) - Billing breakdown including total, searches, and tokens.

#### Response Example
{
  "researchId": "res_12345",
  "status": "completed",
  "output": {
    "content": "Research findings...",
    "parsed": { "key": "value" }
  },
  "costDollars": {
    "total": 0.05,
    "numSearches": 2,
    "numPages": 5,
    "reasoningTokens": 1200
  }
}
```

--------------------------------

### GET /search

Source: https://exa.ai/docs/reference/search

Retrieves search results based on a query, including metadata like titles, URLs, published dates, and synthesized content for deep searches.

```APIDOC
## GET /search

### Description
Performs a search query and returns a list of relevant documents with their associated metadata and optional synthesized content.

### Method
GET

### Endpoint
/search

### Parameters
#### Query Parameters
- **query** (string) - Required - The search term or phrase.
- **type** (string) - Optional - The search type (neural, deep, deep-reasoning).

### Request Example
{
  "query": "Large Language Models",
  "type": "neural"
}

### Response
#### Success Response (200)
- **requestId** (string) - Unique identifier for the request.
- **results** (array) - List of search result objects.
- **searchType** (string) - The type of search performed.
- **output** (object) - Synthesized content for deep search variants.

#### Response Example
{
  "requestId": "b5947044c4b78efa9552a7c89b306d95",
  "results": [
    {
      "title": "A Comprehensive Overview of Large Language Models",
      "url": "https://arxiv.org/pdf/2307.06435.pdf",
      "publishedDate": "2023-11-16T01:36:32.547Z",
      "author": "Humza Naveed",
      "id": "https://arxiv.org/abs/2307.06435"
    }
  ],
  "searchType": "neural"
}
```

--------------------------------

### Configure Deep Search Output Schema

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Demonstrates how to define an outputSchema for deep search queries. Supports both 'text' mode for guided responses and 'object' mode for strictly typed JSON structures.

```json
{
  "query": "what's the fastest web search API",
  "type": "deep",
  "outputSchema": {
    "type": "text",
    "description": "Short one to two sentence answer"
  }
}
```

```json
{
  "query": "top aerospace companies",
  "type": "deep",
  "outputSchema": {
    "type": "object",
    "required": ["companies"],
    "properties": {
      "companies": {
        "type": "array",
        "description": "A list of aerospace companies",
        "items": {
          "type": "object",
          "required": ["company_name", "ceo_name", "stock_price"],
          "properties": {
            "company_name": { "type": "string", "description": "The name of the aerospace company" },
            "ceo_name": { "type": "string", "description": "The name of the company's CEO" },
            "stock_price": { "type": "number", "description": "Current stock price of the company" }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Set up OpenAI Agent with Exa Tools

Source: https://exa.ai/docs/reference/llamaindex

Initializes an OpenAIAgent from the llama_index.agent.openai library, configuring it with the previously selected Exa tools. The 'verbose' flag is set to True for detailed output during agent operation.

```Python
from llama_index.agent.openai import OpenAIAgent

agent = OpenAIAgent.from_tools(
    search_and_retrieve_highlights_tool,
    verbose=True,
)
```

--------------------------------

### GET /api/costs

Source: https://exa.ai/docs/reference/find-similar-links

Retrieves the cost breakdown for API requests, including total expenditure, operation-specific costs, and current pricing tiers.

```APIDOC
## GET /api/costs

### Description
Returns the total cost of the request, a detailed breakdown by operation type (neural search, deep search, content retrieval), and the standard pricing schedule.

### Method
GET

### Endpoint
/api/costs

### Parameters
#### Query Parameters
- **request_id** (string) - Optional - The specific request ID to fetch cost data for.

### Request Example
{
  "request_id": "req_123456789"
}

### Response
#### Success Response (200)
- **total** (number) - Total dollar cost for the request.
- **breakDown** (object) - Detailed costs by operation.
- **perRequestPrices** (object) - Standard pricing per request type.

#### Response Example
{
  "total": 0.007,
  "breakDown": {
    "search": 0.007,
    "contents": 0,
    "breakdown": {
      "neuralSearch": 0.007,
      "deepSearch": 0.012
    }
  },
  "perRequestPrices": {
    "neuralSearch_1_10_results": 0.007,
    "deepSearch": 0.012
  }
}
```

--------------------------------

### GET /research/{researchId}

Source: https://exa.ai/docs/reference/research/list-tasks

Retrieves the details of a specific research request by its unique identifier. Supports optional event logging for debugging purposes.

```APIDOC
## GET /research/{researchId}

### Description
Retrieves the current status and metadata of a research request. Use the events query parameter to include detailed operation logs.

### Method
GET

### Endpoint
/research/{researchId}

### Parameters
#### Path Parameters
- **researchId** (string) - Required - Unique identifier for the research request.

#### Query Parameters
- **events** (boolean) - Optional - If true, includes the detailed log of operations performed during research.

### Request Example
GET /research/01jszdfs0052sg4jc552sg4jc5?events=true

### Response
#### Success Response (200)
- **researchId** (string) - Unique identifier.
- **status** (string) - Current status (completed, canceled, failed, running).
- **model** (string) - The model used (exa-research, exa-research-fast, exa-research-pro).
- **instructions** (string) - The original research instructions.
- **finishedAt** (number) - Unix timestamp in milliseconds when the request concluded.

#### Response Example
{
  "researchId": "01jszdfs0052sg4jc552sg4jc5",
  "model": "exa-research",
  "instructions": "What species of ant are similar to honeypot ants?",
  "status": "completed",
  "output": "Melophorus bagoti"
}
```

--------------------------------

### GET /research/v1

Source: https://exa.ai/docs/reference/research/list-tasks

Retrieves a paginated list of research requests. You can filter the results by specifying a cursor for pagination and a limit for the number of results per page.

```APIDOC
## GET /research/v1

### Description
Get a paginated list of research requests. This endpoint allows you to retrieve past research tasks, with options to control the number of results and paginate through them.

### Method
GET

### Endpoint
/research/v1

### Parameters
#### Query Parameters
- **cursor** (string) - Optional - The cursor to paginate through the results. Use the `nextCursor` from a previous response to fetch the next page.
- **limit** (number) - Optional - Number of results per page. Must be between 1 and 50. Defaults to 10.

### Request Example
```bash
curl -X GET "https://api.exa.ai/research/v1?limit=10" \
  -H "x-api-key: YOUR-EXA-API-KEY"
```

### Response
#### Success Response (200)
- **data** (array) - An array of research request objects.
- **hasMore** (boolean) - Indicates if there are more results available to fetch.
- **nextCursor** (string | null) - A cursor to be used for fetching the next page of results. Null if there are no more pages.

#### Response Example
```json
{
  "data": [
    {
      "researchId": "01jszdfs0052sg4jc552sg4jc5",
      "model": "exa-research",
      "instructions": "What species of ant are similar to honeypot ants?",
      "status": "running"
    },
    {
      "researchId": "01jszdfs0052sg4jc552sg4jc5",
      "model": "exa-research",
      "instructions": "What species of ant are similar to honeypot ants?",
      "status": "completed",
      "output": "Melophorus bagoti"
    }
  ],
  "hasMore": true,
  "nextCursor": "some_cursor_string"
}
```
```

--------------------------------

### POST /contents

Source: https://exa.ai/docs/reference/get-contents

Retrieves the content of specified URLs or document IDs. Supports advanced options like text truncation, highlighting, summarization, and subpage extraction.

```APIDOC
## POST /contents

### Description
Retrieves the content of specified URLs or document IDs. This endpoint allows for deep content extraction including text, highlights, and summaries.

### Method
POST

### Endpoint
https://api.exa.ai/contents

### Parameters
#### Request Body
- **urls** (array) - Required - Array of URLs to crawl (backwards compatible with 'ids').
- **ids** (array) - Optional - Array of document IDs obtained from searches.
- **text** (object/boolean) - Optional - Configuration for text extraction (e.g., maxCharacters, includeHtmlTags).
- **highlights** (object) - Optional - Configuration for content highlighting based on a query.
- **summary** (object) - Optional - Configuration for generating a summary based on a query.

### Request Example
{
  "urls": ["https://arxiv.org/abs/2307.06435"],
  "text": true
}

### Response
#### Success Response (200)
- **results** (array) - List of retrieved content objects.

#### Response Example
{
  "results": [
    {
      "id": "https://arxiv.org/abs/2307.06435",
      "url": "https://arxiv.org/abs/2307.06435",
      "title": "Example Document",
      "text": "Document content..."
    }
  ]
}
```

--------------------------------

### Use Exa AI Research Models

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

This snippet demonstrates how to interact with Exa AI's research models using their API. It shows how to initialize the client and make a request to summarize a given topic. Ensure you replace 'YOUR_EXA_API_KEY' with your actual API key.

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://api.exa.ai",
    api_key="YOUR_EXA_API_KEY"  # Use your Exa API key
)

response = client.responses.create(
    model="exa-research",  # or "exa-research-pro"
    input="Summarize the impact of CRISPR on gene therapy with recent developments"
)

print(response.output)
```

```javascript
import OpenAI from "openai";

const openai = new OpenAI({
  baseURL: "https://api.exa.ai",
  apiKey: "YOUR_EXA_API_KEY", // Use your Exa API key
});

async function main() {
  const response = await openai.responses.create({
    model: "exa-research", // or "exa-research-pro"
    input:
      "Summarize the impact of CRISPR on gene therapy with recent developments",
  });

  console.log(response.output);
}

main();
```

```curl
curl --location 'https://api.exa.ai/responses' \
--header 'x-api-key: YOUR_EXA_API_KEY' \
--header 'Content-Type: application/json' \
--data '{
      "input": "Summarize the impact of CRISPR on gene therapy with recent developments",
      "model": "exa-research"
  }'
```

--------------------------------

### GET /research/v1/{researchId}

Source: https://exa.ai/docs/reference/research/get-a-task

Retrieve the current status and results of a specific research task by its unique identifier. Supports optional streaming for real-time updates.

```APIDOC
## GET /research/v1/{researchId}

### Description
Retrieve research by ID. Add ?stream=true for real-time SSE updates.

### Method
GET

### Endpoint
https://api.exa.ai/research/v1/{researchId}

### Parameters
#### Path Parameters
- **researchId** (string) - Required - The unique identifier of the research request to retrieve

#### Query Parameters
- **stream** (string) - Optional - Set to "true" to receive real-time updates via Server-Sent Events (SSE)
- **events** (string) - Optional - Set to "true" to include the detailed event log of all operations performed

### Request Example
GET /research/v1/01jszdfs0052sg4jc552sg4jc5

### Response
#### Success Response (200)
- **researchId** (string) - Unique identifier for tracking and retrieving this research request
- **createdAt** (number) - When the research was created (Unix timestamp in milliseconds)
- **model** (string) - The model used for this research request (exa-research-fast, exa-research, exa-research-pro)
- **instructions** (string) - The original research instructions provided
- **status** (string) - The current status of the research task

#### Response Example
{
  "researchId": "01jszdfs0052sg4jc552sg4jc5",
  "createdAt": 1715678900000,
  "model": "exa-research",
  "instructions": "Research the latest advancements in AI",
  "status": "pending"
}
```

--------------------------------

### Perform advanced content retrieval with configuration

Source: https://exa.ai/docs/reference/get-contents

Retrieve content with custom parameters including character limits, HTML tag filtering, highlights, summaries, and subpage crawling. This is useful for focused data extraction from research papers or complex web pages.

```bash
curl --request POST \
  --url https://api.exa.ai/contents \
  --header 'x-api-key: YOUR-EXA-API-KEY' \
  --header 'Content-Type: application/json' \
  --data '{
    "urls": ["https://arxiv.org/abs/2307.06435"],
    "text": {
      "maxCharacters": 1000,
      "includeHtmlTags": false
    },
    "highlights": {
      "maxCharacters": 2000,
      "query": "Key findings"
    },
    "summary": {
      "query": "Main research contributions"
    },
    "subpages": 1,
    "subpageTarget": "references",
    "extras": {
      "links": 2,
      "imageLinks": 1
    }
  }'
```

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

results = exa.get_contents(
    urls=["https://arxiv.org/abs/2307.06435"],
    text={
        "maxCharacters": 1000,
        "includeHtmlTags": False
    },
    highlights={
        "maxCharacters": 2000,
        "query": "Key findings"
    },
    summary={
        "query": "Main research contributions"
    },
    subpages=1,
    subpage_target="references",
    extras={
        "links": 2,
        "image_links": 1
    }
)

print(results)
```

--------------------------------

### Sample Agent Output: Function Calls

Source: https://exa.ai/docs/reference/llamaindex

Provides a sample of the verbose output from the agent, showing the sequence of function calls made. This includes calls to 'current_date' and 'search_and_retrieve_highlights' with their respective arguments.

```stdout
Added user message to memory: Can you summarize the news from the last month related to the US stock market?
=== Calling Function ===
Calling function: current_date with args: {}
Got output: 2024-05-09
========================

=== Calling Function ===
Calling function: search_and_retrieve_highlights with args: {"query":"US stock market news","num_results":5,"start_published_date":"2024-04-09","end_published_date":"2024-05-09"}
[Exa Tool] Autoprompt: Here is the latest news on the US stock market:
```

--------------------------------

### Subpage Crawling Configuration

Source: https://exa.ai/docs/reference/get-contents

Controls the crawling of subpages within a website. 'subpages' defines the number of subpages to crawl, while 'subpageTarget' allows specifying terms to find specific subpages.

```yaml
subpages:
  type: integer
  default: 0
  description: >-
    The number of subpages to crawl. The actual number crawled may be
    limited by system constraints.
  example: 1
subpageTarget:
  oneOf:
    - type: string
    - type: array
      items:
        type: string
  description: >-
    Term to find specific subpages of search results. Can be a single
    string or an array of strings, comma delimited.
  example: sources
```

--------------------------------

### Contents API - Get Full Page Text

Source: https://exa.ai/docs/reference/contents-best-practices

Extracts the full page content as clean markdown. Supports limiting the number of characters and preserving HTML tags.

```APIDOC
## GET /v1/contents

### Description
Fetches the complete page content as clean markdown.

### Method
GET

### Endpoint
/v1/contents

### Parameters
#### Query Parameters
- **ids** (string[]) - Required - List of URLs to extract content from.
- **text** (bool/obj) - Optional - Return full page text as markdown. Can specify `maxCharacters` and `includeHtmlTags`.
- **maxAgeHours** (int) - Optional - Maximum age of indexed content in hours. `0` = always livecrawl, `-1` = never livecrawl.
- **livecrawlTimeout** (int) - Optional - Timeout in milliseconds for live crawling.
- **subpages** (int) - Optional - Maximum number of subpages to crawl from each URL.
- **subpageTarget** (string[]) - Optional - Keywords to prioritize when selecting subpages.

### Request Example
#### Simple Text Extraction
```json
{
  "ids": ["https://arxiv.org/abs/2301.07041"],
  "text": true
}
```

#### Text Extraction with Options
```json
{
  "ids": ["https://arxiv.org/abs/2301.07041"],
  "text": {
    "maxCharacters": 8000,
    "includeHtmlTags": true
  }
}
```

### Response
#### Success Response (200)
- **content** (string) - The extracted markdown content.

#### Response Example
```json
{
  "content": "# Extracted Content\nThis is the main content of the page..."
}
```
```

--------------------------------

### Compare Exa AI Configurations (Python)

Source: https://exa.ai/docs/reference/evaluating-exa-search

This Python script demonstrates how to run multiple configurations of the SimpleQA evaluation script to compare performance tradeoffs. It iterates through a list of configurations, runs the evaluation for each, and prints the accuracy and P50 latency.

```python
configs = [
    {'name': 'Fast', 'type': 'fast'},
    {'name': 'Auto', 'type': 'auto'},
    {'name': 'Deep', 'type': 'deep'},
]

for config in configs:
    results = evaluate_simpleqa('simpleqa.json', config)
    print(f"{config['name']}: {results['accuracy']:.1%} @ {results['p50_latency_ms']:.0f}ms")
```

--------------------------------

### Claude Skill Configuration for Exa Code Context

Source: https://exa.ai/docs/reference/code-search-claude-skill

YAML configuration for a Claude skill named 'get-code-context-exa'. This skill leverages Exa to find code snippets, API docs, and technical information.

```yaml
---
name: get-code-context-exa
description: Code context using Exa. Finds real snippets and docs from GitHub, StackOverflow, and technical docs. Use when searching for code examples, API syntax, library documentation, or debugging help.
context: fork
---

# Code Context (Exa)

## Tool Restriction (Critical)

ONLY use `get_code_context_exa`. Do NOT use other Exa tools.

## Token Isolation (Critical)

Never run Exa in main context. Always spawn Task agents:
- Agent calls `get_code_context_exa`
- Agent extracts the minimum viable snippet(s) + constraints
- Agent deduplicates near-identical results (mirrors, forks, repeated StackOverflow answers) before presenting
- Agent returns copyable snippets + brief explanation
- Main context stays clean regardless of search volume

## When to Use

Use this tool for ANY programming-related request:
- API usage and syntax
- SDK/library examples
- config and setup patterns
- framework "how to" questions
- debugging when you need authoritative snippets

## Inputs (Supported)

`get_code_context_exa` supports:
- `query` (string, required)
- `tokensNum` (number, optional; default ~5000; typical range 1000–50000)

## Query Writing Patterns (High Signal)

To reduce irrelevant results and cross-language noise:
- Always include the **programming language** in the query.
  - Example: use **"Go generics"** instead of just **"generics"**.
- When applicable, also include **framework + version** (e.g., "Next.js 14", "React 19", "Python 3.12").
- Include exact identifiers (function/class names, config keys, error messages) when you have them.

## Dynamic Tuning

Token strategy:
- Focused snippet needed → tokensNum 1000–3000
- Most tasks → tokensNum 5000
- Complex integration → tokensNum 10000–20000
- Only go larger when necessary (avoid dumping large context)

## Output Format (Recommended)

Return:
1) Best minimal working snippet(s) (keep it copy/paste friendly)
2) Notes on version / constraints / gotchas
3) Sources (URLs if present in returned context)

Before presenting:
- Deduplicate similar results and keep only the best representative snippet per approach.
```

--------------------------------

### Example: Search Recent Tweets

Source: https://exa.ai/docs/reference/x-search-claude-skill

Demonstrates how to use the `web_search_advanced_exa` tool with the `tweet` category to find recent tweets about a specific topic, including date filtering and live crawl preference.

```json
web_search_advanced_exa {
  "query": "Claude Code MCP experience",
  "category": "tweet",
  "startPublishedDate": "2025-01-01",
  "numResults": 20,
  "type": "auto",
  "livecrawl": "preferred"
}
```

--------------------------------

### Extract Full Page Text via Exa API

Source: https://exa.ai/docs/reference/contents-best-practices

Demonstrates how to request full page content in markdown format. Includes examples for basic extraction and advanced configurations like character limits and HTML tag preservation.

```json
{
  "ids": ["https://arxiv.org/abs/2301.07041"],
  "text": true
}
```

```json
{
  "ids": ["https://arxiv.org/abs/2301.07041"],
  "text": {
    "maxCharacters": 8000,
    "includeHtmlTags": true
  }
}
```

--------------------------------

### Retrieve content from URLs using Exa API

Source: https://exa.ai/docs/reference/get-contents

Perform a basic retrieval of content from a list of URLs. This operation requires an API key and returns the text content of the specified pages.

```bash
curl -X POST 'https://api.exa.ai/contents' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "urls": ["https://arxiv.org/abs/2307.06435"],
    "text": true
  }'
```

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

results = exa.get_contents(
    urls=["https://arxiv.org/abs/2307.06435"],
    text=True
)

print(results)
```

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const results = await exa.getContents(
    ["https://arxiv.org/abs/2307.06435"],
    { text: true }
);

console.log(results);
```

--------------------------------

### Exa web_search_advanced_exa Examples

Source: https://exa.ai/docs/reference/company-research-claude-skill

Demonstrates various ways to use the `web_search_advanced_exa` tool for different research needs, including company discovery, deep dives, news coverage, and LinkedIn profile searches.

```json
web_search_advanced_exa {
  "query": "AI infrastructure startups San Francisco",
  "category": "company",
  "numResults": 20,
  "type": "auto"
}
```

```json
web_search_advanced_exa {
  "query": "Anthropic funding rounds valuation 2024",
  "type": "deep",
  "livecrawl": "fallback",
  "numResults": 10,
  "includeDomains": ["techcrunch.com", "crunchbase.com", "bloomberg.com"]
}
```

```json
web_search_advanced_exa {
  "query": "Anthropic AI safety",
  "category": "news",
  "numResults": 15,
  "startPublishedDate": "2024-01-01"
}
```

```json
web_search_advanced_exa {
  "query": "VP Engineering AI infrastructure",
  "category": "people",
  "numResults": 20
}
```

--------------------------------

### Get Contents API

Source: https://exa.ai/docs/reference/tool-calling-best-practices

This endpoint is used to extract clean content from provided URLs. It can handle various formats including JS-rendered pages and PDFs, returning the content as markdown text, highlights, or summaries.

```APIDOC
## POST /contents

### Description
Extract clean content from URLs. Handles JS-rendered pages, PDFs, and complex layouts. Returns markdown text, highlights, or summaries.

### Method
POST

### Endpoint
/contents

### Parameters
#### Query Parameters
None

#### Request Body
- **ids** (array[string]) - Required - List of URLs to get contents for.

### Request Example
```json
{
  "ids": ["https://example.com/page1", "https://example.com/document.pdf"]
}
```

### Response
#### Success Response (200)
- **content** (string) - The extracted content from the URL.
- **citations** (array) - Field-level citations for the extracted content.

#### Response Example
```json
{
  "output": {
    "content": "Extracted markdown content...",
    "grounding": [
      {
        "field": "content",
        "citations": [
          { "url": "https://example.com/page1", "title": "Example Page Title" }
        ],
        "confidence": "high"
      }
    ]
  }
}
```
```

--------------------------------

### Handle Content Fetch Error Statuses

Source: https://exa.ai/docs/reference/error-codes

Example JSON response structure showing how the API returns granular error information for specific URLs within the 'statuses' array. This allows developers to handle partial failures when processing multiple URLs in a single request.

```json
{
  "results": [...],
  "statuses": [
    {
      "id": "https://example.com",
      "status": "error",
      "error": {
        "tag": "CRAWL_NOT_FOUND",
        "httpStatusCode": 404
      }
    }
  ]
}
```

--------------------------------

### Add Exa MCP to Claude

Source: https://exa.ai/docs/reference/code-search-claude-skill

Command to add the Exa MCP transport to your Claude configuration. This enables Claude to interact with Exa's services for code searching.

```bash
claude mcp add --transport http exa "https://mcp.exa.ai/mcp?tools=get_code_context_exa"
```

--------------------------------

### Compare Flagship GPUs with Exa AI (Python, JavaScript, cURL)

Source: https://exa.ai/docs/reference/exa-research

This snippet demonstrates how to use the Exa AI research API to compare flagship GPUs from major manufacturers. It specifies the desired output schema for model name, MSRP, TDP, and launch date, and includes citations. The code supports Python, JavaScript, and cURL, allowing for flexible integration into various workflows.

```python
import os
from exa_py import Exa

exa = Exa(os.environ["EXA_API_KEY"])

instructions = "Compare the current flagship GPUs from NVIDIA, AMD and Intel. Return a table of model name, MSRP USD, TDP watts, and launch date. Include citations for each cell."
schema = {
    "type": "object",
    "required": ["gpus"],
    "properties": {
        "gpus": {
            "type": "array",
            "items": {
                "type": "object",
                "required": ["manufacturer", "model", "msrpUsd", "tdpWatts", "launchDate"],
                "properties": {
                    "manufacturer": {"type": "string"},
                    "model": {"type": "string"},
                    "msrpUsd": {"type": "number"},
                    "tdpWatts": {"type": "integer"},
                    "launchDate": {"type": "string"}
                }
            }
        }
    },
    "additionalProperties": False
}

research = exa.research.create(
    model="exa-research",
    instructions=instructions,
    output_schema=schema
)

# Poll until completion
result = exa.research.poll_until_finished(research.researchId)
print(result)
```

```javascript
import Exa, { ResearchModel } from "exa-js";

const exa = new Exa(process.env.EXA_API_KEY);

async function compareGPUs() {
  const research = await exa.research.create({
    model: ResearchModel.exa_research,
    instructions:
      "Compare the current flagship GPUs from NVIDIA, AMD and Intel. Return a table of model name, MSRP USD, TDP watts, and launch date. Include citations for each cell.",
    outputSchema: {
      type: "object",
      required: ["gpus"],
      properties: {
        gpus: {
          type: "array",
          items: {
            type: "object",
            required: [
              "manufacturer",
              "model",
              "msrpUsd",
              "tdpWatts",
              "launchDate",
            ],
            properties: {
              manufacturer: { type: "string" },
              model: { type: "string" },
              msrpUsd: { type: "number" },
              tdpWatts: { type: "integer" },
              launchDate: { type: "string" },
            },
          },
        },
      },
      additionalProperties: False,
    },
  });

  // Poll until completion
  const result = await exa.research.pollUntilFinished(research.researchId);
  console.log("Research result:", result);
}

compareGPUs();
```

```bash
curl -X POST https://api.exa.ai/research/v1 \
  -H "x-api-key: $EXA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ \
    "instructions": "Compare the current flagship GPUs from NVIDIA, AMD and Intel. Return a table of model name, MSRP USD, TDP watts, and launch date. Include citations for each cell.", \
    "outputSchema": { \
      "type": "object", \
      "required": ["gpus"], \
      "properties": { \
        "gpus": { \
          "type": "array", \
          "items": { \
            "type": "object", \
            "required": ["manufacturer", "model", "msrpUsd", "tdpWatts", "launchDate"], \
            "properties": { \
              "manufacturer": {"type": "string"}, \
              "model": {"type": "string"}, \
              "msrpUsd": {"type": "number"}, \
              "tdpWatts": {"type": "integer"}, \
              "launchDate": {"type": "string"} \
            } \
          } \
        } \
      }, \
      "additionalProperties": False \
    } \
  }'
```

--------------------------------

### Select and List Exa Tool Functions for Agent

Source: https://exa.ai/docs/reference/llamaindex

Demonstrates how to select specific Exa tool functions, such as 'search_and_retrieve_highlights' and 'current_date', using the .to_tool_list method. It also prints the available spec functions provided by the Exa LlamaIndex integration.

```Python
print('Tools that are provide by Exa LlamaIndex integration:')
print('\n'.join(map(str, (exa_tool.spec_functions))))

search_and_retrieve_highlights_tool = exa_tool.to_tool_list(
    spec_functions=["search_and_retrieve_highlights", "current_date"]
)
```

--------------------------------

### Live Crawling Configuration

Source: https://exa.ai/docs/reference/get-contents

Manages the live crawling behavior for web pages. The 'livecrawl' option is deprecated in favor of 'maxAgeHours' for more precise control over content freshness. It defines when to fetch fresh content versus using cached data.

```yaml
livecrawl:
  type: string
  enum:
    - never
    - fallback
    - preferred
    - always
  deprecated: true
  description: >
    **Deprecated**: Use `maxAgeHours` instead for more precise control
    over content freshness.


    Options for livecrawling pages.

    'never': Disable livecrawling (default for neural search).

    'fallback': Livecrawl when cache is empty.

    'preferred': Always try to livecrawl, but fall back to cache if
    crawling fails.

    'always': Always live-crawl, never use cache. Only use if you cannot
    tolerate any cached content. This option is not recommended unless
    consulted with the Exa team.
  example: preferred
livecrawlTimeout:
  type: integer
  default: 10000
  description: The timeout for livecrawling in milliseconds.
  example: 1000
maxAgeHours:
  type: integer
  description: >
    Maximum age of cached content in hours. Controls when livecrawling
    is triggered based on content freshness.

    - Positive value (e.g. 24): Use cached content if it's less than
    this many hours old, otherwise livecrawl.

    - 0: Always livecrawl, never use cache.

    - -1: Never livecrawl, always use cache.

    - Omit (default): Livecrawl as fallback only when no cached content
    exists.
  example: 24
```

--------------------------------

### Configure ExaSearchRetriever and RAG pipeline

Source: https://exa.ai/docs/reference/langchain

Initializes the Exa search retriever and builds a processing chain that parses search results into XML-formatted context for use in LLM prompts.

```Python
import os
from dotenv import load_dotenv
from langchain_exa import ExaSearchRetriever
from langchain_core.prompts import PromptTemplate
from langchain_core.runnables import RunnableLambda

load_dotenv()
retriever = ExaSearchRetriever(api_key=os.getenv("EXA_API_KEY"), k=3, highlights=True)

document_prompt = PromptTemplate.from_template("<source>\n    <url>{url}</url>\n    <highlights>{highlights}</highlights>\n</source>")

document_chain = RunnableLambda(
    lambda document: {
        "highlights": document.metadata["highlights"],
        "url": document.metadata["url"]
    }
) | document_prompt

retrieval_chain = retriever | document_chain.map() | (lambda docs: "\n".join([i.text for i in docs]))
```

--------------------------------

### Exa Search for Research Papers from Specific Venues

Source: https://exa.ai/docs/reference/research-paper-search-claude-skill

Example demonstrating how to search for research papers from specific domains and with specific text inclusions. It utilizes `query`, `category`, `includeDomains`, `includeText`, `numResults`, and `type`.

```json
web_search_advanced_exa {
  "query": "large language model agents",
  "category": "research paper",
  "includeDomains": ["arxiv.org", "openreview.net"],
  "includeText": ["LLM"],
  "numResults": 20,
  "type": "deep"
}
```

--------------------------------

### Exa Search for Recent Research Papers

Source: https://exa.ai/docs/reference/research-paper-search-claude-skill

Example of how to use the `web_search_advanced_exa` tool to find recent research papers on a specific topic. It demonstrates the use of `query`, `category`, `startPublishedDate`, `numResults`, and `type` parameters.

```json
web_search_advanced_exa {
  "query": "transformer attention mechanisms efficiency",
  "category": "research paper",
  "startPublishedDate": "2024-01-01",
  "numResults": 15,
  "type": "auto"
}
```

--------------------------------

### Exa Advanced Web Search: People by Role

Source: https://exa.ai/docs/reference/people-search-claude-skill

Example of using `web_search_advanced_exa` to find people based on their role. It specifies the query, category as 'people', number of results, and search type.

```json
{
  "query": "VP Engineering AI infrastructure",
  "category": "people",
  "numResults": 20,
  "type": "auto"
}
```

--------------------------------

### Configure Environment Variables

Source: https://exa.ai/docs/reference/openai-tool-calling

Sets the required API keys for OpenAI and Exa within the environment configuration.

```shell
OPENAI_API_KEY=insert your Exa API key here, without quotes
EXA_API_KEY=insert your Exa API key here, without quotes
```

--------------------------------

### Get AI-Powered Answers with EXA_ANSWER

Source: https://exa.ai/docs/reference/exa-for-sheets

The EXA_ANSWER function generates AI-powered answers to a given prompt. It supports optional prefix and suffix text, and a boolean to include citations. It returns the answer text.

```google-sheets
=EXA_ANSWER("What are the latest trends in renewable energy?", "", "", TRUE)
```

--------------------------------

### Instant Search (Lowest Latency) (Python)

Source: https://exa.ai/docs/reference/search

Utilizes the exa-py library to perform an instant search, optimized for low latency. It allows fetching results and their content with specified character limits.

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

results = exa.search_and_contents(
    "What is the capital of France?",
    type="instant",
    num_results=10,
    text={"maxCharacters": 1000}
)

print(results)
```

--------------------------------

### Exa Advanced Web Search: Deep Dive on a Person

Source: https://exa.ai/docs/reference/people-search-claude-skill

Example of a deep dive search using `web_search_advanced_exa` for a specific person's background. It utilizes `livecrawl` for fallback and specifies the number of results.

```json
{
  "query": "Dario Amodei Anthropic CEO background",
  "type": "auto",
  "livecrawl": "fallback",
  "numResults": 15
}
```

--------------------------------

### Perform Simple Search and Contents Retrieval

Source: https://exa.ai/docs/reference/search

Executes a basic search query and retrieves content highlights. Requires the exa-py or exa-js library and a valid API key.

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

results = exa.search_and_contents(
    "Latest research in LLMs", 
    highlights={"max_characters": 4000}
)

print(results)
```

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const results = await exa.searchAndContents(
    'Latest research in LLMs', 
    { highlights: { maxCharacters: 4000 } }
);

console.log(results);
```

--------------------------------

### Exa Advanced Web Search: News Mentions

Source: https://exa.ai/docs/reference/people-search-claude-skill

Shows how to use `web_search_advanced_exa` to find news mentions for a specific query. Includes setting the category to 'news', number of results, and a start publication date.

```json
{
  "query": "Dario Amodei interview",
  "category": "news",
  "numResults": 10,
  "startPublishedDate": "2024-01-01"
}
```

--------------------------------

### Implement Exa Web Search with OpenAI Function Calling

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

This script demonstrates how to define an 'exa_websearch' tool, execute it when requested by an OpenAI model, and feed the search results back into the conversation for a final, cited response. It requires the 'openai' and 'exa_py' libraries and valid API keys for both services.

```python
import json
from openai import OpenAI
from exa_py import Exa

OPENAI_API_KEY = ""  # Add your OpenAI API key here
EXA_API_KEY = ""     # Add your Exa API key here

# Define the tool for Exa web search
tools = [{
    "type": "function",
    "name": "exa_websearch",
    "description": "Use Exa for the most accurate and latest web results for LLMs",
    "parameters": {
        "type": "object",
        "properties": {
            "query": {
                "type": "string",
                "description": "Search query for Exa."
            }
        },
        "required": ["query"],
        "additionalProperties": False
    },
    "strict": True
}]

# Define the system message
system_message = {"role": "system", "content": "You are a helpful assistant. Use exa_websearch to find info when relevant. Always list sources."}

def run_exa_search(user_query):
    """Run an Exa web search with a dynamic user query."""
    openai_client = OpenAI(api_key=OPENAI_API_KEY)
    exa = Exa(api_key=EXA_API_KEY)

    messages = [
        system_message,
        {"role": "user", "content": user_query}
    ]

    # Send initial request
    print("Sending initial request to OpenAI...")
    response = openai_client.responses.create(
        model="gpt-4o",
        input=messages,
        tools=tools
    )

    # Check if the model returned a function call
    function_call = None
    for item in response.output:
        if item.type == "function_call" and item.name == "exa_websearch":
            function_call = item
            break

    if function_call:
        call_id = function_call.call_id
        args = json.loads(function_call.arguments)
        query = args.get("query", "")

        search_results = exa.search_and_contents(
            query=query,
            text = {"max_characters": 4000},
            type="auto"
        )

        citations = [{"url": result.url, "title": result.title} for result in search_results.results]
        search_results_str = str(search_results)

        messages.append({
            "type": "function_call",
            "name": function_call.name,
            "arguments": function_call.arguments,
            "call_id": call_id
        })
        messages.append({
            "type": "function_call_output",
            "call_id": call_id,
            "output": search_results_str
        })

        response = openai_client.responses.create(
            model="gpt-4o",
            input=messages,
            tools=tools
        )
        return response
```

--------------------------------

### Instant Search (Lowest Latency) (JavaScript)

Source: https://exa.ai/docs/reference/search

Implements an instant search using the exa-js library for rapid information retrieval. This method allows specifying the number of results and content length constraints.

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const results = await exa.searchAndContents(
    'What is the capital of France?',
    {
        type: 'instant',
        numResults: 10,
        text: { maxCharacters: 1000 }
    }
);

console.log(results);
```

--------------------------------

### EXA_CONTENTS Function for Google Sheets

Source: https://exa.ai/docs/reference/exa-for-sheets

The EXA_CONTENTS function extracts the main text content from a specified URL. It requires a full URL (starting with http/https) as input and returns a string containing the extracted content from the webpage.

```Google Apps Script
=EXA_CONTENTS("https://example.com/article")
```

--------------------------------

### Python: Using Highlights for Agentic Workflows

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Demonstrates how to use the `highlights=True` parameter in `exa.search_and_contents` for agentic workflows. This helps conserve tokens by retrieving only relevant excerpts instead of full text.

```python
result = exa.search_and_contents(query=query, type="auto", highlights=True)
```

--------------------------------

### Fast-Baseline Configuration

Source: https://exa.ai/docs/reference/evaluating-exa-search

A recommended configuration template for latency-sensitive evaluations, optimizing for speed.

```APIDOC
## Fast-Baseline Configuration

### Description
A recommended configuration template for latency-sensitive evaluations, optimizing for speed.

### Method
POST

### Endpoint
/search

### Parameters
#### Query Parameters
- **type** (string) - `auto`
- **num_results** (integer) - `10`
- **text** (object) - `{"max_characters": 15000}`

### Request Example (Python)
```python
result = exa.search_and_contents(
    query,
    type="auto",
    num_results=10,
    text={"max_characters": 15000}
)
```

### Request Example (JavaScript)
```javascript
const result = await exa.searchAndContents(query, {
    type: "auto",
    numResults: 10,
    text: {maxCharacters: 15000}
});
```

### Request Example (cURL)
```bash
curl -X POST https://api.exa.ai/search \
  -H "x-api-key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "your query here",
    "type": "auto",
    "num_results": 10,
    "contents": {"text": {"max_characters": 15000}}
  }'
```
```

--------------------------------

### Enable All Exa MCP Tools with API Key

Source: https://exa.ai/docs/reference/exa-mcp

This URL enables all available Exa MCP tools and requires an Exa API key to be provided via the 'exaApiKey' parameter. This is necessary to overcome free plan rate limits and access all functionalities.

```url
https://mcp.exa.ai/mcp?exaApiKey=YOUR_KEY&tools=web_search_exa,web_search_advanced_exa,get_code_context_exa,crawling_exa,company_research_exa,people_search_exa,deep_researcher_start,deep_researcher_check,deep_search_exa
```

--------------------------------

### Highlights Configuration

Source: https://exa.ai/docs/reference/evaluating-exa-search

A recommended configuration template for retrieving targeted excerpts, focusing on highlight extracts.

```APIDOC
## Highlights Configuration

### Description
A recommended configuration template for retrieving targeted excerpts, focusing on highlight extracts.

### Method
POST

### Endpoint
/search

### Parameters
#### Query Parameters
- **type** (string) - `auto`
- **num_results** (integer) - `10`
- **highlights** (object) - `{"max_characters": 2000}`

### Request Example (Python)
```python
result = exa.search_and_contents(
    query,
    type="auto",
    num_results=10,
    highlights={"max_characters": 2000}
)
```

### Request Example (JavaScript)
```javascript
const result = await exa.searchAndContents(query, {
    type: "auto",
    numResults: 10,
    highlights: {maxCharacters: 2000}
});
```
```

--------------------------------

### Perform a Search Request with Exa API

Source: https://exa.ai/docs/reference/search

Demonstrates how to execute a search query against the Exa API using cURL. This request includes a query string and specifies content retrieval parameters.

```bash
curl -X POST 'https://api.exa.ai/search' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": "Latest research in LLMs",
    "contents": {
      "highlights": {
        "maxCharacters": 4000
      }
    }
  }'
```

--------------------------------

### Set up OpenAI generation chain

Source: https://exa.ai/docs/reference/langchain

Defines the final RAG generation pipeline using OpenAI's Chat models, incorporating the retrieved context into a system prompt for research-based responses.

```Python
from langchain_core.runnables import RunnablePassthrough, RunnableParallel
from langchain_core.prompts import ChatPromptTemplate
from langchain_openai import ChatOpenAI
from langchain_core.output_parsers import StrOutputParser

generation_prompt = ChatPromptTemplate.from_messages([
    ("system", "You are an expert research assistant. You use xml-formatted context to research people's questions."),
    ("human", """
Please answer the following query based on the provided context. Please cite your sources at the end of your response.:

Query: {query}
---
<context>
{context}
</context>
""")
])
```

--------------------------------

### Instant Search (Lowest Latency) (Bash)

Source: https://exa.ai/docs/reference/search

Performs an instant search with minimal latency, retrieving a specified number of results and content snippets. This is suitable for real-time information retrieval.

```bash
curl --request POST \
  --url https://api.exa.ai/search \
  --header 'x-api-key: <token>' \
  --header 'Content-Type: application/json' \
  --data '{ \
  "query": "What is the capital of France?", \
  "type": "instant", \
  "numResults": 10, \
  "contents": { \
    "text": { \
      "maxCharacters": 1000 \
    } \
  }
}'
```

--------------------------------

### Use Exa's /answer endpoint with OpenAI SDK (Python, JavaScript, cURL)

Source: https://exa.ai/docs/reference/openai-sdk

Demonstrates how to configure the OpenAI SDK to use Exa's `/answer` endpoint by replacing the base URL, API key, and model name. It shows how to send a chat completion request and retrieve the response content and citations. The `extra_body` parameter can be used to pass additional arguments to the Exa endpoint, such as `text: true` to include full text from sources.

```python
from openai import OpenAI

client = OpenAI(
  base_url="https://api.exa.ai", # use exa as the base url
  api_key="YOUR_EXA_API_KEY", # update your api key
)

completion = client.chat.completions.create(
  model="exa",
  messages = [
  {"role": "system", "content": "You are a helpful assistant."},
  {"role": "user", "content": "What are the latest developments in quantum computing?"}
],

  # use extra_body to pass extra parameters to the /answer endpoint
  extra_body={
    "text": True # include full text from sources
  }
)

print(completion.choices[0].message.content)  # print the response content
print(completion.choices[0].message.citations)  # print the citations

```

```javascript
import OpenAI from "openai";

const openai = new OpenAI({
  baseURL: "https://api.exa.ai", // use exa as the base url
  apiKey: "YOUR_EXA_API_KEY", // update your api key
});

async function main() {
  const completion = await openai.chat.completions.create({
    model: "exa",
    messages: [
      { role: "system", content: "You are a helpful assistant." },
      {
        role: "user",
        content: "What are the latest developments in quantum computing?",
      },
    ],
    store: true,
    stream: true,
    extra_body: {
      text: true, // include full text from sources
    },
  });

  for await (const chunk of completion) {
    console.log(chunk.choices[0].delta.content);
  }
}

main();

```

```bash
curl https://api.exa.ai/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $YOUR_EXA_API_KEY" \
  -d '{
    "model": "exa",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "What are the latest developments in quantum computing?"
      }
    ],
    "extra_body": {
      "text": true
    }
  }'

```

--------------------------------

### Auto-Quality Configuration

Source: https://exa.ai/docs/reference/evaluating-exa-search

A recommended configuration template for balanced evaluations, offering a mix of speed and quality.

```APIDOC
## Auto-Quality Configuration

### Description
A recommended configuration template for balanced evaluations, offering a mix of speed and quality.

### Method
POST

### Endpoint
/search

### Parameters
#### Query Parameters
- **type** (string) - `auto`
- **num_results** (integer) - `10`
- **text** (object) - `{"max_characters": 15000}`

### Request Example (Python)
```python
result = exa.search_and_contents(
    query,
    type="auto",
    num_results=10,
    text={"max_characters": 15000}
)
```

### Request Example (JavaScript)
```javascript
const result = await exa.searchAndContents(query, {
    type: "auto",
    numResults: 10,
    text: {maxCharacters: 15000}
});
```
```

--------------------------------

### Configure CrewAI agents

Source: https://exa.ai/docs/reference/crewai

Initializes the researcher and writer agents, assigning them the custom Exa tool to perform research and generate content.

```Python
from crewai import Task, Crew, Agent

exa_tools = search_and_get_contents_tool

researcher = Agent(
  role='Researcher',
  goal='Get the latest research on {topic}',
  verbose=True,
  memory=True,
  backstory=(
    "Driven by curiosity, you're at the forefront of"
    "innovation, eager to explore and share knowledge that could change"
    "the world."
  ),
  tools=[exa_tools],
  allow_delegation=False
)

article_writer = Agent(
  role='Researcher',
  goal='Write a great newsletter article on {topic}',
  verbose=True,
  memory=True,
  backstory=(
    "Driven by a love of writing and passion for"
    "innovation, you are eager to share knowledge with"
    "the world."
  ),
  tools=[exa_tools],
  allow_delegation=False
)
```

--------------------------------

### Implement Exa search tool and processing logic in Python

Source: https://exa.ai/docs/reference/anthropic-tool-calling

Defines the 'exa_search' function to interface with the Exa SDK and a 'process_tool_calls' function to handle tool invocation from LLM outputs. It requires the Exa Python SDK and a configured Claude client.

```python
def exa_search(query: str) -> Dict[str, Any]:
	return exa.search_and_contents(query=query, type='auto', highlights=True)

def process_tool_calls(tool_calls):
	search_results = []
	for tool_call in tool_calls:
		function_name = tool_call.name
		function_args = tool_call.input
		if function_name == "exa_search":
			results = exa_search(**function_args)
			search_results.append(results)
	return search_results
```

--------------------------------

### Build OpenAI Release Timeline with Exa Research API

Source: https://exa.ai/docs/reference/exa-research

This snippet shows how to use the Exa Research API to generate a chronological timeline of OpenAI product releases. It specifies the desired output schema for dates and descriptions. The code polls for completion and prints the structured results. Dependencies include the 'exa_py' library and an EXA_API_KEY environment variable.

```python
import os
from exa_py import Exa

exa = Exa(os.environ["EXA_API_KEY"])

instructions = "Create a chronological timeline (year, month, brief description) of major OpenAI product releases from 2015 to 2023."
schema = {
    "type": "object",
    "required": ["events"],
    "properties": {
        "events": {
            "type": "array",
            "items": {
                "type": "object",
                "required": ["date", "description"],
                "properties": {
                    "date": {"type": "string"},
                    "description": {"type": "string"}
                }
            }
        }
    },
    "additionalProperties": False
}

research = exa.research.create(
    model="exa-research",
    instructions=instructions,
    output_schema=schema
)

# Poll until completion
result = exa.research.poll_until_finished(research.researchId)
print(result)
```

```javascript
import Exa, { ResearchModel } from "exa-js";

const exa = new Exa(process.env.EXA_API_KEY);

async function createTimeline() {
  const research = await exa.research.create({
    model: ResearchModel.exa_research,
    instructions:
      "Create a chronological timeline (year, month, brief description) of major OpenAI product releases from 2015 to 2023.",
    outputSchema: {
      type: "object",
      required: ["events"],
      properties: {
        events: {
          type: "array",
          items: {
            type: "object",
            required: ["date", "description"],
            properties: {
              date: { type: "string" },
              description: { type: "string" },
            },
          },
        },
      },
      additionalProperties: false,
    },
  });

  // Poll until completion
  const result = await exa.research.pollUntilFinished(research.researchId);
  console.log("Research result:", result);
}

createTimeline();
```

```bash
curl -X POST https://api.exa.ai/research/v1 \
  -H "x-api-key: $EXA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{ \
    "instructions": "Create a chronological timeline (year, month, brief description) of major OpenAI product releases from 2015 to 2023.", \
    "outputSchema": { \
      "type": "object", \
      "required": ["events"], \
      "properties": { \
        "events": { \
          "type": "array", \
          "items": { \
            "type": "object", \
            "required": ["date", "description"], \
            "properties": { \
              "date": {"type": "string"}, \
              "description": {"type": "string"} \
            } \
          } \
        } \
      }, \
      "additionalProperties": false \
    } \
  }'
```

--------------------------------

### POST /responses

Source: https://exa.ai/docs/reference/openai-sdk

A simplified interface for single-turn research tasks using the OpenAI Responses API format.

```APIDOC
## POST /responses

### Description
Provides a streamlined interface for single-turn research queries. This endpoint is optimized for quick summaries and direct answers.

### Method
POST

### Endpoint
https://api.exa.ai/responses

### Request Body
- **model** (string) - Required - The model to use: 'exa-research' or 'exa-research-pro'.
- **input** (string) - Required - The research query or prompt.

### Request Example
{
  "model": "exa-research",
  "input": "Summarize the impact of CRISPR on gene therapy"
}

### Response
#### Success Response (200)
- **output** (string) - The generated research response.

#### Response Example
{
  "output": "CRISPR has revolutionized gene therapy by..."
}
```

--------------------------------

### Configure Exa Search API Requests

Source: https://exa.ai/docs/reference/evaluating-exa-search

Demonstrates recommended configurations for the search_and_contents method. It highlights the use of character limits to ensure consistent evaluation results across different queries.

```python
# Option 1: Use text with character limit (recommended for consistent comparisons)
exa.search_and_contents(
    query,
    type="auto",  # or "fast" (for `Deep`, see Option 2)
    num_results=10,
    text={"max_characters": 15000}
)

# Option 2: Use highlights for targeted excerpts
# exa.search_and_contents(
#     query,
#     type="auto",
#     num_results=10,
#     highlights={"max_characters": 2000}
# )

# Option 3 (Deprecated): Use context string for RAG
# Note: The `context` parameter is deprecated. Use `text` or `highlights` instead.
# exa.search_and_contents(
#     query,
#     type="deep",
#     additional_queries=["variation 1", "variation 2"],
#     num_results=10,
#     context={"max_characters": 20000}  # Deprecated
# )

# Option 4: Use full text (may result in very long content)
# exa.search_and_contents(
#     query,
#     type="auto",
#     num_results=10,
#     text=True
# )
```

--------------------------------

### Manage Content Freshness with maxAgeHours

Source: https://exa.ai/docs/reference/search-best-practices

Demonstrates how to control cache versus live-crawl behavior using the maxAgeHours parameter. This is essential for balancing data recency with API latency and cost.

```json
{
  "query": "latest announcements from OpenAI",
  "includeDomains": ["openai.com"],
  "maxAgeHours": 72,
  "contents": {
    "highlights": {
      "maxCharacters": 4000
    }
  }
}
```

--------------------------------

### POST /search - Content Configuration

Source: https://exa.ai/docs/reference/search-best-practices

Configure the content retrieval mode to balance token efficiency and answer quality. Use 'highlights' for agentic workflows or 'text' for deep research.

```APIDOC
## POST /search

### Description
Configures the retrieval mode for search results to optimize token usage.

### Method
POST

### Parameters
#### Request Body
- **query** (string) - Required - The search query string.
- **contents** (object) - Required - Configuration for content retrieval (text, highlights, or summary).
- **maxAgeHours** (number) - Optional - Controls data freshness.

### Request Example
{
  "query": "What is the current Fed interest rate?",
  "contents": {
    "highlights": { "maxCharacters": 4000 }
  },
  "maxAgeHours": 0
}
```

--------------------------------

### Exa Web Search Options Reference

Source: https://exa.ai/docs/reference/vercel

A comprehensive reference object demonstrating all available configuration parameters for the webSearch function, including filters, content settings, and location settings.

```typescript
webSearch({
  type: "auto",
  category: "news",
  numResults: 10,
  includeDomains: ["linkedin.com", "github.com"],
  excludeDomains: ["wikipedia.com"],
  startPublishedDate: "2025-01-01T00:00:00.000Z",
  endPublishedDate: "2025-12-31T23:59:59.999Z",
  startCrawlDate: "2025-01-01T00:00:00.000Z",
  endCrawlDate: "2025-12-31T23:59:59.999Z",
  includeText: ["AI"],
  excludeText: ["spam"],
  userLocation: "US",
  contents: {
    text: {
      maxCharacters: 1000,
      includeHtmlTags: false,
    },
    summary: {
      query: "Main points",
    },
    livecrawl: "fallback",
    livecrawlTimeout: 10000,
    subpages: 5,
    subpageTarget: "about",
    extras: {
      links: 5,
      imageLinks: 3,
    },
  },
})
```

--------------------------------

### TypeScript Type Usage

Source: https://exa.ai/docs/reference/vercel

Demonstrates how to import and use Exa's provided TypeScript interfaces for type-safe configuration.

```typescript
import { webSearch, ExaSearchConfig, ExaSearchResult } from "@exalabs/ai-sdk";

const config: ExaSearchConfig = {
  numResults: 10,
  type: "auto",
};

const search = webSearch(config);
```

--------------------------------

### Deep-Comprehensive Configuration

Source: https://exa.ai/docs/reference/evaluating-exa-search

A recommended configuration template for agentic and research evaluations, utilizing deep search capabilities.

```APIDOC
## Deep-Comprehensive Configuration

### Description
A recommended configuration template for agentic and research evaluations, utilizing deep search capabilities.

### Method
POST

### Endpoint
/search

### Parameters
#### Query Parameters
- **type** (string) - `deep`
- **additional_queries** / **additionalQueries** (array) - Provide 2-3 query variations.
- **num_results** (integer) - `10`
- **text** (boolean) - `true`
- **livecrawl** (string) - `"fallback"`

### Request Example (Python)
```python
result = exa.search_and_contents(
    query,
    type="deep",
    additional_queries=[variation1, variation2],
    num_results=10,
    text=True,
    livecrawl="fallback"
)
```

### Request Example (JavaScript)
```javascript
const result = await exa.searchAndContents(query, {
    type: "deep",
    additionalQueries: [variation1, variation2],
    numResults: 10,
    text: true,
    livecrawl: "fallback"
});
```
```

--------------------------------

### Documentation Index

Source: https://exa.ai/docs/reference/research/list-tasks

Fetch the complete documentation index to discover all available pages.

```APIDOC
## GET /docs/llms.txt

### Description
Fetch the complete documentation index at: https://exa.ai/docs/llms.txt. Use this file to discover all available pages before exploring further.

### Method
GET

### Endpoint
/docs/llms.txt

### Response
#### Success Response (200)
- **content** (string) - The content of the documentation index file, listing available documentation pages.

#### Response Example
(Content will vary, but will be a text file listing documentation paths)
```

--------------------------------

### Main Agent Execution Loop

Source: https://exa.ai/docs/reference/openai-tool-calling

Orchestrates the interaction between the user, the OpenAI model, and the Exa search tool. It manages the multi-turn conversation flow to answer queries based on retrieved web content.

```python
def main():
    messages = [SYSTEM_MESSAGE]
    while True:
        user_query = Prompt.ask("[bold yellow]What do you want to search for?[/bold yellow]")
        messages.append({"role": "user", "content": user_query})
        completion = openai.chat.completions.create(model="gpt-4o", messages=messages, tools=TOOLS, tool_choice="auto")
        message = completion.choices[0].message
        if message.tool_calls:
            messages.append(message)
            messages = process_tool_calls(message.tool_calls, messages)
            messages.append({"role": "user", "content": "Answer my previous query based on the search results."})
            completion = openai.chat.completions.create(model="gpt-4o", messages=messages)
            console.print(Markdown(completion.choices[0].message.content))
```

--------------------------------

### POST /search (Instant Search)

Source: https://exa.ai/docs/reference/search

Performs an instant search for the lowest latency results. This is suitable for real-time applications where speed is critical.

```APIDOC
## POST /search (Instant Search)

### Description
Performs an instant search for the lowest latency results. This is suitable for real-time applications where speed is critical.

### Method
POST

### Endpoint
/search

### Parameters
#### Query Parameters
- **query** (string) - Required - The search query.
- **type** (string) - Optional - The search type. Defaults to 'neural'. Can be 'instant'.
- **numResults** (integer) - Optional - The number of results to return. Maximum 100.
- **contents** (object) - Optional - Specifies the content to retrieve. `text: { maxCharacters: 1000 }` retrieves the text content up to 1000 characters.

### Request Example
```json
{
  "query": "What is the capital of France?",
  "type": "instant",
  "numResults": 10,
  "contents": {
    "text": {
      "maxCharacters": 1000
    }
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - An array of search results.

#### Response Example
```json
{
  "results": [
    {
      "title": "Paris - Wikipedia",
      "url": "https://en.wikipedia.org/wiki/Paris",
      "text": "Paris is the capital and most populous city of France..."
    }
  ]
}
```
```

--------------------------------

### Configure Content Freshness and Crawling Parameters

Source: https://exa.ai/docs/reference/contents-best-practices

Demonstrates how to control cache freshness using maxAgeHours and set timeouts for live crawls, ensuring data is retrieved according to specific latency and accuracy requirements.

```json
{
  "ids": ["https://www.apple.com/newsroom/"],
  "maxAgeHours": 24,
  "livecrawlTimeout": 6000,
  "highlights": {
    "maxCharacters": 4000
  }
}
```

--------------------------------

### Configure Exa Search Parameters in Chat Completions

Source: https://exa.ai/docs/reference/openai-sdk

Shows how to pass custom Exa search parameters into the chat completions create method. This allows control over search behavior, result limits, domain filtering, and content categories.

```python
completion = exa_openai.chat.completions.create(
    model="gpt-4o",
    messages=messages,
    use_exa="auto",              # "auto", "required", or "none"
    num_results=5,               # defaults to 3
    result_max_len=1024,         # defaults to 2048 characters
    include_domains=["arxiv.org"],
    category="research paper",
    start_published_date="2019-01-01"
)
```

--------------------------------

### Generate search answers using Exa API

Source: https://exa.ai/docs/reference/answer

Demonstrates how to perform a search query and retrieve a generated answer using the Exa API. Supports various programming languages to integrate search-based intelligence into applications.

```bash
curl -X POST 'https://api.exa.ai/answer' \
  -H 'x-api-key: YOUR-EXA-API-KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "query": "What is the latest valuation of SpaceX?",
    "text": true
  }'
```

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

result = exa.answer(
    "What is the latest valuation of SpaceX?",
    text=True
)

print(result)
```

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const result = await exa.answer(
    'What is the latest valuation of SpaceX?',
    { text: true }
);

console.log(result);
```

--------------------------------

### POST /context

Source: https://exa.ai/docs/reference/context

Retrieves relevant code context for a given query, with options for token limit management.

```APIDOC
## POST /context

### Description
This endpoint retrieves relevant code context for a given query. It allows for dynamic or specific token limits to control the response length and cost.

### Method
POST

### Endpoint
/context

### Parameters
#### Query Parameters
None

#### Request Body
- **query** (string) - Required - The search query for which to retrieve context.
- **tokensNum** (string | integer) - Optional - The token limit for the response. Defaults to "dynamic".
  - Accepted values: "dynamic", or an integer between 50 and 100000.
  - "dynamic": Automatically determines the optimal response length.
  - Integer: Specifies an exact number of tokens.

### Request Example
```json
{
  "query": "Express.js middleware for authentication",
  "tokensNum": "dynamic"
}
```

### Response
#### Success Response (200)
- **response** (string) - The retrieved code context.

#### Response Example
```json
{
  "response": "// Example code context..."
}
```
```

--------------------------------

### Main Function for Interactive Search Agent

Source: https://exa.ai/docs/reference/openai-tool-calling

The main function orchestrates the search agent's interaction loop. It prompts the user for queries, uses OpenAI to determine search actions, processes tool calls (like exa_search), and displays responses using markdown. It includes error handling and utilizes the 'rich' library for console output. Dependencies include 'openai', 'rich', and the 'process_tool_calls' function.

```python
def main():
    messages = [SYSTEM_MESSAGE]
    while True:
        try:
            user_query = Prompt.ask(
                "[bold yellow]What do you want to search for?[/bold yellow]",
            )
            messages.append({"role": "user", "content": user_query})
            completion = openai.chat.completions.create(
                model="gpt-4o-mini",
                messages=messages,
                tools=TOOLS,
            )
            message = completion.choices[0].message
            tool_calls = message.tool_calls
            if tool_calls:
                messages.append(message)
                messages = process_tool_calls(tool_calls, messages)
                messages.append(
                    {
                        "role": "user",
                        "content": "Answer my previous query based on the search results.",
                    }
                )
                completion = openai.chat.completions.create(
                    model="gpt-4o-mini",
                    messages=messages,
                )
                console.print(Markdown(completion.choices[0].message.content))
            else:
                console.print(Markdown(message.content))
        except Exception as e:
            console.print(f"[bold red]An error occurred:[/bold red] {str(e)}")
if __name__ == "__main__":
    main()
```

--------------------------------

### Define tasks and initialize crew

Source: https://exa.ai/docs/reference/crewai

Sets up specific tasks for the agents and organizes them into a Crew object to manage the research and writing workflow.

```Python
research_task = Task(
  description=(
    "Identify the latest research in {topic}."
    "Your final report should clearly articulate the key points,"
  ),
  expected_output='A comprehensive 3 paragraphs long report on the {topic}.',
  tools=[exa_tools],
  agent=researcher,
)

write_article = Task(
  description=(
    "Write a newsletter article on the latest research in {topic}."
    "Your article should be engaging, informative, and accurate."
    "The article should address the audience with a greeting to the newsletter audience \"Hi readers!\", plus a similar signoff"
  ),
  expected_output='A comprehensive 3 paragraphs long newsletter article on the {topic}.',
  agent=article_writer,
)

crew = Crew(
  agents=[researcher, article_writer],
  tasks=[research_task, write_article],
  memory=True,
  cache=True,
  max_rpm=100,
  share_crew=True
)
```

--------------------------------

### Exa AI Search API - Configuration Parameters

Source: https://exa.ai/docs/reference/evaluating-exa-search

This section outlines the available configuration parameters for the Exa AI Search API, detailing their purpose and recommended usage for different evaluation strategies.

```APIDOC
## Exa AI Search API - Configuration Parameters

### Description
This section outlines the available configuration parameters for the Exa AI Search API, detailing their purpose and recommended usage for different evaluation strategies.

### Parameters
#### Query Parameters
- **type** (string) - Optional - Specifies the search method. Recommended values: `fast`, `auto`, `deep`.
- **num_results** (integer) - Optional - The number of search results to retrieve. Default is 10.
- **text** (boolean or object) - Optional - If `true`, retrieves the full content. Can also be an object to specify content retrieval options, e.g., `{"max_characters": 15000}`.
- **context** (string) - Deprecated - Use `text` or `highlights` instead.
- **livecrawl** (string) - Optional - Controls real-time web fetching. Recommended: `"fallback"`. Use `"preferred"` for freshness tests.
- **additional_queries** / **additionalQueries** (array) - Optional - Used with `type: "deep"` to provide query variations. Expects an array of strings.

### Request Example (Conceptual)
```json
{
  "query": "your search query",
  "type": "auto",
  "num_results": 10,
  "text": {"max_characters": 15000},
  "livecrawl": "fallback"
}
```

### Response (Conceptual)
```json
{
  "results": [
    {
      "title": "Example Title",
      "url": "http://example.com",
      "content": "The full content of the page..."
    }
  ]
}
```
```

--------------------------------

### POST /search/options

Source: https://exa.ai/docs/reference/find-similar-links

Configuration options for controlling content highlights, summaries, and livecrawling behavior in search requests.

```APIDOC
## POST /search/options

### Description
Configures the extraction of highlights, generation of summaries, and livecrawling behavior for search results.

### Method
POST

### Endpoint
/search/options

### Parameters
#### Request Body
- **highlights** (object) - Optional - Advanced options for controlling highlight extraction.
  - **maxCharacters** (integer) - Optional - Maximum number of characters to return for highlights.
  - **query** (string) - Optional - Custom query to direct the LLM's selection of highlights.
- **summary** (object) - Optional - Configuration for LLM-generated webpage summaries.
  - **query** (string) - Optional - Custom query for the LLM-generated summary.
  - **schema** (object) - Optional - JSON schema for structured output from summary.
- **livecrawlTimeout** (integer) - Optional - The timeout for livecrawling in milliseconds (default: 10000).
- **maxAgeHours** (integer) - Optional - Maximum age of cached content in hours to trigger livecrawling.

### Request Example
{
  "highlights": {
    "maxCharacters": 2000,
    "query": "Key advancements"
  },
  "summary": {
    "query": "Main developments"
  },
  "livecrawlTimeout": 1000,
  "maxAgeHours": 24
}

### Response
#### Success Response (200)
- **status** (string) - Success status message

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### Perform Chat Completions with Exa Research Models

Source: https://exa.ai/docs/reference/openai-sdk

Demonstrates how to stream research responses using the OpenAI SDK or cURL by pointing the base URL to Exa's API. This method is suitable for interactive, multi-turn chat interfaces.

```python
import os
from openai import OpenAI

client = OpenAI(
    base_url="https://api.exa.ai",
    api_key=os.environ["EXA_API_KEY"],
)

completion = client.chat.completions.create(
    model="exa-research", # or exa-research-pro
    messages=[
        {"role": "user", "content": "What makes some LLMs so much better than others?"}
    ],
    stream=True,
)

for chunk in completion:
    if chunk.choices and chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
```

```javascript
import { OpenAI } from "openai";

async function main() {
  const openai = new OpenAI({
    apiKey: process.env.EXA_API_KEY,
    baseURL: "https://api.exa.ai",
  });

  const stream = await openai.chat.completions.create({
    model: "exa-research", // or exa-research-pro
    messages: [
      {
        role: "user",
        content: "What are ants",
      },
    ],
    stream: true,
  });

  for await (const chunk of stream) {
    const content = chunk.choices?.[0]?.delta?.content;
    if (content) {
      process.stdout.write(content);
    }
  }
}

main().catch((err) => {
  console.error("Chat completion example failed:", err);
  process.exit(1);
});
```

```bash
curl https://api.exa.ai/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $YOUR_EXA_API_KEY" \
  -d '{
    "model": "exa-research",
    "messages": [
      {
        "role": "user",
        "content": "What makes some LLMs so much better than others?"
      }
    ],
    "stream": true
  }'
```

--------------------------------

### Define and Execute Exa AI Search Tool

Source: https://exa.ai/docs/reference/openai-tool-calling

Defines the tool schema for OpenAI function calling and implements the search logic using the Exa SDK. The function retrieves web search results with highlights to provide context for the LLM.

```python
TOOLS = [
    {
        "type": "function",
        "function": {
            "name": "exa_search",
            "description": "Perform a search query on the web, and retrieve the world's most relevant information.",
            "parameters": {
                "type": "object",
                "properties": {
                    "query": {
                        "type": "string",
                        "description": "The search query to perform.",
                    },
                },
                "required": ["query"],
            },
        },
    }
]

def exa_search(query: str) -> Dict[str, Any]:
    return exa.search_and_contents(query=query, type='auto', highlights=True)
```

--------------------------------

### Define Web Search Tool for LLM

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

Configuration for an Exa web search tool definition compatible with OpenAI function calling. It specifies the query parameter and tool metadata.

```javascript
const tools = [
  {
    type: "function",
    name: "exa_websearch",
    description: "Use Exa for the most accurate and latest web results for LLMs",
    parameters: {
      type: "object",
      properties: {
        query: {
          type: "string",
          description: "Search query for Exa."
        }
      },
      required: ["query"],
      additionalProperties: false
    },
    strict: true
  }
];
```

--------------------------------

### Perform Retrieval, Synthesis, and Grading Workflow

Source: https://exa.ai/docs/reference/evaluating-exa-search

This Python snippet demonstrates the standard evaluation loop for Exa AI. It covers the retrieval of search results, the generation of an answer using a downstream LLM, and the automated grading of the generated response against ground truth.

```python
# 1. Retrieval step
results = exa.search_and_contents(
    query,
    type="auto",  # or "fast", "deep"
    num_results=10,
    text={"max_characters": 15000}
)

# 2. Answer synthesis (downstream LLM restricted to retrieved context)
context = "\n\n".join([r.text for r in results.results])
answer = llm.generate(
    f"Answer the question using only the provided context.\n\n"
    f"Context: {context}\n\n"
    f"Question: {query}\n\n"
    f"Answer:"
)

# 3. Grading (LLM-based correctness evaluation)
grade = grading_llm.evaluate(
    question=query,
    expected_answer=ground_truth,
    generated_answer=answer
)
# Returns: "correct", "partial", or "incorrect"
```

--------------------------------

### POST /answer

Source: https://exa.ai/docs/reference/answer

Performs an Exa search and uses an LLM to generate an answer or summary based on the retrieved content.

```APIDOC
## POST /answer

### Description
Performs an Exa search and uses an LLM to generate either a direct answer or a detailed summary with citations. Supports streaming and structured output via JSON schema.

### Method
POST

### Endpoint
/answer

### Parameters
#### Request Body
- **query** (string) - Required - The question or topic to search and answer.
- **stream** (boolean) - Optional - If true, returns tokens as they are generated.
- **outputSchema** (object) - Optional - A JSON Schema object to force the response into a specific structured format.

### Request Example
{
  "query": "What is the state of AI in healthcare?",
  "stream": false
}

### Response
#### Success Response (200)
- **answer** (string/object) - The generated answer or structured data.
- **sources** (array) - A list of sources used to generate the answer.

#### Response Example
{
  "answer": "AI in healthcare is currently focused on diagnostic imaging and predictive analytics...",
  "sources": ["https://example.com/article1", "https://example.com/article2"]
}
```

--------------------------------

### Process Tool Calls for Agent

Source: https://exa.ai/docs/reference/anthropic-tool-calling

Iterates through tool calls generated by the LLM, executes the corresponding search function if matched, and logs the activity to the console.

```python
def process_tool_calls(tool_calls):
    search_results = []
    for tool_call in tool_calls:
        function_name = tool_call.name
        function_args = tool_call.input
        if function_name == "exa_search":
            results = exa_search(**function_args)
            search_results.append(results)
            console.print(
                f"[bold cyan]Context updated[/bold cyan] [i]with[/i] "
                f"[bold green]exa_search[/bold green]: ",
                function_args.get("query"),
            )
    return search_results
```

--------------------------------

### Define custom Exa search tool

Source: https://exa.ai/docs/reference/crewai

Creates a custom tool using the @tool decorator that utilizes the Exa SDK to perform neural searches and return formatted highlights.

```Python
from crewai_tools import tool
from exa_py import Exa
import os

exa_api_key = os.getenv("EXA_API_KEY")

@tool("Exa search and get contents")
def search_and_get_contents_tool(question: str) -> str:
    """Tool using Exa's Python SDK to run semantic search and return result highlights."""

    exa = Exa(exa_api_key)

    response = exa.search_and_contents(
        question,
        type="neural",
        num_results=3,
        highlights=True
    )

    parsedResult = ''.join([
      f'<Title id={idx}>{eachResult.title}</Title>'
      f'<URL id={idx}>{eachResult.url}</URL>'
      f'<Highlight id={idx}>{"".join(eachResult.highlights)}</Highlight>'
      for (idx, eachResult) in enumerate(response.results)
    ])

    return parsedResult
```

--------------------------------

### Connect Claude Desktop to Remote MCP

Source: https://exa.ai/docs/reference/exa-mcp

This JSON configuration is used to connect Claude Desktop to a remote Exa MCP instance. It specifies the command to execute ('npx') and its arguments, including the 'mcp-remote' wrapper and the MCP URL.

```json
{
  "command": "npx",
  "args": ["-y", "mcp-remote", "https://mcp.exa.ai/mcp"]
}
```

--------------------------------

### POST /chat/completions

Source: https://exa.ai/docs/reference/openai-sdk

Uses the OpenAI-compatible chat completions interface to perform research tasks with streaming support.

```APIDOC
## POST /chat/completions

### Description
Provides access to Exa's research models using the standard OpenAI chat completions interface. Ideal for multi-turn conversations and streaming responses.

### Method
POST

### Endpoint
https://api.exa.ai/chat/completions

### Request Body
- **model** (string) - Required - The model to use: 'exa-research' or 'exa-research-pro'.
- **messages** (array) - Required - A list of message objects representing the conversation history.
- **stream** (boolean) - Optional - Whether to stream the response.

### Request Example
{
  "model": "exa-research",
  "messages": [{"role": "user", "content": "What makes some LLMs so much better than others?"}],
  "stream": true
}

### Response
#### Success Response (200)
- **choices** (array) - The list of completion choices.

#### Response Example
{
  "choices": [{"delta": {"content": "LLMs differ based on..."}}]
}
```

--------------------------------

### Perform Web Search with Exa API

Source: https://exa.ai/docs/reference/anthropic-tool-calling

A wrapper function for the Exa search client that executes a search query and retrieves content highlights. It returns a dictionary containing search results.

```python
def exa_search(query: str) -> Dict[str, Any]:
    return exa.search_and_contents(query=query, type='auto', highlights=True)
```

--------------------------------

### Execute interactive search agent loop

Source: https://exa.ai/docs/reference/anthropic-tool-calling

The main loop manages user input, triggers Claude's tool-calling capabilities, and feeds search results back into the model for final summarization. It uses the Rich library for console output and Markdown rendering.

```python
def main():
	messages = []
	while True:
		user_query = Prompt.ask("[bold yellow]What do you want to search for?[/bold yellow]")
		messages.append({"role": "user", "content": user_query})
		completion = claude.messages.create(model="claude-sonnet-4-6", messages=messages, tools=TOOLS)
		tool_calls = [c for c in completion.content if c.type == "tool_use"]
		if tool_calls:
			search_results = process_tool_calls(tool_calls)
			messages.append({"role": "assistant", "content": f"Results: {search_results}"})
			completion = claude.messages.create(model="claude-sonnet-4-6", messages=messages)
			console.print(Markdown(completion.content[0].text))
```

--------------------------------

### Simple Search and Contents

Source: https://exa.ai/docs/reference/search

Perform a basic search and retrieve content for the given query. This is useful for general information retrieval.

```APIDOC
## POST /search

### Description
Performs a search query and retrieves content, including text, summaries, and links.

### Method
POST

### Endpoint
https://api.exa.ai/search

### Parameters
#### Query Parameters
None

#### Request Body
- **query** (string) - Required - The search query.
- **highlights** (object) - Optional - Configuration for highlighting search results.
  - **max_characters** (integer) - Optional - Maximum characters for highlights.

### Request Example
```json
{
  "query": "Latest research in LLMs",
  "highlights": {
    "max_characters": 4000
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - List of search results.
  - Each result contains fields like `title`, `url`, `content`, etc.

#### Response Example
```json
{
  "results": [
    {
      "title": "Example Title",
      "url": "http://example.com",
      "content": "Example content..."
    }
  ]
}
```
```

--------------------------------

### Enable Specific Exa MCP Tools

Source: https://exa.ai/docs/reference/exa-mcp

This URL enables a specific set of Exa MCP tools by listing them in the 'tools' query parameter. This is useful for tailoring the MCP's capabilities to specific tasks.

```url
https://mcp.exa.ai/mcp?tools=get_code_context_exa,people_search_exa
```

--------------------------------

### Perform Structured Content Extraction with JSON Schema

Source: https://exa.ai/docs/reference/contents-best-practices

Demonstrates how to generate an LLM-based abstract from a URL while enforcing a specific JSON output schema for structured data extraction.

```json
{
  "ids": ["https://example.com/company-page"],
  "summary": {
    "query": "Extract company information",
    "schema": {
      "type": "object",
      "properties": {
        "name": { "type": "string" },
        "industry": { "type": "string" },
        "founded": { "type": "number" }
      },
      "required": ["name", "industry"]
    }
  }
}
```

--------------------------------

### HuggingGPT Orchestration API

Source: https://exa.ai/docs/reference/search

This API allows users to submit complex tasks to HuggingGPT, which will then plan, select models, execute, and summarize the results.

```APIDOC
## POST /api/hugginggpt/tasks

### Description
Submit a complex task to the HuggingGPT framework for processing. HuggingGPT will use ChatGPT to plan the task, select appropriate AI models from Hugging Face, execute subtasks, and provide a summarized result.

### Method
POST

### Endpoint
/api/hugginggpt/tasks

### Parameters
#### Request Body
- **task_description** (string) - Required - A natural language description of the complex task to be solved.
- **domain** (string) - Optional - The specific domain of the task (e.g., 'vision', 'speech', 'language').
- **modality** (string) - Optional - The modality of the task (e.g., 'image', 'audio', 'text').

### Request Example
```json
{
  "task_description": "Generate an image of a cat sitting on a mat and describe it in text.",
  "domain": "vision",
  "modality": "image"
}
```

### Response
#### Success Response (200)
- **task_id** (string) - A unique identifier for the submitted task.
- **status** (string) - The current status of the task (e.g., 'pending', 'processing', 'completed', 'failed').
- **result** (object) - The final result of the task, including a summary and potentially intermediate outputs. This field is populated when the task status is 'completed'.
  - **summary** (string) - A natural language summary of the task outcome.
  - **intermediate_outputs** (array) - Optional - An array of outputs from intermediate steps.

#### Response Example (Pending Task)
```json
{
  "task_id": "task_12345abc",
  "status": "pending"
}
```

#### Response Example (Completed Task)
```json
{
  "task_id": "task_12345abc",
  "status": "completed",
  "result": {
    "summary": "An image of a cat on a mat was generated and described. The cat is fluffy and sleeping peacefully on a red mat.",
    "intermediate_outputs": [
      {
        "step": 1,
        "model": "stable-diffusion-v1-5",
        "output": "image_url_or_data"
      },
      {
        "step": 2,
        "model": "gpt-4-vision-preview",
        "output": "The cat is fluffy and sleeping peacefully on a red mat."
      }
    ]
  }
}
```

### Error Handling
- **400 Bad Request**: Invalid input parameters.
- **500 Internal Server Error**: An error occurred on the server side.
```

--------------------------------

### Interact with Agent using Exa-powered Search

Source: https://exa.ai/docs/reference/llamaindex

Uses the chat method of the configured agent to make a query. The agent leverages the Exa tools to find and summarize news related to the US stock market from the last month.

```Python
agent.chat(
    "Can you summarize the news from the last month related to the US stock market?"
)
```

--------------------------------

### Stream RAG Chain Output

Source: https://exa.ai/docs/reference/langchain

Demonstrates how to stream responses from the RAG chain using both synchronous and asynchronous methods. This is useful for improving perceived latency in user-facing applications.

```Python
for chunk in chain.stream("Latest research on climate change innovation"):
  print(chunk, end="|", flush=True)

async def run_async():
  async for chunk in chain.astream("Latest research on climate change innovation"):
    print(chunk, end="|", flush=True)

import asyncio
asyncio.run(run_async())
```

--------------------------------

### Retrieve Content Highlights and Full Text

Source: https://exa.ai/docs/reference/contents-best-practices

Shows how to request specific content modes. Highlights are ideal for agentic workflows, while full text is used for deep analysis, both supporting character limits to manage token usage.

```json
{
  "ids": ["https://example.com/article"],
  "highlights": {
    "query": "key findings",
    "maxCharacters": 2000
  }
}
```

```json
{
  "ids": ["https://arxiv.org/abs/2301.07041"],
  "text": { "maxCharacters": 20000 }
}
```

--------------------------------

### Research vs Web Search Tool

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

Comparison between Exa's Direct Research and the Web Search Tool (Function Calling).

```APIDOC
## Research vs Web Search Tool

### Description
Understand the differences between Exa's Direct Research capabilities and its Web Search Tool (often used with Function Calling) to choose the best approach for your specific use case.

| Feature           | Web Search Tool (Function Calling)               | Direct Research                     |
| ----------------- | ------------------------------------------------ | ----------------------------------- |
| **Use Case**      | Augment LLM conversations with web data          | Get comprehensive research reports  |
| **Control**       | Full control over search queries and integration | Automated multi-step research       |
| **Response Time** | Fast (seconds)                                   | Longer (45-180 seconds)             |
| **Best For**      | Interactive chatbots, real-time Q&A              | In-depth analysis, research reports |
```

--------------------------------

### Authentication

Source: https://exa.ai/docs/reference/answer

Information on how to authenticate your API requests using an API key.

```APIDOC
## Authentication

API key can be provided either via `x-api-key` header or `Authorization` header with Bearer scheme.

### Security Schemes

- **apikey** (apiKey)
  - **Name**: `x-api-key`
  - **In**: header
  - **Description**: API key can be provided either via x-api-key header or Authorization header with Bearer scheme

```

--------------------------------

### Exa Research Models

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

Information on the available research models for Exa AI.

```APIDOC
## Available Models

### Description
Exa AI offers different research models tailored for various needs:

*   **`exa-research`**: This model adapts compute to the difficulty of the task and is suitable for most general use cases.
*   **`exa-research-pro`**: This model provides the highest quality output and possesses the greatest reasoning capability, making it ideal for complex, multi-step research tasks.
```

--------------------------------

### Web Search (/search) - OpenAI Tool Definition

Source: https://exa.ai/docs/reference/tool-calling-best-practices

This section provides the function definition for Exa's web search (`/search`) endpoint, specifically formatted for OpenAI's tool calling API. It outlines the available parameters such as query, numResults, category, and content retrieval options.

```APIDOC
## POST /search

### Description
Searches the web using Exa with natural language queries. Supports filtering by category and content retrieval options like highlights.

### Method
POST

### Endpoint
/search

#### Parameters

#### Request Body
- **query** (string) - Required - Natural language search query.
- **numResults** (integer) - Optional - Number of results. Default: 10.
- **category** (string) - Optional - Enum: ['company', 'people', 'research paper']. Filters search results. Omit for general queries.
- **contents** (object) - Optional - Content retrieval options.
  - **highlights** (object) - Optional - Token-efficient excerpts.
    - **maxCharacters** (integer) - Optional - Max characters per highlight. Default: 4000.

### Request Example
```json
{
  "query": "latest advancements in renewable energy",
  "numResults": 5,
  "category": "research paper",
  "contents": {
    "highlights": {
      "maxCharacters": 1000
    }
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - List of search results, each containing title, url, content, etc.

#### Response Example
```json
{
  "results": [
    {
      "title": "Example Research Paper on Solar Energy",
      "url": "https://example.com/paper.pdf",
      "content": "Abstract: This paper discusses the latest breakthroughs...",
      "score": 0.95
    }
  ]
}
```
```

--------------------------------

### Auto-Quality Configuration for Balanced Evaluations

Source: https://exa.ai/docs/reference/evaluating-exa-search

This configuration provides a balance between speed and quality, suitable for general evaluations. It uses the 'auto' search type and retrieves a fixed number of results with a specified character limit for the text content. Available in Python and JavaScript.

```python
result = exa.search_and_contents(
    query,
    type="auto",
    num_results=10,
    text={"max_characters": 15000}
)
```

```javascript
const result = await exa.searchAndContents(query, {
    type: "auto",
    numResults: 10,
    text: {maxCharacters: 15000}
});
```

--------------------------------

### Configure Exa AI Search with Category Filters

Source: https://exa.ai/docs/reference/search-best-practices

This JSON snippet demonstrates how to integrate a category filter into an Exa AI search request. It specifies the search query, sets the category to 'company', and defines the number of results and highlight parameters.

```json
{
  "query": "agtech companies in the US that have raised series A",
  "type": "auto",
  "category": "company",
  "numResults": 10,
  "contents": {
    "highlights": {
      "maxCharacters": 4000
    }
  }
}
```

--------------------------------

### Website Summarization

Source: https://exa.ai/docs/reference/search

Generates a summary of the webpage content. Allows for custom queries and structured output schemas.

```APIDOC
## GET /websites/exa_ai/summary

### Description
Generates a summary of the webpage content. You can provide a custom query to guide the summary generation and specify a JSON schema for structured output.

### Method
GET

### Endpoint
/websites/exa_ai/summary

### Parameters
#### Query Parameters
- **summary[query]** (string) - Optional - Custom query for the LLM-generated summary. Example: "Main developments"
- **summary[schema]** (object) - Optional - JSON schema for structured output from the summary. See https://json-schema.org/overview/what-is-jsonschema for documentation. Example:
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Title",
  "type": "object",
  "properties": {
    "Property 1": {
      "type": "string",
      "description": "Description"
    },
    "Property 2": {
      "type": "string",
      "enum": [
        "option 1",
        "option 2",
        "option 3"
      ],
      "description": "Description"
    }
  },
  "required": [
    "Property 1"
  ]
}
```

### Response
#### Success Response (200)
- **summary** (string | object) - The generated summary of the webpage, either as plain text or a structured object based on the provided schema.

#### Response Example
```json
{
  "summary": "This is an example summary of the webpage content."
}
```
```

--------------------------------

### Define Content Extraction Tool

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Configures the exa_get_contents function for use as a tool in LLM agents. Provides schema definitions compatible with OpenAI and Anthropic function calling standards.

```json
{
  "type": "function",
  "function": {
    "name": "exa_get_contents",
    "description": "Extract clean content from URLs. Handles JS-rendered pages, PDFs, and complex layouts. Returns markdown text, highlights, or summaries.",
    "parameters": {
      "type": "object",
      "properties": {
        "ids": {
          "type": "array",
          "items": { "type": "string" },
          "description": "List of URLs to get contents for."
        }
      },
      "required": ["ids"]
    }
  }
}
```

```json
{
  "name": "exa_get_contents",
  "description": "Extract clean content from URLs. Handles JS-rendered pages, PDFs, and complex layouts. Returns markdown text, highlights, or summaries.",
  "input_schema": {
    "type": "object",
    "properties": {
      "ids": {
        "type": "array",
        "items": { "type": "string" },
        "description": "List of URLs to get contents for."
      }
    },
    "required": ["ids"]
  }
}
```

--------------------------------

### Configure Auto Search in Python

Source: https://exa.ai/docs/reference/evaluating-exa-search

Auto search is the default mode, providing a balanced performance profile with a median latency of 1000ms. It is recommended for general-purpose search tasks where query types vary significantly.

```python
result = exa.search_and_contents(
    "companies building climate tech solutions",
    type="auto",  # or omit - auto is default
    num_results=10,
    text={"max_characters": 15000}
)
```

--------------------------------

### Estimate Battery Recycling Market Size (Python, JavaScript, cURL)

Source: https://exa.ai/docs/reference/exa-research

Estimates the global market size for battery recycling in 2030, providing reasoning steps and citing sources. This functionality is accessible via Python, JavaScript, and cURL, requiring an EXA_API_KEY for authentication. The output is structured according to a defined schema, including the estimated USD value and the methodology used.

```python
import os
from exa_py import Exa

exa = Exa(os.environ["EXA_API_KEY"])

instructions = "Estimate the global market size for battery recycling in 2030. Provide reasoning steps and cite sources."
schema = {
    "type": "object",
    "required": ["estimateUsd", "methodology"],
    "properties": {
        "estimateUsd": {"type": "number"},
        "methodology": {"type": "string"}
    },
    "additionalProperties": False
}

research = exa.research.create(
    model="exa-research",
    instructions=instructions,
    output_schema=schema
)

# Poll until completion
result = exa.research.poll_until_finished(research.researchId)
print(result)
```

```javascript
import Exa, { ResearchModel } from "exa-js";

const exa = new Exa(process.env.EXA_API_KEY);

async function estimateMarketSize() {
  const research = await exa.research.create({
    model: ResearchModel.exa_research,
    instructions:
      "Estimate the global market size for battery recycling in 2030. Provide reasoning steps and cite sources.",
    outputSchema: {
      type: "object",
      required: ["estimateUsd", "methodology"],
      properties: {
        estimateUsd: { type: "number" },
        methodology: { type: "string" },
      },
      additionalProperties: false,
    },
  });

  // Poll until completion
  const result = await exa.research.pollUntilFinished(research.researchId);
  console.log("Research result:", result);
}

estimateMarketSize();
```

```curl
curl -X POST https://api.exa.ai/research/v1 \
  -H "x-api-key: $EXA_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "instructions": "Estimate the global market size for battery recycling in 2030. Provide reasoning steps and cite sources.",
    "outputSchema": {
      "type": "object",
      "required": ["estimateUsd", "methodology"],
      "properties": {
        "estimateUsd": {"type": "number"},
        "methodology": {"type": "string"}
      },
      "additionalProperties": false
    }
  }'
```

--------------------------------

### POST /answer

Source: https://exa.ai/docs/reference/answer

Performs a search based on the provided query and generates either a direct answer or a detailed summary with citations.

```APIDOC
## POST /answer

### Description
Performs a search based on the query and generates either a direct answer or a detailed summary with citations, depending on the query type.

### Method
POST

### Endpoint
https://api.exa.ai/answer

### Parameters
#### Request Body
- **query** (string) - Required - The question or query to answer.
- **stream** (boolean) - Optional - If true, the response is returned as a server-sent events (SSE) stream.
- **text** (boolean) - Optional - If true, the response includes full text content in the search results.
- **outputSchema** (object) - Optional - A JSON Schema specification for the desired answer structure.

### Request Example
{
  "query": "What is the latest valuation of SpaceX?",
  "text": true
}

### Response
#### Success Response (200)
- **answer** (string) - The generated answer content.
- **costDollars** (number) - The cost associated with the request.

#### Response Example
{
  "answer": "SpaceX's valuation is approximately $180 billion as of late 2023.",
  "costDollars": 0.005
}
```

--------------------------------

### POST /chat/completions

Source: https://exa.ai/docs/reference/openai-sdk

This endpoint allows users to interact with Exa's research models using the standard OpenAI Chat Completions interface. It supports passing specific Exa parameters via the extra_body field.

```APIDOC
## POST /chat/completions

### Description
Provides a drop-in replacement for the OpenAI Chat Completions API, routing requests to Exa's research models.

### Method
POST

### Endpoint
https://api.exa.ai/chat/completions

### Parameters
#### Request Body
- **model** (string) - Required - The model to use (e.g., "exa", "exa-research", "exa-research-pro").
- **messages** (array) - Required - A list of message objects representing the conversation history.
- **extra_body** (object) - Optional - Additional parameters passed to the underlying Exa /answer endpoint (e.g., {"text": true}).

### Request Example
{
  "model": "exa",
  "messages": [
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "What are the latest developments in quantum computing?"}
  ],
  "extra_body": {
    "text": true
  }
}

### Response
#### Success Response (200)
- **choices** (array) - The list of completion choices.
- **message** (object) - The content and metadata of the response.
- **citations** (array) - Sources used to generate the answer.

#### Response Example
{
  "choices": [
    {
      "message": {
        "content": "Quantum computing is advancing...",
        "citations": ["https://example.com/source1"]
      }
    }
  ]
}
```

--------------------------------

### Implement Exa Search Tool Function

Source: https://exa.ai/docs/reference/openai-tool-calling

Defines the Python function that executes the Exa search and processes the tool call results.

```python
def exa_search(query: str) -> Dict[str, Any]:
    return exa.search_and_contents(query=query, type='auto', highlights=True)

def process_tool_calls(tool_calls, messages):
    for tool_call in tool_calls:
        # Implementation logic here
```

--------------------------------

### Perform Fresh Content Search with Bing and Exa

Source: https://exa.ai/docs/reference/migrating-from-bing

Demonstrates how to retrieve recent search results filtered by a specific timeframe. Requires API keys for either Bing or Exa services.

```bash
curl -H "Ocp-Apim-Subscription-Key: YOUR_KEY" \
  "https://api.bing.microsoft.com/v7.0/search?q=AI+news&freshness=Week"
```

```python
import requests

response = requests.get(
    'https://api.bing.microsoft.com/v7.0/search',
    params={'q': 'AI news', 'freshness': 'Week'},
    headers={'Ocp-Apim-Subscription-Key': 'YOUR_KEY'}
)
```

```javascript
fetch("https://api.bing.microsoft.com/v7.0/search?q=AI+news&freshness=Week", {
  headers: {
    "Ocp-Apim-Subscription-Key": "YOUR_KEY",
  },
});
```

```bash
curl -X POST https://api.exa.ai/search \
  -H "x-api-key: YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "AI news",
    "startPublishedDate": "2025-08-04T00:00:00Z",
    "type": "auto"
  }'
```

```python
from datetime import datetime, timedelta

week_ago = (datetime.now() - timedelta(days=7)).isoformat() + "Z"
results = exa.search(
    "AI news",
    start_published_date=week_ago,
    type="auto"
)
```

```javascript
const weekAgo = new Date();
weekAgo.setDate(weekAgo.getDate() - 7);

const results = await exa.search("AI news", {
  startPublishedDate: weekAgo.toISOString(),
  type: "auto",
});
```

--------------------------------

### Highlights Configuration for Targeted Excerpts

Source: https://exa.ai/docs/reference/evaluating-exa-search

This configuration focuses on retrieving targeted excerpts by specifying a maximum character count for highlights. It uses the 'auto' search type and retrieves a fixed number of results. Available in Python and JavaScript.

```python
result = exa.search_and_contents(
    query,
    type="auto",
    num_results=10,
    highlights={"max_characters": 2000}
)
```

```javascript
const result = await exa.searchAndContents(query, {
    type: "auto",
    numResults: 10,
    highlights: {maxCharacters: 2000}
});
```

--------------------------------

### Deep Search with Query Variations (JavaScript)

Source: https://exa.ai/docs/reference/search

Executes a deep search using the exa-js library, allowing for structured output based on a defined schema. Requires the 'exa-js' package and an API key.

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const results = await exa.search('Who is the CEO of OpenAI?', {
    type: 'deep',
    outputSchema: {
        type: 'object',
        properties: {
            leader: { type: 'string' },
            title: { type: 'string' },
            sourceCount: { type: 'number' }
        },
        required: ['leader', 'title']
    },
    contents: {
        text: true
    }
});

console.log(results);
```

--------------------------------

### Fetch Code Context using JavaScript/Node.js

Source: https://exa.ai/docs/reference/context

This JavaScript function utilizes the 'fetch' API to send a POST request to the Exa AI context API. It accepts a 'query' and an optional 'tokensNum' parameter to obtain code context. The function returns the 'response' from the JSON output. Remember to replace 'YOUR_API_KEY' with your valid API key.

```javascript
async function getCodeContext(query, tokensNum = "dynamic") {
  const response = await fetch("https://api.exa.ai/context", {
    method: "POST",
    headers অন্তর্ভুক্ত {
      "Content-Type": "application/json",
      "x-api-key": "YOUR_API_KEY"
    },
    body: JSON.stringify({
      query,
      tokensNum
    })
  });
  
  const result = await response.json();
  return result.response;
}

// Example usage
const context = await getCodeContext("Svelte component lifecycle methods");
console.log(context);
```

--------------------------------

### POST /search

Source: https://exa.ai/docs/reference/find-similar-links

Performs a search query with configurable crawling behavior, subpage extraction, and additional content metadata.

```APIDOC
## POST /search

### Description
Executes a search query with options to control live-crawling behavior, limit subpage retrieval, and request additional metadata like image links or specific page highlights.

### Method
POST

### Endpoint
/search

### Parameters
#### Request Body
- **livecrawl** (integer) - Optional - Controls crawling behavior: 0 (always live), -1 (always cache), Omit (fallback).
- **subpages** (integer) - Optional - The number of subpages to crawl.
- **subpageTarget** (string/array) - Optional - Term to find specific subpages of search results.
- **extras** (object) - Optional - Extra parameters including 'links' (number of URLs) and 'imageLinks' (number of images).

### Request Example
{
  "livecrawl": 0,
  "subpages": 1,
  "subpageTarget": "sources",
  "extras": {
    "links": 1,
    "imageLinks": 1
  }
}

### Response
#### Success Response (200)
- **text** (string) - The full content text of the search result.
- **highlights** (array) - Array of highlights extracted from the content.
- **highlightScores** (array) - Array of cosine similarity scores for highlights.
- **summary** (string) - Summary of the webpage.
- **subpages** (array) - Array of subpages for the search result.

#### Response Example
{
  "text": "Abstract Large Language Models (LLMs) have recently demonstrated remarkable capabilities...",
  "highlights": ["Such requirements have limited their adoption..."],
  "highlightScores": [0.4600165784358978],
  "summary": "This overview paper on Large Language Models (LLMs) highlights key developments..."
}
```

--------------------------------

### Execute Research Tasks via Responses API

Source: https://exa.ai/docs/reference/openai-sdk

Utilizes the OpenAI Responses API format for simplified, single-turn research queries. This interface is optimized for direct input-to-output research tasks.

```python
from openai import OpenAI

client = OpenAI(
    base_url="https://api.exa.ai",
    api_key="YOUR_EXA_API_KEY"
)

response = client.responses.create(
    model="exa-research",  # or "exa-research-pro"
    input="Summarize the impact of CRISPR on gene therapy with recent developments"
)

print(response.output)
```

```javascript
import OpenAI from "openai";

const openai = new OpenAI({
  baseURL: "https://api.exa.ai",
  apiKey: "YOUR_EXA_API_KEY",
});

async function main() {
  const response = await openai.responses.create({
    model: "exa-research", // or "exa-research-pro"
    input:
      "Summarize the impact of CRISPR on gene therapy with recent developments",
  });

  console.log(response.output);
}

main();
```

```bash
curl --location 'https://api.exa.ai/responses' \
--header 'x-api-key: YOUR_EXA_API_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "input": "Summarize the impact of CRISPR on gene therapy with recent developments",
    "model": "exa-research"
}'
```

--------------------------------

### Perform Search Requests with Bing and Exa

Source: https://exa.ai/docs/reference/migrating-from-bing

Comparison of search implementation patterns between the legacy Bing Search API and the Exa API across cURL, Python, and JavaScript.

```cURL
# Bing
curl -H "Ocp-Apim-Subscription-Key: YOUR_BING_KEY" \
  "https://api.bing.microsoft.com/v7.0/search?q=latest%20AI%20news&count=10"

# Exa
curl -X POST https://api.exa.ai/search \
  -H "x-api-key: YOUR_EXA_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "latest AI news",
    "numResults": 10
  }'
```

```python
# Bing
import requests

response = requests.get(
    'https://api.bing.microsoft.com/v7.0/search',
    params={'q': 'latest AI news', 'count': 10},
    headers={'Ocp-Apim-Subscription-Key': 'YOUR_BING_KEY'}
)

# Exa
from exa_py import Exa
exa = Exa('YOUR_EXA_KEY')
results = exa.search("latest AI news", num_results=10)
```

```javascript
// Bing
fetch(
  "https://api.bing.microsoft.com/v7.0/search?q=latest%20AI%20news&count=10",
  {
    headers: {
      "Ocp-Apim-Subscription-Key": "YOUR_BING_KEY",
    },
  }
);

// Exa
import Exa from "exa-js";
const exa = new Exa("YOUR_EXA_KEY");
const results = await exa.search("latest AI news", { numResults: 10 });
```

--------------------------------

### Search API Reference

Source: https://exa.ai/docs/reference/search-best-practices

This section details the parameters available for the Exa Search API, enabling users to refine their search queries for optimal results.

```APIDOC
## POST /search

### Description
Performs a search using natural language queries and returns a list of relevant webpages and their content, optimized for LLM consumption.

### Method
POST

### Endpoint
/search

### Parameters
#### Query Parameters
None

#### Request Body
- **query** (string) - Required - The search query. Supports long, semantically rich descriptions for finding niche content.
- **type** (string) - Optional - Search method: `auto` (highest quality), `fast` (low latency), `instant` (lowest latency), `deep` (deep web research with structured outputs). Defaults to `auto`.
- **numResults** (int) - Optional - Number of results to return (1-100). Defaults to 10.
- **highlights** (bool/obj) - Optional - Return token-efficient excerpts most relevant to your query. Can also request full text. Example: `{ "maxCharacters": 4000 }`.
- **maxAgeHours** (int) - Optional - Maximum age of indexed content in hours. `0` = always livecrawl, `-1` = never livecrawl (cache only).
- **category** (string) - Optional - Target specific content types: `company`, `people`, `tweet`, `news`.

### Request Example
```json
{
  "query": "blog post about embeddings and vector search",
  "type": "auto",
  "numResults": 5,
  "highlights": true,
  "maxAgeHours": 24,
  "category": "news"
}
```

### Response
#### Success Response (200)
- **results** (array) - A list of search results, each containing webpage information and content.
- **result** (object) - Contains details about a single search result, including title, url, content, and highlights.
  - **title** (string) - The title of the webpage.
  - **url** (string) - The URL of the webpage.
  - **content** (string) - The full content of the webpage (if requested).
  - **highlights** (string) - Token-efficient excerpts relevant to the query.

#### Response Example
```json
{
  "results": [
    {
      "title": "Understanding Embeddings and Vector Search",
      "url": "https://example.com/embeddings-vector-search",
      "content": "This article explains the concepts behind embeddings and vector search...",
      "highlights": "Key excerpts about embeddings and vector search..."
    }
  ]
}
```
```

--------------------------------

### Run SimpleQA Evaluation with Exa AI (Python)

Source: https://exa.ai/docs/reference/evaluating-exa-search

This Python script evaluates the SimpleQA dataset using the Exa AI search and content retrieval. It measures retrieval latency and uses external LLMs for answer synthesis and grading. The function returns accuracy, P50 latency, total queries, and the configuration used.

```python
from exa_py import Exa
import json
from datetime import datetime

exa = Exa(api_key="YOUR_API_KEY")

def evaluate_simpleqa(dataset_path, config):
    """
    Run SimpleQA evaluation with specified configuration.

    Args:
        dataset_path: Path to SimpleQA JSON file
        config: Dict with keys: type, num_results, text, livecrawl
    """
    with open(dataset_path) as f:
        questions = json.load(f)

    results = []
    latencies = []

    for item in questions:
        query = item['question']
        ground_truth = item['answer']

        # Retrieval
        start = datetime.now()
        search_result = exa.search_and_contents(
            query,
            type=config['type'],
            num_results=config['num_results'],
            text=config['text'],
            livecrawl=config['livecrawl']
        )
        latency = (datetime.now() - start).total_seconds() * 1000
        latencies.append(latency)

        # Synthesis (using your LLM)
        context = "\n\n".join([r.text for r in search_result.results])
        answer = your_llm.generate(
            f"Answer concisely using only the context.\n\n"
            f"Context: {context}\n\n"
            f"Question: {query}\n\n"
            f"Answer:"
        )

        # Grading (using your grading LLM)
        grade = grading_llm.evaluate(
            question=query,
            expected=ground_truth,
            generated=answer
        )

        results.append({
            'query': query,
            'grade': grade,
            'latency_ms': latency
        })

    # Calculate metrics
    accuracy = sum(1 for r in results if r['grade'] == 'correct') / len(results)
    p50_latency = sorted(latencies)[len(latencies) // 2]

    return {
        'accuracy': accuracy,
        'p50_latency_ms': p50_latency,
        'total_queries': len(results),
        'config': config
    }

# Run evaluation
config = {
    'type': 'auto',
    'num_results': 10,
    'text': {'max_characters': 15000}
}

results = evaluate_simpleqa('simpleqa.json', config)
print(f"Accuracy: {results['accuracy']:.2%}")
print(f"P50 Latency: {results['p50_latency_ms']:.0f}ms")
```

--------------------------------

### Perform Search with Content Extraction using Exa

Source: https://exa.ai/docs/reference/migrating-from-bing

Demonstrates Exa's capability to perform a search and return extracted text content and highlights in a single API call.

```bash
curl -X POST https://api.exa.ai/search \
  -H "x-api-key: YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "climate change research",
    "numResults": 5,
    "contents": {
      "text": true,
      "highlights": {
        "maxCharacters": 2000,
        "query": "key findings"
      }
    }
  }'
```

```python
results = exa.search_and_contents(
    "climate change research",
    num_results=5,
    text=True,
    highlights={
        "max_characters": 2000,
        "query": "key findings"
    }
)
```

```javascript
const results = await exa.searchAndContents("climate change research", {
  numResults: 5,
  text: true,
  highlights: {
    maxCharacters: 2000,
    query: "key findings",
  },
});
```

--------------------------------

### Plan Operation Event - Crawl

Source: https://exa.ai/docs/reference/research/list-tasks

Represents a 'plan-operation' event with a 'crawl' operation, detailing the goal and the URL being crawled.

```APIDOC
## POST /websites/exa_ai/events

### Description
Records a 'plan-operation' event with a 'crawl' operation, specifying the goal and the URL to be crawled.

### Method
POST

### Endpoint
/websites/exa_ai/events

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'plan-operation'.
- **planId** (string) - Required - Which plan this operation belongs to.
- **operationId** (string) - Required - Unique identifier for this specific operation.
- **data** (object) - Required - The details of the operation.
  - **type** (string) - Required - Must be 'crawl'.
  - **goal** (string) - Required - What information the AI expects to find on this page.
  - **result** (object) - Required - Information about the crawled page.
    - **url** (string) - The URL that was crawled.

### Request Example
```json
{
  "eventType": "plan-operation",
  "planId": "plan-123",
  "operationId": "op-def",
  "data": {
    "type": "crawl",
    "goal": "Extract the main findings from the research paper",
    "result": {
      "url": "http://example.com/paper1"
    }
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Plan operation event recorded successfully."
}
```
```

--------------------------------

### Apply Dynamic Prefixes and Suffixes

Source: https://exa.ai/docs/reference/exa-for-sheets

Utilizes the prefix and suffix parameters in EXA_SEARCH to automatically wrap cell-based queries with specific search modifiers or context strings.

```Google Sheets Formula
=EXA_SEARCH(A2, 5, "neural", "Find information about: ", " site:edu")
```

--------------------------------

### List Research Tasks using cURL

Source: https://exa.ai/docs/reference/research/list-tasks

This code snippet demonstrates how to list research tasks using a cURL command. It requires an API key and specifies the number of results per page.

```bash
curl -X GET 'https://api.exa.ai/research/v1?limit=10' \
  -H 'x-api-key: YOUR-EXA-API-KEY'
```

--------------------------------

### OpenAI Tool Definition for Web Search

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Defines the Exa web search tool for OpenAI's function calling. It specifies the function name, a detailed description of its capabilities and usage constraints, and the parameters it accepts, including query, numResults, category, and content retrieval options.

```json
{
  "type": "function",
  "function": {
    "name": "exa_search_auto",
    "description": "Search the web via Exa. Use natural language queries, not keywords. Default numResults=10. Categories: use 'company' only for company research, 'people' only for non-public figures, 'research paper' only for academic papers. Omit category for news, sports, general facts.",
    "parameters": {
      "type": "object",
      "properties": {
        "query": {
          "type": "string",
          "description": "Natural language search query."
        },
        "numResults": {
          "type": "integer",
          "description": "Number of results. Default: 10."
        },
        "category": {
          "type": "string",
          "enum": ["company", "people", "research paper"],
          "description": "Optional filter. Most queries should omit this."
        },
        "contents": {
          "type": "object",
          "description": "Content retrieval options. Use highlights for token-efficient excerpts.",
          "properties": {
            "highlights": {
              "type": "object",
              "properties": {
                "maxCharacters": {
                  "type": "integer",
                  "description": "Max characters per highlight. Default: 4000."
                }
              }
            }
          }
        }
      },
      "required": ["query"]
    }
  }
}
```

--------------------------------

### Plan Definition and Operations

Source: https://exa.ai/docs/reference/research/get-a-task

Defines the structure for plan definitions and the various operations an AI can perform within a plan, such as thinking, searching, and crawling.

```APIDOC
## Plan Definition and Operations

### Description
This section details the structure of a plan definition, including its required fields and the possible operations an AI can execute. Operations include 'think' for reasoning, 'search' for information retrieval, and 'crawl' for page content extraction.

### Method
N/A (This describes a data structure, not an endpoint)

### Endpoint
N/A

### Parameters
#### Request Body (Plan Definition)
- **eventType** (string) - Required - Must be 'plan-operation'.
- **planId** (string) - Required - The ID of the plan this operation belongs to.
- **operationId** (string) - Required - A unique identifier for this specific operation.
- **data** (object) - Required - Contains the details of the AI's operation. The structure of 'data' depends on the 'type' field within it.

##### Data Object Types:
- **Think Operation**
  - **type** (string) - Required - Must be 'think'.
  - **content** (string) - Required - The AI's reasoning process and decision-making steps.

- **Search Operation**
  - **type** (string) - Required - Must be 'search'.
  - **searchType** (string) - Required - The search algorithm used ('neural', 'auto', 'fast').
  - **goal** (string) - Required - What the AI is trying to find with this search.
  - **query** (string) - Required - The exact search query sent to the search engine.
  - **results** (array) - Required - A list of search results, each containing at least a 'url'.
    - **url** (string) - Required - The URL of the search result.
  - **pageTokens** (number) - Required - Token cost for processing search result snippets.

- **Crawl Operation**
  - **type** (string) - Required - Must be 'crawl'.
  - **goal** (string) - Required - What information the AI expects to find on this page.
  - **result** (object) - Required - Details of the crawled page.
    - **url** (string) - Required - The specific page that was crawled.
  - **pageTokens** (number) - Required - Token cost for processing the full page content.

### Request Example
```json
{
  "eventType": "plan-operation",
  "planId": "plan_abc123",
  "operationId": "op_xyz789",
  "data": {
    "type": "search",
    "searchType": "neural",
    "goal": "Find the latest research papers on AI ethics",
    "query": "AI ethics research papers 2023",
    "results": [
      { "url": "http://example.com/paper1" },
      { "url": "http://example.com/paper2" }
    ],
    "pageTokens": 500
  }
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

### POST /research/v1

Source: https://exa.ai/docs/reference/research/create-a-task

Create a new asynchronous research task. This endpoint allows you to submit research instructions, specify a model, and optionally provide a JSON schema for structured output. The API will explore the web, gather sources, synthesize findings, and return structured results with citations.

```APIDOC
## POST /research/v1

### Description
Create a new research request. This endpoint allows for asynchronous research tasks that explore the web, gather sources, synthesize findings, and return structured results with citations.

### Method
POST

### Endpoint
/research/v1

### Parameters
#### Request Body
- **model** (string) - Optional - Research model to use. Options include `exa-research-fast`, `exa-research`, and `exa-research-pro`. `exa-research` is faster and cheaper, while `exa-research-pro` provides more thorough analysis and stronger reasoning. Defaults to `exa-research`.
- **instructions** (string) - Required - Instructions for what you would like research on. A good prompt clearly defines what information you want to find, how research should be conducted, and what the output should look like. Maximum length is 4096 characters.
- **outputSchema** (object) - Optional - JSON Schema to enforce structured output. When provided, the research output will be validated against this schema and returned as parsed JSON.

### Request Example
```json
{
  "instructions": "Summarize the latest developments in AI safety research",
  "model": "exa-research"
}
```

### Response
#### Success Response (201)
- **researchId** (string) - Unique identifier for tracking and retrieving this research request.
- **createdAt** (number) - When the research was created (Unix timestamp in milliseconds).
- **model** (string) - The model used for this research request.
- **instructions** (string) - The original research instructions provided.
- **outputSchema** (object) - The JSON Schema used to validate the output, if provided.
- **status** (string) - The current status of the research task (e.g., `pending`).

#### Response Example
```json
{
  "researchId": "res_abcdef123456",
  "createdAt": 1678886400000,
  "model": "exa-research",
  "instructions": "Summarize the latest developments in AI safety research",
  "status": "pending"
}
```
```

--------------------------------

### POST /search

Source: https://exa.ai/docs/reference/search

The search endpoint enables users to query the web and extract relevant content based on search criteria.

```APIDOC
## POST /search

### Description
Performs a search across the web and returns extracted content from the matching results.

### Method
POST

### Endpoint
/search

### Parameters
#### Request Body
- **query** (string) - Required - The search query string.
- **numResults** (integer) - Optional - Number of search results to return.
- **type** (string) - Optional - The type of search (e.g., 'neural', 'keyword').

### Request Example
{
  "query": "latest advancements in artificial intelligence",
  "numResults": 5
}

### Response
#### Success Response (200)
- **results** (array) - A list of search result objects containing title, url, and extracted content.

#### Response Example
{
  "results": [
    {
      "title": "AI Trends 2024",
      "url": "https://example.com/ai-trends",
      "content": "Extracted text from the page..."
    }
  ]
}
```

--------------------------------

### Fetch Code Context using Python

Source: https://exa.ai/docs/reference/context

This Python function uses the 'requests' library to make a POST request to the Exa AI context API. It sends a query and an optional 'tokensNum' parameter to retrieve relevant code context. The function returns the 'response' field from the JSON result. Ensure you replace 'YOUR_API_KEY' with your actual API key.

```python
import requests

def get_code_context(query, tokens="dynamic"):
    response = requests.post(
        "https://api.exa.ai/context",
        headers={
            "Content-Type": "application/json",
            "x-api-key": "YOUR_API_KEY"
        },
        json={
            "query": query,
            "tokensNum": tokens
        }
    )
    
    result = response.json()
    return result["response"]

# Example usage
context = get_code_context("Express.js middleware for authentication")
print(context)
```

--------------------------------

### Fast-Baseline Configuration for Latency-Sensitive Evaluations

Source: https://exa.ai/docs/reference/evaluating-exa-search

This configuration is optimized for speed and is suitable for latency-sensitive evaluations. It uses the 'auto' search type and retrieves a fixed number of results with a specified character limit for the text content. Available in Python, JavaScript, and cURL.

```python
result = exa.search_and_contents(
    query,
    type="auto",
    num_results=10,
    text={"max_characters": 15000}
)
```

```javascript
const result = await exa.searchAndContents(query, {
    type: "auto",
    numResults: 10,
    text: {maxCharacters: 15000}
});
```

```curl
curl -X POST https://api.exa.ai/search \
  -H "x-api-key: YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "your query here",
    "type": "auto",
    "num_results": 10,
    "contents": {"text": {"max_characters": 15000}}
  }'
```

--------------------------------

### Define Deep Search Output Schemas

Source: https://exa.ai/docs/reference/search-best-practices

Configures the output format for deep search variants using outputSchema. Supports both plain text responses and structured JSON objects with defined properties.

```json
{
  "query": "what's the fastest web search api",
  "type": "deep",
  "outputSchema": {
    "type": "text",
    "description": "Short one to two sentence answer"
  }
}
```

```json
{
  "query": "top aerospace companies",
  "type": "deep",
  "outputSchema": {
    "type": "object",
    "required": ["companies"],
    "properties": {
      "companies": {
        "type": "array",
        "description": "A list of aerospace companies",
        "items": {
          "type": "object",
          "required": ["company_name", "ceo_name", "stock_price"],
          "properties": {
            "company_name": { "type": "string", "description": "The name of the aerospace company" },
            "ceo_name": { "type": "string", "description": "The name of the company's CEO" },
            "stock_price": { "type": "number", "description": "Current stock price of the company" }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Execute Automated Subpage Crawling

Source: https://exa.ai/docs/reference/contents-best-practices

Configures the API to discover and extract content from linked subpages, using target keywords to prioritize relevant sections of a website.

```json
{
  "ids": ["https://docs.example.com"],
  "subpages": 10,
  "subpageTarget": ["api", "reference", "guide"],
  "highlights": {
    "maxCharacters": 4000
  }
}
```

```json
{
  "ids": ["https://platform.openai.com/docs"],
  "subpages": 15,
  "subpageTarget": ["api", "models", "embeddings"],
  "maxAgeHours": 24,
  "livecrawlTimeout": 15000,
  "text": { "maxCharacters": 5000 }
}
```

```json
{
  "ids": ["https://stripe.com"],
  "subpages": 8,
  "subpageTarget": ["about", "careers", "press", "blog"],
  "summary": { "query": "Company overview, culture, and recent news" }
}
```

--------------------------------

### Define Personal Site Search Skill

Source: https://exa.ai/docs/reference/personal-site-search-claude-skill

Configuration block for the Claude skill, defining the tool name, description, and context requirements for searching personal web content.

```yaml
name: web-search-advanced-personal-site
description: Search personal websites and blogs using Exa advanced search. Full filter support for finding individual perspectives, portfolios, and personal blogs. Use when searching for personal sites, blog posts, or portfolio websites.
context: fork
```

--------------------------------

### Display US Stock Market News Highlights

Source: https://exa.ai/docs/reference/llamaindex

This snippet displays a formatted summary of US stock market news. It includes key financial data points and market trends. The output is a string containing the summarized news.

```text
Here are some highlights related to the US stock market news from the last month:

1. Companies have repurchased more than $383 billion in shares over the past 13 weeks, marking a 30% increase from the same period last year. This is the highest level since June 2018. The Dow rose 75 points, the S&P 500 dipped 0.1%, and the Nasdaq dropped 0.2%. AMC Entertainment and Robinhood will release their quarterly reports after markets close.

2. A California-based company reported a net loss of $270.6 million, or 43 cents per share, for the current period. Revenue increased by 22.3% to $801.3 million, falling short of expectations. Bookings rose by 19% to $923.8 million, just missing expectations.

3. The Dow and other indexes opened higher as the latest jobs report suggests the Federal Reserve may lower interest rates this year. Weekly jobless claims have risen to 231,000, the highest level since August, raising hopes among investors for a potential interest rate reduction.

4. Following the news, a stock declined 9.5% in mid-morning trading. Bitcoin price surged to $64,000 amid the resurgence of Grayscale’s Bitcoin ETF seeing inflows after daily outflows for almost four months.

5. Debt due in 2025 is trading at 73 cents on the dollar, and 2026 debt is at 55 cents. Following the news, a stock declined 9.7% by the end of the day. Spirit Airlines’ rivals, including American Airlines, Southwest Airlines, and United Airlines, saw their stocks soar. Paramount Global's shares went up 3% amid acquisition discussions.

These are some of the key highlights from the US stock market news in the last month.
```

--------------------------------

### Build Complex Queries with Cell References

Source: https://exa.ai/docs/reference/exa-for-sheets

Demonstrates how to combine multiple cell references using the ampersand operator or CONCAT function to construct dynamic search queries for the EXA_SEARCH function.

```Google Sheets Formula
=EXA_SEARCH(A2 & " " & B2 & " in " & C2, 10, "neural")
```

```Google Sheets Formula
=EXA_SEARCH(CONCAT("research papers about ", A2, " published after ", B2), 5)
```

--------------------------------

### Extract Query-Relevant Highlights via Exa API

Source: https://exa.ai/docs/reference/contents-best-practices

Demonstrates how to retrieve extractive highlights from a URL based on a specific query. This is useful for focusing on relevant sections of a document.

```json
{
  "ids": ["https://example.com/research-paper"],
  "highlights": {
    "query": "methodology and results",
    "maxCharacters": 2000
  }
}
```

--------------------------------

### Run SimpleQA Evaluation with Exa AI (JavaScript)

Source: https://exa.ai/docs/reference/evaluating-exa-search

This JavaScript script evaluates the SimpleQA dataset using the Exa AI search and content retrieval. It measures retrieval latency and uses external LLMs for answer synthesis and grading. The function returns accuracy, P50 latency, total queries, and the configuration used. It requires Node.js and the 'exa-js' package.

```javascript
import Exa from 'exa-js';
import fs from 'fs/promises';

const exa = new Exa("YOUR_API_KEY");

async function evaluateSimpleQA(datasetPath, config) {
    const data = JSON.parse(await fs.readFile(datasetPath, 'utf8'));

    const results = [];
    const latencies = [];

    for (const item of data) {
        const { question, answer: groundTruth } = item;

        // Retrieval
        const start = Date.now();
        const searchResult = await exa.searchAndContents(question, {
            type: config.type,
            numResults: config.numResults,
            text: config.text,
            livecrawl: config.livecrawl
        });
        const latency = Date.now() - start;
        latencies.push(latency);

        // Synthesis
        const context = searchResult.results
            .map(r => r.text)
            .join('\n\n');
        const answer = await yourLLM.generate(
            `Answer concisely using only the context.\n\n` +
            `Context: ${context}\n\n` +
            `Question: ${question}\n\n` +
            `Answer:`
        );

        // Grading
        const grade = await gradingLLM.evaluate({
            question,
            expected: groundTruth,
            generated: answer
        });

        results.push({ question, grade, latency });
    }

    // Calculate metrics
    const accuracy = results.filter(r => r.grade === 'correct').length / results.length;
    const p50Latency = latencies.sort((a, b) => a - b)[Math.floor(latencies.length / 2)];

    return { accuracy, p50Latency, totalQueries: results.length, config };
}

// Run evaluation
const config = {
    type: 'auto',
    numResults: 10,
    text: {maxCharacters: 15000}
};

const results = await evaluateSimpleQA('simpleqa.json', config);
console.log(`Accuracy: ${(results.accuracy * 100).toFixed(1)}%`);
console.log(`P50 Latency: ${results.p50Latency}ms`);
```

--------------------------------

### Anthropic Tool Definition for Web Search

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Defines the Exa web search tool for Anthropic's Claude models. It outlines the tool's name, description, and input schema, detailing the parameters for search queries, result counts, category filtering, and content retrieval options like highlights.

```json
{
  "name": "exa_search_auto",
  "description": "Search the web via Exa. Use natural language queries, not keywords. Default numResults=10. Categories: use 'company' only for company research, 'people' only for non-public figures, 'research paper' only for academic papers. Omit category for news, sports, general facts.",
  "input_schema": {
    "type": "object",
    "properties": {
      "query": {
        "type": "string",
        "description": "Natural language search query."
      },
      "numResults": {
        "type": "integer",
        "description": "Number of results. Default: 10."
      },
      "category": {
        "type": "string",
        "enum": ["company", "people", "research paper"],
        "description": "Optional filter. Most queries should omit this."
      },
      "contents": {
        "type": "object",
        "description": "Content retrieval options. Use highlights for token-efficient excerpts.",
        "properties": {
          "highlights": {
            "type": "object",
            "properties": {
              "maxCharacters": {
                "type": "integer",
                "description": "Max characters per highlight. Default: 4000."
              }
            }
          }
        }
      }
    },
    "required": ["query"]
  }
}
```

--------------------------------

### Define Exa Web Search Tool Schema

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

JSON representation of the tool definition required for OpenAI to recognize and invoke the Exa web search function.

```json
{
  "type": "function",
  "name": "exa_websearch",
  "description": "Search the web using Exa...",
  "parameters": {
    "query": "string"
  }
}
```

--------------------------------

### Dynamic Query with Concatenation

Source: https://exa.ai/docs/reference/exa-for-sheets

Demonstrates how to build dynamic search queries in Google Sheets by concatenating text strings with cell references using the '&' operator. This allows search queries to be constructed based on values in other cells.

```google-sheets
=EXA_SEARCH("latest news about " & A2, 5)
```

--------------------------------

### Main Execution Loop for Conversational Agent

Source: https://exa.ai/docs/reference/anthropic-tool-calling

The primary loop that manages user input, interacts with the Claude API, handles tool execution, and renders formatted responses using the Rich library.

```python
def main():
    messages = []
    while True:
        try:
            user_query = Prompt.ask(
                "[bold yellow]What do you want to search for?[/bold yellow]",
            )
            messages.append({"role": "user", "content": user_query})
            completion = claude.messages.create(
                model="claude-sonnet-4-6",
                max_tokens=1024,
                system=SYSTEM_MESSAGE,
                messages=messages,
                tools=TOOLS,
            )
            message = completion.content[0]
            tool_calls = [content for content in completion.content if content.type == "tool_use"]
            if tool_calls:
                search_results = process_tool_calls(tool_calls)
                messages.append({"role": "assistant", "content": f"I've performed a search and found the following results: {search_results}"})
                messages.append({"role": "user", "content": "Please summarise this information and answer my previous query based on these results."})
                completion = claude.messages.create(
                    model="claude-sonnet-4-6",
                    max_tokens=1024,
                    system=SYSTEM_MESSAGE,
                    messages=messages,
                )
                response = completion.content[0].text
                console.print(Markdown(response))
                messages.append({"role": "assistant", "content": response})
            else:
                console.print(Markdown(message.text))
                messages.append({"role": "assistant", "content": message.text})
        except Exception as e:
            console.print(f"[bold red]An error occurred:[/bold red] {str(e)}")
if __name__ == "__main__":
    main()
```

--------------------------------

### Website Crawling and Content Retrieval Parameters

Source: https://exa.ai/docs/reference/search

This section details the various parameters that can be used to control website crawling behavior and the type of content retrieved.

```APIDOC
## Website Crawling and Content Retrieval Parameters

### Description
This section details the various parameters that can be used to control website crawling behavior and the type of content retrieved.

### Method
GET (Assumed for retrieval operations)

### Endpoint
/websites/exa_ai (Assumed base endpoint)

### Parameters
#### Query Parameters
- **cacheHours** (integer) - Optional - Controls the caching behavior. Positive values (e.g., 24) use cached content if it's younger than the specified hours, otherwise live crawl. A value of 0 forces a live crawl, and -1 always uses the cache. Omitting this parameter defaults to live crawl only when no cached content exists.
- **subpages** (integer) - Optional - The number of subpages to crawl. The actual number crawled may be limited by system constraints. Defaults to 0.
- **subpageTarget** (string or array of strings) - Optional - A term to find specific subpages of search results. Can be a single string or an array of strings.
- **extras** (object) - Optional - Extra parameters to pass.
  - **links** (integer) - Optional - Number of URLs to return from each webpage. Defaults to 0.
  - **imageLinks** (integer) - Optional - Number of images to return for each result. Defaults to 0.
- **context** (boolean or object) - Deprecated - Use `highlights` or `text` instead. Returns page contents as a combined context string.
  - **maxCharacters** (integer) - Deprecated - Maximum character limit for the context string.

### Request Example
```json
{
  "cacheHours": 24,
  "subpages": 1,
  "subpageTarget": "sources",
  "extras": {
    "links": 1,
    "imageLinks": 1
  }
}
```

### Response
#### Success Response (200)
- **ResultWithContent** (object) - Contains the search result with content details.
  - **text** (string) - The full content text of the search result.
  - **highlights** (array of strings) - Array of highlights extracted from the search result content.
  - **highlightScores** (array of floats) - Array of cosine similarity scores for each highlight.
  - **summary** (string) - Summary of the webpage.
  - **subpages** (array of ResultWithContent) - Array of subpages for the search result.

#### Response Example
```json
{
  "text": "Abstract Large Language Models (LLMs) have recently demonstrated remarkable capabilities...",
  "highlights": [
    "Such requirements have limited their adoption..."
  ],
  "highlightScores": [
    0.4600165784358978
  ],
  "summary": "This overview paper on Large Language Models (LLMs) highlights key developments...",
  "subpages": [
    {
      "id": "https://arxiv.org/abs/2303.17580",
      "url": "https://arxiv.org/pdf/2303.17580.pdf",
      "title": "HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face",
      "author": "Yongliang Shen, Microsoft Research Asia, Kaitao Song, Microsoft Research Asia, Xu Tan, Microsoft Research Asia, Dongsheng Li, Microsoft Research Asia, Weiming Lu, Microsoft Research Asia, Yueting Zhuang, Microsoft Research Asia, yzhuang@zju.edu.cn, Zhejiang University, Microsoft Research Asia, Microsoft Research, Microsoft Research Asia",
      "publishedDate": "2023-11-16T01:36:20.486Z",
      "text": "HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face Date Published: 2023-05-25 Authors: Yongliang Shen, Microsoft Research Asia Kaitao Song, Microsoft Research Asia Xu Tan, Microsoft Research Asia Dongsheng Li, Microsoft Research Asia Weiming Lu, Microsoft Research Asia Yueting Zhuang, Microsoft Research Asia, yzhuang@zju.edu.cn Zhejiang University, Microsoft Research Asia Microsoft Research, Microsoft Research Asia Abstract Solving"
    }
  ]
}
```
```

--------------------------------

### Deep-Comprehensive Configuration for Agentic and Research Evaluations

Source: https://exa.ai/docs/reference/evaluating-exa-search

This configuration is designed for complex agentic and research evaluations, utilizing the 'deep' search type. It supports additional query variations, full text retrieval, and a fallback live crawl mechanism. Available in Python and JavaScript.

```python
result = exa.search_and_contents(
    query,
    type="deep",
    additional_queries=[variation1, variation2],
    num_results=10,
    text=True,
    livecrawl="fallback"
)
```

```javascript
const result = await exa.searchAndContents(query, {
    type: "deep",
    additionalQueries: [variation1, variation2],
    numResults: 10,
    text: true,
    livecrawl: "fallback"
});
```

--------------------------------

### Plan Operation Event - Search

Source: https://exa.ai/docs/reference/research/list-tasks

Represents a 'plan-operation' event with a 'search' operation, including search parameters and results.

```APIDOC
## POST /websites/exa_ai/events

### Description
Records a 'plan-operation' event with a 'search' operation, detailing the search query, algorithm, and results.

### Method
POST

### Endpoint
/websites/exa_ai/events

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'plan-operation'.
- **planId** (string) - Required - Which plan this operation belongs to.
- **operationId** (string) - Required - Unique identifier for this specific operation.
- **data** (object) - Required - The details of the operation.
  - **type** (string) - Required - Must be 'search'.
  - **searchType** (string) - Required - Search algorithm used (e.g., 'neural', 'auto', 'fast').
  - **goal** (string) - Required - What the AI is trying to find with this search.
  - **query** (string) - Required - The exact search query sent to the search engine.
  - **results** (array) - Required - URLs returned by the search, ranked by relevance.
    - **url** (string) - URL of the search result.
  - **pageTokens** (number) - Required - Token cost for processing search result snippets.

### Request Example
```json
{
  "eventType": "plan-operation",
  "planId": "plan-123",
  "operationId": "op-abc",
  "data": {
    "type": "search",
    "searchType": "neural",
    "goal": "Find recent research papers on AI ethics",
    "query": "AI ethics recent papers",
    "results": [
      {"url": "http://example.com/paper1"},
      {"url": "http://example.com/paper2"}
    ],
    "pageTokens": 50
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Plan operation event recorded successfully."
}
```
```

--------------------------------

### POST /search

Source: https://exa.ai/docs/reference/migrating-from-bing

Performs a search query using the Exa search engine to retrieve relevant web results.

```APIDOC
## POST /search

### Description
Executes a search query to retrieve web results based on the provided criteria.

### Method
POST

### Endpoint
https://api.exa.ai/search

### Parameters
#### Request Body
- **query** (string) - Required - The search query string.
- **numResults** (integer) - Optional - Number of results to return (Default: 10, Max: 100).
- **userLocation** (string) - Optional - 2-letter ISO country code for localization.
- **startPublishedDate** (string) - Optional - ISO 8601 start date for filtering.
- **endPublishedDate** (string) - Optional - ISO 8601 end date for filtering.
- **includeDomains** (array) - Optional - List of domains to include.
- **excludeDomains** (array) - Optional - List of domains to exclude.
- **moderation** (boolean) - Optional - Enable safe search (Default: false).

### Request Example
{
  "query": "latest AI news",
  "numResults": 10
}

### Response
#### Success Response (200)
- **results** (array) - List of search result objects.
- **requestId** (string) - Unique identifier for the request.

#### Response Example
{
  "results": [
    {
      "title": "Page Title",
      "url": "https://example.com",
      "publishedDate": "2025-08-11",
      "author": "Author Name",
      "text": "Full content when requested...",
      "highlights": ["Key sentences..."]
    }
  ],
  "requestId": "unique-id"
}
```

--------------------------------

### Configure Deep Search in Python

Source: https://exa.ai/docs/reference/evaluating-exa-search

Deep search is designed for complex, multi-hop research tasks with a median latency of 5000ms. It supports automatic or manual query expansion to ensure comprehensive coverage.

```python
result = exa.search_and_contents(
    "impact of quantum computing on cryptography",
    type="deep",
    additional_queries=[
        "quantum threats to encryption",
        "post-quantum cryptography research"
    ],
    num_results=10,
    text=True
)
```

--------------------------------

### Process Tool Calls for Exa Search

Source: https://exa.ai/docs/reference/openai-tool-calling

This function processes tool calls, specifically handling the 'exa_search' function. It extracts search arguments, executes the search, and updates the message history with the search results. Dependencies include the 'exa_py' library and 'json'.

```python
function_name = tool_call.function.name
function_args = json.loads(tool_call.function.arguments)
if function_name == "exa_search":
    search_results = exa_search(**function_args)
    messages.append(
        {
            "role": "tool",
            "content": str(search_results),
            "tool_call_id": tool_call.id,
        }
    )
    console.print(
        f"[bold cyan]Context updated[/bold cyan] [i]with[/i] "
        f"[bold green]exa_search ({function_args.get('mode')})[/bold green]": ",
        function_args.get("query"),
    )
return messages
```

--------------------------------

### Task Definition Object

Source: https://exa.ai/docs/reference/research/list-tasks

Defines the structure of a task, including its event type, associated plan and task IDs, creation timestamp, and the specific operation performed.

```APIDOC
## Task Definition Object

### Description
Represents a task within the Exa AI system. It includes metadata like event type, plan ID, task ID, and creation timestamp, along with the details of the operation performed.

### Method
N/A (This describes a data structure, not an endpoint)

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **eventType** (string) - Required - The type of event associated with the task (e.g., 'task-operation').
- **planId** (string) - Required - The identifier of the plan that owns this task.
- **taskId** (string) - Required - The identifier of the task performing this operation.
- **instructions** (string) - Optional - Instructions related to the task.
- **createdAt** (number) - Required - Timestamp indicating when the task was created.
- **researchId** (string) - Optional - Identifier for the research associated with the task.
- **data** (object) - Required - Contains the details of the operation performed. This is a polymorphic field determined by the 'type' property within 'data'.

### Request Example
```json
{
  "eventType": "task-operation",
  "planId": "plan_abc123",
  "taskId": "task_xyz789",
  "instructions": "Summarize the key findings from the search results.",
  "createdAt": 1678886400,
  "researchId": "research_def456",
  "data": {
    "type": "search",
    "searchType": "neural",
    "goal": "Find recent studies on AI ethics",
    "query": "AI ethics recent studies",
    "results": [
      {
        "url": "https://example.com/study1"
      },
      {
        "url": "https://example.com/study2"
      }
    ],
    "pageTokens": 50
  }
}
```

### Response
#### Success Response (200)
This structure describes the expected format of a task definition.

#### Response Example
```json
{
  "eventType": "task-operation",
  "planId": "plan_abc123",
  "taskId": "task_xyz789",
  "instructions": "Summarize the key findings from the search results.",
  "createdAt": 1678886400,
  "researchId": "research_def456",
  "data": {
    "type": "search",
    "searchType": "neural",
    "goal": "Find recent studies on AI ethics",
    "query": "AI ethics recent studies",
    "results": [
      {
        "url": "https://example.com/study1"
      },
      {
        "url": "https://example.com/study2"
      }
    ],
    "pageTokens": 50
  }
}
```
```

--------------------------------

### Content Freshness and Crawling Control

Source: https://exa.ai/docs/reference/search

Control how and when the API fetches fresh content from websites, including timeouts and cache freshness.

```APIDOC
## GET /websites/exa_ai

### Description
Controls content freshness and livecrawling behavior for website content retrieval.

### Method
GET

### Endpoint
/websites/exa_ai

### Parameters
#### Query Parameters
- **livecrawl** (string) - Deprecated. Use `maxAgeHours` instead. Options: 'never', 'fallback', 'preferred', 'always'.
- **livecrawlTimeout** (integer) - Optional - The timeout for livecrawling in milliseconds. Default: 10000. Example: 1000
- **maxAgeHours** (integer) - Optional - Maximum age of cached content in hours. Controls when livecrawling is triggered based on content freshness. Example: 24

### Response
#### Success Response (200)
- **content** (string) - The retrieved website content.

#### Response Example
```json
{
  "content": "<html><body>Website content here...</body></html>"
}
```
```

--------------------------------

### Task Definition Event

Source: https://exa.ai/docs/reference/research/list-tasks

Defines a specific task generated by a plan for execution.

```APIDOC
## POST /events/task-definition

### Description
Registers a new task definition generated by a research plan.

### Method
POST

### Endpoint
/events/task-definition

### Request Body
- **eventType** (string) - Required - Must be 'task-definition'
- **planId** (string) - Required - The plan that generated this task
- **taskId** (string) - Required - Unique identifier for the task
- **instructions** (string) - Required - Description of task goals
- **createdAt** (number) - Required - Unix timestamp in milliseconds
- **researchId** (string) - Required - The associated research request ID

### Request Example
{
  "eventType": "task-definition",
  "planId": "plan-123",
  "taskId": "task-001",
  "instructions": "Analyze the provided data",
  "createdAt": 1672531200000,
  "researchId": "res-789"
}
```

--------------------------------

### Perform Domain-Specific Search with Bing and Exa

Source: https://exa.ai/docs/reference/migrating-from-bing

Shows how to restrict search results to specific domains or websites. Useful for academic or source-verified information retrieval.

```bash
curl -H "Ocp-Apim-Subscription-Key: YOUR_KEY" \
  "https://api.bing.microsoft.com/v7.0/search?q=site:arxiv.org+transformers"
```

```python
import requests

response = requests.get(
    'https://api.bing.microsoft.com/v7.0/search',
    params={'q': 'site:arxiv.org transformers'},
    headers={'Ocp-Apim-Subscription-Key': 'YOUR_KEY'}
)
```

```javascript
fetch(
  "https://api.bing.microsoft.com/v7.0/search?q=site:arxiv.org+transformers",
  {
    headers: {
      "Ocp-Apim-Subscription-Key": "YOUR_KEY",
    },
  }
);
```

```bash
curl -X POST https://api.exa.ai/search \
  -H "x-api-key: YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "transformers",
    "includeDomains": ["arxiv.org"],
    "type": "auto"
  }'
```

```python
results = exa.search(
    "transformers",
    include_domains=["arxiv.org"],
    type="auto"
)
```

```javascript
const results = await exa.search("transformers", {
  includeDomains: ["arxiv.org"],
  type: "auto",
});
```

--------------------------------

### POST /search/contents

Source: https://exa.ai/docs/reference/search

Configures search result filtering and defines how webpage content should be extracted and returned.

```APIDOC
## POST /search/contents

### Description
This endpoint allows users to filter search results based on publication dates and specific text inclusion/exclusion criteria. It also provides advanced options for content extraction, such as character limits and semantic section filtering.

### Method
POST

### Endpoint
/search/contents

### Parameters
#### Request Body
- **publishedAfter** (date-time) - Optional - Only links with a published date after this will be returned (ISO 8601).
- **includeText** (array) - Optional - List of strings that must be present in webpage text.
- **excludeText** (array) - Optional - List of strings that must not be present in webpage text.
- **moderation** (boolean) - Optional - Enable content moderation to filter unsafe content.
- **contents** (object) - Optional - Configuration for text retrieval:
  - **text** (boolean/object) - Advanced options for text extraction (maxCharacters, includeHtmlTags, verbosity, includeSections, excludeSections).

### Request Example
{
  "publishedAfter": "2023-12-31T00:00:00.000Z",
  "includeText": ["large language model"],
  "excludeText": ["course"],
  "moderation": true,
  "contents": {
    "text": {
      "maxCharacters": 1000,
      "verbosity": "standard",
      "includeSections": ["body", "header"]
    }
  }
}

### Response
#### Success Response (200)
- **results** (array) - List of retrieved webpage content based on the provided filters.

#### Response Example
{
  "results": [
    {
      "url": "https://example.com",
      "text": "Extracted webpage content..."
    }
  ]
}
```

--------------------------------

### Add Exa API Key to Exa MCP

Source: https://exa.ai/docs/reference/exa-mcp

This URL demonstrates how to add your Exa API key to the Exa MCP configuration. Providing your own API key is recommended to bypass free plan rate limits and ensure uninterrupted service.

```url
https://mcp.exa.ai/mcp?exaApiKey=YOUR_EXA_KEY
```

--------------------------------

### Exa Advanced Web Search: With Query Variations

Source: https://exa.ai/docs/reference/people-search-claude-skill

Demonstrates using `web_search_advanced_exa` with multiple query variations to improve search coverage. Includes specifying the category, number of results, and search type.

```json
{
  "query": "machine learning engineer San Francisco",
  "category": "people",
  "additionalQueries": ["ML engineer SF", "AI engineer Bay Area"],
  "numResults": 25,
  "type": "deep"
}
```

--------------------------------

### Execute the crew

Source: https://exa.ai/docs/reference/crewai

Triggers the crew process with a specific input topic and prints the resulting newsletter.

```Python
response = crew.kickoff(inputs={'topic': 'Latest AI research'})

print(response)
```

--------------------------------

### Fresh Content Search API

Source: https://exa.ai/docs/reference/migrating-from-bing

This endpoint allows you to search for fresh content within a specified timeframe. It supports filtering by freshness.

```APIDOC
## POST /search

### Description
Searches for content with a focus on freshness. You can specify a start date to retrieve results published after a certain point.

### Method
POST

### Endpoint
https://api.exa.ai/search

### Parameters
#### Request Body
- **query** (string) - Required - The search query.
- **startPublishedDate** (string) - Optional - The start date for published content in ISO 8601 format (e.g., "2025-08-04T00:00:00Z").
- **type** (string) - Optional - The search type, defaults to "auto".

### Request Example
```json
{
  "query": "AI news",
  "startPublishedDate": "2025-08-04T00:00:00Z",
  "type": "auto"
}
```

### Response
#### Success Response (200)
- **results** (array) - A list of search results.

#### Response Example
```json
{
  "results": [
    {
      "title": "Example AI News Title",
      "url": "http://example.com/ai-news",
      "publishedDate": "2025-08-03T10:00:00Z"
    }
  ]
}
```
```

--------------------------------

### Plan Output Event

Source: https://exa.ai/docs/reference/research/get-a-task

Represents the decision output from a plan, either generating new tasks or stopping the research.

```APIDOC
## POST /events/plan-output

### Description
Records the decision made by the AI plan, which can be to continue with tasks or to stop researching.

### Method
POST

### Endpoint
/events/plan-output

### Request Body
- **eventType** (string) - Required - Must be 'plan-output'
- **planId** (string) - Required - The plan ID
- **output** (object) - Required - The decision object (Tasks or Stop)
- **createdAt** (number) - Required - Unix timestamp in milliseconds
- **researchId** (string) - Required - The research request ID

### Request Example
{
  "eventType": "plan-output",
  "planId": "plan-123",
  "output": {
    "outputType": "tasks",
    "reasoning": "Need more data on X",
    "tasksInstructions": ["Search for X", "Summarize Y"]
  },
  "createdAt": 1715678901234,
  "researchId": "res-789"
}
```

--------------------------------

### POST /search (Deep Search)

Source: https://exa.ai/docs/reference/search

Performs a deep search to find relevant information based on the query. It allows for specifying an output schema to structure the results.

```APIDOC
## POST /search (Deep Search)

### Description
Performs a deep search to find relevant information based on the query. It allows for specifying an output schema to structure the results.

### Method
POST

### Endpoint
/search

### Parameters
#### Query Parameters
- **query** (string) - Required - The search query.
- **type** (string) - Optional - The search type. Defaults to 'neural'. Can be 'deep' or 'deep-reasoning'.
- **outputSchema** (object) - Optional - A JSON schema to define the structure of the output.
- **contents** (object) - Optional - Specifies the content to retrieve. `text: True` retrieves the text content.

### Request Example
```json
{
  "query": "Who is the CEO of OpenAI?",
  "type": "deep",
  "outputSchema": {
    "type": "object",
    "properties": {
      "leader": {"type": "string"},
      "title": {"type": "string"},
      "sourceCount": {"type": "number"}
    },
    "required": ["leader", "title"]
  },
  "contents": {
    "text": true
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - An array of search results, structured according to the `outputSchema` if provided.

#### Response Example
```json
{
  "results": [
    {
      "leader": "Sam Altman",
      "title": "CEO of OpenAI",
      "sourceCount": 5
    }
  ]
}
```
```

--------------------------------

### Deep Search API

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Performs deep web research, including searching, page reading, and synthesizing findings with citations. It supports structured JSON output via `outputSchema` and offers two variants: `deep` for general queries and `deep-reasoning` for more complex tasks requiring higher effort.

```APIDOC
## POST /search

### Description
Performs deep web research, including searching, page reading, and synthesizing findings with citations. Supports structured JSON output via `outputSchema`.

### Method
POST

### Endpoint
/search

### Parameters
#### Query Parameters
- **type** (string) - Optional - Specifies the search variant: 'deep' (default, 4-12s) or 'deep-reasoning' (12-50s) for complex tasks.
- **numResults** (integer) - Optional - Number of results to retrieve. Default: 10.

#### Request Body
- **query** (string) - Required - The research question to investigate.
- **outputSchema** (object) - Optional - JSON Schema for structured output. Supports 'text' or 'object' type. Max depth: 2, max properties: 10.
- **contents** (object) - Optional - Content retrieval options.
  - **text** (object) - Optional - Text content options.
    - **maxCharacters** (integer) - Optional - Maximum characters of full text. Default: 15000.

### Request Example
```json
{
  "query": "What are the latest advancements in renewable energy technology?",
  "type": "deep",
  "outputSchema": {
    "type": "object",
    "properties": {
      "advancements": {
        "type": "array",
        "items": {
          "type": "object",
          "properties": {
            "technology": {"type": "string"},
            "description": {"type": "string"},
            "citations": {"type": "array", "items": {"type": "string"}}
          }
        }
      }
    }
  },
  "contents": {
    "text": {
      "maxCharacters": 20000
    }
  },
  "numResults": 5
}
```

### Response
#### Success Response (200)
- **results** (array) - An array of search results, each containing synthesized information, citations, and confidence scores.
  - **answer** (string) - The synthesized answer to the query.
  - **citations** (array) - A list of citations for the answer.
  - **confidence** (number) - The confidence score for the answer.
  - **fields** (object) - Structured data if `outputSchema` was provided.

#### Response Example
```json
{
  "results": [
    {
      "answer": "Recent advancements in renewable energy include breakthroughs in perovskite solar cells offering higher efficiency and lower production costs, alongside innovations in solid-state battery technology for improved energy storage.",
      "citations": [
        "https://example.com/perovskite-advancements",
        "https://example.com/solid-state-batteries"
      ],
      "confidence": 0.95,
      "fields": {
        "advancements": [
          {
            "technology": "Perovskite Solar Cells",
            "description": "Higher efficiency and lower production costs.",
            "citations": ["https://example.com/perovskite-advancements"]
          },
          {
            "technology": "Solid-State Batteries",
            "description": "Improved energy storage.",
            "citations": ["https://example.com/solid-state-batteries"]
          }
        ]
      }
    }
  ]
}
```
```

--------------------------------

### Task Operation API

Source: https://exa.ai/docs/reference/research/create-a-task

Provides details about task operations, including event types, plan IDs, task IDs, and timestamps.

```APIDOC
## Task Operation

### Description
This endpoint details the operations performed within a task, including event types, associated plan and task IDs, and creation timestamps.

### Method
GET (Assumed, as no method is specified)

### Endpoint
/websites/exa_ai/task-operation (Assumed endpoint based on context)

### Parameters
#### Query Parameters
- **eventType** (string) - Required - The type of event associated with the task operation.
- **planId** (string) - Required - The ID of the plan that owns this task.
- **taskId** (string) - Required - The ID of the task that generated this output.
- **operationId** (string) - Required - The ID of the operation.
- **data** (object) - Required - Additional data related to the operation.
- **createdAt** (number) - Required - When this event occurred (Unix timestamp in milliseconds).
- **researchId** (string) - Required - The research request this event belongs to.

### Response
#### Success Response (200)
- **result** (object) - Contains the results of the operation.
- **pageTokens** (array) - Tokens related to the page.

#### Response Example
```json
{
  "result": {},
  "pageTokens": []
}
```
```

--------------------------------

### API Response Structures

Source: https://exa.ai/docs/reference/migrating-from-bing

JSON schema comparison between the legacy Bing response format and the modern Exa response format.

```json
// Bing Response
{
  "webPages": {
    "value": [
      {
        "name": "Page Title",
        "url": "https://example.com",
        "snippet": "Description...",
        "dateLastCrawled": "2025-08-11T00:00:00"
      }
    ]
  }
}
```

```json
// Exa Response
{
  "results": [
    {
      "title": "Page Title",
      "url": "https://example.com",
      "publishedDate": "2025-08-11",
      "author": "Author Name",
      "text": "Full content when requested...",
      "highlights": ["Key sentences..."]
    }
  ],
  "requestId": "unique-id"
}
```

--------------------------------

### Cost Dollars Schema

Source: https://exa.ai/docs/reference/answer

Details the cost breakdown for API requests, including total cost, per-operation costs, and pricing details.

```APIDOC
## Cost Dollars Schema

### Description
Provides a detailed breakdown of costs associated with API usage, including total cost, operational costs, and pricing tiers.

### Schema
#### `CostDollars` (object)
- **total** (number) - The total dollar cost for the request.
  - *Format*: float
  - *Example*: 0.007
- **breakDown** (array) - A breakdown of costs by operation type.
  - *Items* (object):
    - **search** (number) - Cost of search operations.
      - *Format*: float
      - *Example*: 0.007
    - **contents** (number) - Cost of content operations.
      - *Format*: float
      - *Example*: 0
    - **breakdown** (object) - Detailed breakdown of content-related costs.
      - **neuralSearch** (number) - Cost of neural search operations.
        - *Format*: float
        - *Example*: 0.007
      - **deepSearch** (number) - Cost of deep search operations.
        - *Format*: float
        - *Example*: 0.012
      - **contentText** (number) - Cost of text content retrieval.
        - *Format*: float
        - *Example*: 0
      - **contentHighlight** (number) - Cost of highlight generation.
        - *Format*: float
        - *Example*: 0
      - **contentSummary** (number) - Cost of summary generation.
        - *Format*: float
        - *Example*: 0
- **perRequestPrices** (object) - Standard price per request for different operations.
  - **neuralSearch_1_10_results** (number) - Standard price for search with 1-10 results.
    - *Format*: float
    - *Example*: 0.007
  - **neuralSearch_additional_result** (number) - Standard price per additional result beyond 10.
    - *Format*: float
    - *Example*: 0.001
  - **deepSearch** (number) - Standard price for deep search per request.
    - *Format*: float
    - *Example*: 0.012
  - **deepReasoningSearch** (number) - Standard price for deep-reasoning search per request.
    - *Format*: float
    - *Example*: 0.015
- **perPagePrices** (object) - Standard price per page for different content operations.
  - **contentText** (number) - Standard price per page for text content.
    - *Format*: float
    - *Example*: 0.001
  - **contentHighlight** (number) - Standard price per page for highlights.
    - *Format*: float
    - *Example*: 0.001
  - **contentSummary** (number) - Standard price per result for summaries.
    - *Format*: float
    - *Example*: 0.001
```

--------------------------------

### Task Output API

Source: https://exa.ai/docs/reference/research/create-a-task

Retrieves the output of a completed task, including the content gathered and completion status.

```APIDOC
## Task Output

### Description
This endpoint provides the successful completion result of a task, including the type of output and the content gathered.

### Method
GET (Assumed, as no method is specified)

### Endpoint
/websites/exa_ai/task-output (Assumed endpoint based on context)

### Parameters
#### Query Parameters
- **eventType** (string) - Required - Must be 'task-output'.
- **planId** (string) - Required - The ID of the plan that owns this task.
- **taskId** (string) - Required - Which task produced this output.
- **outputType** (string) - Required - The type of output, must be 'completed'.
- **content** (string) - Required - The information gathered by this task.
- **createdAt** (number) - Required - When this event occurred (Unix timestamp in milliseconds).
- **researchId** (string) - Required - The research request this event belongs to.

### Response
#### Success Response (200)
- **output** (object) - The successful completion result of this task.
  - **outputType** (string) - Enum: ['completed'] - The type of output.
  - **content** (string) - The information gathered by this task.

#### Response Example
```json
{
  "output": {
    "outputType": "completed",
    "content": "Information gathered by the task."
  }
}
```
```

--------------------------------

### POST /api/tasks/operations

Source: https://exa.ai/docs/reference/research/create-a-task

Logs a new task operation, such as a reasoning step, a search execution, or a page crawl, associated with a specific research task.

```APIDOC
## POST /api/tasks/operations

### Description
Records a specific operation performed during the execution of a research task. This endpoint supports multiple operation types including 'think' (reasoning), 'search' (web search), and 'crawl' (page extraction).

### Method
POST

### Endpoint
/api/tasks/operations

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'task-operation'.
- **planId** (string) - Required - The ID of the plan owning this task.
- **taskId** (string) - Required - The ID of the task performing the operation.
- **operationId** (string) - Required - Unique identifier for this specific operation.
- **data** (object) - Required - The operation details, which can be a 'think', 'search', or 'crawl' object.

### Request Example
{
  "eventType": "task-operation",
  "planId": "plan_123",
  "taskId": "task_456",
  "operationId": "op_789",
  "data": {
    "type": "search",
    "searchType": "neural",
    "goal": "Find recent AI trends",
    "query": "AI trends 2024",
    "results": [{"url": "https://example.com"}],
    "pageTokens": 150
  }
}

### Response
#### Success Response (200)
- **status** (string) - Confirmation of operation logging.

#### Response Example
{
  "status": "success",
  "operationId": "op_789"
}
```

--------------------------------

### Retrieve Research Task with Exa AI API

Source: https://exa.ai/docs/reference/research/get-a-task

This snippet demonstrates how to retrieve a research task using the Exa AI API. It supports fetching a specific research task by its ID and optionally enables real-time streaming updates and detailed event logs. The API requires an 'x-api-key' for authentication.

```yaml
openapi: 3.1.0
info:
  title: Exa Research API
  description: >-
    Create asynchronous research tasks that explore the web, gather sources,
    synthesize findings, and return structured results with citations. Perfect
    for complex, multi-step research that requires reasoning over web data.
  version: 1.0.0
  contact: {}
servers:
  - url: https://api.exa.ai
    description: Production
security:
  - api_key: []
tags: []
paths:
  /research/v1/{researchId}:
    get:
      tags:
        - Research
      summary: Get a research request by id
      description: Retrieve research by ID. Add ?stream=true for real-time SSE updates.
      operationId: ResearchController_getResearch
      parameters:
        - name: researchId
          required: true
          in: path
          description: The unique identifier of the research request to retrieve
          schema:
            type: string
        - name: stream
          required: false
          in: query
          description: >-
            Set to "true" to receive real-time updates via Server-Sent Events
            (SSE)
          schema:
            type: string
        - name: events
          required: false
          in: query
          description: >-
            Set to "true" to include the detailed event log of all operations
            performed
          schema:
            type: string
      responses:
        '200':
          description: ''
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ResearchDtoClass'
x-codeSamples:
  - lang: bash
    label: Get research task
    source: >
      curl -X GET
      'https://api.exa.ai/research/v1/01jszdfs0052sg4jc552sg4jc5' \
        -H 'x-api-key: YOUR-EXA-API-KEY'
  - lang: bash
    label: Get research task with streaming
    source: >
      curl -X GET
      'https://api.exa.ai/research/v1/01jszdfs0052sg4jc552sg4jc5?stream=true'
      \
        -H 'x-api-key: YOUR-EXA-API-KEY'
  - lang: python
    label: Get research task
    source: |
      # pip install exa-py
      from exa_py import Exa
      exa = Exa('YOUR_EXA_API_KEY')

      task = exa.research.get_task('01jszdfs0052sg4jc552sg4jc5')
      print(task)
  - lang: javascript
    label: Get research task
    source: >
      // npm install exa-js

      import Exa from 'exa-js';

      const exa = new Exa('YOUR_EXA_API_KEY');


      const task = await
      exa.research.getTask('01jszdfs0052sg4jc552sg4jc5');

      console.log(task);
components:
  schemas:
    ResearchDtoClass:
      discriminator:
        propertyName: status
      oneOf:
        - type:
            - object
          properties:
            researchId:
              type:
                - string
              description: >-
                Unique identifier for tracking and retrieving this research
                request
            createdAt:
              type:
                - number
              description: When the research was created (Unix timestamp in milliseconds)
            model:
              default: exa-research
              type:
                - string
              enum:
                - exa-research-fast
                - exa-research
                - exa-research-pro
              description: The model used for this research request
            instructions:
              type:
                - string
              description: The original research instructions provided
            outputSchema:
              type:
                - object
              additionalProperties: {}
              description: The JSON Schema used to validate the output, if provided
            status:
              type:
                - string
              enum:
                - pending
          required:
            - researchId
            - createdAt
            - instructions
            - status
          title: Pending
        - type:
            - object
          properties:
            researchId:
              type:
                - string
              description: >-
                Unique identifier for tracking and retrieving this research
                request
            createdAt:
              type:
                - number
              description: When the research was created (Unix timestamp in milliseconds)
            model:
              default: exa-research
              type:
                - string
              enum:
                - exa-research-fast
                - exa-research
                - exa-research-pro
              description: The model used for this research request
            instructions:
              type:
                - string
              description: The original research instructions provided

```

--------------------------------

### Plan Operation Event - Think

Source: https://exa.ai/docs/reference/research/list-tasks

Represents a 'plan-operation' event with a 'think' operation, detailing the AI's reasoning process.

```APIDOC
## POST /websites/exa_ai/events

### Description
Records a 'plan-operation' event with a 'think' operation, detailing the AI's reasoning process.

### Method
POST

### Endpoint
/websites/exa_ai/events

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'plan-operation'.
- **planId** (string) - Required - Which plan this operation belongs to.
- **operationId** (string) - Required - Unique identifier for this specific operation.
- **data** (object) - Required - The details of the operation.
  - **type** (string) - Required - Must be 'think'.
  - **content** (string) - Required - The AI's reasoning process and decision-making steps.

### Request Example
```json
{
  "eventType": "plan-operation",
  "planId": "plan-123",
  "operationId": "op-xyz",
  "data": {
    "type": "think",
    "content": "The user is asking for information about X, so I need to search for relevant articles."
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Plan operation event recorded successfully."
}
```
```

--------------------------------

### Find Similar Pages with EXA_FINDSIMILAR

Source: https://exa.ai/docs/reference/exa-for-sheets

The EXA_FINDSIMILAR function finds URLs similar to a given reference URL. It accepts parameters for the number of results, and optional filters for including or excluding specific domains and text phrases. It returns a vertical array of similar URLs.

```google-sheets
=EXA_FINDSIMILAR("https://example.com", 5)
```

--------------------------------

### Content Fetch Statuses

Source: https://exa.ai/docs/reference/error-codes

When using the /contents or /search endpoints, errors for individual URLs are provided in the 'statuses' field. This allows for detailed error handling for each fetched URL.

```APIDOC
## GET /contents or GET /search with contents options

### Description
This endpoint (or search with content options) returns results along with a 'statuses' field for per-URL error handling.

### Method
GET

### Endpoint
/contents or /search?options=contents

### Parameters
#### Query Parameters
- **statuses** (array) - Contains objects detailing the status and errors for each URL processed.

### Response
#### Success Response (200)
- **results** (array) - The fetched content results.
- **statuses** (array) - An array of status objects for each URL.
  - **id** (string) - The URL that was processed.
  - **status** (string) - The status of the fetch operation ('error' or 'success').
  - **error** (object) - Contains details if the status is 'error'.
    - **tag** (string) - An error tag (e.g., 'CRAWL_NOT_FOUND').
    - **httpStatusCode** (integer) - The HTTP status code associated with the error.

#### Response Example
```json
{
  "results": [...],
  "statuses": [
    {
      "id": "https://example.com",
      "status": "error",
      "error": {
        "tag": "CRAWL_NOT_FOUND",
        "httpStatusCode": 404
      }
    }
  ]
}
```

### Error Tags
| Tag                       | HTTP Code | Description                                      |
| ------------------------- | --------- | ------------------------------------------------ |
| `CRAWL_NOT_FOUND`         | `404`     | Content not found at the specified URL           |
| `CRAWL_TIMEOUT`           | `408`     | Request timed out while fetching content         |
| `CRAWL_LIVECRAWL_TIMEOUT` | `408`     | Live crawl operation timed out                   |
| `SOURCE_NOT_AVAILABLE`    | `403`     | Access forbidden or source unavailable           |
| `UNSUPPORTED_URL`         | `—`       | URL scheme is not supported for content fetching |
| `CRAWL_UNKNOWN_ERROR`     | `500+`    | Other crawling errors                            |

### How to Handle
- **`CRAWL_NOT_FOUND`**: Verify the URL is correct and accessible.
- **`CRAWL_TIMEOUT`**: Retry the request or increase timeout if available.
- **`CRAWL_LIVECRAWL_TIMEOUT`**: Try again with `livecrawl: "fallback"` or `livecrawl: "never"`.
- **`SOURCE_NOT_AVAILABLE`**: Check if the source requires authentication or is behind a paywall.
- **`UNSUPPORTED_URL`**: Use a standard HTTP/HTTPS URL.
- **`CRAWL_UNKNOWN_ERROR`**: Retry the request; contact support if persistent.
```

--------------------------------

### POST /search/contents

Source: https://exa.ai/docs/reference/find-similar-links

Retrieves search results with advanced content extraction options, including text filtering and semantic section control.

```APIDOC
## POST /search/contents

### Description
Retrieves webpage content based on search criteria with options to filter by text inclusion/exclusion and extract specific page sections.

### Method
POST

### Endpoint
/search/contents

### Parameters
#### Request Body
- **includeText** (array) - Optional - List of strings that must be present in webpage text.
- **excludeText** (array) - Optional - List of strings that must not be present in webpage text.
- **moderation** (boolean) - Optional - Enable content moderation to filter unsafe content.
- **contents** (object) - Optional - Configuration for text and highlight retrieval.
  - **text** (object/boolean) - Advanced options for text extraction (maxCharacters, includeHtmlTags, verbosity, includeSections, excludeSections).

### Request Example
{
  "includeText": ["large language model"],
  "excludeText": ["course"],
  "moderation": true,
  "contents": {
    "text": {
      "maxCharacters": 1000,
      "verbosity": "standard",
      "includeSections": ["body", "header"]
    }
  }
}

### Response
#### Success Response (200)
- **results** (array) - List of retrieved content objects.

#### Response Example
{
  "results": [
    {
      "url": "https://example.com",
      "text": "Extracted page content..."
    }
  ]
}
```

--------------------------------

### POST /findSimilar

Source: https://exa.ai/docs/reference/find-similar-links

Finds links that are similar to a provided URL. This endpoint can optionally retrieve the content of the similar links found.

```APIDOC
## POST /findSimilar

### Description
Finds links that are similar to a provided URL. This endpoint can optionally retrieve the content of the similar links found.

### Method
POST

### Endpoint
/findSimilar

### Parameters
#### Request Body
- **url** (string) - Required - The URL for which to find similar links.
- **numResults** (integer) - Optional - The number of results to return. Defaults to 10. Maximum is 100.
- **includeDomains** (array of strings) - Optional - A list of domains to include in the search. If specified, results will only come from these domains.
- **excludeDomains** (array of strings) - Optional - A list of domains to exclude from search results.
- **startCrawlDate** (string) - Optional - Results will include links crawled after this date. Must be in ISO 8601 format.
- **endCrawlDate** (string) - Optional - Results will include links crawled before this date. Must be in ISO 8601 format.
- **startPublishedDate** (string) - Optional - Only links published after this date will be returned. Must be in ISO 8601 format.
- **endPublishedDate** (string) - Optional - Only links published before this date will be returned. Must be in ISO 8601 format.
- **contents** (object) - Optional - Specifies which content fields to retrieve for the found links.
  - **text** (boolean) - Optional - If true, the text content of the links will be returned.

### Request Example
```json
{
  "url": "https://arxiv.org/abs/2307.06435",
  "contents": {
    "text": true
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - A list of similar links found.
  - Each item in the array is an object containing details about the link, such as its URL, title, and potentially its content if requested.

#### Response Example
```json
{
  "results": [
    {
      "url": "https://example.com/similar-link-1",
      "title": "Example Similar Link 1",
      "text": "This is the content of the first similar link."
    },
    {
      "url": "https://example.com/similar-link-2",
      "title": "Example Similar Link 2"
    }
  ]
}
```
```

--------------------------------

### Operation Data Types

Source: https://exa.ai/docs/reference/research/list-tasks

Details the different types of operations that can be performed within a task, including 'think', 'search', and 'crawl'.

```APIDOC
## Operation Data Types

### Description
This section details the possible structures for the `data` field within a Task Definition, representing different types of operations.

### Method
N/A (This describes data structures within the Task Definition)

### Endpoint
N/A

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
This describes the possible object types for the `data` field:

**1. Think Operation**
- **type** (string) - Enum: `think` - Required - Indicates a reasoning operation.
- **content** (string) - Required - The AI's reasoning process and decision-making steps.

**2. Search Operation**
- **type** (string) - Enum: `search` - Required - Indicates a search operation.
- **searchType** (string) - Enum: `neural`, `auto`, `fast` - Required - The search algorithm used.
- **goal** (string) - Required - What the AI is trying to find with this search.
- **query** (string) - Required - The exact search query sent to the search engine.
- **results** (array) - Required - URLs returned by the search, ranked by relevance. Each item must have a `url` (string).
- **pageTokens** (number) - Required - Token cost for processing search result snippets.

**3. Crawl Operation**
- **type** (string) - Enum: `crawl` - Required - Indicates a crawl operation.
- **goal** (string) - Required - What information the AI expects to find on this page.
- **result** (object) - Required - The specific page that was crawled. Must have a `url` (string).
- **pageTokens** (number) - Required - Token cost for processing the full page content.

### Request Example
**Think Operation Example:**
```json
{
  "type": "think",
  "content": "The user is asking for recent studies on AI ethics. I should perform a search."
}
```

**Search Operation Example:**
```json
{
  "type": "search",
  "searchType": "neural",
  "goal": "Find recent studies on AI ethics",
  "query": "AI ethics recent studies",
  "results": [
    {
      "url": "https://example.com/study1"
    },
    {
      "url": "https://example.com/study2"
    }
  ],
  "pageTokens": 50
}
```

**Crawl Operation Example:**
```json
{
  "type": "crawl",
  "goal": "Extract the main arguments from the linked article.",
  "result": {
    "url": "https://example.com/article/ai-ethics-debate"
  },
  "pageTokens": 120
}
```

### Response
#### Success Response (200)
N/A (This describes data structures within the Task Definition)

#### Response Example
N/A
```

--------------------------------

### POST /search - Deep Search Schema

Source: https://exa.ai/docs/reference/search-best-practices

Define structured output schemas for deep search variants to receive machine-readable JSON responses.

```APIDOC
## POST /search

### Description
Enforces a structured JSON schema for deep search query responses.

### Method
POST

### Parameters
#### Request Body
- **query** (string) - Required - The search query.
- **type** (string) - Required - Must be 'deep' or 'deep-reasoning'.
- **outputSchema** (object) - Required - The JSON schema definition for the response.

### Request Example
{
  "query": "top aerospace companies",
  "type": "deep",
  "outputSchema": {
    "type": "object",
    "properties": {
      "companies": {
        "type": "array",
        "items": {
          "type": "object",
          "properties": {
            "company_name": { "type": "string" },
            "stock_price": { "type": "number" }
          }
        }
      }
    }
  }
}
```

--------------------------------

### Implement Conditional Search Logic

Source: https://exa.ai/docs/reference/exa-for-sheets

Integrates standard Google Sheets IF statements with EXA_SEARCH to ensure queries only execute when specific input cells contain data.

```Google Sheets Formula
=IF(A2<>"", EXA_SEARCH(CONCAT("latest ", A2, " trends"), 5), "Enter a topic")
```

--------------------------------

### Configure Fast Search in Python

Source: https://exa.ai/docs/reference/evaluating-exa-search

Fast search is optimized for speed-critical applications with a median latency of approximately 500ms. It is ideal for real-time applications like voice agents or high-volume workflows.

```python
result = exa.search_and_contents(
    "latest AI breakthroughs in 2025",
    type="fast",
    num_results=10,
    text={"max_characters": 15000}
)
```

--------------------------------

### Format Search Results with Citations

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

Utility function to append citation URLs to text and generate an annotation object. This helps in mapping source references to specific parts of the generated text.

```python
def format_response_with_citations(text, citations):
    """Format the response to include citations as annotations."""
    annotations = []
    formatted_text = text

    for i, citation in enumerate(citations):
        start_index = len(formatted_text)
        citation_text = f"\n\n[{i+1}] {citation['url']}"
        end_index = start_index + len(citation_text)

        annotation = {
            "type": "url_citation",
            "start_index": start_index,
            "end_index": end_index,
            "url": citation["url"],
            "title": citation["title"]
        }

        annotations.append(annotation)
        formatted_text += citation_text

    return {
        "text": formatted_text,
        "annotations": annotations
    }
```

--------------------------------

### List Tasks API

Source: https://exa.ai/docs/reference/research/list-tasks

Retrieve a paginated list of your research tasks. Supports cursor-based pagination with limit and cursor parameters.

```APIDOC
## GET /tasks

### Description
Retrieve a paginated list of your research tasks. The response follows a cursor-based pagination pattern. Pass the `limit` parameter to control page size (max 50) and use the `cursor` token returned in the response to fetch subsequent pages.

### Method
GET

### Endpoint
/tasks

#### Query Parameters
- **limit** (integer) - Optional - The maximum number of tasks to return per page. Defaults to 20. Maximum value is 50.
- **cursor** (string) - Optional - A token returned from a previous request to fetch the next page of results.

### Response
#### Success Response (200)
- **data** (array) - A list of task objects.
  - **id** (string) - The unique identifier for the task.
  - **name** (string) - The name of the task.
  - **status** (string) - The current status of the task (e.g., 'running', 'completed', 'failed').
  - **createdAt** (string) - The timestamp when the task was created.
- **next_cursor** (string) - A token to fetch the next page of results. Null if there are no more pages.

#### Response Example
{
  "data": [
    {
      "id": "task_123",
      "name": "My First Research Task",
      "status": "completed",
      "createdAt": "2023-10-27T10:00:00Z"
    }
  ],
  "next_cursor": "cursor_abc123"
}
```

--------------------------------

### Task Operation

Source: https://exa.ai/docs/reference/research/get-a-task

Represents a single operation performed within a task, including its metadata and the specific action taken.

```APIDOC
## Task Operation Object

### Description
Represents a single operation performed within a task, including its metadata and the specific action taken.

### Properties
- **eventType** (string) - Required - The type of event that occurred.
- **planId** (string) - Required - The ID of the plan this operation belongs to.
- **taskId** (string) - Required - The ID of the task performing this operation.
- **operationId** (string) - Required - Unique identifier for this specific operation.
- **data** (object) - Required - The actual operation performed within this task. See nested types below.
- **createdAt** (number) - Required - When this event occurred (Unix timestamp in milliseconds).
- **researchId** (string) - Required - The research request this event belongs to.

### Data Object Types

#### Think Operation
- **type** (string) - Required - Must be 'think'.
- **content** (string) - Required - The AI's reasoning process and decision-making steps.

#### Search Operation
- **type** (string) - Required - Must be 'search'.
- **searchType** (string) - Required - Search algorithm used (neural for semantic search, auto for intelligent search method selection).
- **goal** (string) - Required - What the AI is trying to find with this search.
- **query** (string) - Required - The exact search query sent to the search engine.
- **results** (array) - Required - URLs returned by the search, ranked by relevance. Each item has a 'url' (string).
- **pageTokens** (number) - Required - Token cost for processing search result snippets.

#### Crawl Operation
- **type** (string) - Required - Must be 'crawl'.
- **goal** (string) - Required - What information the AI expects to find on this page.
- **result** (object) - Required - The specific page that was crawled. Contains a 'url' (string).
- **pageTokens** (number) - Required - Token cost for processing the full page content.

### Example Request Body (Think Operation)
```json
{
  "eventType": "TASK_OPERATION",
  "planId": "plan_123",
  "taskId": "task_abc",
  "operationId": "op_xyz",
  "data": {
    "type": "think",
    "content": "The user wants to know the capital of France. I should search for it."
  },
  "createdAt": 1678886400000,
  "researchId": "research_789"
}
```

### Example Request Body (Search Operation)
```json
{
  "eventType": "TASK_OPERATION",
  "planId": "plan_123",
  "taskId": "task_abc",
  "operationId": "op_xyz",
  "data": {
    "type": "search",
    "searchType": "neural",
    "goal": "Find the capital of France",
    "query": "capital of France",
    "results": [
      {"url": "https://en.wikipedia.org/wiki/Paris"}
    ],
    "pageTokens": 50
  },
  "createdAt": 1678886400000,
  "researchId": "research_789"
}
```

### Example Request Body (Crawl Operation)
```json
{
  "eventType": "TASK_OPERATION",
  "planId": "plan_123",
  "taskId": "task_abc",
  "operationId": "op_xyz",
  "data": {
    "type": "crawl",
    "goal": "Extract key information about AI advancements",
    "result": {
      "url": "https://example.com/ai-advancements"
    },
    "pageTokens": 200
  },
  "createdAt": 1678886400000,
  "researchId": "research_789"
}
```
```

--------------------------------

### Exa API Response Structure

Source: https://exa.ai/docs/reference/context

Defines the expected JSON response format from the Exa Context API, including the request ID, the original query, the formatted response string, and metadata regarding cost and search performance.

```json
{
  "requestId": "req_12345",
  "query": "how to use React hooks for state management",
  "response": "// Formatted code snippets and contextual examples\n...",
  "resultsCount": 15,
  "costDollars": "0.0025",
  "searchTime": 1.234,
  "outputTokens": 1247
}
```

--------------------------------

### Process Tool Calls and Manage Conversation State

Source: https://exa.ai/docs/reference/openai-tool-calling

Handles the execution of tool calls generated by the LLM and updates the message history with search results. This ensures the model has access to external data before generating a final response.

```python
def process_tool_calls(tool_calls, messages):
    for tool_call in tool_calls:
        function_name = tool_call.function.name
        function_args = json.loads(tool_call.function.arguments)
        if function_name == "exa_search":
            search_results = exa_search(**function_args)
            messages.append({"role": "tool", "content": str(search_results), "tool_call_id": tool_call.id})
    return messages
```

--------------------------------

### Plan Output Event

Source: https://exa.ai/docs/reference/research/create-a-task

Represents the output of a research plan, which can either be a set of tasks or a stop signal.

```APIDOC
## Plan Output Event

### Description
Represents the output of a research plan, which can either be a set of tasks or a stop signal.

### Event Type
`plan-output`

### Data Structure
```json
{
  "eventType": "plan-output",
  "planId": "string",
  "output": {
    "discriminator": {
      "propertyName": "outputType"
    },
    "oneOf": [
      {
        "type": ["object"],
        "properties": {
          "outputType": {
            "type": ["string"],
            "enum": ["tasks"]
          },
          "reasoning": {
            "type": ["string"],
            "description": "Why these specific tasks were chosen"
          },
          "tasksInstructions": {
            "type": ["array"],
            "items": {
              "type": ["string"]
            },
            "description": "List of task instructions that will be executed in parallel"
          }
        },
        "required": ["outputType", "reasoning", "tasksInstructions"]
      },
      {
        "type": ["object"],
        "properties": {
          "outputType": {
            "type": ["string"],
            "enum": ["stop"]
          },
          "reasoning": {
            "type": ["string"],
            "description": "Why the AI decided to stop researching"
          }
        },
        "required": ["outputType", "reasoning"]
      }
    ]
  },
  "createdAt": "number",
  "researchId": "string"
}
```

### Required Fields
- `eventType`
- `planId`
- `output`
- `createdAt`
- `researchId`
```

--------------------------------

### Plan Operation Event

Source: https://exa.ai/docs/reference/research/list-tasks

Tracks the execution of specific operations like crawling, searching, or thinking within a research plan.

```APIDOC
## POST /events/plan-operation

### Description
Logs an operation performed by the AI during a research plan, such as a web crawl.

### Method
POST

### Endpoint
/events/plan-operation

### Request Body
- **eventType** (string) - Required - Must be 'plan-operation'
- **planId** (string) - Required - The ID of the plan
- **operationId** (string) - Required - Unique identifier for the operation
- **data** (object) - Required - Operation details including 'type', 'result', and 'pageTokens'
- **createdAt** (number) - Required - Unix timestamp in milliseconds
- **researchId** (string) - Required - The associated research request ID

### Request Example
{
  "eventType": "plan-operation",
  "planId": "plan-123",
  "operationId": "op-456",
  "data": {
    "type": "crawl",
    "result": {"url": "https://example.com"},
    "pageTokens": 150
  },
  "createdAt": 1672531200000,
  "researchId": "res-789"
}
```

--------------------------------

### Plan Definition Event

Source: https://exa.ai/docs/reference/research/get-a-task

Defines the schema for a plan-definition event used to track planning cycles within the research process.

```APIDOC
## Plan Definition Event

### Description
Represents the initiation or update of a planning cycle for a research request.

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'plan-definition'
- **planId** (string) - Required - Identifier for this planning cycle
- **createdAt** (number) - Required - Unix timestamp in milliseconds

### Response Example
{
  "eventType": "plan-definition",
  "planId": "plan_abc",
  "createdAt": 1672531200000
}
```

--------------------------------

### EXA_ANSWER Function for Google Sheets

Source: https://exa.ai/docs/reference/exa-for-sheets

The EXA_ANSWER function generates AI-powered answers based on web search results. It accepts a prompt and optional parameters for text prefixes/suffixes and whether to include citations. The function returns a string containing the answer, with citations included if specified.

```Google Apps Script
=EXA_ANSWER("What is quantum computing?", "", "", TRUE)
```

--------------------------------

### Format Search Results with Citations in JavaScript

Source: https://exa.ai/docs/reference/openai-responses-api-with-exa

A utility function that processes raw text and citation objects into a structured format with appended references and annotation metadata. It calculates index offsets to map citations to the text body.

```javascript
function formatResponseWithCitations(text, citations) {
  const annotations = [];
  let formattedText = text;

  citations.forEach((citation, index) => {
    const annotation = {
      type: "url_citation",
      start_index: formattedText.length,
      end_index: formattedText.length + citation.url.length + 3,
      url: citation.url,
      title: citation.title,
    };

    annotations.push(annotation);
    formattedText += `\n\n[${index + 1}] ${citation.url}`;
  });

  return {
    text: formattedText,
    annotations,
  };
}
```

--------------------------------

### Highlights Retrieval

Source: https://exa.ai/docs/reference/search

Retrieve text snippets identified as most relevant from each page. Supports simple boolean toggling or advanced options for customization.

```APIDOC
## GET /websites/exa_ai/highlights

### Description
Retrieves text snippets that the LLM identifies as most relevant from each page. This can be controlled with simple boolean values or advanced options.

### Method
GET

### Endpoint
/websites/exa_ai/highlights

### Parameters
#### Query Parameters
- **highlights** (boolean | object) - Optional - Controls the retrieval of highlights. If true, returns highlights with default settings. If an object, allows advanced options.
  - **maxCharacters** (integer) - Optional - Maximum number of characters to return for highlights. Controls the total length of highlight text returned per URL. Example: 2000
  - **numSentences** (integer) - Optional - Deprecated. Mapped to character budget. Use `maxCharacters` instead. Example: 1
  - **highlightsPerUrl** (integer) - Optional - Deprecated. Ignored. Use `maxCharacters` instead. Example: 1
  - **query** (string) - Optional - Custom query to direct the LLM's selection of highlights. Example: "Key advancements"

### Response
#### Success Response (200)
- **highlights** (array) - An array of highlight objects, each containing relevant text snippets.

#### Response Example
```json
{
  "highlights": [
    {
      "text": "Example highlight text..."
    }
  ]
}
```
```

--------------------------------

### Research Paper Search Skill Configuration

Source: https://exa.ai/docs/reference/research-paper-search-claude-skill

Configuration for the Claude skill to search for research papers using Exa's advanced search.

```APIDOC
## Web Search Advanced - Research Paper Category Skill

### Description
This skill enables searching for academic papers, arXiv preprints, and scientific research using Exa's advanced search capabilities. It supports full filter options including date ranges and text filtering.

### Skill Definition
```yaml
---
name: web-search-advanced-research-paper
description: Search for research papers and academic content using Exa advanced search. Full filter support including date ranges and text filtering. Use when searching for academic papers, arXiv preprints, or scientific research.
context: fork
---

# Web Search Advanced - Research Paper Category

## Tool Restriction (Critical)
ONLY use `web_search_advanced_exa` with `category: "research paper"`. Do NOT use other categories or tools.

## Full Filter Support
The `research paper` category supports ALL available parameters:

### Core
- `query` (required)
- `numResults`
- `type` ("auto", "fast", "deep", "neural")

### Domain filtering
- `includeDomains` (e.g., ["arxiv.org", "openreview.net"])
- `excludeDomains`

### Date filtering (ISO 8601)
- `startPublishedDate` / `endPublishedDate`
- `startCrawlDate` / `endCrawlDate`

### Text filtering
- `includeText` (must contain ALL)
- `excludeText` (exclude if ANY match)

**Array size restriction:** `includeText` and `excludeText` only support **single-item arrays**. Multi-item arrays (2+ items) cause 400 errors. To match multiple terms, put them in the `query` string or run separate searches.

### Content extraction
- `textMaxCharacters` / `contextMaxCharacters`
- `enableSummary` / `summaryQuery`
- `enableHighlights` / `highlightsNumSentences` / `highlightsPerUrl` / `highlightsQuery`

### Additional
- `userLocation`
- `moderation`
- `additionalQueries`
- `livecrawl` / `livecrawlTimeout`
- `subpages` / `subpageTarget`

## Token Isolation (Critical)
Never run Exa searches in main context. Always spawn Task agents:
- Agent calls `web_search_advanced_exa` with `category: "research paper"`
- Agent merges + deduplicates results before presenting
- Agent returns distilled output (brief markdown or compact JSON)
- Main context stays clean regardless of search volume

## When to Use
Use this category when you need:
- Academic papers from arXiv, OpenReview, PubMed, etc.
- Scientific research on specific topics
- Literature reviews with date filtering
- Papers containing specific methodologies or terms

## Examples

### Recent papers on a topic
```json
web_search_advanced_exa {
  "query": "transformer attention mechanisms efficiency",
  "category": "research paper",
  "startPublishedDate": "2024-01-01",
  "numResults": 15,
  "type": "auto"
}
```

### Papers from specific venues
```json
web_search_advanced_exa {
  "query": "large language model agents",
  "category": "research paper",
  "includeDomains": ["arxiv.org", "openreview.net"],
  "includeText": ["LLM"],
  "numResults": 20,
  "type": "deep"
}
```

## Output Format
Return:
1) Results (structured list with title, authors, date, abstract summary)
2) Sources (URLs with publication venue)
3) Notes (methodology differences, conflicting findings)
```
```

--------------------------------

### Python: Handling Contents API Errors

Source: https://exa.ai/docs/reference/contents-best-practices

This Python code snippet demonstrates how to iterate through the 'statuses' array returned by the Exa AI Contents API. It checks the 'status' field for each entry and prints an error message along with the URL and the specific error tag if a failure is detected.

```python
result = exa.get_contents(["https://example.com", "https://example.com/maybe-broken"])
for status in result.statuses:
    if status.status == "error":
        print(f"Failed: {status.id} - {status.error.tag}")
```

--------------------------------

### Plan Definition Event

Source: https://exa.ai/docs/reference/research/list-tasks

Represents a 'plan-definition' event, which includes details about a planning cycle within a research request.

```APIDOC
## POST /websites/exa_ai/events

### Description
Records a 'plan-definition' event associated with a research request.

### Method
POST

### Endpoint
/websites/exa_ai/events

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'plan-definition'.
- **planId** (string) - Required - Identifier for this planning cycle.
- **createdAt** (number) - Required - When this event occurred (Unix timestamp in milliseconds).
- **researchId** (string) - Required - The research request this event belongs to.

### Request Example
```json
{
  "eventType": "plan-definition",
  "planId": "plan-123",
  "createdAt": 1678886400000,
  "researchId": "research-abc"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Plan definition event recorded successfully."
}
```
```

--------------------------------

### Plan Operation Event

Source: https://exa.ai/docs/reference/research/get-a-task

Represents an operation performed by the AI plan, such as thinking, searching, or crawling.

```APIDOC
## POST /events/plan-operation

### Description
Logs an operation performed by the AI during the research process.

### Method
POST

### Endpoint
/events/plan-operation

### Request Body
- **eventType** (string) - Required - The type of operation (e.g., think, search, crawl)
- **planId** (string) - Required - The ID of the plan
- **operationId** (string) - Required - Unique identifier for the operation
- **data** (object) - Required - The actual operation details
- **createdAt** (number) - Required - Unix timestamp in milliseconds
- **researchId** (string) - Required - The research request ID

### Request Example
{
  "eventType": "search",
  "planId": "plan-123",
  "operationId": "op-456",
  "data": { "query": "AI trends 2024" },
  "createdAt": 1715678901234,
  "researchId": "res-789"
}
```

--------------------------------

### Perform Deep Search with Structured Output

Source: https://exa.ai/docs/reference/search

Executes a deep search query that returns results mapped to a specific JSON schema. Useful for extracting structured data from search results.

```bash
curl --request POST \
  --url https://api.exa.ai/search \
  --header 'x-api-key: <token>' \
  --header 'Content-Type: application/json' \
  --data '{
  "query": "Who is the CEO of OpenAI?",
  "type": "deep",
  "outputSchema": {
    "type": "object",
    "properties": {
      "leader": { "type": "string" },
      "title": { "type": "string" },
      "sourceCount": { "type": "number" }
    },
    "required": ["leader", "title"]
  },
  "contents": {
    "text": true
  }
}'
```

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

results = exa.search(
    "Who is the CEO of OpenAI?",
    type="deep",
    output_schema={
        "type": "object",
        "properties": {
            "leader": {"type": "string"},
            "title": {"type": "string"},
            "sourceCount": {"type": "number"}
        },
        "required": ["leader", "title"]
    }
)
```

--------------------------------

### Task Definition Event

Source: https://exa.ai/docs/reference/research/create-a-task

Defines a specific task to be executed within a research plan.

```APIDOC
## Task Definition Event

### Description
Defines a specific task to be executed within a research plan.

### Event Type
`task-definition`

### Data Structure
```json
{
  "eventType": "task-definition",
  "planId": "string",
  "taskId": "string",
  "instructions": "string",
  "createdAt": "number"
}
```

### Required Fields
- `eventType`
- `planId`
- `taskId`
- `instructions`
- `createdAt`
```

--------------------------------

### Invoke RAG Chain

Source: https://exa.ai/docs/reference/langchain

Executes the configured RAG chain synchronously using the invoke method to retrieve and generate a response based on a specific user query.

```Python
result = chain.invoke("Latest research on climate change innovation")
print(result)
```

--------------------------------

### Search with Content Extraction API

Source: https://exa.ai/docs/reference/migrating-from-bing

This endpoint combines search functionality with integrated content extraction, allowing you to retrieve search results along with their content or highlights.

```APIDOC
## POST /search

### Description
Performs a search and extracts content from the results. You can request the full text or specific highlights based on a query.

### Method
POST

### Endpoint
https://api.exa.ai/search

### Parameters
#### Request Body
- **query** (string) - Required - The search query.
- **numResults** (integer) - Optional - The number of search results to retrieve.
- **contents** (object) - Optional - Configuration for content extraction.
  - **text** (boolean) - Optional - If true, returns the full text content of the page.
  - **highlights** (object) - Optional - Configuration for extracting highlights.
    - **maxCharacters** (integer) - Optional - The maximum number of characters for each highlight.
    - **query** (string) - Optional - The query to use for generating highlights.

### Request Example
```json
{
  "query": "climate change research",
  "numResults": 5,
  "contents": {
    "text": true,
    "highlights": {
      "maxCharacters": 2000,
      "query": "key findings"
    }
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - A list of search results, potentially including extracted content or highlights.

#### Response Example
```json
{
  "results": [
    {
      "title": "Climate Change Research Findings",
      "url": "http://example.com/climate-research",
      "content": "This is the extracted text content...",
      "highlights": "Key findings include..."
    }
  ]
}
```
```

--------------------------------

### Plan Output Event

Source: https://exa.ai/docs/reference/research/list-tasks

Records the decision output of a research plan, determining whether to proceed with tasks or stop the research.

```APIDOC
## POST /events/plan-output

### Description
Logs the output of a research plan, which can be a set of tasks to execute or a command to stop.

### Method
POST

### Endpoint
/events/plan-output

### Request Body
- **eventType** (string) - Required - Must be 'plan-output'
- **planId** (string) - Required - The ID of the plan
- **output** (object) - Required - The decision object (tasks or stop)
- **createdAt** (number) - Required - Unix timestamp in milliseconds
- **researchId** (string) - Required - The associated research request ID

### Request Example
{
  "eventType": "plan-output",
  "planId": "plan-123",
  "output": {
    "outputType": "tasks",
    "reasoning": "Need to gather more data",
    "tasksInstructions": ["Search for X", "Summarize Y"]
  },
  "createdAt": 1672531200000,
  "researchId": "res-789"
}
```

--------------------------------

### Claude Skill Configuration for People Research

Source: https://exa.ai/docs/reference/people-search-claude-skill

YAML configuration for a Claude skill named 'people-research'. It specifies the tool to use (`web_search_advanced_exa`) and provides guidelines for its operation, including tool restrictions, token isolation, dynamic tuning, and category usage.

```yaml
---
name: people-research
description: People research using Exa search. Finds LinkedIn profiles, professional backgrounds, experts, team members, and public bios across the web. Use when searching for people, finding experts, or looking up professional profiles.
context: fork
---

# People Research

## Tool Restriction (Critical)

ONLY use `web_search_advanced_exa`. Do NOT use `web_search_exa` or any other Exa tools.

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents:
- Agent runs Exa search internally
- Agent processes results using LLM intelligence
- Agent returns only distilled output (compact JSON or brief markdown)
- Main context stays clean regardless of search volume

## Dynamic Tuning

No hardcoded numResults. Tune to user intent:
- User says "a few" → 10-20
- User says "comprehensive" → 50-100
- User specifies number → match it
- Ambiguous? Ask: "How many profiles would you like?"

## Query Variation

Exa returns different results for different phrasings. For coverage:
- Generate 2-3 query variations
- Run in parallel
- Merge and deduplicate

## Categories

Use appropriate Exa `category` depending on what you need:
- `people` → LinkedIn profiles, public bios (primary for discovery)
- `personal site` → personal blogs, portfolio sites, about pages
- `news` → press mentions, interviews, speaker bios
- No category (`type: "auto"`) → general web results, broader context

Start with `category: "people"` for profile discovery, then use other categories or no category with `livecrawl: "fallback"` for deeper research on specific individuals.

### Category-Specific Filter Restrictions

When using `category: "people"`, these parameters cause errors:
- `startPublishedDate` / `endPublishedDate`
- `startCrawlDate` / `endCrawlDate`
- `includeText` / `excludeText`
- `excludeDomains`
- `includeDomains` — **LinkedIn domains only** (e.g., "linkedin.com")

When searching without a category, all parameters are available (but `includeText`/`excludeText` still only support single-item arrays).

## LinkedIn

Public LinkedIn via Exa: `category: "people"`, no other filters.
Auth-required LinkedIn → use Claude in Chrome browser fallback.

## Browser Fallback

Auto-fallback to Claude in Chrome when:
- Exa returns insufficient results
- Content is auth-gated
- Dynamic pages need JavaScript

```

--------------------------------

### Define OpenAI Tool Schema

Source: https://exa.ai/docs/reference/openai-tool-calling

Defines the JSON structure required by OpenAI to understand and invoke external functions.

```json
{
    "name": "my_function_name",
    "description": "The description of my function",
    "input_schema": {
        "type": "object",
        "properties": {
            "query": {
                "type": "string",
                "description": "The search query to perform."
            }
        },
        "required": ["query"]
    }
}
```

--------------------------------

### Common Request Parameters

Source: https://exa.ai/docs/reference/search

Common parameters applicable to various search requests, including result limits, domain filtering, and date range filtering.

```APIDOC
## Common Request Parameters

### Parameters
#### Query Parameters
- **numResults** (integer) - Optional - Number of results to return. Maximum 100. Limits vary by search type.
- **includeDomains** (array of strings) - Optional - List of domains to include in the search. Results will only come from these domains.
- **excludeDomains** (array of strings) - Optional - List of domains to exclude from search results.
- **startCrawlDate** (string, date-time) - Optional - Results will include links crawled after this date. Must be in ISO 8601 format.
- **endCrawlDate** (string, date-time) - Optional - Results will include links crawled before this date. Must be in ISO 8601 format.
- **startPublishedDate** (string, date-time) - Optional - Only links with a published date after this will be returned. Must be in ISO 8601 format.
- **endPublishedDate** (string, date-time) - Optional - Only links with a published date before this will be returned. Must be in ISO 8601 format.

### Example Usage
These parameters can be appended to the `/search` endpoint requests to refine the search results.
```

--------------------------------

### Website Search API

Source: https://exa.ai/docs/reference/search

This API allows users to search for websites using various criteria. It supports filtering by confidence levels and requires content and grounding information.

```APIDOC
## POST /websites/exa_ai

### Description
Allows searching for websites based on provided criteria.

### Method
POST

### Endpoint
/websites/exa_ai

### Parameters
#### Request Body
- **content** (string) - Required - The content to search for.
- **grounding** (string) - Required - Grounding information for the search.
- **confidence** (string) - Optional - The confidence level for the search results. Allowed values: "low", "medium", "high".
- **costDollars** (object) - Optional - Cost details in dollars. (Refer to '#/components/schemas/CostDollars' for schema)

### Request Example
```json
{
  "content": "example content",
  "grounding": "example grounding",
  "confidence": "high",
  "costDollars": {
    "amount": 10,
    "currency": "USD"
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - A list of website search results.
- **total** (integer) - The total number of results found.

#### Response Example
```json
{
  "results": [
    {
      "url": "http://example.com",
      "title": "Example Website",
      "snippet": "This is a snippet of the website content."
    }
  ],
  "total": 1
}
```

### Security
API key can be provided either via x-api-key header or Authorization header with Bearer scheme.
```

--------------------------------

### Advanced Search with Filters

Source: https://exa.ai/docs/reference/search

Conduct a search with advanced filtering options, including content type, number of results, and specific content extraction settings.

```APIDOC
## POST /search

### Description
Performs a search with advanced filtering options such as content type, number of results, and detailed content extraction.

### Method
POST

### Endpoint
https://api.exa.ai/search

### Parameters
#### Query Parameters
None

#### Request Body
- **query** (string) - Required - The search query.
- **type** (string) - Optional - The type of search ('auto', 'web', 'news', '論文'). Defaults to 'auto'.
- **category** (string) - Optional - Filters results by category (e.g., 'research paper').
- **numResults** (integer) - Optional - The number of results to return. Defaults to 10.
- **moderation** (boolean) - Optional - Whether to apply content moderation. Defaults to false.
- **contents** (object) - Optional - Specifies what content to retrieve.
  - **text** (boolean) - Optional - Whether to retrieve the text content.
  - **summary** (object) - Optional - Configuration for generating a summary.
    - **query** (string) - Required if summary is enabled - The query for the summary.
  - **subpages** (integer) - Optional - Number of subpages to crawl.
  - **subpageTarget** (string) - Optional - Target for subpage crawling ('sources', 'all').
  - **extras** (object) - Optional - Additional data to retrieve.
    - **links** (integer) - Optional - Number of links to retrieve.
    - **imageLinks** (integer) - Optional - Number of image links to retrieve.

### Request Example
```json
{
  "query": "Latest research in LLMs",
  "type": "auto",
  "category": "research paper",
  "numResults": 10,
  "moderation": true,
  "contents": {
    "text": true,
    "summary": {
      "query": "Main developments"
    },
    "subpages": 1,
    "subpageTarget": "sources",
    "extras": {
      "links": 1,
      "imageLinks": 1
    }
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - List of search results with detailed content.

#### Response Example
```json
{
  "results": [
    {
      "title": "Example Research Paper",
      "url": "http://example.com/paper",
      "content": "Detailed text content...",
      "summary": "Summary of main developments..."
    }
  ]
}
```
```

--------------------------------

### Task Output Event

Source: https://exa.ai/docs/reference/research/list-tasks

Records the final output or completion status of a research task.

```APIDOC
## POST /tasks/outputs

### Description
Records the successful completion result and gathered information from a task.

### Method
POST

### Endpoint
/tasks/outputs

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'task-output'.
- **planId** (string) - Required - The ID of the plan owning the task.
- **taskId** (string) - Required - The ID of the task.
- **output** (object) - Required - The completion result.
  - **outputType** (string) - Required - Must be 'completed'.
  - **content** (string) - Required - The information gathered.
- **createdAt** (number) - Required - Unix timestamp in milliseconds.
- **researchId** (string) - Required - The research request ID.

### Request Example
{
  "eventType": "task-output",
  "planId": "plan_123",
  "taskId": "task_456",
  "output": {
    "outputType": "completed",
    "content": "Research findings..."
  },
  "createdAt": 1672531200000,
  "researchId": "res_001"
}
```

--------------------------------

### JSON Response Structure for Contents API Statuses

Source: https://exa.ai/docs/reference/contents-best-practices

This JSON structure illustrates the response from the Contents API, specifically highlighting the 'statuses' field which contains detailed status information for each requested URL. It shows successful and error states, including specific error details like 'tag' and 'httpStatusCode'.

```json
{
  "results": [...],
  "statuses": [
    {
      "id": "https://example.com",
      "status": "success"
    },
    {
      "id": "https://example.com/broken",
      "status": "error",
      "error": {
        "tag": "CRAWL_NOT_FOUND",
        "httpStatusCode": 404
      }
    }
  ]
}
```

--------------------------------

### API Error Response Structure

Source: https://exa.ai/docs/reference/error-codes

Standard structure for API error responses, including fields for troubleshooting and programmatic handling.

```APIDOC
## Error Response Structure

### Description
Standard error format returned by the API. Include the `requestId` when contacting support for faster troubleshooting.

### Response
#### Error Response (400/401/402/403/500)
- **requestId** (string) - Unique identifier for the request.
- **error** (string) - Human-readable error message.
- **tag** (string) - Programmatic identifier for the error type.

### Response Example
{
  "requestId": "67207943fab9832d162b5317f4cca830",
  "error": "Invalid request body | Validation error: Invalid enum value...",
  "tag": "INVALID_REQUEST_BODY"
}
```

--------------------------------

### Deep Search Function Definition (OpenAI)

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Defines the 'exa_search_deep' function for OpenAI's API, outlining its parameters for deep web research, including query, search type, output schema, content retrieval options, and number of results. This is used for complex queries requiring synthesized answers with citations.

```json
{
  "type": "function",
  "function": {
    "name": "exa_search_deep",
    "description": "Deep web research via Exa. Searches, reads pages, and synthesizes findings with citations. Use when simple search isn't enough. Supports structured JSON output via outputSchema.",
    "parameters": {
      "type": "object",
      "properties": {
        "query": {
          "type": "string",
          "description": "Research question to investigate."
        },
        "type": {
          "type": "string",
          "enum": ["deep", "deep-reasoning"],
          "description": "'deep' (default, 4-12s) or 'deep-reasoning' (12-50s) for complex tasks."
        },
        "outputSchema": {
          "type": "object",
          "description": "Optional JSON Schema for structured output. Supports 'text' or 'object' type. Max depth: 2, max properties: 10."
        },
        "contents": {
          "type": "object",
          "description": "Content retrieval options.",
          "properties": {
            "text": {
              "type": "object",
              "properties": {
                "maxCharacters": {
                  "type": "integer",
                  "description": "Max characters of full text. Default: 15000."
                }
              }
            }
          }
        },
        "numResults": {
          "type": "integer",
          "description": "Number of results. Default: 10."
        }
      },
      "required": ["query"]
    }
  }
}
```

--------------------------------

### Claude Skill Configuration for Company Research

Source: https://exa.ai/docs/reference/company-research-claude-skill

YAML configuration for a Claude skill designed for company research using Exa search. It specifies the tool to use, operational constraints, and search tuning parameters.

```yaml
---
name: company-research
description: Company research using Exa search. Finds company info, competitors, news, tweets, financials, LinkedIn profiles, builds company lists. Use when researching companies, doing competitor analysis, market research, or building company lists.
context: fork
---

# Company Research

## Tool Restriction (Critical)

ONLY use `web_search_advanced_exa`. Do NOT use `web_search_exa` or any other Exa tools.

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents:
- Agent runs Exa search internally
- Agent processes results using LLM intelligence
- Agent returns only distilled output (compact JSON or brief markdown)
- Main context stays clean regardless of search volume

## Dynamic Tuning

No hardcoded numResults. Tune to user intent:
- User says "a few" → 10-20
- User says "comprehensive" → 50-100
- User specifies number → match it
- Ambiguous? Ask: "How many companies would you like?"

## Query Variation

Exa returns different results for different phrasings. For coverage:
- Generate 2-3 query variations
- Run in parallel
- Merge and deduplicate

## Categories

Use appropriate Exa `category` depending on what you need:
- `company` → homepages, rich metadata (headcount, location, funding, revenue)
- `news` → press coverage, announcements
- `tweet` → social presence, public commentary
- `people` → LinkedIn profiles (public data)
- No category (`type: "auto"`) → general web results, deep dives, broader context

Start with `category: "company"` for discovery, then use other categories or no category with `livecrawl: "fallback"` for deeper research.

### Category-Specific Filter Restrictions

When using `category: "company"`, these parameters cause 400 errors:
- `includeDomains` / `excludeDomains`
- `startPublishedDate` / `endPublishedDate`
- `startCrawlDate` / `endCrawlDate`

When searching without a category (or with `news`), domain and date filters work fine.

**Universal restriction:** `includeText` and `excludeText` only support **single-item arrays**. Multi-item arrays cause 400 errors across all categories.

## LinkedIn

Public LinkedIn via Exa: `category: "people"`, no other filters.
Auth-required LinkedIn → use Claude in Chrome browser fallback.

## Browser Fallback

Auto-fallback to Claude in Chrome when:
- Exa returns insufficient results
- Content is auth-gated
- Dynamic pages need JavaScript

## Examples

### Discovery: find companies in a space
```json
web_search_advanced_exa {
  "query": "AI infrastructure startups San Francisco",
  "category": "company",
  "numResults": 20,
  "type": "auto"
}
```

### Deep dive: research a specific company
```json
web_search_advanced_exa {
  "query": "Anthropic funding rounds valuation 2024",
  "type": "deep",
  "livecrawl": "fallback",
  "numResults": 10,
  "includeDomains": ["techcrunch.com", "crunchbase.com", "bloomberg.com"]
}
```

### News coverage
```json
web_search_advanced_exa {
  "query": "Anthropic AI safety",
  "category": "news",
  "numResults": 15,
  "startPublishedDate": "2024-01-01"
}
```

### LinkedIn profiles
```json
web_search_advanced_exa {
  "query": "VP Engineering AI infrastructure",
  "category": "people",
  "numResults": 20
}
```

## Output Format

Return:
1) Results (structured list; one company per row)
2) Sources (URLs; 1-line relevance each)
3) Notes (uncertainty/conflicts)

```

--------------------------------

### Research Event Schema

Source: https://exa.ai/docs/reference/research/create-a-task

Defines the structure for various research events including plan definitions and operational steps like thinking and searching.

```APIDOC
## Research Event Schema

### Description
This schema defines the structure for tracking research-related events, including plan definitions and specific operations performed during the research process.

### Parameters
#### Request Body
- **eventType** (string) - Required - The type of event (e.g., 'plan-definition', 'plan-operation')
- **researchId** (string) - Required - The unique identifier for the research request
- **createdAt** (number) - Required - Unix timestamp in milliseconds
- **planId** (string) - Optional - Identifier for the planning cycle
- **operationId** (string) - Optional - Unique identifier for a specific operation
- **data** (object) - Optional - Payload containing specific operation details (e.g., 'think' or 'search')

### Request Example
{
  "eventType": "plan-operation",
  "researchId": "res_123",
  "planId": "plan_456",
  "operationId": "op_789",
  "data": {
    "type": "search",
    "searchType": "neural",
    "query": "latest AI trends",
    "results": [{"url": "https://example.com"}],
    "pageTokens": 150
  }
}

### Response
#### Success Response (200)
- **status** (string) - Confirmation of event ingestion

#### Response Example
{
  "status": "success"
}
```

--------------------------------

### Search Web with EXA_SEARCH

Source: https://exa.ai/docs/reference/exa-for-sheets

The EXA_SEARCH function performs a semantic web search based on a query. It allows specifying the number of results, search type (neural, fast, auto), and optional prefix and suffix text. It returns an array of URLs.

```google-sheets
=EXA_SEARCH("startup funding rounds in AI sector 2024", 10, "neural")
```

--------------------------------

### Deep Search with Query Variations (Python)

Source: https://exa.ai/docs/reference/search

Performs a deep search to find information related to a query, with specific output schema requirements. This function is useful for structured data extraction.

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

results = exa.search("Who is the CEO of OpenAI?", {
    "type": "deep",
    "outputSchema": {
        "type": "object",
        "properties": {
            "leader": {"type": "string"},
            "title": {"type": "string"},
            "source_count": {"type": "number"}
        },
        "required": ["leader", "title"]
    },
    "contents":{"text": True}
})

print(results)
```

--------------------------------

### Search Results Schema

Source: https://exa.ai/docs/reference/answer

This section details the structure of the search result objects returned by the API.

```APIDOC
## Search Results Schema

This schema describes the fields available for each search result.

### Fields

- **title** (string) - The title of the search result.
  * Example: SpaceX valued at $350bn as company agrees to buy shares from ...
- **author** (string, nullable) - If available, the author of the content.
  * Example: Dan Milmon
- **publishedDate** (string, nullable) - An estimate of the creation date, from parsing HTML content. Format is YYYY-MM-DD.
  * Example: '2023-11-16T01:36:32.547Z'
- **text** (string) - The full text content of each source. Only present when includeText is enabled.
  * Example: SpaceX valued at $350bn as company agrees to buy shares from ...
- **image** (string, format: uri) - The URL of the image associated with the search result, if available.
  * Example: https://i.guim.co.uk/img/media/7cfee7e84b24b73c97a079c402642a333ad31e77/0_380_6176_3706/master/6176.jpg?width=1200&height=630&quality=85&auto=format&fit=crop&overlay-align=bottom%2Cleft&overlay-width=100p&overlay-base64=L2ltZy9zdGF0aWMvb3ZlcmxheXMvdGctZGVmYXVsdC5wbmc&enable=upscale&s=71ebb2fbf458c185229d02d380c01530
- **favicon** (string, format: uri) - The URL of the favicon for the search result's domain, if available.
  * Example: https://assets.guim.co.uk/static/frontend/icons/homescreen/apple-touch-icon.svg

```

--------------------------------

### Define Claude Tool Schema

Source: https://exa.ai/docs/reference/anthropic-tool-calling

Define the JSON structure required for Claude to understand and invoke custom functions, specifically for search operations.

```json
{
    "name": "my_function_name",
    "description": "The description of my function",
    "input_schema": {
        "type": "object",
        "properties": {
            "query": {
                "description": "The search query to perform."
            }
        },
        "required": ["query"]
    }
}
```

--------------------------------

### Domain-Specific Search API

Source: https://exa.ai/docs/reference/migrating-from-bing

Perform searches within specific domains to narrow down results to relevant websites.

```APIDOC
## POST /search

### Description
Searches for content within a specified list of domains.

### Method
POST

### Endpoint
https://api.exa.ai/search

### Parameters
#### Request Body
- **query** (string) - Required - The search query.
- **includeDomains** (array of strings) - Optional - A list of domains to include in the search (e.g., ["arxiv.org"]).
- **type** (string) - Optional - The search type, defaults to "auto".

### Request Example
```json
{
  "query": "transformers",
  "includeDomains": ["arxiv.org"],
  "type": "auto"
}
```

### Response
#### Success Response (200)
- **results** (array) - A list of search results from the specified domains.

#### Response Example
```json
{
  "results": [
    {
      "title": "Transformers Research Paper",
      "url": "http://arxiv.org/abs/12345",
      "domain": "arxiv.org"
    }
  ]
}
```
```

--------------------------------

### Plan Operation Event

Source: https://exa.ai/docs/reference/research/create-a-task

Represents an operation performed as part of a research plan, such as crawling a webpage.

```APIDOC
## Plan Operation Event

### Description
Represents an operation performed as part of a research plan, such as crawling a webpage.

### Event Type
`plan-operation`

### Data Structure
```json
{
  "eventType": "plan-operation",
  "planId": "string",
  "operationId": "string",
  "data": {
    "type": "object",
    "properties": {
      "result": {
        "type": ["object"],
        "properties": {
          "url": {
            "type": ["string"],
            "description": "The specific page that was crawled"
          }
        },
        "required": ["url"],
        "description": "The specific page that was crawled"
      },
      "pageTokens": {
        "type": ["number"],
        "description": "Token cost for processing the full page content"
      }
    },
    "required": ["type", "result", "pageTokens"]
  },
  "createdAt": "number",
  "researchId": "string"
}
```

### Required Fields
- `eventType`
- `planId`
- `operationId`
- `data`
- `createdAt`
- `researchId`
```

--------------------------------

### EXA_SEARCH Function for Google Sheets

Source: https://exa.ai/docs/reference/exa-for-sheets

The EXA_SEARCH function allows you to perform semantic web searches directly from Google Sheets. It takes a query and optional parameters for the number of results, search type, and text prefixes/suffixes. The function returns a vertical array of URLs that automatically populates adjacent cells.

```Google Apps Script
=EXA_SEARCH("latest developments in renewable energy", 5)
```

--------------------------------

### Rate Limit Error Response

Source: https://exa.ai/docs/reference/error-codes

Specific response format for 429 Too Many Requests errors.

```APIDOC
## Rate Limit Error

### Description
Returned when the client exceeds the allowed request rate.

### Response
#### Error Response (429)
- **error** (string) - Message indicating the rate limit has been exceeded.

### Response Example
{
  "error": "You've exceeded your Exa rate limit of 10 requests per second."
}
```

--------------------------------

### Answer Result Schema

Source: https://exa.ai/docs/reference/answer

Defines the structure of an answer result, including the generated answer and citations.

```APIDOC
## Answer Result Schema

### Description
Represents the result of an answer generation query, including the textual answer and any supporting citations.

### Schema
#### `AnswerResult` (object)
- **answer** (string | object) - The generated answer. Can be a string or a structured object if `outputSchema` is provided.
  - *Example*: "$350 billion."
- **citations** (array) - A list of citations used to generate the answer.
  - *Items*: `AnswerCitation` (object)

#### `AnswerCitation` (object)
- **id** (string) - A unique identifier for the citation document.
  - *Example*: "https://www.theguardian.com/science/2024/dec/11/spacex-valued-at-350bn-as-company-agrees-to-buy-shares-from-employees"
- **url** (string) - The URL of the source document.
  - *Example*: "https://www.theguardian.com/science/2024/dec/11/spacex-valued-at-350bn-as-company-agrees-to-buy-shares-from-employees"
```

--------------------------------

### Research Definition Event

Source: https://exa.ai/docs/reference/research/list-tasks

This event defines a research task, including instructions and expected output schema.

```APIDOC
## POST /research/define

### Description
Defines a new research task with specific instructions and an optional output schema.

### Method
POST

### Endpoint
/research/define

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'research-definition'.
- **instructions** (string) - Required - The complete research instructions.
- **outputSchema** (object) - Optional - The JSON Schema to validate the final output.
- **createdAt** (number) - Required - Unix timestamp in milliseconds when the event occurred.
- **researchId** (string) - Required - The unique identifier for the research request.

### Request Example
```json
{
  "eventType": "research-definition",
  "instructions": "Research the impact of AI on the job market.",
  "outputSchema": {
    "type": "object",
    "properties": {
      "summary": {"type": "string"},
      "job_growth": {"type": "number"}
    }
  },
  "createdAt": 1678886400000,
  "researchId": "res_12345"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Research definition received successfully."
}
```
```

--------------------------------

### Claude Skill Configuration for Research Paper Search

Source: https://exa.ai/docs/reference/research-paper-search-claude-skill

Defines a Claude skill named 'web-search-advanced-research-paper' that utilizes the Exa advanced search tool for academic content. It specifies tool restrictions, supported filters, and usage guidelines.

```yaml
---
name: web-search-advanced-research-paper
description: Search for research papers and academic content using Exa advanced search. Full filter support including date ranges and text filtering. Use when searching for academic papers, arXiv preprints, or scientific research.
context: fork
---

# Web Search Advanced - Research Paper Category

## Tool Restriction (Critical)

ONLY use `web_search_advanced_exa` with `category: "research paper"`. Do NOT use other categories or tools.

## Full Filter Support

The `research paper` category supports ALL available parameters:

### Core
- `query` (required)
- `numResults`
- `type` ("auto", "fast", "deep", "neural")

### Domain filtering
- `includeDomains` (e.g., ["arxiv.org", "openreview.net"])
- `excludeDomains`

### Date filtering (ISO 8601)
- `startPublishedDate` / `endPublishedDate`
- `startCrawlDate` / `endCrawlDate`

### Text filtering
- `includeText` (must contain ALL)
- `excludeText` (exclude if ANY match)

**Array size restriction:** `includeText` and `excludeText` only support **single-item arrays**. Multi-item arrays (2+ items) cause 400 errors. To match multiple terms, put them in the `query` string or run separate searches.

### Content extraction
- `textMaxCharacters` / `contextMaxCharacters`
- `enableSummary` / `summaryQuery`
- `enableHighlights` / `highlightsNumSentences` / `highlightsPerUrl` / `highlightsQuery`

### Additional
- `userLocation`
- `moderation`
- `additionalQueries`
- `livecrawl` / `livecrawlTimeout`
- `subpages` / `subpageTarget`

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents:
- Agent calls `web_search_advanced_exa` with `category: "research paper"`
- Agent merges + deduplicates results before presenting
- Agent returns distilled output (brief markdown or compact JSON)
- Main context stays clean regardless of search volume

## When to Use

Use this category when you need:
- Academic papers from arXiv, OpenReview, PubMed, etc.
- Scientific research on specific topics
- Literature reviews with date filtering
- Papers containing specific methodologies or terms

```

--------------------------------

### Perform Advanced Search with Filters

Source: https://exa.ai/docs/reference/search

Performs a search with specific categories, moderation, and content extraction settings like summaries and subpages. Available via REST API, Python, and JavaScript.

```bash
curl --request POST \
  --url https://api.exa.ai/search \
  --header 'x-api-key: <token>' \
  --header 'Content-Type: application/json' \
  --data '{
  "query": "Latest research in LLMs",
  "type": "auto",
  "category": "research paper",
  "numResults": 10,
  "moderation": true,
  "contents": {
    "text": true,
    "summary": {
      "query": "Main developments"
    },
    "subpages": 1,
    "subpageTarget": "sources",
    "extras": {
      "links": 1,
      "imageLinks": 1
    }
  }
}'
```

```python
# pip install exa-py
from exa_py import Exa
exa = Exa('YOUR_EXA_API_KEY')

results = exa.search_and_contents(
    "Latest research in LLMs",
    type="auto",
    category="research paper",
    num_results=10,
    moderation=True,
    text=True,
    summary={
        "query": "Main developments"
    },
    subpages=1,
    subpage_target="sources",
    extras={
        "links": 1,
        "image_links": 1
    }
)

print(results)
```

```javascript
// npm install exa-js
import Exa from 'exa-js';
const exa = new Exa('YOUR_EXA_API_KEY');

const results = await exa.searchAndContents('Latest research in LLMs', {
    type: 'auto',
    category: 'research paper',
    numResults: 10,
    moderation: true,
    contents: {
        text: true,
        summary: {
            query: 'Main developments'
        },
        subpages: 1,
        subpageTarget: 'sources',
        extras: {
            links: 1,
            imageLinks: 1
        }
    }
});

console.log(results);
```

--------------------------------

### Configure Claude Skill for Financial Reports

Source: https://exa.ai/docs/reference/financial-report-search-claude-skill

YAML configuration for a Claude skill named 'web-search-advanced-financial-report'. This skill utilizes the Exa advanced search with a specific category for financial documents.

```yaml
---
name: web-search-advanced-financial-report
description: Search for financial reports using Exa advanced search. Near-full filter support for finding SEC filings, earnings reports, and financial documents. Use when searching for 10-K filings, quarterly earnings, or annual reports.
context: fork
---

# Web Search Advanced - Financial Report Category

## Tool Restriction (Critical)

ONLY use `web_search_advanced_exa` with `category: "financial report"`. Do NOT use other categories or tools.

## Filter Restrictions (Critical)

The `financial report` category has one known restriction:

- `excludeText` - NOT SUPPORTED (causes 400 error)

## Supported Parameters

### Core
- `query` (required)
- `numResults`
- `type` ("auto", "fast", "deep", "neural")

### Domain filtering
- `includeDomains` (e.g., ["sec.gov", "investor.apple.com"])
- `excludeDomains`

### Date filtering (ISO 8601) - Very useful for financial reports!
- `startPublishedDate` / `endPublishedDate`
- `startCrawlDate` / `endCrawlDate`

### Text filtering
- `includeText` (must contain ALL) - **single-item arrays only**; multi-item causes 400
- ~~`excludeText`~~

### Content extraction
- `textMaxCharacters` / `contextMaxCharacters`
- `enableSummary` / `summaryQuery`
- `enableHighlights` / `highlightsNumSentences` / `highlightsPerUrl` / `highlightsQuery`

### Additional
- `additionalQueries`
- `livecrawl` / `livecrawlTimeout`
- `subpages` / `subpageTarget`

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents:
- Agent calls `web_search_advanced_exa` with `category: "financial report"`
- Agent merges + deduplicates results before presenting
- Agent returns distilled output (brief markdown or compact JSON)
- Main context stays clean regardless of search volume

## When to Use

Use this category when you need:
- SEC filings (10-K, 10-Q, 8-K, S-1)
- Quarterly earnings reports
- Annual reports
- Investor presentations
- Financial statements

## Output Format

Return:
1) Results (company name, filing type, date, key figures/highlights)
2) Sources (Filing URLs)
3) Notes (reporting period, any restatements, auditor notes)

```

--------------------------------

### Standard API Error Response Structure

Source: https://exa.ai/docs/reference/error-codes

The standard error response format used for most API errors. It includes a unique requestId for support tracking, a descriptive error message, and a programmatic error tag.

```json
{
  "requestId": "67207943fab9832d162b5317f4cca830",
  "error": "Invalid request body | Validation error: Invalid enum value. Expected 'never' | 'always' | 'fallback' | 'auto' | 'preferred' | 'fallback1.6', received 'alwayss' at \"livecrawl\"",
  "tag": "INVALID_REQUEST_BODY"
}
```

--------------------------------

### Task Operation Event

Source: https://exa.ai/docs/reference/research/list-tasks

Represents a generic operation event triggered during the execution of a research task.

```APIDOC
## POST /tasks/operations

### Description
Logs a specific operation event associated with a research task.

### Method
POST

### Endpoint
/tasks/operations

### Parameters
#### Request Body
- **eventType** (string) - Required - The type of operation event.
- **planId** (string) - Required - The ID of the plan owning the task.
- **taskId** (string) - Required - The ID of the task.
- **operationId** (string) - Required - Unique identifier for the operation.
- **data** (object) - Required - Metadata associated with the operation.
- **createdAt** (number) - Required - Unix timestamp in milliseconds.
- **researchId** (string) - Required - The research request ID.

### Request Example
{
  "eventType": "operation-start",
  "planId": "plan_123",
  "taskId": "task_456",
  "operationId": "op_789",
  "data": {},
  "createdAt": 1672531200000,
  "researchId": "res_001"
}
```

--------------------------------

### Define Research Status Schema

Source: https://exa.ai/docs/reference/research/get-a-task

Defines the structure for research objects in canceled or failed states. These schemas include metadata like researchId, model, timestamps, and specific status-related fields like error messages.

```json
{
  "type": "object",
  "properties": {
    "researchId": { "type": "string" },
    "status": { "enum": ["canceled", "failed"] },
    "error": { "type": "string" },
    "finishedAt": { "type": "number" }
  },
  "required": ["researchId", "status", "finishedAt"]
}
```

--------------------------------

### Deep Search Function Definition (Anthropic)

Source: https://exa.ai/docs/reference/tool-calling-best-practices

Defines the 'exa_search_deep' function for Anthropic's API, specifying the input schema for deep web research. It includes parameters for the query, search type, output schema, content retrieval, and number of results, facilitating complex research with structured outputs.

```json
{
  "name": "exa_search_deep",
  "description": "Deep web research via Exa. Searches, reads pages, and synthesizes findings with citations. Use when simple search isn't enough. Supports structured JSON output via outputSchema.",
  "input_schema": {
    "type": "object",
    "properties": {
      "query": {
        "type": "string",
        "description": "Research question to investigate."
      },
      "type": {
        "type": "string",
        "enum": ["deep", "deep-reasoning"],
        "description": "'deep' (default, 4-12s) or 'deep-reasoning' (12-50s) for complex tasks."
      },
      "outputSchema": {
        "type": "object",
        "description": "Optional JSON Schema for structured output. Supports 'text' or 'object' type. Max depth: 2, max properties: 10."
      },
      "contents": {
        "type": "object",
        "description": "Content retrieval options.",
        "properties": {
          "text": {
            "type": "object",
            "properties": {
              "maxCharacters": {
                "type": "integer",
                "description": "Max characters of full text. Default: 15000."
              }
            }
          }
        }
      },
      "numResults": {
        "type": "integer",
        "description": "Number of results. Default: 10."
      }
    },
    "required": ["query"]
  }
}
```

--------------------------------

### POST /web_search_advanced_exa

Source: https://exa.ai/docs/reference/people-search-claude-skill

Executes an advanced search query using the Exa search engine, optimized for people discovery and professional research.

```APIDOC
## POST web_search_advanced_exa

### Description
Performs a targeted search to find LinkedIn profiles, professional backgrounds, and public bios. This tool is designed for use within Task agents to maintain context cleanliness.

### Method
POST

### Endpoint
web_search_advanced_exa

### Parameters
#### Request Body
- **query** (string) - Required - The search query string.
- **category** (string) - Optional - The search category (e.g., "people", "news", "personal site"). Note: "people" category restricts certain filters.
- **numResults** (integer) - Optional - Number of results to return (tuned based on user intent).
- **type** (string) - Optional - Search type (e.g., "auto", "deep").
- **livecrawl** (string) - Optional - Set to "fallback" for deeper research on specific individuals.
- **additionalQueries** (array) - Optional - List of query variations for parallel execution.
- **startPublishedDate** (string) - Optional - Filter by date (ISO 8601). Not compatible with "people" category.

### Request Example
{
  "query": "VP Engineering AI infrastructure",
  "category": "people",
  "numResults": 20,
  "type": "auto"
}

### Response
#### Success Response (200)
- **results** (array) - List of objects containing name, title, company, and location.
- **sources** (array) - List of profile URLs.
- **notes** (string) - Summary of profile completeness and verification status.

#### Response Example
{
  "results": [
    {
      "name": "John Doe",
      "title": "VP Engineering",
      "company": "Tech Corp",
      "location": "San Francisco"
    }
  ],
  "sources": ["https://linkedin.com/in/johndoe"],
  "notes": "Profile verified via public bio."
}
```

--------------------------------

### Research Output Event

Source: https://exa.ai/docs/reference/research/get-a-task

Defines the schema for a research-output event, which includes either a successful completion with cost metrics or a failure status.

```APIDOC
## Research Output Event

### Description
Represents the final state of a research request, containing metadata, cost analysis, and the resulting content or error details.

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'research-output'
- **researchId** (string) - Required - The unique identifier for the research request
- **createdAt** (number) - Required - Unix timestamp in milliseconds
- **output** (object) - Required - The result object containing either 'Completed' or 'Failed' data

### Response
#### Success Response (200)
- **outputType** (string) - 'completed' or 'failed'
- **costDollars** (object) - Contains total, numSearches, numPages, and reasoningTokens
- **content** (string) - The research output text
- **parsed** (object) - Structured JSON if outputSchema was provided

### Response Example
{
  "eventType": "research-output",
  "researchId": "res_123",
  "createdAt": 1672531200000,
  "output": {
    "outputType": "completed",
    "costDollars": {
      "total": 0.05,
      "numSearches": 2,
      "numPages": 5,
      "reasoningTokens": 150
    },
    "content": "Research findings..."
  }
}
```

--------------------------------

### Deep Search with Query Variations

Source: https://exa.ai/docs/reference/search

Perform a 'deep' search that attempts to extract specific structured information based on a defined output schema.

```APIDOC
## POST /search

### Description
Performs a 'deep' search designed to extract specific structured information from search results based on a provided output schema.

### Method
POST

### Endpoint
https://api.exa.ai/search

### Parameters
#### Query Parameters
None

#### Request Body
- **query** (string) - Required - The search query.
- **type** (string) - Required - Set to 'deep' for this search type.
- **outputSchema** (object) - Required - Defines the structure of the expected output.
  - **type** (string) - The type of the schema (e.g., 'object', 'array').
  - **properties** (object) - Defines the properties of the object schema.
    - **fieldName** (object) - Defines a specific field within the schema.
      - **type** (string) - The data type of the field (e.g., 'string', 'number', 'boolean').
  - **required** (array) - List of required fields in the output.
- **contents** (object) - Optional - Specifies what content to retrieve.
  - **text** (boolean) - Optional - Whether to retrieve the text content.

### Request Example
```json
{
  "query": "Who is the CEO of OpenAI?",
  "type": "deep",
  "outputSchema": {
    "type": "object",
    "properties": {
      "leader": { "type": "string" },
      "title": { "type": "string" },
      "sourceCount": { "type": "number" }
    },
    "required": ["leader", "title"]
  },
  "contents": {
    "text": true
  }
}
```

### Response
#### Success Response (200)
- **results** (array) - List of search results, structured according to the `outputSchema`.

#### Response Example
```json
{
  "results": [
    {
      "leader": "Sam Altman",
      "title": "CEO",
      "sourceCount": 5
    }
  ]
}
```
```

--------------------------------

### Rate Limit Error Response Structure

Source: https://exa.ai/docs/reference/error-codes

The simplified error response format returned when a client exceeds their rate limit (HTTP 429). It contains only an error message field.

```json
{
  "error": "You've exceeded your Exa rate limit of 10 requests per second. If you want this increased, please email hello@exa.ai :)"
}
```

--------------------------------

### POST /web_search_advanced_exa

Source: https://exa.ai/docs/reference/company-research-claude-skill

The primary tool for performing advanced web searches. It supports various categories and filtering options to retrieve company data, news, and social information.

```APIDOC
## POST web_search_advanced_exa

### Description
Performs a search using the Exa search engine. This tool is optimized for company research, competitor analysis, and general web discovery.

### Method
POST

### Endpoint
web_search_advanced_exa

### Parameters
#### Request Body
- **query** (string) - Required - The search query string.
- **category** (string) - Optional - The type of search: "company", "news", "tweet", "people".
- **numResults** (integer) - Optional - Number of results to return (10-100 recommended).
- **type** (string) - Optional - Search mode: "auto" or "deep".
- **livecrawl** (string) - Optional - Set to "fallback" for deep research on dynamic pages.
- **includeDomains** (array) - Optional - List of domains to include (Not supported with category: "company").
- **excludeDomains** (array) - Optional - List of domains to exclude (Not supported with category: "company").
- **startPublishedDate** (string) - Optional - ISO date string (Not supported with category: "company").
- **includeText** (array) - Optional - Single-item array of text to include.
- **excludeText** (array) - Optional - Single-item array of text to exclude.

### Request Example
{
  "query": "AI infrastructure startups San Francisco",
  "category": "company",
  "numResults": 20,
  "type": "auto"
}

### Response
#### Success Response (200)
- **results** (array) - List of found entities or web pages.
- **sources** (array) - List of URLs used for the research.
- **notes** (string) - Any uncertainty or conflicting data found during research.

#### Response Example
{
  "results": [{"name": "Example AI", "location": "San Francisco"}],
  "sources": ["https://example.com"],
  "notes": "Data based on recent funding rounds."
}
```

--------------------------------

### Research Output Event

Source: https://exa.ai/docs/reference/research/list-tasks

This event represents the result of a research task, either completed successfully or failed.

```APIDOC
## POST /research/output

### Description
Receives the output of a research task, which can be a successful completion or a failure.

### Method
POST

### Endpoint
/research/output

### Parameters
#### Request Body
- **eventType** (string) - Required - Must be 'research-output'.
- **output** (object) - Required - The result of the research.
  - **outputType** (string) - Required - Enum: 'completed' or 'failed'.
  - **costDollars** (object) - Required if outputType is 'completed' - Cost details.
    - **total** (number) - Required - Total cost in USD.
    - **numSearches** (number) - Required - Number of web searches performed.
    - **numPages** (number) - Required - Number of web pages crawled.
    - **reasoningTokens** (number) - Required - Total AI tokens used for reasoning.
  - **content** (string) - Required - The research output as text.
  - **parsed** (object) - Optional - Structured JSON object matching the outputSchema, if provided.
  - **error** (string) - Required if outputType is 'failed' - Detailed error message.
- **createdAt** (number) - Required - Unix timestamp in milliseconds when the event occurred.
- **researchId** (string) - Required - The unique identifier for the research request.

### Request Example (Success)
```json
{
  "eventType": "research-output",
  "output": {
    "outputType": "completed",
    "costDollars": {
      "total": 5.50,
      "numSearches": 10,
      "numPages": 5,
      "reasoningTokens": 1000
    },
    "content": "AI is projected to create more jobs than it displaces...",
    "parsed": {
      "summary": "AI's net effect on jobs is positive...",
      "job_growth": 1.2
    }
  },
  "createdAt": 1678887000000,
  "researchId": "res_12345"
}
```

### Request Example (Failure)
```json
{
  "eventType": "research-output",
  "output": {
    "outputType": "failed",
    "error": "Failed to access the requested data source."
  },
  "createdAt": 1678887000000,
  "researchId": "res_12345"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Research output received successfully."
}
```
```

--------------------------------

### Claude Skill Definition for Twitter Search

Source: https://exa.ai/docs/reference/x-search-claude-skill

Defines a Claude skill named 'web-search-advanced-tweet' for searching X/Twitter content. It specifies tool restrictions, filter limitations, supported parameters, and usage guidelines.

```yaml
---
name: web-search-advanced-tweet
description: Search tweets and Twitter/X content using Exa advanced search. Limited filter support - text and domain filters are NOT supported. Use when searching for tweets, Twitter/X discussions, or social media sentiment.
context: fork
---

# Web Search Advanced - Tweet Category

## Tool Restriction (Critical)

ONLY use `web_search_advanced_exa` with `category: "tweet"`. Do NOT use other categories or tools.

## Filter Restrictions (Critical)

The `tweet` category has **LIMITED filter support**. The following parameters are **NOT supported** and will cause 400 errors:

- `includeText` - NOT SUPPORTED
- `excludeText` - NOT SUPPORTED
- `includeDomains` - NOT SUPPORTED
- `excludeDomains` - NOT SUPPORTED
- `moderation` - NOT SUPPORTED (causes 500 server error)

## Supported Parameters

### Core
- `query` (required)
- `numResults`
- `type` ("auto", "fast", "deep", "neural")

### Date filtering (ISO 8601) - Use these instead of text filters!
- `startPublishedDate` / `endPublishedDate`
- `startCrawlDate` / `endCrawlDate`

### Content extraction
- `textMaxCharacters` / `contextMaxCharacters`
- `enableHighlights` / `highlightsNumSentences` / `highlightsPerUrl` / `highlightsQuery`
- `enableSummary` / `summaryQuery`

### Additional
- `additionalQueries` - useful for hashtag variations
- `livecrawl` / `livecrawlTimeout` - use "preferred" for recent tweets

## Token Isolation (Critical)

Never run Exa searches in main context. Always spawn Task agents:
- Agent calls `web_search_advanced_exa` with `category: "tweet"`
- Agent merges + deduplicates results before presenting
- Agent returns distilled output (brief markdown or compact JSON)
- Main context stays clean regardless of search volume

## When to Use

Use this category when you need:
- Social discussions on a topic
- Product announcements from company accounts
- Developer opinions and experiences
- Trending topics and community sentiment
- Expert takes and threads

```

--------------------------------

### Research Polling API

Source: https://exa.ai/docs/reference/exa-research

Polls the status of an ongoing research task and retrieves the results once completed. This is used in conjunction with the research initiation endpoint.

```APIDOC
## Research Polling API

### Description
Polls the status of an ongoing research task and retrieves the results once completed. This is used in conjunction with the research initiation endpoint.

### Method
GET

### Endpoint
https://api.exa.ai/research/v1/poll/{researchId}

### Parameters
#### Path Parameters
- **researchId** (string) - Required - The ID of the research task to poll.

### Request Example
```bash
curl -X GET https://api.exa.ai/research/v1/poll/res_abcdef1234567890 \
  -H "x-api-key: $EXA_API_KEY"
```

### Response
#### Success Response (200)
- **status** (string) - The current status of the research task (e.g., 'RUNNING', 'COMPLETED', 'FAILED').
- **result** (object) - The research results, structured according to the `outputSchema` if provided during initiation. This field is only present if the status is 'COMPLETED'.

#### Response Example
```json
{
  "status": "COMPLETED",
  "result": {
    "gpus": [
      {
        "manufacturer": "NVIDIA",
        "model": "RTX 4090",
        "msrpUsd": 1599,
        "tdpWatts": 450,
        "launchDate": "2022-10-12"
      },
      {
        "manufacturer": "AMD",
        "model": "RX 7900 XTX",
        "msrpUsd": 999,
        "tdpWatts": 355,
        "launchDate": "2022-12-13"
      }
    ]
  }
}
```
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.