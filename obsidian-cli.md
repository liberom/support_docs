### Everyday Use Examples

Source: https://help.obsidian.md/cli/index

Examples of common tasks that can be performed using the Obsidian CLI.

## Everyday Use Examples

### Open Today's Daily Note
```bash
obsidian daily
```

### Add a Task to Daily Note

```bash
obsidian daily:append content="- [ ] Buy groceries"
```

### Search Vault

```bash
obsidian search query="meeting notes"
```

### Read Active File

```bash
obsidian read
```

### List Tasks from Daily Note

```bash
obsidian tasks daily
```

### Create New Note from Template

```bash
obsidian create name="Trip to Paris" template=Travel
```

### List Tags with Counts

```bash
obsidian tags counts
```

### Compare File Versions

```bash
obsidian diff file=README from=1 to=3
```


--------------------------------

### Install Community Theme (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Installs a theme from the community repository. The 'enable' option automatically activates the theme after installation.

```shell
name=<name>        # (required) theme name
enable             # activate after install
```

--------------------------------

### Developer Commands Examples

Source: https://help.obsidian.md/cli/index

Examples of developer-focused commands available through the Obsidian CLI for plugin and theme development.

## Developer Commands Examples

### Open Developer Tools
```bash
obsidian devtools
```

### Reload Community Plugin

```bash
obsidian plugin:reload id=my-plugin
```

### Take Screenshot

```bash
obsidian dev:screenshot path=screenshot.png
```

### Run JavaScript in Console

```bash
obsidian eval code="app.vault.getFiles().length"
```

--------------------------------

### List Installed Themes (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Lists all themes currently installed in the Obsidian vault. An option is available to include version numbers for each theme.

```shell
versions           # include version numbers
```

--------------------------------

### List CSS Snippets (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Lists all installed CSS snippets in the Obsidian vault.

```shell

```

--------------------------------

### Themes and Snippets API

Source: https://help.obsidian.md/cli/index

Commands for managing themes and CSS snippets in Obsidian. Includes listing, enabling, disabling, installing, and uninstalling.

## `themes`

### Description
List all installed themes in the vault. Can optionally include version numbers.

### Method
GET

### Endpoint
/themes

### Parameters
#### Query Parameters
- **versions** (boolean) - Optional - include version numbers

### Response
#### Success Response (200)
- **themes** (array) - List of theme names, optionally with versions.

#### Response Example
```json
{
  "themes": ["Default", "Solarized Light"]
}
```

## `theme`

### Description
Show information about the currently active theme or details about a specific theme by name.

### Method
GET

### Endpoint
/theme

### Parameters
#### Query Parameters
- **name** (string) - Optional - theme name for details

### Response
#### Success Response (200)
- **active_theme** (string) - The name of the currently active theme.
- **theme_info** (object) - Details about a specific theme if requested.

#### Response Example
```json
{
  "active_theme": "Default"
}
```

## `theme:set`

### Description
Set the active theme for the Obsidian vault. Can be set to a specific theme name or empty for the default.

### Method
POST

### Endpoint
/theme/set

### Parameters
#### Query Parameters
- **name** (string) - Required - theme name (empty for default)

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Theme set to 'Solarized Light'."
}
```

## `theme:install`

### Description
Install a community theme from a repository. Can optionally activate the theme immediately after installation.

### Method
POST

### Endpoint
/theme/install

### Parameters
#### Query Parameters
- **name** (string) - Required - theme name
- **enable** (boolean) - Optional - activate after install

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Theme 'Dracula' installed and activated."
}
```

## `theme:uninstall`

### Description
Uninstall a previously installed theme from the vault.

### Method
DELETE

### Endpoint
/theme/uninstall

### Parameters
#### Query Parameters
- **name** (string) - Required - theme name

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Theme 'Dracula' uninstalled."
}
```

## `snippets`

### Description
List all installed CSS snippets in the vault.

### Method
GET

### Endpoint
/snippets

### Response
#### Success Response (200)
- **snippets** (array) - List of CSS snippet names.

#### Response Example
```json
{
  "snippets": ["custom_styles.css", "code_block_enhancements.css"]
}
```

## `snippets:enabled`

### Description
List all enabled CSS snippets in the vault.

### Method
GET

### Endpoint
/snippets/enabled

### Response
#### Success Response (200)
- **enabled_snippets** (array) - List of enabled CSS snippet names.

#### Response Example
```json
{
  "enabled_snippets": ["custom_styles.css"]
}
```

## `snippet:enable`

### Description
Enable a specific CSS snippet.

### Method
POST

### Endpoint
/snippet/enable

### Parameters
#### Query Parameters
- **name** (string) - Required - snippet name

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Snippet 'custom_styles.css' enabled."
}
```

## `snippet:disable`

### Description
Disable a specific CSS snippet.

### Method
POST

### Endpoint
/snippet/disable

### Parameters
#### Query Parameters
- **name** (string) - Required - snippet name

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Snippet 'custom_styles.css' disabled."
}
```

--------------------------------

### Get Tag Information (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Retrieves information about a specific tag, including its occurrence count. The 'verbose' option provides a detailed list of files containing the tag and their respective counts.

```shell
name=<tag>         # (required) tag name

total              # return occurrence count
verbose            # include file list and count
```

--------------------------------

### Obsidian CLI: Create Note with Parameters and Flags

Source: https://help.obsidian.md/cli/index

Demonstrates how to create a new note using the Obsidian CLI, including the use of parameters like 'name' and 'content', and flags like 'open' and 'overwrite'. It also shows how to handle multiline content using newline ('\n') and tab ('\t') characters.

```bash
# Create a new note using the default "Untitled" name
obsidian create

# Create a new note called "Note" with content "Hello world"
obsidian create name=Note content="Hello world"

# Create a note and open it
obsidian create name=Note content="Hello" open overwrite

