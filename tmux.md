# tmux - Terminal Multiplexer

tmux is a terminal multiplexer that enables multiple terminal sessions to be created, accessed, and controlled from a single screen. It allows users to run and manage multiple programs in one terminal, detach from sessions while programs continue running in the background, and later reattach from the same or a different terminal. tmux runs on OpenBSD, FreeBSD, NetBSD, Linux, macOS, and Solaris, with dependencies on libevent 2.x and ncurses.

The core architecture revolves around a client-server model where the tmux server manages all state including sessions, windows, and panes. Sessions group one or more windows together, windows contain one or more panes arranged in various layouts, and each pane runs a terminal with a program inside it. Users interact through a client that attaches to the server, with all commands passing through a prefix key (default `C-b`) or via the command line.

## Session Management

### new-session - Create a New Session

Creates a new tmux session with optional name, starting directory, and initial command. Sessions are the top-level organizational unit that can be attached to by clients.

```bash
# Create a new session (automatically named 0, 1, 2, etc.)
tmux new-session

# Create a named session
tmux new -s mysession

# Create a detached session with a custom starting directory
tmux new -d -s dev -c ~/projects

# Create session running a specific command
tmux new -s logs 'tail -f /var/log/syslog'

# Create session with custom window name
tmux new -s work -n editor vim

# Attach to existing session or create new one if it doesn't exist
tmux new -A -s mysession

# Create detached session with specific size
tmux new -d -s mysession -x 160 -y 48
```

### attach-session - Attach to an Existing Session

Connects the current client to an existing tmux session. If no session is specified, attaches to the most recently used unattached session.

```bash
# Attach to most recent session
tmux attach

# Attach to a specific named session
tmux attach -t mysession

# Attach and detach all other clients from the session
tmux attach -d -t mysession

# Change session working directory when attaching
tmux attach -c /tmp -t mysession
```

### list-sessions - List All Sessions

Displays all available sessions in the tmux server with their window counts and creation times.

```bash
# List all sessions with default format
tmux ls
# Output:
# mysession: 2 windows (created Sat Mar 9 10:00:00 2024)
# work: 3 windows (created Sat Mar 9 09:30:00 2024)

# List sessions with custom format
tmux ls -F '#{session_id} #{session_name} #{session_windows}'
# Output:
# $0 mysession 2
# $1 work 3
```

### kill-session - Terminate a Session

Destroys the specified session, closing all windows and panes within it.

```bash
# Kill the current session
tmux kill-session

# Kill a specific session by name
tmux kill-session -t mysession

# Kill all sessions except the current one
tmux kill-session -a

# Clear all alert flags in a session without killing it
tmux kill-session -C
```

## Window Management

### new-window - Create a New Window

Creates a new window in the specified session or the current session if not specified.

```bash
# Create new window (from within tmux or command prompt)
# Key binding: C-b c
tmux new-window

# Create window with a name
tmux neww -n mywindow

# Create window without making it current
tmux neww -d -n background-tasks

# Create window at specific index
tmux neww -t :99

# Create window running a specific command
tmux neww top

# Create window with custom working directory
tmux neww -c /var/log -n logs 'tail -f syslog'

# Print the new window target for scripting
W=$(tmux neww -dPF '#{window_id}')
echo "Created window: $W"
```

### select-window - Change Current Window

Switches the current window in the attached session.

```bash
# Select window by index (key bindings: C-b 0-9)
tmux select-window -t :0
tmux selectw -t :5

# Select next window (key binding: C-b n)
tmux next-window

# Select previous window (key binding: C-b p)
tmux previous-window

# Select last window (key binding: C-b l)
tmux last-window

# Select window by name
tmux selectw -t :=editor
```

### rename-window - Rename the Current Window

Changes the name of the specified window.

```bash
# Rename current window (key binding: C-b ,)
tmux rename-window newname

# Rename a specific window
tmux renamew -t :2 mywindow
```

### kill-window - Close a Window

Destroys the specified window and all panes within it.

```bash
# Kill current window (key binding: C-b &)
tmux kill-window

# Kill specific window
tmux killw -t :3

# Kill all windows except the current one
tmux killw -a
```

### list-windows - List Windows in a Session

Shows all windows in a session with their indexes and names.

