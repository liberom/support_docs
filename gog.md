# gogcli - Google CLI

gogcli is a fast, script-friendly command-line interface for Google services including Gmail, Calendar, Drive, Sheets, Contacts, Tasks, Chat, Classroom, and more. It provides JSON-first output, multiple account support, and least-privilege OAuth authentication with secure credential storage using your system's keychain. The tool is designed for both interactive use and automation/scripting workflows.

The CLI supports multiple authentication methods including OAuth2 refresh tokens stored securely in your system keychain, and service accounts with domain-wide delegation for Google Workspace. All commands support `--json` output for easy parsing, `--plain` for TSV output, and human-readable table formats by default. Environment variables (`GOG_ACCOUNT`, `GOG_JSON`, etc.) provide flexible configuration.

## Authentication Setup

Store OAuth client credentials and authorize an account to access Google APIs securely. Tokens are stored in your system keychain (macOS Keychain, Linux Secret Service, or Windows Credential Manager).

```bash
# Store OAuth client credentials (download from Google Cloud Console)
gog auth credentials ~/Downloads/client_secret_12345.apps.googleusercontent.com.json

# Authorize and store refresh token for an account
gog auth add you@gmail.com

# Authorize with specific services only
gog auth add you@gmail.com --services drive,calendar

# Read-only authorization (write operations will fail with 403)
gog auth add you@gmail.com --services drive --readonly

# List stored accounts
gog auth list

# Verify tokens are valid
gog auth list --check

# Show auth configuration status
gog auth status
```

## Gmail Search

Search Gmail threads using Gmail query syntax with concurrent thread detail fetching for optimal performance.

```bash
# Search recent emails
gog gmail search 'newer_than:7d' --max 10

# Search with JSON output for scripting
gog gmail search 'from:boss@example.com is:unread' --max 5 --json

# Search all pages
gog gmail search 'label:important' --all

# Get specific thread details
gog gmail thread get <threadId>

# Download thread attachments
gog gmail thread get <threadId> --download --out-dir ./attachments
```

## Gmail Send

Send emails with support for HTML bodies, attachments, reply threading, and optional email open tracking.

```bash
# Send a basic email
gog gmail send --to recipient@example.com --subject "Hello" --body "Plain text message"

# Send HTML email
gog gmail send --to recipient@example.com --subject "Hello" --body-html "<p>HTML content</p>"

# Reply to a message with quoted original
gog gmail send --reply-to-message-id <messageId> --quote --to sender@example.com --subject "Re: Subject" --body "My reply"

# Send with open tracking (requires Cloudflare Worker setup)
gog gmail send --to recipient@example.com --subject "Hello" --body-html "<p>Hi!</p>" --track

# Check email opens
gog gmail track opens <tracking_id>
gog gmail track opens --to recipient@example.com
```

## Gmail Labels and Batch Operations

Manage Gmail labels and perform batch operations on threads and messages.

```bash
# List all labels
gog gmail labels list

# Create a new label
gog gmail labels create "My Label"

# Modify thread labels (archive and star)
gog gmail thread modify <threadId> --remove INBOX --add STARRED

# Batch modify multiple messages
gog gmail batch modify <messageId1> <messageId2> --add STARRED --remove INBOX

# Batch delete messages
gog gmail batch delete <messageId1> <messageId2>
```

## Calendar Events

List, search, create, and manage calendar events with timezone-aware time handling and support for multiple calendars.

```bash
# List today's events
gog calendar events primary --today

# List events for the week
gog calendar events primary --week

# List next 3 days of events
gog calendar events primary --days 3

# List events from all calendars
gog calendar events --all

# Search events
gog calendar search "meeting" --days 30

# Get specific event with JSON output (includes day-of-week fields)
gog calendar get primary <eventId> --json
```

## Calendar Create and Update

Create and update calendar events with attendees, recurrence, reminders, and special event types.

