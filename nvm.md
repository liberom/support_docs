### Manually Install nvm

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Clones the nvm repository and loads nvm. This is the initial setup for manual installation.

```sh
export NVM_DIR="$HOME/.nvm" && (
  git clone https://github.com/nvm-sh/nvm.git "$NVM_DIR"
  cd "$NVM_DIR"
  git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1)`
) && \. "$NVM_DIR/nvm.sh"
```

--------------------------------

### nvm Compatibility Issue Example

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Illustrates a common compatibility issue related to the npmrc prefix setting which can conflict with nvm's management of Node.js installations.

```bash
prefix='some/path'
```

--------------------------------

### Install nvm using Wget

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Downloads and executes the nvm installation script using Wget. Similar to the cURL method, this command downloads the script and pipes it to bash for installation and shell configuration.

```shell
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

--------------------------------

### Install nvm on Alpine Linux (3.13+)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Provides the necessary commands to install nvm on Alpine Linux. It first installs required dependencies using apk and then downloads and executes the nvm installation script.

```bash
apk add -U curl bash ca-certificates openssl ncurses coreutils python3 make gcc g++ libgcc linux-headers grep util-linux binutils findutils
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

--------------------------------

### Install nvm using cURL

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Downloads and executes the nvm installation script using cURL. This command fetches the script and pipes it directly to bash for execution, installing nvm and configuring the shell environment.

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

--------------------------------

### List Installed and Available Node.js Versions

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Provides commands to view currently installed Node.js versions and to list all versions available for installation from the remote repository.

```shell
nvm ls
```

```shell
nvm ls-remote
```

--------------------------------

### Switch Node.js Versions using nvm

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Demonstrates how to use nvm to switch between installed Node.js versions and install new versions. It shows switching to v16, then v14, and installing v12, verifying the active version after each command.

```shell
nvm use 16
Now using node v16.9.1 (npm v7.21.1)
$ node -v
v16.9.1
$ nvm use 14
Now using node v14.18.0 (npm v6.14.15)
$ node -v
v14.18.0
$ nvm install 12
Now using node v12.22.6 (npm v6.14.5)
$ node -v
v12.22.6
```

--------------------------------

### Install NVM using Ansible

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

This Ansible task installs NVM by downloading and executing the official install script. It uses the 'shell' module and specifies a target file to ensure idempotency.

```yaml
- name: Install nvm
  ansible.builtin.shell: >
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
  args:
    creates: "{{ ansible_env.HOME }}/.nvm/nvm.sh"
```

--------------------------------

### Install NVM on Alpine Linux

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Installs NVM and its dependencies on Alpine Linux versions 3.5 to 3.12. It first installs necessary packages like curl, bash, and build tools, then downloads and executes the NVM installation script.

```sh
apk add -U curl bash ca-certificates openssl ncurses coreutils python2 make gcc g++ libgcc linux-headers grep util-linux binutils findutils
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

--------------------------------

### nvm Usage Examples

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Demonstrates tab completion for various nvm commands, showing available subcommands and version/alias options.

```bash
nvm
```

```bash
nvm alias
```

```bash
nvm alias my_alias
```

```bash
nvm use
```

```bash
nvm uninstall
```

--------------------------------

### Install io.js

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Installs io.js, a JavaScript runtime. It can also migrate npm packages from a previous io.js version to a new one.

```shell
nvm install iojs
```

```shell
nvm install --reinstall-packages-from=iojs iojs
```

--------------------------------

### Running NVM Project Tests with npm

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Instructions for running tests for the nvm project using npm. It distinguishes between fast tests (simulating installs) and slow tests (actual installs and version checks), and provides commands to run each type or all tests.

```bash
npm install

npm run test/fast

npm run test/slow

npm test

```

--------------------------------

### Force Install Node from Source

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Installs a specific Node.js version from source when binary packages are incompatible due to shared library issues. This uses the '-s' option with the 'nvm install' command.

```sh
nvm install -s 0.8.6
```

--------------------------------

### Install nvm and Node.js in Docker for CI/CD

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

A robust Dockerfile for installing nvm and a specified Node.js version, suitable for CI/CD pipelines. It includes setting the NVM environment and entrypoint for sourcing nvm commands.