# For multiline content use \n for newline. Use \t for tab.
obsidian create name=Note content="# Title\n\nBody text"
```

--------------------------------

### Parameters and Flags

Source: https://help.obsidian.md/cli/index

Information on how to use parameters and flags with Obsidian CLI commands.

## Use Parameters and Flags

Commands can use **parameters** and **flags**. Required parameters are marked as `required`.

### Parameters
Parameters take a value in the format `parameter=value`. If the value contains spaces, enclose it in quotes.

```bash
# Create a note named "Note" with content "Hello world"
obsidian create name=Note content="Hello world"
```

### Flags

Flags are boolean switches that are included to enable a feature. They do not take a value.

```bash
# Create a note and open it, overwriting if it exists
obsidian create name=Note content="Hello" open overwrite
```

### Multiline Content

Use `\n` for newlines and `\t` for tabs in content.

```bash
obsidian create name=Note content="# Title\n\nBody text"
```

--------------------------------

### Run Obsidian CLI Help Command

Source: https://help.obsidian.md/cli/index

Executes the help command in the Obsidian CLI to display available commands and their usage. This is a fundamental command for understanding the CLI's capabilities.

```bash
# Run the help command
obsidian help
```

--------------------------------

### Troubleshooting

Source: https://help.obsidian.md/cli/index

Guidance for troubleshooting issues with the Obsidian CLI on Windows and macOS.

## Troubleshooting

### General

*   Ensure you are using the latest Obsidian installer version (1.12.4 or above).
*   Restart your terminal after registering the CLI for PATH changes to take effect.
*   Obsidian must be running for the CLI to connect. The first CLI command should launch the app if it's not running.

### Windows

*   Requires Obsidian 1.12.4+ installer.
*   Uses a terminal redirector (`Obsidian.com`) to connect Obsidian to stdin/stdout properly.

### macOS

*   The CLI registration adds Obsidian's binary directory to your PATH via `~/.zprofile`.
*   Verify that `~/.zprofile` contains the line: `export PATH="$PATH:/Applications/Obsidian.app/Contents/MacOS"`.


--------------------------------

### Show Theme Information (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Displays information about the currently active theme or details for a specific theme when a name is provided.

```shell
name=<name>        # theme name for details
```

--------------------------------

### Keyboard Shortcuts

Source: https://help.obsidian.md/cli/index

List of available keyboard shortcuts for navigation, editing, autocomplete, and other actions within the Obsidian TUI.

## Keyboard Shortcuts

### Navigation

| Action                                      | Shortcut              |
| ------------------------------------------- | --------------------- |
| Move cursor left                            | `←` / `Ctrl+B`        |
| Move cursor right (accepts suggestion)      | `→` / `Ctrl+F`        |
| Jump to start of line                       | `Ctrl+A`              |
| Jump to end of line                         | `Ctrl+E`              |
| Move back one word                          | `Alt+B`               |
| Move forward one word                       | `Alt+F`               |

### Editing

| Action                    | Shortcut                  |
| ------------------------- | ------------------------- |
| Delete to start of line   | `Ctrl+U`                  |
| Delete to end of line     | `Ctrl+K`                  |
| Delete previous word      | `Ctrl+W` / `Alt+Backspace`|

### Autocomplete

| Action                                      | Shortcut              |
| ------------------------------------------- | --------------------- |
| Enter suggestion mode / accept suggestion   | `Tab`                 |
| Exit suggestion mode                        | `Shift+Tab`           |
| Enter suggestion mode (from fresh input)    | `↓`                   |
| Accept first/selected suggestion            | `→`                   |

### History

| Action                                      | Shortcut              |
| ------------------------------------------- | --------------------- |
| Previous history entry / navigate up        | `↑` / `Ctrl+P`        |
| Next history entry / navigate down          | `↓` / `Ctrl+N`        |
| Reverse history search                      | `Ctrl+R`              |

### Other

| Action                                      | Shortcut              |
| ------------------------------------------- | --------------------- |
| Execute command or accept suggestion        | `Enter`               |
| Undo autocomplete / exit suggestion / clear | `Escape`              |
| Clear screen                                | `Ctrl+L`              |
| Exit                                        | `Ctrl+C` / `Ctrl+D`   |


--------------------------------

### Everyday Obsidian CLI Commands

Source: https://help.obsidian.md/cli/index

A collection of common Obsidian CLI commands for daily use. These include opening daily notes, appending tasks, searching the vault, reading the active file, listing tasks, creating notes from templates, listing tags, and comparing file versions.

```bash
# Open today's daily note
obsidian daily

# Add a task to your daily note
obsidian daily:append content="- [ ] Buy groceries"

# Search your vault
obsidian search query="meeting notes"

# Read the active file
obsidian read

# List all tasks from your daily note
obsidian tasks daily

# Create a new note from a template
obsidian create name="Trip to Paris" template=Travel

# List all tags in your vault with counts
obsidian tags counts

# Compare two versions of a file
obsidian diff file=README from=1 to=3
```

--------------------------------

### List Templates (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Lists all available templates within the Obsidian vault. An option is available to return the total count of templates.

```shell
total              # return template count
```

--------------------------------

### Create Unique Note (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Creates a new note with a unique name, optionally providing initial content. The note can be opened in a new tab, split pane, or window. The 'open' flag ensures the file is opened after creation.

```shell
name=<text>        # note name
content=<text>     # initial content
paneType=tab|split|window    # pane type to open in