```bash
# Create a simple event
gog calendar create primary \
  --summary "Team Meeting" \
  --from 2025-01-15T10:00:00Z \
  --to 2025-01-15T11:00:00Z

# Create event with attendees
gog calendar create primary \
  --summary "Team Sync" \
  --from 2025-01-15T14:00:00Z \
  --to 2025-01-15T15:00:00Z \
  --attendees "alice@example.com,bob@example.com" \
  --location "Zoom"

# Create recurring event with reminders
gog calendar create primary \
  --summary "Payment Reminder" \
  --from 2025-02-11T09:00:00-03:00 \
  --to 2025-02-11T09:15:00-03:00 \
  --rrule "RRULE:FREQ=MONTHLY;BYMONTHDAY=11" \
  --reminder "email:3d" \
  --reminder "popup:30m"

# Update event
gog calendar update primary <eventId> \
  --summary "Updated Meeting" \
  --from 2025-01-15T11:00:00Z \
  --to 2025-01-15T12:00:00Z

# RSVP to an event
gog calendar respond primary <eventId> --status accepted

# Check free/busy status
gog calendar freebusy --calendars "primary,work@example.com" \
  --from 2025-01-15T00:00:00Z \
  --to 2025-01-16T00:00:00Z

# Find scheduling conflicts
gog calendar conflicts --calendars "primary" --today
```

## Drive List and Search

List files, search Drive, and get file metadata with support for shared drives.

```bash
# List files in root
gog drive ls --max 20

# List files in a specific folder
gog drive ls --parent <folderId> --max 20

# Search for files
gog drive search "invoice" --max 20

# Search with Drive query language
gog drive search "mimeType = 'application/pdf'" --raw-query

# Get file metadata
gog drive get <fileId>

# Get web URL for a file
gog drive url <fileId>

# List shared drives (Team Drives)
gog drive drives --max 100
```

## Drive Upload and Download

Upload files to Drive and download files with automatic export format conversion for Google Workspace files.

```bash
# Upload a file
gog drive upload ./path/to/file --parent <folderId>

# Upload and convert to Google Doc
gog drive upload ./report.docx --convert

# Replace file content in-place (preserves shared link)
gog drive upload ./path/to/file --replace <fileId>

# Download a file
gog drive download <fileId> --out ./downloaded.bin

# Export Google Doc as PDF
gog drive download <docId> --format pdf --out ./doc.pdf

# Export Google Sheet as Excel
gog drive download <sheetId> --format xlsx --out ./data.xlsx
```

## Drive File Operations

Create folders, move, rename, delete, and manage file permissions.

```bash
# Create a folder
gog drive mkdir "New Folder" --parent <parentFolderId>

# Rename a file
gog drive rename <fileId> "New Name"

# Move a file to a different folder
gog drive move <fileId> --parent <destinationFolderId>

# Delete (move to trash)
gog drive delete <fileId>

# Permanently delete
gog drive delete <fileId> --permanent

# Share with a user
gog drive share <fileId> --to user --email user@example.com --role reader

# Share publicly (anyone with link)
gog drive share <fileId> --to anyone --role reader

# List permissions
gog drive permissions <fileId>

# Remove permission
gog drive unshare <fileId> --permission-id <permissionId>
```

## Sheets Operations

Read, write, and manage Google Sheets data with cell formatting and data validation support.

```bash
# Read values from a range
gog sheets get <spreadsheetId> 'Sheet1!A1:B10'

# Get spreadsheet metadata
gog sheets metadata <spreadsheetId>

# Update values (pipe-separated cells, comma-separated rows)
gog sheets update <spreadsheetId> 'A1' 'val1|val2,val3|val4'

# Update with JSON values
gog sheets update <spreadsheetId> 'A1' --values-json '[["a","b"],["c","d"]]'

# Append rows
gog sheets append <spreadsheetId> 'Sheet1!A:C' 'new|row|data'

# Copy data validation from template row
gog sheets append <spreadsheetId> 'Sheet1!A:C' 'new|row|data' --copy-validation-from 'Sheet1!A2:C2'

# Clear a range
gog sheets clear <spreadsheetId> 'Sheet1!A1:B10'

# Create new spreadsheet
gog sheets create "My New Spreadsheet" --sheets "Sheet1,Sheet2"

# Export to Excel
gog sheets export <spreadsheetId> --format xlsx --out ./sheet.xlsx
```

