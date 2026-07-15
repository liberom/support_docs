# Oh My Zsh

Oh My Zsh is an open source, community-driven framework for managing your Zsh shell configuration. It provides a plugin and theme system that enhances the terminal experience with hundreds of helpful plugins for common developer tools (git, docker, npm, etc.), beautiful themes with git integration, and useful shell functions and aliases. The framework simplifies Zsh customization by offering a standardized structure for configuration, making it easy to enable features, switch themes, and add custom functionality.

The project is designed to work across multiple operating systems including Linux, macOS, FreeBSD, and Windows (via WSL2). It requires Zsh v4.3.9 or newer (5.0.8+ recommended), along with `curl`/`wget` and `git` for installation and updates. Oh My Zsh follows a rolling release model based on the master branch, with automatic update checking and easy manual updates through the `omz` command-line interface.

## Installation

### Install via curl

Downloads and executes the installation script that clones the repository, backs up existing `.zshrc`, and configures Zsh.

```bash
# Standard installation with curl
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Alternative mirror (for regions with GitHub restrictions)
sh -c "$(curl -fsSL https://install.ohmyz.sh/)"

# Unattended installation (no prompts, doesn't change shell or run zsh)
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" "" --unattended

# Custom installation directory
ZSH="$HOME/.dotfiles/oh-my-zsh" sh install.sh

# Installation from a fork
REPO=myuser/ohmyzsh BRANCH=mybranch sh install.sh
```

### Manual Installation

Step-by-step manual installation process for advanced users who want full control.

```bash
# 1. Clone the repository
git clone https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh

# 2. Backup existing zshrc
cp ~/.zshrc ~/.zshrc.orig

# 3. Create new zshrc from template
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc

# 4. Change default shell to zsh
chsh -s $(which zsh)

# 5. Start a new zsh session
zsh
```

## Configuration (.zshrc)

### Basic Configuration

The `.zshrc` file controls Oh My Zsh settings including themes, plugins, and custom options.

```bash
# ~/.zshrc

# Path to Oh My Zsh installation
export ZSH="$HOME/.oh-my-zsh"

# Set theme (see https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)
ZSH_THEME="robbyrussell"

# Use random theme from favorites
# ZSH_THEME="random"
# ZSH_THEME_RANDOM_CANDIDATES=("robbyrussell" "agnoster" "bureau")

# Case-sensitive completion
# CASE_SENSITIVE="true"

# Hyphen-insensitive completion (_ and - interchangeable)
# HYPHEN_INSENSITIVE="true"

# Disable auto-update prompts
# zstyle ':omz:update' mode disabled

# Auto-update without confirmation
# zstyle ':omz:update' mode auto

# Check for updates every 7 days
# zstyle ':omz:update' frequency 7

# Enable command auto-correction
# ENABLE_CORRECTION="true"

# Show red dots while waiting for completion
# COMPLETION_WAITING_DOTS="true"

# Plugins to load (space-separated, no commas!)
plugins=(git docker npm node kubectl)

# Load Oh My Zsh
source $ZSH/oh-my-zsh.sh

# User configuration
export EDITOR='vim'
alias zshconfig="$EDITOR ~/.zshrc"
```

### Skip Aliases Configuration

Control which aliases are loaded from plugins and lib files using zstyle.

```bash
# ~/.zshrc (before sourcing oh-my-zsh.sh)

# Skip all aliases from lib files and plugins
zstyle ':omz:*' aliases no

# Skip only lib file aliases
zstyle ':omz:lib:*' aliases no

# Skip specific lib aliases (directories.zsh provides cd aliases)
zstyle ':omz:lib:directories' aliases no

# Skip all plugin aliases
zstyle ':omz:plugins:*' aliases no

# Skip only git plugin aliases
zstyle ':omz:plugins:git' aliases no

# Skip all plugin aliases except git
zstyle ':omz:plugins:*' aliases no
zstyle ':omz:plugins:git' aliases yes

source $ZSH/oh-my-zsh.sh
```

### Async Git Prompt Configuration

Configure asynchronous git prompt for improved performance on large repositories.

