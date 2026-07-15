### Start Tailscale Daemon with Static Binaries

Source: https://tailscale.com/docs/install/linux

Starts the Tailscale daemon using static binaries. This command is part of the manual installation process for distributions not supported by the install script. The `--state` flag specifies the location for the daemon's state file.

```bash
sudo tailscaled --state=tailscaled.state
```

--------------------------------

### Clone Tailscale Kubernetes Examples

Source: https://tailscale.com/docs/kubernetes

Clones the Tailscale GitHub repository to access Kubernetes documentation and example configurations. This is a prerequisite for following the setup and usage examples in this document.

```bash
gh repo clone tailscale/tailscale
cd tailscale/docs/k8s
```

--------------------------------

### Run Tailscale Program (Go)

Source: https://tailscale.com/docs/features/tsnet/how-to/create-basic-tsnet-app

Starts the Tailscale program using 'go run'. It outputs a Tailscale authentication URL for device registration. This is the initial step to get the program running.

```bash
go run .
```

--------------------------------

### Start a Basic Web Server with http-server

Source: https://tailscale.com/docs/features/tailscale-services

Installs and runs a basic web server using Node.js and the `http-server` package. This server listens on port 8080 and serves static files from the current directory. It's a prerequisite for advertising a resource as a Tailscale Service host.

```bash
# Install globally
npm install -g http-server

# Then start a basic web server
http-server -p 8080

```

--------------------------------

### Start WSL 2 Instance

Source: https://tailscale.com/docs/install/windows/wsl2

Command to launch a WSL 2 instance from PowerShell. This is necessary to access the Linux environment for Tailscale installation.

```powershell
wsl.exe
```

--------------------------------

### Install Tailscale Client on Arch Linux

Source: https://tailscale.com/docs/install/arch

Installs the Tailscale package using pacman and enables/starts the Tailscale daemon using systemctl. This is the initial setup step for using Tailscale on Arch Linux.

```bash
pacman -S tailscale
sudo systemctl enable --now tailscaled
```

--------------------------------

### Run DERP Server Binary (Bash)

Source: https://tailscale.com/docs/reference/derp-servers/custom-derp-servers

Starts the DERP server using the installed binary. This command requires a domain name pointing to your server and exposes the DERP server on port 443. Ensure you have the necessary permissions using 'sudo'.

```bash
sudo derper --hostname=example.com

```

--------------------------------

### Enable and Start Tailscale Service

Source: https://tailscale.com/docs/install/amazon-linux-2

Uses 'systemctl' to enable the Tailscale service to start on boot and immediately starts the service.

```bash
sudo systemctl enable --now tailscaled

```

--------------------------------

### Run Tailscale Serve to Forward App Capabilities

Source: https://tailscale.com/docs/reference/examples/serve

This command starts the Tailscale Serve proxy, configured to accept and forward a specific application capability (`example.com/cap/sql`) to a local service running on port 8080. This allows the local service to receive authorization information via the `Tailscale-App-Capabilities` header.

```bash
tailscale serve --accept-app-caps=example.com/cap/sql 8080
```

--------------------------------

### Create Files for File Server Example

Source: https://tailscale.com/docs/reference/examples/funnel

This snippet demonstrates how to create sample files and a directory for the file server example using standard shell commands. It sets up a temporary directory and populates it with text files.

```bash
mkdir /tmp/public
echo "Hello World" > /tmp/public/hello.txt
echo "Pangolin" > /tmp/public/animal.txt
```

--------------------------------

### Initialize Go Module and Install tsnet

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

Initializes a new Go module for the tshello application and installs the necessary tsnet library. This sets up the project structure and fetches the required dependencies.

```bash
go mod init tshello
go get tailscale.com/tsnet
```

--------------------------------

### Install DERP Server from Source (Go)

Source: https://tailscale.com/docs/reference/derp-servers/custom-derp-servers

Installs the latest version of the DERP server binary using the Go toolchain. This command fetches and installs the 'derper' executable to your Go bin directory, typically `$HOME/go/bin`.

```bash
go install tailscale.com/cmd/derper@latest

```

--------------------------------

### Install Tailscale with MSI Properties on Windows

Source: https://tailscale.com/docs/install/windows/msi

Installs Tailscale using the MSI package and customizes the installation by setting MSI properties. This example hides the Network Devices menu item. Replace the filename and property values as needed.

```bash
msiexec TS_NETWORKDEVICES="hide" /i tailscale-setup-1.22.0-amd64.msi
```

--------------------------------

### Install Tailscale via cloud-init Script

Source: https://tailscale.com/docs/install/with-cloud-init

This script automates the installation of Tailscale on a new machine using cloud-init. It downloads the installation script, configures IP forwarding for potential exit node functionality, and joins the tailnet using a provided authentication key. It also includes optional steps for enabling Tailscale SSH and advertising the node as an exit node.

```cloud-config
#cloud-config
# The above header must generally appear on the first line of a cloud config
# file, but all other lines that begin with a # are optional comments.

runcmd:
  # One-command install, from https://tailscale.com/download/
  - ['sh', '-c', 'curl -fsSL https://tailscale.com/install.sh | sh']
  # Set sysctl settings for IP forwarding (useful when configuring an exit node)
  - ['sh', '-c', "echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf && echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf && sudo sysctl -p /etc/sysctl.d/99-tailscale.conf" ]
  # Generate an auth key from your Admin console
  # https://login.tailscale.com/admin/settings/keys
  # and replace the placeholder below
  - ['tailscale', 'up', '--auth-key=tskey-abcdef1432341818']
  # (Optional) Include this line to make this node available over Tailscale SSH
  - ['tailscale', 'set', '--ssh']
  # (Optional) Include this line to configure this machine as an exit node
  - ['tailscale', 'set', '--advertise-exit-node']

```

--------------------------------

### Start and Verify Tailscale on OPNsense

Source: https://tailscale.com/docs/install/opnsense

Commands to enable and start the tailscaled daemon on OPNsense, followed by a command to check the installed Tailscale version. This ensures the service is running and accessible.

```shell
# service tailscaled enable
# service tailscaled start
# tailscale version
root@opnsense:~ # tailscale version
1.56.1
  go version: go1.21.5

```

--------------------------------

### Install Tailscale on RHEL 9

Source: https://tailscale.com/docs/install/rhel/rhel-9

Installs Tailscale on RHEL 9 by adding the official repository and then installing the package using dnf. This is the initial setup step for Tailscale on this operating system.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/rhel/9/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Start tsnet Server

Source: https://tailscale.com/docs/reference/tsnet-server-api

Initializes and starts a tsnet.Server instance with default settings. It's crucial to defer the Close() method to ensure proper cleanup. Errors during startup are fatal.

```go
srv := new(tsnet.Server)
if err := srv.Start(); err != nil {
    log.Fatalf("can't start tsnet server: %v", err)
}
def srv.Close()
```

--------------------------------

### Setting up an OAuth Client

Source: https://tailscale.com/docs/features/oauth-clients

Step-by-step guide to creating a new OAuth client in the Tailscale admin console, including selecting scopes and generating credentials.

```APIDOC
## Setting up an OAuth client

1. Open the Trust credentials page of the admin console.
2. Select the **Credential** button.
3. Select **OAuth**.
4. Select the set of operations that can be performed with tokens created by the new OAuth client. For a given operation, select **Read** or **Write**. For a description of the operations, refer to Scopes.
5. Select **Generate credential**.
6. In the **Credential created** page, you can access the new OAuth client's ID and secret. Copy both the client ID and secret, as you need them for your client code. Note that after you close the **Credential created** page, you won't be able to copy the secret again.

Store the client secret securely.

7. Select **Done**.

Your OAuth client is now configured. Use the client ID and secret when you configure your OAuth client application. Note that Tailscale-generated OAuth client secrets are case-sensitive.

If a user creates an OAuth client, the OAuth client will continue to function and generate API access tokens even if the user no longer has access to the tailnet. Admins can access all configured OAuth clients in the Trust credentials page of the admin console.
```

--------------------------------

### Tailscale Access Rule with Kandji Posture

Source: https://tailscale.com/docs/integrations/kandji

This example demonstrates how to define Tailscale access rules using device posture attributes from Kandji. It allows access to 'tag:production' only from devices where the Kandji agent is installed and active, ensuring a trusted environment.

```json
{
  "postures": {
    "posture:trusted": [
      "kandji:agentInstalled == true"
    ]
  },
  "grants": [
    {
      "src": ["autogroup:member"],
      "dst": ["tag:production"],
      "ip": ["*"],
      "srcPosture": ["posture:trusted"]
    }
  ]
}
```

--------------------------------

### Install and Configure Tailscale on PiKVM

Source: https://tailscale.com/docs/integrations/pikvm

This snippet covers the essential commands to install the Tailscale package on a PiKVM, enable and start the Tailscale service, log in to your Tailscale account, and optionally enable Tailscale SSH. It also includes commands to manage read-write and read-only modes for the PiKVM filesystem.

```bash
# Elevate to root
su -

# Enable read-write mode
rw

# Install tailscale-pikvm package
pacman -Sy tailscale-pikvm

# Enable and start Tailscale service
systemctl enable --now tailscaled

# Log in to Tailscale
tailscale up

# (Optional) Enable Tailscale SSH
tailscale set --ssh

# Revert to read-only mode
ro
```

--------------------------------

### Enable and Start Tailscale Service on CentOS 8

Source: https://tailscale.com/docs/install/centos/centos-8

This command uses `systemctl` to enable the Tailscale service to start on boot and immediately starts the service. This ensures Tailscale runs automatically after system restarts.

```bash
sudo systemctl enable --now tailscaled
```

--------------------------------

### Kubernetes Ingress and Service Configuration Example

Source: https://tailscale.com/docs/reference/troubleshooting/kubernetes-operator

Example Kubernetes Ingress and Service definitions for a Tailscale Ingress setup. This demonstrates how to define the ingress resource with a Tailscale ingress class and a backend service.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: my-app
spec:
ingressClassName: tailscale
rules:
- http:
    paths:
    - backend:
        service:
          name: my-app
          port:
            number: 80
      path: /login
      pathType: Prefix
tls:
- hosts:
  - my-app
---
apiVersion: v1
kind: Service
metadata:
name: my-app
spec:
clusterIP: 192.0.2.9
ports:
- port: 80

```

--------------------------------

### Install Tailscale on OPNsense

Source: https://tailscale.com/docs/install/opnsense

Steps to install Tailscale on OPNsense by updating the ports tree and then installing the tailscale package. This process involves navigating to the tailscale port directory and executing the make install command.

```shell
# opnsense-code ports
Updating OPNsense repository catalogue...
...
Cloning into '/usr/ports'...
...
Your branch is up to date with 'origin/master'.

# cd /usr/ports/security/tailscale
# make install

```

--------------------------------

### Install Motion on Raspberry Pi

Source: https://tailscale.com/docs/solutions/set-up-dogcam

Installs the Motion software, which is used for motion detection and video streaming, on a Raspberry Pi using the apt package manager.

```bash
sudo apt install motion
```

--------------------------------

### Example: Setting Up and Modifying Tailscale L7 Endpoints

Source: https://tailscale.com/docs/features/tailscale-services

Demonstrates the process of setting up multiple L7 endpoints for a service, draining the host, and then selectively removing specific endpoint configurations.

```bash
# Set up a few L7 endpoints:
tailscale serve --service="svc:web-server" --https=443 8080
tailscale serve --service="svc:web-server" --https=443 --set-path /mt2 8081
tailscale serve --service="svc:web-server" --http=80 3000

# When you want to modify config, drain it first.
tailscale serve drain svc:web-server

# Wait until all connections close.

# To only remove the endpoint configuration for the /mt2 path on port 443:
tailscale serve --service="svc:web-server" --https=443 --set-path /mt2 off

# Then, advertise it again and it will only create one endpoint on HTTPS port 443
tailscale serve advertise svc:web-server

# To remove the endpoint configuration for for HTTPS port 443:
tailscale serve --service:"svc:web-server" --https=443 off
# You will see a prompt asking you to confirm
# After you confirm, it removes all configured endpoints on port 443 but preserves other port configured for the same service resource.
# Advertise the service again without the removed HTTPS port:
tailscale serve advertise svc:web-server
```

--------------------------------

### Example Output of Tailscale Drive List

Source: https://tailscale.com/docs/features/taildrive?tab=linux

Example output from the `tailscale drive list` command, showing the 'name', 'path', and 'as' (user context) for each shared directory.

```text
$ tailscale drive list

name      path                      as
------    ----------------------    ----
nas       /media/data-A/nas-data    root
docs      /pi/docs                  root
backup    /pi/system-backups        root

```

--------------------------------

### Install Tailscale on Fedora

Source: https://tailscale.com/docs/install/fedora/fedora-1

Installs Tailscale on Fedora by adding the official repository and then installing the package using DNF. This is the initial step for setting up Tailscale.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/fedora/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Start Tailscale App Connector on Linux

Source: https://tailscale.com/docs/solutions/create-a-secure-connection-to-mongodb-atlas

This command starts a Tailscale client on a Linux device, configuring it as an app connector. It advertises the connector capability and associates it with a specific tag for routing.

```bash
tailscale up --advertise-connector --advertise-tags=tag:atlas-app-connector
```

--------------------------------

### Install Pi-hole using Official Script

Source: https://tailscale.com/docs/solutions/block-ads-all-devices-anywhere-using-raspberry-pi

Downloads and executes the Pi-hole installation script from the official source. It's recommended to review the script's content before execution for security purposes, as it runs with elevated privileges.

```bash
curl -sSL https://install.pi-hole.net | bash
```

--------------------------------

### Install Tailscale on CentOS Stream 9

Source: https://tailscale.com/docs/install/centos/centos-stream-9

Installs Tailscale on CentOS Stream 9 by adding the official repository and then installing the package using dnf. This is the initial setup step for using Tailscale on this operating system.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/centos/9/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Create start.sh for Tailscale and App on Fly.io

Source: https://tailscale.com/docs/install/cloud/flydotio

This shell script initializes the Tailscale daemon in the background, brings up the Tailscale interface using a provided authentication key, and then starts the main application binary. It assumes Tailscale binaries and the application binary are in `/app/`.

```bash
#!/bin/sh

/app/tailscaled --state=/var/lib/tailscale/tailscaled.state --socket=/var/run/tailscale/tailscaled.sock &
/app/tailscale up --auth-key=${TAILSCALE_AUTHKEY} --hostname=fly-app
/app/my-app
```

--------------------------------

### Example: Peer Relay with Two Static Endpoints (Bash)

Source: https://tailscale.com/docs/features/peer-relay

An example command demonstrating how to configure a peer relay to advertise two specific static endpoints: `[2001:db8::1]:40000` and `192.0.2.2:40000`, using UDP port `40000`.

```bash
tailscale set --relay-server-port=40000 --relay-server-static-endpoints="[2001:db8::1]:40000,192.0.2.2:40000"
```

--------------------------------

### Verify WSL 2 Version

Source: https://tailscale.com/docs/install/windows/wsl2

This command checks if the Windows Subsystem for Linux is running version 2. It's a prerequisite for following the installation guide.

```powershell
wsl -l -v
```

--------------------------------

### Parallel Testing with Tailscale Matrix Strategy

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This example demonstrates using a GitHub Actions matrix strategy to run parallel test jobs that require Tailscale access. Each job in the matrix gets its own ephemeral Tailscale connection, allowing concurrent testing against private infrastructure. It configures the Tailscale connection using the `tailscale/github-action@v4` and then executes service-specific test scripts.

```yaml
strategy:
  matrix: 
    service: [database, api, frontend]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - name: Connect to Tailscale
      uses: tailscale/github-action@v4
      with:
        oauth-client-id: ${{ secrets.TS_OAUTH_CLIENT_ID }}
        oauth-secret: ${{ secrets.TS_OAUTH_SECRET }}
        tags: tag:ci

    - name: Test ${{ matrix.service }}
      run: |
        ./test-${{ matrix.service }}.sh

```

--------------------------------

### Manual Tailscale Update Commands

Source: https://tailscale.com/docs/features/client/update?tab=ios

Provides examples of commands to manually update the Tailscale client on different operating systems. These commands are essential for users who prefer or require manual control over their Tailscale installations.

```bash
# Linux (Debian/Ubuntu)
sudo apt update && sudo apt upgrade tailscale

# Linux (Fedora/CentOS)
sudo dnf upgrade tailscale

# macOS (using Homebrew)
brew upgrade tailscale

# Windows (using winget)
winget upgrade tailscale
```

--------------------------------

### Configure Motion Daemon to Start Automatically

Source: https://tailscale.com/docs/solutions/set-up-dogcam

Modifies the default motion configuration file to ensure the motion detection daemon starts automatically when the Raspberry Pi boots up.

```bash
sudo nano /etc/default/motion
```

```ini
start_motion_daemon=yes
```

--------------------------------

### Configure App Connectors for Domains

Source: https://tailscale.com/docs/reference/syntax/policy-file

This example configures the `example-connector` tag for the `example.com` domains using the `app` section of the policy file. It specifies routes and connects to devices tagged with `tag:example-connector`.

```json
{
  "target": ["*"],
  "app": {
    "tailscale.com/app-connectors": [
      {
        "name": "example-app",
        "connectors": ["tag:example-connector"],
        "domains": ["example.com"],
        "routes": ["192.0.2.0/24"]
      }
    ]
  }
}
```

--------------------------------

### Install code-server using curl script

Source: https://tailscale.com/docs/solutions/code-on-ipad-vscode-caddy-code-server

Installs code-server on the server using a one-line curl command. This script downloads and executes the official installation script for code-server.

```bash
curl -fsSL https://code-server.dev/install.sh | sh
```

--------------------------------

### Start Tailscale Web Server

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Starts a web server for controlling the `tailscaled` daemon, useful for devices where the CLI is impractical. Allows configuration of CGI mode, listen address, origin, URL prefix, and read-only mode.

```bash
tailscale web [flags]

```

--------------------------------

### Install Tailscale on Ubuntu

Source: https://tailscale.com/docs/how-to/secure-ubuntu-server-with-ufw

Install the Tailscale client on your Ubuntu server using a curl script. This command downloads and executes the official installation script from Tailscale.

```bash
curl -fsSL https://tailscale.com/install.sh | sh

```

--------------------------------

### Install Tailscale Repository and Package on CentOS Stream 10

Source: https://tailscale.com/docs/install/centos/centos-stream-10

Adds the official Tailscale repository for CentOS 10 and then installs the Tailscale package using dnf. This is the first step to get Tailscale onto your system.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/centos/10/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Install Tailscale Repository and Package on Oracle Linux 8

Source: https://tailscale.com/docs/install/oracle-linux/oracle-linux-8

Adds the official Tailscale stable repository for Oracle Linux 8 and then installs the Tailscale package using dnf. This is the initial setup step for Tailscale on this operating system.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/oracle/8/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Install Docker on Linux

Source: https://tailscale.com/docs/features/containers/docker/how-to/connect-docker-container

Installs Docker on a Linux device or cloud VM using a curl script and executes the installation. It also includes commands to modify user permissions for Docker interaction and verify the installation.

```bash
curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh
sudo usermod -aG docker username
docker run --rm hello-world
```

--------------------------------

### Install and Configure Tailscale Client on Hetzner VM

Source: https://tailscale.com/docs/install/cloud/hetzner

This snippet demonstrates how to install the Tailscale client on a Hetzner virtual machine and then bring the machine online within your Tailscale network. It involves downloading and executing an installation script and running the 'tailscale up' command.

```bash
# curl -fsSL https://tailscale.com/install.sh | sh
# tailscale up
```

--------------------------------

### Create tshello directory and initialize Go module

Source: https://tailscale.com/docs/features/tsnet/how-to/create-basic-tsnet-app

These commands create a new directory for the project and initialize a Go module within it, setting up the basic structure for a Go application.

```bash
mkdir tshello
cd tshello
go mod init tshello
```

--------------------------------

### Install Tailscale Repository and Package on Oracle Linux 10

Source: https://tailscale.com/docs/install/oracle-linux/oracle-linux-10

Adds the Tailscale stable repository for Oracle Linux 10 and installs the Tailscale package using dnf. This is the initial step to get Tailscale onto the system.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/oracle/10/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Install Caddy on Ubuntu

Source: https://tailscale.com/docs/solutions/code-on-ipad-vscode-caddy-code-server

These commands install Caddy on an Ubuntu server. They add Caddy's GPG key and repository, update package lists, and install Caddy as a service. This ensures Caddy is up-to-date and properly integrated.

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https curl
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
chmod o+r /usr/share/keyrings/caddy-stable-archive-keyring.gpg
chmod o+r /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

--------------------------------

### Example DNS Test Output on macOS

Source: https://tailscale.com/docs/reference/dns-in-tailscale

This example demonstrates the output of the `dscacheutil` command when querying for a MagicDNS hostname. It shows the resolved domain name and its corresponding IP address, confirming successful DNS resolution.

```bash
name: my-server.example.ts.net
ip_address: 100.15.193.72
```

--------------------------------

### Make Scripts Executable and Start Service

Source: https://tailscale.com/docs/solutions/set-up-minecraft

This command makes the `start.sh` and `stop.sh` scripts executable. Following this, the Minecraft server service can be started using `systemctl`.

```bash
chmod +x /opt/minecraft/start.sh /opt/minecraft/stop.sh
systemctl start minecraft
```

--------------------------------

### Define Multiple Tailscale Postures

Source: https://tailscale.com/docs/features/device-posture

This example demonstrates defining multiple distinct postures within a single Tailscale policy file. It includes 'posture:latestMac' and 'posture:anyMac', each with specific attribute requirements for matching devices.

```json
"postures": {
  "posture:latestMac": [
    "node:os == 'macos'",
    "node:osVersion == '13.4.0'",
    "node:tsReleaseTrack == 'stable'",
  ],
  "posture:anyMac": [
    "node:os == 'macos'",
    "node:tsReleaseTrack == 'stable'",
  ]
}
```

--------------------------------

### Install apt-transport-https Plugin (Bash)

Source: https://tailscale.com/docs/install/rpi/rpi-bookworm

Installs the 'apt-transport-https' plugin required for managing packages over HTTPS. This is a prerequisite for adding external repositories.

```bash
sudo apt-get install apt-transport-https

```

--------------------------------

### Install Tailscale using MSI on Windows

Source: https://tailscale.com/docs/install/windows/msi

Installs the Tailscale client on Windows using the MSI package. This command can be used with or without logging enabled. The MSI file and log file path should be replaced with the actual paths.

```bash
msiexec /i <path_to_tailscale_msi.msi>
msiexec /L <path_to_log.log> /i <path_to_tailscale_msi.msi>
```

--------------------------------

### Configure Tailscale Access Rules with Jamf Pro Posture

Source: https://tailscale.com/docs/integrations/jamf-pro

This example demonstrates how to define Tailscale access rules that leverage Jamf Pro device posture attributes. It requires the Jamf Pro integration to be set up and devices to have 'remoteManaged' and 'supervised' attributes reported by Jamf Pro. The rules grant access to 'tag:production' only for devices meeting these posture criteria.

```json
{
  "postures": {
    "posture:trusted": [
      "jamfPro:remoteManaged == true",
      "jamfPro:supervised == true"
    ]
  },
  "grants": [
    {
      "src": ["autogroup:member"],
      "dst": ["tag:production"],
      "ip": ["*"],
      "srcPosture": ["posture:trusted"]
    }
  ]
}
```

--------------------------------

### Initialize and Start tsnet Server in Go

Source: https://tailscale.com/docs/features/tsnet

This Go code initializes and starts a tsnet.Server, which is the primary entry point for connecting to your Tailscale network. It requires specifying an address to listen on and a hostname for the device within the tailnet. The server must be started before interacting with the tailnet.

```go
var (
	addr     = flag.String("addr", ":80", "address to listen on")
	hostname = flag.String("hostname", "tshello", "hostname to use in the tailnet")
)

func main() {
	flag.Parse()
	srv := new(tsnet.Server)
	srv.Addr = *addr
	srv.Hostname = *hostname
	if err := srv.Start(); err != nil {
		log.Fatalf("can't start tsnet server: %v", err)
	}
	defer srv.Close()

	// Use the tsnet.Server object to interact with your tailnet
    ...
}

```

--------------------------------

### Verify and Install Curl on Raspberry Pi OS

Source: https://tailscale.com/docs/install/rpi/rpi-trixie

Checks if `curl` is installed and provides commands to install it if it's not found. This is a prerequisite for downloading Tailscale packages.

```bash
curl --version
```

```bash
apt-get update
apt-get install curl
```

--------------------------------

### Start and Defer Close tsnet Server

Source: https://tailscale.com/docs/reference/tsnet-server-api

This snippet shows the essential steps to start a tsnet Server connection and ensure it is properly closed using defer. The Start method initiates the connection, and defer srv.Close() guarantees resource cleanup when the function exits.

```go
srv := new(tsnet.Server)

if err := srv.Start(); err != nil {
    log.Fatal(err)
}
defersrv.Close()

```

--------------------------------

### Start HTTPS and HTTP Servers with Tailscale Serve

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

The `tailscale serve` command can start both HTTPS and HTTP servers. It supports modes like reverse proxy, file server, and static text server. HTTPS traffic uses automatically provisioned TLS certificates. The `--https=<port>` or `--http=<port>` flags specify the listening port, and `<target>` defines the content to serve.

```bash
tailscale serve --https=<port> <target> [off]
tailscale serve --http=<port> <target> [off]
```

--------------------------------

### Call Tailscale API for Network Logs

Source: https://tailscale.com/docs/features/logging/network-flow-logs

This example demonstrates how to use `curl` to make a GET request to the Tailscale API's network logging endpoint. It utilizes the previously set environment variables for authentication and time range filtering. The output is raw JSON.

```shell
curl -u $ACCESS_TOKEN: \
  "https://api.tailscale.com/api/v2/tailnet/{$TAILNET_ID}/logging/network?start={$START}&end={$END}"

```

--------------------------------

### Configure Default Tags via Helm

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/customize

This example shows how to set default tags for proxy devices when installing the Tailscale operator with Helm, using the `.proxyConfig.defaultTags` value.

```yaml
# Example Helm values snippet
proxyConfig:
  defaultTags: "tag:prod,tag:emea"
```

--------------------------------

### Get Network Flow Logs

Source: https://tailscale.com/docs/features/logging/network-flow-logs

Retrieves network flow logs within a specified time range. The `start` and `end` parameters define the timeframe for the logs.

```APIDOC
## GET /websites/tailscale/logs

### Description
Retrieves network flow logs within a specified time range. The `start` and `end` parameters define the timeframe for the logs.

### Method
GET

### Endpoint
/websites/tailscale/logs

### Parameters
#### Query Parameters
- **start** (string) - Required - Start of the timeframe, in RFC 3339 timestamp format, for the logs to retrieve. For example: `2022-07-20T00:00:00Z`.
- **end** (string) - Required - End of the timeframe, in RFC3339 timestamp format, for the logs to retrieve. For example: `2022-07-20T23:59:59Z`.

### Request Example
```
GET /websites/tailscale/logs?start=2022-07-20T00:00:00Z&end=2022-07-20T23:59:59Z
```

### Response
#### Success Response (200)
- **Message** (object) - Contains details about the log entry.
  - **NodeID** (string) - The ID of the node from which the message originated.
  - **OS** (string) - The operating system of the node.
  - **User** (string) - The user that owns the node (if not tagged).
  - **Tags** (array of strings) - The tags of the node (if owned by a user).
- **Start** (string) - The start timestamp of the network flow.
- **End** (string) - The end timestamp of the network flow.
- **SrcNode** (string) - The source node ID of the network flow.
- **DstNodes** (array of strings) - The destination node IDs of the network flow.
- **VirtualTraffic** (object) - Details about virtual traffic.
- **SubnetTraffic** (object) - Details about subnet traffic.
- **ExitTraffic** (object) - Details about exit traffic.
- **PhysicalTraffic** (object) - Details about physical traffic.

#### Response Example
```json
{
  "Message": {
    "NodeID": "node-123",
    "OS": "linux",
    "User": "johndoe@example.com",
    "Tags": ["tag:prod"]
  },
  "Start": "2022-07-20T10:00:00Z",
  "End": "2022-07-20T10:00:05Z",
  "SrcNode": "node-123",
  "DstNodes": ["node-456", "node-789"],
  "VirtualTraffic": {
    "Bytes": 1024
  },
  "SubnetTraffic": {
    "Bytes": 512
  },
  "ExitTraffic": {
    "Bytes": 0
  },
  "PhysicalTraffic": {
    "Bytes": 1024
  }
}
```
```

--------------------------------

### Run Tailscale Serve for a Local Port

Source: https://tailscale.com/docs/features/tailscale-serve

This command starts Tailscale Serve to share a local service running on a specific port (e.g., port 3000) with other devices on your Tailscale network. It requires Tailscale to be installed and configured, and HTTPS to be enabled in your tailnet. The command outputs a URL accessible within your tailnet.

```bash
tailscale serve 3000
```

--------------------------------

### Starter Plan Tailscale ACL for Remote Device Access

Source: https://tailscale.com/docs/reference/examples/acls

This example provides a basic Tailscale ACL configuration suitable for Starter plan users, enabling remote access to corporate and production devices. It defines access for all members, admins, and tag owners.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": [
        "autogroup:member"
      ],
      "dst": [
        "autogroup:self:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "autogroup:member"
      ],
      "dst": [
        "tag:corp:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "autogroup:admin"
      ],
      "dst": [
        "tag:prod:*"
      ]
    }
  ],
  "tagOwners": {
    "tag:corp": [
      "autogroup:admin"
    ],
    "tag:prod": [
      "autogroup:admin"
    ]
  }
}
```

--------------------------------

### View Tailscale IP Routes (Linux)

Source: https://tailscale.com/docs/reference/troubleshooting?tab=macos

On Linux, view routes installed by Tailscale using the `ip route` command with table 52, as these are not displayed by legacy tools like `netstat`.

```bash
ip route show table 52
```

--------------------------------

### Tailscale Infrastructure as Code with Terraform

Source: https://tailscale.com/docs/reference/best-practices/security

This example shows how to use the Terraform Tailscale provider to programmatically manage Tailscale infrastructure. It demonstrates defining a tailnet policy file, setting DNS configurations, and generating authentication keys.

```hcl
provider "tailscale" {
  # Configure your Tailscale provider here
}

resource "tailscale_tailnet_policy" "example" {
  policy = "{\"acls\": [{\"action\": \"accept\", \"src\": [\"group:example\"], \"dst\": [\"*:*\"]}]}"
}

resource "tailscale_dns_settings" "example" {
  magicdns = true
  nameservers = ["100.100.100.100"]
}

resource "tailscale_auth_key" "example" {
  reusable = true
  description = "Terraform generated key"
}

```

--------------------------------

### Log Retrieval API Parameters (Example)

Source: https://tailscale.com/docs/features/logging/network-flow-logs

Illustrates the usage of 'start' and 'end' query parameters for retrieving Tailscale network flow logs. These parameters define the time range for the logs, specified in RFC 3339 timestamp format. The API returns all logs within the specified range, and 'end' can exceed the latest known timestamp.

```text
API Endpoint Example:
GET /logs?start=2022-07-20T00:00:00Z&end=2022-07-20T23:59:59Z
```

--------------------------------

### Enable and start code-server systemd service

Source: https://tailscale.com/docs/solutions/code-on-ipad-vscode-caddy-code-server

Configures systemd to automatically start code-server on boot and immediately starts the service for the current user. This ensures code-server runs in the background.

```bash
sudo systemctl enable --now code-server@$USER
```

--------------------------------

### Set Default ProxyClass via Helm

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/customize

This example shows how to configure a default ProxyClass for the Tailscale operator when installing via Helm, using the `proxyConfig.defaultProxyClass` value.

```yaml
# Example Helm values snippet
proxyConfig:
  defaultProxyClass: "default-proxy-class-name"
```

--------------------------------

### Tailscale Funnel File Server Example

Source: https://tailscale.com/docs/reference/tailscale-cli/funnel

An example of using `tailscale funnel` to serve files from a local directory. This requires providing the absolute path to the file or directory. Note the macOS limitation for serving files/directories.

```bash
tailscale funnel /home/alice/blog/index.html
```

--------------------------------

### DigitalOcean NixOS Installation Script

Source: https://tailscale.com/docs/solutions/set-up-nixos-minecraft

This cloud-config YAML file is used for DigitalOcean Droplets to install NixOS. It writes a host configuration file and then executes a script to replace the existing Ubuntu installation with NixOS, using the specified host configuration.

```yaml
#cloud-config
write_files:
  - path: /etc/nixos/host.nix
    permissions: "0644"
    content: |
      { pkgs, config, ... }:

      {

      }

runcmd:
  - curl https://raw.githubusercontent.com/elitak/nixos-infect/master/nixos-infect | PROVIDER=digitalocean NIXOS_IMPORT=./host.nix NIX_CHANNEL=nixos-20.09 bash 2>&1 | tee /tmp/infect.log

```

--------------------------------

### Tailscale: Build and Run get-authkey Utility

Source: https://tailscale.com/docs/features/oauth-clients

Provides instructions and commands to build and run the `get-authkey` utility, which generates authentication keys for scripts. It requires Go 1.23+ and environment variables for OAuth client ID and secret. Various parameters like `-tags`, `-reusable`, `-ephemeral`, and `-preauth` can be used.

```bash
export TS_API_CLIENT_ID=<clientID> TS_API_CLIENT_SECRET=<secret>

```

```bash
go run tailscale.com/cmd/get-authkey@latest -tags tag:development

```

```bash
go run tailscale.com/cmd/get-authkey@latest -reusable -tags tag:development

```

```bash
go run ./cmd/get-authkey/main.go -tags tag:development

```

--------------------------------

### Get Mullvad Exit Node NodeKeys with jq

Source: https://tailscale.com/docs/features/exit-nodes/mullvad-exit-nodes?tab=linux

This command uses `jq` to filter and extract the `DNSName` and `NodeKey` of Mullvad exit nodes from the output of `tailscale lock status --json`. It requires `jq` to be installed.

```bash
tailscale lock status --json | jq '[.FilteredPeers[] | select(.DNSName | contains("mullvad.ts.net")) | {DNSName, NodeKey: .NodeKey}] | sort_by(.DNSName)'
```

--------------------------------

### Install apt-transport-https plugin on Raspberry Pi

Source: https://tailscale.com/docs/install/rpi

Installs the 'apt-transport-https' plugin, which is required for APT to fetch packages over HTTPS. This is a prerequisite for adding external repositories.

```bash
sudo apt-get install apt-transport-https

```

--------------------------------

### Provision Server with Tags and Auth Key

Source: https://tailscale.com/docs/how-to/set-up-servers

This command illustrates provisioning a server with Tailscale using an authentication key and explicitly advertising tags. This is necessary if the authentication key was not originally generated with specific tags associated with it.

```bash
tailscale up --auth-key=$TS_AUTHKEY --advertise-tags=<tags>

```

--------------------------------

### Expose Local Server with Tailscale Funnel

Source: https://tailscale.com/docs/reference/examples/funnel

Exposes a local HTTP server running on a specified port to the internet via HTTPS using Tailscale Funnel. This allows public access to your development server. It requires Tailscale to be installed and configured.

```bash
sudo tailscale funnel 3000
```

--------------------------------

### Install Tailscale package on Raspberry Pi

Source: https://tailscale.com/docs/install/rpi

Updates the package list and installs the Tailscale client on your Raspberry Pi. This command fetches the latest package information and then installs the 'tailscale' package.

```bash
sudo apt-get update
sudo apt-get install tailscale

```

--------------------------------

### Verify curl Installation (Shell)

Source: https://tailscale.com/docs/install/debian/debian-trixie

Checks if the `curl` command-line tool is installed on the system. `curl` is a prerequisite for downloading Tailscale packages.

```shell
curl --version
```

--------------------------------

### Tailscale SSH Rule: Domain Users to Tagged Devices

Source: https://tailscale.com/docs/features/tailscale-ssh

This example allows any user from the 'example.com' domain to SSH into devices tagged 'tag:prod'. Users authenticate as their local part (e.g., 'dave' for 'dave@example.com').

```json
{
  "grants": [
    {
      "src": ["user:*@example.com"],
      "dst": ["tag:prod"],
      "ip": ["*"]
    }
  ],
  "ssh": [
    {
      "action": "accept",
      "dst": ["tag:prod"],
      "src": ["user:*@example.com"],
      "users": ["localpart:*@example.com"]
    }
  ]
}
```

--------------------------------

### Install Yum Repository Manager

Source: https://tailscale.com/docs/install/amazon-linux-2

Installs the 'yum-utils' package, which provides the 'yum-config-manager' command used to add repositories.

```bash
sudo yum install yum-utils

```

--------------------------------

### Install Tailscale Package on openSUSE Leap

Source: https://tailscale.com/docs/install/opensuse/opensuse-leap-15-5

Installs the Tailscale package on openSUSE Leap after the repository has been added. It first refreshes the package list and then installs the 'tailscale' package using zypper.

```shell
sudo zypper ref
sudo zypper in tailscale
```

--------------------------------

### Install Tailscale on Mainstream Linux Distributions

Source: https://tailscale.com/docs/install/linux

Installs the Tailscale client on mainstream Linux distributions using a curl script. This method is suitable for distributions with package managers like apt, yum, or zypper. It downloads and executes an installation script from Tailscale's official repository.

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

--------------------------------

### Install Tailscale on Oracle Linux 9

Source: https://tailscale.com/docs/install/oracle-linux/oracle-linux-9

Installs Tailscale on Oracle Linux 9 by adding the official repository and then installing the package using dnf. This is the initial step for setting up Tailscale.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/oracle/9/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Install curl (Shell)

Source: https://tailscale.com/docs/install/debian/debian-trixie

Installs the `curl` utility using the APT package manager if it's not already present. This is necessary for downloading files from the internet.

```shell
apt-get update
apt-get install curl
```

--------------------------------

### Get Tailscale IPv4 Address

Source: https://tailscale.com/docs/install/opensuse/opensuse-leap-15-6

This command retrieves and displays the Tailscale IPv4 address assigned to the current machine. This is useful for verifying the connection and for use in network configurations. This command requires root privileges.

```shell
sudo tailscale ip -4
```

--------------------------------

### Install apt-transport-https on Ubuntu

Source: https://tailscale.com/docs/install/ubuntu/ubuntu-1604

Installs the apt-transport-https plugin, which is required to fetch packages over HTTPS. This is a prerequisite for adding external repositories.

```bash
sudo apt-get install apt-transport-https
```

--------------------------------

### Install Packages and Create Minecraft User on Debian/Ubuntu

Source: https://tailscale.com/docs/solutions/set-up-minecraft

This snippet demonstrates the commands to create a dedicated system user for the Minecraft server and install necessary packages like unzip, curl, tmux, git, and wget on Debian-based Linux distributions.

```bash
adduser --system --home /opt/minecraft minecraft
addgroup --system minecraft
adduser minecraft minecraft
chsh --shell /bin/bash minecraft
apt install unzip curl tmux git wget
```

--------------------------------

### Tailscale IP Set Syntax Example

Source: https://tailscale.com/docs/features/tailnet-policy-file/ip-sets

Defines the basic structure for creating an IP set within a Tailscale tailnet policy file. It shows how to name an IP set and specify operations to add or remove targets.

```json
"ipsets": {
  "ipset:<name>": [
    "add <target>",
    "remove <target>"
  ]
}
```

--------------------------------

### Install Tailscale Operator with Helm

Source: https://tailscale.com/docs/features/kubernetes-operator

This command installs or upgrades the Tailscale operator using Helm. It specifies the namespace, creates it if it doesn't exist, and passes OAuth client details as string values. The '--wait' flag ensures the command waits for the installation to complete.

```bash
helm upgrade \
  --install \
  tailscale-operator \
  tailscale/tailscale-operator \
  --namespace=tailscale \
  --create-namespace \
  --set-string oauth.clientId="<OAauth client ID>" \
  --set-string oauth.audience="<OAuth client audience>" \
  --wait
```

--------------------------------

### Set Up Go Environment in GitHub Actions

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This step configures the Go programming language environment for the GitHub Actions runner using the 'actions/setup-go@v5' action. It specifies the Go version to be '1.23', ensuring the correct toolchain is available for building and testing Go applications.

```yaml
- name: Set up Go
  uses: actions/setup-go@v5
  with:
    go-version: '1.23'
```

--------------------------------

### Start Script for Tailscale and Application on Koyeb

Source: https://tailscale.com/docs/install/cloud/koyeb

A shell script that starts the Tailscale daemon and connects to the tailnet using a provided authentication key. It then runs the application binary. The `--ssh` flag enables SSH access to the node from the tailnet.

```shell
#!/bin/sh
# Start Tailscale
/app/tailscaled --state=/var/lib/tailscale/tailscaled.state --socket=/var/run/tailscale/tailscaled.sock &
/app/tailscale up --ssh --auth-key=${TAILSCALE_AUTHKEY} --hostname=tailscale-on-koyeb

# Start your app
/app/my-app

```

--------------------------------

### Add Tailscale Repo and Install on Fedora

Source: https://tailscale.com/docs/install/fedora/fedora-2

This snippet adds the official Tailscale repository to your Fedora system and then installs the Tailscale package using the DNF package manager. Ensure you have sudo privileges to execute these commands.

```bash
sudo dnf config-manager addrepo --from-repofile=https://pkgs.tailscale.com/stable/fedora/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Install Tailscale on RHEL 10 using DNF

Source: https://tailscale.com/docs/install/rhel/rhel-10

This snippet demonstrates how to add the Tailscale repository and install the Tailscale package on RHEL 10 using the DNF package manager. It ensures that the necessary repository is configured before proceeding with the installation.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/rhel/10/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Capture Network Traffic with Tailscale CLI

Source: https://tailscale.com/docs/reference/troubleshooting

This command captures network traffic within a Tailscale tunnel and saves it to a pcap file. It's useful for debugging and inspecting unencrypted packets. The output file can be analyzed with Wireshark after installing a specific Lua dissector.

```bash
tailscale debug capture -o /path/to/capture.pcap
```

--------------------------------

### Install Tailscale on Raspberry Pi OS

Source: https://tailscale.com/docs/install/rpi/rpi-stretch

Updates the package list and installs the Tailscale package. This command ensures your system has the latest package information before installing Tailscale.

```bash
sudo apt-get update && sudo apt-get install tailscale
```

--------------------------------

### Get Tailscale IPv4 Address

Source: https://tailscale.com/docs/install/debian/debian-bookworm

This command retrieves and displays the Tailscale IPv4 address assigned to your machine. This is useful for verifying connectivity and for use in network configurations. This command requires root privileges.

```bash
sudo tailscale ip -4
```

--------------------------------

### Create startup script for Tailscale and application

Source: https://tailscale.com/docs/install/cloud/cloudrun

This shell script initializes Tailscale in userspace networking mode and starts the application. It uses the TAILSCALE_AUTHKEY environment variable for authentication and sets up a SOCKS5 proxy for the application to use. The script ensures Tailscale is running before launching the main application.

```shell
#!/bin/sh

/app/tailscaled --tun=userspace-networking --socks5-server=localhost:1055 &
/app/tailscale up --auth-key=${TAILSCALE_AUTHKEY} --hostname=cloudrun-app
echo Tailscale started
ALL_PROXY=socks5://localhost:1055/ /app/my-app

```

--------------------------------

### Verify Tailscale Installation - Status

Source: https://tailscale.com/docs/install/linux

Checks the connection status of the Tailscale client. This command helps confirm that the device is connected to the tailnet and can communicate with other nodes.

```bash
tailscale status
```

--------------------------------

### Install and Configure Tailscale on EC2

Source: https://tailscale.com/docs/install/cloud/aws

Installs Tailscale on an EC2 instance, enables the systemd service, and advertises specific subnet routes. This requires IP forwarding to be enabled and user authentication to the Tailscale network.

```shell
sudo systemctl enable --now tailscaled
sudo tailscale set --advertise-routes=10.0.0.0/24,10.0.1.0/24
```

--------------------------------

### Install Tailscale Package (Bash)

Source: https://tailscale.com/docs/install/rpi/rpi-bookworm

Updates the package list and installs the Tailscale client on your Raspberry Pi OS system. This command fetches the latest version from the added repository.

```bash
sudo apt-get update && sudo apt-get install tailscale

```

--------------------------------

### Set up .env for Tailscale Auth Key

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This snippet shows how to create a .env file to store your Tailscale authentication key. This key is necessary for the tests to authenticate with Tailscale and establish network connections. Ensure you replace the placeholder with your actual auth key.

```shell
TS_AUTHKEY=<your-ts-auth-key>

```

--------------------------------

### Grant Access to Tailscale Service (JSON Example)

Source: https://tailscale.com/docs/features/tailscale-services

Example of a JSON grant rule to provide access to a Tailscale Service. It specifies the source group, destination service, and the port for access.

```json
{
  "src":  ["autogroup:member"],
  "dst":  ["svc:web-server"],
  "ip": ["443"],
}
```

--------------------------------

### Install Tailscale Operator

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

Installs or upgrades the Tailscale operator in the 'tailscale' namespace. It configures the operator with provided OAuth client ID and secret, and waits for the installation to complete.

```bash
helm upgrade --install operator tailscale/tailscale-operator \
    -n tailscale --create-namespace \
    --set oauth.clientId=<id> \
    --set oauth.clientSecret=<key> \
    --wait

```

--------------------------------

### Extract Tailscale Static Binaries

Source: https://tailscale.com/docs/install/linux

Unpacks the Tailscale static binaries archive. This command is used when installing Tailscale on Linux distributions not covered by the automated install script. Replace `<version>` and `<architecture>` with the appropriate values for your download.

```bash
tar xvf tailscale_<version>_<architecture>.tgz
```

--------------------------------

### Make HTTP GET Request (Go)

Source: https://tailscale.com/docs/features/tsnet/how-to/create-basic-tsnet-app

Makes an HTTP GET request to a resource within the Tailscale network using a configured HTTP client. It then prints the response body to standard output.

```go
resp, err := httpCli.Get("http://tshello")
if err != nil {
	log.Fatal(err)
}
deffer resp.Body.Close()

_, err = io.Copy(os.Stdout, resp.Body)
if err != nil {
	log.Fatal(err)
}
```

--------------------------------

### Fetch and Process Tailscale Network Logs with netlogfmt

Source: https://tailscale.com/docs/features/logging/network-flow-logs

This example demonstrates how to fetch network logs from the Tailscale API using `curl` and then process them with the `netlogfmt` tool. It utilizes the `--resolve-addrs=names` flag to convert IP addresses to hostnames and requires API key and tailnet name for older client versions.

```shell
curl -u $ACCESS_TOKEN:  -X GET \
  "https://api.tailscale.com/api/v2/tailnet/{$TAILNET_ID}/logging/network?start={$START}&end={$END}" \
  | go run tailscale.com/cmd/netlogfmt@latest --resolve-addrs=names --api-key=$ACCESS_TOKEN --tailnet-name=$TAILNET

```

--------------------------------

### Example Hook Grant for Specific User (Aperture)

Source: https://tailscale.com/docs/features/aperture/configuration

An example demonstrating how to configure a hook grant to send specific data ('tools', 'user_message') to a webhook ('my-webhook') for requests originating from a particular user ('developer@company.com') and matching specific providers and events.

```json
{
  "temp_grants": [
    {
      "src": ["developer@company.com"],
      "grants": [
        {
          "hook": {
            "match": {
              "providers": ["anthropic", "openai"],
              "models": ["*"],
              "events": ["tool_call_entire_request"]
            },
            "hook": "my-webhook",
            "fields": ["tools", "user_message"]
          }
        }
      ]
    }
  ]
}
```

--------------------------------

### Tailscale Funnel Static Text Server Example

Source: https://tailscale.com/docs/reference/tailscale-cli/funnel

An example of configuring `tailscale funnel` to serve static plain text. The `text:<value>` format is used to specify the content to be served.

```bash
tailscale funnel text:"Hello, world!"
```

--------------------------------

### Add Tailscale Repository and Install (Bash)

Source: https://tailscale.com/docs/install/centos/centos-7

Adds the official Tailscale stable repository for CentOS 7 and then installs the Tailscale package using yum.

```bash
sudo yum-config-manager --add-repo https://pkgs.tailscale.com/stable/centos/7/tailscale.repo
sudo yum install tailscale

```

--------------------------------

### Install Tailscale CLI Tab Completion for Bash (macOS)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=bash

This command installs Tailscale CLI tab completions for Bash on macOS using Homebrew. It places the completion script in the appropriate Homebrew directory, making it available in new shell sessions. Ensure Homebrew is installed.

```bash
tailscale completion bash > $(brew --prefix)/etc/bash_completion.d/tailscale
```

--------------------------------

### Docker Compose Example with Tailscale

Source: https://tailscale.com/docs/features/containers/docker

A complete Docker Compose configuration demonstrating how to set up Tailscale with an Nginx service. It includes environment variables for authentication, advertising tags, state directory, and userspace networking, along with volume mounts and device capabilities for network administration.

```yaml
---
version: "3.7"
services:
  tailscale-nginx:
    image: tailscale/tailscale:latest
    hostname: tailscale-nginx
    environment:
      - TS_AUTHKEY=tskey-client-notAReal-OAuthClientSecret1Atawk
      - TS_EXTRA_ARGS=--advertise-tags=tag:container
      - TS_STATE_DIR=/var/lib/tailscale
      - TS_USERSPACE=false
    volumes:
      - ${PWD}/tailscale-nginx/state:/var/lib/tailscale
    devices:
      - /dev/net/tun:/dev/net/tun
    cap_add:
      - net_admin
    restart: unless-stopped
  nginx:
    image: nginx
    depends_on:
      - tailscale-nginx
    network_mode: service:tailscale-nginx

```

--------------------------------

### Configure Tailscale Access Rules with SentinelOne Posture

Source: https://tailscale.com/docs/integrations/sentinelone

This example demonstrates how to define Tailscale access rules that leverage SentinelOne device posture attributes. It specifies conditions for 'posture:trusted' based on SentinelOne's operational state and active threats, and then grants access to 'tag:production' only to devices meeting these trusted criteria.

```json
"postures": {
  "posture:trusted": [
    "sentinelOne:operationalState == 'na'",
    "sentinelOne:activeThreats == 0"
  ]
},
"grants": [
  {
    "src": ["autogroup:member"],
    "dst": ["tag:production"],
    "ip": ["*"],
    "srcPosture": ["posture:trusted"]
  }
]
```

--------------------------------

### Create Static Site Files

Source: https://tailscale.com/docs/reference/examples/funnel

This snippet shows the content for an index.html and styles.css file, which together form a simple static website. These files would be placed in a directory to be served by Tailscale Funnel.

```html
<html>
  <head>
    <title>Hello World</title>
    <link rel="stylesheet" href="/styles.css" />
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

```css
*,
html {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: monospace;
  font-size: 10vw;
  text-transform: uppercase;
}

body {
  position: absolute;
  left: 50%;
  top: 25%;
  transform: translate3d(-50%, -50%, 0);
  overflow: hidden;
}

h1 {
  position: relative;
  top: 2em;
  animation: slide-up 3s infinite;
}

@keyframes slide-up {
  0% {
    top: 2em;
  }
  50% {
    top: 0em;
  }
  100% {
    top: 2em;
  }
}
```

--------------------------------

### Create HTTP Client with Server.HTTPClient

Source: https://tailscale.com/docs/reference/tsnet-server-api

Provides a convenient wrapper for creating an HTTP client pre-configured for outgoing connections within your tailnet. The Start method is called implicitly at the time of use when making HTTP requests. This method does not implicitly call Start.

```go
srv := new(tsnet.Server)
srv.Hostname = "looker"

cli := srv.HTTPClient()

resp, err := cli.Get("http://yourmachine/hello")
if err != nil {
    log.Fatal(err)
}


```

--------------------------------

### Set up Raw TCP Forwarder with Tailscale Serve

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

Configure a raw TCP forwarder using `tailscale serve` with the `--tcp=<port>` flag, followed by the target TCP service. This forwards raw TCP packets to the specified local port.

```bash
tailscale serve --tcp=<port> tcp://localhost:<local-port> [off]
```

--------------------------------

### Install Tailscale VPN on macOS

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Installs the Tailscale VPN configuration into the macOS system settings. This allows the system to manage the Tailscale connection.

```bash
tailscale configure mac-vpn install
```

--------------------------------

### Print QNAP Tailscale Package Path and Run CLI Command

Source: https://tailscale.com/docs/integrations/qnap

This snippet demonstrates how to retrieve the installation path of the Tailscale QPKG on a QNAP device and subsequently execute the `tailscale` command-line interface with provided arguments. It's useful for scripting or direct terminal access to manage Tailscale configurations.

```shell
# print the package path:
echo $(getcfg SHARE_DEF defVolMP -f /etc/config/def_share.info)/.qpkg/Tailscale/
# run the tailscale CLI:
$(getcfg SHARE_DEF defVolMP -f /etc/config/def_share.info)/.qpkg/Tailscale/tailscale ...
```

--------------------------------

### Add Tailscale Repository and Install Tailscale

Source: https://tailscale.com/docs/install/amazon-linux-2

Adds the official Tailscale stable repository for Amazon Linux 2 and then installs the Tailscale package using yum.

```bash
sudo yum-config-manager --add-repo https://pkgs.tailscale.com/stable/amazon-linux/2/tailscale.repo
sudo yum install tailscale

```

--------------------------------

### Add Tailscale Repository and Key on Ubuntu

Source: https://tailscale.com/docs/install/ubuntu/ubuntu-2004

This snippet adds Tailscale's package signing key and repository to your Ubuntu system. It uses `curl` to download the necessary files and `tee` to save them to the appropriate locations. Ensure `curl` is installed before running these commands.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/focal.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/focal.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Advertise App Connector with Tags

Source: https://tailscale.com/docs/how-to/set-up-high-availability

This command sets up a machine as an app connector and advertises it with a specific tag. This is the first step in configuring multiple app connectors for high availability, allowing Tailscale to group and manage them.

```bash
sudo tailscale up --advertise-connector --advertise-tags="tag:connector"
```

--------------------------------

### Add Tailscale Repository and Key (Bash)

Source: https://tailscale.com/docs/install/ubuntu/ubuntu-2404

This snippet adds Tailscale's package signing key and repository to your Ubuntu system. It uses `curl` to download the key and list files, piping them to `tee` to save them in the appropriate locations. Ensure `curl` is installed before running.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/noble.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/noble.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Deploy Sample Nginx Application

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

Deploys a simple Nginx web server as a `Pod` and exposes it via a Kubernetes `Service`. This serves as a sample workload to test ingress routing.

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
---
apiVersion: v1
kind: Service
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    run: nginx

```

--------------------------------

### Example JWT Token Structure

Source: https://tailscale.com/docs/features/workload-identity-federation?tab=github+actions

This example illustrates a typical JSON Web Token (JWT) structure, showing common claims like 'sub' (subject), 'iss' (issuer), 'aud' (audience), and custom claims like 'user'. This helps in understanding how to reference claims in Tailscale configuration.

```json
{
	"sub": "123456-example",
	"iss": "https://example.com",
	"aud": "api.tailscale.com/12345-67890",
	"user": "example"
}

```

--------------------------------

### Create Layer 3 Tailscale Service Endpoint (CLI Example)

Source: https://tailscale.com/docs/features/tailscale-services

Command to create a Layer 3 protocol-agnostic endpoint for a Tailscale Service using the `tailscale serve` command with the `--tun` flag. This forwards all traffic unmodified.

```bash
tailscale serve --service=svc:<service-name> --tun
```

--------------------------------

### Create a basic HTML file for testing

Source: https://tailscale.com/docs/features/tailscale-funnel/how-to/host-websites

This snippet demonstrates the basic HTML structure for a test website. It includes a heading and a paragraph, serving as a simple placeholder for content when testing website hosting.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Test Website</title>
    </head>
    <body>
        <h1>This is a heading</h1>
        <p>This is a paragraph</p>
    </body>
</html>

```

--------------------------------

### Test Subnet Connectivity with Ping

Source: https://tailscale.com/docs/features/site-to-site

Demonstrates testing the established site-to-site connection between two subnets using the `ping` command. This example shows pinging a device in subnet B from a device in subnet A.

```bash
ping 172.16.100.3

PING 172.16.100.3 (172.16.100.3) 56(84) bytes of data.
64 bytes from 172.16.100.3: icmp_seq=1 ttl=64 time=9.34 ms
64 bytes from 172.16.100.3: icmp_seq=2 ttl=64 time=3.85 ms
```

--------------------------------

### Full Tailscale Policy Example

Source: https://tailscale.com/docs/features/tailscale-ssh

An example of a comprehensive Tailscale access control policy, including grants and SSH rules. This policy defines broad access and specific SSH rules for self, tagged devices, and shared tagged devices.

```json
{
  "grants": [
    {
      "src": ["*"],
      "dst": ["*"],
      "ip": ["*"]
    }
  ],
  "ssh": [
    {
      "action": "accept",
      "dst": ["autogroup:self"],
      "src": ["autogroup:member"],
      "users": ["root", "autogroup:nonroot"]
    },
    {
      "action": "accept",
      "dst": ["tag:prod"],
      "src": ["autogroup:member"],
      "users": ["root", "autogroup:nonroot"]
    },
    {
      "action": "accept",
      "dst": ["tag:prod"],
      "src": ["tag:logging"],
      "users": ["root", "autogroup:nonroot"]
    }
  ]
}
```

--------------------------------

### Apply Multiple Postures with OR Logic in Tailscale Grants

Source: https://tailscale.com/docs/features/device-posture

This example shows how to specify multiple postures in the 'srcPosture' field of a Tailscale 'grants' rule, using OR logic. Access to 'tag:production' is permitted if the connecting device meets any of the listed postures ('posture:approvedMacs', 'posture:approvedWindows', 'posture:approvedLinux').

```json
"grants": [
  {
    "src": ["group:dev"],
    "dst": ["tag:production"],
    "ip": ["*"],
    "srcPosture": ["posture:approvedMacs", "posture:approvedWindows", "posture:approvedLinux"]
  }
]
```

--------------------------------

### Configure Tailscale Access Rules with Fleet Posture

Source: https://tailscale.com/docs/integrations/fleet

This example demonstrates how to adjust Tailscale access rules using device posture attributes from Fleet. It defines a posture rule 'posture:managed' that checks for the 'fleet:present' attribute and then grants access to 'tag:production' only from devices meeting this posture. This requires the Fleet posture integration to be set up.

```json
{
  "postures": {
    "posture:managed": [
      "fleet:present"
    ]
  },
  "grants": [
    {
      "src": ["autogroup:member"],
      "dst": ["tag:production"],
      "ip": ["*"],
      "srcPosture": ["posture:managed"]
    }
  ]
}
```

--------------------------------

### Configure ufw to Lock Down Ubuntu Server

Source: https://tailscale.com/docs/integrations/firewalls

Example of using `ufw` (Uncomplicated Firewall) on Ubuntu to restrict traffic and enforce the use of Tailscale. This snippet demonstrates how to set up firewall rules to allow only necessary traffic over the Tailscale network.

```bash
# Example ufw configuration to restrict traffic over Tailscale
# This is a conceptual example and requires specific rules based on your needs.
# sudo ufw default deny incoming
# sudo ufw default deny outgoing
# sudo ufw allow in on tailscale0 from any to any
# sudo ufw allow out on tailscale0 from any to any
# sudo ufw allow ssh # Example: Allow SSH access if needed
# sudo ufw enable
```

--------------------------------

### Add Tailscale Repository and Key on Ubuntu

Source: https://tailscale.com/docs/install/ubuntu/ubuntu-1604

Adds Tailscale's package signing key and repository to your system's sources. This allows `apt-get` to find and install Tailscale packages. It uses `curl` to download the key and repository list, and `tee` to save them to the appropriate file.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/xenial.gpg | sudo apt-key add -
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/xenial.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Add Tailscale Repository and Key on Ubuntu

Source: https://tailscale.com/docs/install/ubuntu/ubuntu-2104

This snippet adds Tailscale's package signing key and repository to your Ubuntu system. It uses curl to download the necessary files and pipes them to tee for saving in the appropriate locations. Ensure curl is installed before running these commands.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/hirsute.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/hirsute.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Add Tailscale Package Signing Key and Repository on Ubuntu

Source: https://tailscale.com/docs/install/ubuntu/ubuntu-2510

This snippet adds Tailscale's package signing key and repository to your Ubuntu system, allowing you to install and manage Tailscale packages via apt. It uses curl to fetch the necessary files and pipes them to the appropriate locations.

```shell
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/questing.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/questing.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Example Tailscale API Access Token Response

Source: https://tailscale.com/docs/features/oauth-clients

This is an example JSON response received after successfully generating an API access token from the Tailscale OAuth token endpoint.

```json
{"access_token":"tskey-0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ","token_type":"Bearer","expires_in":3600,"scope":"devices"}

```

--------------------------------

### Define tsnet Hello, World program in Go

Source: https://tailscale.com/docs/features/tsnet/how-to/create-basic-tsnet-app

This Go program demonstrates using tsnet as a library to create a simple HTTP server. It listens on a specified address, handles incoming requests, and uses Tailscale's LocalClient to identify the connecting user. It supports HTTPS if listening on port 443.

```Go
// This program demonstrates how to use tsnet as a library.
package main

import (
	"crypto/tls"
	"flag"
	"fmt"
	"html"
	"log"
	"net/http"
	"strings"

	"tailscale.com/tsnet"
)

var (
	addr = flag.String("addr", ":80", "address to listen on")
)

func main() {
	flag.Parse()
	srv := new(tsnet.Server)
	defer srv.Close()
	ln, err := srv.Listen("tcp", *addr)
	if err != nil {
		log.Fatal(err)
	}
	defer ln.Close()

	lc, err := srv.LocalClient()
	if err != nil {
		log.Fatal(err)
	}

	if *addr == ":443" {
		ln = tls.NewListener(ln, &tls.Config{
			GetCertificate: lc.GetCertificate,
		})
	}

	log.Fatal(http.Serve(ln, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		who, err := lc.WhoIs(r.Context(), r.RemoteAddr)
		if err != nil {
			http.Error(w, err.Error(), 500)
			return
		}
		fmt.Fprintf(w, "<html><body><h1>Hello, world!</h1>\n")
		fmt.Fprintf(w, "<p>You are <b>%s</b> from <b>%s</b> (%s)</p>",
			html.EscapeString(who.UserProfile.LoginName),
			html.EscapeString(firstLabel(who.Node.ComputedName)),
			r.RemoteAddr)
	})))
}

func firstLabel(s string) string {
	s, _, _ = strings.Cut(s, ".")
	return s
}

```

--------------------------------

### Tailscale Funnel Use Cases

Source: https://tailscale.com/docs/reference/tailscale-cli/funnel

Examples demonstrating how to use `tailscale funnel` for different types of services.

```APIDOC
## Tailscale Funnel Use Cases

### Description

This section details various ways to use the `tailscale funnel` command, including serving HTTPS/HTTP servers, files, directories, and static text.

### Use Cases

#### 1. HTTPS and HTTP Servers

Exposes an HTTPS server that can act as a reverse proxy, file server, or static text server. HTTPS traffic is secured with automatically provisioned TLS certificates.

**Usage:**
```bash
tailscale funnel --https=<port> <target> [off]
```

**Parameters:**
- **`--https=<port>`**: Specifies the port to listen on. Allowed ports: `443`, `8443`, `10000`.
- **`--set-path=<path>`**: A slash-separated URL path (e.g., `/`).
- **`<target>`**: The service to expose. Can be:
    - **Reverse proxy**: `localhost:3000` or `http://127.0.0.1:3000`
    - **File server**: `/home/alice/blog/index.html` (absolute path)
    - **Static text server**: `text:"Hello, world!"`

**Example (Reverse Proxy):**
```bash
tailscale funnel --https=8443 localhost:3000
```

**Example (File Server):**
```bash
tailscale funnel --https=8443 /home/user/public_html
```

**Example (Static Text):**
```bash
tailscale funnel --https=8443 text:"Welcome to my service!"
```

**Note:** File serving is not available on macOS App Store or Standalone variants due to sandbox limitations.

#### 2. TCP Forwarding

Exposes a TCP forwarder to forward TCP packets.

**Usage:**
```bash
tailscale funnel --tcp=<port> <target>
```

**Parameters:**
- **`--tcp=<port>`**: The port to listen on for TCP connections.
- **`<target>`**: The local TCP service address (e.g., `localhost:8080`).

**Example:**
```bash
tailscale funnel --tcp=8080 localhost:80
```

#### 3. TLS-Terminated TCP Forwarding

Exposes a TCP forwarder for TLS-terminated TCP packets.

**Usage:**
```bash
tailscale funnel --tls-terminated-tcp=<port> <target>
```

**Parameters:**
- **`--tls-terminated-tcp=<port>`**: The port to listen on for TLS-terminated TCP connections.
- **`<target>`**: The local TCP service address (e.g., `localhost:8443`).

**Example:**
```bash
tailscale funnel --tls-terminated-tcp=443 localhost:8443
```

```

--------------------------------

### Install Dependencies with Go Mod Tidy

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

Ensures all project dependencies, including the tsnet library, are correctly downloaded and recorded in the go.mod file. This command tidies up the module dependencies.

```bash
go mod tidy
```

--------------------------------

### API Request Example (cURL)

Source: https://tailscale.com/docs/features/tailscale-accessbot-jit

This cURL command demonstrates how to make an API request to set a device posture attribute. It includes the endpoint, authentication, and the JSON payload for the attribute's value and expiry.

```bash
curl "https://api.tailscale.com/api/v2/device/11055/attributes/custom:my_attribute" \
-u "tskey-api-xxxxx:" \
--data-binary '{"value": "my_value", "expiry": "2024-04-23T18:25:43.511Z"}'
```

--------------------------------

### Install jq Package Manager

Source: https://tailscale.com/docs/integrations/proxmox

Installs the 'jq' package manager, a dependency for the Tailscale certificate generation script. This can be done using either 'apt' on Debian-based systems or 'brew' on macOS.

```bash
apt -y install jq

```

```bash
brew install jq

```

--------------------------------

### Build and Push Container Images with Tailscale

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This example demonstrates building and pushing Docker container images to a private registry using Tailscale. It executes `docker build` and `docker push` commands targeting a private registry endpoint on the tailnet, without exposing the registry to the internet. This ensures secure image management within your private network.

```yaml
- name: Build and push container
  run: |
    docker build -t registry.tail-scale.ts.net/my-app:${{ github.sha }} .
    docker push registry.tail-scale.ts.net/my-app:${{ github.sha }}

```

--------------------------------

### Go Test for tshello Server Initialization and Shutdown

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This Go test function, `TestTshelloServer`, verifies that the tshello server can initialize correctly, create a listener, and shut down gracefully. It utilizes the `tsnet` package to create a temporary server and validates its startup and shutdown process within a given timeout.

```go
func TestTshelloServer(t *testing.T) {
 if testing.Short() {
  t.Skip("skipping test in short mode")
 }

 ctx, cancel := context.WithTimeout(context.Background(), 2*time.Minute)
 defer cancel()

 srv := &tsnet.Server{
  Hostname: "tshello-test",
  Dir:      t.TempDir(),
 }
 defer srv.Close()

 ln, err := srv.Listen("tcp", ":0")
 if err != nil {
  t.Fatalf("failed to listen: %v", err)
 }
 defer ln.Close()

 lc, err := srv.LocalClient()
 if err != nil {
  t.Fatalf("failed to get local client: %v", err)
 }

 serverURL := fmt.Sprintf("http://%s", ln.Addr().String())
 t.Logf("Test server listening on %s", serverURL)

 httpServer := &http.Server{
  Handler: http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
   who, err := lc.WhoIs(r.Context(), r.RemoteAddr)
   if err != nil {
    http.Error(w, err.Error(), 500)
    return
   }
   fmt.Fprintf(w, "Hello, %s!", who.UserProfile.LoginName)
  }),
 }

 errCh := make(chan error, 1)
 go func() {
  errCh <- httpServer.Serve(ln)
 }()

 select {
 case <-ctx.Done():
  t.Fatal("test timed out waiting for server to start")
 case err := <-errCh:
  if err != nil && err != http.ErrServerClosed {
   t.Fatalf("server error: %v", err)
  }
 case <-time.After(5 * time.Second):
  t.Log("Server started successfully")
 }

 if err := httpServer.Shutdown(ctx); err != nil {
  t.Logf("server shutdown error: %v", err)
 }
}

```

--------------------------------

### Example Tailscale Application Capability Grant

Source: https://tailscale.com/docs/reference/troubleshooting/grants

Demonstrates a correctly structured application capability grant within a Tailscale policy file. This example shows how to define source, destination, IP, and application-specific capabilities, including parameters like `dataSrc` for the `tailscale.com/cap/tailsql` capability.

```json
{
  "grants": [
    {
      "src": ["group:eng"],
      "dst": ["tag:tailsql"],
      "ip":  ["tcp:443"],
      "app": {
        "tailscale.com/cap/tailsql": [
          {
            "dataSrc": ["prod", "staging"]
          }
        ]
      }
    }
  ]
}
```

--------------------------------

### Configure Tailscale ACL for App Capabilities

Source: https://tailscale.com/docs/reference/examples/serve

This example demonstrates how to define access control lists (ACLs) in Tailscale to grant specific application capabilities to users or tagged nodes. It shows how to specify source groups, destination tags, and the application capabilities with their respective source scopes.

```json
{
  "grants": [
    {
      "src": ["group:eng"],
      "dst": ["tag:sql"],
      "app": {
        "example.com/cap/sql": [
          {"src": ["main", "self"]}
        ]
      }
    },
    {
      "src": ["group:admin"],
      "dst": ["tag:sql"],
      "app": {
        "example.com/cap/sql": [
          {"src": ["*"]}
        ]
      }
    }
  ]

}
```

--------------------------------

### Minecraft Server Start Script

Source: https://tailscale.com/docs/solutions/set-up-minecraft

This shell script (`start.sh`) is responsible for launching the Minecraft Bedrock server. It uses `tmux` to create a detached session named 'minecraft', starts the server, and sets two game rules: `showcoordinates` and `keepInventory`.

```bash
#!/bin/sh
/usr/bin/tmux new-session -s minecraft -d
tmux send -t minecraft "LD_LIBRARY_PATH=. ./bedrock_server" ENTER
tmux send -t minecraft "gamerule showcoordinates true" ENTER
tmux send -t minecraft "gamerule keepInventory true" ENTER
```

--------------------------------

### Get Tailscale Serve Service Configuration

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

Retrieves the configuration for services hosted by the current node. The output is in a format suitable for later use with `set-config`. Flags like `--all` or `--service=<name>` can filter the configuration retrieved.

```bash
tailscale serve get-config <file> [--all | --service=<name>]
```

--------------------------------

### Configure Federated Identities with tailscale-client-go-v2

Source: https://tailscale.com/docs/features/workload-identity-federation

Demonstrates how to configure federated identities using the `tailscale-client-go-v2` Go library. This involves creating a `tailscale.Client` and a `tailscale.CreateFederatedIdentityRequest` with relevant identity details.

```Go
package main

import (
	"context"
	"os"

	"tailscale.com/client/tailscale/v2"
)

func main() {
	client := &tailscale.Client{
		// Client configuration
	}

	req := tailscale.CreateFederatedIdentityRequest {
		Description: "Example federated identity",
		Scopes:  []string{"auth_keys", "devices:core"},
		Tags:    []string{"tag:test"},
		Subject: "example-sub-*",
		CustomClaimRules: map[string]string{
			"repo_name": "example-repo-name",
		},
	}

	federatedIdentity, err := client.Keys().CreateFederatedIdentity(context.Background(), req)
}

```

--------------------------------

### Configure Tailscale ACLs with Provisioned Groups

Source: https://tailscale.com/docs/reference/examples/acls

This example shows how to configure Tailscale ACLs using provisioned groups, which are managed by identity providers. It simplifies ACL management by avoiding manual group definitions within the ACL file.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": [
        "group:engineering@example.com"
      ],
      "dst": [
        "tag:frontend:*",
        "tag:backend:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "group:devops@example.com"
      ],
      "dst": [
        "tag:frontend:*",
        "tag:backend:*",
        "tag:logging:*"
      ]
    }
  ]
}
```

--------------------------------

### Configure and Advertise a Service Host with `tailscale serve`

Source: https://tailscale.com/docs/features/tailscale-services

Configures a device as a Service host and advertises an endpoint for a Tailscale Service. This command automatically handles configuration and advertisement, and provisions a TLS certificate for HTTPS endpoints. Approval from an admin may be required.

```bash
tailscale serve --service=svc:web-server --https=443 127.0.0.1:8080

```

--------------------------------

### Add Repository and Install Tailscale on RHEL 8

Source: https://tailscale.com/docs/install/rhel/rhel-8

This snippet adds the official Tailscale repository for RHEL 8 and then installs the Tailscale package using the dnf package manager. Ensure you have sudo privileges to execute these commands.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/rhel/8/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### Install Tailscale Manually on AWS VM

Source: https://tailscale.com/docs/install/cloud/aws/quickstart

Installs the Tailscale client on an AWS EC2 VM using a curl command. It requires SSH access to the VM and provides options for authentication using an auth key or manual login via a browser.

```bash
curl -fsSL https://tailscale.com/install.sh | sh
```

```bash
sudo tailscale up --auth-key=foo
```

```bash
sudo tailscale up
```

--------------------------------

### Tailscale ACL Policy Syntax Example

Source: https://tailscale.com/docs/features/access-control/acls

This example demonstrates the basic structure of a Tailscale Access Control List (ACL) policy file. It defines an 'accept' action, specifying the source devices or users allowed to connect to a particular destination device and port.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": [ <list-of-sources> ], // These sources (devices or users)
      "dst": [ <destination>:<port> ], // can access these destination devices on their defined ports
    }
  ]
}
```

--------------------------------

### Install Tailscale Kubernetes Operator with Helm

Source: https://tailscale.com/docs/features/kubernetes-operator

Installs or upgrades the Tailscale Kubernetes operator using Helm. This command deploys the operator into the 'tailscale' namespace and configures it with provided OAuth client credentials.

```bash
helm upgrade \
  --install \
  tailscale-operator \
  tailscale/tailscale-operator \
  --namespace=tailscale \
  --create-namespace \
  --set-string oauth.clientId="<OAauth client ID>" \
  --set-string oauth.clientSecret="<OAuth client secret>" \
  --wait
```

--------------------------------

### Install Tailscale CLI Integration on macOS (Standalone)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=macos

Instructions to install the Tailscale CLI integration for the Standalone macOS client. This requires macOS version 13.0 or later and adds a 'tailscale' launcher to '/usr/local/bin/tailscale'.

```bash
tailscale completion <shell> [--flags] [--descs]
```

--------------------------------

### Manually Ping Tailscale Peers using CLI

Source: https://tailscale.com/docs/integrations/github/github-action

This example demonstrates how to use the 'tailscale ping' command directly within a workflow step to check connectivity to a specific Tailscale peer. This is an alternative to using the 'ping' input parameter in the GitHub Action.

```bash
tailscale ping my-target.my-tailnet.ts.net

```

--------------------------------

### Install Tailscale Repository and Package on CentOS 8

Source: https://tailscale.com/docs/install/centos/centos-8

This snippet adds the official Tailscale repository for CentOS 8 and then installs the Tailscale package using dnf. Ensure you have sudo privileges to execute these commands.

```bash
sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/centos/8/tailscale.repo
sudo dnf install tailscale
```

--------------------------------

### HTTP Server with Tailscale LocalClient Identity Lookup (Go)

Source: https://tailscale.com/docs/reference/tsnet-server-api

This Go code snippet demonstrates how to set up an HTTP server using `tsnet.Server` and leverage the `LocalClient` to identify incoming connections. It retrieves user profile and node information for each request, handling potential errors during the lookup process. The `LocalClient` is implicitly started if not already running.

```go
s := new(tsnet.Server)
s.Hostname = "aran"
defers.Close()

ln, err := s.Listen("tcp", ":80")
if err != nil {
    log.Fatal(err)
}
defers.Close()

lc, err := s.LocalClient()
if err != nil {
    log.Fatal(err)
}

log.Fatal(http.Serve(ln, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
    who, err := lc.WhoIs(r.Context(), r.RemoteAddr)
    if err != nil {
        http.Error(w, err.Error(), 500)
        return
    }
    fmt.Fprintf(w, "<html><body><h1>Hello, world!</h1>\n")
    fmt.Fprintf(w, "<p>You are <b>%s</b> from <b>%s</b> (%s)</p>",
        html.EscapeString(who.UserProfile.LoginName),
        html.EscapeString(firstLabel(who.Node.ComputedName)),
        r.RemoteAddr)
        }))

```

--------------------------------

### Provision Server with Tailscale Auth Key

Source: https://tailscale.com/docs/how-to/set-up-servers

This command demonstrates how to provision a new server onto a Tailscale network using an authentication key. The `--auth-key` flag is essential for connecting the server. This is the basic command to initiate the connection.

```bash
tailscale up --auth-key=$TS_AUTHKEY

```

--------------------------------

### Tailscale Policy File Example with Entra ID Groups

Source: https://tailscale.com/docs/integrations/identity/entra/entra-id-scim

Example of a Tailscale policy file demonstrating how to refer to Microsoft Entra ID groups using their human-readable name or group ID. This allows for granular access control within the Tailscale network.

```json
{
  "grants": [
    {
      "src": ["group:groupname@example.com"],
      "dst": ["*"],
      "ip": ["*"]
    },
    {
      "src": ["group:all employees@example.com"],
      "dst": ["autogroup:self"],
      "ip": ["*"]
    },
    {
      "src": ["group:3ac067a2-f424-87b0-14a3-926482d83980@example.com"],
      "dst": ["tag:logging"],
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Grant Access to Group of Tailscale Services (JSON Example)

Source: https://tailscale.com/docs/features/tailscale-services

Example of a JSON grant rule to grant access to a group of Tailscale Services identified by a tag. It specifies the source tag, destination service, and the port.

```json
{
  "src":  ["tag:prod-service"],
  "dst":  ["svc:database"],
  "ip": ["5432"],
}
```

--------------------------------

### Install Tailscale CLI Tab Completion for Bash (Linux)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=bash

This command installs Tailscale CLI tab completions for Bash on Linux systems. It directs the completion script to a system-wide directory, ensuring completions are available in new shell sessions. This requires root privileges.

```bash
tailscale completion bash > /etc/bash_completion.d/tailscale
```

--------------------------------

### Define Tailscale Access Rules with Huntress Posture

Source: https://tailscale.com/docs/integrations/huntress

This example demonstrates how to define Tailscale access rules that leverage device posture attributes from Huntress. It specifies conditions for antivirus scanning and firewall status to grant access to tagged resources. This configuration is typically managed via the Tailscale policy file.

```json
{
  "postures": {
    "posture:trusted": [
      "huntress:defenderStatus == 'Healthy'",
      "huntress:firewallStatus == 'Enabled'"
    ]
  },
  "grants": [
    {
      "src": ["autogroup:member"],
      "dst": ["tag:production"],
      "ip": ["*"],
      "srcPosture": ["posture:trusted"]
    }
  ]
}
```

--------------------------------

### Add Tailscale Repository on openSUSE

Source: https://tailscale.com/docs/install/opensuse/opensuse-leap-15-4

Adds Tailscale's package signing key and repository to the system using rpm and zypper commands. This is a prerequisite for installing Tailscale on openSUSE Leap 15.4.

```bash
sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/leap/15.4/repo.gpg
sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/leap/15.4/tailscale.repo
```

--------------------------------

### Tailscale Funnel Reverse Proxy Example

Source: https://tailscale.com/docs/reference/tailscale-cli/funnel

An example of configuring `tailscale funnel` to act as a reverse proxy for a local HTTP web server. The target specifies the address of the local service.

```bash
tailscale funnel localhost:3000
```

--------------------------------

### Configure Federated Identities with tailscale-client-go-v2

Source: https://tailscale.com/docs/features/workload-identity-federation?tab=github+actions

Demonstrates how to configure federated identities using the `tailscale-client-go-v2` library. It shows the creation of a `CreateFederatedIdentityRequest` with relevant parameters.

```Go
package main

import (
	"context"
	"os"

	"tailscale.com/client/tailscale/v2"
)

func main() {
	client := &tailscale.Client{
		// Client configuration
	}

	req := tailscale.CreateFederatedIdentityRequest {
		Description: "Example federated identity",
		Scopes:  []string{"auth_keys", "devices:core"},
		Tags:    []string{"tag:test"},
		Subject: "example-sub-*",
		CustomClaimRules: map[string]string{
			"repo_name": "example-repo-name",
		},
	}

	federatedIdentity, err := client.Keys().CreateFederatedIdentity(context.Background(), req)
}

```

--------------------------------

### Configure Tailscale Serve as a File Server

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

Serve files or directories using `tailscale serve` by providing an absolute path to the file or directory as the `<target>`. If a directory is specified, it will render a directory listing. This feature has limitations on macOS for certain installation types.

```bash
tailscale serve /home/alice/blog/index.html
```

--------------------------------

### Create start.sh script for Tailscale on Heroku

Source: https://tailscale.com/docs/install/cloud/heroku

This shell script initializes Tailscale in userspace networking mode and then starts the application. It uses the TAILSCALE_AUTHKEY environment variable for authentication and sets ALL_PROXY to route traffic through the Tailscale SOCKS5 proxy.

```shell
#!/bin/sh

/app/tailscaled --tun=userspace-networking --socks5-server=localhost:1055 & 
/app/tailscale up --auth-key=${TAILSCALE_AUTHKEY} --hostname=heroku-app
echo Tailscale started
ALL_PROXY=socks5://localhost:1055/ /app/my-app

```

--------------------------------

### Connect to Windows RDP using FreeRDP

Source: https://tailscale.com/docs/solutions/access-remote-desktops-using-windows-rdp?tab=linux+%28freerdp%29

This command-line instruction demonstrates how to initiate an RDP connection to a remote Windows PC using the FreeRDP client. It requires the username, password, and the host address (Tailscale IP or hostname) of the remote machine. Ensure FreeRDP is installed on your local machine.

```bash
xfreerdp /u:<username> /p:<password> /v:<hostaddress>
```

--------------------------------

### Add Tailscale Repository on openSUSE

Source: https://tailscale.com/docs/install/opensuse/opensuse-leap-15-2

This snippet adds Tailscale's package signing key and repository to the openSUSE Leap 15.2 system. It uses `rpm` to import the key and `zypper` to add the repository, enabling the installation of Tailscale packages.

```bash
sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/leap/15.2/repo.gpg
sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/leap/15.2/tailscale.repo
```

--------------------------------

### Tailscale Serve Status Output

Source: https://tailscale.com/docs/features/tailscale-serve

This is an example of the output when the `tailscale serve` command is run successfully. It shows the URL accessible within the tailnet and the service being proxied. The session runs in the foreground and can be stopped by pressing Ctrl+C.

```text
tailscale serve 3000
Available within your tailnet:
https://amelie-workstation.pango-lin.ts.net

|-- / proxy http://127.0.0.1:3000

Press Ctrl+C to exit.

```

--------------------------------

### Set Tailscale Serve Service Configuration

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

Applies a configuration from a file to one or all services hosted by the node. This command declares the desired configuration for services. Use `--all` to apply to all services or `--service=<name>` for a specific one.

```bash
tailscale serve set-config <file> [--all | --service=<name>]
```

--------------------------------

### Serve Files with Tailscale Funnel (Windows)

Source: https://tailscale.com/docs/reference/examples/funnel

This command uses Tailscale Funnel to expose a local directory containing files to the public internet over HTTPS on Windows. It should be run from an Administrator command prompt.

```bash
c:\Users\Amelie> tailscale funnel c:\tmp\public
```

--------------------------------

### Example JWT with Nested Claims

Source: https://tailscale.com/docs/features/workload-identity-federation?tab=github+actions

This example demonstrates a JWT containing nested claims, specifically within the 'user' field. It shows how to access nested claim values like 'name' using dot notation in configurations.

```json
{
	"sub": "123456-example",
	"iss": "https://example.com",
	"aud": "api.tailscale.com/12345-67890",
	"user": "example",
	"user": {
		"name": "foobar"
	}
}

```

--------------------------------

### Initialize Git Repository and Add Remote

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

Initializes a Git repository in the current directory and adds a remote origin pointing to a GitHub repository. This prepares the project for version control and deployment.

```bash
git init
git remote add origin https://github.com/<username>/<repository-name>.git
git commit -m "Init tshello app"
git push -u origin main
```

--------------------------------

### Bootstrap script for Tailscale and application startup

Source: https://tailscale.com/docs/install/cloud/aws/aws-app-runner

This script initializes the Tailscale daemon in userspace networking mode, configures a SOCKS5 proxy, and then starts the main application. It uses the TAILSCALE_AUTHKEY environment variable for authentication and sets ALL_PROXY to route traffic through the Tailscale SOCKS5 proxy.

```shell
#!/bin/sh

mkdir -p /tmp/tailscale
/var/runtime/tailscaled --tun=userspace-networking --socks5-server=localhost:1055 & 
/var/runtime/tailscale up --auth-key=${TAILSCALE_AUTHKEY} --hostname=aws-apprunner-app
echo Tailscale started
ALL_PROXY=socks5://localhost:1055/ /var/runtime/my-app

```

--------------------------------

### Add Tailscale Repository and Key (RPM/Shell)

Source: https://tailscale.com/docs/install/opensuse/opensuse-leap-15-1

Adds Tailscale's package signing key and repository configuration to the openSUSE Leap 15.1 system using rpm and zypper commands. This is a prerequisite for installing Tailscale via the package manager.

```shell
sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/leap/15.1/repo.gpg
sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/leap/15.1/tailscale.repo
```

--------------------------------

### Configure Tailscale via CloudFormation ExtraArgs

Source: https://tailscale.com/docs/install/cloud/aws/quickstart

Specifies optional arguments for Tailscale installation using AWS CloudFormation. These arguments enable advanced features such as Tailscale SSH and advertising routes for subnet routers.

```bash
--ssh
```

```bash
--advertise-routes=192.0.1.0/24
```

```bash
--ssh --advertise-routes=192.0.1.0/24
```

--------------------------------

### Allow Access to Environments by Group with Port Restrictions

Source: https://tailscale.com/docs/reference/examples/grants

This example implements group-based access control with port restrictions for shared resources. It provides precise control over which protocols and ports each group can use, balancing accessibility with security, commonly used for internal tools accessed by different teams.

```json
{
  "grants": [
    {
      "src": ["group:eng"],
      "dst": ["tag:internal-tools"],
      "ip": ["*"]
    },
    {
      "src": ["group:sales"],
      "dst": ["tag:internal-tools"],
      "ip": ["tcp:443", "tcp:22"]
    },
    {
      "src": ["*"],
      "dst": ["tag:dns"],
      "ip": ["udp:53"]
    }
  ]
}
```

--------------------------------

### Build and Run the tsnet Application Locally

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

Compiles the Go application into an executable named 'tshello' and then runs it, specifying the server address. This step tests the local compilation and execution of the tsnet app.

```bash
go build -o tshello
./tshello -addr tshello
```

--------------------------------

### Automate Tailscale Status Data Collection with jq

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

An example demonstrating how to use `tailscale status --json` combined with `jq` to count and sort relay servers connected by Tailscale peers. This showcases practical automation for network data analysis.

```bash
tailscale status --json | jq -r '.Peer[].Relay | select(.!="")' | sort | uniq -c | sort -nr
```

--------------------------------

### Update Tailscale on OPNsense

Source: https://tailscale.com/docs/install/opnsense

Procedure to update the Tailscale installation on OPNsense. This involves updating the ports tree, de-installing the current version, cleaning up, installing the new version, and restarting the service.

```shell
# opnsense-code ports
# cd /usr/ports/security/tailscale
# make deinstall
# make clean
# make install
# service tailscaled restart

```

--------------------------------

### Add Tailscale repository and GPG key on Raspberry Pi

Source: https://tailscale.com/docs/install/rpi

Adds Tailscale's official package signing key and repository to your Raspberry Pi's APT sources. This allows your system to securely download and install Tailscale packages.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/buster.gpg | sudo apt-key add -
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/buster.list | sudo tee /etc/apt/sources.list.d/tailscale.list

```

--------------------------------

### Build 'tshello' Application in GitHub Actions

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This step executes commands within the GitHub Actions runner to build the 'tshello' application. It navigates to the 'tshello' directory, downloads Go module dependencies, and then compiles the application using 'go build'.

```yaml
- name: Build tshello
  run: |
    cd tshello
    go mod download
    go build -v ./...
```

--------------------------------

### Configure Application Peering with Tailscale Tags

Source: https://tailscale.com/docs/reference/examples/grants

This example configures bidirectional peer-to-peer connections between applications across different cloud providers and SaaS applications. It uses Tailscale tags to define sources and destinations for communication, allowing infrastructure teams to manage access based on device function and environment.

```json
{
  "groups": {
    "group:infra": ["carl@example.com"]
  },
  "grants": [
    {
      "src": ["tag:database", "tag:gcp", "tag:aws"],
      "dst": ["tag:database"],
      "ip": ["*"]
    }
  ],
  "tagOwners": {
    "tag:database": ["group:infra"],
    "tag:gcp": ["group:infra"],
    "tag:aws": ["group:infra"]
  }
}
```

--------------------------------

### Set Up Tailscale API Environment Variables

Source: https://tailscale.com/docs/features/logging/network-flow-logs

This snippet shows how to set the necessary environment variables for making authenticated API calls to Tailscale. These include the access token, tailnet ID, and the start and end times for log retrieval.

```shell
export ACCESS_TOKEN=tskey-api-k123456CNTRL-0123456789abcdef
export TAILNET_ID=example.com
export START=2022-10-28T22:40:00.000000000Z
export END=2022-10-28T22:40:04.999999999Z

```

--------------------------------

### Add Tailscale Repository and Key on Ubuntu

Source: https://tailscale.com/docs/install/ubuntu/ubuntu-2110

This snippet adds Tailscale's package signing key and repository to your Ubuntu system. It uses curl to fetch the necessary files and pipes them to the appropriate locations for apt to use. Ensure you have curl installed.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/impish.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/impish.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Example JWT with Escaped Claim Names

Source: https://tailscale.com/docs/features/workload-identity-federation?tab=github+actions

This example shows a JWT where a claim name contains a period ('open.id'). It illustrates how to correctly reference such claims, including nested ones, by enclosing the key in double quotes.

```json
{
	"sub": "123456-example",
	"iss": "https://example.com",
	"aud": "api.tailscale.com/12345-67890",
	"user": "example",
	"open.id": {
		"username": "foobar"
	}
}

```

--------------------------------

### Add Tailscale Repository on openSUSE

Source: https://tailscale.com/docs/install/opensuse/opensuse-leap-16.0

This snippet adds Tailscale's package signing key and repository to the openSUSE Leap 16.0 system. It uses `rpm` to import the key and `zypper` to add the repository configuration. This is a prerequisite for installing Tailscale using the package manager.

```bash
sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/leap/16.0/repo.gpg
sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/leap/16.0/tailscale.repo
```

--------------------------------

### Add Tailscale Repository on openSUSE Leap

Source: https://tailscale.com/docs/install/opensuse/opensuse-leap-15-5

Adds Tailscale's package signing key and repository to the system for openSUSE Leap 15.5. This is a prerequisite for installing Tailscale using zypper. It involves importing a GPG key and adding a zypper repository URL.

```shell
sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/leap/15.5/repo.gpg
sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/leap/15.5/tailscale.repo
```

--------------------------------

### Serve Static Site with Tailscale

Source: https://tailscale.com/docs/reference/examples/serve

Serves static HTML and CSS files from a local directory to your Tailscale network. This allows other devices on your tailnet to access the site via a generated HTTPS URL. Ensure the directory exists and contains your website's assets.

```Shell
sudo tailscale serve /tmp/static-site
```

--------------------------------

### Run Tailscale CLI from macOS App Bundle

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=macos

Command to execute the Tailscale CLI when the macOS client is installed via the App Store. The CLI is bundled within the application executable.

```bash
/Applications/Tailscale.app/Contents/MacOS/Tailscale <command>
```

--------------------------------

### Download and Initialize Minecraft Bedrock Server with Git

Source: https://tailscale.com/docs/solutions/set-up-minecraft

This code block shows how to switch to the Minecraft user, download the latest Bedrock server binary, unzip it, remove the zip archive, and initialize a Git repository to track server file changes, particularly `permissions.json` and `server.properties`.

```bash
su -s -u minecraft
cd ~
wget "download path copied from https://www.minecraft.net/en-us/download/server/bedrock"
git init .
unzip bedrock_server*.zip
rm bedrock_server*.zip
git add -A
git commit -m "Initial bedrock_server"
```

--------------------------------

### Adjust Tailscale Access Rules with Posture Integration

Source: https://tailscale.com/docs/integrations/kolide

This example demonstrates how to adjust Tailscale access rules by incorporating device posture attributes from an integration like 1Password XAM (Kolide). It defines a posture rule to trust devices with a specific authentication state and then uses this posture in an access grant to control access to a production tag.

```json
{
  "postures": {
    "posture:trusted": [
      "kolide:authState != 'Blocked'"
    ]
  },
  "grants": [
    {
      "src": ["autogroup:member"],
      "dst": ["tag:production"],
      "ip": ["*"],
      "srcPosture": ["posture:trusted"]
    }
  ]
}
```

--------------------------------

### Test ICMP Access for Specific Tags

Source: https://tailscale.com/docs/reference/syntax/policy-file

This example tests ICMP access for a user `alice@example.com` to devices tagged with `tag:production`. It uses the `icmp` protocol and specifies port `0` for the destination.

```json
{
  "tests": [
    {
      "src": "alice@example.com",
      "proto": "icmp",
      "accept": ["tag:production:0"]
    }
  ]
}
```

--------------------------------

### Install Tailscale VPN Configuration Profile (.mobileconfig)

Source: https://tailscale.com/docs/integrations/mdm/mac

This Property List (.plist) file configures the Tailscale VPN connection on macOS before the app launches. It pre-empts the app's automatic VPN configuration step. Adjust the `VPNSubType` and `ProviderBundleIdentifier` if using the Standalone variant of Tailscale for macOS.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>PayloadDisplayName</key>
  <string>Tailscale VPN Configuration Profile</string>
  <key>PayloadType</key>
  <string>Configuration</string>
  <key>PayloadVersion</key>
  <integer>1</integer>
  <key>PayloadIdentifier</key>
  <string>com.your-company-name.tailscale.797d4461-837c-4f5a-b18e-7e300a057018</string>
  <key>PayloadUUID</key>
  <string>0f451881-7ac4-4171-80fd-b55251053231</string>
  <key>PayloadContent</key>
  <array>
        <dict>
        <key>PayloadDisplayName</key>
        <string>Tailscale VPN Configuration</string>
        <key>PayloadType</key>
        <string>com.apple.vpn.managed</string>
        <key>PayloadVersion</key>
        <integer>1</integer>
        <key>PayloadIdentifier</key>
        <string>com.your-company-name.tailscale-tunnel</string>
        <key>PayloadUUID</key>
        <string>7ec957e2-b165-4d1f-9946-3a7a16ae0f9b</string>
        <key>UserDefinedName</key>
        <string>Tailscale MobileConfig</string>
        <key>VPNType</key>
        <string>VPN</string>
        <key>VPNSubType</key>
        <string>io.tailscale.ipn.macos</string>
        <key>VPN</key>
         <dict>
            <key>RemoteAddress</key>
            <string>Tailscale Mesh</string>
            <key>AuthenticationMethod</key>
            <string>Password</string>
            <key>ProviderBundleIdentifier</key>
            <string>io.tailscale.ipn.macos.network-extension</string>
        </dict>
    </dict>
  </array>
</dict>
</plist>
```

--------------------------------

### Example: Configure HTTPS Web Server Endpoint

Source: https://tailscale.com/docs/reference/tailscale-services-configuration-file

An example of a Tailscale Service configuration file that sets up an endpoint for a local web server. It maps incoming TCP traffic on port 443 to an HTTPS service running on localhost:443.

```json
{
  "version": "0.0.1",
  "services": {
    "svc:web-server": {
      "endpoints": {
        "tcp:443": "https://localhost:443"
      }
    }
  }
}
```

--------------------------------

### Add Tailscale Repository on openSUSE Tumbleweed

Source: https://tailscale.com/docs/install/opensuse/opensuse-tumbleweed

This snippet adds Tailscale's package signing key and repository to your openSUSE Tumbleweed system. This is a prerequisite for installing Tailscale using the zypper package manager. It ensures that your system trusts the Tailscale packages.

```shell
sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/tumbleweed/repo.gpg
sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/tumbleweed/tailscale.repo
```

--------------------------------

### Tailscale Lock Status Example

Source: https://tailscale.com/docs/reference/tailscale-cli/lock

Demonstrates how to check the current status of Tailnet Lock, including whether it is enabled, the node's accessibility, its Tailnet Lock key, and a list of trusted signing keys.

```bash
tailscale lock

```

--------------------------------

### Add Tailscale Repository on openSUSE Leap 15.6

Source: https://tailscale.com/docs/install/opensuse/opensuse-leap-15-6

This snippet adds Tailscale's package signing key and repository to the openSUSE Leap 15.6 system. It uses `rpm` to import the GPG key and `zypper` to add the repository URL. This is a prerequisite for installing Tailscale using the package manager.

```shell
sudo rpm --import https://pkgs.tailscale.com/stable/opensuse/leap/15.6/repo.gpg
sudo zypper ar -g -r https://pkgs.tailscale.com/stable/opensuse/leap/15.6/tailscale.repo
```

--------------------------------

### Start Script for Tailscale on Azure App Service

Source: https://tailscale.com/docs/install/cloud/azure/azure-app-service

This shell script is used as the entry point for the Docker container on Azure App Service. It initializes SSH, starts the Tailscale daemon in userspace networking mode, and then launches the application, directing all traffic through Tailscale.

```shell
#!/bin/sh

/usr/bin/ssh-keygen -A
mkdir -p /var/run/sshd
/usr/sbin/sshd

/app/tailscaled --tun=userspace-networking --socks5-server=localhost:1055 &
/app/tailscale up --auth-key=${TAILSCALE_AUTHKEY} --hostname=azure-app
echo Tailscale started
ALL_PROXY=socks5://localhost:1055/ /app/my-app

```

--------------------------------

### Reference IP Sets in Grants

Source: https://tailscale.com/docs/features/tailnet-policy-file/ip-sets

Illustrates how to use IP sets within 'grants' to define network access rules. This example shows granting access to the 'ipset:dev' from specific source groups on particular ports, with an optional 'via' clause for routing.

```json
"grants": [
  {
    "src": ["group:devops"],
    "dst": ["ipset:dev"],
    "ip": ["80,443,22"]
  },
  {
    "src": ["group:dev"],
    "dst": ["ipset:dev"],
    "ip": ["80,443"],
    "via": ["tag:office-routers"],
  },
]
```

--------------------------------

### Serve Static Site with Tailscale Funnel (Linux/macOS)

Source: https://tailscale.com/docs/reference/examples/funnel

This command uses Tailscale Funnel to expose a local directory containing a static website to the public internet over HTTPS. It requires root privileges and will output the public URL.

```bash
sudo tailscale funnel /tmp/static-site
```

--------------------------------

### Set up TLS-Terminated TCP Forwarder with Tailscale Serve

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

Set up a TLS-terminated TCP forwarder using `tailscale serve` with the `--tls-terminated-tcp=<port>` flag. This forwards TLS-terminated TCP packets to the specified local port, allowing services like Caddy to handle TLS.

```bash
tailscale serve --tls-terminated-tcp=<port> tcp://localhost:<local-port> [off]
```

--------------------------------

### Add Tailscale Repository and Key (Bash)

Source: https://tailscale.com/docs/install/rpi/rpi-bookworm

Adds Tailscale's official package signing key and repository to your system's APT sources. This allows your system to fetch Tailscale packages.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/bookworm.asc | sudo apt-key add -
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/bookworm.list | sudo tee /etc/apt/sources.list.d/tailscale.list

```

--------------------------------

### Define Access Control Policy Tests

Source: https://tailscale.com/docs/reference/syntax/policy-file

This example demonstrates how to define tests for access control policies. It checks if a user `dave@example.com` with a Windows OS posture can access specific hosts and ports, while denying access to others.

```json
{
  "tests": [
    {
      "src": "dave@example.com",
      "srcPostureAttrs": {
        "node:os": "windows"
      },
      "proto": "tcp",
      "accept": ["example-host-1:22", "vega:80"],
      "deny": ["192.0.2.3:443"]
    }
  ]
}
```

--------------------------------

### Run 'tshello' Application Tests

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This step runs the test suite for the 'tshello' application within the GitHub Actions workflow. It navigates to the 'tshello' directory and executes 'go test' with verbose output and a 30-second timeout to ensure tests complete promptly and verify application functionality over the Tailscale network.

```yaml
- name: Run tests
  run: |
    cd tshello
    go test -v -timeout 30s ./...
```

--------------------------------

### Fortinet SSL Inspection Error Example

Source: https://tailscale.com/docs/integrations/firewalls

This example demonstrates a certificate verification error that may occur when FortiGate application control rules with SSL inspection interfere with Tailscale's control plane connections. This error indicates that the firewall is intercepting and not trusting HTTPS connections to the Tailscale control plane.

```text
fetch control key: Get "https://controlplane.tailscale.com/key?v=123": x509: "controlplane.tailscale.com" certificate is not trusted
```

--------------------------------

### Register Node with Client ID and Optional Parameters

Source: https://tailscale.com/docs/features/workload-identity-federation

This snippet demonstrates registering a node with Tailscale using `tailscale up`, including optional URL-style parameters for `--client-id`. These parameters control ephemeral node registration and preauthorization.

```shell
tailscale up --client-id='${CLIENT_ID}?ephemeral=false&preauthorized=true' --id-token=${IDENTITY_TOKEN} --advertise-tags=tag:ci
```

--------------------------------

### Verify File Server Access with Curl

Source: https://tailscale.com/docs/reference/examples/funnel

These curl commands demonstrate how to access the files served by Tailscale Funnel. The first command retrieves the directory listing, and the second retrieves a specific file.

```bash
curl -L https://amelie-workstation.pango-lin.ts.net
curl -L https://amelie-workstation.pango-lin.ts.net/animal.txt
```

--------------------------------

### Add Tailscale Package Signing Key and Repository (Debian)

Source: https://tailscale.com/docs/install/debian/debian-sid

This snippet adds Tailscale's package signing key and repository to your Debian system. It uses curl to download the necessary files and pipes them to tee for saving in the appropriate locations. Ensure curl is installed before running these commands.

```shell
curl -fsSL https://pkgs.tailscale.com/stable/debian/sid.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/debian/sid.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Add Tailscale Repository and Key on Ubuntu

Source: https://tailscale.com/docs/install/ubuntu/ubuntu-2210

This snippet adds Tailscale's package signing key and repository to the system's sources. It uses curl to download the necessary files and pipes them to tee for saving to the appropriate locations. No specific input is required, and the output is the successful addition of the repository.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/kinetic.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/kinetic.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Install Tailscale CLI on Azure Windows VM

Source: https://tailscale.com/docs/install/cloud/azure/windows

This snippet shows how to install the Tailscale client on a Windows VM in Azure using the command line and an authentication key. It configures Tailscale to not override DNS settings, allowing Azure to manage them.

```bash
tailscale up --accept-dns=false --auth-key=tskey-0123456789abcdef
```

--------------------------------

### Custom Application API Request Example (OpenAI Chat Completions)

Source: https://tailscale.com/docs/features/aperture

Demonstrates how to configure a custom application to use Aperture as an API gateway for OpenAI's chat completions endpoint. The request is sent to Aperture's base URL, which then routes it to the appropriate provider based on the model specified.

```http
POST http://ai/v1/chat/completions
Content-Type: application/json

{
  "model": "gpt-4o",
  "messages": [{"role": "user", "content": "Hello"}]
}
```

--------------------------------

### Configure Dockerfile for Tailscale on Fly.io

Source: https://tailscale.com/docs/install/cloud/flydotio

This Dockerfile uses a multi-stage build to create a production image for a Fly.io application. It copies application code from a builder stage and installs Tailscale binaries from the official Tailscale Docker image.

```dockerfile
FROM alpine:latest as builder
WORKDIR /app
COPY . ./ 
# This is where one could build the application code as well.

# https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds
FROM alpine:latest
RUN apk update && apk add ca-certificates iptables ip6tables && rm -rf /var/cache/apk/*

# Copy binary to production image.
COPY --from=builder /app/start.sh /app/start.sh

# Copy Tailscale binaries from the tailscale image on Docker Hub.
COPY --from=docker.io/tailscale/tailscale:stable /usr/local/bin/tailscaled /app/tailscaled
COPY --from=docker.io/tailscale/tailscale:stable /usr/local/bin/tailscale /app/tailscale
RUN mkdir -p /var/run/tailscale /var/cache/tailscale /var/lib/tailscale

# Run on container startup.
CMD ["/app/start.sh"]
```

--------------------------------

### Run API Integration Tests with Tailscale

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This example shows how to execute API integration tests against internal services not exposed to the internet, using Tailscale. It sets the API_BASE_URL environment variable to a staging API endpoint on the tailnet and runs npm integration tests. This ensures staging environments remain private yet accessible for automated testing with production-like network access.

```yaml
- name: Run API integration tests
  run: |
    export API_BASE_URL="https://staging-api.tail-scale.ts.net"
    npm test:integration

```

--------------------------------

### Share Files with Tailscale Serve (Windows)

Source: https://tailscale.com/docs/reference/examples/serve

This command uses Tailscale Serve to share the contents of the `c:\tmp\public` directory as a file server accessible within your tailnet. It is intended for Windows users and should be run from an Administrator console without `sudo`.

```bash
c:\Users\Amelie> tailscale serve c:\tmp\public
```

--------------------------------

### Connect to Minecraft server command line using mcrcon

Source: https://tailscale.com/docs/solutions/set-up-nixos-minecraft

This command demonstrates how to connect to a Minecraft server's command line interface using 'mcrcon'. Ensure you replace 'hunter2' with your actual RCON password if it has been changed.

```bash
mcrcon -p hunter2
```

--------------------------------

### Add Tailscale Repository and Key on Debian

Source: https://tailscale.com/docs/install/debian/debian-bookworm

This snippet adds Tailscale's package signing key and repository to your Debian system. It uses curl to download the necessary files and pipes them to the appropriate locations for package management. Ensure curl is installed before running these commands.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/debian/bookworm.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/debian/bookworm.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Advertise Service with Server.ListenService

Source: https://tailscale.com/docs/reference/tsnet-server-api

Creates a network listener for a Tailscale Service host, advertising this node as a service provider. Requires specific prerequisites like auto-approval and tagged nodes. Supports multiple ports and reverse proxy configurations. This method implicitly calls Start if not already invoked.

```go
srv := new(tsnet.Server)
srv.Hostname = "atum"

ln, err := srv.ListenService("svc:my-service", tsnet.ServiceModeHTTP{
    HTTPS: true,
    Port:  443,
})
if err != nil {
    log.Fatal(err)
}

log.Printf("Listening on https://%v\n", ln.FQDN)
log.Fatal(http.Serve(ln, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hi there! Welcome to the tailnet!")
})))

```

```go
// targetAddress represents the address of the backing server.
const targetAddress = "1.2.3.4:80"

srv := new(tsnet.Server)
srv.Hostname = "tefnut"

ln, err := srv.ListenService("svc:my-service", tsnet.ServiceModeHTTP{
    HTTPS: true,
    Port:  443,
})
if err != nil {
    log.Fatal(err)
}

log.Printf("Listening on https://%v\n", ln.FQDN)
log.Fatal(http.Serve(ln, httputil.NewSingleHostReverseProxy(&url.URL{
    Scheme: "http",
    Host:   targetAddress,
})))

```

--------------------------------

### Update Tailscale on Debian/Ubuntu

Source: https://tailscale.com/docs/features/client/update?tab=linux

This command sequence updates the package list and then installs the latest version of Tailscale on Debian and Ubuntu-based systems using apt-get.

```bash
sudo apt-get update
sudo apt-get install tailscale
```

--------------------------------

### Enable and Start systemd-resolved Service

Source: https://tailscale.com/docs/reference/messages/client/resolv-conf-overwritten

This command enables and starts the systemd-resolved service on Linux distributions that support it. This service is crucial for managing DNS settings and can help resolve conflicts that prevent Tailscale from configuring DNS correctly. Ensure you have sudo privileges to execute this command.

```bash
sudo systemctl enable --now systemd-resolved
```

--------------------------------

### Add Tailscale Repository and Key (Debian)

Source: https://tailscale.com/docs/install/debian/debian-bullseye

This snippet adds Tailscale's package signing key and repository to your Debian Bullseye system. It uses curl to download the necessary files and pipes them to tee for saving to the appropriate locations. Ensure curl is installed before running these commands.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/debian/bullseye.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/debian/bullseye.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Enable Randomize Client Port with Node Attributes

Source: https://tailscale.com/docs/reference/syntax/policy-file

This example shows how to use `nodeAttrs` to enable the `randomize-client-port` setting for specific devices. It targets devices in `tag:office-network` and `group:sea-office`.

```json
{
  "nodeAttrs": [
    {
      "target": ["tag:office-network", "group:sea-office"],
      "attr":   ["randomize-client-port"]
    }
  ]
}
```

--------------------------------

### Install Tailscale Operator with API Server Proxy (Helm)

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/api-server-proxy

Installs the Tailscale Kubernetes Operator using Helm, enabling the API server proxy in 'noauth' mode. Requires specifying OAuth client ID and secret.

```bash
helm upgrade \
  --install \
  tailscale-operator \
  tailscale/tailscale-operator \
  --namespace=tailscale \
  --create-namespace \
  --set-string oauth.clientId=<OAauth client ID> \
  --set-string oauth.clientSecret=<OAuth client secret> \
  --set-string apiServerProxyConfig.mode="noauth" \
  --wait

```

--------------------------------

### OpenAI Provider Configuration

Source: https://tailscale.com/docs/features/aperture/configuration

Configures the OpenAI provider, enabling support for both chat and responses APIs. This example specifies the base URL, an API key placeholder, a list of available models, and compatibility flags.

```json
{
  "providers": {
    "openai": {
      "baseurl": "https://api.openai.com/",
      "apikey": "YOUR_OPENAI_KEY",
      "models": ["gpt-5", "gpt-5-mini", "gpt-4.1"],
      "name": "OpenAI",
      "description": "OpenAI models",
      "compatibility": {
        "openai_chat": true,
        "openai_responses": true
      }
    }
  }
}
```

--------------------------------

### Add Tailscale Repository and Key (Bash)

Source: https://tailscale.com/docs/install/debian/debian-buster

This snippet adds Tailscale's package signing key and repository to your Debian Buster system using curl. It ensures that your system trusts the Tailscale package source before installation. No specific inputs are required, and the output is the configuration of your package manager.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/debian/buster.gpg | sudo apt-key add -
curl -fsSL https://pkgs.tailscale.com/stable/debian/buster.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Create Tailscale Service Listener with tsnet in Go

Source: https://tailscale.com/docs/features/tsnet/how-to/register-service

This Go program configures and starts a tsnet server to listen for HTTPS connections on a specified Tailscale Service. It uses the 'tailscale.com/tsnet' package to create a virtual node and the standard 'net/http' package to serve responses. The program requires a service name as a command-line argument and logs the Fully Qualified Domain Name (FQDN) for access.

```go
package main

import (
	"flag"
	"fmt"
	"log"
	"net/http"

	"tailscale.com/tsnet"
)

var (
	svcName = flag.String("service", "", "the name of your Service, e.g. svc:tsnet-demo")
)

func main() {
	flag.Parse()
	if *svcName == "" {
		log.Fatal("a Service name must be provided")
	}

	s := &tsnet.Server{
		Hostname: "tsnet-services-demo",
	}
	defer s.Close()

	ln, err := s.ListenService(*svcName, tsnet.ServiceModeHTTP{
		HTTPS: true,
		Port:  443,
	})
	if err != nil {
		log.Fatal(err)
	}
	defer ln.Close()

	log.Printf("Listening on https://%v\n", ln.FQDN)

	err = http.Serve(ln, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintln(w, "<html><body><h1>Hello, tailnet!</h1>")
	}))
	log.Fatal(err)
}

```

--------------------------------

### Add Tailscale Repository and Key (Bash)

Source: https://tailscale.com/docs/install/rpi/rpi-bullseye

Adds Tailscale's official package signing key and repository to the system's APT sources. This allows the system to securely fetch Tailscale packages.

```bash
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/bullseye.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg > /dev/null
curl -fsSL https://pkgs.tailscale.com/stable/raspbian/bullseye.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Connect Machine to Tailscale Network on CentOS 8

Source: https://tailscale.com/docs/install/centos/centos-8

This command initiates the connection process for your machine to your Tailscale network. It will typically open a browser window for authentication.

```bash
sudo tailscale up
```

--------------------------------

### Serve Files with Tailscale Funnel (Linux/macOS)

Source: https://tailscale.com/docs/reference/examples/funnel

This command uses Tailscale Funnel to expose a local directory containing files to the public internet over HTTPS. It requires root privileges and will output the public URL.

```bash
sudo tailscale funnel /tmp/public
```

--------------------------------

### Create directories for website files

Source: https://tailscale.com/docs/features/tailscale-funnel/how-to/host-websites

This command creates a temporary directory and a subdirectory within it. This structure is used to organize website files before serving them, ensuring a clean and accessible file path.

```bash
mkdir /tmp

```

```bash
mkdir /tmp/test-funnel

```

--------------------------------

### Add Account using Tailscale CLI

Source: https://tailscale.com/docs/features/client/fast-user-switching?tab=android

This command allows users to add a new account to their Tailscale client on Linux, macOS, or Windows. It opens a browser window for authentication. Ensure the Tailscale CLI is installed and configured.

```bash
tailscale login

```

--------------------------------

### Mount Taildrive Share using davfs2

Source: https://tailscale.com/docs/features/taildrive?tab=linux

Example command to mount a Taildrive share on a client machine using the davfs2 filesystem. It connects to the Tailscale IP and default port, mounting it to a local directory.

```bash
# sudo mount -t davfs http://100.100.100.100:8080 /mount/tailscale
```

--------------------------------

### Configure Motion for Web Streaming

Source: https://tailscale.com/docs/solutions/set-up-dogcam

Adjusts the motion configuration file to enable web streaming of the camera feed and disable saving images or videos to the SD card, optimizing it for live viewing.

```bash
sudo nano /etc/motion/motion.conf
```

```ini
stream_port 8081
stream_localhost off
output_pictures off
ffmpeg_output_movies off
```

--------------------------------

### Install Tailscale Kubernetes Operator with API Server Proxy (Helm)

Source: https://tailscale.com/docs/solutions/manage-multi-cluster-kubernetes-deployments-argocd

Installs the Tailscale Kubernetes Operator in a cluster using Helm, enabling the API server proxy for secure remote access. Requires OAuth credentials and a unique hostname for the cluster. The `apiServerProxyConfig.mode=true` flag is crucial for enabling this functionality.

```bash
helm upgrade --install tailscale-operator tailscale/tailscale-operator \
  --namespace=tailscale \
  --create-namespace \
  --set-string oauth.clientId=<YOUR_OAUTH_CLIENT_ID> \
  --set-string oauth.clientSecret=<YOUR_OAUTH_CLIENT_SECRET> \
  --set operatorConfig.hostname=cluster1-k8s-operator \
  --set apiServerProxyConfig.mode=true \
  --wait

```

```bash
helm upgrade --install tailscale-operator tailscale/tailscale-operator \
  --namespace=tailscale \
  --create-namespace \
  --set-string oauth.clientId=<YOUR_OAUTH_CLIENT_ID> \
  --set-string oauth.clientSecret=<YOUR_OAUTH_CLIENT_SECRET> \
  --set operatorConfig.hostname=cluster2-k8s-operator \
  --set apiServerProxyConfig.mode=true \
  --wait

```

--------------------------------

### GET /api/v2/tailnet/{tailnet_id}/logging/configuration

Source: https://tailscale.com/docs/features/logging/audit-logging

Retrieves configuration audit logs for a specified tailnet within a given timeframe. Requires an API access token with the `logs:configuration:read` scope.

```APIDOC
## GET /api/v2/tailnet/{tailnet_id}/logging/configuration

### Description
Retrieves configuration audit logs for a specified tailnet within a given timeframe. Requires an API access token with the `logs:configuration:read` scope.

### Method
GET

### Endpoint
`/api/v2/tailnet/{tailnet_id}/logging/configuration`

### Parameters
#### Path Parameters
- **tailnet_id** (string) - Required - The ID of the tailnet for which to retrieve logs.

#### Query Parameters
- **start** (string) - Required - The start of the timeframe, in RFC3339 timestamp format, for the logs to retrieve. Example: `2022-07-20T00:00:00Z`.
- **end** (string) - Required - The end of the timeframe, in RFC3339 timestamp format, for the logs to retrieve. Example: `2022-07-21T00:00:00Z`.

### Request Example
```bash
curl -u  $ACCESS_TOKEN:  -X GET \
  "https://api.tailscale.com/api/v2/tailnet/{$TAILNET_ID}/logging/configuration?start={$START}&end={$END}"
```

### Response
#### Success Response (200)
- **version** (string) - The API version.
- **tailnetId** (string) - The ID of the tailnet.
- **logs** (array) - An array of log entries, ordered chronologically.
  - **action** (string) - The action performed (e.g., "UPDATE", "CREATE").
  - **actor** (object) - Information about the actor who performed the action.
    - **displayName** (string) - The display name of the actor.
    - **id** (string) - The ID of the actor.
    - **loginName** (string) - The login name of the actor.
    - **type** (string) - The type of the actor (e.g., "USER").
  - **deferredAt** (string) - The timestamp when the action was deferred.
  - **eventGroupID** (string) - A unique identifier for a group of related events.
  - **eventTime** (string) - The timestamp when the event occurred.
  - **new** (any) - The new state of the configuration after the action.
  - **old** (any) - The previous state of the configuration before the action.
  - **origin** (string) - The origin of the event (e.g., "NODE", "ADMIN_UI").
  - **target** (object) - Information about the target of the action.
    - **id** (string) - The ID of the target.
    - **name** (string) - The name of the target.
    - **property** (string) - The specific property that was affected.
    - **type** (string) - The type of the target (e.g., "NODE", "API_KEY").
  - **type** (string) - The type of the log entry (e.g., "CONFIG").

#### Response Example
```json
{
	"logs": [
		{
			"action": "UPDATE",
			"actor": {
				"displayName": "Alice Architect",
				"id": "123456CNTRL",
				"loginName": "alice@example.com",
				"type": "USER"
			},
			"deferredAt": "0001-01-01T00:00:00Z",
			"eventGroupID": "12345",
			"eventTime": "2022-07-20T20:13:30.136022207Z",
			"new": "2023-01-14T20:13:30.134350003Z",
			"old": "0001-01-01T00:00:00Z",
			"origin": "NODE",
			"target": {
				"id": "654321CNTRL",
				"name": "node1.yak-bebop.ts.net",
				"property": "KEY_EXPIRY_TIME",
				"type": "NODE"
			},
			"type": "CONFIG"
		}
	],
	"tailnetId": "example.com",
	"version": "1.1"
}
```
```

--------------------------------

### Get Tailscale License Information

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Displays open source license information for the components used in Tailscale. This is important for compliance and understanding dependencies.

```bash
tailscale licenses
```

--------------------------------

### Configure Dockerfile for Tailscale on Cloud Run

Source: https://tailscale.com/docs/install/cloud/cloudrun

This Dockerfile uses a multistage build to create a production image for Google Cloud Run. It copies application code from a builder stage and installs Tailscale binaries from a stable Docker image. The final image includes the application and Tailscale, ready to run on startup.

```dockerfile
FROM golang:1.16.2-alpine3.13 as builder
WORKDIR /app
COPY . ./ 
# This is where one could build the application code as well.

FROM alpine:latest
RUN apk update && apk add ca-certificates && rm -rf /var/cache/apk/*

# Copy binary to production image.
COPY --from=builder /app/start.sh /app/start.sh

# Copy Tailscale binaries from the tailscale image on Docker Hub.
COPY --from=docker.io/tailscale/tailscale:stable /usr/local/bin/tailscaled /app/tailscaled
COPY --from=docker.io/tailscale/tailscale:stable /usr/local/bin/tailscale /app/tailscale
RUN mkdir -p /var/run/tailscale /var/cache/tailscale /var/lib/tailscale

# Run on container startup.
CMD ["/app/start.sh"]

```

--------------------------------

### Turn Off Tailscale Funnel Service

Source: https://tailscale.com/docs/reference/tailscale-cli/funnel

Disables a previously started Tailscale Funnel service. The `off` keyword is appended to the original command used to start the service. The target argument is optional in the `off` command.

```bash
tailscale funnel --https=443 /home/alice/blog/index.html off
```

```bash
tailscale funnel --https=443 --set-path=/foo off
```

--------------------------------

### Connect to Tailscale using OAuth Client in GitHub Actions

Source: https://tailscale.com/docs/integrations/github/github-action

This example shows how to use the Tailscale GitHub Action with an OAuth client for authentication. It requires creating GitHub repository secrets for the OAuth Client ID and Client Secret, and assigning tags to the ephemeral nodes.

```yaml
- name: Tailscale
  uses: tailscale/github-action@v4
  with:
    oauth-client-id: ${{ secrets.TS_OAUTH_CLIENT_ID }}
    oauth-secret: ${{ secrets.TS_OAUTH_SECRET }}
    tags: tag:ci

```

--------------------------------

### Commit and Push Tailscale Policy File using Git

Source: https://tailscale.com/docs/integrations/github/gitops

This snippet demonstrates the basic Git commands to add, commit, and push a policy file to a GitHub repository. It assumes the policy file has been created and added to the staging area.

```bash
git add .
git commit -sm "policy: import from admin console"
git push -u origin main

```

--------------------------------

### SSH Connection Example using MagicDNS

Source: https://tailscale.com/docs/how-to/connect-to-devices

Demonstrates how to establish an SSH connection to a device within your Tailscale tailnet using its MagicDNS name. This method simplifies remote access by abstracting away IP addresses. Ensure SSH is running on the target device and you have the correct username.

```bash
ssh username@dev-build-server
```

--------------------------------

### Get Ingress Information

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

Retrieves information about the deployed Ingress resources. This command is used to verify the hostname and status of the Ingress, including the generated MagicDNS name.

```bash
kubectl get ingress

```

--------------------------------

### Configure Synology for Tailscale Outbound Connections

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Enables Synology devices to make outbound connections required for Tailscale functionality. This command simplifies the setup process for Synology NAS devices.

```bash
tailscale configure synology
```

--------------------------------

### Get Tailscale Funnel Status

Source: https://tailscale.com/docs/reference/tailscale-cli/funnel

Retrieves the current status of Tailscale Funnel services. The `--json` flag can be used to get the status output in JSON format for programmatic parsing.

```bash
tailscale funnel status [--json]
```

```bash
tailscale funnel status --json
```

--------------------------------

### Bootstrap Script for Tailscale and Application Startup

Source: https://tailscale.com/docs/install/cloud/aws/aws-lightsail

This shell script is executed on container startup. It initializes Tailscale in userspace networking mode, starts the Tailscale daemon, and then launches the application using SOCKS5 proxying. The TAILSCALE_AUTHKEY environment variable is used for authentication.

```sh
#!/bin/sh

mkdir -p /tmp/tailscale
/var/runtime/tailscaled --tun=userspace-networking --socks5-server=localhost:1055 & 
/var/runtime/tailscale up --auth-key=${TAILSCALE_AUTHKEY} --hostname=aws-lightsail-app
echo Tailscale started
ALL_PROXY=socks5://localhost:1055/ /var/runtime/my-app

```

--------------------------------

### Configure Aperture with Anthropic Models (JSON)

Source: https://tailscale.com/docs/features/aperture

A minimal JSON configuration file example for Aperture, setting up access to Anthropic's Claude Sonnet 4.5 and Claude Opus 4.5 models. This configuration specifies the provider, base URL, supported models, and authorization method.

```json
{
  "providers": {
    "anthropic": {
      "baseurl": "https://api.anthropic.com",
      "models": [
        "claude-sonnet-4-5",
        "claude-opus-4-5"
      ],
      "authorization": "x-api-key",
      "compatibility": {
        "anthropic_messages": true
      }
    }
  }
}
```

--------------------------------

### Update Raspberry Pi OS Packages

Source: https://tailscale.com/docs/solutions/block-ads-all-devices-anywhere-using-raspberry-pi

Updates the package list and upgrades installed packages on a Raspberry Pi. This is a standard maintenance step to ensure the system has the latest security patches and software versions before installing new applications.

```bash
sudo apt update
sudo apt upgrade -y
```

--------------------------------

### Authenticate and Connect to Tailscale Network

Source: https://tailscale.com/docs/how-to/secure-ubuntu-server-with-ufw

After installing Tailscale, authenticate and connect your Ubuntu server to your Tailscale network (tailnet). This command initiates the connection process and requires user interaction for authentication.

```bash
sudo tailscale up

```

--------------------------------

### Tailscale SSH Policy with Custom Check Period and User Restrictions

Source: https://tailscale.com/docs/features/tailscale-ssh

This example shows a more complex Tailscale SSH policy configuration. It includes a rule to accept SSH connections to self-owned devices for non-root users and a separate rule requiring check mode for specific external connections (`tag:prod`) with a defined `checkPeriod` of 1 hour. This illustrates how to manage different access levels and security requirements within the same policy.

```json
{
  "grants": [
    {
      "src": ["*" ],
      "dst": ["*"],
      "ip": ["*" ]
    }
  ],
  "ssh": [
    {
      "action": "accept",
      "dst": ["autogroup:self"],
      "src": ["alice@example.com"],
      "users": ["autogroup:nonroot"]
    },
    {
      "action": "check",
      "checkPeriod": "1h",
      "dst": ["tag:prod"],
      "src": ["alice@example.com"],
      "users": ["root"]
    }
  ]
}
```

--------------------------------

### Restart Motion Service

Source: https://tailscale.com/docs/solutions/set-up-dogcam

Restarts the Motion service to apply the latest configuration changes, ensuring the camera stream is accessible.

```bash
sudo service motion restart
```

--------------------------------

### Configure Tailscale System Policies with `defaults` CLI (Standalone)

Source: https://tailscale.com/docs/integrations/mdm/mac

These `defaults` CLI commands configure Tailscale system policies for the Standalone variant by specifying the explicit Property List (.plist) path. They set the organization name and suppress the IP address copied alert. These commands can be used to test MDM configurations without a full MDM setup.

```bash
defaults write ~/Library/Preferences/io.tailscale.ipn.macsys.plist ManagedByOrganizationName "Tailscale, Inc."
defaults write ~/Library/Preferences/io.tailscale.ipn.macsys.plist IPAddressCopiedAlertSuppressed -bool true

```

--------------------------------

### Configure Service Host using JSON Configuration File

Source: https://tailscale.com/docs/features/tailscale-services

Configures a Tailscale service host by applying a JSON configuration file. This method involves creating a JSON file with service and endpoint definitions, then using `tailscale serve set-config` to apply it. Finally, the service is advertised.

```json
{
"version": "0.0.1",
  "services": {
    "svc:web-server": {
      "endpoints": {
        "tcp:443": "https://localhost:443"
      }
    }
  }
}
```

```bash
tailscale serve set-config --all serveconfig.json
tailscale serve get-config --all
tailscale serve advertise svc:<service-name>
```

--------------------------------

### Verify Client Traffic to Custom DERP Server

Source: https://tailscale.com/docs/reference/derp-servers/custom-derp-servers

This command starts the `derper` process with the `--verify-clients` flag. This ensures that only traffic originating from your tailnet is routed through your custom DERP server, enhancing security and preventing unauthorized usage.

```bash
sudo derper --hostname=example.com --verify-clients
```

--------------------------------

### Configure Tailscale Serve as a Static Text Server

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

Configure a static plain-text server by specifying `text:<value>` as the `<target>` for the `tailscale serve` command. This is primarily useful for debugging purposes.

```bash
tailscale serve text:"Hello, world!"
```

--------------------------------

### Export Auth Key for Tailscale Lock

Source: https://tailscale.com/docs/features/tailnet-lock?tab=ios

Sets the `AUTH_KEY` environment variable to a pre-signed auth key. This is the first step in adding devices to a locked tailnet using pre-signed keys. Ensure you replace the example key with your actual auth key.

```bash
export AUTH_KEY="tskey-auth-<XXXXCTRL-NNNNNN>"
```

--------------------------------

### Create Tailscale ProxyGroup for Ingress

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Defines a `ProxyGroup` resource with `spec.type` set to `ingress`. This is a prerequisite for exposing Tailscale Ingress resources. It requires the Kubernetes API and the Tailscale operator to be installed.

```yaml
apiVersion: tailscale.com/v1alpha1
kind: ProxyGroup
metadata:
  name: ingress-proxies
spec:
  type: ingress

```

--------------------------------

### Tailscale ACL Policy with Okta Group Sync

Source: https://tailscale.com/docs/integrations/identity/okta/okta-scim

Example of a Tailscale ACL policy file demonstrating how to reference groups synced from Okta using their email addresses. This allows for human-readable group names in policy definitions.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": ["group:groupname@example.com"],
      "dst": ["*:*"]
    },
    {
      "action": "accept",
      "src": ["group:all employees@example.com"],
      "dst": ["autogroup:self:*"]
    },
    {
      "action": "accept",
      "src": ["group:engineering@example.com"],
      "dst": ["tag:logging:*"]
    }
  ]
}
```

--------------------------------

### Update Tailscale to Unstable Track (Linux, Windows, macOS)

Source: https://tailscale.com/docs/install/unstable?tab=tailscale+cli

This command updates the Tailscale client to the unstable release track on Linux, Windows, and macOS. It allows users to test new features and fixes before they are released to the general public. Ensure you have the Tailscale CLI installed and are running it with appropriate permissions.

```bash
tailscale update --track=unstable

```

--------------------------------

### Get Tailscale Ingress Details

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Retrieves details about a Kubernetes `Ingress` resource, including its class, hosts, address, and ports. This is useful for verifying the Ingress configuration and obtaining the tailnet DNS name.

```bash
kubectl get ingress nginx
```

--------------------------------

### Set Posture Attribute with Comment (JSON)

Source: https://tailscale.com/docs/features/tailscale-accessbot-jit

This JSON example illustrates setting a posture attribute's value, expiry, and an optional comment. The 'comment' field provides a reason for setting the attribute, aiding in auditing and understanding.

```json
{
  "value": "foo",
  "expiry": "2024-04-23T18:25:43.511Z",
  "comment": "access needed to inspect logs on prod vm"
}
```

--------------------------------

### Install Tailscale Kubernetes Operator with API Server Proxy in Auth Mode (Helm)

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/api-server-proxy

Installs or upgrades the Tailscale Kubernetes Operator using Helm, enabling the API server proxy in authentication mode. Requires OAuth client ID and secret. The `--wait` flag ensures the command waits for resources to be ready.

```bash
helm upgrade \
  --install \
  tailscale-operator \
  tailscale/tailscale-operator \
  --namespace=tailscale \
  --create-namespace \
  --set-string oauth.clientId=<OAauthClientId> \
  --set-string oauth.clientSecret=<OAuthClientSecret> \
  --set-string apiServerProxyConfig.mode="true" \
  --wait

```

--------------------------------

### Share Files with Tailscale Serve (Linux/macOS)

Source: https://tailscale.com/docs/reference/examples/serve

This command uses Tailscale Serve to share the contents of the `/tmp/public` directory as a file server accessible within your tailnet. It displays the available URL and indicates that the server runs in the foreground, stopping when the session ends. Requires `sudo` on Linux.

```bash
sudo tailscale serve /tmp/public
```

--------------------------------

### Connect to Rebound SSH Service

Source: https://tailscale.com/docs/reference/examples/serve

Connects to a local SSH server that has been rebound to a different port using `tailscale serve`. This command allows you to specify the new port and the Tailscale IP address of the target device.

```Shell
ssh -p 2222 <user>@100.x.y.z
```

--------------------------------

### Manage Tailscale Funnel Status and Reset

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=bash

Manages the status and configuration of Tailscale Funnel. Use `status` to get current settings and `reset` to revert to defaults.

```bash
tailscale funnel status
tailscale funnel reset
```

--------------------------------

### Kubernetes Access Control with Session Recording (Tailscale Policy)

Source: https://tailscale.com/docs/features/access-control/grants/grants-app-capabilities

Sets up secure access to Kubernetes clusters using the `tailscale.com/cap/kubernetes` capability. This example configures session recording and enforces its availability for audit purposes.

```json
{
  "grants": [
    {
      "src": ["group:devops"],
      "dst": ["tag:k8s-cluster"],
      "app": {
        "tailscale.com/cap/kubernetes": [
          {
            "recorders": ["tag:k8s-recorder"],
            "enforceRecorder": true,
            "impersonate": {
              "groups": ["system:masters"]
            }
          }
        ]
      }
    }
  ]
}
```

--------------------------------

### GET /api/v2/tailnet/{$TAILNET_ID}/logging/network

Source: https://tailscale.com/docs/features/logging/network-flow-logs

Retrieves network logs for a specified Tailnet. Requires an API access token with the `logs:network:read` scope.

```APIDOC
## GET /api/v2/tailnet/{$TAILNET_ID}/logging/network

### Description
Retrieves network logs for a specified Tailnet. This endpoint provides detailed insights into network traffic, including virtual, subnet, and exit node traffic.

### Method
GET

### Endpoint
`/api/v2/tailnet/{$TAILNET_ID}/logging/network`

### Parameters
#### Path Parameters
- **TAILNET_ID** (string) - Required - The unique identifier of the Tailnet for which to retrieve logs.

#### Query Parameters
- **start** (string) - Optional - The start of the time range for logs (RFC3339 format).
- **end** (string) - Optional - The end of the time range for logs (RFC3339 format).

### Request Example
```bash
curl -H "Authorization: Bearer YOUR_API_TOKEN" \
     "https://api.tailscale.com/api/v2/tailnet/YOUR_TAILNET_ID/logging/network?start=2023-01-01T00:00:00Z&end=2023-01-01T01:00:00Z"
```

### Response
#### Success Response (200)
- **logs** (array) - An array of `Message` objects, each representing a network log entry.

```json
{
  "logs": [
    {
      "nodeId": "n123456CNTRL",
      "logged": "2023-01-01T00:05:00Z",
      "start": "2023-01-01T00:04:55Z",
      "end": "2023-01-01T00:05:00Z",
      "srcNode": {
        "nodeId": "n123456CNTRL",
        "name": "carbonite.example.ts.net",
        "addresses": ["100.12.34.56", "fd7a:115c:a1e0::0123:4567"]
      },
      "dstNodes": [
        {
          "nodeId": "n789012CTRL",
          "name": "server.example.ts.net",
          "addresses": ["100.65.43.21"]
        }
      ],
      "virtualTraffic": [
        {
          "proto": 6,
          "src": "100.12.34.56:12345",
          "dst": "100.65.43.21:80",
          "txPkts": 100,
          "txBytes": 10000,
          "rxPkts": 50,
          "rxBytes": 5000
        }
      ],
      "subnetTraffic": [],
      "exitTraffic": [],
      "physicalTraffic": []
    }
  ]
}
```

#### Error Response (401)
- **message** (string) - Unauthorized. Missing or invalid API token.

#### Error Response (403)
- **message** (string) - Forbidden. Insufficient permissions for the API token.

#### Error Response (404)
- **message** (string) - Not Found. The specified Tailnet ID does not exist.
```

--------------------------------

### Create IAM Policy for S3 Access

Source: https://tailscale.com/docs/features/tailscale-ssh/how-to/session-recording-s3

This JSON policy grants necessary permissions for Tailscale SSH session recorders to interact with an S3 bucket. It allows putting and getting objects, and getting bucket location. Ensure you replace `<bucket-name>` with your actual bucket name.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:PutObject",
        "s3:GetBucketLocation",
        "s3:GetObject",
        "s3:ListBucket"
      ],
      "Resource": [
        "arn:aws:s3:::<bucket-name>/*",
        "arn:aws:s3:::<bucket-name>"
      ]
    }
  ]
}
```

--------------------------------

### Define Custom Groups and Access Rules in Tailscale ACLs

Source: https://tailscale.com/docs/reference/examples/acls

This example demonstrates how to define custom user groups (e.g., Engineering, DevOps) and specify access rules for devices tagged with specific tags. It uses JSON format for ACL configuration.

```json
{
  "groups": {
    "group:engineering": [
      "alice@example.com",
      "bob@example.com"
    ],
    "group:devops": [
      "amelie@example.com",
      "carl@example.com"
    ]
  },
  "acls": [
    {
      "action": "accept",
      "src": [
        "group:engineering"
      ],
      "dst": [
        "tag:frontend:*",
        "tag:backend:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "group:devops"
      ],
      "dst": [
        "tag:frontend:*",
        "tag:backend:*",
        "tag:logging:*"
      ]
    }
  ]
}
```

--------------------------------

### Get HTTP Client from Server (Go)

Source: https://tailscale.com/docs/features/tsnet/how-to/create-basic-tsnet-app

Retrieves an HTTP client configured to use the Tailscale network from a tsnet.Server instance. This client can be used for making outgoing HTTP requests within the tailnet.

```go
httpCli := srv.HTTPClient()
```

--------------------------------

### Restrict Tailscale Access Based on Individual Users

Source: https://tailscale.com/docs/reference/examples/acls

This example demonstrates how to grant access to devices based on individual user email addresses. It allows for fine-grained control over who can access specific resources tagged within the Tailscale network.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": [
        "amelie@example.com"
      ],
      "dst": [
        "tag:frontend:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "bob@example.com"
      ],
      "dst": [
        "tag:backend:*"
      ]
    }
  ]
}
```

--------------------------------

### Apply ProxyClass to Tailscale Ingress

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/customize

This example shows how to annotate a Tailscale Ingress resource with `tailscale.com/proxy-class=prod` to apply the configurations defined in the 'prod' ProxyClass.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app
  annotations:
    tailscale.com/proxy-class: "prod"
spec:
  rules:
  ...
  ingressClassName: tailscale
```

--------------------------------

### Configure Unraid as Tailscale Subnet Router

Source: https://tailscale.com/docs/integrations/unraid

Advertise specific subnet routes from your Unraid server to your Tailscale network. This allows access to devices on your physical network that are not directly on the tailnet. Ensure your Unraid server has Tailscale installed and configured.

```bash
tailscale up --advertise-routes=192.0.2.0/24

```

```bash
tailscale up --advertise-routes=192.168.1.0/24,198.160.50.0/24

```

--------------------------------

### Enable Tailscale Service on NixOS

Source: https://tailscale.com/docs/install/nixos

This code snippet enables the Tailscale service within the NixOS configuration. After adding this line to your configuration.nix file, you need to apply the changes for Tailscale to be activated.

```nix
services.tailscale.enable = true;
```

--------------------------------

### Manage macOS VPN Configuration

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=zsh

Installs or uninstalls the Tailscale VPN configuration on macOS. This command is used for both App Store and Standalone variants of macOS to manage the VPN settings.

```bash
tailscale configure mac-vpn install
tailscale configure mac-vpn uninstall
```

--------------------------------

### Go tsnet Application: Main Function and Server Initialization

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

Initializes the tsnet server, creates a TCP listener, and obtains a local client for Tailscale network interaction. It handles potential errors during initialization and ensures resources are closed.

```go
func main() {
    flag.Parse()
    srv := new(tsnet.Server)
    defer srv.Close()
    ln, err := srv.Listen("tcp", *addr)
    if err != nil {
       log.Fatal(err)
    }
    defer ln.Close()

    lc, err := srv.LocalClient()
    if err != nil {
     log.Fatal(err)
    }

```

--------------------------------

### Tailscale SSH Rule: User to Own Devices (Non-Root)

Source: https://tailscale.com/docs/features/tailscale-ssh

An example SSH access rule that allows any tailnet member to SSH into their own devices, but only as a non-root user. This enhances security by restricting root access.

```json
{
  "grants": [
    {
      "src": ["*"],
      "dst": ["*"],
      "ip": ["*"]
    }
  ],
  "ssh": [
    {
      "action": "accept",
      "dst": ["autogroup:self"],
      "src": ["autogroup:member"],
      "users": ["autogroup:nonroot"]
    }
  ]
}
```

--------------------------------

### Install Tailscale Kubernetes Operator for High Availability API Server Proxy (Helm)

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/api-server-proxy

Installs or upgrades the Tailscale Kubernetes Operator using Helm, configuring it for a highly available API server proxy with impersonation enabled. This allows for reduced permissions for the operator's service account. Requires OAuth client ID and secret.

```bash
helm upgrade \
  --install \
  tailscale-operator \
  tailscale/tailscale-operator \
  --namespace=tailscale \
  --create-namespace \
  --set-string oauth.clientId=<OAauthClientId> \
  --set-string oauth.clientSecret=<OAuthClientSecret> \
  --set-string apiServerProxyConfig.allowImpersonation="true" \
  --wait

```

--------------------------------

### Tailscale Bug Report Identifier Example

Source: https://tailscale.com/docs/account/bug-report?tab=tvos

An example of a Tailscale bug report identifier. This identifier is used to mark a specific section of diagnostic logs for easier troubleshooting by the Tailscale support team. It contains no personally-identifiable information.

```text
BUG-1b7641a16971a9cd75822c0ed8043fee70ae88cf05c52981dc220eb96a5c49a8-20210427151443Z-fbcd4fd3a4b7ad94
```

--------------------------------

### Connecting Device to Tailscale (Basic)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=windows

The 'tailscale up' command connects your device to the Tailscale network. Running it without any flags initiates a standard connection, prompting for authentication if necessary.

```bash
tailscale up

```

--------------------------------

### Advertise SSH on Host with Tailscale CLI

Source: https://tailscale.com/docs/features/tailscale-ssh

This command initializes Tailscale SSH on a host, generating keys and configuring the daemon to manage SSH connections from the Tailscale network. It only needs to be run once per host. Existing SSH connections will hang after running this command.

```bash
tailscale set --ssh

```

--------------------------------

### Configure Connector with ProxyClass

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/customize

This example shows how to specify a ProxyClass for a Connector resource by setting the `spec.proxyClass` field to the desired ProxyClass name.

```yaml
apiVersion: tailscale.com/v1alpha1
kind: Connector
metadata:
  name: prod
spec:
  proxyClass: prod
  ...
```

--------------------------------

### Uninstall Tailscale

Source: https://tailscale.com/docs/install/windows/wsl2

This command removes the Tailscale package from a Debian-based Linux distribution within WSL 2.

```bash
sudo apt-get remove tailscale
```

--------------------------------

### Get Tailscale Version

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Prints the current Tailscale client version. Can also display the daemon version, a machine-readable JSON output, or the latest upstream release version.

```bash
tailscale version [flags]

```

```bash
tailscale version

```

--------------------------------

### Default SSH Policy Example

Source: https://tailscale.com/docs/reference/syntax/policy-file

This JSON snippet represents a broad default SSH policy allowing any member to access any destination. It includes grants and SSH rules, specifying actions, sources, destinations, and users.

```json
{
  "grants": [
    {
      "src": ["*"],
      "dst": ["*"],
      "ip": ["*"]
    }
  ],
  "ssh": [
    {
      "action": "accept",
      "src": ["autogroup:member"],
      "dst": ["autogroup:self"],
      "users": ["root", "autogroup:nonroot"]
    },
    {
      "action": "accept",
      "src": ["autogroup:member"],
      "dst": ["tag:prod"],
      "users": ["root", "autogroup:nonroot"]
    },
    {
      "action": "accept",
      "src": ["tag:logging"],
      "dst": ["tag:prod"],
      "users": ["root", "autogroup:nonroot"]
    }
  ]
}
```

--------------------------------

### Manage Tailscale System Policies

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=fish

Provides functionality to list, reload, or inspect system policies configured in your Tailscale network. The `--json` flag can be used to get machine-readable output.

```bash
tailscale syspolicy

```

```bash
tailscale syspolicy list

```

```bash
tailscale syspolicy reload

```

```bash
tailscale syspolicy --json

```

--------------------------------

### Get Device Posture Attributes

Source: https://tailscale.com/docs/features/tailscale-accessbot-jit

Retrieves all posture attributes for a specified device. This includes both standard node attributes and custom attributes, along with their expiry times if set.

```APIDOC
## GET /api/v2/device/{deviceID}/attributes

### Description
Retrieve all posture attributes for the specified device. This returns a JSON object of all the key-value pairs of posture attributes for the device.

### Method
GET

### Endpoint
/api/v2/device/{deviceID}/attributes

#### Path Parameters
- **deviceID** (string) - Required - The ID of the device to fetch posture attributes for.

### Request Example
```bash
curl "https://api.tailscale.com/api/v2/device/11055/attributes" \
-u "tskey-api-xxxxx:"
```

### Response
#### Success Response (200)
- **attributes** (object) - A key-value map of all attributes associated with a given node. The values can be either a number, string, or boolean.
- **expiries** (object) - A key-value map of attributes that have an expiry time, and when they will expire. Any attribute without an expiry is omitted. If there are no attributes with expiries, the entire `expiries` field is omitted.

#### Response Example
```json
{
  "attributes": {
    "custom:myScore": 87,
    "custom:diskEncryption": true,
    "custom:myAttribute": "my_value",
    "node:os": "linux",
    "node:osVersion": "5.19.0-42-generic",
    "node:tsReleaseTrack": "stable",
    "node:tsVersion": "1.40.0",
    "node:tsAutoUpdate": false
  },
  "expiries": {
    "custom:myScore": "2024-04-23T18:25:43.511Z"
  }
}
```
```

--------------------------------

### Go Test for tshello HTTP Client Connectivity

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This Go test function, `TestTshelloHTTPClient`, creates a `tsnet` client and attempts to connect to running tshello instances over the tailnet. It requires a valid `TS_AUTHKEY` environment variable and tests connectivity to both test and production servers. The test skips if the auth key is not provided.

```go
func TestTshelloHTTPClient(t *testing.T) {
 if testing.Short() {
  t.Skip("skipping test in short mode")
 }

 authKey := os.Getenv("TS_AUTHKEY")
 if authKey == "" {
  t.Skip("TS_AUTHKEY not set, skipping Tailscale connectivity test")
 }

 ctx, cancel := context.WithTimeout(context.Background(), 2*time.Minute)
 defer cancel()

 srv := &tsnet.Server{
  Hostname: "tshello-client-test",
  Dir:      t.TempDir(),
  AuthKey:  authKey,
 }
 defer srv.Close()

 if err := srv.Start(); err != nil {
  t.Fatalf("failed to start tsnet: %v", err)
 }

 httpClient := srv.HTTPClient()

 targets := []string{
  "tshello-test",
  "tshello",
 }

 for _, target := range targets {
  t.Run(fmt.Sprintf("ping_%s", target), func(t *testing.T) {
   url := fmt.Sprintf("http://%s/", target)

   req, err := http.NewRequestWithContext(ctx, "GET", url, nil)
   if err != nil {
    t.Skipf("failed to create request for %s: %v", target, err)
    return
   }

   resp, err := httpClient.Do(req)
   if err != nil {
    if strings.Contains(err.Error(), "no such host") ||
       strings.Contains(err.Error(), "connection refused") ||
       strings.Contains(err.Error(), "timeout") {

```

--------------------------------

### Create Tailscale CLI Alias in macOS Shell Config

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=macos

Example of creating a shell alias in `.bashrc`, `.zshrc`, or other shell configuration files to easily access the Tailscale CLI on macOS.

```bash
alias tailscale="/Applications/Tailscale.app/Contents/MacOS/Tailscale"
```

--------------------------------

### Example Grant for Subnet Access

Source: https://tailscale.com/docs/reference/route-injection

This JSON snippet defines an access control grant for Tailscale. It specifies that members of the 'group:engineering' can send traffic to the '192.168.0.0/16' IP range from any source IP.

```json
{
  "grants": [
    {
      "src": ["group:engineering"],
      "dst": ["192.168.0.0/16"],
      "ip": ["*"]
    }
  ]
}

```

--------------------------------

### IP and Hostname Based Access Control in Tailscale ACLs

Source: https://tailscale.com/docs/reference/examples/acls

This example demonstrates how to configure Tailscale ACLs to allow access between specific IP addresses and hostnames. It also shows how to grant access to subnets via a subnet router using both IP addresses and hostnames. The `hosts` section allows for defining human-friendly names for IP addresses or CIDR ranges.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": [
        "100.100.123.124"
      ],
      "dst": [
        "100.100.123.123:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "100.100.123.124"
      ],
      "dst": [
        "192.0.2.0/24:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "frontend-server-01"
      ],
      "dst": [
        "192.0.2.0/24:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "frontend-server-01"
      ],
      "dst": [
        "dev-network-01:*"
      ]
    }
  ],
  "hosts": {
    "frontend-server-01": "100.100.123.123",
    "dev-network-01": "203.0.113.0/24"
  }
}
```

--------------------------------

### Tailscale Access Rule with Synced Okta Group

Source: https://tailscale.com/docs/integrations/identity/okta/okta-scim

Example of how to reference a synced Okta group within a Tailscale access control policy file. This rule grants access from the 'engineering@example.com' group to the 'logging' tag for all IPs.

```json
{
  "grants": [
    {
      "src": ["group:engineering@example.com"],
      "dst": ["tag:logging"],
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Commit and Push Tailnet Policy File using Git CLI

Source: https://tailscale.com/docs/integrations/bitbucket/gitops

This code snippet demonstrates how to add, commit, and push your tailnet policy file to a Bitbucket repository using the Git command-line interface. Ensure you have Git installed and configured for your repository.

```bash
git add .
git commit -sm "policy: import from admin console"
git push -u origin main

```

--------------------------------

### Secure CI/CD Pipeline Access with Tailscale Groups and Tags

Source: https://tailscale.com/docs/reference/examples/grants

This example demonstrates how to restrict access to CI/CD pipeline components based on team roles, separating development and production environments. It uses Tailscale groups and tags to ensure developers can access development tools while the DevOps team manages access to build tools and production.

```json
{
  "groups": {
    "group:dev": ["alice@example.com", "bob@example.com"],
    "group:devops": ["carl@example.com"]
  },
  "grants": [
    {
      "src": ["group:dev"],
      "dst": ["tag:dev"],
      "ip": ["*"]
    },
    {
      "src": ["group:devops"],
      "dst": ["tag:ci", "tag:prod"],
      "ip": ["*"]
    }
  ],
  "tagOwners": {
    "tag:ci": ["group:devops"],
    "tag:dev": ["group:devops", "tag:ci"],
    "tag:prod": ["group:devops", "tag:ci"]
  }
}
```

--------------------------------

### Configure Let's Encrypt Staging Environment for ProxyGroup

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

This configuration demonstrates how to set up a ProxyGroup to use Let's Encrypt's staging environment for issuing TLS certificates. It involves defining a ProxyGroup and a ProxyClass, where the ProxyClass specifies `useLetsEncryptStagingEnvironment: true`.

```yaml
apiVersion: tailscale.com/v1alpha1
kind: ProxyGroup
metadata:
  name: ingress-proxies
spec:
  type: ingress
  replicas: 2
  tags: ["tag:ingress-proxies"]
  proxyClass: letsencrypt-staging
---
apiVersion: tailscale.com/v1alpha1
kind: ProxyClass
metadata:
  name: letsencrypt-staging
spec:
  useLetsEncryptStagingEnvironment: true

```

--------------------------------

### Advertise Tailscale Serve Service

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

Advertises the current node as a host for a specific service on the tailnet. This command is useful for bringing a service back online after it has been drained or for initial service setup. The `--service=<name>` flag can be used to specify a particular service.

```bash
tailscale serve advertise <service> [--service=<name>]
```

--------------------------------

### Get Device Information with Whois

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Retrieves information about the machine and user associated with a Tailscale IP. Can output in a human-readable format or as JSON. Supports specifying the protocol (TCP/UDP) for the request.

```bash
tailscale whois ip[:port]

```

```bash
tailscale whois --json ip[:port]

```

--------------------------------

### Configure Tailscale System Policies with `defaults` CLI (Mac App Store)

Source: https://tailscale.com/docs/integrations/mdm/mac

These `defaults` CLI commands configure Tailscale system policies for the Mac App Store variant. They set the organization name and suppress the IP address copied alert by writing directly to the application's preferences. These commands can be used to test MDM configurations without a full MDM setup.

```bash
defaults write io.tailscale.ipn.macos ManagedByOrganizationName "Tailscale, Inc."
defaults write io.tailscale.ipn.macos IPAddressCopiedAlertSuppressed -bool true

```

--------------------------------

### Schedule Tailscale Client Updates on Synology

Source: https://tailscale.com/docs/integrations/synology

This script automates the process of checking for and installing updates for the Tailscale client on a Synology device. It is designed to be run as a scheduled task.

```bash
tailscale update --yes

```

--------------------------------

### Tag-Based Access Control in Tailscale ACLs

Source: https://tailscale.com/docs/reference/examples/acls

This example shows how to use tags in Tailscale ACLs to control access between devices based on their assigned tags. Tags provide a way to group devices by their purpose, allowing for more flexible and maintainable access policies.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": [
        "tag:frontend"
      ],
      "dst": [
        "tag:backend:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "tag:backend"
      ],
      "dst": [
        "tag:logging:*"
      ]
    }
  ]
}
```

--------------------------------

### Provision Server with Hostname and Auth Key

Source: https://tailscale.com/docs/how-to/set-up-servers

This command shows how to provision a server with Tailscale, specifying both an authentication key and a custom hostname. The `--hostname` flag allows you to set a specific machine name for the server within the Tailscale network, which is useful for MagicDNS.

```bash
tailscale up --auth-key=$TS_AUTHKEY --hostname=$TS_HOSTNAME

```

--------------------------------

### Get Proxy Logs and Events for ProxyGroup

Source: https://tailscale.com/docs/reference/troubleshooting/kubernetes-operator

These commands retrieve logs and events for a proxy pod associated with a ProxyGroup. This is useful for troubleshooting proxy configurations managed by ProxyGroups.

```bash
$ pod_name=$(kubectl get pod --selector=tailscale.com/parent-resource-type=proxygroup,tailscale.com/parent-resource=<proxy-group-name> \
  --namespace tailscale -ojsonpath='{.items[0].metadata.name}')
$ kubectl logs ${pod_name} --namespace tailscale
$ kubectl describe pod ${pod_name} --namespace tailscale

```

--------------------------------

### Get Ingress Details with Kubectl

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

Retrieves Ingress resource details, including the MagicDNS name exposed to Tailscale, from a Kubernetes cluster. This is the first step in validating cluster routing.

```bash
kubectl get ingress
```

--------------------------------

### Tailscale Policy: Grant and Deny Access (Tailnet 2)

Source: https://tailscale.com/docs/features/multiple-tailnets

This JSON policy grants access for 'group2@example.com' to 'tag:production' on port 443 and explicitly denies 'group1@example.com' access to the same resource. It serves as an example for configuring access control in a separate tailnet environment.

```json
{
  "grants": [
    {
      "src": ["group2@example.com"],
      "dst": ["tag:production"],
      "ip": ["443"]
    }
  ],
  "tests": [
    {
      "src": "group1@example.com",
      "deny": ["tag:production:443"]
    }
  ]
}
```

--------------------------------

### Enforce Communication Boundaries with Tags

Source: https://tailscale.com/docs/reference/examples/grants

This example enforces communication boundaries between application components using tags, ideal for zero-trust architectures. It ensures each tier can only communicate with adjacent tiers, controlling traffic flow between application layers like frontend, backend, and database.

```json
{
  "grants": [
    {
      "src": ["tag:frontend"],
      "dst": ["tag:backend"],
      "ip": ["*"]
    },
    {
      "src": ["tag:backend"],
      "dst": ["tag:logging"],
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Configure Device as Tailscale App Connector

Source: https://tailscale.com/docs/features/app-connectors/how-to/setup

This command configures a device to act as a Tailscale app connector. It advertises the device as a connector and assigns it specific tags, enabling it to route traffic according to the tailnet policy file.

```bash
tailscale up --advertise-connector --advertise-tags=tag:<connector-tag-name>
```

--------------------------------

### Configure Tailscale Pulumi Provider

Source: https://tailscale.com/docs/integrations/pulumi-provider

Sets the Tailscale API key and tailnet name for Pulumi configuration. Requires the Tailscale Pulumi provider to be installed. The API key should be set as a secret.

```bash
pulumi config set tailscale:apiKey tskey-1234567CNTRL-abcdefghijklmnopqrstu --secret
pulumi config set tailscale:tailnet example.com
```

--------------------------------

### Get Tailscale Connection Status (Human-Readable)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=powershell

Retrieves the status of connections to other Tailscale devices, displaying a condensed table of human-readable information. This is useful for a quick overview of your tailnet.

```bash
tailscale status

```

--------------------------------

### Add Tailscale Helm Repository

Source: https://tailscale.com/docs/features/kubernetes-operator

Adds the official Tailscale Helm chart repository to your local Helm configuration. This allows you to access and install Tailscale-related Helm charts.

```bash
helm repo add tailscale https://pkgs.tailscale.com/helmcharts
```

--------------------------------

### Export Auth Key for Tailscale Lock

Source: https://tailscale.com/docs/features/tailnet-lock?tab=tailscale+cli

Sets the AUTH_KEY environment variable to a pre-signed auth key. This is the first step in adding a node to a locked tailnet using a pre-signed key. Ensure you replace the example key with your actual auth key.

```bash
export AUTH_KEY="tskey-auth-<XXXXCTRL-NNNNNN>"

```

--------------------------------

### Get Proxy Logs and Events for Ingress

Source: https://tailscale.com/docs/reference/troubleshooting/kubernetes-operator

These commands retrieve logs and describe events for a proxy pod associated with an Ingress resource. They help in diagnosing issues related to traffic being proxied for Ingress configurations.

```bash
$ pod_name=$(kubectl get pod --selector=tailscale.com/parent-resource-type=ingress,tailscale.com/parent-resource=<ingress-name>,tailscale.com/parent-resource-ns=<ingress-namespace> \
  --namespace tailscale -ojsonpath='{.items[0].metadata.name}')
$ kubectl logs ${pod_name} --namespace tailscale
$ kubectl describe pod ${pod_name} --namespace tailscale

```

--------------------------------

### Add Tailscale Repository and Key (Shell)

Source: https://tailscale.com/docs/install/debian/debian-trixie

Adds Tailscale's official package signing key and repository configuration to the APT package manager. This allows the system to trust and find Tailscale packages.

```shell
curl -fsSL https://pkgs.tailscale.com/stable/debian/trixie.noarmor.gpg | sudo tee /usr/share/keyrings/tailscale-archive-keyring.gpg >/dev/null
curl -fsSL https://pkgs.tailscale.com/stable/debian/trixie.tailscale-keyring.list | sudo tee /etc/apt/sources.list.d/tailscale.list
```

--------------------------------

### Run Tailscale System Tray Application (Linux)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Launches the system tray application for Linux desktop clients, enabling access to common actions like fast user switching and exit node selection. This command is in beta and requires Tailscale v1.88 or later. Do not run with `sudo`.

```bash
tailscale systray
```

--------------------------------

### Get Proxy Logs and Events for Connector

Source: https://tailscale.com/docs/reference/troubleshooting/kubernetes-operator

These commands fetch logs and events for a proxy pod created for a Tailscale Connector. This is vital for diagnosing connectivity and proxy issues when using Connectors.

```bash
$ pod_name=$(kubectl get pod --selector=tailscale.com/parent-resource-type=connector,tailscale.com/parent-resource=<connector-name> \
  --namespace tailscale -ojsonpath='{.items[0].metadata.name}')
$ kubectl logs ${pod_name} --namespace tailscale
$ kubectl describe pod ${pod_name} --namespace tailscale

```

--------------------------------

### Anthropic Provider Configuration

Source: https://tailscale.com/docs/features/aperture/configuration

Configures the Anthropic provider to use the messages API with 'x-api-key' authorization. This example details the base URL, API key, supported models, and compatibility settings.

```json
{
  "providers": {
    "anthropic": {
      "baseurl": "https://api.anthropic.com",
      "apikey": "YOUR_ANTHROPIC_KEY",
      "authorization": "x-api-key",
      "models": ["claude-sonnet-4-5", "claude-haiku-4-5", "claude-opus-4-5"],
      "compatibility": {
        "openai_chat": false,
        "anthropic_messages": true
      }
    }
  }
}
```

--------------------------------

### Serve Content with a Valid Certificate using Tailscale Serve

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

When serving content with `tailscale serve` and you have a valid certificate, use the `https` pseudo-protocol in the `<target>` argument. This ensures secure HTTPS connections.

```bash
tailscale serve https:<target>
```

--------------------------------

### API Error Response Example

Source: https://tailscale.com/docs/features/workload-identity-federation

This snippet shows the structure of an API error response from the Tailscale token exchange endpoint. The error message contains a link to the federated identity in the admin console for detailed debugging.

```json
{ "message": "Unauthorized. Visit [link to admin console] for details" }
```

--------------------------------

### Use PROXY Protocol with Tailscale Serve

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

Enable the PROXY protocol with `tailscale serve` to preserve connection information like the source IP address. Version 2 is recommended for most situations. The `--proxy-protocol=<version>` flag specifies the protocol version.

```bash
tailscale serve --proxy-protocol=<version> <target>
```

--------------------------------

### Define Tailscale API Audit Log Variables

Source: https://tailscale.com/docs/features/logging/audit-logging

Sets environment variables for accessing Tailscale configuration audit logs. These include the API access token, tailnet ID, and the start and end timestamps for the log retrieval period.

```bash
export ACCESS_TOKEN=tskey-api-k123456CNTRL-0123456789abcdef
export TAILNET_ID=example.com
export START=2022-07-20T00:00:00Z
export END=2022-07-21T00:00:00Z
```

--------------------------------

### Get Tailscale Proxy Pods

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

This command retrieves a list of pods belonging to a specific ProxyGroup, identified by the `tailscale.com/parent-resource` label. It's useful for debugging by showing the status and readiness of the proxy instances.

```bash
kubectl get pod -n tailscale -l tailscale.com/parent-resource="ingress-proxies",tailscale.com/parent-resource-type="proxygroup"

```

--------------------------------

### Load TUN Kernel Module

Source: https://tailscale.com/docs/install/linux

Loads the 'tun' kernel module, which is required by Tailscale. This command is useful if Tailscale encounters errors related to missing kernel modules. It can be run manually or configured to load automatically on boot.

```bash
sudo modprobe tun

```

--------------------------------

### Advertise Subnet Routes on macOS

Source: https://tailscale.com/docs/features/subnet-routers?tab=macos

This snippet demonstrates how to configure a macOS device to advertise specific subnet routes using the Tailscale CLI. It assumes Tailscale is installed and the CLI is accessible. The command enables IP forwarding and makes the specified IPv4 subnets available to the tailnet.

```shell
# If Tailscale CLI is not in PATH, use the full path to the executable
/Applications/Tailscale.app/Contents/MacOS/Tailscale set --advertise-routes=192.0.2.0/24,198.51.100.0/24

# If Tailscale CLI is in PATH
sudo tailscale set --advertise-routes=192.0.2.0/24,198.51.100.0/24
```

--------------------------------

### Example asciinema Session Recording Structure

Source: https://tailscale.com/docs/features/tailscale-ssh/tailscale-ssh-session-recording

This snippet shows the structure of a typical `asciinema` session recording file. It's a newline-delimited JSON format containing metadata about the session and subsequent events, each with a timestamp and output data. This format allows for easy parsing and searching of session content.

```json
{"version":2,"width":203,"height":38,"timestamp":1679441819,"env":{"TERM":"xterm-256color"},"srcNode":"srcnode.ts.net","srcNodeID":"nguedK2CNTRL","srcNodeTags":null,"sshUser":"alice","localUser":"alice","srcNodeUserID":30585448562688899,"srcNodeUser":"alice@tailscale.com"}
[0.456997416,"o","Last login: Tue Mar 21 16:35:14 from 1.2.3.4\r\n"]
[0.552500666,"o","\u001b[1m\u001b[7m%\u001b[27m\u001b[1m\u001b[0m                                                                                                                                                                                                          \r \r"]
[0.557596708,"o","\u001b]2;alice@laptop:~\u0007\u001b]1;~\u0007"]
[0.567016125,"o","\r\u001b[0m\u001b[27m\u001b[24m\u001b[J\u001b[01;32m➜  \u001b[36m~\u001b[00m \u001b[K"]
[0.567112833,"o","\u001b[?1h\u001b=\u001b[?2004h"]
[1.500827583,"o","e"]
[1.58455025,"o","\u0008ec"]
[1.6682777500000001,"o","h"]
[1.7546742499999999,"o","o"]
[1.896455708,"o"," "]
[2.020248958,"o","h"]
[2.08789675,"o","i"]
[2.323278875,"o","\u001b[?1l\u001b\u003e"]
[2.323438208,"o","\u001b[?2004l\r\r\n"]
[2.324209,"o","\u001b]2;echo hi\u0007"]
[2.324296291,"o","\u001b]1;echo\u0007hi\r\n\u001b[1m\u001b[7m%\u001b[27m\u001b[1m\u001b[0m                                                                                                                                                                                                          \r \r"]
[2.334692083,"o","\u001b]2;alice@laptop:~\u0007\u001b]1;~\u0007"]
[2.349814583,"o","\r\u001b[0m\u001b[27m\u001b[24m\u001b[J\u001b[01;32m➜  \u001b[36m~\u001b[00m \u001b[K"]
[2.349910875,"o","\u001b[?1h\u001b=\u001b[?2004h"]
[2.89156075,"o","\u001b[?2004l\r\r\n"]
```

--------------------------------

### Deploy Tailscale Application to Koyeb

Source: https://tailscale.com/docs/install/cloud/koyeb

This command deploys the application to Koyeb, creating a new service that connects to the tailnet. It uses the previously created TAILSCALE_AUTHKEY secret and specifies deployment options like instance type, region, and archive builder.

```bash
koyeb deploy . myapp/main --instance-type small --region was --type worker --archive-builder docker --env TAILSCALE_AUTHKEY=@TAILSCALE_AUTHKEY --privileged
```

--------------------------------

### Dockerfile for Tailscale Integration on Koyeb

Source: https://tailscale.com/docs/install/cloud/koyeb

A multistage Dockerfile that builds an application and then copies the application code and Tailscale binaries into a final production image. This allows the Koyeb service to run Tailscale and join the tailnet.

```dockerfile
FROM alpine:latest as builder
WORKDIR /app
COPY . ./ 
# This is where you build the application code as well.

# https://docs.docker.com/develop/develop-images/multistage-build/#use-multi-stage-builds
FROM alpine:latest
RUN apk update && apk add ca-certificates iptables ip6tables && rm -rf /var/cache/apk/*

# Copy binary to production image.
COPY --from=builder /app/start.sh /app/start.sh

# Copy Tailscale binaries from the tailscale image on Docker Hub.
COPY --from=docker.io/tailscale/tailscale:stable /usr/local/bin/tailscaled /app/tailscaled
COPY --from=docker.io/tailscale/tailscale:stable /usr/local/bin/tailscale /app/tailscale
RUN mkdir -p /var/run/tailscale /var/cache/tailscale /var/lib/tailscale

# Run on container startup.
CMD ["/app/start.sh"]
```

--------------------------------

### Share Files in Background with Tailscale Serve (Linux/macOS)

Source: https://tailscale.com/docs/reference/examples/serve

This command shares the `/tmp/public` directory in the background using Tailscale Serve. The `--bg` flag ensures the server continues running even after the terminal session closes. To stop it, `tailscale serve off` must be executed. Requires `sudo` on Linux.

```bash
sudo tailscale serve --bg /tmp/public
```

--------------------------------

### Bootstrap script for Tailscale on AWS Lambda

Source: https://tailscale.com/docs/install/cloud/aws/aws-lambda

This script initializes Tailscale in userspace networking mode and starts the SOCKS5 proxy before executing the main application. It uses the TAILSCALE_AUTHKEY environment variable for authentication and sets a hostname for the Lambda instance.

```sh
#!/bin/sh

mkdir -p /tmp/tailscale
/var/runtime/tailscaled --tun=userspace-networking --socks5-server=localhost:1055 &
/var/runtime/tailscale up --auth-key=${TAILSCALE_AUTHKEY} --hostname=aws-lambda-app
echo Tailscale started
ALL_PROXY=socks5://localhost:1055/ /var/runtime/my-app

```

--------------------------------

### Advertise Subnet Routes with Tailscale

Source: https://tailscale.com/docs/features/subnet-routers/how-to/setup

Advertises specific IPv4 subnet routes for a device to use as a subnet router within the Tailscale network. Replace the example subnets with your actual network ranges.

```shell
sudo tailscale set --advertise-routes=192.0.2.0/24,198.51.100.0/24
```

--------------------------------

### Get Tailscale Nameserver IP (Shell)

Source: https://tailscale.com/docs/solutions/manage-multi-cluster-kubernetes-deployments-argocd

Retrieves the IP address of the Tailscale nameserver deployed by the Tailscale Kubernetes Operator. This IP address is necessary for configuring CoreDNS to forward Tailscale-specific DNS queries. The command uses `kubectl` to get the `DNSConfig` resource and extracts the nameserver IP from its status.

```bash
kubectl get dnsconfig ts-dns -o jsonpath='{.status.nameserverStatus.ip}'
```

--------------------------------

### Autogroup Based Access Control in Tailscale ACLs

Source: https://tailscale.com/docs/reference/examples/acls

This example demonstrates how to leverage Tailscale's autogroups in ACLs to manage access for different sets of users or devices. It shows how to grant general members access to tagged resources and how administrators can access specific tagged resources.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": [
        "autogroup:member"
      ],
      "dst": [
        "tag:frontend:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "autogroup:admin"
      ],
      "dst": [
        "tag:backend:*",
        "tag:logging:*"
      ]
    }
  ]
}
```

--------------------------------

### Approve Tailscale System Extension with Configuration Profile (macOS)

Source: https://tailscale.com/docs/integrations/mdm/mac

This XML configuration snippet allows the Tailscale system extension to be approved automatically on macOS Standalone installations. It requires setting the PayloadScope to 'System' and includes a system extension policy to permit extensions signed by Tailscale without user interaction. This configuration must be deployed via an MDM server.

```xml
<key>PayloadScope</key>
<string>System</string>
```

```xml
<dict>
  <key>PayloadUUID</key>
  <string>1d08bf7d-7898-43b3-88e3-76cfb74a7c33</string>
  <key>PayloadType</key>
  <string>com.apple.system-extension-policy</string>
  <key>PayloadOrganization</key>
  <string>Tailscale</string>
  <key>PayloadIdentifier</key>
  <string>8a790b57-16da-4371-8baf-d6f65e7b50ee</string>
  <key>PayloadDisplayName</key>
  <string>Allows system extensions signed by Tailscale to run without user approval.</string>
  <key>PayloadDescription</key>
  <string/>
  <key>PayloadVersion</key>
  <integer>1</integer>
  <key>PayloadEnabled</key>
  <true/>
  <key>AllowedTeamIdentifiers</key>
  <array>
    <string>W5364U7YZB</string>
  </array>
</dict>
```

--------------------------------

### tailscale-client-go-v2 Authentication

Source: https://tailscale.com/docs/features/workload-identity-federation?tab=github+actions

Illustrates how to authenticate the `tailscale-client-go-v2` library using workload identity by providing a ClientID and an IDTokenFunc to the Tailscale client.

```APIDOC
## tailscale-client-go-v2

### Description
Authenticates the `tailscale-client-go-v2` library using workload identity. This involves configuring the `tailscale.Client` with a `ClientID` and an `IDTokenFunc` that provides the identity token.

### Method
N/A (Configuration within Go code)

### Endpoint
N/A

### Parameters
#### `tailscale.Client` Configuration
- **Tailnet** (string) - Optional - Your Tailscale tailnet name (e.g., from environment variable `TAILSCALE_TAILNET`).
- **Auth** (`tailscale.IdentityFederation`) - Required for workload identity authentication.
  - **ClientID** (string) - Required - Your Tailscale OAuth Client ID (e.g., from environment variable `TAILSCALE_OAUTH_CLIENT_ID`).
  - **IDTokenFunc** (func() (string, error)) - Required - A function that returns the workload identity token (e.g., from environment variable `IDENTITY_TOKEN`).

### Request Example
```go
package main

import (
	"context"
	"os"

	"tailscale.com/client/tailscale/v2"
)

func main() {
	client := &tailscale.Client{
		Tailnet: os.Getenv("TAILSCALE_TAILNET"),
		Auth: &tailscale.IdentityFederation{
			ClientID: os.Getenv("TAILSCALE_OAUTH_CLIENT_ID"),
			IDTokenFunc: func() (string, error) {
				return os.Getenv("IDENTITY_TOKEN"), nil
            },
		},
	}

	// Example API call
	devices, err := client.Devices().List(context.Background())
}
```
```

--------------------------------

### Reference IP Sets in ACLs

Source: https://tailscale.com/docs/features/tailnet-policy-file/ip-sets

Demonstrates how to reference an IP set within Access Control Lists (ACLs) to define traffic acceptance rules. This example allows traffic from 'group:devops' to any destination within 'ipset:prod'.

```json
"acls": [
  {
    "src": ["group:devops"],
    "dst": ["ipset:prod:*"],
    "action": "accept",
  },
]
```

--------------------------------

### Get Certificate using Tailscale Go Client

Source: https://tailscale.com/docs/how-to/set-up-https-certificates

Implement the `tls.Config.GetCertificate` callback in Go to automatically obtain TLS certificates for your Tailscale nodes. This method handles the certificate provisioning process seamlessly within your Go application. Ensure you have the Tailscale Go client library imported.

```go
import (
	"crypto/tls"
	"tailscale.com/client/tailscale"
)

// ... within your TLS configuration
GetCertificate: tailscale.LocalClient.GetCertificate,
```

--------------------------------

### Start Tailscale in Userspace Networking Mode (CLI)

Source: https://tailscale.com/docs/concepts/userspace-networking

Enables userspace networking mode for Tailscale via the CLI, configuring both SOCKS5 and HTTP proxies to listen on the same port. This method is recommended for ephemeral nodes and auth keys.

```bash
tailscaled --tun=userspace-networking --socks5-server=localhost:1055 --outbound-http-proxy-listen=localhost:1055 &
tailscale up --auth-key=<your-auth-key>
```

--------------------------------

### Tailscale Access Control Policy Example

Source: https://tailscale.com/docs/concepts/corporate-vpn

This JSON snippet demonstrates how to define access control rules in Tailscale. It specifies which users or groups can access which destinations and on which ports, using tags for categorization and IP addresses for port restrictions. This configuration is managed via the Tailscale admin console or a policy file.

```json
"grants": [
  // Engineering users, plus the president, can access port 22 (ssh)
  // and port 3389 (remote desktop protocol) on all servers, and all
  // ports on git-server or ci-server.
  {
    "src": ["group:engineering", "president@example.com"],
    "dst": ["*"],
    "ip": ["22", "3389"]
  },
  {
    "src": ["group:engineering", "president@example.com"],
    "dst": ["git-server", "ci-server"],
    "ip": ["*"]
  }
]

```

--------------------------------

### Configure MagicDNS Nameservers and Search Domains

Source: https://tailscale.com/docs/install/nixos

This NixOS configuration sets up the nameservers and search domains required for Tailscale's MagicDNS feature. It includes the Tailscale MagicDNS nameserver and fallback public DNS servers, along with a custom search domain.

```nix
networking.nameservers = [ "100.100.100.100" "8.8.8.8" "1.1.1.1" ];
networking.search = [ "example.ts.net" ];
```

--------------------------------

### Apply Tailscale Postures to Access Grants

Source: https://tailscale.com/docs/features/device-posture

This JSON snippet illustrates how to use the 'srcPosture' field within a 'grants' rule in a Tailscale policy file. It shows two examples: one requiring 'posture:anyMac' for access to 'tag:development', and another requiring 'posture:latestMac' for access to 'tag:production' by 'group:dev'.

```json
"grants": [
  {
    "src": ["autogroup:member"],
    "dst": ["tag:development"],
    "ip": ["*"],
    "srcPosture": ["posture:anyMac"]
  },
  {
    "src": ["group:dev"],
    "dst": ["tag:production"],
    "ip": ["*"],
    "srcPosture": ["posture:latestMac"]
  }
]
```

--------------------------------

### Network Microsegmentation with Tailscale Policy

Source: https://tailscale.com/docs/reference/examples/grants

Implements logical tailnet segmentation to enhance security and limit the spread of attacks. This example allows controlled cross-segment access for a support team, granting them access to specific ports across isolated segments. It requires defining groups, grants, and tag owners.

```json
{
  "grants": [
    {
      "src": ["group:support"],
      "dst": ["tag:segment-abc", "tag:segment-xyz"],
      "ip": ["443"]
    },
    {
      "src": ["tag:support"],
      "dst": ["tag:segment-abc", "tag:segment-xyz"],
      "ip": ["443"]
    }
  ],
  "groups": {
    "group:support": ["alice@example.com", "bob@example.com"]
  },
  "tagOwners": {
    "tag:support": ["autogroup:admin"]
  }
}
```

--------------------------------

### Configure Tailscale Resources

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=macos

Configure various resources within your tailnet. This includes setting up `kubectl` for Kubernetes (`kubeconfig`), managing macOS VPN configurations (`mac-vpn`), configuring Synology for outbound connections (`synology`), managing macOS system extensions (`sysext`), and controlling the Linux `systray` client.

```bash
tailscale configure kubeconfig <hostname-or-fqdn>
tailscale configure mac-vpn install
tailscale configure mac-vpn uninstall
tailscale configure synology
tailscale configure sysext activate
tailscale configure sysext deactivate
tailscale configure sysext status
tailscale configure systray --enable-startup=systemd
```

--------------------------------

### Customize autogroup:internet with IP Sets

Source: https://tailscale.com/docs/features/tailnet-policy-file/ip-sets

Explains how to customize `autogroup:internet` using IP sets to control traffic flowing through an exit node. This example adds `autogroup:internet`, removes specific application gateways and partner networks, and then grants access to the defined internet subset from office exit nodes.

```json
"ipsets": {
  "ipset:internet": [
    "add autogroup:internet",
    "remove ipset:cdn-edge",
    "remove ipset:partner-net"
  ],
  "ipset:cdn-edge": ["8.21.9.6", "8.21.9.7", "8.21.9.13", "8.21.9.14"],
  "ipset:partner-net": ["52.23.40.0/24"]
},
"grants": [
  {
    "src": ["group:sea"],
    "dst": ["ipset:internet"],
    "ip":  ["*"],
    "via": ["tag:officerouter-sea"],
  },
  {
    "src": ["group:lhr"],
    "dst": ["ipset:internet"],
    "ip":  ["*"],
    "via": ["tag:officerouter-lhr"],
  }
]
```

--------------------------------

### Configure Tailscale CLI Tab Completion

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=bash

This command configures tab completion for the Tailscale CLI in Bash. It sources the completion script, enabling auto-completion for commands, flags, and arguments. Ensure you have Bash installed and configured.

```bash
source <(tailscale completion bash)
```

--------------------------------

### Create TLS Listener with Server.ListenTLS

Source: https://tailscale.com/docs/reference/tsnet-server-api

Creates a TLS-wrapped network listener for your tailnet using Tailscale's Let's Encrypt support. It returns a net.Listener that wraps incoming connections with TLS, suitable for HTTPS services. This method implicitly calls Start if not already invoked.

```go
srv := new(tsnet.Server)
srv.Hostname = "aegis"

ln, err := srv.ListenTLS("tcp", ":443")
if err != nil {
    log.Fatal(err)
}

log.Fatal(http.Serve(ln, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hi there! Welcome to the tailnet!")
})))

```

--------------------------------

### Control Environment Access by Device Posture (JSON)

Source: https://tailscale.com/docs/reference/examples/grants

This configuration controls access to different infrastructure environments (development, staging, production) based on device security posture. It enforces stricter security requirements for more sensitive environments, ensuring progressive security postures. Requires defining postures, IP sets, groups, and tags elsewhere in the policy file.

```json
{
  "grants": [
    {
      "src": ["group:devs"],
      "dst": ["ipset:prod-infra"],
      "ip": ["*"],
      "via": ["tag:prod-connector"],
      "srcPosture": ["posture:strict-mac"]
    },
    {
      "src": ["group:devs"],
      "dst": ["ipset:stg-infra"],
      "ip": ["*"],
      "via": ["tag:stg-connector"],
      "srcPosture": ["posture:semi-strict-mac"]
    },
    {
      "src": ["group:devs"],
      "dst": ["ipset:dev-infra"],
      "ip": ["*"],
      "via": ["tag:dev-connector"],
      "srcPosture": ["posture:any-mac"]
    }
  ]
}
```

--------------------------------

### Complete Tailscale Configuration

Source: https://tailscale.com/docs/features/aperture/configuration

This JSON configuration outlines a full setup for Tailscale, including access control lists (ACLs) for user permissions, database settings for data storage, exporter configurations for LLM session logs to S3, detailed settings for various LLM providers (OpenAI, Anthropic, Gemini, private), and integration hooks for external services like Oso.

```json
{
  // Access control: who can use which models
  "temp_grants": [
    // Allow all users basic access
    {
      "src": ["*"],
      "grants": [
        {"role": "user"},
        {"providers": [{"provider": "*", "model": "*"}]}
      ]
    },
    // Admin access for specific user
    {
      "src": ["admin@company.com"],
      "grants": [
        {"role": "admin"},
        {"providers": [{"provider": "*", "model": "*"}]},
        {"mcp": [{"server": "*", "tool": "*"}]}
      ]
    },
  ],

  // Database settings
  "database": {
    "save_raws": false,
    "keep_encrypted_blobs": false
  },

  // LLM session log export configuration
  "exporters": {
    "s3": {
      "bucket_name": "aperture-exports",
      "region": "us-west-2",
      "prefix": "prod",
      "access_key_id": "YOUR_AWS_KEY",
      "access_secret": "YOUR_AWS_SECRET",
      "every": 3600,
      "limit": 1000
    }
  },

  // LLM providers
  "providers": {
    "openai": {
      "baseurl": "https://api.openai.com/",
      "apikey": "YOUR_OPENAI_KEY",
      "models": ["gpt-5", "gpt-5-mini", "gpt-4.1"],
      "name": "OpenAI",
      "description": "OpenAI models for coding and chat",
      "compatibility": {
        "openai_chat": true,
        "openai_responses": true
      }
    },
    "anthropic": {
      "baseurl": "https://api.anthropic.com",
      "apikey": "YOUR_PROXY_ANTHROPIC_KEY",
      "authorization": "x-api-key",
      "models": ["claude-sonnet-4-5", "claude-haiku-4-5", "claude-opus-4-5"],
      "name": "Anthropic",
      "compatibility": {
        "openai_chat": false,
        "anthropic_messages": true
      }
    },
    "gemini": {
      "baseurl": "https://generativelanguage.googleapis.com",
      "apikey": "YOUR_PROXY_GEMINI_KEY",
      "authorization": "x-goog-api-key",
      "models": ["gemini-2.5-flash", "gemini-2.5-pro"],
      "name": "Google Gemini",
      "compatibility": {
        "openai_chat": false,
        "gemini_generate_content": true
      }
    },
    "private": {
      "baseurl": "YOUR_PRIVATE_LLM_URL",
      "tailnet": true,
      "models": ["qwen3-coder-30b"]
    }
  },

  // Hooks for external integrations
  "hooks": {
      "oso": {
          "url":    "https://api.osohq.com/api/agents/v1/model-request",
          "apikey": "YOUR_OSO_API_KEY",
      },
  },
}

```

--------------------------------

### Get Tailscale Service Details

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Retrieves details about a Kubernetes `Service` of type `LoadBalancer`, including its cluster IP, external IP (Tailscale IP), and ports. This is useful for verifying the Service configuration and obtaining the Tailscale IP address.

```bash
kubectl get svc nginx
```

--------------------------------

### Get Tailscale IP Address

Source: https://tailscale.com/docs/features/subnet-routers?tab=android

Retrieves the IPv4 address assigned to the Tailscale interface on a subnet router. This command is useful for verification and network configuration tasks.

```bash
tailscale ip -4

```

--------------------------------

### Get Recorder Status and UI URL

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/tsrecorder

Retrieves the status and UI endpoint for a deployed Kubernetes Recorder resource. This command helps in accessing the recorder's user interface and confirming its operational status.

```bash
$ kubectl get Recorder recorder
NAME       STATUS            URL
recorder   RecorderCreated   https://recorder-0.tails-scales.ts.net

```

--------------------------------

### Generate and Set Tailscale Certificate for Proxmox

Source: https://tailscale.com/docs/integrations/proxmox

This bash script generates a valid certificate for the Proxmox host using Tailscale and then sets it within the Proxmox certificate store. It requires 'jq' to be installed and assumes Tailscale is already configured.

```bash
#!/bin/bash
NAME="$(tailscale status --json | jq '.Self.DNSName | .[:-1]' -r)"
tailscale cert "${NAME}"
pvenode cert set "${NAME}.crt" "${NAME}.key" --force --restart

```

--------------------------------

### Get Tailscale Lock Status (CLI)

Source: https://tailscale.com/docs/features/tailnet-lock?tab=ios

Retrieves the Tailnet Lock status for the current node using the Tailscale CLI. This command is only available on Linux, macOS, and Windows and displays the node's Tailnet Lock public key.

```bash
tailscale lock status
```

--------------------------------

### Get Tailscale Connection Status (JSON)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Retrieves the status of connections to other Tailscale devices in a machine-readable JSON format. This is ideal for automation and scripting, providing detailed peer and user information along with metadata.

```bash
tailscale status --json
```

--------------------------------

### GET /api/v2/tailnet/{TAILNET_ID}/logging/network

Source: https://tailscale.com/docs/features/logging/network-flow-logs

Retrieves network traffic logs for a given tailnet within a specified time frame. Requires an API access token for authentication.

```APIDOC
## GET /api/v2/tailnet/{TAILNET_ID}/logging/network

### Description
Retrieves network traffic logs for a given tailnet within a specified time frame. Requires an API access token for authentication.

### Method
GET

### Endpoint
`https://api.tailscale.com/api/v2/tailnet/{TAILNET_ID}/logging/network`

### Parameters
#### Query Parameters
- **start** (string) - Required - The start of the timeframe for the logs to retrieve (ISO 8601 format).
- **end** (string) - Required - The end of the timeframe for the logs to retrieve (ISO 8601 format).

### Request Example
```bash
export ACCESS_TOKEN=tskey-api-k123456CNTRL-0123456789abcdef
export TAILNET_ID=example.com
export START=2022-10-28T22:40:00.000000000Z
export END=2022-10-28T22:40:04.999999999Z

curl -u $ACCESS_TOKEN: \
  "https://api.tailscale.com/api/v2/tailnet/{$TAILNET_ID}/logging/network?start={$START}&end={$END}"
```

### Response
#### Success Response (200)
- **logs** (array) - An array of log objects, each containing details about network traffic.
  - **start** (string) - The start time of the log entry.
  - **end** (string) - The end time of the log entry.
  - **logged** (string) - The timestamp when the log was recorded.
  - **nodeId** (string) - The ID of the node associated with the log.
  - **srcNode** (object) - Information about the source node.
    - **nodeId** (string)
    - **addresses** (array of strings)
    - **os** (string)
    - **name** (string)
    - **user** (string)
  - **dstNodes** (array of objects) - Information about the destination nodes.
  - **virtualTraffic** (array of objects) - Details of virtual network traffic.
  - **physicalTraffic** (array of objects) - Details of physical network traffic.

#### Response Example
```json
{
	"logs": [
		 {
			"start":  "2025-10-28T22:39:51.890385065Z",
			"end":    "2025-10-28T22:39:56.886545512Z",
			"logged": "2025-10-28T22:40:00.290605382Z",

			"nodeId": "nBcdef1CNTRL",
			"srcNode":
					{
						"nodeId": "nBcdef1CNTRL",
						"addresses": ["100.111.22.33", "fd7a:115c:a1e0::c034:c374"],
						"os": "linux",
						"name": "pangolin.example.ts.net",
						"user": "joe@example.com"
					},
			"dstNodes": [
					{
						"nodeId": "n22daC8CNTRL",
						"addresses": ["100.111.44.55", "fd7a:115c:a1e0::abcd:0123"],
						"os": "windows",
						"name": "alice-laptop.example.ts.net",
						"user": "alice@example.com"
					},
					{
						"nodeId": "nX8fDaxCNTRL",
						"addresses": ["100.44.55.66",  "fd7a:115c:a1e0::a1b2:c3d4"],
						"os": "linux",
						"name": "prod.example.ts.net",
						"tags": ["tag:prod"]},
					{
						"nodeId": "n7sUpZQCNTRL",
						"addresses": ["100.99.88.77",  "fd7a:115c:a1e0::91ab:84ab"],
						"os": "linux",
						"name": "logstream.remote.ts.net",
						"tags": ["tag:logstream"]}
			]
		}
	]
}
```

### Error Handling
- **401 Unauthorized**: Invalid or missing API access token.
- **400 Bad Request**: Invalid query parameters (e.g., invalid date format for start/end).
- **404 Not Found**: The specified tailnet ID does not exist.
```

--------------------------------

### Configure Device Posture Rules in Tailscale Policy

Source: https://tailscale.com/docs/reference/syntax/policy-file

The `postures` section defines rules for device posture management. These rules ensure devices meet specific criteria, such as operating system and Tailscale version, before being granted access. Each posture must start with the `posture:` prefix.

```json
"postures": {
  "posture:latestMac": [
    "node:os IN ['macos']",
    "node:tsReleaseTrack == 'stable'",
    "node:tsVersion >= '1.40'",
  ],
}
```

--------------------------------

### Configure Minecraft Server on NixOS

Source: https://tailscale.com/docs/solutions/set-up-nixos-minecraft

This NixOS configuration enables and sets up a Minecraft server. It includes options for EULA agreement, declarative mode, and various server properties like port, gamemode, MOTD, and RCON password. It also enables the use of unfree packages.

```nix
# enable closed source packages such as the minecraft server
nixpkgs.config.allowUnfree = true;

services.minecraft-server = {
  enable = true;
  eula = false; # set to true if you agree to Mojang's EULA: https://account.mojang.com/documents/minecraft_eula
  declarative = true;

  # see here for more info: https://minecraft.gamepedia.com/Server.properties#server.properties
  serverProperties = {
    server-port = 25565;
    gamemode = "survival";
    motd = "NixOS Minecraft server on Tailscale!";
    max-players = 5;
    enable-rcon = true;
    # This password can be used to administer your minecraft server.
    # Exact details as to how will be explained later. If you want
    # you can replace this with another password.
    "rcon.password" = "hunter2";
    level-seed = "10292992";
  };
};

```

--------------------------------

### Get Proxy Logs and Events for Service

Source: https://tailscale.com/docs/reference/troubleshooting/kubernetes-operator

These commands retrieve logs and describe events for a proxy pod associated with a Service resource (ingress or egress). They are crucial for troubleshooting proxy behavior related to Kubernetes Services.

```bash
$ pod_name=$(kubectl get pod --selector=tailscale.com/parent-resource-type=svc,tailscale.com/parent-resource=<service-name>,tailscale.com/parent-resource-ns=<service-namespace> \
  --namespace tailscale -ojsonpath='{.items[0].metadata.name}')
$ kubectl logs ${pod_name} --namespace tailscale
$ kubectl describe pod ${pod_name} --namespace tailscale

```

--------------------------------

### Get Tailscale IP Address (IPv6)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=zsh

Retrieves the IPv6 Tailscale IP address for the current device. This command is useful for environments that primarily use IPv6.

```bash
tailscale ip -6
```

--------------------------------

### Tailscale IP Address Retrieval

Source: https://tailscale.com/docs/reference/tailscale-cli

Get the Tailscale IP address for the current device or other devices on your network. You can specify IPv4 or IPv6, or request only one address.

```APIDOC
## GET /websites/tailscale/ip

### Description
Get a device's Tailscale IP address.

### Method
GET

### Endpoint
/websites/tailscale/ip

### Parameters
#### Query Parameters
- **hostname** (string) - Optional - The hostname of the device for which to retrieve the IP address.
- **4** (boolean) - Optional - Only return an IPv4 address.
- **6** (boolean) - Optional - Only return an IPv6 address.
- **1** (boolean) - Optional - Only return one address, preferring IPv4.

### Request Example
```json
{
  "hostname": "raspberrypi"
}
```
```json
{
  "4": true
}
```

### Response
#### Success Response (200)
- **ip_address** (string) - The Tailscale IP address(es).

#### Response Example
```json
{
  "ip_address": "100.121.112.23"
}
```
```json
{
  "ip_address": "100.126.153.111\nfd7a:115c:a1e0:ab12:4843:cd96:627e:9975"
}
```
```

--------------------------------

### Add Signing Nodes with Tailscale Lock

Source: https://tailscale.com/docs/features/tailnet-lock?tab=ios

Adds one or more nodes as signing nodes to the Tailnet Lock configuration. This command requires the Tailnet Lock public keys of the nodes to be added. Replace the example keys with your actual Tailnet Lock keys.

```bash
tailscale lock add tlpub:trusted-key1 tlpub:trusted-key2
```

--------------------------------

### Run tsnet Service Program

Source: https://tailscale.com/docs/features/tsnet/how-to/register-service

This command executes the Go program created in the previous step, initiating the Tailscale Service listener. It requires the '--service' flag to be set with the name of the Tailscale Service to be exposed.

```bash
go run tsnet-services.go --service=svc:tsnet-demo

```

--------------------------------

### Fetch Tailscale Configuration Audit Logs via API

Source: https://tailscale.com/docs/features/logging/audit-logging

Makes a GET request to the Tailscale API to retrieve configuration audit logs within a specified time range. Requires an API access token and tailnet ID. The response is a JSON object containing log entries.

```bash
curl -u  $ACCESS_TOKEN:  -X GET \
  "https://api.tailscale.com/api/v2/tailnet/{$TAILNET_ID}/logging/configuration?start={$START}&end={$END}"
```

--------------------------------

### ACL Rule Example in JSON

Source: https://tailscale.com/docs/reference/syntax/policy-file

This JSON snippet demonstrates a basic access control list (ACL) rule within the Tailscale policy file. It specifies an 'accept' action, allowing traffic from a defined list of sources to a defined list of destinations using TCP protocol.

```json
{
  "action": "accept",
  "src": [ <list-of-sources> ],
  "proto": "tcp", // optional
  "dst": [ <list-of-destinations> ]
}
```

--------------------------------

### Get Tailscale IP Address

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=macos

Retrieves the Tailscale IP address (IPv4 and/or IPv6) for the current or a specified device. Supports filtering by IP version.

```bash
tailscale ip [flags] [<hostname>]
tailscale ip -4
tailscale ip -6
tailscale ip -1
tailscale ip raspberrypi
```

--------------------------------

### Uninstall Tailscale using MSI on Windows

Source: https://tailscale.com/docs/install/windows/msi

Uninstalls the Tailscale client from Windows using the MSI package. This command can be used with or without logging enabled. The MSI file and log file path should be replaced with the actual paths.

```bash
msiexec /x <path_to_tailscale_msi.msi>
msiexec /L <path_to_log.log> /x <path_to_tailscale_msi.msi>
```

--------------------------------

### Get Tailnet Lock Status

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Outputs the current state and configuration of Tailnet Lock for your tailnet. Running `tailscale lock` without arguments defaults to this command.

```bash
tailscale lock status
```

```bash
tailscale lock
```

--------------------------------

### Configure Tailscale Funnel Access with Node Attributes

Source: https://tailscale.com/docs/reference/syntax/policy-file

This example demonstrates how to use the `nodeAttrs` policy to enable Tailscale Funnel for members of the tailnet. It targets users in `autogroup:member` and applies the `funnel` attribute.

```json
{
  "nodeAttrs": [
    {
      "target": ["autogroup:member"],
      "attr":   ["funnel"]
    }
  ]
}
```

--------------------------------

### Configure Tailnet Policy File

Source: https://tailscale.com/docs/features/tsnet/how-to/register-service

This code snippet shows an example of a tailnet policy file configuration. It includes definitions for tag owners, auto-approvers for services, and general access grants, specifying source, destination, and IP access rules.

```json
{
  "tagOwners": {
    "tag:tsnet-demo-host": ["autogroup:member"]
  },
  "autoApprovers": {
    "services": {
      "svc:tsnet-demo": ["tag:tsnet-demo-host"]
    }
  },
  "grants": [
    {
      "src": ["*"]
      "dst": ["svc:tsnet-demo"]
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Minimal Aperture Configuration (JSON)

Source: https://tailscale.com/docs/features/aperture/configuration

This JSON configuration defines a minimal setup for Aperture by Tailscale. It specifies an LLM provider (Anthropic) with its base URL, API key placeholder, available models, and authorization method. It also includes compatibility settings for Anthropic's Messages API. The configuration is essential for controlling model availability and authentication with upstream providers.

```json
{
  "providers": {
    "anthropic": {
      "baseurl": "https://api.anthropic.com",
      "apikey": "YOUR_ANTHROPIC_API_KEY",
      "models": [
        "claude-sonnet-4-5",
        "claude-opus-4-5"
      ],
      "authorization": "x-api-key",
      "compatibility": {
        "anthropic_messages": true
      }
    }
  }
}
```

--------------------------------

### Get Tailscale IP Address for a Specific Host

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Retrieves the Tailscale IP addresses (both IPv4 and IPv6) for a specified hostname on your tailnet. Useful for network diagnostics.

```bash
tailscale ip raspberrypi
```

--------------------------------

### Configure Sysctl for Network Hardening

Source: https://tailscale.com/docs/install/arch

Sets reverse path filtering to strict mode (1) for enhanced network security. This prevents the kernel from accepting packets from a source address unless a route back to that source exists.

```bash
net.ipv4.conf.default.rp_filter = 1
net.ipv4.conf.all.rp_filter = 1
```

--------------------------------

### Tailscale: Register Node with OAuth Credentials

Source: https://tailscale.com/docs/features/oauth-clients

Shows how to register a new node using `tailscale up` with an OAuth secret. It covers specifying tags and using URL-style parameters like `ephemeral`, `preauthorized`, and `baseURL` within the `--auth-key` flag. The OAuth client requires the `auth_keys` scope.

```bash
tailscale up --auth-key=${OAUTH_CLIENT_SECRET} --advertise-tags=tag:ci

```

```bash
tailscale up --auth-key='${OAUTH_CLIENT_SECRET}?ephemeral=false&preauthorized=true' --advertise-tags=tag:ci

```

--------------------------------

### Tailscale Funnel Status and URL

Source: https://tailscale.com/docs/reference/examples/funnel

Displays the status of the Tailscale Funnel service, including the public HTTPS URL and the local proxy target. This output confirms that the local server is successfully exposed to the internet. It is generated after running the `tailscale funnel` command.

```bash
sudo tailscale funnel 3000
Available on the internet:
https://amelie-workstation.pango-lin.ts.net

|-- / proxy http://127.0.0.1:3000

Press Ctrl+C to exit.
```

--------------------------------

### Tailscale SSH Policy File Configuration Example

Source: https://tailscale.com/docs/reference/syntax/policy-file

This JSON snippet demonstrates the structure of an 'ssh' definition within a Tailscale policy file. It specifies actions, sources, destinations, allowed users, and re-authentication periods for Tailscale SSH connections. The 'action' can be 'accept' or 'check', with 'check' requiring periodic re-authentication defined by 'checkPeriod'.

```json
{
  "action": "check",
  "src": [ <list-of-sources> ],
  "dst": [ <list-of-destinations> ],
  "users": [ <list-of-ssh-users> ],
  "checkPeriod": "20h",
  "acceptEnv": [ "GIT_EDITOR", "GIT_COMMITTER_*", "CUSTOM_VAR_V?" ],
  "srcPosture": [ <list-of-posture-conditions> ]
}
```

--------------------------------

### Restrictive CI Access Rules (JSON)

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This JSON snippet provides examples of more restrictive access rules for CI runners. It limits access to specific destinations and ports, such as PostgreSQL databases on port 5432 and staging APIs on ports 443 and 8080.

```json
"grants": [
  {
    "src": ["tag:ci"],
    "dst": ["tag:prod-db"],
    "ip": ["5432"]
  },
  {
    "src": ["tag:ci"],
    "dst": ["tag:staging-api"],
    "ip": ["443", "8080"]
  },
  // Other access rules
]
```

--------------------------------

### Configure Fortinet for Tailscale Direct Connections

Source: https://tailscale.com/docs/integrations/firewalls

This configuration snippet for Fortinet firewalls allows Tailscale devices to establish direct connections by randomizing the WireGuard client port. It involves updating the tailnet policy file to include `randomizeClientPort: true`.

```json
{
  // Tailnet policy file settings and other configurations
  "randomizeClientPort": true
}
```

--------------------------------

### Configure Tailnet Policy for Service AutoApprovers

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Configures the `autoApprovers` section of a tailnet policy file to allow specific `ProxyGroup` devices to advertise Tailscale Services. This example permits devices tagged with `tag:eu-cluster` to advertise services tagged with `tag:monitoring`.

```json
{
  "autoApprovers": {
    "services": {
      "tag:monitoring": ["tag:eu-cluster"],
    },
  },
}

```

--------------------------------

### Define Auth Key Flag (Go)

Source: https://tailscale.com/docs/features/tsnet/how-to/create-basic-tsnet-app

Defines a command-line flag for a Tailscale authentication key. This allows users to provide an auth key when running the program.

```go
var (
	addr      = flag.String("addr", ":80", "address to listen on")
	tsAuthKey = flag.String("ts-authkey", "", "Tailscale auth key")
)
```

--------------------------------

### Tailscale Exit Node Information

Source: https://tailscale.com/docs/reference/tailscale-cli

Retrieve information about exit nodes in your Tailscale network, including listing available exit nodes and getting a suggested exit node.

```APIDOC
## GET /websites/tailscale/exit-node

### Description
Get information about exit nodes in your Tailscale network.

### Method
GET

### Endpoint
/websites/tailscale/exit-node

### Parameters
#### Query Parameters
- **subcommand** (string) - Required - The subcommand to execute: 'list' or 'suggest'.
- **filter** (string) - Optional - Filter exit nodes by country (only applicable for 'list' subcommand).

### Request Example
```json
{
  "subcommand": "list",
  "filter": "US"
}
```
```json
{
  "subcommand": "suggest"
}
```

### Response
#### Success Response (200)
- **exit_nodes** (array) - List of available exit nodes (if subcommand is 'list'). Each object may contain 'country', 'ip', 'hostname'.
- **suggested_exit_node** (object) - Details of the suggested exit node (if subcommand is 'suggest').

#### Response Example
```json
{
  "exit_nodes": [
    {
      "country": "US",
      "ip": "100.x.y.z",
      "hostname": "us-exit-node"
    }
  ]
}
```
```json
{
  "suggested_exit_node": {
    "country": "DE",
    "ip": "100.a.b.c",
    "hostname": "de-exit-node"
  }
}
```
```

--------------------------------

### Grant User Access to Aperture Instance (Tailscale ACL JSON)

Source: https://tailscale.com/docs/features/aperture

An example of Tailscale access control rules in JSON format to grant specific users access to the Aperture instance. This configuration defines user groups, hostnames, and grant rules for network access.

```json
{
  // Define the ai-users group in the "groups" section of the access control rules.
  "groups" : [
    "group:ai-users": [
      "dave@example.com",
      "alice@example.com"
    ]
 ],
   // Set the hostname of your Aperture instance to "ai" in the "hosts" section of the access control rules.
  "host": [
    "ai": "<YOUR_APERTURE_IP_ADDRESS>"
  ],
  // Create a grant access control rule that allows users in the "group:ai-users" group to access the "ai" host on TCP ports 80, 443, and all ICMP types.
  "grants": [
    {
      "src": [
        "group:ai-users"
       ],
       "dst": ["ai"],
       "ip": ["tcp:80", "tcp:443", "icmp:*"]
    }
  ]
}
```

--------------------------------

### Get Tailscale IP Address (IPv4 and IPv6)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=bash

Retrieves the Tailscale IP addresses (both IPv4 and IPv6) for the current device. This command can be modified to return only IPv4 or IPv6.

```bash
tailscale ip
tailscale ip -4
tailscale ip -6
tailscale ip --1
```

--------------------------------

### Get Tailscale Serve Status

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

Retrieves the current status of Tailscale serve services running on the device. The `--json` flag can be used to obtain the status in JSON format for programmatic parsing.

```bash
tailscale serve status [--json]
```

--------------------------------

### Run Tailscale CLI Commands (Linux)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

On Linux, the `tailscale` binary is typically in your PATH, allowing you to execute commands directly. This is the primary interface for managing Tailscale on Linux systems.

```bash
tailscale <command>

```

--------------------------------

### Define Tag Owners with No Specific Owners (JSON)

Source: https://tailscale.com/docs/features/tags

This JSON example illustrates defining tag owners in the tailnet policy file where a tag, 'tag:infrastructure', has an empty list of owners. This signifies that the tag is implicitly owned by Owners, Admins, and Network admins of the tailnet and can be applied via the admin console or an auth key.

```json
{
  "tagOwners": {
    "tag:server": ["dave@tailscale.com"],
    "tag:infrastructure": [] // No tag owners defined
  }
}
```

--------------------------------

### Compress Tailscale Binary with UPX (Bash)

Source: https://tailscale.com/docs/how-to/set-up-small-tailscale

Demonstrates compressing a combined Tailscale binary using UPX with LZMA compression and the 'best' compression level. This significantly reduces the on-disk size of the binary, but carries security risks and may be flagged by antivirus software.

```bash
go build -o tailscale.combined -tags ts_include_cli -ldflags="-s -w" ./cmd/tailscaled
du -hs tailscale.combined
upx --lzma --best ./tailscale.combined
du -hs tailscale.combined
```

--------------------------------

### Tailscale Policy: User Self-Access

Source: https://tailscale.com/docs/reference/examples/grants

This policy enables authenticated users to access their own devices while maintaining isolation from other users' devices. It utilizes the `autogroup:member` and `autogroup:self` autogroups for dynamic user and device referencing. This is a good starting point for implementing the principle of least privilege.

```json
{
  "grants": [
    {
      "src": ["autogroup:member"],
      "dst": ["autogroup:self"],
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Configure Default Tags via Environment Variable

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/customize

This snippet demonstrates how to set default tags for proxy devices using the `PROXY_TAGS` environment variable when installing the Tailscale operator with static manifests. Multiple tags are comma-separated.

```bash
export PROXY_TAGS="tag:prod,tag:emea"
```

--------------------------------

### Configure Intune Posture Integration in Tailscale

Source: https://tailscale.com/docs/integrations/mdm/intune

Steps to connect Tailscale with Microsoft Intune to fetch device posture data. This involves navigating the Tailscale admin console, providing Intune account details like Microsoft Region, Application (Client) ID, Directory (Tenant) ID, and Client Secret.

```text
1. Open the Device management page of the Tailscale admin console.
2. Under the **Device Posture Integrations** section, locate the Intune integration, then select **Connect**.
3. Select your **Microsoft Region** , the region where your Intune account is located.
4. Enter your **Application (Client) ID** , **Directory (Tenant) ID** and **Client Secret**.
5. Select **Connect to Intune**.
```

--------------------------------

### Enable Tailscale Web Interface

Source: https://tailscale.com/docs/reference/tailscale-client-metrics

Enables the Tailscale web interface on a client device to expose metrics. This is a prerequisite for collecting metrics remotely via the web interface.

```bash
tailscale set --webclient
```

--------------------------------

### Configure Tailscale Client System Policies (MDM)

Source: https://tailscale.com/docs/reference/deployment-checklist

Configure Tailscale client applications using system policies via an MDM solution. These policies control various client behaviors, such as DNS settings, subnet advertising, posture checking, and UI elements. They help enforce organizational standards and user experience.

```text
UseTailscaleDNSSettings: always | never
UseTailscaleSubnets: always | never
PostureChecking: always | never
AdminConsole: show | hide
HiddenNetworkDevices: show | hide
ManageTailnetLock: show | hide
RunExitNode: show | hide
ManagedByCaption: "Your Caption"
ManagedByOrganizationName: "Your Organization Name"
ManagedByURL: "http://your-support-url.com"
```

--------------------------------

### Create Public and Tailnet Listener with Server.ListenFunnel

Source: https://tailscale.com/docs/reference/tsnet-server-api

Establishes a TLS-wrapped network listener accessible from both the tailnet and the public internet via Funnel. Allows exposing services publicly. The `tsnet.FunnelOnly()` option can create a public-only listener. This method implicitly calls Start if not already invoked.

```go
srv := new(tsnet.Server)
srv.Hostname = "ophion"

ln, err := srv.ListenFunnel("tcp", ":443")
if err != nil {
    log.Fatal(err)
}

log.Fatal(http.Serve(ln, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hi there! Welcome to the tailnet!")
})))

```

```go
srv := new(tsnet.Server)

publicLn, err := srv.ListenFunnel("tcp", ":443", tsnet.FunnelOnly())
if err != nil {
    log.Fatal(err)
}

privateLn, err := srv.ListenTLS("tcp", ":443")
if err != nil {
    log.Fatal(err)
}

```

--------------------------------

### Diagnose Connection Path with `tailscale ping`

Source: https://tailscale.com/docs/reference/troubleshooting?tab=macos

The `tailscale ping` command helps determine if a device is reachable via a direct path or through a DERP relay. It stops once a direct path is established or after sending a set number of pings.

```bash
tailscale ping device2
```

--------------------------------

### Enable Taildrive File Sharing on macOS (App Store)

Source: https://tailscale.com/docs/features/taildrive

This command enables the File Sharing option in the Tailscale client settings on macOS for applications installed from the App Store. After running, the Tailscale client needs to be closed and reopened.

```shell
defaults write io.tailscale.ipn.macos FileSharingConfiguration -string show
```

--------------------------------

### Configure Federated Identities using tailscale-client-go-v2

Source: https://tailscale.com/docs/features/workload-identity-federation

This section demonstrates how to configure federated identities programmatically using the `tailscale-client-go-v2` library.

```APIDOC
## POST /websites/tailscale/federated_identities (tailscale-client-go-v2)

### Description
Configures federated identities using the `tailscale-client-go-v2` library.

### Method
POST (via client library)

### Endpoint
N/A (Client Library Method)

### Parameters
#### Request Body (via `tailscale.CreateFederatedIdentityRequest` struct)
- **Description** (string) - Required - A description for the federated identity.
- **Scopes** (array of strings) - Required - The scopes to be granted to the federated identity.
- **Tags** (array of strings) - Optional - Tags to associate with the federated identity.
- **Subject** (string) - Required - The subject identifier for the federated identity.
- **CustomClaimRules** (map[string]string) - Optional - Custom claim rules for the federated identity.
  - **repo_name** (string) - Optional - Example custom claim rule for repository name.

### Request Example (Go Code)
```go
package main

import (
	"context"
	"os"

	"tailscale.com/client/tailscale/v2"
)

func main() {
	client := &tailscale.Client{
		// Client configuration
	}

	req := tailscale.CreateFederatedIdentityRequest {
		Description: "Example federated identity",
		Scopes:  []string{"auth_keys", "devices:core"},
		Tags:    []string{"tag:test"},
		Subject: "example-sub-*",
		CustomClaimRules: map[string]string{
			"repo_name": "example-repo-name",
		},
	}

	federatedIdentity, err := client.Keys().CreateFederatedIdentity(context.Background(), req)
}
```

### Response
#### Success Response
- **federatedIdentity** (*tailscale.FederatedIdentity) - The created federated identity object.
- **err** (error) - An error object if the operation failed.

#### Response Example (Conceptual)
```json
{
  "id": "fedid-12345abcde",
  "description": "Example federated identity",
  "scopes": ["auth_keys", "devices:core"],
  "tags": ["tag:test"],
  "issuer": "https://example.com",
  "subject": "example-sub-*",
  "customClaimRules": {
    "repo_name": "example-repo-name"
  }
}
```
```

--------------------------------

### Add tsnet Dependency to Go Program

Source: https://tailscale.com/docs/features/tsnet

This command adds the tsnet library to your Go project's dependencies, making it available for import and use within your Go source files. Ensure you have Go installed and configured.

```bash
go get tailscale.com/tsnet

```

--------------------------------

### Deploy Tailscale System Policy Configuration Profile (XML)

Source: https://tailscale.com/docs/integrations/mdm/mac

This XML configuration profile deploys the required system policies for Tailscale VPN on macOS. It sets 'VPNOnDemandIsUserConfigured' to true and 'VPNOnDemandSettings' to 'hide', ensuring automatic client restarts and hiding the VPN On Demand UI from the user.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>PayloadDisplayName</key>
        <string>Tailscale: System Policy Configuration Profile</string>
        <key>PayloadType</key>
        <string>Configuration</string>
        <key>PayloadVersion</key>
        <integer>1</integer>
        <key>PayloadIdentifier</key>
        <string>io.tailscale.ipn.macos.mdm.797d4461-837c-4f5a-b18e-7e300b057018</string>
        <key>PayloadUUID</key>
        <string>0f451881-7ac4-4171-80ed-b55251053231</string>
        <key>PayloadContent</key>
        <array>
            <dict>
                <key>PayloadDisplayName</key>
                <string>System Policies</string>
                <key>PayloadType</key>
                <string>io.tailscale.ipn.macos</string>
                <key>PayloadVersion</key>
                <integer>1</integer>
                <key>PayloadIdentifier</key>
                <string>io.tailscale.ipn.macos.f4806335-6703-4680-8f41-f40e6f281c71</string>
                <key>PayloadUUID</key>
                <string>3e44f9b0-d309-48d3-b055-6dc683d438c8</string>
                <key>ManagedByOrganizationName</key>
                <string>Tail and Scales, Inc.</string>
                <key>VPNOnDemandIsUserConfigured</key>
                <true/>
                <key>VPNOnDemandSettings</key>
                <string>hide</string>
            </dict>
        </array>
    </dict>
</plist>
```

--------------------------------

### Share Serve Node via SSH Reverse Proxy

Source: https://tailscale.com/docs/reference/examples/serve

Establishes an SSH reverse proxy to forward traffic from a local development server (port 3000) to a shared Serve node (port 8080). This allows multiple collaborators to access the development server through a stable, shared Serve DNS name.

```Shell
ssh -NT -R 8080:127.0.0.1:3000 web-dev.pango-lin.ts.net
```

--------------------------------

### Configure IP Forwarding with sysctl.d

Source: https://tailscale.com/docs/how-to/connect-vpc

These commands enable IPv4 and IPv6 forwarding by creating or appending to a sysctl configuration file within '/etc/sysctl.d'. The 'sysctl -p' command then applies these new settings.

```bash
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

--------------------------------

### Configure Sysctl for Subnet Routing/Exit Nodes

Source: https://tailscale.com/docs/install/arch

Sets reverse path filtering to loose (2) or off (0) to allow packet forwarding when Tailscale is used as a subnet router or exit node. This is necessary for proper traffic routing in these configurations.

```bash
net.ipv4.conf.default.rp_filter = 2
net.ipv4.conf.all.rp_filter = 2
```

--------------------------------

### Fetch and Prettify Tailscale Configuration Audit Logs

Source: https://tailscale.com/docs/features/logging/audit-logging

Fetches configuration audit logs from the Tailscale API and uses `json_pp` to format the JSON output for better readability. This is useful for inspecting the log data.

```bash
curl -u  $ACCESS_TOKEN: -X GET \
  "https://api.tailscale.com/api/v2/tailnet/{$TAILNET_ID}/logging/configuration?start={$START}&end={$END}" \
  | json_pp
```

--------------------------------

### Bind Local TCP Service (SSH) to Tailnet

Source: https://tailscale.com/docs/reference/examples/serve

Binds a local TCP-based service, such as SSH, to a specific port on your Tailscale IP address, making it accessible privately across your tailnet. This is useful for providing backup access or alternative connection methods.

```Shell
tailscale serve --tcp 2222 22
```

--------------------------------

### Build Combined Tailscale Binary (Go)

Source: https://tailscale.com/docs/how-to/set-up-small-tailscale

Builds a single binary that acts as both the Tailscale client and daemon. The behavior is determined by how the binary is invoked (e.g., renamed to 'tailscale' or 'tailscaled'). Requires a Go development environment.

```bash
go build -o tailscale.combined -tags ts_include_cli ./cmd/tailscaled
du -hs tailscale.combined
```

--------------------------------

### Get Tailscale Connection Status

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=fish

Retrieves the status of connections to other Tailscale devices. The default output is a human-readable table, but a `--json` flag provides machine-readable output suitable for automation.

```bash
tailscale status

```

```bash
tailscale status --json

```

--------------------------------

### Print Tailscale Metrics to CLI

Source: https://tailscale.com/docs/reference/tailscale-client-metrics

Prints all available Tailscale metrics directly to the command line interface. This is useful for quick inspection or scripting.

```bash
tailscale metrics print
```

--------------------------------

### Kubernetes Recorder with S3 Storage and Static Credentials

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/tsrecorder

Configures the tsrecorder on Kubernetes to use S3 for durable storage of recordings. This example includes a Kubernetes Secret for AWS credentials and defines the S3 bucket, endpoint, and credential source within the Recorder resource spec. It also assigns a tag for the recorder device and enables the UI.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: s3-auth
  namespace: tailscale
stringData:
  AWS_ACCESS_KEY_ID: ABC...
  AWS_SECRET_ACCESS_KEY: xyz123...
---
apiVersion: tailscale.com/v1alpha1
kind: Recorder
metadata:
  name: recorder
spec:
  enableUI: true
  tags:
    - "tag:k8s-recorder"
  storage:
    s3:
      endpoint: s3.us-east-1.amazonaws.com
      bucket: tsrecorder-bucket
      credentials:
        secret:
          name: s3-auth

```

--------------------------------

### Register Node with Client ID and Identity Token

Source: https://tailscale.com/docs/features/workload-identity-federation

This snippet shows how to register a new node with Tailscale using the `tailscale up` command with `--client-id` and `--id-token` flags. It requires a client ID and an OIDC identity token. Optional flags like `--advertise-tags` can be included.

```shell
tailscale up --client-id=${CLIENT_ID} --id-token=${IDENTITY_TOKEN} --advertise-tags=tag:ci
```

--------------------------------

### Get Tailscale IP Address

Source: https://tailscale.com/docs/features/subnet-routers?tab=windows

Retrieves the IPv4 address assigned to the Tailscale interface on the subnet router. This command is used for verification purposes to confirm the subnet router's connectivity within the Tailscale network.

```bash
tailscale ip -4
```

--------------------------------

### Example Tailscale Webhook Events Payload (JSON)

Source: https://tailscale.com/docs/features/webhooks

This JSON snippet demonstrates a typical webhook payload from Tailscale, containing an array of event objects. Each event includes details such as timestamp, version, type, tailnet, message, and specific data related to the event. This format is used to minimize overhead when sending multiple events.

```json
[
  {
    "timestamp": "2022-09-21T13:37:51.658918-04:00",
    "version": 1,
    "type": "test",
    "tailnet": "example.com",
    "message": "This is a test event",
    "data": null
  },
  {
    "timestamp": "2022-09-21T13:59:02.949217-04:00",
    "version": 1,
    "type": "nodeCreated",
    "tailnet": "example.com",
    "message": "Node alice-workstation1.yak-bebop.ts.net created",
    "data": {
      "nodeID": "nFJw3SRKTM59",
      "deviceName": "alice-workstation1.yak-bebop.ts.net",
      "managedBy": "alice@example.com",
      "actor": "alice@example.com",
      "url": "https://login.tailscale.com/admin/machines/100.12.345.67"
    }
  },
  {
    "timestamp": "2022-09-21T13:59:02.949278-04:00",
    "version": 1,
    "type": "nodeNeedsApproval",
    "tailnet": "example.com",
    "message": "Node alice-workstation1.yak-bebop.ts.net needs approval",
    "data": {
      "nodeID": "nFJw3SRKTM59",
      "deviceName": "alice-workstation1.yak-bebop.ts.net",
      "managedBy": "alice@example.com",
      "actor": "alice@example.com",
      "url": "https://login.tailscale.com/admin/machines/100.12.345.67"
    }
  },
  {
    "timestamp": "2022-09-21T13:59:15.966728-04:00",
    "version": 1,
    "type": "nodeApproved",
    "tailnet": "example.com",
    "message": "Node alice-workstation1.yak-bebop.ts.net approved",
    "data": {
      "nodeID": "nFJw3SRKTM59",
      "deviceName": "alice-workstation1.yak-bebop.ts.net",
      "managedBy": "alice@example.com",
      "actor": "admin@example.com",
      "url": "https://login.tailscale.com/admin/machines/100.12.345.67"
    }
  },
  {
    "timestamp": "2023-04-21T13:59:15.966728-04:00",
    "version": 1,
    "type": "nodeDeleted",
    "tailnet": "example.com",
    "message": "Node alice-workstation1.yak-bebop.ts.net deleted",
    "data": {
      "nodeID": "nFJw3SRKTM59",
      "deviceName": "alice-workstation1.yak-bebop.ts.net",
      "managedBy": "alice@example.com",
      "actor": "admin@example.com",
      "url": "https://login.tailscale.com/admin/machines/100.12.345.67"
    }
  },
  {
    "timestamp": "2022-09-27T09:51:46.512946-07:00",
    "version": 1,
    "type": "policyUpdate",
    "tailnet": "example.com",
    "message": "Tailnet policy file updated",
    "data": {
      "newPolicy": "{\n\t\"acls\": [\n\t\t{\"action\": \"accept\", \"src\": [\"autogroup:member\"], \"dst\": [\"*:*\"]},\n\t],
}",
      "oldPolicy": "{\n\t\"acls\": [\n\t\t{\"action\": \"accept\", \"src\": [\"*\"], \"dst\": [\"*:*\"]},\n\t],
}",
      "url": "https://login.tailscale.com/admin/acls",
      "actor": "admin@example.com"
    }
  },
  {
    "timestamp": "2022-11-08T10:26:08.775392-08:00",
    "version": 1,
    "type": "nodeKeyExpiringInOneDay",
    "tailnet": "example.com",
    "message": "Node alice-workstation1.yak-bebop.ts.net key expiring in less than one day",
    "data": {
      "nodeID": "nFJw3SRKTM59",
      "url": "https://login.tailscale.com/admin/machines/100.12.345.67",
      "deviceName": "alice-workstation1.yak-bebop.ts.net",
      "managedBy": "alice@example.com",
      "actor": "expiring-node-key-marker",
      "expiration": "2022-11-08T18:44:46.979292Z"
    }
  },
  {
    "timestamp": "2022-11-08T10:45:08.775392-08:00",
    "version": 1,
    "type": "nodeKeyExpired",
    "tailnet": "example.com",
    "message": "Node alice-workstation1.yak-bebop.ts.net key recently expired",
    "data": {
      "nodeID": "nFJw3SRKTM59",
      "url": "https://login.tailscale.com/admin/machines/100.12.345.67",
      "deviceName": "alice-workstation1.yak-bebop.ts.net",
      "managedBy": "alice@example.com",
      "actor": "expiring-node-key-marker",
      "expiration": "2022-11-08T18:44:46.979292Z"
    }
  },
  {
    "timestamp": "2023-02-27T11:49:25.208092-08:00",
    "version": 1,
    "type": "userRoleUpdated",
    "tailnet": "example.com",
    "message": "User alice@example.com role changed",
    "data": {
      "user": "alice@example.com",
      "url": "https://login.tailscale.com/admin/users?q=alice%40example.com",
      "actor": "admin@example.com",
      "oldRoles": ["Member"],
      "newRoles": ["Member", "IT admin"]
    }
  }
]
```

--------------------------------

### Tailscale Grants with Device Posture and Via Routing

Source: https://tailscale.com/docs/features/access-control/grants/grants-via

This example illustrates advanced Tailscale routing using device posture rules and the 'via' field. It defines posture criteria for the 'eng' group to access a destination, while other members use a designated office router.

```json
{
  "postures": {
    "posture:latestMac": [
      "node:os == 'macos'",
      "node:osVersion == '13.4.0'",
      "node:tsReleaseTrack == 'stable'",
    ]
  },
  "grants": [
    {
      "src": ["group:eng"],
      "srcPosture": ["posture:latestMac"],
      "dst": ["192.0.2.0/24"],
      "ip": ["*"]
    },
    {
      "src": ["autogroup:member"],
      "dst": ["192.0.2.0/24"],
      "via": ["tag:office-router"],
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Create IP Set with Subnets and Exclusions

Source: https://tailscale.com/docs/features/tailnet-policy-file/ip-sets

Demonstrates creating an IP set that includes multiple subnets while excluding a specific IP address. This allows for granular control over network access.

```json
"ipsets": {
  "ipset:prod": [
    "add 192.0.2.0/24",
    "add 2001:db8::/32",
    "add 198.51.100.0/24",
    "add 203.0.113.0/24",
    "remove 192.0.2.33",
  ],
}
```

--------------------------------

### Receive Files with Tailscale CLI

Source: https://tailscale.com/docs/features/taildrop?tab=linux

Use the `tailscale file get` command to receive files on a device within your Tailscale network. Specify the directory where you want to save the received files. Note that `tailscaled` runs as root, so you might need `sudo` to access the received files.

```bash
sudo tailscale file get .

# Where '.' can be any directory to copy files to.
```

--------------------------------

### Enable Tailscale Subnet Router and Assign Gateway Tag

Source: https://tailscale.com/docs/solutions/protect-postgresql-unencrypted-macbooks

Configures a Linux server to act as a Tailscale subnet router and assigns it the `tag:db-gateway`. This command advertises the specified subnet range, enabling the server to forward PostgreSQL traffic to production databases and allowing it to be used as a monitoring gateway.

```bash
sudo tailscale up --advertise-routes=<subnet-range> --advertise-tags=tag:db-gateway
```

--------------------------------

### Create Google Cloud Service Account for Log Streaming

Source: https://tailscale.com/docs/features/logging/log-streaming?tab=google+cloud+storage

This snippet demonstrates the command to create a Google Cloud service account. This account is used by Tailscale to upload logs to a GCS bucket. It's recommended to assign the 'storage.objectCreator' role to this service account.

```bash
gcloud iam service-accounts create <tailnet-uploader> \
  --display-name "Tailscale Uploader Account"
```

--------------------------------

### Allow Subnet Traffic with Tailscale Access Control Policies (JSON)

Source: https://tailscale.com/docs/features/site-to-site

Define access rules in the tailnet policy file's `grants` section to permit traffic between subnets. This JSON example allows all traffic in both directions between two specified subnets.

```json
{
  "grants": [
    {
      "src": [ <first-subnet-CIDR> ],
      "dst": [ <second-subnet-CIDR> ],
      "ip": ["*"]
    },
    {
      "src": [ <second-subnet-CIDR> ],
      "dst": [ <first-subnet-CIDR> ],
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Go Test File Imports for Tailscale Integration

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This Go code snippet declares the package and imports necessary libraries for Tailscale integration tests. It includes standard Go testing, networking, and HTTP packages, along with the tailscale.com/tsnet package for creating ephemeral Tailscale nodes.

```go
package main

import (
 "context"
 "fmt"
 "io"
 "net"
 "net/http"
 "os"
 "strings"
 "testing"
 "time"

 "tailscale.com/tsnet"
)

```

--------------------------------

### Enabling Route Acceptance on Linux

Source: https://tailscale.com/docs/reference/route-injection

This command enables the acceptance of advertised routes on a Tailscale client running Linux. This is a necessary step if the 'RouteAll' preference is false and you want the client to use subnet routes.

```bash
tailscale set --accept-routes

```

--------------------------------

### Tailscale Log Streaming Events (SIEM)

Source: https://tailscale.com/docs/reference/deployment-checklist

Stream configuration and network flow logs to a SIEM system for monitoring and alerting. This snippet shows example JSON payloads for events related to settings changes made through the Tailscale admin console, including create, update, and delete actions.

```json
// Other fields omitted for brevity
{
  "action": "CREATE",
  "origin": "ADMIN_CONSOLE",
  // ...
},
{
  "action": "UPDATE",
  "origin": "ADMIN_CONSOLE",
  // ...
},
{
  "action": "DELETE",
  "origin": "ADMIN_CONSOLE",
  // ...
}
```

--------------------------------

### Manage Multiple tsnet Servers

Source: https://tailscale.com/docs/reference/tsnet-server-api

Demonstrates how to manage multiple tsnet.Server instances within a single OS process. Each server requires a unique data directory and can be configured with hostname, auth key, and ephemeral settings.

```go
baseDir := "/data"
var servers []*tsnet.Server
for _, hostname := range []string{"ichika", "nino", "miku", "yotsuba", "itsuki"} {
    os.MkdirAll(filepath.Join(baseDir, hostname), 0700)
    srv := &tsnet.Server{
        Hostname: hostname,
        AuthKey: os.Getenv("TS_AUTHKEY"),
        Ephemeral: true,
        Dir: filepath.Join(baseDir, hostname),
    }
    if err := srv.Start(); err != nil {
        log.Fatalf("can't start tsnet server: %v", err)
    }
    servers = append(servers, srv)
}
```

--------------------------------

### Configure Peer Relay with Static Endpoints (Bash)

Source: https://tailscale.com/docs/features/peer-relay

Configures a Tailscale peer relay device with a specified UDP port and advertises additional static endpoints. This is useful for devices behind NATs or load balancers, ensuring discoverability. The endpoints are provided as a comma-separated list of `ip:port` pairs.

```bash
tailscale set --relay-server-port=<port> --relay-server-static-endpoints="<ip-address-1>:<port>,<ip-address-2>:<port>"
```

--------------------------------

### Get Tailscale IP Address (Single Preferred IPv4)

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=zsh

Retrieves a single Tailscale IP address, preferring IPv4 if available. This is a convenient option when you need one IP and IPv4 is the priority.

```bash
tailscale ip --1
```

--------------------------------

### Add Node with Pre-signed Auth Key using Tailscale CLI

Source: https://tailscale.com/docs/features/tailnet-lock?tab=tailscale+admin+console

Adds a device to a locked tailnet using a pre-signed authentication key. This involves setting an environment variable with the auth key and then using the `tailscale lock sign` command to sign it. The resulting key is used to pre-approve devices.

```bash
export AUTH_KEY="tskey-auth-<XXXXCTRL-NNNNNN>"
tailscale lock sign $AUTH_KEY
```

--------------------------------

### Get Tailscale Lock Sign Command via CLI

Source: https://tailscale.com/docs/features/tailnet-lock?tab=ios

This command retrieves the necessary `tailscale lock sign` command from the CLI output. After running `tailscale lock status` on the node to be added, you can copy the generated sign command and execute it on a trusted signing node to add the new node to the tailnet.

```bash
tailscale lock status
```

```bash
tailscale lock sign nodekey:<your-node-key> tlpub:<your-tailnet-lock-key>
```

--------------------------------

### Tailscale netlogfmt: Resolve IP Addresses to User/Tags

Source: https://tailscale.com/docs/features/logging/network-flow-logs

This snippet demonstrates the `--resolve-addrs=users` flag for `netlogfmt`. This flag resolves Tailscale IP addresses to the user or tags that own the respective machines, offering insights into traffic patterns based on user or tag assignments.

```shell
# Example usage (assuming logs are piped to netlogfmt):
netlogfmt --resolve-addrs=users
```

--------------------------------

### Advertise Subnet Routes with Tailscale CLI

Source: https://tailscale.com/docs/features/subnet-routers/how-to/setup?tab=windows

This command advertises specific subnet routes for a device to act as a subnet router within a Tailscale tailnet. Ensure you replace the example subnets with your actual network subnets. This is a crucial step for enabling access to local networks through Tailscale.

```bash
tailscale set --advertise-routes=192.0.2.0/24,198.51.100.0/24
```

--------------------------------

### Wait for Tailscale Ingress Readiness

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Waits for a Kubernetes `Ingress` resource to become ready, specifically checking for the presence of a port in the load balancer status. This command is used after creating an Ingress resource to ensure it's accessible.

```bash
kubectl wait --timeout=80s  ingress nginx --for=jsonpath='{.status.loadBalancer.ingress[0].ports[0].port}'=443
```

--------------------------------

### Grant Read-Only Access to Web Interface (Grants)

Source: https://tailscale.com/docs/features/client/device-web-interface

This configuration snippet uses the newer grants syntax to achieve the same read-only access as the ACL example. It allows members of the tailnet to access port 5252 on their own devices. This syntax offers a more structured approach to defining access.

```json
{
  "grants": [
    // Allow access only to users' own web interfaces.
    {
      "src": ["autogroup:member"],
      "dst": ["autogroup:self"],
      "ip": ["5252"]
    }
  ]
}
```

--------------------------------

### Set Default ProxyClass via Environment Variable

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/customize

This snippet illustrates how to set the default ProxyClass for the Tailscale operator using the `PROXY_DEFAULT_CLASS` environment variable when installing with static manifests.

```bash
export PROXY_DEFAULT_CLASS="default-proxy-class-name"
```

--------------------------------

### Aperture Grant Types: Role and Provider

Source: https://tailscale.com/docs/features/aperture/configuration

Examples of different grant types within Aperture's `temp_grants` configuration. Role grants assign predefined roles like 'user' or 'admin'. Provider grants specify access to particular providers and models, supporting wildcards for broader or more specific permissions.

```json
{"role": "user"}
```

```json
{"role": "admin"}
```

```json
{"providers": [{"provider": "*", "model": "*"}]}
```

```json
{"providers": [{"provider": "openai", "model": "gpt-5"}]}
```

```json
{"providers": [{"provider": "anthropic", "model": "*"}]}
```

--------------------------------

### Show Databases in MongoDB Atlas

Source: https://tailscale.com/docs/solutions/create-a-secure-connection-to-mongodb-atlas

This command is executed within the mongosh prompt to list all available databases in the connected MongoDB Atlas project. It's used to verify a successful connection and confirm access to the database. The output typically shows database names and their sizes.

```mongosh
show dbs;
```

--------------------------------

### Manage Files with Tailscale Taildrop

Source: https://tailscale.com/docs/reference/tailscale-cli

Access and manage files using Tailscale's Taildrop feature. Copy files to a host using `cp` or retrieve files from the Taildrop inbox using `get`. Options include specifying alternate filenames, listing targets, and handling file conflicts.

```bash
tailscale file cp <files...> <target> [--name=<name>] [--targets] [--verbose]
tailscale file get <target-directory> [--conflict=<behavior>] [--loop] [--verbose] [--wait]

```

--------------------------------

### Match Host Users with Login Emails for SSH Access

Source: https://tailscale.com/docs/reference/syntax/policy-file

This policy allows any Tailnet member in the 'example.com' domain to SSH into production devices tagged 'tag:prod'. It maps login emails to host usernames using the 'localpart' directive.

```json
{
  "grants": [
    {
      "src": ["user:*@example.com"],
      "dst": ["tag:prod"],
      "ip": ["*"]
    }
  ],
  "ssh": [
    {
      "action": "accept",
      "src": ["user:*@example.com"],
      "dst": ["tag:prod"],
      "users": ["localpart:*@example.com"]
    }
  ]
}
```

--------------------------------

### iOS/tvOS Tailscale VPN Configuration Profile (.mobileconfig)

Source: https://tailscale.com/docs/integrations/mdm/ios

This XML defines a configuration profile for Tailscale VPN on iOS and tvOS. It specifies VPN type, subtype, and provider bundle identifier. For tvOS, the ProviderBundleIdentifier needs adjustment. This profile is intended to be installed before the Tailscale app launches.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>PayloadDisplayName</key>
  <string>Tailscale iOS VPN Configuration Profile</string>
  <key>PayloadType</key>
  <string>Configuration</string>
  <key>PayloadVersion</key>
  <integer>1</integer>
  <key>PayloadIdentifier</key>
  <string>com.your-company-name.tailscale.797d4461-837c-4f5a-b18e-7e300a057020</string>
  <key>PayloadUUID</key>
  <string>0f451881-7ac4-4171-80fd-b55251053233</string>
  <key>PayloadContent</key>
  <array>
        <dict>
        <key>PayloadDisplayName</key>
        <string>Tailscale VPN Configuration</string>
        <key>PayloadType</key>
        <string>com.apple.vpn.managed</string>
        <key>PayloadVersion</key>
        <integer>1</integer>
        <key>PayloadIdentifier</key>
        <string>com.your-company-name.tailscale-tunnel</string>
        <key>PayloadUUID</key>
        <string>7ec957e2-b165-4d1f-9946-3a7a16ae0f9c</string>
        <key>UserDefinedName</key>
        <string>Tailscale MobileConfig</string>
        <key>VPNType</key>
        <string>VPN</string>
        <key>VPNSubType</key>
        <string>io.tailscale.ipn.ios</string>
        <key>VPN</key>
         <dict>
            <key>RemoteAddress</key>
            <string>Tailscale Mesh</string>
            <key>AuthenticationMethod</key>
            <string>Password</string>
            <key>ProviderBundleIdentifier</key>
            <string>io.tailscale.ipn.ios.network-extension</string>
        </dict>
    </dict>
  </array>
</dict>
</plist>
```

--------------------------------

### Run Database Migrations with Tailscale

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This snippet demonstrates how to run database migrations against private PostgreSQL, MySQL, or MongoDB instances using Tailscale within a GitHub Actions workflow. It sets the DATABASE_URL environment variable to connect to a private database endpoint on the tailnet and executes npm migration commands. The database remains private, with connections encrypted and authenticated via Tailscale.

```yaml
- name: Run database migrations
  run: |
    export DATABASE_URL="postgresql://user:pass@prod-db.tail-scale.ts.net:5432/my-app"
    npm run migrate:latest
    npm run migrate:status

```

--------------------------------

### Configure Advertise Routes for Cloud Environments (Tailscale CLI)

Source: https://tailscale.com/docs/reference/troubleshooting?tab=macos

This command configures Tailscale to advertise a specific private IP address range, useful for cloud environments where certain public IP ranges might conflict. It's recommended to use the `172.16.0.0/12` range instead of `172.0.0.0/8` to avoid conflicts with public IP space used by services like Google.

```bash
tailscale set --advertise-routes=172.16.0.0/12

```

--------------------------------

### Create and Listen on tsnet Network

Source: https://tailscale.com/docs/reference/tsnet-server-api

This snippet demonstrates how to create a tsnet Server, set its hostname, and then create a network listener for TCP traffic on a specific port. It returns a `net.Listener` that accepts connections from within the tailnet and includes a basic HTTP server handler.

```go
srv := new(tsnet.Server)
srv.Hostname = "tadaima"

ln, err := srv.Listen("tcp", ":80")
if err != nil {
    log.Fatal(err)
}

log.Fatal(http.Serve(ln, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hi there! Welcome to the tailnet!")
})))

```

--------------------------------

### Share Funnel Device with SSH Reverse Proxy

Source: https://tailscale.com/docs/reference/examples/funnel

Establishes an SSH reverse proxy to connect a local development server to a shared Funnel device. This allows collaborators to access your local server through the Funnel's stable DNS name. It requires SSH access and Tailscale to be running on both ends.

```bash
ssh -NT -R 8080:127.0.0.1:3000 github-hook-dev.pango-lin.ts.net
```

--------------------------------

### Troubleshoot Tailscale Device Posture Verification

Source: https://tailscale.com/docs/reference/troubleshooting/grants

This section focuses on resolving failures in device posture verification using the `srcPosture` field in Tailscale policy grants. It explains common causes such as outdated client versions, overly strict conditions, or misconfigurations. The provided example demonstrates how to define and apply posture conditions.

```json
{
  "postures": {
    "posture:latest": [
      "node:tsVersion >= '1.42.0'",
      "node:os == 'linux'"
    ]
  },
  "grants": [
    {
      "src": ["group:eng"],
      "dst": ["tag:prod"],
      "ip":  ["*"],
      "srcPosture": ["posture:latest"]
    }
  ]
}
```

--------------------------------

### Get Kubernetes Cluster Issuer using kubectl and jq

Source: https://tailscale.com/docs/features/kubernetes-operator

This command retrieves the OIDC issuer URL from your Kubernetes cluster's OpenID Connect configuration. It requires the 'jq' utility to parse the JSON output. The output is stored in the 'ISSUER' shell variable.

```bash
ISSUER="$(kubectl get --raw /.well-known/openid-configuration | jq '.issuer châssis')"
```

--------------------------------

### Create Symlinks for Combined Binary (Bash)

Source: https://tailscale.com/docs/how-to/set-up-small-tailscale

Creates symbolic links to a combined Tailscale binary, allowing it to be executed as both the 'tailscale' CLI and the 'tailscaled' daemon. Demonstrates basic usage help messages.

```bash
ln -s tailscale.combined tailscale
ln -s tailscale.combined tailscaled

./tailscale --help
./tailscaled --help
```

--------------------------------

### Enable Prometheus ServiceMonitor for Tailscale Proxies

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/customize

This configuration enables the Prometheus ServiceMonitor for proxy resources within the Kubernetes Operator. It requires the Prometheus operator to be installed and a ProxyClass to be applied with metrics and ServiceMonitor creation enabled. The ingested metrics will include labels identifying the proxy.

```yaml
apiVersion: tailscale.com/v1alpha1
kind: ProxyClass
metadata:
  name: prod
spec:
  metrics:
    enable: true
    serviceMonitor:
      enable: true

```

--------------------------------

### Connect to RDS using MySQL Shell

Source: https://tailscale.com/docs/install/cloud/aws/aws-rds

This snippet demonstrates how to connect to an AWS RDS instance from a Tailscale node using the MySQL Shell. It shows the command to initiate the connection and an example of executing a SQL query to list databases. Ensure your Tailscale network is configured to allow access to the RDS instance.

```bash
mysqlsh --uri=admin@database-2.0123456789ab.us-west-2.rds.amazonaws.com:3306
MySQL  database-2.0123456789ab.us-west-2.rds.amazonaws.com:3306 ssl  JS > \sql
Switching to SQL mode... Commands end with ;
MySQL  database-2.0123456789ab.us-west-2.rds.amazonaws.com:3306 ssl  SQL > show databases;
+--------------------+
| Database           |
+--------------------+
| demo               |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.0297 sec)
```

--------------------------------

### Access IP Behind Subnet Router via Cluster DNS - Curl Command

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-egress

Shows how cluster workloads can access a target IP address behind a subnet router using the ExternalName Service's cluster DNS name. This example uses curl to connect to the service.

```bash
curl.ts-egress.default.svc.cluster.local:8080
...

```

--------------------------------

### Disable Tailscale Key Expiry

Source: https://tailscale.com/docs/install/linux

Disables key expiry for a Tailscale device, preventing the need for re-authentication. This is useful for always-on systems but reduces security. It requires an authentication key and can optionally advertise an exit node.

```bash
sudo tailscale up --auth-key=<your-key> --advertise-exit-node
```

--------------------------------

### Obtain Tailscale IP Address

Source: https://tailscale.com/docs/install/oracle-linux/oracle-linux-8

Displays the IP address assigned to the Tailscale network interface (tailscale0) on the machine. This is used to verify the Tailscale connection and identify the node within the Tailscale network.

```bash
ip addr show tailscale0
```

--------------------------------

### Initialize Tailnet Lock with tailscale lock init

Source: https://tailscale.com/docs/features/tailnet-lock?tab=macos

The `tailscale lock init` command is used to enable Tailnet Lock. This command generates disablement secrets and establishes trusted signing nodes. Ensure nodes are running Tailscale v1.46.1 or later. The command requires at least two signing nodes.

```bash
tailscale lock init
```

--------------------------------

### Review Session Recordings from CLI

Source: https://tailscale.com/docs/features/tailscale-ssh/tailscale-ssh-session-recording

These commands demonstrate how to review Tailscale SSH session recordings from the command line. The `cat` command displays the raw recording data, while the `play` command, using the `asciinema` tool, allows for playback of the recording.

```bash
cat <session-recording.cast>
```

```bash
play <session-recording.cast>
```

--------------------------------

### Remove Signing Nodes with Tailscale Lock

Source: https://tailscale.com/docs/features/tailnet-lock?tab=ios

Removes one or more nodes from the Tailnet Lock signing configuration. This command requires the Tailnet Lock public keys of the nodes to be removed. Replace the example keys with your actual Tailnet Lock keys.

```bash
tailscale lock remove tlpub:trusted-key7 tlpub:trusted-key8
```

--------------------------------

### Create Google Service Account for Log Streaming

Source: https://tailscale.com/docs/features/logging/log-streaming?tab=google+cloud+storage

This snippet demonstrates the creation of a Google Cloud service account, which is a prerequisite for configuring log streaming to Google Cloud Storage. It also shows how to assign the recommended 'storage.objectCreator' role.

```bash
gcloud iam service-accounts create <tailnet-uploader> \
  --display-name "Tailscale Log Uploader"
```

```bash
gcloud projects add-iam-policy-binding <project> \
  --member="serviceAccount:<tailnet-uploader>@<project>.iam.gserviceaccount.com" \
  --role="roles/storage.objectCreator"
```

--------------------------------

### Review Intune Integration Status in Tailscale

Source: https://tailscale.com/docs/integrations/mdm/intune

Instructions on how to verify if the Intune integration has successfully synced device posture data. This check is performed in the Device Posture Integrations section of the Tailscale admin console.

```text
1. Go to the **Device Posture Integrations** section of the Device management page.
2. Locate the Intune integration under the **Integrations** section.
```

--------------------------------

### Get Tailscale Ingress StatefulSet using kubectl

Source: https://tailscale.com/docs/features/kubernetes-operator

This command retrieves the StatefulSet for a Tailscale Ingress resource. It uses label selectors to filter for resources managed by Tailscale, specifically for an Ingress type, with the parent resource name and namespace provided. This is useful for directly managing or inspecting the proxy pods associated with an Ingress.

```bash
$ kubectl get statefulset \
  --namespace tailscale \
  --selector="tailscale.com/managed=true,tailscale.com/parent-resource-type=ingress,tailscale.com/parent-resource=ts-ingress,tailscale.com/parent-resource-ns=prod"

```

--------------------------------

### Get Network Conditions Report with tailscale netcheck

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

The `tailscale netcheck` command provides a report on current physical network conditions to help debug connection issues. It outputs details about UDP, IPv4/IPv6 connectivity, NAT behavior, port mapping services, and DERP server latency. If fields are blank, Tailscale could not measure that property.

```bash
tailscale netcheck

```

--------------------------------

### Advertise Device as Tailscale Exit Node

Source: https://tailscale.com/docs/features/exit-nodes?tab=linux

Sets up the current device to be advertised as a Tailscale exit node. This command enables the device to act as a gateway for your Tailscale network's internet traffic.

```shell
sudo tailscale set --advertise-exit-node
```

```shell
sudo tailscale set --advertise-exit-node
sudo tailscale up
```

--------------------------------

### Disable Subnet Route Masquerading (Linux)

Source: https://tailscale.com/docs/reference/troubleshooting?tab=macos

Disable subnet route masquerading on Linux to prevent Tailscale from rewriting source IP addresses for local routes. This requires manual routing configuration for NAT traffic.

```bash
tailscale up --snat-subnet-routes=false
```

--------------------------------

### Generate Tailscale Policy Snippets with connector-gen

Source: https://tailscale.com/docs/reference/best-practices/app-connectors

This command uses the connector-gen tool to parse common providers and generate Tailscale policy file snippets and `--advertise-routes` flags. It's a Go-based tool for automating route preconfiguration.

```bash
./tool/go run ./cmd/connector-gen github
```

--------------------------------

### Prioritize LAN traffic on Linux with IP rules

Source: https://tailscale.com/docs/reference/troubleshooting?tab=macos

On Linux, this command adds an IP rule to prioritize traffic destined for a specific subnet (e.g., 192.168.2.0/24) by directing it to the main routing table, ensuring it bypasses Tailscale rules. This is useful for preventing routing conflicts with local LAN subnets. The rule has a higher priority than Tailscale's default rules. Note that this change is not persistent and requires additional configuration for boot-time application.

```bash
ip rule add to 192.168.2.0/24 priority 2500 lookup main

```

--------------------------------

### Run Go Tests Locally

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This command executes all tests within the current Go module. The `-v` flag enables verbose output, showing the status of each individual test. This is a standard command for running tests during local development and debugging.

```bash
go test -v
```

--------------------------------

### Advertise Specific IP Range with Tailscale

Source: https://tailscale.com/docs/reference/troubleshooting?tab=windows

This command allows you to advertise a specific private IP range for your Tailscale network. It's useful for scenarios like AWS where you might need to advertise a subset of private IP addresses to avoid conflicts with public IP spaces used by services like Google.

```bash
tailscale set --advertise-routes=172.16.0.0/12
```

--------------------------------

### Configure NixOS for Tailscale Service

Source: https://tailscale.com/docs/solutions/set-up-nixos-minecraft

This Nix configuration snippet enables the Tailscale service and makes the tailscale command available in the system's packages. It's a foundational step for integrating Tailscale into a NixOS environment.

```nix
{ config, pkgs, ... }:

{
  # make the tailscale command usable to users
  environment.systemPackages = [ pkgs.tailscale ];

  # enable the tailscale service
  services.tailscale.enable = true;
}

```

--------------------------------

### Revoke Tailnet Lock Keys (Initial Command)

Source: https://tailscale.com/docs/reference/tailscale-cli/lock

This is the initial command to start the process of revoking Tailnet Lock keys. It requires a list of public keys to be revoked and accepts optional flags for advanced usage.

```bash
tailscale lock revoke-keys <tlpub:key1 tlpub:key2 ...> [flags]
```

--------------------------------

### Configure Device as Peer Relay (Tailscale CLI)

Source: https://tailscale.com/docs/features/peer-relay

Configures a Tailscale device to act as a peer relay by setting a specific UDP port for relay traffic. This command is run on the device intended to be the relay server. It requires the Tailscale client to be authenticated.

```bash
tailscale set --relay-server-port=40000
```

--------------------------------

### Troubleshoot Tailscale 'via' Field Routing

Source: https://tailscale.com/docs/reference/troubleshooting/grants

This section details how to diagnose and resolve issues related to the 'via' field in Tailscale policy grants. It covers verifying 'via' target reachability, subnet router configurations, app connector setups, and exit node approvals. Commands like `tailscale status` and `tailscale ping` are essential for troubleshooting.

```json
{
  "grants": [
    {
      "src": ["group:eng"],
      "dst": ["192.0.2.0/24"],
      "ip":  ["*"],
      "via": ["tag:subnet-router"]
    }
  ]
}
```

--------------------------------

### Configure Tailscale iOS Notifications via MDM Profile

Source: https://tailscale.com/docs/integrations/mdm/ios

This XML configuration profile payload automates the allowance of push notifications for the Tailscale app on supervised iOS devices. It specifies notification settings such as enabling badges, critical alerts, and showing notifications in the notification center. This reduces user prompt fatigue during initial setup.

```xml
<dict>
  <key>NotificationSettings</key>
  <array>
    <dict>
      <key>AlertType</key>
      <integer>1</integer>
      <key>BadgesEnabled</key>
      <true/>
      <key>BundleIdentifier</key>
      <string>io.tailscale.ipn.ios</string>
      <key>CriticalAlertEnabled</key>
      <true/>
      <key>NotificationsEnabled</key>
      <true/>
      <key>ShowInNotificationCenter</key>
      <true/>
    </dict>
  </array>
  <key>PayloadDisplayName</key>
  <string>Allow Tailscale Notifications</string>
  <key>PayloadIdentifier</key>
  <string>b3dc3535-1b06-4f2d-a684-4518a6589dfe</string>
  <key>PayloadOrganization</key>
  <string>Tailscale Inc.</string>
  <key>PayloadType</key>
  <string>com.apple.notificationsettings</string>
  <key>PayloadUUID</key>
  <string>056ec734-91b7-45a3-8787-98ebf2e84025</string>
  <key>PayloadVersion</key>
  <integer>1</integer>
</dict>
```

--------------------------------

### Define Tailscale Postures with Node Attributes

Source: https://tailscale.com/docs/features/device-posture

This snippet shows how to define a posture named 'posture:latestMac' in a Tailscale policy file. It includes conditions based on the node's operating system, Tailscale release track, and client version. All conditions must be met for the posture to match.

```json
"postures": {
  "posture:latestMac": [
    "node:os IN ['macos', 'linux']",
    "node:tsReleaseTrack == 'stable'",
    "node:tsVersion >= '1.40'",
  ]
}
```

--------------------------------

### View Tailscale Open Source Licenses

Source: https://tailscale.com/docs/reference/tailscale-cli

Retrieve information about the open source licenses used by Tailscale.

```bash
tailscale licenses

```

--------------------------------

### Add mcrcon package to Nix system configuration

Source: https://tailscale.com/docs/solutions/set-up-nixos-minecraft

This snippet shows how to add the 'mcrcon' package to your system configuration alongside the 'tailscale' package using Nix. This allows for remote administration of a Minecraft server.

```nix
environment.systemPackages = with pkgs; [
  tailscale
  mcrcon
];
```

--------------------------------

### Apply Recorder Resource to Kubernetes

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/tsrecorder

Applies a Kubernetes resource definition from a YAML file. This command is used to create or update resources in a Kubernetes cluster, such as the tsrecorder's Recorder Custom Resource.

```bash
kubectl apply -f recorder.yaml

```

--------------------------------

### Get Tailscale IP Address on Linux

Source: https://tailscale.com/docs/solutions/code-on-ipad-vscode-caddy-code-server

This command retrieves the Tailscale IPv4 address of the current machine. It's a prerequisite to verify your Tailscale network connectivity before setting up other services.

```bash
tailscale ip --4

```

--------------------------------

### List Tailscale Accounts using CLI

Source: https://tailscale.com/docs/features/client/fast-user-switching?tab=android

Lists all available Tailscale accounts on the device, indicating the currently active account with an asterisk. This command is useful for verifying account status before or after operations.

```bash
tailscale switch --list
```

--------------------------------

### Tailscale Access Rule with Default Source Posture

Source: https://tailscale.com/docs/features/device-posture

Demonstrates an access rule that inherits the default source posture because it lacks a specific posture condition. This rule grants access to 'tag:intranet' from members of 'autogroup:member'.

```json
{
  "src": ["autogroup:member"],
  "dst": ["tag:intranet"],
  "ip": ["*"]
}
```

--------------------------------

### Allow Alice SSH Access to Shared Development Devices

Source: https://tailscale.com/docs/reference/syntax/policy-file

This SSH rule permits 'alice@example.com' to access devices tagged 'tag:dev' that have been shared with her. It specifies the source, destination, and allowed users for the connection.

```json
{
  "ssh": [
    {
      "action": "accept",
      "src": ["alice@example.com"],
      "dst": ["tag:dev"],
      "users": ["root", "alice"]
    }
  ]
}
```

--------------------------------

### Automatic Cloud Token Discovery with Tailscale

Source: https://tailscale.com/docs/features/workload-identity-federation

This snippet illustrates automatic cloud token discovery and exchange for registering a node with Tailscale. It uses `tailscale up` with `--client-id` and `--audience` flags, enabling workload identity federation without manual credential management.

```shell
tailscale up --client-id=${CLIENT_ID} --audience=${AUDIENCE} --advertise-tags=tag:ci
```

--------------------------------

### Move HTML file to the website directory

Source: https://tailscale.com/docs/features/tailscale-funnel/how-to/host-websites

This command moves a locally created HTML file into the designated website directory. It assumes the HTML file is in the user's home directory and relocates it to the '/tmp/test-funnel' subdirectory.

```bash
mv /home/amelie/index.html /tmp/test-funnel

```

--------------------------------

### Define Tag Owners in Tailscale Policy

Source: https://tailscale.com/docs/solutions/migrate-legacy-vpn-tailscale

This JSON snippet defines which users or groups are allowed to assign specific tags to devices within a Tailscale network. In this example, 'autogroup:admin' is designated as the owner for 'tag:engineering', meaning only administrators can apply this tag.

```json
// All employees can access devices tagged with tag:internal

  {

    "src": ["autogroup:member"],

    "dst": ["tag:internal"],

    "ip":  ["*"]

  }

],


  "tagOwners": {



    // Users who are Tailscale admins can apply the tag tag:engineering



    "tag:engineering": ["autogroup:admin"],


```

--------------------------------

### Create a Funnel using Tailscale CLI

Source: https://tailscale.com/docs/features/tailscale-funnel

This command enables sharing a local service (e.g., running on port 3000) to the public internet via Tailscale Funnel. It provides a public HTTPS URL and displays the local proxy target. Press Ctrl+C to stop.

```bash
tailscale funnel 3000
Available on the internet:
https://amelie-workstation.pango-lin.ts.net

|-- / proxy http://127.0.0.1:3000

Press Ctrl+C to exit.

```

--------------------------------

### Authenticate Device with Specific Tags using CLI

Source: https://tailscale.com/docs/features/tags

Authenticates a device using an auth key and applies specific tags during the process. This is useful for deployment systems that need to tag devices with appropriate infrastructure tags for access control.

```bash
sudo tailscale up --auth-key=<key-1> --advertise-tags=tag:prod-2

```

--------------------------------

### Configure Tailscale CLI Tab Completion

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

The Tailscale CLI supports tab completion for commands, flags, and arguments. Use the `completion` command followed by your shell to set this up. Follow the on-screen instructions to load the completions.

```bash
tailscale completion <shell> [--flags] [--descs]

```

--------------------------------

### Enable Route Discovery on Linux

Source: https://tailscale.com/docs/features/subnet-routers?tab=android

Configures Linux devices to automatically discover and accept new subnet routes advertised by Tailscale subnet routers. This command ensures seamless connectivity to resources behind the subnet router.

```bash
sudo tailscale set --accept-routes

```

--------------------------------

### Secrets Management Access Control (Tailscale Policy)

Source: https://tailscale.com/docs/features/access-control/grants/grants-app-capabilities

Defines access permissions for secrets management using the `tailscale.com/cap/secrets` capability. This allows specific groups to perform actions like 'get' or 'put' on defined secret paths.

```json
{
  "grants": [
    {
      "src": ["group:developers"],
      "dst": ["tag:app-servers"],
      "app": {
        "tailscale.com/cap/secrets": [
          {"action": ["get", "info"], "secret": ["dev/*"]}
        ]
      }
    },
    {
      "src": ["group:security"],
      "dst": ["tag:app-servers"],
      "app": {
        "tailscale.com/cap/secrets": [
          {"action": ["get", "put", "delete"], "secret": ["prod/api-keys/*"]}
        ]
      }
    }
  ]
}
```

--------------------------------

### Set Up Tailscale Auto-Connection with Systemd on NixOS

Source: https://tailscale.com/docs/solutions/set-up-nixos-minecraft

This Nix configuration sets up a systemd oneshot job to automatically authenticate and connect to Tailscale using a provided auth key. It ensures Tailscale is running before attempting to connect and checks the current status to avoid redundant connections.

```nix
# ...

# create a oneshot job to authenticate to Tailscale
systemd.services.tailscale-autoconnect = {
  description = "Automatic connection to Tailscale";

  # make sure tailscale is running before trying to connect to tailscale
  after = [ "network-pre.target" "tailscale.service" ];
  wants = [ "network-pre.target" "tailscale.service" ];
  wantedBy = [ "multi-user.target" ];

  # set this service as a oneshot job
  serviceConfig.Type = "oneshot";

  # have the job run this shell script
  script = with pkgs; ''
    # wait for tailscaled to settle
    sleep 2

    # check if we are already authenticated to tailscale
    status="$(${tailscale}/bin/tailscale status -json | ${jq}/bin/jq -r .BackendState)"
    if [ $status = "Running" ]; then # if so, then do nothing
      exit 0
    fi

    # otherwise authenticate with tailscale
    ${tailscale}/bin/tailscale up -authkey <your-auth-key>
  '';
};

```

--------------------------------

### Verify Service Host Configuration with `tailscale serve status`

Source: https://tailscale.com/docs/features/tailscale-services

Checks the current status and configuration of Tailscale Service hosts. This command is used to verify that a service host has been correctly configured and is advertising its endpoints.

```bash
tailscale serve status --json

```

--------------------------------

### Disable Tailscale Logging

Source: https://tailscale.com/docs/install/linux

Disables the sending of logs to Tailscale servers. This is done by editing the `/etc/default/tailscaled` configuration file or by adding a flag to the TAILSCALED_EXTRA_ARGS variable. Disabling logs may affect Tailscale's ability to provide technical support.

```bash
TS_NO_LOGS_NO_SUPPORT=true

```

```bash
--no-logs-no-support

```

--------------------------------

### Allow UDP Port for Peer-to-Peer Connections (Ubuntu)

Source: https://tailscale.com/docs/reference/faq/firewall-ports

Configure the Uncomplicated Firewall (ufw) on Ubuntu to allow incoming UDP traffic on port 41641. This can help establish direct peer-to-peer connections between Tailscale devices, bypassing relays.

```bash
sudo ufw allow 41641/udp
```

--------------------------------

### Configure Tailscale Serve for Reverse Proxy

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

To use `tailscale serve` as a reverse proxy, provide the location of the local backend service as the `<target>`. This can be a port number, a partial URL, or a full URL. Note that only `http://127.0.0.1` is supported for proxies.

```bash
tailscale serve localhost:3000
tailscale serve --http=80 localhost:3000
```

--------------------------------

### Tailscale Policy: Allow All Traffic

Source: https://tailscale.com/docs/reference/examples/grants

This policy allows all devices and users within a Tailscale tailnet to communicate freely with each other. It uses wildcards for source, destination, and IP protocols, making it the most permissive default policy. This is suitable for trusted environments or as a starting point for policy configuration.

```json
{
  "grants": [
    {
      "src": ["*"],
      "dst": ["*"],
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Go tsnet Application: Helper Function for Hostname Formatting

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

Provides a helper function 'firstLabel' to extract the first label from a domain name, used for formatting the device name in the HTTP response. This simplifies displaying the computed hostname.

```go
func firstLabel(s string) string {
    s, _, _ = strings.Cut(s, ".")
    return s
}

```

--------------------------------

### Remove and Reconfigure Endpoint Protocol with tailscale serve

Source: https://tailscale.com/docs/features/tailscale-services

Demonstrates how to change the protocol for an existing endpoint. It first removes the current HTTPS configuration for a port and then adds a new HTTP configuration. This is useful for switching between protocols or updating target resources.

```bash
tailscale serve --service="svc:my-web-app" --https=443 off
tailscale serve --service="svc:my-web-app" --http=443 http://localhost:8081
```

--------------------------------

### Disable IPv4 for Specific Targets (Tailscale ACL)

Source: https://tailscale.com/docs/reference/troubleshooting?tab=macos

This JSON snippet demonstrates how to selectively disable IPv4 for specific targets within your Tailscale network by applying the `disable-ipv4` node attribute. This is useful for devices or groups of devices that should only use IPv6.

```json
{
  "nodeAttrs": [
    {
      "target": ["tag:lab-foo"],
      "attr":   ["disable-ipv4"],
    },
  ]
}

```

--------------------------------

### Enable LAN Access with Mullvad Exit Node in Tailscale CLI

Source: https://tailscale.com/docs/features/exit-nodes/mullvad-exit-nodes?tab=linux

This command configures a device to use a Mullvad exit node and enables direct access to the local network while routing traffic through the exit node. Use the `--exit-node-allow-lan-access=true` flag to activate this feature, which can simplify DNS configuration for local network access.

```bash
sudo tailscale set --exit-node=<exit-node-name-or-ip> --exit-node-allow-lan-access=true
```

--------------------------------

### List Possible Tailscale File Copy Targets

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=windows

Lists the possible targets for the `tailscale file cp` command. This helps users identify where they can copy files to within their Tailscale network.

```bash
tailscale file cp --targets
```

--------------------------------

### Configure Tailscale VPN On-Demand Rules (XML)

Source: https://tailscale.com/docs/integrations/mdm/mac

This XML configuration defines rules for Tailscale VPN on-demand behavior. It specifies conditions for connecting or disconnecting the VPN based on network interface type and SSID. This is typically used within an Apple Configuration Profile for MDM deployment.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>PayloadDisplayName</key>
  <string>Tailscale VPN Configuration Profile</string>
  <key>PayloadType</key>
  <string>Configuration</string>
  <key>PayloadVersion</key>
  <integer>1</integer>
  <key>PayloadIdentifier</key>
  <string>com.your-company-name.tailscale.797d4461-837c-4f5a-b18e-7e300a057018</string>
  <key>PayloadUUID</key>
  <string>0f451881-7ac4-4171-80fd-b55251053231</string>
  <key>PayloadContent</key>
  <array>
        <dict>
        <key>PayloadDisplayName</key>
        <string>Tailscale VPN Configuration</string>
        <key>PayloadType</key>
        <string>com.apple.vpn.managed</string>
        <key>PayloadVersion</key>
        <integer>1</integer>
        <key>PayloadIdentifier</key>
        <string>com.your-company-name.tailscale-tunnel</string>
        <key>PayloadUUID</key>
        <string>7ec957e2-b165-4d1f-9946-3a7a16ae0f9b</string>
        <key>UserDefinedName</key>
        <string>Tailscale MobileConfig</string>
        <key>VPNType</key>
        <string>VPN</string>
        <key>VPNSubType</key>
        <string>io.tailscale.ipn.macos</string>
        <key>VPN</key>
         <dict>
            <key>RemoteAddress</key>
            <string>Tailscale Mesh</string>
            <key>AuthenticationMethod</key>
            <string>Password</string>
            <key>ProviderBundleIdentifier</key>
            <string>io.tailscale.ipn.macos.network-extension</string>
            <key>OnDemandEnabled</key>
            <integer>1</integer>
            <key>OnDemandRules</key>
            <array>
              <dict>
                <key>InterfaceTypeMatch</key>
                <string>WiFi</string>
                <key>SSIDMatch</key>
                <string>TailAndScales</string>
                <key>Action</key>
                <string>Disconnect</string>
              </dict>
              <dict>
                <key>InterfaceTypeMatch</key>
                <string>WiFi</string>
                <key>Action</key>
                <string>Connect</string>
              </dict>
              <dict>
                <key>InterfaceTypeMatch</key>
                <string>Cellular</string>
                <key>Action</key>
                <string>Connect</string>
              </dict>
            </array>
        </dict>
    </dict>
  </array>
</dict>
</plist>
```

--------------------------------

### Add and Commit Changes to Git Repository

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

These commands stage all changes in the current directory using `git add .`, commit them with a specified message using `git commit -m "Add tshello test"`, and then push the changes to the `main` branch of the remote repository using `git push -u origin main`. This is a typical workflow for saving and sharing code changes.

```bash
git add .
git commit -m "Add tshello test"
git push -u origin main
```

--------------------------------

### Connect to Tailscale in GitHub Actions with Caching

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This GitHub Actions workflow snippet shows how to connect to Tailscale, enabling caching for the Tailscale binary. It uses the `tailscale/github-action@v4` action, configuring OAuth credentials, tags, and pinning the version for consistency. Enabling `use-cache: 'true'` optimizes workflow performance by reducing download times for the Tailscale binary.

```yaml
- name: Connect to Tailscale
  uses: tailscale/github-action@v4
  with:
    oauth-client-id: ${{ secrets.TS_OAUTH_CLIENT_ID }}
    oauth-secret: ${{ secrets.TS_OAUTH_SECRET }}
    tags: tag:ci
    version: '1.76.1'  # Pin version for consistency
    use-cache: 'true' # Enable caching

```

--------------------------------

### Connect to MongoDB Atlas Database using mongosh

Source: https://tailscale.com/docs/solutions/create-a-secure-connection-to-mongodb-atlas

This command initiates a connection to a MongoDB Atlas database using the mongosh client. It requires the cluster URI, API version, and database username. Successful execution will open the mongosh prompt, allowing database interaction. Ensure placeholders are replaced with actual values.

```bash
mongosh "mongodb+srv://<cluster-name>.<hash>.mongodb.net/"
  --apiVersion 1 
  --username <database-user-name>
```

--------------------------------

### Enable Tailscale Client and Configure DNS on Raspberry Pi

Source: https://tailscale.com/docs/solutions/block-ads-all-devices-anywhere-using-raspberry-pi

This command enables the Tailscale client and configures it to not use the tailnet's DNS settings, as the Raspberry Pi will act as the DNS server. This is crucial for ad-blocking configurations. It requires root privileges.

```bash
sudo tailscale up --accept-dns=false
```

--------------------------------

### Configure Codex with Aperture (TOML)

Source: https://tailscale.com/docs/features/aperture

Sets up Codex to use Aperture by configuring the `base_url` in its `config.toml` file and specifying a Codex-compatible model. It also includes settings for `model_provider`, `model_reasoning_effort`, and `wire_api` to ensure compatibility with the OpenAI Responses API format.

```toml
model = "gpt-5.2-codex"
model_provider = "llm-ai-ts-net"
model_reasoning_effort = "high"

[model_providers.llm-ai-ts-net]
name = "Tailscale AI Gateway"
base_url = "http://ai/v1" # Required: Aperture URL

# Required to use "gpt-5-codex" model
wire_api = "responses"
```

--------------------------------

### Customize Internet Access with IP Sets and Subnet Routers

Source: https://tailscale.com/docs/reference/examples/grants

Creates custom internet access rules using IP sets and routes traffic through specific subnet routers. This allows granular control over external resource access by defining custom subsets of internet addresses and applying different routing rules.

```json
{
  "ipsets": {
    "ipset:internet": [
      "add autogroup:internet",
      "remove ipset:cdn-edge",
      "remove ipset:partner-net"
    ],
    "ipset:cdn-edge": ["198.51.100.6", "198.51.100.7", "198.51.100.13", "198.51.100.14"],
    "ipset:partner-net": ["203.0.113.0/24"]
  },
  "grants": [
    {
      "src": ["group:sea"],
      "dst": ["ipset:internet"],
      "ip": ["*"],
      "via": ["tag:officerouter-sea"]
    },
    {
      "src": ["group:lon"],
      "dst": ["ipset:internet"],
      "ip": ["*"],
      "via": ["tag:officerouter-lon"]
    }
  ]
}
```

--------------------------------

### Enable Network Flow Logs

Source: https://tailscale.com/docs/features/logging/network-flow-logs

Instructions for enabling network flow logs. Requires Owner, Admin, Network admin, or IT admin privileges.

```APIDOC
## Enable Network Flow Logs

Network flow logs are disabled by default.

You must be an Owner, Admin, Network admin, or IT admin of a tailnet to enable Network flow logs.

1.  Open the Network flow logs page of the admin console.
2.  Select **Start logging**.
3.  In the **Start logging network flows** dialog, select **Start logging**.
```

--------------------------------

### Register Node with Client ID and ID Token

Source: https://tailscale.com/docs/features/workload-identity-federation?tab=google+cloud

Registers a new node with Tailscale using a client ID and an OIDC ID token. Supports optional parameters like ephemeral and preauthorized. Requires Tailscale v1.90.1 or later.

```bash
tailscale up --client-id=${CLIENT_ID} --id-token=${IDENTITY_TOKEN} --advertise-tags=tag:ci
```

```bash
tailscale up --client-id='${CLIENT_ID}?ephemeral=false&preauthorized=true' --id-token=${IDENTITY_TOKEN} --advertise-tags=tag:ci
```

--------------------------------

### Serve Content with Insecure Certificates using Tailscale Serve

Source: https://tailscale.com/docs/reference/tailscale-cli/serve

If running a local web server with HTTPS and an invalid or self-signed certificate, use the `https+insecure` pseudo-protocol for your `tailscale serve` command. This bypasses certificate validation.

```bash
tailscale serve https+insecure:<target>
```

--------------------------------

### Authenticate tailscale-client-go-v2 with Workload Identity

Source: https://tailscale.com/docs/features/workload-identity-federation

Illustrates how to authenticate `tailscale-client-go-v2` using workload identity. This is achieved by configuring the `tailscale.Client` with a `ClientID` and an `IDTokenFunc` that retrieves the identity token.

```Go
package main

import (
	"context"
	"os"

	"tailscale.com/client/tailscale/v2"
)

func main() {
	client := &tailscale.Client{
		Tailnet: os.Getenv("TAILSCALE_TAILNET"),
		Auth: &tailscale.IdentityFederation{
			ClientID: os.Getenv("TAILSCALE_OAUTH_CLIENT_ID"),
			IDTokenFunc: func() (string, error) {
				return os.Getenv("IDENTITY_TOKEN"), nil
            },
		},
	}

	// Example API call

devices, err := client.Devices().List(context.Background())
}

```

--------------------------------

### Configure GitHub Preset App in Tailscale Policy

Source: https://tailscale.com/docs/features/app-connectors/how-to/setup

This snippet demonstrates how to configure the GitHub preset app within a Tailscale tailnet policy file. It specifies the target for the rule, the name of the app connector, the tags associated with the connectors, and the `presetAppID` for GitHub. This configuration allows Tailscale to automatically manage domains and routes for GitHub.

```json
{
  "nodeAttrs": [
    {
      "target": ["*"],
      "app": {
        "tailscale.com/app-connectors": [
          {
            "name": "github app",
            "connectors": ["tag:code", "tag:ci-cd"],
            "presetAppID": "github"
          }
        ]
      }
    }
  ]
}
```

--------------------------------

### Get Tailscale IP Address (CLI)

Source: https://tailscale.com/docs/concepts/ip-and-dns-addresses?tab=linux

Retrieve the Tailscale IP address for a node using the `tailscale ip` command. The `--4` flag can be used to specifically request an IPv4 address. This command is available on Tailscale v1.8 and later.

```bash
tailscale ip --4
```

--------------------------------

### Deploy Tailscale Subnet Router for Kubernetes Cluster

Source: https://tailscale.com/docs/kubernetes

This section outlines the steps to deploy a Tailscale subnet router, enabling access to the entire Kubernetes cluster network over Tailscale. It requires identifying and exporting the cluster's Service and Pod CIDRs, deploying the subnet-router pod, and ensuring route enablement in the Tailscale admin console and on client machines.

```bash
SERVICE_CIDR=10.20.0.0/16
POD_CIDR=10.42.0.0/15
export TS_ROUTES=$SERVICE_CIDR,$POD_CIDR

make subnet-router | kubectl apply -f-
# If not using an auth key, authenticate by grabbing the Login URL here:
kubectl logs subnet-router

# Check connectivity to a Service IP or Pod IP
INTERNAL_IP="$(kubectl get svc <SVC_NAME> -o=jsonpath='{.spec.clusterIP}')"
# or, the Pod IP
# INTERNAL_IP="$(kubectl get po <POD_NAME> -o=jsonpath='{.status.podIP}')"
INTERNAL_PORT=8080
curl http://$INTERNAL_IP:$INTERNAL_PORT
```

--------------------------------

### Tailscale netlogfmt: API Key and Tailnet Name for Older Clients

Source: https://tailscale.com/docs/features/logging/network-flow-logs

This snippet highlights the requirement to use `--api-key` and `--tailnet-name` flags when resolving addresses with `netlogfmt` for Tailscale clients older than v1.92. These parameters are necessary to authenticate with the Tailscale API and identify the specific tailnet.

```shell
# Example usage with API key and tailnet name:
netlogfmt --resolve-addrs=names --api-key=$ACCESS_TOKEN --tailnet-name=$TAILNET
```

--------------------------------

### systemd Service File for Minecraft Server

Source: https://tailscale.com/docs/solutions/set-up-minecraft

This is the content for the `minecraft.service` systemd unit file. It defines how the Minecraft server should be managed as a service, including user, working directory, start/stop commands, and restart policies.

```systemd
[Unit]
Description=Minecraft Service
Wants=network.target
After=network.target

[Service]
User=minecraft
Group=minecraft

Type=forking

ProtectHome=true
ProtectSystem=full
PrivateDevices=true
NoNewPrivileges=true
InaccessibleDirectories=/root /sys /srv /media -/lost+found
ReadWriteDirectories=/opt/minecraft
WorkingDirectory=/opt/minecraft
ExecStart=/opt/minecraft/start.sh
ExecStop=/opt/minecraft/stop.sh
TimeoutStopSec=20
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

--------------------------------

### Configure API Server Proxy Environment Variable (Static Manifests)

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/api-server-proxy

Sets the APISERVER_PROXY environment variable to 'noauth' within the Tailscale Kubernetes Operator deployment manifest when using static manifests for installation.

```yaml
name: APISERVER_PROXY
value: "noauth"

```

--------------------------------

### Create Outgoing Connections with Server.Dial

Source: https://tailscale.com/docs/reference/tsnet-server-api

Enables creating outgoing network connections to nodes within your tailnet. The resulting connections can be used like any standard Go network connection. MagicDNS names can be used if enabled. This method implicitly calls Start if not already invoked.

```go
srv := new(tsnet.Server)
srv.Hostname = "gaga"

conn, err := srv.Dial(r.Context(), "tcp", "yourmachine:80")
if err != nil {
    log.Fatal(err)
}


```

--------------------------------

### Serve Local Content with tailscale serve

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

The `tailscale serve` command allows you to serve content and local servers from your Tailscale node to your tailnet. It supports subcommands like `status` and `reset` for managing the serving configuration. For public internet sharing, the `funnel` command should be used.

```bash
tailscale serve <target>
tailscale serve <subcommand> [flags] <args>

```

--------------------------------

### Go tsnet Application: Package and Imports

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

Defines the main package and imports necessary Go libraries for networking, HTTP, TLS, and the tailscale.com/tsnet package. This forms the foundation of the tsnet application.

```go
// This program demonstrates how to use tsnet as a library.
package main

import (
    "crypto/tls"
    "flag"
    "fmt"
    "html"
    "log"
    "net/http"
    "strings"

    "tailscale.com/tsnet"
)
```

--------------------------------

### Create GitHub Actions Workflow File

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This command creates a new YAML file for a GitHub Actions workflow. The filename should follow the convention '.github/workflows/<name>.yml', where '<name>' is a descriptive name for the workflow.

```bash
touch .github/workflows/<name>.yml
```

--------------------------------

### Prevent DNS Rebinding Attacks with Host Header

Source: https://tailscale.com/docs/reference/best-practices/security

This snippet demonstrates how to set the Host header in an HTTP request to prevent DNS rebinding attacks on HTTP services within a Tailscale network. It shows examples using a standard domain and a MagicDNS fully qualified domain name.

```http
GET /resource HTTP/1.1
Host: www.example.com


```

```http
GET /resource HTTP/1.1
Host: webserver.example2.ts.net


```

--------------------------------

### Define macOS Device Encryption Posture (Jamf Pro)

Source: https://tailscale.com/docs/solutions/protect-postgresql-unencrypted-macbooks

This snippet defines a device posture policy for macOS devices using Jamf Pro integration. It checks for macOS version, Tailscale release track, and FileVault encryption status. Devices must meet all criteria to be compliant.

```json
"postures": {
  "posture:encryptedMacBook": [
    "node:os == 'macos'",
    "node:osVersion >= '13.4.0'",
    "node:tsReleaseTrack == 'stable'",
    "jamfPro:fileVaultStatus == 'ALL_ENCRYPTED'"
  ]
}
```

--------------------------------

### Connect to Tailscale with tailscale up

Source: https://tailscale.com/docs/reference/tailscale-cli/up

The `tailscale up` command connects your device to Tailscale and handles authentication. Flags can be used to configure its behavior, but they are not persistent and must be re-specified with each command. To clear previous flag settings, pass the flag with an empty argument.

```bash
tailscale up [flags]

# Connects with `tag:server`
tailscale up --advertise-tags=tag:server
```

--------------------------------

### Enable Port Forwarding on Linux (sysctl.d)

Source: https://tailscale.com/docs/features/exit-nodes?tab=linux

Enables IPv4 and IPv6 forwarding on Linux systems with a `/etc/sysctl.d` directory by modifying the sysctl configuration. This is a prerequisite for using a Linux device as a Tailscale exit node.

```shell
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

--------------------------------

### Print App Connector Routes

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Displays the current status of app connector routes. By default, it shows configured domains and learned routes. Flags allow printing all learned routes, a map of learned domains, or the total number of advertised routes.

```bash
tailscale appc-routes [flags]

```

--------------------------------

### Restart Tailscale Client using CLI Commands

Source: https://tailscale.com/docs/reference/messages/client/invalid-packet-filter

These commands are used to restart the Tailscale client from the command-line interface. This can help resolve issues by re-initializing the client and its connection to the coordination server. Ensure you have the Tailscale CLI installed and accessible in your terminal.

```bash
tailscale down
tailscale up
```

--------------------------------

### Manage Tailscale Systray Client on Linux

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Manages the Tailscale systray client for Linux, which provides a graphical interface for network status and control. Supports systemd for startup scripts.

```bash
tailscale configure systray --enable-startup=systemd
```

--------------------------------

### Connect to Tailscale Device (Bash)

Source: https://tailscale.com/docs/features/tsnet/how-to/create-basic-tsnet-app

Connects to a Tailscale device using curl to retrieve its HTTP response. This demonstrates accessing the service running on the Tailscale network.

```bash
curl http://tshello
```

--------------------------------

### Provision Let's Encrypt Certificates with Tailscale CLI

Source: https://tailscale.com/docs/how-to/set-up-https-certificates

Automatically request and provision TLS certificates for a machine using Tailscale's CLI tool. This process involves DNS TXT record challenges with Let's Encrypt. The private keys are stored locally and never shared with Tailscale. Note that manual renewal is required for file-based certificates.

```bash
sudo tailscale cert
```

--------------------------------

### Check Node Attributes via Tailscale API

Source: https://tailscale.com/docs/integrations/mdm/intune

Demonstrates how to use the Tailscale API to inspect device attributes after setting up the Intune integration. This allows for programmatic confirmation that Intune data is being written to Tailscale node attributes.

```json
{
  "postures": {
    "posture:trusted": [
      "intune:complianceState == 'compliant'",
      "intune:isSupervised == true"
    ]
  },
  "grants": [
    {
      "src": ["autogroup:member"],
      "dst": ["tag:production"],
      "ip": ["*"],
      "srcPosture": ["posture:trusted"]
    }
  ]
}
```

--------------------------------

### Configure Tailscale Session Recording for Kubernetes

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/session-recording

This configuration sets up session recording for kubectl sessions to API server proxies. It specifies the source (engineering group), destination (k8s-operator tag), and the trecorder instance. It enforces recording and sets the failure policy to 'fail closed'.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": ["group:engineering"],
      "dst": ["tag:k8s-operator:443"]
    }
  ],
  "grants": [
    {
      "src": ["group:engineering"],
      "dst": ["tag:k8s-operator"],
      "app": {
        "tailscale.com/cap/kubernetes": [{
          "recorder":        ["tag:tsrecorder"],
          "enforceRecorder": true
        }]
      }
    }
  ]
}
```

--------------------------------

### Capture Network Traffic with Wireshark on TUN Device

Source: https://tailscale.com/docs/reference/troubleshooting

This method involves using Wireshark directly on the network interface used by Tailscale. It requires Wireshark version 3.65 or later and may not work with userspace-networking mode. The specific interface name varies by operating system.

```bash
# Linux and Windows:
tailscale0

# macOS:
utun#
```

--------------------------------

### Format Tailscale API Network Logs with netlogfmt

Source: https://tailscale.com/docs/features/logging/network-flow-logs

This snippet shows how to pipe the output of the Tailscale API `curl` command to the `netlogfmt` Go binary. This utility formats the raw JSON log data into a more human-readable table, making it easier to analyze network traffic.

```shell
curl -u $ACCESS_TOKEN: \
  "https://api.tailscale.com/api/v2/tailnet/{$TAILNET_ID}/logging/network?start={$START}&end={$END}" \
  | go run tailscale.com/cmd/netlogfmt@latest

```

--------------------------------

### Set Operator Log Level to Debug (Helm)

Source: https://tailscale.com/docs/reference/troubleshooting/kubernetes-operator

This command upgrades or installs the Tailscale operator using Helm and sets the operator's logging level to 'debug' to enable detailed diagnostic logs. This is useful for identifying and resolving issues with the operator's functionality.

```bash
helm upgrade --install \
  operator tailscale/tailscale-operator \
  --set operatorConfig.logging=debug

```

--------------------------------

### Node Registration with OAuth

Source: https://tailscale.com/docs/features/oauth-clients

Register a new node (device) in your tailnet using OAuth credentials. This command allows specifying ephemeral status, preauthorization, and custom base URLs.

```APIDOC
## tailscale up --auth-key

### Description
Registers a new node in the Tailscale network using an OAuth client secret as an authentication key. This command supports additional parameters for controlling node behavior and API endpoint.

### Method
CLI Command

### Endpoint
N/A (CLI command)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Command Usage
```bash
tailscale up --auth-key='${OAUTH_CLIENT_SECRET}?ephemeral=false&preauthorized=true' --advertise-tags=tag:ci
```

### Parameters
- **--auth-key** (string) - Required - The OAuth client secret. Can include URL-style parameters:
  - `ephemeral` (boolean) - Register as an ephemeral node (defaults to `true`).
  - `preauthorized` (boolean) - Skip manual device approval (defaults to `false`).
  - `baseURL` (string) - Base URL for the Tailscale API (defaults to `https://api.tailscale.com`).
- **--advertise-tags** (string) - Required - Comma-separated list of tags to advertise for the node.

### Response
N/A (CLI command output)

### Response Example
N/A
```

--------------------------------

### SSH Reverse Proxy Error Message

Source: https://tailscale.com/docs/reference/examples/funnel

An error message indicating that a remote port forwarding failed when establishing an SSH reverse proxy. This typically occurs if the specified remote port on the Funnel device is already in use. It suggests an alternative port or checking existing connections.

```bash
Warning: remote port forwarding failed for listen port 8080
```

--------------------------------

### Allow Resource Access Based on Device Posture (JSON)

Source: https://tailscale.com/docs/reference/examples/grants

Controls access to resources through subnet routers based on device compliance. Ensures only compliant devices access sensitive resources. Requires defining posture checks, groups, and subnet routers.

```json
{
  "postures": {
    "posture:latestMac": [
      "node:os == 'macos'",
      "node:osVersion == '13.4.0'",
      "node:tsReleaseTrack == 'stable'"
    ]
  },
  "grants": [
    {
      "src": ["group:eng"],
      "srcPosture": ["posture:latestMac"],
      "dst": ["192.0.2.0/24"],
      "ip": ["*"]
    },
    {
      "src": ["autogroup:member"],
      "dst": ["192.0.2.0/24"],
      "via": ["tag:office-router"],
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Test firstLabel Utility Function

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This is a unit test for the `firstLabel` utility function, which extracts the first label from a domain name. It uses a table-driven approach to test various input formats, including standard domain names, subdomains, localhost, empty strings, and single labels. This test does not require network access or authentication.

```go
func TestFirstLabel(t *testing.T) {
 tests := []struct {
  input    string
  expected string
 }{
  {"example.com", "example"},
  {"sub.example.com", "sub"},
  {"localhost", "localhost"},
  {"", ""},
  {"single", "single"},
 }

 for _, tt := range tests {
  t.Run(tt.input, func(t *testing.T) {
   result := firstLabel(tt.input)
   if result != tt.expected {
    t.Errorf("firstLabel(%q) = %q, want %q", tt.input, result, tt.expected)
   }
  })
 }
}
```

--------------------------------

### Create IP Sets with Add Operations Only

Source: https://tailscale.com/docs/features/tailnet-policy-file/ip-sets

Defines IP sets where only 'add' operations are used, simplifying the syntax by assuming 'add' as the default operation. This is useful for static lists of IPs or hosts.

```json
"ipsets": {
  "ipset:prod": ["192.0.2.0/24"],
  "ipset:dev": [
    "198.51.100.0/24",
    "203.0.113.0/24",
    "host:sql-server-1",
  ]
}
```

--------------------------------

### Test Tailscale ethtool Configuration Script

Source: https://tailscale.com/docs/reference/best-practices/performance

Tests the persistence script created for `ethtool` UDP throughput optimizations on Linux. This command verifies that the script runs successfully and applies the necessary network device configurations.

```bash
sudo /etc/networkd-dispatcher/routable.d/50-tailscale
test $? -eq 0 || echo 'An error occurred.'

```

--------------------------------

### Disable IPv4 for Specific Targets in Tailscale Access Policies

Source: https://tailscale.com/docs/reference/troubleshooting?tab=windows

This JSON snippet demonstrates how to selectively disable IPv4 for specific targets within your Tailscale network using node attributes in your access control policies. This is useful for managing CGNAT conflicts on a per-device or per-group basis.

```json
{
  "nodeAttrs": [
    {
      "target": ["tag:lab-foo"],
      "attr":   ["disable-ipv4"],
    },
  ]
}
```

--------------------------------

### Disable IPv4 Tailnet-Wide (Tailscale ACL)

Source: https://tailscale.com/docs/reference/troubleshooting?tab=macos

This JSON snippet shows how to disable IPv4 for all devices in your Tailscale network by applying the `disable-ipv4` node attribute to all targets (`*`). This forces the entire tailnet to use IPv6 only, which can resolve CGNAT conflicts but may prevent access to IPv4-only resources.

```json
{
  "nodeAttrs": [
    {
      "target": ["*"],
      "attr":   ["disable-ipv4"],
    },
  ]
}

```

--------------------------------

### Connect External Device to Aperture Proxy with ts-unplug

Source: https://tailscale.com/docs/features/aperture

This command demonstrates how to use the ts-unplug tool to expose the Aperture proxy instance to a device outside the tailnet. It requires the fully qualified domain name (FQDN) of the Aperture proxy and an available port number.

```bash
ts-unplug -dir ./state -port <PORT_NUMBER> ai.<YOUR_TAILNET_ID>.ts.net

```

--------------------------------

### Serve website files within the tailnet

Source: https://tailscale.com/docs/features/tailscale-funnel/how-to/host-websites

This command uses Tailscale Serve to host the specified directory's contents, making them accessible only to devices within your Tailscale network (tailnet). It's ideal for internal testing or private content sharing.

```bash
tailscale serve /tmp/test-funnel/index.html

```

--------------------------------

### Wait for ProxyGroup to be Ready

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

Waits for the 'ingress-proxies' `ProxyGroup` to reach a ready state. This command is useful for ensuring that the proxy infrastructure is operational before proceeding.

```bash
kubectl wait proxygroup ingress-proxies --for=condition=ProxyGroupReady=true

```

--------------------------------

### Access Tailscale Service via Cluster DNS - Curl Command

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-egress

Demonstrates how cluster workloads can access a Tailscale target service using the ExternalName Service's cluster DNS name. This example uses curl to connect to a service named 'ts-egress' on port 8080.

```bash
$ curl ts-egress.default.svc.cluster.local:8080
...

```

--------------------------------

### Apply Tags to Device using Tailscale CLI

Source: https://tailscale.com/docs/features/tags

Assigns tags to a device using the Tailscale command-line interface. Supports single tags, multiple comma-separated tags, and removing all tags by providing an empty value. The `--force-reauth` flag can be used to re-authenticate the device with the current user.

```bash
sudo tailscale login --advertise-tags=tag:server

```

```bash
sudo tailscale login --advertise-tags=tag:server,tag:development

```

```bash
sudo tailscale login --advertise-tags=

```

```bash
sudo tailscale up --advertise-tags=tag:server --force-reauth

```

--------------------------------

### Get Tailscale IP Address (System Utility)

Source: https://tailscale.com/docs/concepts/ip-and-dns-addresses?tab=linux

Find the Tailscale IP address by using the system's `ip` utility, which is a universal method applicable to all versions of Tailscale. This command displays network interface details, including the IP address assigned to the `tailscale0` interface.

```bash
ip addr show tailscale0
```

--------------------------------

### Connect OPNsense to Tailnet

Source: https://tailscale.com/docs/install/opnsense

Command to connect the OPNsense machine to your Tailscale network (tailnet). This command initiates the connection process and provides a URL for authentication.

```shell
# tailscale up
To authenticate, visit:
    https://tailscale.com/a/abc123abc123

```

--------------------------------

### Reference Synced Groups in Tailscale Access Rules

Source: https://tailscale.com/docs/reference/syntax/policy-file

This example demonstrates how to reference a synced group, 'security-team', in Tailscale access rules. Synced groups are managed externally via an identity provider and provisioned into Tailscale. This rule grants the 'security-team' access to 'tag:logging' resources.

```json
{
  "grants": [
    {
      "src": ["group:security-team@example.com"],
      "dst": ["tag:logging"],
      "ip": ["*"]
    }
  ],
  "tagOwners": {
    "tag:logging": ["group:security-team@example.com"]
  }
}
```

--------------------------------

### Configure SCIM Provisioning in Microsoft Entra ID for Tailscale

Source: https://tailscale.com/docs/integrations/identity/entra/entra-id-scim

Steps to configure automatic SCIM provisioning for Tailscale in Microsoft Entra ID. This involves logging into the Azure portal, navigating to Enterprise applications, selecting Tailscale, and configuring provisioning settings including Tenant URL and Secret Token.

```text
1. Log in to the Microsoft Azure portal.
2. Select **Microsoft Entra ID**.
3. Under **Manage**, select **Enterprise applications**.
4. Select **New application**.
5. Search for **Tailscale** and select it.
6. Select **Sign up for Tailscale**.
7. On the application **Overview** page, under **Manage**, select **Provisioning**.
8. Select **Get started**.
9. Set **Provisioning Mode** to **Automatic**.
10. Under **Admin Credentials**, for **Tenant URL**, enter `https://controlplane.tailscale.com/scim/v2/?aadOptscim062020`.
11. For **Secret Token**, enter the SCIM API key generated in the Tailscale admin console.
12. Select **Test Connection**.
13. Ensure **Send an email notification when an error occurs** is checked and provide an email.
14. Under **Scope**, choose to sync all users and groups or only assigned users and groups.
15. Ensure **Provisioning Status** is set to **On**.
16. Select **Save**.
17. Return to the **Provisioning** page and select **Start Provisioning**.
```

--------------------------------

### Automate Container Tailscale Integration with Auth Key

Source: https://tailscale.com/docs/integrations/unraid

Automatically join Docker containers created on Unraid to your Tailnet using a Tailscale OAuth client secret. This assigns each container a unique device identity within your tailnet. Prerequisites include setting up Tailscale tags, generating an OAuth client, and enabling HTTPS certificates.

```bash
--authkey=tskey-client-kQ3XbSTPg921CNTRL-teMgW7PkZ2No9xr1CRTt1N7k45u3MnKpZ --advertise-tags=tag:example

```

--------------------------------

### Persist Linux ethtool Settings with networkd-dispatcher

Source: https://tailscale.com/docs/reference/best-practices/performance

Creates a script to automatically apply `ethtool` UDP throughput optimizations on Linux systems using `networkd-dispatcher` after each boot. This ensures persistent configuration for Tailscale subnet routers and exit nodes.

```bash
printf '#!/bin/sh\n\nethtool -K %s rx-udp-gro-forwarding on rx-gro-list off \n' "$(ip -o route get 8.8.8.8 | cut -f 5 -d " ")" | sudo tee /etc/networkd-dispatcher/routable.d/50-tailscale
sudo chmod 755 /etc/networkd-dispatcher/routable.d/50-tailscale

```

--------------------------------

### Advertise Subnet Routes with Tailscale

Source: https://tailscale.com/docs/how-to/connect-vpc

This command configures the Tailscale client to advertise specific subnet routes, making them accessible to other devices on the Tailscale network. Replace placeholders with actual subnet ranges.

```bash
sudo tailscale set --advertise-routes=<subnet range 1>,<subnet range 2>,...
```

```bash
sudo tailscale set --advertise-routes=10.0.0.0/24,10.0.1.0/24
```

--------------------------------

### Amazon Bedrock Provider Configuration

Source: https://tailscale.com/docs/features/aperture/configuration

Sets up the Amazon Bedrock provider, specifically for the Bedrock model invocation API. It includes the base URL, an API key, supported models, and the necessary compatibility flag.

```json
{
  "providers": {
    "bedrock": {
      "baseurl": "https://bedrock-runtime.us-east-1.amazonaws.com",
      "apikey": "bedrock-api-key-xxx",
      "authorization": "bearer",
      "models": [
        "us.anthropic.claude-haiku-4-5-20251001-v1:0",
        "us.anthropic.claude-sonnet-4-5-20250929-v1:0",
        "us.anthropic.claude-opus-4-5-20251101-v1:0",
        "us.anthropic.claude-opus-4-6-v1"
      ],
      "compatibility": {
        "bedrock_model_invoke": true
      }
    }
  }
}
```

--------------------------------

### Test DNS Resolution on macOS using dscacheutil

Source: https://tailscale.com/docs/reference/dns-in-tailscale?tab=macos

This command-line utility on macOS is used to query the directory service cache for host information, including IP addresses associated with domain names or MagicDNS hostnames. It's a recommended alternative to 'nslookup' for testing DNS configurations, especially with split DNS or MagicDNS.

```bash
dscacheutil -q host -a name <domain-or-magic-dns-hostname>
```

```bash
$ dscacheutil -q host -a name my-server

name: my-server.example.ts.net
ip_address: 100.15.193.72
```

--------------------------------

### Expose Cloud Service with Kubernetes ExternalName Service

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cloud-services

This YAML defines a Kubernetes Service of type ExternalName to expose a cloud service, such as an RDS instance, to a Tailscale network. It requires the Tailscale Kubernetes Operator to be installed and uses the `tailscale.com/expose: "true"` annotation.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-rds
  annotations:
    tailscale.com/expose: "true"
spec:
  type: ExternalName
  externalName: my-rds.eu-central-1.rds.amazonaws.com

```

--------------------------------

### Wait for Recorder to be Ready

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/tsrecorder

Waits for a specific Kubernetes resource, in this case, the 'Recorder' named 'recorder', to reach a 'RecorderReady' condition. This is useful for ensuring the recorder is fully operational before proceeding with further actions.

```bash
$ kubectl wait --for condition=RecorderReady=true Recorder recorder
recorder.tailscale.com/recorder condition met

```

--------------------------------

### Tailscale netlogfmt: Resolve IP Addresses to Hostnames

Source: https://tailscale.com/docs/features/logging/network-flow-logs

This snippet shows how to use the `--resolve-addrs=names` flag with `netlogfmt`. This option resolves Tailscale IP addresses to their associated hostnames, providing a more human-readable representation of network traffic origins and destinations.

```shell
# Example usage (assuming logs are piped to netlogfmt):
netlogfmt --resolve-addrs=names
```

--------------------------------

### Configure Routes via Tailscale Access Control Policy

Source: https://tailscale.com/docs/reference/best-practices/app-connectors

This JSON snippet demonstrates how to define routes and domains for an application connector within a Tailscale access control policy file. It specifies the target nodes, application details, associated connectors, domains, and the IP routes to be advertised. This configuration is applied to the `nodeAttrs` field in the tailnet policy file.

```json
{
  "target": ["*"],
  "app": {
    "tailscale.com/app-connectors": [
      {
        "name": "example-app",
        "connectors": ["tag:example-connector"],
        "domains": ["example.com"],
        "routes": ["192.0.2.0/24"],
      }
    ],
  },
}

```

--------------------------------

### Configure Mullvad License Pool in Tailscale Policy

Source: https://tailscale.com/docs/features/exit-nodes/mullvad-exit-nodes

This configuration allows multiple devices to share a limited pool of Mullvad VPN licenses. Devices access licenses on a first-come, first-served basis as they connect to the tailnet. Ensure enough licenses are purchased to cover peak usage.

```json
{
  "nodeAttrs": [
    {
      "target": ["group:mullvad"],
      "attr": [
        "mullvad"
      ]
    }
  ]
}
```

--------------------------------

### Serve website files to the public internet

Source: https://tailscale.com/docs/features/tailscale-funnel/how-to/host-websites

This command utilizes Tailscale Funnel to expose the specified directory's contents to the public internet. This allows anyone with the correct URL to access your hosted website.

```bash
tailscale funnel /tmp/test-funnel/index.html

```

--------------------------------

### Enable Tailscale Client

Source: https://tailscale.com/docs/solutions/create-a-secure-connection-to-mongodb-atlas

This command is used to enable the Tailscale client on a device after it has been disabled for testing. Re-enabling Tailscale restores network connectivity through the secure tailnet, allowing access to resources like the MongoDB Atlas database.

```bash
tailscale up
```

--------------------------------

### Configure Linux Device to Use Exit Node

Source: https://tailscale.com/docs/solutions/secure-traffic-public-wifi-appletv?tab=linux

This snippet shows how to configure a Linux device to route its internet traffic through a specified Tailscale exit node. It includes options to allow direct access to the local network and how to disable the exit node configuration.

```bash
sudo tailscale set --exit-node=<exit-node-ip>

```

```bash
sudo tailscale set --exit-node=<exit-node-ip> --exit-node-allow-lan-access=true

```

```bash
sudo tailscale set --exit-node=

```

--------------------------------

### Enable Tailscale SSH on a Device

Source: https://tailscale.com/docs/features/tailscale-ssh

Enable Tailscale SSH on a device if it was previously disabled or not configured. This allows the device to accept SSH connections over Tailscale.

```bash
tailscale set --ssh
```

--------------------------------

### Tailscale Policy: Grant and Deny Access (Tailnet 1)

Source: https://tailscale.com/docs/features/multiple-tailnets

This JSON policy grants access for 'group1@example.com' to 'tag:staging' on port 443 and explicitly denies 'group2@example.com' access to the same resource. This is useful for defining granular access controls within a specific tailnet.

```json
{
  "grants": [
    {
      "src": ["group1@example.com"],
      "dst": ["tag:staging"],
      "ip": ["443"]
    }
  ],
  "tests": [
    {
      "src": "group2@example.com",
      "deny": ["tag:staging:443"]
    }
  ]
}
```

--------------------------------

### Check Tailscale Network Mapping

Source: https://tailscale.com/docs/integrations/firewalls

Use the Tailscale CLI command `tailscale netcheck` to verify network mapping behavior. This is particularly useful in networks with Sophos security gateways to confirm that the mapping does not vary by destination IP.

```bash
tailscale netcheck
```

--------------------------------

### Get Device Posture Attributes API

Source: https://tailscale.com/docs/features/tailscale-accessbot-jit

Retrieves all posture attributes for a specified Tailscale device. This API endpoint returns a JSON object containing key-value pairs of attributes and their expiration times if set. It's useful for auditing and understanding the current state of device access controls.

```bash
curl "https://api.tailscale.com/api/v2/device/11055/attributes" \
-u "tskey-api-xxxxx:"
```

```json
{
  "attributes": {
    "custom:myScore": 87,
    "custom:diskEncryption": true,
    "custom:myAttribute": "my_value",
    "node:os": "linux",
    "node:osVersion": "5.19.0-42-generic",
    "node:tsReleaseTrack": "stable",
    "node:tsVersion": "1.40.0",
    "node:tsAutoUpdate": false
  },
  "expiries": {
    "custom:myScore": "2024-04-23T18:25:43.511Z"
  }
}
```

--------------------------------

### Go tsnet Application: HTTP Handler with WhoIs API

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

Implements an HTTP handler that uses the Tailscale WhoIs API to authenticate connecting clients. It displays a 'Hello, world!' message along with the client's identity information.

```go
    log.Fatal(http.Serve(ln, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        who, err := lc.WhoIs(r.Context(), r.RemoteAddr)
            if err != nil {
                http.Error(w, err.Error(), 500)
            return
        }
        fmt.Fprintf(w, "<html><body><h1>Hello, world!</h1>\n")
        fmt.Fprintf(w, "<p>You are <b>%s</b> from <b>%s</b> (%s)</p>",
            html.EscapeString(who.UserProfile.LoginName),
            html.EscapeString(firstLabel(who.Node.ComputedName)),
            r.RemoteAddr)
     })))
}

```

--------------------------------

### Commit and Push GitHub Actions Workflow

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

These Git commands are used to stage all changes, commit them with a descriptive message, and push the new GitHub Actions workflow file to the 'main' branch of the repository. This makes the workflow active and ready to run.

```bash
git add .
git commit -m "Add GitHub workflow"
git push origin main
```

--------------------------------

### Tailscale SSH Rule with Autogroups

Source: https://tailscale.com/docs/reference/syntax/policy-file

This example demonstrates how to configure an SSH rule in Tailscale's ACL policy file. It utilizes autogroups like 'autogroup:member', 'autogroup:self', and 'autogroup:nonroot' to grant specific access permissions. The rule allows members to SSH into their own devices as non-root users.

```json
{
  "ssh": [
    {
      "action": "accept",
      "src": ["autogroup:member"],
      "dst": ["autogroup:self"],
      "users": ["autogroup:nonroot"]
    }
  ]
}
```

--------------------------------

### Ping Database for Direct Connectivity Test

Source: https://tailscale.com/docs/solutions/protect-postgresql-unencrypted-macbooks

This command tests the connection path to a production database. When run from an encrypted MacBook, it should show direct connectivity, bypassing the monitoring gateway. Replace placeholders with your actual database and tailnet names.

```bash
tailscale ping <database-name>.<tailnet-name>.ts.net
```

--------------------------------

### Serve Content from Tailscale Node

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=bash

Serves content and local servers from your Tailscale node to the internet. The `serve` command specifically limits access to your tailnet.

```bash
tailscale funnel <target>
tailscale funnel serve [flags] <args>
```

--------------------------------

### Create Basic Connector Resource - Kubernetes Operator YAML

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/app-connector

Defines a basic `Connector` resource for deploying an app connector on Kubernetes using the Tailscale Kubernetes Operator. This is the minimal configuration required.

```yaml
apiVersion: tailscale.com/v1alpha1
kind: Connector
metadata:
  name: appc-github
spec: {}

```

--------------------------------

### Configure Aperture Oso Grant and Hook

Source: https://tailscale.com/docs/features/aperture

This snippet shows how to configure Aperture to send traffic to Oso based on specific grant conditions and how to define the Oso hook with its URL and API key. It requires the 'oso' hook to be defined in the 'hooks' section.

```json
// Other Aperture configuration settings...
"temp_grants": [
  // Example hook: send traffic to Oso if it matches certain parameters.
  // You need to also configure Oso in the "hooks" section for this to work.
  {
      "src": [
          // No users by default. Try "*" to capture everyone's traffic.
      ],
      "grants": [
          {
              "hook": {
                  "match": {
                      "providers": ["*"],
                      "models":    ["*"],
                      // Capturing only tool calls
                      "events":    ["tool_call_entire_request"],
                  },
                  "hook":   "oso",
                  "fields": ["user_message", "tools", "request_body", "response_body"],
              },
          },
      ],
  },
],

// Other Aperture configuration settings...
"hooks": {
    "oso": {
        "url":    "https://api.osohq.com/api/agents/v1/model-request",
        "apikey": "YOUR_OSO_API_KEY",
    },
},

```

--------------------------------

### View Tailscale Proxy Container Logs

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

This command fetches the logs from the 'tailscale' container within a specific proxy pod. Examining these logs is crucial for diagnosing issues related to certificate issuance, network connectivity, or the Tailscale daemon's operation.

```bash
kubectl logs ingress-proxies-0 -n tailscale -c tailscale

```

--------------------------------

### Enable Tailscale Peer Relays for VPC Communication

Source: https://tailscale.com/docs/reference/examples/grants

This configuration allows devices tagged with `tag:us-east-vpc` to use devices tagged with `tag:us-east-relays` as underlay network relays. It utilizes the `tailscale.com/cap/relay` application capability. Proper configuration of peer relay devices and a basic grant policy are required.

```json
{
  "grants": [
    {
      "src": ["tag:us-east-vpc"],
      "dst": ["tag:us-east-relays"],
      "app": {
        "tailscale.com/cap/relay": []
      }
    }
  ]
}
```

--------------------------------

### Define User Groups in Tailscale ACLs

Source: https://tailscale.com/docs/reference/syntax/policy-file

This snippet shows how to define user groups within the Tailscale policy file. Groups allow you to manage access rules for multiple users collectively. Membership changes propagate to all rules referencing the group. Groups must start with the 'group:' prefix and cannot contain other groups.

```json
{
  "groups": {
    "group:engineering": [
      "dave@example.com",
      "laura@example.com"
    ],
    "group:sales": [
      "brad@example.com",
      "alice@example.com"
    ]
  }
}
```

--------------------------------

### Apply DNS Configuration (Shell)

Source: https://tailscale.com/docs/solutions/manage-multi-cluster-kubernetes-deployments-argocd

Applies the created DNS configuration resource to the Kubernetes cluster using the `kubectl` command-line tool. This command takes a YAML file (e.g., `dns-config.yaml`) as input and applies the specified configuration to the cluster's resources.

```bash
kubectl apply -f dns-config.yaml
```

--------------------------------

### Switch Account using Tailscale CLI

Source: https://tailscale.com/docs/features/client/fast-user-switching?tab=android

This command enables switching between already added Tailscale accounts using the CLI on Linux, macOS, or Windows. It supports switching by email address or by a previously set nickname. Re-authentication is only required if the node key has expired or the account is new to the device.

```bash
tailscale switch alice@example.com

```

```bash
tailscale switch work

```

--------------------------------

### Switch Tailscale Account

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Allows switching to a different Tailscale account on the local machine. You can specify the account by email address or a nickname. Use the `--list` flag to see available accounts.

```bash
tailscale switch <account> [flags]
```

```bash
tailscale switch alice@example.com
```

```bash
tailscale switch work
```

--------------------------------

### List Existing Taildrive Shares with CLI

Source: https://tailscale.com/docs/features/taildrive?tab=linux

Command to display all currently shared directories from a device via Taildrive. It outputs the share name, local path, and the user context.

```bash
tailscale drive list
```

--------------------------------

### List Accounts using Tailscale CLI

Source: https://tailscale.com/docs/features/client/fast-user-switching?tab=android

This command lists all authenticated Tailscale accounts on the device using the CLI for Linux, macOS, or Windows. It indicates the currently active account with an asterisk and displays nicknames if set. This helps manage multiple logged-in accounts.

```bash
tailscale switch --list

```

--------------------------------

### Google Gemini Provider Configuration

Source: https://tailscale.com/docs/features/aperture/configuration

Sets up the Google Gemini provider, utilizing the Gemini API with 'x-goog-api-key' authorization. The configuration includes the base URL, API key placeholder, model list, and specific compatibility flags.

```json
{
  "providers": {
    "gemini": {
      "baseurl": "https://generativelanguage.googleapis.com",
      "apikey": "YOUR_GEMINI_KEY",
      "authorization": "x-goog-api-key",
      "models": ["gemini-2.5-flash", "gemini-2.5-pro"],
      "name": "Google Gemini",
      "compatibility": {
        "openai_chat": false,
        "gemini_generate_content": true
      }
    }
  }
}
```

--------------------------------

### Combine Tailscale Session Recording and Group Impersonation

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/session-recording

This configuration combines session recording rules with API server proxy impersonation. It allows requests from the engineering group, enforces session recording, and configures requests to be impersonated as from the Kubernetes group 'system:masters'.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": ["group:engineering"],
      "dst": ["tag:k8s-operator:443"]
    }
  ],
  "grants": [
    {
      "src": ["group:engineering"],
      "dst": ["tag:k8s-operator"],
      "app": {
        "tailscale.com/cap/kubernetes": [{
          "impersonate": {
            "groups": ["system:masters"]
          },
          "recorder": ["tag:tsrecorder"]
        }]
      }
    }
  ]
}
```

--------------------------------

### Configure Traefik Router to Use Tailscale Certificate Resolver (YAML)

Source: https://tailscale.com/docs/integrations/web-servers/traefik/traefik-certificates

This YAML snippet demonstrates how to configure a Traefik router ('routertailscale') to use the previously defined Tailscale certificate resolver. It sets a rule to match a specific host and path within the *.ts.net domain and explicitly assigns the 'tailscale' certResolver for enabling HTTPS. The example also includes a basic service definition.

```yaml
http:
  routers:
    routertailscale:
      service: "myservice"
      rule: "Host(`example.foo.ts.net`) && Path(`/tailscale`)"
      tls:
        certResolver: tailscale

  services:
    myservice:
      loadBalancer:
        servers:
         - url: "http://localhost:6060"
```

--------------------------------

### Rotate Node and SSH Host Keys with Tailscale

Source: https://tailscale.com/docs/features/tailscale-ssh

Generate new node and SSH host keys for a device. This is useful for security or after re-authentication to ensure fresh keys are in use.

```bash
tailscale up --ssh --force-reauth
```

--------------------------------

### Tailscale netlogfmt: Resolve IP Addresses to Node IDs

Source: https://tailscale.com/docs/features/logging/network-flow-logs

This snippet illustrates the use of the `--resolve-addrs=nodeids` flag with the `netlogfmt` tool. This option converts Tailscale IP addresses into their corresponding node IDs, making it easier to identify specific devices within the network logs.

```shell
# Example usage (assuming logs are piped to netlogfmt):
netlogfmt --resolve-addrs=nodeids
```

--------------------------------

### Sign Pre-Approved Auth Key with Tailscale Lock

Source: https://tailscale.com/docs/features/tailnet-lock?tab=ios

Signs a pre-approved authentication key using the `tailscale lock sign` command. This command takes the value of the `AUTH_KEY` environment variable and generates a new key that can be used to pre-approve devices.

```bash
tailscale lock sign $AUTH_KEY
```

--------------------------------

### Provision Server with Tailscale SSH Enabled

Source: https://tailscale.com/docs/how-to/set-up-servers

This command demonstrates provisioning a server with Tailscale while enabling Tailscale SSH. The `--ssh` flag configures the server to accept SSH connections over the Tailscale network, enhancing secure remote access capabilities.

```bash
tailscale up --auth-key=$TS_AUTHKEY --ssh

```

--------------------------------

### tailscale-client-go-v2 Authentication

Source: https://tailscale.com/docs/features/workload-identity-federation?tab=google+cloud

This section describes how to authenticate `tailscale-client-go-v2` using workload identity by providing a ClientID and an IDTokenFunc to the Tailscale client.

```APIDOC
## tailscale-client-go-v2 Authentication

### Description
Authenticates `tailscale-client-go-v2` using workload identity. This involves configuring the `tailscale.Client` with `ClientID` and an `IDTokenFunc` that provides the identity token.

### Usage
```go
package main

import (
	"context"
	"os"

	"tailscale.com/client/tailscale/v2"
)

func main() {
	client := &tailscale.Client{
		Tailnet: os.Getenv("TAILSCALE_TAILNET"),
		Auth: &tailscale.IdentityFederation{
			ClientID: os.Getenv("TAILSCALE_OAUTH_CLIENT_ID"),
			IDTokenFunc: func() (string, error) {
				return os.Getenv("IDENTITY_TOKEN"), nil
            },
		},
	}

	// Example API call

devices, err := client.Devices().List(context.Background())
}
```
```

--------------------------------

### Configure Tailscale CLI Tab-Completion

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=macos

Set up tab-completion for the Tailscale CLI in various shells. You can configure whether to suggest flags and descriptions using `--flags` and `--descs` options.

```bash
tailscale completion bash
tailscale completion zsh
tailscale completion fish
tailscale completion powershell
tailscale completion --flags=false --descs=false bash
```

--------------------------------

### Manage Tailscale DNS Settings

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

The `dns` command provides access to Tailscale DNS settings, available from v1.74.0 onwards. Subcommands include `status` to view DNS configurations and `query` (v1.76.0+) to perform DNS queries. The `--all` flag for `status` provides advanced debugging information.

```bash
tailscale dns status
tailscale dns status --all
tailscale dns query example.com
```

--------------------------------

### Test Aperture Configuration with cURL (OpenAI Chat Completions API)

Source: https://tailscale.com/docs/features/aperture

Provides a cURL command to test the connection and routing to Aperture for the OpenAI chat completions API format. This command sends a request to the /v1/chat/completions endpoint.

```bash
curl -s http://ai/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o",
    "messages": [{"role": "user", "content": "respond with: hello"}]
  }'
```

--------------------------------

### Wait for Tailscale Service Configuration

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Waits for a Kubernetes `Service` resource to be fully configured by the Tailscale operator. This command is used after creating a LoadBalancer Service to ensure it's ready to receive traffic.

```bash
kubectl wait svc nginx --for condition=TailscaleIngressSvcConfigured
```

--------------------------------

### tailscale-client-go-v2 Authentication with Workload Identity

Source: https://tailscale.com/docs/features/workload-identity-federation

This section explains how to authenticate the `tailscale-client-go-v2` library using workload identity.

```APIDOC
## Client Configuration for Workload Identity (tailscale-client-go-v2)

### Description
Authenticates the `tailscale-client-go-v2` client by providing a `ClientID` and an `IDTokenFunc` that retrieves the workload identity token.

### Method
N/A (Client Library Initialization)

### Endpoint
N/A

### Parameters
#### `tailscale.Client` Configuration
- **Tailnet** (string) - Required - The name of your Tailscale tailnet (e.g., from environment variable `TAILSCALE_TAILNET`).
- **Auth** (*tailscale.IdentityFederation) - Required - Configuration for identity federation.
  - **ClientID** (string) - Required - Your Tailscale OAuth client ID (e.g., from environment variable `TAILSCALE_OAUTH_CLIENT_ID`).
  - **IDTokenFunc** (func() (string, error)) - Required - A function that returns the workload identity token (e.g., reads from environment variable `IDENTITY_TOKEN`).

### Request Example (Go Code)
```go
package main

import (
	"context"
	"os"

	"tailscale.com/client/tailscale/v2"
)

func main() {
	client := &tailscale.Client{
		Tailnet: os.Getenv("TAILSCALE_TAILNET"),
		Auth: &tailscale.IdentityFederation{
			ClientID: os.Getenv("TAILSCALE_OAUTH_CLIENT_ID"),
			IDTokenFunc: func() (string, error) {
				return os.Getenv("IDENTITY_TOKEN"), nil
            },
		},
	}

	// Example API call
	devices, err := client.Devices().List(context.Background())
}
```

### Response
#### Success Response
Successful authentication of the client with Tailscale.

#### Response Example
N/A (This is a client initialization, not a direct API response)
```

--------------------------------

### Configure Device Routes for Subnet Connectivity

Source: https://tailscale.com/docs/features/site-to-site

Sets static routes on devices within a subnet to direct traffic destined for other subnets through the respective subnet router. These commands are executed on each device within the subnet, excluding the subnet router itself.

```bash
ip route add 100.64.0.0/10 via 192.0.2.2
ip route add 172.16.100.0/24 via 192.0.2.2
```

```bash
ip route add 100.64.0.0/10 via 172.16.100.2
ip route add 192.0.2.0/24 via 172.16.100.2
```

--------------------------------

### Basic CI Access Rule (JSON)

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This JSON snippet defines a basic access rule for CI runners. The 'grants' section specifies that devices with 'tag:ci' can access all other devices ('*') on all IP addresses and ports ('*'). This is a lenient policy for demonstration.

```json
"grants": [
  {
    "src": ["tag:ci"],
    "dst": ["*"],
    "ip": ["*"]
  },
  // Other access rules
]
```

--------------------------------

### Deploy Tailscale Proxy for Kubernetes Service

Source: https://tailscale.com/docs/kubernetes

This snippet demonstrates how to deploy a Tailscale proxy to provide inbound connectivity to a specific Kubernetes Service. It involves obtaining the ClusterIP of the target service and then applying the proxy deployment. Authentication can be handled via an auth key or by obtaining a login URL from the proxy logs.

```bash
kubectl create deployment nginx --image nginx
kubectl expose deployment nginx --port 80
export TS_DEST_IP="$(kubectl get svc nginx -o=jsonpath='{.spec.clusterIP}')"

# Or for an existing service:
# export TS_DEST_IP="$(kubectl get svc <SVC_NAME> -o=jsonpath='{.spec.clusterIP}')"

make proxy | kubectl apply -f-
# If not using an auth key, authenticate by grabbing the Login URL here:
kubectl logs proxy

# Check connectivity
curl http://proxy
# Or if MagicDNS is disabled:
curl "http://$(tailscale ip -4 proxy)"
```

--------------------------------

### Configure Default Source Posture in Tailscale Policy

Source: https://tailscale.com/docs/features/device-posture

Sets a baseline security posture that applies to all access rules unless overridden. This configuration is part of the Tailscale policy file and accepts an array of posture identifiers.

```json
"defaultSrcPosture": [
  "posture:basicWindows",
  "posture:basicMac",
  "posture:basicLinux"
]
```

--------------------------------

### Configure Tailscale Provider with Environment Variables (Terraform)

Source: https://tailscale.com/docs/integrations/terraform-provider

This snippet demonstrates how to configure the Tailscale Terraform provider by setting various environment variables. These variables control authentication (API key, OAuth credentials, identity token), the base URL for the Tailscale API, and the specific tailnet to interact with. Ensure sensitive variables are handled securely.

```bash
# Example environment variables for Tailscale Terraform provider
export TAILSCALE_API_KEY="your_api_key"
# or
# export TAILSCALE_OAUTH_CLIENT_ID="your_client_id"
# export TAILSCALE_OAUTH_CLIENT_SECRET="your_client_secret"
# or
# export TAILSCALE_IDENTITY_TOKEN="your_identity_token"

export TAILSCALE_BASE_URL="https://api.tailscale.com"
export TAILSCALE_TAILNET="your_tailnet_id"

# Terraform configuration would then use these variables implicitly
# provider "tailscale" {}
```

--------------------------------

### Tailscale ACLs for Pair Programming

Source: https://tailscale.com/docs/reference/examples/acls

This JSON configuration sets up Tailscale ACLs for pair programming. It allows specific users (Alice and Bob) to access a corporate device tagged for pair programming over SSH. It also designates Bob as the owner of the pair programming tag.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": [
        "alice@example.com",
        "bob@example.com"
      ],
      "dst": [
        "tag:pair-programming:22"
      ]
    }
  ],
  "tagOwners": {
    "tag:pair-programming": [
      "bob@example.com"
    ]
  }
}
```

--------------------------------

### Tailscale Completion Configuration

Source: https://tailscale.com/docs/reference/tailscale-cli

Configure tab-completion for the Tailscale CLI in your shell (bash, zsh, fish, powershell). You can choose to include flags and descriptions in the suggestions.

```APIDOC
## POST /websites/tailscale/completion

### Description
Configure tab-completion for the Tailscale CLI for various shells.

### Method
POST

### Endpoint
/websites/tailscale/completion

### Parameters
#### Query Parameters
- **subcommand** (string) - Required - The shell for which to configure completion (e.g., bash, zsh, fish, powershell).
- **flags** (boolean) - Optional - Whether to suggest flags in addition to subcommands. Defaults to true.
- **descs** (boolean) - Optional - Whether to include descriptions of subcommands in suggestions. Defaults to true.

### Request Example
```json
{
  "subcommand": "bash",
  "flags": true,
  "descs": false
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating completion setup.

#### Response Example
```json
{
  "message": "Tab completion configured for bash shell."
}
```
```

--------------------------------

### Configure Tailscale Ping Verification in GitHub Action

Source: https://tailscale.com/docs/integrations/github/github-action

This snippet shows how to use the 'ping' input in the Tailscale GitHub Action to verify connectivity to specified IP addresses or hostnames. The action waits up to three minutes for direct or relayed connectivity. This is useful for ensuring new Tailscale devices are reachable after propagation delays.

```yaml
- name: Tailscale
  uses: tailscale/github-action@v4
  with:
    ping: 100.x.y.z,machine-1.my-tailnet.ts.net,machine-2

```

--------------------------------

### Configure Google Vertex AI Models

Source: https://tailscale.com/docs/features/aperture/configuration

This configuration sets up Google Vertex AI as a provider, enabling support for both Gemini and Anthropic models. It specifies the base URL, authorization method, API key, and lists compatible models. The `compatibility` section enables raw predict for Anthropic models and general content generation for Gemini.

```json
{
  "providers": {
    "vertex": {
      "baseurl": "https://aiplatform.googleapis.com",
      "authorization": "bearer",
      "apikey": "keyfile::ba3..3kb.data...67",
      "models": [
        "gemini-2.0-flash-exp",
        "gemini-2.5-flash",
        "gemini-2.5-flash-image",
        "gemini-2.5-pro",
        "claude-opus-4-5@20251101",
        "claude-haiku-4-5@20251001",
        "claude-sonnet-4-5@20250929",
        "claude-opus-4-6"
      ],
      "compatibility": {
        "google_generate_content": true,
        "google_raw_predict": true
      }
    }
  }
}
```

--------------------------------

### Generate Tailscale API Access Token using Go

Source: https://tailscale.com/docs/features/oauth-clients

This Go code snippet demonstrates how to create an OAuth client using client ID and secret to generate an API access token for Tailscale API calls. It requires environment variables OAUTH_CLIENT_ID and OAUTH_CLIENT_SECRET to be set.

```go
package main

import (
        "context"
        "fmt"
        "io/ioutil"
        "log"
        "os"

        "golang.org/x/oauth2/clientcredentials"
)

func main() {
        var oauthConfig = &clientcredentials.Config{
                ClientID:     os.Getenv("OAUTH_CLIENT_ID"),
                ClientSecret: os.Getenv("OAUTH_CLIENT_SECRET"),
                TokenURL:     "https://api.tailscale.com/api/v2/oauth/token",
        }

        client := oauthConfig.Client(context.Background())
        // Replace example.com with your tailnet ID.
        resp, err := client.Get("https://api.tailscale.com/api/v2/tailnet/example.com/devices")
        if err != nil {
                log.Fatalf("error getting keys: %v", err)
        }

        body, err := ioutil.ReadAll(resp.Body)
        if err != nil {
                log.Fatalf("error reading response body: %v", err)
        }

        fmt.Printf("response: %s", string(body))
}

```

--------------------------------

### Test Tshello Connection and Response Handling

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This test function verifies the connection to a target host and handles the response. It gracefully skips unavailable targets and logs the status code and response body. This test is useful for ensuring basic connectivity and response integrity.

```go
func TestTshelloConnection(t *testing.T) {
 // ... test implementation ...
 defer resp.Body.Close()

 body, err := io.ReadAll(resp.Body)
 if err != nil {
  t.Errorf("failed to read response from %s: %v", target, err)
  return
 }

 t.Logf("Response from %s (status %d): %s", target, resp.StatusCode, string(body))

 if resp.StatusCode != http.StatusOK {
  t.Errorf("unexpected status code from %s: %d", target, resp.StatusCode)
 }
 // ... rest of the test ...
}
```

--------------------------------

### Run Tailscale Recorder Docker Container

Source: https://tailscale.com/docs/features/tailscale-ssh/tailscale-ssh-session-recording

Runs the Tailscale recorder Docker container, mounting a local directory for data storage and configuring authentication. This command saves recordings to the Docker host's filesystem and enables the web UI.

```docker
docker run --name tsrecorder --rm -it \
  -e TS_AUTHKEY=$TS_AUTHKEY \
  -v $HOME/tsrecorder:/data \
  tailscale/tsrecorder:stable \
  /tsrecorder --dst=/data/recordings --statedir=/data/state --ui

```

--------------------------------

### Feature Settings API

Source: https://tailscale.com/docs/reference/trust-credentials

Endpoints for managing posture integrations and tailnet feature settings, including reading and creating posture integrations. Requires 'feature_settings:read' or 'feature_settings' credentials.

```APIDOC
## Feature Settings API

### Description
Manage posture integrations and tailnet feature settings.

### Endpoints

#### GET /api/v2/tailnet/:tailnet/posture/integrations

##### Description
Retrieves a list of posture integrations for a given tailnet.

##### Method
GET

##### Endpoint
/api/v2/tailnet/:tailnet/posture/integrations

##### Parameters
- **tailnet** (string) - Required - The name of the tailnet.

#### GET /api/v2/posture/integrations/:integrationID

##### Description
Retrieves a specific posture integration by its ID.

##### Method
GET

##### Endpoint
/api/v2/posture/integrations/:integrationID

##### Parameters
- **integrationID** (string) - Required - The ID of the posture integration.

#### GET /api/v2/tailnet/:tailnet/settings

##### Description
Retrieves tailnet settings, which may include feature settings.

##### Method
GET

##### Endpoint
/api/v2/tailnet/:tailnet/settings

##### Parameters
- **tailnet** (string) - Required - The name of the tailnet.

#### POST /api/v2/tailnet/:tailnet/posture/integrations

##### Description
Creates a new posture integration for a given tailnet.

##### Method
POST

##### Endpoint
/api/v2/tailnet/:tailnet/posture/integrations

##### Parameters
- **tailnet** (string) - Required - The name of the tailnet.

##### Request Body
- **name** (string) - Required - The name of the integration.
- **config** (object) - Required - The configuration for the integration.

### Response Examples
(Specific response examples depend on the exact endpoint and method used.)
```

--------------------------------

### Assign Mullvad Access via Tailnet Policy File (JSON)

Source: https://tailscale.com/docs/features/exit-nodes/mullvad-exit-nodes?tab=linux

This snippet demonstrates how to grant Mullvad VPN access to devices using node attributes within a Tailscale policy file. It requires the `mullvad` attribute to be assigned to specific targets, such as user email addresses. This method offers more flexibility than the admin console.

```json
{
  "nodeAttrs": [
    {
      "target": ["joe@example.com"],
      "attr": [
        "mullvad",
      ],
    },
  ],

}
```

--------------------------------

### Go tsnet Application: TLS Listener Configuration

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

Wraps the TCP listener with TLS when the server address is port 443, utilizing Tailscale's automatic certificate provisioning. This enables HTTPS without manual certificate management.

```go
    if *addr == ":443" {
       ln = tls.NewListener(ln, &tls.Config{
          GetCertificate: lc.GetCertificate,
     })
    }

```

--------------------------------

### Viewing Tailscale Preferences on Linux

Source: https://tailscale.com/docs/reference/route-injection

This command displays the current Tailscale preferences on a Linux client. It helps in verifying settings like route acceptance, which is crucial for subnet routing to function correctly.

```bash
tailscale debug prefs

```

--------------------------------

### Basic Provider Structure

Source: https://tailscale.com/docs/features/aperture/configuration

Defines the fundamental structure for configuring LLM providers in Aperture. It shows how to list different providers like OpenAI, Anthropic, and private instances, each identified by a unique string key.

```json
{
  "providers": {
    "openai": { ... },
    "anthropic": { ... },
    "private": { ... }
  }
}
```

--------------------------------

### Add QNAP Tailscale Package Path to PATH Environment Variable

Source: https://tailscale.com/docs/integrations/qnap

This command adds the directory containing the `tailscale` executable to the system's PATH environment variable. This allows you to run `tailscale` commands directly without specifying the full path, simplifying command-line operations on the QNAP NAS.

```shell
export PATH=$PATH:$(getcfg SHARE_DEF defVolMP -f /etc/config/def_share.info)/.qpkg/Tailscale/
tailscale ...
```

--------------------------------

### GitHub Actions Workflow for Syncing Tailscale ACLs

Source: https://tailscale.com/docs/integrations/github/gitops?tab=oauth+client

This YAML workflow automates the synchronization of Tailscale Access Control Lists (ACLs) using the `tailscale/gitops-acl-action`. It supports both deploying ACLs on push events and testing them on pull request events, utilizing GitHub secrets for authentication.

```yaml
name: Sync Tailscale ACLs

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  acls:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Deploy ACL
        if: github.event_name == 'push'
        id: deploy-acl
        uses: tailscale/gitops-acl-action@v1
        with:
          oauth-client-id: ${{ secrets.TS_OAUTH_ID }}
          oauth-secret: ${{ secrets.TS_OAUTH_SECRET }}
          tailnet: ${{ secrets.TS_TAILNET }}
          action: apply

      - name: Test ACL
        if: github.event_name == 'pull_request'
        id: test-acl
        uses: tailscale/gitops-acl-action@v1
        with:
          oauth-client-id: ${{ secrets.TS_OAUTH_ID }}
          oauth-secret: ${{ secrets.TS_OAUTH_SECRET }}
          tailnet: ${{ secrets.TS_TAILNET }}
          action: test

```

--------------------------------

### Monitor Custom DERP Servers with derpprobe

Source: https://tailscale.com/docs/reference/derp-servers/custom-derp-servers

This command utilizes the `derpprobe` binary to monitor the health and functionality of your custom DERP servers. You must provide a `--derp-map` URL pointing to a JSON document containing your DERP map configuration.

```bash
cmd/derpprobe --derp-map=file:///path/to/your/derp-map.json
```

--------------------------------

### Expose Multiple Services with a Single Kubernetes Ingress to Tailnet

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Use a single Kubernetes Ingress resource to front multiple backend services. This is done by defining multiple rules within the `spec.rules.http.paths` section, each mapping a specific path to a service.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress
spec:
  ingressClassName: tailscale
  rules:
    - http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: ui-svc
                port:
                  number: 80
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: api-svc
                port:
                  number: 80

```

--------------------------------

### Tailscale ACL Configuration (JSON)

Source: https://tailscale.com/docs/reference/examples/acls

This JSON configuration defines Tailscale Access Control Lists (ACLs) to manage network access. It specifies user groups, access rules (accept/deny), tag owners for resource categorization, and tests to verify the ACL logic. This allows for fine-grained control over which users or groups can access specific devices or services based on tags and ports.

```json
{
  "groups": {
    "group:dev": [
      "alice@example.com",
      "bob@example.com"
    ]
  },
  "acls": [
    {
      "action": "accept",
      "src": [
        "autogroup:member"
      ],
      "dst": [
        "autogroup:self:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "group:dev"
      ],
      "dst": [
        "tag:dev:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "autogroup:admin"
      ],
      "dst": [
        "tag:prod:*"
      ]
    },
    {
      "action": "accept",
      "src": [
        "autogroup:member"
      ],
      "dst": [
        "tag:monitoring:80,443"
      ]
    }
  ],
  "tagOwners": {
    "tag:monitoring": [
      "autogroup:admin"
    ],
    "tag:dev": [
      "autogroup:admin"
    ],
    "tag:prod": [
      "autogroup:admin"
    ]
  },
  "tests": [
    {
      "src": "carl@example.com",
      "accept": [
        "tag:prod:80"
      ]
    },
    {
      "src": "alice@example.com",
      "accept": [
        "tag:dev:80"
      ],
      "deny": [
        "tag:prod:80"
      ]
    }
  ]
}
```

--------------------------------

### Tailscale Configuration

Source: https://tailscale.com/docs/reference/tailscale-cli

Configure various resources and settings within your Tailscale network, including Kubernetes integration, macOS VPN settings, Synology connections, system extensions, and Linux systray client.

```APIDOC
## POST /websites/tailscale/configure

### Description
Configure resources and settings for your Tailscale network.

### Method
POST

### Endpoint
/websites/tailscale/configure

### Parameters
#### Query Parameters
- **subcommand** (string) - Required - The configuration subcommand to execute (e.g., kubeconfig, mac-vpn, synology, sysext, systray).

#### Request Body (Conditional based on subcommand)

**For `kubeconfig`:**
- **hostname** (string) - Required - The hostname or FQDN of the auth proxy.
- **http** (boolean) - Optional - Use HTTP instead of HTTPS. Ignored if scheme is included in hostname.

**For `mac-vpn`:**
- **action** (string) - Required - 'install' or 'uninstall'.

**For `sysext`:**
- **action** (string) - Required - 'activate', 'deactivate', or 'status'.

**For `systray`:**
- **enable_startup** (string) - Optional - The init system for startup script installation (e.g., 'systemd').

### Request Example
```json
{
  "subcommand": "kubeconfig",
  "hostname": "auth.example.com",
  "http": false
}
```
```json
{
  "subcommand": "mac-vpn",
  "action": "install"
}
```
```json
{
  "subcommand": "systray",
  "enable_startup": "systemd"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation of the configuration action.

#### Response Example
```json
{
  "message": "kubectl configured successfully."
}
```
```

--------------------------------

### ACL to Grant Conversion: Wildcard Ports

Source: https://tailscale.com/docs/reference/migrate-acls-grants

Demonstrates how to convert an ACL using a wildcard for ports to a grant. The wildcard '*' is used in the 'ip' field to signify access to all ports on the specified destination tag.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": ["group:prod"],
      "dst": ["tag:database:*"]
    }
  ]
}

```

```json
{
  "grants": [
    {
      "src": ["group:prod"],
      "dst": ["tag:database"],
      "ip": ["*"]
    }
  ]
}

```

--------------------------------

### Activate Tailscale System Extension on macOS

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Registers the Tailscale system extension with macOS, enabling its core networking functionalities. This is necessary for the Standalone variant of macOS.

```bash
tailscale configure sysext activate
```

--------------------------------

### Set Auth Key for Managed Devices (macOS/iOS/tvOS/Windows/Android)

Source: https://tailscale.com/docs/features/tailscale-system-policies

Allows specifying an authentication key to automatically authenticate managed devices without user interaction. This policy (`AuthKey`) is crucial for headless devices but carries security risks if the MDM solution is compromised. It's recommended to use one-off auth keys with specific tags and access control policies.

```text
A Tailscale auth key. We recommend you use a one-off auth key.
```

--------------------------------

### Enable Kubernetes API Request Event Recording with Tailscale

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/session-recording

This configuration enables recording of both kubectl sessions and Kubernetes API request events. It directs recorded sessions to a specified trecorder instance and enables event recording via the `enableEvents` flag.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": ["group:engineering"],
      "dst": ["tag:k8s-operator:443"]
    }
  ],
  "grants": [
    {
      "src": ["group:engineering"],
      "dst": ["tag:k8s-operator"],
      "app": {
        "tailscale.com/cap/kubernetes": [{
          "recorder":        ["tag:tsrecorder"],
          "enableEvents":    true
        }]
      }
    }
  ]
}
```

--------------------------------

### Expose Tailscale Web Interface using CLI

Source: https://tailscale.com/docs/features/client/device-web-interface

Commands to expose the Tailscale web interface using the Tailscale CLI. 'tailscale web' exposes it in foreground mode, which stops when the session ends. 'tailscale set --webclient' exposes it persistently in the background.

```bash
tailscale web

```

```bash
tailscale set --webclient

```

--------------------------------

### Allow Masquerading with firewalld

Source: https://tailscale.com/docs/features/exit-nodes?tab=linux

Enables masquerading on Linux systems using firewalld, which can be a necessary workaround for known issues when routing traffic through a Tailscale exit node.

```shell
firewall-cmd --permanent --add-masquerade
```

--------------------------------

### Define macOS Device Encryption Posture (SentinelOne)

Source: https://tailscale.com/docs/solutions/protect-postgresql-unencrypted-macbooks

This snippet defines a device posture policy for macOS devices using SentinelOne integration. It checks for macOS version, Tailscale release track, and application encryption status. Devices must meet all criteria to be compliant.

```json
"postures": {
  "posture:encryptedMacBook": [
    "node:os == 'macos'",
    "node:osVersion >= '13.4.0'",
    "node:tsReleaseTrack == 'stable'",
    "sentinelOne:encryptedApplications == true"
  ]
}
```

--------------------------------

### Enable Port Forwarding on Linux (sysctl.conf)

Source: https://tailscale.com/docs/features/exit-nodes?tab=linux

Enables IPv4 and IPv6 forwarding on Linux systems without a `/etc/sysctl.d` directory by modifying the main sysctl configuration file. This is necessary for Linux devices acting as Tailscale exit nodes.

```shell
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p /etc/sysctl.conf
```

--------------------------------

### Node Information Data Structure (Go)

Source: https://tailscale.com/docs/features/logging/network-flow-logs

Defines the data structure for node information, including OS, User, and Tags. The 'User' field is not populated if the node is tagged, and 'Tags' are not populated if the node is owned by a user. This structure is used for representing node metadata.

```Go
type NodeInfo struct {
  OS   string   `json:"os"` // for example, "linux"
  User string `json:"user"` // for example, "johndoe@example.com"
  Tags []string `json:"tags"` // for example, ["tag:prod","tag:logs"]
}
```

--------------------------------

### Deploy Nginx with Tailscale Sidecar

Source: https://tailscale.com/docs/kubernetes

Deploys a sample Nginx pod with a Tailscale sidecar container. This exposes the Nginx service over Tailscale, enabling bi-directional connectivity without public internet exposure. Authentication can be handled via an auth key or by logging in using a URL from the logs.

```bash
make sidecar | kubectl apply -f-
# If not using an auth key, authenticate by grabbing the Login URL here:
kubectl logs nginx ts-sidecar
```

--------------------------------

### Deploy tsrecorder with IAM Roles (Docker)

Source: https://tailscale.com/docs/features/tailscale-ssh/how-to/session-recording-s3

This command deploys the tsrecorder container, retrieving AWS credentials from the metadata service via an attached IAM role. It mounts a volume for state storage and specifies the S3 destination bucket.

```docker
docker run --name tsrecorder --rm -it \
  -e TS_AUTHKEY=$TS_AUTHKEY \
  -v $HOME/tsrecorder:/data \
  tailscale/tsrecorder:stable \
  /tsrecorder --dst='s3://s3.us-east-2.amazonaws.com' --statedir=/data/state \
  --bucket=$S3_BUCKET_NAME --ui \

```

--------------------------------

### Add Static Routes on Linux (Tailscale)

Source: https://tailscale.com/docs/features/site-to-site

Adds static routes to a Linux device to direct traffic to specific subnets via a designated router. These commands are not persistent across reboots and may require additional configuration for persistence.

```bash
ip route add <first-subnet-CIDR> via <first-subnet-router-IP-address>
ip route add <second-subnet-CIDR> via <second-subnet-router-IP-address>
```

--------------------------------

### Create GitHub Actions Workflow Directory Structure

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This command creates the necessary directory structure for GitHub Actions workflows within a repository. It ensures that the '.github/workflows' directory exists, which is where workflow definition files should be placed.

```bash
mkdir -p .github/workflows
```

--------------------------------

### get-authkey Utility

Source: https://tailscale.com/docs/features/oauth-clients

A utility to generate new authentication keys for scripts and automation. It uses environment variables for OAuth client credentials and accepts parameters for key type and tags.

```APIDOC
## get-authkey Utility

### Description
Generates a new authentication key using environment variables for OAuth client ID and secret. This utility is useful for automating Tailscale node registration.

### Method
CLI Command (Go program)

### Endpoint
N/A (CLI command)

### Prerequisites
- Go 1.23 or later.
- Environment variables `TS_API_CLIENT_ID` and `TS_API_CLIENT_SECRET` must be set.

### Command Usage
**Building and running directly:**
```bash
export TS_API_CLIENT_ID=<clientID>
export TS_API_CLIENT_SECRET=<secret>
go run tailscale.com/cmd/get-authkey@latest -tags tag:development
```

**Running from a local repository:**
```bash
git clone https://github.com/tailscale/tailscale.git
cd tailscale
go run ./cmd/get-authkey/main.go -tags tag:development
```

### Parameters
- **-tags** (string) - Required - A comma-separated list of tags to apply to the auth key.
- **-reusable** (boolean) - Optional - Allocate a reusable auth key (defaults to `false`).
- **-ephemeral** (boolean) - Optional - Allocate an ephemeral auth key (defaults to `false`).
- **-preauth** (boolean) - Optional - Allocate the auth key as pre-authorized (defaults to `true`).

### Response
Outputs the generated authentication key to standard output (stdout).

### Response Example
```
tskey-abcdefghijklmnopqrstuvwxyz1234567890
```
```

--------------------------------

### Tailscale Policy File with Google Groups

Source: https://tailscale.com/docs/integrations/google-sync

This JSON snippet demonstrates how to define access control rules in a Tailscale policy file, referencing groups synced from Google Workspace. It shows different source groups ('group:admins@example.com', 'group:employees@example.com', 'group:engineering@example.com') and their corresponding destinations and IP access.

```json
{
  "grants": [
    {
      "src": ["group:admins@example.com"],
      "dst": ["*"],
      "ip": ["*"]
    },
    {
      "src": ["group:employees@example.com"],
      "dst": ["autogroup:self"],
      "ip": ["*"]
    },
    {
      "src": ["group:engineering@example.com"],
      "dst": ["tag:logging"],
      "ip": ["*"]
    }
  ]
}
```

--------------------------------

### Configure Tailscale Port on Linux

Source: https://tailscale.com/docs/reference/connection-types

This configuration snippet shows how to set a custom port for the Tailscale daemon on Linux systems. By modifying the default configuration file, users can specify a different UDP port for Tailscale to use, which can help in scenarios where the default port might be blocked or restricted.

```bash
# On Linux, you can set this in /etc/defaults/tailscaled.
# Example: tailscaled --port=41641

```

--------------------------------

### GitLab CI Configuration for Syncing Tailscale ACLs

Source: https://tailscale.com/docs/integrations/gitlab/gitops

This GitLab CI configuration uses a template to sync Tailscale ACLs. It requires API key and tailnet ID secrets to be set up in GitLab. The configuration defines 'test' and 'apply' stages that run on merge request events and pushes to the main branch, respectively.

```yaml
include:
  - project: 'tailscale-dev/gitops-acl-ci'
    ref: main
    file: 'acls.gitlab-ci.yaml'
    inputs:
      api-key: $TS_API_KEY
      tailnet: $TS_TAILNET

stages:
  - test
  - apply

test:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "merge_request_event" && $CI_MERGE_REQUEST_TARGET_BRANCH_NAME == $CI_DEFAULT_BRANCH'

apply:
  rules:
    - if: '$CI_PIPELINE_SOURCE == "push" && $CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'

```

--------------------------------

### Configure Tailscale Serve for PiKVM Web Interface

Source: https://tailscale.com/docs/integrations/pikvm

This command sets up Tailscale Serve to proxy the PiKVM's web interface. This ensures a valid TLS certificate for your PiKVM device, preventing browser security warnings. The server is only accessible over your tailnet.

```bash
tailscale serve --bg https+insecure://localhost:443
```

--------------------------------

### Import tsnet Package in Go Program

Source: https://tailscale.com/docs/features/tsnet

This Go code snippet demonstrates how to import the tsnet package into your main program file. This is a prerequisite for utilizing tsnet's functionalities, such as creating a server instance.

```go
package main

import (
    "flag"
    "fmt"
    "html"
    "log"
    "net/http"
    "strings"

    "tailscale.com/tsnet"
)

```

--------------------------------

### Tailscale System Policy Configuration via AppConfig (XML)

Source: https://tailscale.com/docs/integrations/mdm/ios

This XML snippet demonstrates how to configure system policies for the Tailscale app on iOS/tvOS using the AppConfig standard. It's deployed via an MDM solution and allows administrators to set client-side configurations like the organization name. Note that not all policies are supported on tvOS.

```xml
<dict>
<key>ManagedByOrganizationName</key>
<string>Tailscale, Inc.</string>
</dict>
```

--------------------------------

### Define ProxyGroup and ProxyClass Resources

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

Defines a `ProxyGroup` for ingress proxies and a `ProxyClass` using Let's Encrypt's staging environment. This configuration sets up Tailscale devices to act as proxies for ingress traffic.

```yaml
apiVersion: tailscale.com/v1alpha1
kind: ProxyGroup
metadata:
  name: ingress-proxies
spec:
  type: ingress
  hostnamePrefix: eu-west
  replicas: 2
  tags: ["tag:ingress-proxies"]
  proxyClass: letsencrypt-staging
---
apiVersion: tailscale.com/v1alpha1
kind: ProxyClass
metadata:
  name: letsencrypt-staging
spec:
  useLetsEncryptStagingEnvironment: true

```

--------------------------------

### Tailscale Funnel Command Syntax

Source: https://tailscale.com/docs/reference/tailscale-cli/funnel

The basic syntax for the `tailscale funnel` command. It accepts various flags to configure how a local service is shared over the internet. The `<target>` can be a file, directory, text, or a local service address.

```bash
tailscale funnel [flags] <target>
```

--------------------------------

### Serve Local Content via Tailscale Funnel

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Serves local content and servers from your Tailscale node to the internet. Use the `serve` command to limit access to your tailnet.

```bash
tailscale funnel <target>
```

```bash
tailscale funnel <subcommand> [flags] <args>
```

--------------------------------

### Enable Automatic Subnet Route Discovery on Linux

Source: https://tailscale.com/docs/features/subnet-routers?tab=windows

Configures Linux devices to automatically discover and accept new subnet routes advertised by Tailscale subnet routers. This command ensures seamless connectivity to resources behind the subnet router without manual route configuration on each client.

```bash
sudo tailscale set --accept-routes
```

--------------------------------

### Check Existing Firewall Rules with ufw

Source: https://tailscale.com/docs/how-to/secure-ubuntu-server-with-ufw

Displays the current status and verbose rules of the ufw firewall. This command is useful for auditing existing configurations and identifying rules that need to be maintained or modified.

```bash
sudo ufw status verbose
```

--------------------------------

### Configure Mullvad License Pool Sharing in Tailscale Policy

Source: https://tailscale.com/docs/features/exit-nodes/mullvad-exit-nodes?tab=linux

This configuration snippet for the Tailscale policy file allows devices within the 'mullvad' group to use Mullvad exit nodes. It assigns the 'mullvad' attribute to the specified group, enabling license sharing on a first-come, first-served basis.

```json
{
  "nodeAttrs": [
    {
      "target": ["group:mullvad"],
      "attr": [
        "mullvad"
      ]
    }
  ]
}
```

--------------------------------

### Log into Tailscale Network with CLI

Source: https://tailscale.com/docs/reference/tailscale-cli

The `tailscale login` command logs a device into your Tailscale network. It offers numerous flags to configure DNS settings, route advertisement, exit node usage, authentication methods, and more. This command is essential for adding a device to your Tailscale network.

```bash
tailscale login [flags]
```

--------------------------------

### Manual Tailscale Update Command

Source: https://tailscale.com/docs/features/client/update?tab=linux

This command initiates a manual update for the Tailscale client on supported Linux distributions, provided you are using Tailscale v1.36 or later.

```bash
tailscale update
```

--------------------------------

### Configure Google Cloud Workload Identity Federation for Log Streaming

Source: https://tailscale.com/docs/features/logging/log-streaming?tab=google+cloud+storage

These commands set up a Google Cloud workload identity pool and provider, specifically for AWS, enabling secure authentication for log streaming. The `account-id` attribute must be set to `891612552178` when adding the AWS provider.

```bash
gcloud iam workload-identity-pools create <tailnet-logstreaming-pool> \
  -location="global" \
  --display-name="Logstreaming Pool"
```

```bash
gcloud iam workload-identity-pools providers create-aws <tailnet-aws-provider> \
  --location="global" \
  --workload-identity-pool="<tailnet-logstreaming-pool>" \
  --account-id="891612552178" \
  --display-name="AWS provider for logstreaming"
```

```bash
gcloud iam service-accounts add-iam-policy-binding \
  <tailnet-uploader>@<project>.iam.gserviceaccount.com \
  --role="roles/iam.workloadIdentityUser" \
  --member="principalSet://iam.googleapis.com/projects/<project-number>/locations/global/workloadIdentityPools/<tailnet-logstreaming-pool>/*"
```

--------------------------------

### Initiate SSH Connection to a VM via Tailscale

Source: https://tailscale.com/docs/how-to/connect-ssh-linux-vm

This command establishes an SSH connection to a VM on your Tailscale network from your local machine. You can use either the VM's Tailscale IP address or its MagicDNS hostname. Optionally, you can specify a local username to use for the connection.

```bash
ssh <your-vm-ip-address>

```

```bash
ssh local-user@100.64.65.66

```

--------------------------------

### Tailscale GitHub Action Authentication

Source: https://tailscale.com/docs/features/workload-identity-federation?tab=github+actions

Demonstrates how to use workload identity to authenticate the Tailscale GitHub Action. Requires specific permissions and arguments for the action.

```APIDOC
## Tailscale GitHub Action

### Description
Authenticates the Tailscale GitHub Action using workload identity. This involves setting specific `with` arguments and `permissions` for the workflow.

### Method
N/A (Configuration within GitHub Actions workflow)

### Endpoint
N/A

### Parameters
#### Workflow `permissions`
- **id-token** (string) - Required - Must be set to `write` to allow the action to request a JWT from GitHub.

#### Action `with` arguments
- **oauth-client-id** (string) - Required - Your Tailscale OAuth Client ID.
- **audience** (string) - Required - The audience for the token exchange.
- **tags** (string) - Optional - Tags to apply to the authenticated node (e.g., `tag:ci`).

### Request Example
```yaml
- name: Tailscale
  uses: tailscale/github-action@v4
  with:
    oauth-client-id: "${{ secrets.TS_OAUTH_CLIENT_ID }}"
    audience: "${{ secrets.TS_AUDIENCE }}"
    tags: "tag:ci"
```

### Workflow Permissions Example
```yaml
permissions:
  id-token: write # Required for the tailscale action to request a JWT from GitHub
  # Additional required permissions for your workflow
```
```

--------------------------------

### Configure Kubernetes Device Plugin for /dev/net/tun Devices

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/customize

This command configures a generic Kubernetes device plugin to create `/dev/net/tun` devices, which are required for Tailscale proxies. It specifies the device name as 'tun' and allows for up to 1000 devices. This is part of a process to restrict Tailscale container permissions and delegate device creation.

```bash
--device='{"name": "tun", "groups": [{"paths": [{"path": "/dev/net/tun"}]}, "count": 1000]}'

```

--------------------------------

### Joining an Unlisted Tailnet via URL

Source: https://tailscale.com/docs/features/multiple-tailnets

This URL demonstrates how a user can join an unlisted Tailscale tailnet by appending the 'tailnet' query parameter with the specific tailnet ID. This method bypasses the standard tailnet selector UI for users who have not yet joined the tailnet.

```url
https://login.tailscale.com/welcome?tailnet=T123456789CNTRL
```

--------------------------------

### Connect via Tailscale IP Address

Source: https://tailscale.com/docs/reference/ssh-over-tailscale

Connect to your SSH server using its Tailscale IP address. This method requires you to first find the server's IP using the `tailscale ip` command. The connection is established using the standard SSH command format.

```bash
ssh username@100.100.123.123
```

--------------------------------

### Request Tailscale Certificate

Source: https://tailscale.com/docs/solutions/code-on-ipad-vscode-caddy-code-server

This command requests a Let's Encrypt certificate for your Tailscale domain. It requires your machine name and tailnet name. The output confirms the creation of certificate and key files.

```bash
sudo tailscale cert machine-name.tailnet-name.ts.net
```

--------------------------------

### Check Network Conditions with Tailscale CLI

Source: https://tailscale.com/docs/solutions/migrate-legacy-vpn-tailscale

This command provides a report on your current physical network conditions and the status of your connection to Tailscale's DERP servers. It's useful for diagnosing connectivity issues and understanding network latency.

```bash
tailscale netcheck --verbose
```

--------------------------------

### Tailscale Ping Command Showing DERP Relayed Connection

Source: https://tailscale.com/docs/reference/connection-types

This command demonstrates how a Tailscale ping between two devices might show a relayed connection via a DERP server. It highlights the latency introduced by using a relay and indicates when a direct connection is not established. This output is typical when network conditions prevent direct peer-to-peer communication.

```bash
> user@your-device:~$ tailscale ping another-device
pong from another-device (100.104.93.78) via DERP(tor) in 53ms
pong from another-device (100.104.93.78) via DERP(tor) in 196ms
pong from another-device (100.104.93.78) via DERP(tor) in 50ms
pong from another-device (100.104.93.78) via DERP(tor) in 214ms
pong from another-device (100.104.93.78) via DERP(tor) in 273ms
pong from another-device (100.104.93.78) via DERP(tor) in 274ms
pong from another-device (100.104.93.78) via DERP(tor) in 282ms
pong from another-device (100.104.93.78) via DERP(tor) in 273ms
pong from another-device (100.104.93.78) via DERP(tor) in 76ms
pong from another-device (100.104.93.78) via DERP(tor) in 152ms
direct connection not established

```

--------------------------------

### Enable Device Identity Collection via CLI (Linux, macOS, Windows)

Source: https://tailscale.com/docs/features/access-control/device-management/how-to/manage-identity?tab=macos

Commands to enable device identity collection using the `tailscale set` CLI command. This method is the primary way for Linux devices and an alternative for macOS and Windows. Requires restarting the Tailscale client for changes to take effect.

```bash
tailscale set --posture-checking=true
tailscale down
tailscale up
```

```bash
/Applications/Tailscale.app/Contents/MacOS/Tailscale set --posture-checking=true
/Applications/Tailscale.app/Contents/MacOS/Tailscale down
/Applications/Tailscale.app/Contents/MacOS/Tailscale up
```

--------------------------------

### Provider Configuration API

Source: https://tailscale.com/docs/features/aperture/configuration

The `providers` section in the configuration allows you to define and manage different LLM providers. Each provider is configured with its base URL, available models, authentication details, and compatibility flags.

```APIDOC
## Provider Configuration

### Description
Defines the LLM providers to which Aperture routes requests. Each provider is identified by a unique string key.

### Method
N/A (Configuration Section)

### Endpoint
N/A (Configuration Section)

### Parameters
#### Provider Fields
- **`baseurl`** (string) - Required - Base URL for the provider's API.
- **`models`** (array) - Required - List of model IDs available from this provider.
- **`apikey`** (string) - Optional - API key for authentication. Defaults to `""`.
- **`authorization`** (string) - Optional - Authorization header type. Defaults to `"bearer"`.
- **`tailnet`** (boolean) - Optional - Route requests over the tailnet. Defaults to `false`.
- **`name`** (string) - Optional - Display name for the UI. Defaults to `""`.
- **`description`** (string) - Optional - Description shown in the UI. Defaults to `""`.
- **`compatibility`** (object) - Optional - API compatibility flags. Varies by provider.

#### Authorization Types
- **`bearer`**: `Authorization: Bearer <key>` (Used by OpenAI and most providers)
- **`x-api-key`**: `x-api-key: <key>` (Used by Anthropic)
- **`x-goog-api-key`**: `x-goog-api-key: <key>` (Used by Google Gemini)

#### Provider Compatibility Fields
- **`openai_chat`** (boolean) - Supports `/v1/chat/completions`. Defaults to `true`.
- **`openai_responses`** (boolean) - Supports `/v1/responses`. Defaults to `false`.
- **`anthropic_messages`** (boolean) - Supports `/v1/messages`. Defaults to `false`.
- **`gemini_generate_content`** (boolean) - Supports Gemini API format. Defaults to `false`.
- **`bedrock_model_invoke`** (boolean) - Supports Amazon Bedrock format. Defaults to `false`.
- **`google_generate_content`** (boolean) - Supports Vertex AI Gemini format. Defaults to `false`.
- **`google_raw_predict`** (boolean) - Supports Vertex AI raw predict for Anthropic models. Defaults to `false`.

### Request Example
```json
{
  "providers": {
    "openai": {
      "baseurl": "https://api.openai.com/",
      "apikey": "YOUR_OPENAI_KEY",
      "models": ["gpt-5", "gpt-5-mini", "gpt-4.1"],
      "name": "OpenAI",
      "description": "OpenAI models",
      "compatibility": {
        "openai_chat": true,
        "openai_responses": true
      }
    },
    "anthropic": {
      "baseurl": "https://api.anthropic.com",
      "apikey": "YOUR_ANTHROPIC_KEY",
      "authorization": "x-api-key",
      "models": ["claude-sonnet-4-5", "claude-haiku-4-5", "claude-opus-4-5"],
      "compatibility": {
        "anthropic_messages": true
      }
    }
  }
}
```

### Response
N/A (Configuration Section)
```

--------------------------------

### Enable Bash Tab Completion (Linux)

Source: https://tailscale.com/docs/reference/tailscale-cli

This command loads Tailscale CLI tab completions for the Bash shell on Linux. It sources the completion script, enabling command suggestions as you type.

```bash
source <(tailscale completion bash)

```

--------------------------------

### Configure Subnet Router with CLI Flags

Source: https://tailscale.com/docs/features/site-to-site

Use `tailscale up` or `tailscale set` commands to configure subnet router options. The `--advertise-routes` flag specifies the CIDR range to expose, and `--snat-subnet-routes=false` (Linux only) disables source NAT for direct IP visibility.

```bash
tailscale up --advertise-routes=<CIDR>
tailscale set --snat-subnet-routes=false
```

--------------------------------

### Configure Tailscale Exit Node on Client

Source: https://tailscale.com/docs/features/exit-nodes?tab=linux

Configures a client device to use a specific Tailscale exit node for its internet traffic. Replace `<exit-node-ip>` with the actual Tailscale IP address of your exit node.

```shell
sudo tailscale set --exit-node=<exit-node-ip>
```

```shell
sudo tailscale set --exit-node=<exit-node-ip> --exit-node-allow-lan-access=true
```

```shell
sudo tailscale set --exit-node=
```

--------------------------------

### Set Custom Posture Attribute

Source: https://tailscale.com/docs/features/tailscale-accessbot-jit

Creates or updates a custom posture attribute on a specified device. Custom attributes must be in the `custom` namespace.

```APIDOC
## POST /api/v2/device/{deviceID}/attributes/{attributeKey}

### Description
Create or update a custom posture attribute on the specified device. User-managed attributes must be in the `custom` namespace, which is indicated by prefixing the attribute key with `custom:`.

### Method
POST

### Endpoint
/api/v2/device/{deviceID}/attributes/{attributeKey}

#### Path Parameters
- **deviceID** (string) - Required - The ID of the device on which to set the custom posture attribute.
- **attributeKey** (string) - Required - The key of the custom attribute to set (e.g., `custom:accessLevel`).

#### Request Body
- **value** (any) - Required - The value to assign to the attribute. Can be a string, number, or boolean.
- **expiry** (string) - Optional - The expiry time for the attribute in RFC 3339 format (e.g., `2024-04-23T18:25:43Z`).

### Response
#### Success Response (200 or 204)
Indicates the attribute was successfully set or updated. No response body is typically returned for a successful POST request of this nature.
```

--------------------------------

### Register New Nodes

Source: https://tailscale.com/docs/features/workload-identity-federation?tab=google+cloud

Register new nodes to your Tailnet using the `tailscale up` command with workload identity federation, supporting direct token exchange or automatic cloud token discovery.

```APIDOC
## Register New Nodes using Workload Identity

### Description
Registers a new node to your Tailnet using workload identity federation. This can be done by directly providing a client ID and OIDC token, or by enabling automatic cloud token discovery.

### Method
`tailscale up` command

### Endpoint
N/A (Command-line interface)

### Parameters
#### Command Flags
- **--client-id** (string) - Required - The Client ID used to generate auth keys with workload identity federation. Can include URL parameters like `?ephemeral=false&preauthorized=true`.
  - `ephemeral` (boolean) - Optional - Register as an ephemeral node (defaults to `true`).
  - `preauthorized` (boolean) - Optional - Skip manual device approval (defaults to `false`).
- **--id-token** (string) - Required (when not using automatic discovery) - The ID token from the identity provider to exchange with the control server.
- **--audience** (string) - Required (when using automatic discovery) - The audience specified in the trust configuration for the federated identity.
- **--advertise-tags** (string) - Required - Tags to advertise for the node, must match tags configured in federated identity.

### Request Example (Direct Token Exchange)
```bash
tailscale up --client-id=${CLIENT_ID} --id-token=${IDENTITY_TOKEN} --advertise-tags=tag:ci
```

### Request Example (with URL parameters)
```bash
tailscale up --client-id='${CLIENT_ID}?ephemeral=false&preauthorized=true' --id-token=${IDENTITY_TOKEN} --advertise-tags=tag:ci
```

### Request Example (Automatic Cloud Token Discovery)
```bash
tailscale up --client-id=${CLIENT_ID} --audience=${AUDIENCE} --advertise-tags=tag:ci
```

### Response
N/A (Command-line operation)

### Error Handling
Error details for token exchange can be found in the Tailscale admin console under Trust credentials.
```

--------------------------------

### Connect to a Tailscale Host using IP Address via SSH

Source: https://tailscale.com/docs/features/tailscale-ssh

Connect to a Tailscale host using its persistent Tailscale IP address. This method ensures connectivity even if the device's network changes.

```bash
ssh user@100.64.0.1
```

--------------------------------

### Assign Tag to Monitoring Gateway Server (CLI)

Source: https://tailscale.com/docs/solutions/protect-postgresql-unencrypted-macbooks

This command assigns the 'tag:db-gateway' tag to the monitoring gateway server using the Tailscale CLI. This allows the server to be identified and managed with this specific tag.

```bash
sudo tailscale login --advertise-tags=tag:db-gateway
```

--------------------------------

### Configure Kubernetes with Tailscale

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=zsh

Configures kubectl to connect to a Kubernetes cluster using Tailscale. This command requires a hostname or FQDN as an argument and may use HTTP or HTTPS for the auth proxy connection.

```bash
tailscale configure kubeconfig <hostname-or-fqdn>
tailscale configure kubeconfig <hostname-or-fqdn> --http
```

--------------------------------

### Define Tag Owners in Tailnet Policy File (JSON)

Source: https://tailscale.com/docs/features/tags

This JSON snippet demonstrates how to define tag owners in the tailnet policy file. It shows the creation of a tag named 'tag:server' and assigns 'dave@example.com' as its sole owner, who is the only one permitted to authenticate devices with this tag.

```json
{
  "tagOwners": {
    "tag:server": ["dave@example.com"] // dave@example.com can authenticate devices with the tag:server tag
  }
}
```

--------------------------------

### Advertise Subnet Routes for Failover

Source: https://tailscale.com/docs/how-to/set-up-high-availability

This command configures a machine to act as a subnet router and advertise specific IP address ranges. Running this on multiple machines with the same routes enables failover, ensuring traffic is rerouted if one router becomes unavailable.

```bash
sudo tailscale set --advertise-routes=10.0.0.0/24,10.1.0.0/24
```

--------------------------------

### Configure Tailscale CLI Tab-Completion

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

The `completion` command helps configure tab-completion for the Tailscale CLI in various shells like bash, zsh, fish, and PowerShell. Flags `--flags` and `--descs` control whether to suggest flags and descriptions for subcommands, respectively.

```bash
tailscale completion bash
tailscale completion zsh
tailscale completion fish
tailscale completion powershell
tailscale completion bash --flags=false --descs=false
```

--------------------------------

### Configure Shell Completion for Tailscale CLI

Source: https://tailscale.com/docs/reference/tailscale-cli

Set up tab-completion for the Tailscale CLI in various shells like bash, zsh, fish, and PowerShell. This feature helps in quickly typing commands and their arguments. Options include whether to suggest flags and descriptions.

```bash
tailscale completion <subcommand>

```

--------------------------------

### policy_file:read Scope

Source: https://tailscale.com/docs/reference/trust-credentials

Grants access to read and validate the tailnet policy file. Requires `devices:posture_attributes:read` and `devices:core:read`.

```APIDOC
## policy_file:read Scope

### Description
The credential has access to read and validate the tailnet policy file. `devices:posture_attributes:read` and `devices:core:read` are required when using this scope.

### Allowed Endpoints
* `GET /api/v2/tailnet/:tailnet/acl`
* `POST /api/v2/tailnet/:tailnet/acl/preview`
* `POST /api/v2/tailnet/:tailnet/acl/validate`
```

--------------------------------

### Verify iptables Rules and Tailscale Network Check

Source: https://tailscale.com/docs/reference/messages/client/docker-stateful-filtering

These commands are used to inspect and verify firewall rules and Tailscale's network connectivity. `iptables -L -v` lists the current iptables rules with verbose output, and `tailscale netcheck` performs a network diagnostic.

```bash
iptables -L -v
```

```bash
tailscale netcheck
```

--------------------------------

### Configure Claude Code with Aperture via Vertex AI (JSON)

Source: https://tailscale.com/docs/features/aperture

Configures Claude Code to use Aperture through Google Cloud's Vertex AI. This requires setting Vertex AI-specific environment variables in `settings.json`, including project ID, region, and flags to enable Vertex AI usage and skip authentication.

```json
{
  "env": {
    "CLOUD_ML_REGION": "global",
    "ANTHROPIC_VERTEX_PROJECT_ID": "YOUR_PROJECT_ID",
    "CLAUDE_CODE_USE_VERTEX": "1",
    "CLAUDE_CODE_SKIP_VERTEX_AUTH": "1",
    "ANTHROPIC_VERTEX_BASE_URL": "http://ai/v1"
  }
}
```

--------------------------------

### Grant Management Access to Web Interface (Grants)

Source: https://tailscale.com/docs/features/client/device-web-interface

This configuration snippet demonstrates granting specific management access to a tagged device's web interface using the grants syntax. It allows a specified user to manage Tailscale SSH and subnet routing features for devices tagged as 'dev'. This provides granular control over administrative privileges.

```json
{
  "grants": [
    {
      "src": ["user@example.com"],
      "dst": ["tag:dev"],
      "ip": ["5252"],
      "app": {
        "tailscale.com/cap/webui": [
          {
            // Grants user@example.com edit access to "tag:dev" devices' web interfaces.
            "canEdit": ["ssh", "subnets"]
          }
        ]
      }
    }
  ]
}
```

--------------------------------

### Triggering Hooks with Grants

Source: https://tailscale.com/docs/features/aperture/configuration

Configures hook grants within `temp_grants` to trigger specific webhooks based on request matching criteria and data inclusion.

```APIDOC
## Triggering Hooks with Grants

### Description
To trigger a hook, add a hook grant to a policy in the `temp_grants` section. Hook grants specify which requests trigger the hook and what data to include.

### Method
N/A (Configuration Section)

### Endpoint
N/A (Configuration Section)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
**temp_grants** (array) - Required - A list of grant configurations.

**grant configuration** (object) - Required - Configuration for a single grant.
- **src** (array of strings) - Required - Specifies the source(s) that trigger this grant. Use `"*"` to match any source.
- **grants** (array of objects) - Required - A list of grants to apply.
  - **hook** (object) - Required - Configuration for the hook grant.
    - **match** (object) - Required - Conditions that determine when the hook triggers. All non-empty fields must match (AND logic). Within each field, any element matching is sufficient (OR logic).
      - **providers** (array of strings) - Optional - Provider IDs to match. Use `"*"` to match any provider.
      - **models** (array of strings) - Optional - Model IDs to match. Use `"*"` to match any model.
      - **events** (array of strings) - Required - Event types that trigger the hook. Available events: `tool_call_entire_request`.
    - **hook** (string) - Required - Key referencing a hook defined in the top-level `hooks` section.
    - **fields** (array of strings) - Required - List of data fields to include in the hook payload. Available fields: `tools`, `request_body`, `user_message`, `response_body`, `raw_responses`.

### Request Example
```json
{
  "temp_grants": [
    {
      "src": ["*"],
      "grants": [
        {
          "hook": {
            "match": {
              "providers": ["*"],
              "models": ["*"],
              "events": ["tool_call_entire_request"]
            },
            "hook": "oso",
            "fields": ["user_message", "tools", "request_body", "response_body"]
          }
        }
      ]
    }
  ]
}
```

### Response
N/A (Configuration Section)

#### Success Response (200)
N/A

#### Response Example
N/A
```

--------------------------------

### Kubernetes Recorder Resource Definition

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/tsrecorder

Defines a basic Recorder resource for Tailscale's Kubernetes operator. This configuration saves recordings to a local temporary directory, persisting only for the pod's lifetime. Ensure the 'apiVersion' and 'kind' are correctly set for your Kubernetes environment.

```yaml
apiVersion: tailscale.com/v1alpha1
kind: Recorder
metadata:
  name: recorder
spec:
  enableUI: true

```

--------------------------------

### Assign Auth Key to Server (Go)

Source: https://tailscale.com/docs/features/tsnet/how-to/create-basic-tsnet-app

Assigns a provided Tailscale authentication key to the tsnet.Server object. This enables programmatic authentication for the device.

```go
flag.Parse()

srv := new(tsnet.Server)
srv.AuthKey = *tsAuthKey
```

--------------------------------

### Ping Another Device using Tailscale App (Android)

Source: https://tailscale.com/docs/solutions/migrate-legacy-vpn-tailscale

For Android users, this describes how to ping another device within the Tailscale app. It initiates ten ping attempts and displays the results, provided the target device is connected.

```java
// On Android, open the Tailscale app.
// The app shows the list of devices in your tailnet.
// Long press one of the other devices and then select the Count Down Timer icon.
// The app shows the result of ten pings from your device to the other device, unless the other device is not connected.
```

--------------------------------

### Access Taildrive Shares on Synology (WebDAV)

Source: https://tailscale.com/docs/features/taildrive?tab=synology

Configuration steps to access Taildrive shares on Synology File Station using WebDAV. Requires setting up a remote connection with specific hostname and port.

```bash
Hostname or IP: 100.100.100.100
Port: 8080
Account Name: (blank)
Password: (blank)
Codepage: Unicode (UTF-8)
```

--------------------------------

### Webhook Configuration

Source: https://tailscale.com/docs/features/aperture/configuration

Defines webhook endpoints that Aperture calls when specific conditions are met. Each hook is identified by a unique string key.

```APIDOC
## Webhook Configuration

### Description
Defines webhook endpoints that Aperture calls when specific conditions are met. Each hook is identified by a unique string key.

### Method
N/A (Configuration Section)

### Endpoint
N/A (Configuration Section)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
**hooks** (object) - Required - A map of hook keys to their configurations.

**hook configuration** (object) - Required - Configuration for a single webhook.
- **url** (string) - Required - HTTP or HTTPS endpoint to POST hook data to.
- **apikey** (string) - Optional - API key sent in the `Authorization: Bearer` header. Defaults to `""`.
- **timeout** (string) - Optional - Maximum duration to wait for the hook to respond. Accepts Go duration strings (e.g., `"5s"`, `"1m"`). Defaults to `"5s"`. Set to `"0"` to disable.

### Request Example
```json
{
  "hooks": {
    "oso": {
      "url": "https://api.osohq.com/api/agents/v1/model-request",
      "apikey": "YOUR_OSO_API_KEY",
      "timeout": "10s"
    },
    "my-webhook": {
      "url": "https://example.com/webhook",
      "apikey": "YOUR_API_KEY"
    }
  }
}
```

### Response
N/A (Configuration Section)

#### Success Response (200)
N/A

#### Response Example
N/A
```

--------------------------------

### Set Posture Attribute with Expiry (JSON)

Source: https://tailscale.com/docs/features/tailscale-accessbot-jit

This JSON structure demonstrates how to set a posture attribute's value along with an optional expiry time. The 'expiry' field must be an RFC3339 formatted string representing a future date and time.

```json
{
  "value": "foo",
  "expiry": "2024-04-23T18:25:43.511Z"
}
```

--------------------------------

### View Suggested Exit Node (Tailscale CLI)

Source: https://tailscale.com/docs/features/exit-nodes/auto-exit-nodes

This command allows users to view the suggested exit node provided by Tailscale. It helps in identifying the optimal exit node based on client information like location and latency.

```bash
tailscale exit-node suggest

```

--------------------------------

### Convert IP Ranges/CIDR from ACLs to Grants in Tailscale

Source: https://tailscale.com/docs/reference/migrate-acls-grants

Demonstrates how to convert ACL entries with IP address ranges or CIDR notation to the grants format. The CIDR notation moves to the 'dst' field, while protocol and port specifications are moved to the 'ip' field.

```json
"acls": [
  {
    "action": "accept",
    "src": ["group:devops"],
    "dst": ["192.0.2.0/24:22"],
    "proto": ["tcp"]
  }
]

```

```json
"grants": [
  {
    "src": ["group:devops"],
    "dst": ["192.0.2.0/24"],
    "ip": ["tcp:22"]
  }
]

```

--------------------------------

### Configure Dockerfile for Tailscale on AWS Lightsail

Source: https://tailscale.com/docs/install/cloud/aws/aws-lightsail

This Dockerfile uses a multistage build to create a production image for AWS Lightsail containers. It copies application code from a builder stage and Tailscale binaries from the official Tailscale Docker image. It also sets up necessary directories and symbolic links for Tailscale to function correctly in userspace mode.

```dockerfile
FROM alpine:latest as builder
WORKDIR /app
COPY . ./ 
# This is where one could build the application code as well.

FROM alpine:latest
# Copy binary to production image.
COPY --from=builder /app/bootstrap /var/runtime/bootstrap

# Copy Tailscale binaries from the tailscale image on Docker Hub.
COPY --from=docker.io/tailscale/tailscale:stable /usr/local/bin/tailscaled /var/runtime/tailscaled
COPY --from=docker.io/tailscale/tailscale:stable /usr/local/bin/tailscale /var/runtime/tailscale
RUN mkdir -p /var/run && ln -s /tmp/tailscale /var/run/tailscale && \
    mkdir -p /var/cache && ln -s /tmp/tailscale /var/cache/tailscale && \
    mkdir -p /var/lib && ln -s /tmp/tailscale /var/lib/tailscale && \
    mkdir -p /var/task && ln -s /tmp/tailscale /var/task/tailscale

EXPOSE 8080

# Run on container startup.
ENTRYPOINT ["/var/runtime/bootstrap"]

```

--------------------------------

### Enable IP Forwarding on Linux

Source: https://tailscale.com/docs/features/exit-nodes?tab=linux

Configures the Linux kernel to forward IPv4 and IPv6 traffic, a prerequisite for advertising a device as a Tailscale exit node. This involves modifying sysctl configuration files and applying the changes.

```shell
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.d/99-tailscale.conf
sudo sysctl -p /etc/sysctl.d/99-tailscale.conf
```

```shell
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p /etc/sysctl.conf
```

--------------------------------

### Send Files with Tailscale CLI

Source: https://tailscale.com/docs/features/taildrop?tab=linux

Use the `tailscale file cp` command to send files between devices on your Tailscale network. The command takes the file path and the destination device name or IP address followed by a colon. You can find device names and IPs using `tailscale status`. This method is suitable for various file types and supports resuming interrupted transfers.

```bash
tailscale file cp <files> <name-or-ip>:

# Example:
tailscale file cp ./my-file.txt my-phone:
```

--------------------------------

### Expose Tailscale Ingress in HA Mode

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Creates a Kubernetes `Ingress` resource that references a `ProxyGroup`. This exposes a service within the cluster to the tailnet. The `spec.tls.hosts` field configures the DNS name for the Ingress. Requires a `ProxyGroup` to be pre-configured.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx
  annotations:
    tailscale.com/proxy-group: ingress-proxies
spec:
  defaultBackend:
    service:
      name: nginx
      port:
        number: 80
  ingressClassName: tailscale
  tls:
    - hosts:
        - nginx

```

--------------------------------

### Expose Tailscale Metrics Locally

Source: https://tailscale.com/docs/reference/tailscale-client-metrics

Makes Tailscale metrics accessible on a specific network interface and port. This is useful for exposing metrics to other networks or specific IPs.

```bash
tailscale web --readonly --listen 203.0.113.5:8080
```

--------------------------------

### Create DNSConfig Custom Resource for Tailscale Nameserver

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-egress

This YAML defines a `DNSConfig` custom resource, which instructs the Tailscale Kubernetes Operator to deploy a nameserver. This nameserver will be dynamically populated with DNS records for Tailscale services exposed via cluster egress proxies and for cluster workloads exposed via Tailscale Ingress.

```yaml
apiVersion: tailscale.com/v1alpha1
kind: DNSConfig
metadata:
  name: ts-dns
spec:
  nameserver:
    image:
      repo: tailscale/k8s-nameserver
      tag: unstable

```

--------------------------------

### ACL to Grant Conversion: Multiple Ports on Different Tags

Source: https://tailscale.com/docs/reference/migrate-acls-grants

Shows the conversion of an ACL where multiple destination entries refer to different tags and ports. This requires creating separate grant entries for each unique tag-port combination to maintain distinct permissions.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": ["group:eng"],
      "dst": ["tag:web-server:80", "tag:dev-server:22"]
    }
  ]
}

```

```json
{
  "grants": [
    {
      "src": ["group:eng"],
      "dst": ["tag:web-server"],
      "ip": ["80"]
    },
    {
      "src": ["group:eng"],
      "dst": ["tag:dev-server"],
      "ip": ["22"]
    }
  ]
}

```

--------------------------------

### devices:core Scope

Source: https://tailscale.com/docs/reference/trust-credentials

Grants access to read device information, authorize/remove machines, and manipulate device tags. Requires tag selection during credential creation.

```APIDOC
## devices:core Scope

### Description
The credential has access to read the list of all devices in the tailnet, authorize or remove machines, and manipulate tags on devices. You must select one or more tags when you create a credential with the `devices:core` scope. Auth keys created with this credential must have those exact tags, or tags owned by the credential's tags.

### Allowed Endpoints
* Endpoints from `devices:core:read`
* `DELETE /api/v2/device/:deviceID`
* `POST /api/v2/device/:deviceID/authorized`
* `POST /api/v2/device/:deviceID/expire`
* `POST /api/v2/device/:deviceID/ip`
* `POST /api/v2/device/:deviceID/name`
* `POST /api/v2/device/:deviceID/key`
* `POST /api/v2/device/:deviceID/tags`
```

--------------------------------

### Caddyfile Configuration for Static File Server with Tailscale HTTPS

Source: https://tailscale.com/docs/integrations/web-servers/caddy/caddy-certificates

This Caddyfile configuration demonstrates how to set up a static file server for a Tailscale domain. Caddy automatically enables HTTPS for *.ts.net domains by fetching certificates from the local Tailscale daemon, requiring no extra configuration for certificate management.

```plaintext
machine-name.domain-alias.ts.net

root * /var/www
file_server

```

--------------------------------

### Search Tailscale Recordings with grep

Source: https://tailscale.com/docs/features/tailscale-ssh/tailscale-ssh-session-recording

This command uses `grep` to search for a specific pattern (e.g., 'sudo') within a Tailscale session recording file. Recordings are in the `asciinema` format, which is newline-delimited JSON, making them searchable as plain text.

```bash
grep "sudo" <session-recording.cast>
```

--------------------------------

### Ping Another Device using Tailscale App (iOS)

Source: https://tailscale.com/docs/solutions/migrate-legacy-vpn-tailscale

For iOS users, this describes how to ping another device within the Tailscale app. It initiates ten ping attempts and displays the results, provided the target device is connected.

```swift
// On iOS, open the Tailscale app.
// The app shows the list of devices in your tailnet.
// Long press one of the other devices and then select **Ping**.
// The app shows the result of ten pings from your device to the other device, unless the other device is not connected.
```

--------------------------------

### Configure Claude Code with Aperture via Amazon Bedrock (JSON)

Source: https://tailscale.com/docs/features/aperture

Sets up Claude Code to use Aperture through Amazon Bedrock. This involves configuring specific environment variables in `settings.json`, including the Bedrock base URL and flags to enable Bedrock usage and skip authentication.

```json
{
  "env": {
    "ANTHROPIC_MODEL": "claude-sonnet-4-5",
    "ANTHROPIC_BEDROCK_BASE_URL": "http://ai/bedrock",
    "CLAUDE_CODE_USE_BEDROCK": "1",
    "CLAUDE_CODE_SKIP_BEDROCK_AUTH": "1"
  }
}
```

--------------------------------

### Test DNS Configuration on macOS

Source: https://tailscale.com/docs/reference/dns-in-tailscale

This command tests DNS resolution on macOS by querying the system's cache for host information. It is useful for verifying how macOS resolves domain names or MagicDNS hostnames, especially when split DNS or MagicDNS features are in use.

```bash
dscacheutil -q host -a name <domain-or-magic-dns-hostname>
```

--------------------------------

### Test DNS Resolution on Windows PowerShell

Source: https://tailscale.com/docs/reference/dns-in-tailscale?tab=windows

This snippet demonstrates how to test DNS resolution on Windows using the `Resolve-DnsName` PowerShell cmdlet. This command properly honors Tailscale's Name Resolution Policy Table (NRPT) rules, providing accurate results for split DNS and MagicDNS configurations, unlike the `nslookup` command.

```powershell
Resolve-DnsName -Name <domain-or-magic-dns-hostname>
```

```powershell
PS C:\> Resolve-DnsName -Name my-server

Name                       Type   TTL   Section   IPAddress
----                       ----   ---   -------   ---------
my-server.example.ts.net   AAAA   600   Answer    fd7a:115c:a1e0:ab12:4843:cd96:6251:c348
my-server.example.ts.net   A      600   Answer    100.15.193.72
```

--------------------------------

### Automate Device Approval with Tailscale API

Source: https://tailscale.com/docs/features/access-control/device-management/device-approval

This snippet demonstrates how to use the Tailscale API to programmatically approve or revoke device access. It requires an API key and the device ID. The API allows for setting an 'authorized' flag to true or false.

```shell
curl "https://api.tailscale.com/api/v2/device/11055/authorized" \
-u "tskey-api-xxxxx:" \
--data-binary '{"authorized": true}'

curl "https://api.tailscale.com/api/v2/device/11055/authorized" \
-u "tskey-api-xxxxx:" \
--data-binary '{"authorized": false}'
```

--------------------------------

### List Tailscale DERP Regions and IDs with jq

Source: https://tailscale.com/docs/reference/derp-servers

This command-line snippet utilizes `curl` and `jq` to retrieve the official Tailscale DERP map and then formats the output to list each DERP region's ID and name. This is helpful for identifying the correct RegionIDs to use in your policy file.

```bash
curl --silent https://controlplane.tailscale.com/derpmap/default | jq -r '.Regions[] | "\(.RegionID) \(.RegionName)"'
```

--------------------------------

### Generate Auth Keys

Source: https://tailscale.com/docs/features/oauth-clients

Generate new authentication keys using an OAuth client configured with the `auth_keys` scope. This involves a POST request to the `/api/v2/tailnet/:tailnet/keys` endpoint.

```APIDOC
## POST /api/v2/tailnet/:tailnet/keys

### Description
Generates new authentication keys for a specified tailnet. Requires an OAuth client with the `auth_keys` scope.

### Method
POST

### Endpoint
https://api.tailscale.com/api/v2/tailnet/:tailnet/keys

### Parameters
#### Path Parameters
- **tailnet** (string) - Required - Your Tailscale tailnet identifier.

#### Request Body
- **tags** (array of strings) - Required - A list of tags to assign to the generated auth key. Must be a subset of tags the OAuth client has permission for.
- **expiry** (string) - Optional - The expiration time for the auth key. Format: `YYYY-MM-DDTHH:MM:SSZ`. If omitted, a default expiration (e.g., 90 days) may apply, or it might be a one-off key.

### Request Example
```json
{
  "tags": ["tag:server"],
  "expiry": "2024-12-31T23:59:59Z"
}
```

### Response
#### Success Response (200)
- **key** (string) - The generated authentication key.
- **tailnet** (string) - The tailnet identifier.
- **expires** (string) - The expiration timestamp of the key.
- **tags** (array of strings) - The tags assigned to the key.

#### Response Example
```json
{
  "key": "tskey-auth-example12345abcdef",
  "tailnet": "your-tailnet-id",
  "expires": "2024-12-31T23:59:59Z",
  "tags": ["tag:server"]
}
```
```

--------------------------------

### Connect to Tailscale using Auth Key in GitHub Actions

Source: https://tailscale.com/docs/integrations/github/github-action

This code snippet illustrates how to authenticate with the Tailscale GitHub Action using an auth key. A GitHub repository secret named `TAILSCALE_AUTHKEY` must be created and its value set to your Tailscale auth key. The `authkey` field in the action configuration references this secret.

```yaml
- name: Tailscale
  uses: tailscale/github-action@v4
  with:
    authkey: ${{ secrets.TAILSCALE_AUTHKEY }}

```

--------------------------------

### Share Directories with Tailscale Drive (tailscale drive)

Source: https://tailscale.com/docs/reference/tailscale-cli

The `tailscale drive` command enables sharing directories within your tailnet. Use `share <name> <path>` to create or modify a share, `rename <oldname> <newname>` to change a share's name, `unshare <name>` to remove a share, and `list` to view all active shares.

```bash
tailscale drive share my-files /path/to/files
tailscale drive rename my-files important-files
tailscale drive unshare important-files
tailscale drive list

```

--------------------------------

### Configure IP Forwarding without sysctl.d

Source: https://tailscale.com/docs/how-to/connect-vpc

These commands enable IPv4 and IPv6 forwarding by directly modifying the '/etc/sysctl.conf' file. The 'sysctl -p' command then applies these new settings.

```bash
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p /etc/sysctl.conf
```

--------------------------------

### Reload Tailscale and Caddy Services

Source: https://tailscale.com/docs/solutions/code-on-ipad-vscode-caddy-code-server

These commands reload the `tailscaled` and `caddy` services to apply configuration changes. Reloading ensures that the new certificate permissions and Caddyfile configurations are active.

```bash
sudo systemctl reload tailscaled
sudo systemctl reload caddy
```

--------------------------------

### Ping Another Device with Tailscale CLI

Source: https://tailscale.com/docs/solutions/migrate-legacy-vpn-tailscale

This command verifies connectivity between two devices in your Tailscale network. It requires the device name or IP address of the target device. The command returns a 'pong' message indicating successful communication and latency.

```bash
tailscale ping <other-device-name-or-ip>
```

--------------------------------

### Advertise Subnet Routes with Tailscale CLI

Source: https://tailscale.com/docs/features/site-to-site

Configures a Tailscale client to advertise specific subnet routes. This command is run on each subnet router to enable connectivity to the specified CIDR ranges. The `--snat-subnet-routes=false` flag is specific to Linux environments.

```bash
tailscale up --advertise-routes=192.0.2.0/24 --snat-subnet-routes=false --accept-routes
```

```bash
tailscale up --advertise-routes=172.16.100.0/24 --snat-subnet-routes=false --accept-routes
```

--------------------------------

### Enable Auto-Updates via CLI

Source: https://tailscale.com/docs/features/client/update?tab=linux

This command enables automatic updates for the Tailscale client on a device. It's a simple CLI command applicable across various platforms.

```bash
tailscale set --auto-update
```

--------------------------------

### Define Tailscale Groups and Access Grants

Source: https://tailscale.com/docs/solutions/migrate-legacy-vpn-tailscale

This snippet defines user groups and the access rules (grants) that specify which groups can access which resources (devices tagged with specific tags). It demonstrates how to set up role-based access control in Tailscale.

```json
{
  "groups": {
    "group:engineering": ["alice@example.com", "frank@example.com"],
    "group:finance": ["bob@example.com", "dana@example.com"],
    "group:legal": ["carl@example.com"]
  },

  "grants": [
    {
      "src": ["autogroup:member"],
      "dst": ["autogroup:self"],
      "ip":  ["*"]
    },
    {
      "src": ["group:engineering"],
      "dst": ["tag:engineering"],
      "ip":  ["*"]
    },
    {
      "src": ["group:finance"],
      "dst": ["tag:finance"],
      "ip":  ["*"]
    },
    {
      "src": ["group:legal"],
      "dst": ["tag:legal"],
      "ip":  ["*"]
    },
    {
      "src": ["autogroup:member"],
      "dst": ["tag:internal"],
      "ip":  ["*"]
    }
  ],

  "tagOwners": {
    "tag:engineering": ["autogroup:admin"],
    "tag:finance": ["autogroup:admin"],
    "tag:legal": ["autogroup:admin"],
    "tag:internal": ["autogroup:admin"]
  }
}
```

--------------------------------

### Configure Tag Ownership for Auth Keys

Source: https://tailscale.com/docs/features/oauth-clients

This JSON snippet shows how to configure tag owners for Tailscale auth keys. It allows assigning multiple tags to a tag owner, which can then be used to create auth keys with specific tags.

```json
{
  "tagOwners": {
    "tag:terraform-tag-owner": ["<your-email-address>"],
    "tag:server": ["tag:terraform-tag-owner"],
    "tag:database": ["tag:terraform-tag-owner"],
  },
}

```

--------------------------------

### Suggest Tailscale Exit Node

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Provides a recommendation for an exit node based on network conditions or proximity. This helps in selecting an optimal exit node.

```bash
tailscale exit-node suggest
```

--------------------------------

### Configure Access Rules in Tailnet Policy File

Source: https://tailscale.com/docs/how-to/set-up-servers

This JSON snippet shows how to configure access rules in a Tailscale tailnet policy file. It defines network access grants, allowing specific sources (e.g., 'group:sre') to reach tagged destinations ('tag:server') across all IPs. It also includes rules for Tailscale SSH, permitting SSH connections from specified sources to tagged resources for particular users.

```json
{
  "grants": [
    {
      "src": ["group:sre"],
      "dst": ["tag:server"],
      "ip": ["*"]
    }
  ],
  "ssh": [
    {
      "action": "accept",
      "src": ["group:sre"],
      "dst": ["tag:server"],
      "users": ["ubuntu", "root"]
    }
  ]
}

```

--------------------------------

### Configure Webhook Endpoints (Aperture)

Source: https://tailscale.com/docs/features/aperture/configuration

Defines webhook endpoints that Aperture calls when specific conditions are met. Each hook requires a URL and can optionally include an API key for authentication and a timeout duration. The timeout accepts Go duration strings.

```json
{
  "hooks": {
    "oso": {
      "url": "https://api.osohq.com/api/agents/v1/model-request",
      "apikey": "YOUR_OSO_API_KEY",
      "timeout": "10s"
    },
    "my-webhook": {
      "url": "https://example.com/webhook",
      "apikey": "YOUR_API_KEY"
    }
  }
}
```

--------------------------------

### ACL to Grant Conversion: Multiple Ports on Single Tag

Source: https://tailscale.com/docs/reference/migrate-acls-grants

Illustrates how to convert an ACL with multiple port specifications for a single destination tag into a grant. Each port is listed individually within the 'ip' array.

```json
{
  "acls": [
    {
      "action": "accept",
      "src": ["group:eng"],
      "dst": ["tag:web-server:80", "tag:web-server:22"]
    }
  ]
}

```

```json
{
  "grants": [
    {
      "src": ["group:eng"],
      "dst": ["tag:web-server"],
      "ip": ["80", "22"]
    }
  ]
}

```

--------------------------------

### Terraform Configuration for Service IP Ranges

Source: https://tailscale.com/docs/reference/best-practices/app-connectors

This Terraform configuration demonstrates how to use the HTTP data provider to fetch IP address lists from Okta, GitHub, and AWS. It decodes JSON responses and consolidates IP ranges for preconfiguring routes.

```hcl
data "http" "okta_ip_range_json" {
  url = "https://s3.amazonaws.com/okta-ip-ranges/ip_ranges.json"
}

locals {
  okta_ip_range_data = jsondecode(data.http.okta_ip_range_json.response_body)
  okta_cell_ranges   = [for key in keys(local.okta_ip_range_data) : local.okta_ip_range_data["${key}"].ip_ranges if key == "us_cell_1"]
  okta_ip_ranges     = sort(distinct(flatten(local.okta_cell_ranges)))
}

data "http", "github_meta_json" {
  url = "https://api.github.com/meta"
}

locals {
  github_meta = jsondecode(data.http.github_meta_json.response_body)
  github_ips  = concat(local.github_meta.hooks, local.github_meta.web, local.github_meta.api, local.github_meta.git, local.github_meta.github_enterprise_importer, local.github.meta.packages, local.github_meta.pages, local.github_meta.importer, local.github_meta.actions, local.github_meta.dependabot)
  github_domains = concat(local.github_meta.domains.website, local.github_meta.domains.codespaces, local.github_meta.domains.copilot, local.github_meta.domains.packages, local.github_meta.domains.actions)
}

data "http", "aws_ip_ranges_json" {
  url = "https://ip-ranges.amazonaws.com/ip-ranges.json"
}

locals {
  aws_ip_range_data = jsondecode(data.http.aws_ip_ranges_json.response_body)
  aws_ip_ranges     = sort(distinct(concat([for prefix in local.aws_ip_range_data.prefixes : prefix.ip_prefix], [for prefix in local.aws_ip_range_data.ipv6_prefixes : prefix.ipv6_prefix])))
}

locals {
  all_ip_ranges = conact(local.okta_ip_ranges, local.github_ips, local.aws_ip_ranges)
}

```

--------------------------------

### Golink Policy Configuration for Admin Access

Source: https://tailscale.com/docs/features/access-control/grants/grants-app-capabilities

Configures Golink application capability grants, enabling admin privileges for specific users or devices. The 'admin' parameter set to 'true' grants elevated access to the Golink service.

```json
{
  "grants": [
    {
      "src": ["group:managers"],
      "dst": ["tag:golink-server"],
      "app": {
        "tailscale.com/cap/golink": [{"admin": true}]
      }
    }
  ]

}
```

--------------------------------

### Expose Nginx with Tailscale Ingress

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/multi-cluster-ingress

Applies an `Ingress` resource to expose the Nginx service using Tailscale. It configures DNS name, TLS settings using Let's Encrypt staging, and directs traffic to the Nginx service via the 'ingress-proxies' `ProxyGroup`.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx
  annotations:
    tailscale.com/proxy-group: ingress-proxies
    tailscale.com/tags: "tag:internal-apps"
spec:
  tls:
  - hosts:
    - nginx
  rules:
  - http:
      paths:
      - backend:
          service:
            name: nginx
            port:
              number: 80
        pathType: Prefix
        path: /
  ingressClassName: tailscale

```

--------------------------------

### Configure OpenRouter as a Multi-Provider Aggregator

Source: https://tailscale.com/docs/features/aperture/configuration

This configuration sets up OpenRouter as a provider, acting as an aggregator for multiple LLM services. It requires the base URL and an API key. The `models` array lists the specific models available through OpenRouter that Aperture can access.

```json
{
  "providers": {
    "openrouter": {
      "baseurl": "https://openrouter.ai/api/",
      "apikey": "YOUR_OPENROUTER_KEY",
      "models": [
        "qwen/qwen3-235b-a22b-2507",
        "google/gemini-2.5-pro-preview",
        "x-ai/grok-code-fast-1"
      ]
    }
  }
}
```

--------------------------------

### Set Mullvad Exit Node via Tailscale CLI

Source: https://tailscale.com/docs/features/exit-nodes/mullvad-exit-nodes?tab=linux

This command allows you to configure a device to use a Mullvad exit node. You can specify the exit node by its name (if MagicDNS is enabled) or its IP address using the `--exit-node=` flag. This is essential for routing traffic through Mullvad VPN servers.

```bash
sudo tailscale set --exit-node=<exit-node-name-or-ip>
```

--------------------------------

### Manage Tailscale Funnel Service

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=windows

Serves content and local servers from your Tailscale node to the internet. Use the `serve` command to limit access to your tailnet. Subcommands include 'status' and 'reset'.

```bash
tailscale funnel <target>
```

```bash
tailscale funnel <subcommand> [flags] <args>
```

```bash
tailscale funnel status
```

```bash
tailscale funnel reset
```

--------------------------------

### Deploy Nginx with Userspace Tailscale Sidecar

Source: https://tailscale.com/docs/kubernetes

Deploys an Nginx pod with a Tailscale sidecar running in userspace mode. This reduces the required permissions for Tailscale but necessitates using a SOCKS5 or HTTP proxy for outbound connectivity to the tailnet.

```bash
make userspace-sidecar | kubectl apply -f-
# If not using an auth key, authenticate by grabbing the Login URL here:
kubectl logs nginx ts-sidecar
```

--------------------------------

### Tailscale Licenses Information

Source: https://tailscale.com/docs/reference/tailscale-cli

Retrieve information about the open source licenses used by Tailscale.

```APIDOC
## GET /websites/tailscale/licenses

### Description
Get open source license information for Tailscale.

### Method
GET

### Endpoint
/websites/tailscale/licenses

### Parameters
None

### Request Example
```json
{
  "request": "GET /websites/tailscale/licenses"
}
```

### Response
#### Success Response (200)
- **licenses** (string) - A string containing the open source license information.

#### Response Example
```json
{
  "licenses": "This Tailscale installation includes software licensed under the following open source licenses..."
}
```
```

--------------------------------

### Connect Runner to Tailscale Network

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This step utilizes the 'tailscale/github-action@v4' action to connect the GitHub Actions runner to a Tailscale network (tailnet). It authenticates using OAuth client ID and secret from repository secrets, assigns the ephemeral node the tag 'tag:ci', and uses the latest Tailscale version.

```yaml
- name: Connect to Tailscale
  uses: tailscale/github-action@v4
  with:
    oauth-client-id: ${{ secrets.TS_OAUTH_CLIENT_ID }}
    oauth-secret: ${{ secrets.TS_OAUTH_SECRET }}
    tags: tag:ci
    version: latest
```

--------------------------------

### Define Application Layer Capabilities in Tailscale

Source: https://tailscale.com/docs/reference/syntax/grants

This snippet demonstrates how to define application layer capabilities for Tailscale. It uses a JSON object where keys are capability strings (e.g., 'domainName/capabilityName') and values are arrays of parameter objects. The parameters are opaque JSON and are validated by the client application.

```json
"app": {
  "<domainName>/<capabilityName>": [
    {
      "<parameterName>": "<parameterValue>",
      "// Additional parameters as defined by the application": ""
    }
  ]
}

```

```json
"app": {
  "tailscale.com/cap/tailsql": [
    {
      "dataSrc": ["*"]
    }
  ]
}

```

```json
"app": {
  "tailscale.com/cap/golink": [
    {
      "admin": true
    }
  ]
}

```

```json
"app": {
  "tailscale.com/cap/kubernetes": [
    {
      "impersonate": {
        "groups": ["system:masters"]
      }
    }
  ]
}

```

--------------------------------

### Retrieve Files from Tailscale Target Directory

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=linux

Retrieves files from the Tailscale file inbox on a target host. Supports conflict resolution, looping, and verbose output.

```bash
tailscale file get <target-directory> --conflict=<behavior> --loop --verbose --wait
```

--------------------------------

### Define Tailscale Tag and Service in Admin Console

Source: https://tailscale.com/docs/features/tsnet/how-to/register-service

This section outlines the steps to create a Tailscale tag and define a service within the Tailscale admin console. It specifies the tag name, owner, service name, and ports required for the configuration.

```text
tsnet-demo-host
autogroup:member
tsnd-demo
443
svc:tsnet-demo
tag:tsnet-demo-host
svc:tsnet-demo
```

--------------------------------

### TailSQL Policy Configuration

Source: https://tailscale.com/docs/features/access-control/grants/grants-app-capabilities

Defines TailSQL application capability grants, specifying allowed data sources for querying. It uses 'src' for allowed data sources like 'main' or 'self', controlling access to tailnet configuration and state.

```json
{
  "grants": [
    {
      "src": ["group:eng"],
      "dst": ["tag:tailsql"],
      "app": {
        "tailscale.com/cap/tailsql": [
          {"src": ["main", "self"]}
        ]
      }
    }
  ]

}
```

--------------------------------

### LocalClient Usage for HTTP Server Identity

Source: https://tailscale.com/docs/reference/tsnet-server-api

Demonstrates how to obtain a LocalClient instance and use it within an HTTP server to identify connecting users based on their IP address and Tailscale identity.

```APIDOC
## `Server.LocalClient`

### Description

The `LocalClient` type in `tsnet` allows programmatic configuration changes and identity lookups, mirroring the functionality of the `tailscale` command-line tool. This example shows how to use `LocalClient` within an HTTP server to get user identity information for incoming requests.

### Method

Implicitly called via `Server.LocalClient()`

### Endpoint

N/A (Local client interaction)

### Parameters

#### Path Parameters

None

#### Query Parameters

None

#### Request Body

None

### Request Example

```go
s := new(tsnet.Server)
s.Hostname = "aran"
defer s.Close()

ln, err := s.Listen("tcp", ":80")
if err != nil {
    log.Fatal(err)
}
defer ln.Close()

lc, err := s.LocalClient()
if err != nil {
    log.Fatal(err)
}

log.Fatal(http.Serve(ln, http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
    who, err := lc.WhoIs(r.Context(), r.RemoteAddr)
    if err != nil {
        http.Error(w, err.Error(), 500)
        return
    }
    fmt.Fprintf(w, "<html><body><h1>Hello, world!</h1>\n")
    fmt.Fprintf(w, "<p>You are <b>%s</b> from <b>%s</b> (%s)</p>",
        html.EscapeString(who.UserProfile.LoginName),
        html.EscapeString(firstLabel(who.Node.ComputedName)),
        r.RemoteAddr)
})))
```

### Response

#### Success Response (200)

- **who** (`apitype.WhoIsResponse`) - Contains identity information about the connecting client, including `UserProfile` and `Node` details.

#### Response Example

```json
{
  "who": {
    "node": {
      "id": "1234567890abcdef",
      "addresses": [
        "fd7a:42:c3:0:1000:a7ad:708c:9123",
        "100.101.102.103"
      ],
      "endpoints": [
        "1.2.3.4:56789"
      ],
      "machineName": "my-tailscale-machine",
      "name": "my-tailscale-machine.tailnet.example.com",
      "user": "user@example.com",
      "certificateFingerprint": "sha256:abc...",
      "tags": [
        "tag:server"
      ],
      "active": true,
      "lastSeen": "2023-10-27T10:00:00Z",
      "routes": [],
      "advertisedRoutes": [],
      "controlled": false,
      "keyExpiration": "2023-11-26T10:00:00Z",
      "hostName": "my-tailscale-machine",
      "os": "linux",
      "created": "2023-01-01T00:00:00Z",
      "groupByTags": [],
      "computedName": "my-tailscale-machine",
      "userProfile": {
        "id": "user-id-123",
        "loginName": "user@example.com",
        "displayName": "User Name",
        "photoURL": "https://example.com/photo.jpg"
      }
    },
    "authenticated": true,
    "error": ""
  }
}
```

### Error Handling

- **500 Internal Server Error**: Returned if there is an error retrieving identity information using `lc.WhoIs()`.
```

--------------------------------

### Configure Federated Identities with Tailscale API

Source: https://tailscale.com/docs/features/workload-identity-federation

Shows how to configure federated identities by making a POST request to the Tailscale API endpoint `https://api.tailscale.com/api/v2/tailnet/-/keys`. The request body includes details like key type, description, scopes, tags, issuer, subject, and custom claim rules.

```cURL
curl -X POST https://api.tailscale.com/api/v2/tailnet/-/keys \
  -H "Content-Type: application/json" \
  -d   '{ \
  "keyType": "federated", \
  "description": "Example federated identity", \
  "scopes": [ \
    "auth_keys", \
    "devices:core" \
  ], \
  "tags": [ \
    "tag:test" \
  ], \
  "issuer": "https://example.com", \
  "subject": "example-sub-*", \
  "customClaimRules": { \
    "repo_name": "example-repo-name", \
  }'

```

--------------------------------

### Monitor Application Access with Tailscale Policy

Source: https://tailscale.com/docs/reference/examples/grants

Enables monitoring server access to specific application ports on services across the tailnet. This approach balances observability needs with security by allowing monitoring servers to access only necessary ports without granting full tailnet access. It requires defining groups, grants, and tag owners in the Tailscale policy file.

```json
{
  "groups": {
    "group:devops": ["carl@example.com"]
  },
  "grants": [
    {
      "src": ["tag:monitoring"],
      "dst": ["tag:logging"],
      "ip": ["80", "443", "9100"]
    },
    {
      "src": ["group:devops"],
      "dst": ["tag:monitoring", "tag:logging"],
      "ip": ["*"]
    }
  ],
  "tagOwners": {
    "tag:monitoring": ["group:devops"],
    "tag:logging": ["group:devops"]
  }
}
```

--------------------------------

### Register New Nodes using Workload Identity

Source: https://tailscale.com/docs/features/workload-identity-federation

Register new nodes to your Tailnet using `tailscale up` with workload identity federation, providing a client ID and an OIDC token.

```APIDOC
## Register New Nodes using Workload Identity

### Description
Registers a new node to your Tailscale network using workload identity federation. Requires Tailscale v1.90.1 or later.

### Method
CLI Command

### Endpoint
N/A (CLI Command)

### Parameters
#### CLI Flags
- **--client-id** (string) - Required - The Client ID used to generate auth keys with workload identity federation. Can include URL parameters like `?ephemeral=false&preauthorized=true`.
  - `ephemeral` (boolean) - Optional - Register as an ephemeral node (defaults to `true`).
  - `preauthorized` (boolean) - Optional - Skip manual device approval (defaults to `false`).
- **--id-token** (string) - Required - The ID token from the identity provider to exchange with the control server for workload federation. This is the signed OIDC JWT.
- **--advertise-tags** (string) - Required - Tags to advertise for the node, must match tags configured in federated identity.

### Request Example
```bash
tailscale up --client-id=${CLIENT_ID} --id-token=${IDENTITY_TOKEN} --advertise-tags=tag:ci
```

### Request Example with Optional Parameters
```bash
tailscale up --client-id='${CLIENT_ID}?ephemeral=false&preauthorized=true' --id-token=${IDENTITY_TOKEN} --advertise-tags=tag:ci
```

### Response
#### Success Response
Node is registered to the Tailnet.

#### Error Response
Errors will be reported by the `tailscale up` command. Specific error details for token exchange can be found in the admin console.
```

--------------------------------

### Create IP Set Excluding Another IP Set

Source: https://tailscale.com/docs/features/tailnet-policy-file/ip-sets

Shows how to define an IP set that excludes all targets present in another defined IP set. This is useful for creating broader access rules that avoid specific groups.

```json
"ipsets": {
  "ipset:dev": ["host:sql-server-1"],
  "ipset:prod": [
    "add 192.0.2.0/24",
    "add 198.51.100.0/24",
    "remove ipset:dev",
  ]
}
```

--------------------------------

### Default Aperture Configuration (JSON)

Source: https://tailscale.com/docs/features/aperture/configuration

This JSON configuration defines the default settings for Aperture, including temporary grants for user access and model permissions, definitions for OpenAI and Anthropic providers, and a hook configuration for Oso. It outlines how users are granted access and how LLM providers are set up.

```json
{
    "temp_grants": [
        {
            "src": [
                "example-user@example.com",
                "*"
            ],
            "grants": [
                {"role": "admin"}
            ]
        },
        {
            "src": ["*"],
            "grants": [
                {"role": "user"}
            ]
        },
        {
            "src": ["*"],
            "grants": [
                {
                    "providers": [
                         {"provider": "*", "model": "*"}
                    ]
                }
            ]
        },
        {
            "src": [
            ],
            "grants": [
                {
                    "hook": {
                        "match": {
                            "providers": ["*"],
                            "models":    ["*"],
                            "events":    ["tool_call_entire_request"]
                        },
                        "hook":   "oso",
                        "fields": ["user_message", "tools", "request_body", "response_body"]
                    }
                }
            ]
        }
    ],
    "providers": {
        "openai": {
            "baseurl": "https://api.openai.com",
            "name": "OpenAI",
            "apikey": "YOUR_OPENAI_API_KEY",
            "models": [
                "gpt-5",
                "gpt-5-mini",
                "gpt-5-nano",
                "gpt-4.1",
                "gpt-4.1-nano",
                "gpt-5.1-codex",
                "gpt-5.1-codex-max"
            ],
            "compatibility": {
                "openai_chat": true,
                "openai_responses": true,
                "anthropic_messages": false
            }
        },
        "anthropic": {
            "baseurl": "https://api.anthropic.com",
            "name": "Anthropic",
            "apikey": "YOUR_ANTHROPIC_API_KEY",
            "models": [
                "claude-sonnet-4-5",
                "claude-sonnet-4-5-20250929",
                "claude-haiku-4-5",
                "claude-haiku-4-5-20251001",
                "claude-opus-4-5",
                "claude-opus-4-5-20251101"
            ],
            "compatibility": {
                "openai_chat": false,
                "openai_responses": false,
                "anthropic_messages": true
            }
        }
    },
    "hooks": {
        "oso": {
            "url":    "https://api.osohq.com/api/agents/v1/model-request",
            "apikey": "YOUR_OSO_API_KEY"
        }
    }
}
```

--------------------------------

### Access Minecraft Server Console via Tmux

Source: https://tailscale.com/docs/solutions/set-up-minecraft

This command allows you to attach to the running Minecraft server's console session managed by tmux. This is useful for interacting with the server directly, issuing commands, or monitoring its status. Remember to detach using Ctrl-B then 'd'.

```bash
sudo -s -u minecraft
tmux attach
```

--------------------------------

### Expose Kubernetes Ingress to Tailnet

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Configure a Kubernetes Ingress resource to expose a service to your tailnet. This requires setting the `ingressClassName` to `tailscale` and specifying the desired host name in `tls.hosts`. The backend service defaults to HTTP.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx
spec:
  defaultBackend:
    service:
      name: nginx
      port:
        number: 80
  ingressClassName: tailscale
  tls:
    - hosts:
        - nginx

```

--------------------------------

### Build Extra-Small Tailscale Binary (Shell)

Source: https://tailscale.com/docs/how-to/set-up-small-tailscale

Uses a build script to create an 'extra-small' Tailscale binary. This flag omits debug information and less frequently used features to reduce binary size, suitable for resource-constrained environments.

```bash
build_dist.sh --extra-small
```

--------------------------------

### Configure Default Firewall Rules with ufw

Source: https://tailscale.com/docs/how-to/secure-ubuntu-server-with-ufw

Sets default policies for incoming and outgoing traffic using ufw. Denies all incoming traffic by default and allows all outgoing traffic by default. This is a foundational step for network security.

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

--------------------------------

### Ping Device for Connectivity Check

Source: https://tailscale.com/docs/how-to/connect-to-devices

Provides a command to test network reachability to a specific device within your Tailscale tailnet. This is a fundamental troubleshooting step to verify that Tailscale is correctly routing traffic between devices.

```bash
tailscale ping <device-name-or-ip>
```

--------------------------------

### Connect to PostgreSQL via MagicDNS Name

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cloud-services

This command demonstrates connecting to a PostgreSQL database instance from a tailnet client using the MagicDNS name obtained from the Tailscale Kubernetes Operator. It assumes the database is running on the exposed service.

```bash
psql -h ${rds_magic_dns_name} -U postgres

```

--------------------------------

### devices:core:read Scope

Source: https://tailscale.com/docs/reference/trust-credentials

Grants access to read device information within the tailnet.

```APIDOC
## devices:core:read Scope

### Description
The credential has access to read devices in the tailnet.

### Allowed Endpoints
* `GET /api/v2/tailnet/:tailnet/devices`
* `GET /api/v2/device/:deviceID`
```

--------------------------------

### Deploy to Kubernetes with Tailscale

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This snippet illustrates deploying applications to Kubernetes using `kubectl` commands through Tailscale. It configures the Kubernetes API server endpoint to use a private tailnet address and applies Kubernetes manifests. The Kubernetes API server does not require a public endpoint, as the connection is secured via the tailnet with audit logging.

```yaml
- name: Deploy to Kubernetes
  run: |
    kubectl config set-cluster production --server=https://k8s-api.tail-scale.ts.net:6443
    kubectl apply -f ./k8s/production/
    kubectl rollout status deployment/my-app -n production

```

--------------------------------

### Uninstall Tailscale on Windows

Source: https://tailscale.com/docs/features/client/uninstall

This snippet shows how to uninstall Tailscale on Windows using the Control Panel. It also lists the default file paths for Tailscale's local data, which can be manually removed for a complete reset. Removing these files ensures that no local state or configuration is retained.

```powershell
Get-AppxPackage *tailscale* | Remove-AppxPackage
# Or via Control Panel: Settings > Apps > Tailscale > Uninstall
```

```powershell
# Paths to remove for a complete reset:
Remove-Item -Recurse -Force "C:\ProgramData\Tailscale"
Remove-Item -Recurse -Force "C:\Users\$env:USERNAME\AppData\Local\Tailscale"
Remove-Item -Recurse -Force "C:\Windows\System32\config\systemprofile\AppData\Local\Tailscale"
```

--------------------------------

### Create Kubernetes ClusterRoleBinding for Tailnet User

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/api-server-proxy

This command creates a Kubernetes ClusterRoleBinding named 'alice-view'. It binds the Kubernetes user 'alice@tailscale.com' to the 'view' ClusterRole, granting read-only access to Kubernetes resources for the specified Tailscale user.

```bash
kubectl create clusterrolebinding alice-view --user="alice@tailscale.com"  --clusterrole=view

```

--------------------------------

### Specify Device Serial Number (iOS/tvOS)

Source: https://tailscale.com/docs/features/tailscale-system-policies

Enables reporting of the device serial number to the Tailscale coordination server for posture checking on iOS and tvOS. This requires an MDM solution to provide the serial number via the `DeviceSerialNumber` policy, as these platforms restrict direct access to this information.

```text
a String containing the device serial number
```

--------------------------------

### Revoke Compromised Tailscale Signing Node Keys

Source: https://tailscale.com/docs/features/tailnet-lock?tab=tailscale+admin+console

Initiates the process to revoke compromised signing node keys. This is a multi-step process requiring co-signing. The initial command identifies keys to revoke, and subsequent `--cosign` commands are used for co-signing until a `--finish` command is executed.

```bash
tailscale lock revoke-keys tlpub:compromised-key1 tlpub:compromised-key2
```

```bash
tailscale lock revoke-keys --cosign <hex-data>
```

```bash
tailscale lock revoke-keys --finish <hex-data>
```

--------------------------------

### Copy Files to a Tailscale Host

Source: https://tailscale.com/docs/reference/tailscale-cli?tab=fish

Copies specified files to a target host within your tailnet using Tailscale's file transfer capabilities. Supports standard input and alternate filenames.

```bash
tailscale file cp <files...> <target>
```

```bash
tailscale file cp --name=<name> <files...> <target>
```

--------------------------------

### Test Tailscale Connectivity in GitHub Actions

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This step verifies the GitHub Actions runner's connection to the Tailscale network. It runs 'tailscale status' to check the connection status and 'tailscale ip -4' to display the assigned IPv4 address from the Tailscale CGNAT range, confirming successful integration with the tailnet.

```yaml
- name: Test connectivity
  run: |
    # Test that we can reach the Tailscale network
    tailscale status

    # Show our IP address
    tailscale ip -4
```

--------------------------------

### Account Settings API

Source: https://tailscale.com/docs/reference/trust-credentials

Endpoints for managing tailnet contacts and resending verification emails. Requires 'account_settings:read' or 'account_settings' credentials.

```APIDOC
## Account Settings API

### Description
Manage tailnet contacts and resend verification emails.

### Endpoints

#### GET /api/v2/tailnet/:tailnet/contacts

##### Description
Retrieves a list of tailnet contacts for a given tailnet.

##### Method
GET

##### Endpoint
/api/v2/tailnet/:tailnet/contacts

##### Parameters
- **tailnet** (string) - Required - The name of the tailnet.

#### PATCH /api/v2/tailnet/:tailnet/contacts/:contactType

##### Description
Modifies tailnet contacts of a specific type.

##### Method
PATCH

##### Endpoint
/api/v2/tailnet/:tailnet/contacts/:contactType

##### Parameters
- **tailnet** (string) - Required - The name of the tailnet.
- **contactType** (string) - Required - The type of contact to modify (e.g., 'email').

##### Request Body
- **value** (string) - Required - The new value for the contact.

#### POST /api/v2/tailnet/:tailnet/contacts/:contactType/resend-verification-email

##### Description
Resends the verification email for a specific contact type.

##### Method
POST

##### Endpoint
/api/v2/tailnet/:tailnet/contacts/:contactType/resend-verification-email

##### Parameters
- **tailnet** (string) - Required - The name of the tailnet.
- **contactType** (string) - Required - The type of contact for which to resend the verification email.

### Response Examples
(Specific response examples depend on the exact endpoint and method used.)
```

--------------------------------

### Manage Kubernetes Operator Access with Privileges (JSON)

Source: https://tailscale.com/docs/reference/examples/grants

This configuration manages access to the Kubernetes Operator with different privilege levels using Tailscale's capabilities. It grants administrative privileges to the production team and read-only access to other users. Requires tagging the Kubernetes Operator device and configuring impersonated groups in Kubernetes.

```json
{
  "grants": [
    {
      "src": [
        "group:prod"
      ],
      "dst": [
        "tag:k8s-operator"
      ],
      "app": {
        "tailscale.com/cap/kubernetes": [
          {
            "impersonate": {
              "groups": [
                "system:masters"
              ]
            }
          }
        ]
      }
    },
    {
      "src": [
        "group:k8s-readers"
      ],
      "dst": [
        "tag:k8s-operator"
      ],
      "app": {
        "tailscale.com/cap/kubernetes": [
          {
            "impersonate": {
              "groups": [
                "tailnet-readers"
              ]
            }
          }
        ]
      }
    }
  ]
}
```

--------------------------------

### View Operator Logs

Source: https://tailscale.com/docs/reference/troubleshooting/kubernetes-operator

This command retrieves the logs from the operator's deployment in the 'tailscale' namespace. It is essential for understanding the operator's behavior and diagnosing any operational problems.

```bash
kubectl logs deployment/operator --namespace tailscale

```

--------------------------------

### all Scope

Source: https://tailscale.com/docs/reference/trust-credentials

Grants complete access to the tailnet, including future endpoints. Allows listing all access tokens.

```APIDOC
## all Scope

### Description
The credential has complete access to the tailnet. This scope is not restricted to only access of APIs that existed at the time the credential was initially authorized—the `all` scope also grants access to new APIs created in the future. The `all` and `all:read` scopes are the only scopes which can get a list of all access tokens which exist in the tailnet.

### Allowed Endpoints
* All endpoints, even endpoints which did not exist when the credential was initially authorized.
* `GET, DELETE /api/v2/tailnet/:tailnet/keys/:keyID` (for any key, not just itself)
```

--------------------------------

### policy_file Scope

Source: https://tailscale.com/docs/reference/trust-credentials

Grants access to read, validate, and modify the tailnet policy file. Requires `devices:posture_attributes` and `devices:core:read`.

```APIDOC
## policy_file Scope

### Description
The credential has access to read, validate, and modify the tailnet policy file. `devices:posture_attributes` and `devices:core:read` are required when using this scope.

### Allowed Endpoints
* Endpoints from `policy_file:read`
* `POST /api/v2/tailnet/:tailnet/acl`
```

--------------------------------

### Configure tsnet Server to Advertise Tags

Source: https://tailscale.com/docs/reference/tsnet-server-api

This snippet demonstrates how to configure the tsnet Server to advertise specific tags from the tailnet's ACL policy. These tags will be applied to the node. The tags are provided as a comma-separated string via a command-line flag.

```go
tsAdvertiseTags := flag.String("ts-advertise-tags", "", "Comma-separated list of tags to advertise")

flag.Parse()

srv := new(tsnet.Server)
srv.AdvertiseTags = strings.Split(*tsAdvertiseTags, ",")

```

--------------------------------

### Configure OAuth Client ID and Secret in YAML

Source: https://tailscale.com/docs/features/kubernetes-operator

This snippet demonstrates how to correctly format OAuth client ID and client secret values within a YAML manifest. Quoting these values is crucial to prevent potential misinterpretations by the YAML parser, especially for sensitive credentials.

```yaml
client_id: "k123456CNTRL"
client_secret: "tskey-client-k123456CNTRL-abcdef"
```

--------------------------------

### Test Aperture Configuration with cURL (Anthropic API)

Source: https://tailscale.com/docs/features/aperture

Provides a cURL command to test the connection and routing to Aperture for the Anthropic API format. This command sends a request to the /v1/messages endpoint, simulating a client interaction.

```bash
curl -s http://ai/v1/messages \
  -H "Content-Type: application/json" \
  -d '{
    "model": "claude-haiku-4-5-20251001",
    "max_tokens": 25,
    "messages": [{"role": "user", "content": "respond with: hello"}]
  }'
```

--------------------------------

### Monitor Peer Relay Traffic (Tailscale CLI)

Source: https://tailscale.com/docs/features/peer-relay

Filters the output of the `tailscale status` command to identify and monitor devices that are actively using the peer relay functionality. This helps verify the peer relay configuration is working.

```bash
tailscale status | grep peer-relay
```

--------------------------------

### Export Environment Variables from .env File

Source: https://tailscale.com/docs/solutions/connect-github-CICD-workflows-to-private-infrastructure-without-public-exposure

This command exports environment variables defined in a `.env` file. It uses `cat` to read the file and `xargs` to pass the content as arguments to `export`, making these variables available in the current shell session. This is commonly used for managing local development configurations.

```bash
export $(cat .env | xargs)
```

--------------------------------

### Apply Connector Resource - Kubectl Command

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/app-connector

Applies a Kubernetes resource definition from a YAML file using `kubectl`. This command is used to deploy or update resources in a Kubernetes cluster.

```bash
kubectl apply -f connector.yaml

```

--------------------------------

### Verify API Access Token Generation with Curl

Source: https://tailscale.com/docs/features/oauth-clients

This curl command verifies your ability to generate API access tokens by making a request to the Tailscale OAuth token endpoint. It requires the OAUTH_CLIENT_ID and OAUTH_CLIENT_SECRET environment variables to be set.

```bash
curl -d "client_id=${OAUTH_CLIENT_ID}" -d "client_secret=${OAUTH_CLIENT_SECRET}" \
     "https://api.tailscale.com/api/v2/oauth/token"

```

--------------------------------

### Configure Docker Container Auto-updates with Tailscale

Source: https://tailscale.com/docs/features/client/update?tab=ios

This snippet demonstrates how to configure Tailscale within a Docker container to automatically update. It highlights the use of the 'stable' tag and the 'tailscale set --auto-update' command, along with important considerations regarding persistence and versioning.

```bash
docker run -d --name tailscale tailscale/tailscale:stable
# To enable auto-updates inside the container (requires re-issuing on restart):
tailscale set --auto-update
```

--------------------------------

### Tailscale Funnel Command Overview

Source: https://tailscale.com/docs/reference/tailscale-cli/funnel

The `tailscale funnel` command enables sharing of local services over the internet. It supports various targets and configurations for exposing services.

```APIDOC
## `tailscale funnel` Command

### Description

The `tailscale funnel` command allows you to share a local service over the internet. It can be used as an alternative to `tailscale serve` for sharing within your tailnet.

### Method

CLI Command

### Endpoint

N/A (CLI Command)

### Parameters

#### Path Parameters

- **`<target>`** (string) - Required - The target to share. This can be a file, directory, text, or a local service address (e.g., port number, partial URL, full URL).

#### Query Parameters

None

#### Request Body

None

### Request Example

```bash
tailscale funnel --https=8443 localhost:3000
```

### Response

#### Success Response (200)

Indicates the funnel service has started successfully. Specific output may vary.

#### Response Example

```
Funnel is serving on https://<your-tailnet-domain>:<port>
```

```

--------------------------------

### Configure Caddy Reverse Proxy

Source: https://tailscale.com/docs/solutions/code-on-ipad-vscode-caddy-code-server

This configuration sets up Caddy to act as a reverse proxy for code-server. It directs traffic for your Tailscale domain to the specified IP address and port where code-server is running.

```caddyfile
machine-name.tailnet-name.ts.net {
  reverse_proxy 100.x.y.z:8080
}
```

--------------------------------

### Expose Kubernetes Ingress to Public Internet with Tailscale Funnel

Source: https://tailscale.com/docs/features/kubernetes-operator/how-to/cluster-ingress

Expose a Kubernetes Ingress resource to the public internet using Tailscale Funnel. This involves adding the `tailscale.com/funnel: "true"` annotation to the Ingress resource.

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: funnel
  annotations:
    tailscale.com/funnel: "true"
spec:
  defaultBackend:
    service:
      name: funnel
      port:
        number: 80
  ingressClassName: tailscale
  tls:
    - hosts:
        - funnel

```