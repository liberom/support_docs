# gws - Google Workspace CLI

`gws` is a unified command-line interface for all Google Workspace APIs, built for both humans and AI agents. It dynamically discovers API endpoints from Google's Discovery Service at runtime, meaning it automatically supports new API features without requiring updates. The CLI provides structured JSON output, auto-pagination, multipart uploads, and 100+ pre-built agent skills for common workflows across Drive, Gmail, Calendar, Sheets, Docs, Chat, and other Workspace services.

The project is designed to eliminate boilerplate when working with Google APIs. Instead of writing curl commands or custom API clients, developers can use intuitive CLI syntax with built-in authentication, request validation via `--dry-run`, and multiple output formats (JSON, YAML, CSV, table). For AI agent integration, the included SKILL.md files provide structured documentation that LLMs can parse to autonomously manage Google Workspace operations.

## Authentication

### Interactive OAuth Login

Browser-based OAuth authentication for desktop environments with credentials encrypted at rest using AES-256-GCM.

```bash
# One-time setup: creates GCP project, enables APIs, and logs you in
gws auth setup

# Subsequent logins with scope selection
gws auth login

# Login with specific services only (recommended for unverified apps)
gws auth login -s drive,gmail,sheets

# Export credentials for headless/CI environments
gws auth export --unmasked > credentials.json
```

### Environment Variable Authentication

Configure authentication via environment variables for CI/CD pipelines and server deployments.

```bash
# Use a pre-obtained access token (highest priority)
export GOOGLE_WORKSPACE_CLI_TOKEN=$(gcloud auth print-access-token)

# Use exported credentials file
export GOOGLE_WORKSPACE_CLI_CREDENTIALS_FILE=/path/to/credentials.json

# Service account authentication
export GOOGLE_APPLICATION_CREDENTIALS=/path/to/service-account.json

# Run any gws command - authentication is automatic
gws drive files list --params '{"pageSize": 5}'
```

## Google Drive API

### List Files

Retrieve files from Google Drive with pagination and filtering support.

```bash
# List the 10 most recent files
gws drive files list --params '{"pageSize": 10}'

# List files with a specific query filter
gws drive files list --params '{"q": "mimeType=\"application/pdf\"", "pageSize": 20}'

# Auto-paginate through all results (NDJSON output)
gws drive files list --params '{"pageSize": 100}' --page-all | jq -r '.files[].name'

# List files in a specific folder
gws drive files list --params '{"q": "\"FOLDER_ID\" in parents", "pageSize": 50}'

# Output as table format for human readability
gws drive files list --params '{"pageSize": 5}' --format table
```

### Upload Files

Upload files to Google Drive with automatic MIME type detection and metadata handling.

```bash
# Simple file upload (MIME type auto-detected)
gws drive +upload ./report.pdf

# Upload to a specific folder
gws drive +upload ./report.pdf --parent FOLDER_ID

# Upload with custom filename
gws drive +upload ./data.csv --name 'Sales Data Q1 2024.csv'

# Upload and convert to Google Docs format
gws drive files create \
  --json '{"name": "My Doc", "mimeType": "application/vnd.google-apps.document"}' \
  --upload notes.md
```

### Create and Manage Files

Create files, folders, and manage file metadata using the Drive API.

```bash
# Create a new folder
gws drive files create --json '{"name": "Project Docs", "mimeType": "application/vnd.google-apps.folder"}'

# Copy a file
gws drive files copy --params '{"fileId": "FILE_ID"}' --json '{"name": "Copy of Document"}'

# Get file metadata
gws drive files get --params '{"fileId": "FILE_ID", "fields": "id,name,mimeType,size,createdTime"}'

# Download a file
gws drive files get --params '{"fileId": "FILE_ID", "alt": "media"}' -o ./downloaded-file.pdf

# Delete a file (moves to trash)
gws drive files update --params '{"fileId": "FILE_ID"}' --json '{"trashed": true}'
```

### Share Files and Manage Permissions

Control access to files and folders by creating and managing permissions.

```bash
# Share a file with a specific user (writer access)
gws drive permissions create \
  --params '{"fileId": "FILE_ID"}' \
  --json '{"type": "user", "role": "writer", "emailAddress": "alice@example.com"}'

# Share with anyone who has the link (reader access)
gws drive permissions create \
  --params '{"fileId": "FILE_ID"}' \
  --json '{"type": "anyone", "role": "reader"}'

# List permissions on a file
gws drive permissions list --params '{"fileId": "FILE_ID"}'

# Remove a permission
gws drive permissions delete --params '{"fileId": "FILE_ID", "permissionId": "PERMISSION_ID"}'
```

