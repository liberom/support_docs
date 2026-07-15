# Kitty Terminal Emulator

Kitty is a fast, feature-rich, GPU-based terminal emulator designed for power keyboard users. It is written in a mix of C (for performance-critical parts), Python (for extensibility), and Go (for command-line tools called "kittens"). Kitty uses OpenGL for rendering, supports true color, ligatures, Unicode, and provides advanced features like image display, multiple layouts, tabs, and a powerful remote control system.

The terminal supports modern features including an innovative graphics protocol for displaying images directly in the terminal, a comprehensive keyboard protocol adopted by many other terminals and applications, shell integration for seamless interaction with common shells, and an extensible kitten framework for creating custom terminal programs. Kitty can be controlled remotely via scripts, supports sessions for complex window arrangements, and includes built-in tools for SSH, file diffing, clipboard management, and more.

## Remote Control API

The remote control system allows scripts and programs to control kitty from the command line, including opening windows, sending text, changing colors, and managing layouts. Remote control must be enabled in the configuration via `allow_remote_control` or by using password-based authentication.

```bash
# Start kitty with remote control enabled
kitty -o allow_remote_control=yes -o enabled_layouts=tall

# Launch a new window running cat and keep focus on current window
kitten @ launch --title Output --keep-focus cat

# Send text to a window matching a specific command line
kitten @ send-text --match cmdline:cat Hello, World

# Pipe command output to another window
ls | kitten @ send-text --match 'title:^Output' --stdin

# Open a new tab with a custom title
kitten @ launch --type=tab --tab-title "My Tab" --keep-focus bash

# Change tab title
kitten @ set-tab-title --match 'title:^My' New Title

# Focus a specific window
kitten @ focus-window --match 'title:^Output'

# Get JSON listing of all windows and tabs
kitten @ ls

# Remote control via socket (from outside kitty)
kitty -o allow_remote_control=yes --listen-on unix:/tmp/mykitty
kitten @ --to unix:/tmp/mykitty ls

# Password-protected remote control
# In kitty.conf: remote_control_password "control colors" get-colors set-colors
kitten @ --password="control colors" set-colors background=red
```

## Graphics Protocol

The graphics protocol allows displaying arbitrary pixel graphics in the terminal. Images integrate with text, support alpha blending, and scroll with content. The protocol is also implemented in other terminals like WezTerm, Ghostty, and iTerm2.

```bash
# Display an image using the icat kitten
kitten icat path/to/image.png

# Display image with specific placement
kitten icat --place 80x24@0x0 image.png

# Display image over SSH
kitten icat --transfer-mode=stream image.png
```

```python
#!/usr/bin/env python
# Minimal PNG display script using graphics protocol
import sys
from base64 import standard_b64encode

first, eof, buf = True, False, memoryview(bytearray(3 * 4096 // 4))
w = sys.stdout.buffer.write
with open(sys.argv[-1], 'rb') as f:
    while not eof:
        p = buf[:]
        while p and not eof:
            n = f.readinto1(p)
            p, eof = p[n:], n == 0
        encoded = standard_b64encode(buf[:len(buf)-len(p)])
        metadata, first = "a=T,f=100," if first else "", False
        w(f'\x1b_G{metadata}m={0 if eof else 1};'.encode('ascii'))
        w(encoded)
        w(b'\x1b\\')
```

```c
// Get terminal window size in pixels for image positioning
#include <stdio.h>
#include <sys/ioctl.h>

int main(int argc, char **argv) {
    struct winsize sz;
    ioctl(0, TIOCGWINSZ, &sz);
    printf("rows: %i, cols: %i, width: %i, height: %i\n",
           sz.ws_row, sz.ws_col, sz.ws_xpixel, sz.ws_ypixel);
    return 0;
}
```

## Keyboard Protocol

Kitty's keyboard protocol solves limitations of traditional terminal keyboard handling, supporting all modifier keys, distinguishing key press/release/repeat events, and eliminating ambiguous escape codes. The protocol is backward compatible and progressively enhanceable.

```bash
# Test keyboard protocol - shows all key events with full information
kitten show-key -m kitty
```