```bash
# List windows in current session
tmux list-windows
# Output:
# 0: bash* (1 panes) [158x43] [layout ab12,158x43,0,0,0] @0 (active)
# 1: vim- (2 panes) [158x43] [layout ab13,158x43,0,0{79x43,0,0,1,78x43,80,0,2}] @1

# List all windows in the server
tmux lsw -a

# Custom format showing window ID and name
tmux lsw -aF '#{window_id} #{window_name} #{window_panes}'
# Output:
# @0 bash 1
# @1 vim 2
# @2 top 1
```

## Pane Management

### split-window - Split a Pane

Divides the current pane into two panes, either horizontally or vertically.

```bash
# Split vertically (top/bottom) - key binding: C-b "
tmux split-window

# Split horizontally (left/right) - key binding: C-b %
tmux split-window -h

# Split and run a command
tmux splitw -v top

# Split without changing active pane
tmux splitw -d

# Split using full window width/height
tmux splitw -f -v

# Split with specific percentage
tmux splitw -p 30

# Split with specific number of lines/columns
tmux splitw -l 10

# Split using current pane's working directory
tmux splitw -c '#{pane_current_path}'

# Get new pane ID for scripting
P=$(tmux splitw -dPF '#{pane_id}')
echo "Created pane: $P"
```

### select-pane - Change Active Pane

Changes which pane is active within the current window.

```bash
# Select pane by direction (key bindings: C-b Up/Down/Left/Right)
tmux select-pane -U  # up
tmux select-pane -D  # down
tmux select-pane -L  # left
tmux select-pane -R  # right

# Select pane by index
tmux selectp -t 2

# Select pane by ID
tmux selectp -t %5

# Cycle through panes (key binding: C-b o)
tmux select-pane -t :.+

# Display pane numbers (key binding: C-b q)
tmux display-panes

# Set pane title
tmux selectp -T "My Pane Title"

# Mark pane for swap operations (key binding: C-b m)
tmux selectp -m

# Clear marked pane (key binding: C-b M)
tmux selectp -M
```

### resize-pane - Change Pane Size

Adjusts the dimensions of a pane within its window.

```bash
# Resize in direction (key bindings: C-b C-Up/Down/Left/Right)
tmux resize-pane -U 5    # up 5 lines
tmux resize-pane -D 5    # down 5 lines
tmux resize-pane -L 10   # left 10 columns
tmux resize-pane -R 10   # right 10 columns

# Set absolute size
tmux resizep -x 80 -y 24

# Set percentage of window
tmux resizep -x 50%

# Zoom/unzoom pane to fill window (key binding: C-b z)
tmux resize-pane -Z
```

### kill-pane - Close a Pane

Destroys the specified pane.

```bash
# Kill current pane (key binding: C-b x)
tmux kill-pane

# Kill specific pane
tmux killp -t 2

# Kill all panes except current
tmux killp -a
```

### swap-pane - Exchange Pane Positions

Swaps two panes within a window.

```bash
# Swap with previous pane (key binding: C-b {)
tmux swap-pane -U

# Swap with next pane (key binding: C-b })
tmux swap-pane -D

# Swap current pane with marked pane
tmux swap-pane

# Swap specific panes
tmux swapp -s %1 -t %2
```

### list-panes - List Panes

Displays all panes in a window or session.

```bash
# List panes in current window
tmux list-panes
# Output:
# 0: [158x21] [history 0/2000, 0 bytes] %0 (active)
# 1: [158x21] [history 0/2000, 0 bytes] %1

# List all panes in session
tmux lsp -s

# List all panes in server
tmux lsp -a

# Custom format for scripting
tmux lsp -F '#{pane_id} #{pane_width}x#{pane_height} #{pane_current_command}'
# Output:
# %0 158x21 bash
# %1 158x21 vim
```

## Key Bindings

### bind-key - Create Key Binding

Associates a key press with a tmux command.

```bash
# Bind key in prefix table (requires C-b first)
tmux bind-key x kill-pane

# Bind key in root table (no prefix needed)
tmux bind -n M-Left select-pane -L
tmux bind -n M-Right select-pane -R

# Bind with repeat (can press multiple times without prefix)
tmux bind -r h resize-pane -L 5
tmux bind -r l resize-pane -R 5

# Bind in specific key table
tmux bind -T copy-mode-vi v send -X begin-selection
tmux bind -T copy-mode-vi y send -X copy-selection-and-cancel

# Bind command sequence
tmux bind R source ~/.tmux.conf \; display "Config reloaded"

# Bind with conditional
tmux bind T if -F '#{==:#{pane_mode},copy-mode}' 'send -X history-top'
```