```Dockerfile
FROM ubuntu:latest
ARG NODE_VERSION=20

# install curl
RUN apt update && apt install curl -y

# install nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash

# set env
ENV NVM_DIR=/root/.nvm

# install node
RUN bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION"

# set ENTRYPOINT for reloading nvm-environment
ENTRYPOINT ["bash", "-c", "source $NVM_DIR/nvm.sh && exec \"$@\"", "--"]

# set cmd to bash
CMD ["/bin/bash"]

```

--------------------------------

### List Available Node.js Versions

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Retrieves and lists all remote versions of Node.js available for installation.

```sh
nvm ls-remote
```

--------------------------------

### Install Latest Node.js Version

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Downloads, compiles, and installs the latest stable release of Node.js using the 'node' alias.

```sh
nvm install node # "node" is an alias for the latest version
```

--------------------------------

### Install Node.js and Reinstall Packages

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Installs a new version of Node.js and migrates npm packages from a previous version. It first identifies the current version, resolves the new version, installs it, and then reinstalls npm packages. It does not update npm by default.

```shell
nvm install --reinstall-packages-from=node node
```

```shell
nvm install --reinstall-packages-from=5 6
nvm install --reinstall-packages-from=iojs v4.2
```

```shell
nvm install --reinstall-packages-from=default --latest-npm 'lts/*'
```

--------------------------------

### Using .nvmrc to Switch Node.js Versions

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Demonstrates how nvm uses the .nvmrc file to automatically switch to the specified Node.js version when running 'nvm use' or 'nvm install'. It shows the process of finding the file, downloading (if necessary), and activating the version.

```sh
$ nvm use
Found '/path/to/project/.nvmrc' with version <5.9>
Now using node v5.9.1 (npm v3.7.3)
```

```sh
$ nvm install
Found '/path/to/project/.nvmrc' with version <5.9>
Downloading and installing node v5.9.1...
Downloading https://nodejs.org/dist/v5.9.1/node-v5.9.1-linux-x64.tar.xz...
#################################################################################### 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v5.9.1 (npm v3.7.3)
```

--------------------------------

### Use Installed Node.js Version

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Switches the current shell to use a specific installed Node.js version.

```sh
nvm use node
```

--------------------------------

### Install Specific Node.js Version

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Installs a specific version of Node.js by providing the version number.

```sh
nvm install 14.7.0 # or 16.3.0, 12.22.1, etc
```

--------------------------------

### Define Default Global Packages

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Specifies a list of npm packages to be installed automatically whenever a new Node.js version is installed. Packages are listed one per line in the `$NVM_DIR/default-packages` file.

```shell
# $NVM_DIR/default-packages

rimraf
object-inspect@1.0.2
stevemao/left-pad
```

--------------------------------

### Install Rosetta on Apple Silicon Macs (Shell)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Provides the command to install Rosetta, a translation layer that enables Macs with Apple Silicon chips to run applications built for Intel processors. This is a prerequisite for running older Node.js versions.

```shell
$ softwareupdate --install-rosetta
```

--------------------------------

### Install nvm without Editing Profile

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Installs nvm by downloading the script and running it with the PROFILE environment variable set to /dev/null. This prevents the script from modifying shell configuration files, useful when using other nvm management tools.

```shell
PROFILE=/dev/null bash -c 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash'
```

--------------------------------

### Commit Message Format

Source: https://github.com/nvm-sh/nvm/blob/master/CONTRIBUTING.md

Example structure for commit messages, including a tag, short description, longer explanation, and issue referencing.

```gitcommit
[Tag]: Short description of what you did

Longer description here if necessary

Fixes #1234
```

--------------------------------

### Verify NVM Installation

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

This command verifies if NVM has been successfully installed by checking if the 'nvm' command is available in the current shell environment. It's important to note that 'which nvm' will not work as nvm is a sourced shell function.

```sh
command -v nvm
```

--------------------------------

### Run NVM Docker Container

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Starts an interactive Docker container named 'nvm-dev' using the previously built image. This allows development and testing within a pre-configured environment.