```python
# Enable enhanced keyboard mode in your application
# Send at startup (or when entering alternate screen):
print('\x1b[>1u', end='', flush=True)  # Enable disambiguate mode

# Key events arrive as: CSI unicode-key-code ; modifiers u
# For example, Ctrl+Shift+A: \x1b[97;6u
# Where 97 = 'a', 6 = shift(1) + ctrl(4)

# Restore keyboard mode at exit:
print('\x1b[<u', end='', flush=True)

# Modifier encoding (bit field):
# shift=1, alt=2, ctrl=4, super=8, hyper=16, meta=32, caps_lock=64, num_lock=128
```

## Desktop Notifications

The OSC 99 escape code displays desktop notifications from terminal applications, supporting titles, bodies, click actions, and close events.

```bash
# Simple notification
printf '\x1b]99;;Hello world\x1b\\'

# Notification with title and body (chunked)
printf '\x1b]99;i=1:d=0;Hello world\x1b\\'
printf '\x1b]99;i=1:p=body;This is cool\x1b\\'

# Using the notify kitten (recommended)
kitten notify "Hello world" A good day to you

# Notification with report action (app receives callback when clicked)
printf '\x1b]99;i=myid:a=report;Click me\x1b\\'
# Terminal sends back: \x1b]99;i=myid;\x1b\\ when clicked

# Notification with close event reporting
printf '\x1b]99;i=myid:c=1;Hello\x1b\\'
# Terminal sends: \x1b]99;i=myid:p=close;\x1b\\ when closed
```

## Launch Command

The launch command creates new windows, tabs, or overlays with extensive options for program execution, input piping, and environment control.

```conf
# Basic launch mappings in kitty.conf
map f1 launch                              # New window with shell
map f2 launch vim path/to/file             # Launch vim
map f3 launch --cwd=current                # New window, same directory
map f4 launch --type=tab                   # New tab
map f5 launch --type=overlay htop          # Overlay window

# Pipe scrollback to a program
map f6 launch --stdin-source=@screen_scrollback less +G -R

# Launch with specific environment
map f7 launch --env MY_VAR=value zsh

# Launch with remote control permissions
map f8 launch --allow-remote-control some_program

# Action alias for common patterns
action_alias launch_tab launch --cwd=current --type=tab
map f9 launch_tab vim
map f10 launch_tab emacs
```

```python
# Window watcher example (~/.config/kitty/mywatcher.py)
from kitty.boss import Boss
from kitty.window import Window

def on_resize(boss: Boss, window: Window, data: dict) -> None:
    # Called when window is resized
    # data contains old_geometry and new_geometry
    pass

def on_focus_change(boss: Boss, window: Window, data: dict) -> None:
    # data contains 'focused' boolean
    pass

def on_close(boss: Boss, window: Window, data: dict) -> None:
    # Called when window is closed
    pass

# Use watcher: map f1 launch --watcher mywatcher.py some_program
```

## SSH Kitten

The SSH kitten provides enhanced SSH with automatic shell integration, config file copying, and connection reuse.

```bash
# Basic SSH with shell integration
kitten ssh some-hostname

# Create alias in shell rc file
alias s="kitten ssh"

# Pass kitten-specific options
kitten ssh --kitten interpreter=python servername
```

```conf
# ~/.config/kitty/ssh.conf
# Copy shell configuration files to remote
copy .zshrc .vimrc .vim

# Set environment variables
env SOME_VAR=x
env COPIED_VAR=_kitty_copy_env_var_  # Copy local value

# Per-hostname settings
hostname myserver-*
copy --dest my-conf/zsh/.zshrc .zshrc
env ZDOTDIR=$HOME/my-conf/zsh

hostname someuser@somehost
copy --glob some/files.*
```

## Themes Kitten

The themes kitten provides interactive theme selection with live preview from over 300 pre-built themes.

```bash
# Interactive theme selection
kitten themes

# Non-interactive theme change
kitten themes --reload-in=all "Dimmed Monokai"

# Create custom theme: ~/.config/kitty/themes/My Theme.conf
# Then run: kitten themes
# Select "My Theme" to apply
```

## Diff Kitten

