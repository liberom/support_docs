### Start Bitwarden On-Premise Instance

Source: https://bitwarden.com/help/cli/install-on-premise

This command initiates all Bitwarden containers, starting the on-premise instance. The first start may take longer as it downloads Docker images.

```Bash
./bitwarden.sh start
```

--------------------------------

### Start Bitwarden On-Premise Instance

Source: https://bitwarden.com/help/cli/install-on-premise-linux

This command initiates all Docker containers required for the Bitwarden instance to run. The initial startup may take longer as it downloads necessary images from Docker Hub.

```Bash
./bitwarden.sh start
```

--------------------------------

### Verify Running Docker Containers for Bitwarden

Source: https://bitwarden.com/help/cli/install-on-premise

This command lists all currently running Docker containers, allowing users to verify that all Bitwarden components are active and healthy after starting the instance.

```Bash
docker ps
```

--------------------------------

### Start Bitwarden Self-Hosted Instance

Source: https://bitwarden.com/help/cli/install-on-premise-windows

Initiate the Bitwarden self-hosted instance by running the PowerShell script with the `-start` command. This command should be executed after all previous installation and configuration steps have been successfully completed.

```PowerShell
.\bitwarden.ps1 -start
```

--------------------------------

### Verify Running Bitwarden Docker Containers

Source: https://bitwarden.com/help/cli/install-on-premise-linux

Use this command to list all active Docker containers on your system. It helps confirm that all Bitwarden components are running correctly after starting the instance.

```Bash
docker ps
```

--------------------------------

### Bitwarden Installation Script Commands Reference

Source: https://bitwarden.com/help/cli/install-on-premise-linux

This API documentation provides a comprehensive list of commands available for the `bitwarden.sh` (or `bitwarden.ps1`) installation script. Each command's purpose and functionality are detailed, aiding in server management.

```APIDOC
Command Reference:
  install: Start the installer.
  start: Start all containers.
  restart: Restart all containers (same as start).
  stop: Stop all containers.
  update: Update all containers and the database.
  updatedb: Update/initialize the database.
  updaterun: Update the `run.sh` file.
  updateself: Update this main script.
  updateconf: Update all containers without restarting the running instance.
  uninstall: Before this command executes, you will be prompted to save database files. `y` will create a tarfile of your database including the most recent backup. Stops containers, deletes the `bwdata` directory and all its contents, and removes ephemeral volumes. After executing, you will be asked whether you also want to purge all Bitwarden images.
  compresslogs: Download a tarball of all server logs, or of server logs in a specified date range, to the current directory. For example, use `./bitwarden.sh compresslogs 20240304 20240305` to download logs from March 4th, 2024 to March 5th, 2024.
  renewcert: Renew certificates.
  rebuild: Rebuild generated installation assets from `config.yml`.
  help: List all commands.
```

--------------------------------

### Bitwarden Installation Script Commands Reference

Source: https://bitwarden.com/help/cli/install-on-premise

This section provides a comprehensive reference for all available commands of the `bitwarden.sh` (or `bitwarden.ps1`) installation script, detailing their purpose and usage. PowerShell users should prefix commands with a hyphen.

```APIDOC
Command: install
  Description: Start the installer.
Command: start
  Description: Start all containers.
Command: restart
  Description: Restart all containers (same as start).
Command: stop
  Description: Stop all containers.
Command: update
  Description: Update all containers and the database.
Command: updatedb
  Description: Update/initialize the database.
Command: updaterun
  Description: Update the `run.sh` file.
Command: updateself
  Description: Update this main script.
Command: updateconf
  Description: Update all containers without restarting the running instance.
Command: uninstall
  Description: Before this command executes, you will be prompted to save database files. `y` will create a tarfile of your database including the most recent backup. Stops containers, deletes the `bwdata` directory and all its contents, and removes ephemeral volumes. After executing, you will be asked whether you also want to purge all Bitwarden images.
Command: compresslogs
  Description: Download a tarball of all server logs, or of server logs in a specified date range, to the current directory. For example, use `./bitwarden.sh compresslogs 20240304 20240305` to download logs from March 4th, 2024 to March 5th, 2024.
Command: renewcert
  Description: Renew certificates.
Command: rebuild
  Description: Rebuild generated installation assets from `config.yml`.
Command: help
  Description: List all commands.
```

--------------------------------

### Onboarding Guides and Resources Email Template

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

Offers a quick email template to share useful resources and guides for Bitwarden onboarding, making it easy for new users to get started with links to relevant documentation and videos.

```Email
Subject: Make it easy to get started with these guides

Body:

Hi *[name]*,

Put together an email, internal message, or document with a list of useful resources about Bitwarden onboarding. Here's a quick template you can use:

*Hi there,*

*Here are three resources that will help you get started with your new password manager:*

* *[Guide]* [*Get started with Bitwarden Password Manager*](/learning/getting-started-password-manager/)
* *[Guide]* [*Get started with Bitwarden as an individual user*](/learning/getting-started-as-an-individual-user/)
* *[Video series]* [*Password Manager 101*](/learning/pm-101-getting-started-as-a-user/)

*[Name] is the Bitwarden implementation champion, so feel free to reach out directly with any questions.*
```

--------------------------------

### Install Bitwarden On-Premise using Official Shell Script

Source: https://bitwarden.com/help/cli/install-on-premise-linux

This section details the process of installing Bitwarden on a Linux server using the official bitwarden.sh shell script. It covers downloading the script, executing the installer, and navigating through the interactive prompts for configuring the domain, SSL certificates (Let's Encrypt or custom), and providing installation ID and key for licensing.

```Bash
curl -Lso bitwarden.sh "https://func.bitwarden.com/api/dl/?app=self-host&platform=linux" && chmod 700 bitwarden.sh
```

```Bash
./bitwarden.sh install
```

--------------------------------

### Install Bitwarden using Shell Script on Linux

Source: https://bitwarden.com/help/cli/install-on-premise

This section details how to download and execute the Bitwarden installation script (`bitwarden.sh`) on a Linux machine. It also describes the various interactive prompts encountered during the installation process, such as domain name, SSL certificate options (Let's Encrypt, custom, or self-signed), installation ID, installation key, and region selection. Ensure you run these commands as the `bitwarden` user from the `/opt/bitwarden` directory.

```Bash
curl -Lso bitwarden.sh "https://func.bitwarden.com/api/dl/?app=self-host&platform=linux" && chmod 700 bitwarden.sh
```

```Bash
./bitwarden.sh install
```

--------------------------------

### Download Bitwarden Installation Script

Source: https://bitwarden.com/help/cli/install-on-premise-windows

Download the Bitwarden self-host installation script (`bitwarden.ps1`) specifically for Windows using the `Invoke-RestMethod` cmdlet from the official Bitwarden API endpoint.

```PowerShell
Invoke-RestMethod -OutFile bitwarden.ps1 -Uri "https://func.bitwarden.com/api/dl/?app=self-host&platform=windows"
```

--------------------------------

### Bitwarden PowerShell Script Commands Reference

Source: https://bitwarden.com/help/cli/install-on-premise-windows

This section provides a comprehensive reference for commands available in the bitwarden.ps1 installation script. These commands facilitate various management tasks for on-premise Bitwarden deployments, including installation, starting/stopping containers, updates, and uninstallation.

```APIDOC
bitwarden.ps1 commands:
  -install:
    Description: Start the installer.
  -start:
    Description: Start all containers.
  -restart:
    Description: Restart all containers.
  -stop:
    Description: Stop all containers.
  -update:
    Description: Update all containers and the database.
  -updatedb:
    Description: Update/initialize the database.
  -updaterun:
    Description: Update the run.ps1 file.
  -updateself:
    Description: Update the installation script.
  -updateconf:
    Description: Update all containers without restarting the running instance.
  -uninstall:
    Description: Before this command executes, you will be prompted to save database files. `y` will create a tarfile of your database including the most recent backup. Stops containers, deletes the `bwdata` directory and all its contents, and removes ephemeral volumes. After executing, you will be asked whether you want to purge all Bitwarden images.
  -renewcert:
    Description: Renew certificates.
  -rebuild:
    Description: Rebuild generated installation assets from `config.yml`.
  -help:
    Description: List all commands.
```

--------------------------------

### Rebuild Bitwarden Installation Assets from config.yml

Source: https://bitwarden.com/help/cli/install-on-premise-linux

This command regenerates the necessary installation assets based on the current settings in `./bwdata/config.yml`. It is particularly useful for applying adjustments related to network configurations or alternate ports after initial setup.

```Bash
./bitwarden.sh rebuild
```

--------------------------------

### Build Docker Image for Bitwarden CLI

Source: https://bitwarden.com/help/cli/developer-quick-start

This command builds the Docker image using the current directory's Dockerfile and tags it with a specified name. It compiles all the setup steps into a runnable container image.

```Bash
docker build -t image-name
```

--------------------------------

### Email Template: Install Bitwarden Browser Extension (1/5)

Source: https://bitwarden.com/help/cli/end-user-onboarding-emails

This email guides new users to install the Bitwarden browser extension, providing a direct link to the download page and outlining the full onboarding checklist for their reference.

```Email
Subject: Get started: Install the Bitwarden browser extension (1/5)

Body:
Hi there,

Your organization is using Bitwarden to secure passwords and other sensitive data. You will receive five emails with tips on how to get started.

Today's stop is to head over to the [download page](/download/#downloads-web-browser) and install the Bitwarden extension on your favorite browser.

Download the browser extension

The rest of your onboarding checklist:

* [**Download the browser extension**](/download/#downloads-web-browser)
* [Add logins and passwords to your account](/help/getting-started-webvault/#add-a-login)
* [Learn how to autofill](/help/auto-fill-browser/)
* [Learn how to share items with collections](/learning/individual-and-organizational-vaults/)

Stay secure,

Team Bitwarden
```

--------------------------------

### Run Bitwarden Self-Host Installer

Source: https://bitwarden.com/help/cli/install-on-premise-windows

Execute the downloaded Bitwarden PowerShell script with the `-install` flag to initiate the self-hosted installation process. This command will trigger a series of interactive prompts for configuring the Bitwarden instance.

```PowerShell
.\bitwarden.ps1 -install
```

--------------------------------

### Configure Linux Server for Bitwarden On-Premise Installation

Source: https://bitwarden.com/help/cli/install-on-premise-linux

These steps outline the recommended best practices for preparing a Linux server for Bitwarden installation. It involves creating a dedicated 'bitwarden' service account, setting a strong password, ensuring the user is part of the 'docker' group, and establishing proper ownership and permissions for the /opt/bitwarden installation directory to enhance security and isolation.

```Bash
sudo adduser bitwarden
```

```Bash
sudo passwd bitwarden
```

```Bash
sudo groupadd docker
```

```Bash
sudo usermod -aG docker bitwarden
```

```Bash
sudo mkdir /opt/bitwarden
```

```Bash
sudo chmod -R 700 /opt/bitwarden
```

```Bash
sudo chown -R bitwarden:bitwarden /opt/bitwarden
```

--------------------------------

### Email Template for Bitwarden Onboarding Guides

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

Provides a template for an email or internal message listing useful resources and guides to help users get started with Bitwarden Password Manager.

```Email
Subject: Make it easy to get started with these guides

Body: Hi there,

Here are three resources that will help you get started with your new password manager:

* [Guide] Get started with Bitwarden Password Manager
* [Guide] Get started with Bitwarden as an individual user
* [Video series] Password Manager 101

[Name] is the Bitwarden implementation champion, so feel free to reach out directly with any questions.
```

--------------------------------

### Start Bitwarden Server with Docker Compose

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This command starts the Bitwarden server containers in detached mode using the specified Docker Compose file. It's the initial step to bring up a self-hosted Bitwarden instance.

```Bash
docker compose -f ./docker/docker-compose.yml up -d
```

--------------------------------

### Create Bitwarden Local User and Directory on Linux

Source: https://bitwarden.com/help/cli/install-on-premise

These steps outline the recommended best practices for configuring a Linux server with a dedicated `bitwarden` service account and directory, ensuring isolation for your Bitwarden instance. This involves creating the user, setting a password, adding the user to the docker group, creating the installation directory, and setting appropriate permissions and ownership.

```Bash
sudo adduser bitwarden
```

```Bash
sudo passwd bitwarden
```

```Bash
sudo groupadd docker
```

```Bash
sudo usermod -aG docker bitwarden
```

```Bash
sudo mkdir /opt/bitwarden
```

```Bash
sudo chmod -R 700 /opt/bitwarden
```

```Bash
sudo chown -R bitwarden:bitwarden /opt/bitwarden
```

--------------------------------

### Configure Private Key after Keyring Setup

Source: https://bitwarden.com/help/cli/directory-sync-cli

After successfully starting and unlocking the Gnome Keyring daemon, attempt to configure your private key again using this command. This example shows configuring a GSuite key.

```Bash
bwdc config gsuite.key /path/to/key/
```

--------------------------------

### Bitwarden CLI: Get Notes Example

Source: https://bitwarden.com/help/cli/cli

Provides an example of retrieving a note for a vault item using `bw get notes` with a search term. The command will return the note for the first matching item found.

```Bash
bw get notes Github
```

--------------------------------

### Install Bitwarden Secrets Manager CLI in Dockerfile

Source: https://bitwarden.com/help/cli/developer-quick-start

This Dockerfile snippet demonstrates how to install necessary dependencies (ca-certificates, curl, jq, unzip), download and unzip the Bitwarden Secrets Manager CLI (bws), and set up an entrypoint script for runtime secret injection. It ensures the CLI is available within the Docker image.

```Dockerfile
# Install dependencies
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
  apt-get install -y \
  ca-certificates \
  curl \
  jq \
  unzip && \
  rm -rf /var/lib/apt/lists/*

# Download bws
RUN curl -LO https://github.com/bitwarden/sdk/releases/download/bws-v1.0.0/bws-x86_64-unknown-linux-gnu-1.0.0.zip && \
  unzip bws-x86_64-unknown-linux-gnu-1.0.0.zip -d /usr/local/bin/ && \
  rm -f bws-x86_64-unknown-linux-gnu-1.0.0.zip

# Add anything else you will need to your image

# Entrypoint script will retrieve secrets at runtime
COPY ./entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
```

--------------------------------

### Start Bitwarden Self-Hosted Server

Source: https://bitwarden.com/help/cli/migration

After installing and configuring Bitwarden on your self-hosted server, use this shell command to initiate all necessary Bitwarden services. This command is essential to make your Bitwarden instance operational and accessible.

```Shell
./bitwarden.sh start
```

--------------------------------

### Bitwarden CLI: Example Data Import from CSV

Source: https://bitwarden.com/help/cli/import-from-lastpass

An example of using the Bitwarden CLI import command to import data from a CSV file. The <format> placeholder should be replaced with the actual file format, which can be listed using `bw import --formats`.

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Navigate to Bitwarden Installation Directory

Source: https://bitwarden.com/help/cli/install-on-premise-windows

Change the current directory to the designated Bitwarden installation path, typically `C:\Bitwarden`, as a prerequisite for executing subsequent installation scripts.

```PowerShell
cd C:\Bitwarden
```

--------------------------------

### Create Bitwarden Installation Directory

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Creates the primary directory '/opt/bitwarden' where all Bitwarden installation files and data will reside. This centralizes the installation.

```Bash
sudo mkdir /opt/bitwarden
```

--------------------------------

### Rebuild Bitwarden Installation Assets from config.yml

Source: https://bitwarden.com/help/cli/install-on-premise

This command is used to regenerate necessary installation assets after making adjustments to the `./bwdata/config.yml` file, which is often required for specific installation scenarios like those behind a proxy.

```Bash
./bitwarden.sh rebuild
```

--------------------------------

### Apply Bitwarden Environment Variable Changes

Source: https://bitwarden.com/help/cli/install-on-premise

After modifying the `global.override.env` file, this command must be run to apply the changes and restart all Bitwarden containers, ensuring the new configurations take effect.

```Bash
./bitwarden.sh restart
```

--------------------------------

### Get help for Bitwarden Directory Connector CLI commands

Source: https://bitwarden.com/help/cli/directory-sync-cli

The Bitwarden Directory Connector CLI is self-documented. Use the `--help` option globally to list all available commands, or on a specific command to learn more about its usage and examples.

```Bash
bwdc --help
```

```Bash
bwdc test --help
bwdc config --help
```

--------------------------------

### Email Template: Learn How to Autofill with Bitwarden (3/5)

Source: https://bitwarden.com/help/cli/end-user-onboarding-emails

This email introduces the autofill feature, encouraging users to get acquainted with it after installing the extension and adding items. It highlights the convenience of one-click logins and provides a link to detailed instructions.

```Email
Subject: Autofill is auto-AMAZING (3/5)

Body:
Hi there,

Now that you've [installed the browser extension](/download/#downloads-web-browser) and added a few items to your vault, learn how to autofill for one-click logins!

Today's task is to get acquainted with the [autofill feature](/help/auto-fill-browser/). Here's what it looks like:

Autofill

Head over to Help for [instructions](/help/auto-fill-browser/).

The rest of your onboarding checklist:

*  [Download the browser extension](/download/#downloads-web-browser)
*  [Add logins and passwords to your account](/help/getting-started-webvault/#add-a-login)
* [**Learn how to autofill**](/help/auto-fill-browser/)
* [Learn how to share items with collections](/learning/individual-and-organizational-vaults/)

Stay secure,

Team Bitwarden
```

--------------------------------

### Email Template for Administrators: Announcing Company-Wide Bitwarden Deployment

Source: https://bitwarden.com/help/cli/welcome-email-templates

This template is intended for IT administrators before the company-wide rollout of Bitwarden Password Manager. It announces the deployment, emphasizes Bitwarden's security record, and outlines the ease of setup for managing users and passwords. It also provides steps for administrators to get started, join the organization, and access training resources. Placeholder text, such as '[company]' and '[Event details]', must be customized.

```text
To: Company IT administrators

Subject: Introducing Bitwarden Password Manager for company-wide deployment

Body:

Hello *[company]* IT administrators,

We are happy to announce the company-wide deployment of Bitwarden Password Manager. Bitwarden is a respected, industry-leading company with a strong security record, and we will utilize their password management solution to bring extra security to our business.

It is easy to set up Bitwarden and begin managing users and passwords. You can import saved credentials from other password managers and browsers to quickly get your users secure and practicing better password habits right away.

You will be given admin privileges in our Bitwarden deployment to help manage other team members and assist with onboarding users. To get started, sign up for an account and join our organization following the steps below:

*[Insert company-preferred onboarding workflow]*

Once you are confirmed to our organization, *[next steps for company-wide deployment]*.

Resources and training

To assist with deployment, training is available for administrators:

Admin training session option 1: *[Event details]*

Admin training session option 2: *[Event details]*

Visit the [Bitwarden learning page](/learning/getting-started-password-manager/) for video demos and setup guides. More about Bitwarden can be found at [bitwarden.com](/) within their extensive [documentation](/help/).

Thank you,

*[Sender's name and title]*
```

--------------------------------

### Create Bitwarden installation directory

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Creates the primary directory '/opt/bitwarden' where Bitwarden will be installed. This directory will house all Bitwarden related files.

```Bash
sudo mkdir /opt/bitwarden
```

--------------------------------

### Apply Bitwarden Configuration Changes with Restart

Source: https://bitwarden.com/help/cli/install-on-premise-linux

After modifying configuration files like `global.override.env`, this command is crucial for applying the updated settings. Executing `./bitwarden.sh restart` ensures that all changes take effect across the Bitwarden instance.

```Bash
./bitwarden.sh restart
```

--------------------------------

### Start Bitwarden Server with Docker Compose

Source: https://bitwarden.com/help/cli/install-on-premise-manual

This command starts the Bitwarden server in detached mode using Docker Compose, based on the `docker-compose.yml` file located in the `./docker` directory. It brings up all services defined in the compose file.

```Bash
docker compose -f ./docker/docker-compose.yml up -d
```

--------------------------------

### Start and Unlock Gnome Keyring Daemon

Source: https://bitwarden.com/help/cli/directory-sync-cli

After installing necessary dependencies, run these commands to start the D-Bus session and the Gnome Keyring daemon. This is crucial for resolving private key configuration errors related to the Linux keyring.

```Bash
export $(dbus-launch)
dbus-launch
gnome-keyring-daemon --start --daemonize --components=secrets
echo '<RANDOM-PASSPHRASE>' | gnome-keyring-daemon -r -d --unlock
```

--------------------------------

### Make Entrypoint Script Executable

Source: https://bitwarden.com/help/cli/developer-quick-start

This command makes the `entrypoint.sh` script executable, which is a prerequisite before building the Docker image. It ensures the script can be run by the container.

```Bash
chmod +x ./entrypoint.sh
```

--------------------------------

### Bitwarden CLI: Get Password Example

Source: https://bitwarden.com/help/cli/cli

Demonstrates retrieving a password using `bw get` by providing a search term. The command will return the password for the first matching item found in the vault.

```Bash
bw get password Github
```

--------------------------------

### Bitwarden CLI: Create Folder Workflow Example

Source: https://bitwarden.com/help/cli/cli

Demonstrates a typical workflow for creating a new folder using `bw create`. It involves getting a folder template, modifying its name with `jq`, encoding the JSON, and then creating the folder in the vault.

```Bash
bw get template folder | jq '.name="My First Folder"' | bw encode | bw create folder
```

--------------------------------

### Configure Bitwarden SMTP and Admin Environment Variables

Source: https://bitwarden.com/help/cli/install-on-premise-linux

This snippet illustrates the essential environment variables within `global.override.env` that must be configured. It includes settings for connecting to an SMTP mail server to enable email verification and invitations, and for granting access to the System Administrator Portal.

```Bash
globalSettings__mail__smtp__host=<placeholder>
globalSettings__mail__smtp__port=<placeholder>
globalSettings__mail__smtp__ssl=<placeholder>
globalSettings__mail__smtp__username=<placeholder>
globalSettings__mail__smtp__password=<placeholder>
...
adminSettings__admins=
```

--------------------------------

### Create and Save Passkeys with Bitwarden on iOS

Source: https://bitwarden.com/help/cli/auto-fill-ios

Guide on how to create and store new passkeys using Bitwarden on iOS when prompted by a website or app, including options to save new or overwrite existing passkeys.

```APIDOC
When creating a new passkey on a website or app, the iOS application will prompt you to store the passkey. Select Continue.
Note: Select Other Options if you do not wish to store the passkey in Bitwarden or Other Sign In Options to sign in with a passkey not stored in Bitwarden.
If a passkey already exists for this service, Bitwarden will allow you to save a new passkey by selecting the + icon to create a new item, or by overwriting an existing passkey.
```

--------------------------------

### Start Bitwarden Server with Docker Compose

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Starts the Bitwarden server containers defined in the docker-compose.yml file in detached mode. This command initializes all necessary server services.

```Bash
docker compose -f ./docker/docker-compose.yml up -d
```

--------------------------------

### Configure Keyboard Autofill for Passwords and Passkeys on iOS

Source: https://bitwarden.com/help/cli/auto-fill-ios

Step-by-step guide to enable Bitwarden's keyboard autofill feature on iOS, allowing automatic population of passwords and passkeys from the vault. Includes instructions for testing the setup.

```APIDOC
1. Open iOS Settings and then General on your device.
2. Tap AutoFill & Passwords.
3. Toggle AutoFill Passwords and Passkeys on and tap Bitwarden in the Autofill From: list.
   Tip: We highly recommend deactivating any other autofill service (like Keychain) in the Autofill From: list.
   Test autofill:
4. Open an app or website that you aren't currently signed in to.
5. Tap the username or password field on the login screen. A keyboard will slide up with a matching login (my_username), or with a Passwords button.
   If a matching login is displayed, tap it to autofill. If the Passwords button is displayed, tap it to browse your vault for the login to use.
   Note: Are you getting a Biometric unlock disabled pending verification of master password message? Learn what to do.
```

--------------------------------

### Install libsecret Dependency for Linux

Source: https://bitwarden.com/help/cli/directory-sync-cli

Instructions for installing the `libsecret` dependency on Linux distributions, which is required for the Bitwarden Directory Connector CLI. The example includes commands for Debian/Ubuntu and a general package manager (brew, often used on macOS but presented here in a Linux context).

```Bash
apt-get install libsecret-1-0
brew install libsecret
```

--------------------------------

### Run Docker Container with Bitwarden Secrets Injection

Source: https://bitwarden.com/help/cli/developer-quick-start

This command runs the Docker container, removing it after exit (`--rm`), running interactively (`-it`), and passing the Bitwarden Access Token as an environment variable (`-e BWS_ACCESS_TOKEN`). It starts the container, allowing the `entrypoint.sh` script to inject secrets at runtime securely.

```Bash
docker run --rm -it -e BWS_ACCESS_TOKEN=<your-access-token> image-name
```

--------------------------------

### Bitwarden CLI: Create Secure Note Example

Source: https://bitwarden.com/help/cli/cli

Provides an example of creating a secure note using `bw create`. It demonstrates how to change the item type to `2` for secure notes and set the note content and name using `jq`.

```Bash
bw get template item | jq '.type = 2 | .secureNote.type = 0 | .notes = "Contents of my Secure Note." | .name = "My Secure Note"' | bw encode | bw create item
```

--------------------------------

### Bitwarden CLI Import Example with File Path

Source: https://bitwarden.com/help/cli/import-from-keeper

An example of importing data using the Bitwarden CLI, demonstrating the use of a specific file path for a CSV file. Remember to replace `<format>` with the actual file format.

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Configure Bitwarden SMTP and Admin Environment Variables

Source: https://bitwarden.com/help/cli/install-on-premise

This snippet shows how to edit the `global.override.env` file to configure SMTP settings for email verification and add administrator email addresses for the System Administrator Portal. These settings are crucial for new user registration and organization invitations.

```Bash
...
globalSettings__mail__smtp__host=<placeholder>
globalSettings__mail__smtp__port=<placeholder>
globalSettings__mail__smtp__ssl=<placeholder>
globalSettings__mail__smtp__username=<placeholder>
globalSettings__mail__smtp__password=<placeholder>
...
adminSettings__admins=
...
```

--------------------------------

### Verify Running Docker Containers

Source: https://bitwarden.com/help/cli/install-on-premise-windows

This command checks the status of all Docker containers to ensure Bitwarden services are running as expected after initial setup. It helps confirm the health of the deployment.

```Bash
docker ps
```

--------------------------------

### Bitwarden Starts With Match Detection for Autofill

Source: https://bitwarden.com/help/cli/uri-match-detection

Describes Bitwarden's 'Starts with' match detection, which offers autofill when the detected resource begins with the specified URI. Includes a table illustrating autofill behavior.

```APIDOC
For example, if the URI https://sub.domain.com/path/ uses starts with match detection:
| URL | Autofill? |
| --- | --- |
| https://sub.domain.com/path/ |  |
| https://sub.domain.com/path/page.html |  |
| https://sub.domain.com |  |
| https://sub.domain.com:4000/path/page.html (interrupted with a port) |  |
| https://sub.domain.com/path (absent trailing slash) |  |
```

--------------------------------

### Bitwarden Server Install and Update URLs

Source: https://bitwarden.com/help/cli/bitwarden-addresses

Provides URLs used for self-hosting Bitwarden servers, including installation and update resources.

```APIDOC
func.bitwarden.com
artifacts.bitwarden.com
selfhost.bitwarden.com
btwrdn.co
ghcr.io/bitwarden
```

--------------------------------

### Initial Setup for Bitwarden Passkey Usage on iOS

Source: https://bitwarden.com/help/cli/auto-fill-ios

Prerequisite steps to configure iOS settings to allow Bitwarden to manage and use passkeys, ensuring the 'AutoFill Passwords and Passkeys' option is enabled.

```APIDOC
To use passkey functionality, open your iOS Settings app and navigate to Passwords → Password Options. Toggle the following options on:
- Toggle AutoFill Passwords and Passkeys on.
- Toggle Bitwarden on in the Use passwords and passkeys from: list.
```

--------------------------------

### Start Bitwarden CLI Application

Source: https://bitwarden.com/help/cli/kerberos-integration

This command restarts the Bitwarden containers after initial setup. Upon restart, the `admin` container will populate the configured external MSSQL database. Users who previously used the built-in `mssql` container will need to migrate their data to the new external database using backup/restore or export/import methods.

```Shell
./bitwarden restart
```

--------------------------------

### Bitwarden Two-Step Login Methods and Requirements

Source: https://bitwarden.com/help/cli/setup-two-step-login

Provides a structured overview of all available two-step login methods in Bitwarden, detailing their setup instructions and subscription requirements for individual users and organizational accounts (Teams and Enterprise).

```APIDOC
Two-step login methods for individuals:
  - Method: FIDO2 WebAuthn credentials (e.g., hardware keys like YubiKeys and Google Titan)
    Setup instructions: /help/setup-two-step-login-fido/
    Subscription requirements: Free for all
  - Method: Authenticator app (e.g., Bitwarden Authenticator)
    Setup instructions: /help/setup-two-step-login-authenticator/
    Subscription requirements: Free for all
  - Method: Email
    Setup instructions: /help/setup-two-step-login-email/
    Subscription requirements: Free for all
  - Method: Duo Security with Duo Push, SMS, phone call, and security keys
    Setup instructions: /help/setup-two-step-login-duo/
    Subscription requirements: Requires premium
  - Method: YubiKey OTP (any 4/5 series device or YubiKey NEO/NFC)
    Setup instructions: /help/setup-two-step-login-yubikey/
    Subscription requirements: Requires premium

Two-step login methods for Teams and Enterprise:
  - Method: Duo Security with Duo Push, SMS, phone call, and security keys
    Setup instructions: /help/setup-two-step-login-duo/
    Subscription requirements: Requires Teams or Enterprise

Additional Enterprise organization options:
  - Require two-step login with a policy: /help/policies/#two-step-login
  - Achieve protection outside Bitwarden using Identity Provider with Single Sign-On (SSO)
```

--------------------------------

### Rebuild Bitwarden Installation Assets

Source: https://bitwarden.com/help/cli/install-on-premise-windows

Execute the Bitwarden PowerShell script with the `-rebuild` flag to regenerate installation assets. This command is typically used after making manual adjustments to the `config.yml` file, especially for advanced installation scenarios like those involving proxies or alternate ports.

```PowerShell
.\bitwarden.ps1 -rebuild
```

--------------------------------

### Sample Bitwarden Public API GET Request (Bash)

Source: https://bitwarden.com/help/cli/public-api

Provides an example of a GET request to the Bitwarden Public API's collections endpoint using curl. It demonstrates how to include the obtained bearer token in the Authorization header for authentication.

```Bash
curl -X GET \
  https://api.bitwarden.com/public/collections \
  -H 'Authorization: Bearer <TOKEN>'
```

--------------------------------

### Example: Import CSV data with Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-from-dashlane

An example of using the `bw import` command to import a CSV file from a specified path into your Bitwarden vault.

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Retrieve Bitwarden Secrets in Entrypoint Script

Source: https://bitwarden.com/help/cli/developer-quick-start

This `entrypoint.sh` script demonstrates two methods for retrieving secrets using the Bitwarden Secrets Manager CLI. It shows how to get an individual secret by ID and how to use the `bws run` command to inject secrets based on names, preparing them for application use. Note that the `bws run` method is sensitive to spaces in secret names.

```Bash
#!/usr/bin/env bash
# One way to retrieve individual secrets is to use the `get` command and extract the value:
SECRET_1=$(bws secret get fc3a93f4-2a16-445b-b0c4-aeaf0102f0ff | jq '.value')

# Another option., this method is sensitive to spaces in the secret name. See the `run` command documentation for more options
bws run -- 'echo $SECRET_NAME'

# Run your project
```

--------------------------------

### Verify Running Docker Containers

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This command lists all currently running Docker containers, allowing verification that the Bitwarden server components are active and healthy after startup.

```Bash
docker ps
```

--------------------------------

### Start Bitwarden Unified Deployment using Docker Compose

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command starts all services defined in the docker-compose.yml file in detached mode, allowing them to run in the background.

```Bash
docker compose up -d
```

--------------------------------

### Get Bitwarden CLI Version

Source: https://bitwarden.com/help/cli/versioning

This command prints the currently installed Bitwarden CLI version to the console. It is used to quickly check the version of the command-line interface application.

```Bash
bw -v
```

--------------------------------

### Bitwarden Desktop App Win32 Install and Uninstall Commands for Intune

Source: https://bitwarden.com/help/cli/deploy-desktop-apps-with-intune

Specifies the command-line arguments for silent installation and uninstallation of the Bitwarden desktop application when deployed as a Win32 app through Microsoft Intune. The install command requires replacing '{version}' with the actual application version.

```CLI
Install command: Bitwarden-installer-{version}.exe /allusers /S
Uninstall command: C:\Program Files\Bitwarden\Uninstall Bitwarden.exe /allusers /S
```

--------------------------------

### Bitwarden CLI: `bw send` Full Example with Options

Source: https://bitwarden.com/help/cli/send-cli

This example demonstrates how to create a text Send using multiple options, including specifying a custom name, a 7-day deletion period, and making the text content hidden for recipients.

```Bash
bw send -n "My First Send" -d 7 --hidden "The contents of my first Send."
```

--------------------------------

### Create Bitwarden Directory in PowerShell

Source: https://bitwarden.com/help/cli/install-on-premise-windows

This PowerShell command creates a new directory named 'Bitwarden' directly under the C: drive. This directory will be used to store Bitwarden installation files and data, and it needs to be shared with Docker Desktop.

```PowerShell
mkdir Bitwarden
```

--------------------------------

### Verify Bitwarden Directory Connector CLI Installation

Source: https://bitwarden.com/help/cli/directory-sync-cli

Run this command in your terminal to confirm that the `bwdc` executable is correctly installed and accessible in your system's PATH, ensuring the CLI is ready for use.

```Bash
bwdc --help
```

--------------------------------

### Contribute to Bitwarden Language Translations via Crowdin

Source: https://bitwarden.com/help/cli/localization

Learn how to contribute to or correct existing Bitwarden translations, or start translating to a new language using the Crowdin platform.

```User
Bitwarden uses a translation tool called Crowdin to manage our localization effort across many different languages (no programming knowledge required).
* To contribute to or make corrections to an existing translation, join our project.
* To start translating Bitwarden to a new language, join our project and contact the project owner.
```

--------------------------------

### Install Bitwarden CLI with Snap on Linux

Source: https://bitwarden.com/help/cli/cli

This command installs the Bitwarden Command Line Interface using Snap, a universal software packaging and deployment system for Linux. It offers a sandboxed and easy-to-manage installation.

```Bash
sudo snap install bw
```

--------------------------------

### Start SQLCMD Utility for MSSQL Database

Source: https://bitwarden.com/help/cli/backup-on-premise

Launch the `sqlcmd` command-line utility inside the `mssql` container to interact with the SQL Server database. Replace `<sa>` and `<sa-password>` with the credentials found in your `global.override.env` file.

```Bash
/opt/mssql-tools/bin/sqlcmd -S localhost -U <sa> -P <sa-password>
```

--------------------------------

### Apply Configuration Changes to Bitwarden Self-Hosted Installation

Source: https://bitwarden.com/help/cli/self-hosting-scim

Runs the update script again to ensure all changes, including the SCIM enablement, are fully applied and the server is running with the new configuration.

```Bash
./bitwarden.sh update
```

--------------------------------

### Display Helm Command Help

Source: https://bitwarden.com/help/cli/secrets-manager-kubernetes-operator

These commands display the detailed help documentation for the `helm install` and `helm upgrade` commands. Running these provides comprehensive information on all available options, flags, and usage examples for each command.

```bash
helm install --help
helm upgrade --help
```

--------------------------------

### Bitwarden CLI: Create Login Item Workflow Example

Source: https://bitwarden.com/help/cli/cli

Illustrates how to create a new login item with a username and password using `bw create`. This example shows nested JSON manipulation with `jq` to set the item's name and login credentials.

```Bash
bw get template item | jq ".name=\"My Login Item\" | .login=$(bw get template item.login | jq '.username=\"jdoe\" | .password=\"myp@ssword123\"')" | bw encode | bw create item
```

--------------------------------

### Bitwarden CLI: Get Attachment with Output Directory Example

Source: https://bitwarden.com/help/cli/cli

Illustrates how to download a file attachment to a specific directory using the `--output` option with `bw get attachment`. The output path must end with a forward slash for a directory or specify a full filename.

```Bash
bw get attachment photo.png --itemid 99ee88d2-6046-4ea7-92c2-acac464b1412 --output /Users/myaccount/Pictures/
```

--------------------------------

### Accessing Specific Bitwarden Command Help

Source: https://bitwarden.com/help/cli/cli

These commands demonstrate how to get detailed help for specific Bitwarden CLI commands, such as 'list' or 'move'. Appending '--help' to any 'bw' command provides information on its available options and usage examples.

```Bash
bw list --help
bw move --help
```

--------------------------------

### Create Bitwarden local user

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Creates a new dedicated 'bitwarden' service account on the system. This user will be used to install and run Bitwarden, isolating it from other applications.

```Bash
sudo adduser bitwarden
```

--------------------------------

### Install or Upgrade Bitwarden Helm Chart

Source: https://bitwarden.com/help/cli/self-host-with-helm

This command installs or upgrades the Bitwarden self-host Helm chart into the 'bitwarden' namespace. It utilizes the configurations defined in 'my-values.yaml' to customize the deployment, including certificate settings and other parameters.

```Bash
helm upgrade bitwarden bitwarden/self-host --install --namespace bitwarden --values my-values.yaml
```

--------------------------------

### Example: Import CSV Data to Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-from-chrome

An example demonstrating the `bw import` command to import a CSV file from a specified path. Replace `<format>` with the actual format (e.g., `csv`) and the path with your file's location.

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Install Bitwarden CLI Globally with NPM

Source: https://bitwarden.com/help/cli/cli

This command installs the Bitwarden Command Line Interface globally using Node Package Manager (NPM). It is the preferred installation method for users already comfortable with NPM, offering ease of updates.

```Bash
npm install -g @bitwarden/cli
```

--------------------------------

### Bitwarden CLI: `bw send get` Command Options

Source: https://bitwarden.com/help/cli/send-cli

Available options for the `bw send get` command, allowing specification of output format for text or file Sends.

```APIDOC
Options:
* --text: Output only the text contents of a text Send.
* --file: Output only the file of a file Send. Pair --file with --output to specify a directory, or with --raw to output to stdout.
* --output <output>: Specify the output directory for the --file option.
```

--------------------------------

### Bitwarden CLI: Get Help and Check Version

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Learn how to access help documentation for Bitwarden Secrets Manager CLI commands and check the installed version. This section also notes a syntax change for listing secrets as of version 0.3.0.

```Bash
bws run --help
bws secret --help
bws project --help
```

```Bash
bws --version
```

--------------------------------

### Update and Restart Bitwarden Server with Docker Compose

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This command first stops and removes the current Bitwarden server containers, then restarts them in detached mode with updated configurations and container images. It's used for applying server updates to a manually installed server.

```Bash
docker compose -f ./docker/docker-compose.yml down && docker compose -f ./docker/docker-compose.yml up -d
```

--------------------------------

### Set Ownership of Bitwarden Directory

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Changes the ownership of the '/opt/bitwarden' directory and its contents to the 'bitwarden' user and group, aligning with the dedicated service account setup.

```Bash
sudo chown -R bitwarden:bitwarden /opt/bitwarden
```

--------------------------------

### Email Template for End-Users: Announcing Bitwarden Password Manager

Source: https://bitwarden.com/help/cli/welcome-email-templates

This template is designed to be sent to end-users before the Bitwarden Password Manager rollout. It introduces Bitwarden as a security and productivity tool, highlights its benefits like generating and autofilling strong passwords, and provides steps for getting started and accessing training resources. Placeholder text, such as '[Event details]' and '[Insert company-preferred onboarding workflow]', must be replaced with specific business information.

```text
To: All end-users

Subject: Introducing Bitwarden Password Manager - new security and productivity tool

Body:

Hello everyone,

We are happy to announce the deployment of Bitwarden Password Manager for everyone at [company].

A password manager is a very important tool for staying secure online. Bitwarden generates, saves, and then autofills strong passwords for you, so that you don’t have to remember or type any passwords. Importantly, this makes it easy to have passwords that are unique to every website and app that you log into, which is the best way to stay secure and protect against a data breach. A weak or reused password is a vulnerable entry point for hackers to hurt our business through data breaches, ransomware, or other attacks.

It’s easy to import any passwords that you have saved in your web browser or other solution, so you can get started practicing secure password habits today.

To get started, follow these steps:

*[Insert company-preferred onboarding workflow]*

Your administrator will help to make sure you have access to the correct shared password collections.

Resources and training

To help you be successful with password management, training is available for users:

Training session option 1: *[Event details]*

Training session option 2: *[Event details]*

Visit the [Bitwarden learning page](/learning/getting-started-password-manager/) for video demos and setup guides. More about Bitwarden can be found at [bitwarden.com](/) within their extensive [documentation](/help/).

Thank you,

*[Sender's name and title]*
```

--------------------------------

### Bitwarden Regular Expression Match Detection (Safe Example)

Source: https://bitwarden.com/help/cli/uri-match-detection

Provides a safe example of using regular expressions for URI matching, demonstrating a more precise pattern to control autofill behavior.

```APIDOC
If the URI ^https://[a-z]+\.wikipedia\.org/w/index\.php uses regular expression match detection:
| URL | Autofill? |
| --- | --- |
| https://en.wikipedia.org/w/index.php?title=Special:UserLogin&returnto=Bitwarden |  |
| https://pl.wikipedia.org/w/index.php?title=Specjalna:Zaloguj&returnto=Bitwarden |  |
| https://en.wikipedia.org/w/index.php |  |
| https://malicious-site.com |  |
| https://en.wikipedia.org/wiki/Bitwarden |  |
```

--------------------------------

### Example JSON Output for Bitwarden Project List

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This is an example of the default JSON array output when listing Bitwarden projects. Each object represents a project with details such as its ID, organization ID, name, and creation/revision dates.

```JSON
[
  {
    "object": "project",
    "id": "e325ea69-a3ab-4dff-836f-b02e013fe530",
    "organizationId": "10e8cbfa-7bd2-4361-bd6f-b02e013f9c41",
    "name": "App 1",
    "creationDate": "2023-06-27T19:24:42.181607Z",
    "revisionDate": "2023-06-27T19:24:42.181607Z"
  },
  ...
]
```

--------------------------------

### Example LastPass CSV entry with grouping column

Source: https://bitwarden.com/help/cli/import-from-lastpass

This snippet shows a single line from a LastPass CSV export that includes the 'grouping' column, which needs to be removed to resolve the maximum collections error.

```CSV
https://github.com/login,username,password,,,Github,Productivity Tools,0
```

--------------------------------

### Bitwarden Passkey Creation Mechanics

Source: https://bitwarden.com/help/cli/login-with-passkeys

Explains the underlying process of registering a passkey with Bitwarden, detailing key generation and data exchange for both encrypted and unencrypted vault setups.

```APIDOC
When a passkey is registered for log in to Bitwarden:
* A passkey public and private key pair is generated by the authenticator via the WebAuthn API. This key pair, by definition, is what constitutes your passkey.
* A PRF symmetric key is generated by the authenticator via the WebAuthn API's PRF extension. This key is derived from an internal secret unique to your passkey and a salt provided by Bitwarden.
* A PRF public and private key pair is generated by the Bitwarden client. The PRF public key encrypts your account encryption key, which your client will have access to by virtue of being logged in and unlocked, and the resulting PRF-encrypted account encryption key is sent to the server.
* The PRF private key is encrypted with the PRF symmetric key (see Step 2) and the resulting PRF-encrypted private key is sent to the server.
* Your client sends data to Bitwarden servers to create a new passkey credential record for your account. If your passkey is registered with support for vault encryption and decryption, this record includes:
  + The passkey name
  + The passkey public key
  + The PRF public key
  + The PRF-encrypted account encryption key
  + The PRF-encrypted private key
Your passkey private key, which is required to accomplish authentication, only ever leaves the client in an encrypted format.
```

```APIDOC
When a passkey is registered for log in to Bitwarden:
1. A passkey public and private key pair is created. This key pair, by definition, is what constitutes your passkey.
2. Your client sends data to Bitwarden servers to create a new passkey credential record for your account. If your passkey is not registered with support for vault encryption and decryption, this record includes:
   * The passkey's name
   * The passkey's public key
Your passkey's private key, which is required to accomplish authentication, only ever leaves the client in an encrypted format.
```

--------------------------------

### Export Identity Certificate to PFX with OpenSSL

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This command exports the generated `identity.key` and `identity.crt` into a PKCS#12 archive (`.pfx` file) named `identity.pfx`. It requires the certificate password created in a previous step.

```Bash
openssl pkcs12 -export -out ./identity/identity.pfx -inkey identity.key -in identity.crt -passout pass:IDENTITY_CERT_PASSWORD
```

--------------------------------

### Install Build-Essential for Bitwarden CLI on Linux

Source: https://bitwarden.com/help/cli/cli

On Linux systems, installing the Bitwarden CLI via NPM may require the `build-essential` dependency. This command installs the necessary packages using `apt` on Debian/Ubuntu-based distributions.

```Plain
apt install build-essential
```

--------------------------------

### Install Dependencies for Linux Keyring Issues

Source: https://bitwarden.com/help/cli/directory-sync-cli

To resolve the "Object does not exist at path \"/org/freedesktop/secrets/collection/login\"" error when configuring a private key, ensure these dependencies are installed. They are required for the Bitwarden Directory Connector to use Linux's keyring.

```Bash
sudo apt install dbus-x11 gnome-keyring
```

--------------------------------

### Example LastPass CSV entry after removing grouping column

Source: https://bitwarden.com/help/cli/import-from-lastpass

This snippet shows the corrected version of a LastPass CSV entry, with the 'grouping' column and its corresponding data removed, resolving the maximum collections error.

```CSV
https://github.com/login,username,password,,,Github,0
```

--------------------------------

### Download Bitwarden Docker Stub Archive

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Downloads the specified Bitwarden Docker stub archive (e.g., `docker-stub-US.zip`) from the official GitHub releases using `curl`. Replace `<version_number>` with the desired release version.

```Bash
curl -L https://github.com/bitwarden/server/releases/download/v<version_number>/docker-stub-US.zip \
 -o docker-stub-US.zip
```

--------------------------------

### Configure Bitwarden Extension Force Installation for Chrome on Linux

Source: https://bitwarden.com/help/cli/browserext-deploy

This JSON snippet, to be added to `managed_preferences.json`, forces the installation of the Bitwarden browser extension (ID `nngceckbapebfimnlniiiahkandclblb`) in Google Chrome on Linux. It uses the `ExtensionSettings` policy to specify the installation mode and update URL from the Chrome Web Store.

```JSON
{
  "policies:": {
  "ExtensionSettings": {
    "nngceckbapebfimnlniiiahkandclblb": {
      "installation_mode": "force_installed",
      "update_url":
         "https://clients2.google.com/service/update2/crx"
      }
    }
  }
}
```

--------------------------------

### Authenticate Bitwarden Secrets Manager CLI with Access Token

Source: https://bitwarden.com/help/cli/developer-quick-start

This snippet demonstrates how to authenticate the Bitwarden Secrets Manager CLI by setting the `BWS_ACCESS_TOKEN` environment variable. This token is generated for a machine account and limits access to secrets and projects the account has permissions for.

```Bash
export BWS_ACCESS_TOKEN=0.48c78342-1635-48a6-accd-afbe01336365.C0tMmQqHnAp1h0gL8bngprlPOYutt0:B3h5D+YgLvFiQhWkIq6Bow==
```

--------------------------------

### Add Bitwarden Secrets Manager CLI to GitLab CI/CD Workflow

Source: https://bitwarden.com/help/cli/gitlab-integration

This snippet provides a rudimentary GitLab CI/CD workflow definition to be saved as `.gitlab-ci.yml`. It demonstrates how to install the Bitwarden Secrets Manager CLI (bws) within the pipeline and then use the `bws run` command to inject secrets into subsequent commands, such as `npm run start`.

```Bash
stages:
- default_runner

image: ubuntu
build:
  stage: default_runner
  script:
  - |
    # install bws
    apt-get update && apt-get install -y curl git jq unzip
    export BWS_VER="1.0.0"
    curl -LO \
      "https://github.com/bitwarden/sdk/releases/download/bws-v$BWS_VER/bws-x86_64-unknown-linux-gnu-$BWS_VER.zip"
    unzip -o bws-x86_64-unknown-linux-gnu-$BWS_VER.zip -d /usr/local/bin

  # use the `bws run` command to inject secrets into your commands
  - bws run -- 'npm run start'
```

--------------------------------

### Restart Bitwarden Self-Hosted Installation

Source: https://bitwarden.com/help/cli/deploy-key-connector

This command restarts your self-hosted Bitwarden installation to apply configuration changes, such as those made for Key Connector activation. It ensures that all new settings take effect.

```Bash
./bitwarden.sh restart
```

--------------------------------

### Allow Bitwarden Snap App to Access Secure Storage on Linux

Source: https://bitwarden.com/help/cli/getting-started-desktop

For users who installed the Bitwarden desktop app via Snap, this command grants the application access to secure storage for persisting authentication tokens. This step is crucial for proper functionality after installation and requires logging out and back into all accounts if already logged in.

```Bash
sudo snap connect bitwarden:password-manager-service
```

--------------------------------

### Example: Import CSV Data with Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-from-passwordsafe

An example demonstrating how to import a CSV file named `mydata.csv` into your Bitwarden vault using the `bw import` command. Replace `<format>` with the appropriate file format for CSV.

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Example Environment Variable Output for Bitwarden Secret List

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This is an example of the `env` output format when listing Bitwarden secrets. It shows secrets as `KEY="VALUE"` pairs, with invalid key names commented out to indicate modification.

```Plain
this_is_a_keyname="this is a key value"
CLOUDFLARE_API_TOKEN="123412341234123412341234"
# This is an invalid keyname="this will get commented-out"
```

--------------------------------

### Email Template for Bitwarden Adoption Program Introduction

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

An introductory email template outlining a six-day plan designed to increase user adoption of Bitwarden, covering essential strategies for successful deployment.

```Email
Subject: Tips to get your team to use Bitwarden

Body: Hi [name],

Getting the right start with password management can lead to a successful deployment for employees.

You'll soon receive a six-day plan to help increase user adoption of your new password manager among your colleagues.

These brief, actionable emails will cover essential strategies including:
1. Appoint an implementation champion
2. Communicate your rollout plan
3. Explain the top benefits of a password manager
4. Share get-started guides
5. Use email templates for easy sharing

Be on the lookout for the adoption program coming your way shortly.
```

--------------------------------

### Customize TOTP Parameters with otpauth URI Example (Bash)

Source: https://bitwarden.com/help/cli/integrated-authenticator

This example demonstrates how to customize TOTP parameters like algorithm, digits, and period by manually editing the `otpauth://totp/` URI for a vault item. This allows Bitwarden to generate TOTPs with non-default settings required by some services.

```Bash
otpauth://totp/Test:me?secret=JBSWY3DPEHPK3PXP&algorithm=sha256&digits=8&period=60
```

--------------------------------

### Ansible Playbook Example for Bitwarden Secret Lookup

Source: https://bitwarden.com/help/cli/ansible-integration

Provides a comprehensive Ansible playbook example showcasing various ways to lookup Bitwarden secrets. It includes examples for using environment variables for access tokens, specifying state file directories, retrieving specific fields, and referencing secrets within tasks.

```Ansible
--- 
- name: Using secrets from Bitwarden

  vars:
    bws_access_token: "{{ lookup('env', 'CUSTOM_ACCESS_TOKEN_VAR') }}"
    state_file_dir: "{{ '~/.config/bitwarden-sm' | expanduser }}"
    secret_id: "9165d7a8-2c22-476e-8add-b0d50162c5cc"

    secret: "{{ lookup('bitwarden.secrets.lookup', secret_id) }}"
    secret_with_field: "{{ lookup('bitwarden.secrets.lookup', secret_id, field='note' ) }}"
    secret_with_access_token: "{{ lookup('bitwarden.secrets.lookup', secret_id, access_token=bws_access_token ) }}"
    secret_with_state_file: "{{ lookup('bitwarden.secrets.lookup', secret_id, state_file_dir=state_file_dir ) }}"

  tasks:
    - name: Use the secret in a task
      include_tasks: tasks/add_db_user.yml # reference the secrets with "{{ secret }}", "{{ secret_with_field }}", etc.
```

--------------------------------

### Start Bitwarden CLI Local API Server (serve command)

Source: https://bitwarden.com/help/cli/cli

The `bw serve` command starts a local Express web server, enabling RESTful API calls to access CLI actions via an HTTP interface. It defaults to port 8087 and binds to `localhost`, but these can be customized. Origin protection is enabled by default and should not be disabled.

```Bash
bw serve --port <port> --hostname <hostname>
```

--------------------------------

### Skip SQL Server Database Preparation

Source: https://bitwarden.com/help/cli/environment-variables

Specify `true` to skip application-side database preparation during installation. If skipped, the named database must exist before initiating installation, and this task requires elevated MSSQL privileges.

```APIDOC
globalSettings__sqlServer__SkipDatabasePreparation=true
```

--------------------------------

### Configure Individual Bitwarden CLI Service URLs

Source: https://bitwarden.com/help/cli/change-client-environment

For unique setups, these commands allow specifying separate URLs for different Bitwarden services (web vault, API, identity, icons, notifications, events, key connector) when connecting the CLI to a self-hosted instance.

```Bash
bw config server --web-vault <url>
bw config server --api <url>
bw config server --identity <url>
bw config server --icons <url>
bw config server --notifications <url>
bw config server --events <url>
bw config server --key-connector <url>
```

--------------------------------

### Configure Bitwarden Extension Force Installation for Firefox on Linux

Source: https://bitwarden.com/help/cli/browserext-deploy

This JSON snippet, to be added to `policies.json` in Firefox's `distribution` directory, forces the installation of the Bitwarden browser extension (ID `446900e4-71c2-419f-a6a7-df9c091e268b`) in Firefox on Linux. It uses the `ExtensionSettings` policy to specify the installation mode and URL from the Mozilla Add-ons store.

```JSON
{
"policies": {
 "ExtensionSettings": {
   "446900e4-71c2-419f-a6a7-df9c091e268b": {
     "installation_mode": "force_installed",
     "install_url": "https://addons.mozilla.org/firefox/downloads/latest/bitwarden-password-manager/latest.xpi"
      }
    }
  }
}
```

--------------------------------

### Install Bitwarden SDK for Ansible Integration

Source: https://bitwarden.com/help/cli/ansible-integration

This command installs the Bitwarden SDK, a prerequisite for using the Bitwarden Ansible collection. It is recommended to install Python packages within a Python virtual environment.

```Bash
pip install bitwarden-sdk
```

--------------------------------

### Bitwarden Single Sign-On Configuration Fields from Cloudflare Setup

Source: https://bitwarden.com/help/cli/cloudflare-zero-trust-sso-implementation

This table outlines the values to be copied from the Cloudflare Zero Trust 'Setup' screen into their corresponding fields on the Bitwarden Single Sign-On page.

```APIDOC
SSO endpoint: The SSO endpoint directs where your SaaS application will send login requests. This value will be entered into the Single Sign On Service URL field in Bitwarden.
Access Entity ID or Issuer: The Access Entity ID or Issuer is the unique identifier of your SaaS application. This will value will be entered into the Entity ID field on Bitwarden.
Public key: The Public key is the access public certificate that will be used to verify your identity. This value will be entered into the X509 Public Certificate field on Bitwarden.
```

--------------------------------

### Install Bitwarden CLI with Chocolatey on Windows

Source: https://bitwarden.com/help/cli/cli

This command installs the Bitwarden Command Line Interface using Chocolatey, a popular package manager for Windows. It provides a convenient way to manage CLI installations on Windows systems.

```Bash
choco install bitwarden-cli
```

--------------------------------

### Bitwarden API Response with Continuation Token Example (APIDOC)

Source: https://bitwarden.com/help/cli/public-api

Illustrates a JSON response structure that includes a 'continuationToken' for paginated results. This example shows a list object containing collection details, demonstrating where the token is provided.

```APIDOC
{
  "object": "list",
  "data": [
    {
      "externalId": "external_id_123456",
      "object": "collection",
      "id": "539a36c5-e0d2-4cf9-979e-51ecf5cf6593",
      "groups": [
        {
          "id": "bfbc8338-e329-4dc0-b0c9-317c2ebf1a09",
          "readOnly": true,
          "hidePasswords": true,
          "manage": true
        }
      ]
    }
  ],
  "continuationToken": "string"
}
```

--------------------------------

### Configure Key Connector Endpoints

Source: https://bitwarden.com/help/cli/deploy-key-connector

Example configuration for Key Connector endpoints in `key-connector.override.env`, specifying the Bitwarden web vault and identity server URIs. These values are crucial for Key Connector's communication with Bitwarden services.

```Bash
keyConnectorSettings__webVaultUri=https://your.bitwarden.domain.com
keyConnectorSettings__identityServerUri=http://identity:5000
```

--------------------------------

### Configure Key Connector Certificate Filesystem Path

Source: https://bitwarden.com/help/cli/deploy-key-connector

Shows how to specify the filesystem path for a PEM-encoded public key certificate required by Key Connector. The example uses a path mounted within the container.

```Plain
keyConnectorSettings__certificate__filesystemPath=/etc/bitwarden/key-connector/certificate.pem
```

--------------------------------

### Bitwarden Browser Extension Full Service URL Configuration (Linux Chrome/Chromium)

Source: https://bitwarden.com/help/cli/deploy-clients

Advanced JSON configuration for `bitwarden.json` to specify individual URLs for all Bitwarden services (webVault, api, identity, icons, notifications, events) for the browser extension. This is used in unique self-hosted setups where different services might reside at distinct endpoints. The extension ID (`nngceckbapebfimnlniiiahkandclblb`) is specific to the installation.

```JSON
{
  "3rdparty": {
  "extensions": {
  "nngceckbapebfimnlniiiahkandclblb": {
      "environment": {
        "base": "https://my.bitwarden.server.com",
        "webVault": "https://my.bitwarden.server.com",
        "api": "https://my.bitwarden.server.com",
        "identity": "https://my.bitwarden.server.com",
        "icons": "https://my.bitwarden.server.com",
        "notifications": "https://my.bitwarden.server.com",
        "events": "https://my.bitwarden.server.com"
        }
      }
    }
  }
}
```

--------------------------------

### Configure Detailed Bitwarden Browser Extension Server URLs (Linux Chrome/Chromium)

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This JSON configuration file allows for independent specification of various Bitwarden service URLs (webVault, API, identity, icons, notifications, events) for the browser extension on Linux systems using Chrome or Chromium. This detailed configuration is typically required for unique setups where a single base URL is insufficient. The extension ID (nngceckbapebfimnlniiiahkandclblb) is a placeholder and will vary depending on your installation method, which can be found in your browser's extension menu.

```JSON
{
  "3rdparty": {
  "extensions": {
  "nngceckbapebfimnlniiiahkandclblb": {
      "environment": {
        "base": "https://my.bitwarden.server.com",
        "webVault": "https://my.bitwarden.server.com",
        "api": "https://my.bitwarden.server.com",
        "identity": "https://my.bitwarden.server.com",
        "icons": "https://my.bitwarden.server.com",
        "notifications": "https://my.bitwarden.server.com",
        "events": "https://my.bitwarden.server.com"
        }
      }
    }
  }
}
```

--------------------------------

### Example LastPass CSV causing maximum collections error

Source: https://bitwarden.com/help/cli/import-from-lastpass

This CSV snippet demonstrates a LastPass export that would trigger the 'Maximum collections error' in Bitwarden due to having three distinct 'grouping' values (Social, Productivity Tools, Finance), exceeding the two-collection limit for free organizations.

```CSV
url,username,password,totp,extra,name,grouping,fav
https://www.facebook.com/login.php,username,password,,,Facebook,Social,0
https://twitter.com/login,username,password,,,Twitter,Social,0
https://asana.com/,login,password,,,Asana,Productivity Tools,0
https://github.com/login,username,password,,,Github,Productivity Tools,0
https://www.paypal.com/login,username,password,,,Paypal,Finance,0
https://www.bankofamerica.com/,username,password,,,Bankofamerica,Finance,0
```

--------------------------------

### Inject Database Credentials into Docker Container at Runtime

Source: https://bitwarden.com/help/cli/developer-quick-start

This `docker run` command demonstrates how to inject the previously stored temporary environment variables (`SECRET_1` for username and `SECRET_2` for password) into a Bitwarden Unified Docker container. The `-env` flag passes these variables, allowing the container to securely access sensitive database credentials without exposing them in plaintext.

```Bash
docker run -d --name bitwarden .... -env BW_DB_USERNAME=$SECRET_1 BW_BD_PASSWORD=$SECRET_2 .... bitwarden/self-host:beta
```

--------------------------------

### Configure Okta SCIM API Integration for Bitwarden

Source: https://bitwarden.com/help/cli/okta-scim-integration

Details the steps to enable and configure the API integration for SCIM provisioning in Okta, including setting the Base URL and API Token for Bitwarden.

```APIDOC
Provisioning Settings - Configure API Integration:
  1. Check the "Enable API Integration" checkbox.
  2. In the "Base URL" field, enter your SCIM URL.
  3. In the "API Token" field, enter your SCIM API Key.
  4. Use the "Test API Credentials" button to test your configuration.
  5. Select the "Save" button.
```

--------------------------------

### Configure Firefox Policy with All Bitwarden Service URLs

Source: https://bitwarden.com/help/cli/deploy-clients

This JSON configuration file provides a comprehensive setup for the Bitwarden extension in Firefox, specifying individual URLs for various services like web vault, API, identity, and notifications. This is for unique setups requiring explicit service URL definitions.

```JSON
{
 "policies": {
    "3rdparty": {
      "Extensions": {
        "{446900e4-71c2-419f-a6a7-df9c091e268b}": {
          "environment": {
            "base": "https://my.bitwarden.server.com",
            "webVault": "https://my.bitwarden.server.com",
            "api": "https://my.bitwarden.server.com",
            "identity": "https://my.bitwarden.server.com",
            "icons": "https://my.bitwarden.server.com",
            "notifications": "https://my.bitwarden.server.com",
            "events": "https://my.bitwarden.server.com"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Required Environment Variables for Bitwarden Unified Deployment

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This section details the essential environment variables required for configuring the Bitwarden unified deployment. These variables, such as domain, database provider, and installation IDs, must be set either via a `settings.env` file or `--env` flags to ensure proper server operation and database connectivity.

```APIDOC
BW_DOMAIN:
  Description: Replace bitwarden.yourdomain.com with the domain where Bitwarden will be accessed.
BW_DB_PROVIDER:
  Description: The database provider you will be using for your Bitwarden server. Available options are sqlserver, postgresql, sqlite, or mysql/mariadb.
BW_DB_SERVER:
  Description: The name of the server on which your database is running.
BW_DB_DATABASE:
  Description: The name of your Bitwarden database.
BW_DB_USERNAME:
  Description: The username for accessing the Bitwarden database.
BW_DB_PASSWORD:
  Description: The password for accessing the Bitwarden database.
BW_DB_FILE:
  Description: Only required for sqlite if you would like to specify the path to your database file. If not specified, sqlite will automatically create a vault.db file under the /etc/bitwarden volume.
BW_INSTALLATION_ID:
  Description: A valid installation ID generated from https://bitwarden.com/host/.
BW_INSTALLATION_KEY:
  Description: A valid installation key generated from https://bitwarden.com/host/.
```

--------------------------------

### Create Docker Group

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Ensures the 'docker' group exists on the system. This group is necessary for users to interact with the Docker daemon.

```Bash
sudo groupadd docker
```

--------------------------------

### Apply Bitwarden Environment Variable Changes

Source: https://bitwarden.com/help/cli/install-on-premise-windows

Run the Bitwarden PowerShell script with the `-restart` flag to apply any modifications made to the `global.override.env` file. This ensures that the updated environment variable configurations are loaded and take effect within the Bitwarden instance.

```PowerShell
.\bitwarden.ps1 -restart
```

--------------------------------

### Bitwarden CLI: Get Command Syntax

Source: https://bitwarden.com/help/cli/cli

Defines the general syntax for the `bw get` command, used to retrieve single objects from the vault, such as items, usernames, passwords, or attachments. It requires an ID or a search string.

```Bash
bw get (item|username|password|uri|totp|exposed|attachment|folder|collection|organization|org-collection|template|fingerprint) <id> [options]
```

--------------------------------

### Bitwarden CLI: `bw send get` Command Syntax

Source: https://bitwarden.com/help/cli/send-cli

Shows the basic syntax for the `bw send get` command, used to retrieve a Send by its exact `id` value or a matching string, outputting it as a JSON object.

```Bash
bw send get [options] <id / string>
```

--------------------------------

### Export Identity Certificate to PFX Format

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Converts the generated `identity.key` and `identity.crt` into a PKCS#12 (`.pfx`) file, which is required by the identity container. Replace `IDENTITY_CERT_PASSWORD` with the secure password set in a previous step.

```Bash
openssl pkcs12 -export -out ./identity/identity.pfx -inkey identity.key -in identity.crt -passout pass:IDENTITY_CERT_PASSWORD
```

--------------------------------

### Bitwarden CLI: Get Notes Command Syntax

Source: https://bitwarden.com/help/cli/cli

Defines the syntax for retrieving notes associated with a vault item using `bw get notes`. It accepts an exact item ID or a search string.

```Bash
bw get notes <id>
```

--------------------------------

### Bitwarden Public API Collections Response Example (APIDOC)

Source: https://bitwarden.com/help/cli/public-api

Shows an example JSON response from the Bitwarden Public API's collections endpoint. It includes a list object with data containing event details like object type, ID, and date, along with a continuation token for pagination.

```APIDOC
{
  "object": "list",
  "data": [
    {
      "object": "event",
      "type": 1000,
      "itemId": "string",
      "collectionId": "string",
      "groupId": "string",
      "policyId": "string",
      "memberId": "string",
      "actingUserId": "string",
      "date": "2020-11-04T15:01:21.698Z",
      "device": 0,
      "ipAddress": "xxx.xx.xxx.x"
    }
  ],
  "continuationToken": "string"
}
```

--------------------------------

### Install cert-manager on Kubernetes Cluster

Source: https://bitwarden.com/help/cli/self-host-with-helm

This command installs cert-manager on a Kubernetes cluster, which is essential for automating the issuance and renewal of TLS certificates. It applies the official cert-manager manifest directly from its GitHub release.

```Bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml
```

--------------------------------

### Bitwarden CLI: Get Attachment Command Syntax

Source: https://bitwarden.com/help/cli/cli

Shows the syntax for downloading a file attachment using `bw get attachment`. It requires the filename and the exact item ID to which the attachment belongs.

```Bash
bw get attachment <filename> --itemid <id>
```

--------------------------------

### Create Bitwarden Service User

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Creates a dedicated 'bitwarden' service account on the Linux server to isolate the Bitwarden instance from other applications. This is a recommended best practice for security and organization.

```Bash
sudo adduser bitwarden
```

--------------------------------

### Example Website Icon Request URL

Source: https://bitwarden.com/help/cli/website-icons

Illustrates the format of a request made to the Bitwarden icon server, showing how the hostname of a website is included in the URL. This example highlights the 'leakage' of hostname information during icon retrieval.

```Text
https://icons.bitwarden.net/google.com/icon.png
```

--------------------------------

### Splunk Search All Bitwarden Events

Source: https://bitwarden.com/help/cli/splunk-siem

This example demonstrates a basic Splunk query to retrieve all event logs from the 'bitwarden:events' sourcetype, using a wildcard to include all event types.

```Bash
sourcetype="bitwarden:events" type=*
```

--------------------------------

### Install Python 'requests' module using pip

Source: https://bitwarden.com/help/cli/migration-script

This command uses pip3 to install the 'requests' Python module, which is a required dependency for the Bitwarden migration script. It ensures the script can make necessary HTTP requests to the Bitwarden API.

```Bash
pip3 install requests
```

--------------------------------

### Get Help for Bitwarden Secrets Manager CLI

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command displays the available commands and options for the Bitwarden Secrets Manager CLI, providing self-documentation directly from the command line.

```Bash
bws --help, -h
```

--------------------------------

### Bitwarden SCIM Provisioning Workflow Steps

Source: https://bitwarden.com/help/cli/microsoft-entra-id-scim-integration

Outlines the final steps in the SCIM provisioning process, including initiating the provisioning service and the subsequent user onboarding workflow in Bitwarden.

```APIDOC
Start Provisioning:
- Action: Select the "Start provisioning" button on the enterprise application's Provisioning page.

Finish User Onboarding:
- Action: Instruct users to accept the invitation to join the organization.
- Action: Confirm users to the organization once they have accepted.
- Note: The Invite → Accept → Confirm workflow facilitates the decryption key handshake that allows users to securely access organization vault data.
```

--------------------------------

### Bitwarden CLI: Create a Text Send

Source: https://bitwarden.com/help/cli/send-cli

Demonstrates a typical workflow to create a text Send. It uses `bw send template` to get a template, `jq` to set the name and text content, `bw encode` to encode the JSON, and finally `bw send create` to create the Send.

```Bash
bw send template send.text | jq '.name="My First Send" | .text.text="Secrets I want to share."' | bw encode | bw send create
```

--------------------------------

### Set Okta Provisioning Actions for Bitwarden

Source: https://bitwarden.com/help/cli/okta-scim-integration

Specifies the minimum required provisioning actions to enable in Okta for Bitwarden, ensuring proper user lifecycle management.

```APIDOC
Provisioning Actions - To App screen:
  1. Enable, at a minimum, the following actions:
    - Create Users
    - Deactivate Users
  2. Select "Save" when done.
```

--------------------------------

### Configure Chrome to Force Install Bitwarden Extension on macOS

Source: https://bitwarden.com/help/cli/browserext-deploy

This snippet shows how to add an ExtensionSettings key to the com.Google.Chrome.plist file to force install the Bitwarden browser extension. The nngceckbapebfimnlniiiahkandclblb identifier is for the Bitwarden extension, and the update_url points to the Chrome Web Store.

```XML
<key>ExtensionSettings</key>
<dict>
  <key>nngceckbapebfimnlniiiahkandclblb</key>
  <dict>
    <key>installation_mode</key>
    <string>force_installed</string>
    <key>update_url</key>
    <string>https://clients2.google.com/service/update2/crx</string>
  </dict>
</dict>
```

--------------------------------

### Recreate Bitwarden Docker Compose Containers

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command recreates and starts the services defined in the docker-compose.yml file in detached mode, applying any updates from newly pulled images.

```Bash
docker compose up -d
```

--------------------------------

### Create Domain-Specific SSL Directory

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Creates a new subdirectory within `./bwdata/ssl` named after your Bitwarden instance's domain. This directory will house your trusted SSL certificate and private key for NGINX.

```Bash
mkdir ./ssl/bitwarden.example.com
```

--------------------------------

### Display Example Bitwarden Account Fingerprint Phrase

Source: https://bitwarden.com/help/cli/fingerprint-phrase

This code block shows a typical example of a Bitwarden account's permanent five-word fingerprint phrase. This phrase is used for secure identification during encryption-related operations.

```Bash
alligator-transfer-laziness-macaroni-blue
```

--------------------------------

### Create New Local User for Bitwarden in PowerShell

Source: https://bitwarden.com/help/cli/install-on-premise-windows

This PowerShell command creates a new local user named 'Bitwarden' on the Windows machine. It assigns the previously captured secure password to the user and provides a descriptive note indicating its role as a local administrator for Bitwarden.

```PowerShell
New-LocalUser "Bitwarden" -Password $Password -Description "Bitwarden Local Admin"
```

--------------------------------

### Bitwarden CLI: `bw send create` Command Options

Source: https://bitwarden.com/help/cli/send-cli

Available options for the `bw send create` command, allowing specification of file/text content, visibility, password, and output format.

```APIDOC
Options:
* --file <path>: Specify the file to Send (this can also be specified in encoded JSON).
* --text <text>: Specify the text to Send (this can also be specified in encoded JSON).
* --hidden: Specify that a text Send require recipients to toggle visibility.
* --password <password>: Specify the password needed to access password-protected Sends.
* --fullObject: Output the full Send object as JSON rather than only the Send link (pair this option with the --pretty option for formatted JSON).
```

--------------------------------

### Download Docker Image for Offline Use

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Downloads a specified Docker image from a registry and saves it to a local .img file. This prepares the image for transfer to an offline machine. The example shown is for the mssql image.

```Bash
docker image save -o mssql.img ghcr.io/bitwarden/mssql:latest
```

--------------------------------

### Other Bitwarden Unified Deployment Configuration Variables

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This section provides a list of miscellaneous environment variables in `settings.env` for Bitwarden unified deployments, covering user registration, Have I Been Pwnd API key, admin email addresses, real IP settings, Content Security Policy, and custom database port.

```APIDOC
globalSettings__disableUserRegistration: Enable or disable user account registration capabilities.
globalSettings__hibpApiKey: Enter the API key provided by Have I Been Pwnd.
adminSettings__admins: Enter admin email addresses.
BW_REAL_IPS: Define real IPs in nginx.conf in a comma seperated list. Useful for defining proxy servers that forward the client IP address.
BW_CSP: Content-Security-Policy parameter. Reconfiguring this parameter may break features. By changing this parameter, you become responsible for maintaining this value.
BW_DB_PORT: Specify a custom port for database traffic. If unspecified, the default will depend on your chosen database provider.
```

--------------------------------

### Create Bitwarden Directory in PowerShell

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This PowerShell command creates a new directory named 'Bitwarden' directly under the C: drive. This folder is designated to store Bitwarden server assets and is a prerequisite for configuring Docker Desktop file sharing.

```PowerShell
mkdir Bitwarden
```

--------------------------------

### Install Bitwarden Ansible Secrets Collection

Source: https://bitwarden.com/help/cli/ansible-integration

This command installs the official Bitwarden Secrets Ansible collection, which enables the lookup plugin to fetch secrets from Secrets Manager within your playbooks.

```Bash
ansible-galaxy collection install bitwarden.secrets
```

--------------------------------

### Bitwarden CLI: Import Data Command Syntax

Source: https://bitwarden.com/help/cli/import-from-lastpass

This command is used to import data into your Bitwarden vault via the command-line interface. It requires specifying the import format and the path to the source file.

```Bash
bw import <format> <path>
```

--------------------------------

### Example Bitwarden Directory Connector Cron Job Entry

Source: https://bitwarden.com/help/cli/schedule-directory-sync

This cron job entry schedules the `bwdcSyncService.sh` script to run every Monday at 12:00 PM. The line is commented out as an example of how to format the entry within a crontab file.

```Bash
# 0 12 * * 1 bwdcSyncService.sh
```

--------------------------------

### Example YAML Output for Bitwarden Secret Retrieval

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This is an example of the YAML output format when retrieving a Bitwarden secret. It displays secret details such as ID, organization ID, project ID, key, value, notes, and creation/revision dates.

```YAML
object: secret
id: 2863ced6-eba1-48b4-b5c0-afa30104877a
organizationId: b8824f88-c57c-4a36-8b1a-afa300fe0b52
projectId: 1d0a63e8-3974-4cbd-a7e4-afa30102257e
key: Stripe API Key
value: osiundfpowubefpouwef
note: 'These are notes.'
creationDate: 2023-02-08T15:48:33.470701Z
revisionDate: 2023-02-08T15:48:33.470702Z
```

--------------------------------

### Update Bitwarden Self-Hosted Installation

Source: https://bitwarden.com/help/cli/self-hosting-scim

Executes the Bitwarden update script to pull the latest changes for your self-hosted server. This is a prerequisite before modifying the configuration.

```Bash
./bitwarden.sh update
```

--------------------------------

### Create New Local Bitwarden User in PowerShell

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This command creates a new local user account named "Bitwarden" on the machine. It uses the securely stored password from the $Password variable and assigns a description, establishing a dedicated local administrator account for Bitwarden server operations.

```PowerShell
New-LocalUser "Bitwarden" -Password $Password -Description "Bitwarden Local Admin"
```

--------------------------------

### Enable Browser App Extension Autofill for Bitwarden on iOS

Source: https://bitwarden.com/help/cli/auto-fill-ios

Instructions to activate and test the Bitwarden browser app extension for autofill on iOS, facilitating seamless login credential population within web browsers.

```APIDOC
1. Open your Bitwarden app and tap Settings.
2. Tap Autofill.
3. Tap the App extension option in the Autofill section.
4. Tap the Activate app extension button.
5. From the share menu that slides up, tap Bitwarden.
   A green Extension Activated! message will indicate success.
   Test the app extension:
6. Open your device's web browser and navigate to a website that you aren't currently signed in to.
7. Tap the Share icon.
8. Scroll down and tap the Bitwarden option.
   Note: If you have unlock with biometrics enabled, the first time you tap this option you will be prompted to verify your master password.
9. A Bitwarden screen will slide up on your device and will list matching logins for the website. Tap the item to autofill.
   Tip: If there are no logins listed, it's probably because there isn't a login in your vault with a matching URI.
```

--------------------------------

### Configure Bitwarden Web App for SSO

Source: https://bitwarden.com/help/cli/saml-adfs

Instructions for initial Single Sign-On (SSO) setup within the Bitwarden web application, including creating an SSO identifier and selecting SAML type.

```APIDOC
Bitwarden Web App Configuration:
  1. Log in to the Bitwarden web app.
  2. Open the Admin Console using the product switcher.
  3. Navigate to "Settings" → "Single sign-on".
  4. Create a unique "SSO identifier" for your organization.
  5. Select "SAML" from the "Type" dropdown.
  6. (Optional) Turn off the "Set a unique SP entity ID" option if desired, though it's generally recommended to leave it on.
```

--------------------------------

### Generate Identity Server Certificate Key and CRT with OpenSSL

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This command generates a new RSA 4096-bit key and a self-signed X.509 certificate for the Bitwarden IdentityServer, valid for 10950 days (30 years). It creates `identity.key` and `identity.crt` files.

```Bash
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout identity.key -out identity.crt -subj "/CN=Bitwarden IdentityServer" -days 10950
```

--------------------------------

### Rebuild Bitwarden Self-Hosted Installation

Source: https://bitwarden.com/help/cli/self-hosting-scim

Rebuilds the Bitwarden server containers after modifying the `config.yml` file. This step applies the changes made to the configuration.

```Bash
./bitwarden.sh rebuild
```

--------------------------------

### Load Docker Image from File on Offline Machine

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This command loads a Docker image from a local `.img` file into the Docker daemon. This is used on an offline machine to make the transferred images available.

```Bash
docker image load -i mssql.img
```

--------------------------------

### Bitwarden Passkey Login Mechanics

Source: https://bitwarden.com/help/cli/login-with-passkeys

Details the process of logging into Bitwarden using a passkey, including authentication and vault decryption steps for both encrypted and unencrypted vault setups.

```APIDOC
When a passkey is used to log in and, specifically, to decrypt your vault data:
* Using WebAuthn API public key cryptography, your authentication request is asserted and affirmed.
* Your PRF-encrypted account encryption key and PRF-encrypted private key are sent from the server to your client.
* Using the same salt provided by Bitwarden and the internal secret unique to your passkey, the PRF symmetric key is re-created locally.
* The PRF symmetric key is used to decrypt your PRF-encrypted private key, resulting in your PRF private key.
* The PRF private key is used to decrypt your PRF-encrypted account encryption key, resulting in your account encryption key. Your account encryption key is used to decrypt your vault data.
```

```APIDOC
When a passkey is used to log in, your authentication request is asserted and affirmed using WebAuthn API public key cryptography. You will then be required to decrypt your vault using your master password.
```

--------------------------------

### Retrieve Bitwarden CLI User Fingerprint

Source: https://bitwarden.com/help/cli/cli

The `bw get fingerprint` command retrieves the unique fingerprint phrase associated with a user. Users can specify a `userId` directly or use the `me` shortcut to get their own fingerprint.

```Plain
bw get fingerprint <userId>
```

```Plain
bw get fingerprint me
```

--------------------------------

### Bitwarden CLI: Create Password-Protected File Send

Source: https://bitwarden.com/help/cli/send-cli

Illustrates how to create a password-protected file Send. The example uses `bw send template` for a file Send, `jq` to set the name, type, file name, and password, then `bw encode` and `bw send create` to finalize the creation.

```Bash
bw send template send.file | jq '.name="My File Send" | .type=1 | .file.fileName="paperwork.png" | .password="p@ssw0rd"' | bw encode | bw send create
```

--------------------------------

### Rebuild Bitwarden Self-Hosted Instance

Source: https://bitwarden.com/help/cli/deploy-key-connector

Initiates a rebuild of your self-hosted Bitwarden installation. This step is required after making changes to configuration files (e.g., `config.yml`) to ensure the new settings are compiled and applied to the running services.

```Bash
./bitwarden.sh rebuild
```

--------------------------------

### Specify User Filters: Include/Exclude by Email

Source: https://bitwarden.com/help/cli/okta-directory

These examples demonstrate how to include or exclude specific users from synchronization based on a comma-separated list of their email addresses.

```Bash
include:joe@example.com,bill@example.com,tom@example.com
```

```Bash
exclude:joe@example.com,bill@example.com,tom@example.com
```

--------------------------------

### Get Bitwarden Project Details via CLI

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Use `bws project get` to retrieve details for a specific project from the vault. The machine account must have access to the project to retrieve its information. The command returns the project details as a JSON object.

```Bash
bws project get <PROJECT_ID>
```

```Bash
bws project get e325ea69-a3ab-4dff-836f-b02e013fe530
```

```JSON
{
  "object": "project",
  "id": "e325ea69-a3ab-4dff-836f-b02e013fe530",
  "organizationId": "10e8cbfa-7bd2-4361-bd6f-b02e013f9c41",
  "name": "App 1",
  "creationDate": "2023-06-27T19:24:42.181607Z",
  "revisionDate": "2023-06-27T19:24:42.181607Z"
}
```

--------------------------------

### Configure Bitwarden Unified Deployment with Docker Compose

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This YAML configuration defines a docker-compose setup for Bitwarden, including a Bitwarden service dependent on a MariaDB database. It specifies image versions, environment file, port mappings, and volume mounts for persistent data.

```YAML
version: "3.8"

services:
  bitwarden:
    depends_on:
      - db
    env_file:
      - settings.env
    image: ghcr.io/bitwarden/self-host:beta
    restart: always
    ports:
      - "80:8080"
    volumes:
      - bitwarden:/etc/bitwarden

  db:
    environment:
      MARIADB_USER: "bitwarden"
      MARIADB_PASSWORD: "super_strong_password"
      MARIADB_DATABASE: "bitwarden_vault"
      MARIADB_RANDOM_ROOT_PASSWORD: "true"
    image: mariadb:10
    restart: always
    volumes:
      - data:/var/lib/mysql

volumes:
  bitwarden:
  data:
```

--------------------------------

### Bitwarden CLI: Create Send from Template with jq

Source: https://bitwarden.com/help/cli/send-cli

Demonstrates a common workflow for creating a new Send: piping the output of `bw send template` to `jq` for modification, then encoding with `bw encode`, and finally creating the Send with `bw send create`.

```Bash
bw send template send.text | jq '.name="My First Send" | .text.text="Secrets I want to share."' | bw encode | bw send create
```

--------------------------------

### Update Bitwarden Self-Hosted Instance

Source: https://bitwarden.com/help/cli/deploy-key-connector

Executes the Bitwarden update script to fetch and apply the latest changes to your self-hosted Bitwarden installation. This command is crucial for keeping your instance up-to-date and for applying configuration changes after modifications.

```Bash
./bitwarden.sh update
```

--------------------------------

### Setup Autofill for Bitwarden on Android

Source: https://bitwarden.com/help/cli/getting-started-mobile

Provides step-by-step instructions to enable Bitwarden's autofill service on an Android device, allowing the app to automatically enter login credentials into web browsers and other applications. It covers navigating Bitwarden settings and Android system settings.

```Android
1. Open your Bitwarden Android app and tap the Settings tab.
2. Tap the Autofill option.
3. Toggle the Autofill Services option. You'll be automatically redirected to an Android Settings screen.
4. From the Autofill Services list, tap Bitwarden.

You'll be prompted to confirm you trust Bitwarden. Tapping OK will let Bitwarden read content on the screen to know when to offer autofill. For more information, see Autofill logins on Android.
```

--------------------------------

### Onboarding a Trusted Device: Key Generation and Exchange

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Details the steps involved when a user opts to trust a new device, including the generation of device keys, RSA key pairs, and the encryption and exchange of user and device keys with the server to establish trust.

```APIDOC
1. A new Device Key is generated by the client. This key never leaves the client.
2. A new RSA key pair, called the Device Private Key and Device Public Key, is generated by the client.
3. The user's account encryption key is encrypted with the unencrypted Device Public Key and the resultant value is sent to the server as the Public Key-Encrypted User Key.
4. The Device Public Key is encrypted with the user's account encryption key and the resultant value is sent to the server as the User Key-Encrypted Public Key.
5. The Device Private Key is encrypted with the first Device Key and the resultant value is sent to the server as the Device Key-Encrypted Private Key.

Crucial Data Sent from Server to Client on Login:
- Public Key-Encrypted User Key
- Device Key-Encrypted Private Key

Data Used for Account Encryption Key Rotation:
- User Key-Encrypted Public Key
```

--------------------------------

### Example Bitwarden Event Log Export CSV

Source: https://bitwarden.com/help/cli/event-logs

This snippet shows an example of the CSV format generated when exporting Bitwarden event logs. It includes columns for message, application details, user information, timestamp, IP address, and event type, demonstrating typical audit log entries.

```CSV
message,appIcon,appName,userId,userName,userEmail,date,ip,type
Logged in.,fa-globe,Web Vault - Chrome,1234abcd-56de-78ef-91gh-abcdef123456,Alice,alice@bitwarden.com,2021-06-14T14:22:23.331751Z,111.11.111.111,User_LoggedIn
Invited user zyxw9876.,fa-globe,Unknown,1234abcd-56de-78ef-91gh-abcdef123456,Alice,alice@bitwarden.com,2021-06-14T14:14:44.7566667Z,111.11.111.111,OrganizationUser_Invited
Edited organization settings.,fa-globe,Web Vault - Chrome,9876dcba-65ed-87fe-19hg-654321fedcba,Bob,bob@bitwarden.com,2021-06-07T17:57:08.1866667Z,222.22.222.222,Organization_Updated
```

--------------------------------

### Encrypted Login Item Structure Example

Source: https://bitwarden.com/help/cli/encrypted-export

Demonstrates how the same login item appears after encryption in an encrypted export file, with sensitive fields obfuscated by cryptographic values.

```Bash
{
      ...
      "login": {
        "username": "9.dZwQ+b9Zasp98dnfp[g|dHZZ1p19783bn1KzkEsA=l52bcWB/w9unvCt2zE/kCwdpiubAOf104os}",
        "password": "1o8y3oqsp8n8986HmW7qA=oiCZo872b3dbp0nzT/Pw=|A2lgso87bfDBCys049ano278ebdmTe4:",
        "totp": "2CIUxtpo870B)*^GW2ta/xb0IYyepO(*&G(&BB84LZ5ByZxu0E9hTTs6PHg0=8q5DHEPU&bp9&*bns3EYgETXpiu9898sxO78l"
      },
      ...
}
```

--------------------------------

### Configure YubiKey OTP API for Self-Hosted Bitwarden

Source: https://bitwarden.com/help/cli/setup-two-step-login-yubikey

Organization administrators must configure these environment variables in `global.override.env` to enable calls to the YubiKey OTP API for self-hosted Bitwarden instances. The client ID and key are obtained from Yubico.

```Configuration
| Variable | Description |
| --- | --- |
| globalSettings__yubico__clientId | Replace value with ID received from your Yubico Key. Sign up for Yubico Key here. |
| globalSettings__yubico__key | Input the key value received from Yubico. |
```

--------------------------------

### Bitwarden CLI: Create Attachment Example

Source: https://bitwarden.com/help/cli/cli

Shows how to attach a file to an existing item using `bw create attachment`. This command does not require JSON encoding and uses `--file` and `--itemid` options to specify the file path and target item.

```Bash
bw create attachment --file ./path/to/file --itemid 16b15b89-65b3-4639-ad2a-95052a6d8f66
```

--------------------------------

### Save Docker Image to File for Offline Transfer

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This command saves a specified Docker image (e.g., `ghcr.io/bitwarden/mssql:latest`) to a local `.img` file. This is useful for transferring images to an offline machine.

```Bash
docker image save -o mssql.img ghcr.io/bitwarden/mssql:latest
```

--------------------------------

### Setup Autofill for Bitwarden on iOS

Source: https://bitwarden.com/help/cli/getting-started-mobile

Provides step-by-step instructions to enable Bitwarden's autofill service on an iOS device, allowing the app to automatically enter login credentials into web browsers and other applications. It covers navigating iOS system settings.

```iOS
1. On the iOS home screen, tap the Settings app.
2. From the Settings menu, tap Passwords.
3. Tap Password Options.
4. Tap the AutoFill Passwords toggle. Green indicates that AutoFill is active.
5. From the Use Passwords and Passkeys From: list, select Bitwarden. A check-mark indicates that Bitwarden is selected.

When you create new logins, make sure you enter a website in the URI field to surface them for AutoFill. For more information, see Autofill Logins on iOS.
```

--------------------------------

### New Public API Operation: Get Organization Subscription

Source: https://bitwarden.com/help/cli/releasenotes

A new GET operation has been added to the Bitwarden Public API. This endpoint allows retrieval of organization subscription details, expanding programmatic access to Bitwarden's features.

```APIDOC
GET /public/organization/subscription
```

--------------------------------

### Bitwarden Included Environment Variables

Source: https://bitwarden.com/help/cli/environment-variables

This section lists environment variables that are pre-configured in `global.override.env` for Bitwarden installations. It details their purpose and configuration requirements, including settings for service URIs, database connections, authentication providers, email, and user registration.

```APIDOC
globalSettings__baseServiceUri__vault: string
  Description: Enter the domain of your Bitwarden instance. If not configured, domain will default to localhost. Must not include a trailing slash.
globalSettings__sqlServer__connectionString: string
  Description: Use this field to connect to an external MSSQL database.
globalSettings__oidcIdentityClientKey: string
  Description: A randomly generated OpenID Connect client key. For more information, see OpenID Documentation.
globalSettings__duo__aKey: string
  Description: A randomly generated Duo akey. For more information, see Duo's Documentation.
globalSettings__yubico__clientId: string
  Description: Client ID for YubiCloud Validation Service or self-hosted Yubico Validation Server. If YubiCloud, get your client ID and secret key here. If self-hosted, see optional variable `globalSettings__yubico__validationUrls`.
globalSettings__yubico__key: string
  Description: Secret Key for YubiCloud Validation Service or self-hosted Yubico Validation Server. If YubiCloud, get your client ID and secret key here. If self-hosted, see optional variable `globalSettings__yubico__validationUrls`.
globalSettings__mail__replyToEmail: string
  Description: Email address used for invitations, typically `no_reply@smpt__host`.
globalSettings__mail__smtp__host: string
  Description: Your SMTP server hostname (recommended) or IP address.
globalSettings__mail__smtp__port: number
  Description: The SMTP port used by the SMTP server.
globalSettings__mail__smtp__ssl: boolean
  Description: Whether your SMTP server uses an encryption protocol: `true` = SSL `false` = TLS.
globalSettings__mail__smtp__username: string
  Description: A valid username for the `smtp__host`.
globalSettings__mail__smtp__password: string
  Description: A valid password for the `smtp__host`. Dollar sign `$` characters are not supported in SMTP passwords.
globalSettings__disableUserRegistration: boolean
  Description: Specify `true` to disable new users signing up for an account on this instance via the registration page.
globalSettings__hibpApiKey: string
  Description: Your HaveIBeenPwned (HIBP) API Key, available here. This key allows users to run the Data Breach report and to check their master password for presence in breaches when they create an account.
adminSettings__admins: string
  Description: Email addresses which may access the System Administrator Portal.
```

--------------------------------

### Run Bitwarden Unified Deployment with Docker

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This Docker command initiates the Bitwarden unified deployment in detached mode, naming the container 'bitwarden', mounting a local volume for data persistence, mapping host port 80 to container port 8080, and loading environment variables from `settings.env`. It uses the `ghcr.io/bitwarden/self-host:beta` image.

```Bash
docker run -d --name bitwarden -v /$(pwd)/bwdata/:/etc/bitwarden -p 80:8080  --env-file settings.env ghcr.io/bitwarden/self-host:beta
```

--------------------------------

### Configure Bitwarden Environment Variables

Source: https://bitwarden.com/help/cli/install-on-premise-windows

Edit the `global.override.env` file to set critical environment variables. This includes configuring SMTP mail server settings for email notifications and defining `adminSettings__admins` to provision access to the System Administrator Portal. Placeholder values must be replaced with actual configuration details.

```Configuration
...
globalSettings__mail__smtp__host=<placeholder>
globalSettings__mail__smtp__port=<placeholder>
globalSettings__mail__smtp__ssl=<placeholder>
globalSettings__mail__smtp__username=<placeholder>
globalSettings__mail__smtp__password=<placeholder>
...
adminSettings__admins=
...
```

--------------------------------

### Verify Running Docker Containers

Source: https://bitwarden.com/help/cli/install-on-premise-manual

This command lists all currently running Docker containers, allowing verification that the Bitwarden server containers are active and healthy after startup.

```Bash
docker ps
```

--------------------------------

### Disable Push Relay for Offline/Manual Bitwarden Self-Hosted Installations

Source: https://bitwarden.com/help/cli/configure-push-relay

For offline or manual Bitwarden server installations, disable push relay by adding a blank `globalSettings__pushRelayBaseUri` variable to `global.override.env` and then restarting the server. This effectively prevents the server from connecting to any push relay service.

```Shell
# Open the global override environment file
# Path: ./bwdata/env/global.override.env
# Add the following line to disable push relay (leave the value blank):
globalSettings__pushRelayBaseUri=

# After saving the file, restart Bitwarden to apply changes
# (e.g., ./bitwarden.sh restart or equivalent method for your setup)
```

--------------------------------

### Configure Okta Bookmark App for Bitwarden Web Vault Login

Source: https://bitwarden.com/help/cli/saml-okta

Provides step-by-step instructions for Okta administrators to create a Bookmark App that links directly to the Bitwarden web vault login page, facilitating user access and ensuring the SSO flow is initiated from Bitwarden.

```APIDOC
Okta Bookmark App Configuration Steps:
1. As an admin, navigate to the Applications drop down and select Applications.
2. Click Browse App Catalog.
3. Search for Bookmark App and click Add Integration.
4. Add the following settings to the application:
   a. Give the application a name such as Bitwarden Login.
   b. In the URL field, provide the URL to your Bitwarden client such as https://vault.bitwarden.com/#/login or your-self-hostedURL.com.
5. Select Done and return to the applications dashboard and edit the newly created app.
6. Assign people and groups to the application. You may also assign a logo to the application for end user recognition. The Bitwarden logo can be obtained here: https://github.com/bitwarden/brand/tree/master.
```

--------------------------------

### Retrieve Database Password Secret using Bitwarden Secrets Manager CLI

Source: https://bitwarden.com/help/cli/developer-quick-start

This command retrieves a specific database password secret using its identifier (e.g., `80b55c29-5cc8-42eb-a898-acfd01232bbb`) and stores its value as a temporary environment variable named `SECRET_2`. The `jq` utility is used to extract the 'value' field from the JSON output.

```Bash
export SECRET_2=$(bws secret get 80b55c29-5cc8-42eb-a898-acfd01232bbb | jq '.value')
```

--------------------------------

### Disable Push Relay for Standard Bitwarden Self-Hosted Installations

Source: https://bitwarden.com/help/cli/configure-push-relay

Disable push notifications for standard self-hosted Bitwarden server installations by changing a setting in `config.yml` and then rebuilding the server to apply the change. This prevents automatic mobile app syncing.

```Shell
# Open the Bitwarden configuration file
# Path: ./bwdata/config.yml
# Change the 'push_notifications' attribute from 'true' to 'false':
push_notifications: false

# After saving the file, rebuild Bitwarden to apply changes
./bitwarden.sh rebuild
```

--------------------------------

### Upgrade or Install Bitwarden Secrets Manager Operator Helm Chart

Source: https://bitwarden.com/help/cli/secrets-manager-kubernetes-operator

This command performs an in-place upgrade of the `sm-operator` release or installs it if it doesn't exist (`-i`). It uses the specified `my-values.yaml` file for configuration, creates the `sm-operator-system` namespace if it doesn't already exist, and enables debugging output (`--debug`).

```bash
helm upgrade sm-operator bitwarden/sm-operator -i --debug -n sm-operator-system --create-namespace --values my-values.yaml --devel
```

--------------------------------

### PKCS#11 Key Connector Configuration Parameters Reference

Source: https://bitwarden.com/help/cli/deploy-key-connector

Comprehensive reference for required and optional parameters when configuring Bitwarden Key Connector with a PKCS#11 provider. Details each parameter's purpose, valid values, and usage conditions.

```APIDOC
Required in all circumstances:
- keyConnectorSettings__rsaKey__provider: Must be 'pkcs11'.
- keyConnectorSettings__rsaKey__pkcs11Provider: Must be 'yubihsm' or 'opensc'.
- keyConnectorSettings__rsaKey__pkcs11SlotTokenSerialNumber: Serial number used to identify the token to be used.
- keyConnectorSettings__rsaKey__pkcs11LoginUserType: Can be 'user', 'so', or 'context_specific'.
- keyConnectorSettings__rsaKey__pkcs11LoginPin: PIN code used to access the token.
- keyConnectorSettings__certificate__provider: Can be 'filesystem', 'azurestorage', 'azurekv', or 'vault'.

Required in some circumstances:
- keyConnectorSettings__rsaKey__pkcs11PrivateKeyLabel: (Required if not using '...__pkcsPrivateKeyId=') Label, or "alias", of your private key.
- keyConnectorSettings__rsaKey__pkcs11PrivateKeyId: (Required if not using '...__pkcs11PrivateKeyLabel=') Unique identifier of your private key.
- keyConnectorSettings__certificate__filesystem...: Set both '...__certificate__filesystem...' values if you store your public key on a file system (see Certificates tab).
- keyConnectorSettings__certificate__azure...: Set all '...__certificate__azure...' values if you store your public key in Azure Blob Storage (see Certificates tab).
- keyConnectorSettings__certificate__azureKeyvault...: Set all '...__certificate__azureKeyvault...' values if you store your public key in Azure Key Vault (see Certificates tab).
- keyConnectorSettings__certificate__vault...: Set all '...__certificate__vault...' values if you store your public key in Hashicorp Vault (see Certificates tab).

Optional:
- keyConnectorSettings__rsaKey__pkcs11LibraryPath: Optionally, point Key Connector to a library file, for example '=/etc/bitwarden/libfxpkcs11.so'. Doing so will supersede the value 'keyConnectorSettings__rsaKey__pkcs11Provider='.
```

--------------------------------

### Plaintext Login Item Structure Example

Source: https://bitwarden.com/help/cli/encrypted-export

Illustrates the unencrypted structure of a login item within a Bitwarden vault, showing typical fields like username, password, and TOTP before encryption.

```Bash
{
      ...
      "login": {
        "username": "mylogin",
        "password": "mypassword",
        "totp": "otpauth://totp/my-secret-key"
      },
      ...
}
```

--------------------------------

### Complete GitHub Actions Workflow with Bitwarden Secrets

Source: https://bitwarden.com/help/cli/github-actions-integration

This comprehensive GitHub Actions workflow example demonstrates the full integration of Bitwarden Secrets Manager. It first retrieves a GPG private key and passphrase using `bitwarden/sm-action@v2`, then uses these secrets with `crazy-max/ghaction-import-gpg@v6` to import the GPG key for signing commits. This showcases a practical application of secure secret injection.

```YAML
- name: Get Secrets
        uses: bitwarden/sm-action@v2
        with:
          access_token: ${{ secrets.BW_ACCESS_TOKEN }}
          secrets: |
            fc3a93f4-2a16-445b-b0c4-aeaf0102f0ff > GITHUB_GPG_PRIVATE_KEY
            bdbb16bc-0b9b-472e-99fa-af4101309076 > GITHUB_GPG_PRIVATE_KEY_PASSPHRASE

- name: Import GPG key
        uses: crazy-max/ghaction-import-gpg@v6
        with:
          gpg_private_key: ${{ env.GITHUB_GPG_PRIVATE_KEY }}
          passphrase: ${{ env.GITHUB_GPG_PRIVATE_KEY_PASSPHRASE }}
          git_user_signingkey: true
          git_commit_gpgsign: true
```

--------------------------------

### Get Bitwarden CLI JSON Template

Source: https://bitwarden.com/help/cli/cli

The `bw get template` command returns the expected JSON structure for various Bitwarden vault objects like items, folders, or collections. It is commonly used to pipe the output into `bw create` operations after manipulation with a JSON processor like `jq`.

```Bash
bw get template (item|item.field|item.login|item.login.uri|item.card|item.identity|item.securenote|folder|collection|item-collections|org-collection)
```

```Bash
bw get template folder | jq '.name="My First Folder"' | bw encode | bw create folder
```

```Bash
bw get template item | jq ".name=\"My Login Item\" | .login=$(bw get template item.login | jq '.username=\"jdoe\" | .password=\"myp@ssword123\"')" | bw encode | bw create item
```

--------------------------------

### Add Bitwarden Helm Repository

Source: https://bitwarden.com/help/cli/self-host-with-helm

These commands add the official Bitwarden Helm chart repository to your Helm configuration and then update your local chart repository cache. This step is essential to make Bitwarden charts available for installation.

```Bash
helm repo add bitwarden https://charts.bitwarden.com/
helm repo update
```

--------------------------------

### Specify Bitwarden CLI Profile for Commands

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Use the `--profile` option with `list` or `get` commands to specify which configured profile the Bitwarden CLI should use. This helps manage different sets of configurations or environments.

```Bash
bws secret get 2863ced6-eba1-48b4-b5c0-afa30104877a --profile dev
```

--------------------------------

### Edit Bitwarden Configuration File for SCIM

Source: https://bitwarden.com/help/cli/self-hosting-scim

Opens the `config.yml` file using `nano` to enable SCIM. The `enable_scim` flag must be toggled to `true` within this file.

```Bash
nano bwdata/config.yml
```

--------------------------------

### Switch Bitwarden Accounts During Autofill on iOS

Source: https://bitwarden.com/help/cli/auto-fill-ios

Describes how users logged into multiple Bitwarden accounts on iOS can switch between them directly during the autofill process by tapping the avatar bubble.

```APIDOC
If you are logged in to more than one account, your mobile app will default to trying to autofill credentials from the currently active account. You can switch from one account to another during autofill by tapping the avatar bubble.
```

--------------------------------

### Retrieve Database Username Secret using Bitwarden Secrets Manager CLI

Source: https://bitwarden.com/help/cli/developer-quick-start

This command retrieves a specific database username secret using its identifier (e.g., `fc3a93f4-2a16-445b-b0c4-aeaf0102f0ff`) and stores its value as a temporary environment variable named `SECRET_1`. The `jq` utility is used to extract the 'value' field from the JSON output.

```Bash
export SECRET_1=$(bws secret get fc3a93f4-2a16-445b-b0c4-aeaf0102f0ff | jq '.value')
```

--------------------------------

### Bitwarden Web App SSO Configuration

Source: https://bitwarden.com/help/cli/saml-duo

Steps to initiate the Single Sign-On setup within the Bitwarden web application, including creating a unique SSO identifier and selecting SAML as the authentication type.

```APIDOC
Bitwarden Web App Admin Console:
  - Log in to the Bitwarden web app.
  - Open the Admin Console using the product switcher.
  - Navigate to "Settings" -> "Single sign-on" screen.
  - Create a unique "SSO identifier" for your organization.
  - Select "SAML" from the "Type" dropdown.
  - (Optional) Turn off "Set a unique SP entity ID" (leaving it on is recommended).
```

--------------------------------

### Example Bitwarden Organization Vault CSV Data

Source: https://bitwarden.com/help/cli/condition-bitwarden-import

This example illustrates the structure of a .csv file for importing data into a Bitwarden organization vault. It demonstrates how to use the 'collections' field to assign items to one or more collections. This format is vital for organizing shared credentials and notes within an organization.

```CSV
collections,type,name,notes,fields,reprompt,login_uri,login_username,login_password,login_totp
"Social,Marketing",login,Twitter,,,0,twitter.com,me@example.com,password123,
"Finance",login,My Bank,"Bank PIN is 1234","PIN: 1234",0,https://www.wellsfargo.com/home.jhtml,john.smith,password123456,
"Finance",login,EVGA,,,0,https://www.evga.com/support/login.asp,hello@bitwarden.com,fakepassword,TOTPSEED123
"Finance",note,My Note,"This is a secure note.",,0,,,
```

--------------------------------

### Setup ZSH Shell Completion for Bitwarden CLI

Source: https://bitwarden.com/help/cli/cli

The Bitwarden CLI supports ZSH shell completion to enhance command-line usability. This snippet provides three different methods to set up shell completion, catering to vanilla ZSH, vendor completions, and zinit users.

```Bash
eval "$(bw completion --shell zsh); compdef _bw bw;"
```

```Bash
bw completion --shell zsh | sudo tee /usr/share/zsh/vendor-completions/_bw
```

```Bash
bw completion --shell zsh > ~/.local/share/zsh/completions/_bw
zinit creinstall ~/.local/share/zsh/completions
```

--------------------------------

### Example Bitwarden Individual Vault CSV Data

Source: https://bitwarden.com/help/cli/condition-bitwarden-import

This example demonstrates how to structure data within a .csv file for import into an individual Bitwarden vault. It includes various entry types like logins and secure notes, showing how to populate fields such as URI, username, password, and notes. This format is crucial for successful data migration of personal vault items.

```CSV
folder,favorite,type,name,notes,fields,reprompt,login_uri,login_username,login_password,login_totp
Social,1,login,Twitter,,,0,twitter.com,me@example.com,password123,
,,login,EVGA,,,,https://www.evga.com/support/login.asp,hello@bitwarden.com,fakepassword,TOTPSEED123
,,login,My Bank,Bank PIN is 1234,"PIN: 1234",,https://www.wellsfargo.com/home.jhtml,john.smith,password123456,
,,note,My Note,"This is a secure note.",,,,,
```

--------------------------------

### View Bitwarden Authenticator Export Data in CSV Format

Source: https://bitwarden.com/help/cli/authenticator-import-export

This snippet provides an example of data exported from Bitwarden Authenticator in CSV format. It includes common fields such as "folder", "favorite", "type", "name", "login_uri", "login_username", "login_password", and "login_totp". This format is suitable for direct import into spreadsheet applications or for preparing custom import files.

```csv
folder,favorite,type,name,notes,fields,reprompt,login_uri,login_username,login_password,login_totp
,,login,Amazon,,,0,,alice@bitwarden.com,,otpauth://totp/Amazon:alice@bitwarden.com?secret=IIO5SCP3766LMSAB5HJCQPNDCCNAZ532&issuer=Amazon&algorithm=SHA1&digits=6&period=30
,,login,Apple,,,0,,alice@bitwarden.com,,otpauth://totp/Apple:alice@bitwarden.com?secret=IIO5SCQ3766LMSBB5HJCQPNDCCNAZ532&issuer=Apple&algorithm=SHA1&digits=6&period=30
,,login,Bitwarden,,,0,,alice@bitwarden.com,,otpauth://totp/Bitwarden:alice@bitwarden.com?secret=IIO5SCP3766LMSBB5HJCQPNDCCNAZ532&issuer=Bitwarden&algorithm=SHA1&digits=6&period=30
,,login,Microsoft,,,0,,alice@bitwarden.com,,otpauth://totp/Microsoft:alice@bitwarden.com?secret=IIO5SCP3766LMSBB5HJCHPNDCCNAZ532&issuer=Microsoft&algorithm=SHA1&digits=6&period=30
,,login,Reddit,,,0,,alice@bitwarden.com,,otpauth://totp/Reddit:alice@bitwarden.com?secret=IIO5SCP3766LNSBB5HJCQPNDCCNAZ532&issuer=Reddit&algorithm=SHA1&digits=6&period=30
```

--------------------------------

### Construct Bitwarden SSO Login Redirect URLs

Source: https://bitwarden.com/help/cli/sso-faqs

Provides example URLs for automatically redirecting users to the Bitwarden SSO login screen. These URLs require an organization's SSO identifier and vary based on the Bitwarden instance (US cloud, EU cloud, or self-hosted). Administrators should distribute the appropriate URL to users.

```APIDOC
https://vault.bitwarden.com/#/sso?identifier={your-sso-identifier}
```

```APIDOC
https://vault.bitwarden.eu/#/sso?identifier={your-sso-identifier}
```

```APIDOC
https://your.domain.com/#/sso?identifier={your-sso-identifier}
```

--------------------------------

### Generate SHA-256 Checksum for Bitwarden Packages

Source: https://bitwarden.com/help/cli/security-faqs

This command generates a SHA-256 hash for a downloaded Bitwarden package (desktop, Android, or CLI). Users should compare the output hash with the corresponding checksum file provided by Bitwarden to verify package integrity and authenticity. The command requires `sha256sum` to be installed on the system.

```Bash
sha256sum Bitwarden-2024.8.2-universal.dmg
```

--------------------------------

### Update and Restart Bitwarden Server with Docker Compose

Source: https://bitwarden.com/help/cli/install-on-premise-manual

This command is used to update a manually installed self-hosted Bitwarden server. It first stops and removes the existing containers (`down`), then restarts them in detached mode (`up -d`) with the updated configuration and potentially new images.

```Bash
docker compose -f ./docker/docker-compose.yml down && docker compose -f ./docker/docker-compose.yml up -d
```

--------------------------------

### Bitwarden CLI: Export Individual Vault Data

Source: https://bitwarden.com/help/cli/export-your-data

This command exports an individual Bitwarden vault using the CLI. It demonstrates how to specify an output directory, choose a JSON format, and set a password for encrypted exports. It's recommended to sync the vault with `bw sync` before exporting.

```Bash
bw export --output /users/me/documents/ --format json --password mYP@ssw0rd
```

--------------------------------

### Include or Exclude Groups by Name

Source: https://bitwarden.com/help/cli/okta-directory

Provides examples for including or excluding specific groups from synchronization using comma-separated names. Note that Okta does not support syncing nested groups.

```Bash
include:Group A,Group B
```

```Bash
exclude:Group A,Group B
```

--------------------------------

### Email Template: Appointing an Implementation Champion for Bitwarden

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

This email emphasizes the importance of a designated cybersecurity champion to accelerate password management adoption, detailing their responsibilities like hosting workshops and assisting with client setup.

```Email
Subject: Appoint an implementation champion

Body:

Hi *[name]*,

A designated cybersecurity champion can accelerate password management adoption across your organization. This person will rally feedback, suggestions, and overall excitement for your new tool! By appointing an implementation champion, or even a bench of experts, you can ensure someone is always available to answer questions or provide guidance.

Your implementation champion should be empowered to:

* Host workshops or open office hours to review Bitwarden Learning material with users.
* Help teams set up collections through use of a member role such as manager or the custom role.
* Assist users in downloading Bitwarden clients to all their devices.

An implementation champion can significantly increase user adoption, and will have your organization on the road to password security in no time!
```

--------------------------------

### Example Kubernetes Deployment Consuming Bitwarden Synchronized Secret

Source: https://bitwarden.com/help/cli/secrets-manager-kubernetes-operator

This snippet provides an example of a standard Kubernetes Deployment manifest that consumes secrets synchronized by the Bitwarden Kubernetes Operator. It demonstrates how to reference the generated Kubernetes secret (`bw-sample-secret`) for `imagePullSecrets` and `envFrom`, allowing applications to access the synchronized Bitwarden secrets as environment variables or for image pull authentication.

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
  labels:
    app: my-deployment
spec:
  selector:
    matchLabels:
      app: my-deployment
  template:
    metadata:
      labels:
        app: my-deployment
    spec:
      containers:
      - name: my-deployment
        image: <some-image>
      imagePullSecrets:
      - name: container__registry__secret
      envFrom:
      - secretRef:
          name: bw-sample-secret
```

--------------------------------

### Connect Bitwarden CLI to Self-Hosted Server

Source: https://bitwarden.com/help/cli/change-client-environment

This command logs out the current CLI session and then configures the Bitwarden CLI to connect to a specified self-hosted server URL. Replace `https://your.bw.domain.com` with your actual server address.

```Bash
bw config server https://your.bw.domain.com
```

--------------------------------

### Run Multiple Bitwarden Directory Connector Sync Operations

Source: https://bitwarden.com/help/cli/schedule-directory-sync

This example demonstrates how to run `bwdc sync` for multiple directory instances by setting the `BITWARDENCLI_CONNECTOR_APPDATA_DIR` environment variable for each operation. Each instance must have its own `data.json` file containing its specific directory sync settings.

```Bash
BITWARDENCLI_CONNECTOR_APPDATA_DIR="./instance-1" bwdc sync
BITWARDENCLI_CONNECTOR_APPDATA_DIR="./instance-2" bwdc sync
```

--------------------------------

### Bitwarden CLI: Run Single Command with Injected Secrets

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Execute a single shell command with secrets automatically injected as environment variables. This example shows how to run an npm project.

```Bash
# run an npm project with secrets injected
bws run -- 'npm run start'
```

--------------------------------

### Prompt for Secure Password Input in PowerShell

Source: https://bitwarden.com/help/cli/install-and-deploy-offline-windows

This PowerShell command securely prompts the user to enter a password, storing it as a SecureString object. This method prevents the password from being displayed in plain text or stored insecurely in memory, making it suitable for sensitive operations like creating new user accounts.

```PowerShell
$Password = Read-Host -AsSecureString
```

--------------------------------

### Bitwarden Yubico API (YubiKey) Configuration Variables

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This section lists environment variables in `settings.env` for integrating Yubico API with Bitwarden. It includes variables for the Yubico client ID and key, required for YubiKey functionality.

```APIDOC
globalSettings__yubico__clientId: Replace value with ID received from your Yubico Key.
globalSettings__yubico__key: Input the key value received from Yubico.
```

--------------------------------

### Directory Connector User Sync Filters

Source: https://bitwarden.com/help/cli/onelogin-directory

These Bash examples demonstrate how to specify user inclusion or exclusion filters for Directory Connector sync operations. Filters are defined using comma-separated lists of user email addresses.

```Bash
include:joe@example.com,bill@example.com,tom@example.com
```

```Bash
exclude:joe@example.com,bill@example.com,tom@example.com
```

--------------------------------

### Example Bitwarden Organization Vault CSV Nested Collections

Source: https://bitwarden.com/help/cli/condition-bitwarden-import

This snippet provides an example of how to structure a .csv file to import nested collections into a Bitwarden organization vault. It shows how to define parent and child collections, even if they don't contain items directly. This method ensures the correct hierarchical organization of collections upon import.

```CSV
collections,type,name,notes,fields,reprompt,login_uri,login_username,login_password,login_totp
Parent Collection,,,,,,,,,
Parent Collection/First Child Collection,,,,,,,,,
Parent Collection/First Child Collection/Second Child Collection,login,Shared Credential,,,,https://website.com,username,password,,
```

--------------------------------

### Create ADFS Relying Party Trust for Bitwarden SAML

Source: https://bitwarden.com/help/cli/saml-adfs

Step-by-step guide to create a new Relying Party Trust in AD FS Server Manager for Bitwarden SAML 2.0 integration.

```APIDOC
AD FS Server Manager Configuration:
  Action: Add Relying Party Trust
  Wizard Steps:
    1. On the Welcome screen: Select "Claims Aware".
    2. On the Select Data Source screen: Select "Enter data about the relying party manually".
    3. On the Specify Display Name screen: Enter a Bitwarden-specific display name.
    4. On the Configure URL screen:
         - Select "Enable support for SAML 2.0 WebSSO protocol".
         - In the "Relying party SAML 2.0 SSO service URL" input: Enter the Assertion Consumer Service (ACS) URL (copied from Bitwarden).
    5. On the Choose Access Control Policy screen: Select the policy that meets your security standards.
    6. On the Configure Identifiers screen: Add the SP Entity ID as a relying party trust identifier (copied from Bitwarden).
    7. On the Choose Access Control Policy screen: Select the desired policy (by default, "Permit Everyone").
    8. On the Ready to Add Trust screen: Review your selections.
```

--------------------------------

### Set Log File Size Limit

Source: https://bitwarden.com/help/cli/environment-variables

Specify the size limit in bytes to use for container log files. For example, `1073741824` bytes equals 1 GB.

```APIDOC
globalSettings__logRollBySizeLimit=1073741824
```

--------------------------------

### Check Git Version

Source: https://bitwarden.com/help/cli/ssh-agent

Command to check the installed Git version, a prerequisite for using Bitwarden SSH Agent to sign Git commits.

```Shell
git --version
```

--------------------------------

### Bitwarden Regular Expression Match Detection (Unsafe Example)

Source: https://bitwarden.com/help/cli/uri-match-detection

Illustrates an unsafe use of regular expressions for URI matching, highlighting how a broad regex can lead to unintended autofill matches. Includes a warning about the dangers of incorrect regex usage.

```APIDOC
If the URI ^https://.*google\.com$ uses regular expression match detection:
| URL | Autofill? |
| --- | --- |
| https://google.com |  |
| https://sub.google.com |  |
| https://malicious-site.com?q=google.com |  |
| http://google.com |  |
| https://yahoo.com |  |
```

--------------------------------

### Specify Bitwarden CLI Config File and Profile

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Combine the `--config-file` option with `--profile` when using `list` or `get` commands to specify a profile from a particular configuration file. This is useful for managing multiple configuration files.

```Bash
bws secret get 2863ced6-eba1-48b4-b5c0-afa30104877a --config-file ~/.bws/alt_config --profile alt_dev
```

--------------------------------

### Keycloak Client Creation - General Settings

Source: https://bitwarden.com/help/cli/saml-keycloak

Describes the fields to configure when creating a new client in Keycloak, specifically for general settings related to SAML SSO.

```APIDOC
Field: Client type
  Description: Select SAML.
Field: Client ID
  Description: Set this field to the pre-generated SP Entity ID. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Field: Name
  Description: Enter a name of your choice for the Keycloak client.
```

--------------------------------

### Log in with SSO using Bitwarden CLI

Source: https://bitwarden.com/help/cli/cli

Explains how to log in using SSO, which initiates the authentication flow in your web browser. This method is recommended if your organization requires SSO authentication. An alternative using `--apikey` is also mentioned for organizations with SSO requirements.

```Bash
bw login --sso
```

--------------------------------

### Check OpenSSH Version

Source: https://bitwarden.com/help/cli/ssh-agent

Command to check the installed OpenSSH version, a prerequisite for using Bitwarden SSH Agent to sign Git commits.

```Shell
ssh -V
```

--------------------------------

### Set Permissions for Bitwarden Directory

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Applies restrictive permissions (700) to the '/opt/bitwarden' directory, ensuring that only the owner (bitwarden user) has read, write, and execute access, enhancing security.

```Bash
sudo chmod -R 700 /opt/bitwarden
```

--------------------------------

### Configure Group Filters by Name

Source: https://bitwarden.com/help/cli/microsoft-entra-id

Examples of how to include or exclude groups from a sync based on their group name using comma-separated lists in the Group Filter field.

```Bash
include:Group A,Group B
```

```Bash
exclude:Group A,Group B
```

--------------------------------

### Set Password for Bitwarden User

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Assigns a password to the newly created 'bitwarden' user account. This step secures the service account.

```Bash
sudo passwd bitwarden
```

--------------------------------

### Update Self-Hosted Bitwarden Server

Source: https://bitwarden.com/help/cli/updating-on-premise

Commands to update a standard self-hosted Bitwarden instance. This sequence first updates the `bitwarden.sh` or `bitwarden.ps1` script itself, then proceeds to update the main server components. It is applicable for standard installations on Linux, macOS, and Windows.

```Bash
./bitwarden.sh updateself
./bitwarden.sh update
```

```PowerShell
.\bitwarden.ps1 -updateself
.\bitwarden.ps1 -update
```

--------------------------------

### Bitwarden Helm Chart my-values.yaml Configuration Reference

Source: https://bitwarden.com/help/cli/self-host-with-helm

A comprehensive reference for the essential configuration values within the `my-values.yaml` file, used to customize a Bitwarden Helm chart deployment. This includes settings for general domain, ingress, email, cloud communication, shared storage, secrets, database, and component-specific options.

```APIDOC
general.domain: The domain that will point to your cluster's public IP address.
general.ingress.enabled: Whether to use the nginx ingress controller defined in the chart (see an example using a non-included ingress controller).
general.ingress.className: For example, "nginx" or "azure-application-gateway". Set general.ingress.enabled: false to use other ingress controllers.
general.ingress.annotations: Annotations to add to the ingress controller. If you're using the included nginx controller, defaults are provided that you must uncomment and can customize as needed.
general.ingress.paths: If you're using the default nginx controller, defaults are provided that you can customize as needed.
general.ingress.tls.name: The name of your TLS certificate. We will walk through an example later, so enter it now if you have it or circle back later.
general.ingress.tls.clusterIssuer: The name of your TLS certificate issuer. We will walk through an example later, so enter it now if you have it or circle back later.
general.email.replyToEmail: Email address used for invitations, typically no_reply@smtp_host.
general.email.smtpHost: Your SMTP server hostname or IP address.
general.email.smtpPort: The SMTP port used by the SMTP server.
general.email.smtpSsl: Whether your SMTP server uses an encryption protocol ("true" = SSL, "false" = TLS).
enableCloudCommunication: Set to "true" to allow communication between your server and our cloud system. Doing so enables billing and license sync.
cloudRegion: By default, "US". Set to "EU" if your organization was started via the EU cloud server.
sharedStorageClassName: The name of the shared storage class, which you will need to provide and must support ReadWriteMany (see an example using Azure File Storage) unless it's a single-node cluster.
secrets.secretName: The name of your Kubernetes secret object. You will create this object in the next step, so decide on a name now or circle back to this value.
database.enabled: Whether to use the SQL pod included in the chart. Only set to false if you're using an external SQL server.
component.scim.enabled: The SCIM pod is disabled by default. To enable the SCIM pod, set value = true.
volume.logs.enabled: While not required, we recommend setting to true for troubleshooting purposes.
```

--------------------------------

### Specify User Filters: Concatenate with Okta API Filter

Source: https://bitwarden.com/help/cli/okta-directory

These examples show how to combine email-based user inclusion or exclusion with an Okta API 'filter' parameter using a pipe ('|') for more advanced filtering criteria.

```Bash
include:john@example.com,bill@example.com|profile.firstName eq "John"
```

```Bash
exclude:john@example.com,bill@example.com|profile.firstName eq "John"
```

--------------------------------

### Set SSH_AUTH_SOCK for Snap and Flatpak

Source: https://bitwarden.com/help/cli/ssh-agent

Commands to configure the `SSH_AUTH_SOCK` environment variable specifically for Bitwarden SSH Agent installations via Snap or Flatpak, using their respective socket paths.

```Shell
# Snap
export SSH_AUTH_SOCK=/home/<user>/snap/bitwarden/current/.bitwarden-ssh-agent.sock

# Flatpak
export SSH_AUTH_SOCK=/home/<user>/.var/app/com.bitwarden.desktop/data/.bitwarden-ssh-agent.sock
```

--------------------------------

### Prompt for Secure Password Input in PowerShell

Source: https://bitwarden.com/help/cli/install-on-premise-windows

This PowerShell command prompts the user to enter a password securely. The input is stored as a SecureString object in the $Password variable, preventing it from being displayed directly in the console history or memory.

```PowerShell
$Password = Read-Host -AsSecureString
```

--------------------------------

### Configure User Filters by Email Address

Source: https://bitwarden.com/help/cli/microsoft-entra-id

Examples of how to include or exclude specific users from a sync based on their email address using comma-separated lists in the User Filter field.

```Bash
include:joe@example.com,bill@example.com,tom@example.com
```

```Bash
exclude:jow@example.com,bill@example.com,tom@example.com
```

--------------------------------

### Rebuild and Start Bitwarden Self-Hosted Server

Source: https://bitwarden.com/help/cli/licensing-on-premise

After modifying configuration settings, such as enabling cloud communication, you must rebuild and restart your Bitwarden self-hosted server for the changes to take effect. Use the provided `bitwarden.sh` script for these operations.

```Bash
./bitwarden.sh rebuild
./bitwarden.sh start
```

--------------------------------

### Bitwarden CLI: `bw send create` Command Syntax

Source: https://bitwarden.com/help/cli/send-cli

Shows the basic syntax for the `bw send create` command, which allows creating a Send with advanced configuration by taking encoded JSON as an argument.

```Bash
bw send create [options] <encodedJson>
```

--------------------------------

### Customize Bitwarden TOTP Parameters with otpauth URI

Source: https://bitwarden.com/help/cli/authenticator-keys

This example demonstrates how to construct an `otpauth://totp/` URI to customize TOTP generation parameters in Bitwarden. It allows specifying the cryptographic algorithm (SHA-256), number of digits (8), and rotation period (60 seconds) for a vault item, overriding default settings.

```Bash
otpauth://totp/Test:me?secret=JBSWY3DPEHPK3PXP&algorithm=sha256&digits=8&period=60
```

--------------------------------

### Bitwarden CLI: Get Send Object Template

Source: https://bitwarden.com/help/cli/send-cli

The `template` command outputs the expected JSON format for a Send object. It accepts either `send.text` or `send.file` to specify the type of Send template to generate.

```Bash
bw send template <object>
```

--------------------------------

### Use a Bitwarden CLI Profile for Commands

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Once a profile is created, it can be used with other Bitwarden CLI commands to route requests to the server configured within that profile. This example demonstrates retrieving a secret using the 'dev' profile.

```Bash
bws secret get 2863ced6-eba1-48b4-b5c0-afa30104877a --profile dev
```

--------------------------------

### Configure Bitwarden SMTP Mail Server

Source: https://bitwarden.com/help/cli/hosting-faqs

Instructions to connect a self-hosted Bitwarden instance to an existing SMTP mail server by editing specific environment variables in `./bwdata/env/global.override.env`. This enables features like email notifications.

```Configuration
# In ./bwdata/env/global.override.env, configure the following:
# globalSettings__mail__smtp__host=your.smtp.host
# globalSettings__mail__smtp__port=587
# globalSettings__mail__smtp__ssl=true
# globalSettings__mail__smtp__username=your_smtp_username
# globalSettings__mail__smtp__password=your_smtp_password
# globalSettings__mail__smtp__from=no-reply@yourdomain.com
```

--------------------------------

### Create Firefox Policies Directory on Linux

Source: https://bitwarden.com/help/cli/deploy-clients

This command creates the necessary directory structure for Firefox policies on Linux systems. The `-p` flag ensures that parent directories are created if they don't exist.

```Bash
mkdir -p /etc/firefox/policies
```

--------------------------------

### Extract Bitwarden Docker Stub to bwdata

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Extracts the downloaded `docker-stub-US.zip` file into a new `bwdata` directory. This directory is crucial as it matches the volume mappings expected by the `docker-compose.yml` file.

```Bash
unzip docker-stub-US.zip -d bwdata
```

--------------------------------

### Configure SQL Server Connection String for Integrated Authentication

Source: https://bitwarden.com/help/cli/kerberos-integration

This snippet provides an example SQL connection string for Bitwarden's `globalSettings__sqlServer__connectionString` variable. It configures the connection to an external MSSQL database using integrated Kerberos authentication, requiring updates to the hostname and database name.

```Text
globalSettings__sqlServer__connectionString="Data Source=tcp:example-sql-server.example.domain,1433;Initial Catalog=vault;Persist Security Info=False;Integrated Security=true;Multiple Active Result Sets=False;Connect Timeout=30;Encrypt=True;Trust Server Certificate=True"
```

--------------------------------

### Get last sync timestamp for Bitwarden Directory Connector

Source: https://bitwarden.com/help/cli/directory-sync-cli

The `last-sync` command returns an ISO 8601 timestamp for the most recent sync operation. You must specify whether to query for `users` or `groups`.

```Bash
bwdc last-sync <object>
```

--------------------------------

### Bitwarden CLI: Run Command with Custom Shell

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Override the default shell (`sh` on Linux/macOS, PowerShell on Windows) by using the `--shell` option. This allows commands to be executed with a different installed shell, such as `fish`.

```Bash
bws run --shell fish -- echo “running a command with the Fish shell”
```

--------------------------------

### Bitwarden Unified Deployment Environment Variables

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

Documentation for environment variables used to configure webserver ports and SSL settings for the Bitwarden unified deployment. These variables allow customization of network and security aspects.

```APIDOC
Webserver ports:
  BW_PORT_HTTP:
    Description: Change the port used for HTTP traffic. By default, `8080`.
  BW_PORT_HTTPS:
    Description: Change the port used for HTTPS traffic. By default, `8443`.
SSL:
  BW_ENABLE_SSL:
    Description: Use SSL/TLS. `true`/`false`. Default `false`. SSL is required for Bitwarden to function properly. If you are not using SSL configured in the Bitwarden container you should front Bitwarden with a SSL proxy.
  BW_SSL_CERT:
    Description: The name of your SSL certificate file. The file must be located in the `/etc/bitwarden` directory within the container. Default `ssl.crt`.
  BW_SSL_KEY:
    Description: The name of your SSL key file. The file must be located in the `/etc/bitwarden` directory within the container. Default `ssl.key`.
  BW_ENABLE_SSL_CA:
    Description: Use SSL with certificate authority(CA) backed service. `true`/`false`. Default `false`.
  BW_SSL_CA_CERT:
    Description: The name of your SSL CA certificate. The file must be located in the `/etc/bitwarden` directory within the container. Default `ca.crt`.
  BW_ENABLE_SSL_DH:
    Description: Use SSL with Diffie-Hellman key exchange. `true`/`false`. Default `false`.
  BW_SSL_DH_CERT:
    Description: The name of your Diffie-Hellman parameters file. The file must be located in the `/etc/bitwarden` directory within the container. Default `dh.pem`.
  BW_SSL_PROTOCOLS:
    Description: SSL version used by NGINX. Leave empty for recommended default. [Learn more](https://wiki.mozilla.org/Security/Server_Side_TLS).
  BW_SSL_CIPHERS:
    Description: SSL ciphersuites used by NGINX. Leave empty for recommended default. [Learn more](https://wiki.mozilla.org/Security/Server_Side_TLS).
```

--------------------------------

### Configure All Bitwarden Browser Extension Environment URLs on macOS

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This snippet provides the XML content for a Property List (.plist) file to pre-configure all environment URLs (base, webVault, api, identity, icons, notifications, events) for the Bitwarden browser extension on macOS. This is for unique setups requiring independent service URL configurations.

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>environment</key>
        <dict>
            <key>base</key>
            <string>https://my.bitwarden.server.com</string>
                            <key>webVault</key>
                           <string>https://my.bitwarden.server.com</string>
                           <key>api</key>
                           <string>https://my.bitwarden.server.com></string>
                           <key>identity</key>
                           <string>https://my.bitwarden.server.com</string>
                           <key>icons</key>
                           <string>https://my.bitwarden.server.com</string>
                           <key>notifications</key>
                           <string>https://my.bitwarden.server.com</string>
                           <key>events</key>
                           <string>https://my.bitwarden.server.com</string>
        </dict>
    </dict>
</plist>
```

--------------------------------

### Run a live sync operation with Bitwarden Directory Connector

Source: https://bitwarden.com/help/cli/directory-sync-cli

The `sync` command executes a live synchronization, pushing user and group data to your Bitwarden organization. Newly added users will receive an email invite.

```Bash
bwdc sync
```

--------------------------------

### Set SSH_AUTH_SOCK for Standard Shells

Source: https://bitwarden.com/help/cli/ssh-agent

Command to set the `SSH_AUTH_SOCK` environment variable in `.bashrc` or `.zshrc` for standard Bitwarden SSH Agent installations, pointing to the agent's socket.

```Shell
export SSH_AUTH_SOCK=/home/<user>/.bitwarden-ssh-agent.sock
```

--------------------------------

### Retrieve a specific secret with Bitwarden CLI

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Use `bws secret get` to fetch a secret object by its unique ID. By default, the command returns the secret's details as a JSON object.

```Bash
bws secret get <SECRET_ID>
```

```Bash
bws secret get be8e0ad8-d545-4017-a55a-b02f014d4158
```

```JSON
{
  "object": "secret",
  "id": "be8e0ad8-d545-4017-a55a-b02f014d4158",
  "organizationId": "10e8cbfa-7bd2-4361-bd6f-b02e013f9c41",
  "projectId": "e325ea69-a3ab-4dff-836f-b02e013fe530",
  "key": "SES_KEY",
  "value": "0.982492bc-7f37-4475-9e60",
  "note": "",
  "creationDate": "2023-06-28T20:13:20.643567Z",
  "revisionDate": "2023-06-28T20:13:20.643567Z"
}
```

--------------------------------

### Configure Bitwarden Service Provider for JumpCloud SAML

Source: https://bitwarden.com/help/cli/saml-jumpcloud

This section details the fields required to configure Bitwarden as a Service Provider within the JumpCloud SAML setup. It outlines the purpose and recommended settings for each field, including Name ID Format, Outbound Signing Algorithm, Signing Behavior, Minimum Incoming Signing Algorithm, Want Assertions Signed, and Validate Certificates.

```APIDOC
Service Provider Configuration Fields:
- Name ID Format: If you created a Custom SAML Application, set this to whatever the specified SAMLSubject NameID Format is. Otherwise, leave Unspecified.
- Outbound Signing Algorithm: The algorithm Bitwarden will use to sign SAML requests.
- Signing Behavior: Whether/when SAML requests will be signed. By default, JumpCloud will not require requests to be signed.
- Minimum Incoming Signing Algorithm: If you created a Custom SAML Application, set this to whichever Signature Algorithm you selected. Otherwise, leave as rsa-sha256.
- Want Assertions Signed: If you created a Custom SAML Application, check this box if you set the Sign Assertion option in JumpCloud. Otherwise, leave unchecked.
- Validate Certificates: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured within the Bitwarden login with SSO docker image.
```

--------------------------------

### Autofill with Long-Press on iOS Text Fields

Source: https://bitwarden.com/help/cli/auto-fill-ios

Explains how to use the long-press gesture on any text field in iOS to trigger Bitwarden's autofill functionality, provided keyboard autofill is active.

```APIDOC
To autofill data from Bitwarden by long-pressing any text field, ensure Bitwarden is active as the keyboard auto-fill option.
```

--------------------------------

### Docker Run Command Options for Bitwarden Deployment

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This section explains the key options used with the `docker run` command for the Bitwarden unified deployment. It covers options like `--detach` for background execution, `--name` for container identification, `--volume` for data persistence, `--publish` for port mapping, and `--env-file` for environment variable loading.

```APIDOC
--detach , -d:
  Description: Run the container in the background and print container ID.
--name:
  Description: Provide a name for the container. bitwarden is used in the example.
--volume , -v:
  Description: Bind mount a volume. At a minimum, mount /etc/bitwarden.
--publish , -p:
  Description: Map container ports to the host. The example shows the port 80:8080 mapped. Port 8443 is required when configuring SSL.
--env-file:
  Description: Path of the file to read environment variables from. Alternatively, use the --env flag to declare environment variables inline.
```

--------------------------------

### JSON Schema for Importing Projects and Secrets

Source: https://bitwarden.com/help/cli/import-secrets-data

This JSON schema example shows how to structure an import file when importing both projects and secrets. It includes definitions for two projects with unique IDs and names, and two secrets with unique IDs, keys, values, notes, and empty 'projectIds' arrays.

```JSON
{
  "projects": [
    {
      "id": "00000000-0000-0000-0000-000000000001",
      "name": "New Project"
    },
    {
      "id": "00000000-0000-0000-0000-000000000002",
      "name": "Second New Project"
    }
  ],
  "secrets": [
    {
      "key": "Secret for Import",
      "value": "this-is-my-value",
      "note": "These are some notes.",
      "id": "00000000-0000-0000-0000-000000000003",
      "projectIds": []
    },
    {
      "key": "Second Secret for Import 2",
      "value": "this-is-my-value",
      "note": "These are some notes.",
      "id": "00000000-0000-0000-0000-000000000004",
      "projectIds": []
    }
  ]
}
```

--------------------------------

### User Filter: Sync Users by Organizational Unit Path

Source: https://bitwarden.com/help/cli/workspace-directory

This filter specifies syncing users belonging to a particular organizational unit (OU) by its path. The pipe character `|` indicates a query parameter, and the `orgUnitPath` specifies the OU. For example, `/Engineering` targets the 'Engineering' OU. The root group is represented by `/`.

```Plain
|orgUnitPath=/Engineering
```

--------------------------------

### Configure Firefox Policy for Bitwarden Base URL (Linux/macOS)

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This JSON configuration defines a policies.json file used by Firefox to set the base environment URL for the Bitwarden browser extension. This minimal setup directs the extension to a custom Bitwarden server instance on Linux and macOS.

```JSON
{
 "policies": {
    "3rdparty": {
      "Extensions": {
        "{446900e4-71c2-419f-a6a7-df9c091e268b}": {
          "environment": {
            "base": "https://my.bitwarden.server.com"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Bitwarden Equivalent Domains for Autofill

Source: https://bitwarden.com/help/cli/uri-match-detection

Details how equivalent domains link related sites for easier autofill, allowing a vault item for one domain to be offered for another. Mentions Bitwarden's default list and how to manage them.

```APIDOC
Equivalent domains, which can be set from the Account settings → Domain rules page of the web vault, allow you to link domains for easier autofill. For example, setting turbotax.com and intuit.com as equivalent means that a vault item with turbotax.com saved as a URI will also be offered for auto-fill at intuit.com.

Bitwarden maintains a vetted list of default equivalent domains of major sites, for example apple.com and icloud.com, to improve your autofill experience. You can disable any given equivalence by hovering over it and using the  options menu to select  Exclude.

An equivalent domain will be negated for an item that uses exact match detection. For example, an item with the saved URI apple.com set to Exact will not offer autofill for icloud.com despite that being a default equivalent.
```

--------------------------------

### Create SAML Application in AWS IAM Identity Center

Source: https://bitwarden.com/help/cli/saml-aws

This snippet outlines the process of adding a new SAML 2.0 application within the AWS Console's IAM Identity Center, specifying the application type for setup.

```APIDOC
1. In the AWS Console, navigate to IAM Identity Center.
2. Select Application assignments -> Applications from the navigation.
3. Select the Add application button.
4. On the Select application type screen, select 'I have an application I want to set up' and 'SAML 2.0'.
```

--------------------------------

### Create Microsoft Edge Configuration Plist File on macOS

Source: https://bitwarden.com/help/cli/browserext-deploy

This Bash command creates an initial `com.microsoft.Edge.plist` file on the desktop, setting a default preference. This file will be further modified to configure Edge policies.

```Bash
/usr/bin/defaults write ~/Desktop/com.microsoft.Edge.plist RestoreOnStartup -int 1
```

--------------------------------

### Define cert-manager ClusterIssuer for Let's Encrypt Staging

Source: https://bitwarden.com/help/cli/self-host-with-helm

This YAML configuration defines a ClusterIssuer named 'letsencrypt-staging' for cert-manager. It uses the Let's Encrypt staging ACME server, which is recommended for initial setup and testing to avoid production rate limits. Remember to replace the placeholder email address with a valid one.

```YAML
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: letsencrypt-staging
spec:
  acme:
    server: https://acme-staging-v02.api.letsencrypt.org/directory
    email: me@example.com
    privateKeySecretRef:
      name: tls-secret
    solvers:
      - http01:
          ingress:
            class: nginx #use "azure/application-gateway" for Application Gateway ingress
```

--------------------------------

### Generate Base Bitwarden Helm Chart Configuration File

Source: https://bitwarden.com/help/cli/self-host-with-helm

Use the `helm show values` command to generate a base `my-values.yaml` file from the Bitwarden self-host Helm chart, which can then be customized for your deployment.

```Bash
helm show values bitwarden/self-host > my-values.yaml
```

--------------------------------

### Load Docker Image on Offline Machine

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Loads a Docker image from a local .img file into the Docker daemon on an offline machine. This makes the image available for use by Docker containers. The example shown is for the mssql image.

```Bash
docker image load -i mssql.img
```

--------------------------------

### Splunk Filter Bitwarden Events with Implied AND Operator

Source: https://bitwarden.com/help/cli/splunk-siem

This example illustrates a Splunk query that combines two conditions using the implied AND operator, searching for results containing a specific 'type' and 'actingUserName'.

```Bash
sourcetype="bitwarden:events" type=1000 actingUserName="John Doe"
```

--------------------------------

### Configure Bitwarden Docker for External MSSQL Database

Source: https://bitwarden.com/help/cli/external-db

Provides step-by-step instructions for connecting a self-hosted Bitwarden Docker instance to an external MSSQL database. It covers creating a new database, setting up a dedicated DBO, and modifying the `global.override.env` file with the correct connection string parameters.

```Configuration
1. Create a new MSSQL database.
2. (Recommended) Create a dedicated DBO for your database.
3. In the `global.override.env` file for your server, edit the `globalSettings__sqlServer__connectionString=` value for the following information:
   * Replace "Data Source=tcp:mssql,1433"; with your MSSQL server name, for example "Data Source=protocol:server_url,port".
   * Replace the `vault` in `Initial Catalog=vault`; with your database name.
   * Replace the `sa` in `User ID=sa;` with your DBO User ID.
   * Replace the `<default_pw>` in `Password=<default_pw>;` with your DBO password.
4. Save your changes to `global.override.env`.
5. Start Bitwarden (`./bitwarden.sh start`).
```

--------------------------------

### Configure Firefox Policy for All Bitwarden Environment URLs (Linux/macOS)

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This comprehensive JSON configuration for policies.json specifies all individual environment URLs (webVault, api, identity, icons, notifications, events) for the Bitwarden extension in Firefox. This is required for unique server setups on Linux and macOS where a single base URL is insufficient.

```JSON
{
 "policies": {
    "3rdparty": {
      "Extensions": {
        "{446900e4-71c2-419f-a6a7-df9c091e268b}": {
          "environment": {
            "base": "https://my.bitwarden.server.com",
            "webVault": "https://my.bitwarden.server.com",
            "api": "https://my.bitwarden.server.com",
            "identity": "https://my.bitwarden.server.com",
            "icons": "https://my.bitwarden.server.com",
            "notifications": "https://my.bitwarden.server.com",
            "events": "https://my.bitwarden.server.com"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Bitwarden Self-Hosted Linux Server Migration Commands

Source: https://bitwarden.com/help/cli/migration

A collection of essential shell commands used during the migration of a Bitwarden self-hosted server from one Linux machine to another. These commands facilitate stopping the service, identifying the Bitwarden user ID, rebuilding the server configuration, and starting the service.

```Shell
./bitwarden.sh stop
```

```Shell
id -u bitwarden
```

```Shell
./bitwarden.sh rebuild
```

```Shell
./bitwarden.sh start
```

--------------------------------

### JSON Schema for Importing Secrets Only

Source: https://bitwarden.com/help/cli/import-secrets-data

This JSON schema example demonstrates how to structure an import file when only importing secrets. It requires an empty 'projects' array and defines two secret objects with keys, values, notes, unique IDs, and empty 'projectIds' arrays.

```JSON
{
  "projects": [],
  "secrets": [
    {
      "key": "Secret for Import 1",
      "value": "this-is-my-value",
      "note": "These are some notes.",
      "id": "00000000-0000-0000-0000-000000000001",
      "projectIds": []
    },
    {
      "key": "Secret for Import 2",
      "value": "this-is-my-value",
      "note": "These are some notes.",
      "id": "00000000-0000-0000-0000-000000000002",
      "projectIds": []
    }
  ]
}
```

--------------------------------

### Bitwarden SSL Certificate Configuration Notes

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

Notes on configuring SSL certificates for Bitwarden, including requirements for existing certificates (stored in `/etc/bitwarden`, referenced in `docker-compose.yml`, matching `settings.env` names) and the default behavior of generating a self-signed certificate if none are found.

```APIDOC
If you are using an existing SSL certificate, you will have to enable the appropriate SSL options in `settings.env`. SSL files must be stored in `/etc/bitwarden`, which can be referenced in the the `docker-compose.yml` file. These files must match the names configured in `settings.env`.

The default behavior is to generate a self-signed certificate if SSL is enabled and no existing certificate files are in the expected location (`/etc/bitwarden`).
```

--------------------------------

### Configure Extra CA Certificates for TLS Connections

Source: https://bitwarden.com/help/cli/directory-sync-cli

If encountering an "unable to get local issuer certificate" error, set the `NODE_EXTRA_CA_CERTS` environment variable to the absolute path of your `root.pem` or `certificates.pem` file. This helps resolve TLS connection issues.

```Bash
export NODE_EXTRA_CA_CERTS="absolute/path/to/your/certificates.pem"
```

--------------------------------

### Bitwarden Directory Connector Configuration Options

Source: https://bitwarden.com/help/cli/directory-sync-cli

This section details the available configuration options for the Bitwarden Directory Connector, which can be set using the `config` command. It includes server URLs, directory types, and authentication keys/tokens for various directory services.

```APIDOC
Available Options:
- server <server-url>: URL of your self-hosted installation (e.g. `https://business.bitwarden.com`) or EU server (`https://vault.bitwarden.eu`).
- directory <directory-type>: Type of directory to use. See the following table for enumerated values.
- ldap.password <password>: Password for connection to the LDAP server.
- azure.key <key>: Azure AD secret key.
- gsuite.key <key>: Google Workspace/GSuite private key.
- okta.token <token>: Okta token.
- onelogin.secret <secret>: OneLogin client secret.

directory-type values:
- Active Directory/LDAP: 0
- Azure Active Directory: 1
- Google Workspace/GSuite: 2
- Okta: 3
- OneLogin: 4
```

--------------------------------

### Configure Bitwarden SMTP with Gmail App Passwords

Source: https://bitwarden.com/help/cli/hosting-faqs

Instructions for configuring Bitwarden to use Gmail's SMTP service, specifically addressing the upcoming requirement for app passwords instead of basic authentication. This involves setting specific mail server variables in the `global.override.env` file.

```Bash
globalSettings__mail__replyToEmail=no-reply@your.domain
globalSettings__mail__smtp__host=smtp.gmail.com
globalSettings__mail__smtp__port=587
globalSettings__mail__smtp__ssl=false
globalSettings__mail__smtp__username=<valid-gmail-username>
globalSettings__mail__smtp__password=<valid-app-password>
```

--------------------------------

### Bitwarden CLI: Create Send with Deletion Date (Linux)

Source: https://bitwarden.com/help/cli/send-cli

Example for creating a text Send with an explicit deletion date on Linux. It calculates the deletion date using the `date` command and incorporates it into the `jq` command, highlighting the necessary shell escaping for nested quotes and command substitution.

```Bash
bw send template send.text | jq ".name=\"My Send\" | .text.text=\"Secrets I want to share.\" | .password=\"mypassword\" | .deletionDate=\"$(date +\"%Y-%m-%dT%H:%M:%SZ\" -d \"+14 days\")\"" | bw encode | bw send create
```

--------------------------------

### Set Permissions for Chrome Policy Directories on Linux

Source: https://bitwarden.com/help/cli/browserext-deploy

This Bash command sets read, write, and execute permissions for the owner, and read and execute permissions for group and others, on the `/etc/opt/chrome/policies` directory and its contents. This ensures only administrators can write files in the `/managed` directory.

```Bash
chmod -R 755 /etc/opt/chrome/policies
```

--------------------------------

### Extract Firefox Tarball (Linux)

Source: https://bitwarden.com/help/cli/deactivate-browser-password-managers

This command extracts the contents of the downloaded Firefox tarball (`.tar.bz2` file) into the current directory. This is the first step in manually installing Firefox on a Linux system.

```Shell
tar xjf firefox-*.tar.bz2
```

--------------------------------

### Bitwarden CLI: Create Send with Deletion Date (Windows)

Source: https://bitwarden.com/help/cli/send-cli

Example for creating a text Send with an explicit deletion date on Windows. It calculates the deletion date using PowerShell's `Get-Date` and incorporates it into the `jq` command, highlighting the necessary PowerShell-specific escaping for nested quotes.

```Bash
$delDate = (Get-Date).AddDays(14) | date -UFormat "%Y-%m-%dT%H:%M:%SZ"
bw send template send.text | jq ".name=\`"My Send\`" | .text.text=\`"Secrets I want to share.\`" | .password=\`"password\`" | .deletionDate=\`"$delDate\`"" | bw encode | bw send create
```

--------------------------------

### Verify Running Docker Containers

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Lists all currently running Docker containers. This command is used to verify that the Bitwarden server components are active and healthy after startup.

```Bash
docker ps
```

--------------------------------

### Configure Windows Registry for All Bitwarden Firefox Environment URLs

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This APIDOC-like structure lists additional Value name properties for Registry items that need to be created via Windows Group Policy Manager. These are used to set all specific environment URLs (webVault, api, identity, icons, notifications, events) for the Bitwarden Firefox extension, in addition to the base URL, for unique server setups. Each listed value name requires a separate Registry item creation following the same structure as the base URL configuration.

```APIDOC
Additional Registry Value Names:
  webVault
  api
  identity
  icons
  notifications
  events
```

--------------------------------

### Create Firefox Distribution Policy Directory (Linux)

Source: https://bitwarden.com/help/cli/deactivate-browser-password-managers

This command creates the `distribution` directory within the Firefox installation path. This directory is where the `policies.json` file should be placed for Firefox to apply group policies.

```Shell
mkdir /opt/firefox/distribution
```

--------------------------------

### Set Bitwarden user ownership of directory

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Assigns ownership of the '/opt/bitwarden' directory and its contents to the 'bitwarden' user and group. This aligns the directory's ownership with the dedicated service account.

```Bash
sudo chown -R bitwarden:bitwarden /opt/bitwarden
```

--------------------------------

### Set password for Bitwarden user

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Assigns a password to the newly created 'bitwarden' user. This password will be required for logging in as the bitwarden user.

```Bash
sudo passwd bitwarden
```

--------------------------------

### Configure User Filters by Microsoft Entra ID Group Membership

Source: https://bitwarden.com/help/cli/microsoft-entra-id

Examples of how to include or exclude users from a sync based on their Microsoft Entra ID group membership using `includeGroup` and `excludeGroup` keywords with Group Object IDs.

```Bash
includeGroup:963b5acd-9540-446c-8e99-29d68fcba8eb,9d05a51c-f173-4087-9741-a7543b0fd3bc
```

```Bash
excludeGroup:963b5acd-9540-446c-8e99-29d68fcba8eb,9d05a51c-f173-4087-9741-a7543b0fd3bc
```

--------------------------------

### Bitwarden CLI: Create Send with Deletion Date (macOS)

Source: https://bitwarden.com/help/cli/send-cli

Example for creating a text Send with an explicit deletion date on macOS. It calculates the deletion date using the `date` command and incorporates it into the `jq` command, highlighting the necessary shell escaping for nested quotes and command substitution.

```Bash
bw send template send.text | jq ".name=\"My Send\" | .text.text=\"Secrets I want to share.\" | .password=\"mypassword\" | .deletionDate=\"$(date -uv+14d +\"%Y-%m-%dT%H:%M:%SZ\")\"" | bw encode | bw send create
```

--------------------------------

### Configure Bitwarden Extension Force-Install for Edge via GPO

Source: https://bitwarden.com/help/cli/browserext-deploy

This snippet provides the extension ID and update URL required to silently install the Bitwarden browser extension for Microsoft Edge using Windows Group Policy. This ensures the extension is automatically deployed and updated on managed machines.

```Configuration
jbkfoedolllekgbhcbcoahefnbanhhlh;https://edge.microsoft.com/extensionwebstorebase/v1/crx
```

--------------------------------

### Configure Bitwarden to Validate MSSQL Server Certificate

Source: https://bitwarden.com/help/cli/add-rawmanifest-files

This example demonstrates how to configure Bitwarden to validate your MSSQL database server's certificate by adding a `ConfigMap` with the root CA certificate to the `preInstall` section of `rawManifests`. Remember to also enable `caCertificate.enabled: true` in your `my-values.yaml` file for this configuration to take effect.

```YAML
rawManifests:
  preInstall:
  - kind: ConfigMap
    apiVersion: v1
    metadata:
      name: cacert
    data:
      rootca.crt: |
        -----BEGIN CERTIFICATE-----
         ...
        -----END CERTIFICATE-----
  postInstall:
```

--------------------------------

### Launch Websites from Bitwarden Mobile App

Source: https://bitwarden.com/help/cli/getting-started-mobile

Explains how to directly launch a website from a Bitwarden vault item on a mobile device by using the 'Launch' button, provided the item has a valid URI. This functionality is consistent across Android and iOS.

```Android
You can launch a website directly from Bitwarden by selecting the Launch button in any vault item with a valid URI. If you are unfamiliar with using URIs, see Using URIs.
```

```iOS
You can launch a website directly from Bitwarden by selecting the Launch button in any vault item with a valid URI. If you're unfamiliar with using URIs, see Using URIs.
```

--------------------------------

### Bitwarden CLI: Delete a Send

Source: https://bitwarden.com/help/cli/send-cli

The `delete` command removes a Send owned by the user. It requires the exact ID of the Send as an argument. If the ID is unknown, use `bw send get <search term>` to find it.

```Bash
bw send delete <id>
```

--------------------------------

### Add Bitwarden Secrets Manager Helm Repository

Source: https://bitwarden.com/help/cli/secrets-manager-kubernetes-operator

This command adds the official Bitwarden Secrets Manager Helm chart repository to your local Helm configuration. This step is essential to enable Helm to locate and install Bitwarden charts.

```bash
helm repo add bitwarden https://charts.bitwarden.com/
```

--------------------------------

### Bitwarden Service Enablement Variables

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This section lists environment variables in `settings.env` to enable or disable various Bitwarden services for specific use cases. It includes descriptions, default values, and important warnings for critical services.

```APIDOC
BW_ENABLE_ADMIN: Do not disable this service. Default true.
BW_ENABLE_API: Do not disable this service. Default true.
BW_ENABLE_EVENTS: Enable or disable Bitwarden events logs for teams and enterprise event monitoring. Default false.
BW_ENABLE_ICONS: Enable or disable Bitwarden brand icons that are set with the login item URI's. Default true.
BW_ENABLE_IDENTITY: Do not disable this service. Default true.
BW_ENABLE_NOTIFICATIONS: Enable or disable notification services for receiving push notifications to mobile devices, using login with device, mobile vault sync, and more. Default true.
BW_ENABLE_SCIM: Enable or disable SCIM for Enterprise organizations. Default false.
BW_ENABLE_SSO: Enable or disable SSO services for Enterprise organizations. Default false.
BW_ICONS_PROXY_TO_CLOUD: Enabling this service will proxy icon service requests to operate through cloud services in order to lower system memory load. If choosing to use this setting, BW_ENABLE_ICONS should be set to false in order to reduce container load. Default false.
```

--------------------------------

### Define Azure File StorageClass for Kubernetes

Source: https://bitwarden.com/help/cli/azure-aks-deployment

This illustrative example demonstrates how to define an Azure File StorageClass in Kubernetes for Bitwarden deployment. It uses the `file.csi.azure.com` provisioner and sets specific mount options for file and directory permissions, as well as caching. Users should adjust permissions according to their specific security requirements.

```bash
cat <<EOF | kubectl apply -n bitwarden -f -
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: azure-file
  namespace: bitwarden
provisioner: file.csi.azure.com
allowVolumeExpansion: true
mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=0
  - gid=0
  - mfsymlinks
  - cache=strict
  - actimeo=30
parameters:
  skuName: Standard_LRS
EOF
```

--------------------------------

### Configure Additional Keycloak Client Settings for SAML

Source: https://bitwarden.com/help/cli/saml-keycloak

Describes additional configuration options available on the Keycloak Client Settings tab relevant to SAML integration with Bitwarden.

```APIDOC
Additional Keycloak settings:
  Sign Documents: Specify whether SAML documents should be signed by the Keycloak realm.
  Sign Assertions: Specify whether SAML assertions should be signed by the Keycloak realm.
  Signature Algorithm: If Sign Assertions is enabled, select what algorithm to sign with (sha-256 by default).
  Name ID Format: Select the Name ID Format for Keycloak to use in SAML responses.
```

--------------------------------

### Get path to Bitwarden Directory Connector data file

Source: https://bitwarden.com/help/cli/directory-sync-cli

The `data-file` command returns the absolute path to the `data.json` configuration file used by the Directory Connector CLI. While some settings can be edited directly, sensitive keys must be modified via the `config` command or desktop app.

```Bash
bwdc data-file
```

--------------------------------

### Set sharedStorageClassName in Bitwarden Helm Values

Source: https://bitwarden.com/help/cli/azure-aks-deployment

This snippet shows how to configure the `sharedStorageClassName` value within your `my-values.yaml` file. It must be set to match the name of the StorageClass defined previously, which in this example is `"azure-file"`.

```yaml
sharedStorageClassName: "azure-file"
```

--------------------------------

### Pull Latest Bitwarden Unified Docker Image (Direct Docker)

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command pulls the most recent 'beta' tag of the Bitwarden self-host unified image from the GitHub Container Registry.

```Bash
docker pull ghcr.io/bitwarden/self-host:beta
```

--------------------------------

### View Bitwarden Authenticator Export Data in JSON Format

Source: https://bitwarden.com/help/cli/authenticator-import-export

This snippet displays a sample of data exported from Bitwarden Authenticator in JSON format. It shows the structure of individual login entries, including "id", "name", "type", "favorite", and "login" details with "username" and "totp" URI. This format is useful for programmatic processing or understanding the schema for custom imports.

```json
{
  "encrypted": false,
  "items": [
    {
      "favorite": false,
      "id": "52A4DFB0-F19E-4C9D-82A1-BBEE95BBEF81",
      "login": {
        "totp": "otpauth://totp/Amazon:alice@bitwarden.com?secret=IIO5SCP3766LMSAB5HJCQPNDCCNAZ532&issuer=Amazon&algorithm=SHA1&digits=6&period=30",
        "username": "alice@bitwarden.com"
      },
      "name": "Amazon",
      "type": 1
    },
    {
      "favorite": false,
      "id": "DC81A830-ED98-4F45-9B73-B147E40134AB",
      "login": {
        "totp": "otpauth://totp/Apple:alice@bitwarden.com?secret=IIO5SCQ3766LMSBB5HJCQPNDCCNAZ532&issuer=Apple&algorithm=SHA1&digits=6&period=30",
        "username": "alice@bitwarden.com"
      },
      "name": "Apple",
      "type": 1
    },
    {
      "favorite": false,
      "id": "4EF44090-4B6A-4E98-A94C-CF7B0F2CC35D",
      "login": {
        "totp": "otpauth://totp/Bitwarden:alice@bitwarden.com?secret=IIO5SCP3766LMSBB5HJCQPNDCCNAZ532&issuer=Bitwarden&algorithm=SHA1&digits=6&period=30",
        "username": "alice@bitwarden.com"
      },
      "name": "Bitwarden",
      "type": 1
    },
    {
      "favorite": false,
      "id": "59B09168-502A-4D38-B218-FACF66E6A365",
      "login": {
        "totp": "otpauth://totp/Microsoft:alice@bitwarden.com?secret=IIO5SCP3766LMSBB5HJCHPNDCCNAZ532&issuer=Microsoft&algorithm=SHA1&digits=6&period=30",
        "username": "alice@bitwarden.com"
      },
      "name": "Microsoft",
      "type": 1
    },
    {
      "favorite": false,
      "id": "789F095B-95B2-4816-A5F7-01095116C10E",
      "login": {
        "totp": "otpauth://totp/Reddit:alice@bitwarden.com?secret=IIO5SCP3766LNSBB5HJCQPNDCCNAZ532&issuer=Reddit&algorithm=SHA1&digits=6&period=30",
        "username": "alice@bitwarden.com"
      },
      "name": "Reddit",
      "type": 1
    }
  ]
}
```

--------------------------------

### Configure Basic SAML Fields for Bitwarden Azure SSO

Source: https://bitwarden.com/help/cli/saml-microsoft-entra-id

Details the essential SAML fields (Identifier, Reply URL, Sign on URL) required for integrating Bitwarden with Azure for single sign-on, including where to find pre-generated values and examples for cloud/self-hosted instances.

```APIDOC
Identifier (Entity ID):
  Description: Set this field to the pre-generated SP Entity ID. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Reply URL (Assertion Consumer Service URL):
  Description: Set this field to the pre-generated Assertion Consumer Service (ACS) URL. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Sign on URL:
  Description: Set this field to the login URL from which users will access Bitwarden. For cloud-hosted customers, this is https://vault.bitwarden.com/#/sso or https://vault.bitwarden.eu/#/sso. For self-hosted instances, this is determined by you configured server URL, for example https://your-domain.com/#/sso.
```

--------------------------------

### JSON Schema for Associating Secrets with New Projects

Source: https://bitwarden.com/help/cli/import-secrets-data

This JSON schema example illustrates how to associate a secret with a newly imported project using the 'projectIds' attribute. It defines one project and one secret, where the secret's 'projectIds' array references the ID of the new project.

```JSON
{
  "projects": [
    {
      "id": "00000000-0000-0000-0000-000000000001",
      "name": "New Project"
    }
  ],
  "secrets": [
    {
      "key": "New Secret",
      "value": "this-is-my-value",
      "note": "This secret will go in the new project.",
      "id": "00000000-0000-0000-0000-000000000003",
      "projectIds": [
        "00000000-0000-0000-0000-000000000001"
      ]
    }
  ]
}
```

--------------------------------

### Minimum Required JSON Structure for Bitwarden Import

Source: https://bitwarden.com/help/cli/condition-bitwarden-import

This JSON example demonstrates the most basic structure for an `items` array, containing different Bitwarden item types (Login, Secure Note, Card, Identity). Each item includes its `type`, `name`, and an empty object for its specific data type, which is the minimum required for the Bitwarden importer.

```JSON
{
  "items": [
    {
    "type": 1,
    "name": "Login Item's Name",
    "login": {}
  },
  {
    "type": 2,
    "name": "Secure Note Item's Name",
    "secureNote": {}
  },
  {
    "type": 3,
    "name": "Card Item's Name",
    "card": {}
  },
  {
    "type": 4,
    "name": "Identity Item's Name",
    "identity": {}
  }
  ]
}
```

--------------------------------

### Create Directories for Chrome Policies on Linux

Source: https://bitwarden.com/help/cli/browserext-deploy

These Bash commands create the necessary directory structure (`/etc/opt/chrome/policies` and `/etc/opt/chrome/policies/managed`) on Linux for storing Google Chrome managed preferences files.

```Bash
mkdir /etc/opt/chrome/policies
mkdir /etc/opt/chrome/policies/managed
```

--------------------------------

### Example Comma-Separated Blocked URIs for Android Autofill

Source: https://bitwarden.com/help/cli/blocking-uris

This code snippet illustrates the required format for entering multiple URIs to block autofill within the Bitwarden Android app. URIs must be provided as a single, comma-separated string, including both web addresses and Android application URIs.

```Bash
https://instagram.com,androidapp://com.instagram.android,https://facebook.com
```

--------------------------------

### Configure Optional Bitwarden Browser Extension Service URLs on Windows

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This snippet lists additional optional value names for Registry Items that can be created to configure individual service URLs (webVault, api, identity, icons, notifications, events) for the Bitwarden browser extension on Windows, for setups requiring independent service configurations.

```Windows
Value names for individual services:
  webVault
  api
  identity
  icons
  notifications
  events
```

--------------------------------

### Configure SSL Certificate Paths in config.yml

Source: https://bitwarden.com/help/cli/certificates

Shows the configuration parameters in `config.yml` for specifying the paths to the SSL server certificate, private key, and CA certificate files.

```Bash
ssl_certificate_path: <path>
ssl_key_path: <path>
ssl_ca_path: <path>
```

--------------------------------

### Get Chrome Extension ID and Update URL for Intune Deployment

Source: https://bitwarden.com/help/cli/deploy-browser-extensions-with-intune

Provides the necessary extension ID and update URL for deploying the Bitwarden Password Manager browser extension to Chrome using Microsoft Intune. These values are crucial for configuring the Intune policy.

```APIDOC
Extension ID: nngceckbapebfimnlniiiahkandclblb
Update URL: https://clients2.google.com/service/update2/crx
```

--------------------------------

### Bitwarden Desktop App Win32 Detection Rules for Intune

Source: https://bitwarden.com/help/cli/deploy-desktop-apps-with-intune

Defines the file-based detection rules for the Bitwarden desktop application in Microsoft Intune, ensuring the application's presence is correctly identified on endpoints after Win32 deployment.

```Configuration
Rule type: File
Path: C:\Program Files\Bitwarden
File or folder: Bitwarden.exe
Detection method: File or folder exists
Associated with a 32-bit app on 64-bit clients: No
```

--------------------------------

### Verify Running Docker Containers

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command lists all currently running Docker containers, allowing verification of their status and port mappings.

```Bash
docker ps
```

--------------------------------

### Test Bitwarden Directory Connector sync operations

Source: https://bitwarden.com/help/cli/directory-sync-cli

The `test` command queries your directory and simulates a sync operation, printing a JSON formatted array of groups and users that would be synced. Use the `--last` option to test only changes since the last successful sync.

```Bash
bwdc test
```

```Bash
bwdc test --last
```

--------------------------------

### Configure Group Filters by Microsoft Entra ID Administrative Unit

Source: https://bitwarden.com/help/cli/microsoft-entra-id

Examples of how to include or exclude groups from a sync based on their tagged Microsoft Entra ID Administrative Units using `includeadministrativeunit` and `excludeadministrativeunit` keywords with the Administrative Unit's Object ID.

```Bash
includeadministrativeunit:7ckcq6e5-d733-4b96-be17-5bad81fe679d
```

```Bash
excludeadministrativeunit:7ckcq6e5-d733-4b96-be17-5bad81fe679d
```

--------------------------------

### Bitwarden Browser Extension Base URL Configuration (Linux Chrome/Chromium)

Source: https://bitwarden.com/help/cli/deploy-clients

JSON configuration for `bitwarden.json` to set the primary base URL for the Bitwarden browser extension. This file is placed in the browser's managed policies directory (`/etc/opt/chrome/policies/managed/` or `/etc/opt/chromium/policies/managed/`) on Linux to pre-configure the server for users. The extension ID may vary based on installation method.

```JSON
{
  "3rdparty": {
  "extensions": {
  "nngceckbapebfimnlniiiahkandclblb": {
      "environment": {
        "base": "https://my.bitwarden.server.com"
        }
      }
    }
  }
}
```

--------------------------------

### Bitwarden CLI: Shortcut to Create File Send

Source: https://bitwarden.com/help/cli/send-cli

Create a file Send by using the `-f` option followed by the path to the desired file. The command will upload the file and output the corresponding Send link.

```Bash
bw send -f <path/to/file.ext>
```

--------------------------------

### Enable Biometric Unlock for Bitwarden on Android

Source: https://bitwarden.com/help/cli/getting-started-mobile

Details the process of setting up fingerprint or face unlock for the Bitwarden vault on Android, requiring prior biometric setup on the device itself. It outlines steps within the Bitwarden app's security settings.

```Android
1. In Bitwarden, tap the Settings tab located at the bottom of your screen.
2. Tap Account security.
3. Tap Unlock with biometrics.
4. You will be asked to verify with your fingerprint or face depending on your selection.

Once enabled, you will be able to open Bitwarden or autofill logins using just your biometric method of choice.
```

--------------------------------

### Configure Azure Enterprise Application for Bitwarden SSO Redirection

Source: https://bitwarden.com/help/cli/saml-azure

These steps guide administrators through setting up a new Azure Enterprise Application to redirect users directly to the Bitwarden SSO login page, which is necessary because Bitwarden does not support unsolicited responses (IdP-initiated login).

```APIDOC
Azure Enterprise Application Setup for Bitwarden SSO Redirection:
1. Disable the existing Bitwarden button in the All Applications page:
   - Navigate to the current Bitwarden enterprise Application.
   - Select Properties.
   - Set the Visible to users option to No.
2. Create a new app registration:
   - Navigate to Enterprise applications.
   - Select New application.
3. Select Create your own application.
4. Provide a name for the application (e.g., Bitwarden), then select Integrate any other application you don't find in the gallery (Non-gallery). Once finished, select Create.
5. Once the app has been created, navigate to Single sign-on located on the navigation menu. Select Linked.
6. Add the following settings to the application:
   - Set the Sign on URL to your Bitwarden client login page, such as https://vault.bitwarden.com/#/sso. Then, select Save.
   - You may change the logo for end-user recognition in Properties. You can retrieve the Bitwarden logo here (https://github.com/bitwarden/brand).
```

--------------------------------

### Configure Bitwarden Pod Service Account in my-values.yaml

Source: https://bitwarden.com/help/cli/kubernetes-service-accounts

This YAML snippet demonstrates how to configure a specific service account, `bitwarden-sa`, for the `admin` component's pod within the `my-values.yaml` file. This allows for applying specific security contexts to the pod. The example shows the structure for `podServiceAccount` and other related settings like `image` and `resources`. Other eligible pods for service account designation include `component.api.podServiceAccount`, `component.attachments.podServiceAccount`, `component.events.podServiceAccount`, `component.icons.podServiceAccount`, `component.identity.podServiceAccount`, `component.notifications.podServiceAccount`, `component.scim.podServiceAccount`, `component.sso.podServiceAccount`, `component.web.podServiceAccount`, and `database.podServiceAccount`.

```YAML
component:
  # The Admin component
  admin:
    # Additional deployment labels
    labels: {}
    # Image name, tag, and pull policy
    image:
      name: ghcr.io/bitwarden/admin
    resources:
      requests:
        memory: "64Mi"
        cpu: "50m"
      limits:
        memory: "128Mi"
        cpu: "100m"
    securityContext:
    podServiceAccount: bitwarden-sa
```

--------------------------------

### Bitwarden CLI: Run Multiple Commands with Injected Secrets

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Execute multiple shell commands sequentially by wrapping them in single quotes. This ensures that special characters are properly interpreted by the shell after the `bws run` command processes the entire string. Examples include managing a Docker container stack and echoing a secret's value.

```Bash
# start a container stack, execute a script, and tear down the container stack
bws run -- 'docker compose up -d && ./second-command.sh; docker compose down'
```

```Bash
# echo a secret's value by name
bws run -- 'echo "$secret_name"'
```

--------------------------------

### Verify Running Docker Compose Containers

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command lists the status of services defined in the docker-compose.yml file, allowing verification that all components are running correctly.

```Bash
docker compose ps
```

--------------------------------

### Configure Bitwarden Browser Extension Base Server URL (Linux Chrome/Chromium)

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This JSON configuration file sets the base server URL for the Bitwarden browser extension on Linux systems using Chrome or Chromium. It is placed in the browser's managed policies directory to centrally configure the extension before deployment. The extension ID (nngceckbapebfimnlniiiahkandclblb) is a placeholder and will vary depending on your installation method, which can be found in your browser's extension menu.

```JSON
{
  "3rdparty": {
  "extensions": {
  "nngceckbapebfimnlniiiahkandclblb": {
      "environment": {
        "base": "https://my.bitwarden.server.com"
        }
      }
    }
  }
}
```

--------------------------------

### Get Edge Extension ID and Update URL for Intune Deployment

Source: https://bitwarden.com/help/cli/deploy-browser-extensions-with-intune

Provides the necessary extension ID and update URL for deploying the Bitwarden Password Manager browser extension to Microsoft Edge using Microsoft Intune. These values are crucial for configuring the Intune policy.

```APIDOC
Extension ID: jbkfoedolllekgbhcbcoahefnbanhhlh
Update URL: https://edge.microsoft.com/extensionwebstorebase/v1/crx
```

--------------------------------

### Enable Bitwarden Desktop App Logging

Source: https://bitwarden.com/help/cli/product-faqs

Enable logging for the Bitwarden desktop application to troubleshoot issues. Logs can be printed to the console via an environment variable or written to a file using command-line switches for Windows and macOS.

```Shell
ELECTRON_ENABLE_LOGGING=true
```

```Batch
Bitwarden.exe --enable-logging=file --log-file=bitwarden.log
```

```Bash
./Bitwarden.app/Contents/MacOS/Bitwarden --enable-logging=file --log-file=bitwarden.log
```

--------------------------------

### Bitwarden CLI: Edit an Existing Send

Source: https://bitwarden.com/help/cli/send-cli

Demonstrates a typical workflow to edit an existing Send. It uses `bw send get` to retrieve the Send, `jq` to modify its properties (e.g., name, password), `bw encode` to encode the manipulated JSON, and `bw send edit` to apply the changes.

```Bash
bw send get <id> | jq '.name="New Name" | .password=null' | bw encode | bw send edit
```

--------------------------------

### Search Bitwarden Vault by Specific Fields

Source: https://bitwarden.com/help/cli/searching-vault

Demonstrates how to narrow down search results by targeting specific fields within vault items, such as username, item name, or custom text fields. Queries start with the 'greater than' (>) character followed by the field name and a colon, then the search term.

```Bitwarden
>login.username:jsmith
```

```Bitwarden
>name:Turbo Tax
```

```Bitwarden
>fields:Security Question
```

--------------------------------

### Email Template: Communicating Your Bitwarden Rollout Plan

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

This email advises communicating the Bitwarden implementation plan in advance to end-users, outlining expectations, specific action items, and due dates for a smooth rollout.

```Email
Subject: Communicate your rollout plan

Body:

Hi *[name]*,

Put end-users at ease by communicating the implementation plan for your new password manager far in advance.

* Let employees know exactly what to expect.
* Communicate specific action items they will need to complete, and the due data. This will help ensure a smooth rollout for your employees.

Here's a sample implementation plan you can use as a guide - just download them and customize them to work for your organization.
```

--------------------------------

### Set permissions for Bitwarden directory

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Configures restrictive permissions (read, write, execute for owner only) for the '/opt/bitwarden' directory. This ensures only the owner can access or modify its contents.

```Bash
sudo chmod -R 700 /opt/bitwarden
```

--------------------------------

### Create Domain-Specific SSL Directory

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Creates a new subdirectory within `./bwdata/ssl` named after your Bitwarden instance's domain (e.g., `bitwarden.example.com`). This directory serves as the designated location for your trusted SSL certificate and private key, which are mapped to the NGINX container.

```Bash
mkdir ./ssl/bitwarden.example.com
```

--------------------------------

### Configure uMatrix Rule for Bitwarden API Access

Source: https://bitwarden.com/help/cli/blocker-access-rule

This uMatrix rule is required to allow the Bitwarden Firefox extension to communicate with Bitwarden API servers. The UUID (e.g., `dc8ef5f6-eb0d-4c87-9e9f-0cf803f619e8`) in the rule is unique to your Bitwarden extension installation and must be located using Firefox's `about:debugging#/runtime/this-firefox` page.

```Bash
dc8ef5f6-eb0d-4c87-9e9f-0cf803f619e8.moz-extension-scheme bitwarden.com xhr allow
```

--------------------------------

### Email Template: Add Passwords and Usernames to Bitwarden (2/5)

Source: https://bitwarden.com/help/cli/end-user-onboarding-emails

This email instructs users on how to add passwords and usernames to their Bitwarden vault. It suggests importing data from other sources or directly adding items into the vault, aiming to simplify the migration process.

```Email
Subject: Add passwords and usernames to Bitwarden (2/5)

Body:
Hi there,

Do you have passwords saved in a browser, like Chrome? Or are you coming to Bitwarden from another password manager? You can [import logins directly to Bitwarden](/help/import-data/) to avoid copy-and-pasting.

Another way is to directly [add items into your vault](/help/getting-started-webvault/#first-steps).

Add an item

The rest of your onboarding checklist:

*  [Download the browser extension](/download/#downloads-web-browser)
* [**Add logins and passwords to your account**](/help/getting-started-webvault/#add-a-login)
* [Learn how to autofill](/help/auto-fill-browser/)
* [Learn how to share items with collections](/learning/individual-and-organizational-vaults/)

Stay secure,

Team Bitwarden
```

--------------------------------

### Configure Bitwarden SSH Agent Socket on macOS (App Store)

Source: https://bitwarden.com/help/cli/ssh-agent

This snippet configures the SSH_AUTH_SOCK environment variable to direct SSH client communication to the Bitwarden SSH Agent for macOS installations obtained from the App Store. Replace <user> with your actual username.

```Plain
export SSH_AUTH_SOCK=/Users/<user>/Library/Containers/com.bitwarden.desktop/Data/.bitwarden-ssh-agent.sock
```

--------------------------------

### User Filter: Exclude Specific User from OU Sync with Attributes

Source: https://bitwarden.com/help/cli/workspace-directory

This filter demonstrates how to exclude a specific user by email while syncing users from an organizational unit (OU) filtered by an attribute. The `exclude:` filter must precede any query declaration (`|`). For example, `bill@example.com` is excluded from the `/Engineering` OU sync where users have `orgTitle:Manager`.

```Bash
exclude:bill@example.com|orgUnitPath=/Engineering orgTitle:Manager
```

--------------------------------

### Bitwarden CLI: `bw send` Command Options Reference

Source: https://bitwarden.com/help/cli/send-cli

Detailed reference for the command-line options available with the `bw send` command, allowing users to customize Send properties such as name, deletion date, access count, visibility, notes, and output format.

```APIDOC
bw send Options:
  -n <name> | --name <name>:
    Description: Specify a name for the Send. If none is specified, name will default to the id for text Sends and file name for file Sends. For multi-word names, use quotations "<name>".
  -d <days> | --deleteInDays <days>:
    Description: Specify a deletion date for the Send (defaults to seven days if unspecified).
  --maxAccessCount | -a:
    Description: Specify the maximum access count for the Send.
  --hidden:
    Description: Specify that a text Send require recipients to toggle visibility.
  --notes <notes>:
    Description: Add private notes to the Send. For multi-word notes, use quotations "<notes>".
  --fullObject:
    Description: Output the full Send object as JSON rather than only the Send link (pair this option with the --pretty option for formatted JSON).
```

--------------------------------

### Bitwarden CLI: Export Organization Vault Data

Source: https://bitwarden.com/help/cli/export-your-data

This command exports an organization's vault data via the Bitwarden CLI. It requires an organization ID and allows specifying an output directory, JSON format, and a session key. Users can find their organization ID using `bw list organizations`. It's recommended to sync the vault with `bw sync` before exporting.

```Bash
bw export my-master-password --organizationid 7063feab-4b10-472e-b64c-785e2b870b92 --output /users/me/documents/ --format json --session my-session-key
```

--------------------------------

### Configure Traefik IngressRoute and Middleware for Bitwarden Self-Host

Source: https://bitwarden.com/help/cli/add-rawmanifest-files

This YAML configuration defines a Traefik Middleware to strip prefixes for several Bitwarden service paths (e.g., /api, /attachments) and an IngressRoute to direct traffic to different Bitwarden services based on host and path. It includes specific rules for services like web, API, attachments, icons, notifications, events, and SCIM, noting limitations for path stripping on SSO, identity, and admin paths. This setup requires disabling the default ingress controller.

```YAML
rawManifests:
  preInstall: []
  postInstall:
  - apiVersion: traefik.containo.us/v1alpha1
    kind: Middleware
    metadata:
      name: "bitwarden-self-host-middleware-stripprefix"
    spec:
      stripPrefix:
        prefixes:
          - /api
          - /attachments
          - /icons
          - /notifications
          - /events
          - /scim
          ##### NOTE:  Admin, Identity, and SSO will not function correctly with path strip middleware
  - apiVersion: traefik.containo.us/v1alpha1
    kind: IngressRoute
    metadata:
      name: "bitwarden-self-host-ingress"
    spec:
      entryPoints:
        - websecure
      routes:
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/`)
          services:
            - kind: Service
              name: bitwarden-self-host-web
              passHostHeader: true
              port: 5000
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/api/`)
          services:
            - kind: Service
              name: bitwarden-self-host-api
              port: 5000
          middlewares:
            - name: "bitwarden-self-host-middleware-stripprefix"
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/attachments/`)
          services:
            - kind: Service
              name: bitwarden-self-host-attachments
              port: 5000
          middlewares:
            - name: "bitwarden-self-host-middleware-stripprefix"
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/icons/`)
          services:
            - kind: Service
              name: bitwarden-self-host-icons
              port: 5000
          middlewares:
            - name: "bitwarden-self-host-middleware-stripprefix"
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/notifications/`)
          services:
            - kind: Service
              name: bitwarden-self-host-notifications
              port: 5000
          middlewares:
            - name: "bitwarden-self-host-middleware-stripprefix"
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/events/`)
          services:
            - kind: Service
              name: bitwarden-self-host-events
              port: 5000
          middlewares:
            - name: "bitwarden-self-host-middleware-stripprefix"
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/scim/`)
          services:
            - kind: Service
              name: bitwarden-self-host-scim
              port: 5000
          middlewares:
            - name: "bitwarden-self-host-middleware-stripprefix"
        ##### NOTE:  SSO will not function correctly with path strip middleware
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/sso/`)
          services:
            - kind: Service
              name: bitwarden-self-host-sso
              port: 5000
        ##### NOTE:  Identity will not function correctly with path strip middleware
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/identity/`)
          services:
            - kind: Service
              name: bitwarden-self-host-identity
              port: 5000
        ##### NOTE:  Admin will not function correctly with path strip middleware
        - kind: Rule
          match: Host(`REPLACEME.COM`) && PathPrefix(`/admin`)
          services:
            - kind: Service
              name: bitwarden-self-host-admin
              port: 5000
      tls:
        certResolver: letsencrypt
```

--------------------------------

### Utilize Retrieved Secrets in GitHub Actions

Source: https://bitwarden.com/help/cli/github-actions-integration

This example shows how to reference the secrets retrieved by the `bitwarden/sm-action` in subsequent steps of your GitHub Actions workflow. The secrets are injected as masked environment variables, accessible using the `$` prefix (e.g., `$SECRET_NAME_1`). This allows secure use of sensitive data in commands or other actions.

```YAML
- name: Use Secret
  run: SQLCMD -S MYSQLSERVER -U "$SECRET_NAME_1" -P "$SECRET_NAME_2"
```

--------------------------------

### Configure Bitwarden SSH Agent Socket on macOS (.dmg)

Source: https://bitwarden.com/help/cli/ssh-agent

This snippet provides two methods to configure the SSH_AUTH_SOCK environment variable for macOS installations from the .dmg file. The first uses 'export' for the current session, and the second uses 'launchctl' for a more persistent setting. Remember to replace <user> with your username and restart the terminal if using 'launchctl'.

```Bash
export SSH_AUTH_SOCK=/Users/<user>/.bitwarden-ssh-agent.sock
```

```Bash
launchctl setenv "SSH_AUTH_SOCKET" "/Users/<user>/.bitwarden-ssh-agent.sock"
```

--------------------------------

### Edit Bitwarden Configuration (config.yml)

Source: https://bitwarden.com/help/cli/deploy-key-connector

Opens the `bwdata/config.yml` file using the nano editor. This file is used to configure various aspects of your Bitwarden instance, including enabling Key Connector by setting `enable_key_connector` to `true`.

```Bash
nano bwdata/config.yml
```

--------------------------------

### Bitwarden Host Match Detection for Autofill

Source: https://bitwarden.com/help/cli/uri-match-detection

Explains how Bitwarden's 'Host' match detection works, where autofill is offered if the hostname and port of the URI exactly match the detected resource. Includes a table demonstrating autofill behavior for various URLs.

```APIDOC
For example, if the URI https://sub.domain.com:4000 uses host match detection:
| URL | Autofill? |
| --- | --- |
| http://sub.domain.com:4000 |  |
| https://sub.domain.com:4000/page.html |  |
| https://domain.com |  |
| https://sub.domain.com |  |
| https://sub2.sub.domain.com:4000 |  |
| https://sub.domain.com:5000 |  |
```

--------------------------------

### Configure Bitwarden CLI with Google Service Account Key (Linux)

Source: https://bitwarden.com/help/cli/workspace-directory

This Bash command configures the Bitwarden Directory Connector CLI on Linux. It extracts the 'private_key' from the downloaded JSON service account file using 'jq' and sets it as the 'gsuite.key' for the CLI, allowing it to authenticate with Google Workspace.

```Bash
bwdc config gsuite.key "\n$(cat projectid-key.json | jq -r '.private_key')"
```

--------------------------------

### JSON Format for Importing Items to Existing Bitwarden Collections

Source: https://bitwarden.com/help/cli/condition-bitwarden-import

This example demonstrates the proper JSON format for importing new login items into pre-existing Bitwarden collections within an organization. It requires obtaining the organization and collection IDs from the web app and defining a 'collections' array that matches these IDs and the collection name to prevent new collection creation.

```JSON
{
  "encrypted": false,
  "collections": [
    {
      "id": "b8e6df17-5143-495e-92b2-aff700f48ecd",
      "organizationId": "55d8fa8c-32bb-47d7-a789-af8710f5eb99",
      "name": "My Existing Collection",
      "externalId": null
    }
  ],
  "folders": [],
  "items": [
    {
      "id": "2f27f8f8-c980-47f4-829a-aff801415845",
      "organizationId": "55d8fa8c-32bb-47d7-a789-af8710f5eb99",
      "folderId": null,
      "type": 1,
      "reprompt": 0,
      "name": "Item to Import",
      "notes": "A login item for sharing.",
      "favorite": false,
      "login": {
        "uris": [
          {
            "match": null,
            "uri": "https://mail.google.com"
          }
        ],
        "username": "my_username",
        "password": "my_password",
        "totp": null
      },
      "collectionIds": ["b8e6df17-5143-495e-92b2-aff700f48ecd"]
    }
  ]
}
```

--------------------------------

### Edit Key Connector Override Environment File

Source: https://bitwarden.com/help/cli/deploy-key-connector

Command to open and edit the `key-connector.override.env` file, which contains configuration settings for Bitwarden Key Connector. This file is pre-populated with defaults but requires modification for production environments.

```Bash
nano bwdata/env/key-connector.override.env
```

--------------------------------

### Accessing Bitwarden CLI General Help

Source: https://bitwarden.com/help/cli/cli

This command displays the general help information for the Bitwarden CLI, listing all available commands and global options. It's the primary way to learn about the CLI's capabilities directly from the command line.

```Bash
bw --help
```

--------------------------------

### Azure Application Gateway Rewrite Rule Condition Pattern

Source: https://bitwarden.com/help/cli/azure-aks-deployment

This regular expression defines the pattern to match for an Azure Application Gateway rewrite rule condition. It targets URI paths that do not start with `/admin`, `/identity`, or `/sso`, capturing the initial segment and the rest of the path for subsequent URL rewriting.

```Regex
^(\/(!admin)(?!identity)(?!sso)[^\/]*)\/.*
```

--------------------------------

### Key Connector Database Configuration Options

Source: https://bitwarden.com/help/cli/deploy-key-connector

Details the required configuration parameters for various database providers supported by Key Connector to store encrypted user keys. It includes settings for Local JSON, Microsoft SQL Server, PostgreSQL, MySQL/MariaDB, and MongoDB, with warnings about migration and backups.

```APIDOC
Database Configuration:
  Local JSON (default):
    Not recommended outside of testing.
    keyConnectorSettings__database__provider=json
    keyConnectorSettings__database__jsonFilePath={File_Path}
  Microsoft SQL Server:
    keyConnectorSettings__database__provider=sqlserver
    keyConnectorSettings__database__sqlServerConnectionString={Connection_String}
  PostgreSQL:
    keyConnectorSettings__database__provider=postgresql
    keyConnectorSettings__database__postgreSqlConnectionString={Connection_String}
  MySQL/MariaDB:
    keyConnectorSettings__database__provider=mysql
    keyConnectorSettings__database__mySqlConnectionString={Connection_String}
  MongoDB:
    keyConnectorSettings__database__provider=mongo
    keyConnectorSettings__database__mongoConnectionString={Connection_String}
    keyConnectorSettings__database__mongoDatabaseName={DatabaseName}
```

--------------------------------

### Bitwarden Web App OIDC Configuration Fields

Source: https://bitwarden.com/help/cli/oidc-azure

Details the specific fields within the Bitwarden web application that need to be configured for OpenID Connect (OIDC) integration with Microsoft Entra ID. Each field's purpose, required input, and any special considerations are outlined to ensure a successful SSO setup.

```APIDOC
Field: Authority
  Description: Enter `https://login.microsoftonline.com/<TENANT_ID>/v2.0`, where `TENANT_ID` is the **Directory (tenant) ID** value retrieved from the app registration's Overview screen.
Field: Client ID
  Description: Enter the App registration's **Application (client) ID**, which can be retrieved from the Overview screen.
Field: Client Secret
  Description: Enter the **Secret Value** of the [created client secret](/help/oidc-azure/#create-a-client-secret).
Field: Metadata Address
  Description: For Azure implementations as documented, you can leave this field blank.
Field: OIDC Redirect Behavior
  Description: Select either **Form POST** or **Redirect GET**.
Field: Get Claims From User Info Endpoint
  Description: Enable this option if you receive URL too long errors (HTTP 414), truncated URLS, and/or failures during SSO.
Field: Additional/Custom Scopes
  Description: Define custom scopes to be added to the request (comma-delimited).
Field: Additional/Custom User ID Claim Types
  Description: Define custom claim type keys for user identification (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
Field: Additional/Custom Email Claim Types
  Description: Define custom claim type keys for users' email addresses (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
Field: Additional/Custom Name Claim Types
  Description: Define custom claim type keys for users' full names or display names (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
Field: Requested Authentication Context Class Reference values
  Description: Define Authentication Context Class Reference identifiers (`acr_values`) (space-delimited). List `acr_values` in preference-order.
Field: Expected "acr" Claim Value in Response
  Description: Define the `acr` Claim Value for Bitwarden to expect and validate in the response.
```

--------------------------------

### Configure Bitwarden Directory Connector CLI with Google Service Account Key (Linux)

Source: https://bitwarden.com/help/cli/gsuite-directory

This Bash command configures the Bitwarden Directory Connector CLI on Linux. It extracts the "private_key" from the downloaded Google service account JSON file using "jq" and passes it to the "bwdc config gsuite.key" command. Remember to replace "projectid-key.json" with your actual key file name.

```Bash
bwdc config gsuite.key "\n$(cat projectid-key.json | jq -r '.private_key')"
```

--------------------------------

### Configure Bitwarden Extension Force-Install for Firefox via GPO

Source: https://bitwarden.com/help/cli/browserext-deploy

This snippet provides the XPI download URL for the Bitwarden browser extension, used to force-install it for Mozilla Firefox via Windows Group Policy. This ensures the extension is automatically deployed on managed machines.

```Configuration
https://addons.mozilla.org/firefox/downloads/latest/bitwarden-password-manager/latest.xpi
```

--------------------------------

### Create/Edit Kerberos Configuration File (krb5.conf)

Source: https://bitwarden.com/help/cli/kerberos-integration

This command opens the `krb5.conf` file for creation or editing using the nano text editor. This file contains Kerberos client configuration, including KDC and admin server details, and ticket lifetime settings.

```Shell
nano /opt/bitwarden/bwdata/kerberos/krb5.conf
```

--------------------------------

### Display Bitwarden Admin Tools Script Help

Source: https://bitwarden.com/help/cli/migration-script

This command executes the `bwAdminTools.py` script with the `-h` flag to display its helper text, providing information on available commands and options.

```Bash
python3 bwAdminTools.py -h
```

--------------------------------

### Bitwarden Send Types Configuration

Source: https://bitwarden.com/help/cli/create-send

Defines the available types for creating a Bitwarden Send (Text or File) and their associated steps and limitations.

```APIDOC
Send Types:
  Text:
    Description: Type or paste the desired text into the input box.
    Options:
      - "When accessing the Send, hide the text by default": Toggle visibility to require recipients to toggle visibility when they open a Send.
    Limitations:
      - Max 1000 characters encrypted (character count increases due to encryption, meaning ~700 unencrypted characters will scale to ~1,000 encrypted characters).
      - Character counts grow between 30-50% when encrypted.
  File:
    Description: Select the Choose File button and browse for the file to Send.
    Limitations:
      - Max file size per Send is 500 MB (100 MB on Mobile).
      - Requires Premium & Verified Email.
```

--------------------------------

### Add Bitwarden User to Docker Group

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Adds the 'bitwarden' user to the 'docker' group, granting it the necessary permissions to run Docker commands without requiring 'sudo' for every operation.

```Bash
sudo usermod -aG docker bitwarden
```

--------------------------------

### Bitwarden Web App OIDC Configuration Fields

Source: https://bitwarden.com/help/cli/oidc-microsoft-entra-id

Details the required fields and their values for configuring OpenID Connect (OIDC) single sign-on within the Bitwarden web application after initial setup in the Azure Portal. These fields define how Bitwarden interacts with Microsoft Entra ID for authentication.

```APIDOC
Field: Authority
  Description: Enter `https://login.microsoftonline.com/<TENANT_ID>/v2.0`, where `TENANT_ID` is the **Directory (tenant) ID** value retrieved from the app registration's Overview screen.
Field: Client ID
  Description: Enter the App registration's **Application (client) ID**, which can be retrieved from the Overview screen.
Field: Client Secret
  Description: Enter the **Secret Value** of the [created client secret](/help/oidc-azure/#create-a-client-secret).
Field: Metadata Address
  Description: For Azure implementations as documented, you can leave this field blank.
Field: OIDC Redirect Behavior
  Description: Select either **Form POST** or **Redirect GET**.
Field: Get Claims From User Info Endpoint
  Description: Enable this option if you receive URL too long errors (HTTP 414), truncated URLS, and/or failures during SSO.
Field: Additional/Custom Scopes
  Description: Define custom scopes to be added to the request (comma-delimited).
Field: Additional/Custom User ID Claim Types
  Description: Define custom claim type keys for user identification (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
Field: Additional/Custom Email Claim Types
  Description: Define custom claim type keys for users' email addresses (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
Field: Additional/Custom Name Claim Types
  Description: Define custom claim type keys for users' full names or display names (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
Field: Requested Authentication Context Class Reference values
  Description: Define Authentication Context Class Reference identifiers (`acr_values`) (space-delimited). List `acr_values` in preference-order.
Field: Expected "acr" Claim Value in Response
  Description: Define the `acr` Claim Value for Bitwarden to expect and validate in the response.
```

--------------------------------

### Move Bitwarden Vault Item using CLI `bw edit` Command

Source: https://bitwarden.com/help/cli/folders

This snippet illustrates the initial steps for moving a Bitwarden vault item using the CLI's `bw edit` command. It involves first retrieving the item's ID with `bw get` and then using `bw edit` to modify the item's JSON object, specifically its `folderId` attribute. This process typically requires a command-line JSON processor like `jq` and the `bw encode` command to apply changes.

```Bash
bw get item 7ac9cae8-5067-4faf-b6ab-acfd00e2c328
bw edit item 7ac9cae8-5067-4faf-b6ab-acfd00e2c328
```

--------------------------------

### Log in to Bitwarden Directory Connector CLI

Source: https://bitwarden.com/help/cli/directory-sync-cli

Use the `login` command to authenticate with Directory Connector using your organization API key. You can log in by prompting for credentials, passing them as parameters, or by setting environment variables.

```Bash
bwdc login
```

```Bash
bwdc login organization.b5351047-89b6-820f-ad21016b6222 yUMB4trbqV1bavhEHGqbuGpz4AlHm9
```

```Bash
BW_CLIENTID="organization.b5351047-89b6-820f-ad21016b6222"
BW_CLIENTSECRET="yUMB4trbqV1bavhEHGqbuGpz4AlHm9"

bwdc login
```

--------------------------------

### Import Data using Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-data-from-myki

Use the Bitwarden command-line interface (CLI) to import data into your vault. The command requires a specified format and the path to the import file. You can retrieve a list of supported formats using `bw import --formats`.

```Bash
bw import <format> <path>
```

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Deploy BitwardenSecret Object with Custom Mapping for Kubernetes

Source: https://bitwarden.com/help/cli/secrets-manager-kubernetes-operator

This example shows the deployment of a `BitwardenSecret` Kubernetes object, which defines the synchronization settings for pulling data from Bitwarden Secrets Manager into a Kubernetes secret. It includes an optional `map` element to customize the key names of the synchronized secrets within Kubernetes. The `organizationId`, `secretName`, and `authToken` fields are crucial for specifying the source organization, the target Kubernetes secret name, and the authentication method, respectively.

```YAML
cat <<EOF | kubectl apply -n <YOUR_NAMESPACE> -f -
apiVersion: k8s.bitwarden.com/v1
kind: BitwardenSecret
metadata:
  labels:
    app.kubernetes.io/name: bitwardensecret
    app.kubernetes.io/instance: bitwardensecret-sample
    app.kubernetes.io/part-of: sm-operator
    app.kubernetes.io/managed-by: kustomize
    app.kubernetes.io/created-by: sm-operator
  name: bitwardensecret-sample
spec:
  organizationId: "a08a8157-129e-4002-bab4-b118014ca9c7"
  secretName: bw-sample-secret
  map:
    - bwSecretId: 6c230265-d472-45f7-b763-b11b01023ca6
      secretKeyName: container__registry__secret
#  - bwSecretId: d132a5ed-12bd-49af-9b74-b11b01025d58
#     secretKeyName: test__secret__2
  authToken:
    secretName: bw-auth-token
    secretKey: token
EOF
```

--------------------------------

### Configure Custom Claim Types in Microsoft Entra ID for Bitwarden SSO

Source: https://bitwarden.com/help/cli/oidc-microsoft-entra-id

Outlines the steps to add and configure custom claim types in Microsoft Entra ID (Azure AD) and how to specify their fully qualified paths in the Bitwarden SSO configuration. This is necessary when your SSO setup requires non-standard claims for user identification or attributes.

```APIDOC
1. On Microsoft Entra ID, add a custom claim type by navigating to **Enterprise applications** → **App registrations** → **Token configuration**.
2. Select  **Add optional claim** and create a new optional claim with a selected value.
3. On the Bitwarden SSO configuration screen, enter the fully qualified path for a custom claim field in the corresponding **custom claim types** field. For example: `https://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn`.
4. Select **Save** once you have completed the configuration.
```

--------------------------------

### Unlock Bitwarden CLI vault

Source: https://bitwarden.com/help/cli/cli

Explains the `bw unlock` command, which is necessary after logging in with an API key or SSO if you intend to work directly with vault data. Unlocking generates a session key, a decryption key required for commands that interact with vault data (e.g., `list`, `get`, `edit`). Session keys are valid until `bw lock` or `bw logout` is used, but do not persist across new terminal windows.

```Bash
bw unlock
```

--------------------------------

### Set Local User and Group IDs for Containers

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Sets the `LOCAL_UID` and `LOCAL_GID` environment variables in `./bwdata/env/uid.env`. These values ensure that Bitwarden Docker containers run with the permissions of the previously created `bitwarden` user and group.

```Bash
LOCAL_UID=1001
LOCAL_GID=1001
```

--------------------------------

### Modify Bitwarden Send 'disabled' status via CLI

Source: https://bitwarden.com/help/cli/send-lifespan

This snippet demonstrates how to modify the 'disabled' status of a Bitwarden Send using the CLI. It retrieves a Send by ID, pipes its JSON output to 'jq' to set the 'disabled' property to 'false' (effectively enabling it if it was disabled), encodes the modified JSON, and then updates the Send. Note: The accompanying text suggests setting 'disabled' to 'true' for deactivation, but the example code sets it to 'false'.

```Bash
bw send get <id> | jq '.disabled=false' | bw encode | bw send edit
```

--------------------------------

### Bitwarden CLI: `bw send` Master Command Syntax

Source: https://bitwarden.com/help/cli/send-cli

The `send` command serves as the primary entry point for all Send-related subcommands in the Bitwarden CLI. It defines the general structure for executing Send operations.

```Bash
bw send [options] [command] <data>
```

--------------------------------

### Bitwarden CLI: Shortcut to Create Text Send

Source: https://bitwarden.com/help/cli/send-cli

Quickly create a text Send by providing the content directly to the `bw send` command. The command will output the generated Send link upon successful creation.

```Bash
bw send "Fastest Send in the West."
```

--------------------------------

### Bitwarden Device Login Authentication Flow

Source: https://bitwarden.com/help/cli/log-in-with-device

Detailed explanation of the internal process for 'Log in with device' authentication, outlining client-server interactions, data encryption, and database operations.

```APIDOC
When logging in with a device is initiated:

1. Initiating Client POSTs Request:
   - Endpoint: Authentication Request table in Bitwarden database
   - Payload: Account email address, unique auth-request public key, access code

2. Registered Devices Receive Request:
   - Description: Mobile/desktop apps logged in with device-specific GUIDs are provided the request.

3. Approving Client Encrypts Data:
   - Action: Encrypts account's master key and master password hash
   - Method: Uses auth-request public key from the request

4. Approving Client PUTs Encrypted Data:
   - Endpoint: Authentication Request record
   - Payload: Encrypted master key, encrypted master password hash
   - Status: Marks request fulfilled

5. Initiating Client GETs Encrypted Data:
   - Endpoint: Authentication Request record
   - Response: Encrypted master key, encrypted master password hash

6. Initiating Client Decrypts Data Locally:
   - Action: Decrypts master key and master password hash
   - Method: Uses auth-request private key

7. Initiating Client Authenticates User:
   - Method: Uses access code and fulfilled authentication request
   - Service: Bitwarden Identity service
```

--------------------------------

### Configure Bitwarden Desktop App for Self-Hosted Server

Source: https://bitwarden.com/help/cli/deploy-clients

To centrally configure the Desktop app for deployment, the 'data.json' file needs to be edited. This snippet shows how to set the 'global_environment_environment' object to specify a self-hosted server URL, allowing the app to connect to a custom instance.

```JSON
"global_environment_environment": {
    "region": "Self-hosted",
    "urls": {
       "base": "self-host.com"
     }
  }
```

--------------------------------

### Configure Bitwarden Directory Connector CLI with Google Service Account Key (Other OSs)

Source: https://bitwarden.com/help/cli/gsuite-directory

This command configures the Bitwarden Directory Connector CLI on non-Linux operating systems. It reads the private key from a ".crt" file (e.g., "google-bwdc-key.crt"), which should contain the private key copied from your Google service account JSON file. Ensure you replace the placeholder filename with your actual ".crt" file.

```Bash
bwdc config gsuite.key "\n$(cat google-bwdc-key.crt)\n"
```

--------------------------------

### Access Git Configuration File with Nano

Source: https://bitwarden.com/help/cli/ssh-agent

Instructions to open the global Git configuration file using the Nano text editor for editing.

```Plain
nano ~/.gitconfig
```

--------------------------------

### Restart Bitwarden Server to Apply Configuration Changes

Source: https://bitwarden.com/help/cli/self-host-an-organization

After modifying the environment variables in `./bwdata/env/global.override.env`, execute this command to restart the Bitwarden server and apply the new configuration settings.

```Shell
./bitwarden.sh restart
```

--------------------------------

### Email Template: Program Introduction for Bitwarden Adoption

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

This email introduces a six-day plan to help increase user adoption of Bitwarden among colleagues, highlighting essential strategies and the complimentary Families plan benefit.

```Email
Subject: Tips to get your team to use Bitwarden

Body:

Hi *[name]*,

Getting the right start with password management can lead to a successful deployment for employees.

You'll soon receive a six-day plan to help increase user adoption of your new password manager among your colleagues.

These brief, actionable emails will cover essential strategies including:

1. Appoint an implementation champion
2. Communicate your rollout plan
3. Explain the top benefits of a password manager
4. Use email templates for easy sharing
5. Share get-started guides

Also, remember that Bitwarden Enterprise plans include complimentary Families plans for personal use. Let your team know they can redeem their free Bitwarden Families plan to keep their data safe both at work and at home.

You can use this example email to share the free Families plan with your team.
```

--------------------------------

### Bitwarden Supported Languages Reference

Source: https://bitwarden.com/help/cli/localization

A comprehensive list of all human languages currently supported across Bitwarden client applications, noting that availability may vary.

```Reference
| Symbol | Language |
| --- | --- |
| af | Afrikaans |
| ar | الفصحى العربية |
| az | Azərbaycanca |
| be | Беларуская |
| bg | български |
| ca | català |
| cs | čeština |
| cy | Welsh |
| da | dansk |
| de | Deutsch |
| el | Ελληνικά |
| en | English |
| en-GB | English (British) |
| eo | Esperanto |
| es | español |
| et | eesti |
| fa | فارسی |
| fi | suomi |
| fr | français |
| gl | Galician |
| he | עברית |
| hi | हिन्दी |
| hr | hrvatski |
| hu | magyar |
| id | Bahasa Indonesia |
| it | italiano |
| ja | 日本語 |
| ko | 한국어 |
| lv | Latvietis |
| ml | മലയാളം |
| mr | मराठी |
| my | မြန်မာဘာသာ |
| nb | norsk (bokmål) |
| ne | नेपाली |
| nl | Nederlands |
| or | ଓଡ଼ିଆ |
| pl | polski |
| pt-BR | português do Brasil |
| pt-PT | português |
| ro | română |
| ru | русский |
| sk | slovenčina |
| sr | Српски |
| sv | svenska |
| te | తెలుగు |
| th | ไทย |
| tr | Türkçe |
| uk | українська |
| vi | Tiếng Việt |
| zh-CN | 中文（中国大陆） |
| zh-TW | 中文（台灣） | 
```

--------------------------------

### Bitwarden CLI: List Sends with Pretty Output and File Redirection

Source: https://bitwarden.com/help/cli/send-cli

Demonstrates how to use the `--pretty` option to format the JSON output of the `bw send list` command and pipe the result to a file for easy storage or further processing.

```Bash
bw send list --pretty > /Users/myaccount/Documents/pretty_list_of_sends.json
```

--------------------------------

### Bitwarden Account Creation: Master Key Derivation

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Explains the derivation of the Master Key and Stretched Master Key during account creation using PBKDF2 and HKDF, including iteration rounds and salts.

```APIDOC
Function: DeriveMasterKey
  Description: Derives the 256-bit Master Key from user's master password and email.
  Parameters:
    master_password: string (User's master password)
    email_address: string (User's email address, used as salt)
  Algorithm: PBKDF2-SHA256
  Iterations: 600,000
  Returns: 256-bit MasterKey

Function: DeriveStretchedMasterKey
  Description: Stretches the Master Key to 512-bits.
  Parameters:
    master_key: 256-bit binary (Derived Master Key)
  Algorithm: HKDF
  Returns: 512-bit StretchedMasterKey
```

--------------------------------

### Set Bitwarden Container User and Group IDs

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Configures the `LOCAL_UID` and `LOCAL_GID` environment variables in `./bwdata/env/uid.env`. These settings ensure that the Bitwarden containers run under the specified `bitwarden` user and group IDs, which is crucial for security and to prevent issues related to running as root.

```Bash
LOCAL_UID=1001
LOCAL_GID=1001
```

--------------------------------

### Configure Bitwarden CLI with Google Service Account Key (Other OSs)

Source: https://bitwarden.com/help/cli/workspace-directory

This Bash command configures the Bitwarden Directory Connector CLI on operating systems other than Linux. It reads the private key from a separate '.crt' file (which should contain only the private key value) and sets it as the 'gsuite.key' for the CLI, enabling authentication with Google Workspace.

```Bash
bwdc config gsuite.key "\n$(cat google-bwdc-key.crt)\n"
```

--------------------------------

### User Filter: Include Specific Users by Email List

Source: https://bitwarden.com/help/cli/workspace-directory

This filter specifies syncing only a selection of users based on their email addresses. A comma-separated list of emails is provided. No query declaration (`|`) is needed if only `include:` or `exclude:` filters are used without additional query parameters like OU or `orgTitle`.

```Bash
include:joe@example.com,bill@example.com,tom@example.com
```

--------------------------------

### Bitwarden CLI Global Options Reference

Source: https://bitwarden.com/help/cli/cli

This section enumerates the global command-line options available across various Bitwarden CLI commands. These options modify output formatting, suppress interactive prompts, or pass session keys.

```APIDOC
Global Options:
  --pretty: Format output. JSON is tabbed with two spaces.
  --raw: Return raw output instead of a descriptive message.
  --response: Return a JSON formatted version of response output.
  --quiet: Don't return anything to stdout. Useful for piping credential values.
  --nointeraction: Do not prompt for interactive user input.
  --session <session>: Pass session key instead of reading from an environment variable.
  -v, --version: Output the Bitwarden CLI version number.
  -h, --help: Display help text for the command.
```

--------------------------------

### Create Firefox Policies Directory on Linux

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This Bash command creates the /etc/firefox/policies directory on Linux systems. The -p flag ensures that parent directories are created if they don't exist, preventing errors and preparing the location for Firefox policy files.

```Bash
mkdir -p /etc/firefox/policies
```

--------------------------------

### Run Bitwarden Unified Docker Container (Direct Docker)

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command runs the Bitwarden container in detached mode, assigning it a name, mapping a local volume for data, mapping port 80 to 8080, and loading environment variables from 'settings.env'.

```Bash
docker run -d --name bitwarden -v /$(pwd)/bwdata/:/etc/bitwarden -p 80:8080 --env-file settings.env ghcr.io/bitwarden/self-host:beta
```

--------------------------------

### Bitwarden Enterprise Features: Application Range and Ease-of-use

Source: https://bitwarden.com/help/cli/enterprise-feature-list

Details the features and their descriptions within the Application Range and Ease-of-use category for Bitwarden Enterprise Organizations, covering deployment options and application availability.

```APIDOC
Deployment Options: Cloud, Private Cloud, and Self-hosted.
Web Application: Fully encrypted cloud web app at https://vault.bitwarden.com, or on your self-hosted server.
Mobile Apps (with Mobile Login Controls): Available for iOS and Android. Learn more.
Browser Extensions: Available for Chrome, Firefox, Opera, Edge, Vivaldi, Brave, Tor, and Safari. Learn more.
Desktop Applications: Available for Windows, Mac, and Linux. Learn more.
Command-line Interface: Available for Windows, Mac, and Linux. Learn More.
```

--------------------------------

### Bitwarden Directory Connector: Combine Exclude Filter with Member Key Query

Source: https://bitwarden.com/help/cli/workspace-directory

Demonstrates combining an `exclude:` filter with a query declaration like `|memberKey:`. Exclusion/inclusion filters must always precede any query declarations.

```Bash
exclude:Group A|memberKey:user@company
```

--------------------------------

### Import Data using Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-from-firefox

Use the Bitwarden CLI to import data into your vault. This command requires specifying the import format and the path to the file. It's important to note that importing does not check for existing items, which can lead to duplicates.

```Bash
bw import <format> <path>
```

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Assign Users and Groups to Okta SAML Application for Bitwarden

Source: https://bitwarden.com/help/cli/saml-okta

Explains how to assign users or groups to the Bitwarden SAML application within Okta, enabling access for individuals or bulk assignment.

```APIDOC
Assignment Options:
  Assign to People: Assign access on a user-by-user basis.
  Assign to Groups: Assign access in-bulk using group membership.
```

--------------------------------

### Bitwarden Send Options Configuration

Source: https://bitwarden.com/help/cli/create-send

Details the configurable options for a Bitwarden Send, including deletion/expiration dates, access limits, password protection, and privacy settings.

```APIDOC
Send Options:
  Deletion date:
    Description: The Send will be permanently deleted on the specified date and time.
    Default: Seven days from creation.
    Maximum: 31 days from creation.
  Expiration date:
    Description: The Send will expire on the specified date and time.
  Maximum access count:
    Description: The Send will be disabled after the specified access count is reached.
    Default: Unspecified.
  Password:
    Description: Require a password to be entered by recipients of this Send in order to gain access.
  Notes:
    Description: Enter private notes for this Send, which will only be visible to you.
  Hide my email address from recipients:
    Description: Hide your email from Send recipients.
  Deactivate this Send so that no one can access it:
    Description: Check this box to prevent this Send from being accessible to any recipients. You will still be able to interact with this Send from your Send view.
```

--------------------------------

### Bitwarden Community Platform URLs

Source: https://bitwarden.com/help/cli/bitwarden-addresses

Compiles links to various official Bitwarden community platforms and social media channels for support and engagement.

```APIDOC
Feature requests: https://community.bitwarden.com/t/about-the-feature-requests-category/12
Contributing: https://github.com/orgs/bitwarden/discussions
Community forums: https://community.bitwarden.com/
X.com: https://x.com/bitwarden
Reddit: https://www.reddit.com/r/Bitwarden/
YouTube: https://www.youtube.com/channel/UCId9a_jQqvJre0_dE2lE_Rw
LinkedIn: https://www.linkedin.com/company/bitwarden1
Facebook: https://www.facebook.com/bitwarden/
Instagram: https://www.instagram.com/bitwarden/
Mastodon: https://fosstodon.org/%40bitwarden
Twitch: https://www.twitch.tv/bitwardenlive
```

--------------------------------

### Configure Bitwarden Directory Connector settings via CLI

Source: https://bitwarden.com/help/cli/directory-sync-cli

Use the `config` command to specify or update various directory settings for the Bitwarden Directory Connector. You must provide a setting name and its corresponding value.

```Bash
bwdc config <setting> <value>
```

--------------------------------

### List Bitwarden Projects using CLI

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command lists all projects the machine account has access to. By default, it returns a JSON array. The output format can be altered using the `--output` flag.

```Bash
bws project list
```

--------------------------------

### Configure Firefox All Service URLs via Windows Registry

Source: https://bitwarden.com/help/cli/deploy-clients

This entry outlines the additional value names required to configure all Bitwarden service URLs independently in Firefox via Windows Group Policy Manager and Registry Editor. Each value name requires a separate registry item with the same key path and type as the base URL.

```APIDOC
Additional Registry Value Names (All Services):
  webVault
  api
  identity
  icons
  notifications
  events
```

--------------------------------

### Configure Basic SAML Fields in Okta for Bitwarden

Source: https://bitwarden.com/help/cli/saml-okta

Details the essential SAML configuration fields within the Okta Admin Portal for integrating with Bitwarden, including Single Sign-On URL, Audience URI, Name ID format, and Application username.

```APIDOC
Single sign on URL:
  Description: Set this field to the pre-generated Assertion Consumer Service (ACS) URL. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Audience URI (SP Entity ID):
  Description: Set this field to the pre-generated SP Entity ID. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Name ID format:
  Description: Select the SAML NameID format to use in SAML assertions. By default, Unspecified.
Application username:
  Description: Select the Okta attribute users will use to login to Bitwarden, typically Email.
```

--------------------------------

### Configure Bitwarden SAML Service Provider Settings

Source: https://bitwarden.com/help/cli/saml-keycloak

Details the fields required to configure Bitwarden as a SAML service provider, determining the format of SAML requests.

```APIDOC
SAML service provider configuration:
  Name ID format: Select Email.
  Outbound Signing Algorithm: The algorithm Bitwarden will use to sign SAML requests.
  Signing Behavior: Whether/when SAML requests will be signed.
  Minimum Incoming Signing Algorithm: Select the algorithm the Keycloak client is configured to use to sign SAML documents or assertions.
  Want Assertions Signed: Whether Bitwarden expects SAML assertions to be signed. If toggled on, make sure you configure the Keycloak client to sign assertions.
  Validate Certificates: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured with the Bitwarden login with SSO docker image.
```

--------------------------------

### Configure All Bitwarden Browser Extension Environment URLs on macOS via .plist

Source: https://bitwarden.com/help/cli/deploy-clients

This snippet provides the XML content for a .plist file to configure all Bitwarden browser extension environment URLs (base, webVault, api, identity, icons, notifications, events) on macOS. This allows for granular control over each service's URL.

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>environment</key>
        <dict>
            <key>base</key>
            <string>https://my.bitwarden.server.com</string>
                            <key>webVault</key>
                           <string>https://my.bitwarden.server.com</string>
                           <key>api</key>
                           <string>https://my.bitwarden.server.com></string>
                           <key>identity</key>
                           <string>https://my.bitwarden.server.com</string>
                           <key>icons</key>
                           <string>https://my.bitwarden.server.com</string>
                           <key>notifications</key>
                           <string>https://my.bitwarden.server.com</string>
                           <key>events</key>
                           <string>https://my.bitwarden.server.com</string>
        </dict>
    </dict>
</plist>
```

--------------------------------

### Filter Users by Last Name

Source: https://bitwarden.com/help/cli/okta-directory

Demonstrates filtering users based on their `lastName` attribute using a direct filter query prefixed with a pipe (`|`). This targets specific user profiles for synchronization.

```Bash
|profile.lastName eq "Smith"
```

--------------------------------

### Verify Bitwarden Docker Container Status

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command is used to list running Docker containers and verify that the Bitwarden unified deployment container is active and healthy after execution. It helps confirm the successful launch of the server.

```Bash
docker ps
```

--------------------------------

### Configure Bitwarden SAML Service Provider Settings

Source: https://bitwarden.com/help/cli/saml-okta

Details the SAML service provider configuration fields within the Bitwarden web app, which determine the format of SAML requests based on choices made in Okta.

```APIDOC
Name ID format:
  Description: Set this to whatever the Name ID format specified in Okta, otherwise leave Unspecified.
Outbound signing algorithm:
  Description: The algorithm Bitwarden will use to sign SAML requests.
Signing behavior:
  Description: Whether/when SAML requests will be signed.
Minimum incoming signing algorithm:
  Description: Set this to the Signature Algorithm specified in Okta.
Expect signed assertions:
  Description: Check this box if you set the Assertion Signature field to Signed in Okta.
Validate certificates:
  Description: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configure within the Bitwarden login with SSO docker image.
```

--------------------------------

### Create Docker group

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Ensures the 'docker' group exists on the system. This group is necessary for managing Docker containers and images.

```Bash
sudo groupadd docker
```

--------------------------------

### Import Data using Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-from-keeper

This command imports data into your Bitwarden vault from the command line interface. It requires a specified format and the path to the import file. Use `bw import --formats` to retrieve a list of supported formats.

```Bash
bw import <format> <path>
```

--------------------------------

### Bitwarden Migration Script Configuration Variables

Source: https://bitwarden.com/help/cli/migration-script

This section outlines the required environment variables for the `bwAdminTools.py` script, categorized into Source and Destination organization settings. These variables must be set in a `config.cfg` file before running the migration script.

```APIDOC
# config.cfg variables
Source organization variables:
  bw_vault_uri: FQDN of your source web vault, e.g. https://company.bitwarden.com or https://vault.bitwarden.com.
  bw_org_client_id: Source organization API key client ID.
  bw_org_client_secret: Source organization API key client secret.
  bw_org_id: Source organization's GUID (from _client_id, remove 'organization.').
  bw_acc_client_id: Source organization admin's or owner's personal API key client ID.
  bw_acc_client_secret: Source organization admin's or owner's personal API key client secret.

Destination organization variables:
  dest_bw_vault_uri: FQDN of your destination web vault, e.g. https://company.bitwarden.com or https://vault.bitwarden.eu.
  dest_bw_org_client_id: Destination organization API key client ID.
  dest_bw_org_client_secret: Destination organization API key client secret.
  dest_bw_org_id: Destination organization's GUID (from _client_id, remove 'organization.').
  dest_bw_acc_client_id: Destination organization admin's or owner's personal API key client ID.
  dest_bw_ac_client_secret: Destination organization admin's or owner's personal API key client secret.
```

--------------------------------

### Configure Advanced SAML Settings in Okta for Bitwarden

Source: https://bitwarden.com/help/cli/saml-okta

Describes advanced SAML settings in Okta, such as response and assertion signature requirements, and the signature and digest algorithms used for signing SAML messages.

```APIDOC
Response:
  Description: Whether the SAML response is signed by Okta.
Assertion Signature:
  Description: Whether the SAML assertion is signed by Okta.
Signature Algorithm:
  Description: The signing algorithm used to sign the response and/or assertion, depending on which is set to Signed. By default, rsa-sha256.
Digest Algorithm:
  Description: The digest algorithm used to sign the response and/or assertion, depending on which is set to Signed. This field must match the selected Signature Algorithm.
```

--------------------------------

### CLI: Generate Passphrase with New Options

Source: https://bitwarden.com/help/cli/releasenotes

The `bw generate --passphrase` command in the Bitwarden CLI now supports additional options `--capitalize` and `--includeNumber` for customizing generated passphrases.

```CLI
bw generate --passphrase --capitalize --includeNumber
```

--------------------------------

### Force SMTP STARTTLS

Source: https://bitwarden.com/help/cli/environment-variables

Specify `true` to force STARTTLS (Opportunistic TLS) for SMTP communication, enhancing security by upgrading a plain text connection to an encrypted one.

```APIDOC
globalSettings__mail__smtp__startTls=true
```

--------------------------------

### Bitwarden CLI: Create Command Syntax

Source: https://bitwarden.com/help/cli/cli

Shows the general syntax for the `bw create` command, which is used to create various object types in the Bitwarden vault, such as items, attachments, folders, or organization collections. It requires an encoded JSON payload and supports optional parameters.

```Bash
bw create (item|attachment|folder|org-collection) <encodedJson> [options]
```

--------------------------------

### Import Data using Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-from-safari

This command imports data into your Bitwarden vault via the command-line interface. It requires specifying the import file format and the path to the file. Use 'bw import --formats' to retrieve a list of supported formats. Importing does not check for existing items, which may create duplicates.

```Bash
bw import <format> <path>
```

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Bitwarden Authentication and Decryption Process

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Outlines the user login process, including Master Key derivation via PBKDF2 and Master Password Hash generation for server-side authentication.

```APIDOC
Process: UserLoginAuthentication
  Description: Authenticates a user upon login.
  Parameters:
    email_address: string (User's account email address)
    master_password: string (User's master password)
  Steps:
    1. DeriveMasterKey(master_password, email_address) -> 256-bit MasterKey (using PBKDF2, 600,000 iterations)
    2. GenerateMasterPasswordHash(MasterKey, master_password) -> ClientMasterPasswordHash (using PBKDF-SHA256)
    3. SendClientMasterPasswordHashToServer(ClientMasterPasswordHash)
    4. ServerAuthenticates(ClientMasterPasswordHash, ServerStoredMasterPasswordHash)
```

--------------------------------

### Configure SQLite Database in Bitwarden settings.env

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This snippet illustrates how to configure Bitwarden to use SQLite as its database provider by setting environment variables in the `settings.env` file. It allows specifying an optional path for the database file, otherwise, a default `vault.db` is created.

```Bash
# Database
BW_DB_PROVIDER=sqlite
BW_DB_FILE=/path/to/.db
```

--------------------------------

### Create Bitwarden Project via CLI

Source: https://bitwarden.com/help/cli/secrets-manager-cli

The `bws project create` command is used to establish a new project, requiring a project name. Machine accounts with read-only access can create projects. The command returns the newly created project as a JSON object.

```Bash
bws project create <NAME>
```

```Bash
bws project create "My project"
```

```JSON
{
  "object": "project",
  "id": "1c80965c-acb3-486e-ac24-b03000dc7318",
  "organizationId": "10e8cbfa-7bd2-4361-bd6f-b02e013f9c41",
  "name": "My project",
  "creationDate": "2023-06-29T13:22:37.942559Z",
  "revisionDate": "2023-06-29T13:22:37.942559Z"
}
```

--------------------------------

### Bitwarden Exact Match Detection for Autofill

Source: https://bitwarden.com/help/cli/uri-match-detection

Explains Bitwarden's 'Exact' match detection, where autofill is offered only when the URI precisely matches the detected resource. Includes a table and a tip about restricting autofill to HTTPS sites.

```APIDOC
For example, if the URI https://www.google.com/page.html uses exact match detection:
| URL | Autofill? |
| --- | --- |
| https://www.google.com/page.html |  |
| http://www.google.com/page.html |  |
| https://www.google.com/page.html?query=123 |  |
| https://www.google.com |  |
```

--------------------------------

### Import Data using Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-from-1password

This command imports data into your Bitwarden vault using the command-line interface. It requires specifying the import file format and the path to the file. Use `bw import --formats` to retrieve a list of supported formats.

```Bash
bw import <format> <path>
```

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Splunk Search Processing Language (SPL) Structure

Source: https://bitwarden.com/help/cli/splunk-siem

This snippet illustrates the fundamental structure of a Splunk Search Processing Language (SPL) query, showing how search terms are piped into subsequent commands with their arguments.

```Bash
search | commands1 arguments1 | commands2 arguments2 | ...
```

--------------------------------

### Import data using Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-from-dashlane

Use the `bw import` command to import data into your Bitwarden vault from the command line interface. This command requires specifying the import format and the path to the data file.

```Bash
bw import <format> <path>
```

--------------------------------

### Retrieve Identity Provider Values from Okta for Bitwarden SAML

Source: https://bitwarden.com/help/cli/saml-okta

Instructions on how to locate and copy critical Identity Provider (IdP) values from Okta, including the Single Sign-On URL, Issuer, and X.509 Certificate, essential for configuring Bitwarden's SAML settings.

```APIDOC
Identity Provider Single Sign-On URL
Identity Provider Issuer
X.509 Certificate
```

--------------------------------

### Log in to Bitwarden CLI with API Key Prompt

Source: https://bitwarden.com/help/cli/cli

This command initiates an interactive login process using your personal API key, prompting for `client_id` and `client_secret`. It is recommended for automated workflows or when your account uses a 2FA method not supported by the CLI.

```Bash
bw login --apikey
```

--------------------------------

### Restart Computer using PowerShell

Source: https://bitwarden.com/help/cli/authenticator-keys

This PowerShell command initiates a system restart. It is recommended after adjusting the time zone or other system clock settings to ensure changes take effect and resolve TOTP synchronization issues.

```PowerShell
Restart-Computer
```

--------------------------------

### Bitwarden Directory Connector: Query Groups by Name with Wildcards

Source: https://bitwarden.com/help/cli/workspace-directory

Sync groups whose names contain a specific term using a wildcard query. The pipe (|) indicates a query, and asterisks (*) act as wildcards for partial matches (case-insensitive).

```Bash
|name:*engineering*
```

--------------------------------

### Configure Firefox Policy with Base Bitwarden URL

Source: https://bitwarden.com/help/cli/deploy-clients

This JSON configuration file sets the base environment URL for the Bitwarden extension in Firefox. It's typically placed in `/etc/firefox/policies/policies.json` on Linux or `/Applications/Firefox.app/Contents/Resources/distribution/policies.json` on macOS.

```JSON
{
 "policies": {
    "3rdparty": {
      "Extensions": {
        "{446900e4-71c2-419f-a6a7-df9c091e268b}": {
          "environment": {
            "base": "https://my.bitwarden.server.com"
          }
        }
      }
    }
  }
}
```

--------------------------------

### Configure Key Connector for PKCS#11 HSM Private Key Storage

Source: https://bitwarden.com/help/cli/deploy-key-connector

Defines settings for Bitwarden Key Connector using a PKCS#11 HSM for private key storage. Includes provider, slot token serial, login type, PIN, and private key identification (label/ID). An optional library path is also available.

```Bash
keyConnectorSettings__rsaKey__provider=pkcs11
keyConnectorSettings__rsaKey__pkcs11Provider={Provider}
keyConnectorSettings__rsaKey__pkcs11SlotTokenSerialNumber={Token_SerialNumber}
keyConnectorSettings__rsaKey__pkcs11LoginUserType={Login_UserType}
keyConnectorSettings__rsaKey__pkcs11LoginPin={Login_PIN}

ONE OF THE FOLLOWING TWO:
keyConnectorSettings__rsaKey__pkcs11PrivateKeyLabel={PrivateKeyLabel}
keyConnectorSettings__rsaKey__pkcs11PrivateKeyId={PrivateKeyId}

OPTIONALLY:
keyConnectorSettings__rsaKey__pkcs11LibraryPath={path/to/library/file}
```

--------------------------------

### Directory Connector Sync Options Configuration

Source: https://bitwarden.com/help/cli/onelogin-directory

This API documentation details the various configuration options available within the Directory Connector's 'Sync' section. It covers settings for automatic sync intervals, handling disabled users, overwriting existing organization users, managing large sync operations, forming email addresses for users without one, and enabling/disabling user and group synchronization with associated filters.

```APIDOC
Option: Interval
Description: Time between automatic sync checks (in minutes).

Option: Remove disabled users during sync
Description: Check this box to remove users from the Bitwarden organization that have been disabled in your directory.

Option: Overwrite existing organization users based on current sync settings
Description: Check this box to always perform a full sync and remove any users from the Bitwarden organization if they are not in the synced user set. Recommended for OneLogin directories.

Option: More than 2000 users or groups are expected to sync
Description: Check this box if you expect to sync 2000+ users or groups. If you don't check this box, Directory Connector will limit a sync at 2000 users or groups.

Option: If a user has no email address, combine a username prefix with a suffix value to form an email
Description: Check this box to form valid email options for users that do not have an email address. Users without real or formed email addresses will be skipped by Directory Connector. Formed Email = `username` + Email Suffix

Option: Email Suffix
Description: A string (`@example.com`) used to create a suffix for formed email addresses.

Option: Sync users
Description: Check this box to sync users to your organization. Checking this box will allow you to specify User Filters.

Option: User Filter
Description: See Specify sync filters.

Option: Sync groups
Description: Check this box to sync groups to your organization. Checking this box will allow you to specify Group Filters. Please be aware, Directory Connector uses OneLogin `role` values to create Bitwarden groups.

Option: Group Filter
Description: See Specify sync filters.
```

--------------------------------

### Bitwarden Issue Tracker URLs

Source: https://bitwarden.com/help/cli/bitwarden-addresses

Lists direct links to the issue tracking repositories for different Bitwarden components on GitHub.

```APIDOC
Bitwarden server issues: https://github.com/bitwarden/server/issues
Bitwarden client issues: https://github.com/bitwarden/clients/issues
Bitwarden mobile issues: https://github.com/bitwarden/mobile/issues
Bitwarden Directory Connector issues: https://github.com/bitwarden/directory-connector/issues
```

--------------------------------

### Configure MySQL/MariaDB Database in Bitwarden settings.env

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This snippet shows how to configure Bitwarden to use MySQL or MariaDB as its database provider by setting environment variables in the `settings.env` file. It specifies the database server, name, username, and password.

```Bash
# Database
BW_DB_PROVIDER=mysql
BW_DB_SERVER=db
BW_DB_DATABASE=bitwarden_vault
BW_DB_USERNAME=bitwarden
BW_DB_PASSWORD=super_strong_password
```

--------------------------------

### Restart Bitwarden Docker Container (Docker Compose)

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This snippet outlines the commands to stop, recreate, and verify the Bitwarden Docker containers when managed with Docker Compose. This process ensures that any changes in the `docker-compose.yml` or environment variables are applied.

```Bash
docker compose down
docker compose up -d
docker compose ps
```

--------------------------------

### Convert Microsoft Edge Plist to XML Format on macOS

Source: https://bitwarden.com/help/cli/browserext-deploy

This Bash command converts the binary `com.microsoft.Edge.plist` file into a human-readable XML format, making it editable for adding further configuration settings.

```Bash
/usr/bin/plutil -convert xml1 ~/Desktop/com.microsoft.Edge.plist
```

--------------------------------

### Keycloak Client Creation - Login Settings

Source: https://bitwarden.com/help/cli/saml-keycloak

Describes the fields to configure on the Login settings screen when creating a new client in Keycloak for SAML SSO.

```APIDOC
Field: Valid redirect URIs
  Description: Set this field to the pre-generated Assertion Consumer Service (ACS) URL. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
```

--------------------------------

### Linux Directories for Trusted CA Certificates

Source: https://bitwarden.com/help/cli/certificates

Lists the common directories on Linux systems where trusted CA certificates should be placed for system-wide trust.

```Bash
/usr/local/share/ca-certificates/
/usr/share/ca-certificates/
```

--------------------------------

### Import Data using Bitwarden CLI

Source: https://bitwarden.com/help/cli/import-from-passwordsafe

Use the `bw import` command to import data into your Bitwarden vault from the command line. This command requires specifying the import format and the path to the import file. You can use `bw import --formats` to retrieve a list of supported formats.

```Bash
bw import <format> <path>
```

--------------------------------

### Include Specific Users by Email

Source: https://bitwarden.com/help/cli/gsuite-directory

This filter specifies that only the listed email addresses (`joe@example.com`, `bill@example.com`, `tom@example.com`) should be synced. No query declaration (`|`) is required when only email-based inclusion or exclusion filters are used.

```Bash
include:joe@example.com,bill@example.com,tom@example.com
```

--------------------------------

### Configure Bitwarden Browser Extension Environment URLs on Windows via Registry

Source: https://bitwarden.com/help/cli/deploy-clients

This documentation outlines the process of pre-configuring Bitwarden browser extension environment URLs on Windows using Group Policy Manager. It details the registry key paths, value names, types, and data required for both Google Chrome and Microsoft Edge, allowing administrators to set the base URL or individual service URLs.

```APIDOC
Registry Item Properties:
  Action: Update
  Hive: HKEY_LOCAL_MACHINE
  Key Path (Google Chrome): HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome\3rdparty\extensions\<extension_id>\policy\environment
  Key Path (Microsoft Edge): HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge\3rdparty\extensions\<extension_id>\policy\environment
  Value name (Base URL): base
  Value name (Web Vault URL): webVault
  Value name (API URL): api
  Value name (Identity URL): identity
  Value name (Icons URL): icons
  Value name (Notifications URL): notifications
  Value name (Events URL): events
  Value type: REG_SZ
  Value data: Your server's configured domain
```

--------------------------------

### Configure Bitwarden SAML Identity Provider Settings

Source: https://bitwarden.com/help/cli/saml-keycloak

Details the fields required to configure Bitwarden's SAML identity provider settings, determining the format to expect for SAML responses.

```APIDOC
SAML identity provider configuration:
  Entity ID: Enter the URL of the Keycloak realm on which the client was created, for example https://<keycloak_domain>/realms/<realm_name>. This field is case sensitive.
  Binding type: Select Redirect.
  Single sign-on service URL: Enter your master SAML processing URL, for example https://<keycloak_domain>/realms/<realm_name>/protocol/saml.
  Single Log Out Service URL: Login with SSO currently does not support SLO. This option is planned for future development, however you may preconfigure it with your Logout URL if you wish.
  X509 public certificate: Enter the RS256 certificate that was copied in the previous step. The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters will cause certificate validation to fail.
  Outbound Signing Algorithm: Select the algorithm the Keycloak client is configured to use to sign SAML documents or assertions.
  Disable Outbound Logout Requests: Login with SSO currently does not support SLO. This option is planned for future development.
  Want Authentication Requests Signed: Whether Keycloak expects SAML requests to be signed.
```

--------------------------------

### Configure PostgreSQL Database in Bitwarden settings.env

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This snippet shows how to configure Bitwarden to use PostgreSQL as its database provider by setting environment variables in the `settings.env` file. It defines the database server, name, username, and password.

```Bash
# Database
BW_DB_PROVIDER=postgresql
BW_DB_SERVER=db
BW_DB_DATABASE=bitwarden_vault
BW_DB_USERNAME=bitwarden
BW_DB_PASSWORD=super_strong_password
```

--------------------------------

### Bitwarden Directory Connector: Sync Groups by Email Address with Wildcards

Source: https://bitwarden.com/help/cli/workspace-directory

Shows how to filter and sync groups based on their email address, supporting combinations with exclude filters and wildcard matching for partial email addresses.

```Bash
exclude:Group B|email:admin*
```

--------------------------------

### Bitwarden SIEM Event Log Fields Reference

Source: https://bitwarden.com/help/cli/monitoring-event-logs

This section details the common fields found within Bitwarden SIEM event logs, providing a description for each field to aid in data interpretation and monitoring.

```APIDOC
SIEM Event Fields:
  actingUserEmail: The email of the user performing the action.
  actingUserId: Unique id of user performing action.
  actingUserName: Name of the user performing an action.
  collectionId: Organization collection id.
  device: Numerical id of device. Exact mapping can be located at https://github.com/bitwarden/server/blob/d50ad97e6eeb733af9c069a949939b0567ba936d/src/Core/Enums/DeviceType.cs#L4.
  ipAddress: The ip address that performed the event.
  itemId: Vault item (cipher, secure note, etc..) of the organization vault.
  policyId: Organization policy update. See organization events at /help/event-logs/#organization-events.
```

--------------------------------

### Sync Bitwarden Directory Connector Groups by Exact Name

Source: https://bitwarden.com/help/cli/gsuite-directory

This snippet demonstrates how to include specific groups in a sync by listing their exact names, separated by commas. This is useful for syncing a predefined set of groups.

```Bash
include:Group A,Group B
```

--------------------------------

### Add Machine Account to Bitwarden Project

Source: https://bitwarden.com/help/cli/secrets-manager-quick-start

Instructions on how to create a machine account in Bitwarden, representing non-human users requiring programmatic access to secrets. This includes setting permissions for project access.

```APIDOC
Add Machine Account:
  1. Use the New dropdown to select Machine account.
  2. Enter a Machine account name and select Save.
  3. Open the machine account and, in the Projects tab, type or select the name of the project(s) this machine account should access.
  4. For each added project, select a level of Permissions:
    - Can read: Machine account can retrieve secrets from assigned projects.
    - Can read, write: Machine account can retrieve and edit secrets from assigned projects, as well as create new secrets or new projects.
```

--------------------------------

### Set Permissions for Firefox Policies Directory on Linux

Source: https://bitwarden.com/help/cli/deploy-clients

This command sets read, write, and execute permissions for the owner, and read and execute permissions for group and others, on the Firefox policies directory. This ensures that old administrators can still write files within the directory.

```Bash
chmod -R 755 /etc/firefox/policies
```

--------------------------------

### Extract Bitwarden Docker Stub Archive

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Extracts the contents of the Bitwarden Docker stub archive (e.g., `docker-stub-US.zip`) into a new `bwdata` directory. This directory structure is crucial as it matches the volume mappings expected by the `docker-compose.yml` file.

```Bash
unzip docker-stub-US.zip -d bwdata
```

--------------------------------

### Bitwarden Account Creation: Symmetric Key and RSA Pair Generation

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Describes the creation of the Protected Symmetric Key using AES-256 and CSPRNG, and the generation of an asymmetric RSA key pair during account registration.

```APIDOC
Function: GenerateProtectedSymmetricKey
  Description: Creates a 512-bit symmetric key and encrypts it.
  Parameters:
    stretched_master_key: 512-bit binary (Stretched Master Key)
  Process:
    1. GenerateSymmetricKeyAndIV(CSPRNG) -> 512-bit GeneratedSymmetricKey, 128-bit InitializationVector
    2. Encrypt(GeneratedSymmetricKey, AES-256, StretchedMasterKey, InitializationVector) -> ProtectedSymmetricKey
  Returns: ProtectedSymmetricKey (sent to server, main key associated with user)

Function: GenerateAsymmetricKeyPair
  Description: Creates an RSA public/private key pair.
  Returns: GeneratedRSAKeyPair (used for organization creation, emergency access)
```

--------------------------------

### Create Bitwarden Kerberos Configuration Directory

Source: https://bitwarden.com/help/cli/kerberos-integration

This command creates a dedicated directory within the Bitwarden data path to store Kerberos-related configuration files, such as the keytab and krb5.conf.

```Shell
mkdir /opt/bitwarden/bwdata/kerberos
```

--------------------------------

### Define SAML Attribute Statements in Okta for Bitwarden

Source: https://bitwarden.com/help/cli/saml-okta

Outlines the necessary SP to IdP attribute mappings to be configured in the Attribute Statements section of the Okta application for Bitwarden SAML integration.

```APIDOC
SP -> IdP Attribute Mappings:
  Description: Construct the necessary attribute mappings between the Service Provider (Bitwarden) and Identity Provider (Okta). Specific mappings are not detailed in text but are implied by the "Attribute Statements" section.
```

--------------------------------

### JumpCloud SAML Application General Info Configuration

Source: https://bitwarden.com/help/cli/saml-jumpcloud

Configures the display label for the Bitwarden application within the JumpCloud Portal's General Info section. This field is essential for identifying the application within JumpCloud.

```APIDOC
General Info Fields:
  Field: Display Label
  Description: Give the Application a Bitwarden-specific name.
```

--------------------------------

### Import Data to Bitwarden Vault using CLI

Source: https://bitwarden.com/help/cli/import-data

Commands for importing data into a Bitwarden vault via the command-line interface. The `bw import` command requires a specified format and the path to the import file. Use `bw import --formats` to list available formats.

```Bash
bw import <format> <path>
```

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Restart Bitwarden Docker Container (Docker Run)

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This snippet provides the sequence of commands to stop, remove, and then restart the Bitwarden Docker container using `docker run`. This is typically done after modifying environment variables or other container configurations to ensure changes take effect.

```Bash
docker stop bitwarden
docker rm bitwarden
docker run -d --name bitwarden -v /$(pwd)/bwdata/:/etc/bitwarden -p 80:8080 --env-file settings.env ghcr.io/bitwarden/self-host:beta
```

--------------------------------

### Use Bitwarden CLI with Alternate Config File and Profile

Source: https://bitwarden.com/help/cli/secrets-manager-cli

After configuring server settings with an alternate config file and profile, these can be used with other Bitwarden CLI commands to direct requests to the specified server and profile combination.

```Bash
bws secret get 2863ced6-eba1-48b4-b5c0-afa30104877a --config-file ~/.bws/alt_config --profile alt_dev
```

--------------------------------

### Bitwarden Desktop Application Keyboard Shortcuts

Source: https://bitwarden.com/help/cli/keyboard-shortcuts

This section details the keyboard shortcuts available for the Bitwarden desktop application, categorized by their function: General, File, Edit, View, and Window. These shortcuts provide quick access to common actions such as preferences, locking the app, adding new logins, editing entries, searching, and managing the application window.

```APIDOC
General:
  Ctrl/CMD + ,: Preferences
  Ctrl/CMD + L: Lock now
  Ctrl/CMD + Q: Quit
File:
  Ctrl/CMD + N: Add new login
Edit:
  Ctrl/CMD + Z: Undo
  Ctrl/CMD + Y: Redo
  Ctrl/CMD + X: Cut
  Ctrl/CMD + C: Copy
  Ctrl/CMD + V: Paste
  Ctrl/CMD + A: Select all
  Ctrl/CMD + U: Copy username
  Ctrl/CMD + P: Copy password
  Ctrl/CMD + T: Copy TOTP
View:
  Ctrl/CMD + F: Search in vault
  Ctrl/CMD + G: Password generator
  Ctrl/CMD + =: Zoom in
  Ctrl/CMD + -: Zoom out
  Ctrl/CMD + 0: Reset zoom
  F11: Full screen
  Ctrl/CMD + Shift + R: Reload
  F12: Developer options
Window:
  Ctrl/CMD + M: Minimize
  Ctrl/CMD + Shift + M: Send to tray/Hide to menu bar
  Ctrl/CMD + Shift + T: Always on top
  Ctrl/CMD + W: Close window
```

--------------------------------

### Configure OneLogin Role Inclusion for Directory Sync (Bash)

Source: https://bitwarden.com/help/cli/onelogin-directory

Use this command-line snippet to define which OneLogin roles should be included in the Bitwarden Directory Connector synchronization. Roles specified here will be synchronized, while others will be ignored unless explicitly included.

```Bash
include:Role A,Role B
```

--------------------------------

### Configure Git for GPG Signing and User Details

Source: https://bitwarden.com/help/cli/ssh-agent

Add GPG format, user signing key, name, and email to your global Git configuration for commit signing using SSH.

```Bash
[gpg]
        format = ssh
[user]
        signingkey = "<YOUR_PUBLIC_KEY>"
        name = <USER_NAME>
        email = <USER_EMAIL>
[commit]
        gpgsign = true
```

--------------------------------

### Bitwarden Mobile App Permissions

Source: https://bitwarden.com/help/cli/security-faqs

Details the specific permissions requested by Bitwarden Android and iOS mobile applications and the corresponding reasons for each permission, such as scanning QR codes or accessing device media for attachments.

```APIDOC
Mobile App Permissions:
  - Permission: "Allow Bitwarden to take pictures and record video?"
    Reason: "To scan QR codes for two-step login or Bitwarden authenticator."
  - Permission: "Allow Bitwarden to access photos and media on your device?"
    Reason: "To create attachments or Sends from a file saved on your device."
```

--------------------------------

### Configure Key Connector for Filesystem Certificate Storage

Source: https://bitwarden.com/help/cli/deploy-key-connector

This snippet configures Bitwarden Key Connector to use a .pfx certificate file stored on the local filesystem. It specifies the certificate provider as 'filesystem' and requires the full path to the certificate file and its password.

```Bash
keyConnectorSettings__rsaKey__provider=certificate
keyConnectorSettings__certificate__provider=filesystem
keyConnectorSettings__certificate__filesystemPath={Certificate_Path}
keyConnectorSettings__certificate__filesystemPassword={Certificate_Password}
```

--------------------------------

### Bitwarden CLI: Retrieve Notes and Configure Sends

Source: https://bitwarden.com/help/cli/releasenotes

New Bitwarden CLI options allow users to easily retrieve notes from a Vault item using its ID and to set a maximum access count for 'Send' items during creation.

```CLI
bw get notes <id>
```

```CLI
bw send create --maxAccessCount <#>
```

--------------------------------

### Bitwarden Mail (SMTP) Configuration Variables

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This section details environment variables for configuring SMTP settings in `settings.env` for a Bitwarden unified deployment. It includes variables for reply-to email, SMTP host, port, SSL usage, username, and password.

```APIDOC
globalSettings__mail__replyToEmail: Enter the reply email for your server.
globalSettings__mail__smtp__host: Enter host domain for your SMTP server.
globalSettings__mail__smtp__port: Enter the port number from the SMTP host.
globalSettings__mail__smtp__ssl: If your SMTP host uses SSL enter true. Set value to false if your host uses TLS service.
globalSettings__mail__smtp__username: Enter the SMTP username.
globalSettings__mail__smtp__password: Enter the SMTP password.
```

--------------------------------

### Duo Admin Portal: Protecting the Bitwarden Application

Source: https://bitwarden.com/help/cli/saml-duo

Instructions for configuring the Bitwarden application within the Duo Admin Portal, ensuring it is protected by Duo's Single Sign-On service.

```APIDOC
Duo Admin Portal:
  - Navigate to the "Applications" screen.
  - Select "Protect an Application".
  - Enter "Bitwarden" into the search bar.
  - Select "Configure" for the "Bitwarden 2FA with SSO hosted by Duo" application.
  - Select "Activate and Start Setup" for the newly created application.
```

--------------------------------

### Manage multiple Bitwarden CLI accounts with aliases

Source: https://bitwarden.com/help/cli/cli

Describes how to log in to multiple accounts simultaneously, similar to account switching in other Bitwarden apps. This is achieved by using the `BITWARDENCLI_APPDATA_DIR` environment variable to point to different configuration files, typically `data.json`, and setting up Bash aliases for convenience.

```Bash
alias bw-personal="BITWARDENCLI_APPDATA_DIR=~/.config/Bitwarden\ CLI\ Personal /path/to/bw $@"
alias bw-work="BITWARDENCLI_APPDATA_DIR=~/.config/Bitwarden\ CLI\ Work /path/to/bw $@"
```

--------------------------------

### Bitwarden CLI: Receive a Send

Source: https://bitwarden.com/help/cli/send-cli

The `receive` command accesses and retrieves the contents of a Send. It requires the Send's URL as an argument. For text Sends, it returns the text; for file Sends, it downloads the file to the current directory. Options include `--password`, `--passwordenv`, or `--passwordfile` for protected Sends, `--obj` to output the full Send object as JSON, and `--output` to specify a download directory for file Sends.

```Bash
bw send receive [options] <url>
```

--------------------------------

### SAML Attribute and Claim Reference for Bitwarden Provisioning

Source: https://bitwarden.com/help/cli/configure-sso-saml

This reference table specifies the SAML attributes and claims used by Bitwarden for account provisioning. An email address is mandatory, and a unique user identifier is highly recommended. Attributes are listed with their preferred and fallback options.

```APIDOC
SAML Attributes & Claims:

- Unique ID:
  - Claim/Attribute: NameID (when not transient), urn:oid:0.9.2342.19200300.100.1.1, Sub UID, UPN, EPPN
  - Fallback claim/attribute: None

- Email:
  - Claim/Attribute: Email, http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress, urn:oid:0.9.2342.19200300.100.1.3, Mail, EmailAddress
  - Fallback claim/attribute: Preferred_Username, Urn:oid:0.9.2342.19200300.100.1.1, UID

- Name:
  - Claim/Attribute: Name, http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name, urn:oid:2.16.840.1.113730.3.1.241, urn:oid:2.5.4.3, DisplayName, CN
  - Fallback claim/attribute: First Name + " " + Last Name

- First Name:
  - Claim/Attribute: urn:oid:2.5.4.42, GivenName, FirstName, FN, FName, Nickname
  - Fallback claim/attribute: None

- Last Name:
  - Claim/Attribute: urn:oid:2.5.4.4, SN, Surname, LastName
  - Fallback claim/attribute: None
```

--------------------------------

### Enable Cloud Communication

Source: https://bitwarden.com/help/cli/environment-variables

Set to `true` to allow communication between your self-hosted server and the Bitwarden cloud system. This enables features like billing and license synchronization.

```APIDOC
globalSettings__enableCloudCommunication=true
```

--------------------------------

### Email Template for Appointing a Bitwarden Implementation Champion

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

A template to encourage appointing a cybersecurity champion to accelerate password management adoption, detailing their responsibilities and impact on user engagement.

```Email
Subject: Appoint an implementation champion

Body: Hi [name],

A designated cybersecurity champion can accelerate password management adoption across your organization. This person will rally feedback, suggestions, and overall excitement for your new tool! By appointing an implementation champion, or even a bench of experts, you can ensure someone is always available to answer questions or provide guidance.

Your implementation champion should be empowered to:
* Host workshops or open office hours to review [Bitwarden Learning] material with users.
* Help teams set up collections through use of a [member role] such as manager or the custom role.
* Assist users in downloading [Bitwarden clients] to all their devices.

An implementation champion can significantly increase user adoption, and will have your organization on the road to password security in no time!
```

--------------------------------

### Bitwarden Web App: Service Provider Configuration Fields

Source: https://bitwarden.com/help/cli/saml-duo

Outlines the fields to configure within the Bitwarden web application's Single Sign-On screen. These settings define how Bitwarden expects SAML requests and responses to be formatted and signed from the Identity Provider (Duo).

```APIDOC
Field: Name ID Format
Description: [NameID Format](https://docs.oracle.com/cd/E19316-01/820-3886/ggvxx/index.html) to use in the SAML request (`NameIDPolicy`). Set this field to [the selected NameID format](#saml-response).

Field: Outbound Signing Algorithm
Description: Algorithm used to sign SAML requests, by default `rsa-sha256`.

Field: Signing Behavior
Description: Whether/when SAML requests will be signed. By default, Duo will not require requests to be signed.

Field: Minimum Incoming Signing Algorithm
Description: The minimum signing algorithm Bitwarden will accept in SAML responses. By default, Duo will sign with `rsa-sha256`, so choose that option from the dropdown unless you have [selected a different option](#saml-response).

Field: Want Assertions Signed
Description: Whether Bitwarden wants SAML assertions signed. Check this box if you [selected the](#saml-response).

Field: Validate Certificates
Description: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured within the Bitwarden Login with SSO docker image.
```

--------------------------------

### Bitwarden Directory Connector: Sync Groups by Member Key

Source: https://bitwarden.com/help/cli/workspace-directory

Illustrates syncing all groups to which a specific user, identified by their member key (e.g., email address), has membership. Wildcards can also be used in this context.

```Bash
|memberKey=user@company.com
```

--------------------------------

### Download a file using Bitwarden CLI

Source: https://bitwarden.com/help/cli/attachments

This command downloads a specific file attachment from a Bitwarden vault item. You must provide the filename, the --itemid of the vault item, and optionally the --output directory where the file will be saved. If --output is not specified, the file might be saved to the current directory.

```Bash
bw get attachment photo.png --itemid 99ee88d2-6046-4ea7-92c2-acac464b1412 --output /Users/myaccount/Pictures/
```

--------------------------------

### Export Identity Server Certificate to PFX Format

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Converts the previously generated `identity.key` and `identity.crt` into a PKCS#12 (`.pfx`) file, which is the required format for the Bitwarden Identity container. The `IDENTITY_CERT_PASSWORD` must be replaced with the secure password configured in `globalSettings__identityServer__certificatePassword`.

```Bash
openssl pkcs12 -export -out ./identity/identity.pfx -inkey identity.key -in identity.crt -passout pass:IDENTITY_CERT_PASSWORD
```

--------------------------------

### Configure Firefox to Force-Install Bitwarden Extension on macOS

Source: https://bitwarden.com/help/cli/browserext-deploy

This XML snippet, to be added to `org.mozilla.firefox.plist`, configures Firefox to force-install the Bitwarden browser extension using its extension ID and the Mozilla Add-ons store URL. It ensures the extension is always present for managed users.

```XML
<key>ExtensionSettings</key>
<dict>
   <key>446900e4-71c2-419f-a6a7-df9c091e268b</key>
   <dict>
     <key>installation_mode</key>
     <string>force_installed</string>
     <key>update_url</key>
     <string>https://addons.mozilla.org/firefox/downloads/latest/bitwarden-password-manager/latest.xpi</string>
   </dict>
 </dict>
```

--------------------------------

### Understand Bitwarden Web App SSO Configuration Sections

Source: https://bitwarden.com/help/cli/saml-jumpcloud

Upon returning to the Bitwarden web vault, the SSO screen is divided into two main sections: SAML service provider configuration for requests and SAML identity provider configuration for responses.

```APIDOC
Bitwarden Web App SSO Configuration Sections:
  SAML service provider configuration:
    Purpose: Determines the format of SAML requests.
  SAML identity provider configuration:
    Purpose: Determines the format to expect for SAML responses.
```

--------------------------------

### Enable Debug Mode for Bitwarden Directory Connector CLI

Source: https://bitwarden.com/help/cli/directory-sync-cli

This environment variable can be added to enable debug mode, providing additional troubleshooting information for the Bitwarden Directory Connector CLI.

```Plain
export BITWARDENCLI_CONNECTOR_DEBUG=true
```

--------------------------------

### Log In Using Bitwarden Autofill on Android

Source: https://bitwarden.com/help/cli/getting-started-mobile

Describes how to use Bitwarden's autofill feature to log into apps or websites on Android after autofill and biometrics have been set up. It covers tapping input fields, selecting the Bitwarden overlay, and authenticating.

```Android
1. Tap the email/username or password input box in the app or website.
2. Depending on which auto-fill option your device uses, tap the available overlay.
3. You will be prompted for your face authentication or fingerprint. If you aren't using biometrics, enter your master password.
4. If you have connected a login to this website or app using the URI field, that login will appear in this window. If you haven't, tap Search to find it.

Tap the login to automatically enter your email/username and password into the boxes, and sign in.
```

--------------------------------

### List Bitwarden Secrets with Environment Variable Output Format

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command lists secrets and formats them in `KEY=VALUE` format suitable for environment variables using the `--output env` flag. Non-POSIX-compliant key names will be commented out in the output.

```Bash
bws secret list --output env
```

--------------------------------

### Default User Attribute Mappings for SCIM Provisioning

Source: https://bitwarden.com/help/cli/microsoft-entra-id-scim-integration

Describes the default attribute mappings between Bitwarden SCIM attributes and Microsoft Entra ID attributes for user objects during provisioning.

```APIDOC
- Bitwarden attribute: active
  Default AAD attribute: Switch([IsSoftDeleted], , "False", "True", "True", "False")
- Bitwarden attribute: emailsª or userName
  Default AAD attribute: mail or userPrincipalName
- Bitwarden attribute: displayName
  Default AAD attribute: displayName
- Bitwarden attribute: externalId
  Default AAD attribute: mailNickname
```

--------------------------------

### Authenticate Bitwarden CLI with Personal API Key

Source: https://bitwarden.com/help/cli/personal-api-key

This command initiates a prompt for your personal `client_id` and `client_secret` to log in to the Bitwarden CLI using your API key. This method is recommended for automated workflows or external applications.

```Bash
bw login --apikey
```

--------------------------------

### Bitwarden Directory Connector: Include Specific Groups by Name

Source: https://bitwarden.com/help/cli/workspace-directory

Filter Bitwarden Directory Connector sync to include only specified groups by their exact names. Multiple groups can be listed, separated by commas.

```Bash
include:Group A,Group B
```

--------------------------------

### Add Secrets to Bitwarden Project

Source: https://bitwarden.com/help/cli/secrets-manager-quick-start

Instructions on how to add sensitive key-value pairs (secrets) to a Bitwarden project, either by importing a JSON file or manually entering them. Secrets include API Keys, Application Configurations, Database Connection Strings, and Environment Variables.

```APIDOC
Add Secrets:
  Import secrets:
    1. Review document for proper import file formatting: /help/import-secrets-data/
    2. Select Settings -> Import data from left-hand navigation.
    3. Select Choose File and choose a .json file for import.
  Add secrets manually:
    1. Use the New dropdown to select Secret.
    2. In the New Secret window, enter a Name and Value. Notes are optional.
    3. In the Project section, type or select the project to associate the secret with.
      - Each secret can only be associated with a single project.
      - Only organization members with access to the project can see/manipulate this secret.
      - Only machine accounts with access to the project can create a pathway for injecting this secret.
    4. Select the Save button.
```

--------------------------------

### Log in to Bitwarden CLI Interactively with Email and Password

Source: https://bitwarden.com/help/cli/cli

This command initiates an interactive login process for the Bitwarden CLI, prompting for your email address, master password, and a two-step login code if enabled. It is the recommended method for interactive user sessions.

```Bash
bw login
```

--------------------------------

### OneLogin SSO Details: Certificate, Algorithms, and Endpoints

Source: https://bitwarden.com/help/cli/saml-onelogin

Outlines the process of retrieving the X.509 PEM Certificate, setting the SAML Signature Algorithm, and noting the Issuer URL and SAML 2.0 Endpoint from OneLogin for Bitwarden SSO configuration.

```APIDOC
X.509 Certificate:
  Action: Download or copy your X.509 PEM Certificate from the Certificate screen.
  Usage: Needed for Identity Provider Configuration in Bitwarden.
SAML Signature Algorithm:
  Action: Set your SAML Signature Algorithm.
Issuer URL:
  Action: Take note of this value.
  Usage: Needed for Identity Provider Configuration in Bitwarden.
SAML 2.0 Endpoint (HTTP):
  Action: Take note of this value.
  Usage: Needed for Identity Provider Configuration in Bitwarden.
```

--------------------------------

### Configure Environment Variables for Self-Hosted EU Server

Source: https://bitwarden.com/help/cli/server-geographies

To connect a self-hosted Bitwarden instance to the EU cloud server, add these environment variables to the `./bwdata/env/global.override.env` file. These settings ensure communication with the correct EU server endpoints for identity, API, and push relay services.

```Bash
globalSettings__baseServiceUri__cloudRegion=EU
globalSettings__installation__identityUri=https://identity.bitwarden.eu
globalSettings__installation__apiUri=https://api.bitwarden.eu
globalSettings__pushRelayBaseUri=https://push.bitwarden.eu
```

--------------------------------

### Generate Kerberos Keytab File (Windows Domain Controller)

Source: https://bitwarden.com/help/cli/kerberos-integration

This command generates a keytab file on a Windows Domain Controller, which is used by the Bitwarden server for domain authentication. The command creates a principal for Bitwarden, maps it to a user, and outputs the keytab file.

```Shell
ktpass /princ bitwarden@<EXAMPLE.DOMAIN> /mapuser "bitwarden" /pass super_secure_password_here /out bitwarden.keytab /crypto all /ptype KRB5_NT_PRINCIPAL /mapop set
```

--------------------------------

### Configure MSSQL Database in Bitwarden settings.env

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This snippet demonstrates how to configure Bitwarden to use MSSQL as its database provider by setting environment variables in the `settings.env` file. It includes settings for the database server, name, username, and password.

```Bash
# Database
BW_DB_PROVIDER=sqlserver
BW_DB_SERVER=db
BW_DB_DATABASE=bitwarden_vault
BW_DB_USERNAME=bitwarden
BW_DB_PASSWORD=super_strong_password
```

--------------------------------

### Bitwarden Identity Provider Configuration Fields for Okta SAML SSO

Source: https://bitwarden.com/help/cli/saml-okta

Details the required fields and their descriptions for configuring an identity provider (Okta) within Bitwarden for SAML-based Single Sign-On. Includes notes on case sensitivity, supported binding types, and certificate handling.

```APIDOC
Identity Provider Configuration Fields:
  Entity ID:
    Description: Your Identity Provider Issuer, retrieved from the Okta Sign On Settings screen. This field is case sensitive.
  Binding Type:
    Description: Set to Redirect. Okta currently does not support HTTP POST.
  Single Sign On Service URL:
    Description: Your Identity Provider Single Sign-On URL, retrieved from the Okta Sign On Settings screen.
  Single Log Out Service URL:
    Description: Login with SSO currently does not support SLO. This option is planned for future development, but can be pre-configured.
  X509 Public Certificate:
    Description: Paste the downloaded certificate, removing -----BEGIN CERTIFICATE----- and -----END CERTIFICATE-----. The certificate value is case sensitive; extra spaces, carriage returns, and other extraneous characters will cause certification validation to fail.
  Outbound Signing Algorithm:
    Description: Select the Signature Algorithm selected during Okta app configuration. Default is rsa-sha256.
  Allow outbound logout requests:
    Description: Login with SSO currently does not support SLO.
  Want Authentication Requests Signed:
    Description: Whether Okta expects SAML requests to be signed.
```

--------------------------------

### Default NGINX Container SSL Path Mappings

Source: https://bitwarden.com/help/cli/certificates

Illustrates the default paths within the NGINX container for SSL certificate files, which map to host directories on the Bitwarden server.

```Bash
ssl_certificate_path: /etc/ssl/your.domain/certificate.crt
ssl_key_path: /etc/ssl/your.domain/private.key
ssl_ca_path: /etc/ssl/your.domain/ca.crt
```

--------------------------------

### Duo Portal: SAML Response Configuration Fields

Source: https://bitwarden.com/help/cli/saml-duo

Describes the fields for configuring the SAML response format within the Duo Admin Portal. These settings dictate how Duo constructs and signs the SAML assertions sent to Bitwarden.

```APIDOC
Field: NameID format
Description: Set this field to the [SAML NameID format](https://docs.oracle.com/cd/E19316-01/820-3886/ggwbz/index.html) for Duo to send in SAML responses.

Field: NameID attribute
Description: Set this field to the Duo attribute that will populate the NameID in responses.

Field: Signature algorithm
Description: Set this field to the encryption algorithm to use for SAML assertions and responses.

Field: Signing options
Description: Select whether to **Sign response**, **Sign assertion**, or both.

Field: Map attributes
Description: Use these fields to map IdP attributes to SAML response attributes. Regardless of which NameID attribute you configured, map the IdP `Email Address` attribute to `Email`, as in the following screenshot:
```

--------------------------------

### Create Kubernetes Namespace for Bitwarden

Source: https://bitwarden.com/help/cli/self-host-with-helm

This command creates a dedicated Kubernetes namespace named 'bitwarden' for deploying the Bitwarden application. Using a specific namespace helps organize resources and avoid conflicts within your Kubernetes cluster.

```Bash
kubectl create namespace bitwarden
```

--------------------------------

### Bitwarden Directory Connector Sync Configuration Options

Source: https://bitwarden.com/help/cli/ldap-directory

This section details the various configuration options available within the Bitwarden Directory Connector's 'Sync' settings tab. It covers parameters for automatic sync intervals, user/group removal, user/group count limits, and attribute mappings for user and group properties.

```APIDOC
Interval: Time between automatic sync check (in minutes).
Remove disabled users during sync (Not available for LDAP): Check this box to remove users from the Bitwarden organization that have been disabled in your organization.
More than 2000 users or groups are expected to sync: Check this box if you expect to sync 2000+ users or groups. If you don't check this box, Directory Connector will limit a sync at 2000 users or groups.
Member Attribute: Name of the attribute used by the directory to define a group's membership (for example, `uniqueMember`).
Creation Data Attribute: Name of the attribute used by the directory to specify when an entry was created (for example, `whenCreated`).
Revision Date Attribute: Name of the attribute used by the directory to specify when an entry was last changed (for example, `whenChanged`).
If a user has no email address, combine a username prefix with a suffix value to form an email: Check this box to form valid email options for users that do not have an email address. This option is available after selecting **This server uses Active Directory**.  **Users without real or formed email addresses will be skipped by Directory Connector.**  Formed Email = **Email Prefix Attribute** + **Email Suffix**
Email Prefix Attribute: Attribute used to create a prefix for formed email addresses.
Email Suffix: A string (`@example.com`) used to create a suffix for formed email addresses.
Sync users: Check this box to sync users to your organization.  Checking this box will allow you to specify a **User Filter**, **User Path**, **User Object Class**, and **User Email Attribute**.
User Filter: See [Specify sync filters](#specify-sync-filters).
User Path: Attribute used with the specified **Root Path** to search for users (for example, `ou=users`). If no value is supplied, the subtree search will start from the root path.
User Object Class: Name of the class used for the LDAP user object (for example, `user`).
User Email Attribute: Attribute to be used to load a user's stored email address.
Sync groups: Check this box to sync groups to your organization.  Checking this box will allow you to specify a **Group Filter**, **Group Path**, **Group Object Class**, **Group Name Attribute**.
Group Filter: See [Specify sync filters](#specify-sync-filters).
Group Path: Attribute used with the specified **Root Path** to search for groups (for example, `ou=groups`). If no value is supplied, the subtree search will start from the root path.
Group Object Class: Name of the class used for the LDAP group object (for example, `groupOfUniqueNames`).
Group Name Attribute: Name of the attribute used by the directory to define the name of a group (for example, `name`).
```

--------------------------------

### Access Bitwarden Global Override Environment File

Source: https://bitwarden.com/help/cli/kerberos-integration

This command opens the `global.override.env` file for editing using the nano text editor. This file is used to add additional environment variables to Bitwarden's configuration.

```Shell
nano ~/global.override.env/
```

--------------------------------

### Bitwarden SAML Service Provider Configuration Fields

Source: https://bitwarden.com/help/cli/saml-auth0

Details the fields required for configuring the service provider (Bitwarden) side of the SAML integration, including Name ID Format, signing algorithms, and certificate validation.

```APIDOC
Service Provider Configuration:
  Name ID Format:
    Description: NameID Format to specify in the SAML request (NameIDPolicy). To omit, set to Not Configured.
  Outbound Signing Algorithm:
    Description: Algorithm used to sign SAML requests, by default rsa-sha256.
  Signing Behavior:
    Description: Whether/when Bitwarden SAML requests will be signed. By default, Auth0 will not require requests to be signed.
  Minimum Incoming Signing Algorithm:
    Description: The minimum signing algorithm Bitwarden will accept in SAML responses. Select rsa-sha256 from the dropdown unless you have configured a custom signing rule.
  Want Assertions Signed:
    Description: Whether Bitwarden wants SAML assertions signed. By default, Auth0 will sign SAML assertions, so check this box unless you've configured a custom signing rule.
  Validate Certificates:
    Description: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured within the Bitwarden Login with SSO docker image.
```

--------------------------------

### Duo SAML X.509 Certificate Download

Source: https://bitwarden.com/help/cli/saml-duo

Instructions for downloading the X.509 Certificate from the Duo Admin Portal, a critical component for establishing trust between Duo and Bitwarden during SAML configuration.

```APIDOC
Duo SAML X.509 Certificate:
  - Action: Select the "Download certificate" button in the Duo Admin Portal.
  - Purpose: Download your X.509 Certificate, which will be used later in the Bitwarden configuration.
```

--------------------------------

### Directory Connector Server Connection Options

Source: https://bitwarden.com/help/cli/ldap-directory

Configuration parameters for connecting Bitwarden Directory Connector to an LDAP or Active Directory server. These options define how the connector establishes and secures its connection to your directory service.

```APIDOC
Server Connection Options:
  Server Hostname:
    description: Hostname of your directory server.
    examples: ad.example.com, ldap.company.org
  Server Port:
    description: Port on which your directory server is listening.
    examples: 389 or 10389
  Root Path:
    description: Root path at which Directory Connector should start all queries.
    examples: cn=users, dc=ad, dc=example, dc=com or dc=ldap, dc=company, dc=org
  This server uses active directory:
    description: Check this box if the server is an Active Directory server.
  This server pages search results:
    description: Check this box if the server paginates search results (LDAP only).
  This server uses an encrypted connection:
    description: Checking this box will prompt you to select one of the following options: Use SSL (LDAPS) If your LDAPS server uses an untrusted certificate, you can configure certificate options on this screen. Use TSL (STARTTLS) If your LDAP server uses a self-signed certificate for STARTTLS, you can configure certification options on this screen.
  Username:
    description: The distinguished name of an administrative user that the application will use when connecting to the directory server. For Active Directory, if synchronizing the status of users removed from the directory is desired, the user should be a member of the built-in administrator group.
  Password:
    description: The password of the user specified above. The password is safely stored in the operating system's native credential manager.
```

--------------------------------

### Configure Self-Signed Certificate Paths in config.yml

Source: https://bitwarden.com/help/cli/certificates

Shows the `config.yml` settings for referencing a self-signed certificate and its private key within the Bitwarden server configuration.

```Bash
ssl_certificate_path: /etc/ssl/bitwarden.example.com/certificate.crt
 ssl_key_path: /etc/ssl/bitwarden.example.com/private.key
```

--------------------------------

### Configure Bitwarden CLI Server with a Specific Profile

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command saves server settings to an alternate profile, allowing users to manage multiple server configurations. The `--profile` option specifies the name of the profile to use or create.

```Bash
bws config server-base http://other_hosted_server.com --profile dev
```

--------------------------------

### Bitwarden CLI Search: Term Presence Queries

Source: https://bitwarden.com/help/cli/searching-vault

Demonstrates how to use '+' and '-' prefixes for term presence in Bitwarden CLI search queries. This allows for precise inclusion or exclusion of terms, and can be used to create exact matches for multi-term phrases.

```Bitwarden
>+name:Gmail +name:Work
```

```Bitwarden
>+name:5 +name:mail +name:01
```

--------------------------------

### OneLogin SCIM API Connection Parameters

Source: https://bitwarden.com/help/cli/onelogin-scim-integration

Defines the required API connection settings within OneLogin for integrating with Bitwarden's SCIM provisioning, including the SCIM base URL and bearer token. These values are retrieved from the Bitwarden Admin Console.

```APIDOC
API Connection Settings:
  SCIM base URL: Set this field to the SCIM URL (retrieved from Bitwarden's SCIM provisioning settings).
  SCIM bearer token: Set this field to the SCIM API key (retrieved from Bitwarden's SCIM provisioning settings).
```

--------------------------------

### Bitwarden CLI API Key Environment Variables

Source: https://bitwarden.com/help/cli/cli

These environment variables (`BW_CLIENTID`, `BW_CLIENTSECRET`) can be set to provide API key credentials to the Bitwarden CLI. Using them prevents the need for manual intervention during authentication in automated workflows.

```APIDOC
BW_CLIENTID: client_id (Required)
BW_CLIENTSECRET: client_secret (Required)
```

--------------------------------

### Bitwarden Webpage URLs

Source: https://bitwarden.com/help/cli/bitwarden-addresses

Provides a list of URLs used for accessing Bitwarden's main website and related content delivery networks.

```APIDOC
bitwarden.com
bitwarden.net
btwrdn.com
start.bitwarden.com
go.bitwarden.com
cdn.bitwarden.com
cdn.bitwarden.net
```

--------------------------------

### Email Template for Bitwarden Company-Wide Deployment

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

Provides a pre-written email to introduce Bitwarden Password Manager for company-wide deployment, highlighting key benefits and next steps for users.

```Email
Subject: Introducing Bitwarden password manager for company-wide deployment

Body: Hi team, we are happy to announce the company-wide deployment of Bitwarden Password Manager. Bitwarden is a respected, industry-leading company with a strong security record.

You will find Bitwarden to be simple and easy to use.

Here are three reasons we're excited to get you on Bitwarden:
1. Easily access all your passwords anytime, anywhere, on any device.
2. Securely share credentials with others.
3. Streamline logging into your accounts with auto-fill.

You will receive an invite via email to join Bitwarden.
```

--------------------------------

### Configure Bitwarden Extension Force-Install for Chrome via GPO

Source: https://bitwarden.com/help/cli/browserext-deploy

This snippet provides the extension ID and update URL required to force-install the Bitwarden browser extension for Google Chrome using Windows Group Policy. This ensures the extension is automatically deployed and updated on managed machines.

```Configuration
nngceckbapebfimnlniiiahkandclblb;https://clients2.google.com/service/update2/crx
```

--------------------------------

### Configure Microsoft Edge to Force-Install Bitwarden Extension on macOS

Source: https://bitwarden.com/help/cli/browserext-deploy

This XML snippet, to be added to `com.microsoft.Edge.plist`, configures Microsoft Edge to force-install the Bitwarden browser extension using its application identifier and the Edge Add-On Store URL. This ensures the extension is always available for managed users.

```XML
<key>ExtensionSettings</key>
<dict>
  <key>jbkfoedolllekgbhcbcoahefnbanhhlh</key>
  <dict>
    <key>installation_mode</key>
    <string>force_installed</string>
    <key>update_url</key>
    <string>https://edge.microsoft.com/extensionwebstorebase/v1/crx</string>
  </dict>
</dict>
```

--------------------------------

### Generate Password using Bitwarden CLI

Source: https://bitwarden.com/help/cli/generator

This snippet demonstrates how to generate a strong password using the Bitwarden Command Line Interface (CLI). It uses the `generate` command with flags to include uppercase, lowercase, numbers, and specify a length of 14 characters. Additional options like `--minNumber`, `--minSpecial`, and `--ambiguous` are also mentioned for further customization.

```Bash
bw generate -uln --length 14
```

--------------------------------

### Import Data to Bitwarden Vault via CLI

Source: https://bitwarden.com/help/cli/import-from-chrome

This command is used to import data into a Bitwarden vault through the command-line interface. It requires specifying the file format and the path to the import file. Use `bw import --formats` to see available formats.

```Bash
bw import <format> <path>
```

--------------------------------

### Logging In with a Trusted Device: Decryption Process

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Explains the sequence of operations when a user logs in using a previously trusted device, focusing on how the client retrieves and decrypts the account encryption key using various encrypted keys from the server and the local device key to access vault data.

```APIDOC
1. The user's Public Key-Encrypted User Key, which is an encrypted version of the account encryption key used to decrypt vault data, is sent from the server to the client.
2. The user's Device Key-Encrypted Private Key, the unencrypted version of which is required to decrypt the Public Key-Encrypted User Key, is sent from the server to the client.
3. The client decrypts the Device Key-Encrypted Private Key using the Device Key, which never leaves the client.
4. The now-unencrypted Device Private Key is used to decrypt the Public Key-Encrypted User Key, resulting in the user's account encryption key.
5. The user's account encryption key decrypts vault data.
```

--------------------------------

### Disable Automatic Database Preparation for External Databases

Source: https://bitwarden.com/help/cli/database-options

This environment variable, set in `global.override.env`, deactivates the automatic database creation step for non-unified self-host deployments. This is useful when deploying your own external database and you prefer to manage its creation manually. The configured SQL user must have administrative privileges if this step is not deactivated.

```Plain
globalSettings__sqlServer__skipDatabasePreparation=true
```

--------------------------------

### Configure Bitwarden Browser Extension for EU Cloud

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This snippet shows the "base" and "notifications" settings required to centrally deploy the Bitwarden browser extension to EU servers. These settings ensure the extension connects to the specified EU cloud endpoints, even when displaying 'self-hosted' status.

```Plain
"base": "https://vault.bitwarden.eu"
"notifications": "https://notifications.bitwarden.eu"
```

--------------------------------

### Bitwarden CLI `move` Command

Source: https://bitwarden.com/help/cli/releasenotes

The Bitwarden CLI `share` command has been updated to `move` to align with the new 'Move to Organization' terminology for shared items, clarifying ownership.

```CLI
bw move
```

--------------------------------

### Add Kerberos User to Bitwarden Global Override Environment

Source: https://bitwarden.com/help/cli/kerberos-integration

This snippet adds the `globalSettings__kerberosUser` variable to the `global.override.env` file. This variable specifies the Active Directory user that Bitwarden will use to authenticate with the domain for Kerberos integration.

```Text
globalSettings__kerberosUser=bitwarden
```

--------------------------------

### Auth0 `api.saml.updateConfiguration` Method Attributes

Source: https://bitwarden.com/help/cli/saml-auth0

This API documentation details the configurable parameters for the `api.saml.updateConfiguration` method used within Auth0 actions. It describes each attribute's purpose, expected values, and implications for SAML assertion and response signing, and name identifier formatting.

```APIDOC
api.saml.updateConfiguration(options: object)
  options:
    signatureAlgorithm: string
      Description: Algorithm Auth0 will use to sign the SAML assertion or response. This value should be set to `rsa-sha256`. You must also set: -Set `digestAlgorithm` to `sha256`. -Set (in Bitwarden) the **Minimum Incoming Signing Algorithm** to `rsa-sha256`.
    digestAlgorithm: string
      Description: Algorithm used to calculate digest of SAML assertion or response. Set to `sha-256`.
    signResponse: boolean
      Description: By default, Auth0 will sign only the SAML assertion. Set this to `true` to sign the SAML response instead of the assertion.
    nameIdentifierFormat: string
      Description: By default, `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`. You can set this value to [any SAML NameID format](https://docs.oracle.com/cd/E19316-01/820-3886/ggwbz/index.html). If you do, change the SP **Name ID Format** field to the corresponding option (see [here](#service-provider-configuration)).
```

--------------------------------

### Configure Key Connector for Google Cloud KMS RSA Key Storage

Source: https://bitwarden.com/help/cli/deploy-key-connector

Specifies environment variables for Bitwarden Key Connector to use Google Cloud KMS for RSA 2048 key pair storage. This includes project, location, keyring, key, and key version IDs.

```Bash
keyConnectorSettings__rsaKey__provider=gcpkms
keyConnectorSettings__rsaKey__googleCloudProjectId={Project_Id}
keyConnectorSettings__rsaKey__googleCloudLocationId={Location_Id}
keyConnectorSettings__rsaKey__googleCloudKeyringId={Keyring_Id}
keyConnectorSettings__rsaKey__googleCloudKeyId={Key_Id}
keyConnectorSettings__rsaKey__googleCloudKeyVersionId={KeyVersionId}
```

--------------------------------

### Configure Bitwarden CLI Server with Alternate Config File and Profile

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command combines the `--config-file` and `--profile` options to save server settings to a specific profile within an alternate configuration file. This offers granular control over CLI environments.

```Bash
bws config server-base http://third_hosted_server.com --config-file ~/.bws/alt_config --profile alt_dev
```

--------------------------------

### Configure Bitwarden Browser Extension for EU Cloud

Source: https://bitwarden.com/help/cli/deploy-clients

To centrally deploy the Bitwarden browser extension to EU servers, the 'base' and 'notifications' URLs must be explicitly set to the EU cloud endpoints. This ensures the extension connects to the correct regional servers.

```Plain
"base": "https://vault.bitwarden.eu"
"notifications": "https://notifications.bitwarden.eu"
```

--------------------------------

### Update Bitwarden Container Image References for Self-Hosting

Source: https://bitwarden.com/help/cli/releasenotes

For self-hosting Bitwarden instances not using the bitwarden.sh or bitwarden.ps1 deployment scripts, update existing container image references from Docker Hub to the new GitHub Container Registry URLs. This ensures continued access to the latest images.

```Shell
ghcr.io/bitwarden/image_name:version
```

--------------------------------

### Communicate Rollout Plan Email Template

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

Provides a template for an email to inform end-users about the implementation plan for a new password manager, detailing expectations and required actions to ensure a smooth rollout.

```Email
Subject: Communicate your rollout plan

Body:

Hi *[name]*,

Put end-users at ease by communicating the implementation plan for your new password manager far in advance.

* Let employees know exactly what to expect.
* Communicate specific action items they will need to complete, and the due data. This will help ensure a smooth rollout for your employees.

Here's a [sample implementation plan](/help/prepare-your-org-for-prod/) you can use as a guide - just download them and customize them to work for your organization.
```

--------------------------------

### Configure JumpCloud Identity Management for Bitwarden SCIM

Source: https://bitwarden.com/help/cli/jumpcloud-scim-integration

This section details the required fields for configuring identity management within the JumpCloud application to enable SCIM provisioning with Bitwarden. It includes the Base URL and Token Key, which are essential for connecting JumpCloud to the Bitwarden SCIM endpoint.

```APIDOC
Identity Management Configuration:
  Configuration Settings:
    Base URL:
      Description: Enter the SCIM URL (learn more about enabling SCIM in the web vault).
    Token Key:
      Description: Enter the SCIM API Key (learn more about enabling SCIM in the web vault).
```

--------------------------------

### Bitwarden CLI Command for Listing Organization Data

Source: https://bitwarden.com/help/cli/event-logs

This snippet describes the usage of the Bitwarden CLI tool to retrieve detailed organization data in JSON format. The `bw-list` command allows users to gather information on organization members, items, collections, and groups, which can then be cross-referenced with data obtained from API calls.

```CLI
bw-list: Retrieve the following items in JSON format:
  - Org members
  - Items
  - Collections
  - Groups
```

--------------------------------

### Set NODE_EXTRA_CA_CERTS for Bitwarden CLI/Directory Connector CLI

Source: https://bitwarden.com/help/cli/certificates

Environment variable configuration to specify an additional CA certificate for Node.js-based Bitwarden CLI and Directory Connector CLI applications to trust self-signed certificates.

```Bash
export NODE_EXTRA_CA_CERTS=~/.config/Bitwarden/certificate.crt
```

--------------------------------

### Add Bitwarden user to Docker group

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Grants the 'bitwarden' user permissions to interact with Docker by adding them to the 'docker' group. This allows the bitwarden user to run Docker commands without sudo.

```Bash
sudo usermod -aG docker bitwarden
```

--------------------------------

### Bitwarden SCIM Required Attributes for User and Group Provisioning

Source: https://bitwarden.com/help/cli/ping-identity-scim-integration

This section outlines the essential SCIM v2 attributes used by Bitwarden for synchronizing user and group data from Ping Identity. It specifies which attributes are required and how certain complex attributes like 'emails' and 'members' are interpreted for successful provisioning.

```APIDOC
SCIM v2 Enterprise Attributes:

User attributes:
- active: Boolean, indicates if the user account is active.
- emails: Array of objects. Bitwarden uses the 'value' of the object which contains "primary": true.
  Example: [{"value": "user@example.com", "type": "work", "primary": true}]
- userName: String, unique identifier for the user (alternative to emails).
- displayName: String, the user's display name.
- externalId: String, a unique identifier for the user in the external system.

Group attributes:
- displayName: String, the group's display name (required).
- members: Array of objects, each object representing a user in that group.
  Example: [{"value": "user_id_1"}, {"value": "user_id_2"}]
- externalId: String, a unique identifier for the group in the external system.
```

--------------------------------

### Log in to Bitwarden CLI with Inline Credentials (Not Recommended)

Source: https://bitwarden.com/help/cli/cli

This command allows providing email, password, two-step login method, and code directly as arguments for Bitwarden CLI login. While possible, this method is not recommended for security reasons due to exposing credentials in command history.

```Bash
bw login [email] [password] --method <method> --code <code>
```

--------------------------------

### Configure Auth0 Post-Login SAML Action with JavaScript

Source: https://bitwarden.com/help/cli/saml-auth0

This JavaScript code snippet defines an Auth0 post-login action. It modifies SAML configuration settings for `samlp` protocol requests, ensuring the correct signature algorithm, digest algorithm, response signing, and name identifier format are applied for Bitwarden SSO.

```JavaScript
exports.onExecutePostLogin = async (event, api) => {
    // Modify SAML configuration settings
    if (event.request.protocol === 'samlp') {
        api.saml.updateConfiguration({
            signatureAlgorithm: "rsa-sha256",
            digestAlgorithm: "sha256",
            signResponse: true,
            nameIdentifierFormat: "urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress",
            binding: "urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect"
        });
    }
};
```

--------------------------------

### Generate Self-Signed SSL Certificate using OpenSSL

Source: https://bitwarden.com/help/cli/certificates

Command to generate a self-signed SSL certificate and private key using OpenSSL, including Subject Alternative Name (SAN) configuration for a specified domain.

```Bash
mkdir ./bwdata/ssl/bitwarden.example.com
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -days 365 \
  -keyout ./bwdata/ssl/bitwarden.example.com/private.key \
  -out ./bwdata/ssl/bitwarden.example.com/certificate.crt \
  -reqexts SAN -extensions SAN \
  -config <(cat /usr/lib/ssl/openssl.cnf <(printf '[SAN]\nsubjectAltName=DNS:bitwarden.example.com\nbasicConstraints=CA:true')) \
  -subj "/C=US/ST=New York/L=New York/O=Company Name/OU=Bitwarden/CN=bitwarden.example.com"
```

--------------------------------

### Bitwarden Log in with Device Protocol

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

This section outlines the step-by-step protocol for logging into Bitwarden using a registered device. It details the exchange of requests, encryption of sensitive keys using temporary public/private key pairs, and local decryption to authenticate the user without transmitting the master password.

```APIDOC
Log in with device process:
1. Initiating client sends request to Bitwarden server:
    - Includes: account email address, unique Auth-request Public Key, access code.
2. Registered devices (mobile/desktop apps with device-specific GUID) are provided the request.
3. Approving client encrypts:
    - Account's Master Key
    - Master Password Hash
    - Using: Auth-request Public Key (from step 1).
4. Approving client sends Encrypted Master Key and Encrypted Master Password Hash to Bitwarden server.
    - Request marked as fulfilled.
5. Initiating client requests Encrypted Master Key and Encrypted Master Password Hash from Bitwarden server.
6. Initiating client locally decrypts:
    - Master Key
    - Master Password Hash
    - Using: Auth-request Private Key.
7. Initiating client authenticates user with Bitwarden Identity service:
    - Using: access code, fulfilled authentication request.

Auth-request Public and Private Keys:
- Uniquely generated for each passwordless login request.
- Exist only for the duration of the request.
- Requests expire and are purged from Bitwarden server every 15 minutes if not approved/denied.
```

--------------------------------

### Configure Bitwarden Self-Hosted for EU Cloud Region

Source: https://bitwarden.com/help/cli/families-for-enterprise-self-hosted

If your Bitwarden cloud organization was created on EU servers, you must configure specific URI and region values in your self-hosted instance's `bwdata/env/global.override.env` file. This ensures proper communication with the EU cloud infrastructure for billing sync and other services.

```Bash
globalSettings__baseServiceUri__cloudRegion=EU
globalSettings__installation__identityUri=https://identity.bitwarden.eu
globalSettings__installation__apiUri=https://api.bitwarden.eu
globalSettings__pushRelayBaseUri=https://push.bitwarden.eu
```

--------------------------------

### Configure Windows Registry for Bitwarden Firefox Base URL

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This APIDOC-like structure outlines the properties for a new Registry item to be created via Windows Group Policy Manager. It sets the base environment URL for the Bitwarden Firefox extension under HKEY_LOCAL_MACHINE, directing the extension to a custom server. Note that some registry management systems may omit HKEY_LOCAL_MACHINE\ from the Full Key Path if they have a separate Hive setting.

```APIDOC
Registry Item Properties:
  Action: Update
  Hive: HKEY_LOCAL_MACHINE
  Key Path: HKEY_LOCAL_MACHINE\\SOFTWARE\\Policies\\Mozilla\\Firefox\\3rdparty\\Extensions\\{446900e4-71c2-419f-a6a7-df9c091e268b}\\environment
  Value name: base
  Value type: REG_SZ
  Value data: Your server's configured domain
```

--------------------------------

### Authenticate Bitwarden CLI with Environment Variable

Source: https://bitwarden.com/help/cli/access-tokens

This command demonstrates how the Bitwarden Secrets Manager CLI automatically authenticates using an access token exported to the BWS_ACCESS_TOKEN environment variable. It retrieves a project by its ID.

```Bash
bws project get e325ea69-a3ab-4dff-836f-b02e013fe530
```

--------------------------------

### Import Data using Bitwarden CLI

Source: https://bitwarden.com/help/cli/encrypted-export

This snippet shows how to import data into your Bitwarden vault using the command-line interface. It requires specifying the import format and the path to the data file. Use `bw import --formats` to list available formats.

```Bash
bw import <format> <path>
```

```Bash
bw import <format> /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Change Bitwarden Self-Hosted Server Name

Source: https://bitwarden.com/help/cli/hosting-faqs

Instructions to update the server's FQDN or name by modifying the `config.yml` and `global.override.env` files, and rebuilding assets. Ensure your certificate contains a Subject Alternative Name (SAN) with the new FQDN.

```YAML
# In ./bwdata/config.yml
url: your.new.server.name
```

```Shell
./bitwarden.sh rebuild
```

```Configuration
# Verify globalSettings_baseServiceUri__* variables in ./bwdata/env/global.override.env
# Example: globalSettings__baseServiceUri__Vault=https://your.new.server.name
```

--------------------------------

### Upload a file using Bitwarden CLI

Source: https://bitwarden.com/help/cli/attachments

This command attaches a specified file to an existing Bitwarden vault item. The --file flag indicates the path to the file, and --itemid specifies the unique ID of the vault item where the file will be attached. Ensure the item ID is correct to avoid errors.

```Bash
bw create attachment --file /path/to/myfile.ext --itemid <itemid>
```

--------------------------------

### Configure Bitwarden Organization Environment Variables

Source: https://bitwarden.com/help/cli/self-host-an-organization

This snippet details the environment variables required to enable advanced features for a self-hosted Bitwarden organization. These variables are set in the `./bwdata/env/global.override.env` file and control aspects like email invitations, cloud communication, Duo two-step login, HaveIBeenPwned API integration, user registration, and SSO policy enforcement.

```Configuration
globalSettings__mail__smtp__host=:
  Description: Your SMTP server hostname (recommended) or IP address.
  Usage: Used for inviting users to your organization.
globalSettings__mail__smtp__port=:
  Description: The SMTP port used by the SMTP server.
  Type: Integer
  Usage: Used for inviting users to your organization.
globalSettings__mail__smtp__ssl=:
  Description: Whether your SMTP server uses an encryption protocol.
  Type: Boolean
  Values: true (SSL), false (TLS)
  Usage: Used for inviting users to your organization.
globalSettings__mail__smtp__username=:
  Description: A valid username for the smtp__host.
  Usage: Used for inviting users to your organization.
globalSettings__mail__smtp__passsword=:
  Description: A valid password for the smtp__username.
  Usage: Used for inviting users to your organization.
globalSettings__enableCloudCommunication=:
  Description: Set to true to allow communication between your server and our cloud system.
  Type: Boolean
  Usage: Used for billing and license sync.
globalSettings__duo__aKey=:
  Description: A randomly generated Duo akey. For more information, see Duo's Documentation.
  Usage: Used for organization-wide two-step login via Duo.
globalSettings__hibpApiKey=:
  Description: Your HaveIBeenPwned (HIBP) API Key, available here.
  Usage: Allows users to run the Data Breach report and to check their master password for presence in breaches when they create an account.
globalSettings__disableUserRegistration=:
  Description: Specify true to disable new users signing up for an account on this instance via the registration page.
  Type: Boolean
  Usage: Used to limit users on the server to those invited to the organization.
globalSettings__sso__enforceSsoPolicyForAllUsers=:
  Description: Specify true to enforce the Require SSO authentication policy for owner and admin roles.
  Type: Boolean
  Usage: Used to enforce the Require SSO authentication policy for owner and admin roles.
```

--------------------------------

### Sync Users from a Specific Organizational Unit (OU)

Source: https://bitwarden.com/help/cli/gsuite-directory

This filter specifies that only users within the `/Engineering` organizational unit path should be synced. The root group, under which OUs are nested, is always referred to as `/` in the `orgUnitPath`.

```Plain
|orgUnitPath=/Engineering
```

--------------------------------

### Internal Messaging System Announcement Template

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

Provides a pre-written post for internal messaging systems to announce the company-wide deployment of Bitwarden, aiming to boost enthusiasm and adoption by outlining key benefits.

```Messaging
Subject: Use this template for easy sharing

Body:

Hi *[name]*,

Here is a pre-written post to share on your organization’s internal messaging systems and let employees know that you’re moving to Bitwarden. This post can help boost enthusiasm and adoption of your new password manager.

***Template: Get started with Bitwarden***

***Subject***: Introducing Bitwarden password manager for company-wide deployment

***Body***:

*Hi team, we are happy to announce the company-wide deployment of Bitwarden Password Manager. Bitwarden is a respected, industry-leading company with a strong security record.*

*You will find Bitwarden to be simple and easy to use.*

*Here are three reasons we're excited to get you on Bitwarden:*

1. *Easily access all your passwords anytime, anywhere, on any device.*
2. *Securely share credentials with others.*
3. *Streamline logging into your accounts with auto-fill.*

*You will receive an invite via email to join Bitwarden.*
```

--------------------------------

### Pull Latest Docker Compose Images for Bitwarden

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command pulls the most recent images for all services defined in the docker-compose.yml file, ensuring that the deployment uses the latest available versions.

```Bash
docker compose pull
```

--------------------------------

### Clone Git Repository using SSH Method

Source: https://bitwarden.com/help/cli/ssh-agent

Clone a Git repository from GitHub using the SSH method, leveraging your configured SSH key for authentication.

```Plain
git clone git@github.com:<USER>/<repository>.git
```

--------------------------------

### Configure Bitwarden Self-Hosted Push Relay URI

Source: https://bitwarden.com/help/cli/configure-push-relay

Modify the `global.env` file to specify a custom push relay service URI for your self-hosted Bitwarden server, then restart the service to apply changes. This allows connecting to a custom or regional push relay.

```Shell
# Open the global environment configuration file
# Path: ./bwdata/docker/global.env
# Add or modify the following line with your push relay service URI:
globalSettings__pushRelayBaseUri=https://your.push.relay.com

# After saving the file, restart Bitwarden to apply changes
./bitwarden.sh restart
```

--------------------------------

### Bitwarden CLI API Key Environment Variables

Source: https://bitwarden.com/help/cli/personal-api-key

These environment variables can be set to provide your `client_id` and `client_secret` to the Bitwarden CLI, preventing manual intervention during authentication, especially useful for automated tasks.

```APIDOC
BW_CLIENTID: client_id
BW_CLIENTSECRET: client_secret
```

--------------------------------

### Configure Ingress Paths in my-values.yaml for Bitwarden Deployment

Source: https://bitwarden.com/help/cli/aws-eks-deployment

This YAML configuration defines the ingress settings for a Bitwarden deployment, including the domain, enabling ingress, specifying the NGINX class, and setting up various path-based routing rules for web, attachments, API, icons, notifications, events, SCIM, SSO, identity, and admin endpoints. It also includes annotations for SSL redirection and regex usage.

```YAML
general:
  domain: "REPLACEME.com"
  ingress:
    enabled: true
    className: "nginx"
     ## - Annotations to add to the Ingress resource
    annotations:
      nginx.ingress.kubernetes.io/ssl-redirect: "true"
      nginx.ingress.kubernetes.io/use-regex: "true"
      nginx.ingress.kubernetes.io/rewrite-target: /$1
    ## - Labels to add to the Ingress resource
    labels: {}
    # Certificate options
    tls:
      # TLS certificate secret name
      name: # Handled via the NLB defined in the ingress controller
      # Cluster cert issuer (ex. Let's Encrypt) name if one exists
      clusterIssuer:
    paths:
      web:
        path: /(.*)
        pathType: ImplementationSpecific
      attachments:
        path: /attachments/(.*)
        pathType: ImplementationSpecific
      api:
        path: /api/(.*)
        pathType: ImplementationSpecific
      icons:
        path: /icons/(.*)
        pathType: ImplementationSpecific
      notifications:
        path: /notifications/(.*)
        pathType: ImplementationSpecific
      events:
        path: /events/(.*)
        pathType: ImplementationSpecific
      scim:
        path: /scim/(.*)
        pathType: ImplementationSpecific
      sso:
        path: /(sso/.*)
        pathType: ImplementationSpecific
      identity:
        path: /(identity/.*)
        pathType: ImplementationSpecific
      admin:
        path: /(admin/?.*)
        pathType: ImplementationSpecific
```

--------------------------------

### Configure Firefox Base URL via Windows Registry

Source: https://bitwarden.com/help/cli/deploy-clients

This entry details the properties for configuring the Bitwarden base environment URL in Firefox using Windows Group Policy Manager and Registry Editor. It specifies the registry hive, key path, value name, type, and data for the base URL.

```APIDOC
Registry Item Properties (Base URL):
  Action: Update
  Hive: HKEY_LOCAL_MACHINE
  Key Path: HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Mozilla\Firefox\3rdparty\Extensions\{446900e4-71c2-419f-a6a7-df9c091e268b}\environment
  Value name: base
  Value type: REG_SZ
  Value data: Your server's configured domain
```

--------------------------------

### Configure Bitwarden Desktop App for Self-Hosted Server

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This JSON object is used within the `data.json` file to configure the Bitwarden Desktop app to connect to a self-hosted server. It sets the `region` to 'Self-hosted' and specifies the `base` URL for the server. This can be deployed as a template via endpoint management solutions.

```Bash
"global_environment_environment": {
    "region": "Self-hosted",
    "urls": {
       "base": "self-host.com"
     }
  }
```

--------------------------------

### Configure AWS Network Load Balancer Ingress Controller with Helm

Source: https://bitwarden.com/help/cli/aws-eks-deployment

This command sequence uses Helm to add the ingress-nginx repository, update it, and then upgrade/install the ingress-nginx controller. It configures the controller service with AWS-specific annotations to create an internet-facing Network Load Balancer (NLB) with SSL termination, cross-zone load balancing, and instance target type, using a specified ACM certificate ARN.

```Bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm upgrade ingress-nginx ingress-nginx/ingress-nginx -i \
  --namespace kube-system \
  --set-string controller.service.annotations.'service\.beta\.kubernetes\.io/aws-load-balancer-backend-protocol'="ssl" \
  --set-string controller.service.annotations.'service\.beta\.kubernetes\.io/aws-load-balancer-cross-zone-load-balancing-enabled'="true" \
  --set-string controller.service.annotations.'service\.beta\.kubernetes\.io/aws-load-balancer-type'="external" \
  --set-string controller.service.annotations.'service\.beta\.kubernetes\.io/aws-load-balancer-nlb-target-type'="instance" \
  --set-string controller.service.annotations.'service\.beta\.kubernetes\.io/aws-load-balancer-scheme'="internet-facing" \
  --set-string controller.service.annotations.'service\.beta\.kubernetes\.io/aws-load-balancer-ssl-cert'="arn:aws:acm:REPLACEME:REPLACEME:certificate/REPLACEME" \
  --set-string controller.service.annotations.'service\.beta\.kubernetes\.io/aws-load-balancer-ssl-ports'="443" \
  --set controller.service.externalTrafficPolicy="Local"
```

--------------------------------

### Bitwarden Application Download URL

Source: https://bitwarden.com/help/cli/bitwarden-addresses

Identifies the official URL for downloading Bitwarden client applications.

```APIDOC
https://bitwarden.com/download/
```

--------------------------------

### Enable Cloud Communication for Bitwarden Self-Hosted

Source: https://bitwarden.com/help/cli/families-for-enterprise-self-hosted

Configure your self-hosted Bitwarden instance to allow communication with Bitwarden's cloud systems. This is achieved by setting the `globalSettings__enableCloudCommunication` parameter to `true` in the `bwdata/env/global.override.env` configuration file. This step is essential for enabling automatic billing synchronization.

```Bash
globalSettings__enableCloudCommunication=true
```

--------------------------------

### Manage Bitwarden Device Approval Requests

Source: https://bitwarden.com/help/cli/cli

Commands to list, approve, or deny pending device authorization requests for an organization. This includes approving or denying all requests at once. Bitwarden recommends caution with bulk approvals, emphasizing manual verification steps.

```bash
bw device-approval list --organizationid <organization_Id>
```

```bash
bw device-approval approve --organizationid <organizationId> <requestId>
```

```bash
bw device-approval approve-all --organization <organizationId>
```

```bash
bw device-approval deny --organizationid <organizationId> <requestId>
```

```bash
bw device-approval deny-all --organizationid <organizationId>
```

--------------------------------

### Create Docker Compose Override File for Bitwarden

Source: https://bitwarden.com/help/cli/kerberos-integration

This command creates or opens the `docker-compose.override.yml` file. This file is used to add custom volume mounts to Bitwarden's Docker containers, ensuring Kerberos configuration is retained across updates.

```Shell
nano /opt/bitwarden/bwdata/docker/docker-compose.override.yml
```

--------------------------------

### Configure Bitwarden CLI State Directory

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command specifies the absolute path for the directory where encrypted state files, containing authentication tokens, will be stored. Using state files can help reduce rate limiting during authentication.

```Plain
bws config state-dir /Users/user/Desktop/bws/state
```

--------------------------------

### Bitwarden Event IDs for Monitoring User Login and Device Approval

Source: https://bitwarden.com/help/cli/monitoring-event-logs

Provides event IDs to track user login frequency and device approval requests, offering insights into user engagement and adherence to security practices.

```APIDOC
User Frequency Event IDs:
  1000: Logged in
  1010: User requested device approval
```

--------------------------------

### Generate PKCS12 Certificate for Key Connector

Source: https://bitwarden.com/help/cli/deploy-key-connector

OpenSSL commands to generate an X509 certificate and export it as a PKCS12 (.pfx) file, which Key Connector can use to access an RSA key pair for protecting user keys at rest. The certificate must be at least 2048 bits.

```Bash
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout bwkc.key -out bwkc.crt -subj "/CN=Bitwarden Key Connector" -days 36500

openssl pkcs12 -export -out ./bwkc.pfx -inkey bwkc.key -in bwkc.crt -passout pass:{Password}
```

--------------------------------

### Change Language in Bitwarden Desktop App

Source: https://bitwarden.com/help/cli/localization

Instructions for changing the display language in the Bitwarden desktop application on Windows or macOS.

```UI
1. Open the desktop app's Preferences panel (on Windows, File → Settings) (on macOS, Bitwarden → Preferences).
2. Scroll to the App Settings section and use the Language dropdown to select your language.
```

--------------------------------

### Splunk Query with Multiple Commands and Top IP Address

Source: https://bitwarden.com/help/cli/splunk-siem

This query demonstrates how to include multiple commands in a Splunk search. It filters Bitwarden events by type and user, then uses the 'top' command to display the most frequent 'ipAddress' values.

```Bash
sourcetype="bitwarden:events" type=1115 actingUserName="John Doe" | top ipAddress
```

--------------------------------

### Set BW_CLIENTSECRET Environment Variable for Bitwarden CLI Authentication

Source: https://bitwarden.com/help/cli/cli-auth-challenges

This snippet provides commands to set the BW_CLIENTSECRET environment variable, allowing the Bitwarden CLI to automatically pass authentication challenges using your personal API key. This is useful for automated workflows.

```Bash
export BW_CLIENTSECRET="client_secret"
```

```PowerShell
env:BW_CLIENTSECRET="client_secret"
```

--------------------------------

### Bitwarden CLI: Run Command with Minimal Environment

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Execute a process with a minimal set of environment variables using the `--no-inherit-env` option. This drops most variables from the parent shell, though `$PATH` and some shell-set variables will still be present. Note that this option does not create a sandbox.

```Bash
bws run --no-inherit-env -- echo "running a command with a minimal environment"
```

--------------------------------

### Migrate Bitwarden Organization Vault Data and Group Permissions

Source: https://bitwarden.com/help/cli/migration-script

This command initiates the `migratebw` function, transferring organization vault data, groups, and their associated permissions from the source to the destination organization. Users must be in at least an invited state in the destination organization for a successful migration.

```Bash
python3 bwAdminTools.py -c migratebw
```

--------------------------------

### Designate Cloud Region for Hyperlinks

Source: https://bitwarden.com/help/cli/environment-variables

Specify `US` or `EU` to designate which Bitwarden cloud server your self-hosted server should hyperlink to. Additional variables may be required for EU region configuration.

```APIDOC
globalSettings__baseServiceUri__cloudRegion=US
# OR
globalSettings__baseServiceUri__cloudRegion=EU
```

--------------------------------

### Bitwarden SAML Service Provider Configuration Fields

Source: https://bitwarden.com/help/cli/ping-identity-saml-implementation

Details the fields required to configure Bitwarden as a SAML service provider within Ping Identity, including Name ID Format, signing algorithms, and assertion expectations.

```APIDOC
Service Provider Configuration Fields:
- Name ID Format: Set this field to the Subject Name ID Format specified in the Ping Identity app configuration.
- Outbound Signing Algorithm: The algorithm Bitwarden will use to sign SAML requests.
- Signing Behavior: Whether/when SAML requests will be signed.
- Minimum Incoming Signing Algorithm: By default, Ping Identity will sign with RSA SHA-256. Select `sha-256` from the dropdown.
- Expect signed assertions: Whether Bitwarden expects SAML assertions to be signed. This setting should be unchecked.
- Validate Certificates: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured with the Bitwarden Login with SSO docker image.
```

--------------------------------

### Using Continuation Token for Bitwarden API Pagination (Plain Text)

Source: https://bitwarden.com/help/cli/public-api

Shows how to append the 'continuationToken' value to an existing API request URL as a query parameter to retrieve subsequent paginated results from endpoints like '/public/events'.

```Plain
https://api.bitwarden.com/public/events?continuationToken=<token_value>
```

--------------------------------

### Combine Group Filters in Bitwarden Directory Connector Sync

Source: https://bitwarden.com/help/cli/gsuite-directory

This snippet demonstrates how to combine 'exclude' filters with a query-based filter. Exclude filters must precede any query declarations, allowing for fine-grained control over which groups are synced.

```Bash
exclude:Group A|memberKey:user@company
```

--------------------------------

### Sync Bitwarden Directory Connector Groups by Name with Wildcard Query

Source: https://bitwarden.com/help/cli/gsuite-directory

This snippet shows how to sync groups whose names contain a specific term using a wildcard query. The pipe symbol indicates a query parameter, and asterisks denote wildcard matches, allowing for flexible pattern matching.

```Bash
|name:*engineering*
```

--------------------------------

### Bitwarden CLI Search: Fuzzy Matching Queries

Source: https://bitwarden.com/help/cli/searching-vault

Illustrates the use of the '~' prefix combined with an edit distance integer for fuzzy matching in Bitwarden CLI search queries. This allows for finding items with similar but not identical names.

```Bitwarden
>name:email~1
```

--------------------------------

### Default Group Attribute Mappings for SCIM Provisioning

Source: https://bitwarden.com/help/cli/microsoft-entra-id-scim-integration

Describes the default attribute mappings between Bitwarden SCIM attributes and Microsoft Entra ID attributes for group objects during provisioning.

```APIDOC
- Bitwarden attribute: displayName
  Default AAD attribute: displayName
- Bitwarden attribute: members
  Default AAD attribute: members
- Bitwarden attribute: externalId
  Default AAD attribute: objectId
```

--------------------------------

### Test Bitwarden SSH Agent Keys

Source: https://bitwarden.com/help/cli/ssh-agent

Command to verify the Bitwarden SSH Agent configuration by requesting a list of SSH keys currently managed by the agent.

```Shell
ssh-add -L
```

--------------------------------

### Create a new secret with Bitwarden CLI

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Use `bws secret create` to provision a new secret. This command requires a key, value, and project ID. An optional note can be added using the `--note` flag. By default, it returns a JSON object representing the newly created secret.

```Bash
bws secret create <KEY> <VALUE> <PROJECT_ID>
```

```Bash
bws secret create SES_KEY 0.982492bc-7f37-4475-9e60 f588b2f2-4780-4a78-be2a-b02d014d622f --note "API Key for AWS SES"
```

```JSON
{
  "object": "secret",
  "id": "be8e0ad8-d545-4017-a55a-b02f014d4158",
  "organizationId": "10e8cbfa-7bd2-4361-bd6f-b02e013f9c41",
  "projectId": "e325ea69-a3ab-4dff-836f-b02e013fe530",
  "key": "SES_KEY",
  "value": "0.982492bc-7f37-4475-9e60",
  "note": "API Key for AWS SES",
  "creationDate": "2023-06-28T20:13:20.643567Z",
  "revisionDate": "2023-06-28T20:13:20.643567Z"
}
```

--------------------------------

### Cloudflare Zero Trust Application Configuration Fields

Source: https://bitwarden.com/help/cli/cloudflare-zero-trust-sso-implementation

This table details the fields to be filled in the Cloudflare Zero Trust 'Configure app' screen, using information from the Bitwarden web vault's Single Sign-On page.

```APIDOC
Application: Enter `Bitwarden`.
Entity ID: Copy the SP entity ID from the Bitwarden Single Sign-On page into this field.
Assertion Consumer Service URL: Copy the Assertion consumer service (ACS) URL from the Bitwarden Single Sign-On page into this field.
Name ID Format: Select Email from the dropdown menu.
```

--------------------------------

### Configure Bitwarden Browser Extension Base URL on macOS via .plist

Source: https://bitwarden.com/help/cli/deploy-clients

This snippet provides the XML content for a .plist file to configure the base environment URL for the Bitwarden browser extension on macOS. This file should be named `com.google.chrome.extensions.<extension_id>.plist` and converted to a `.mobileconfig` profile for distribution.

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>environment</key>
        <dict>
            <key>base</key>
            <string>https://my.bitwarden.server.com</string>
        </dict>
    </dict>
</plist>
```

--------------------------------

### Access Shell Configuration Files

Source: https://bitwarden.com/help/cli/ssh-agent

Commands to open and edit the `.bashrc` or `.zshrc` shell configuration files using the nano text editor.

```Shell
nano ~/.bashrc
nano ~/.zshrc
```

--------------------------------

### Disable User Self-Registration for Self-Hosted Bitwarden

Source: https://bitwarden.com/help/cli/org-faqs

Instructions on how to prevent users from signing up for an account via the registration page on a self-hosted Bitwarden instance by configuring a specific environment variable.

```Configuration
globalSettings__disableUserRegistration=true
```

--------------------------------

### Configure Bitwarden CLI Server with an Alternate Config File

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command saves server settings to a specified alternate configuration file instead of the default. This provides greater flexibility in managing distinct CLI configurations.

```Bash
bws config server-base http://third_hosted_server.com --config-file ~/.bws/alt_config
```

--------------------------------

### Configure HIBP API Key for Self-Hosted Bitwarden Data Breach Report

Source: https://bitwarden.com/help/cli/reports

To enable the Data Breach report in a self-hosted Bitwarden instance, an HIBP subscription key is required. This snippet shows how to add the purchased API key to the `global.override.env` file, replacing the placeholder value.

```Bash
globalSettings__hibpApiKey=REPLACE
```

--------------------------------

### Bitwarden Emergency Access: Technical Flow

Source: https://bitwarden.com/help/cli/emergency-access

Detailed explanation of the cryptographic and user interaction steps involved in Bitwarden's emergency access feature, leveraging public key exchange and symmetric encryption in a zero-knowledge environment.

```APIDOC
Emergency Access Process:
  1. Grantor invites Grantee:
     - Invitation valid for 5 days.
     - Specifies user access level.
     - Requests Grantee's RSA Public Key.
  2. Grantee accepts invitation:
     - Grantee's RSA Public Key stored with user record.
  3. Grantor confirms Grantee:
     - Grantor's User Symmetric Key encrypted using Grantee's RSA Public Key.
     - Encrypted key stored with invitation.
  4. Emergency occurs: Grantee requests access.
  5. Grantor approves request (manual or wait time lapse):
     - Public Key-encrypted User Symmetric Key delivered to Grantee.
     - Grantee decrypts with RSA Private Key.
     - (Alternative: Grantor rejects request, preventing access for this request).
  6. Grantee gains access based on specified level:
     - View: Obtain view/read access to items in grantor's vault.
     - Takeover: Create new master password for grantor's vault.
```

--------------------------------

### Test GitHub SSH Authentication with Bitwarden Agent

Source: https://bitwarden.com/help/cli/ssh-agent

Command to test SSH authentication with GitHub, which will prompt the Bitwarden SSH Agent to verify access if configured correctly.

```Shell
ssh git@github.com
```

--------------------------------

### Recommended User Attribute Mappings for Object ID Prioritization

Source: https://bitwarden.com/help/cli/microsoft-entra-id-scim-integration

Details changes to user attribute mappings to prioritize Microsoft Entra ID `objectId` for improved performance and connection preservation, especially when user email addresses change.

```APIDOC
- Map externalId (customappsso Attribute) to objectId (Microsoft Entra ID Attribute)
  Match objects using this attribute: Yes
  Matching precedence: 1
- For userName (customerappsso Attribute) to userPrincipalName (Microsoft Entra ID Attribute) mapping
  Matching precedence: 2
```

--------------------------------

### List Bitwarden CLI Vault Objects

Source: https://bitwarden.com/help/cli/cli

The `bw list` command retrieves an array of objects from the Bitwarden vault, such as items, folders, or collections. It supports various filters like `--url`, `--folderid`, and `--collectionid` to narrow down results, and `--search` for specific object names.

```Bash
bw list (items|folders|collections|organizations|org-collections|org-members) [options]
```

```Bash
bw list items --folderid null --collectionid null
```

```Bash
bw list items --search github --folderid 9742101e-68b8-4a07-b5b1-9578b5f88e6f
```

--------------------------------

### Configure SAML Application Fields in Ping Identity

Source: https://bitwarden.com/help/cli/ping-identity-saml-implementation

This section details the required fields for configuring a SAML application in the Ping Identity Administrator Portal, specifically for integration with Bitwarden. It lists the field names, their corresponding descriptions, and where to obtain the values from the Bitwarden single sign-on screen.

```APIDOC
Field: ACS URL
Description: Set this field to the pre-generated Assertion Consumer Service (ACS) URL. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.

Field: Entity ID
Description: Set this field to the pre-generated SP Entity ID. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
```

--------------------------------

### Bitwarden Public API Base and Authentication Endpoints

Source: https://bitwarden.com/help/cli/public-api

Details the base URLs for the Bitwarden Public API and the specific authentication endpoints for both cloud-hosted and self-hosted instances.

```APIDOC
Endpoints:
  Base URL:
    - Cloud-hosted: `https://api.bitwarden.com` or `https://api.bitwarden.eu`
    - Self-hosted: `https://your.domain.com/api`
  Authentication Endpoints:
    - Cloud-hosted: `https://identity.bitwarden.com/connect/token` or `https://identity.bitwarden.eu/connect/token`
    - Self-hosted: `https://your.domain.com/identity/connect/token`
```

--------------------------------

### Bitwarden Web Application URLs

Source: https://bitwarden.com/help/cli/bitwarden-addresses

Lists the URLs for accessing the Bitwarden web vault application across different regions.

```APIDOC
vault.bitwarden.com
vault.bitwarden.eu
```

--------------------------------

### Configure Bitwarden API Keys for Elastic SIEM Integration

Source: https://bitwarden.com/help/cli/elastic-siem

This section details the required API key information (URL, Client ID, Client Secret) from Bitwarden to connect the Elastic SIEM integration. It specifies the default URL for Bitwarden cloud users and advises self-hosted users to input their specific URL, ensuring no trailing forward slashes. It also highlights the importance of not sharing sensitive API key values in non-secure locations.

```APIDOC
Elastic Field | Value
--- | ---
URL | For Bitwarden cloud users, the default url will be `https://api.bitwarden.com`. For self-hosted Bitwarden users, input your self-hosted URL. Be sure that the URL does not include any trailing forward slashes at the end of the URL "`\/`"
Client ID | Input the value for `client_id` from the Bitwarden organization API key window.
Client Secret | Input the value for `client_secret` from the Bitwarden organization API key window.
```

--------------------------------

### Auth0 SAML Identity Provider Configuration Fields

Source: https://bitwarden.com/help/cli/saml-auth0

Outlines the fields necessary for configuring the identity provider (Auth0) side of the SAML integration, such as Entity ID, Binding Type, SSO/SLO URLs, and X509 Public Certificate.

```APIDOC
Identity Provider Configuration:
  Entity ID:
    Description: Enter the Domain value of your Auth0 application, prefixed by urn:, for example urn:bw-help.us.auth0.com. This field is case sensitive.
  Binding Type:
    Description: Select HTTP POST to match the Token Endpoint Authentication Method value specified in your Auth0 application.
  Single Sign On Service URL:
    Description: Enter the SAML Protocol URL of your Auth0 application. For example, https://bw-help.us.auth0.com/samlp/HcpxD63h7Qzl420u8qachPWoZEG0Hho2.
  Single Log Out Service URL:
    Description: Login with SSO currently does not support SLO. This option is planned for future development, however you may pre-configure it if you wish.
  X509 Public Certificate:
    Description: Paste the retrieved signing certificate, removing -----BEGIN CERTIFICATE----- and -----END CERTIFICATE-----. The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters will cause certification validation to fail.
  Outbound Signing Algorithm:
    Description: Select rsa-sha256 unless you've configured a custom signing rule.
  Disable Outbound Logout Requests:
    Description: Login with SSO currently does not support SLO. This option is planned for future development.
  Want Authentication Requests Signed:
    Description: Whether Auth0 expects SAML requests to be signed.
```

--------------------------------

### Add Kerberos Volume Mount for SCIM Service (Docker Compose Override)

Source: https://bitwarden.com/help/cli/kerberos-integration

This Docker Compose snippet extends the previous configuration by adding a volume mount for the Kerberos directory to the `scim` service, if SCIM is being used. This ensures the SCIM container also has access to the Kerberos configuration.

```YAML
scim:
        volumes:
            - ../kerberos:/etc/bitwarden/kerberos
```

--------------------------------

### SCIM User Attributes for Bitwarden Provisioning

Source: https://bitwarden.com/help/cli/about-scim

Details the required and optional SCIM v2 attributes Bitwarden uses for user provisioning, including 'active', 'email'/'userName', 'displayName', and 'externalId'. Notes how multiple email addresses are handled by using the 'value' of the object with "primary": true.

```APIDOC
User attributes:
- active (required): Indicates if the user is active.
- email or userName (required): Primary identifier for the user. For multiple emails, uses the 'value' of the object with "primary": true.
- displayName: User's display name.
- externalId: External identifier for the user.
```

--------------------------------

### Check for Bitwarden Directory Connector CLI Updates

Source: https://bitwarden.com/help/cli/directory-sync-cli

The `update` command allows users to check if their Directory Connector CLI is up-to-date. If a newer version is available, it provides a download URL, but the update must be performed manually. It's crucial to match CLI and desktop app versions to avoid issues.

```Bash
bwdc update
```

--------------------------------

### Configure General SAML Settings in JumpCloud for Bitwarden SSO

Source: https://bitwarden.com/help/cli/saml-jumpcloud

This section details the essential SAML configuration fields within JumpCloud's Single Sign-On Configuration for integrating with Bitwarden. It covers unique identifiers for both Identity Provider (IdP) and Service Provider (SP), and the Assertion Consumer Service (ACS) URL.

```APIDOC
SSO Configuration Fields (General):
  IdP Entity ID:
    Description: Set to a unique, Bitwarden-specific value (e.g., `bitwardensso_yourcompany`).
  SP Entity ID:
    Description: Pre-generated value copied from Bitwarden organization's Settings -> Single sign-on screen. Varies based on setup.
  ACS URL:
    Description: Pre-generated Assertion Consumer Service (ACS) URL copied from Bitwarden organization's Settings -> Single sign-on screen. Varies based on setup.
```

--------------------------------

### Create a Bitwarden Send Object via CLI

Source: https://bitwarden.com/help/cli/cli

The `send` command facilitates the creation of Bitwarden Send objects for ephemeral sharing of text or files. This highly flexible tool supports various options for naming, setting expiration durations, and specifying content type (text or file path).

```Bash
bw send -n "My First Send" -d 7 --hidden "The contents of my first text Send."
```

```Bash
bw send -n "A Sensitive File" -d 14 -f /Users/my_account/Documents/sensitive_file.pdf
```

--------------------------------

### Run Bitwarden Secrets Manager CLI using Docker

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command executes the Bitwarden Secrets Manager CLI within a Docker container. The `--rm` flag ensures the container is removed after exit, and `-it` allocates a pseudo-TTY and keeps STDIN open for interactive use.

```Plain
docker run --rm -it bitwarden/bws --help
```

--------------------------------

### Bitwarden Public API Overview and Compatibility

Source: https://bitwarden.com/help/cli/public-api

Describes the Bitwarden Public API as a RESTful API, its compatibility with OpenAPI Specification (OAS3), and access requirements for Enterprise and Teams organizations. It clarifies that it's not for individual vault item management.

```APIDOC
Bitwarden Public API:
  Type: RESTful API
  Compatibility: OpenAPI Specification (OAS3)
  Definition File: `swagger.json`
  Swagger UI URLs:
    - Public Cloud: `https://bitwarden.com/help/api/`
    - Self-hosted: `https://your.domain.com/api/docs/`
  Access: Available for Enterprise and Teams organizations.
  Limitations: Does not allow management of individual vault items.
```

--------------------------------

### Generate Self-Signed Identity Certificate with OpenSSL

Source: https://bitwarden.com/help/cli/install-on-premise-manual

Generates a self-signed X.509 certificate and a 4096-bit RSA private key for the Bitwarden IdentityServer using OpenSSL. The certificate is valid for 30 years (10950 days).

```Bash
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout identity.key -out identity.crt -subj "/CN=Bitwarden IdentityServer" -days 10950
```

--------------------------------

### Import Data into Bitwarden Vault

Source: https://bitwarden.com/help/cli/cli

The `import` command facilitates importing data from a Bitwarden export or other supported password management applications. The command must be pointed to a file and include the format and path as arguments. If importing an encrypted JSON file, you will be prompted for the password.

```bash
bw import <format> <path>
```

```bash
bw import lastpasscsv /Users/myaccount/Documents/mydata.csv
```

--------------------------------

### Enable Bitwarden CLI Debug Mode

Source: https://bitwarden.com/help/cli/cli

To obtain additional troubleshooting information from the Bitwarden CLI, set the `BITWARDENCLI_DEBUG` environment variable to `true`. This will output more detailed logs to aid in debugging issues.

```Bash
export BITWARDENCLI_DEBUG=true
```

--------------------------------

### Configure Bitwarden Self-Hosted for Cloud Communication

Source: https://bitwarden.com/help/cli/licensing-on-premise

To enable automatic billing sync and other cloud-dependent features, set the `globalSettings__enableCloudCommunication` variable to `true` in your `bwdata/env/global.override.env` file. This allows your self-hosted instance to communicate with Bitwarden's cloud systems.

```Bash
globalSettings__enableCloudCommunication=true
```

--------------------------------

### Compare Bitwarden Source and Destination Organizations

Source: https://bitwarden.com/help/cli/migration-script

This command runs the `diffbw` function of the `bwAdminTools.py` script, which compares the configurations and data between the specified source and destination Bitwarden organizations.

```Bash
python3 bwAdminTools.py -c diffbw
```

--------------------------------

### Bitwarden SCIM User Attribute Mapping with JumpCloud

Source: https://bitwarden.com/help/cli/jumpcloud-scim-integration

This section specifies how Bitwarden maps standard SCIM v2 user properties to JumpCloud's default attributes. It includes details on how multiple email addresses are handled, prioritizing the primary email.

```APIDOC
Bitwarden Attribute | JumpCloud Default Property
--------------------|---------------------------
active              | !suspended && !passwordExpired
emails              | email (uses 'value' of object with "primary": true)
displayName         | displayName
```

--------------------------------

### Exclude Specific User from OU and Attribute Sync

Source: https://bitwarden.com/help/cli/gsuite-directory

This filter demonstrates how to exclude a specific user (`bill@example.com`) from an OU sync that also filters by `orgTitle`. Any `include:` or `exclude:` filters must be placed before any query declaration (`|`).

```Bash
exclude:bill@example.com|orgUnitPath=/Engineering orgTitle:Manager
```

--------------------------------

### Configure Identity Provider Application for Automatic Login

Source: https://bitwarden.com/help/cli/policies

To enable automatic login for an application from your identity provider dashboard, append the `?autofill=1` parameter to the application's destination URL. This signals Bitwarden to autofill and log in the user.

```URL
?autofill=1
```

--------------------------------

### Download Firefox Desktop Entry File (Linux)

Source: https://bitwarden.com/help/cli/deactivate-browser-password-managers

This command downloads the `firefox.desktop` file from Mozilla's GitHub repository and saves it to `/usr/local/share/applications`. This file provides metadata for the desktop environment, allowing Firefox to appear in application menus and have proper icons.

```Shell
wget https://raw.githubusercontent.com/mozilla/sumo-kb/main/install-firefox-linux/firefox.desktop -P /usr/local/share/applications
```

--------------------------------

### Import Data to an Organization Vault

Source: https://bitwarden.com/help/cli/cli

Use the `bw import` command with the `--organizationid` option to import data into a Bitwarden organization vault. This command requires specifying the organization ID, the format of the source data (e.g., `bitwardencsv`), and the path to the source file.

```Plain
bw import --organizationid cf14adc3-aca5-4573-890a-f6fa231436d9 bitwardencsv ./from/source.csv
```

--------------------------------

### Accessing Bitwarden Web Vault Local Storage

Source: https://bitwarden.com/help/cli/data-storage

Instructions on how to access the local storage for the Bitwarden Web Vault within various browser developer tools.

```Chrome
Menu → More Tools → Developer Tools, then select the Application → Local storage.
```

```Safari
Develop → Show Web Inspector → Storage → Local Storage.
```

```Firefox
Menu → More tools → Web Developer Tools → Storage → Local Storage.
```

```Edge
Menu → More tools → Developer tools → Application → Local storage.
```

```Opera
Menu → Developer → Developer Tools → Application → Local storage.
```

```Opera
Developer → Developer Tools → Application → Local storage.
```

--------------------------------

### Define cert-manager ClusterIssuer for Let's Encrypt Production

Source: https://bitwarden.com/help/cli/self-host-with-helm

This YAML configuration defines a ClusterIssuer named 'letsencrypt-production' for cert-manager. It uses the Let's Encrypt production ACME server for issuing trusted, publicly valid TLS certificates. Ensure your DNS records are correctly pointed to your cluster before using this configuration and replace the placeholder email.

```YAML
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: letsencrypt-production
spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory
    email: me@example.com
    privateKeySecretRef:
      name: tls-secret
    solvers:
      - http01:
          ingress:
            class: nginx #use "azure/application-gateway" for Application Gateway ingress
```

--------------------------------

### Manually Sync Bitwarden Vault using CLI

Source: https://bitwarden.com/help/cli/vault-sync

This command allows users to manually synchronize their Bitwarden vault data from the command-line interface. Executing `bw sync` pulls the latest changes from the Bitwarden server to the local client, ensuring the vault is up-to-date. This is useful for immediately reflecting changes made from other devices or the web vault.

```Bash
bw sync
```

--------------------------------

### Configure Advanced Options for ADFS Relying Party Trust

Source: https://bitwarden.com/help/cli/saml-adfs

Instructions for accessing and configuring advanced settings for a created Relying Party Trust within AD FS Server Manager.

```APIDOC
AD FS Server Manager Configuration:
  Accessing Advanced Options:
    1. Select "Relying Party Trusts" from the left-hand file navigator.
    2. Select the correct display name of the created trust.
```

--------------------------------

### Download IDP Certificate from JumpCloud for Bitwarden SSO

Source: https://bitwarden.com/help/cli/saml-jumpcloud

After activating the application, the Identity Provider (IdP) certificate needs to be downloaded from JumpCloud. This certificate is crucial for Bitwarden to verify SAML responses.

```APIDOC
Download IDP Certificate:
  Steps:
    1. After application activation, open the created Bitwarden application via the SSO menu option.
    2. Select the "IDP Certificate" dropdown.
    3. Select "Download certificate".
```

--------------------------------

### Configure Custom SAML Application Settings for Bitwarden SSO

Source: https://bitwarden.com/help/cli/saml-jumpcloud

For custom SAML applications, additional fields need configuration, including SAMLSubject NameID, NameID Format, Signature Algorithm, assertion signing, and the Login URL for user access.

```APIDOC
SSO Configuration Fields (Custom SAML App Only):
  SAMLSubject NameID:
    Description: Specify the JumpCloud attribute sent in SAML responses as the NameID.
  SAMLSubject NameID Format:
    Description: Specify the format of the NameID sent in SAML responses.
  Signature Algorithm:
    Description: Select the algorithm to use to sign SAML assertions or responses.
  Sign Assertion:
    Description: Check this box to sign the SAML assertion (JumpCloud signs SAML response by default).
  Login URL:
    Description: URL from which users login to Bitwarden via SSO.
      Cloud-hosted: `https://vault.bitwarden.com/#/sso` or `https://vault.bitwarden.eu/#/sso`
      Self-hosted: Determined by configured server URL (e.g., `https://your.domain.com/#/sso`)
```

--------------------------------

### Access Bitwarden MSSQL Container Bash Session

Source: https://bitwarden.com/help/cli/backup-on-premise

Execute this command to open an interactive bash shell within the `bitwarden-mssql` Docker container, enabling direct command-line operations for troubleshooting or maintenance.

```Bash
docker exec -it bitwarden-mssql /bin/bash
```

--------------------------------

### Combine Group and Attribute Filters

Source: https://bitwarden.com/help/cli/okta-directory

Illustrates how to concatenate group inclusion/exclusion rules with additional attribute filters using a pipe (`|`). This allows for more precise control, such as filtering groups by their `type`.

```Bash
include:Group A|type eq "APP_GROUP"
```

```Bash
exclude:Group A|type eq "APP_GROUP"
```

--------------------------------

### Configure Bitwarden Send Attachment Base Directory

Source: https://bitwarden.com/help/cli/send-hosting

This code snippet shows the default setting for the `globalSettings__send__baseDirectory` environment variable, which specifies the storage location for files attached to Bitwarden Send. This variable is found in `global.override.env` and can be modified to point to a custom attachment volume if the default is not desired.

```Bash
globalSettings__send__baseDirectory=/etc/bitwarden/core/attachments/send
```

--------------------------------

### Configure Admin Email Addresses for System Administrator Portal Access

Source: https://bitwarden.com/help/cli/system-administrator-portal

This snippet demonstrates how to grant access to the Bitwarden System Administrator Portal by specifying email addresses in the `adminSettings__admins` variable. This variable is located in the `./bwdata/env/global.override.env` file. Multiple email addresses can be provided, separated by commas, and they do not need to be pre-registered Bitwarden accounts.

```Bash
adminSettings__admins=john@example.com,bill@gmail.com,tom@example.com
```

--------------------------------

### Export all Bitwarden attachments via CLI

Source: https://bitwarden.com/help/cli/attachments

This command allows users to export all file attachments from their individual Bitwarden vault into a .zip archive using the command-line interface. This is useful for backup or migration purposes.

```Bash
bw export --format zip
```

--------------------------------

### Approving Untrusted Device: Requesting Admin Approval

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Outlines the multi-step process for approving an untrusted device via administrator intervention, involving client requests, admin approval, encryption of the account encryption key by the admin, and subsequent decryption by the initiating client.

```APIDOC
1. The initiating client POSTs a request, which includes the account email address and a unique auth-request public key, to an Authentication Request table in the Bitwarden database.
2. Administrators can approve or deny the request on the Device approvals page.
3. When the request is approved by an administrator, the approving client encrypts the user's account encryption key using the auth-request public key enclosed in the request.
4. The approving client then PUTs the encrypted account encryption key to the Authentication Request record and marks the request fulfilled.
5. The initiating client GETs the encrypted account encryption key and locally decrypts it using the auth-request private key.
6. Using the decrypted account encryption key, trust is established with the client as described in the Onboarding tab.
```

--------------------------------

### Duo Portal: Service Provider Configuration Fields

Source: https://bitwarden.com/help/cli/saml-duo

Details the fields required to configure the Service Provider settings within the Duo Admin Portal for Bitwarden SAML SSO. These fields define how Duo identifies Bitwarden as a service provider.

```APIDOC
Field: Entity ID
Description: Set this field to the pre-generated SP Entity ID. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.

Field: Assertion Consumer Service (ACS) URL
Description: Set this field to the pre-generated Assertion Consumer Service (ACS) URL. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.

Field: Service Provider Login URL
Description: Set this field to the login URL from which users will access Bitwarden. For cloud-hosted customers, this is `https://vault.bitwarden.com/#/sso` or `https://vault.bitwarden.eu/#/sso.` For self-hosted instances, this is determined by your [configured server URL](/help/install-on-premise/#configure-your-domain), for example `https://your.domain.com/#/sso`.
```

--------------------------------

### TOTP Parameter Customization Reference

Source: https://bitwarden.com/help/cli/integrated-authenticator

This table details the available parameters for customizing Time-based One-Time Passwords (TOTPs) within Bitwarden using `otpauth://` URIs. It specifies the cryptographic algorithm, number of digits, and rotation period that can be configured.

```APIDOC
Parameter | Description | Values | Sample Query
--- | --- | --- | ---
Algorithm | Cryptographic algorithm used to generate TOTPs. | -sha1 -sha256 -sha512 -otpauth | `algorithm=sha256`
Digits | Number of digits in the generated TOTP. | 1-10 | `digits=8`
Period | Number of seconds with which to rotate the TOTP. | Must be > 0 | `period=60`
```

--------------------------------

### Bitwarden Web App OIDC Configuration Fields

Source: https://bitwarden.com/help/cli/oidc-okta

Details the required and optional fields to configure OpenID Connect (OIDC) single sign-on in the Bitwarden web application using Okta as the identity provider. These fields are configured in the Bitwarden web app after setting up Okta.

```APIDOC
Bitwarden Web App OIDC Configuration Fields:
  Authority:
    Description: Enter the retrieved Issuer URI for your Authorization Server.
  Client ID:
    Description: Enter the retrieved Client ID for your Okta app.
  Client Secret:
    Description: Enter the retrieved Client secret for your Okta app.
  Metadata Address:
    Description: Enter the retrieved Metadata URI for your Authorization Server.
  OIDC Redirect Behavior:
    Description: Select Redirect GET. Okta currently does not support Form POST.
  Get Claims From User Info Endpoint:
    Description: Enable this option if you receive URL too long errors (HTTP 414), truncated URLS, and/or failures during SSO.
  Additional/Custom Scopes:
    Description: Define custom scopes to be added to the request (comma-delimited).
  Additional/Custom User ID Claim Types:
    Description: Define custom claim type keys for user identification (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
  Additional/Custom Email Claim Types:
    Description: Define custom claim type keys for users' email addresses (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
  Additional/Custom Name Claim Types:
    Description: Define custom claim type keys for users' full names or display names (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
  Requested Authentication Context Class Reference values:
    Description: Define Authentication Context Class Reference identifiers (`acr_values`) (space-delimited). List `acr_values` in preference-order.
  Expected "acr" Claim Value in Response:
    Description: Define the `acr` Claim Value for Bitwarden to expect and validate in the response.
```

--------------------------------

### Troubleshoot TOTP: Sync Windows Device Time with PowerShell

Source: https://bitwarden.com/help/cli/integrated-authenticator

These PowerShell commands help re-synchronize your Windows device's time zone, which is crucial for correct TOTP generation. Replace the placeholder with your actual time zone ID and restart your computer for changes to take effect.

```PowerShell
Set-TimeZone -Id "Central Standard Time"
```

```PowerShell
Restart-Computer
```

--------------------------------

### Configure Bitwarden CLI Server Settings

Source: https://bitwarden.com/help/cli/cli

Commands to specify and manage server settings for the Bitwarden CLI, including connecting to self-hosted or specific regional servers, and configuring individual service URLs. Note that any subsequent use of the config command will overwrite all previous specifications.

```bash
bw config server <setting> [value]
```

```bash
bw config server https://your.bw.domain.com
```

```bash
bw config server https://vault.bitwarden.eu
```

```bash
bw config server --web-vault <url> \
  --api <url> \
  --identity <url> \
  --icons <url> \
  --notifications <url> \
  --events <url> \
  --key-connector <url>
```

--------------------------------

### Configure Yubico Validation URLs

Source: https://bitwarden.com/help/cli/environment-variables

Define the primary URL for your self-hosted Yubico Validation Server. Additional validation server URLs can be added by incrementing the environment variable index.

```APIDOC
globalSettings__yubico__validationUrls__0=https://your.url.com/wsapi/2.0/verify
globalSettings__yubico__validationUrls__1=
globalSettings__yubico__validationUrls__2=
```

--------------------------------

### Duo Identity Provider Configuration Fields for Bitwarden SAML SSO

Source: https://bitwarden.com/help/cli/saml-duo

Details the required fields and their descriptions for configuring Duo as an identity provider for Bitwarden SAML Single Sign-On. This includes information on Entity ID, Binding Type, Service URLs, X509 Certificate, and signing algorithms.

```APIDOC
IdentityProviderConfiguration:
  Entity ID:
    description: "Enter the Entity ID value of your Duo application, which can be retrieved from the Duo app Metadata section. This field is case sensitive."
  Binding Type:
    description: "Set this field to HTTP Post."
  Single Sign On Service URL:
    description: "Enter the Single Sign-On URL value of your Duo application, which can be retrieved from the Duo app Metadata section."
  Single Log Out Service URL:
    description: "Login with SSO currently does not support SLO. This option is planned for future development, however you may pre-configure with the Single Log-Out URL value of your Duo application."
  X509 Public Certificate:
    description: "Paste the downloaded certificate, removing -----BEGIN CERTIFICATE----- and -----END CERTIFICATE-----. The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters will cause certification validation to fail."
  Outbound Signing Algorithm:
    description: "Set this field to the selected SAML Response signature algorithm."
  Disable Outbound Logout Requests:
    description: "Login with SSO currently does not support SLO. This option is planned for future development."
  Want Authentication Requests Signed:
    description: "Whether Duo expects SAML requests to be signed."
```

--------------------------------

### Enable Plaintext Secret Storage for D-Bus Errors

Source: https://bitwarden.com/help/cli/directory-sync-cli

To resolve D-Bus related errors (e.g., "Failed to execute child process \"dbus-launch\"" or "Cannot autolaunch D-Bus without X11") when using `bwdc config`, set this environment variable. This allows secrets to be stored in plaintext in `data.json`.

```Bash
export BITWARDENCLI_CONNECTOR_PLAINTEXT_SECRETS=true
```

--------------------------------

### Bitwarden Event Types and Codes

Source: https://bitwarden.com/help/cli/event-logs

This API documentation outlines the various event types recorded by Bitwarden across different categories like items, collections, groups, organizations, and secrets manager, along with their corresponding numeric identifiers. It also describes how provider-initiated events are logged.

```APIDOC
Item Events:
  - 1100: Created item {item-identifier}
  - 1101: Edited item {item-identifier}
  - 1102: Permanently Deleted item {item-identifier}
  - 1103: Created attachment for item {item-identifier}
  - 1104: Deleted attachment for item {item-identifier}
  - 1105: Moved item {item-identifier} to an organization
  - 1106: Edited collections for item {item-identifier}
  - 1107: Viewed item {item-identifier}
  - 1108: Viewed password for item {item-identifier}
  - 1109: Viewed hidden field for item {item-identifier}
  - 1110: Viewed security code for item {item-identifier}
  - 1111: Copied password for item {item-identifier}
  - 1112: Copied hidden field for item {item-identifier}
  - 1113: Copied security code for item {item-identifier}
  - 1114: Autofilled item {item-identifier}
  - 1115: Sent item {item-identifier} to trash
  - 1116: Restored item {item-identifier}
  - 1117: Viewed Card Number for item {item-identifier}

Collection Events:
  - 1300: Created collection {collection-identifier}
  - 1301: Edited collection {collection-identifier}
  - 1302: Deleted collection {collection-identifier}

Group Events:
  - 1400: Created group {group-identifier}
  - 1401: Edited group {group-identifier}
  - 1402: Deleted group {group-identifier}

Organization Events:
  - 1500: Invited user {user-identifier}
  - 1501: Confirmed user {user-identifier}
  - 1502: Edited user {user-identifier}
  - 1503: Removed user {user-identifier}
  - 1504: Edited groups for user {user-identifier}
  - 1505: Unlinked SSO for user {user-identifier}
  - 1506: {user-identifier} enrolled in account recovery
  - 1507: {user-identifier} withdrew from account recovery
  - 1508: Master Password reset for {user-identifier}
  - 1509: Reset SSO link for user {user-identifier}
  - 1510: {user-identifier} logged in using SSO for the first time
  - 1511: Revoked organization access for {user-identifier}
  - 1512: Restored organization access for {user-identifier}
  - 1513: Approved device for {user-identifier}
  - 1514: Denied device for {user-identifier}
  - 1515: Deleted user {user-identifier} - an owner/admin deleted the user account
  - 1516: User {user-identifier} left organization
  - 1600: Edited organization settings
  - 1601: Purged organization vault
  - 1602: Exported organization vault
  - 1603: Organization Vault access by a managing Provider
  - 1604: Organization enabled SSO
  - 1605: Organization disabled SSO
  - 1606: Organization enabled Key Connector
  - 1607: Organization disabled Key Connector
  - 1608: Families Sponsorships synced
  - 1609: Modified collection management setting
  - 1700: Modified policy {policy-identifier}
  - 2000: Added domain {domain-name}
  - 2001: Removed domain {domain-name}
  - 2002: {Domain-name} verified
  - 2003: {Domain-name} not verified

Secrets Manager Events:
  - 2100: Accessed secret {secret-identifier}

Provider Events:
  - Description: When any of the above events is executed by a member of an administering provider, the User column will record the name of the provider. Additionally, a provider-specific event will record whenever a member of an administering provider accesses your organization vault.
```

--------------------------------

### Bitwarden SAML Service Provider Configuration Fields

Source: https://bitwarden.com/help/cli/saml-adfs

Defines the configurable fields within the Bitwarden web app's SAML service provider section, detailing their purpose and expected values for proper SAML request formatting.

```APIDOC
SAML Service Provider Configuration Fields:
  Name ID Format: Select the Outgoing Name ID Format selected when constructing claims issuance rules (see Rule 3).
  Outbound Signing Algorithm: The algorithm Bitwarden will use to sign SAML requests.
  Signing Behavior: Whether/when SAML requests will be signed.
  Minimum Incoming Signing Algorithm: By default, AD FS will sign with SHA-256. Select SHA-256 from the dropdown unless you have configured AD FS to use different algorithm.
  Want Assertions Signed: Whether Bitwarden expects SAML assertions to be signed.
  Validate Certificates: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured within the Bitwarden login with SSO docker image.
```

--------------------------------

### Okta Web App Integration Configuration Fields

Source: https://bitwarden.com/help/cli/oidc-okta

This APIDOC snippet details the required fields and their descriptions for configuring a new Web Application integration in the Okta Admin Portal, specifically for Bitwarden SSO via OIDC. It covers grant types, redirect URIs, and assignment settings.

```APIDOC
"App integration name": "Give the app a Bitwarden-specific name.",
"Grant type": "Enable the following grant types:\n  - Client acting on behalf of itself → Client Credentials\n  - Client acting on behalf of a user → Authorization Code",
"Sign-in redirect URIs": "Set this field to your Callback Path, which can be retrieved from the Bitwarden SSO Configuration screen.\nFor cloud-hosted customers, this is https://sso.bitwarden.com/oidc-signin or https://sso.bitwarden.eu/oidc-signin. For self-hosted instances, this is determined by your configured server URL, for example https://your.domain.com/sso/oidc-signin.",
"Sign-out redirect URIs": "Set this field to your Signed Out Callback Path, which can be retrieved from the Bitwarden SSO Configuration screen.",
"Assignments": "Use this field to designate whether all or only select groups will be able to use Bitwarden Login with SSO."
```

--------------------------------

### Update and Restart Bitwarden Server

Source: https://bitwarden.com/help/cli/install-and-deploy-offline

Stops all running Bitwarden server containers and then restarts them in detached mode. This command is used to apply updated configurations or container images during a manual server update process.

```Bash
docker compose -f ./docker/docker-compose.yml down && docker compose -f ./docker/docker-compose.yml up -d
```

--------------------------------

### Retrieve Bitwarden CLI Status Information

Source: https://bitwarden.com/help/cli/cli

The `bw status` command provides detailed information about the Bitwarden CLI's current state, including the configured server URL, last sync timestamp, user email and ID, and vault status (unlocked, locked, or unauthenticated). The output is returned as a JSON object.

```Bash
bw status
```

```JSON
{
  "serverUrl": "https://bitwarden.example.com",
  "lastSync": "2020-06-16T06:33:51.419Z",
  "userEmail": "user@example.com",
  "userId": "00000000-0000-0000-0000-000000000000",
  "status": "unlocked"
}
```

--------------------------------

### Configure Bitwarden Mobile App with Self-Hosted Server URL

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This API documentation outlines the application configuration key and value type required to pre-configure Bitwarden Mobile apps for deployment with a self-hosted server URL. Administrators can use MDM/EMM solutions to apply this setting before deployment.

```APIDOC
Configuration Key: baseEnvironmentUrl
Value Type: string
Configuration Value: Your self-hosted Server URL, for example https://my.bitwarden.server.com
```

--------------------------------

### Bitwarden TOTP Parameter Customization Reference

Source: https://bitwarden.com/help/cli/authenticator-keys

This table details the available parameters for customizing Time-based One-Time Passwords (TOTPs) within Bitwarden using `otpauth://` URIs. It specifies the cryptographic algorithm, number of digits, and rotation period that can be configured for generated TOTP codes.

```APIDOC
Parameter | Description | Values | Sample Query
--- | --- | --- | ---
Algorithm | Cryptographic algorithm used to generate TOTPs. | -sha1 -sha256 -sha512 -otpauth | `algorithm=sha256`
Digits | Number of digits in the generated TOTP. | 1-10 | `digits=8`
Period | Number of seconds with which to rotate the TOTP. | Must be > 0 | `period=60`
```

--------------------------------

### Run Bitwarden CLI in Docker with Mounted Config File

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This Docker command runs the Bitwarden CLI container, mounting a local configuration file into the container and passing an access token as an environment variable. This allows for running CLI commands within a Dockerized environment using custom configurations.

```Plain
docker run -it -v /PATH/TO/YOUR/CONFIGFILE:/home/app/.bws/config -e BWS_ACCESS_TOKEN=<ACCESS_TOKEN_VALUE> bitwarden/bws secret list
```

--------------------------------

### Bitwarden Invoked Cryptographic Libraries

Source: https://bitwarden.com/help/cli/what-encryption-is-used

A comprehensive list of the popular and reputable cryptographic libraries and crates that Bitwarden utilizes across its JavaScript and Rust implementations, ensuring security through expert-maintained primitives.

```JavaScript
JavaScript Libraries:
  - Web crypto (https://www.w3.org/TR/WebCryptoAPI/)
  - Node.js crypto (https://nodejs.org/api/crypto.html)
  - Forge (https://github.com/digitalbazaar/forge)
  - Argon2 (https://github.com/antelle/argon2-browser)
```

```Rust
Rust Crates:
  - RustCrypto (https://github.com/rustcrypto)
  - curve25519-dalek (https://github.com/dalek-cryptography/curve25519-dalek)
  - rust-random (https://github.com/rust-random/)
  - rustls (https://github.com/rustls/rustls)
```

--------------------------------

### Combine OU Sync with User Attribute Filter

Source: https://bitwarden.com/help/cli/gsuite-directory

This filter syncs users from the `/Engineering` organizational unit who also have the `orgTitle` of `Manager`. More user attributes than `orgTitle` can be combined with OU queries and are available in the Google Directory API documentation.

```Bash
|orgUnitPath=/Engineering orgTitle:Manager
```

--------------------------------

### Add Kerberos Volume Mounts to Bitwarden Docker Compose Override

Source: https://bitwarden.com/help/cli/kerberos-integration

This Docker Compose snippet adds volume mounts for the Kerberos directory (`../kerberos`) to several Bitwarden service containers (admin, sso, identity, api, events). This ensures that the Kerberos configuration files are accessible within the containers.

```YAML
services:
    admin:
        volumes:
            - ../kerberos:/etc/bitwarden/kerberos
    sso:
        volumes:
            - ../kerberos:/etc/bitwarden/kerberos
    identity:
        volumes:
            - ../kerberos:/etc/bitwarden/kerberos
    api:
        volumes:
            - ../kerberos:/etc/bitwarden/kerberos
    events:
        volumes:
            - ../kerberos:/etc/bitwarden/kerberos
```

--------------------------------

### Create Kubernetes Secret for Bitwarden Configuration using kubectl

Source: https://bitwarden.com/help/cli/self-host-with-helm

This snippet demonstrates how to create a Kubernetes generic secret named `custom-secret` in the `bitwarden` namespace using the `kubectl create secret` command. It sets critical Bitwarden configuration values as literal strings, including `globalSettings__installation__id`, `globalSettings__installation__key`, SMTP credentials, Yubico client ID/key, HIBP API key, and `SA_PASSWORD` for the SQL pod. Users must replace 'REPLACE' placeholders with their actual sensitive data. A warning is included that this method may record commands to shell history, suggesting more secure alternatives for production environments.

```Bash
kubectl create secret generic custom-secret -n bitwarden \
    --from-literal=globalSettings__installation__id="REPLACE" \
    --from-literal=globalSettings__installation__key="REPLACE" \
    --from-literal=globalSettings__mail__smtp__username="REPLACE" \
    --from-literal=globalSettings__mail__smtp__password="REPLACE" \
    --from-literal=globalSettings__yubico__clientId="REPLACE" \
    --from-literal=globalSettings__yubico__key="REPLACE" \
    --from-literal=globalSettings__hibpApiKey="REPLACE" \
    --from-literal=SA_PASSWORD="REPLACE"
```

--------------------------------

### Update Linux CA Certificate Store

Source: https://bitwarden.com/help/cli/certificates

Commands to reconfigure and update the system's CA certificate store on Debian/Ubuntu-based Linux distributions after adding new certificates.

```Bash
sudo dpkg-reconfigure ca-certificates
sudo update-ca-certificates
```

--------------------------------

### Create Firefox Executable Symlink (Linux)

Source: https://bitwarden.com/help/cli/deactivate-browser-password-managers

This command creates a symbolic link (symlink) from the Firefox executable in `/opt/firefox` to `/usr/local/bin/firefox`. This allows users to launch Firefox simply by typing `firefox` in the terminal, as `/usr/local/bin` is typically in the system's PATH.

```Shell
ln -s /opt/firefox /usr/local/bin/firefox
```

--------------------------------

### Promote Password Manager Benefits Email Template

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

Offers an email template to highlight the value and benefits a password manager will bring to end-users, encouraging team excitement and adoption by listing key advantages and providing relevant resources.

```Email
Subject: Promote the top benefits

Body:

Hi *[name]*,

Make sure the end-users understand the value and benefits a password manager will bring to their work.

To get your team excited about Bitwarden, here are three primary benefits to share with everyone:

1. Easily access all your passwords anytime, anywhere, on any device.
2. Securely share credentials with others.
3. Streamline logging into your accounts with auto-fill.

Here are a few resources on the benefits of a password manager that you can send to employees:

* Share this [password strength testing tool](/password-strength/) - let the gamification begin!
* [Blog] [How a password manager adds productivity at the office](/blog/how-a-password-manager-adds-to-productivity-at-the-office/)
* [Blog] [A better password workflow with Bitwarden](/blog/a-better-password-workflow-with-bitwarden/)
* [Blog] [How to better manage your financial information in Bitwarden](/blog/how-to-better-manage-your-financial-information-in-Bitwarden/)
* [Blog] [7 steps to create a secure (and private) profile online](/blog/7-steps-to-create-a-secure-and-private-profile-online/)
```

--------------------------------

### Stop Bitwarden Docker Compose Deployment for Update

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command stops and removes containers, networks, and volumes defined in the docker-compose.yml file, which is a common step before updating services.

```Bash
docker compose down
```

--------------------------------

### Cron Job Scheduling Expression Reference

Source: https://bitwarden.com/help/cli/schedule-directory-sync

This snippet provides a visual reference for the cron job scheduling expression format, explaining the meaning of each asterisk position (minute, hour, day of month, month, day of week) and where to place the command to execute.

```Bash
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday;
# │ │ │ │ │                                   7 is also Sunday on some systems)
# │ │ │ │ │
# │ │ │ │ │
# * * * * * <command to execute>
```

--------------------------------

### Bitwarden Account Creation: Master Password Hash Generation

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Details the generation of the Master Password Hash using PBKDF-SHA256 for user authentication, including its subsequent server-side hashing.

```APIDOC
Function: GenerateMasterPasswordHash
  Description: Generates a hash of the master password for authentication.
  Parameters:
    master_key: 256-bit binary (Derived Master Key)
    master_password: string (User's master password, used as salt)
  Algorithm: PBKDF-SHA256
  Returns: MasterPasswordHash (sent to server for authentication)

ServerProcess: ServerSideMasterPasswordHashHashing
  Description: Re-hashes the received Master Password Hash on the server.
  Parameters:
    received_master_password_hash: string (Master Password Hash from client)
  Algorithm: PBKDF2-SHA256
  Salt: Random
  Iterations: 600,000
  Returns: ServerStoredMasterPasswordHash
```

--------------------------------

### Duo SAML Identity Provider Metadata Retrieval

Source: https://bitwarden.com/help/cli/saml-duo

Details on retrieving essential SAML metadata values from the Duo Admin Portal, which are required for configuring the Identity Provider settings in Bitwarden.

```APIDOC
Duo SAML Identity Provider Configuration (Metadata Section):
  - Identity Provider SSO URL: [Value from Duo Admin Portal]
  - Identity Provider Entity ID: [Value from Duo Admin Portal]
  - Certificate Fingerprint: [Value from Duo Admin Portal]
  Note: These values are for reference and do not require editing in Duo.
```

--------------------------------

### Configure Bitwarden Helm for External MSSQL Database

Source: https://bitwarden.com/help/cli/external-db

Outlines the process for connecting a self-hosted Bitwarden Helm instance to an external MSSQL database. This involves disabling the included SQL pod in `my-values.yaml` and configuring the connection string within a Kubernetes secrets object, detailing required parameters.

```Configuration
1. Create a new MSSQL database.
2. (Recommended) Create a dedicated DBO for your database.
3. In your `my-values.yaml` configuration file, set the value `database.enabled: false` to stop the included SQL pod from being deployed.
4. In the Kubernetes secrets object used for deployment, set a `globalSettings__sqlServer__connectionString=` value with the following information:
   * `Data Source=tcp:<SERVERNAME>,1433` where `<SERVERNAME>` is your MSSQL server's name.
   * `Initial Catalog=<VAULT>` where `<VAULT>` is your database name.
   * `Persist Security Info=False`.
   * `User ID=<USER>` where `<USER>` is your DBO user ID.
   * `Password=<PASSWORD>` where `<PASSWORD>` is your DBO password.
   * `Multiple Active Result Sets=False`.
   * `Connect Timeout=30`.
   * `Encrypt=True`.
   * `Trust Server Certificate=true`. This value can be set to `false` if your require that the Bitwarden server validates your MSSQL server's certificate.
```

--------------------------------

### Bitwarden CLI: `bw send edit` Command Syntax

Source: https://bitwarden.com/help/cli/send-cli

Shows the basic syntax for the `bw send edit` command, which allows editing an existing Send by taking encoded JSON as an argument.

```Bash
bw send edit <encodedJson>
```

--------------------------------

### User Filter: Combine OU Path with User Attribute

Source: https://bitwarden.com/help/cli/workspace-directory

This filter combines an organizational unit (OU) path with an additional user attribute to refine the sync. Users within the specified OU (e.g., `/Engineering`) are further filtered by an attribute like `orgTitle:Manager`, syncing only managers in that OU. More attributes can be found in Google Directory API documentation.

```Bash
|orgUnitPath=/Engineering orgTitle:Manager
```

--------------------------------

### Bitwarden CLI: `bw send edit` Command Options

Source: https://bitwarden.com/help/cli/send-cli

Available options for the `bw send edit` command, allowing overwriting the Send's ID.

```APIDOC
Options:
* --itemid <itemid>: Overwrite the id value provided of the Send with a new one.
```

--------------------------------

### Configure Bitwarden CLI Server Base URL

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command sets the base URL for a self-hosted Bitwarden server. If `server_api` and `server_identity` are not explicitly configured, their values will default based on this `server-base` URL.

```Bash
bws config server-base https://my_hosted_server.com
```

--------------------------------

### Log out from Bitwarden Directory Connector CLI

Source: https://bitwarden.com/help/cli/directory-sync-cli

Use the `logout` command to terminate your session with the Directory Connector CLI.

```Bash
bwdc logout
```

--------------------------------

### Sync Bitwarden Directory Connector Groups by Member Key

Source: https://bitwarden.com/help/cli/gsuite-directory

This snippet illustrates how to sync all groups to which a specific user, identified by their member key (email address), belongs. This ensures that only relevant groups for a particular user are synchronized.

```Bash
|memberKey=user@company.com
```

--------------------------------

### Pass Bitwarden CLI session key as command option

Source: https://bitwarden.com/help/cli/cli

Provides an alternative method for using the session key if the `BW_SESSION` environment variable is not set. The session key can be passed directly as an option (`--session`) with each `bw` command that requires vault data access.

```Bash
bw list items --session "5PBYGU+5yt3RHcCjoeJKx/wByU34vokGRZjXpSH7Ylo8w=="
```

--------------------------------

### Create Microsoft Entra ID App Registration for Bitwarden Directory Connector

Source: https://bitwarden.com/help/cli/microsoft-entra-id

Follow these steps to register a new application in the Microsoft Azure Portal, which will be used by the Bitwarden Directory Connector.

```APIDOC
1. From your Microsoft Azure portal, navigate to the Microsoft Entra ID directory.
2. From the left-hand navigation, select App registrations or enter App registrations into the search bar.
3. Select the New registration button and give your registration a Bitwarden-specific name (such as, `bitwarden-dc`).
4. Select Register.
```

--------------------------------

### Authenticate Bitwarden Secrets Manager CLI Inline with Access Token Flag

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command demonstrates authenticating a specific CLI request by providing the access token directly using the `--access-token` flag. This method is useful for individual commands where persistent environment variable authentication is not desired.

```Bash
bws secret list --access-token 0.48c78342-1635-48a6-accd-afbe01336365.C0tMmQqHnAp1h0gL8bngprlPOYutt0:B3h5D+YgLvFiQhWkIq6Bow==
```

--------------------------------

### Create OpenShift Generic Secret for Bitwarden Configuration

Source: https://bitwarden.com/help/cli/openshift-deployment

This Bash command creates a generic OpenShift secret named `custom-secret` within the `bitwarden` namespace. It populates the secret with various Bitwarden global settings and credentials using literal values. Users must replace 'REPLACE' placeholders with actual sensitive data. A warning is provided that this method records commands to shell history, suggesting alternative secure methods for setting secrets.

```Bash
oc create secret generic custom-secret -n bitwarden \
    --from-literal=globalSettings__installation__id="REPLACE" \
    --from-literal=globalSettings__installation__key="REPLACE" \
    --from-literal=globalSettings__mail__smtp__username="REPLACE" \
    --from-literal=globalSettings__mail__smtp__password="REPLACE" \
    --from-literal=globalSettings__yubico__clientId="REPLACE" \
    --from-literal=globalSettings__yubico__key="REPLACE" \
    --from-literal=globalSettings__hibpApiKey="REPLACE" \
    --from-literal=SA_PASSWORD="REPLACE" # If using SQL pod
    # --from-literal=globalSettings__sqlServer__connectionString="REPLACE" # If using your own SQL server
```

--------------------------------

### Configure SAML SSO in Bitwarden Web App

Source: https://bitwarden.com/help/cli/saml-aws

This snippet details the initial steps to configure SAML 2.0 Single Sign-On within the Bitwarden web application, including navigating to settings, creating an SSO identifier, and selecting the SAML type.

```APIDOC
1. Log in to the Bitwarden web app.
2. Open the Admin Console using the product switcher.
3. Open your organization's Settings -> Single sign-on screen.
4. Create a unique SSO identifier for your organization.
5. Select SAML from the Type dropdown.
6. (Optional) Turn off the Set a unique SP entity ID option if you wish. It is generally recommended to leave this option on.
```

--------------------------------

### Set Git gpg.ssh.program for Windows SSH-Keygen

Source: https://bitwarden.com/help/cli/ssh-agent

Configure the `gpg.ssh.program` parameter in Git to specify the path to `ssh-keygen.exe` for GPG SSH operations on Windows.

```Plain
git config gpg.ssh.program "C:/Windows/System32/OpenSSH/ssh-keygen.exe"
```

--------------------------------

### Include Groups by Name in Directory Connector Sync

Source: https://bitwarden.com/help/cli/azure-active-directory

Syntax to include specific groups in a Bitwarden Directory Connector sync based on their names. Use a comma-separated list of group names.

```Bash
include:Group A,Group B
```

--------------------------------

### Bitwarden Community Contribution URL

Source: https://bitwarden.com/help/cli/bitwarden-addresses

Specifies the dedicated URL for accessing Bitwarden's community contribution guidelines and resources.

```APIDOC
contributing.bitwarden.com
```

--------------------------------

### Authenticate Bitwarden Secrets Manager CLI using Environment Variable

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command sets the `BWS_ACCESS_TOKEN` environment variable with your access token. This token is then automatically used by the CLI for authentication, granting access to secrets and projects associated with the machine account.

```Bash
export BWS_ACCESS_TOKEN=0.48c78342-1635-48a6-accd-afbe01336365.C0tMmQqHnAp1h0gL8bngprlPOYutt0:B3h5D+YgLvFiQhWkIq6Bow==
```

--------------------------------

### Synchronize Bitwarden Vault Data

Source: https://bitwarden.com/help/cli/cli

The `sync` command downloads the encrypted vault from the Bitwarden server to the CLI. This command is most useful when changes have been made in your Bitwarden vault on another client application. The `--last` option can be passed to return only the timestamp of the last sync.

```bash
bw sync
```

--------------------------------

### Configure Bitwarden Mobile App via MDM/EMM

Source: https://bitwarden.com/help/cli/deploy-clients

Administrators can pre-configure Bitwarden Mobile apps using Mobile Device Management (MDM) or Enterprise Mobility Management (EMM) solutions. This API documentation specifies the configuration key and value type required to set a self-hosted Server URL for mobile app deployments.

```APIDOC
Configuration Key: baseEnvironmentUrl
Value Type: string
Configuration Value: Your self-hosted Server URL, for example https://my.bitwarden.server.com
```

--------------------------------

### Include Users by Email in Directory Connector Sync

Source: https://bitwarden.com/help/cli/azure-active-directory

Syntax to include specific users in a Bitwarden Directory Connector sync based on their email addresses. Use a comma-separated list of emails.

```Bash
include:joe@example.com,bill@example.com,tom@example.com
```

--------------------------------

### Filter Groups by Type

Source: https://bitwarden.com/help/cli/okta-directory

Shows how to filter groups based on their `type` attribute, such as `BUILT_IN`, using a direct filter query prefixed with a pipe (`|`). This targets specific group types for synchronization.

```Bash
|type eq "BUILT_IN"
```

--------------------------------

### JSON Format for Bitwarden Organization Import

Source: https://bitwarden.com/help/cli/condition-bitwarden-import

Create a UTF-8 encoded plaintext JSON file to import organization-wide data into Bitwarden. This format includes collections and items, allowing for shared logins and custom fields within an organization. When importing, select 'Bitwarden (json)' as the file format.

```JSON
{
  "collections": [
    {
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "organizationId": "yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy",
      "name": "My Collection",
      "externalId": null
    },
    ...
  ],
  "items": [
    {
      "passwordHistory": [
        {
          "lastUsedDate": "YYYY-MM-00T00:00:00.000Z",
          "password": "passwordValue"
        }
      ],
    "revisionDate": "YYYY-MM-00T00:00:00.000Z",
    "creationDate": "YYYY-MM-00T00:00:00.000Z",
    "deletedDate": null,
    "id": "vvvvvvvv-vvvv-vvvv-vvvv-vvvvvvvvvvvv",
    "organizationId": "yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy",
    "folderId": "zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz",
    "type": 1,
    "reprompt": 1,
    "name": "Our Shared Login",
    "notes": "A login for sharing",
    "favorite": false,
    "fields": [
        {
          "name": "custom-field-1",
          "value": "custom-field-value",
          "type": 0
        },
        ...
      ],
      "login": {
        "uris": [
          {
            "match": null,
            "uri": "https://mail.google.com"
          }
        ],
        "username": "myaccount@gmail.com",
        "password": "myaccountpassword",
        "totp": "otpauth://totp/my-secret-key"
      },
      "collectionIds": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    },
    ...
  ]
}
```

--------------------------------

### Bitwarden SAML Identity Provider Configuration Fields

Source: https://bitwarden.com/help/cli/ping-identity-saml-implementation

Outlines the fields necessary to configure Ping Identity as a SAML identity provider for Bitwarden, covering Entity ID, SSO URL, certificate handling, and signing preferences.

```APIDOC
Identity Provider Configuration Fields:
- Entity ID: Set this field to the Ping Identity application's Entity ID, retrieved from the Ping Identity Configuration screen.
- Binding Type: Set to HTTP POST or Redirect.
- Single Sign On Service URL: Set this field to the Ping Identity application's Single Sign-on Service url, retrieved from the Ping Identity Configuration screen.
- Single Log Out URL: Login with SSO currently does not support SLO. This option is planned for future development, however you may pre-configure it if you wish.
- X509 Public Certificate: Paste the signing certificate retrieved from the application screen. Navigate to the Configuration tab and Download Signing Certificate. Example format: `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----`. The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters will cause certification validation to fail.
- Outbound Signing Algorithm: By default, Ping Identity will sign with RSA SHA-256. Select `sha-256` from the dropdown.
- Disable Outbound Logout Requests: Login with SSO currently does not support SLO. This option is planned for future development.
- Want Authentication Requests Signed: Whether Ping Identity expects SAML requests to be signed.
```

--------------------------------

### Configure Bitwarden Identity Provider for JumpCloud SAML

Source: https://bitwarden.com/help/cli/saml-jumpcloud

This section outlines the fields necessary to configure the Identity Provider settings within Bitwarden, referring to values retrieved from the JumpCloud Portal. It covers Entity ID, Binding Type, Single Sign On Service URL, Single Log Out Service URL, X509 Public Certificate, Outbound Signing Algorithm, Disable Outbound Logout Requests, and Want Authentication Requests Signed.

```APIDOC
Identity Provider Configuration Fields:
- Entity ID: Enter your JumpCloud IdP Entity ID, which can be retrieved from the JumpCloud Single Sign-On Configuration screen. This field is case sensitive.
- Binding Type: Set to Redirect.
- Single Sign On Service URL: Enter your JumpCloud IdP URL, which can be retrieved from the JumpCloud Single Sign-On Configuration screen.
- Single Log Out Service URL: Login with SSO currently does not support SLO. This option is planned for future development.
- X509 Public Certificate: Paste the retrieved certificate, removing -----BEGIN CERTIFICATE----- and -----END CERTIFICATE-----. The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters will cause certification validation to fail.
- Outbound Signing Algorithm: If you created a Custom SAML Application, set this to whichever Signature Algorithm you selected. Otherwise, leave as rsa-sha256.
- Disable Outbound Logout Requests: Login with SSO currently does not support SLO. This option is planned for future development.
- Want Authentication Requests Signed: Whether JumpCloud expects SAML requests to be signed.
```

--------------------------------

### Set Permissions for Firefox Policies Directory on Linux

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This Bash command sets the permissions for the /etc/firefox/policies directory and its contents to 755 (read, write, execute for owner; read and execute for group and others). This ensures that administrators can manage the policy files while maintaining appropriate access for the system.

```Bash
chmod -R 755 /etc/firefox/policies
```

--------------------------------

### Base64 Encode Standard Input with Bitwarden CLI

Source: https://bitwarden.com/help/cli/cli

The `encode` command Base64 encodes data from standard input. This command is typically used in combination with a command-line JSON processor like `jq` when performing `create` and `edit` operations, allowing for programmatic modification of data before sending it to Bitwarden.

```bash
bw get template folder | jq '.name="My First Folder"' | bw encode | bw create folder
```

```bash
bw get item 7ac9cae8-5067-4faf-b6ab-acfd00e2c328 | jq '.login.password="newp@ssw0rd"' | bw encode | bw edit item 7ac9cae8-5067-4faf-b6ab-acfd00e2c328
```

--------------------------------

### Configure Bitwarden Helm Chart Ingress for Azure Application Gateway

Source: https://bitwarden.com/help/cli/azure-aks-deployment

This YAML configuration snippet updates the `general.ingress` section of the `my-values.yaml` file for the Bitwarden Helm chart. It enables ingress, specifies `azure-application-gateway` as the class name, and defines critical annotations for SSL redirection, private IP usage, and a custom rewrite rule set. It also configures TLS certificate details and comprehensive path routing for various Bitwarden services.

```YAML
general:
  domain: "replaceme.com"
  ingress:
    enabled: true
    className: "azure-application-gateway" # This value might be different depending on how you created your ingress controller.  Use "kubectl get ingressclasses -A" to find the name if unsure.
     ## - Annotations to add to the Ingress resource.
    annotations:
      appgw.ingress.kubernetes.io/ssl-redirect: "true"
      appgw.ingress.kubernetes.io/use-private-ip: "false" # This might be true depending on your setup.
      appgw.ingress.kubernetes.io/rewrite-rule-set: "bitwarden-ingress" # Make note of whatever you set this value to.  It will be used later.
      appgw.ingress.kubernetes.io/connection-draining: "true" # Update as necessary.
      appgw.ingress.kubernetes.io/connection-draining-timeout: "30" # Update as necessary.
    ## - Labels to add to the Ingress resource.
    labels: {}
    # Certificate options.
    tls:
      # TLS certificate secret name.
      name: tls-secret
      # Cluster cert issuer (e.g. Let's Encrypt) name if one exists.
      clusterIssuer: letsencrypt-staging
    paths:
      web:
        path: /(.*)
        pathType: ImplementationSpecific
      attachments:
        path: /attachments/(.*)
        pathType: ImplementationSpecific
      api:
        path: /api/(.*)
        pathType: ImplementationSpecific
      icons:
        path: /icons/(.*)
        pathType: ImplementationSpecific
      notifications:
        path: /notifications/(.*)
        pathType: ImplementationSpecific
      events:
        path: /events/(.*)
        pathType: ImplementationSpecific
      scim:
         path: /scim/(.*)
         pathType: ImplementationSpecific
      sso:
        path: /(sso/.*)
        pathType: ImplementationSpecific
      identity:
        path: /(identity/.*)
        pathType: ImplementationSpecific
      admin:
        path: /(admin/?.*)
        pathType: ImplementationSpecific
```

--------------------------------

### Bitwarden CLI: List Sends

Source: https://bitwarden.com/help/cli/send-cli

The `list` command retrieves all Sends owned by the user and outputs them as JSON. If you create a Send in another Bitwarden app while this session is still active, use the `bw sync` command to pull recent sends.

```Bash
bw send list [options]
```

--------------------------------

### Bitwarden Event IDs for Critical Individual Account Actions

Source: https://bitwarden.com/help/cli/monitoring-event-logs

Details event IDs for monitoring high-impact actions performed by individual users, such as changing account passwords, managing two-step login, and exporting personal vault items.

```APIDOC
Individual Account Activity Event IDs:
  1000: Logged in
  1001: Changed account password
  1002: Enabled/updated two-step login
  1003: Disabled two-step login
  1007: User exported their individual vault items
  1603: Organization vault access by a managing provider
```

--------------------------------

### Two-step Login Methods Enum

Source: https://bitwarden.com/help/cli/cli

This enumeration defines the integer values corresponding to different two-step login methods supported by the Bitwarden CLI. These values are used when specifying a method during the login process.

```APIDOC
Two-step Login Methods:
  Authenticator: 0
  Email: 1
  YubiKey: 3
Note: FIDO2 and Duo are not supported by the CLI.
```

--------------------------------

### Manually update a Let's Encrypt certificate

Source: https://bitwarden.com/help/cli/certificates

If you change the domain name of your Bitwarden server, you will need to manually update your generated certificate. Run the following commands to create a backup, update your certificate, and rebuild Bitwarden.

```Bash
./bitwarden.sh stop
mv ./bwdata/letsencrypt ./bwdata/letsencrypt_backup
mkdir ./bwdata/letsencrypt
chown -R bitwarden:bitwarden ./bwdata/letsencrypt
chmod -R 740 ./bwdata/letsencrypt
docker pull certbot/certbot
docker run -i --rm --name certbot -p 443:443 -p 80:80 -v <Full Path from / >/bwdata/letsencrypt:/etc/letsencrypt/ certbot/certbot certonly --email <user@email.com> --logs-dir /etc/letsencrypt/logs
openssl dhparam -out ./bwdata/letsencrypt/live/<your.domain.com>/dhparam.pem 2048
./bitwarden.sh rebuild
./bitwarden.sh start
```

```PowerShell
.\bitwarden.ps1 -stop
mv .\bwdata\letsencrypt .\bwdata\letsencrypt_backup
mkdir .\bwdata\letsencrypt
docker pull certbot/certbot
docker run -i --rm --name certbot -p 443:443 -p 80:80 -v <Full Path from \\ >\\bwdata\\letsencrypt\\:/etc/letsencrypt/ certbot/certbot certonly --email <user@email.com> --logs-dir /etc/letsencrypt/logs
Select 1, then follow instructions
<path/to/openssl.exe> dhparam -out .\bwdata\letsencrypt\live\<your.domain.com>\dhparam.pem 2048
.\bitwarden.ps1 -rebuild
.\bitwarden.ps1 -start
```

--------------------------------

### Google Workspace SAML Identity Provider Configuration Fields

Source: https://bitwarden.com/help/cli/saml-google

Details the required fields and their descriptions for configuring Google Workspace as a SAML identity provider in Bitwarden. This configuration is crucial for enabling Single Sign-On (SSO) for users.

```APIDOC
Identity Provider Configuration Fields:
  Entity ID: Set this field to Workspace's Entity ID, retrieved from the Google Identity Provider details section or using the Download Metadata button. This field is case sensitive.
  Binding Type: Set to HTTP POST or Redirect.
  Single Sign On Service URL: Set this field to Workspace's SSO URL, retrieved from the Google Identity Provider details section or using the Download Metadata button.
  Single Log Out URL: Login with SSO currently does not support SLO. This option is planned for future development, however you may pre-configure it if you wish.
  X509 Public Certificate: Paste the retrieved certificate, removing -----BEGIN CERTIFICATE----- and -----END CERTIFICATE-----. The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters will cause certification validation to fail.
  Outbound Signing Algorithm: By default, Google Workspace will sign with RSA SHA-256. Select sha-256 from the dropdown.
  Disable Outbound Logout Requests: Login with SSO currently does not support SLO. This option is planned for future development.
  Want Authentication Requests Signed: Whether Google Workspace expects SAML requests to be signed.
```

--------------------------------

### Create Initial Microsoft Edge .plist File on macOS

Source: https://bitwarden.com/help/cli/deactivate-browser-password-managers

This shell command uses `defaults write` to create an initial `com.microsoft.Edge.plist` file on the user's desktop, setting a basic preference. This is a preliminary step before adding more specific configurations.

```Shell
/usr/bin/defaults write ~/Desktop/com.microsoft.Edge.plist RestoreOnStartup -int 1
```

--------------------------------

### Configure Git for SSH Signing Format

Source: https://bitwarden.com/help/cli/ssh-agent

Global Git configuration command to set the GPG format to SSH, enabling Git to use SSH keys for commit signing.

```Git
git config --global gpg.format ssh
```

--------------------------------

### Bitwarden Application Endpoints

Source: https://bitwarden.com/help/cli/bitwarden-addresses

Details the various API and service endpoints used by Bitwarden applications for communication and functionality.

```APIDOC
api.bitwarden.com / api.bitwarden.eu
events.bitwarden.com / events.bitwarden.eu
func.bitwarden.com
identity.bitwarden.com / identity.bitwarden.eu
scim.bitwarden.com / scim.bitwarden.eu
sso.bitwarden.com / sso.bitwarden.eu
push.bitwarden.com / push.bitwarden.eu
icons.bitwarden.net
```

--------------------------------

### Bitwarden Account Recovery Process Flow

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Details the step-by-step process for an organization member's account recovery, involving decryption and re-encryption of keys using RSA and symmetric keys.

```APIDOC
Process: AccountRecovery
  Description: Recovers a user's account encryption key (User Symmetric Key) using organization's RSA Private Key.
  Steps:
    1. DecryptOrganizationRSAPrivateKey(OrganizationSymmetricKey) -> DecryptedRSAPrivateKey
    2. DecryptAccountRecoveryKey(AccountRecoveryKey, DecryptedRSAPrivateKey) -> UserSymmetricKey
    3. EncryptUserSymmetricKey(UserSymmetricKey, NewMasterKey) -> MasterKeyEncryptedUserSymmetricKey
    4. SeedNewMasterPasswordHash(NewMasterPassword) -> NewMasterPasswordHash
    5. ReplaceServerValues(MasterKeyEncryptedUserSymmetricKey, NewMasterPasswordHash)
    6. EncryptUserSymmetricKey(UserSymmetricKey, OrganizationRSAPublicKey) -> NewAccountRecoveryKey
    7. ReplacePreviousAccountRecoveryKey(NewAccountRecoveryKey)
```

--------------------------------

### Configure Directory Connector for Large Syncs

Source: https://bitwarden.com/help/cli/user-group-filters

Enable the large import option in the Directory Connector configuration file (`data.json`) to signal that more than 2000 users or groups are expected to sync. This prevents the default sync limit of 2000 users/groups.

```JSON
"syncConfig": {
  ...,
  ...,
  ...,
  "largeImport": true
  },"
```

--------------------------------

### Unlock Bitwarden CLI vault using password file

Source: https://bitwarden.com/help/cli/cli

Illustrates how to use the `--passwordfile` option with `bw unlock` to retrieve your master password from a local file (e.g., `~/Users/Me/Documents/mp.txt`). The file must contain your master password as its first line. A warning is included to protect the password file by restricting access to only the necessary user with read permissions.

```Bash
bw unlock --passwordfile ~/Users/Me/Documents/mp.txt
```

--------------------------------

### Bitwarden and Splunk Default Fields for Event Queries

Source: https://bitwarden.com/help/cli/splunk-siem

This section provides a comprehensive list of fields available for querying Bitwarden event logs in Splunk, including specific Bitwarden-related fields and standard Splunk default fields. Attributes not relevant to an event type will be reported as null.

```APIDOC
Bitwarden Fields:
  actingUserEmail: The email of the user performing the action.
  actingUserId: Unique id of user performing action.
  actingUserName: Name of the user performing an action.
  collectionId: Organization collection id.
  device: Numerical number to identify the device that the action was performed on.
  deviceName: Numerical id of device. Exact mapping can be located here.
  groupId: Organization group id.
  groupName: Organization group name.
  hash: Splunk computed data hash. Learn more about Splunk's data integrity here.
  ipAddress: The ip address that performed the event.
  itemId: Vault item (cipher, secure note, etc..) of the organization vault.
  memberEmail: Email of the organization member that the action was directed towards.
  memberId: Unique id of the organization member that the action was directed towards.
  memberName: Name of organization member that action was directed towards.
  policyId: Organization policy update. See organization events here.
  type: The event type code that represents the organization event that occurred. See a complete list of event codes with descriptions here.
  typeName: Type numerical id. See mappings here.

Splunk Default Fields:
  source
  sourcetype
  date:
    date_hour
    date_mday
    date_minute
    date_month
    date_second
    date_wday
    date_year
    date_zone
  index
  linecount
  punct
  splunk_server
  timestamp
```

--------------------------------

### Specify Syslog Destination

Source: https://bitwarden.com/help/cli/environment-variables

Specify a syslog server or endpoint to send container log output to. This allows integration with external logging systems.

```APIDOC
globalSettings__syslog__destination=udp://example.com:514
```

--------------------------------

### Auth0 Application Settings Configuration for Bitwarden SAML SSO

Source: https://bitwarden.com/help/cli/saml-auth0

This section details the required settings within the Auth0 Portal for configuring a Regular Web Application to work with Bitwarden's SAML 2.0 Single Sign-On. It outlines how to map Bitwarden's SP Entity ID and ACS URL to Auth0's Application Login URI and Allowed Callback URLs, respectively, along with other essential configurations.

```APIDOC
Auth0 Application Settings:
  Name: Give the application a Bitwarden-specific name.
  Domain: Take note of this value. You will need it during a later step.
  Application Type: Select Regular Web Application.
  Token Endpoint Authentication Method: Select Client Secret (Post), which will map to a Binding Type attribute you will configure later.
  Application Login URI: Set this field to the pre-generated SP Entity ID. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
  Allowed Callback URLS: Set this field to the pre-generated Assertion Consumer Service (ACS) URL. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Advanced Settings:
  Grant Types: Ensure that the following Grant Types are selected (they may be pre-selected).
```

--------------------------------

### Disable Bitwarden Desktop App Automatic Updates

Source: https://bitwarden.com/help/cli/product-faqs

To prevent the Bitwarden desktop application from attempting automatic updates, set this environment variable. This is useful for managing updates manually or in controlled environments.

```Shell
ELECTRON_NO_UPDATER=1
```

--------------------------------

### Granting Execute Permissions to Bitwarden CLI Executable

Source: https://bitwarden.com/help/cli/cli

This command is used in Linux and UNIX systems to grant execute permissions to the downloaded Bitwarden CLI native executable. It resolves 'Permission denied' errors, allowing the user to run the CLI commands.

```Bash
chmod +x </path/to/executable>
```

--------------------------------

### Bitwarden Organization Creation and Symmetric Key Protection

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Explains the cryptographic process initiated when creating a Bitwarden organization. It details the generation of the Organization Symmetric Key using CSPRNG, its encryption with the creator's RSA Public Key (RSA-OAEP), and how it's protected and later decrypted by members to access organization-owned vault data.

```APIDOC
When you create an organization:
A Cryptographically Secure Pseudorandom Number Generator (CSPRNG) is used to generate the Organization Symmetric Key. This key is what's used to encrypt vault data owned by the organization, therefore sharing data with organization members requires securely providing access to the Organization Symmetric Key. The unprotected Organization Symmetric Key is never stored on Bitwarden servers.

As soon as the Organization Symmetric Key is created, RSA-OAEP is used to encrypt it with the organization creator's RSA Public Key.

The resultant value of this operation is referred to as the Protected Organization Symmetric Key and is sent to Bitwarden servers.

When the organization creator, or any organization member, logs in to their account, the client application uses the decrypted RSA Private Key to decrypt the Protected Organization Symmetric Key, resulting in the Organization Symmetric Key. Using this, organization-owned vault data is decrypted locally.
```

--------------------------------

### Minimum Required Values for Bitwarden CSV Import

Source: https://bitwarden.com/help/cli/condition-bitwarden-import

This snippet specifies the absolute minimum set of fields required for a .csv file to be successfully imported into Bitwarden. It demonstrates the essential columns for both login and secure note entries. Adhering to these minimums ensures basic functionality even with incomplete data.

```CSV
folder,favorite,type,name,notes,fields,reprompt,login_uri,login_username,login_password,login_totp
,,login,Login Name,,,,,
,,note,Secure Note Name,,,,,,
```

--------------------------------

### Bitwarden OIDC Configuration Fields

Source: https://bitwarden.com/help/cli/configure-sso-oidc

Defines the required and optional fields for configuring OpenID Connect (OIDC) integration within Bitwarden, including callback URLs, authorization server details, client credentials, and behavior settings.

```APIDOC
OIDC Configuration Fields:
  Callback Path:
    Description: Automatically generated URL for authentication automatic redirect.
    Cloud-hosted: https://sso.bitwarden.com/oidc-signin or https://sso.bitwarden.eu/oidc-signin
    Self-hosted: https://your.domain.com/sso/oidc-signin (determined by configured server URL)
  Signed Out Callback Path:
    Description: Automatically generated URL for sign-out automatic redirect.
    Cloud-hosted: https://sso.bitwarden.com/oidc-signedout or https://sso.bitwarden.eu/oidc-signedout
    Self-hosted: https://your.domain.com/sso/oidc-signedout (determined by configured server URL)
  Authority:
    Required: Yes
    Description: The URL of your authorization server.
    Example: https://your.domain.okta.com/oauth2/default or https://login.microsoft.com/<TENANT_ID>/v2.0
  Client ID:
    Required: Yes
    Description: An identifier for the OIDC client, typically specific to an IdP app integration.
  Client Secret:
    Required: Yes
    Description: The client secret used in conjunction with the client ID to exchange for an access token.
  Metadata Address:
    Required: Yes (if Authority is not valid)
    Description: A Metadata URL where Bitwarden can access authorization server metadata as a JSON object.
    Example: https://your.domain.okta.com/oauth2/default/.well-known/oauth-authorization-server
  OIDC Redirect Behavior:
    Required: Yes
    Description: Method used by the IdP to respond to authentication requests from Bitwarden.
    Options: Form POST, Redirect GET
  Get claims from user info endpoint:
    Description: Enable this option if you receive URL too long errors (HTTP 414), truncated URLs, and/or failures during SSO.
  Additional/custom scopes:
    Description: Define custom scopes to be added to the request (comma-delimited).
  Additional/custom user id claim types:
    Description: Define custom claim type keys for user identification (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
  Additional/custom email claim types:
    Description: Define custom claim type keys for users' email addresses (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
  Additional/custom name claim types:
    Description: Define custom claim type keys for users' full names or display names (comma-delimited). When defined, custom claim types are searched for before falling back on standard types.
  Requested authentication context class reference values:
    Description: Define authentication context class reference identifiers (acr_values) (space-delimited). List acr_values in preference-order.
  Expected "acr" Claim Value in Response:
    Description: Define the acr claim value for Bitwarden to expect and validate in the response.
```

--------------------------------

### Configure Key Connector for Hashicorp Vault Certificate

Source: https://bitwarden.com/help/cli/deploy-key-connector

This configuration enables Key Connector to retrieve a base64-encoded PKCS12 certificate from Hashicorp Vault's KV2 Storage Engine. It specifies the Vault server URI, a token, the secret mount point, the secret path, the data key where the certificate is stored, and the certificate's file password.

```Bash
keyConnectorSettings__rsaKey__provider=certificate
keyConnectorSettings__certificate__provider=vault
keyConnectorSettings__certificate__vaultServerUri={Server_URI}
keyConnectorSettings__certificate__vaultToken={Token}
keyConnectorSettings__certificate__vaultSecretMountPoint={Secret_MountPoint}
keyConnectorSettings__certificate__vaultSecretPath={Secret_Path}
keyConnectorSettings__certificate__vaultSecretDataKey={Secret_DataKey}
keyConnectorSettings__certificate__vaultSecretFilePassword={Secret_FilePassword}
```

--------------------------------

### Configure Bitwarden Browser Extension Base URL on Windows

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This snippet details how to pre-configure the base environment URL for the Bitwarden browser extension on Windows using Group Policy Objects (GPO). It involves creating a new Registry Item with specific properties for Google Chrome or Microsoft Edge.

```Windows
Action: Update
Hive: HKEY_LOCAL_MACHINE
Key Path (Google Chrome): HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Google\Chrome\3rdparty\extensions\<extension_id>\policy\environment
Value name: base
Value type: REG_SZ
Value data: Your server's configured domain
```

```Windows
Key Path (Microsoft Edge): HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge\3rdparty\extensions\<extension_id>\policy\environment
```

--------------------------------

### Create Signed Git Commit

Source: https://bitwarden.com/help/cli/ssh-agent

Create a new Git commit with a message, which will be signed using your configured SSH key via Bitwarden's SSH agent.

```Plain
git commit -m "This commit is signed using SSH"
```

--------------------------------

### Bitwarden Web App SAML Service Provider Configuration

Source: https://bitwarden.com/help/cli/saml-aws

Outlines the configurable fields within the Bitwarden web application's SAML service provider settings, affecting how Bitwarden generates and signs SAML requests.

```APIDOC
Service Provider Configuration Fields:
  Name ID Format:
    Description: Set to Email Address.
  Outbound Signing Algorithm:
    Description: The algorithm Bitwarden will use to sign SAML requests.
  Signing Behavior:
    Description: Whether/when SAML requests will be signed.
  Minimum Incoming Signing Algorithm:
    Description: By default, IAM Identity Center will sign with SHA-256. Unless you have changed this, select `sha256` from the dropdown.
  Want Assertions Signed:
    Description: Whether Bitwarden expects SAML assertions to be signed.
  Validate Certificates:
    Description: Check this box when sing trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured within the Bitwarden Login with SSO docker image.
```

--------------------------------

### OneLogin SCIM User Attributes for Bitwarden

Source: https://bitwarden.com/help/cli/onelogin-scim-integration

This section details the standard SCIM v2 user attributes used by Bitwarden when provisioning from OneLogin's SCIM Provisioner with SAML (SCIM v2 Enterprise) application. It specifies which attributes are utilized and notes special handling for email addresses.

```APIDOC
SCIM v2 User Attributes:
- active (boolean): Indicates if the user account is active.
- emails (array of objects): User's email addresses.
  - value (string): The email address itself. Bitwarden uses the 'value' of the object where '"primary": true'.
- userName (string): User's unique identifier, can be used as an alternative to 'emails'.
- displayName (string): The user's full display name.
- externalId (string): An identifier for the user in an external system.
```

--------------------------------

### Configure Custom Server Ports and Rebuild Bitwarden

Source: https://bitwarden.com/help/cli/hosting-faqs

This snippet details how to change the default HTTP (80) and HTTPS (443) server ports for a self-hosted Bitwarden instance. It requires editing port values in `config.yml` and then running a shell command to rebuild the server assets for the changes to take effect.

```YAML
http_port=<your-custom-http-port>
https_port=<your-custom-https-port>
```

```Bash
./bitwarden.sh rebuild
```

--------------------------------

### Configure Bitwarden Browser Extension Base URL on macOS

Source: https://bitwarden.com/help/cli/configure-clients-selfhost

This snippet provides the XML content for a Property List (.plist) file to pre-configure the base environment URL for the Bitwarden browser extension on macOS. The file should be named `com.google.chrome.extensions.<extension_id>.plist` and converted to a `.mobileconfig` profile for distribution.

```XML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>environment</key>
        <dict>
            <key>base</key>
            <string>https://my.bitwarden.server.com</string>
        </dict>
    </dict>
</plist>
```

--------------------------------

### Configure OneLogin Role Exclusion for Directory Sync (Bash)

Source: https://bitwarden.com/help/cli/onelogin-directory

Use this command-line snippet to define which OneLogin roles should be excluded from the Bitwarden Directory Connector synchronization. Roles specified here will not be synchronized, allowing for granular control over user and group imports.

```Bash
exclude:Role A,Role B
```

--------------------------------

### Bitwarden GitHub Organization URL

Source: https://bitwarden.com/help/cli/bitwarden-addresses

Provides the main URL for the Bitwarden organization on GitHub, hosting various open-source projects.

```APIDOC
https://github.com/bitwarden
```

--------------------------------

### Set Git core.sshCommand in .gitconfig for Windows

Source: https://bitwarden.com/help/cli/ssh-agent

Alternatively, add the `core.sshCommand` variable directly to your `.gitconfig` file for Windows OpenSSH integration.

```Plain
[core]
  sshCommand = C:/Windows/System32/OpenSSH/ssh.exe
```

--------------------------------

### JSON Format for Individual Bitwarden Vault Import

Source: https://bitwarden.com/help/cli/condition-bitwarden-import

Create a UTF-8 encoded plaintext JSON file to import individual vault items into Bitwarden. This format includes folders and items with details like password history, login credentials, custom fields, and notes. When importing, select 'Bitwarden (json)' as the file format.

```JSON
{
  "folders": [
    {
      "id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "name": "Folder Name"
    },
    ...
  ],
  "items": [
    {
    "passwordHistory": [
        {
          "lastUsedDate": "YYYY-MM-00T00:00:00.000Z",
          "password": "passwordValue"
        }
    ],
    "revisionDate": "YYYY-MM-00T00:00:00.000Z",
    "creationDate": "YYYY-MM-00T00:00:00.000Z",
    "deletedDate": null,
    "id": "yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy",
    "organizationId": null,
    "folderId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "type": 1,
    "reprompt": 0,
    "name": "My Gmail Login",
    "notes": "This is my gmail login for import.",
    "favorite": false,
    "fields": [
        {
          "name": "custom-field-1",
          "value": "custom-field-value",
          "type": 0
        },
        ...
      ],
      "login": {
        "uris": [
          {
            "match": null,
            "uri": "https://mail.google.com"
          }
        ],
        "username": "myaccount@gmail.com",
        "password": "myaccountpassword",
        "totp": "otpauth://totp/my-secret-key"
      },
      "collectionIds": null
    },
    ...
  ]
}
```

--------------------------------

### Stop Bitwarden Docker Container (Direct Docker)

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command stops the running Bitwarden container by its name, preparing it for removal or update when managing with direct Docker commands.

```Bash
docker stop bitwarden
```

--------------------------------

### Email Template: Promoting Bitwarden Password Manager Benefits

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

This email encourages sharing the value and benefits of Bitwarden with end-users, focusing on easy access, secure sharing, and streamlined logins, along with links to helpful resources.

```Email
Subject: Promote the top benefits

Body:

Hi *[name]*,

Make sure the end-users understand the value and benefits a password manager will bring to their work.

To get your team excited about Bitwarden, here are three primary benefits to share with everyone:

1. Easily access all your passwords anytime, anywhere, on any device.
2. Securely share credentials with others.
3. Streamline logging into your accounts with auto-fill.

Here are a few resources on the benefits of a password manager that you can send to employees:

* Share this password strength testing tool - let the gamification begin!
* [Blog] How a password manager adds productivity at the office
* [Blog] A better password workflow with Bitwarden
* [Blog] How to better manage your financial information in Bitwarden
* [Blog] 7 steps to create a secure (and private) profile online
```

--------------------------------

### Map SP to IdP Attributes for Bitwarden SSO in JumpCloud

Source: https://bitwarden.com/help/cli/saml-jumpcloud

This section describes how to configure attribute mappings between the Service Provider (Bitwarden) and the Identity Provider (JumpCloud) to ensure proper user data synchronization during SSO.

```APIDOC
Attribute Mapping:
  Location: Single Sign-On Configuration -> Attributes section in JumpCloud.
  Purpose: Construct SP (Bitwarden) -> IdP (JumpCloud) attribute mappings.
  Note: If Bitwarden Application was selected in JumpCloud, these should be pre-constructed.
```

--------------------------------

### Bitwarden Service Provider Configuration for OneLogin SSO

Source: https://bitwarden.com/help/cli/saml-onelogin

Details the fields to configure within the Bitwarden web app's SAML service provider section, aligning with choices made in the OneLogin Portal, including Name ID Format, Signing Algorithm, and Certificate Validation.

```APIDOC
Field: Name ID Format
  Description: Set this field to whatever you selected for the OneLogin SAML nameID Format field during app configuration.
Field: Outbound Signing Algorithm
  Description: Algorithm used to sign SAML requests, by default `sha-256`.
Field: Signing Behavior
  Description: Whether/when SAML requests will be signed. By default, OneLogin will not require requests to be signed.
Field: Minimum Incoming Signing Algorithm
  Description: Set this field to whatever you selected for the SAML Signature Algorithm during app configuration.
Field: Want Assertions Signed
  Description: Check this box if you set the SAML signature element in OneLogin to Assertion or Both during app configuration.
Field: Validate Certificates
  Description: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured within the Bitwarden login with SSO docker image.
```

--------------------------------

### Bitwarden Event IDs for Critical Organization-Level Actions

Source: https://bitwarden.com/help/cli/monitoring-event-logs

Lists event IDs for tracking significant administrative actions within an organization, including user invitations, confirmations, edits, group modifications, device approvals, and changes to organization settings or policies.

```APIDOC
Organization Activity Event IDs:
  1500: Invited user `user-identifier`
  1501: Confirmed user `user-identifier`
  1502: Edited user `user-identifier`
  1504: Edited groups for user `user-identifier`
  1511: Revoked organization access for user `user-identifier`
  1512: Restored organization access for `user-identifier`
  1513: Approved device for `user-identifier`
  1600: Edited organization settings
  1609: Modified collection management setting
  1700: Modified policy `policy-identifier`
  2001: Removed domain `domain-name`
```

--------------------------------

### Email Template for Complimentary Bitwarden Families Plan

Source: https://bitwarden.com/help/cli/end-user-adoption-emails

Offers an email template to inform employees about the complimentary Bitwarden Families plan available through their Enterprise subscription, encouraging personal and family security.

```Email
Subject: Your Bitwarden account comes with a free Families plan

Body: Dear [company] employees,

We use Bitwarden for secure password management and sharing secure information across teams and the organization. Proper password management is an important part of our security strategy and we're happy that together we can practice secure password habits.

We can now share password management to you and your family. Through our Bitwarden Enterprise subscription, every employee connected to our Bitwarden instance can redeem a complimentary Bitwarden Families plan using a personal email address and invite five additional family members to join. Every user on the Families plan will have access to secure password sharing and premium features, such as advanced two-step login, emergency access, encrypted file attachments, and more.

We hope that every employee will take advantage of this opportunity to protect themselves and their families. Internet and password security is important both in the office and at home, and staying secure across our personal and work lives is a shared responsibility.

A walkthrough from Bitwarden is available here.

Thank you,

[IT admin name, title]
```

--------------------------------

### Bitwarden SCIM Group Attribute Mapping with JumpCloud

Source: https://bitwarden.com/help/cli/jumpcloud-scim-integration

This section outlines how Bitwarden maps standard SCIM v2 group properties to JumpCloud's default attributes. It clarifies how group memberships are transmitted as an array of user objects.

```APIDOC
Bitwarden Attribute | JumpCloud Default Property
--------------------|---------------------------
displayName         | displayName
members             | members (sent as array of user objects)
```

--------------------------------

### Keycloak Realm Settings - RS256 Certificate Extraction

Source: https://bitwarden.com/help/cli/saml-keycloak

Steps to locate and extract the RS256 certificate from Keycloak's Realm settings, which is necessary for configuring Bitwarden.

```APIDOC
Path: Realm settings -> Keys Tab
Certificate: RS256
Action: Select Certificate to view its value.
```

--------------------------------

### Bitwarden Access Token Response Format (APIDOC)

Source: https://bitwarden.com/help/cli/public-api

Illustrates the JSON response structure received after successfully obtaining a bearer access token. This response includes the access token itself, its expiration time in seconds, and the token type.

```APIDOC
{
  "access_token": "<TOKEN>",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

--------------------------------

### Authenticate Bitwarden CLI Requests with Access Token

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Authenticate individual Bitwarden CLI requests by providing an access token using the `-t` or `--access-token` option with any command. This allows for secure, per-command authentication.

```Bash
bws secret list --access-token 0.48c78342-1635-48a6-accd-afbe01336365.C0tMmQqHnAp1h0gL8bngprlPOYutt0:B3h5D+YgLvFiQhWkIq6Bow==
```

--------------------------------

### Bitwarden Never Match Detection for Autofill

Source: https://bitwarden.com/help/cli/uri-match-detection

Describes the 'Never' match detection option, which explicitly excludes a URI from autofill suggestions.

```APIDOC
Selecting Never will prompt Bitwarden to exclude the URI from match detection for autofill.
```

--------------------------------

### Create SecretProviderClass for Azure Key Vault CSI Driver

Source: https://bitwarden.com/help/cli/azure-aks-deployment

This YAML defines a SecretProviderClass object for the Azure Key Vault Secrets Store CSI Driver. It specifies how secrets from Azure Key Vault should be accessed and projected into Kubernetes pods. Placeholders like '<REPLACE>' for 'userAssignedIdentityID', 'keyvaultName', 'tenantId', and secret names must be updated with actual values. It also defines which secrets to retrieve and how they map to environment variables or files within the pod.

```YAML
cat <<EOF | kubectl apply -n bitwarden -f -
apiVersion: secrets-store.csi.x-k8s.io/v1
kind: SecretProviderClass
metadata:
  name: bitwarden-azure-keyvault-csi
  labels:
    app.kubernetes.io/component: secrets
  annotations:
spec:
  provider: azure
  parameters:
    useVMManagedIdentity: "true" # Set to false for workload identity
    userAssignedIdentityID: "<REPLACE>" # Set the clientID of the user-assigned managed identity to use
    # clientID: "<REPLACE>" # Setting this to use workload identity
    keyvaultName: "<REPLACE>"
    cloudName: "AzurePublicCloud"
    objects: |
      array:
        - |
          objectName: installationid
          objectAlias: installationid
          objectType: secret
          objectVersion: ""
        - |
          objectName: installationkey
          objectAlias: installationkey
          objectType: secret
          objectVersion: ""
        - |
          objectName: smtpusername
          objectAlias: smtpusername
          objectType: secret
          objectVersion: ""
        - |
          objectName: smtppassword
          objectAlias: smtppassword
          objectType: secret
          objectVersion: ""
        - |
          objectName: yubicoclientid
          objectAlias: yubicoclientid
          objectType: secret
          objectVersion: ""
        - |
          objectName: yubicokey
          objectAlias: yubicokey
          objectType: secret
          objectVersion: ""
        - |
          objectName: hibpapikey
          objectAlias: hibpapikey
          objectType: secret
          objectVersion: ""
        - |
          objectName: sapassword #-OR- dbconnectionstring if external SQL
          objectAlias: sapassword #-OR- dbconnectionstring if external SQL
          objectType: secret
          objectVersion: ""
    tenantId: "<REPLACE>"
  secretObjects:
  - secretName: "bitwarden-secret"
    type: Opaque
    data:
    - objectName: installationid
      key: globalSettings__installation__id
    - objectName: installationkey
      key: globalSettings__installation__key
    - objectName: smtpusername
      key: globalSettings__mail__smtp__username
    - objectName: smtppassword
      key: globalSettings__mail__smtp__password
    - objectName: yubicoclientid
      key: globalSettings__yubico__clientId
    - objectName: yubicokey
      key: globalSettings__yubico__key
    - objectName: hibpapikey
      key: globalSettings__hibpApiKey
    - objectName: sapassword #-OR- dbconnectionstring if external SQL
      key: SA_PASSWORD #-OR- globalSettings__sqlServer__connectionString if external SQL
EOF
```

--------------------------------

### Use Bitwarden CLI session key via environment variable

Source: https://bitwarden.com/help/cli/cli

Details how to use the session key generated after unlocking your vault. The CLI returns an `export BW_SESSION` command (for Bash) which, when copied and pasted, sets the required environment variable. With `BW_SESSION` set, subsequent `bw` commands can run cleanly without explicitly passing the session key.

```Bash
export BW_SESSION="5PBYGU+5yt3RHcCjoeJKx/wByU34vokGRZjXpSH7Ylo8w=="

bw list items
```

--------------------------------

### Limit Bitwarden Container Memory Usage (Docker Compose)

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This snippet demonstrates how to configure the `mem_limit` key within a `docker-compose.yml` file to restrict the maximum memory available to the Bitwarden container. This is useful for memory-constrained environments, with a minimum requirement of 200m.

```YAML
services:
  bitwarden:
    env_file:
      - settings.env
    image: ghcr.io/bitwarden/self-host:beta
    restart: always
    mem_limit: 200m
```

--------------------------------

### Use Wildcards and Advanced Parameters in Bitwarden Search

Source: https://bitwarden.com/help/cli/searching-vault

Illustrates the application of the asterisk (*) as a wildcard character for flexible search queries. This allows for partial matches, finding items based on presence or absence of a field, or matching patterns like email domains.

```Bitwarden
>organizationid:*
```

```Bitwarden
>-organizationid:*
```

```Bitwarden
>login.username:*@gmail.com
```

```Bitwarden
>wild*
```

--------------------------------

### OneLogin App Configuration Settings for Bitwarden SSO

Source: https://bitwarden.com/help/cli/saml-onelogin

Details the required application settings within OneLogin for integrating with Bitwarden SSO, including Audience, Recipient, ACS URL, SAML initiator, NameID Format, and Signature Element.

```APIDOC
Application Setting: Audience (EntityID)
  Description: Set this field to the pre-generated SP Entity ID. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Application Setting: Recipient
  Description: Set this field to the same pre-generated SP Entity ID used for the Audience (Entity ID) setting.
Application Setting: ACS (Consumer) URL Validator
  Description: Despite being marked Required by OneLogin, you don't actually need to enter information into this field to integrate with Bitwarden. Skip to the next field, ACS (Consumer) URL.
Application Setting: ACS (Consumer) URL
  Description: Set this field to the pre-generated Assertion Consumer Service (ACS) URL. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Application Setting: SAML initiator
  Description: Select Service Provider. Login with SSO does not currently support IdP-initiated SAML assertions.
Application Setting: SAML nameID Format
  Description: Set this field to the [SAML NameID Format](https://docs.oracle.com/cd/E19316-01/820-3886/ggwbz/index.html) you want to use for SAML assertions.
Application Setting: SAML signature element
  Description: By default, OneLogin will sign the SAML Response. You can set this to Assertion or Both
```

--------------------------------

### Condition UserAccount CSV for Bitwarden Import

Source: https://bitwarden.com/help/cli/import-data-from-myki

Shows the required column header changes and potential reordering for UserAccount CSV files exported from Myki mobile apps to be compatible with Bitwarden's import format. The 'Exported' format is from Myki, and the 'Expected' format is for Bitwarden.

```CSV
Nickname,Url,Username,Password,Additional Info,Two Factor Secret,Status
```

```CSV
nickname,url,username,password,additionalInfo,twofaSecret,status,tags
```

--------------------------------

### Migrate Bitwarden Individual Member Permissions

Source: https://bitwarden.com/help/cli/migration-script

This command executes the `migratebwusers` function, which migrates individual member permissions not tied to groups from the source to the destination organization. Similar to `migratebw`, users must be in at least an invited state in the destination organization.

```Bash
python3 bwAdminTools.py -c migratebwusers
```

--------------------------------

### Configure Identity Provider Settings for Bitwarden SSO

Source: https://bitwarden.com/help/cli/saml-aws

Defines the required fields and their descriptions for configuring an Identity Provider within Bitwarden's SSO settings, specifically for integration with AWS IAM Identity Center. This includes details on Entity ID, Binding Type, SSO/SLO URLs, X509 Certificate, and Outbound Signing Algorithm.

```APIDOC
Identity Provider Configuration Fields:
  Entity ID:
    Description: Enter the IAM Identity Center issuer URL, retrieved from the IAM Identity Center metadata section for your application in the AWS Console. This field is case sensitive.
  Binding Type:
    Description: Set to HTTP POST or Redirect.
  Single Sign On Service URL:
    Description: Enter the IAM Identity Center sign-in URL, retrieved from the IAM Identity Center metadata section for your application in the AWS Console.
  Single Log Out Service URL:
    Description: Login with SSO currently does not support SLO. This option is planned for future development, however you may pre-configure it with the IAM Identity Center sign-out URL retrieved from the IAM Identity Center metadata section for your application in the AWS Console.
  X509 Public Certificate:
    Description: Paste the downloaded certificate, removing: -----BEGIN CERTIFICATE----- and -----END CERTIFICATE-----. The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters will cause certificate validation to fail.
  Outbound Signing Algorithm:
    Description: By default, IAM Identity Center will sign with sha256. Unless you have changed this, select sha256 from the dropdown.
  Disable Outbound Logout Requests:
    Description: Login with SSO currently does not support SLO. This option is planned for future development.
  Want Authentication Requests Signed:
    Description: Whether IAM Identity Center expects SAML requests to be signed.
```

--------------------------------

### Bitwarden SAML Service Provider Configuration Fields

Source: https://bitwarden.com/help/cli/configure-sso-saml

This section describes the configuration fields on the Bitwarden (Service Provider) side for SAML Single Sign-On. These settings define how Bitwarden interacts with the Identity Provider, including its entity ID, metadata URL, assertion consumer service URL, and preferences for name ID format, signing algorithms, and assertion validation.

```APIDOC
SP Entity ID: (Automatically generated) The Bitwarden endpoint for authentication requests. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
SAML 2.0 Metadata URL: (Automatically generated) Metadata URL for the Bitwarden endpoint. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Assertion Consumer Service (ACS) URL: (Automatically generated) Location where the SAML assertion is sent from the IdP. This automatically-generated value can be copied from the organization's Settings → Single sign-on screen and will vary based on your setup.
Name ID Format: Format Bitwarden will request of the SAML assertion. Must be cast as a string. Options include: -Unspecified (default) -Email address -X.509 Subject name -Windows Domain Qualified Name -Kerberos Principal Name -Entity identifier -Persistent -Transient
Outbound Signing Algorithm: The algorithm Bitwarden will use to sign SAML requests. Options include: - http://www.w3.org/2001/04/xmldsig-more#rsa-sha256 (default) - http://www.w3.org/2000/09/xmldsig#rsa-sha384 - http://www.w3.org/2000/09/xmldsig#rsa-sha512
Signing Behavior: Whether/when SAML requests will be signed. Options include: -If IdP wants authn requests signed (default) -Always -Never
Minimum Incoming Signing Algorithm: Minimum strength of the algorithm that Bitwarden will accept in SAML responses.
Expect signed assertations: Check this checkbox if Bitwarden should expect responses from the IdP to be signed.
Validate certificates: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured within the Bitwarden login with SSO docker image.
```

--------------------------------

### Login URI Match Types Enum

Source: https://bitwarden.com/help/cli/cli

This enumeration defines the integer values for URI match detection behaviors used with login items in the Bitwarden CLI. These values determine how a login item's URI is matched against a website's URL.

```APIDOC
Login URI Match Types:
  Domain: 0
  Host: 1
  Starts With: 2
  Exact: 3
  Regular Expression: 4
  Never: 5
```

--------------------------------

### Approving Untrusted Device: Approval from Another Device

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Describes the process where an untrusted device is approved by another trusted device, leading to the client obtaining and decrypting the account encryption key and optionally establishing trust for future use.

```APIDOC
1. The process documented in /help/log-in-with-device/#how-it-works is triggered, resulting in the client having obtained and decrypted the account encryption key.
2. The user can now decrypt their vault data with the decrypted account encryption key. If they have chosen to trust the device, trust is established with the client as described in the Onboarding tab.
```

--------------------------------

### Google Workspace API Scopes for Directory Read-Only Access

Source: https://bitwarden.com/help/cli/gsuite-directory

This string contains the comma-separated Google Workspace API scopes required for read-only access to user, group, and group member directories. These scopes are used during OAuth consent screen configuration and domain-wide delegation to grant the service account necessary permissions for the Bitwarden Directory Connector.

```Plain
https://www.googleapis.com/auth/admin.directory.user.readonly,https://www.googleapis.com/auth/admin.directory.group.readonly,https://www.googleapis.com/auth/admin.directory.group.member.readonly
```

--------------------------------

### Vault Item Types Enum

Source: https://bitwarden.com/help/cli/cli

This enumeration lists the integer values for various vault item types that can be created or managed using the Bitwarden CLI's `create` command. Each value corresponds to a specific type of vault entry.

```APIDOC
Vault Item Types:
  Login: 1
  Secure Note: 2
  Card: 3
  Identity: 4
```

--------------------------------

### Configure Log Directory

Source: https://bitwarden.com/help/cli/environment-variables

Specifies the directory to save container log file output to. By default, logs are saved to `bwdata/logs`.

```APIDOC
globalSettings__logDirectory=bwdata/logs
```

--------------------------------

### Bitwarden SAML Identity Provider Configuration Fields

Source: https://bitwarden.com/help/cli/configure-sso-saml

This section details the configuration fields for the Identity Provider (IdP) side when setting up SAML Single Sign-On with Bitwarden. It covers essential parameters such as the IdP's entity ID, binding type, SSO service URL, X.509 public certificate, and outbound signing algorithm, along with notes on current limitations like Single Log Out (SLO) support.

```APIDOC
Entity ID: (Required) Address or URL of your identity server or the IdP Entity ID. This field is case sensitive and must match the IdP value exactly.
Binding Type: Method used by the IdP to respond to Bitwarden SAML requests. Options include: -Redirect (recommended) -HTTP POST
Single Sign On Service URL: (Required if Entity ID is not a URL) SSO URL issued by your IdP.
Single log out service URL: Login with SSO currently does not support SLO. This option is planned for future use, however we strongly recommend pre-configuring this field.
X509 Public Certificate: (Required) The X.509 Base-64 encoded certificate body. Do not include the -----BEGIN CERTIFICATE----- and -----END CERTIFICATE----- lines or portions of the CER/PEM formatted certificate. The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters inside this field will cause certificate validation failure. Copy only the certificate data into this field.
Outbound Signing Algorithm: The algorithm your IdP will use to sign SAML responses/assertions. Options include: - http://www.w3.org/2001/04/xmldsig-more#rsa-sha256 (default) - http://www.w3.org/2000/09/xmldsig#rsa-sha384 - http://www.w3.org/2000/09/xmldsig#rsa-sha512
Allow outbound logout requests: Login with SSO currently does not support SLO. This option is planned for future use, however we strongly recommend pre-configuring this field.
Sign authentication requests: Check this checkbox if your IdP should expect SAML requests from Bitwarden to be signed.
```

--------------------------------

### Remove Bitwarden Docker Container (Direct Docker)

Source: https://bitwarden.com/help/cli/install-and-deploy-unified-beta

This command removes the stopped Bitwarden container, which is often a prerequisite before pulling a new image or recreating the container.

```Bash
docker rm bitwarden
```

--------------------------------

### Google API Scopes for Directory Read Access

Source: https://bitwarden.com/help/cli/workspace-directory

These Google API scopes grant read-only access to user, group, and group member directories. They are essential for the Bitwarden Directory Connector to synchronize directory information and are required both when obtaining service account credentials and when configuring domain-wide delegation.

```Plain
https://www.googleapis.com/auth/admin.directory.user.readonly,https://www.googleapis.com/auth/admin.directory.group.readonly,https://www.googleapis.com/auth/admin.directory.group.member.readonly
```

--------------------------------

### Configure Browser Extension Keyboard Shortcuts

Source: https://bitwarden.com/help/cli/auto-fill-browser

Instructions for accessing the keyboard shortcut configuration menu in various browsers for the Bitwarden extension. Note that Safari and legacy Edge do not support this feature. Chromium-based browsers can substitute 'chrome' with their browser name.

```Chrome
chrome://extensions/shortcuts
```

```Chromium-based
brave://extensions/shortcuts
```

```Firefox
about:addons
```

--------------------------------

### OneLogin Identity Provider Configuration Fields

Source: https://bitwarden.com/help/cli/saml-onelogin

Details the required fields and their descriptions for configuring an identity provider (OneLogin) for Bitwarden Single Sign-On (SSO). It outlines each parameter, its purpose, and any specific requirements or limitations.

```APIDOC
Identity Provider Configuration Fields:
  - Entity ID:
    Description: Enter your OneLogin Issuer URL, which can be retrieved from the OneLogin app SSO screen. This field is case sensitive.
  - Binding Type:
    Description: Set to HTTP Post (as indicated in the SAML 2.0 Endpoint (HTTP)).
  - Single Sign On Service URL:
    Description: Enter your OneLogin SAML 2.0 Endpoint (HTTP), which can be retrieved from the OneLogin app SSO screen.
  - Single Log Out Service URL:
    Description: Login with SSO currently does not support SLO. This option is planned for future development, however you may pre-configure it if you wish.
  - X509 Public Certificate:
    Description: Paste the retrieved X.509 Certificate, removing -----BEGIN CERTIFICATE----- and -----END CERTIFICATE-----. The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters will cause certification validation to fail.
  - Outbound Signing Algorithm:
    Description: Select the SAML Signature Algorithm selected in the OneLogin SSO configuration section.
  - Disable Outbound Logout Requests:
    Description: Login with SSO currently does not support SLO. This option is planned for future development.
  - Want Authentication Requests Signed:
    Description: Whether OneLogin expects SAML requests to be signed.
```

--------------------------------

### Generate Strong Passwords and Passphrases

Source: https://bitwarden.com/help/cli/cli

The `bw generate` command creates strong passwords or passphrases with customizable options. You can specify character types (uppercase, lowercase, numbers, special characters), password length, number of words for passphrases, and separators.

```Bash
bw generate [--lowercase --uppercase --number --special --length <length> --passphrase --separator <separator> --words <words>]
```

```Bash
bw generate -uln --length 14
```

```Bash
bw generate --passphrase --words <words> --separator <separator>
```

```Bash
bw generate --passphrase --words 3 --separator -
```

--------------------------------

### Enable Overwriting Existing Users and Groups in Directory Sync

Source: https://bitwarden.com/help/cli/user-group-filters

Activate the overwrite existing option in the Directory Connector configuration file (`data.json`). This setting, intended for very specific use-cases or debugging, removes and re-adds all organization users (except one owner) and groups, replacing them with the fetched list from the source directory.

```JSON
"syncConfig": {
  ...,
  ...,
  ...,
  "overwriteExisting": true
  },"
```

--------------------------------

### Bitwarden OIDC User Attributes and Claims Mapping

Source: https://bitwarden.com/help/cli/configure-sso-oidc

Describes the order of preference for OIDC attributes and claims used by Bitwarden for user provisioning, including unique ID, email, and name fields, along with their fallbacks.

```APIDOC
OIDC Attributes & Claims Mapping:
  Note: An email address is required for account provisioning. A unique user identifier is highly recommended.
  Attributes/claims are listed in order of preference for matching, including fallbacks where applicable:
  Unique ID:
    Claim/Attribute: Configured Custom User ID Claims, NameID (when not transient), urn:oid:0.9.2342.19200300.100.1.1, Sub, UID, UPN, EPPN
    Fallback: None
  Email:
    Claim/Attribute: Configured Custom Email Claims, Email, http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress, urn:oid:0.9.2342.19200300.100.1.3, Mail, EmailAddress
    Fallback: Preferred_Username, Urn:oid:0.9.2342.19200300.100.1.1, UID
  Name:
    Claim/Attribute: Configured Custom Name Claims, Name, http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name, urn:oid:2.16.840.1.113730.3.1.241, urn:oid:2.5.4.3, DisplayName, CN
    Fallback: First Name + " " + Last Name
  First Name:
    Claim/Attribute: urn:oid:2.5.4.42, GivenName, FirstName, FN, FName, Nickname
    Fallback: None
  Last Name:
    Claim/Attribute: urn:oid:2.5.4.4, SN, Surname, LastName
    Fallback: None
```

--------------------------------

### Perform Online Bitwarden Database Restore

Source: https://bitwarden.com/help/cli/backup-on-premise

This SQL command executes an online restore of the `vault` database from a specified full backup file. The database remains accessible during the restore operation, minimizing downtime. Update the backup file name to match your specific backup.

```SQL
RESTORE DATABASE vault FROM DISK = '/etc/bitwarden/mssql/backups/vault_FULL_20200302_235901.BAK' WITH REPLACE
GO
```

--------------------------------

### Change Language in Bitwarden Web App

Source: https://bitwarden.com/help/cli/localization

Follow these steps to manually adjust the language settings within the Bitwarden web application.

```UI
1. Select Settings → Preferences from the navigation:
2. Select a language from the Language dropdown.
```

--------------------------------

### Sync Bitwarden Directory Connector Groups by Email Address

Source: https://bitwarden.com/help/cli/gsuite-directory

This snippet shows how to filter and sync groups based on their email addresses, supporting both exact matches and wildcard patterns. This provides an alternative method for group identification and synchronization.

```Bash
exclude:Group B|email:admin*
```

--------------------------------

### Open SSH Connection with Agent Forwarding

Source: https://bitwarden.com/help/cli/ssh-agent

Establish an SSH connection to a remote server with agent forwarding enabled, allowing the remote server to use your local SSH keys for further authentication.

```Plain
ssh -A <HostnameA>
```

--------------------------------

### Organization User Statuses Enum

Source: https://bitwarden.com/help/cli/cli

This enumeration provides the integer values indicating a user's status within a Bitwarden organization. These values reflect the current state of a user's invitation or membership.

```APIDOC
Organization User Statuses:
  Invited: 0
  Accepted: 1
  Confirmed: 2
  Revoked: -1
```

--------------------------------

### Access a Bitwarden Send Object via CLI

Source: https://bitwarden.com/help/cli/cli

The `receive` command is used to access and retrieve the contents of a Bitwarden Send object. To successfully receive a Send, the command requires the password for access and the full URL of the Send object.

```Bash
bw receive --password passwordforaccess https://vault.bitwarden.com/#/send/yawoill8rk6VM6zCATXv2A/9WN8wD-hzsDJjfnXLeNc2Q
```

--------------------------------

### Restore a Deleted Bitwarden Object using CLI

Source: https://bitwarden.com/help/cli/cli

The `restore` command allows users to recover a previously deleted object from their Bitwarden trash. This command strictly requires an exact ID of the object to be restored as its argument.

```Bash
bw restore (item) <id> [options]
```

```Bash
bw restore item 7063feab-4b10-472e-b64c-785e2b870b92
```

--------------------------------

### Bitwarden Account Encryption Key Rotation Process

Source: https://bitwarden.com/help/cli/bitwarden-security-white-paper

Describes the four-step cryptographic process for rotating a user's account encryption key. This includes the exchange and encryption of public and user keys between server and client, and the subsequent clearing of old trusted device keys to maintain security.

```APIDOC
When a user rotates their account encryption key, during the normal rotation process:
1. The User-Key Encrypted Public Key is sent from the server to the client, and subsequently decrypted with the old account encryption key (a.k.a. User Key), resulting in the Device Public Key.
2. The user's new account encryption key is encrypted with the unencrypted Device Public Key and the resultant value is sent to the server as the new Public Key-Encrypted User Key.
3. The Device Public Key is encrypted with the user's new account encryption key and the resultant value is sent to the server as the new User Key-Encrypted Public Key.
4. Trusted device encryption keys for all other devices that are persisted to server storage are cleared for the user. This leaves only the three required keys (Public Key-Encrypted User Key, User Key-Encrypted Public Key, and Device Key-Encrypted Private Key which was not changed by this process) for that single device persisted to the server.
```

--------------------------------

### Configure Key Connector for Azure Blob Storage Certificate

Source: https://bitwarden.com/help/cli/deploy-key-connector

This configuration allows Key Connector to retrieve a certificate from Azure Blob Storage. It requires a connection string (generated from a Shared Access Signature with appropriate permissions), the container name, the file name, and the certificate's password.

```Bash
keyConnectorSettings__rsaKey__provider=certificate
keyConnectorSettings__certificate__provider=azurestorage
keyConnectorSettings__certificate__azureStorageConnectionString={Connection_String}
keyConnectorSettings__certificate__azureStorageContainer={Container_Name}
keyConnectorSettings__certificate__azureStorageFileName={File_Name}
keyConnectorSettings__certificate__azureStorageFilePassword={File_Password}
```

--------------------------------

### Bitwarden Enterprise Features: Administrative Features and Capabilities

Source: https://bitwarden.com/help/cli/enterprise-feature-list

Details the features and their descriptions within the Administrative Features and Capabilities category for Bitwarden Enterprise Organizations, including user management, access control, and policy enforcement.

```APIDOC
Simple user management: Add or remove seats and onboard or offboard users directly from the Web Vault. Learn more.
Role based access control: Assign role-based access for Organization users, including a custom role and granular permissions (e.g. Hide Passwords, Read-Only). Learn more.
Directory sync: Synchronize your Bitwarden Organization with your existing user directory. Provision and deprovision users, groups, and group associations. Learn more.
SCIM support: Use the SCIM protocol to manage and provision Bitwarden users, groups, and group associations from your Identity Provider or directory service for easy onboarding and employee succession. Learn more.
Account recovery administration: Designated administrators can reset Master Password of end-user accounts if an employee loses or forgets their Master Password. Learn more.
Collections with curated access: Create an unlimited amount of password collections containing an unlimited amount of passwords. Collections can be assigned to groups or individual users. Learn more.
Enterprise policies: Enforce security rules for all users, for example mandating use of Two-step Login. Learn more.
Temporary password sharing and generation: Create and share ephemeral data using Bitwarden Send. Learn more.
Complimentary Families plan for users: All enterprise users receive a complimentary family plan for personal use to practice good security habits outside of the workplace. Learn more.
```

--------------------------------

### Condition Note CSV for Bitwarden Import

Source: https://bitwarden.com/help/cli/import-data-from-myki

Specifies the column header changes for Note CSV files exported from Myki mobile apps to be compatible with Bitwarden's import. The 'Exported' format is from Myki, and the 'Expected' format is for Bitwarden.

```CSV
Title,Content,Status
```

```CSV
nickname,status,content
```

--------------------------------

### Whitelist Bitwarden Domain in NoScript

Source: https://bitwarden.com/help/cli/blocker-access-rule

To ensure the Bitwarden Firefox extension can access its API servers, the domain `bitwarden.com` must be explicitly whitelisted within the NoScript extension's settings.

```Text
bitwarden.com
```

--------------------------------

### Bitwarden Helm Chart `my-values.yaml` Configuration

Source: https://bitwarden.com/help/cli/aws-eks-deployment

Specifies essential configuration values for the Bitwarden Helm chart in `my-values.yaml`. These settings link the deployment to the defined Kubernetes SecretProviderClass and service accounts, ensuring proper secret injection and component permissions.

```YAML
secrets:
  secretName: "<secretName defined in your SecretProviderClass (Step 4)>"
  secretProviderClass: "<metedata.name defined in your SecretProviderClass (Step 4)>"
component:
  admin:
    podServiceAccount: "<name defined for your service account (Step 3)>"
  api:
    podServiceAccount: "<name defined for your service account (Step 3)>"
  attachments:
    podServiceAccount: "<name defined for your service account (Step 3)>"
  events:
    podServiceAccount: "<name defined for your service account (Step 3)>"
  icons:
    podServiceAccount: "<name defined for your service account (Step 3)>"
  identity:
    podServiceAccount: "<name defined for your service account (Step 3)>"
  notifications:
    podServiceAccount: "<name defined for your service account (Step 3)>"
  scim:
    podServiceAccount: "<name defined for your service account (Step 3)>"
  sso:
    podServiceAccount: "<name defined for your service account (Step 3)>"
  web:
    podServiceAccount: "<name defined for your service account (Step 3)>"
database:
  podServiceAccount: "<name defined for your service account (Step 3)>"
serviceAccount:
  name: "<name defined for your service account (Step 3)>"
  deployRolesOnly: true
```

--------------------------------

### Perform Offline Bitwarden Database Restore

Source: https://bitwarden.com/help/cli/backup-on-premise

These SQL commands facilitate an offline restore of the `vault` database. The process involves taking the database offline, restoring from a specified full backup file, and then bringing it back online. Ensure to replace `{Backup File Name}` with the actual name of your backup file.

```SQL
use master
GO
alter database vault set offline with rollback immediate
GO
restore database vault from disk='/etc/bitwarden/mssql/backups/vault_FULL_{Backup File Name}.BAK' with replace
GO
alter database vault set online
GO
exit
```

--------------------------------

### Configure Bitwarden SAML Service Provider Settings

Source: https://bitwarden.com/help/cli/saml-microsoft-entra-id

Outlines the SAML service provider configuration fields within the Bitwarden web app, including Name ID Format, Outbound Signing Algorithm, Signing Behavior, Minimum Incoming Signing Algorithm, Want Assertions Signed, and Validate Certificates, with guidance on their typical values for Azure integration.

```APIDOC
Name ID Format:
  Description: By default, Azure will use email address. If you changed this setting, select the corresponding value. Otherwise, set this field to Unspecified or Email Address.
Outbound Signing Algorithm:
  Description: The algorithm Bitwarden will use to sign SAML requests.
Signing Behavior:
  Description: Whether/when SAML requests will be signed.
Minimum Incoming Signing Algorithm:
  Description: By default, Azure will sign with RSA SHA-256. Select `rsa-sha256` from the dropdown.
Want Assertions Signed:
  Description: Whether Bitwarden expects SAML assertions to be signed.
Validate Certificates:
  Description: Check this box when using trusted and valid certificates from your IdP through a trusted CA. Self-signed certificates may fail unless proper trust chains are configured with the Bitwarden login with SSO docker image.
```

--------------------------------

### Condition Address CSV for Bitwarden Import

Source: https://bitwarden.com/help/cli/import-data-from-myki

Outlines the required column adjustments for Address CSV files exported from Myki mobile apps to match Bitwarden's import format. The 'Exported' format is from Myki, and the 'Expected' format is for Bitwarden.

```CSV
Nickname,First Name,Middle Name,Last Name,Email,First Address Line,Second Address Line,Title,Gender,Number,City,Country,Zip Code,Additional Info,Status
```

```CSV
nickname,status,tags,firstName,middleName,lastName,email,firstAddressLine,secondAddressLine,title,gender,number,city,country,zipCode,additionalInfo
```

--------------------------------

### Purge All Collections from Bitwarden Source Organization

Source: https://bitwarden.com/help/cli/migration-script

This command runs the `purgecol` function to delete all collections present in the source Bitwarden organization. Use with caution as this action is irreversible.

```Bash
python3 bwAdminTools.py -c purgecol
```

--------------------------------

### Configure Bitwarden API Connection in Microsoft Sentinel

Source: https://bitwarden.com/help/cli/microsoft-sentinel-siem

This section details the required fields and their corresponding values for connecting a Bitwarden organization to the Microsoft Sentinel Bitwarden Event Logs app. These parameters are essential for establishing secure communication and data flow between Bitwarden and Sentinel.

```APIDOC
Configuration Fields for Bitwarden Event Logs App:
  Bitwarden Identity URL:
    Description: The URL for Bitwarden's identity service.
    Cloud Default: https://identity.bitwarden.com or https://identity.bitwarden.eu
    Self-hosted: https://<self-hosted-url>/identity (no trailing slash)
  Bitwarden API URL:
    Description: The URL for Bitwarden's API service.
    Cloud Default: https://api.bitwarden.com or https://api.bitwarden.eu
    Self-hosted: https://<self-hosted-url>/api (no trailing slash)
  Client ID:
    Description: The client_id value obtained from the Bitwarden organization API key window.
  Client Secret:
    Description: The client_secret value obtained from the Bitwarden organization API key window.
```

--------------------------------

### Microsoft Entra ID SCIM Group Provisioning Behavior

Source: https://bitwarden.com/help/cli/microsoft-entra-id-scim-integration

Details the automated actions taken by Bitwarden when groups are provisioned, modified, or de-provisioned in Microsoft Entra ID via SCIM. This includes group creation, member syncing, and handling of group renames.

```APIDOC
When "Provision Microsoft Entra ID Groups" is enabled:
- New group assigned in Azure: Group created in Bitwarden.
  - Group members already in Bitwarden: Added to the group.
  - Group members not in Bitwarden: Invited to join.
- Existing group assigned in Azure: Bitwarden group linked to Azure through the first available matching precedence attribute.
  - Note: Groups linked in this way will have their members synced from Azure.
- Group renamed in Azure: Updated in Bitwarden (as long as the initial sync has been made).
  - Note: If a group is renamed in Bitwarden, it will be changed back to what it's named in Azure. Always change group names Azure-side.
```

--------------------------------

### Export Bitwarden Vault Data

Source: https://bitwarden.com/help/cli/cli

The `bw export` command allows exporting vault data in various formats such as `.json`, `.csv`, encrypted `.json`, or as a `.zip` with attachments. You can specify the output path, format, encryption password, and target organization.

```Bash
bw export [--output <filePath>] [--format <format>] [--password <password>] [--organizationid <orgid>]
```

```Bash
bw export --organizationid 7063feab-4b10-472e-b64c-785e2b870b92 --format json --output /Users/myaccount/Downloads/
```

--------------------------------

### Bitwarden CLI Data Storage Paths

Source: https://bitwarden.com/help/cli/data-storage

This section provides the default local storage paths for the Bitwarden Command Line Interface (CLI) application across different operating systems. The storage location can be overridden by setting the BITWARDENCLI_APPDATA_DIR environment variable to an absolute path.

```Windows
%AppData%\Bitwarden CLI
```

```macOS
~/Library/Application Support/Bitwarden CLI
```

```Linux
~/.config/Bitwarden CLI
```

--------------------------------

### Bitwarden CLI: Run Command with UUIDs as Environment Variable Names

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Change how secret names are mapped to environment variables. By default, secret names are used. With `--uuids-as-keynames`, POSIX-compliant secret IDs are used instead, which can be useful for programs with strict naming requirements. Alternatively, set the `BWS_UUIDS_AS_KEYNAMES` environment variable.

```Bash
# echo a secret’s value by its POSIX-compliant UUID
bws run --uuids-as-keynames -- 'echo $_64246aa4_70b3_4332_8587_8b1284ce6d76'
```

--------------------------------

### Retrieve Bitwarden Secret with YAML Output Format

Source: https://bitwarden.com/help/cli/secrets-manager-cli

This command retrieves a specific secret and formats the output as YAML using the `--output yaml` flag. The `--output` flag allows users to specify various output formats like JSON, YAML, table, TSV, none, or env.

```Bash
bws secret get 2863ced6-eba1-48b4-b5c0-afa30104877a --output yaml
```

--------------------------------

### Configure Bitwarden Identity Provider Fields for AD FS SSO

Source: https://bitwarden.com/help/cli/saml-adfs

Details the required fields for configuring an identity provider within Bitwarden for AD FS Single Sign-On, including their purpose, expected values, and specific considerations for each field.

```APIDOC
Identity Provider Configuration Fields:
  Entity ID: Enter the retrieved Federation Service Identifier. Please note, this may not use HTTPS. This field is case sensitive.
  Binding Type: By default, AD FS with use HTTP POST endpoint binding. Select HTTP POST unless you have configured AD FS to use a different method.
  Single Sign On Service URL: Enter the SSO Service Endpoint. This value can be constructed in the Service → Endpoints tab in AD FS Manager. The endpoint URL is listed as URL Path for SAML2.0/WS-Federation and is usually something like `https://your-domain/adfs/ls`. You can obtain the exact value from the configuration key for SingleSignOnServce in the `FederationMetadata.xml` document.
  X509 Public Certificate: Paste the downloaded certificate, removing `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` The certificate value is case sensitive, extra spaces, carriage returns, and other extraneous characters will cause certification to fail.
  Outbound Signing Algorithm: By default, AD FS will sign with SHA-256. Select SHA-256 from the dropdown unless you have configured AD FS to use different algorithm.
  Disable Outbound Logout Requests: Login with SSO currently does not support SLO. This option is planned for future development.
  Want Authentication Requests Signed: Whether AD FS expects SAML requests to be signed.
```

--------------------------------

### Create Bitwarden CLI File Send with Deletion Date

Source: https://bitwarden.com/help/cli/create-send

Demonstrates how to create a Bitwarden Send for a file using the CLI, setting a deletion date of 14 days from creation. This command uploads a specified file as an end-to-end encrypted Send.

```Bash
bw send -n "My File Send" - d 14 -f /Users/myaccount/Documents/my_file.pdf
```

--------------------------------

### Include Groups by Microsoft Entra ID Administrative Unit

Source: https://bitwarden.com/help/cli/azure-active-directory

Syntax to include groups in a Bitwarden Directory Connector sync based on their tagged Microsoft Entra ID Administrative Units. Requires the Object ID of the Administrative Unit.

```Bash
includeadministrativeunit:7ckcq6e5-d733-4b96-be17-5bad81fe679d
```

--------------------------------

### Public API Endpoint for Setting External IDs

Source: https://bitwarden.com/help/cli/microsoft-entra-id-scim-integration

Reference to the Bitwarden Public API endpoint used to set external IDs for already-synced users when changing SCIM mapping strategies post-synchronization.

```APIDOC
/public/members/{id}
```

--------------------------------

### Set Secrets in Azure Key Vault

Source: https://bitwarden.com/help/cli/azure-aks-deployment

These Bash commands demonstrate how to set individual secret values within an Azure Key Vault instance using the 'az keyvault secret set' command. Users need to replace '<REPLACE>' with their Key Vault name and the actual secret values. This method records commands in shell history, so alternative secure methods for setting secrets should be considered for production environments.

```Bash
kvname=<REPLACE>
az keyvault secret set --name installationid --vault-name $kvname --value <REPLACE>
az keyvault secret set --name installationkey --vault-name $kvname --value <REPLACE>
az keyvault secret set --name smtpusername --vault-name $kvname --value <REPLACE>
```

--------------------------------

### Generate Default Helm Chart Configuration File

Source: https://bitwarden.com/help/cli/secrets-manager-kubernetes-operator

This command retrieves the default values for the Bitwarden Secrets Manager Operator Helm chart, including development versions, and redirects them into a new file named `my-values.yaml`. This file serves as a template that can be customized for your specific deployment needs.

```bash
helm show values bitwarden/sm-operator --devel > my-values.yaml
```

--------------------------------

### Retrieve Secrets in GitHub Actions Workflow

Source: https://bitwarden.com/help/cli/github-actions-integration

This YAML snippet demonstrates how to add a step to your GitHub Actions workflow to fetch secrets from Bitwarden Secrets Manager. It utilizes the `bitwarden/sm-action@v2` action, requiring an `access_token` (stored as a GitHub secret) and a list of Bitwarden secret IDs mapped to desired environment variable names. For self-hosted instances, `base_url` can be specified.

```YAML
- name: Get Secrets
  uses: bitwarden/sm-action@v2
  with:
    access_token: ${{ secrets.BW_ACCESS_TOKEN }}
    base_url: https://vault.bitwarden.com
    secrets: |
      fc3a93f4-2a16-445b-b0c4-aeaf0102f0ff > SECRET_NAME_1
      bdbb16bc-0b9b-472e-99fa-af4101309076 > SECRET_NAME_2
```

--------------------------------

### List Bitwarden Secrets via CLI

Source: https://bitwarden.com/help/cli/secrets-manager-cli

Use the `bws secret list` command to retrieve secrets accessible by the machine account. This command can list all secrets or filter them by a specific project identifier. The default output is a JSON array of secret objects.

```Bash
bws secret list
```

```Bash
bws secret list e325ea69-a3ab-4dff-836f-b02e013fe530
```

```JSON
[
  {
    "object": "secret",
    "id": "382580ab-1368-4e85-bfa3-b02e01400c9f",
    "organizationId": "10e8cbfa-7bd2-4361-bd6f-b02e013f9c41",
    "projectId": "e325ea69-a3ab-4dff-836f-b02e013fe530",
    "key": "Repository 1",
    "value": "1234567ertthrjytkuy",
    "note": "Main Repo",
    "creationDate": "2023-06-27T19:25:15.822004Z",
    "revisionDate": "2023-06-27T19:25:15.822004Z"
  },
  {
    "object": "secret",
    "id": "be8e0ad8-d545-4017-a55a-b02f014d4158",
    "organizationId": "10e8cbfa-7bd2-4361-bd6f-b02e013f9c41",
    "projectId": "e325ea69-a3ab-4dff-836f-b02e013fe530",
    "key": "SES_KEY",
    "value": "0.982492bc-7f37-4475-9e60",
    "note": "",
    "creationDate": "2023-06-28T20:13:20.643567Z",
    "revisionDate": "2023-06-28T20:13:20.643567Z"
  }
]
```

--------------------------------

### Microsoft Entra ID SCIM User Provisioning Behavior

Source: https://bitwarden.com/help/cli/microsoft-entra-id-scim-integration

Describes the automated actions taken by Bitwarden when users are provisioned, modified, or de-provisioned in Microsoft Entra ID via SCIM. This includes user invitation, linking, access revocation, and removal based on Azure assignments and status changes.

```APIDOC
When "Provision Microsoft Entra ID Users" is enabled:
- New user assigned in Azure: User invited to Bitwarden organization.
- Existing user assigned in Azure: Bitwarden user linked to Azure user through their first available matching precedence attribute.
  - Note: Values like `displayName` and `externalId/mailNickname` are not automatically changed in Bitwarden.
- Assigned user disabled via `accountEnabled` property in Azure: User's access to the organization revoked.
- Assigned user "soft" deleted in Azure: User's access to the organization revoked.
  - When permanently deleted in Azure: User removed from the organization.
- Assigned user removed from the Enterprise application in Azure: User's access to the organization revoked.
- Assigned user removed from a group in Azure: User removed from that group in Bitwarden but remains a member of the organization.
```

--------------------------------

### Bitwarden Web Vault Item Link URL Structure

Source: https://bitwarden.com/help/cli/link-to-an-item

This snippet illustrates the format of a direct link to a Bitwarden vault item in the web vault, highlighting the `itemId` query parameter which uniquely identifies the item.

```URL
?itemnrId=fced56b3-d83c-4b01-8751-ae9301551da7
```