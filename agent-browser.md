# agent-browser

agent-browser is a headless browser automation CLI designed specifically for AI agents. Built as a native Rust binary that communicates with Chrome/Chromium via CDP (Chrome DevTools Protocol), it provides fast, deterministic browser control with sub-millisecond command parsing. The core workflow uses compact "refs" (`@e1`, `@e2`) from accessibility snapshots to identify and interact with elements, reducing token usage from ~3000-5000 to ~200-400 tokens per interaction.

The CLI supports multiple sessions, persistent profiles, authentication state management, and cloud browser providers (Browserless, Browserbase, Browser Use, Kernel). It includes security features for production AI deployments: domain allowlists, action policies, content boundary markers to prevent prompt injection, and an encrypted credential vault. The architecture uses a client-daemon model where the daemon persists between commands for fast subsequent operations.

## Installation

Install agent-browser globally and download Chrome for automation.

```bash
# Global installation (recommended)
npm install -g agent-browser
agent-browser install  # Downloads Chrome from Chrome for Testing

# Alternative: Homebrew (macOS)
brew install agent-browser
agent-browser install

# Alternative: Cargo (Rust)
cargo install agent-browser
agent-browser install

# Quick start without global install
npx agent-browser install
npx agent-browser open example.com
```

## Core Workflow: Navigate, Snapshot, Interact

The fundamental pattern for all browser automation with agent-browser.

```bash
# 1. Navigate to page
agent-browser open https://example.com/login

# 2. Wait for page to load
agent-browser wait --load networkidle

# 3. Get element refs from accessibility snapshot
agent-browser snapshot -i
# Output:
# @e1 [input type="email"] placeholder="Email"
# @e2 [input type="password"] placeholder="Password"
# @e3 [button] "Sign In"

# 4. Interact using refs
agent-browser fill @e1 "user@example.com"
agent-browser fill @e2 "password123"
agent-browser click @e3

# 5. Wait for navigation and re-snapshot (refs invalidate on page change!)
agent-browser wait --url "**/dashboard"
agent-browser snapshot -i
```

## Command Chaining

Chain multiple commands efficiently in a single shell invocation.

```bash
# Chain open + wait + snapshot (no intermediate output needed)
agent-browser open https://example.com && agent-browser wait --load networkidle && agent-browser snapshot -i

# Chain multiple interactions
agent-browser fill @e1 "user@example.com" && agent-browser fill @e2 "password" && agent-browser click @e3

# Navigate and capture screenshot
agent-browser open https://example.com && agent-browser wait --load networkidle && agent-browser screenshot page.png
```

## Snapshot Command Options

Get page structure with element refs for interaction.

```bash
# Interactive elements only (recommended for most use cases)
agent-browser snapshot -i
# Output: @e1 [button] "Submit", @e2 [input type="email"], etc.

# Include cursor-interactive elements (divs with onclick, cursor:pointer)
agent-browser snapshot -i -C

# Compact output (remove empty structural elements)
agent-browser snapshot -c

# Limit tree depth
agent-browser snapshot -d 3

# Scope to specific CSS selector
agent-browser snapshot -s "#main-form"

# Combine options
agent-browser snapshot -i -c -d 5

# JSON output for programmatic parsing
agent-browser snapshot -i --json
# {"success":true,"data":{"snapshot":"...","refs":{"e1":{"role":"button","name":"Submit"},...}}}
```

## Click and Form Interactions

Click elements, fill forms, and interact with page controls.

```bash
# Click using ref from snapshot
agent-browser click @e1

# Click and open in new tab
agent-browser click @e1 --new-tab

# Double-click
agent-browser dblclick @e1

# Fill input (clears existing value first)
agent-browser fill @e2 "user@example.com"

# Type without clearing
agent-browser type @e2 "additional text"

# Select dropdown option
agent-browser select @e1 "California"

# Select multiple options
agent-browser select @e1 "Option A" "Option B"

# Checkbox/radio
agent-browser check @e1
agent-browser uncheck @e1

# Press keys
agent-browser press Enter
agent-browser press Tab
agent-browser press Control+a

# Keyboard input at current focus (no selector)
agent-browser keyboard type "Hello World"
agent-browser keyboard inserttext "Text without key events"

# Scroll page
agent-browser scroll down 500
agent-browser scroll up 300
agent-browser scroll down 500 --selector "div.content"  # Scroll within container

# Scroll element into view
agent-browser scrollintoview @e1

# Drag and drop
agent-browser drag @e1 @e2

# File upload
agent-browser upload @e1 /path/to/file.pdf
```