### unbind-key - Remove Key Binding

Removes an existing key binding.

```bash
# Unbind from prefix table
tmux unbind-key x

# Unbind from root table
tmux unbind -n M-Left

# Unbind from specific table
tmux unbind -T copy-mode C-w
```

### list-keys - Show Key Bindings

Displays all configured key bindings.

```bash
# List all keys (key binding: C-b ?)
tmux list-keys

# List keys with descriptions
tmux lsk -N

# List specific key table
tmux lsk -T prefix

# List specific key
tmux lsk -T prefix c
# Output:
# bind-key -T prefix c new-window

# Search for bindings matching pattern
tmux lsk | grep resize
```

## Options Configuration

### set-option - Set Server/Session/Window Options

Configures tmux behavior through various options.

```bash
# Set global session option
tmux set-option -g mouse on
tmux set -g history-limit 50000
tmux set -g base-index 1
tmux set -g default-terminal "tmux-256color"

# Set global window option
tmux set-option -wg mode-keys vi
tmux set -wg pane-base-index 1
tmux set -wg automatic-rename on

# Set server option
tmux set -s escape-time 10
tmux set -s default-terminal "tmux-256color"

# Unset option (restore default)
tmux set -gu mouse

# Set option for specific session
tmux set -t mysession status off

# Set option for specific window
tmux set -wt :2 synchronize-panes on

# Set with format expansion
tmux set -Fw @myvar '#{window_name}'
```

### show-options - Display Current Options

Shows the current value of tmux options.

```bash
# Show global session options
tmux show-options -g
# Output (partial):
# activity-action other
# base-index 0
# default-shell /bin/bash
# ...

# Show global window options
tmux show -wg

# Show server options
tmux show -s

# Show specific option
tmux show -g status
# Output:
# status on

# Show only the value
tmux show -gv status
# Output:
# on

# Suppress error for unknown option
tmux show -gq nonexistent-option
```

## Copy Mode and Buffers

### copy-mode - Enter Copy Mode

Enters a mode where pane content can be navigated and copied.

```bash
# Enter copy mode (key binding: C-b [)
tmux copy-mode

# Enter copy mode scrolled up one page
tmux copy-mode -u

# Enter copy mode on specific pane
tmux copy-mode -t %1

# In copy mode with emacs keys:
# C-Space  - start selection
# C-w      - copy selection and exit
# M-w      - copy selection and exit
# q        - exit copy mode
# C-r      - search backward
# C-s      - search forward

# In copy mode with vi keys:
# Space    - start selection
# Enter    - copy selection and exit
# y        - copy selection and exit
# q        - exit copy mode
# /        - search forward
# ?        - search backward
```

### paste-buffer - Paste Buffer Content

Pastes the contents of a buffer into a pane.

```bash
# Paste most recent buffer (key binding: C-b ])
tmux paste-buffer

# Paste specific buffer
tmux pasteb -b buffer0

# Paste without bracketed paste mode
tmux pasteb -p

# Delete buffer after pasting
tmux pasteb -d
```

### set-buffer - Set Buffer Content

Creates or modifies a paste buffer.

```bash
# Create buffer with content
tmux set-buffer "Hello, World!"

# Create named buffer
tmux setb -b mybuffer "Some text"

# Rename buffer
tmux setb -b buffer0 -n mybuffer

# Create buffer from command output
echo "test" | tmux loadb -
```

### list-buffers - Show All Buffers

Displays all paste buffers in the server.

```bash
# List all buffers (key binding: C-b =)
tmux list-buffers
# Output:
# buffer0: 25 bytes: "Hello, World!"
# buffer1: 100 bytes: "Some longer text..."

# Custom format
tmux lsb -F '#{buffer_name}: #{buffer_size} bytes'
```

### save-buffer / load-buffer - Buffer File Operations

Saves buffer content to a file or loads from a file.

```bash
# Save buffer to file
tmux save-buffer -b buffer0 ~/clipboard.txt

# Load file into buffer
tmux load-buffer ~/data.txt

# Load into named buffer
tmux loadb -b mydata ~/data.txt

# Pipe to buffer
echo "piped content" | tmux loadb -
```