A side-by-side diff tool with syntax highlighting and image support.

```bash
# Compare two files
kitten diff file1 file2

# Compare directories recursively
kitten diff dir1 dir2

# Create alias
alias d="kitten diff"
```

```ini
# Git integration (~/.gitconfig)
[diff]
    tool = kitty
    guitool = kitty.gui
[difftool]
    prompt = false
    trustExitCode = true
[difftool "kitty"]
    cmd = kitten diff $LOCAL $REMOTE
[difftool "kitty.gui"]
    cmd = kitten diff $LOCAL $REMOTE
```

## Shell Integration

Shell integration enables features like jumping to prompts, viewing command output, and mouse cursor positioning in supported shells (zsh, bash, fish).

```conf
# kitty.conf shell integration options
shell_integration enabled  # Default: all features enabled

# Disable specific features
shell_integration no-cursor no-title

# Custom keybindings for shell integration features
map ctrl+shift+z scroll_to_previous_prompt
map ctrl+shift+x scroll_to_next_prompt
map f1 show_last_command_output

# Mouse bindings
mouse_map right press ungrabbed mouse_select_command_output
```

```bash
# Features available with shell integration:
# - Jump to previous/next prompt: ctrl+shift+z / ctrl+shift+x
# - View last command output: ctrl+shift+g
# - Click to position cursor in command line
# - Automatic window title updates
# - Clone shell to new window with: ctrl+shift+enter
```

## Configuration

Kitty is configured via `~/.config/kitty/kitty.conf` with support for includes, environment variables, and dynamic generation.

```conf
# ~/.config/kitty/kitty.conf

# Font configuration
font_family      JetBrains Mono
bold_font        auto
italic_font      auto
font_size        12.0

# Window layout
remember_window_size  yes
initial_window_width  640
initial_window_height 400

# Tab bar
tab_bar_style powerline
tab_title_template "{index}: {title}"

# Enable remote control with password
remote_control_password "mypass" set-colors get-colors

# Include additional config files
include other.conf
globinclude kitty.d/**/*.conf
envinclude KITTY_CONF_*

# Dynamic configuration
geninclude dynamic.py

# Keyboard shortcuts
map ctrl+shift+t new_tab
map ctrl+shift+enter new_window
map ctrl+shift+l next_layout
map f1 remote_control set-spacing margin=30

# Mouse customization
mouse_map left click ungrabbed mouse_handle_click selection link prompt
```

```bash
# Generate default config with all options commented
kitty +runpy 'from kitty.config import *; print(commented_out_default_config())'

# Reload configuration
kill -SIGUSR1 $KITTY_PID
# Or press ctrl+shift+f5 in kitty
```

## Window Matching

Remote control commands use sophisticated matching syntax to target specific windows and tabs.

```bash
# Match by title
kitten @ focus-window --match 'title:^Output'

# Match by command line
kitten @ send-text --match cmdline:vim "Hello"

# Match by working directory
kitten @ close-window --match cwd:/home/user/project

# Match by environment variable
kitten @ ls --match 'env:USER=admin'

# Boolean combinations
kitten @ focus-window --match 'title:bash and env:USER=kovid'
kitten @ focus-window --match 'id:43 or title:Output'
kitten @ focus-window --match 'not id:1'
kitten @ focus-window --match '(id:2 or id:3) and title:something'
```

Kitty's primary use cases include serving as a daily-driver terminal for developers who need advanced features like image display, efficient keyboard navigation, and powerful scripting capabilities. It excels in workflows involving remote development via SSH, where its shell integration and config copying features create a seamless experience. The graphics protocol makes it ideal for data science, image manipulation, and any workflow requiring visual feedback directly in the terminal.

Integration patterns typically involve configuring kitty.conf for custom keybindings and remote control, setting up ssh.conf for remote hosts, creating custom kittens for specialized workflows, and using the remote control API to integrate kitty with editors, file managers, and other tools. The kitten framework allows building sophisticated terminal UIs, while the graphics protocol enables integration with visualization libraries and image viewers. Shell integration provides hooks for tracking command execution, enabling features like prompt-based navigation and output capture.