## Wait Commands

Wait for elements, network activity, URLs, or JavaScript conditions.

```bash
# Wait for element to be visible
agent-browser wait @e1
agent-browser wait "#loading-spinner"

# Wait for element to disappear
agent-browser wait "#spinner" --state hidden

# Wait for network activity to settle
agent-browser wait --load networkidle
agent-browser wait --load domcontentloaded

# Wait for URL pattern (useful after redirects)
agent-browser wait --url "**/dashboard"
agent-browser wait --url "**/success"

# Wait for text to appear (substring match)
agent-browser wait --text "Welcome back"

# Wait for text to disappear
agent-browser wait --fn "!document.body.innerText.includes('Loading...')"

# Wait for JavaScript condition
agent-browser wait --fn "window.ready === true"
agent-browser wait --fn "document.readyState === 'complete'"

# Wait fixed duration (milliseconds)
agent-browser wait 2000
```

## Get Information

Extract text, HTML, attributes, and page metadata.

```bash
# Get element text
agent-browser get text @e1
agent-browser get text body > page-content.txt

# Get innerHTML
agent-browser get html @e1

# Get input value
agent-browser get value @e1

# Get attribute
agent-browser get attr @e1 href
agent-browser get attr @e1 data-id

# Get page metadata
agent-browser get title    # Page title
agent-browser get url      # Current URL
agent-browser get cdp-url  # CDP WebSocket URL (for debugging)

# Count matching elements
agent-browser get count ".item"
agent-browser get count "button"

# Get bounding box
agent-browser get box @e1
# {"x":100,"y":200,"width":150,"height":40}

# Get computed styles
agent-browser get styles @e1
# {"font":"16px Arial","color":"rgb(0,0,0)",...}

# Check element state
agent-browser is visible @e1
agent-browser is enabled @e1
agent-browser is checked @e1
```

## Screenshots and PDF

Capture visual output of web pages.

```bash
# Screenshot to temporary directory (path returned in output)
agent-browser screenshot
# Screenshot saved to /tmp/screenshot-2024-01-15T10-30-00-abc123.png

# Screenshot to specific path
agent-browser screenshot ./output/page.png

# Full page screenshot (captures entire scrollable content)
agent-browser screenshot --full ./output/fullpage.png

# Annotated screenshot with numbered element labels
agent-browser screenshot --annotate
# Output includes image path and legend:
#   [1] @e1 button "Submit"
#   [2] @e2 link "Home"
#   [3] @e3 textbox "Email"
# Refs are cached, so you can immediately: agent-browser click @e2

# Custom directory
agent-browser screenshot --screenshot-dir ./screenshots

# JPEG format with quality
agent-browser screenshot --screenshot-format jpeg --screenshot-quality 80

# Save as PDF
agent-browser pdf ./output/page.pdf
```

## Semantic Locators

Find elements by role, text, label, or test ID instead of refs.

```bash
# Find by ARIA role
agent-browser find role button click --name "Submit"
agent-browser find role textbox fill "user@example.com" --name "Email"
agent-browser find role link click --name "Home"

# Find by visible text
agent-browser find text "Sign In" click
agent-browser find text "Sign In" click --exact  # Exact match only

# Find by label
agent-browser find label "Email" fill "user@example.com"
agent-browser find label "Password" fill "secret123"

# Find by placeholder
agent-browser find placeholder "Search" type "query"
agent-browser find placeholder "Enter your email" fill "user@example.com"

# Find by alt text (images)
agent-browser find alt "Company Logo" click

# Find by title attribute
agent-browser find title "Close dialog" click

# Find by data-testid
agent-browser find testid "submit-btn" click
agent-browser find testid "email-input" fill "user@example.com"

# Find nth element
agent-browser find first ".item" click
agent-browser find last ".item" click
agent-browser find nth 2 "a" hover
```

## Session Management

Run multiple isolated browser instances concurrently.