```sh
$ docker run -h nvm-dev -it nvm-dev
```

--------------------------------

### Install Older Node.js Version with Shared Zlib (Shell)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Illustrates the command to install a specific older Node.js version (e.g., 12.22.1) targeting the x86_64 architecture for compatibility with Apple Silicon Macs. The `--shared-zlib` flag is included to mitigate potential compilation or runtime errors.

```shell
$ nvm install v12.22.1 --shared-zlib
```

--------------------------------

### Install Latest LTS Node.js Version

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Installs the latest available Long-Term Support (LTS) version of Node.js, optionally reinstalling packages from the 'current' version.

```sh
nvm install --reinstall-packages-from=current 'lts/*'
```

--------------------------------

### Install Latest npm for Current Node Version

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Installs the latest supported npm version for the currently active Node.js version. This is useful if an npm upgrade is needed.

```shell
nvm install-latest-npm
```

--------------------------------

### Use System Node.js Version

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Allows nvm to use the Node.js version that is already installed on the system. This is done using the special 'system' alias.

```shell
nvm use system
nvm run system --version
```

--------------------------------

### Install nvm in Docker (Non-interactive)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Installs nvm within a Docker container, specifically configuring it for non-interactive bash shells by setting the BASH_ENV variable. This ensures nvm is available for subsequent commands in the container.

```Dockerfile
# Use bash for the shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# Create a script file sourced by both interactive and non-interactive bash shells
ENV BASH_ENV /home/user/.bash_env
RUN touch "${BASH_ENV}"
RUN echo '. "${BASH_ENV}"' >> ~/.bashrc

# Download and install nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | PROFILE="${BASH_ENV}" bash
RUN echo node > .nvmrc
RUN nvm install
```

--------------------------------

### Configure Node.js Version with .nvmrc

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Create a .nvmrc file to specify the Node.js version for a project. nvm commands like 'use', 'install', 'exec', 'run', and 'which' will automatically use the version specified in this file if no version is provided on the command line.

```sh
echo "5.9" > .nvmrc
```

```sh
echo "lts/*" > .nvmrc
```

```sh
echo "node" > .nvmrc
```

--------------------------------

### Troubleshooting nvm on Linux (Ksh)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Command to source the nvm installation in a ksh shell on Linux. This command reloads the shell configuration to make the 'nvm' command available.

```shell
. ~/.profile
```

--------------------------------

### Troubleshooting nvm on Linux (Bash)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Command to source the nvm installation in a bash shell on Linux. This command reloads the shell configuration to make the 'nvm' command available.

```shell
source ~/.bashrc
```

--------------------------------

### Get Path to Node.js Executable

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Returns the file path to the executable of a specific Node.js version.

```sh
nvm which 12.22
```

--------------------------------

### Troubleshooting nvm on Linux (Zsh)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Command to source the nvm installation in a zsh shell on Linux. This command reloads the shell configuration to make the 'nvm' command available.

```shell
source ~/.zshrc
```

--------------------------------

### Co-authored Commit

Source: https://github.com/nvm-sh/nvm/blob/master/CONTRIBUTING.md

Example of adding co-authors to a Git commit message, useful for collaborative commits.

```gitcommit
Co-authored-by: Name Here <email@here>
```

--------------------------------

### nvm Shell Profile Configuration (No Auto-Use)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

This configuration loads nvm but postpones the automatic use of a default Node.js version. It's useful if you want to manually select the Node.js version after installation.

```shell
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" --no-use # This loads nvm, without auto-using the default version
```

--------------------------------

### Bash: Auto NVM Version Switching with cd Alias

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

This bash function, when aliased to 'cd', automatically switches Node.js versions based on a .nvmrc file found by traversing up the directory tree. If no .nvmrc is found, it uses the default Node.js version. It handles installation if a specified version is not available.