## Gmail API

### Send Email

Send emails with support for attachments, CC/BCC, HTML content, and send-as aliases.

```bash
# Send a simple plain text email
gws gmail +send --to alice@example.com --subject 'Hello' --body 'Hi Alice!'

# Send with CC and BCC recipients
gws gmail +send \
  --to alice@example.com \
  --cc bob@example.com \
  --bcc manager@example.com \
  --subject 'Project Update' \
  --body 'Please see the attached report.'

# Send HTML email
gws gmail +send \
  --to alice@example.com \
  --subject 'Newsletter' \
  --body '<h1>Welcome</h1><p>Thanks for subscribing!</p>' \
  --html

# Send with attachments (multiple files supported)
gws gmail +send \
  --to alice@example.com \
  --subject 'Report' \
  --body 'See attached' \
  -a report.pdf \
  -a data.xlsx

# Send from an alias address
gws gmail +send \
  --to alice@example.com \
  --subject 'From Sales' \
  --body 'Hi!' \
  --from sales@company.com
```

### Reply and Forward Messages

Handle email threads with automatic threading and recipient management.

```bash
# Reply to a message (threading handled automatically)
gws gmail +reply --message-id MESSAGE_ID --body 'Thanks for the update!'

# Reply-all to a message
gws gmail +reply-all --message-id MESSAGE_ID --body 'Acknowledged, thanks everyone.'

# Forward a message to new recipients
gws gmail +forward --message-id MESSAGE_ID --to manager@example.com --body 'FYI - see below'

# Read a message and extract body/headers
gws gmail +read --message-id MESSAGE_ID
gws gmail +read --message-id MESSAGE_ID --format json
```

### Triage and Search Email

View inbox summary and search for messages using Gmail query syntax.

```bash
# Show unread inbox summary (sender, subject, date)
gws gmail +triage

# List messages matching a query
gws gmail users messages list --params '{"userId": "me", "q": "from:alice@example.com is:unread"}'

# Get full message content
gws gmail users messages get --params '{"userId": "me", "id": "MESSAGE_ID", "format": "full"}'

# List messages with pagination
gws gmail users messages list --params '{"userId": "me", "maxResults": 50}' --page-all
```

### Watch for New Emails

Stream new emails in real-time using Pub/Sub push notifications.

```bash
# Watch for new emails and stream as NDJSON
gws gmail +watch --subscription projects/PROJECT_ID/subscriptions/SUBSCRIPTION_NAME

# Watch with custom output directory for messages
gws gmail +watch \
  --subscription projects/PROJECT_ID/subscriptions/gmail-watch \
  --output-dir ./incoming-emails \
  --msg-format full
```

## Google Sheets API

### Read Spreadsheet Data

Read values from spreadsheets with range selection and formatting options.

```bash
# Read cells from a range (use double quotes for zsh compatibility)
gws sheets +read --spreadsheet SPREADSHEET_ID --range "Sheet1!A1:D10"

# Read using the raw API with more options
gws sheets spreadsheets values get \
  --params '{"spreadsheetId": "SPREADSHEET_ID", "range": "Sheet1!A1:C10"}'

# Get spreadsheet metadata
gws sheets spreadsheets get --params '{"spreadsheetId": "SPREADSHEET_ID"}'

# Read multiple ranges at once
gws sheets spreadsheets values batchGet \
  --params '{"spreadsheetId": "SPREADSHEET_ID", "ranges": ["Sheet1!A1:B5", "Sheet2!A1:C3"]}'
```

### Write and Append Data

Write values to spreadsheets with support for bulk operations and formulas.

```bash
# Append a single row (comma-separated values)
gws sheets +append --spreadsheet SPREADSHEET_ID --values 'Alice,95,true'

# Append multiple rows (JSON format)
gws sheets +append --spreadsheet SPREADSHEET_ID --json-values '[["Name","Score"],["Alice",95],["Bob",87]]'

# Update a specific range
gws sheets spreadsheets values update \
  --params '{"spreadsheetId": "SPREADSHEET_ID", "range": "Sheet1!A1", "valueInputOption": "USER_ENTERED"}' \
  --json '{"values": [["Header1", "Header2"], ["Value1", "Value2"]]}'

# Batch update multiple ranges
gws sheets spreadsheets values batchUpdate \
  --params '{"spreadsheetId": "SPREADSHEET_ID"}' \
  --json '{
    "valueInputOption": "USER_ENTERED",
    "data": [
      {"range": "Sheet1!A1", "values": [["Updated"]]},
      {"range": "Sheet1!B1", "values": [["Also Updated"]]}
    ]
  }'
```