```bash
# Named sessions for isolation
agent-browser --session site1 open https://site-a.com
agent-browser --session site2 open https://site-b.com

# Commands are isolated by session
agent-browser --session site1 snapshot -i
agent-browser --session site2 snapshot -i

# List active sessions
agent-browser session list
# Active sessions:
# -> default
#    site1
#    site2

# Show current session
agent-browser session

# Close specific session
agent-browser --session site1 close

# Environment variable alternative
AGENT_BROWSER_SESSION=site1 agent-browser snapshot -i
```

## Authentication State Management

Save and restore authentication state for reuse across sessions.

```bash
# Method 1: Import from running Chrome (fastest for one-off tasks)
# Start Chrome with: google-chrome --remote-debugging-port=9222
# Log into your sites, then:
agent-browser --auto-connect state save ./my-auth.json
agent-browser --state ./my-auth.json open https://app.example.com/dashboard

# Method 2: Persistent profile (simplest for recurring tasks)
agent-browser --profile ~/.myapp-profile open https://app.example.com/login
# ... complete login flow ...
# All future runs are already authenticated:
agent-browser --profile ~/.myapp-profile open https://app.example.com/dashboard

# Method 3: Session name (auto-save/restore cookies + localStorage)
agent-browser --session-name myapp open https://app.example.com/login
# ... login flow ...
agent-browser close  # State auto-saved to ~/.agent-browser/sessions/
# Next time: state auto-restored
agent-browser --session-name myapp open https://app.example.com/dashboard

# Method 4: Manual state save/load
agent-browser state save ./auth-state.json
agent-browser state load ./auth-state.json

# Encrypt state at rest
export AGENT_BROWSER_ENCRYPTION_KEY=$(openssl rand -hex 32)
agent-browser --session-name secure open https://app.example.com

# Manage saved states
agent-browser state list
agent-browser state show myapp-default.json
agent-browser state clear myapp
agent-browser state clean --older-than 7
```

## Authentication Vault

Store credentials securely and login by name (credentials never exposed to LLM).

```bash
# Save credentials (pipe password via stdin to avoid shell history)
echo "mypassword" | agent-browser auth save github \
  --url https://github.com/login \
  --username myuser \
  --password-stdin

# Login using saved profile
agent-browser auth login github

# List saved profiles (names and URLs only, no secrets)
agent-browser auth list
# github - https://github.com/login
# myapp - https://app.example.com/login

# Show profile metadata
agent-browser auth show github

# Delete a profile
agent-browser auth delete github

# Custom selectors (if auto-detection fails)
agent-browser auth save myapp \
  --url https://app.example.com/login \
  --username user --password pass \
  --username-selector "#email" \
  --password-selector "#password" \
  --submit-selector "button.login"
```

## JavaScript Evaluation

Run JavaScript in the browser context.

```bash
# Simple expressions
agent-browser eval 'document.title'
agent-browser eval 'document.querySelectorAll("img").length'
agent-browser eval 'window.location.href'

# Complex JS with heredoc (recommended for multiline/nested quotes)
agent-browser eval --stdin <<'EVALEOF'
JSON.stringify(
  Array.from(document.querySelectorAll("img"))
    .filter(i => !i.alt)
    .map(i => ({ src: i.src.split("/").pop(), width: i.width }))
)
EVALEOF

# Base64 encoding (avoids all shell escaping issues)
agent-browser eval -b "$(echo -n 'Array.from(document.querySelectorAll("a")).map(a => a.href)' | base64)"

# Pipe script from file
cat myscript.js | agent-browser eval --stdin
```

## Cookies and Storage

Manage browser cookies and storage.

```bash
# Get all cookies
agent-browser cookies

# Set cookie
agent-browser cookies set session_token "abc123xyz"
agent-browser cookies set auth_cookie "value123"

# Clear all cookies
agent-browser cookies clear

# localStorage
agent-browser storage local              # Get all
agent-browser storage local key          # Get specific key
agent-browser storage local set key val  # Set value
agent-browser storage local clear        # Clear all

# sessionStorage
agent-browser storage session
agent-browser storage session key
agent-browser storage session set key val
agent-browser storage session clear
```

## Network Interception

Intercept, mock, or block network requests.