```bash
# ~/.zshrc (before sourcing oh-my-zsh.sh)

# Disable async git prompt (if having issues)
zstyle ':omz:alpha:lib:git' async-prompt no

# Force async git prompt (if git info not appearing)
zstyle ':omz:alpha:lib:git' async-prompt force

source $ZSH/oh-my-zsh.sh
```

### GNU ls Configuration (macOS/FreeBSD)

Enable GNU ls instead of BSD ls for enhanced colorization and features.

```bash
# ~/.zshrc (before sourcing oh-my-zsh.sh)

# Use GNU ls (gls) instead of BSD ls on macOS/FreeBSD
zstyle ':omz:lib:theme-and-appearance' gnu-ls yes

source $ZSH/oh-my-zsh.sh
```

## OMZ CLI Commands

### omz update

Manually update Oh My Zsh to the latest version.

```bash
# Update Oh My Zsh interactively
omz update

# Programmatic update (for scripts)
$ZSH/tools/upgrade.sh
```

### omz plugin

Manage plugins - list, enable, disable, load, and get information.

```bash
# List all available plugins
omz plugin list

# List only enabled plugins
omz plugin list --enabled

# Get information about a plugin (displays README)
omz plugin info git
omz plugin info docker

# Enable plugins (modifies .zshrc and reloads)
omz plugin enable docker kubectl
omz plugin enable aws npm

# Disable plugins (modifies .zshrc and reloads)
omz plugin disable ruby rails

# Load plugin for current session only (doesn't modify .zshrc)
omz plugin load docker
omz plugin load fzf kubectl
```

### omz theme

Manage themes - list available themes, set permanently, or use temporarily.

```bash
# List all available themes
omz theme list

# Set theme permanently (modifies .zshrc and reloads)
omz theme set agnoster
omz theme set robbyrussell

# Use theme for current session only
omz theme use bureau
omz theme use random
```

### omz pr

Test and manage Oh My Zsh pull requests locally.

```bash
# Test a pull request by number
omz pr test 12345

# Test a pull request by URL
omz pr test https://github.com/ohmyzsh/ohmyzsh/pull/12345

# Clean up all PR test branches
omz pr clean
```

### omz changelog and version

View changelog and version information.

```bash
# Show current version
omz version
# Output: master (abc1234)

# View changelog for a specific version/tag
omz changelog v1.0.0

# Reload current zsh session
omz reload
```

## Git Plugin

### Git Aliases

The git plugin provides over 150 aliases for common git operations.

```bash
# Enable git plugin in .zshrc
plugins=(git)

# Common aliases
g        # git
ga       # git add
gaa      # git add --all
gapa     # git add --patch

gc       # git commit --verbose
gcmsg    # git commit --message
gca      # git commit --verbose --all
gca!     # git commit --verbose --all --amend

gco      # git checkout
gcb      # git checkout -b
gcm      # git checkout $(git_main_branch)
gcd      # git checkout $(git_develop_branch)

gb       # git branch
gba      # git branch --all
gbd      # git branch --delete
gbD      # git branch --delete --force

gd       # git diff
gdca     # git diff --cached
gds      # git diff --staged

gf       # git fetch
gfa      # git fetch --all --tags --prune --jobs=10

gl       # git pull
gpr      # git pull --rebase
gpra     # git pull --rebase --autostash

gp       # git push
gpf      # git push --force-with-lease
gpsup    # git push --set-upstream origin $(git_current_branch)

gst      # git status
gss      # git status --short
gsb      # git status --short --branch

gsta     # git stash push
gstp     # git stash pop
gstl     # git stash list

glog     # git log --oneline --decorate --graph
gloga    # git log --oneline --decorate --graph --all
glol     # git log --graph --pretty=format with colors

grb      # git rebase
grbi     # git rebase --interactive
grbm     # git rebase $(git_main_branch)

gm       # git merge
gmom     # git merge origin/$(git_main_branch)
```

### Git Functions

Helper functions for working with git branches and repositories.