```bash
cdnvm() {
    command cd "$@" || return $?
    nvm_path="$(nvm_find_up .nvmrc | command tr -d '\n')"

    # If there are no .nvmrc file, use the default nvm version
    if [[ ! $nvm_path = *[^[:space:]]* ]]; then

        declare default_version
        default_version="$(nvm version default)"

        # If there is no default version, set it to `node`
        # This will use the latest version on your machine
        if [ $default_version = 'N/A' ]; then
            nvm alias default node
            default_version=$(nvm version default)
        fi

        # If the current version is not the default version, set it to use the default version
        if [ "$(nvm current)" != "${default_version}" ]; then
            nvm use default
        fi
    elif [[ -s "${nvm_path}/.nvmrc" && -r "${nvm_path}/.nvmrc" ]]; then
        declare nvm_version
        nvm_version=$(<"${nvm_path}"/.nvmrc)

        declare locally_resolved_nvm_version
        # `nvm ls` will check all locally-available versions
        # If there are multiple matching versions, take the latest one
        # Remove the `->` and `*` characters and spaces
        # `locally_resolved_nvm_version` will be `N/A` if no local versions are found
        locally_resolved_nvm_version=$(nvm ls --no-colors "${nvm_version}" | command tail -1 | command tr -d '\->*' | command tr -d '[:space:]')

        # If it is not already installed, install it
        # `nvm install` will implicitly use the newly-installed version
        if [ "${locally_resolved_nvm_version}" = 'N/A' ]; then
            nvm install "${nvm_version}";
        elif [ "$(nvm current)" != "${locally_resolved_nvm_version}" ]; then
            nvm use "${nvm_version}";
        fi
    fi
}

alias cd='cdnvm'
cdnvm "$PWD" || exit

```

--------------------------------

### Manually Uninstall NVM

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Provides steps to manually remove NVM from a system. It involves unloading NVM from the current session, deleting the NVM installation directory, and removing NVM's sourcing lines from the shell's configuration file.

```sh
$ nvm_dir="${NVM_DIR:-~/.nvm}"
$ nvm unload
$ rm -rf "$nvm_dir"
```

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
```

--------------------------------

### Set Default Node.js Version

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Sets a default Node.js version to be used in all new shell sessions. This can be a specific version, a major version alias, or the latest installed version.

```shell
nvm alias default node
nvm alias default 18
nvm alias default 18.12
```

--------------------------------

### Zsh: Auto NVM Version Switching on Directory Change

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

This zsh function is designed to automatically manage Node.js versions. It's triggered on directory changes ('chpwd' hook) and checks for a .nvmrc file. If found, it installs or uses the specified Node version; otherwise, it reverts to the default.

```zsh
# place this after nvm initialization!
autoload -U add-zsh-hook