## Information and Display

### display-message - Show or Print Message

Displays a message in the status line or prints formatted output.

```bash
# Show message in status line
tmux display-message "Hello!"

# Print to stdout (for scripting)
tmux display -p '#{session_name}'
# Output:
# mysession

# Print pane information
tmux display -p '#{pane_id} #{pane_width}x#{pane_height}'
# Output:
# %0 158x43

# Print to specific pane
tmux display -t %1 "Message for pane 1"

# Set message display duration
tmux display -d 5000 "Displayed for 5 seconds"

# Write to empty pane
echo "hello" | tmux display -I -t %5
```

### display-panes - Show Pane Numbers

Briefly displays pane numbers for quick selection.

```bash
# Display pane numbers (key binding: C-b q)
tmux display-panes

# Custom display duration (milliseconds)
tmux display-panes -d 5000

# Display without command execution
tmux displayp -N
```

### show-messages - Display Message Log

Shows the server's message log.

```bash
# Show message log (key binding: C-b ~)
tmux show-messages

# Show server information
tmux show-messages -JT
```

## Scripting and Automation

### send-keys - Send Keys to a Pane

Sends key presses to a pane as if typed.

```bash
# Send text followed by Enter
tmux send-keys "ls -la" Enter

# Send to specific pane
tmux send-keys -t %1 "cd /tmp" Enter

# Send literal text (no key lookup)
tmux send -l "Enter"

# Send function keys
tmux send F1
tmux send C-c

# Send keys with repeat count
tmux send -N 10 Up

# Copy mode commands
tmux send -X begin-selection
tmux send -X copy-selection-and-cancel
tmux send -X search-backward "pattern"
```

### run-shell - Execute Shell Command

Runs a shell command and optionally displays output.

```bash
# Run command
tmux run-shell "date >> ~/tmux.log"

# Run with format expansion
tmux run "echo Window: #{window_name} >> ~/log"

# Run in background
tmux run -b "sleep 5 && notify-send 'Done'"

# Use in key binding
tmux bind R run "~/.tmux/scripts/reload.sh"
```

### if-shell - Conditional Command

Executes commands based on shell command or format condition.

```bash
# Based on format condition
tmux if-shell -F '#{==:#{pane_mode},copy-mode}' \
    'send -X cancel' \
    'display "Not in copy mode"'

# Based on shell command
tmux if-shell "test -f ~/.tmux.local" \
    "source ~/.tmux.local"

# Check if program exists
tmux if-shell "command -v htop" \
    "bind H splitw htop" \
    "bind H splitw top"

# Used in config file
# %if #{==:#{host_short},workstation}
# source ~/.tmux.conf.work
# %endif
```

### capture-pane - Capture Pane Content

Captures the visible content of a pane to a buffer or stdout.

```bash
# Capture to stdout
tmux capture-pane -p

# Capture specific pane
tmux capturep -pt %1

# Capture with history (start to end)
tmux capturep -p -S - -E -

# Capture specific line range
tmux capturep -p -S -100 -E -50

# Capture with escape sequences (colors)
tmux capturep -pe

# Capture preserving trailing spaces
tmux capturep -pN

# Save capture to file
tmux capturep -p > ~/pane_capture.txt
```

### pipe-pane - Pipe Pane Output

Pipes pane output to a command for logging or processing.

```bash
# Start logging pane output
tmux pipe-pane -o 'cat >> ~/pane.log'

# Stop piping
tmux pipe-pane

# Toggle piping with key binding
tmux bind P pipe-pane -o 'cat >> ~/#{session_name}-#{window_index}.log'

# Send input to pane
tmux pipe-pane -I 'echo hello'
```

### wait-for - Wait for Signal

Blocks until a signal is received, useful for synchronization in scripts.

```bash
# Wait for signal
tmux wait-for mysignal &

# Send signal
tmux wait-for -S mysignal

# Lock (wait only if channel is locked)
tmux wait-for -L mysignal

# Unlock
tmux wait-for -U mysignal

# Example: wait for pane to finish
tmux send-keys "long-command; tmux wait-for -S done" Enter
tmux wait-for done
echo "Command completed"
```

## Configuration File Syntax

### source-file - Load Configuration