```bash
# Get the main branch name (main, master, trunk, etc.)
git_main_branch
# Output: main

# Get the develop branch name (dev, devel, develop, development)
git_develop_branch
# Output: develop

# Get current branch name
git_current_branch
# Output: feature/my-feature

# Rename a branch locally and on remote
grename old-branch-name new-branch-name

# Delete merged branches (except main and develop)
gbda

# Delete squash-merged branches
gbds

# Create a WIP commit
gwip
# Creates: --wip-- [skip ci]

# Undo a WIP commit
gunwip

# Undo all WIP commits
gunwipall

# Check if current branch has WIP commit
work_in_progress
# Output: WIP!! (if WIP commit exists)
```

### Git Prompt Functions

Functions for customizing your prompt with git information.

```bash
# In your theme or .zshrc

# Configure git prompt symbols
ZSH_THEME_GIT_PROMPT_PREFIX="git:("
ZSH_THEME_GIT_PROMPT_SUFFIX=")"
ZSH_THEME_GIT_PROMPT_DIRTY="*"
ZSH_THEME_GIT_PROMPT_CLEAN=""

# Status indicators
ZSH_THEME_GIT_PROMPT_ADDED="%{$fg[green]%}+"
ZSH_THEME_GIT_PROMPT_MODIFIED="%{$fg[yellow]%}!"
ZSH_THEME_GIT_PROMPT_DELETED="%{$fg[red]%}-"
ZSH_THEME_GIT_PROMPT_RENAMED="%{$fg[magenta]%}>"
ZSH_THEME_GIT_PROMPT_UNMERGED="%{$fg[yellow]%}#"
ZSH_THEME_GIT_PROMPT_UNTRACKED="%{$fg[cyan]%}?"
ZSH_THEME_GIT_PROMPT_STASHED="%{$fg[blue]%}$"
ZSH_THEME_GIT_PROMPT_AHEAD="%{$fg[green]%}^"
ZSH_THEME_GIT_PROMPT_BEHIND="%{$fg[red]%}v"

# Use in PROMPT
PROMPT='%n@%m:%~$(git_prompt_info) %# '
RPROMPT='$(git_prompt_status)'

# Available git prompt functions:
git_prompt_info      # Branch name with dirty indicator
git_prompt_status    # File status indicators
git_prompt_ahead     # Ahead of remote indicator
git_prompt_behind    # Behind remote indicator
git_prompt_short_sha # Short commit SHA
git_prompt_long_sha  # Full commit SHA
git_current_branch   # Current branch name
git_repo_name        # Repository name
git_current_user_name   # Git config user.name
git_current_user_email  # Git config user.email
```

## Docker Plugin

### Docker Aliases

Common docker command aliases for container and image management.

```bash
# Enable docker plugin
plugins=(git docker)

# Container operations
dps      # docker ps
dpsa     # docker ps -a
dcls     # docker container ls
dclsa    # docker container ls -a
dr       # docker container run
drit     # docker container run -it
dxc      # docker container exec
dxcit    # docker container exec -it
dst      # docker container start
dstp     # docker container stop
drs      # docker container restart
drm      # docker container rm
drm!     # docker container rm -f
dlo      # docker container logs
dcin     # docker container inspect

# Image operations
dpu      # docker pull
dib      # docker image build
dbl      # docker build
dils     # docker image ls
dirm     # docker image rm
dit      # docker image tag
dipu     # docker image push
dipru    # docker image prune -a
dii      # docker image inspect

# Network operations
dnc      # docker network create
dnls     # docker network ls
dni      # docker network inspect
dnrm     # docker network rm
dncn     # docker network connect
dndcn    # docker network disconnect

# Volume operations
dvls     # docker volume ls
dvi      # docker volume inspect
dvprune  # docker volume prune

# Stats and monitoring
dsts     # docker stats
dtop     # docker top
dsta     # docker stop $(docker ps -q)
```

## Custom Plugins

### Creating a Custom Plugin

Add custom functionality by creating plugins in the custom directory.