load-nvmrc() {
  local nvmrc_path
  nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version
    nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$(nvm version)" ]; then
      nvm use
    fi
  elif [ -n "$(PWD=$OLDPWD nvm_find_nvmrc)" ] && [ "$(nvm version)" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}

add-zsh-hook chpwd load-nvmrc
load-nvmrc

```

--------------------------------

### Fish: Auto NVM Version Switching with Helper Functions

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

This Fish shell configuration utilizes the 'bass' utility to integrate with nvm. It defines functions for nvm, finding .nvmrc, and loading the correct Node.js version based on the .nvmrc file or the default version.

```fish
# ~/.config/fish/functions/nvm.fish
function nvm
  bass source ~/.nvm/nvm.sh --no-use ';' nvm $argv
end

# ~/.config/fish/functions/nvm_find_nvmrc.fish
function nvm_find_nvmrc
  bass source ~/.nvm/nvm.sh --no-use ';' nvm_find_nvmrc
end

# ~/.config/fish/functions/load_nvm.fish
function load_nvm --on-variable="PWD"
  set -l default_node_version (nvm version default)
  set -l node_version (nvm version)
  set -l nvmrc_path (nvm_find_nvmrc)
  if test -n "$nvmrc_path"
    set -l nvmrc_node_version (nvm version (cat $nvmrc_path))
    if test "$nvmrc_node_version" = "N/A"
      nvm install (cat $nvmrc_path)
    else if test "$nvmrc_node_version" != "$node_version"
      nvm use $nvmrc_node_version
    end
  else if test "$node_version" != "$default_node_version"
    echo "Reverting to default Node version"
    nvm use default
  end
end

# ~/.config/fish/config.fish
# You must call it on initialization or listening to directory switching won't work
load_nvm > /dev/stderr

```

--------------------------------

### Use Node.js Binary Mirror

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Configures nvm to download Node.js and io.js binaries from a specified mirror URL instead of the default. This is controlled by setting environment variables.

```shell
export NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist
nvm install node

NVM_NODEJS_ORG_MIRROR=https://nodejs.org/dist nvm install 4.2
```

```shell
export NVM_IOJS_ORG_MIRROR=https://iojs.org/dist
nvm install iojs-v1.0.3

NVM_IOJS_ORG_MIRROR=https://iojs.org/dist nvm install iojs-v1.0.3
```

--------------------------------

### Verify Docker Image

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Lists Docker images to verify that the 'nvm-dev' image has been successfully built.

```sh
$ docker images
```

--------------------------------

### Run Tests

Source: https://github.com/nvm-sh/nvm/blob/master/CONTRIBUTING.md

Command to execute the project's test suite, typically using npm.

```bash
npm test
```

--------------------------------

### Open Zsh Shell Using Rosetta (Shell)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Demonstrates how to launch a zsh shell session specifically using Rosetta translation. This is necessary for compiling or running Node.js versions that are not natively compatible with Apple Silicon architecture.

```shell
$ arch -x86_64 zsh
```

--------------------------------

### Handle Homebrew Insecure Directories in Zsh (Shell)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

This snippet shows the interactive prompt from zsh when Homebrew creates insecure directories, typically related to shell completion files. It provides the user's response to continue the initialization process.

```shell
zsh compinit: insecure directories, run compaudit for list.
Ignore insecure directories and continue [y] or abort compinit [n]? y
```

--------------------------------

### Check resolv.conf Contents

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

This command displays the current content of the resolv.conf file, used to verify the DNS settings after manual configuration.

```shell
cat /etc/resolv.conf
```

--------------------------------

### Exit Rosetta Shell and Check Architecture (Shell)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Demonstrates the commands to exit a shell session running under Rosetta and then check the system's current architecture. This helps verify that the shell has returned to the native ARM64 environment.

```shell
$ exit
$ arch
```

--------------------------------

### nvm Automatic Sourcing in Shell Profiles

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

These lines should be added to your shell's profile file (e.g., .bashrc, .profile, .zshrc) to ensure nvm is automatically sourced every time you log in. This enables nvm commands to be available in your shell environment.

```shell
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

--------------------------------

### Verify Node.js Architecture (Shell)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Shows the command to check the architecture of the running Node.js process. After resolving Apple Silicon compatibility issues, this command should confirm that Node.js is running as 'x64' (x86_64).

```shell
$ node -p process.arch
```

--------------------------------

### Automatically Source nvm on Login

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Adds lines to shell configuration files (like .bashrc, .profile, or .zshrc) to automatically load nvm and its bash completion.

```sh
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

--------------------------------

### Source Bash Completion for nvm

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

This snippet sources the nvm bash completion script, enabling tab completion for nvm commands. It checks if the completion script is readable before sourcing it.

```bash
[[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
```

--------------------------------

### Source nvm in Rosetta-Enabled Shell (Shell)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Shows how to source the nvm script within a shell session that is running under Rosetta. This ensures that nvm is properly initialized and available in that specific shell environment.

```shell
$ source "${NVM_DIR}/nvm.sh"
```

--------------------------------

### Manually Upgrade nvm

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Updates nvm to the latest version by fetching tags, checking out the latest release, and activating it.

```sh
(
  cd "$NVM_DIR"
  git fetch --tags origin
  git checkout `git describe --abbrev=0 --tags --match "v[0-9]*" $(git rev-list --tags --max-count=1))`
) && \. "$NVM_DIR/nvm.sh"
```

--------------------------------

### nvm Shell Profile Configuration

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

These lines are added to your shell profile (e.g., .bashrc, .zshrc) to load nvm. They define the NVM directory and source the nvm.sh script to enable nvm commands.

```shell
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

--------------------------------

### Pass Authorization Header to Mirror with nvm

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Set the NVM_AUTH_HEADER environment variable to pass an Authorization header to a mirror URL. This is useful for private registries or authenticated downloads.

```sh
NVM_AUTH_HEADER="Bearer secret-token" nvm install node
```

--------------------------------

### Build NVM Docker Image

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Builds a Docker image for NVM development using a Dockerfile based on Ubuntu 18.04. This image includes essential tools for NVM development.

```sh
$ docker build -t nvm-dev .
```

--------------------------------

### Enable Current Symlink

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Enables the creation of a 'current' symlink by `nvm use`, which points to the active Node.js version. This can be useful for IDEs but may cause race conditions in multi-tab environments.

```shell
export NVM_SYMLINK_CURRENT="true"
```

--------------------------------

### Rebase onto Upstream

Source: https://github.com/nvm-sh/nvm/blob/master/CONTRIBUTING.md

Commands to fetch the latest changes from the upstream repository and rebase the current branch onto the main branch.

```bash
git fetch upstream
git rebase upstream/main
```

--------------------------------

### Resolve WSL DNS Issues and Configure resolv.conf

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

These commands fix WSL-2 DNS resolution problems by manually setting the nameserver and preventing automatic regeneration of the resolv.conf file. It involves removing the existing file, creating a new one with a specific nameserver, and configuring wsl.conf to disable automatic DNS generation.

```shell
sudo rm /etc/resolv.conf
sudo bash -c 'echo "nameserver 8.8.8.8" > /etc/resolv.conf'
sudo bash -c 'echo "[network]" > /etc/wsl.conf'
sudo bash -c 'echo "generateResolvConf = false" >> /etc/wsl.conf'
sudo chattr +i /etc/resolv.conf
```

--------------------------------

### Run Command with Specific Node.js Version

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Executes a command using a specified Node.js version in a subshell.

```sh
nvm exec 4.2 node --version
```

--------------------------------

### Set Custom Display Colors

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Allows customization of the colors used in nvm's output for version and alias information. Color codes map to specific colors or styles.

```shell
nvm set-colors rgBcm
```

--------------------------------

### Persist Custom Colors

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Ensures custom display colors are retained across shell sessions by exporting the `NVM_COLORS` environment variable in the shell profile.

```shell
export NVM_COLORS='cmgRY'
```

--------------------------------

### Commit Changes

Source: https://github.com/nvm-sh/nvm/blob/master/CONTRIBUTING.md

Command to stage and commit all changes in the current branch.

```bash
git commit -a
```

--------------------------------

### Push Changes

Source: https://github.com/nvm-sh/nvm/blob/master/CONTRIBUTING.md

Command to push the local branch with committed changes to the remote repository.

```bash
git push origin issue1234
```

--------------------------------

### Create Git Branch

Source: https://github.com/nvm-sh/nvm/blob/master/CONTRIBUTING.md

Command to create a new Git branch for development, typically named after an issue number.

```bash
git checkout -b issue1234
```

--------------------------------

### Validate .nvmrc File with npx nvmrc

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Utilize the 'npx nvmrc' command to validate the contents of an .nvmrc file. This helps ensure the file is correctly formatted and that the specified version is recognized by nvm.

```sh
npx nvmrc
```

--------------------------------

### Set Node.js Version Alias

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Creates a custom alias for a specific Node.js version. Aliases cannot contain spaces or slashes.

```sh
nvm alias my_alias v14.4.0
```

--------------------------------

### Fix nvm Node Version Not Found in Vim Shell (Shell)

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Addresses the issue where Vim displays the system Node.js version instead of the one selected by nvm. This often occurs due to path helper configurations. This command modifies file permissions to resolve the conflict.

```shell
sudo chmod ugo-x /usr/libexec/path_helper
```

--------------------------------

### Suppress Colorized Output

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Disables colorized output in nvm commands. This can be achieved using the `--no-colors` flag or by setting the `TERM` environment variable to `dumb`.

```shell
nvm ls --no-colors
nvm help --no-colors
TERM=dumb nvm ls
```

--------------------------------

### Deactivate Node.js Version

Source: https://github.com/nvm-sh/nvm/blob/master/README.md

Removes the current Node.js version from the PATH, effectively deactivating it. This is useful for reverting changes or cleaning up the environment.

```shell
nvm deactivate
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.