```bash
# Intercept requests matching URL pattern
agent-browser network route "**/api/*"

# Block requests
agent-browser network route "**/analytics/*" --abort

# Mock response
agent-browser network route "**/api/user" --body '{"id":1,"name":"Test User"}'

# Remove route
agent-browser network unroute "**/api/*"
agent-browser network unroute  # Remove all routes

# View tracked requests
agent-browser network requests
agent-browser network requests --filter api
```

## Tabs and Windows

Manage browser tabs and windows.

```bash
# List open tabs
agent-browser tab

# Open new tab
agent-browser tab new
agent-browser tab new https://example.com

# Switch to tab by index (0-based)
agent-browser tab 0
agent-browser tab 2

# Close current tab
agent-browser tab close

# Close specific tab
agent-browser tab close 2

# Open new window
agent-browser window new
```

## Viewport and Device Emulation

Set viewport size and emulate devices.

```bash
# Set viewport size (default: 1280x720)
agent-browser set viewport 1920 1080

# Retina/HiDPI (2x pixel density, same CSS layout)
agent-browser set viewport 1920 1080 2
agent-browser screenshot retina.png  # Higher resolution output

# Mobile viewport
agent-browser set viewport 375 812

# Device emulation (viewport + user agent)
agent-browser set device "iPhone 14"
agent-browser set device "iPad Pro"
agent-browser set device "Pixel 7"

# Geolocation
agent-browser set geo 37.7749 -122.4194  # San Francisco

# Color scheme / dark mode
agent-browser set media dark
agent-browser set media light
AGENT_BROWSER_COLOR_SCHEME=dark agent-browser open https://example.com

# Offline mode
agent-browser set offline on
agent-browser set offline off

# HTTP headers (scoped to origin)
agent-browser open https://api.example.com --headers '{"Authorization": "Bearer token123"}'

# HTTP basic auth
agent-browser set credentials username password
```

## Diff (Compare Page States)

Compare snapshots or screenshots for regression testing.

```bash
# Compare current snapshot vs last snapshot in session
agent-browser snapshot -i          # Take baseline
agent-browser click @e2            # Perform action
agent-browser diff snapshot        # See what changed (+/- format)

# Compare against saved baseline file
agent-browser diff snapshot --baseline before.txt

# Scoped comparison
agent-browser diff snapshot --selector "#main" --compact

# Visual pixel diff
agent-browser diff screenshot --baseline before.png
agent-browser diff screenshot --baseline before.png -o diff.png  # Save diff image
agent-browser diff screenshot --baseline before.png -t 0.2       # Adjust threshold

# Compare two URLs
agent-browser diff url https://staging.example.com https://prod.example.com
agent-browser diff url https://v1.example.com https://v2.example.com --screenshot
agent-browser diff url https://v1.com https://v2.com --wait-until networkidle
agent-browser diff url https://v1.com https://v2.com --selector "#main"
```

## Video Recording

Record browser sessions for debugging and documentation.

```bash
# Start recording
agent-browser record start ./demo.webm

# Perform actions...
agent-browser open https://example.com
agent-browser snapshot -i
agent-browser click @e1
agent-browser fill @e2 "test"

# Stop and save
agent-browser record stop
# Video saved to ./demo.webm

# Restart with new file
agent-browser record restart ./take2.webm
```

## Debugging

Tools for debugging automation scripts.

```bash
# Show browser window
agent-browser --headed open https://example.com

# Highlight element
agent-browser highlight @e1

# Open Chrome DevTools
agent-browser inspect

# View console messages
agent-browser console
agent-browser console --clear

# View page errors
agent-browser errors
agent-browser errors --clear

# Chrome DevTools profiling
agent-browser profiler start
# ... perform actions ...
agent-browser profiler stop trace.json

# Trace recording
agent-browser trace start
# ... perform actions ...
agent-browser trace stop trace.zip

# Connect to existing Chrome with remote debugging
agent-browser --auto-connect snapshot
agent-browser --cdp 9222 snapshot
agent-browser connect 9222
```

## iOS Simulator (Mobile Safari)

Control real Mobile Safari in iOS Simulator (macOS only).