### Create Spreadsheets

Create new spreadsheets with custom properties and initial data.

```bash
# Create a new spreadsheet
gws sheets spreadsheets create --json '{"properties": {"title": "Q1 Budget 2024"}}'

# Create with multiple sheets
gws sheets spreadsheets create --json '{
  "properties": {"title": "Sales Tracker"},
  "sheets": [
    {"properties": {"title": "January"}},
    {"properties": {"title": "February"}},
    {"properties": {"title": "Summary"}}
  ]
}'
```

## Google Calendar API

### Create Events

Create calendar events with attendees, locations, and Google Meet integration.

```bash
# Create a simple event
gws calendar +insert \
  --summary 'Team Standup' \
  --start '2024-06-17T09:00:00-07:00' \
  --end '2024-06-17T09:30:00-07:00'

# Create event with attendees
gws calendar +insert \
  --summary 'Project Review' \
  --start '2024-06-17T14:00:00-07:00' \
  --end '2024-06-17T15:00:00-07:00' \
  --attendee alice@example.com \
  --attendee bob@example.com

# Create event with Google Meet link
gws calendar +insert \
  --summary 'Remote Meeting' \
  --start '2024-06-17T10:00:00-07:00' \
  --end '2024-06-17T11:00:00-07:00' \
  --meet

# Create event with location and description
gws calendar +insert \
  --summary 'Client Lunch' \
  --start '2024-06-17T12:00:00-07:00' \
  --end '2024-06-17T13:30:00-07:00' \
  --location '123 Main St, San Francisco, CA' \
  --description 'Discuss Q2 partnership opportunities'
```

### View Agenda and List Events

View upcoming events and manage your calendar schedule.

```bash
# Show today's agenda (uses Google account timezone automatically)
gws calendar +agenda

# Show agenda for a specific day
gws calendar +agenda --today

# Show agenda in a specific timezone
gws calendar +agenda --today --timezone America/New_York

# List events using the raw API with custom time range
gws calendar events list \
  --params '{
    "calendarId": "primary",
    "timeMin": "2024-06-01T00:00:00Z",
    "timeMax": "2024-06-30T23:59:59Z",
    "singleEvents": true,
    "orderBy": "startTime"
  }'

# Query free/busy information
gws calendar freebusy query \
  --json '{
    "timeMin": "2024-06-17T08:00:00Z",
    "timeMax": "2024-06-17T18:00:00Z",
    "items": [{"id": "primary"}, {"id": "colleague@example.com"}]
  }'
```

### Update and Delete Events

Modify existing calendar events or remove them.

```bash
# Update an event (patch semantics)
gws calendar events patch \
  --params '{"calendarId": "primary", "eventId": "EVENT_ID"}' \
  --json '{"summary": "Updated Meeting Title", "location": "Conference Room B"}'

# Move an event to a different time
gws calendar events patch \
  --params '{"calendarId": "primary", "eventId": "EVENT_ID"}' \
  --json '{
    "start": {"dateTime": "2024-06-18T10:00:00-07:00"},
    "end": {"dateTime": "2024-06-18T11:00:00-07:00"}
  }'

# Delete an event
gws calendar events delete --params '{"calendarId": "primary", "eventId": "EVENT_ID"}'
```

## Google Docs API

### Write to Documents

Append text content to Google Docs documents.

```bash
# Append text to a document
gws docs +write --document DOC_ID --text 'Hello, world!'

# Append multiple paragraphs
gws docs +write --document DOC_ID --text 'First paragraph.

Second paragraph with more content.'
```

### Read and Update Documents

Access document content and apply batch updates for rich formatting.

```bash
# Get document content
gws docs documents get --params '{"documentId": "DOC_ID"}'

# Batch update with insertText request
gws docs documents batchUpdate \
  --params '{"documentId": "DOC_ID"}' \
  --json '{
    "requests": [
      {
        "insertText": {
          "location": {"index": 1},
          "text": "Inserted at beginning\n"
        }
      }
    ]
  }'
```