```bash
# Create plugin directory structure
mkdir -p ~/.oh-my-zsh/custom/plugins/mycompany

# Create plugin file
cat > ~/.oh-my-zsh/custom/plugins/mycompany/mycompany.plugin.zsh << 'EOF'
# mycompany.plugin.zsh - Custom company utilities

# Aliases for internal tools
alias deploy='kubectl apply -f'
alias logs='stern --tail 100'
alias vpn='sudo openvpn /etc/openvpn/company.conf'

# SSH shortcuts
alias prod='ssh prod-bastion.company.com'
alias staging='ssh staging-bastion.company.com'

# Helper functions
function ticket() {
    # Open Jira ticket in browser
    open "https://jira.company.com/browse/$1"
}

function pr() {
    # Create PR for current branch
    gh pr create --web
}

function sync-main() {
    # Sync local main with remote
    git checkout main
    git pull --rebase origin main
    git checkout -
    git rebase main
}
EOF

# Enable plugin in .zshrc
plugins=(git docker mycompany)
```

## Custom Themes

### Creating a Custom Theme

Create personalized prompt themes in the custom themes directory.

```bash
# Create custom theme
cat > ~/.oh-my-zsh/custom/themes/mytheme.zsh-theme << 'EOF'
# mytheme.zsh-theme - Minimal prompt with git info

# Git prompt configuration
ZSH_THEME_GIT_PROMPT_PREFIX="%{$fg[blue]%}["
ZSH_THEME_GIT_PROMPT_SUFFIX="]%{$reset_color%}"
ZSH_THEME_GIT_PROMPT_DIRTY=" %{$fg[red]%}*%{$reset_color%}"
ZSH_THEME_GIT_PROMPT_CLEAN=""

# Return status indicator
local ret_status="%(?:%{$fg[green]%}➜:%{$fg[red]%}➜)"

# Main prompt: status arrow, current directory, git info
PROMPT='${ret_status} %{$fg[cyan]%}%c%{$reset_color%} $(git_prompt_info)'

# Right prompt: timestamp
RPROMPT='%{$fg[white]%}%T%{$reset_color%}'
EOF

# Use in .zshrc
ZSH_THEME="mytheme"
```

## Library Functions

### Directory Functions

Built-in directory navigation helpers from lib/directories.zsh.

```bash
# Directory aliases (from directories lib)
..       # cd ..
...      # cd ../..
....     # cd ../../..
.....    # cd ../../../..

-        # cd to previous directory (cd -)

# Directory stack operations
d        # List directory stack
1-9      # cd to nth directory in stack

# Create and enter directory
take myproject
# Equivalent to: mkdir -p myproject && cd myproject

# Push/pop directories
pushd /some/path
popd
```

### Clipboard Functions

Cross-platform clipboard integration from lib/clipboard.zsh.

```bash
# Copy command output to clipboard
echo "Hello World" | clipcopy

# Paste from clipboard
clippaste

# Copy file contents to clipboard
clipcopy < file.txt

# Paste into file
clippaste > output.txt
```

### Open Command

Platform-agnostic file/URL opener from lib/functions.zsh.

```bash
# Open URL in default browser
open_command https://github.com

# Open file with default application
open_command document.pdf

# Works on:
# - macOS: uses 'open'
# - Linux: uses 'xdg-open' or similar
# - Windows/WSL: uses appropriate handler
```

## Uninstallation

### Uninstall Oh My Zsh

Complete removal of Oh My Zsh and restoration of previous configuration.

```bash
# Run uninstall command (restores previous .zshrc)
uninstall_oh_my_zsh

# This will:
# 1. Remove ~/.oh-my-zsh directory
# 2. Restore ~/.zshrc.pre-oh-my-zsh to ~/.zshrc
# 3. Restore previous default shell if changed
```

## Summary

Oh My Zsh serves developers, system administrators, and power users who want a productive and visually appealing terminal experience. The primary use cases include: rapid git workflow management through extensive aliases and prompt integration; streamlined Docker, Kubernetes, and cloud CLI operations; standardized development environment setup across teams; and terminal prompt customization with themes that display contextual information. The framework is particularly valuable for teams that want consistent shell configurations across members.

Integration patterns typically involve: installing Oh My Zsh on development machines and CI/CD environments; selecting a curated set of plugins matching the tech stack (e.g., `git node npm docker kubectl` for a Node.js microservices team); creating custom plugins for company-specific tools and aliases; and optionally customizing or creating themes to match team preferences. The `omz` CLI provides ongoing management capabilities for updates and plugin/theme switching, while the custom directory structure allows persistent local modifications that won't be overwritten by updates.