```bash
# Prerequisites: macOS + Xcode + Appium
npm install -g appium
appium driver install xcuitest

# List available iOS simulators
agent-browser device list

# Launch Safari on specific device
agent-browser -p ios --device "iPhone 16 Pro" open https://example.com

# Same workflow as desktop
agent-browser -p ios snapshot -i
agent-browser -p ios tap @e1          # Tap = click
agent-browser -p ios fill @e2 "text"
agent-browser -p ios screenshot mobile.png

# Mobile-specific gestures
agent-browser -p ios swipe up
agent-browser -p ios swipe down 500

# Close session
agent-browser -p ios close

# Environment variables alternative
export AGENT_BROWSER_PROVIDER=ios
export AGENT_BROWSER_IOS_DEVICE="iPhone 16 Pro"
agent-browser open https://example.com
```

## Cloud Browser Providers

Connect to cloud browser infrastructure.

```bash
# Browserless
export BROWSERLESS_API_KEY="your-api-token"
agent-browser -p browserless open https://example.com

# Browserbase
export BROWSERBASE_API_KEY="your-api-key"
agent-browser -p browserbase open https://example.com

# Browser Use
export BROWSER_USE_API_KEY="your-api-key"
agent-browser -p browseruse open https://example.com

# Kernel
export KERNEL_API_KEY="your-api-key"
agent-browser -p kernel open https://example.com

# Or via environment variable
export AGENT_BROWSER_PROVIDER=browserless
agent-browser open https://example.com
```

## Security Features

Protect AI agent deployments from credential exposure and prompt injection.

```bash
# Domain allowlist (restrict navigation)
agent-browser --allowed-domains "example.com,*.example.com" open https://example.com
export AGENT_BROWSER_ALLOWED_DOMAINS="myapp.com,*.myapp.com,cdn.example.com"

# Content boundary markers (help LLMs distinguish tool output from page content)
agent-browser --content-boundaries snapshot
# Output wrapped in:
# --- AGENT_BROWSER_PAGE_CONTENT nonce=<hex> origin=https://example.com ---
# [snapshot content]
# --- END_AGENT_BROWSER_PAGE_CONTENT nonce=<hex> ---

export AGENT_BROWSER_CONTENT_BOUNDARIES=1

# Action policy (gate dangerous actions)
# policy.json: {"default":"deny","allow":["navigate","snapshot","click","scroll","wait","get"]}
agent-browser --action-policy ./policy.json open https://example.com
export AGENT_BROWSER_ACTION_POLICY=./policy.json

# Output length limits (prevent context flooding)
agent-browser --max-output 50000 get text body
export AGENT_BROWSER_MAX_OUTPUT=50000

# Action confirmation (require explicit approval)
agent-browser --confirm-actions eval,download eval "document.title"
# Returns confirmation_required response, then:
agent-browser confirm c_8f3a1234
agent-browser deny c_8f3a1234
```

## Configuration File

Set persistent defaults in `agent-browser.json`.

```json
{
  "headed": true,
  "proxy": "http://localhost:8080",
  "profile": "./browser-data",
  "userAgent": "my-agent/1.0",
  "ignoreHttpsErrors": true,
  "contentBoundaries": true,
  "maxOutput": 50000,
  "allowedDomains": ["myapp.com", "*.myapp.com"],
  "colorScheme": "dark",
  "downloadPath": "./downloads",
  "screenshotDir": "./screenshots",
  "screenshotFormat": "png"
}
```

```bash
# Load custom config file
agent-browser --config ./ci-config.json open https://example.com
AGENT_BROWSER_CONFIG=./ci-config.json agent-browser open https://example.com

# Priority (lowest to highest):
# ~/.agent-browser/config.json < ./agent-browser.json < env vars < CLI flags
```

## Environment Variables

Key environment variables for configuration.