open               # open file after creating
```

--------------------------------

### Search with Context API

Source: https://help.obsidian.md/cli/index

Searches the Obsidian vault for a query and returns matching lines with context. Output is in a grep-style format.

## Search with Context

### Description
Search with matching line context. Returns grep-style `path:line: text` output.

### Method
GET

### Endpoint
/search/context

### Parameters
#### Query Parameters
- **query** (string) - Required - The search query text.
- **path** (string) - Optional - Limit the search to this folder.
- **limit** (integer) - Optional - Maximum number of files to return.
- **format** (string) - Optional - Output format: `text` or `json` (default: `text`).
- **case** (boolean) - Optional - Perform a case-sensitive search.

### Request Example
```json
{
  "example": "GET /search/context?query=specific_phrase&path=docs"
}
```

### Response

#### Success Response (200)

- **results** (array) - List of strings, each representing a matching line with context.

#### Response Example

```json
{
  "example": {
    "results": [
      "docs/document.md:42: This line contains the specific_phrase."
    ]
  }
}
```


--------------------------------

### Targeting Vaults and Files

Source: https://help.obsidian.md/cli/index

How to specify which vault or file a command should operate on.


## Target a Vault or File

### Target a Vault
If the terminal's current working directory is a vault folder, that vault is used by default. Otherwise, the currently active vault is used.

Use `vault=<name>` or `vault=<id>` to target a specific vault. This must be the first parameter before your command.

```bash
obsidian vault=Notes daily
obsidian vault="My Vault" search query="test"
```

In the TUI, use `vault:open <name>` or `<id>` to switch vaults.

### Target a File

Many commands accept `file` and `path` parameters to target a specific file. If neither is provided, the command defaults to the active file.

- `file=<name>`: Resolves the file using wikilink resolution, matching by file name without requiring the full path or extension.
- `path=<path>`: Requires the exact path from the vault root, e.g., `folder/note.md`.

```bash
# Example using path parameter (assuming command supports it)
# obsidian <command> path=folder/my_note.md
```

--------------------------------

### Show Vault Information (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Displays information about the current Obsidian vault. Specific details like name, path, file count, folder count, or size can be requested.

```shell
info=name|path|files|folders|size  # return specific info only
```

--------------------------------

### Open URL in Web Viewer (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Opens a specified URL in the Obsidian web viewer. The 'newtab' option allows opening the URL in a new tab.

```shell
url=<url>          # (required) URL to open
newtab             # open in new tab
```

--------------------------------

### Templates API

Source: https://help.obsidian.md/cli/index

Commands for managing templates within the Obsidian vault. Includes listing, reading, and inserting templates.

## `templates`

### Description
List all available templates in the vault. Can return the total count of templates.

### Method
GET

### Endpoint
/templates

### Parameters
#### Query Parameters
- **total** (boolean) - Optional - return template count

### Response
#### Success Response (200)
- **templates** (array) - List of template names.

#### Response Example
```json
{
  "templates": ["meeting", "daily_note"]
}
```

## `template:read`

### Description
Read the content of a specific template. Supports resolving template variables like date, time, and title.

### Method
GET

### Endpoint
/template/read

### Parameters
#### Query Parameters
- **name** (string) - Required - template name
- **title** (string) - Optional - title for variable resolution
- **resolve** (boolean) - Optional - resolve template variables

### Response
#### Success Response (200)
- **content** (string) - The content of the template.

#### Response Example
```json
{
  "content": "# Meeting Notes\nDate: {{date}}\nTitle: {{title}}"
}
```

## `template:insert`

### Description
Insert a specified template into the currently active file. This command is typically executed within the Obsidian application context.

### Method
POST

### Endpoint
/template/insert

### Parameters
#### Query Parameters
- **name** (string) - Required - template name

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the template was inserted.

#### Response Example
```json
{
  "message": "Template 'meeting' inserted successfully."
}
```

--------------------------------

### Web Viewer API

Source: https://help.obsidian.md/cli/index

Command to open a URL in the Obsidian web viewer, with options to open in a new tab.


## `web`

### Description
Open a specified URL in the Obsidian web viewer. Can be configured to open in a new tab.

### Method
GET

### Endpoint
/web

### Parameters
#### Query Parameters
- **url** (string) - Required - URL to open
- **newtab** (boolean) - Optional - open in new tab

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Opening URL in web viewer."
}
```

--------------------------------

### Open Search View API

Source: https://help.obsidian.md/cli/index

Opens the search view within Obsidian, optionally pre-filling it with an initial search query.


## Open Search View

### Description
Open search view.

### Method
GET

### Endpoint
/search/open

### Parameters
#### Query Parameters
- **query** (string) - Optional - The initial search query to populate the search view with.

### Request Example
```json
{
  "example": "GET /search/open?query=initial search"
}
```

### Response

#### Success Response (200)

- **message** (string) - Confirmation that the search view has been opened.

#### Response Example

```json
{
  "example": {
    "message": "Search view opened."
  }
}
```

--------------------------------

### Obsidian CLI: Target a Specific File

Source: https://help.obsidian.md/cli/index

Explains how to target a specific file for Obsidian CLI commands using 'file' or 'path' parameters. If neither is provided, the command defaults to the currently active file. 'file' resolves by name, while 'path' requires the exact path from the vault root.

```bash
# Example using file parameter (resolves by name)
# obsidian some_command file=MyNote

# Example using path parameter (requires exact path from vault root)
# obsidian some_command path=folder/MyNote.md
```

--------------------------------

### Developer Commands

Source: https://help.obsidian.md/cli/index

Commands to assist in developing Community plugins and Themes, including toggling dev tools, debugging, and inspecting elements.

## Developer Commands

### `devtools`

Toggle Electron dev tools.

### `dev:debug`

Attach/detach Chrome DevTools Protocol debugger.

#### Parameters

##### Query Parameters

- **on** (boolean) - Optional - Attach debugger.
- **off** (boolean) - Optional - Detach debugger.

### `dev:cdp`

Run a Chrome DevTools Protocol command.

#### Parameters

##### Query Parameters

- **method** (string) - Required - CDP method to call.
- **params** (JSON) - Optional - Method parameters as JSON.

### `dev:errors`

Show captured JavaScript errors.

#### Parameters

##### Query Parameters

- **clear** (boolean) - Optional - Clear the error buffer.

### `dev:screenshot`

Take a screenshot (returns base64 PNG).

#### Parameters

##### Query Parameters

- **path** (string) - Required - Output file path.

### `dev:console`

Show captured console messages.

#### Parameters

##### Query Parameters

- **limit** (integer) - Optional - Max messages to show (default 50).
- **level** (string) - Optional - Filter by log level (log, warn, error, info, debug).
- **clear** (boolean) - Optional - Clear the console buffer.

### `dev:css`

Inspect CSS with source locations.

#### Parameters

##### Query Parameters

- **selector** (string) - Required - CSS selector.
- **prop** (string) - Optional - Filter by property name.

### `dev:dom`

Query DOM elements.

#### Parameters

##### Query Parameters

- **selector** (string) - Required - CSS selector.
- **attr** (string) - Optional - Get attribute value.
- **css** (string) - Optional - Get CSS property value.
- **total** (boolean) - Optional - Return element count.
- **text** (boolean) - Optional - Return text content.
- **inner** (boolean) - Optional - Return innerHTML instead of outerHTML.
- **all** (boolean) - Optional - Return all matches instead of first.

### `dev:mobile`

Toggle mobile emulation.

#### Parameters

##### Query Parameters

- **on** (boolean) - Optional - Enable mobile emulation.
- **off** (boolean) - Optional - Disable mobile emulation.

### `eval`

Execute JavaScript and return result.

#### Parameters

##### Query Parameters

- **code** (string) - Required - JavaScript code to execute.


--------------------------------

### Obsidian CLI Overview

Source: https://help.obsidian.md/cli/index

The Obsidian CLI allows you to interact with Obsidian from your terminal. It supports both single commands and an interactive terminal user interface (TUI) with features like autocomplete and command history.