Loads and executes a tmux configuration file.

```bash
# Load config file
tmux source-file ~/.tmux.conf

# Shorter alias
tmux source ~/.tmux.conf

# Parse without executing (syntax check)
tmux source -n ~/.tmux.conf

# Verbose mode (print parsed commands)
tmux source -v ~/.tmux.conf

# Source with quiet mode (ignore missing file)
tmux source -q ~/.tmux.local
```

### Example Configuration File

A typical `.tmux.conf` configuration demonstrating common customizations.

```bash
# ~/.tmux.conf - Example tmux configuration

# Change prefix key to C-a
set -g prefix C-a
unbind C-b
bind C-a send-prefix

# Enable mouse support
set -g mouse on

# Set terminal type
set -s default-terminal "tmux-256color"
set -as terminal-features ",xterm-256color:RGB"

# Reduce escape time for vim
set -s escape-time 10

# Increase history limit
set -g history-limit 50000

# Start window numbering at 1
set -g base-index 1
set -wg pane-base-index 1

# Renumber windows when one is closed
set -g renumber-windows on

# Use vi keys in copy mode
set -wg mode-keys vi

# Status line customization
set -g status-position top
set -g status-style 'bg=#333333 fg=#ffffff'
set -g status-left '[#S] '
set -g status-right '%H:%M %d-%b-%y'

# Pane border colors
set -g pane-border-style 'fg=#555555'
set -g pane-active-border-style 'fg=#00ff00'

# Split panes using | and -
bind | split-window -h -c '#{pane_current_path}'
bind - split-window -v -c '#{pane_current_path}'

# Vim-style pane navigation
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R

# Resize panes with vim keys
bind -r H resize-pane -L 5
bind -r J resize-pane -D 5
bind -r K resize-pane -U 5
bind -r L resize-pane -R 5

# Reload config
bind R source ~/.tmux.conf \; display "Config reloaded!"

# Copy mode bindings (vi-style)
bind -T copy-mode-vi v send -X begin-selection
bind -T copy-mode-vi y send -X copy-selection-and-cancel

# Conditional configuration based on tmux version
%if #{>=:#{version},3.2}
set -g extended-keys on
%endif
```

## Layouts and Organization

### select-layout - Apply Window Layout

Applies a predefined or custom layout to the current window.

```bash
# Apply even-horizontal layout (key binding: C-b M-1)
tmux select-layout even-horizontal

# Apply even-vertical layout (key binding: C-b M-2)
tmux select-layout even-vertical

# Apply main-horizontal layout (key binding: C-b M-3)
tmux select-layout main-horizontal

# Apply main-vertical layout (key binding: C-b M-4)
tmux select-layout main-vertical

# Apply tiled layout (key binding: C-b M-5)
tmux select-layout tiled

# Cycle through layouts (key binding: C-b Space)
tmux next-layout

# Apply custom layout string
tmux selectlay "bb62,159x48,0,0{79x48,0,0,0,79x48,80,0,1}"
```

### choose-tree - Interactive Session/Window Browser

Opens an interactive tree view for selecting sessions, windows, or panes.

```bash
# Show sessions collapsed (key binding: C-b s)
tmux choose-tree -s

# Show windows expanded (key binding: C-b w)
tmux choose-tree -w

# Show with custom format
tmux choose-tree -F '#{window_name}: #{pane_current_command}'

# Filter results
tmux choose-tree -f '#{==:#{session_name},mysession}'

# Run command on selection
tmux choose-tree 'kill-window -t %%'
```

## Summary

tmux provides a comprehensive terminal multiplexing solution that excels in remote server management, multi-tasking workflows, and session persistence. Its client-server architecture ensures that sessions survive network disconnections and terminal closures, making it invaluable for system administrators, developers, and anyone working extensively in terminal environments. The hierarchical organization of sessions, windows, and panes provides flexible workspace management, while the extensive command set enables both interactive use and sophisticated scripting.

For integration, tmux works seamlessly with shell scripts through its command-line interface, supports format strings for dynamic content generation, and provides hooks for event-driven automation. Common integration patterns include using tmux for CI/CD job management, creating development environment scripts that set up multiple windows and panes with specific applications, and building terminal-based dashboards. The configuration system supports conditional logic and modular configuration files, enabling complex setups that adapt to different environments and use cases.