## Contacts Management

Search, create, and manage Google Contacts and access Workspace directory.

```bash
# Search contacts
gog contacts search "Ada" --max 50

# List contacts
gog contacts list --max 50

# Get a specific contact
gog contacts get people/<resourceName>
gog contacts get user@example.com

# Create a contact
gog contacts create \
  --given "John" \
  --family "Doe" \
  --email "john@example.com" \
  --phone "+1234567890"

# Update a contact
gog contacts update people/<resourceName> \
  --given "Jane" \
  --email "jane@example.com" \
  --birthday "1990-05-12" \
  --notes "Met at WWDC"

# Search other contacts (people you've interacted with)
gog contacts other search "John" --max 50

# Search Workspace directory
gog contacts directory search "Jane" --max 50
```

## Tasks Management

Manage Google Tasks including task lists and individual tasks with due dates and recurrence.

```bash
# List task lists
gog tasks lists --max 50

# Create a task list
gog tasks lists create "My Tasks"

# List tasks in a list
gog tasks list <tasklistId> --max 50

# Get a specific task
gog tasks get <tasklistId> <taskId>

# Add a task
gog tasks add <tasklistId> --title "Task title"

# Add recurring task
gog tasks add <tasklistId> --title "Weekly sync" --due 2025-02-01 --repeat weekly --repeat-count 4

# Mark task complete
gog tasks done <tasklistId> <taskId>

# Mark task incomplete
gog tasks undo <tasklistId> <taskId>

# Update a task
gog tasks update <tasklistId> <taskId> --title "New title"

# Delete a task
gog tasks delete <tasklistId> <taskId>

# Clear completed tasks
gog tasks clear <tasklistId>
```

## Google Chat

Send messages, list spaces, and manage Chat conversations (Google Workspace only).

```bash
# List Chat spaces
gog chat spaces list

# Find a space by name
gog chat spaces find "Engineering"

# Create a space with members
gog chat spaces create "Engineering" --member alice@company.com --member bob@company.com

# List messages in a space
gog chat messages list spaces/<spaceId> --max 5

# List unread messages
gog chat messages list spaces/<spaceId> --unread

# Send a message
gog chat messages send spaces/<spaceId> --text "Build complete!"

# Send a direct message
gog chat dm send user@company.com --text "ping"
```

## Docs and Slides

Export, create, and manage Google Docs and Slides presentations.

```bash
# Get document info
gog docs info <docId>

# Extract text from a document
gog docs cat <docId> --max-bytes 10000

# Create a new document
gog docs create "My Doc"

# Import markdown to document
gog docs create "My Doc" --file ./doc.md

# Update document content from markdown
gog docs write <docId> --replace --markdown --file ./doc.md

# Export as PDF
gog docs export <docId> --format pdf --out ./doc.pdf

# Create a presentation
gog slides create "My Deck"

# Create slides from markdown
gog slides create-from-markdown "My Deck" --content-file ./slides.md

# Export presentation
gog slides export <presentationId> --format pptx --out ./deck.pptx
```

## Service Accounts (Workspace)

Configure service accounts for domain-wide delegation in Google Workspace environments.

```bash
# Configure service account for user impersonation
gog auth service-account set you@yourdomain.com --key ~/Downloads/service-account.json

# Check service account status
gog auth service-account status you@yourdomain.com

# Use with Keep (requires domain-wide delegation)
gog keep list --account you@yourdomain.com
gog keep get <noteId> --account you@yourdomain.com
```

## Summary

gogcli provides comprehensive command-line access to Google's productivity suite, making it ideal for automation scripts, CI/CD pipelines, and power users who prefer terminal workflows. The JSON output mode enables easy integration with tools like `jq` for complex data processing, while the plain text mode provides stable TSV output for shell scripting.

Common integration patterns include batch processing Gmail threads with shell pipelines (`gog --json gmail search ... | jq ... | xargs gog gmail labels modify`), automated calendar management for meeting scheduling bots, Drive synchronization scripts, and Sheets-based data workflows. The multiple account support and OAuth client isolation make it suitable for managing both personal and work accounts, while service account support enables server-side automation in Google Workspace environments.