```bash
# Session and state
export AGENT_BROWSER_SESSION="mysession"
export AGENT_BROWSER_SESSION_NAME="myapp"
export AGENT_BROWSER_PROFILE="~/.myapp-profile"
export AGENT_BROWSER_STATE="./auth.json"

# Browser settings
export AGENT_BROWSER_EXECUTABLE_PATH="/path/to/chrome"
export AGENT_BROWSER_ENGINE="chrome"  # or "lightpanda"
export AGENT_BROWSER_HEADED=1
export AGENT_BROWSER_COLOR_SCHEME="dark"

# Security
export AGENT_BROWSER_ENCRYPTION_KEY="64-char-hex-key"
export AGENT_BROWSER_ALLOWED_DOMAINS="example.com,*.example.com"
export AGENT_BROWSER_CONTENT_BOUNDARIES=1
export AGENT_BROWSER_MAX_OUTPUT=50000
export AGENT_BROWSER_ACTION_POLICY="./policy.json"

# Cloud providers
export AGENT_BROWSER_PROVIDER="browserless"
export BROWSERLESS_API_KEY="your-key"
export BROWSERBASE_API_KEY="your-key"

# Timeouts
export AGENT_BROWSER_DEFAULT_TIMEOUT=25000
export AGENT_BROWSER_IDLE_TIMEOUT_MS=60000
```

## Complete Form Automation Example

End-to-end example of form filling with validation.

```bash
#!/bin/bash
set -euo pipefail

FORM_URL="https://example.com/signup"

# Navigate and wait for load
agent-browser open "$FORM_URL"
agent-browser wait --load networkidle

# Get form structure
agent-browser snapshot -i
# @e1 [input type="text"] placeholder="Full Name"
# @e2 [input type="email"] placeholder="Email"
# @e3 [input type="password"] placeholder="Password"
# @e4 [select] "Country"
# @e5 [checkbox] "I agree to terms"
# @e6 [button] "Sign Up"

# Fill form fields
agent-browser fill @e1 "Jane Doe"
agent-browser fill @e2 "jane@example.com"
agent-browser fill @e3 "SecureP@ss123"
agent-browser select @e4 "United States"
agent-browser check @e5

# Submit and wait for result
agent-browser click @e6
agent-browser wait --url "**/welcome"

# Verify success
agent-browser snapshot -i
agent-browser screenshot ./signup-complete.png

# Save auth state for future use
agent-browser state save ./auth-state.json

# Cleanup
agent-browser close
```

## Complete Data Extraction Example

Extract content from web pages with screenshots.

```bash
#!/bin/bash
set -euo pipefail

TARGET_URL="https://example.com/products"
OUTPUT_DIR="./output"
mkdir -p "$OUTPUT_DIR"

# Navigate
agent-browser open "$TARGET_URL"
agent-browser wait --load networkidle

# Get metadata
TITLE=$(agent-browser get title)
URL=$(agent-browser get url)
echo "Title: $TITLE"
echo "URL: $URL"

# Capture screenshots
agent-browser screenshot "$OUTPUT_DIR/viewport.png"
agent-browser screenshot --full "$OUTPUT_DIR/fullpage.png"
agent-browser screenshot --annotate "$OUTPUT_DIR/annotated.png"

# Extract content
agent-browser snapshot -i > "$OUTPUT_DIR/structure.txt"
agent-browser get text body > "$OUTPUT_DIR/text.txt"
agent-browser pdf "$OUTPUT_DIR/page.pdf"

# Extract specific elements
agent-browser snapshot -i
agent-browser get text @e5 > "$OUTPUT_DIR/main-content.txt"

# Handle infinite scroll
for i in {1..5}; do
    agent-browser scroll down 1000
    agent-browser wait 1000
done
agent-browser screenshot --full "$OUTPUT_DIR/scrolled.png"

# Cleanup
agent-browser close
echo "Extraction complete: $OUTPUT_DIR"
```

## Summary

agent-browser is optimized for AI agent workflows where token efficiency and deterministic element selection are critical. The snapshot-ref pattern (`snapshot -i` to get refs, then `click @e1` or `fill @e2 "value"`) provides a 10-15x reduction in context usage compared to traditional DOM-based automation. The CLI handles browser lifecycle automatically through its daemon architecture, so commands can be chained efficiently or run independently.

For production AI deployments, enable security features: `--content-boundaries` to prevent prompt injection from malicious page content, `--allowed-domains` to restrict navigation to trusted sites, `--action-policy` to gate destructive actions, and the auth vault (`auth save`/`auth login`) to keep credentials out of LLM context. The tool integrates with cloud browser providers for serverless deployments and supports iOS Simulator for mobile web testing. Configuration can be set via JSON files, environment variables, or CLI flags with clear precedence rules.