## Google Chat API

### Send Messages

Send messages to Google Chat spaces and manage conversations.

```bash
# Send a plain text message to a space
gws chat +send --space spaces/AAAAxxxx --text 'Hello team!'

# List available spaces to find space names
gws chat spaces list

# Send message using the raw API (for cards/advanced formatting)
gws chat spaces messages create \
  --params '{"parent": "spaces/AAAAxxxx"}' \
  --json '{"text": "Deploy complete. All systems operational."}'

# Preview a message without sending (dry run)
gws chat spaces messages create \
  --params '{"parent": "spaces/AAAAxxxx"}' \
  --json '{"text": "Test message"}' \
  --dry-run
```

## Workflow Helpers

### Productivity Workflows

Cross-service helpers that combine multiple Google Workspace APIs for common tasks.

```bash
# Morning standup summary: today's meetings + open tasks
gws workflow +standup-report

# Prepare for your next meeting: agenda, attendees, linked docs
gws workflow +meeting-prep

# Convert a Gmail message into a Google Tasks entry
gws workflow +email-to-task --message-id MESSAGE_ID

# Weekly digest: this week's meetings + unread email count
gws workflow +weekly-digest

# Announce a Drive file in a Chat space
gws workflow +file-announce --file-id FILE_ID --space spaces/AAAAxxxx
```

## API Schema Introspection

### Discover API Methods

Inspect API schemas to understand parameters, request bodies, and response formats before making calls.

```bash
# List all resources and methods for a service
gws drive --help
gws gmail --help
gws sheets --help

# Get detailed schema for a specific method
gws schema drive.files.list
gws schema gmail.users.messages.get
gws schema sheets.spreadsheets.values.update

# Preview a request without executing (validate parameters)
gws drive files list --params '{"pageSize": 10}' --dry-run
```

## Output Formatting

### Format Options

Control output format for different use cases and downstream processing.

```bash
# JSON output (default)
gws drive files list --params '{"pageSize": 5}'

# Table format for human readability
gws drive files list --params '{"pageSize": 5}' --format table

# YAML output
gws drive files list --params '{"pageSize": 5}' --format yaml

# CSV output for spreadsheet import
gws drive files list --params '{"pageSize": 5}' --format csv

# Stream paginated results as NDJSON
gws drive files list --params '{"pageSize": 100}' --page-all

# Pipe to jq for JSON processing
gws drive files list --params '{"pageSize": 10}' | jq -r '.files[] | "\(.name) - \(.id)"'
```

## Model Armor Integration

### Content Safety Screening

Integrate Google Cloud Model Armor to scan API responses for prompt injection and safety risks.

```bash
# Sanitize API response through Model Armor template
gws gmail users messages get --params '{"userId": "me", "id": "MSG_ID"}' \
  --sanitize "projects/PROJECT/locations/LOCATION/templates/TEMPLATE"

# Set default sanitization via environment variable
export GOOGLE_WORKSPACE_CLI_SANITIZE_TEMPLATE="projects/myproject/locations/us-central1/templates/default"
export GOOGLE_WORKSPACE_CLI_SANITIZE_MODE="block"  # or "warn" (default)

# Create a new Model Armor template
gws modelarmor +create-template --name my-template --project PROJECT_ID

# Sanitize user prompts before processing
gws modelarmor +sanitize-prompt --template TEMPLATE_NAME --text "User input to check"

# Sanitize model responses before returning to user
gws modelarmor +sanitize-response --template TEMPLATE_NAME --text "Model output to check"
```

## Summary

`gws` serves as a comprehensive interface for Google Workspace automation, supporting use cases ranging from simple file operations to complex multi-service workflows. For developers, it eliminates the need to write custom API clients by providing consistent CLI patterns across all Workspace services. The structured JSON output and exit codes enable reliable scripting and CI/CD integration. For AI agents, the 100+ included SKILL.md files provide machine-readable documentation that enables autonomous Workspace management.

The CLI integrates seamlessly into existing toolchains through multiple authentication methods (OAuth, service accounts, environment tokens), flexible output formats, and Unix-style composability with tools like `jq`. Helper commands (prefixed with `+`) provide opinionated shortcuts for common tasks while the raw API surface remains accessible for advanced operations. The Model Armor integration adds a security layer for AI applications processing untrusted content from Workspace APIs.