## Obsidian CLI

### Description
Obsidian CLI is a command-line interface that lets you control Obsidian from your terminal for scripting, automation, and integration with external tools. Anything you can do in Obsidian you can do from the command line. Obsidian CLI even includes developer commands to access developer tools, inspect elements, take screenshots, reload plugins, and more.

### Requirements
- Obsidian 1.12 installer or later.
- Obsidian CLI enabled in Obsidian settings (**Settings** → **General** → **Command line interface**).
- Obsidian app must be running (the first command will launch it if it's not).

### Usage
**Run a single command:**
```bash
obsidian [command] [parameters...]
```

**Use the terminal interface (TUI):**

```bash
obsidian
```

Within the TUI, you can enter commands directly without the `obsidian` prefix. Use `Ctrl+R` to search command history.


--------------------------------

### Workspace Management

Source: https://help.obsidian.md/cli/index

Commands for managing Obsidian workspaces, including showing the workspace tree, listing saved workspaces, saving, loading, and deleting them.


## Workspace Management

### `workspace`

Show workspace tree.

#### Parameters

##### Query Parameters

- **ids** (boolean) - Optional - Include workspace item IDs.

### `workspaces`

List saved workspaces.

#### Parameters

##### Query Parameters

- **total** (boolean) - Optional - Return workspace count.

### `workspace:save`

Save current layout as workspace.

#### Parameters

##### Query Parameters

- **name** (string) - Required - Workspace name.

### `workspace:load`

Load a saved workspace.

#### Parameters

##### Query Parameters

- **name** (string) - Required - Workspace name.

### `workspace:delete`

Delete a saved workspace.

#### Parameters

##### Query Parameters

- **name** (string) - Required - Workspace name.


--------------------------------

### Publish Site Info API

Source: https://help.obsidian.md/cli/index

Retrieves information about the Obsidian Publish site, including its slug and URL.


## Publish Site Info

### Description
Show publish site info (slug, URL).

### Method
GET

### Endpoint
/publish/site

### Parameters
None

### Request Example
```json
{
  "example": "GET /publish/site"
}
```

### Response

#### Success Response (200)

- **slug** (string) - The unique identifier for the publish site.
- **url** (string) - The URL of the published site.

#### Response Example

```json
{
  "example": {
    "slug": "my-vault",
    "url": "https://publish.obsidian.md/my-vault"
  }
}
```

--------------------------------

### Set Active Theme (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Sets the active theme in Obsidian. Providing an empty name reverts to the default theme.

```shell
name=<name>        # (required) theme name (empty for default)
```

--------------------------------

### Properties API

Source: https://help.obsidian.md/cli/index

Commands to list and manage properties within the Obsidian vault. Supports filtering by file, path, or specific property name, and options for sorting and output format.


## Properties

### Description
List properties in the vault. Use `active` or `file`/`path` to show properties for a specific file.

### Method
GET

### Endpoint
/properties

### Parameters
#### Query Parameters
- **file** (string) - Optional - File name to filter properties.
- **path** (string) - Optional - File path to filter properties.
- **name** (string) - Optional - Get specific property count.
- **sort** (string) - Optional - Sort by count (default: name).
- **format** (string) - Optional - Output format: `yaml`, `json`, or `tsv` (default: `yaml`).
- **total** (boolean) - Optional - Return property count.
- **counts** (boolean) - Optional - Include occurrence counts.
- **active** (boolean) - Optional - Show properties for the currently active file.

### Request Example
```json
{
  "example": "GET /properties?file=example.md&sort=count"
}
```

### Response

#### Success Response (200)

- **properties** (object) - Object containing properties and their values or counts.

#### Response Example

```json
{
  "example": {
    "properties": {
      "key1": "value1",
      "key2": {
        "count": 5
      }
    }
  }
}
```


--------------------------------

### List Tasks in Vault (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Lists tasks from the Obsidian vault. Tasks can be filtered by file, path, or status. Options include showing only completed or incomplete tasks, displaying task counts, and enabling verbose output with file grouping and line numbers. Supports filtering tasks from the daily note.

```shell
file=<name>        # filter by file name
path=<path>        # filter by file path
status="<char>"    # filter by status character

total              # return task count
done               # show completed tasks
todo               # show incomplete tasks
verbose            # group by file with line numbers
format=json|tsv|csv  # output format (default: text)
active             # show tasks for active file
daily              # show tasks from daily note
```

--------------------------------

### List Published Files API

Source: https://help.obsidian.md/cli/index

Lists all files currently published on the Obsidian Publish site. Supports an option to return the total count of published files.


## List Published Files

### Description
List published files.

### Method
GET

### Endpoint
/publish/list

### Parameters
#### Query Parameters
- **total** (boolean) - Optional - Return the total count of published files.

### Request Example
```json
{
  "example": "GET /publish/list"
}
```

### Response

#### Success Response (200)

- **files** (array) - List of published file names.
- **count** (integer) - Total number of published files (if `total` is true).

#### Response Example

```json
{
  "example": {
    "files": [
      "file1.md",
      "file2.md"
    ]
  }
}
```


--------------------------------

### Insert Template into File (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Inserts the content of a specified template into the currently active file in Obsidian.

```shell
name=<template>    # (required) template name
```

--------------------------------

### List Tags in Vault (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Lists all tags present in the Obsidian vault. Supports filtering by a specific file or path, sorting by count or name, and outputting in JSON, TSV, or CSV formats. Can also show tags for the currently active file.

```shell
file=<name>        # file name
path=<path>        # file path
sort=count         # sort by count (default: name)

total              # return tag count
counts             # include tag counts
format=json|tsv|csv  # output format (default: tsv)
active             # show tags for active file
```

--------------------------------

### Tags API

Source: https://help.obsidian.md/cli/index

Commands for listing and managing tags within the Obsidian vault. Supports filtering by file or path, sorting, and different output formats.


## `tags`

### Description
List tags in the vault. Use `active` or `file`/`path` to show tags for a specific file.

### Method
GET

### Endpoint
/tags

### Parameters
#### Query Parameters
- **file** (string) - Optional - file name
- **path** (string) - Optional - file path
- **sort** (string) - Optional - sort by count (default: name)
- **total** (boolean) - Optional - return tag count
- **counts** (boolean) - Optional - include tag counts
- **format** (string) - Optional - output format (json|tsv|csv, default: tsv)
- **active** (boolean) - Optional - show tags for active file

### Response
#### Success Response (200)
- **tags** (array) - List of tags with optional counts and file information.

#### Response Example
```json
{
  "tags": [
    {
      "tag": "#example",
      "count": 5,
      "files": ["file1.md", "file2.md"]
    }
  ]
}
```


## `tag`

### Description
Get tag info. Requires a tag name and can optionally return total count or a verbose list including files.

### Method
GET

### Endpoint
/tag

### Parameters
#### Query Parameters
- **name** (string) - Required - tag name
- **total** (boolean) - Optional - return occurrence count
- **verbose** (boolean) - Optional - include file list and count

### Response
#### Success Response (200)
- **tag** (string) - The requested tag name.
- **total** (integer) - The total count of the tag.
- **files** (array) - List of files containing the tag, with counts.

#### Response Example
```json
{
  "tag": "#example",
  "total": 5,
  "files": [
    {
      "file": "file1.md",
      "count": 2
    },
    {
      "file": "file2.md",
      "count": 3
    }
  ]
}
```


--------------------------------

### Open Published File API

Source: https://help.obsidian.md/cli/index

Opens a specified file on the Obsidian Publish site in a web browser. Defaults to the active file.


## Open Published File

### Description
Open file on published site (default: active file).

### Method
GET

### Endpoint
/publish/open

### Parameters
#### Query Parameters
- **file** (string) - Optional - File name to open.
- **path** (string) - Optional - File path to open.

### Request Example
```json
{
  "example": "GET /publish/open?file=my_document.md"
}
```

### Response

#### Success Response (200)

- **url** (string) - The URL of the published file.

#### Response Example

```json
{
  "example": {
    "url": "https://publish.obsidian.md/my-vault/my_document"
  }
}
```


--------------------------------

### Developer Commands for Obsidian CLI

Source: https://help.obsidian.md/cli/index

A set of Obsidian CLI commands tailored for developers, useful for plugin and theme development. These include opening developer tools, reloading plugins, taking screenshots, and executing JavaScript code within the app console.

```bash
# Open developer tools
obsidian devtools

# Reload a community plugin you're developing
obsidian plugin:reload id=my-plugin

# Take a screenshot of the app
obsidian dev:screenshot path=screenshot.png

# Run JavaScript in the app console
obsidian eval code="app.vault.getFiles().length"
```

--------------------------------

### Show or Update a Task (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Displays information about a specific task or allows updating its status. Tasks can be identified by reference (path:line), file and line number, or directly within the daily note. Supports toggling completion status and setting custom statuses.

```shell
ref=<path:line>    # task reference (path:line)
file=<name>        # file name
path=<path>        # file path
line=<n>           # line number
status="<char>"    # set status character

toggle             # toggle task status
daily              # daily note
done               # mark as done
todo               # mark as todo
```

--------------------------------

### Open Sync History API

Source: https://help.obsidian.md/cli/index

Opens the sync history view for a specified file in Obsidian, defaulting to the active file.


## Open Sync History

### Description
Open sync history (default: active file).

### Method
GET

### Endpoint
/sync/open

### Parameters
#### Query Parameters
- **file** (string) - Optional - File name to open history for.
- **path** (string) - Optional - File path to open history for.

### Request Example
```json
{
  "example": "GET /sync/open?file=document.md"
}
```

### Response

#### Success Response (200)

- **message** (string) - Confirmation that the sync history view has been opened.

#### Response Example

```json
{
  "example": {
    "message": "Sync history view opened."
  }
}
```

--------------------------------

### Enable CSS Snippet (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Enables a specified CSS snippet, applying its styles to the Obsidian interface.

```shell
name=<name>        # (required) snippet name
```

--------------------------------

### Publish File API

Source: https://help.obsidian.md/cli/index

Publishes a specified file or all changed files to the Obsidian Publish site. Defaults to publishing the active file.


## Publish File

### Description
Publish a file or all changed files (default: active file).

### Method
POST

### Endpoint
/publish/add

### Parameters
#### Request Body
- **file** (string) - Optional - File name to publish.
- **path** (string) - Optional - File path to publish.
- **changed** (boolean) - Optional - Publish all changed files.

### Request Example
```json
{
  "example": {
    "file": "my_document.md"
  }
}
```

### Response

#### Success Response (200)

- **message** (string) - Confirmation message.

#### Response Example

```json
{
  "example": {
    "message": "File 'my_document.md' published successfully."
  }
}
```


--------------------------------

### Unique Notes API

Source: https://help.obsidian.md/cli/index

Command for creating unique notes with specified name and content, with options to control the pane type and opening behavior.


## `unique`

### Description
Create a unique note with specified name and initial content. Options to control the pane type (tab, split, window) and whether to open the file after creation.

### Method
POST

### Endpoint
/unique

### Parameters
#### Query Parameters
- **name** (string) - Optional - note name
- **content** (string) - Optional - initial content
- **paneType** (string) - Optional - pane type to open in (tab|split|window)
- **open** (boolean) - Optional - open file after creating

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.
- **file_path** (string) - Path to the created unique note.

#### Response Example
```json
{
  "message": "Unique note created successfully.",
  "file_path": "path/to/your/unique_note.md"
}
```


--------------------------------

### Tags API

Source: https://help.obsidian.md/cli/index

Commands related to managing and interacting with tags in Obsidian.


## Tags API

### Description
Commands for Tags. This section outlines operations related to tags within the Obsidian vault.

### Method
GET/POST/DELETE (depending on specific tag operation)

### Endpoint
/tags or /tags/{tag_name}

### Parameters
(Specific parameters depend on the exact tag operation, e.g., listing all tags, finding files with a specific tag, etc.)

### Request Example
```json
{
  "example": "GET /tags"
}
```

### Response

#### Success Response (200)

(Response structure depends on the specific tag operation.)

#### Response Example

```json
{
  "example": {
    "tags": ["#project", "#idea", "#meeting"]
  }
}
```


--------------------------------

### Uninstall Theme (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Uninstalls a specified theme from the Obsidian vault.

```shell
name=<name>        # (required) theme name
```

--------------------------------

### Set Property API

Source: https://help.obsidian.md/cli/index

Sets a property on a specified file, defaulting to the active file. Requires property name and value, with optional type and file/path specification.


## Property Set

### Description
Set a property on a file (default: active file).

### Method
POST

### Endpoint
/property/set

### Parameters
#### Request Body
- **name** (string) - Required - Property name.
- **value** (string) - Required - Property value.
- **type** (string) - Optional - Property type: `text`, `list`, `number`, `checkbox`, `date`, `datetime`.
- **file** (string) - Optional - File name to set the property on.
- **path** (string) - Optional - File path to set the property on.

### Request Example
```json
{
  "example": {
    "name": "status",
    "value": "in-progress",
    "type": "text",
    "file": "task.md"
  }
}
```

### Response

#### Success Response (200)

- **message** (string) - Confirmation message.

#### Response Example

```json
{
  "example": {
    "message": "Property 'status' set successfully."
  }
}
```


--------------------------------

### Tasks API

Source: https://help.obsidian.md/cli/index

Commands for managing tasks within the Obsidian vault. Supports listing, filtering, and updating tasks across files and daily notes.


## `tasks`

### Description
List tasks in the vault. Supports filtering by file, path, status, and showing completed or incomplete tasks. Can also provide counts or verbose output.

### Method
GET

### Endpoint
/tasks

### Parameters
#### Query Parameters
- **file** (string) - Optional - filter by file name
- **path** (string) - Optional - filter by file path
- **status** (string) - Optional - filter by status character (e.g., 'x', ' ')
- **total** (boolean) - Optional - return task count
- **done** (boolean) - Optional - show completed tasks
- **todo** (boolean) - Optional - show incomplete tasks
- **verbose** (boolean) - Optional - group by file with line numbers
- **format** (string) - Optional - output format (json|tsv|csv, default: text)
- **active** (boolean) - Optional - show tasks for active file
- **daily** (boolean) - Optional - show tasks from daily note

### Response
#### Success Response (200)
- **tasks** (array) - List of tasks matching the criteria.

#### Response Example
```json
[
  {
    "text": "Complete project proposal",
    "status": "[",
    "file": "project.md",
    "line": 5
  }
]
```


## `task`

### Description
Show or update a specific task. Can be identified by reference, file/path and line number, or toggled/set to done/todo.

### Method
GET | POST | PUT

### Endpoint
/task

### Parameters
#### Query Parameters
- **ref** (string) - Optional - task reference (path:line)
- **file** (string) - Optional - file name
- **path** (string) - Optional - file path
- **line** (integer) - Optional - line number
- **status** (string) - Optional - set status character (e.g., 'x', ' ')
- **toggle** (boolean) - Optional - toggle task status
- **daily** (boolean) - Optional - daily note context
- **done** (boolean) - Optional - mark as done
- **todo** (boolean) - Optional - mark as todo

### Response
#### Success Response (200)
- **message** (string) - Confirmation message of the action taken.

#### Response Example
```json
{
  "message": "Task toggled successfully."
}
```


--------------------------------

### Tab Management

Source: https://help.obsidian.md/cli/index

Commands for managing open tabs in Obsidian, including listing tabs, opening new ones, and viewing recent files.


## Tab Management

### `tabs`

List open tabs.

#### Parameters

##### Query Parameters

- **ids** (boolean) - Optional - Include tab IDs.

### `tab:open`

Open a new tab.

#### Parameters

##### Query Parameters

- **group** (string) - Optional - Tab group ID.
- **file** (string) - Optional - File path to open.
- **view** (string) - Optional - View type to open (e.g., 'preview', 'source').

### `recents`

List recently opened files.

#### Parameters

##### Query Parameters

- **total** (boolean) - Optional - Return recent file count.


--------------------------------

### Aliases API

Source: https://help.obsidian.md/cli/index

Commands to list aliases within the Obsidian vault. Supports filtering by file or path, and options for verbose output or alias count.


## Aliases

### Description
List aliases in the vault. Use `active` or `file`/`path` to show aliases for a specific file.

### Method
GET

### Endpoint
/aliases

### Parameters
#### Query Parameters
- **file** (string) - Optional - File name to filter aliases.
- **path** (string) - Optional - File path to filter aliases.
- **total** (boolean) - Optional - Return alias count instead of aliases.
- **verbose** (boolean) - Optional - Include file paths in the output.
- **active** (boolean) - Optional - Show aliases for the currently active file.

### Request Example
```json
{
  "example": "GET /aliases?active=true"
}
```

### Response

#### Success Response (200)

- **aliases** (array) - List of aliases found.
- **count** (integer) - Total number of aliases (if `total` is true).

#### Response Example

```json
{
  "example": {
    "aliases": [
      "alias1",
      "alias2"
    ]
  }
}
```


--------------------------------

### Obsidian CLI: Target a Specific Vault

Source: https://help.obsidian.md/cli/index

Illustrates how to specify a target vault when running Obsidian CLI commands. This is useful when you have multiple vaults and need to ensure commands are executed in the correct one. The vault can be specified by name or ID.

```bash
# Target a vault by name
obsidian vault=Notes daily

# Target a vault by name with spaces
obsidian vault="My Vault" search query="test"
```

--------------------------------

### List Known Vaults (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Lists all vaults that Obsidian is aware of. The 'verbose' option includes the full path for each vault, and 'total' returns only the count of known vaults.

```shell
total              # return vault count
verbose            # include vault paths
```

--------------------------------

### Read Template Content (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Reads and displays the content of a specified template. Supports resolving template variables like {{date}}, {{time}}, and {{title}} when the 'resolve' option is used.

```shell
name=<template>    # (required) template name
title=<title>      # title for variable resolution

resolve            # resolve template variables
```

--------------------------------

### Read Sync Version API

Source: https://help.obsidian.md/cli/index

Reads a specific version of a file from Obsidian Sync, defaulting to the active file. Requires the version number.


## Read Sync Version

### Description
Read a sync version (default: active file).

### Method
GET

### Endpoint
/sync/read

### Parameters
#### Query Parameters
- **file** (string) - Optional - File name to read.
- **path** (string) - Optional - File path to read.
- **version** (integer) - Required - The version number to read.

### Request Example
```json
{
  "example": "GET /sync/read?file=document.md&version=2"
}
```

### Response

#### Success Response (200)

- **content** (string) - The content of the specified file version.

#### Response Example

```json
{
  "example": {
    "content": "Content of version 2."
  }
}
```


--------------------------------

### Read Property API

Source: https://help.obsidian.md/cli/index

Reads the value of a property from a specified file, defaulting to the active file. Requires the property name and optional file/path specification.


## Property Read

### Description
Read a property value from a file (default: active file).

### Method
GET

### Endpoint
/property/read

### Parameters
#### Query Parameters
- **name** (string) - Required - Property name to read.
- **file** (string) - Optional - File name to read the property from.
- **path** (string) - Optional - File path to read the property from.

### Request Example
```json
{
  "example": "GET /property/read?name=status&file=task.md"
}
```

### Response

#### Success Response (200)

- **value** (any) - The value of the requested property.

#### Response Example

```json
{
  "example": {
    "value": "in-progress"
  }
}
```


--------------------------------

### Interact with Obsidian CLI Terminal User Interface (TUI)

Source: https://help.obsidian.md/cli/index

Launches the interactive terminal user interface (TUI) for the Obsidian CLI. Once in the TUI, commands can be entered directly without the 'obsidian' prefix. Features include autocomplete, command history, and reverse search.

```bash
# Open the TUI, then run help
obsidian
help
```

--------------------------------

### Sync Status API

Source: https://help.obsidian.md/cli/index

Retrieves the current status of the Obsidian Sync service, including usage information.


## Sync Status

### Description
Show sync status and usage.

### Method
GET

### Endpoint
/sync/status

### Parameters
None

### Request Example
```json
{
  "example": "GET /sync/status"
}
```

### Response

#### Success Response (200)

- **status** (string) - Current sync status (e.g., 'active', 'paused').
- **usage** (object) - Information about sync usage (e.g., storage used, bandwidth).

#### Response Example

```json
{
  "example": {
    "status": "active",
    "usage": {
      "storage_used": "1.2 GB",
      "bandwidth_used": "500 MB"
    }
  }
}
```


--------------------------------

### Search Vault API

Source: https://help.obsidian.md/cli/index

Searches the Obsidian vault for a given query. Returns matching file paths and supports options for limiting results, specifying output format, and case sensitivity.


## Search Vault

### Description
Search vault for text. Returns matching file paths.

### Method
GET

### Endpoint
/search

### Parameters
#### Query Parameters
- **query** (string) - Required - The search query text.
- **path** (string) - Optional - Limit the search to this folder.
- **limit** (integer) - Optional - Maximum number of files to return.
- **format** (string) - Optional - Output format: `text` or `json` (default: `text`).
- **total** (boolean) - Optional - Return the total count of matches.
- **case** (boolean) - Optional - Perform a case-sensitive search.

### Request Example
```json
{
  "example": "GET /search?query=important&limit=10&format=json"
}
```

### Response

#### Success Response (200)

- **matches** (array) - List of file paths matching the query.
- **count** (integer) - Total number of matches (if `total` is true).

#### Response Example

```json
{
  "example": {
    "matches": [
      "folder/file1.md",
      "another/file2.md"
    ]
  }
}
```


--------------------------------

### Sync History API

Source: https://help.obsidian.md/cli/index

Lists the version history for a specific file in Obsidian Sync, defaulting to the active file. Supports an option to return the total count of versions.


## Sync History

### Description
List sync version history for a file (default: active file).

### Method
GET

### Endpoint
/sync/history

### Parameters
#### Query Parameters
- **file** (string) - Optional - File name to get history for.
- **path** (string) - Optional - File path to get history for.
- **total** (boolean) - Optional - Return the total count of versions.

### Request Example
```json
{
  "example": "GET /sync/history?file=document.md"
}
```

### Response

#### Success Response (200)

- **versions** (array) - List of version objects, each containing version number and timestamp.
- **count** (integer) - Total number of versions (if `total` is true).

#### Response Example

```json
{
  "example": {
    "versions": [
      {"version": 1, "timestamp": "2023-10-27T10:00:00Z"},
      {"version": 2, "timestamp": "2023-10-27T11:00:00Z"}
    ]
  }
}
```


--------------------------------

### Sync Control API

Source: https://help.obsidian.md/cli/index

Controls the Obsidian Sync service, allowing users to pause or resume synchronization.


## Sync Control

### Description
Pause or resume sync.

### Method
POST

### Endpoint
/sync

### Parameters
#### Request Body
- **on** (boolean) - Set to `true` to resume sync.
- **off** (boolean) - Set to `true` to pause sync.

### Request Example
```json
{
  "example": {
    "off": true
  }
}
```

### Response

#### Success Response (200)

- **message** (string) - Confirmation message indicating sync status change.

#### Response Example

```json
{
  "example": {
    "message": "Sync paused."
  }
}
```


--------------------------------

### List Deleted Sync Files API

Source: https://help.obsidian.md/cli/index

Lists files that have been deleted within Obsidian Sync. Supports an option to return the total count of deleted files.


## List Deleted Sync Files

### Description
List deleted files in sync.

### Method
GET

### Endpoint
/sync/deleted

### Parameters
#### Query Parameters
- **total** (boolean) - Optional - Return the total count of deleted files.

### Request Example
```json
{
  "example": "GET /sync/deleted"
}
```

### Response

#### Success Response (200)

- **deleted_files** (array) - List of deleted file names.
- **count** (integer) - Total number of deleted files (if `total` is true).

#### Response Example

```json
{
  "example": {
    "deleted_files": [
      "old_file.md",
      "temp_file.md"
    ]
  }
}
```


--------------------------------

### Restore Sync Version API

Source: https://help.obsidian.md/cli/index

Restores a specific version of a file from Obsidian Sync, defaulting to the active file. Requires the version number.


## Restore Sync Version

### Description
Restore a sync version (default: active file).

### Method
POST

### Endpoint
/sync/restore

### Parameters
#### Request Body
- **file** (string) - Optional - File name to restore.
- **path** (string) - Optional - File path to restore.
- **version** (integer) - Required - The version number to restore.

### Request Example
```json
{
  "example": {
    "file": "document.md",
    "version": 1
  }
}
```

### Response

#### Success Response (200)

- **message** (string) - Confirmation message indicating the file has been restored.

#### Response Example

```json
{
  "example": {
    "message": "File 'document.md' restored to version 1."
  }
}
```


--------------------------------

### Open Vault (Obsidian CLI - TUI Only)

Source: https://help.obsidian.md/cli/index

Switches to a different Obsidian vault. This command is only available in the Text User Interface (TUI) mode.

```shell
name=<name>        # (required) vault name
```

--------------------------------

### Vault API

Source: https://help.obsidian.md/cli/index

Commands for retrieving information about the current vault and listing known vaults. Supports specifying which info to retrieve.


## `vault`

### Description
Show information about the current vault. Allows specifying the type of info to retrieve (name, path, files, folders, size).

### Method
GET

### Endpoint
/vault

### Parameters
#### Query Parameters
- **info** (string) - Optional - return specific info only (name|path|files|folders|size)

### Response
#### Success Response (200)
- **vault_info** (object) - Object containing vault details.

#### Response Example
```json
{
  "vault_info": {
    "name": "My Obsidian Vault",
    "path": "/Users/user/Documents/Obsidian Vault",
    "files": 1500,
    "folders": 100,
    "size": "10MB"
  }
}
```


## `vaults`

### Description
List all known vaults accessible by Obsidian. Can return the total count or verbose information including paths.

### Method
GET

### Endpoint
/vaults

### Parameters
#### Query Parameters
- **total** (boolean) - Optional - return vault count
- **verbose** (boolean) - Optional - include vault paths

### Response
#### Success Response (200)
- **vaults** (array) - List of vault names or detailed vault objects.

#### Response Example
```json
{
  "vaults": [
    {"name": "Vault 1", "path": "/path/to/vault1"},
    {"name": "Vault 2", "path": "/path/to/vault2"}
  ]
}
```


## `vault:open`

### Description
Switch to a different vault. This command is typically interactive (TUI only).

### Method
POST

### Endpoint
/vault/open

### Parameters
#### Query Parameters
- **name** (string) - Required - vault name

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Switching to vault 'My Other Vault'."
}
```


--------------------------------

### Open Random Note API

Source: https://help.obsidian.md/cli/index

Opens a random note within the Obsidian vault. Can optionally limit the search to a specific folder and open the note in a new tab.


## Open Random Note

### Description
Open a random note.

### Method
GET

### Endpoint
/random

### Parameters
#### Query Parameters
- **folder** (string) - Optional - Limit the random note selection to this folder.
- **newtab** (boolean) - Optional - Open the note in a new tab.

### Request Example
```json
{
  "example": "GET /random?folder=notes&newtab=true"
}
```

### Response

#### Success Response (200)

- **path** (string) - The path to the opened random note.

#### Response Example

```json
{
  "example": {
    "path": "notes/random_note.md"
  }
}
```


--------------------------------

### Unpublish File API

Source: https://help.obsidian.md/cli/index

Unpublishes a specified file from the Obsidian Publish site. Defaults to the active file.


## Unpublish File

### Description
Unpublish a file (default: active file).

### Method
DELETE

### Endpoint
/publish/remove

### Parameters
#### Request Body
- **file** (string) - Optional - File name to unpublish.
- **path** (string) - Optional - File path to unpublish.

### Request Example
```json
{
  "example": {
    "file": "old_document.md"
  }
}
```

### Response

#### Success Response (200)

- **message** (string) - Confirmation message.

#### Response Example

```json
{
  "example": {
    "message": "File 'old_document.md' unpublished successfully."
  }
}
```


--------------------------------

### Wordcount API

Source: https://help.obsidian.md/cli/index

Command to count words and characters in a file, defaulting to the active file. Supports specifying file/path and requesting only word or character counts.


## `wordcount`

### Description
Count words and characters in a file (defaults to the active file). Options to specify file/path and retrieve only word or character counts.

### Method
GET

### Endpoint
/wordcount

### Parameters
#### Query Parameters
- **file** (string) - Optional - file name
- **path** (string) - Optional - file path
- **words** (boolean) - Optional - return word count only
- **characters** (boolean) - Optional - return character count only

### Response
#### Success Response (200)
- **word_count** (integer) - The number of words.
- **character_count** (integer) - The number of characters.

#### Response Example
```json
{
  "word_count": 1250,
  "character_count": 7500
}
```


--------------------------------

### Count Words and Characters (Obsidian CLI)

Source: https://help.obsidian.md/cli/index

Counts words and characters in a file, defaulting to the active file. Options allow returning only the word count or character count.

```shell
file=<name>        # file name
path=<path>        # file path

words              # return word count only
characters         # return character count only
```

--------------------------------

### Publish Status API

Source: https://help.obsidian.md/cli/index

Lists changes related to Obsidian Publish, including new, changed, and deleted files. Supports options to filter by change type or return the total change count.


## Publish Status

### Description
List publish changes.

### Method
GET

### Endpoint
/publish/status

### Parameters
#### Query Parameters
- **total** (boolean) - Optional - Return the total count of changes.
- **new** (boolean) - Optional - Show only new files.
- **changed** (boolean) - Optional - Show only changed files.
- **deleted** (boolean) - Optional - Show only deleted files.

### Request Example
```json
{
  "example": "GET /publish/status?changed=true"
}
```

### Response

#### Success Response (200)

- **changes** (object) - Object detailing new, changed, and deleted files.
- **count** (integer) - Total number of changes (if `total` is true).

#### Response Example

```json
{
  "example": {
    "changes": {
      "new": ["new_file.md"],
      "changed": ["updated_file.md"],
      "deleted": []
    }
  }
}
```


--------------------------------

### Read Random Note API

Source: https://help.obsidian.md/cli/index

Reads the content and path of a random note within the Obsidian vault. Can optionally limit the search to a specific folder.


## Read Random Note

### Description
Read a random note (includes path).

### Method
GET

### Endpoint
/random/read

### Parameters
#### Query Parameters
- **folder** (string) - Optional - Limit the random note selection to this folder.

### Request Example
```json
{
  "example": "GET /random/read?folder=notes"
}
```

### Response

#### Success Response (200)

- **path** (string) - The path to the random note.
- **content** (string) - The content of the random note.

#### Response Example

```json
{
  "example": {
    "path": "notes/random_note.md",
    "content": "# Random Note\nThis is the content of a random note."
  }
}
```


--------------------------------

### Remove Property API

Source: https://help.obsidian.md/cli/index

Removes a property from a specified file, defaulting to the active file. Requires the property name and optional file/path specification.


## Property Remove

### Description
Remove a property from a file (default: active file).

### Method
DELETE

### Endpoint
/property/remove

### Parameters
#### Request Body
- **name** (string) - Required - Property name to remove.
- **file** (string) - Optional - File name to remove the property from.
- **path** (string) - Optional - File path to remove the property from.

### Request Example
```json
{
  "example": {
    "name": "status",
    "file": "task.md"
  }
}
```

### Response

#### Success Response (200)

- **message** (string) - Confirmation message.

#### Response Example

```json
{
  "example": {
    "message": "Property 'status' removed successfully."
  }
}
```


=== COMPLETE CONTENT === 