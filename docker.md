### Docker Offload Quickstart and Troubleshooting

Source: https://docs.docker.com/llms

Guides for getting started with Docker Offload and troubleshooting common issues.

```APIDOC
## Docker Offload Quickstart and Troubleshooting

### Description
Offers a quickstart guide to rapidly begin using Docker Offload for faster builds and provides resources for troubleshooting any encountered issues.

### Method
N/A (Documentation Link)

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A

### Further Information
[Docker Offload quickstart](https://docs.docker.com/offload/quickstart/)
[Troubleshoot Docker Offload](https://docs.docker.com/offload/troubleshoot/)
```

--------------------------------

### Set up and Use Docker Compose

Source: https://docs.docker.com/llms

Get started with Docker Compose by following this guide on setting up and using it for your applications. Learn how to define and run multi-container Docker applications.

```YAML
# Example docker-compose.yml for a simple web application
version: '3.8'
services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    volumes:
      - ./html:/usr/share/nginx/html
  app:
    build: .
    ports:
      - "3000:3000"
```

--------------------------------

### Docker Extension Quickstart and Process

Source: https://docs.docker.com/llms

Guides on the overall process of creating Docker extensions, including a quickstart guide and understanding the build and publish workflow.

```APIDOC
## Docker Extension Quickstart and Process

### Description
Offers a quickstart guide for building Docker extensions and explains the comprehensive process involved in creating, building, and publishing extensions.

### Method
N/A (Documentation Link)

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A

### Further Information
[Quickstart](https://docs.docker.com/extensions/extensions-sdk/quickstart/)
[The build and publish process](https://docs.docker.com/extensions/extensions-sdk/process/)
```

--------------------------------

### Get Started with Docker Model Runner (DMR)

Source: https://docs.docker.com/llms

Instructions on how to install, enable, and begin using Docker Model Runner (DMR). This guide covers the initial setup required to manage and execute AI models within the Docker environment.

```bash
docker extensions enable model-runner
docker run -d --name dmr model-runner:latest
```

--------------------------------

### Install Node.js Dependencies and Start Server

Source: https://docs.docker.com/guides/wiremock

Commands to install project dependencies using npm and start the Node.js server. This prepares the application to run and listen for requests.

```console
npm install 
npm run start
```

--------------------------------

### Install RQT and Launch GUI

Source: https://docs.docker.com/guides/ros2/turtlesim-example

Installs the RQT framework and launches the RQT GUI, a powerful tool for visualizing and interacting with ROS 2 systems. This includes installing all RQT plugins.

```bash
sudo apt update
sudo apt install -y 'ros-humble-rqt*'
ros2 run rqt_gui rqt_gui
```

--------------------------------

### Create Dockerfile for Nginx Website

Source: https://docs.docker.com/docker-hub/quickstart

This Dockerfile extends the official Nginx image to serve a simple 'Hello World' HTML page. It's a basic example demonstrating how to customize a base image for a static website. No external dependencies are required beyond Docker itself.

```dockerfile
FROM nginx
RUN echo "<h1>Hello world from Docker!</h1>" > /usr/share/nginx/html/index.html
```

--------------------------------

### Example MCP Client Configuration (JSON)

Source: https://docs.docker.com/ai/mcp-catalog-and-toolkit/get-started

An example JSON configuration for an MCP client, specifying how to connect to the Docker MCP gateway using stdio.

```json
{
  "servers": {
    "MCP_DOCKER": {
      "command": "docker",
      "args": ["mcp", "gateway", "run"],
      "type": "stdio"
    }
  }
}
```

--------------------------------

### Create Project Directory

Source: https://docs.docker.com/compose/gettingstarted

Shell commands to create a new directory for the project and navigate into it. This is the initial setup step for the Docker Compose quickstart.

```bash
mkdir composetest
cd composetest

```

--------------------------------

### Install Frontend Dependencies (Console)

Source: https://docs.docker.com/guides/localstack

These console commands navigate to the frontend directory and install the required dependencies for the frontend application. This is a prerequisite for starting the frontend development server.

```bash
$ cd frontend
$ npm install
```

--------------------------------

### Run Application with Docker Compose

Source: https://docs.docker.com/compose/gettingstarted

Starts all services defined in the `docker-compose.yaml` file. This command builds necessary images, creates networks, and starts containers for each service. It's the primary command for launching a multi-container application.

```console
$ docker compose up
```

--------------------------------

### Example: Full Docker Plugin Upgrade Workflow

Source: https://docs.docker.com/reference/cli/docker/plugin/upgrade

This example demonstrates the complete process of installing, using, disabling, upgrading, and re-enabling a Docker plugin. It covers plugin installation, volume creation using the plugin, disabling the plugin, performing the upgrade, re-enabling the plugin, and verifying the upgrade by listing volumes and using the volume again.

```bash
# Install the plugin
docker plugin install vieux/sshfs DEBUG=1

# Use the plugin to create and use a volume
docker volume create -d vieux/sshfs:next -o sshcmd=root@1.2.3.4:/tmp/shared -o password=XXX sshvolume
docker run -it -v sshvolume:/data alpine sh -c "touch /data/hello"

# Disable the plugin before upgrading
docker plugin disable -f vieux/sshfs:next

# Upgrade the plugin
docker plugin upgrade vieux/sshfs:next vieux/sshfs:next

# Re-enable the plugin
docker plugin enable vieux/sshfs:next

# Verify the upgrade
docker volume ls
docker run -it -v sshvolume:/data alpine sh -c "ls /data"
```

--------------------------------

### Docker Compose Commands for Managing Example Application

Source: https://docs.docker.com/guides/traefik

Provides essential Docker Compose commands for managing the example application, including stopping existing stacks and starting the application with a specific Compose file. These commands are crucial for setting up and tearing down the environment.

```bash
docker compose down
```

```bash
docker compose -f compose-native.yaml up
```

--------------------------------

### Docker Desktop Installer Flags: Basic Installation

Source: https://docs.docker.com/desktop/setup/install/windows-install

Provides examples of common Docker Desktop installer flags for basic installation customization. These flags control aspects like quiet installation, license acceptance, and installation directory.

```console
"Docker Desktop Installer.exe" install --quiet --accept-license --installation-dir="C:\Program Files\Docker\Docker"
```

--------------------------------

### Clone Sample Application and Start LocalStack

Source: https://docs.docker.com/guides/localstack

This snippet shows how to clone a sample todo-list application repository and start LocalStack with a MongoDB database using Docker Compose. It requires Git and Docker to be installed.

```console
$ git clone https://github.com/dockersamples/todo-list-localstack-docker
$ cd todo-list-localstack-docker
$ docker compose -f compose-native.yml up -d
```

--------------------------------

### Simple Docker Frontend Extension Tutorial

Source: https://docs.docker.com/llms

A minimal example demonstrating the structure of a simple frontend Docker extension. This serves as a starting point for creating basic extensions that integrate with Docker Desktop.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Simple Extension</title>
</head>
<body>
  <h1>Hello from Simple Extension!</h1>
  <script src="extension.js"></script>
</body>
</html>
```

```javascript
console.log("Simple extension loaded!");
```

--------------------------------

### Install and Start Dex Server in GitHub Actions

Source: https://docs.docker.com/guides/dex

This snippet demonstrates how to download the Dex binary, make it executable, and start the Dex server within a GitHub Actions workflow. It assumes a `config.yaml` file is present for Dex configuration. The server is run in the background, and a short delay is included to allow it to start.

```yaml
jobs:
  test-oauth:
    runs-on: ubuntu-latest
    steps:
      - name: Install Dex
        run: |
          curl -L https://github.com/dexidp/dex/releases/download/v2.37.0/dex_linux_amd64 -o dex
          chmod +x dex

      - name: Start Dex Server
        run: |
          nohup ./dex serve config.yaml > dex.log 2>&1 &
          sleep 5  # Give Dex time to start
```

--------------------------------

### Create and Mount Block Device Example (Shell)

Source: https://docs.docker.com/engine/storage/volumes

This sequence of shell commands illustrates the process of creating a file, formatting it with an ext4 filesystem, setting it up as a loop device, and then mounting that loop device into a Docker container. This is a step-by-step guide for preparing and using a block device as a container volume.

```shell
$ fallocate -l 1G disk.raw
$ mkfs.ext4 disk.raw
$ losetup -f --show disk.raw
/dev/loop5
```

--------------------------------

### Start Docker Offload using CLI

Source: https://docs.docker.com/offload/quickstart

Initiates the Docker Offload service from the command line. This command connects your local Docker Desktop to a cloud environment for building and running containers. It may prompt for organization selection if you belong to multiple subscribed organizations.

```bash
docker offload start
```

--------------------------------

### Starting the Dockerized Application Stack

Source: https://docs.docker.com/guides/localstack

This command initiates the Docker Compose setup defined in the `compose.yml` file. It builds the images if necessary, starts the services in detached mode (`-d`), and ensures all services are running before proceeding.

```bash
docker compose -f compose.yml up -d --build

```

--------------------------------

### Docker Init - Go Application Example

Source: https://docs.docker.com/engine/reference/commandline/init

This example demonstrates the interactive prompts and output when using 'docker init' to set up files for a Go server application. It shows how to specify the Go version, main package directory, and server port.

```bash
$ docker init

Welcome to the Docker Init CLI!

This utility will walk you through creating the following files with sensible defaults for your project:
  - .dockerignore
  - Dockerfile
  - compose.yaml
  - README.Docker.md

Let's get started!

? What application platform does your project use?  [Use arrows to move, type to filter]
> PHP with Apache - (detected) suitable for a PHP web application
  Go - suitable for a Go server application
  Java - suitable for a Java application that uses Maven and packages as an uber jar
  Python - suitable for a Python server application
  Node - suitable for a Node server application
  Rust - suitable for a Rust server application
  ASP.NET Core - suitable for an ASP.NET Core application
  Other - general purpose starting point for containerizing your application
  Don't see something you need? Let us know!
  Quit

? What application platform does your project use? Go
? What version of Go do you want to use? 1.20
? What's the relative directory (with a leading .) of your main package? .
? What port does your server listen on? 3333

CREATED: .dockerignore
CREATED: Dockerfile
CREATED: compose.yaml
CREATED: README.Docker.md

✔ Your Docker files are ready!

Take a moment to review them and tailor them to your application.

When you're ready, start your application by running: docker compose up --build

Your application will be available at http://localhost:3333

Consult README.Docker.md for more information about using the generated files.

```

--------------------------------

### Docker Compose Command Usage Examples

Source: https://docs.docker.com/compose/faq

Illustrates the basic usage of `docker compose up`, `docker compose run`, and `docker compose start` commands. `up` is used to start services, `run` for one-off tasks, and `start` for restarting stopped containers.

```bash
docker compose up
docker compose up -d
docker compose run <service_name>
docker compose start
```

--------------------------------

### Docker Desktop Installer Flags: Service Management

Source: https://docs.docker.com/desktop/setup/install/windows-install

Shows how to configure the Docker service to start automatically upon installation. This flag bypasses the need for manual administrator intervention to start the service, which is required for Windows containers and the Hyper-V backend.

```console
"Docker Desktop Installer.exe" install --always-run-service
```

--------------------------------

### Test DMR installation and run a model

Source: https://docs.docker.com/ai/model-runner/get-started

Verifies the Docker Model Runner installation by checking its version and then runs a sample model ('ai/smollm2').

```bash
docker model version
docker model run ai/smollm2
```

--------------------------------

### Install Dependencies in Sandbox

Source: https://docs.docker.com/ai/sandboxes/workflows

Demonstrates how to instruct an agent to install system and language-specific dependencies within a sandbox. Installed packages persist for the sandbox's lifetime. This example shows installation via pip and apt.

```plaintext
You: "Install pytest and black"
Agent: [Installs packages via pip]

You: "Install build-essential"
Agent: [Installs via apt]
```

--------------------------------

### Docker Desktop Start

Source: https://docs.docker.com/reference/cli/docker/desktop

Start Docker Desktop.

```APIDOC
## docker desktop start

### Description
Start Docker Desktop.

### Method
CLI COMMAND

### Endpoint
docker desktop start

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
docker desktop start
```

### Response
#### Success Response (0)
- **message** (string) - Confirmation that Docker Desktop has started.

#### Response Example
```
Docker Desktop started successfully.
```
```

--------------------------------

### Install Docker Desktop with PowerShell and ArgumentList

Source: https://docs.docker.com/desktop/setup/install/windows-install

Demonstrates how to install Docker Desktop using PowerShell, specifically utilizing the `ArgumentList` parameter to pass installer flags. This is a common pattern when security policies restrict direct execution of installers with arguments.

```powershell
Start-Process 'Docker Desktop Installer.exe' -Wait -ArgumentList 'install', '--accept-license'
```

--------------------------------

### Install DMR on Ubuntu/Debian

Source: https://docs.docker.com/ai/model-runner/get-started

Installs the Docker Model Runner plugin on Ubuntu or Debian-based systems using apt-get. This enables the 'docker model' CLI commands.

```bash
sudo apt-get update
sudo apt-get install docker-model-plugin
```

--------------------------------

### Start Node.js Backend Service (Console)

Source: https://docs.docker.com/guides/localstack

This console command starts the Node.js backend service. Ensure all dependencies are installed and environment variables are set correctly before executing this command.

```bash
$ node index.js
```

--------------------------------

### Linux Mount Command Example

Source: https://docs.docker.com/engine/storage/volumes

A specific example of the Linux 'mount' command, demonstrating how to mount an ext4 filesystem from the '/dev/loop5' device to the '/external-drive' path on the host system.

```console
$ mount -t ext4 /dev/loop5 /external-drive
```

--------------------------------

### Build Your First Docker Image with Dockerfile

Source: https://docs.docker.com/llms

Learn how to build your first Docker image by writing a Dockerfile. This guide provides a fundamental understanding of Docker image creation.

```dockerfile
FROM alpine:latest

RUN apk --no-cache add ca-certificates

COPY . /app

WORKDIR /app

CMD ["echo", "Hello, Docker!"]
```

--------------------------------

### Docker Model Runner (DMR) API

Source: https://docs.docker.com/llms

Reference documentation for the Docker Model Runner (DMR) REST API, including configuration options, examples, getting started guides, IDE integrations, inference engines, and Open WebUI integration.

```APIDOC
## Docker Model Runner (DMR) API

### Description
This section provides API reference documentation for the Docker Model Runner (DMR). It covers the REST API endpoints, configuration options for models, example projects and workflows, guides for getting started with DMR, integrating DMR with IDEs and tools, details on supported inference engines (llama.cpp, vLLM, Diffusers), and instructions for integrating with Open WebUI.

### Endpoints

- **DMR REST API Reference**: [https://docs.docker.com/ai/model-runner/api-reference/](https://docs.docker.com/ai/model-runner/api-reference/)
- **Configuration Options**: [https://docs.docker.com/ai/model-runner/configuration/](https://docs.docker.com/ai/model-runner/configuration/)
- **DMR Examples**: [https://docs.docker.com/ai/model-runner/examples/](https://docs.docker.com/ai/model-runner/examples/)
- **Get Started with DMR**: [https://docs.docker.com/ai/model-runner/get-started/](https://docs.docker.com/ai/model-runner/get-started/)
- **IDE and Tool Integrations**: [https://docs.docker.com/ai/model-runner/ide-integrations/](https://docs.docker.com/ai/model-runner/ide-integrations/)
- **Inference Engines**: [https://docs.docker.com/ai/model-runner/inference-engines/](https://docs.docker.com/ai/model-runner/inference-engines/)
- **Open WebUI Integration**: [https://docs.docker.com/ai/model-runner/openwebui-integration/](https://docs.docker.com/ai/model-runner/openwebui-integration/)
```

--------------------------------

### Install Docker Desktop from Command Line (Windows)

Source: https://docs.docker.com/desktop/setup/install/windows-install

Installs Docker Desktop using the command line. This method is useful for automated or scripted installations. It requires the Docker Desktop installer executable to be present in the current directory or specified path.

```console
$ "Docker Desktop Installer.exe" install
```

```powershell
Start-Process 'Docker Desktop Installer.exe' -Wait install
```

```cmd
start /w "" "Docker Desktop Installer.exe" install
```

--------------------------------

### Start Container with Volume using -v

Source: https://docs.docker.com/storage/volumes

Starts a detached Nginx container named 'devtest' and mounts a volume named 'myvol2' to the '/app/' directory using the older -v flag. This achieves the same result as the --mount example, providing data persistence.

```bash
$ docker run -d \
  --name devtest \
  -v myvol2:/app \
  nginx:latest

```

--------------------------------

### Starting an A2A Server

Source: https://docs.docker.com/ai/cagent/integrations/a2a

Instructions and examples for starting a cagent A2A server with basic and custom configurations.

```APIDOC
## Starting an A2A server

Basic usage:

```console
$ cagent a2a ./agent.yaml
```

Your agent is now accessible via HTTP. Other A2A systems can discover your
agent's capabilities and call it.

Custom port:

```console
$ cagent a2a ./agent.yaml --port 8080
```

Specific agent in a team:

```console
$ cagent a2a ./agent.yaml --agent engineer
```

From OCI registry:

```console
$ cagent a2a agentcatalog/pirate --port 9000
```
```

--------------------------------

### Clone GenAI Sample Project (Bash)

Source: https://docs.docker.com/ai/model-runner/examples

Clones the 'hello-genai' repository from GitHub to set up a sample generative AI application. This is the initial step to get a pre-built GenAI app running locally.

```bash
git clone https://github.com/docker/hello-genai.git
```

--------------------------------

### Install DMR on RPM-based distributions

Source: https://docs.docker.com/ai/model-runner/get-started

Installs the Docker Model Runner plugin on RPM-based distributions like Fedora or CentOS using dnf. This enables the 'docker model' CLI commands.

```bash
sudo dnf update
sudo dnf install docker-model-plugin
```

--------------------------------

### Package and push GGUF model

Source: https://docs.docker.com/ai/model-runner/get-started

Downloads a model file in GGUF format from HuggingFace, packages it as an OCI Artifact, and pushes it to a container registry. This example uses 'mistral-7b-v0.1.Q4_K_M.gguf'.

```bash
# Download a model file in GGUF format, for example from HuggingFace
$ curl -L -o model.gguf https://huggingface.co/TheBloke/Mistral-7B-v0.1-GGUF/resolve/main/mistral-7b-v0.1.Q4_K_M.gguf

# Package it as OCI Artifact and push it to Docker Hub
$ docker model package --gguf "$(pwd)/model.gguf" --push myorg/mistral-7b-v0.1:Q4_K_M
```

--------------------------------

### Install Go SDK for Docker

Source: https://docs.docker.com/reference/api/engine/sdk

Installs the Go SDK for Docker using the go get command. Requires a recent, supported version of Go.

```console
go get github.com/moby/moby/client
```

--------------------------------

### Create Dockerfile and Sample File

Source: https://docs.docker.com/build/buildkit

Creates a directory named 'sample_dockerfile', navigates into it, and then creates a Dockerfile and a 'hello.txt' file. The Dockerfile is configured to use a Windows NanoServer base image, copy the text file, append text to it, and display its content upon container startup.

```powershell
> mkdir sample_dockerfile
> cd sample_dockerfile
> Set-Content Dockerfile @"
FROM mcr.microsoft.com/windows/nanoserver:ltsc2022
USER ContainerAdministrator
COPY hello.txt C:/
RUN echo "Goodbye!" >> hello.txt
CMD ["cmd", "/C", "type C:\hello.txt"]
"@
Set-Content hello.txt @"
Hello from BuildKit!
This message shows that your installation appears to be working correctly.
"@
```

--------------------------------

### Verify Docker installation and status

Source: https://docs.docker.com/engine/install/ubuntu

Checks if the Docker service is running after installation. If not, it provides a command to start the service manually.

```console
$ sudo systemctl status docker

$ sudo systemctl start docker
```

--------------------------------

### Pull model from HuggingFace

Source: https://docs.docker.com/ai/model-runner/get-started

Pulls a model directly from HuggingFace.co, specifying the model repository and tag. This example pulls 'Llama-3.2-1B-Instruct-GGUF'.

```bash
docker model pull hf.co/bartowski/Llama-3.2-1B-Instruct-GGUF
```

--------------------------------

### Docker Engine Installation

Source: https://docs.docker.com/llms

Documentation on installing Docker Engine from binaries.

```APIDOC
## Install Docker Engine from Binaries

### Description
Instructions for installing Docker Engine from pre-compiled binaries, suitable for testing purposes.

### Method
N/A (Installation guide)

### Endpoint
N/A (Installation guide)

### Parameters
N/A

### Request Example
N/A

### Response
N/A
```

--------------------------------

### Docker --mount Flag Example for Volumes

Source: https://docs.docker.com/engine/storage/volumes

Provides a concrete example of using the `--mount` flag to mount a named volume with specific options, including a source volume name, destination path, read-only setting, and a volume subdirectory.

```console
$ docker run --mount type=volume,src=myvolume,dst=/data,ro,volume-subpath=/foo
```

--------------------------------

### Clone Sample Deno Application using Git

Source: https://docs.docker.com/guides/deno/develop

This command clones the sample Deno application repository from GitHub and changes the current directory into the cloned repository. It serves as the starting point for setting up the containerized development environment.

```bash
git clone https://github.com/dockersamples/docker-deno.git && cd docker-deno
```

--------------------------------

### Remove a Docker Sandbox (CLI)

Source: https://docs.docker.com/ai/sandboxes/get-started

Deletes a specified Docker sandbox VM and all its installed packages. This command can also be used to remove multiple sandboxes simultaneously by listing their names.

```console
docker sandbox rm <sandbox-name>
```

```console
docker sandbox rm <sandbox-1> <sandbox-2>
```

--------------------------------

### Start Interactive Container on Overlay Network

Source: https://docs.docker.com/engine/network/drivers/overlay

Starts an interactive Alpine Linux container named 'alpine1' and connects it to the 'test-net' overlay network. Requires the 'test-net' network to exist and Docker installed.

```console
$ docker run -it --name alpine1 --network test-net alpine
/ #
```

--------------------------------

### Docker Compose Example for PostgreSQL Database

Source: https://docs.docker.com/guides/python/develop

This Docker Compose configuration defines a PostgreSQL database service. It utilizes a specific image, restarts policy, user, secrets for password management, volumes for data persistence, environment variables for database setup, and a healthcheck to ensure the database is ready before other services start.

```yaml
services:
  app:
    build: .
    depends_on:
      db:
        condition: service_healthy
    ports:
      - 8000:8000
    volumes:
      - .:/code
      - log:/code/logs
    environment:
      - MESSAGE_BROKER_URL=amqp://guest:guest@rabbitmq:5672/
      - DATABASE_URL=postgres://user:password@db:5432/example
  db:
    image: postgres:18
    restart: always
    user: postgres
    secrets:
      - db-password
    volumes:
      - db-data:/var/lib/postgresql
    environment:
      - POSTGRES_DB=example
      - POSTGRES_PASSWORD_FILE=/run/secrets/db-password
    expose:
      - 5432
    healthcheck:
      test: [ "CMD", "pg_isready" ]
      interval: 10s
      timeout: 5s
      retries: 5

volumes:
  db-data:

secrets:
  db-password:
    file: db/password.txt

```

--------------------------------

### List Local Docker Images

Source: https://docs.docker.com/compose/gettingstarted

Displays a list of all local Docker images available on the system. This command is useful for verifying that images, such as 'redis' and 'web' in this context, have been built or pulled correctly.

```console
$ docker image ls
```

--------------------------------

### Docker Checkpoint and Restore Example

Source: https://docs.docker.com/reference/cli/docker/checkpoint

Provides a practical example of using Docker checkpoint and restore. It demonstrates creating a busybox container, creating a checkpoint for it, and then restoring the container from that checkpoint, showing how the process state is preserved.

```bash
$ docker run --security-opt=seccomp:unconfined --name cr -d busybox /bin/sh -c 'i=0; while true; do echo $i; i=$(expr $i + 1); sleep 1; done'
abc0123

$ docker checkpoint create cr checkpoint1

# <later>
$ docker start --checkpoint checkpoint1 cr
abc0123
```

--------------------------------

### Install Dependencies with RUN Instruction

Source: https://docs.docker.com/build/concepts/dockerfile

The `RUN` instruction executes commands within the base image during the build process. This example updates the package index and installs Python 3 and pip. It's crucial for setting up the environment and installing necessary tools.

```dockerfile
# install app dependencies
RUN apt-get update && apt-get install -y python3 python3-pip
```

--------------------------------

### Install Continue AI Assistant

Source: https://docs.docker.com/ai/sandboxes/agents/shell

Installs the Continue AI code assistant globally using npm. Node.js is pre-installed in the shell sandbox environment. Includes a command to verify the installation.

```bash
npm install -g @continuedev/cli
cn --version
```

--------------------------------

### Docker Desktop Installation with User and Proxy Settings

Source: https://docs.docker.com/desktop/setup/install/mac-install

This example shows how to install Docker Desktop with specific user privileges and manual proxy configuration, including specifying a PAC file URL. It requires the Docker.app to be in the Applications folder.

```console
sudo /Applications/Docker.app/Contents/MacOS/install --user testuser --proxy-http-mode="manual" --override-proxy-pac="http://localhost:8080/myproxy.pac"
```

--------------------------------

### Install and Use Pre-commit Hooks

Source: https://docs.docker.com/guides/python/lint-format-typing

Installs the pre-commit hooks and demonstrates how to trigger them. Running `pre-commit install` sets up the hooks, and subsequent commits will automatically run the configured checks.

```bash
pre-commit install
git commit -m "Test commit"  # Automatically runs checks
```

--------------------------------

### Access a Running Docker Sandbox (CLI)

Source: https://docs.docker.com/ai/sandboxes/get-started

Executes a command within a running Docker sandbox. The `-it` flags are used to open an interactive shell, which is useful for debugging or installing additional tools inside the sandbox environment.

```console
docker sandbox exec -it <sandbox-name> bash
```

--------------------------------

### Navigate to Project Directory

Source: https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-registry

Changes the current directory to the cloned 'helloworld-demo-node' project folder.

```bash
cd helloworld-demo-node
```

--------------------------------

### Start Docker service manually

Source: https://docs.docker.com/engine/install/ubuntu

Manually starts the Docker service if it is not running automatically after installation. This command is used when the system's configuration prevents the Docker service from starting on its own.

```console
sudo systemctl start docker
```

--------------------------------

### Install Latest Docker Engine (Fedora)

Source: https://docs.docker.com/engine/install/fedora

Installs the latest stable version of Docker Engine, Docker CLI, containerd.io, and Docker Compose plugin using the DNF package manager. This command installs the packages but does not start the Docker service.

```bash
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

--------------------------------

### Run Docker Compose with Watch Mode

Source: https://docs.docker.com/compose/gettingstarted

Builds and launches the application using Docker Compose and enables file watch mode. This command automatically rebuilds and restarts containers when source files change. It requires Docker Compose to be installed and configured for the project.

```console
docker compose watch
docker compose up --watch
```

--------------------------------

### Verify Docker Installation with hello-world Image (PowerShell)

Source: https://docs.docker.com/engine/install/binaries

This command verifies the Docker installation by downloading and running the 'hello-world:nanoserver' image. A successful execution will display a confirmation message from Docker, indicating that the installation and service are functioning correctly.

```powershell
& $Env:ProgramFiles\Docker\docker run hello-world:nanoserver
```

--------------------------------

### Dockerfile for Python Web App

Source: https://docs.docker.com/compose/gettingstarted

Defines the steps to build a Docker image for the Python web application. It specifies the base image, sets up the working directory, installs dependencies, exposes the application port, and defines the command to run the application.

```dockerfile
# syntax=docker/dockerfile:1
FROM python:3.10-alpine
WORKDIR /code
ENV FLASK_APP=app.py
ENV FLASK_RUN_HOST=0.0.0.0
RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
EXPOSE 5000
COPY . .
CMD ["flask", "run", "--debug"]

```

--------------------------------

### Setup Docker Desktop in GitHub Actions Workflow

Source: https://docs.docker.com/extensions/extensions-sdk/dev/continuous-integration

This YAML snippet demonstrates how to add the Docker Desktop Action to a GitHub Actions workflow to start Docker Desktop. This is a prerequisite for installing and validating Docker extensions in a CI environment. Note that this action currently only supports macOS runners.

```yaml
steps:
  - id: start_desktop
    uses: docker/desktop-action/start@v0.1.0
```

--------------------------------

### Policy Templates and Examples for Docker Builds

Source: https://docs.docker.com/llms

This documentation provides a collection of policy templates and examples for Docker builds. These resources range from simple configurations to complex security templates for production environments.

```markdown
This section offers a library of pre-
```

--------------------------------

### Build Docker Image

Source: https://docs.docker.com/docker-hub/quickstart

Builds a Docker image from the current directory's Dockerfile and tags it with a specified username and image name for Docker Hub. Replace <YOUR-USERNAME> with your actual Docker ID. This command prepares the image for pushing to a remote registry.

```bash
$ docker build -t <YOUR-USERNAME>/nginx-custom .
```

--------------------------------

### Configure iptables for Swarm data path port encryption

Source: https://docs.docker.com/engine/swarm/swarm-tutorial

This example demonstrates an iptables rule to drop unencrypted UDP traffic on the Swarm data path port (4789). This is a security measure for untrusted networks when using encrypted overlay networks.

```bash
iptables -I INPUT -m udp --dport 4789 -m policy --dir in --pol none -j DROP
```

--------------------------------

### Migrate Go Application to Docker Hardened Image

Source: https://docs.docker.com/llms

This guide provides instructions and examples for migrating a Go application to use Docker Hardened Images. It outlines the steps necessary to adapt your existing Go project for a hardened environment.

```go
package main

import "fmt"

func main() {
	fmt.Println("Hello from a Go application in a DHI!")
}
```

--------------------------------

### Using ADD to Download and Extract Remote Artifacts

Source: https://docs.docker.com/build/building/best-practices

Illustrates the use of the ADD instruction to download a .NET installer from a remote URL and extract it. This example leverages multi-stage builds to ensure only the necessary runtime remains in the final image.

```dockerfile
# syntax=docker/dockerfile:1

FROM scratch AS src
ARG DOTNET_VERSION=8.0.0-preview.6.23329.7
ADD --checksum=sha256:270d731bd08040c6a3228115de1f74b91cf441c584139ff8f8f6503447cebdbb \
    https://dotnetcli.azureedge.net/dotnet/Runtime/$DOTNET_VERSION/dotnet-runtime-$DOTNET_VERSION-linux-arm64.tar.gz /dotnet.tar.gz

FROM mcr.microsoft.com/dotnet/runtime-deps:8.0.0-preview.6-bookworm-slim-arm64v8 AS installer

# Retrieve .NET Runtime
RUN --mount=from=src,target=/src <<EOF
mkdir -p /dotnet
tar -oxzf /src/dotnet.tar.gz -C /dotnet
EOF

FROM mcr.microsoft.com/dotnet/runtime-deps:8.0.0-preview.6-bookworm-slim-arm64v8

COPY --from=installer /dotnet /usr/share/dotnet
RUN ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet
```

--------------------------------

### Ignore Cache for Specific Dockerfile Stages (Example)

Source: https://docs.docker.com/engine/reference/commandline/buildx_build

Demonstrates how to use the `--no-cache-filter` flag to ignore the build cache for specific stages in a multi-stage Dockerfile. This example shows ignoring the 'install' stage and then ignoring both 'install' and 'release' stages.

```bash
$ docker buildx build --no-cache-filter install .
$ docker buildx build --no-cache-filter install,release .
```

--------------------------------

### Execute Helper Script with Default Command

Source: https://docs.docker.com/develop/security-best-practices

Demonstrates running a Docker container where the ENTRYPOINT is a script that defaults to starting the 'postgres' process.

```shell
$ docker run postgres
```

--------------------------------

### Verify Docker service status

Source: https://docs.docker.com/engine/install/ubuntu

Checks if the Docker service is running after installation or manual start. This command is useful for confirming that Docker has been successfully installed and is operational.

```console
sudo systemctl status docker
```

--------------------------------

### Complete Dockerfile Example

Source: https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile

This is a complete Dockerfile that combines all the previous instructions to create a runnable image for a Node.js application. It sets the base image, working directory, copies files, installs dependencies, and specifies the entry point command.

```dockerfile
FROM node:22-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "./src/index.js"]
```

--------------------------------

### Install Docker Desktop with Organization Enforcement

Source: https://docs.docker.com/enterprise/security/enforce-sign-in/methods

Configure Docker Desktop to enforce organization sign-in during the installation process on Windows and macOS. This method requires specific command-line arguments during setup.

```powershell
# PowerShell
Start-Process '.\Docker Desktop Installer.exe' -Wait 'install --allowed-org=myorg'
```

```cmd
"Docker Desktop Installer.exe" install --allowed-org=myorg
```

```bash
sudo hdiutil attach Docker.dmg
sudo /Volumes/Docker/Docker.app/Contents/MacOS/install --allowed-org=myorg
sudo hdiutil detach /Volumes/Docker
```

--------------------------------

### Start Docker container with host directory obscuring container contents (--mount)

Source: https://docs.docker.com/engine/storage/bind-mounts

Demonstrates mounting a host directory ('/tmp') over a non-empty directory ('/usr') within a container using the '--mount' flag. This example is intended to show how existing container contents can be obscured, potentially leading to a non-functional container.

```console
$ docker run -d \
  -it \
  --name broken-container \
  --mount type=bind,source=/tmp,target=/usr \
  nginx:latest
```

--------------------------------

### Start Docker Desktop service on Fedora

Source: https://docs.docker.com/desktop/setup/install/linux/fedora

Starts the Docker Desktop service for the current user using systemctl. This command is an alternative to launching Docker Desktop from the desktop environment.

```bash
$ systemctl --user start docker-desktop
```

--------------------------------

### Docker Events Output Example

Source: https://docs.docker.com/reference/cli/docker/system/events

This is an example of the output generated by the `docker events` command when containers are created, started, and stopped. The output includes timestamps, event types, container IDs, and associated metadata.

```console
2017-01-05T00:35:58.859401177+08:00 container create 0fdb48addc82871eb34eb23a847cfd033dedd1a0a37bef2e6d9eb3870fc7ff37 (image=alpine:latest, name=test)
2017-01-05T00:36:04.703631903+08:00 network connect e2e1f5ceda09d4300f3a846f0acfaa9a8bb0d89e775eb744c5acecd60e0529e2 (container=0fdb...ff37, name=bridge, type=bridge)
2017-01-05T00:36:04.795031609+08:00 container start 0fdb...ff37 (image=alpine:latest, name=test)
2017-01-05T00:36:09.830268747+08:00 container kill 0fdb...ff37 (image=alpine:latest, name=test, signal=15)
2017-01-05T00:36:09.840186338+08:00 container die 0fdb...ff37 (exitCode=143, image=alpine:latest, name=test)
2017-01-05T00:36:09.880113663+08:00 network disconnect e2e...29e2 (container=0fdb...ff37, name=bridge, type=bridge)
2017-01-05T00:36:09.890214053+08:00 container stop 0fdb...ff37 (image=alpine:latest, name=test)
```

--------------------------------

### Start Container with Volume (-v flag)

Source: https://docs.docker.com/engine/storage/volumes

This command achieves the same result as the --mount flag example: it starts a detached Nginx container named 'devtest' and mounts the volume 'myvol2' to the '/app/' directory. Docker creates the volume if it doesn't exist.

```console
$ docker run -d \
  --name devtest \
  -v myvol2:/app \
  nginx:latest
```

--------------------------------

### Enable Docker Desktop to start on sign-in on Fedora

Source: https://docs.docker.com/desktop/setup/install/linux/fedora

Enables the Docker Desktop service to start automatically when the user signs in to their system. This is an alternative to configuring the startup behavior through the Docker Desktop settings GUI.

```bash
$ systemctl --user enable docker-desktop
```

--------------------------------

### RUN --network=none: Isolate pip installs

Source: https://docs.docker.com/engine/reference/builder

This example shows how to use `RUN --network=none` to isolate a `pip install` command, ensuring that packages are only installed from a local wheelhouse. This prevents unintended network access during package installation, enhancing build reproducibility and security.

```dockerfile
# syntax=docker/dockerfile:1
FROM python:3.6
ADD mypackage.tgz wheels/
RUN --network=none pip install --find-links wheels mypackage
# `pip` will only be able to install the packages provided in the tarfile, which can be controlled by an earlier build stage.
```

--------------------------------

### Example Complete Project Configuration

Source: https://docs.docker.com/ai/cagent/reference/config

A comprehensive example configuration demonstrating various features of the project setup. It includes agent definitions, model configurations, and RAG settings.

```yaml
agents:
  root:
    model: claude
    description: Technical lead
    instruction: Coordinate development tasks and delegate to specialists
    sub_agents: [developer, reviewer]
    toolsets:
      - type: filesystem
      - type: mcp
        ref: docker:duckduckgo
    rag: [readmes]
    commands:
      status: "Check project status"

  developer:
    model: gpt
    description: Software developer
    instruction: Write clean, maintainable code
    toolsets:
      - type: filesystem
      - type: shell

  reviewer:
    model: claude
    description: Code reviewer
    instruction: Review for quality and security
    toolsets:
      - type: filesystem

models:
  gpt:
    provider: openai
    model: gpt-5

  claude:
    provider: anthropic
    model: claude-sonnet-4-5
    max_tokens: 64000

rag:
  readmes:
    docs: ["**/README.md"]
    strategies:
      - type: chunked-embeddings
        embedding_model: openai/text-embedding-3-small
        vector_dimensions: 1536
        database: ./embeddings.db
        limit: 10
      - type: bm25
        database: ./bm25.db
        limit: 10
    results:
      fusion:
        strategy: rrf
        k: 60
      limit: 5
```

--------------------------------

### Run a container with Docker Offload

Source: https://docs.docker.com/offload/quickstart

Executes a container using Docker Offload. This command verifies that Docker Offload is functioning correctly by running the standard 'hello-world' container remotely. The output should confirm successful execution.

```bash
docker run --rm hello-world
```

--------------------------------

### Install Docker Rootless Mode with Packages (RPM/DEB)

Source: https://docs.docker.com/engine/security/rootless

Installs Docker in rootless mode using the `dockerd-rootless-setuptool.sh` script, typically available when Docker is installed via RPM or DEB packages. This script automates the setup process for the rootless daemon.

```bash
$ dockerd-rootless-setuptool.sh install
```

--------------------------------

### Install XQuartz for Docker GUI on macOS

Source: https://docs.docker.com/guides/ros2/turtlesim-example

Installs XQuartz, a prerequisite for running GUI applications from Docker containers on macOS. It enables X11 support and requires enabling network client connections.

```bash
brew install --cask xquartz
defaults write org.xquartz.X11 nolisten_tcp -bool false
xhost +localhost
xhost + 127.0.0.1
```

--------------------------------

### Docker Login Examples

Source: https://docs.docker.com/reference/cli/docker/login

Provides examples of how to use the `docker login` command for different scenarios.

```APIDOC
## Docker Login Examples

### Authenticate to Docker Hub with web-based login

This method uses a device code flow for authentication without entering a password directly.

**Command:**
```console
$ docker login
```

**Output Example:**
```console
USING WEB-BASED LOGIN
To sign in with credentials on the command line, use 'docker login -u <username>'

Your one-time device confirmation code is: LNFR-PGCJ
Press ENTER to open your browser or submit your device code here: https://login.docker.com/activate 

Waiting for authentication in the browser…
```

### Authenticate to a self-hosted registry

Specify the server name for self-hosted registries. The port can also be specified if it's not the default (443 or 80).

**Command (hostname only):**
```console
$ docker login registry.example.com
```

**Command (with port):**
```console
$ docker login registry.example.com:1337
```

**Note:** Registry addresses should only include the hostname and optional port. Avoid URL path components, except for the Docker Hub registry (`/v1/`).

### Authenticate to a registry with a username and password

Use the `--username` or `-u` flag to provide credentials. The password will be prompted interactively.

**Command:**
```console
$ docker login -u moby
```
```

--------------------------------

### Docker Extension Backend Tutorial

Source: https://docs.docker.com/llms

Illustrates how to add a backend service to a Docker extension. This involves setting up a Go application that communicates with the Docker Desktop frontend.

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintf(w, "Hello from extension backend!")
	})
	http.ListenAndServe(":8080", nil)
}
```

--------------------------------

### Install Docker pre-releases using convenience script

Source: https://docs.docker.com/engine/install/fedora

This command downloads the Docker convenience script from test.docker.com and executes it with sudo privileges. This installs pre-release versions of Docker, allowing you to test new features and evaluate them before stable releases.

```bash
curl -fsSL https://test.docker.com -o test-docker.sh
sudo sh test-docker.sh
```

--------------------------------

### List Docker Images

Source: https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-registry

Displays a list of all Docker images available on your local system, including the newly built 'docker-quickstart' image.

```bash
docker images
```

--------------------------------

### Dockerfile Example for C Program Build

Source: https://docs.docker.com/build/cache

A sample Dockerfile demonstrating a multi-stage build process for a C program. It includes steps for updating packages, installing build essentials, copying source code, and compiling the program. This example helps illustrate Docker's layer caching.

```dockerfile
# syntax=docker/dockerfile:1
FROM ubuntu:latest

RUN apt-get update && apt-get install -y build-essentials
COPY main.c Makefile /src/
WORKDIR /src/
RUN make build
```

--------------------------------

### Format Volume List with Go Template

Source: https://docs.docker.com/reference/cli/docker/volume/ls

This example demonstrates how to use the --format option with a Go template to display specific volume information (Name and Driver) separated by a colon. It requires the 'docker' CLI and assumes volumes are present.

```console
$ docker volume ls --format "{{.Name}}: {{.Driver}}"

vol1: local
vol2: local
vol3: local
```

--------------------------------

### Set up and Use Docker Build Cloud in Development

Source: https://docs.docker.com/llms

Discover how to set up and utilize Docker Build Cloud for your local development builds. This guide helps you leverage Build Cloud for faster local development cycles.

```Shell
# Example command to build an image using Docker Build Cloud locally
docker buildx build --platform linux/amd64,linux/arm64 -t your-dockerhub-username/your-app:latest --push .
```

--------------------------------

### Build Multi-Platform Docker Images with GitHub Actions

Source: https://docs.docker.com/llms

This example demonstrates building Docker images for multiple architectures (e.g., amd64, arm64) using GitHub Actions. It leverages QEMU emulation or multiple native builders to achieve cross-platform compatibility.

```yaml
name: Multi-Platform Build

on: [push]

jobs:
  multi-platform-build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2
    - name: Build multi-platform image
      uses: docker/build-push-action@v4
      with:
        context: .
        file: ./Dockerfile
        push: true
        platforms: linux/amd64,linux/arm64
        tags: your-dockerhub-username/your-multiarch-image:latest
```

--------------------------------

### Complete Example: Open WebUI with Multiple Models Pre-pulled

Source: https://docs.docker.com/ai/model-runner/openwebui-integration

This Docker Compose setup configures Open WebUI, pre-pulls multiple AI models (llama3.2, qwen2.5-coder, smollm2), and sets up a dependency for model pulling. It uses `host.docker.internal` for the Ollama base URL and disables authentication. The `model-setup` service ensures models are pulled before Open WebUI starts.

```yaml
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:main
    ports:
      - "3000:8080"
    environment:
      - OLLAMA_BASE_URL=http://host.docker.internal:12434
      - WEBUI_AUTH=false
      - DEFAULT_MODELS=ai/llama3.2
    extra_hosts:
      - "host.docker.internal:host-gateway"
    volumes:
      - open-webui:/app/backend/data
    depends_on:
      model-setup:
        condition: service_completed_successfully

  model-setup:
    image: docker:cli
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    command: >
      sh -c "
        docker model pull ai/llama3.2 &&
        docker model pull ai/qwen2.5-coder &&
        docker model pull ai/smollm2
      "

volumes:
  open-webui:

```

--------------------------------

### Install and Run Turtlesim Node (ROS 2 Humble)

Source: https://docs.docker.com/guides/ros2/turtlesim-example

Installs the Turtlesim package within the ROS 2 Humble environment inside the Docker container and then runs the Turtlesim node. This requires updating the package manager first.

```bash
sudo apt update
sudo apt install -y ros-humble-turtlesim
ros2 run turtlesim turtlesim_node
```

--------------------------------

### Get Information About a ROS 2 Topic

Source: https://docs.docker.com/guides/ros2/turtlesim-example

Displays information about a specific ROS 2 topic, including its type and the nodes that publish and subscribe to it.

```bash
ros2 topic info /turtle1/pose
```

--------------------------------

### Install PHP Extensions and Composer

Source: https://docs.docker.com/guides/frameworks/laravel/development-setup

Installs common PHP extensions like pdo_mysql, pdo_pgsql, redis, intl, zip, bcmath, and soap. It also installs Composer globally for managing PHP dependencies. System dependencies like curl, unzip, and various development libraries are installed first.

```dockerfile
FROM php:8.5-cli

ARG UID=1000
ARG GID=1000
ARG NODE_VERSION=22.0.0

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    unzip \
    libpq-dev \
    libonig-dev \
    libssl-dev \
    libxml2-dev \
    libcurl4-openssl-dev \
    libicu-dev \
    libzip-dev \
    && docker-php-ext-install -j$(nproc) \
    pdo_mysql \
    pdo_pgsql \
    pgsql \
    intl \
    zip \
    bcmath \
    soap \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
```

--------------------------------

### GitHub Actions Workflow for Model Runner

Source: https://docs.docker.com/ai/model-runner/examples

This YAML workflow automates the process of setting up Docker, installing the docker-model-plugin, testing the installation, pulling and running a specified model, and testing its API endpoint. It includes input parameters for selecting the model to test and uses standard GitHub Actions steps and shell commands.

```yaml
name: Docker Model Runner Example Workflow

permissions:
  contents: read

on:
  workflow_dispatch:
    inputs:
      test_model:
        description: 'Model to test with (default: ai/smollm2:360M-Q4_K_M)'
        required: false
        type: string
        default: 'ai/smollm2:360M-Q4_K_M'

jobs:
  dmr-test:
    runs-on: ubuntu-latest
    timeout-minutes: 30

    steps:
      - name: Set up Docker
        uses: docker/setup-docker-action@v4

      - name: Install docker-model-plugin
        run: |
          echo "Installing docker-model-plugin..."
          # Add Docker's official GPG key:
          sudo apt-get update
          sudo apt-get install ca-certificates curl
          sudo install -m 0755 -d /etc/apt/keyrings
          sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
          sudo chmod a+r /etc/apt/keyrings/docker.asc
          
          # Add the repository to Apt sources:
          echo \
          "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
          $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
          sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
          sudo apt-get update
          sudo apt-get install -y docker-model-plugin
          
          echo "Installation completed successfully"

      - name: Test docker model version
        run: |
          echo "Testing docker model version command..."
          sudo docker model version
          
          # Verify the command returns successfully
          if [ $? -eq 0 ]; then
            echo "✅ docker model version command works correctly"
          else
            echo "❌ docker model version command failed"
            exit 1
          fi

      - name: Pull the provided model and run it
        run: |
          MODEL="${{ github.event.inputs.test_model || 'ai/smollm2:360M-Q4_K_M' }}"
          echo "Testing with model: $MODEL"
          
          # Test model pull
          echo "Pulling model..."
          sudo docker model pull "$MODEL"
          
          if [ $? -eq 0 ]; then
            echo "✅ Model pull successful"
          else
            echo "❌ Model pull failed"
            exit 1
          fi
                  
          # Test basic model run (with timeout to avoid hanging)
          echo "Testing docker model run..."
          timeout 60s sudo docker model run "$MODEL" "Give me a fact about whales." || {
            exit_code=$?
            if [ $exit_code -eq 124 ]; then
              echo "✅ Model run test completed (timed out as expected for non-interactive test)"
            else
              echo "❌ Model run failed with exit code: $exit_code"
              exit 1
            fi
          }
      - name: Test model pull and run
        run: |
          MODEL="${{ github.event.inputs.test_model || 'ai/smollm2:360M-Q4_K_M' }}"
          echo "Testing with model: $MODEL"
          
          # Test model pull
          echo "Pulling model..."
          sudo docker model pull "$MODEL"
          
          if [ $? -eq 0 ]; then
            echo "✅ Model pull successful"
          else
            echo "❌ Model pull failed"
            exit 1
          fi
                  
          # Test basic model run (with timeout to avoid hanging)
          echo "Testing docker model run..."
          timeout 60s sudo docker model run "$MODEL" "Give me a fact about whales." || {
            exit_code=$?
            if [ $exit_code -eq 124 ]; then
              echo "✅ Model run test completed (timed out as expected for non-interactive test)"
            else
              echo "❌ Model run failed with exit code: $exit_code"
              exit 1
            fi
          }

      - name: Test API endpoint
        run: |
          MODEL="${{ github.event.inputs.test_model || 'ai/smollm2:360M-Q4_K_M' }}"
          echo "Testing API endpoint with model: $MODEL"
                  
          # Test API call with curl
          echo "Testing API call..."
          RESPONSE=$(curl -s http://localhost:12434/engines/llama.cpp/v1/chat/completions \
            -H "Content-Type: application/json" \
            -d "{
                \"model\": \"$MODEL\",
                \"messages\": [
                    {
                        \"role\": \"user\",
                        \"content\": \"Say hello\"
                    }
                ],
                \"top_k\": 1,
                \"temperature\": 0
            }")
          
          if [ $? -eq 0 ]; then
            echo "✅ API call successful"
            echo "Response received: $RESPONSE"

```

--------------------------------

### Start cagent for MCP Clients

Source: https://docs.docker.com/ai/cagent/integrations/mcp

Starts the cagent with MCP support, specifying the agent configuration file and working directory. This is a prerequisite for other MCP-compatible clients to communicate with cagent.

```console
cagent mcp /path/to/agent.yml --working-dir /project/path
```

--------------------------------

### Python Project Dependencies

Source: https://docs.docker.com/compose/gettingstarted

Lists the Python packages required for the Flask application to run. These are typically installed using pip.

```text
flask
redis

```

--------------------------------

### Enable Docker Desktop to Start on Sign In

Source: https://docs.docker.com/desktop/setup/install/linux/ubuntu

This command configures Docker Desktop to automatically start when the user signs in to their computer. This ensures Docker is ready to use immediately after login, bypassing the need for manual startup.

```console
systemctl --user enable docker-desktop
```

--------------------------------

### Install Docker Desktop on Debian Linux

Source: https://docs.docker.com/llms

Step-by-step instructions for installing Docker Desktop on Debian-based Linux distributions. This typically involves adding the Docker repository and installing the appropriate package.

```bash
# Update package index and install prerequisites
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg

# Add Docker's official GPG key
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources
echo 
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian 
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | 
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Desktop
sudo apt-get update
sudo apt-get install -y docker-desktop
```

--------------------------------

### Install Docker Engine from Binaries

Source: https://docs.docker.com/llms

Instructions for installing Docker Engine directly from pre-compiled binaries. This method is often suitable for testing or environments where package managers are not available.

```bash
# Download the binary
curl -fsSL https://get.docker.com/ | sh

# Alternatively, download specific versions:
# wget https://download.docker.com/linux/static/stable/x86_64/docker-20.10.7.tgz
# tar -xzf docker-20.10.7.tgz
# sudo mv docker/* /usr/local/
# sudo dockerd --daemon &
```

--------------------------------

### Clone and Navigate Project Directory (Bash)

Source: https://docs.docker.com/get-started/introduction/develop-with-containers

Clones the 'getting-started-todo-app' repository from GitHub and navigates into the newly created project directory. This is the initial step to set up the local development environment.

```bash
$ git clone https://github.com/docker/getting-started-todo-app
$ cd getting-started-todo-app
```

--------------------------------

### Expose host devices to Windows containers (--device)

Source: https://docs.docker.com/reference/cli/docker/container/run

Illustrates how to expose host devices to a Windows container using the --device option with a device interface class GUID. This example makes all COM ports available in the container.

```powershell
PS C:\> docker run --device=class/86E0D1E0-8089-11D0-9CE4-08003E301F73 mcr.microsoft.com/windows/servercore:ltsc2019
```

--------------------------------

### Develop with Docker and WSL 2

Source: https://docs.docker.com/llms

Understand how to develop applications using Docker and WSL 2 on Windows. This guide covers setting up your environment, leveraging WSL 2's Linux capabilities for Docker, and utilizing features like GPU support for machine learning workloads.

```bash
# Ensure Docker Desktop is installed and configured to use the WSL 2 backend.
# Develop your application within your WSL 2 distribution and use Docker commands as usual.
```

--------------------------------

### Start Turtlesim Docker Container (Linux)

Source: https://docs.docker.com/guides/ros2/turtlesim-example

Starts the ROS 2 environment and Turtlesim within a Docker container on Linux. This involves navigating to the workspace directory and using Docker Compose to bring up the services.

```bash
cd ws_linux
docker compose up -d
docker compose exec ros2 /bin/bash
```

--------------------------------

### Node.js Dockerfile Migration to Docker Hardened Images (Single-stage)

Source: https://docs.docker.com/dhi/migration/examples/node

This Dockerfile example demonstrates a Node.js application after migrating to Docker Hardened Images using a single-stage build. While simpler than multi-stage builds, this approach results in a larger image with a broader attack surface. It includes steps for dependency installation and application setup within a single stage.

```dockerfile
#syntax=docker/dockerfile:1

FROM dhi.io/node:23-alpine3.21-dev
WORKDIR /usr/src/app

COPY package*.json ./

# Install any additional packages if needed using apk
# RUN apk add --no-cache python3 make g++

RUN npm install

COPY . .

CMD ["node", "index.js"]
```

--------------------------------

### Nodemon Development Server Output

Source: https://docs.docker.com/get-started/workshop/06_bind_mounts

This is an example of the output seen when the Node.js development server starts using Nodemon. It indicates that Nodemon is watching for file changes and has successfully started the Node.js application, showing the port it's listening on.

```console
nodemon -L src/index.js
[nodemon] 2.0.20
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,json
[nodemon] starting `node src/index.js`
Using sqlite database at /etc/todos/todo.db
Listening on port 3000
```

--------------------------------

### Start Ubuntu Container

Source: https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers

Initiates a new Ubuntu container and provides an interactive shell prompt within it. This is the first step to modifying the base OS.

```console
$ docker run --name=base-container -ti ubuntu
```

--------------------------------

### Recreate a Docker Sandbox (CLI)

Source: https://docs.docker.com/ai/sandboxes/get-started

Removes an existing Docker sandbox and then recreates it. This process is used to start with a clean environment. Custom templates and workspace paths are configured during the recreation process.

```console
docker sandbox rm <sandbox-name>
docker sandbox run claude [PATH]
```

--------------------------------

### Start Development Environment with Docker Compose

Source: https://docs.docker.com/guides/frameworks/laravel/development-setup

This command builds and starts all defined services in the Docker Compose configuration in detached mode. It ensures the development environment is running and accessible.

```bash
docker compose -f compose.dev.yaml up --build -d
```

--------------------------------

### Start Turtlesim Docker Container (macOS)

Source: https://docs.docker.com/guides/ros2/turtlesim-example

Starts the ROS 2 environment and Turtlesim within a Docker container on macOS. This involves navigating to the workspace directory and using Docker Compose to bring up the services.

```bash
cd ws_mac
docker compose up -d
docker compose exec ros2 /bin/bash
```

--------------------------------

### Docker FROM Instruction: Basic Usage

Source: https://docs.docker.com/engine/reference/builder

Provides the syntax for the FROM instruction, which initializes a new build stage and sets the base image. It can accept an image name, optionally with a tag or digest, and can be aliased with AS.

```dockerfile
FROM [--platform=<platform>] <image> [AS <name>]
```

```dockerfile
FROM [--platform=<platform>] <image>[:<tag>] [AS <name>]
```

```dockerfile
FROM [--platform=<platform>] <image>[@<digest>] [AS <name>]
```

--------------------------------

### QEMU and Buildx Setup Actions

Source: https://docs.docker.com/build/ci/github-actions/manage-tags-labels

Sets up QEMU for cross-platform emulation and Docker Buildx for enhanced Docker build capabilities. These actions are prerequisites for building multi-architecture Docker images efficiently within the GitHub Actions environment.

```yaml
- name: Set up QEMU
  uses: docker/setup-qemu-action@v3

- name: Set up Docker Buildx
  uses: docker/setup-buildx-action@v3
```

--------------------------------

### Create and Run Copilot Sandbox After Authentication

Source: https://docs.docker.com/ai/sandboxes/agents/copilot

Steps to create a Copilot sandbox and then run it after setting up environment variables. This involves creating the sandbox and then starting it.

```console
$ docker sandbox create copilot ~/project
$ docker sandbox run <sandbox-name>

```

--------------------------------

### Docker Offload Commands

Source: https://docs.docker.com/llms

Commands for diagnosing, starting, checking status, stopping, and getting the version of Docker offload.

```APIDOC
## Docker Offload Diagnose

### Description
Diagnose issues with Docker offload.

### Method
`docker offload diagnose`

### Endpoint
`/offload/diagnose`

### Request Example
```json
{
  "example": "docker offload diagnose"
}
```

### Response
#### Success Response (200)
- **Diagnosis Report** (string) - A report detailing any diagnosed issues.

#### Response Example
```json
{
  "example": "No issues found."
}
```

## Docker Offload Start

### Description
Start Docker offload.

### Method
`docker offload start`

### Endpoint
`/offload/start`

### Request Example
```json
{
  "example": "docker offload start"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Docker offload started."
}
```

## Docker Offload Status

### Description
Get the status of Docker offload.

### Method
`docker offload status`

### Endpoint
`/offload/status`

### Request Example
```json
{
  "example": "docker offload status"
}
```

### Response
#### Success Response (200)
- **Status** (string) - The current status of Docker offload.

#### Response Example
```json
{
  "example": "running"
}
```

## Docker Offload Stop

### Description
Stop Docker offload.

### Method
`docker offload stop`

### Endpoint
`/offload/stop`

### Request Example
```json
{
  "example": "docker offload stop"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Docker offload stopped."
}
```

## Docker Offload Version

### Description
Get the version of Docker offload.

### Method
`docker offload version`

### Endpoint
`/offload/version`

### Request Example
```json
{
  "example": "docker offload version"
}
```

### Response
#### Success Response (200)
- **Version** (string) - The version of Docker offload.

#### Response Example
```json
{
  "example": "1.0.0"
}
```
```

--------------------------------

### Verify Docker Installation

Source: https://docs.docker.com/engine/install/fedora

Runs the 'hello-world' Docker image to confirm that Docker Engine is installed correctly and running. This command downloads and executes a test container.

```bash
sudo docker run hello-world
```

--------------------------------

### Docker --volume Flag Example

Source: https://docs.docker.com/engine/storage/volumes

Presents an example of the `--volume` flag used to mount a named volume to a container path with the read-only option enabled. This demonstrates the concise syntax of the `-v` flag.

```console
$ docker run -v myvolume:/data:ro
```

--------------------------------

### Migrate Go App to DHI with Docker

Source: https://docs.docker.com/llms

This guide covers migrating a Go application to Docker Hub Images (DHI). It provides steps and examples for containerizing your Go application for DHI.

```Dockerfile
# Example Dockerfile for migrating a Go app to DHI
FROM golang:1.19-alpine AS builder
WORKDIR /app
COPY go.mod go.sum ./ 
RUN go mod download
COPY *.go ./ 
RUN CGO_ENABLED=0 GOOS=linux go build -o main .

FROM alpine:latest
WORKDIR /root/
COPY --from=builder /app/main .
CMD ["./main"]
```

--------------------------------

### Docker Daemon Configuration Example (JSON)

Source: https://docs.docker.com/reference/cli/dockerd

This JSON object represents a full example of the configuration options available for the Docker daemon on Linux systems. It covers various aspects such as networking, logging, storage, and security. Ensure that options set here do not conflict with daemon startup flags.

```json
{
  "allow-direct-routing": false,
  "authorization-plugins": [],
  "bip": "",
  "bip6": "",
  "bridge": "",
  "bridge-accept-fwmark": "",
  "builder": {
    "gc": {
      "enabled": true,
      "defaultReservedSpace": "10GB",
      "policy": [
        { "maxUsedSpace": "512MB", "keepDuration": "48h", "filter": [ "type=source.local" ] },
        { "reservedSpace": "10GB", "maxUsedSpace": "100GB", "keepDuration": "1440h" },
        { "reservedSpace": "50GB", "minFreeSpace": "20GB", "maxUsedSpace": "200GB", "all": true }
      ]
    }
  },
  "cgroup-parent": "",
  "containerd": "/run/containerd/containerd.sock",
  "containerd-namespace": "docker",
  "containerd-plugins-namespace": "docker-plugins",
  "data-root": "",
  "debug": true,
  "default-address-pools": [
    {
      "base": "172.30.0.0/16",
      "size": 24
    },
    {
      "base": "172.31.0.0/16",
      "size": 24
    }
  ],
  "default-cgroupns-mode": "private",
  "default-gateway": "",
  "default-gateway-v6": "",
  "default-network-opts": {},
  "default-runtime": "runc",
  "default-shm-size": "64M",
  "default-ulimits": {
    "nofile": {
      "Hard": 64000,
      "Name": "nofile",
      "Soft": 64000
    }
  },
  "dns": [],
  "dns-opts": [],
  "dns-search": [],
  "exec-opts": [],
  "exec-root": "",
  "experimental": false,
  "features": {
    "cdi": true,
    "containerd-snapshotter": true
  },
  "firewall-backend": "",
  "fixed-cidr": "",
  "fixed-cidr-v6": "",
  "group": "",
  "host-gateway-ip": "",
  "hosts": [],
  "proxies": {
    "http-proxy": "http://proxy.example.com:80",
    "https-proxy": "https://proxy.example.com:443",
    "no-proxy": "*.test.example.com,.example.org"
  },
  "icc": false,
  "init": false,
  "init-path": "/usr/libexec/docker-init",
  "insecure-registries": [],
  "ip": "0.0.0.0",
  "ip-forward": false,
  "ip-masq": false,
  "iptables": false,
  "ip6tables": false,
  "ipv6": false,
  "labels": [],
  "live-restore": true,
  "log-driver": "json-file",
  "log-format": "text",
  "log-level": "",
  "log-opts": {
    "cache-disabled": "false",
    "cache-max-file": "5",
    "cache-max-size": "20m",
    "cache-compress": "true",
    "env": "os,customer",
    "labels": "somelabel",
    "max-file": "5",
    "max-size": "10m"
  },
  "max-concurrent-downloads": 3,
  "max-concurrent-uploads": 5,
  "max-download-attempts": 5,
  "mtu": 0,
  "no-new-privileges": false,
  "node-generic-resources": [
    "NVIDIA-GPU=UUID1",
    "NVIDIA-GPU=UUID2"
  ],
  "pidfile": "",
  "raw-logs": false,
  "registry-mirrors": [],
  "runtimes": {
    "cc-runtime": {
      "path": "/usr/bin/cc-runtime"
    },
    "custom": {
      "path": "/usr/local/bin/my-runc-replacement",
      "runtimeArgs": [
        "--debug"
      ]
    }
  },
  "seccomp-profile": "",
  "selinux-enabled": false,
  "shutdown-timeout": 15,
  "storage-driver": "",
  "storage-opts": [],
  "swarm-default-advertise-addr": "",
  "tls": true,
  "tlscacert": "",
  "tlscert": "",
  "tlskey": "",
  "tlsverify": true,
  "userland-proxy": false,
  "userland-proxy-path": "/usr/libexec/docker-proxy",
  "userns-remap": ""
}
```

--------------------------------

### Format Docker Service List with Go Template

Source: https://docs.docker.com/reference/cli/docker/service/ls

This example demonstrates how to use the `--format` option with a Go template to display specific service details (ID, Mode, Replicas) separated by a colon. It does not include table headers.

```console
$ docker service ls --format "{{.ID}}: {{.Mode}} {{.Replicas}}"

0zmvwuiu3vue: replicated 10/10
fm6uf97exkul: global 5/5
```

--------------------------------

### Run Docker Compose in Detached Mode and List Services

Source: https://docs.docker.com/compose/gettingstarted

Starts Docker Compose services in the background using the detached flag (`-d`) and then lists the currently running services. This is useful for long-running applications where you don't need to attach to the container's output directly.

```console
$ docker compose up -d

Starting composetest_redis_1...
Starting composetest_web_1...

$ docker compose ps

         Name                      Command               State           Ports         
  -------------------------------------------------------------------------------------
  composetest_redis_1   docker-entrypoint.sh redis ...   Up      6379/tcp              
  composetest_web_1     flask run                        Up      0.0.0.0:8000->5000/tcp
```

--------------------------------

### Clone Example Application Repository

Source: https://docs.docker.com/guides/golang/develop

Command to clone the 'docker-gs-ping-dev' repository, which contains the example application code. This is recommended for setting up the application that will interact with the configured database.

```git
git clone https://github.com/docker/docker-gs-ping-dev.git
```

--------------------------------

### Start Frontend Development Server (Console)

Source: https://docs.docker.com/guides/localstack

This console command starts the frontend development server, typically using Vite. It will provide a local URL to access the running application in the browser.

```bash
$ npm run dev
```

--------------------------------

### Install Node.js via NVM

Source: https://docs.docker.com/guides/frameworks/laravel/development-setup

Installs Node Version Manager (NVM) and the specified Node.js version for the 'www' user. This allows for flexible management of Node.js versions within the container.

```dockerfile
USER www

RUN export NVM_DIR="$HOME/.nvm" && \
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.0/install.sh | bash && \
    [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" && \
    nvm install ${NODE_VERSION} && \
    nvm alias default ${NODE_VERSION} && \
    nvm use default
```

--------------------------------

### Start Docker Compose Application

Source: https://docs.docker.com/guides/python/develop

This command builds the Docker images defined in the `compose.yaml` file and starts the services. The `--build` flag ensures that any changes to the Dockerfiles or build contexts are incorporated before starting the containers.

```bash
docker compose up --build

```

--------------------------------

### Run Docker Image with Default Command

Source: https://docs.docker.com/develop/security-best-practices

Demonstrates how to run a Docker container that has an ENTRYPOINT and CMD defined, resulting in the default command (help in this case) being executed.

```shell
$ docker run s3cmd
```

--------------------------------

### Run a container using Docker API

Source: https://docs.docker.com/reference/api/engine/sdk

Demonstrates how to pull an image, create, start, wait for, and retrieve logs from a container using the Docker API. This example requires the Docker client library for Go and handles API errors.

```go
package main

import (
	"context"
	"io"
	"os"

	"github.com/moby/moby/api/pkg/stdcopy"
	"github.com/moby/moby/api/types/container"
	"github.com/moby/moby/client"
)

func main() {
	ctx := context.Background()
	apiClient, err := client.New(client.FromEnv)
	if err != nil {
		panic(err)
	}
	defer apiClient.Close()

	reader, err := apiClient.ImagePull(ctx, "docker.io/library/alpine", client.ImagePullOptions{})
	if err != nil {
		panic(err)
	}
	io.Copy(os.Stdout, reader)

	resp, err := apiClient.ContainerCreate(ctx, client.ContainerCreateOptions{
		Image: "alpine",
		Config: &container.Config{
			Cmd: []string{"echo", "hello world"},
		},
	})
	if err != nil {
		panic(err)
	}

	if _, err := apiClient.ContainerStart(ctx, resp.ID, client.ContainerStartOptions{}); err != nil {
		panic(err)
	}

	wait := apiClient.ContainerWait(ctx, resp.ID, client.ContainerWaitOptions{})
	select {
	case err := <-wait.Error:
		if err != nil {
			panic(err)
		}
	case <-wait.Result:
	}

	out, err := apiClient.ContainerLogs(ctx, resp.ID, client.ContainerLogsOptions{ShowStdout: true})
	if err != nil {
		panic(err)
	}

	stdcopy.StdCopy(os.Stdout, os.Stderr, out)
}
```

--------------------------------

### Docker Build Process Output (Initial)

Source: https://docs.docker.com/get-started/docker-concepts/building-images/using-the-build-cache

Example output of the initial Docker build process, showing the time taken for each step. This illustrates the duration of the first build, including dependency installation.

```console
[+] Building 20.0s (10/10) FINISHED
```

--------------------------------

### Create Docker Bind Mount

Source: https://docs.docker.com/engine/containers/run

Demonstrates how to create a bind mount using the `docker run` command with the `--mount` flag. It specifies the type as 'bind' and provides source and target paths. The source is the host path, and the target is the container's mount destination. Bind mounts are read-write by default.

```console
$ docker run -it --mount type=bind,source=[PATH],target=[PATH] busybox
```

```console
$ docker run -it --mount type=bind,source=.,target=/foo busybox
/ # echo "hello from container" > /foo/hello.txt
/ # exit
$ cat hello.txt
hello from container
```

--------------------------------

### Multi-stage Dockerfile Build Example

Source: https://docs.docker.com/engine/reference/builder

This Dockerfile demonstrates a multi-stage build. It first builds an executable 'hello' in an 'alpine' stage with clang, then copies the compiled binary to a 'scratch' stage.

```dockerfile
# syntax=docker/dockerfile:1
FROM alpine AS build
COPY . .
RUN apk add clang
RUN clang -o /hello hello.c

FROM scratch
COPY --from=build /hello /

```

--------------------------------

### Run the hello-world Docker image

Source: https://docs.docker.com/engine/install/ubuntu

Executes the 'hello-world' Docker image to confirm that Docker Engine is installed correctly and can pull and run images.

```console
$ sudo docker run hello-world
```

--------------------------------

### Complex Docker Build Command

Source: https://docs.docker.com/build/bake/introduction

This example illustrates a more complex `docker build` command, including build arguments, disabling cache, specifying multiple platforms, and a Dockerfile. It highlights the limitations of managing such complexity with CLI flags.

```console
$ docker build \
  -f Dockerfile \
  -t myapp:latest \
  --build-arg foo=bar \
  --no-cache \
  --platform linux/amd64,linux/arm64 \
  .
```

--------------------------------

### Clone Node.js Sample Project

Source: https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-a-registry

Clones the 'helloworld-demo-node' repository from GitHub, which contains a pre-built Dockerfile for building a Docker image.

```bash
git clone https://github.com/dockersamples/helloworld-demo-node
```

--------------------------------

### Check Docker service status

Source: https://docs.docker.com/engine/install/raspberry-pi-os

Verifies if the Docker service is running. This command is useful after installation or to troubleshoot issues. If the service is not active, a manual start command is also provided.

```console
sudo systemctl status docker
```

```console
sudo systemctl start docker
```

--------------------------------

### Start Detached Interactive Container on Overlay Network

Source: https://docs.docker.com/engine/network/drivers/overlay

Starts a detached, interactive Alpine Linux container named 'alpine2' and connects it to the 'test-net' overlay network. This is useful for running services that need to be accessible. Requires the 'test-net' network to exist and Docker installed.

```console
$ docker run -dit --name alpine2 --network test-net alpine
fb635f5ece59563e7b8b99556f816d24e6949a5f6a5b1fbd92ca244db17a4342
```

--------------------------------

### Install Docker Extension API Client

Source: https://docs.docker.com/extensions/extensions-sdk/build/frontend-extension-tutorial

Installs the necessary library to interact with Docker Desktop's Extension APIs. This is the first step for any extension that needs to perform actions with Docker.

```bash
npm install @docker/extension-api-client
```

--------------------------------

### Run Nginx with Read-Only Volume (-v)

Source: https://docs.docker.com/storage/volumes

Starts an Nginx container with a named volume mounted as read-only using the `-v` flag. The `ro` option is appended to the volume path. This achieves the same result as the `--mount` example.

```bash
$ docker run -d \
  --name=nginxtest \
  -v nginx-vol:/usr/share/nginx/html:ro \
  nginx:latest

```

--------------------------------

### Build Log Output for Bind Mount Example

Source: https://docs.docker.com/build/cache/optimize

Provides the build log output for the Dockerfile example demonstrating bind mounts. It shows the execution of 'touch' and two 'ls' commands, highlighting the difference in output when a bind mount is active.

```plaintext
#8 [stage-0 3/5] RUN touch foo.txt
#8 DONE 0.1s

#9 [stage-0 4/5] RUN --mount=target=. ls -1
#9 0.040 Dockerfile
#9 DONE 0.0s

#10 [stage-0 5/5] RUN ls -1
#10 0.046 foo.txt
#10 DONE 0.1s
```

--------------------------------

### Initialize Project with Docker Files (docker init)

Source: https://docs.docker.com/engine/reference/commandline/init

The 'docker init' command creates essential Docker configuration files (.dockerignore, Dockerfile, compose.yaml, README.Docker.md) for a project. It offers templates for various application platforms and prompts the user for configuration details. Requires Docker Desktop 4.27 or later.

```bash
docker init
```

--------------------------------

### Configure gVisor Runtime with containerd Shim Options

Source: https://docs.docker.com/reference/cli/dockerd

This JSON example demonstrates configuring the gVisor runtime using its containerd shim. It specifies the 'runtimeType' and provides 'options' for TypeUrl and ConfigPath, enabling custom configurations for the shim.

```json
{
  "runtimes": {
    "gvisor": {
      "runtimeType": "io.containerd.runsc.v1",
      "options": {
        "TypeUrl": "io.containerd.runsc.v1.options",
        "ConfigPath": "/etc/containerd/runsc.toml"
      }
    }
  }
}
```

--------------------------------

### Docker Registry Token Request Example

Source: https://docs.docker.com/reference/api/registry/auth

This example shows the HTTP GET request a Docker client makes to the token server to obtain an authentication token. It includes the URL with parameters for service and scope, and explains the authentication process and access control checks performed by the token server.

```text
https://auth.docker.io/token?service=registry.docker.io&scope=repository:samalba/my-app:pull,push
```

--------------------------------

### Initialize Python Project and Set Up Virtual Environment

Source: https://docs.docker.com/guides/github-sonarqube-sandbox/workflow

Creates a new project directory and sets up a Python virtual environment using venv. This isolates project dependencies and ensures a clean development environment. It also installs required Python packages like e2b and python-dotenv.

```bash
mkdir github-sonarqube-workflow
cd github-sonarqube-workflow
```

```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

```bash
pip install e2b python-dotenv
```

--------------------------------

### Bash Helper Script for Docker ENTRYPOINT

Source: https://docs.docker.com/develop/develop-images/dockerfile_best-practices

Provides an example of a Bash script used as an ENTRYPOINT in a Docker container. The script handles initialization tasks, such as setting permissions and initializing a database, before executing the main command.

```bash
#!/bin/bash
set -e

if [ "$1" = 'postgres' ]; then
    chown -R postgres "$PGDATA"

    if [ -z "$(ls -A "$PGDATA")" ]; then
        gosu postgres initdb
    fi

    exec gosu postgres "$@"
fi

exec "$@"
```

--------------------------------

### Install Docker Compose Plugin on Linux

Source: https://docs.docker.com/llms

Step-by-step instructions for installing the Docker Compose plugin on Linux. This can be done using a package repository for easier updates or manually by downloading the binary. Ensure you have the necessary permissions to install system-wide packages.

```bash
# Using a package repository (example for Debian/Ubuntu)
apt-get update
apt-get install -y docker-compose-plugin

# Manual installation
LATEST_COMPOSE_VERSION=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d"\"" -f4)
curl -L "https://github.com/docker/compose/releases/download/${LATEST_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

--------------------------------

### Docker Model Runner Examples

Source: https://docs.docker.com/llms

Example projects and Continuous Integration/Continuous Deployment (CI/CD) workflows demonstrating the use of Docker Model Runner (DMR). These examples showcase practical applications and integration patterns.

```dockerfile
FROM docker.io/library/ubuntu:latest
RUN apt-get update && apt-get install -y python3
COPY . /app
WORKDIR /app
CMD ["python3", "app.py"]
```

--------------------------------

### Dockerfile for Local Directory Context

Source: https://docs.docker.com/build/building/context

Provides an example Dockerfile that utilizes files from a local directory build context. It copies package files, runs npm install, and then copies source files.

```dockerfile
#syntax=docker/dockerfile:1
FROM node:latest
WORKDIR /src
COPY package.json package-lock.json .
RUN npm ci
COPY index.ts src .

```

--------------------------------

### Using Here-Documents with RUN for Multi-line Scripts (Bash)

Source: https://docs.docker.com/reference/dockerfile

Illustrates how to use here-documents (delimited by EOT) with the RUN instruction to execute multi-line scripts within a Dockerfile. This example uses bash and installs vim.

```dockerfile
# syntax=docker/dockerfile:1
FROM debian
RUN <<EOT bash
  set -ex
  apt-get update
  apt-get install -y vim
EOT
```

--------------------------------

### Run Container with Specific Logging Driver (CLI)

Source: https://docs.docker.com/engine/logging/configure

Starts a new container with a logging driver different from the daemon's default. This example uses the `docker run` command to start an Alpine container with the 'none' logging driver.

```bash
$ docker run -it --log-driver none alpine ash
```

--------------------------------

### Docker Desktop Installer Flags: Backend Selection

Source: https://docs.docker.com/desktop/setup/install/windows-install

Illustrates how to specify the backend for Docker Desktop during installation. Options include Hyper-V, Windows containers, or WSL 2. The default is WSL 2.

```console
"Docker Desktop Installer.exe" install --backend=wsl-2
```

--------------------------------

### Windows Docker Volume Mount Example

Source: https://docs.docker.com/reference/cli/docker/container/run

Provides examples of mounting volumes on Windows using Windows-style path semantics. It also highlights limitations and failure cases for Windows-based containers regarding volume destinations and source paths.

```powershell
PS C:\> docker run -v c:\foo:c:\dest microsoft/nanoserver cmd /s /c type c:\dest\somefile.txt
Contents of file

PS C:\> docker run -v c:\foo:d: microsoft/nanoserver cmd /s /c type d:\somefile.txt
Contents of file
```

--------------------------------

### Uninstall Docker Compose

Source: https://docs.docker.com/llms

Guide on how to uninstall Docker Compose from your system. This typically involves removing the installed binaries or packages. The exact commands depend on how Docker Compose was initially installed (e.g., package manager, pip, standalone binary).

```bash
# If installed via package manager (e.g., apt)
sudo apt-get remove docker-compose

# If installed as a standalone binary
sudo rm /usr/local/bin/docker-compose
```

--------------------------------

### Dockerfile for AI Application Build (Dockerfile)

Source: https://docs.docker.com/guides/agentic-ai

Builds the Docker image for the AI application. It starts from a Python 3.13 slim base image, installs system dependencies using `uv`, copies application code, and compiles it. It also defines an entrypoint script that handles API key configuration (OpenAI or Docker Model Runner) and starts the ADK web server.

```dockerfile
# Use Python 3.11 slim image as base
FROM python:3.13-slim
ENV PYTHONUNBUFFERED=1

RUN pip install uv

WORKDIR /app
# Install system dependencies
COPY pyproject.toml uv.lock ./
RUN --mount=type=cache,target=/root/.cache/uv \
    UV_COMPILE_BYTECODE=1 UV_LINK_MODE=copy \
    uv pip install --system .
# Copy application code
COPY agents/ ./agents/
RUN python -m compileall -q .

COPY <<EOF /entrypoint.sh
#!/bin/sh
set -e

if test -f /run/secrets/openai-api-key; then
    export OPENAI_API_KEY=$(cat /run/secrets/openai-api-key)
fi

if test -n "${OPENAI_API_KEY}"; then
    echo "Using OpenAI with ${OPENAI_MODEL_NAME}"
else
    echo "Using Docker Model Runner with ${MODEL_RUNNER_MODEL}"
    export OPENAI_BASE_URL=${MODEL_RUNNER_URL}
    export OPENAI_MODEL_NAME=openai/${MODEL_RUNNER_MODEL}
    export OPENAI_API_KEY=cannot_be_empty
fi
exec adk web --host 0.0.0.0 --port 8080 --log_level DEBUG
EOF
RUN chmod +x /entrypoint.sh

```

--------------------------------

### Commit Docker Container to Image using Go, Python, and HTTP

Source: https://docs.docker.com/reference/api/engine/sdk/examples

Illustrates how to commit the state of a running Docker container into a new image. Examples are provided for Go, Python, and HTTP requests. The Go and Python examples show the programmatic approach, while the HTTP example uses `curl` to interact with the Docker daemon.

```go
package main

import (
	"context"
	"fmt"

	"github.com/moby/moby/api/types/container"
	"github.com/moby/moby/client"
)

func main() {
	ctx := context.Background()
	apiClient, err := client.New(client.FromEnv)
	if err != nil {
		panic(err)
	}
	defer apiClient.Close()

	createResp, err := apiClient.ContainerCreate(ctx, client.ContainerCreateOptions{
		Config: &container.Config{
			Cmd: []string{"touch", "/helloworld"},
		},
		Image: "alpine",
	})
	if err != nil {
		panic(err)
	}

	if _, err := apiClient.ContainerStart(ctx, createResp.ID, client.ContainerStartOptions{}); err != nil {
		panic(err)
	}

	wait := apiClient.ContainerWait(ctx, createResp.ID, client.ContainerWaitOptions{})
	select {
	case err := <-wait.Error:
		if err != nil {
			panic(err)
		}
	case <-wait.Result:
	}

	commitResp, err := apiClient.ContainerCommit(ctx, createResp.ID, client.ContainerCommitOptions{Reference: "helloworld"})
	if err != nil {
		panic(err)
	}

	fmt.Println(commitResp.ID)
}
```

```python
import docker
client = docker.from_env()
container = client.containers.run("alpine", ["touch", "/helloworld"], detach=True)
container.wait()
image = container.commit("helloworld")
print(image.id)
```

```http
$ docker run -d alpine touch /helloworld
0888269a9d584f0fa8fc96b3c0d8d57969ceea3a64acf47cd34eebb4744dbc52
$ curl --unix-socket /var/run/docker.sock\
  -X POST "http://localhost/v1.53/commit?container=0888269a9d&repo=helloworld"
{"Id":"sha256:6c86a5cd4b87f2771648ce619e319f3e508394b5bfc2cdbd2d60f59d52acda6c"}
```

--------------------------------

### Run MCP Gateway

Source: https://docs.docker.com/ai/mcp-catalog-and-toolkit/get-started

This command runs the MCP gateway, which is used to manually connect MCP clients to the toolkit over stdio.

```plaintext
docker mcp gateway run
```

--------------------------------

### Pull Docker Image using Go, Python, and HTTP

Source: https://docs.docker.com/reference/api/engine/sdk/examples

Demonstrates how to pull a Docker image (e.g., 'alpine') using the Docker API. This includes examples for Go, Python, and direct HTTP requests. The HTTP example shows the raw API call and its JSON output.

```go
package main

import (
	"context"
	"io"
	"os"

	"github.com/moby/moby/client"
)

func main() {
	ctx := context.Background()
	apiClient, err := client.New(client.FromEnv)
	if err != nil {
		panic(err)
	}
	defer apiClient.Close()

	out, err := apiClient.ImagePull(ctx, "alpine", client.ImagePullOptions{})
	if err != nil {
		panic(err)
	}

	defer out.Close()

	io.Copy(os.Stdout, out)
}
```

```python
import docker
client = docker.from_env()
image = client.images.pull("alpine")
print(image.id)
```

```http
$ curl --unix-socket /var/run/docker.sock \
  -X POST "http://localhost/v1.53/images/create?fromImage=alpine"
{"status":"Pulling from library/alpine","id":"3.1"}
{"status":"Pulling fs layer","progressDetail":{},"id":"8f13703509f7"}
{"status":"Downloading","progressDetail":{"current":32768,"total":2244027},"progress":"[\u003e                                                  ] 32.77 kB/2.244 MB","id":"8f13703509f7"}
...
```

--------------------------------

### Initialize Node.js Project and Install Express

Source: https://docs.docker.com/guides/genai-claude-code-mcp/claude-code-mcp-guide

This sequence of commands sets up a new Node.js project within an 'app' directory. It initializes npm, installs the 'express' package, and prepares the project for a basic web server setup. This is a prerequisite for generating a Docker Compose file for a Node.js application.

```bash
mkdir app
cd app
npm init -y
npm install express
```

--------------------------------

### Basic Docker Desktop Installation on macOS

Source: https://docs.docker.com/desktop/setup/install/mac-install

This snippet demonstrates the fundamental commands to attach a Docker disk image, run the installer, and detach the disk image. It assumes the Docker.dmg file has been downloaded.

```console
sudo hdiutil attach Docker.dmg
sudo /Volumes/Docker/Docker.app/Contents/MacOS/install
sudo hdiutil detach /Volumes/Docker
```

--------------------------------

### Fetch and Install Zscaler Root Certificate from Artifact Repository

Source: https://docs.docker.com/guides/zscaler

This Dockerfile example shows how to fetch the Zscaler root certificate directly from an artifact repository using the ADD instruction with a checksum for verification. It then installs the certificate into the Debian image's trust store.

```dockerfile
FROM debian:bookworm
ADD --checksum=sha256:24454f830cdb571e2c4ad15481119c43b3cafd48dd869a9b2945d1036d1dc68d \
    https://artifacts.example/certs/zscaler-root-ca.crt /usr/local/share/ca-certificates/zscaler-root-ca.crt
RUN apt-get update && \
    apt-get install -y ca-certificates && \
    update-ca-certificates
```

--------------------------------

### Clone Sample Application Repository

Source: https://docs.docker.com/get-started/docker-concepts/building-images/build-tag-and-publish-an-image

Clone the sample application repository using Git to follow along with the hands-on guide. This provides the necessary files for building and pushing a Docker image.

```console
$ git clone https://github.com/docker/getting-started-todo-app
```

--------------------------------

### Expose All GPUs to Container

Source: https://docs.docker.com/config/containers/resource_constraints

Starts a Docker container and makes all available NVIDIA GPUs accessible within it. This is achieved by using the `--gpus all` flag. The example command then runs `nvidia-smi` inside the container to display GPU information.

```bash
docker run -it --rm --gpus all ubuntu nvidia-smi
```

--------------------------------

### vLLM Setup and Usage

Source: https://docs.docker.com/ai/model-runner/inference-engines

Instructions for installing and using the vLLM inference engine with Docker Model Runner, focusing on its high-throughput capabilities for production environments.

```APIDOC
## Installing vLLM Backend (Linux)

### Description
Installs the vLLM inference engine for Docker Model Runner on Linux systems with CUDA-enabled NVIDIA GPUs.

### Method
CLI Command

### Endpoint
N/A

### Parameters
#### Command Line Arguments
- **--backend** (string) - Required - Specifies the backend to install. Set to `vllm`.
- **--gpu** (string) - Required - Specifies the GPU type. Set to `cuda` for NVIDIA GPUs.

### Request Example
```bash
docker model install-runner --backend vllm --gpu cuda
```

### Response
#### Success Response
Indicates successful installation and that vLLM is running alongside other available backends.

#### Response Example
```text
Docker Model Runner is running

Status:
llama.cpp: running llama.cpp version: c22473b
vllm: running vllm version: 0.11.0
```

## Installing vLLM Backend (Windows with WSL2)

### Description
Installs the vLLM inference engine for Docker Model Runner on Windows using WSL2, requiring Docker Desktop and an NVIDIA GPU.

### Method
CLI Command

### Endpoint
N/A

### Prerequisites
- Docker Desktop 4.54 or later
- NVIDIA GPU with updated drivers
- WSL2 enabled

### Parameters
#### Command Line Arguments
- **--backend** (string) - Required - Specifies the backend to install. Set to `vllm`.
- **--gpu** (string) - Required - Specifies the GPU type. Set to `cuda` for NVIDIA GPUs.

### Request Example
```bash
docker model install-runner --backend vllm --gpu cuda
```

### Response
#### Success Response
Confirms the installation of the vLLM backend.

#### Response Example
(Output similar to Linux installation, confirming vLLM status)

## Running Models with vLLM

### Description
Demonstrates how to run models specifically using the vLLM inference engine, often identified by a `-vllm` suffix in their Docker Hub tag.

### Method
CLI Command

### Endpoint
N/A

### Parameters
#### Command Line Arguments
- **model_name** (string) - Required - The name or tag of the model to run (e.g., `ai/smollm2-vllm`).
- **--backend** (string) - Optional - Explicitly specifies the backend to use. Set to `vllm`.

### Request Example 1 (Using vLLM tagged model)
```bash
docker model run ai/smollm2-vllm
```

### Request Example 2 (Explicitly specifying vLLM backend)
```bash
docker model run ai/model --backend vllm
```

### Response
#### Success Response
Indicates the model is running successfully using the vLLM engine.

#### Response Example
(Output showing model loading and readiness for inference)
```

--------------------------------

### Mount Block Device to Container (Docker)

Source: https://docs.docker.com/engine/storage/volumes

This example demonstrates mounting a block device (like a loop device created from a file) as a volume within a Docker container. It uses the --mount flag with specific volume options to achieve this. The container's filesystem will see the mounted device at the specified destination path.

```console
$ docker run \
  --mount='type=volume,dst=/external-drive,volume-driver=local,volume-opt=device=/dev/loop5,volume-opt=type=ext4'
```

--------------------------------

### Troubleshoot systemd Detection with dockerd-rootless-setuptool.sh

Source: https://docs.docker.com/engine/security/rootless/troubleshoot

This example shows the output when `dockerd-rootless-setuptool.sh install` fails to detect systemd properly, often occurring when switching users via `sudo su`. It suggests using `machinectl` for users that cannot be logged in directly.

```console
$ dockerd-rootless-setuptool.sh install
[INFO] systemd not detected, dockerd-rootless.sh needs to be started manually:
...
```

--------------------------------

### Gin Application Setup with Metrics Middleware in Go

Source: https://docs.docker.com/guides/go-prometheus-monitoring/application

This Go code sets up a Gin web server. It defines routes for `/health`, `/v1/users`, and `/metrics`. Crucially, it includes a `RequestMetricsMiddleware` that intercepts all incoming requests to record metrics like path and status code using the previously defined Prometheus counters. The `/metrics` endpoint is specifically configured to serve these metrics using a custom Prometheus registry.

```go
func main() {
	router := gin.Default()

	// Register /metrics before middleware
	router.GET("/metrics", PrometheusHandler())
	
	router.Use(RequestMetricsMiddleware())
	router.GET("/health", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "Up and running!",
		})
	})
	router.GET("/v1/users", func(c *gin.Context) {
		c.JSON(200, gin.H{
			"message": "Hello from /v1/users",
		})
	})

	router.Run(":8000")
}

// Custom metrics handler with custom registry
func PrometheusHandler() gin.HandlerFunc {
	h := promhttp.HandlerFor(customRegistry, promhttp.HandlerOpts{})
	return func(c *gin.Context) {
		h.ServeHTTP(c.Writer, c.Request)
	}
}

// Middleware to record incoming requests metrics
func RequestMetricsMiddleware() gin.HandlerFunc {
	return func(c *gin.Context) {
		path := c.Request.URL.Path
		c.Next()
		status := c.Writer.Status()
		if status < 400 {
			HttpRequestTotal.WithLabelValues(path, strconv.Itoa(status)).Inc()
		} else {
			HttpRequestErrorTotal.WithLabelValues(path, strconv.Itoa(status)).Inc()
		}
	}
}
```

--------------------------------

### BuildKit Daemon Configuration Example (TOML)

Source: https://docs.docker.com/build/buildkit/toml-configuration

A complete example of the buildkitd.toml configuration file. This file sets global daemon options and configures specific sections for logging, DNS, gRPC, OpenTelemetry, and CDI. Note that some options are for edge cases.

```toml
# debug enables additional debug logging
debug = true
# trace enables additional trace logging (very verbose, with potential performance impacts)
trace = true
# root is where all buildkit state is stored.
root = "/var/lib/buildkit"
# insecure-entitlements allows insecure entitlements, disabled by default.
insecure-entitlements = [ "network.host", "security.insecure", "device" ]
# provenanceEnvDir is the directory where extra config is loaded that is added
# to the provenance of builds:
# slsa v0.2: invocation.environment.*
# slsa v1: buildDefinition.internalParameters.*
provenanceEnvDir = "/etc/buildkit/provenance.d"

[log]
  # log formatter: json or text
  format = "text"

[dns]
  nameservers=["1.1.1.1","8.8.8.8"]
  options=["edns0"]
  searchDomains=["example.com"]

[grpc]
  address = [ "tcp://0.0.0.0:1234" ]
  # debugAddress is address for attaching go profiles and debuggers.
  debugAddress = "0.0.0.0:6060"
  uid = 0
  gid = 0
  [grpc.tls]
    cert = "/etc/buildkit/tls.crt"
    key = "/etc/buildkit/tls.key"
    ca = "/etc/buildkit/tlsca.crt"

[otel]
  # OTEL collector trace socket path
  socketPath = "/run/buildkit/otel-grpc.sock"

[cdi]
  # Disables support of the Container Device Interface (CDI).
  disabled = true
  # List of directories to scan for CDI spec files. For more details about CDI
  # specification, please refer to https://github.com/cncf-tags/container-device-interface/blob/main/SPEC.md#cdi-json-specification
  specDirs = ["/etc/cdi", "/var/run/cdi", "/etc/buildkit/cdi"]

```

--------------------------------

### Inspecting SBOMs with Docker Buildx Imagetools

Source: https://docs.docker.com/build/metadata/attestations/sbom

These commands show how to inspect SBOMs generated by Docker BuildKit using `docker buildx imagetools inspect`. The `--format` option allows for custom output formatting. The first example retrieves the raw SPDX JSON content of an SBOM, while the second example demonstrates listing all installed packages and their version identifiers within the SBOM.

```bash
docker buildx imagetools inspect <namespace>/<image>:<version> \
    --format "{{ json .SBOM.SPDX }}"
```

```bash
docker buildx imagetools inspect <namespace>/<image>:<version> \
    --format "{{ range .SBOM.SPDX.packages }}{{ .name }}@{{ .versionInfo }}{{ println }}{{ end }}"
```

--------------------------------

### Initialize Docker Configuration Files using docker init

Source: https://docs.docker.com/guides/nodejs/containerize

The `docker init` command interactively scaffolds essential Docker configuration files for your project, including Dockerfile, .dockerignore, compose.yaml, and README.Docker.md. It guides you through setup questions to generate sensible defaults.

```bash
cd docker-nodejs-sample
docker init
```

--------------------------------

### Build Rust Docker Images

Source: https://docs.docker.com/llms

Learn the fundamentals of building your first Rust Docker image. This guide covers the basic steps to containerize a Rust application.

```Dockerfile
# Example Dockerfile for building a Rust image
FROM rust:latest

WORKDIR /app

COPY . .

RUN cargo build --release

# For a minimal image, you might copy only the compiled binary
# FROM alpine:latest
# COPY --from=0 /app/target/release/<your-app-binary> /usr/local/bin/<your-app-binary>
```

--------------------------------

### Docker Sample Applications

Source: https://docs.docker.com/llms

A collection of sample applications demonstrating various use cases with Docker.

```APIDOC
## Docker Sample Applications

### Description
This section lists various sample applications and projects that showcase how to use Docker for different technologies and use cases.

### Method
GET

### Endpoints
- /reference/samples/agentic-ai/
- /reference/samples/ai-ml/
- /reference/samples/angular/
- /reference/samples/cloudflared/
- /reference/samples/django/
- /reference/samples/dotnet/
- /reference/samples/elasticsearch/
- /reference/samples/express/
- /reference/samples/fastapi/
- /reference/samples/flask/
- /reference/samples/gitea/
- /reference/samples/go/
- /reference/samples/java/
- /reference/samples/javascript/
- /reference/samples/mariadb/
- /reference/samples/minecraft/
- /reference/samples/mongodb/
- /reference/samples/ms-sql/
- /reference/samples/mysql/
- /reference/samples/nextcloud/
- /reference/samples/nginx/

### Parameters
None for general overview.

### Request Example
None

### Response
#### Success Response (200)
- **documentation** (string) - Information and links to the sample application code and setup instructions.

#### Response Example
```json
{
  "documentation": "..."
}
```
```

--------------------------------

### Auto-starting Profiles for Targeted Services in Docker Compose

Source: https://docs.docker.com/compose/how-tos/profiles

This example illustrates how Docker Compose automatically starts a service's profile when the service itself is explicitly targeted, even if the profile isn't otherwise active. This is useful for running one-off tasks or debugging tools, ensuring dependencies are also started.

```yaml
services:
  backend:
    image: backend

  db:
    image: mysql

  db-migrations:
    image: backend
    command: myapp migrate
    depends_on:
      - db
    profiles:
      - tools
```

--------------------------------

### Push Docker Image to Docker Hub

Source: https://docs.docker.com/docker-hub/quickstart

Pushes the locally built and tagged Docker image to Docker Hub. Ensure you are signed in to Docker Hub via the command line or Docker Desktop. This command makes your image available to others or for deployment.

```bash
$ docker push <YOUR-USERNAME>/nginx-custom
```

--------------------------------

### Set up Docker's apt repository on Ubuntu

Source: https://docs.docker.com/engine/install/ubuntu

This snippet configures the Docker apt repository on Ubuntu systems. It involves updating the package list, installing necessary prerequisites, adding Docker's GPG key, and defining the repository source in apt's configuration.

```bash
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```

--------------------------------

### Run a Docker Container using Go, Python, and HTTP API

Source: https://docs.docker.com/reference/api/engine/sdk/examples

This snippet shows how to run a Docker container that executes 'echo hello world' using the Alpine image. It demonstrates the equivalent of the 'docker run alpine echo hello world' command in Go, Python, and via HTTP requests using curl.

```go
package main

import (
	"context"
	"io"
	"os"

	"github.com/moby/moby/api/pkg/stdcopy"
	"github.com/moby/moby/api/types/container"
	"github.com/moby/moby/client"
)

func main() {
	ctx := context.Background()
	apiClient, err := client.New(client.FromEnv)
	if err != nil {
		panic(err)
	}
	defer apiClient.Close()

	reader, err := apiClient.ImagePull(ctx, "docker.io/library/alpine", client.ImagePullOptions{})
	if err != nil {
		panic(err)
	}

	defer reader.Close()
	// cli.ImagePull is asynchronous.
	// The reader needs to be read completely for the pull operation to complete.
	// If stdout is not required, consider using io.Discard instead of os.Stdout.
	io.Copy(os.Stdout, reader)

	resp, err := apiClient.ContainerCreate(ctx, client.ContainerCreateOptions{
		Config: &container.Config{
			Cmd: []string{"echo", "hello world"},
			Tty: false,
		},
		Image: "alpine",
	})
	if err != nil {
		panic(err)
	}

	if _, err := apiClient.ContainerStart(ctx, resp.ID, client.ContainerStartOptions{}); err != nil {
		panic(err)
	}

	wait := apiClient.ContainerWait(ctx, resp.ID, client.ContainerWaitOptions{})
	select {
	case err := <-wait.Error:
		if err != nil {
			panic(err)
		}
	case <-wait.Result:
	}

	out, err := apiClient.ContainerLogs(ctx, resp.ID, client.ContainerLogsOptions{ShowStdout: true})
	if err != nil {
		panic(err)
	}

	stdcopy.StdCopy(os.Stdout, os.Stderr, out)
}
```

```python
import docker
client = docker.from_env()
print(client.containers.run("alpine", ["echo", "hello", "world"]))

```

```http
$ curl --unix-socket /var/run/docker.sock -H "Content-Type: application/json" \
  -d '{"Image": "alpine", "Cmd": ["echo", "hello world"]}' \
  -X POST http://localhost/v1.53/containers/create
{"Id":"1c6594faf5","Warnings":null}

$ curl --unix-socket /var/run/docker.sock -X POST http://localhost/v1.53/containers/1c6594faf5/start

$ curl --unix-socket /var/run/docker.sock -X POST http://localhost/v1.53/containers/1c6594faf5/wait
{"StatusCode":0}

$ curl --unix-socket /var/run/docker.sock "http://localhost/v1.53/containers/1c6594faf5/logs?stdout=1"
hello world

```

--------------------------------

### GET /info

Source: https://docs.docker.com/engine/release-notes/27

Retrieves system-wide information about the Docker daemon. This endpoint no longer displays warnings related to iptables bridge filtering when the daemon starts.

```APIDOC
## GET /info

### Description
Retrieves system-wide information about the Docker daemon. This endpoint no longer displays warnings related to iptables bridge filtering when the daemon starts.

### Method
GET

### Endpoint
/info

### Parameters
#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **ID** (string) - The unique identifier for the Docker daemon.
- **Containers** (integer) - The number of containers.
- **Images** (integer) - The number of images.
- **...** (other system information fields)

#### Response Example
```json
{
  "ID": "abcdef1234567890",
  "Containers": 10,
  "Images": 50,
  "OSType": "linux",
  "Architecture": "x86_64"
}
```
```

--------------------------------

### Populate Volume with Container Data using -v

Source: https://docs.docker.com/storage/volumes

Starts a detached Nginx container named 'nginxtest' using the -v flag to mount a new volume 'nginx-vol' to '/usr/share/nginx/html'. Similar to the --mount example, this pre-populates the volume with Nginx's default HTML content.

```bash
$ docker run -d \
  --name=nginxtest \
  -v nginx-vol:/usr/share/nginx/html \
  nginx:latest

```

--------------------------------

### Docker Run: Set Process Limit (nproc) Example

Source: https://docs.docker.com/reference/cli/docker/container/run

Demonstrates how setting the 'nproc' ulimit option on multiple Docker containers for the same user can lead to resource exhaustion and container startup failures. This highlights that 'nproc' applies to the host user, not individual containers.

```bash
# Start three containers, each with a process limit of 3 for the 'daemon' user.
$ docker run -d -u daemon --ulimit nproc=3 busybox top
$ docker run -d -u daemon --ulimit nproc=3 busybox top
$ docker run -d -u daemon --ulimit nproc=3 busybox top

# Attempting to start a fourth container with the same settings will fail.
# This is because the 'daemon' user has reached its process quota of 3.
$ docker run -d -u daemon --ulimit nproc=3 busybox top
# Expected output: [8] System error: resource temporarily unavailable
```

--------------------------------

### Configure Welcome Page Routing with Traefik

Source: https://docs.docker.com/guides/traefik

Starts the 'docker/welcome-to-docker' container on the 'traefik-demo' network. It configures Traefik routing using a label, making the welcome page accessible via 'welcome.localhost' without exposing container ports directly.

```bash
docker run -d --network=traefik-demo --label 'traefik.http.routers.welcome.rule=Host(`welcome.localhost`)' docker/welcome-to-docker
```

--------------------------------

### Create and Start Interactive Container with TTY

Source: https://docs.docker.com/reference/cli/docker/container/create

This snippet demonstrates how to create an interactive Docker container with a pseudo-TTY attached, then start and attach to it. It shows the equivalent functionality using `docker run`.

```console
$ docker container create -i -t --name mycontainer alpine
6d8af538ec541dd581ebc2a24153a28329acb5268abe5ef868c1f1a261221752

$ docker container start --attach -i mycontainer
/ # echo hello world
hello world
```

```console
$ docker run -it --name mycontainer2 alpine
/ # echo hello world
hello world
```

--------------------------------

### Docker Compose Basic Network Setup

Source: https://docs.docker.com/compose/how-tos/networking

This example demonstrates a basic Docker Compose file where two services, 'web' and 'db', are defined. Compose will create a default network, and both containers will join it, becoming discoverable by their service names.

```yaml
services:
  web:
    build: .
    ports:
      - "8000:8000"
  db:
    image: postgres:18
    ports:
      - "8001:5432"
```

--------------------------------

### Dockerfile: Basic Copy and Build (Inefficient)

Source: https://docs.docker.com/build/cache/optimize

An example of a less efficient Dockerfile that copies all source files at once before installing dependencies. This leads to unnecessary re-installation of dependencies when any source file changes, invalidating the cache for the 'npm install' layer.

```dockerfile
# syntax=docker/dockerfile:1
FROM node
WORKDIR /app
COPY . .
RUN npm install
RUN npm build
```

--------------------------------

### Multi-stage Dockerfile Example

Source: https://docs.docker.com/guides/golang/build-images

Defines a multi-stage Docker build process. This Dockerfile first builds a Go application using a full Go image and then copies the compiled binary into a lean, final image, significantly reducing the overall image size and improving security by excluding build tools.

```dockerfile
# syntax=docker/dockerfile:1

# Build the application from source
FROM golang:1.19 AS build-stage

WORKDIR /app

COPY go.mod go.sum ./ 
RUN go mod download

COPY *.go ./

RUN CGO_ENABLED=0 GOOS=linux go build -o /docker-gs-ping

# Run the tests in the container
FROM build-stage AS run-test-stage
RUN go test -v ./...

```

--------------------------------

### Start Service with Replicated Volumes

Source: https://docs.docker.com/storage/volumes

Creates an Nginx service named 'devtest-service' with four replicas. Each replica is configured with a local volume named 'myvol2' mounted to '/app/'. This demonstrates how to manage volumes for replicated services.

```bash
$ docker service create -d \
  --replicas=4 \
  --name devtest-service \
  --mount source=myvol2,target=/app \
  nginx:latest

```

--------------------------------

### GET /images/{name}/json - Empty/nil fields in image Config

Source: https://docs.docker.com/engine/deprecated

Details changes to the `Config` field returned by the `docker image inspect` command and the `GET /images/{name}/json` API endpoint. Certain fields will be omitted if they are empty or nil starting in Docker v29.0.

```APIDOC
## GET /images/{name}/json - Empty/nil fields in image Config

### Description
The `Config` field in the response of `docker image inspect` and the `GET /images/{name}/json` API endpoint currently includes fields even when they are empty or nil. Starting with Docker v29.0, the following fields will be omitted from the API response when they contain empty or default values: `Cmd`, `Entrypoint`, `Env`, `Labels`, `OnBuild`, `User`, `Volumes`, `WorkingDir`. Applications consuming this API should be updated to handle the absence of these fields gracefully.

### Method
GET

### Endpoint
`/images/{name}/json`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name or ID of the image.

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```bash
curl --unix-socket /var/run/docker.sock http://localhost/images/my-image/json
```

### Response
#### Success Response (200)
- **Config** (object) - Image configuration details.
  - **Cmd** (array of strings) - Command to run when the container launches. Omitted if empty/nil in v29.0+.
  - **Entrypoint** (array of strings) - Entrypoint for the container. Omitted if empty/nil in v29.0+.
  - **Env** (array of strings) - Environment variables. Omitted if empty/nil in v29.0+.
  - **Labels** (object) - Metadata labels. Omitted if empty/nil in v29.0+.
  - **OnBuild** (array of strings) - Build instructions. Omitted if empty/nil in v29.0+.
  - **User** (string) - Username or UID to run as. Omitted if empty/nil in v29.0+.
  - **Volumes** (object) - Volume declarations. Omitted if empty/nil in v29.0+.
  - **WorkingDir** (string) - Working directory. Omitted if empty/nil in v29.0+.

#### Response Example
```json
{
  "Id": "sha25c03471306f...",
  "Config": {
    "Image": "ubuntu",
    "Cmd": [
      "/bin/sh"
    ],
    "Env": [
      "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
    ],
    "Labels": {
      "maintainer": "Docker Docs <docs@docker.com>"
    },
    "WorkingDir": "/app"
  },
  "...other fields..."
}
```
```

--------------------------------

### Dockerfile FROM Instruction with Tag and AS

Source: https://docs.docker.com/reference/dockerfile

Provides examples of the FROM instruction in Dockerfile, used to set the base image for a build stage. It shows variations including specifying a tag and aliasing the stage with 'AS'.

```dockerfile
FROM [--platform=<platform>] <image>[:<tag>] [AS <name>]
```

--------------------------------

### GET /v1.53/plugins

Source: https://docs.docker.com/reference/api/engine/latest

Returns information about installed plugins. Filters can be applied to narrow down the results based on capability or enabled status.

```APIDOC
## GET /v1.53/plugins

### Description
Returns information about installed plugins. Filters can be applied to narrow down the results based on capability or enabled status.

### Method
GET

### Endpoint
/v1.53/plugins

### Parameters
#### Query Parameters
- **filters** (string) - Optional - A JSON encoded value of the filters (a `map[string][]string`) to process on the plugin list. Available filters:
  - `capability=<capability name>`
  - `enable=<true>|<false>`

### Response
#### Success Response (200)
No error. Returns a list of plugin objects.

#### Response Example (200)
```json
[
  {
    "Id": "5724e2c8652da337ab2eedd19fc6fc0ec908e4bd907c7421bf6a8dfc70c4c078",
    "Name": "tiborvass/sample-volume-plugin",
    "Enabled": true,
    "Settings": {
      "Mounts": [
        {
          "Name": "some-mount",
          "Description": "This is a mount that's used by the plugin.",
          "Settable": [
            "string"
          ],
          "Source": "/var/lib/docker/plugins/",
          "Destination": "/mnt/state",
          "Type": "bind",
          "Options": [
            "rbind",
            "rw"
          ]
        }
      ],
      "Env": [
        "DEBUG=0"
      ],
      "Args": [
        "string"
      ],
      "Devices": [
        {
          "Name": "string",
          "Description": "string",
          "Settable": [
            "string"
          ],
          "Path": "/dev/fuse"
        }
      ]
    },
    "PluginReference": "localhost:5000/tiborvass/sample-volume-plugin:latest",
    "Config": {
      "Description": "A sample volume plugin for Docker",
      "Documentation": "https://docs.docker.com/engine/extend/plugins/",
      "Interface": {
        "Types": [
          "docker.volumedriver/1.0"
        ],
        "Socket": "plugins.sock",
        "ProtocolScheme": "some.protocol/v1.0"
      },
      "Entrypoint": [
        "/usr/bin/sample-volume-plugin",
        "/data"
      ],
      "WorkDir": "/bin/",
      "User": {
        "UID": 1000,
        "GID": 1000
      },
      "Network": {
        "Type": "host"
      },
      "Linux": {
        "Capabilities": [
          "CAP_SYS_ADMIN",
          "CAP_SYSLOG"
        ],
        "AllowAllDevices": false,
        "Devices": [
          {
            "Name": "string",
            "Description": "string",
            "Settable": [
              "string"
            ],
            "Path": "/dev/fuse"
          }
        ]
      },
      "PropagatedMount": "/mnt/volumes",
      "IpcHost": false,
      "PidHost": false,
      "Mounts": [
        {
          "Name": "some-mount",
          "Description": "This is a mount that's used by the plugin.",
          "Settable": [
            "string"
          ],
          "Source": "/var/lib/docker/plugins/",
          "Destination": "/mnt/state",
          "Type": "bind",
          "Options": [
            "rbind",
            "rw"
          ]
        }
      ],
      "Env": [
        {
          "Name": "DEBUG",
          "Description": "If set, prints debug messages",
          "Settable": null,
          "Value": "0"
        }
      ],
      "Args": {
        "Name": "args",
        "Description": "command line arguments",
        "Settable": [
          "string"
        ],
        "Value": [
          "string"
        ]
      },
      "rootfs": {
        "type": "layers",
        "diff_ids": [
          "sha256:675532206fbf3030b8458f88d6e26d4eb1577688a25efec97154c94e8b6b4887",
          "sha256:e216a057b1cb1efc11f8a268f37ef62083e70b1b38323ba252e25ac88904a7e8"
        ]
      }
    }
  }
]
```

#### Error Responses
- **500** - Server error.
```

--------------------------------

### Start Container with Volume (--mount flag)

Source: https://docs.docker.com/engine/storage/volumes

This command starts a detached Nginx container named 'devtest' and mounts a volume named 'myvol2' to the '/app/' directory within the container. If 'myvol2' does not exist, Docker creates it automatically.

```console
$ docker run -d \
  --name devtest \
  --mount source=myvol2,target=/app \
  nginx:latest
```

--------------------------------

### Use Environment Variables and Labels with Docker Logging Drivers

Source: https://docs.docker.com/engine/logging/configure

This example shows how to start a Docker container with environment variables and labels, which can be added to container logs by supported logging drivers. The output demonstrates how the 'json-file' driver includes these attributes in its log entries.

```console
docker run -dit --label production_status=testing -e os=ubuntu alpine sh
```

```json
"attrs":{"production_status":"testing","os":"ubuntu"}
```

--------------------------------

### Install Docker Desktop via MSI (Command Line)

Source: https://docs.docker.com/enterprise/enterprise-deployment/msi-install-and-configure

These commands demonstrate how to install Docker Desktop using the MSI package from the command line. They cover interactive, non-interactive, verbose logging, reboot suppression, and custom admin settings. Admin rights are required for all commands.

```powershell
msiexec /i "DockerDesktop.msi" /L*V ".\msi.log"
```

```powershell
msiexec /i "DockerDesktop.msi"
```

```powershell
msiexec /i "DockerDesktop.msi" /L*V ".\msi.log" /quiet
```

```powershell
msiexec /i "DockerDesktop.msi" /L*V ".\msi.log" /quiet /norestart
```

```powershell
msiexec /i "DockerDesktop.msi" /L*V ".\msi.log" /quiet /norestart ADMINSETTINGS="{ \"configurationFileVersion\":2, \"enhancedContainerIsolation\":{ \"value\":true, \"locked\":false } }" ALLOWEDORG="your-organization"
```

```powershell
msiexec /i "DockerDesktop.msi" /L*V ".\msi.log" /quiet /norestart ALLOWEDORG="your-organization" ALWAYSRUNSERVICE=1
```

```powershell
msiexec --% /i "DockerDesktop.msi" /L*V ".\msi.log"  PROXYHTTPMODE="manual" OVERRIDEPROXYPAC="http://localhost:8080/myproxy.pac"
```

--------------------------------

### Configure Btrfs Storage Driver Options

Source: https://docs.docker.com/reference/cli/dockerd

This example demonstrates configuring the Docker daemon with the Btrfs storage driver and setting a minimum space allocation for container subvolumes using the --storage-opt btrfs.min_space flag. This is useful for managing disk space effectively.

```console
sudo dockerd -s btrfs --storage-opt btrfs.min_space=10G

```

--------------------------------

### Metadata File Output Example

Source: https://docs.docker.com/reference/cli/docker/buildx/bake

This example illustrates how the `--metadata-file` option writes build results for each target to a specified file. The output is a map containing details about the build artifacts, similar to the functionality provided by `buildx build --metadata-file`.

```hcl
target "default" {
  output = ["type=tar,dest=hi.tar"]
}
```

```console
$ docker buildx bake --load --print
...
"output": [
  {
    "dest": "hi.tar"
    "type": "tar",
   }
]
```

--------------------------------

### Containerize a Golang Application

Source: https://docs.docker.com/llms

Learn the essential steps to containerize a Golang application using Docker. This guide covers creating a Dockerfile to package your Go application into a portable image.

```dockerfile
FROM golang:1.19-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./ 
RUN go mod download

COPY *.go . 
RUN go build -o /app/my_app

FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/my_app .

CMD ["./my_app"]
```

--------------------------------

### Docker Node PS Example

Source: https://docs.docker.com/reference/cli/docker/node/ps

An example demonstrating the 'docker node ps' command without any filters, showing all running tasks on a specified node. The output includes task names, image, node, desired state, and current state.

```bash
docker node ps swarm-manager1
```

--------------------------------

### Verify Service Readiness from Logs

Source: https://docs.docker.com/guides/genai-leveraging-rag

Identify specific log lines that indicate successful service startup and readiness. These messages confirm that the application stack is operational and ready for use.

```text
pull-model-1 exited with code 0
database-1    | 2024-12-29 09:35:53.269+0000 INFO  Started.
pdf_bot-1     |   You can now view your Streamlit app in your browser.
loader-1      |   You can now view your Streamlit app in your browser.
bot-1         |   You can now view your Streamlit app in your browser.
```

--------------------------------

### Comprehensive apt-get install with cleanup

Source: https://docs.docker.com/build/building/best-practices

Presents a well-formed RUN instruction that includes `apt-get update`, installs multiple packages with version pinning for `s3cmd`, and cleans up the apt cache (`rm -rf /var/lib/apt/lists/*`) to reduce image size.

```dockerfile
RUN apt-get update && apt-get install -y --no-install-recommends \
    aufs-tools \
    automake \
    build-essential \
    curl \
    dpkg-sig \
    libcap-dev \
    libsqlite3-dev \
    mercurial \
    reprepro \
    ruby1.9.1 \
    ruby1.9.1-dev \
    s3cmd=1.1.* \
    && rm -rf /var/lib/apt/lists/*
```

--------------------------------

### Docker Compose Application Configuration Example

Source: https://docs.docker.com/compose/intro/compose-application-model

An illustrative `compose.yaml` file defining a frontend and backend service, including volumes, networks, configurations, and secrets. This example demonstrates how to structure a multi-service application.

```yaml
services:
  frontend:
    image: example/webapp
    ports:
      - "443:8043"
    networks:
      - front-tier
      - back-tier
    configs:
      - httpd-config
    secrets:
      - server-certificate

  backend:
    image: example/database
    volumes:
      - db-data:/etc/data
    networks:
      - back-tier

volumes:
  db-data:
    driver: flocker
    driver_opts:
      size: "10GiB"

configs:
  httpd-config:
    external: true

secrets:
  server-certificate:
    external: true

networks:
  # The presence of these objects is sufficient to define them
  front-tier: {}
  back-tier: {}
```

--------------------------------

### Debugging Docker Plugins with Dockerd Logs

Source: https://docs.docker.com/engine/extend

Examples of Docker plugin interactions and their corresponding log entries in the dockerd logs. These logs help in understanding the plugin's behavior during installation, volume creation, and container runtime.

```console
$ docker plugin install tiborvass/sample-volume-plugin

INFO[0036] Starting...       Found 0 volumes on startup  plugin=f52a3df433b9aceee436eaada0752f5797aab1de47e5485f1690a073b860ff62
```

```console
$ docker volume create -d tiborvass/sample-volume-plugin samplevol

INFO[0193] Create Called...  Ensuring directory /data/samplevol exists on host...  plugin=f52a3df433b9aceee436eaada0752f5797aab1de47e5485f1690a073b860ff62
INFO[0193] open /var/lib/docker/plugin-data/local-persist.json: no such file or directory  plugin=f52a3df433b9aceee436eaada0752f5797aab1de47e5485f1690a073b860ff62
INFO[0193]                   Created volume samplevol with mountpoint /data/samplevol  plugin=f52a3df433b9aceee436eaada0752f5797aab1de47e5485f1690a073b860ff62
INFO[0193] Path Called...    Returned path /data/samplevol  plugin=f52a3df433b9aceee436eaada0752f5797aab1de47e5485f1690a073b860ff62
```

```console
$ docker run -v samplevol:/tmp busybox sh

INFO[0421] Get Called...     Found samplevol                plugin=f52a3df433b9aceee436eaada0752f5797aab1de47e5485f1690a073b860ff62
INFO[0421] Mount Called...   Mounted samplevol              plugin=f52a3df433b9aceee436eaada0752f5797aab1de47e5485f1690a073b860ff62
INFO[0421] Path Called...    Returned path /data/samplevol  plugin=f52a3df433b9aceee436eaada0752f5797aab1de47e5485f1690a073b860ff62
INFO[0421] Unmount Called... Unmounted samplevol            plugin=f52a3df433b9aceee436eaada0752f5797aab1de47e5485f1690a073b860ff62
```

--------------------------------

### Example FIPS Attestation JSON Output

Source: https://docs.docker.com/dhi/core-concepts/fips

This is an example of the JSON output returned by the `docker scout attest get` command. It lists details about the cryptographic modules used, including their certification ID, URL, name, package information, FIPS standard, status, and sunset date.

```json
[
  {
    "certification": "CMVP #4985",
    "certificationUrl": "https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/4985",
    "name": "OpenSSL FIPS Provider",
    "package": "pkg:dhi/openssl-provider-fips@3.1.2",
    "standard": "FIPS 140-3",
    "status": "active",
    "sunsetDate": "2030-03-10",
    "version": "3.1.2"
  }
]
```

--------------------------------

### Configure Bind Propagation with --mount Flag

Source: https://docs.docker.com/engine/storage/bind-mounts

This example demonstrates how to configure bind propagation using the `--mount` flag. It mounts a directory into the container twice, with the second mount having read-only access and the 'rslave' bind propagation option. This is only configurable for bind mounts on Linux host machines.

```bash
docker run -d \
  -it \
  --name devtest \
  --mount type=bind,source="$(pwd)"/target,target=/app \
  --mount type=bind,source="$(pwd)"/target,target=/app2,readonly,bind-propagation=rslave \
  nginx:latest
```

--------------------------------

### Learn Docker Concepts and Commands with Gordon

Source: https://docs.docker.com/ai/gordon/use-cases

Gain a better understanding of Docker concepts and commands through Gordon's explanations. Ask questions about networking, specific Dockerfile instructions like COPY vs. ADD, or how to debug common issues.

```console
# Explain Docker concepts
$ docker ai "explain how Docker networking works"

# Understand commands
$ docker ai "what's the difference between COPY and ADD in Dockerfile?"

# Get troubleshooting guidance
$ docker ai "how do I debug a container that exits immediately?"
```

--------------------------------

### Connect Services with Docker Compose for Prometheus Monitoring

Source: https://docs.docker.com/llms

Learn how to connect services using Docker Compose to monitor a Golang application with Prometheus and Grafana. This guide focuses on the infrastructure setup for observability.

```yaml
version: '3.7'

services:
  app: 
    build: .
    ports:
      - "8080:8080"
    
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    depends_on:
      - app

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
    depends_on:
      - prometheus
```

--------------------------------

### Verify MCP Server Connection (Claude Code)

Source: https://docs.docker.com/ai/mcp-catalog-and-toolkit/get-started

This command lists the status of connected MCP servers. The output should show 'MCP_DOCKER' as connected.

```console
$ claude mcp list
Checking MCP server health...

MCP_DOCKER: docker mcp gateway run - ✓ Connected
```

--------------------------------

### Docker Desktop Installer Flags: Proxy Configuration (Manual)

Source: https://docs.docker.com/desktop/setup/install/windows-install

Shows how to configure manual proxy settings for Docker Desktop, including specifying HTTP and HTTPS proxy URLs and hosts to exclude. This is useful in environments with strict network policies.

```console
"Docker Desktop Installer.exe" install --proxy-http-mode="manual" --override-proxy-http="http://proxy.example.com:8080" --override-proxy-https="https://proxy.example.com:8081" --override-proxy-exclude="localhost,docker.local"
```

--------------------------------

### Pull Docker Image with Authentication using Go, Python, and HTTP

Source: https://docs.docker.com/reference/api/engine/sdk/examples

Shows how to pull a Docker image using authentication credentials. Examples are provided for Go, Python, and HTTP requests. The Go and HTTP examples explicitly handle encoding credentials, while the Python SDK relies on the Docker configuration.

```go
package main

import (
	"context"
	"encoding/base64"
	"encoding/json"
	"io"
	"os"

	"github.com/moby/moby/api/types/registry"
	"github.com/moby/moby/client"
)

func main() {
	ctx := context.Background()
	apiClient, err := client.New(client.FromEnv)
	if err != nil {
		panic(err)
	}
	defer apiClient.Close()

	authConfig := registry.AuthConfig{
		Username: "username",
		Password: "password",
	}
	encodedJSON, err := json.Marshal(authConfig)
	if err != nil {
		panic(err)
	}
	authStr := base64.URLEncoding.EncodeToString(encodedJSON)

	out, err := apiClient.ImagePull(ctx, "alpine", client.ImagePullOptions{RegistryAuth: authStr})
	if err != nil {
		panic(err)
	}

	defer out.Close()
	io.Copy(os.Stdout, out)
}
```

```python
import docker
client = docker.from_env()
image = client.images.pull("alpine")
print(image.id)
```

```http
$ JSON=$(echo '{"username": "string", "password": "string", "serveraddress": "string"}' | base64)

$ curl --unix-socket /var/run/docker.sock \
  -H "Content-Type: application/tar" 
  -X POST "http://localhost/v1.53/images/create?fromImage=alpine" 
  -H "X-Registry-Auth" 
  -d "$JSON"
{"status":"Pulling from library/alpine","id":"3.1"}
{"status":"Pulling fs layer","progressDetail":{},"id":"8f13703509f7"}
{"status":"Downloading","progressDetail":{"current":32768,"total":2244027},"progress":"[\u003e                                                  ] 32.77 kB/2.244 MB","id":"8f13703509f7"}
...
```

--------------------------------

### Docker run command example

Source: https://docs.docker.com/reference/dockerfile

Example of running a Docker container with specified port mapping and interactive mode.

```console
$ docker run -i -t --rm -p 80:80 nginx
```

--------------------------------

### Start Node.js Server

Source: https://docs.docker.com/guides/wiremock

Starts the Node.js server for the Express API. This command executes the main script (src/index.js) and makes the API accessible on localhost.

```bash
npm run start
```

--------------------------------

### Set up Docker Buildx in Standalone Mode for Kubernetes Driver

Source: https://docs.docker.com/build/ci/github-actions/configure-builder

This example shows how to use the Buildx binary directly when the Docker CLI is not installed on the GitHub Runner. This is particularly useful for leveraging the `kubernetes` driver in self-hosted runners. It ensures Buildx can be invoked as a standalone executable.

```yaml
name: ci

on:
  push:

jobs:
  buildx:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
        with:
          driver: kubernetes
      
      - name: Build
        run: |
          buildx build .
```

--------------------------------

### Docker Compose: Short Syntax for Depends On

Source: https://docs.docker.com/reference/compose-file/services

Controls the order of service startup and shutdown using the short syntax for 'depends_on'. It specifies service names that must be started before the current service. Compose creates and removes services in dependency order. This example ensures 'db' and 'redis' start before 'web'.

```yaml
services:
  web:
    build: .
    depends_on:
      - db
      - redis
  redis:
    image: redis
  db:
    image: postgres:18
```

--------------------------------

### Start and Enable Docker Engine Service

Source: https://docs.docker.com/engine/install/fedora

Starts the Docker Engine service and configures it to automatically start on system boot. Alternatively, `sudo systemctl start docker` can be used to start it without enabling auto-start.

```bash
sudo systemctl enable --now docker
```

--------------------------------

### Dockerfile: Start Nginx with Custom Configuration

Source: https://docs.docker.com/guides/angular/containerize

This Dockerfile snippet defines the entrypoint and command for starting an Nginx server. It specifies a custom Nginx configuration file and runs Nginx in the foreground. It utilizes the nginx-unprivileged image for enhanced security by running as a non-root user.

```dockerfile
# Start Nginx directly with custom config
ENTRYPOINT ["nginx", "-c", "/etc/nginx/nginx.conf"]
CMD ["-g", "daemon off;"]
```

--------------------------------

### List Docker Sandboxes (CLI)

Source: https://docs.docker.com/ai/sandboxes/get-started

Lists all available Docker sandboxes, including running and stopped ones. The output displays sandbox IDs, names, status, workspace paths, and creation times. Sandboxes are not listed by `docker ps` as they are microVMs.

```console
docker sandbox ls
```

--------------------------------

### Docker MCP Catalog and Toolkit

Source: https://docs.docker.com/llms

Documentation for the Docker MCP Catalog and Toolkit, including MCP Catalog benefits, Dynamic MCP, E2B sandboxes, security FAQs, getting started, Docker Hub MCP server, MCP Gateway, and the MCP Toolkit.

```APIDOC
## Docker MCP Catalog and Toolkit

### Description
This section details the Docker MCP Catalog and Toolkit, which facilitates the use of AI tools. It covers the MCP Catalog's features, Dynamic MCP for on-demand server discovery, E2B sandboxes for secure AI agent environments, security information, setup guides, the Docker Hub MCP server for image metadata access, the MCP Gateway for orchestration, and the MCP Toolkit for setting up servers and clients.

### Endpoints

- **MCP Catalog**: [https://docs.docker.com/ai/mcp-catalog-and-toolkit/catalog/](https://docs.docker.com/ai/mcp-catalog-and-toolkit/catalog/)
- **Dynamic MCP**: [https://docs.docker.com/ai/mcp-catalog-and-toolkit/dynamic-mcp/](https://docs.docker.com/ai/mcp-catalog-and-toolkit/dynamic-mcp/)
- **E2B Sandboxes**: [https://docs.docker.com/ai/mcp-catalog-and-toolkit/e2b-sandboxes/](https://docs.docker.com/ai/mcp-catalog-and-toolkit/e2b-sandboxes/)
- **Security FAQs**: [https://docs.docker.com/ai/mcp-catalog-and-toolkit/faqs/](https://docs.docker.com/ai/mcp-catalog-and-toolkit/faqs/)
- **Get Started**: [https://docs.docker.com/ai/mcp-catalog-and-toolkit/get-started/](https://docs.docker.com/ai/mcp-catalog-and-toolkit/get-started/)
- **Docker Hub MCP Server**: [https://docs.docker.com/ai/mcp-catalog-and-toolkit/hub-mcp/](https://docs.docker.com/ai/mcp-catalog-and-toolkit/hub-mcp/)
- **MCP Gateway**: [https://docs.docker.com/ai/mcp-catalog-and-toolkit/mcp-gateway/](https://docs.docker.com/ai/mcp-catalog-and-toolkit/mcp-gateway/)
- **MCP Toolkit**: [https://docs.docker.com/ai/mcp-catalog-and-toolkit/toolkit/](https://docs.docker.com/ai/mcp-catalog-and-toolkit/toolkit/)
```

--------------------------------

### Migrate Python Application to Docker Hardened Image

Source: https://docs.docker.com/llms

This guide provides instructions and examples for migrating a Python application to use Docker Hardened Images. It details the process of adapting your Python code and dependencies for a hardened container environment.

```python
print('Hello from a Python application in a DHI!')
```

--------------------------------

### List ROS 2 Services

Source: https://docs.docker.com/guides/ros2/turtlesim-example

Lists all available ROS 2 services in the current network. This command helps in discovering services like pen control and turtle teleportation.

```console
ros2 service list
```

--------------------------------

### Access Spring Boot Application via cURL

Source: https://docs.docker.com/get-started/docker-concepts/building-images/multi-stage-builds

Example cURL command to test the running Spring Boot application by sending a GET request to the root endpoint.

```bash
curl localhost:8080
```

--------------------------------

### Configure Bind Propagation with -v Flag

Source: https://docs.docker.com/engine/storage/bind-mounts

This example shows how to configure bind propagation using the `-v` flag, achieving the same result as the `--mount` example. It mounts a directory into the container twice, with the second mount having read-only access and the 'rslave' bind propagation option. This is only configurable for bind mounts on Linux host machines.

```bash
docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app \
  -v "$(pwd)"/target:/app2:ro,rslave \
  nginx:latest
```

--------------------------------

### Clone Golang Prometheus Monitoring App

Source: https://docs.docker.com/guides/go-prometheus-monitoring/application

Clones the sample Golang application repository from GitHub. This is the initial step to obtain the project files for local development and Dockerization.

```console
git clone https://github.com/dockersamples/go-prometheus-monitoring.git
```

--------------------------------

### Clone C++ Docker Sample Application

Source: https://docs.docker.com/guides/cpp/develop

Clones the sample C++ Docker application repository from GitHub and changes the current directory to the cloned repository. This is the initial step to get the sample code for the guide.

```console
$ git clone https://github.com/dockersamples/c-plus-plus-docker.git && cd c-plus-plus-docker
```

--------------------------------

### Format Docker Version Output with Go Templates

Source: https://docs.docker.com/reference/cli/docker/version

Demonstrates how to use the --format flag with the 'docker version' command to customize output. This allows for specific data extraction or pretty-printing using Go templates. The input is the 'docker version' command, and the output is formatted according to the provided template.

```console
$ docker version --format '{{.Server.Version}}'

28.5.1
```

```console
$ docker version --format '{{.Client.APIVersion}}'

1.51
```

```console
$ docker version --format '{{json .}}'

{"Client":"Version":"28.5.1","ApiVersion":"1.51", ...}
```

--------------------------------

### Tag and push a model

Source: https://docs.docker.com/ai/model-runner/get-started

Tags a previously pulled model ('ai/smollm2') under a new name ('myorg/smollm2') and then pushes it to a container registry, such as Docker Hub.

```bash
# Tag a pulled model under a new name
$ docker model tag ai/smollm2 myorg/smollm2

# Push it to Docker Hub
$ docker model push myorg/smollm2
```

--------------------------------

### Initialize Node.js Project and Configure ES Modules (TypeScript)

Source: https://docs.docker.com/guides/github-sonarqube-sandbox/workflow

Initializes a new Node.js project, configures it for ES modules by setting 'type': 'module' in package.json, and installs necessary development dependencies like TypeScript and tsx. This setup is crucial for running TypeScript files directly.

```bash
mkdir github-sonarqube-workflow
cd github-sonarqube-workflow
npm init -y
```

```json
{
  "name": "github-sonarqube-workflow",
  "version": "1.0.0",
  "description": "Automated code quality workflow using E2B, GitHub, and SonarQube",
  "type": "module",
  "main": "quality-workflow.ts",
  "scripts": {
    "start": "tsx quality-workflow.ts"
  },
  "keywords": ["e2b", "github", "sonarqube", "mcp", "code-quality"],
  "author": "",
  "license": "MIT"
}
```

```bash
npm install e2b dotenv
npm install -D typescript tsx @types/node
```

--------------------------------

### Docker Init

Source: https://docs.docker.com/llms

Initialize a Dockerfile in the current directory.

```APIDOC
## docker init

### Description
Initializes a Dockerfile in the current directory based on the project's detected language and framework.

### Method
CLI Command

### Endpoint
docker init

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
docker init
```

### Response
#### Success Response (0)
Creates a Dockerfile in the current directory.

#### Response Example
```
Dockerfile created successfully.
```
```

--------------------------------

### Python Dockerfile Migration: Before Docker Official Images (DOI)

Source: https://docs.docker.com/dhi/migration/examples/python

This Dockerfile illustrates a Python application setup using a Docker Official Image (DOI) before migrating to Docker Hardened Images. It includes standard Python environment configurations, virtual environment setup, dependency installation, and application deployment.

```dockerfile
#syntax=docker/dockerfile:1

FROM python:latest AS builder

ENV LANG=C.UTF-8
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PATH="/app/venv/bin:$PATH"

WORKDIR /app

RUN python -m venv /app/venv
COPY requirements.txt .

# Install any additional packages if needed using apt
# RUN apt-get update && apt-get install -y gcc && rm -rf /var/lib/apt/lists/*

RUN pip install --no-cache-dir -r requirements.txt

FROM python:latest

WORKDIR /app

ENV PYTHONUNBUFFERED=1
ENV PATH="/app/venv/bin:$PATH"

COPY app.py ./
COPY --from=builder /app/venv /app/venv

ENTRYPOINT [ "python", "/app/app.py" ]
```

--------------------------------

### Migrate Node.js Application to Docker Hardened Image

Source: https://docs.docker.com/llms

This guide provides instructions and examples for migrating a Node.js application to use Docker Hardened Images. It covers the necessary steps to ensure your Node.js application runs correctly within a hardened container.

```javascript
console.log('Hello from a Node.js application in a DHI!');
```

--------------------------------

### Enable GitHub Official MCP Server via CLI

Source: https://docs.docker.com/ai/mcp-catalog-and-toolkit/get-started

This command enables the GitHub Official MCP server using the Docker CLI. It's a prerequisite for authenticating the server.

```bash
docker mcp server enable github-official
```

--------------------------------

### Docker IPvlan Network Configuration Examples

Source: https://docs.docker.com/engine/network/drivers/ipvlan

Provides examples of Docker network create commands with different VLAN IDs, subnets, and gateways, demonstrating how to map physical network segments to Docker IPvlan networks.

```console
- VLAN: 10, Subnet: 172.16.80.0/24, Gateway: 172.16.80.1
  - `--subnet=172.16.80.0/24 --gateway=172.16.80.1 -o parent=eth0.10`
- VLAN: 20, IP subnet: 172.16.50.0/22, Gateway: 172.16.50.1
  - `--subnet=172.16.50.0/22 --gateway=172.16.50.1 -o parent=eth0.20`
- VLAN: 30, Subnet: 10.1.100.0/16, Gateway: 10.1.100.1
  - `--subnet=10.1.100.0/16 --gateway=10.1.100.1 -o parent=eth0.30`
```

--------------------------------

### Pull model from Docker Hub

Source: https://docs.docker.com/ai/model-runner/get-started

Pulls a specific version of the 'ai/smollm2' model from Docker Hub. The format '360M-Q4_K_M' specifies the model size and quantization.

```bash
docker model pull ai/smollm2:360M-Q4_K_M
```

--------------------------------

### Full Docker Daemon Configuration Example (JSON)

Source: https://docs.docker.com/reference/cli/dockerd

This JSON object demonstrates all possible configuration options for the Docker daemon on Windows. It covers settings for authorization plugins, networking, containerd integration, debugging, logging, registries, and TLS.

```json
{
  "authorization-plugins": [],
  "bridge": "",
  "containerd": "\\\\.\\pipe\\containerd-containerd",
  "containerd-namespace": "docker",
  "containerd-plugins-namespace": "docker-plugins",
  "data-root": "",
  "debug": true,
  "default-network-opts": {},
  "default-runtime": "",
  "default-ulimits": {},
  "dns": [],
  "dns-opts": [],
  "dns-search": [],
  "exec-opts": [],
  "experimental": false,
  "features": {},
  "fixed-cidr": "",
  "group": "",
  "host-gateway-ip": "",
  "hosts": [],
  "insecure-registries": [],
  "labels": [],
  "log-driver": "",
  "log-format": "text",
  "log-level": "",
  "max-concurrent-downloads": 3,
  "max-concurrent-uploads": 5,
  "max-download-attempts": 5,
  "mtu": 0,
  "pidfile": "",
  "raw-logs": false,
  "registry-mirrors": [],
  "shutdown-timeout": 15,
  "storage-driver": "",
  "storage-opts": [],
  "swarm-default-advertise-addr": "",
  "tlscacert": "",
  "tlscert": "",
  "tlskey": "",
  "tlsverify": true
}
```

--------------------------------

### Dockerfile Environment Variable Replacement Examples

Source: https://docs.docker.com/reference/dockerfile

Demonstrates various ways to use environment variables and bash-like modifiers for string manipulation within Dockerfiles. This includes removing patterns from the start or end of a string and replacing patterns.

```bash
str=foobarbaz echo ${str#f*b}     # arbaz
str=foobarbaz echo ${str##f*b}    # az
string=foobarbaz echo ${string%b*}    # foobar
string=foobarbaz echo ${string%%b*}   # foo
string=foobarbaz echo ${string/ba/fo}  # fooforbaz
string=foobarbaz echo ${string//ba/fo}  # fooforfoz
```

```dockerfile
FROM busybox
ENV FOO=/bar
WORKDIR ${FOO}   # WORKDIR /bar
ADD . $FOO       # ADD . /bar
COPY $FOO /quux # COPY $FOO /quux
```

--------------------------------

### Enable Playwright MCP Server via CLI

Source: https://docs.docker.com/ai/mcp-catalog-and-toolkit/get-started

This command enables the Playwright MCP server using the Docker CLI. It's used after authorizing other servers.

```bash
docker mcp server enable playwright
```

--------------------------------

### Clone Sample Rust Application using Git

Source: https://docs.docker.com/guides/rust/build-images

Clones the 'docker-rust-hello' sample application repository from GitHub and changes the current directory to the cloned repository. This is the first step to get a sample Rust project for building a Docker image.

```bash
$ git clone https://github.com/docker/docker-rust-hello && cd docker-rust-hello
```

--------------------------------

### Build and Push Docker Image with Inline Cache

Source: https://docs.docker.com/build/ci/github-actions/cache

This example demonstrates building and pushing a Docker image using the inline cache exporter. It's suitable for 'min' cache mode and requires login to a Docker registry and setup of Docker Buildx.

```yaml
name: ci

on:
  push:

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ vars.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Build and push
        uses: docker/build-push-action@v6
        with:
          push: true
          tags: user/app:latest
          cache-from: type=registry,ref=user/app:latest
          cache-to: type=inline
```

--------------------------------

### Authorize GitHub MCP Server via CLI

Source: https://docs.docker.com/ai/mcp-catalog-and-toolkit/get-started

This command initiates the OAuth authorization process for the GitHub MCP server. It opens a browser for user authentication.

```bash
docker mcp oauth authorize github
```

--------------------------------

### Install Docker Desktop with Manual Proxy Configuration (PowerShell)

Source: https://docs.docker.com/enterprise/enterprise-deployment/msi-install-and-configure

Installs Docker Desktop interactively, specifying a manual proxy configuration with a PAC script. This command uses msiexec with specific properties to define proxy settings.

```powershell
msiexec --% /i "DockerDesktop.msi" /L*V ".\msi.log"  PROXYHTTPMODE="manual" OVERRIDEPROXYEMBEDDEDPAC="function FindProxyForURL(url,host) {return \"DIRECT\" ;; }"
```

--------------------------------

### Dockerfile for Supervisord Process Manager

Source: https://docs.docker.com/engine/containers/multi-service_container

This Dockerfile installs supervisor, configures it to manage processes, and copies the necessary application executables. It starts supervisord as the main container process.

```dockerfile
# syntax=docker/dockerfile:1
FROM ubuntu:latest
RUN apt-get update && apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY my_first_process my_first_process
COPY my_second_process my_second_process
CMD ["/usr/bin/supervisord"]
```

--------------------------------

### Build Docker Image

Source: https://docs.docker.com/get-started/workshop/06_bind_mounts

This command builds a new Docker image from a Dockerfile in the current directory and tags it as 'getting-started'. This is typically done after making changes to the application code or Dockerfile to create a new deployable image.

```bash
docker build -t getting-started .
```

--------------------------------

### Create Node.js App Directory and Install Dependencies

Source: https://docs.docker.com/guides/opentelemetry

Initializes a new Node.js project directory and installs essential OpenTelemetry packages including API, SDK, auto-instrumentations, and OTLP HTTP exporter. This sets up the foundation for instrumenting the application.

```bash
mkdir otel-js-app
cd otel-js-app
mkdir app && cd app
npm init -y
npm install express @opentelemetry/api @opentelemetry/sdk-node \
            @opentelemetry/auto-instrumentations-node \
            @opentelemetry/exporter-trace-otlp-http
```

--------------------------------

### Launch BuildKit Daemon (Unix Socket)

Source: https://docs.docker.com/build/builders/drivers/remote

Example command to launch a BuildKit daemon (`buildkitd`) listening on a Unix socket. This is a prerequisite for connecting Buildx using the remote driver with a Unix socket endpoint. It requires BuildKit to be installed.

```console
sudo ./buildkitd --group $(id -gn) --addr unix://$HOME/buildkitd.sock
```

--------------------------------

### Get Container Exit Code

Source: https://docs.docker.com/engine/reference/commandline/attach

Demonstrates how to retrieve the exit code of a container's command. The `docker attach` command returns the exit code of the process it was attached to. This example shows an exit code of 13.

```bash
$ docker run --name test -dit alpine
275c44472aebd77c926d4527885bb09f2f6db21d878c75f0a1c212c03d3bcfab

$ docker attach test
/# exit 13

$ echo $?
13

$ docker ps -a --filter name=test

CONTAINER ID   IMAGE     COMMAND     CREATED              STATUS                       PORTS     NAMES
a2fe3fd886db   alpine    "/bin/sh"   About a minute ago   Exited (13) 40 seconds ago             test
```

--------------------------------

### Execute Commands in Sandbox

Source: https://docs.docker.com/ai/sandboxes/agents/shell

Passes shell options after the '--' separator to execute specific commands within the running sandbox environment. This example echoes a string from within the sandbox.

```bash
docker sandbox run <sandbox-name> -- -c "echo 'Hello from sandbox'"
```

--------------------------------

### Test MCP Server with Prompt (Claude Code)

Source: https://docs.docker.com/ai/mcp-catalog-and-toolkit/get-started

This command demonstrates how to test an MCP server connection by sending a prompt to the Claude AI. It specifically requests information from the GitHub MCP server.

```console
$ claude "Use the GitHub MCP server to show me my open pull requests"
```

--------------------------------

### Docker Build Command with Progress and --allow flag

Source: https://docs.docker.com/build/building/cdi

This command builds a Dockerfile using the RUN --device instruction, similar to the previous example, but also includes the --progress=plain flag for detailed build output and the --allow device flag to permit device usage.

```bash
docker buildx build --progress=plain --allow device .
```

--------------------------------

### Dockerfile for PHP-FPM Production Environment

Source: https://docs.docker.com/guides/frameworks/laravel/production-setup

This Dockerfile defines a multi-stage build for a production PHP-FPM image. It installs necessary system dependencies and PHP extensions in the builder stage, copies application code, installs Composer dependencies, and then creates a lean production image with only runtime libraries and a health check script. It also copies initialization scripts and storage structures.

```dockerfile
# Stage 1: Build environment and Composer dependencies
FROM php:8.5-fpm AS builder

# Install system dependencies and PHP extensions for Laravel with MySQL/PostgreSQL support.
# Dependencies in this stage are only required for building the final image.
# Node.js and asset building are handled in the Nginx stage, not here.
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    unzip \
    libpq-dev \
    libonig-dev \
    libssl-dev \
    libxml2-dev \
    libcurl4-openssl-dev \
    libicu-dev \
    libzip-dev \
    && docker-php-ext-install -j$(nproc) \
    pdo_mysql \
    pdo_pgsql \
    pgsql \
    intl \
    zip \
    bcmath \
    soap \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set the working directory inside the container
WORKDIR /var/www

# Copy the entire Laravel application code into the container
# -----------------------------------------------------------
# In Laravel, `composer install` may trigger scripts
# needing access to application code.
# For example, the `post-autoload-dump` event might execute
# Artisan commands like `php artisan package:discover`. If the
# application code (including the `artisan` file) is not
# present, these commands will fail, leading to build errors.
#
# By copying the entire application code before running
# `composer install`, we ensure that all necessary files are
# available, allowing these scripts to run successfully.
# In other cases, it would be possible to copy composer files
# first, to leverage Docker's layer caching mechanism.
# -----------------------------------------------------------
COPY . /var/www

# Install Composer and dependencies
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer install --no-dev --optimize-autoloader --no-interaction --no-progress --prefer-dist

# Stage 2: Production environment
FROM php:8.5-fpm AS production

# Install only runtime libraries needed in production
# libfcgi-bin and procps are required for the php-fpm-healthcheck script
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpq-dev \
    libicu-dev \
    libzip-dev \
    libfcgi-bin \
    procps \
    && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Download and install php-fpm health check script
RUN curl -o /usr/local/bin/php-fpm-healthcheck \
    https://raw.githubusercontent.com/renatomefi/php-fpm-healthcheck/master/php-fpm-healthcheck \
    && chmod +x /usr/local/bin/php-fpm-healthcheck

# Copy the initialization script
COPY ./docker/php-fpm/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

# Copy the initial storage structure
COPY ./storage /var/www/storage-init

# Copy PHP extensions and libraries from the builder stage
COPY --from=builder /usr/local/lib/php/extensions/ /usr/local/lib/php/extensions/
COPY --from=builder /usr/local/etc/php/conf.d/ /usr/local/etc/php/conf.d/
COPY --from=builder /usr/local/bin/docker-php-ext-* /usr/local/bin/

```

--------------------------------

### Check Kubernetes Version with kubectl

Source: https://docs.docker.com/desktop/kubernetes

This command checks the currently installed version of the Kubernetes command-line tool (`kubectl`). It's useful for verifying your Kubernetes setup after enabling it in Docker Desktop.

```bash
kubectl version

```

--------------------------------

### Multi-stage Dockerfile Migration (Dockerfile)

Source: https://docs.docker.com/dhi/migration/migrate-from-ubuntu

An example of a multi-stage Dockerfile migrating from Ubuntu to DHI Debian. It shows a build stage using a `dev` image for installing dependencies and compiling, followed by a runtime stage using a minimal Debian image to copy the compiled artifact.

```dockerfile
# Build stage
FROM dhi.io/golang:1-debian13-dev AS builder
WORKDIR /app

# Install system dependencies (only available in dev images)
RUN apt-get update && apt-get install -y \
    git \
    && rm -rf /var/lib/apt/lists/*

# Copy application files
COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -a -ldflags="-s -w" -o main .

# Runtime stage
FROM dhi.io/golang:1-debian13
WORKDIR /app

# Copy compiled binary from builder
COPY --from=builder /app/main /app/main

# Run the application
ENTRYPOINT ["/app/main"]

```

--------------------------------

### Taskfile.yml Development and Production Commands

Source: https://docs.docker.com/guides/nodejs/develop

This snippet shows example commands from a Taskfile.yml for managing development and production Docker environments. It includes tasks for starting the development environment, building development and production images, running containers, and performing build-and-run operations.

```console
# Development
$ task dev              # Start development environment
$ task dev:build        # Build development image
$ task dev:run          # Run development container

# Production
$ task build            # Build production image
$ task run              # Run production container
$ task build-run        # Build and run in one step

# Testing
$ task test             # Run all tests
$ task test:unit        # Run unit tests with coverage
$ task test:lint        # Run linting

# Kubernetes
$ task k8s:deploy       # Deploy to Kubernetes
$ task k8s:status       # Check deployment status
$ task k8s:logs         # View pod logs

```

--------------------------------

### Run UBI9 Container with Red Hat Subscription Data

Source: https://docs.docker.com/desktop/setup/install/linux/rhel

An example command to run a Red Hat Universal Base Image 9 container, mounting local Red Hat subscription data into the container. This allows the container to access subscription-related information.

```console
docker run --rm -it -v "/etc/pki/entitlement:/etc/pki/entitlement" -v "/etc/rhsm:/etc/rhsm-host" -v "/etc/yum.repos.d/redhat.repo:/etc/yum.repos.d/redhat.repo" registry.access.redhat.com/ubi9
```

--------------------------------

### Docker Sandbox Path Resolution Example

Source: https://docs.docker.com/ai/sandboxes/workflows

This example demonstrates how Docker resolves relative paths for workspaces. It shows the effect of changing the directory before running the sandbox command and how paths are mounted inside the sandbox, distinguishing between read-write and read-only mounts.

```console
$ cd /Users/bob/projects
$ docker sandbox run AGENT ./app ~/docs:ro
```

--------------------------------

### BuildKit Outputs Configuration Example

Source: https://docs.docker.com/reference/api/engine/latest

Example of the `outputs` query parameter for the Docker build API, demonstrating how to configure BuildKit outputs. This example specifies an 'moby' type output with compression enabled.

```json
[{"Type":"moby","Attrs":{"type":"image","force-compression":"true","compression":"zstd"}}]
```

--------------------------------

### Dockerfile Reference

Source: https://docs.docker.com/llms

Documentation for the Dockerfile syntax, which is used to define how to build a Docker image. It covers instructions like FROM, RUN, COPY, EXPOSE, CMD, and more. Understanding these instructions is crucial for creating custom container images.

```Dockerfile
# Example Dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y nginx
COPY index.html /var/www/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

--------------------------------

### Run an interactive shell in a Docker sandbox

Source: https://docs.docker.com/reference/cli/docker/sandbox/exec

This example shows how to start an interactive bash shell inside a Docker sandbox. The '-it' flags are used to allocate a pseudo-TTY and keep STDIN open, enabling interactive use.

```console
$ docker sandbox exec -it my-sandbox /bin/bash
```

--------------------------------

### Start Docker container with read-write bind mount using -v

Source: https://docs.docker.com/engine/storage/bind-mounts

Starts a Docker container named 'devtest' with a read-write bind mount using the '-v' flag. The host's './target' directory is mounted to '/app' inside the container, enabling bidirectional file access and modification.

```console
$ docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app \
  nginx:latest
```

--------------------------------

### Inspect Legacy Sandbox Packages

Source: https://docs.docker.com/ai/sandboxes/migration

This command inspects the installed packages within a legacy sandbox container using dpkg. It's used in the 'Migrate configuration' option to understand the sandbox's setup.

```bash
docker exec <old-sandbox-container> dpkg -l
```

--------------------------------

### Disable Docker Engine Auto-Start

Source: https://docs.docker.com/desktop/setup/install/linux

This command disables the Docker Engine service from automatically starting on system boot. This is recommended to prevent resource consumption and potential conflicts with Docker Desktop.

```bash
sudo systemctl disable docker docker.socket containerd
```

--------------------------------

### Format Volume List as JSON

Source: https://docs.docker.com/reference/cli/docker/volume/ls

This example shows how to use the --format option with the 'json' directive to output all volume details in JSON format. It requires the 'docker' CLI and assumes volumes are present.

```console
$ docker volume ls --format json
{"Driver":"local","Labels":"","Links":"N/A","Mountpoint":"/var/lib/docker/volumes/docker-cli-dev-cache/_data","Name":"docker-cli-dev-cache","Scope":"local","Size":"N/A"}
```

--------------------------------

### Start Docker container with read-write bind mount using --mount

Source: https://docs.docker.com/engine/storage/bind-mounts

Starts a Docker container named 'devtest' with a read-write bind mount. The host's './target' directory is mounted to '/app' inside the container. This allows the container to access and modify files in the host's target directory.

```console
$ docker run -d \
  -it \
  --name devtest \
  --mount type=bind,source="$(pwd)"/target,target=/app \
  nginx:latest
```

--------------------------------

### Dockerfile Multi-stage Build Example

Source: https://docs.docker.com/build/building/best-practices

Demonstrates a multi-stage Dockerfile to separate build environments from runtime environments, resulting in smaller final images. This approach improves efficiency and security by only including necessary artifacts in the production image.

```dockerfile
# syntax=docker/dockerfile:1
FROM ubuntu:24.04
RUN apt-get -y update && apt-get install -y --no-install-recommends python3
```

--------------------------------

### Pass Runtime Options to Copilot Sandbox

Source: https://docs.docker.com/ai/sandboxes/agents/copilot

Example of how to pass runtime options, such as '--yolo' to disable approval prompts for a single session, to a running Copilot sandbox. Options are passed after a '--' separator.

```console
$ docker sandbox run <sandbox-name> -- --yolo

```

--------------------------------

### Install Legacy Docker Compose Standalone on Linux

Source: https://docs.docker.com/llms

Instructions for installing the legacy Docker Compose standalone tool on Linux. This method is for older versions or specific use cases where the plugin is not preferred. It involves downloading a binary and making it executable.

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

--------------------------------

### Execute Helper Script with Custom Arguments

Source: https://docs.docker.com/develop/security-best-practices

Shows how to run a Docker container and pass arguments to the helper script defined as the ENTRYPOINT, allowing for custom command execution.

```shell
$ docker run postgres postgres --help
```

--------------------------------

### Bake Command to Build Target

Source: https://docs.docker.com/build/bake/introduction

This console command demonstrates how to use Bake to build a previously defined target ('myapp'). It leverages the Bake configuration file to execute the build process.

```console
$ docker buildx bake myapp
```

--------------------------------

### Docker Client: Connect to Remote Daemon via SSH

Source: https://docs.docker.com/reference/cli/dockerd

These examples illustrate connecting the Docker client to a remote daemon using SSH. Public key authentication is required, and password authentication is not supported. SSH agent setup is necessary for passphrase-protected keys.

```console
docker -H ssh://me@example.com:22/var/run/docker.sock ps
```

```console
docker -H ssh://me@example.com:22 ps
```

```console
docker -H ssh://me@example.com ps
```

```console
docker -H ssh://example.com ps
```

--------------------------------

### Configure MCP Servers in JSON

Source: https://docs.docker.com/ai/cagent/integrations/mcp

An example of configuring MCP servers within a JSON structure, specifying the command to run cagent and its arguments, including the agent reference. This is used in MCP client configurations.

```json
{
  "mcpServers": {
    "myagent": {
      "command": "/usr/local/bin/cagent",
      "args": ["mcp", "agentcatalog/pirate"]
    }
  }
}
```

--------------------------------

### Build with Specific Target and Build Arguments

Source: https://docs.docker.com/reference/cli/docker/buildx/build

Provides an example of how to execute a Docker build for a specific target (`--target`) and supply custom values for the build arguments that the target consumes.

```console
$ docker buildx build \
  --build-arg GO_VERSION=1.22 \
  --build-arg HUGO_VERSION=0.127.0 \
  --build-arg HUGO_ENV=production \
  --build-arg DOCS_URL=https://example.com \
  --build-arg PAGEFIND_VERSION=1.1.0 \
  --target release https://github.com/docker/docs.git
```

--------------------------------

### Update DMR in Docker Engine

Source: https://docs.docker.com/ai/model-runner/get-started

Updates the Docker Model Runner in Docker Engine by first uninstalling the current version and then reinstalling it. Local models are preserved by default.

```bash
docker model uninstall-runner --images && docker model install-runner
```

--------------------------------

### Set Default WSL Version to v2

Source: https://docs.docker.com/desktop/features/wsl

This command configures WSL to use version 2 as the default for all future Linux distribution installations. This simplifies setup by ensuring new distributions are automatically compatible with Docker Desktop's requirements.

```console
wsl.exe --set-default-version 2
```

--------------------------------

### Initialize Docker Assets using `docker init` (DHI Example)

Source: https://docs.docker.com/guides/dotnet/containerize

Initializes Docker assets (.dockerignore, Dockerfile, compose.yaml, README.Docker.md) for an ASP.NET Core project using the `docker init` CLI. This example configures the Dockerfile to use DHI base images.

```console
$ docker init
Welcome to the Docker Init CLI!

This utility will walk you through creating the following files with sensible defaults for your project:
  - .dockerignore
  - Dockerfile
  - compose.yaml
  - README.Docker.md

Let's get started!

? What application platform does your project use? ASP.NET Core
? What's the name of your solution's main project? myWebApp
? What version of .NET do you want to use? 10.0
? What local port do you want to use to access your server? 8080
```

--------------------------------

### Dockerfile for Building Go Backend in Docker Extension

Source: https://docs.docker.com/extensions/extensions-sdk/build/backend-extension-tutorial

This Dockerfile snippet demonstrates how to build a Go backend application for a Docker extension. It uses multi-stage builds to compile the Go binary and then copies it into a minimal Alpine Linux image. This ensures the final image is small and contains only the necessary executable.

```dockerfile
# syntax=docker/dockerfile:1
FROM node:17.7-alpine3.14 AS client-builder
# ... build frontend application

# Build the Go backend
FROM golang:1.17-alpine AS builder
ENV CGO_ENABLED=0
WORKDIR /backend
RUN --mount=type=cache,target=/go/pkg/mod \
    --mount=type=cache,target=/root/.cache/go-build \
    --mount=type=bind,source=vm/.,target=. \
    go build -trimpath -ldflags="-s -w" -o bin/service

FROM alpine:3.15

```

--------------------------------

### Install Docker Desktop on Fedora Linux

Source: https://docs.docker.com/llms

Instructions for installing Docker Desktop on Fedora Linux. Similar to Debian, this process involves adding the Docker repository and installing the Docker Desktop package.

```bash
# Update package index and install prerequisites
sudo dnf -y update
sudo dnf install -y dnf-plugins-core

# Add Docker's official GPG key
sudo install -m 0755 -d /etc/pki/rpm-gpg
curl -fsSL https://download.docker.com/linux/fedora/gpg | sudo gpg --dearmor -o /etc/pki/rpm-gpg/docker-archive-keyring.gpg
sudo chmod a+r /etc/pki/rpm-gpg/docker-archive-keyring.gpg

# Add the repository
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo

# Install Docker Desktop
sudo dnf install -y docker-desktop
```

--------------------------------

### Run ROS 2 in a Docker Container

Source: https://docs.docker.com/llms

This guide demonstrates how to run ROS 2 in an isolated Docker container using official ROS 2 images. It also covers installing additional ROS 2 packages.

```Dockerfile
# Example Dockerfile for running ROS 2
FROM osrf/ros:humble-desktop

# Install additional ROS 2 packages if needed
# RUN apt-get update && apt-get install -y ros-humble-navigation2

CMD ["ros2", "launch", "demo_nodes_cpp", "talker"]
```

--------------------------------

### Run Ubuntu Container with Bind Mount (Command Prompt)

Source: https://docs.docker.com/get-started/workshop/06_bind_mounts

Starts an interactive bash session in an Ubuntu container, mounting the current host directory (dynamically determined by `%cd%`) to `/src` inside the container. This enables file sharing and synchronization between the host and the container.

```console
docker run -it --mount "type=bind,src=%cd%,target=/src" ubuntu bash
```

--------------------------------

### Develop Docker Plugin System

Source: https://docs.docker.com/llms

Guides on developing and using plugins with the Docker managed plugin system. Covers plugin configuration versions and the Docker Plugin API.

```go
// Example of a basic Docker plugin structure (conceptual)
package main

import (
	"encoding/json"
	"fmt"
	"net/http"
	"os/exec"
	"strings"
)

func main() {
	http.HandleFunc("/Plugin.Activate", activateHandler)
	http.HandleFunc("/MyPlugin.MyMethod", myMethodHandler)
	http.ListenAndServe(":8080", nil)
}

func activateHandler(w http.ResponseWriter, r *http.Request) {
	response := map[string]interface{}{
		"Implements": []string{"MyPlugin"}
	}
	json.NewEncoder(w).Encode(response)
}

func myMethodHandler(w http.ResponseWriter, r *http.Request) {
	// Implement your plugin logic here
	fmt.Fprintf(w, "Hello from MyPlugin!")
}

// To register this plugin with Docker, you would typically use:
// docker plugin install --grant-all-permissions your-plugin-image
```

--------------------------------

### Install rclone Docker Volume Plugin

Source: https://docs.docker.com/engine/storage/volumes

Installs the rclone Docker volume plugin, enabling SFTP volume creation. This command requires administrative privileges and grants all necessary permissions to the plugin.

```bash
docker plugin install --grant-all-permissions rclone/docker-volume-rclone --aliases rclone
```

--------------------------------

### Docker Volume Mounting Syntax

Source: https://docs.docker.com/engine/storage/volumes

Demonstrates the basic syntax for mounting volumes using both the `--mount` and `--volume` flags in Docker. The `--mount` flag is generally preferred for its explicitness and broader option support.

```console
$ docker run --mount type=volume,src=<volume-name>,dst=<mount-path>
$ docker run --volume <volume-name>:<mount-path>
```

--------------------------------

### Configure MariaDB Database in Docker Compose

Source: https://docs.docker.com/guides/php/develop

This YAML configuration defines the MariaDB database service within a Docker Compose setup. It specifies the image to use, restart policy, user, secrets for authentication, volume for data persistence, environment variables for database setup, exposed port, and a healthcheck to ensure the database is ready before other services start.

```yaml
services:
  server:
    build:
      context: .
    ports:
      - 9000:80
    depends_on:
      db:
        condition: service_healthy
    secrets:
      - db-password
    environment:
      - PASSWORD_FILE_PATH=/run/secrets/db-password
      - DB_HOST=db
      - DB_NAME=example
      - DB_USER=root
  db:
    image: mariadb
    restart: always
    user: root
    secrets:
      - db-password
    volumes:
      - db-data:/var/lib/mysql
    environment:
      - MARIADB_ROOT_PASSWORD_FILE=/run/secrets/db-password
      - MARIADB_DATABASE=example
    expose:
      - 3306
    healthcheck:
      test:
        [
          "CMD",
          "/usr/local/bin/healthcheck.sh",
          "--su-mysql",
          "--connect",
          "--innodb_initialized",
        ]
      interval: 10s
      timeout: 5s
      retries: 5
volumes:
  db-data:
secrets:
  db-password:
    file: db/password.txt
```

--------------------------------

### Extension Folder Structure Example

Source: https://docs.docker.com/extensions/extensions-sdk/build/minimal-frontend-extension

Illustrates the typical file and directory layout for a minimal frontend Docker extension, including Dockerfile, metadata.json, and the UI source folder.

```text
. 
├── Dockerfile # (1) 
├── metadata.json # (2) 
└── ui # (3) 
    └── index.html
```

--------------------------------

### Execute Docker Operations with Gordon

Source: https://docs.docker.com/ai/gordon/use-cases

Run essential Docker commands through Gordon's natural language interface. This includes starting containers with specific configurations, building and tagging images for deployment, and cleaning up unused Docker resources.

```console
# Start containers with configuration
$ docker ai "run a redis container with persistence"

# Build and tag images
$ docker ai "build my Dockerfile and tag it for production"

# Clean up resources
$ docker ai "clean up all unused Docker resources"
```

--------------------------------

### Register and Start Docker Service on Windows (PowerShell)

Source: https://docs.docker.com/engine/install/binaries

These PowerShell commands register the Docker daemon as a service and then start the Docker service. This is a crucial step for enabling Docker functionality on Windows Server after extracting the binaries.

```powershell
& $Env:ProgramFiles\Docker\dockerd --register-service
Start-Service docker
```

--------------------------------

### Kubernetes Deployment and Pods for BuildKit

Source: https://docs.docker.com/build/builders/drivers/kubernetes

These commands display the Kubernetes resources created by the Buildx Kubernetes driver. The first command lists the BuildKit deployment named 'kube0', showing that 4 out of 4 replicas are ready. The second command lists the individual pods associated with the 'kube0' deployment, confirming their running status.

```bash
kubectl -n buildkit get deployments
NAME    READY   UP-TO-DATE   AVAILABLE   AGE
kube0   4/4     4            4           8s
```

```bash
kubectl -n buildkit get pods
NAME                     READY   STATUS    RESTARTS   AGE
kube0-6977cdcb75-48ld2   1/1     Running   0          8skube0-6977cdcb75-rkc6b   1/1     Running   0          8skube0-6977cdcb75-vb4ks   1/1     Running   0          8skube0-6977cdcb75-z4fzs   1/1     Running   0          8s
```

--------------------------------

### Example: Docker --mount with Read-Only and Bind Propagation

Source: https://docs.docker.com/storage/bind-mounts

This example demonstrates using the `--mount` flag with a bind mount, specifying the source directory, destination in the container, read-only option, and bind propagation settings.

```bash
$ docker run --mount type=bind,src=.,dst=/project,ro,bind-propagation=rshared

```

--------------------------------

### Enable CRB and Install EPEL and Pass (RHEL 9)

Source: https://docs.docker.com/desktop/setup/install/linux/rhel

Enables the CodeReady Linux Builder (CRB) repository, installs the EPEL repository, and installs the 'pass' package for RHEL 9. This is a prerequisite for Docker Desktop installation.

```bash
sudo subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm
sudo dnf install pass
```

--------------------------------

### Dockerfile RUN Instruction: --device Option Example

Source: https://docs.docker.com/engine/reference/builder

Demonstrates the use of the --device option with the RUN instruction to make CDI devices available during the build. This requires BuildKit and specific daemon configurations. The example shows requesting all NVIDIA GPU devices.

```dockerfile
# syntax=docker/dockerfile:1-labs

FROM scratch AS model
ADD https://huggingface.co/bartowski/Llama-3.2-1B-Instruct-GGUF/resolve/main/Llama-3.2-1B-Instruct-Q4_K_M.gguf /model.gguf

FROM scratch AS prompt
COPY <<EOF prompt.txt
Q: Generate  a list of 10 unique biggest countries by population in JSON with their estimated poulation in 1900 and 2024. Answer only newline formatted JSON with keys "country", "population_1900", "population_2024" with 10 items.
A:
[
    {

EOF

FROM ghcr.io/ggml-org/llama.cpp:full-cuda-b5124
RUN --device=nvidia.com/gpu=all \
    --mount=from=model,target=/models \
    --mount=from=prompt,target=/tmp \
    ./llama-cli -m /models/model.gguf -no-cnv -ngl 99 -f /tmp/prompt.txt
```

--------------------------------

### Configure Docker gcplogs Driver with Labels and Environment Variables

Source: https://docs.docker.com/engine/logging/drivers/gcplogs

This example demonstrates how to configure the Docker gcplogs driver to log to the default destination. It includes container labels, environment variables, and the command used to start the container. The driver automatically discovers the Google Cloud project from the metadata server.

```console
docker run \
    --log-driver=gcplogs \
    --log-opt labels=location \
    --log-opt env=TEST \
    --log-opt gcp-log-cmd=true \
    --env "TEST=false" \
    --label location=west \
    your/application
```

--------------------------------

### Initialize and Use Named Docker Volume

Source: https://docs.docker.com/reference/cli/docker/container/create

This example illustrates how to create a Docker container with a named volume (`/data`) and then use that volume from another container. Volumes are initialized during the `docker create` phase.

```console
$ docker create -v /data --name data ubuntu

240633dfbb98128fa77473d3d9018f6123b99c454b3251427ae190a7d951ad57

$ docker run --rm --volumes-from data ubuntu ls -la /data

total 8
drwxr-xr-x  2 root root 4096 Dec  5 04:10 .
drwxr-xr-x 48 root root 4096 Dec  5 04:11 ..
```

--------------------------------

### Enable CRB and Install EPEL and Pass (RHEL 8)

Source: https://docs.docker.com/desktop/setup/install/linux/rhel

Enables the CodeReady Linux Builder (CRB) repository, installs the EPEL repository, and installs the 'pass' package for RHEL 8. This is a prerequisite for Docker Desktop installation.

```bash
sudo subscription-manager repos --enable codeready-builder-for-rhel-8-$(arch)-rpms
sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo dnf install pass
```

--------------------------------

### Install Docker Engine from RPM Package (Fedora)

Source: https://docs.docker.com/engine/install/fedora

Installs Docker Engine by providing the path to a downloaded `.rpm` package file. This method is used when the Docker repository is not available or preferred.

```bash
sudo dnf install /path/to/package.rpm
```

--------------------------------

### RUN --mount=type=bind Example in Dockerfile

Source: https://docs.docker.com/reference/dockerfile

This example demonstrates the `RUN --mount=type=bind` instruction, which allows binding files or directories into the build container. The mount is read-only by default.

```dockerfile
RUN --mount=type=bind
```

--------------------------------

### Dockerfile Example for --squash Build

Source: https://docs.docker.com/reference/cli/docker/build-legacy

This Dockerfile demonstrates a simple build process that includes creating a file, adding content to it, creating another file, setting an environment variable, and then removing the second file. This is used to illustrate the effect of the --squash flag.

```dockerfile
FROM busybox
RUN echo hello > /hello
RUN echo world >> /hello
RUN touch remove_me /remove_me
ENV HELLO=world
RUN rm /remove_me
```

--------------------------------

### Dry-run Docker installation script

Source: https://docs.docker.com/engine/install/fedora

This command downloads the Docker convenience script and runs it with the --dry-run option. This allows you to preview the installation steps without actually installing Docker, which is useful for understanding the process and potential impacts.

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh --dry-run
```

--------------------------------

### Example .dockerignore file

Source: https://docs.docker.com/build/building/context

An example of a .dockerignore file listing directories and files to be excluded from the Docker build context. This helps optimize build times by preventing unnecessary data transfer to the Docker daemon.

```dockerignore
# .dockerignore
node_modules
bar
```

--------------------------------

### Configure CI/CD for .NET Application with Docker

Source: https://docs.docker.com/llms

This guide explains how to set up Continuous Integration and Continuous Deployment (CI/CD) pipelines for your .NET application using Docker. It ensures automated building, testing, and deployment.

```YAML
# Example GitHub Actions workflow for .NET CI/CD
name: .NET CI/CD

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Setup .NET
      uses: actions/setup-dotnet@v3
      with:
        dotnet-version: '6.0.x'
    - name: Build application
      run: dotnet build --configuration Release
    - name: Test application
      run: dotnet test --configuration Release
    - name: Build and push Docker image
      uses: docker/build-push-action@v4
      with:
        context: .
        push: true
        tags: your-dockerhub-username/your-app:latest
```

--------------------------------

### Pull Docker Image Example

Source: https://docs.docker.com/engine/storage/drivers/vfs-driver

Example command to pull a Docker image. This demonstrates the process that leads to the creation of VFS storage layers on the host.

```bash
$ docker pull ubuntu
```

--------------------------------

### List Kubernetes Namespaces with kubectl

Source: https://docs.docker.com/extensions/extensions-sdk/guides/kubernetes

This example demonstrates how to list Kubernetes namespaces using `kubectl get namespaces`. It specifies the `docker-desktop` context and uses custom columns to output only the namespace names without headers. The `ddClient.extension.host?.cli.exec` method facilitates the execution of this command.

```typescript
const output = await ddClient.extension.host?.cli.exec("kubectl", [
  "get",
  "namespaces",
  "--no-headers",
  "-o",
  'custom-columns=":metadata.name"',
  "--context",
  "docker-desktop",
]);
```

--------------------------------

### Configure DOCKER_HOST for Docker SDKs

Source: https://docs.docker.com/desktop/setup/install/linux

Example of setting the DOCKER_HOST environment variable to connect Docker SDKs and tools to Docker Desktop on Linux. Docker Desktop for Linux uses a per-user socket, requiring this configuration for direct daemon connections.

```bash
# Example for bash/zsh
export DOCKER_HOST="unix:///run/user/$(id -u)/docker.sock"
```

--------------------------------

### Bash Script: Starter script with exec and gosu for PostgreSQL

Source: https://docs.docker.com/reference/dockerfile

A bash script designed to be used as an ENTRYPOINT. It handles PostgreSQL initialization and ensures the final executable receives Unix signals correctly by using 'exec' and 'gosu'.

```bash
#!/usr/bin/env bash
set -e

if [ "$1" = 'postgres' ]; then
    chown -R postgres "$PGDATA"

    if [ -z "$(ls -A "$PGDATA")" ]; then
        gosu postgres initdb
    fi

    exec gosu postgres "$@"
fi

exec "$@"
```

--------------------------------

### Install Node.js Dependencies (Console)

Source: https://docs.docker.com/guides/localstack

These console commands are used to navigate to the backend directory and install the necessary Node.js dependencies for the application. This step is crucial before running the backend service.

```bash
$ cd backend/
$ npm install
```

--------------------------------

### Install Docker Client Binary on Linux

Source: https://docs.docker.com/desktop/setup/install/linux/archlinux

This snippet downloads and installs the Docker client binary on a Linux system. It fetches a compressed tarball, extracts the binary, and copies it to a system-wide executable path. Ensure you have `wget` and `tar` installed.

```console
$ wget https://download.docker.com/linux/static/stable/x86_64/docker-29.2.1.tgz -qO- | tar xvfz - docker/docker --strip-components=1
$ sudo cp -rp ./docker /usr/local/bin/ && rm -r ./docker
```

--------------------------------

### Test Docker Compose Installation

Source: https://docs.docker.com/compose/install/standalone

Tests the installation of Docker Compose by checking its version. This command works for both Linux and Windows installations after the binary is in the system's PATH.

```console
docker-compose.exe version
```

--------------------------------

### Start Containers Automatically

Source: https://docs.docker.com/llms

Configure containers to start automatically when the Docker daemon starts. This is typically managed using restart policies.

```bash
# Example: Always restart the container if it stops
docker run -d --restart always my-image

# Example: Restart the container unless it is explicitly stopped
docker run -d --restart unless-stopped my-image

# Example: Restart the container only on failure
docker run -d --restart on-failure my-image
```

--------------------------------

### Custom Registry Configuration Example ('kind' Mode)

Source: https://docs.docker.com/desktop/use-desktop/kubernetes

Demonstrates how Docker Desktop pulls images from a custom registry when the 'KubernetesImagesRepository' setting is configured. This example shows the image paths for 'kind' mode with a custom registry 'my-registry:5000/kind-images'.

```console
my-registry:5000/kind-images/node:<tag>
my-registry:5000/kind-images/envoy:<tag>
my-registry:5000/kind-images/desktop-cloud-provider-kind:<tag>
my-registry:5000/kind-images/desktop-containerd-registry-mirror:<tag>
```

--------------------------------

### Inspect Docker Node with Custom Format

Source: https://docs.docker.com/reference/cli/docker/node/inspect

This endpoint allows you to inspect a Docker node and retrieve specific information using a Go template format. The example shows how to get the leader status of the swarm manager.

```APIDOC
## GET /nodes/{id}

### Description
Inspects a Docker node and returns detailed information about it. The `--format` flag allows for custom output formatting using Go templates.

### Method
GET

### Endpoint
`/nodes/{id}`

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID or name of the node to inspect.

#### Query Parameters
- **format** (string) - Optional - Go template to format the output. If not specified, the output is in JSON format.

### Request Example
```console
$ docker node inspect --format '{{ .ManagerStatus.Leader }}' self
```

### Response
#### Success Response (200)
- **output** (string) - The formatted output based on the provided Go template.

#### Response Example
```
false
```
```

--------------------------------

### Install Node.js Dependencies

Source: https://docs.docker.com/guides/wiremock

Installs all the necessary packages for the Node.js project as defined in the package.json file. This command is essential for the project to run correctly.

```bash
npm install
```

--------------------------------

### Back Up Docker Volume to Host Directory

Source: https://docs.docker.com/storage/volumes

This example shows how to create a backup of a Docker volume by running a temporary container that mounts the source volume and tars its contents into a file within a local host directory. The host directory must be mounted into the backup container.

```bash
$ docker run -v /dbdata --name dbstore ubuntu /bin/bash
$ docker run --rm --volumes-from dbstore -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata
```

--------------------------------

### Install Docker Extension (Bash)

Source: https://docs.docker.com/extensions/extensions-sdk/build/frontend-extension-tutorial

Installs the built Docker extension image onto Docker Desktop. After installation, the extension will appear in the Docker Desktop Dashboard.

```bash
docker extension install awesome-inc/my-extension:latest
```

--------------------------------

### docker plugin install

Source: https://docs.docker.com/reference/cli/docker/plugin/install

Installs and enables a plugin. Docker looks first for the plugin on your Docker host. If the plugin does not exist locally, then the plugin is pulled from the registry.

```APIDOC
## POST /plugins

### Description
Installs and enables a plugin. Docker looks first for the plugin on your Docker host. If the plugin does not exist locally, then the plugin is pulled from the registry. Note that the minimum required registry version to distribute plugins is 2.3.0.

### Method
POST

### Endpoint
/plugins

### Parameters
#### Query Parameters
- **PLUGIN** (string) - Required - The name of the plugin to install.
- **KEY=VALUE...** (string) - Optional - Environment variables for the plugin.

#### Request Body
- **alias** (string) - Optional - Local name for plugin.
- **disable** (boolean) - Optional - Do not enable the plugin on install.
- **grant_all_permissions** (boolean) - Optional - Grant all permissions necessary to run the plugin.

### Request Example
```json
{
  "plugin": "vieux/sshfs",
  "alias": "my-sshfs",
  "disable": false,
  "grant_all_permissions": true,
  "env": {
    "DEBUG": "1"
  }
}
```

### Response
#### Success Response (200)
- **ID** (string) - The ID of the installed plugin.
- **Name** (string) - The name of the installed plugin.
- **Description** (string) - A description of the plugin.
- **Enabled** (boolean) - Whether the plugin is enabled.

#### Response Example
```json
{
  "ID": "69553ca1d123",
  "Name": "vieux/sshfs:latest",
  "Description": "sshFS plugin for Docker",
  "Enabled": true
}
```
```

--------------------------------

### Configure Private Marketplace Settings in JSON

Source: https://docs.docker.com/extensions/private-marketplace

Example JSON configuration for `admin-settings.json` to enable and configure the private Docker extension marketplace. This includes enabling extensions, activating the private marketplace, controlling installation sources, and setting a contact URL.

```json
{
  "extensionsEnabled": {
    "locked": true,
    "value": true
  },
  "extensionsPrivateMarketplace": {
    "locked": true,
    "value": true
  },
  "onlyMarketplaceExtensions": {
    "locked": false,
    "value": true
  },
  "extensionsPrivateMarketplaceAdminContactURL": {
    "locked": true,
    "value": "mailto:admin@acme.com"
  }
}
```

--------------------------------

### Creating File with COPY and Here-Document

Source: https://docs.docker.com/engine/reference/builder

Shows how to use the COPY instruction with a here-document to create a file directly within the Docker image. This example creates a file named 'greeting.txt' with the content 'hello world'.

```dockerfile
# syntax=docker/dockerfile:1
FROM alpine
COPY <<EOF greeting.txt
hello world
EOF
```

--------------------------------

### Best Practices for Docker Desktop with WSL 2

Source: https://docs.docker.com/llms

Follow best practices for optimal performance and stability when using Docker Desktop with the Windows Subsystem for Linux (WSL) 2. This includes tips on resource allocation, file sharing, and network configuration to ensure a smooth development experience.

```bash
# Ensure WSL 2 is set as the default version: wsl --set-default-version 2
# Allocate sufficient resources (CPU, Memory) to WSL 2 via .wslconfig file.
```

--------------------------------

### Configure GH_TOKEN or GITHUB_TOKEN Environment Variable

Source: https://docs.docker.com/ai/sandboxes/agents/copilot

Example of how to set the GH_TOKEN or GITHUB_TOKEN environment variable in shell configuration files like .bashrc or .zshrc to authenticate with GitHub Copilot. This is recommended for persistent access.

```plaintext
export GH_TOKEN=ghp_xxxxx

```

```plaintext
export GITHUB_TOKEN=ghp_xxxxx

```

--------------------------------

### Run Docker Container Locally

Source: https://docs.docker.com/docker-hub/quickstart

Runs a Docker container from the built image, mapping port 8080 on the host to port 80 in the container. The --rm flag ensures the container is removed upon exit. This is useful for testing the image before pushing it.

```bash
$ docker run -p 8080:80 --rm <YOUR-USERNAME>/nginx-custom
```

--------------------------------

### Kubernetes Pod Definition (YAML)

Source: https://docs.docker.com/guides/orchestration

Defines a simple Kubernetes pod named 'demo' that runs an 'alpine:latest' container. The container executes a 'ping' command to '8.8.8.8'. This is used for testing Kubernetes setup.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: demo
spec:
  containers:
    - name: testpod
      image: alpine:latest
      command: ["ping", "8.8.8.8"]

```

--------------------------------

### Search for Official Nginx Image using Docker CLI

Source: https://docs.docker.com/docker-hub/quickstart

This command searches Docker Hub for official images related to 'nginx'. It filters results to include only official images, ensuring higher quality and security. The output lists available nginx images.

```bash
docker search --filter is-official=true nginx
```

--------------------------------

### Stop container and remove network

Source: https://docs.docker.com/engine/network/drivers/macvlan

Stops a running Docker container and removes the macvlan network created for the 802.1Q trunked bridge mode example. This is a cleanup step to revert the changes made during the setup.

```console
docker container stop my-second-macvlan-alpine
docker network rm my-8021q-macvlan-net
```

--------------------------------

### Dockerignore File Syntax Examples

Source: https://docs.docker.com/build/concepts/context

Illustrates the syntax and behavior of patterns within a .dockerignore file. It covers basic exclusion rules, negation with '!', and how the order of rules affects the final outcome. These patterns are processed using Go's filepath.Match rules.

```text
# comment
*/temp*
*/*/temp*
temp?

```

```text
*.md
!README.md

```

```text
*.md
!README*.md
README-secret.md

```

```text
*.md
README-secret.md
!README*.md

```

--------------------------------

### Docker Plugin API Call Format (curl 7.5+)

Source: https://docs.docker.com/engine/extend

This example demonstrates the URL format for making API calls to Docker plugins using curl version 7.5 and above. It specifies the structure `http://hostname/APICall`, where `hostname` is the server where the plugin is installed and `APICall` is the specific API endpoint.

```console
http://localhost/VolumeDriver.List
```

--------------------------------

### Run Docker Hardened Python Image

Source: https://docs.docker.com/dhi/get-started

Executes a command within a container created from the Python DHI. This confirms the image is functional and can run Python code.

```console
docker run --rm dhi.io/python:3.13 python -c "print('Hello from DHI')"
```

--------------------------------

### Docker Build Overview

Source: https://docs.docker.com/llms

This documentation provides a high-level overview of Docker Build and its components. It explains the core concepts and functionalities of the Docker Build system.

```markdown
Docker Build is the process of creating a Docker image from a Dockerfile. It involves several key components:

*   **Dockerfile**: A text file containing instructions to build an image.
*   **Build Context**: The set of files sent to the Docker daemon for the build.
*   **Docker Daemon**: The background service that manages Docker objects like images, containers, networks, and volumes.
*   **BuildKit**: An enhanced builder backend for Docker that provides features like parallel build execution, caching, and advanced build features.

The build process typically involves the daemon receiving the build context and Dockerfile, executing the instructions, and creating a new image layer by layer. BuildKit optimizes this process for speed and efficiency.
```

--------------------------------

### Install Docker Desktop on Arch-based Linux Distributions

Source: https://docs.docker.com/llms

Instructions for installing Docker Desktop on Arch-based Linux distributions using the provided Arch package. This is intended for users who want to experiment with Docker Desktop on various Arch derivatives.

```bash
# Example using yay (an AUR helper):
yay -S docker-desktop
```

--------------------------------

### Example dig command output

Source: https://docs.docker.com/get-started/workshop/07_multi_container

This is an example output from the 'dig mysql' command, showing the DNS resolution process and the 'A' record that maps the 'mysql' hostname to its container's IP address.

```text
; <<>> DiG 9.18.8 <<>> mysql
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 32162
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;mysql.			IN	A

;; ANSWER SECTION:
mysql.			600	IN	A	172.23.0.2

;; Query time: 0 msec
;; SERVER: 127.0.0.11#53(127.0.0.11)
;; WHEN: Tue Oct 01 23:47:24 UTC 2019
;; MSG SIZE  rcvd: 44
```

--------------------------------

### Deploy to Docker Swarm

Source: https://docs.docker.com/llms

This guide explains how to describe and deploy a simple application on Docker Swarm. It covers the basics of using Docker Swarm for orchestration.

```YAML
# Example docker-compose.yml for Docker Swarm
version: '3.8'

services:
  web:
    image: nginx:latest
    ports:
      - "80:80"
    deploy:
      replicas: 3

networks:
  default:
    driver: overlay
```

--------------------------------

### Compare Docker Images with Docker Scout

Source: https://docs.docker.com/dhi/get-started

Compares a Docker Hardened Image (DHI) with a non-hardened Docker Official Image. This command helps visualize security improvements, size reduction, and package count differences. It filters the output to show only the overview section.

```console
$ docker scout compare dhi.io/python:3.13 \
    --to python:3.13 \
    --platform linux/amd64 \
    --ignore-unchanged \
    2>/dev/null | sed -n '/## Overview/,/^  ## /p' | head -n -1
```

--------------------------------

### Go: Customize Docker Compose SDK Options

Source: https://docs.docker.com/compose/compose-sdk

Demonstrates how to create a Docker Compose service instance with custom options, such as redirecting output streams, setting concurrency limits, and configuring prompt behavior. These options allow fine-grained control over the SDK's operation.

```go
import (
    "bytes"
    "os"

    "github.com/docker/cli/cli/command"
    "github.com/docker/compose/v5/pkg/compose"
)

// Assuming dockerCLI is already initialized as shown in the previous example
var dockerCLI *command.DockerCli

// Create a custom output buffer to capture logs
var outputBuffer bytes.Buffer

// Create a compose service with custom options
service, err := compose.NewComposeService(dockerCLI,
    compose.WithOutputStream(&outputBuffer),          // Redirect output to custom writer
    compose.WithErrorStream(os.Stderr),               // Use stderr for errors
    compose.WithMaxConcurrency(4),                    // Limit concurrent operations
    compose.WithPrompt(compose.AlwaysOkPrompt()),     // Auto-confirm all prompts
)
```

--------------------------------

### Install Docker Rootless Extras Package

Source: https://docs.docker.com/engine/security/rootless

Installs the `docker-ce-rootless-extras` package using apt-get, which provides the necessary tools for running Docker in rootless mode when the main installation script is not available.

```bash
$ sudo apt-get install -y docker-ce-rootless-extras
```

--------------------------------

### Started On (runDetails.metadata.startedOn)

Source: https://docs.docker.com/build/metadata/attestations/slsa-definitions

Timestamp indicating when the build started. This field is included when `mode=min` and `mode=max`.

```APIDOC
## Started On (runDetails.metadata.startedOn)

### Description
Timestamp when the build started.

### Method
N/A (Run detail field)

### Endpoint
N/A

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
- **runDetails.metadata.startedOn** (string) - Required - Timestamp when the build started (ISO 8601 format).

### Request Example
```json
{
  "runDetails": {
    "metadata": {
      "startedOn": "2021-11-17T15:00:00Z"
    }
  }
}
```

### Response
#### Success Response (200)
N/A (Run detail field)

#### Response Example
N/A
```

--------------------------------

### Run Node.js App in Docker Container with Bind Mount (Git Bash CLI)

Source: https://docs.docker.com/get-started/workshop/06_bind_mounts

This command runs a Node.js application in a Docker container. It maps host port 3000 to container port 3000, sets the working directory to `/app` inside the container, and uses a bind mount to sync the current directory on the host to `/app` in the container. It installs npm dependencies and starts the development server using `npm run dev`.

```bash
docker run -dp 127.0.0.1:3000:3000 \
    -w //app --mount type=bind,src="/.",target=/app \
    node:24-alpine \
    sh -c "npm install && npm run dev"
```

--------------------------------

### Docker Run Command with -v for Bind Mount

Source: https://docs.docker.com/storage/bind-mounts

This command achieves the same result as the `--mount` example by starting a detached Nginx container and bind-mounting a local directory's 'target' subdirectory to '/app' using the `-v` flag. It also includes options for interactive and pseudo-TTY access.

```bash
$ docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app \
  nginx:latest

```

--------------------------------

### Install a specific version of Docker Engine

Source: https://docs.docker.com/engine/install/ubuntu

Installs a specific version of Docker Engine by first listing available versions and then specifying the desired version string during the apt install command.

```console
$ apt list --all-versions docker-ce

docker-ce/noble 5:29.2.1-1~ubuntu.24.04~noble <arch>
docker-ce/noble 5:29.2.0-1~ubuntu.24.04~noble <arch>
...

$ VERSION_STRING=5:29.2.1-1~ubuntu.24.04~noble
$ sudo apt install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-buildx-plugin docker-compose-plugin
```

--------------------------------

### Run Ubuntu Container with Bind Mount (Mac/Linux)

Source: https://docs.docker.com/get-started/workshop/06_bind_mounts

Starts an interactive bash session in an Ubuntu container, mounting the current host directory to `/src` inside the container. This allows for real-time file synchronization between the host and the container.

```console
docker run -it --mount type=bind,src=.,target=/src ubuntu bash
```

--------------------------------

### Pre-seed Database with Schema and Data in Docker

Source: https://docs.docker.com/llms

Learn how to pre-seed a database with schema and data at startup for a development environment using Docker. This is useful for setting up initial database states.

```Shell
# Example script to pre-seed a PostgreSQL database
# Assumes you have a docker-compose.yml setting up PostgreSQL

# Create schema script
cat <<EOF > ./init/init.sql
CREATE TABLE users (id SERIAL PRIMARY KEY, name VARCHAR(100));
INSERT INTO users (name) VALUES ('Alice'), ('Bob');
EOF

# In your docker-compose.yml for PostgreSQL:
# volumes:
#   - ./init:/docker-entrypoint-initdb.d
```

--------------------------------

### Install latest stable Docker using convenience script

Source: https://docs.docker.com/engine/install/fedora

This command downloads the Docker convenience script from get.docker.com and executes it with sudo privileges. It installs the latest stable release of Docker, containerd, and runc on your Linux system.

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

--------------------------------

### Reading Docker Compose Configuration from Stdin

Source: https://docs.docker.com/compose/how-tos/multiple-compose-files/merge

This example demonstrates how to pipe Docker Compose configuration directly from stdin using the `-f -` flag. Paths within the configuration are relative to the current working directory when stdin is used. This is useful for dynamic or scripted Compose setups.

```console
docker compose -f - <<EOF
  webapp:
    image: examples/web
    ports:
     - "8000:8000"
    volumes:
     - "/data"
    environment:
     - DEBUG=1
EOF
```

--------------------------------

### Create a Docker Volume with Local Driver Options (btrfs)

Source: https://docs.docker.com/reference/cli/docker/volume/create

This example demonstrates creating a Docker volume with the 'local' driver and specifying 'btrfs' as the filesystem type, along with the device path for the btrfs partition.

```console
docker volume create --driver local \
    --opt type=btrfs \
    --opt device=/dev/sda2 \
    foo
```

--------------------------------

### Example: Docker --volume with Read-Only and Bind Propagation

Source: https://docs.docker.com/storage/bind-mounts

This example shows how to use the `-v` flag for a bind mount, including the source and destination paths, and specifying read-only and shared bind propagation options.

```bash
$ docker run -v .:/project:ro,rshared

```

--------------------------------

### Define Container Start Command (Dockerfile)

Source: https://docs.docker.com/build/concepts/dockerfile

Sets the command to run when a container starts. Supports both 'exec' and 'shell' forms, with differences in signal handling. The 'exec' form is generally preferred for better signal management.

```dockerfile
CMD ["flask", "run", "--host", "0.0.0.0", "--port", "8000"]
```

```dockerfile
CMD flask run --host 0.0.0.0 --port 8000
```

--------------------------------

### Install Docker Desktop in Passive Mode (PowerShell)

Source: https://docs.docker.com/enterprise/enterprise-deployment/msi-install-and-configure

Performs a non-interactive installation of Docker Desktop while displaying a progress dialog. The `/passive` option ensures no user prompts or error messages appear, and the installation cannot be cancelled.

```powershell
msiexec /i "DockerDesktop.msi" /L*V ".\msi.log" /passive /norestart
```

--------------------------------

### Build Golang Server for Prometheus Metrics

Source: https://docs.docker.com/llms

Learn how to create a Golang server that registers metrics with Prometheus. This guide covers the application development aspect for monitoring.

```go
package main

import (
	"net/http"

	"github.com/prometheus/client_golang/prometheus"
	"github.com/prometheus/client_golang/prometheus/promauto"
	"github.com/prometheus/client_golang/prometheus/promhttp"
)

var ( 
	myGauge = promauto.NewGauge(prometheus.GaugeOpts{
		Name: "my_gauge_value",
		Help: "A sample gauge metric.",
	})
)

func myHandler(w http.ResponseWriter, r *http.Request) {
	myGauge.Set(123.45)
	// Your application logic here
}

func main() {
	http.Handle("/metrics", promhttp.Handler())
	http.HandleFunc("/", myHandler)
	http.ListenAndServe(":8080", nil)
}
```

--------------------------------

### Verify Docker Compose Installation

Source: https://docs.docker.com/compose/install/linux

Checks if the Docker Compose plugin has been installed correctly by displaying its version. This command should be run after either the repository-based or manual installation method.

```bash
$ docker compose version
```

--------------------------------

### Display Docker Command Help

Source: https://docs.docker.com/engine/reference/commandline/cli

This snippet demonstrates how to display detailed help text for any Docker command by appending the `--help` option. It shows an example for the `docker run` command, illustrating its usage and available options.

```bash
$ docker run --help

Usage: docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Create and run a new container from an image

Options:
      --add-host value             Add a custom host-to-IP mapping (host:ip) (default [])
  -a, --attach value               Attach to STDIN, STDOUT or STDERR (default [])
<...>

```

--------------------------------

### Configure Docker Storage Drivers (OverlayFS, BTRFS, ZFS)

Source: https://docs.docker.com/llms

This snippet demonstrates how to configure different storage drivers for Docker, such as OverlayFS, BTRFS, and ZFS. Choosing the right driver can impact performance and storage efficiency.

```json
{
  "storage-driver": "overlay2"
}

```

```json
{
  "storage-driver": "btrfs"
}

```

```json
{
  "storage-driver": "zfs"
}

```

--------------------------------

### Install Docker Desktop PKG from Command Line (macOS)

Source: https://docs.docker.com/enterprise/enterprise-deployment/pkg-install-and-configure

This command installs the Docker Desktop PKG installer from the command line on macOS. It requires administrator privileges and specifies the target directory for installation. Ensure the path to the Docker.pkg file is correct.

```bash
sudo installer -pkg "/path/to/Docker.pkg" -target /

```

--------------------------------

### Docker Compose YAML Example

Source: https://docs.docker.com/reference/cli/docker/compose/pull

An example 'compose.yaml' file demonstrating service definitions, including image sources and build configurations, used in conjunction with 'docker compose pull'.

```yaml
services:
  db:
    image: postgres
  web:
    build: .
    command: bundle exec rails s -p 3000 -b '0.0.0.0'
    volumes:
      - .:/myapp
    ports:
      - "3000:3000"
    depends_on:
      - db
```

--------------------------------

### Configure CI/CD for Rust Applications

Source: https://docs.docker.com/llms

This guide explains how to set up Continuous Integration and Continuous Deployment (CI/CD) for your Rust application. It covers automating builds and tests.

```YAML
# Example GitHub Actions workflow for Rust
name: Rust CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Build
      run: cargo build --verbose
    - name: Run tests
      run: cargo test --verbose
```

--------------------------------

### Build Alpine Base Image with Bash

Source: https://docs.docker.com/engine/storage/drivers

This Dockerfile uses the 'alpine' base image and installs the 'bash' package. It's a common starting point for minimal Linux environments requiring shell access.

```dockerfile
# syntax=docker/dockerfile:1
FROM alpine
RUN apk add --no-cache bash
```

--------------------------------

### Start Docker Service

Source: https://docs.docker.com/engine/storage/drivers/device-mapper-driver

Commands to start the Docker service using either systemd or the older service command. These commands require superuser privileges.

```shell
sudo systemctl start docker
```

```shell
sudo service docker start
```

--------------------------------

### Start Docker Buildx Build

Source: https://docs.docker.com/engine/reference/commandline/buildx_build

Initiates a build process using Docker BuildKit. This command allows for advanced build configurations and options. It requires a build context path, URL, or '-' for stdin.

```bash
docker buildx build [OPTIONS] PATH | URL | -
```

--------------------------------

### Start Development Environment with Docker Compose (Bash)

Source: https://docs.docker.com/get-started/introduction/develop-with-containers

Starts the development environment for the project using Docker Compose. This command pulls necessary container images, starts containers, and sets up the application services. The output indicates the progress of container orchestration.

```bash
$ docker compose watch
```

--------------------------------

### Create and Use Docker Volume Mounts

Source: https://docs.docker.com/engine/containers/run

This example shows how to create a Docker volume mount and use it for persistent data storage. First, a container writes data to a file within a volume named 'my_volume' mounted at '/foo'. Then, another container mounts the same volume at '/bar' and displays the content of the file, demonstrating data persistence.

```console
docker run --rm --mount source=my_volume,target=/foo busybox \
  echo "hello, volume!" > /foo/hello.txt
docker run --mount source=my_volume,target=/bar busybox
  cat /bar/hello.txt
```

--------------------------------

### Docker Build Process Output (Cached)

Source: https://docs.docker.com/get-started/docker-concepts/building-images/using-the-build-cache

Example output of a subsequent Docker build process after the initial one. It highlights the significantly reduced build time due to the utilization of cached layers, skipping time-consuming steps like dependency installation.

```console
[+] Building 1.0s (9/9) FINISHED                                                                            docker:desktop-linux
 => [internal] load build definition from Dockerfile                                                                        0.0s
 => => transferring dockerfile: 187B                                                                                        0.0s
 ...
 => [internal] load build context                                                                                           0.0s
 => => transferring context: 8.16kB                                                                                         0.0s
 => CACHED [2/4] WORKDIR /app                                                                                               0.0s
 => CACHED [3/4] COPY . .                                                                                                   0.0s
 => CACHED [4/4] RUN yarn install --production                                                                              0.0s
 => exporting to image                                                                                                      0.0s
 => => exporting layers                                                                                                     0.0s
 => => exporting manifest
```

--------------------------------

### Configure Xdebug Dynamically

Source: https://docs.docker.com/guides/frameworks/laravel/development-setup

Conditionally installs and enables the Xdebug extension based on the XDEBUG_ENABLED build argument. It configures Xdebug settings like mode, IDE key, log file, log level, and client host via environment variables passed during the build process.

```dockerfile
ARG XDEBUG_ENABLED
ARG XDEBUG_MODE
ARG XDEBUG_HOST
ARG XDEBUG_IDE_KEY
ARG XDEBUG_LOG
ARG XDEBUG_LOG_LEVEL

RUN if [ "${XDEBUG_ENABLED}" = "true" ]; then \
    pecl install xdebug && \
    docker-php-ext-enable xdebug && \
    echo "xdebug.mode=${XDEBUG_MODE}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.idekey=${XDEBUG_IDE_KEY}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.log=${XDEBUG_LOG}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.log_level=${XDEBUG_LOG_LEVEL}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini && \
    echo "xdebug.client_host=${XDEBUG_HOST}" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini ; \
    echo "xdebug.start_with_request=yes" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini ; \
fi
```

--------------------------------

### Set Environment Variables with Docker Exec

Source: https://docs.docker.com/engine/reference/commandline/exec

This example shows how to set environment variables specifically for a command executed using 'docker exec'. The variables are only applied to the process started by 'docker exec' and do not affect other processes within the container.

```bash
# Start an interactive shell in 'mycontainer' with VAR_A and VAR_B set
docker exec -e VAR_A=1 -e VAR_B=2 mycontainer env
# Expected output will include:
# VAR_A=1
# VAR_B=2
```

--------------------------------

### Use ENTRYPOINT with a Helper Script

Source: https://docs.docker.com/build/building/best-practices

Combines ENTRYPOINT with a shell script to handle complex initialization steps before executing the main command. The script uses 'exec' to ensure the application becomes PID 1.

```bash
#!/bin/bash
set -e

if [ "$1" = 'postgres' ]; then
    chown -R postgres "$PGDATA"

    if [ -z "$(ls -A \"$PGDATA\")" ]; then
        gosu postgres initdb
    fi

    exec gosu postgres "$@"
fi

exec "$@"
```

--------------------------------

### Create Ubuntu Base Image using Tar

Source: https://docs.docker.com/build/building/base-images

This example shows how to create a full Ubuntu base image by using debootstrap to create a root filesystem, then packaging it as a tar archive and importing it into Docker. It demonstrates creating a distribution-specific base image.

```bash
$ sudo debootstrap noble noble > /dev/null
$ sudo tar -C noble -c . | docker import - noble

sha256:81ec9a55a92a5618161f68ae691d092bf14d700129093158297b3d01593f4ee3

$ docker run noble cat /etc/lsb-release
```

--------------------------------

### Docker run options

Source: https://docs.docker.com/engine/deprecated

Illustrates the replacement of various deprecated single-dash options for 'docker run' with their double-dash equivalents, such as --cidfile, --dns, --entrypoint, --expose, --link, --volumes-from.

```console
# Deprecated:
# docker run -cidfile file.txt IMAGE
# docker run -dns 8.8.8.8 IMAGE
# docker run -entrypoint /bin/bash IMAGE
# docker run -expose 80 IMAGE
# docker run -link name:alias IMAGE
# docker run -volumes-from other_container IMAGE

# Recommended:
docker run --cidfile file.txt IMAGE
docker run --dns 8.8.8.8 IMAGE
docker run --entrypoint /bin/bash IMAGE
docker run --expose 80 IMAGE
docker run --link name:alias IMAGE
docker run --volumes-from other_container IMAGE
```

--------------------------------

### Dockerfile Cache Mounts Example

Source: https://docs.docker.com/build/ci/github-actions/cache

Example Dockerfile demonstrating the use of cache mounts for Go module downloads and build caches. It utilizes `--mount=type=cache` for efficient caching of Go build artifacts.

```Dockerfile
FROM golang:1.21.1-alpine as base-build

WORKDIR /build

RUN --mount=type=cache,target=/go/pkg/mod \
    --mount=type=bind,source=go.mod,target=go.mod \
    --mount=type=bind,source=go.sum,target=go.sum \
    go mod download

RUN --mount=type=cache,target=/go/pkg/mod \
    --mount=type=cache,target=/root/.cache/go-build \
    --mount=type=bind,target=. \
    go build -o /bin/app ./src
```

--------------------------------

### Version pinning with apt-get install

Source: https://docs.docker.com/build/building/best-practices

Demonstrates version pinning for a package (`s3cmd=1.1.*`) within a combined `apt-get update` and `apt-get install` RUN statement. This ensures a specific version is installed, acting as a cache bust and improving build stability.

```dockerfile
RUN apt-get update && apt-get install -y --no-install-recommends \
    package-bar \
    package-baz \
    package-foo=1.3.*
```

--------------------------------

### Docker Desktop Lifecycle Management

Source: https://docs.docker.com/llms

Start, stop, restart, and update Docker Desktop.

```APIDOC
## docker desktop restart

### Description
Restarts the Docker Desktop application.

### Method
CLI Command

### Endpoint
docker desktop restart

## docker desktop start

### Description
Starts the Docker Desktop application if it is not running.

### Method
CLI Command

### Endpoint
docker desktop start

## docker desktop stop

### Description
Stops the Docker Desktop application.

### Method
CLI Command

### Endpoint
docker desktop stop

## docker desktop update

### Description
Checks for and applies updates to Docker Desktop.

### Method
CLI Command

### Endpoint
docker desktop update

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
docker desktop start
```

### Response
#### Success Response (0)
Confirmation message indicating the action taken.

#### Response Example
```
Docker Desktop started.
```
```

--------------------------------

### Create Docker Bind Mount

Source: https://docs.docker.com/reference/run

Illustrates how to create a bind mount using `docker run` with the `--mount` flag. It specifies the type as 'bind', the source path on the host, and the target path inside the container. Changes made within the container to the mounted directory are reflected on the host.

```bash
$ docker run -it --mount type=bind,source=[PATH],target=[PATH] busybox

```

```bash
$ docker run -it --mount type=bind,source=.,target=/foo busybox
/ # echo "hello from container" > /foo/hello.txt
/ # exit
$ cat hello.txt
hello from container

```

--------------------------------

### Install Docker Extension

Source: https://docs.docker.com/extensions/extensions-sdk/build/minimal-frontend-extension

Command to install the built Docker extension into Docker Desktop. After installation, the extension will appear in the Docker Desktop Dashboard.

```bash
$ docker extension install awesome-inc/my-extension:latest
```

--------------------------------

### Create PHP-CLI Dockerfile for Production

Source: https://docs.docker.com/guides/frameworks/laravel/production-setup

This Dockerfile sets up a production PHP-CLI environment, suitable for running Artisan commands and migrations. It uses a multi-stage build process, first installing dependencies and Composer packages in a 'builder' stage, then copying the necessary components to a clean production image.

```dockerfile
# Stage 1: Build environment and Composer dependencies
FROM php:8.5-cli AS builder

# Install system dependencies and PHP extensions required for Laravel + MySQL/PostgreSQL support
# Some dependencies are required for PHP extensions only in the build stage
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    unzip \
    libpq-dev \
    libonig-dev \
    libssl-dev \
    libxml2-dev \
    libcurl4-openssl-dev \
    libicu-dev \
    libzip-dev \
    && docker-php-ext-install -j$(nproc) \
    pdo_mysql \
    pdo_pgsql \
    pgsql \
    intl \
    zip \
    bcmath \
    soap \
    && pecl install redis \
    && docker-php-ext-enable redis \
    && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set the working directory inside the container
WORKDIR /var/www

# Copy the entire Laravel application code into the container
COPY . /var/www

# Install Composer and dependencies
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer install --no-dev --optimize-autoloader --no-interaction --no-progress --prefer-dist

# Stage 2: Production environment
FROM php:8.5-cli

# Install client libraries required for php extensions in runtime
RUN apt-get update && apt-get install -y --no-install-recommends \
    libpq-dev \
    libicu-dev \
    libzip-dev \
    && apt-get autoremove -y && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Copy PHP extensions and libraries from the builder stage
COPY --from=builder /usr/local/lib/php/extensions/ /usr/local/lib/php/extensions/
COPY --from=builder /usr/local/etc/php/conf.d/ /usr/local/etc/php/conf.d/
COPY --from=builder /usr/local/bin/docker-php-ext-* /usr/local/bin/

# Use the default production configuration for PHP runtime arguments
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"

# Copy the application code and dependencies from the build stage
COPY --from=builder /var/www /var/www

# Set working directory
WORKDIR /var/www

# Ensure correct permissions
RUN chown -R www-data:www-data /var/www

# Switch to the non-privileged user to run the application
USER www-data

# Default command: Provide a bash shell to allow running any command
CMD ["bash"]

```

--------------------------------

### Docker Pull Command Example

Source: https://docs.docker.com/admin/organization/image-access

Demonstrates how to pull an image using the Docker CLI. This example shows pulling a Docker Official Image, which will succeed if Docker Official Images are allowed by the Image Access Management policy.

```bash
$ docker pull nginx  # Docker Official Image
# Pull succeeds if Docker Official Images are allowed
```

--------------------------------

### Build Multi-Arch Image with QEMU (Docker CLI)

Source: https://docs.docker.com/build/builders/drivers/kubernetes

Builds a multi-architecture Docker image (e.g., amd64 and arm64) using the Kubernetes driver and QEMU for emulation. This command targets specific platforms and pushes the resulting image.

```console
docker buildx build \
  --builder=kube \
  --platform=linux/amd64,linux/arm64 \
  -t <user>/<image> \
  --push .
```

--------------------------------

### Enable Synchronized File Shares in Docker Desktop

Source: https://docs.docker.com/llms

Get started with synchronized file shares on Docker Desktop. This feature allows seamless sharing of files between your host machine and containers, improving development workflows by enabling live code updates without rebuilding images.

```bash
# Example: Mounting a local directory into a container
docker run -v /path/on/host:/path/in/container nginx
```

--------------------------------

### Node.js Dockerfile Migration to Docker Hardened Images (Wolfi)

Source: https://docs.docker.com/dhi/migration/examples/node

This Dockerfile example demonstrates a Node.js application before migrating to Docker Hardened Images, utilizing a Wolfi distribution image. It includes steps for setting the work directory, copying package JSON, installing npm packages, copying the rest of the application code, and specifying the entry point.

```dockerfile
#syntax=docker/dockerfile:1

FROM cgr.dev/chainguard/node:latest-dev
WORKDIR /usr/src/app

COPY package*.json ./

# Install any additional packages if needed using apk
# RUN apk add --no-cache python3 make g++

RUN npm install

COPY . .

CMD ["node", "index.js"]
```

--------------------------------

### Run Command Directly in Container using Docker Debug

Source: https://docs.docker.com/reference/cli/docker/debug

Execute a command directly within a specified Docker image without starting an interactive session. This is useful for scripting and quick checks. The output of the command is displayed.

```console
$ docker debug --command "cat /usr/share/nginx/html/index.html" nginx

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

--------------------------------

### Expose host devices to Linux containers (--device)

Source: https://docs.docker.com/reference/cli/docker/container/run

Demonstrates how to expose host devices like block storage or character devices to a Linux container using the --device flag. It shows mapping specific devices and their permissions.

```console
$ docker run -it --rm \
    --device=/dev/sdc:/dev/xvdc \
    --device=/dev/sdd \
    --device=/dev/zero:/dev/foobar \
    ubuntu ls -l /dev/{xvdc,sdd,foobar}

brw-rw---- 1 root disk 8, 2 Feb  9 16:05 /dev/xvdc
brw-rw---- 1 root disk 8, 3 Feb  9 16:05 /dev/sdd
crw-rw-rw- 1 root root 1, 5 Feb  9 16:05 /dev/foobar
```

```console
$ docker run --device=/dev/sda:/dev/xvdc --rm -it ubuntu fdisk  /dev/xvdc

Command (m for help): q
```

```console
$ docker run --device=/dev/sda:/dev/xvdc:r --rm -it ubuntu fdisk  /dev/xvdc
You will not be able to write the partition table.

Command (m for help): q

$ docker run --device=/dev/sda:/dev/xvdc:rw --rm -it ubuntu fdisk  /dev/xvdc

Command (m for help): q

$ docker run --device=/dev/sda:/dev/xvdc:m --rm -it ubuntu fdisk  /dev/xvdc
fdisk: unable to open /dev/xvdc: Operation not permitted
```

--------------------------------

### Git Commands for Repository Setup

Source: https://docs.docker.com/guides/dotnet/configure-ci-cd

These console commands are used to configure your local Git repository to point to a new GitHub repository, rename the default branch to 'main', and push your initial commit.

```console
$ git remote set-url origin https://github.com/your-username/your-repository.git
$ git branch -M main
$ git add -A
$ git commit -m "my first commit"
$ git push -u origin main
```

--------------------------------

### Enable QEMU Installation for Kubernetes Builder

Source: https://docs.docker.com/build/drivers/kubernetes

This command creates a Kubernetes Buildx builder and explicitly enables QEMU installation. This is necessary when using custom BuildKit images or non-native binaries that require QEMU for multi-platform builds.

```bash
$ docker buildx create \
  --bootstrap \
  --name=kube \
  --driver=kubernetes \
  --driver-opt=namespace=buildkit,qemu.install=true

```

--------------------------------

### Check Docker and Docker Compose versions

Source: https://docs.docker.com/desktop/setup/install/linux/fedora

Verifies the installed versions of Docker Compose and the Docker CLI. This is useful after installation to confirm that the binaries have been updated correctly.

```bash
$ docker compose version
Docker Compose version v2.39.4

$ docker --version
Docker version 28.4.0, build d8eb465

$ docker version
Client:
 Version:           28.4.0
 API version:       1.51
 Go version:        go1.24.7
<...>
```

--------------------------------

### Python Flask App with Redis Connection

Source: https://docs.docker.com/compose/gettingstarted

The main application logic written in Python using the Flask framework. It connects to a Redis instance to increment and retrieve a hit counter. Includes basic error handling for Redis connection.

```python
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)

def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)

@app.route('/')
def hello():
    count = get_hit_count()
    return f'Hello World! I have been seen {count} times.\n'

```

--------------------------------

### Initialize Private Marketplace Folder and Navigate

Source: https://docs.docker.com/desktop/extensions/private-marketplace

Creates a local directory for marketplace content and changes the current directory into it. This is the first step in setting up the private marketplace.

```bash
$ mkdir my-marketplace
$ cd my-marketplace
```

--------------------------------

### List Docker Contexts

Source: https://docs.docker.com/desktop/setup/install/linux

This command lists all available Docker contexts on the machine. The current context is indicated by an asterisk (*). This helps in managing and switching between different Docker environments.

```bash
docker context ls
```

--------------------------------

### Update Container Restart Policy

Source: https://docs.docker.com/reference/cli/docker/container/update

This example demonstrates how to change a container's restart policy to `on-failure` with a maximum of 3 retries. The change takes effect immediately for running containers. This option cannot be used with containers started with the `--rm` flag.

```console
docker update --restart=on-failure:3 abebf7571666 hopeful_morse
```

--------------------------------

### Dockerfile Example for GPU Usage

Source: https://docs.docker.com/build/building/cdi

A basic Dockerfile demonstrating how to utilize GPU devices within a container. This snippet is intended to be used with a GPU-enabled Buildx builder to perform tasks that can leverage GPU acceleration.

```dockerfile
FROM nvidia/cuda:11.0-base

# Example command to use GPU
RUN nvidia-smi
```

--------------------------------

### Compose Build Specification Example (YAML)

Source: https://docs.docker.com/compose/compose-file/build

An example demonstrating the Compose Build Specification, showing how to define build contexts and Dockerfile locations for services. It illustrates building images from source and specifies image names for publishing.

```yaml
services:
  frontend:
    image: example/webapp
    build: ./webapp

  backend:
    image: example/database
    build:
      context: backend
      dockerfile: ../backend.Dockerfile

  custom:
    build: ~/custom
```

--------------------------------

### Install Python SDK for Docker

Source: https://docs.docker.com/reference/api/engine/sdk

Installs the Python SDK for Docker using pip. Alternatively, it can be installed by downloading the package directly and running setup.py install.

```bash
pip install docker
```

--------------------------------

### Start Alpine Container with Limited Log Size and Files (Console)

Source: https://docs.docker.com/engine/logging/drivers/json-file

This example demonstrates how to run an Alpine container with specific logging configurations. It limits the maximum size of log files to 10 megabytes each and sets a maximum of 3 log files. This is useful for managing disk space and log rotation.

```console
$ docker run -it --log-opt max-size=10m --log-opt max-file=3 alpine ash
```

--------------------------------

### Deploy Services to a Docker Swarm

Source: https://docs.docker.com/llms

This example shows how to deploy services to a Docker Swarm cluster. Swarm mode enables you to manage a cluster of Docker Engines as a single, virtual Docker host.

```bash
# Initialize a swarm (on manager node)
docker swarm init

# Deploy a service
docker service create --name my-web-server -p 80:80 nginx

# Scale a service
docker service scale my-web-server=5

```

--------------------------------

### Build Cross-Platform Binaries with Buildx Bake (Console)

Source: https://docs.docker.com/guides/bake

This command executes the 'bin-cross' target, building the binary for all specified platforms. The output will be organized into subdirectories within './build/' for each platform variant.

```bash
docker buildx bake bin-cross
```

--------------------------------

### Multi-line RUN statement with apt-get install

Source: https://docs.docker.com/build/building/best-practices

Demonstrates splitting a long RUN statement for `apt-get update` and `apt-get install` across multiple lines using backslashes for improved Dockerfile readability and maintainability.

```dockerfile
RUN apt-get update && apt-get install -y --no-install-recommends \
    package-bar \
    package-baz \
    package-foo
```

--------------------------------

### Dockerfile Overview

Source: https://docs.docker.com/llms

This documentation provides an overview of Dockerfiles. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Docker uses Dockerfiles to build images.

```markdown
A Dockerfile is a text file that contains a series of instructions for building a Docker image. Each instruction creates a new layer in the image. Dockerfiles support a wide range of instructions, including:

*   `FROM`: Specifies the base image for the build.
*   `RUN`: Executes commands in a new layer on top of the current image.
*   `COPY`: Copies files from the build context into the image.
*   `ADD`: Similar to `COPY`, but with additional features like URL downloading and tar extraction.
*   `CMD`: Provides defaults for an executing container.
*   `EXPOSE`: Informs Docker that the container listens on the specified network ports at runtime.
*   `WORKDIR`: Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions that follow.

Example Dockerfile:

```dockerfile
# Use an official Ubuntu runtime as a parent image
FROM ubuntu:latest

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Install any needed packages specified in requirements.txt
RUN apt-get update && apt-get install -y --no-install-recommends some-package

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```
```

--------------------------------

### Node.js Dockerfile Migration to Docker Hardened Images (Ubuntu)

Source: https://docs.docker.com/dhi/migration/examples/node

This Dockerfile example shows a Node.js application before migration to Docker Hardened Images, using an Ubuntu-based image. It sets up the working directory, copies package files, installs dependencies, copies application code, and defines the command to run the application.

```dockerfile
#syntax=docker/dockerfile:1

FROM ubuntu/node:18-24.04_edge
WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

CMD ["node", "index.js"]
```

--------------------------------

### Create Container Response Example

Source: https://docs.docker.com/reference/api/engine/latest

Example of a successful response when creating a Docker container.

```APIDOC
### Responses
#### Success Response (201)
- **Id** (string) - The ID of the created container.
- **Warnings** (array of strings) - Any warnings generated during container creation.

#### Response Example
```json
{
  "Id": "ede54ee1afda366ab42f824e8a5ffd195155d853ceaec74a927f249ea270c743",
  "Warnings": [ ]
}
```
```

--------------------------------

### Verify Docker Installation and Status

Source: https://docs.docker.com/engine/install/debian

Verifies that the Docker Engine is installed and running correctly. It checks the service status and runs the 'hello-world' container to confirm Docker's operational capability.

```console
$ sudo systemctl status docker
$ sudo docker run hello-world
```

--------------------------------

### Dockerfile using OCI layout build context

Source: https://docs.docker.com/reference/cli/docker/build

Dockerfile example showing how to use an OCI layout directory as a build context named 'foo'. It demonstrates using the context in a FROM instruction and copying a file from it.

```dockerfile
# syntax=docker/dockerfile:1
FROM alpine
RUN apk add git
COPY --from=foo myfile /

FROM foo

```

--------------------------------

### Verify Docker Installation and Status

Source: https://docs.docker.com/engine/install/raspberry-pi-os

Commands to verify the Docker installation and check its running status. It includes running the 'hello-world' container to confirm Docker is functioning correctly and checking the systemd service status.

```bash
# Verify Docker is running:
sudo systemctl status docker

# Start Docker if disabled:
sudo systemctl start docker

# Run the hello-world image:
sudo docker run hello-world
```

--------------------------------

### Example Docker Build Command

Source: https://docs.docker.com/build/bake/reference

This snippet shows a standard `docker build` command executed from the command line. It includes options for specifying the Dockerfile, tagging the image, and providing the build context.

```bash
$ docker build \
  --file=Dockerfile.webapp \
  --tag=docker.io/username/webapp:latest \
  https://github.com/username/webapp
```

--------------------------------

### PHP-FPM Entrypoint Script

Source: https://docs.docker.com/guides/frameworks/laravel/production-setup

This shell script serves as the entrypoint for the PHP-FPM container in a production environment. It first executes a health check script to ensure PHP-FPM is ready, then copies initial storage files, and finally starts the PHP-FPM process. This script ensures proper initialization before the application becomes fully available.

```bash
#!/bin/sh

# Wait for PHP-FPM to be ready
php-fpm-healthcheck --wait

# Copy initial storage structure
if [ -d "/var/www/storage-init" ]; then
    cp -R /var/www/storage-init/* /var/www/storage/
    rm -rf /var/www/storage-init
fi

# Execute the original entrypoint script from the PHP image
exec docker-php-entrypoint "$@"

```

--------------------------------

### Run a Container from a Custom Docker Image

Source: https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers

This command starts a new container using the `sample-app` image. Because the image was configured with a default command (`CMD node app.js`), the Node.js program will run automatically.

```console
$ docker run sample-app
```

--------------------------------

### Docker Run: Mount Volumes with --mount Flag

Source: https://docs.docker.com/storage/volumes

Demonstrates how to mount volumes using the --mount flag with Docker. This method is preferred for its explicitness and support for advanced options like volume driver options, mounting subdirectories, and use in Swarm services. It takes key-value pairs for configuration.

```bash
$ docker run --mount type=volume,src=<volume-name>,dst=<mount-path>
```

```bash
$ docker run --mount type=volume,src=myvolume,dst=/data,ro,volume-subpath=/foo
```

--------------------------------

### Start BuildKit Daemon

Source: https://docs.docker.com/build/buildkit

Starts the BuildKit daemon process. This command can be run directly or with an argument to specify a different containerd worker address if needed, such as when using a dockerd-managed containerd.

```console
> buildkitd.exe
```

```console
> buildkitd.exe --containerd-worker-addr "npipe:////./pipe/docker-containerd"
```

--------------------------------

### Set up Docker APT Repository

Source: https://docs.docker.com/engine/install/raspberry-pi-os

This script configures the Docker apt repository on Debian-based systems. It adds the Docker GPG key and the repository to the apt sources list, ensuring that Docker packages can be retrieved and installed.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/raspbian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/raspbian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

--------------------------------

### Docker Desktop Mac: Install Symlinks for CLI Tools

Source: https://docs.docker.com/desktop/setup/install/mac-permission-requirements

Demonstrates how Docker Desktop on Mac installs symlinks for its binaries. Users can choose between system-wide installation in `/usr/local/bin` (requiring authorization) or user-specific installation in `$HOME/.docker/bin` (manual PATH configuration required).

```Shell
# Example of choosing installation directory during setup (conceptual)
# User selects either /usr/local/bin or $HOME/.docker/bin

# If /usr/local/bin is chosen and not writable by unprivileged users:
# Docker Desktop prompts for authorization to create symlinks.

# If $HOME/.docker/bin is chosen:
# User must manually add $HOME/.docker/bin to PATH.
# Example: export PATH="$HOME/.docker/bin:$PATH"
```

--------------------------------

### Invoke Host Binaries from Frontend (JavaScript)

Source: https://docs.docker.com/llms

Demonstrates how to invoke host binaries from the frontend of a Docker extension using the extension SDK. This allows extensions to interact with the host system's command-line tools.

```javascript
async function invokeBinaries() {
  const result = await window.ddClient.extension.vm.cli.exec("docker", ["ps", "-a"]);
  console.log(result.stdout);
}
```

--------------------------------

### Dockerfile Example with Bind Mount and ls

Source: https://docs.docker.com/build/cache/optimize

Illustrates the behavior of bind mounts in a Dockerfile by mounting the current directory and executing 'ls' commands. The first 'ls' shows the mounted content, while the second shows the original build context after the mount is removed.

```dockerfile
FROM alpine:latest
WORKDIR /work
RUN touch foo.txt
RUN --mount=type=bind,target=. ls
RUN ls
```

--------------------------------

### Run htop in a Docker Container with Host PID Namespace

Source: https://docs.docker.com/reference/cli/docker/container/run

An example demonstrating how to run the 'htop' command inside an Alpine Linux container that shares the host's PID namespace. This allows the container to see all system processes.

```console
docker run --rm -it --pid=host alpine
```

```console
/ # apk add --quiet htop
```

```console
/ # htop
```

--------------------------------

### Example Docker Build Output

Source: https://docs.docker.com/guides/golang/build-images

An example of the diagnostic messages printed during the Docker image build process. Successful builds typically end with 'FINISHED' and indicate the image name.

```bash
[+] Building 2.2s (15/15) FINISHED
 => [internal] load build definition from Dockerfile                                                                                       0.0s
 => => transferring dockerfile: 701B                                                                                                       0.0s
 => [internal] load .dockerignore                                                                                                          0.0s
 => => transferring context: 2B                                                                                                            0.0s
 => resolve image config for docker.io/docker/dockerfile:1                                                                                 1.1s
 => CACHED docker-image://docker.io/docker/dockerfile:1@sha256:39b85bbfa7536a5feceb7372a0817649ecb2724562a38360f4d6a7782a409b14            0.0s
 => [internal] load build definition from Dockerfile                                                                                       0.0s
 => [internal] load .dockerignore                                                                                                          0.0s
 => [internal] load metadata for docker.io/library/golang:1.19                                                                             0.7s
 => [1/6] FROM docker.io/library/golang:1.19@sha256:5d947843dde82ba1df5ac1b2ebb70b203d106f0423bf5183df3dc96f6bc5a705                       0.0s
 => [internal] load build context                                                                                                          0.0s
 => => transferring context: 6.08kB                                                                                                        0.0s
 => CACHED [2/6] WORKDIR /app                                                                                                              0.0s
 => CACHED [3/6] COPY go.mod go.sum ./                                                                                                     0.0s
 => CACHED [4/6] RUN go mod download                                                                                                       0.0s
 => CACHED [5/6] COPY *.go ./                                                                                                              0.0s
 => CACHED [6/6] RUN CGO_ENABLED=0 GOOS=linux go build -o /docker-gs-ping                                                                  0.0s
 => exporting to image                                                                                                                     0.0s
 => => exporting layers                                                                                                                    0.0s
 => => writing image sha256:ede8ff889a0d9bc33f7a8da0673763c887a258eb53837dd52445cdca7b7df7e3                                               0.0s
 => => naming to docker.io/library/docker-gs-ping                                                                                          0.0s
```

--------------------------------

### Start Docker container with read-only bind mount using --mount

Source: https://docs.docker.com/engine/storage/bind-mounts

Starts a Docker container named 'devtest' with a read-only bind mount. The host's './target' directory is mounted to '/app' inside the container, preventing the container from modifying files in the host directory.

```console
$ docker run -d \
  -it \
  --name devtest \
  --mount type=bind,source="$(pwd)"/target,target=/app,readonly \
  nginx:latest
```

--------------------------------

### Start Docker container with read-only bind mount using -v

Source: https://docs.docker.com/engine/storage/bind-mounts

Starts a Docker container named 'devtest' with a read-only bind mount using the '-v' flag. The host's './target' directory is mounted to '/app' inside the container, ensuring that the container cannot alter the contents of the host directory.

```console
$ docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app:ro \
  nginx:latest
```

--------------------------------

### Handling Empty/Nil Fields in Docker Image Inspect API

Source: https://docs.docker.com/engine/deprecated

Explains that starting with Docker v29.0, certain fields in the `Config` object returned by `docker image inspect` and the `GET /images/{name}/json` API will be omitted if they are empty or nil. Applications should be updated to handle the absence of these fields gracefully.

```json
// Example of fields that may be omitted when empty in API response:
// Cmd, Entrypoint, Env, Labels, OnBuild, User, Volumes, WorkingDir
```

--------------------------------

### Kubectl Installation Paths

Source: https://docs.docker.com/desktop/kubernetes

Illustrates the default installation paths for the `kubectl` command-line tool on macOS and Windows when Kubernetes is enabled in Docker Desktop. It also provides a note for Linux users.

```text
Mac: /usr/local/bin/kubectl
Windows: C:\\Program Files\\Docker\\Docker\\resources\\bin\\kubectl.exe
Linux: Ensure the `kubectl` binary is installed at /usr/local/bin/kubectl.

```

--------------------------------

### Create Thin Pool Logical Volumes with lvcreate

Source: https://docs.docker.com/engine/storage/drivers/device-mapper-driver

Creates two logical volumes: 'thinpool' for data (95% of VG) and 'thinpoolmeta' for metadata (1% of VG). These are essential for the thin-provisioning setup.

```console
sudo lvcreate --wipesignatures y -n thinpool docker -l 95%VG
sudo lvcreate --wipesignatures y -n thinpoolmeta docker -l 1%VG
```

--------------------------------

### Start Docker Container

Source: https://docs.docker.com/reference/cli/docker/container/start

Starts one or more stopped containers. You can attach to the container's STDOUT/STDERR, use interactive mode, or override detach keys.

```APIDOC
## POST /containers/start

### Description
Start one or more stopped containers.

### Method
POST

### Endpoint
/containers/{id}/start

### Parameters
#### Path Parameters
- **id** (string) - Required - The ID or name of the container to start.

#### Query Parameters
- **detachKeys** (string) - Optional - Override the key sequence for detaching a container.

#### Request Body
- **Checkpoint** (string) - Optional - **experimental (daemon)** Restore from this checkpoint.
- **CheckpointDir** (string) - Optional - **experimental (daemon)** Use a custom checkpoint storage directory.

### Request Example
```json
{
  "Checkpoint": "my_checkpoint",
  "CheckpointDir": "/path/to/checkpoints"
}
```

### Response
#### Success Response (204 No Content)
This endpoint does not return a response body on success.

#### Error Response (404 Not Found)
- **message** (string) - Description of the error.

### Examples
```console
$ docker start my_container
```

```console
$ docker start -a my_container
```

```console
$ docker start -i my_container
```
```

--------------------------------

### Set up Docker repository on RHEL

Source: https://docs.docker.com/engine/install/rhel

These commands install the `dnf-plugins-core` package, which is necessary for managing DNF repositories, and then add the official Docker CE repository to your RHEL system. This enables you to install and update Docker Engine using the `dnf` package manager. This is the recommended method for installing Docker Engine.

```bash
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
```

--------------------------------

### Create Kubernetes Builder with QEMU Support (Docker CLI)

Source: https://docs.docker.com/build/builders/drivers/kubernetes

Creates a Kubernetes-based Buildx builder instance that is configured to use QEMU for emulating non-native architectures. This enables cross-platform builds when native nodes are not available.

```console
docker buildx create \
  --bootstrap \
  --name=kube \
  --driver=kubernetes \
  --driver-opt=namespace=buildkit,qemu.install=true
```

--------------------------------

### Docker Compose Configuration for Traefik with File Provider

Source: https://docs.docker.com/guides/traefik

Configures Traefik within a Docker Compose setup to use the File provider. This involves mounting a configuration file into the Traefik container and specifying its path in the command arguments. Two examples are provided for using DHI and official Traefik images.

```yaml
services:
  proxy:
    image: dhi.io/traefik:3.6.2
    command: --providers.docker --providers.file.filename=/config/traefik-config.yaml --api.insecure
    ports:
      - 80:80
      - 8080:8080
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./dev/traefik-config.yaml:/config/traefik-config.yaml
```

```yaml
services:
  proxy:
    image: traefik:v3.6.2
    command: --providers.docker --providers.file.filename=/config/traefik-config.yaml --api.insecure
    ports:
      - 80:80
      - 8080:8080
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - ./dev/traefik-config.yaml:/config/traefik-config.yaml
```

--------------------------------

### Git Commands for Repository Setup

Source: https://docs.docker.com/guides/php/configure-ci-cd

These console commands are used to configure your local Git repository to point to a new GitHub repository, rename the default branch to 'main', and push your initial commit.

```console
git remote set-url origin https://github.com/your-username/your-repository.git
git branch -M main
git add -A
git commit -m "my first commit"
git push -u origin main
```

--------------------------------

### Docker --mount flag for bind mounts

Source: https://docs.docker.com/engine/storage/bind-mounts

Demonstrates the syntax for the Docker --mount flag when performing a bind mount. It shows the key-value pair structure and common options like source, destination, readonly, and bind-propagation.

```console
docker run --mount type=bind,src=<host-path>,dst=<container-path>[,<key>=<value>...]
```

```console
docker run --mount type=bind,src=.,dst=/project,ro,bind-propagation=rshared
```

--------------------------------

### Python Dockerfile Migration: Before Ubuntu

Source: https://docs.docker.com/dhi/migration/examples/python

This Dockerfile demonstrates a Python application setup using an Ubuntu-based image before migration to Docker Hardened Images. It includes environment variable configurations, virtual environment creation, dependency installation, and application copying.

```dockerfile
#syntax=docker/dockerfile:1

FROM ubuntu/python:3.13-24.04_stable AS builder

ENV LANG=C.UTF-8
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PATH="/app/venv/bin:$PATH"

WORKDIR /app

RUN python -m venv /app/venv
COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

FROM ubuntu/python:3.13-24.04_stable

WORKDIR /app

ENV PYTHONUNBUFFERED=1
ENV PATH="/app/venv/bin:$PATH"

COPY app.py ./
COPY --from=builder /app/venv /app/venv

ENTRYPOINT [ "python", "/app/app.py" ]
```

--------------------------------

### Populate Docker Volume with Container Data (--mount)

Source: https://docs.docker.com/engine/storage/volumes

This command demonstrates how to start an Nginx container and populate a new volume named 'nginx-vol' with the default HTML content from the container's '/usr/share/nginx/html' directory. Docker automatically copies the directory's contents into the volume upon creation.

```console
docker run -d \
  --name=nginxtest \
  --mount source=nginx-vol,destination=/usr/share/nginx/html \
  nginx:latest
```

--------------------------------

### Dockerfile with ARG and Heredoc

Source: https://docs.docker.com/engine/reference/builder

This Dockerfile example demonstrates how to use the ARG instruction to define a build-time variable and how to use a heredoc with the COPY instruction to embed multi-line content into the image. The ENTRYPOINT then executes the copied script.

```dockerfile
# syntax=docker/dockerfile:1
FROM alpine
ARG FOO=bar
COPY <<-"EOT" /script.sh
  echo "hello ${FOO}"
EOT
ENTRYPOINT ash /script.sh
```

--------------------------------

### Include External Compose File and Define Web Service

Source: https://docs.docker.com/compose/gettingstarted

Configures the main Docker Compose file (`compose.yaml`) to include an external service definition file (`infra.yaml`) and defines the web service. It specifies the build context, port mapping, and enables watch mode for file synchronization.

```yaml
include:
   - infra.yaml
services:
  web:
    build: .
    ports:
      - "8000:5000"
    develop:
      watch:
        - action: sync
          path: .
          target: /code
```

--------------------------------

### Python Dockerfile Migration: Before Wolfi

Source: https://docs.docker.com/dhi/migration/examples/python

This Dockerfile shows a Python application setup using a Wolfi distribution-based image prior to migrating to Docker Hardened Images. It configures the environment, sets up a virtual environment, installs dependencies, and copies the application code.

```dockerfile
#syntax=docker/dockerfile:1

FROM cgr.dev/chainguard/python:latest-dev AS builder

ENV LANG=C.UTF-8
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PATH="/app/venv/bin:$PATH"

WORKDIR /app

RUN python -m venv /app/venv
COPY requirements.txt .

# Install any additional packages if needed using apk
# RUN apk add --no-cache gcc musl-dev

RUN pip install --no-cache-dir -r requirements.txt

FROM cgr.dev/chainguard/python:latest

WORKDIR /app

ENV PYTHONUNBUFFERED=1
ENV PATH="/app/venv/bin:$PATH"

COPY app.py ./
COPY --from=builder /app/venv /app/venv

ENTRYPOINT [ "python", "/app/app.py" ]
```

--------------------------------

### Install Docker Engine .deb packages

Source: https://docs.docker.com/engine/install/raspberry-pi-os

Installs Docker Engine, CLI, containerd, and Docker Compose by using the dpkg command to install the downloaded .deb files. Ensure you update the paths to where the .deb files were downloaded.

```console
sudo dpkg -i ./containerd.io_<version>_<arch>.deb \
  ./docker-ce_<version>_<arch>.deb \
  ./docker-ce-cli_<version>_<arch>.deb \
  ./docker-buildx-plugin_<version>_<arch>.deb \
  ./docker-compose-plugin_<version>_<arch>.deb
```

--------------------------------

### Illustrative Example of Compose Develop Specification

Source: https://docs.docker.com/reference/compose-file/develop

This example demonstrates the 'develop' subsection within a Compose file, showcasing how to configure 'watch' actions for services like 'frontend' and 'backend'. It illustrates 'sync' and 'rebuild' actions based on local file changes.

```yaml
services:
  frontend:
    image: example/webapp
    build: ./webapp
    develop:
      watch:
        # sync static content
        - path: ./webapp/html
          action: sync
          target: /var/www
          ignore:
            - node_modules/

  backend:
    image: example/backend
    build: ./backend
    develop:
      watch:
        # rebuild image and recreate service
        - path: ./backend/src
          action: rebuild
```

--------------------------------

### Start Docker Compose sandbox services

Source: https://docs.docker.com/engine/security/trust/trust_sandbox

This command starts the services defined in the 'compose.yaml' file in detached mode. It will download the necessary Docker images if they are not already present locally.

```bash
docker compose up -d
```

--------------------------------

### Node.js Dockerfile Migration to Docker Hardened Images (Multi-stage)

Source: https://docs.docker.com/dhi/migration/examples/node

This Dockerfile example shows a Node.js application after migrating to Docker Hardened Images using a multi-stage build. It features a build stage for installing dependencies and compiling the application, followed by a final stage that creates a minimal runtime image, recommended for security and size optimization.

```dockerfile
#syntax=docker/dockerfile:1

# === Build stage: Install dependencies and build application ===
FROM dhi.io/node:23-alpine3.21-dev AS builder
WORKDIR /usr/src/app

COPY package*.json ./

# Install any additional packages if needed using apk
# RUN apk add --no-cache python3 make g++

RUN npm install

COPY . .

# === Final stage: Create minimal runtime image ===
FROM dhi.io/node:23-alpine3.21
ENV PATH=/app/node_modules/.bin:$PATH

COPY --from=builder --chown=node:node /usr/src/app /app

WORKDIR /app

CMD ["index.js"]
```

--------------------------------

### Download and Install Docker Compose Standalone on Linux

Source: https://docs.docker.com/compose/install/standalone

Downloads the Docker Compose standalone binary for Linux x86_64 architecture and saves it to /usr/local/bin/docker-compose. This command requires curl to be installed.

```console
curl -SL https://github.com/docker/compose/releases/download/v5.0.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
```

--------------------------------

### Clone Sample Bun Application

Source: https://docs.docker.com/guides/bun/containerize

Clones a sample Bun application repository from GitHub to a local directory. This command requires a Git client to be installed.

```bash
git clone https://github.com/dockersamples/bun-docker.git && cd bun-docker
```

--------------------------------

### Execute Different Tool via Helper Script Entrypoint

Source: https://docs.docker.com/develop/security-best-practices

Illustrates running a Docker container and using the helper script ENTRYPOINT to execute a different tool, such as 'bash', by overriding the default CMD.

```shell
$ docker run --rm -it postgres bash
```

--------------------------------

### Define Custom JupyterLab Environment (Dockerfile)

Source: https://docs.docker.com/guides/jupyter

This Dockerfile defines a custom JupyterLab environment. It starts from the 'quay.io/jupyter/base-notebook' image and then uses the RUN instruction to install 'matplotlib' and 'scikit-learn' using pip. This ensures these packages are pre-installed in any container created from this image, saving time and ensuring consistency.

```dockerfile
# syntax=docker/dockerfile:1

FROM quay.io/jupyter/base-notebook
RUN pip install --no-cache-dir matplotlib scikit-learn
```

--------------------------------

### RUN statement using a here document for apt-get install

Source: https://docs.docker.com/build/building/best-practices

Shows how to use a here document (<<EOF) within a RUN instruction to execute multiple commands, including `apt-get update` and `apt-get install`, without needing explicit chaining with `&&`.

```dockerfile
RUN <<EOF
apt-get update
apt-get install -y --no-install-recommends \
    package-bar \
    package-baz \
    package-foo
EOF
```

--------------------------------

### Specify Destination Path for ADD Instruction in Dockerfile

Source: https://docs.docker.com/engine/reference/builder

This example demonstrates how the ADD instruction interprets destination paths. Paths starting with a forward slash are absolute, while those without are relative to the current working directory. Trailing slashes are significant, affecting whether a file is placed inside a directory or replaces it.

```dockerfile
# create /abs/test.txt
ADD test.txt /abs/
```

```dockerfile
WORKDIR /usr/src/app
# create /usr/src/app/rel/test.txt
ADD test.txt rel/
```

--------------------------------

### Run Container from New Image

Source: https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers

Starts a new container using the 'node-base' image and executes a Node.js command to verify Node.js functionality in the new image.

```console
$ docker run node-base node -e "console.log('Hello again')"
```

--------------------------------

### CDI Device Specification Example

Source: https://docs.docker.com/reference/dockerfile

Provides an example YAML configuration for defining CDI devices, including device names, container edits, and annotations. This demonstrates how to register custom devices for use with BuildKit.

```yaml
cdiVersion: "0.6.0"
kind: "vendor1.com/device"
devices:
  - name: foo
    containerEdits:
      env:
        - FOO=injected
  - name: bar
    annotations:
      org.mobyproject.buildkit.device.class: class1
    containerEdits:
      env:
        - BAR=injected
  - name: baz
    annotations:
      org.mobyproject.buildkit.device.class: class1
    containerEdits:
      env:
        - BAZ=injected
  - name: qux
    annotations:
      org.mobyproject.buildkit.device.class: class2
    containerEdits:
      env:
        - QUX=injected
annotations:
  org.mobyproject.buildkit.device.autoallow: true
```

--------------------------------

### Container File System Navigation and File Creation

Source: https://docs.docker.com/get-started/workshop/06_bind_mounts

Demonstrates navigating into the mounted source directory (`/src`) within an Ubuntu container and creating a new file (`myfile.txt`). This showcases the ability to modify container file system from within the container, which is reflected on the host.

```console
root@ac1237fad8db:/# cd src
root@ac1237fad8db:/src# touch myfile.txt
root@ac1237fad8db:/src# ls
Dockerfile  myfile.txt  node_modules  package.json  package-lock.json  spec  src  
```

--------------------------------

### Environment Configuration Example (.env file)

Source: https://docs.docker.com/guides/nodejs/containerize

An example of an .env file used to configure environment variables for the Docker Compose services. It includes settings for application ports, production resource limits, and database credentials.

```env
# Application Configuration
NODE_ENV=development
APP_PORT=3000
VITE_PORT=5173
DEBUG_PORT=9229

# Production Configuration
PROD_PORT=8080
PROD_MEMORY_LIMIT=2G
PROD_CPU_LIMIT=1.0
PROD_MEMORY_RESERVATION=512M
PROD_CPU_RESERVATION=0.25

# Database Configuration
POSTGRES_HOST=db
POSTGRES_PORT=5432
POSTGRES_DB=todoapp
POSTGRES_USER=todoapp
POSTGRES_PASSWORD=todoapp_password
DB_PORT=5432
```

--------------------------------

### Print Default Build Context and Dockerfile

Source: https://docs.docker.com/build/bake/reference

This console example demonstrates how `docker buildx bake --print` displays the default `context` and `dockerfile` for a target when they are not explicitly defined in the bake definition.

```bash
$ docker buildx bake --print -f - <<< 'target "default" {}'
[+] Building 0.0s (0/0)
{
  "target": {
    "default": {
      "context": ".",
      "dockerfile": "Dockerfile"
    }
  }
}
```

--------------------------------

### Join Nodes to a Docker Swarm

Source: https://docs.docker.com/llms

This example demonstrates how to add worker and manager nodes to an existing Docker Swarm. Proper node management is crucial for a resilient swarm.

```bash
# On a manager node, get the join token
docker swarm join-token worker

# On a worker node, join the swarm using the token
docker swarm join --token <SWMTKN-...> <MANAGER-IP>:<PORT>

```

--------------------------------

### Stop and Remove Docker Compose Services

Source: https://docs.docker.com/compose/gettingstarted

Commands to manage the lifecycle of Docker Compose services. `docker compose stop` halts running services without removing them, while `docker compose down` stops and removes all containers, networks, and volumes associated with the Compose project.

```console
docker compose stop
docker compose down
```

--------------------------------

### List Build Targets and Variables

Source: https://docs.docker.com/reference/cli/docker/buildx/bake

These commands demonstrate how to list available build targets and variables defined in a Bake configuration file. The `--list=targets` option shows targets and their descriptions, while `--list=variables` displays variables with their type, value, and description. The `format=json` option allows for JSON output.

```console
$ docker buildx bake --list=targets
TARGET              DESCRIPTION
binaries
default             binaries
update-docs
validate
validate-golangci   Validate .golangci.yml schema (does not run Go linter)
```

```console
$ docker buildx bake --list=variables
VARIABLE      TYPE      VALUE                DESCRIPTION
REGISTRY      string    docker.io/username   Registry and namespace
IMAGE_NAME    string    my-app               Image name
GO_VERSION              <null>
DEBUG         bool      false                Add debug symbols
```

```console
$ docker buildx bake --list=type=targets,format=json
```

--------------------------------

### Create and Configure Bake File (HCL)

Source: https://docs.docker.com/guides/compose-bake

Create a `docker-bake.hcl` file to customize build configurations. This example redefines the 'default' group to include specific targets, excluding the 'seed' target.

```bash
$ touch docker-bake.hcl
```

```hcl
group "default" {
  targets = ["vote", "result", "worker"]
}
```

--------------------------------

### Set up Docker Buildx Action

Source: https://docs.docker.com/build/ci/github-actions/cache

This snippet shows how to use the `docker/setup-buildx-action` to install the latest version of Docker Buildx, ensuring compatibility with newer GitHub Cache service API versions.

```yaml
- name: Set up Docker Buildx
  uses: docker/setup-buildx-action@v3
  with:
   version: latest
```

--------------------------------

### Declare and Use Basic AI Model in Docker Compose

Source: https://docs.docker.com/reference/compose-file/models

This example demonstrates a basic setup where a service ('app') uses a defined AI model ('ai_model'). The model is specified as an OCI artifact, and Docker Compose automatically injects connection information (e.g., AI_MODEL_URL) into the service container.

```yaml
services:
  app:
    image: app
    models:
      - ai_model

models:
  ai_model:
    model: ai/model
```

--------------------------------

### Modify Files in a Running Container (nginx)

Source: https://docs.docker.com/reference/cli/docker/debug

Illustrates how to modify files within a running container using `docker debug`. This example uses `vim` to change the default `index.html` of an nginx container, demonstrating the ability to alter container files non-destructively for debugging or testing purposes.

```console
docker run -d --name web-app -p 8080:80 nginx
vim /usr/share/nginx/html/index.html
```

--------------------------------

### Start a Container

Source: https://docs.docker.com/reference/api/engine/latest

Starts a specified container. This action resumes a stopped container.

```APIDOC
## Start a container 

### Method
POST

### Endpoint
/v1.53/containers/{id}/start

### Parameters
#### Path Parameters
- **id** (string) - Required - ID or name of the container

#### Query Parameters
- **detachKeys** (string) - Optional - Override the key sequence for detaching a container. Format is a single character `[a-Z]` or `ctrl-<value>` where `<value>` is one of: `a-z`, `@`, `^`, `[`, `,` or `_`.

### Responses
#### Success Response (204)
No error

#### Error Responses
- **304** - Container already started
- **404** - No such container
- **500** - Server error

### Request Example
```json
{
  "message": "No such container: c2ada9df5af8"
}
```
```

--------------------------------

### Run a Docker Sandbox for Claude Code (CLI)

Source: https://docs.docker.com/ai/sandboxes/get-started

Creates and runs a new Docker sandbox for the Claude Code agent. The sandbox is a lightweight microVM with a private Docker daemon. You can specify a workspace path, which defaults to the current directory if omitted. Multiple workspaces can be mounted, with options for read-only access.

```console
docker sandbox run claude [PATH]
```

```console
cd ~/my-project
docker sandbox run claude
```

```console
docker sandbox run claude ~/my-project ~/docs:ro
```

--------------------------------

### Clone Go Application Repository

Source: https://docs.docker.com/guides/golang/build-images

Clones the example Go application repository from GitHub to your local machine. This is the first step to obtaining the source code for the application you will containerize.

```bash
$ git clone https://github.com/docker/docker-gs-ping
```

--------------------------------

### Install All Dependencies for Building

Source: https://docs.docker.com/guides/nodejs/containerize

This stage installs all dependencies, including those needed for building, using `npm ci` without audit or fund information. It also caches npm and prepares necessary directories with correct ownership.

```dockerfile
# Build Dependencies Stage
FROM base AS build-deps

# Copy package files
COPY package*.json ./

# Install all dependencies with build optimizations
RUN --mount=type=cache,target=/root/.npm,sharing=locked \
    npm ci --no-audit --no-fund && \
    npm cache clean --force

# Create necessary directories and set permissions
RUN mkdir -p /app/node_modules/.vite && \
    chown -R nodejs:nodejs /app
```

--------------------------------

### Configure Nginx and Serve Laravel Assets (Dockerfile)

Source: https://docs.docker.com/guides/frameworks/laravel/production-setup

This snippet configures Nginx by replacing the default configuration with a custom one optimized for Laravel. It then copies the built public assets from a previous stage and sets the working directory. Finally, it exposes port 80 and starts the Nginx server.

```dockerfile
# Replace the default Nginx configuration with our custom one
# that is optimized for serving a Laravel application.
# ----------------------------------------------------------- 
COPY ./docker/nginx/nginx.conf /etc/nginx/nginx.conf

# Copy Laravel's public assets from the builder stage
# ----------------------------------------------------------- 
# We only need the 'public' directory from our Laravel app.
# ----------------------------------------------------------- 
COPY --from=builder /var/www/public /var/www/public

# Set the working directory to the public folder
WORKDIR /var/www/public

# Expose port 80 and start Nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

--------------------------------

### Create Nginx Dockerfile for Production Assets

Source: https://docs.docker.com/guides/frameworks/laravel/production-setup

This Dockerfile builds a production Nginx image. It first uses a 'builder' stage with Node.js to install npm dependencies and compile frontend assets. The compiled assets are then copied to a lean Nginx Alpine image, along with custom Nginx configurations.

```dockerfile
# docker/nginx/Dockerfile
# Stage 1: Build assets
FROM debian AS builder

# Install Node.js and build tools
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    nodejs \
    npm \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Set working directory
WORKDIR /var/www

# Copy Laravel application code
COPY . /var/www

# Install Node.js dependencies and build assets
RUN npm install && npm run build

# Stage 2: Nginx production image
FROM nginx:alpine

# Copy custom Nginx configuration
# ----------------------------------------------------------- 

```

--------------------------------

### Install Node.js Dependencies

Source: https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile

Executes a command inside the container during the image build process. Here, it installs the production dependencies for the Node.js application using the 'yarn install --production' command.

```dockerfile
RUN yarn install --production
```

--------------------------------

### Create Container Request Example

Source: https://docs.docker.com/reference/api/engine/latest

Example of a request payload for creating a Docker container.

```APIDOC
## POST /containers/create

### Description
Creates a new container from a given image.

### Method
POST

### Endpoint
/containers/create

### Parameters
#### Query Parameters
- **name** (string) - Optional - Assign a name to the container.
- **tag** (string) - Optional - Tag for the image.

#### Request Body
- **Hostname** (string) - Optional - The hostname to use for the container.
- **Domainname** (string) - Optional - The domain name to use for the container.
- **User** (string) - Optional - The user to run the command as.
- **AttachStdin** (boolean) - Optional - Attach the standard input, makes it possible to feed data to the container.
- **AttachStdout** (boolean) - Optional - Attach the standard output.
- **AttachStderr** (boolean) - Optional - Attach the standard error.
- **Tty** (boolean) - Optional - Allocate a pseudo-TTY.
- **OpenStdin** (boolean) - Optional - Keep STDIN open even if not attached.
- **StdinOnce** (boolean) - Optional - Close the Stdin after the first byte is received.
- **Env** (array of strings) - Optional - An array of environment variables.
- **Cmd** (array of strings) - Optional - The command to run in the container.
- **Entrypoint** (string) - Optional - The entrypoint for the container.
- **Image** (string) - Required - The name of the image to use for the container.
- **Labels** (object) - Optional - A map of metadata to set on the container.
- **Volumes** (object) - Optional - A map of volume bindings for the container.
- **WorkingDir** (string) - Optional - The working directory for the container.
- **NetworkDisabled** (boolean) - Optional - Whether to disable networking for the container.
- **ExposedPorts** (object) - Optional - A map of ports to expose from the container.
- **StopSignal** (string) - Optional - The signal to send to stop the container.
- **StopTimeout** (integer) - Optional - The timeout to wait for the container to stop.
- **HostConfig** (object) - Optional - Configuration for the host environment.
  - **Binds** (array of strings) - Optional - Bind mounts for the container.
  - **Links** (array of strings) - Optional - Links to other containers.
  - **Memory** (integer) - Optional - Memory limit for the container.
  - **MemorySwap** (integer) - Optional - Total memory and swap for the container.
  - **MemoryReservation** (integer) - Optional - Memory reservation for the container.
  - **NanoCpus** (integer) - Optional - CPU share in nano-CPUs.
  - **CpuPercent** (integer) - Optional - CPU percentage limit.
  - **CpuShares** (integer) - Optional - CPU shares (relative weight).
  - **CpuPeriod** (integer) - Optional - CPU CFS period.
  - **CpuRealtimePeriod** (integer) - Optional - CPU realtime period.
  - **CpuRealtimeRuntime** (integer) - Optional - CPU realtime runtime.
  - **CpuQuota** (integer) - Optional - CPU CFS quota.
  - **CpusetCpus** (string) - Optional - CPU(s) to use.
  - **CpusetMems** (string) - Optional - MEMORY nodes(s) to use.
  - **MaximumIOps** (integer) - Optional - Maximum IOps.
  - **MaximumIOBps** (integer) - Optional - Maximum IO Bps.
  - **BlkioWeight** (integer) - Optional - Block I/O weight.
  - **BlkioWeightDevice** (array of objects) - Optional - Block I/O weight per device.
  - **BlkioDeviceReadBps** (array of objects) - Optional - Block I/O rate limit per device (read).
  - **BlkioDeviceReadIOps** (array of objects) - Optional - Block I/O count limit per device (read).
  - **BlkioDeviceWriteBps** (array of objects) - Optional - Block I/O rate limit per device (write).
  - **BlkioDeviceWriteIOps** (array of objects) - Optional - Block I/O count limit per device (write).
  - **DeviceRequests** (array of objects) - Optional - Device requests for the container.
  - **MemorySwappiness** (integer) - Optional - Memory swappiness behavior.
  - **OomKillDisable** (boolean) - Optional - Whether to disable OOM killer.
  - **OomScoreAdj** (integer) - Optional - Adjust OOM score.
  - **PidMode** (string) - Optional - PID sharing mode.
  - **PidsLimit** (integer) - Optional - Maximum number of processes.
  - **PortBindings** (object) - Optional - Port bindings for the container.
  - **PublishAllPorts** (boolean) - Optional - Publish all exposed ports.
  - **Privileged** (boolean) - Optional - Give extended privileges to the container.
  - **ReadonlyRootfs** (boolean) - Optional - Mount the container's root filesystem as read-only.
  - **Dns** (array of strings) - Optional - DNS servers to use.
  - **DnsOptions** (array of strings) - Optional - DNS options.
  - **DnsSearch** (array of strings) - Optional - DNS search domains.
  - **VolumesFrom** (array of strings) - Optional - Volumes to inherit from other containers.
  - **CapAdd** (array of strings) - Optional - Kernel capabilities to add.
  - **CapDrop** (array of strings) - Optional - Kernel capabilities to drop.
  - **GroupAdd** (array of strings) - Optional - Add container to additional groups.
  - **RestartPolicy** (object) - Optional - Restart policy for the container.
  - **AutoRemove** (boolean) - Optional - Automatically remove the container when it exits.
  - **NetworkMode** (string) - Optional - Network mode for the container.
  - **Devices** (array of objects) - Optional - Devices to add to the container.
  - **Ulimits** (array of objects) - Optional - Ulimits for the container.
  - **LogConfig** (object) - Optional - Log configuration for the container.
  - **SecurityOpt** (array of strings) - Optional - Security options for the container.
  - **StorageOpt** (object) - Optional - Storage options for the container.
  - **CgroupParent** (string) - Optional - Parent cgroup for the container.
  - **VolumeDriver** (string) - Optional - Volume driver for the container.
  - **ShmSize** (integer) - Optional - Size of /dev/shm in bytes.
- **NetworkingConfig** (object) - Optional - Networking configuration for the container.
  - **EndpointsConfig** (object) - Optional - Endpoint configuration for networks.

### Request Example
```json
{
  "Hostname": "",
  "Domainname": "",
  "User": "",
  "AttachStdin": false,
  "AttachStdout": true,
  "AttachStderr": true,
  "Tty": false,
  "OpenStdin": false,
  "StdinOnce": false,
  "Env": [
    "FOO=bar",
    "BAZ=quux"
  ],
  "Cmd": [
    "date"
  ],
  "Entrypoint": "",
  "Image": "ubuntu",
  "Labels": {
    "com.example.vendor": "Acme",
    "com.example.license": "GPL",
    "com.example.version": "1.0"
  },
  "Volumes": {
    "/volumes/data": { }
  },
  "WorkingDir": "",
  "NetworkDisabled": false,
  "ExposedPorts": {
    "22/tcp": { }
  },
  "StopSignal": "SIGTERM",
  "StopTimeout": 10,
  "HostConfig": {
    "Binds": [
      "/tmp:/tmp"
    ],
    "Links": [
      "redis3:redis"
    ],
    "Memory": 0,
    "MemorySwap": 0,
    "MemoryReservation": 0,
    "NanoCpus": 500000,
    "CpuPercent": 80,
    "CpuShares": 512,
    "CpuPeriod": 100000,
    "CpuRealtimePeriod": 1000000,
    "CpuRealtimeRuntime": 10000,
    "CpuQuota": 50000,
    "CpusetCpus": "0,1",
    "CpusetMems": "0,1",
    "MaximumIOps": 0,
    "MaximumIOBps": 0,
    "BlkioWeight": 300,
    "BlkioWeightDevice": [
      { }
    ],
    "BlkioDeviceReadBps": [
      { }
    ],
    "BlkioDeviceReadIOps": [
      { }
    ],
    "BlkioDeviceWriteBps": [
      { }
    ],
    "BlkioDeviceWriteIOps": [
      { }
    ],
    "DeviceRequests": [
      {
        "Driver": "nvidia",
        "Count": -1,
        "DeviceIDs": [
          "0",
          "1",
          "GPU-fef8089b-4820-abfc-e83e-94318197576e"
        ],
        "Capabilities": [
          [
            "gpu",
            "nvidia",
            "compute"
          ]
        ],
        "Options": {
          "property1": "string",
          "property2": "string"
        }
      }
    ],
    "MemorySwappiness": 60,
    "OomKillDisable": false,
    "OomScoreAdj": 500,
    "PidMode": "",
    "PidsLimit": 0,
    "PortBindings": {
      "22/tcp": [
        {
          "HostPort": "11022"
        }
      ]
    },
    "PublishAllPorts": false,
    "Privileged": false,
    "ReadonlyRootfs": false,
    "Dns": [
      "8.8.8.8"
    ],
    "DnsOptions": [
      ""
    ],
    "DnsSearch": [
      ""
    ],
    "VolumesFrom": [
      "parent",
      "other:ro"
    ],
    "CapAdd": [
      "NET_ADMIN"
    ],
    "CapDrop": [
      "MKNOD"
    ],
    "GroupAdd": [
      "newgroup"
    ],
    "RestartPolicy": {
      "Name": "",
      "MaximumRetryCount": 0
    },
    "AutoRemove": true,
    "NetworkMode": "bridge",
    "Devices": [ ],
    "Ulimits": [
      { }
    ],
    "LogConfig": {
      "Type": "json-file",
      "Config": { }
    },
    "SecurityOpt": [ ],
    "StorageOpt": { },
    "CgroupParent": "",
    "VolumeDriver": "",
    "ShmSize": 67108864
  },
  "NetworkingConfig": {
    "EndpointsConfig": {
      "isolated_nw": {
        "IPAMConfig": {
          "IPv4Address": "172.20.30.33",
          "IPv6Address": "2001:db8:abcd::3033",
          "LinkLocalIPs": [
            "169.254.34.68",
            "fe80::3468"
          ]
        },
        "Links": [
          "container_1",
          "container_2"
        ],
        "Aliases": [
          "server_x",
          "server_y"
        ]
      },
      "database_nw": { }
    }
  }
}
```
```

--------------------------------

### Pull Models via Open WebUI Command Line

Source: https://docs.docker.com/ai/model-runner/openwebui-integration

This command demonstrates how to pull AI models using the Docker CLI. It's used within a Docker Compose setup to pre-load models before Open WebUI starts. Replace `ai/model-name` with the desired model identifier.

```console
docker model pull ai/llama3.2
```

--------------------------------

### Basic Docker Build Command

Source: https://docs.docker.com/build/bake/introduction

This snippet shows a standard `docker build` command to build an image from a Dockerfile in the current directory and tag it. It serves as a baseline for comparison with Bake configurations.

```console
$ docker build -f Dockerfile -t myapp:latest .
```

--------------------------------

### Initialize Docker Swarm

Source: https://docs.docker.com/engine/network/drivers/overlay

Initializes a Docker Swarm on the first host and provides instructions to join worker nodes. Requires Docker to be installed.

```console
$ docker swarm init
Swarm initialized: current node (vz1mm9am11qcmo979tlrlox42) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-5g90q48weqrtqryq4kj6ow0e8xm9wmv9o6vgqc5j320ymybd5c-8ex8j0bc40s6hgvy5ui5gl4gy 172.31.47.252:2377
```

--------------------------------

### Docker Extension Development Lifecycle

Source: https://docs.docker.com/llms

Guides on testing, debugging, packaging, releasing, and distributing Docker extensions, including CI integration and marketplace publishing.

```APIDOC
## Docker Extension Development Lifecycle

### Description
Covers the essential aspects of the Docker extension development lifecycle, from continuous integration and testing to packaging, releasing, and publishing on the Docker Marketplace.

### Method
N/A (Documentation Link)

### Endpoint
N/A

### Parameters
N/A

### Request Example
N/A

### Response
N/A

### Further Information
[Continuous Integration (CI)](https://docs.docker.com/extensions/extensions-sdk/dev/continuous-integration/)
[Test and debug](https://docs.docker.com/extensions/extensions-sdk/dev/test-debug/)
[Package and release your extension](https://docs.docker.com/extensions/extensions-sdk/extensions/DISTRIBUTION/)
[Publish in the Marketplace](https://docs.docker.com/extensions/extensions-sdk/extensions/publish/)
```

--------------------------------

### Sample Docker Configuration File

Source: https://docs.docker.com/engine/reference/commandline/cli

A sample `config.json` file demonstrating various Docker configuration options, including HTTP headers, output formatting for commands, detach keys, credential helpers, plugins, and proxy settings.

```json
{
  "HttpHeaders": {
    "MyHeader": "MyValue"
  },
  "psFormat": "table {{.ID}}\t{{.Image}}\t{{.Command}}\t{{.Labels}}",
  "imagesFormat": "table {{.ID}}\t{{.Repository}}\t{{.Tag}}\t{{.CreatedAt}}",
  "pluginsFormat": "table {{.ID}}	{{.Name}}	{{.Enabled}}",
  "statsFormat": "table {{.Container}}\t{{.CPUPerc}}\t{{.MemUsage}}",
  "servicesFormat": "table {{.ID}}\t{{.Name}}\t{{.Mode}}",
  "secretFormat": "table {{.ID}}\t{{.Name}}\t{{.CreatedAt}}\t{{.UpdatedAt}}",
  "configFormat": "table {{.ID}}\t{{.Name}}\t{{.CreatedAt}}\t{{.UpdatedAt}}",
  "serviceInspectFormat": "pretty",
  "nodesFormat": "table {{.ID}}\t{{.Hostname}}\t{{.Availability}}",
  "detachKeys": "ctrl-e,e",
  "credsStore": "secretservice",
  "credHelpers": {
    "awesomereg.example.org": "hip-star",
    "unicorn.example.com": "vcbait"
  },
  "plugins": {
    "plugin1": {
      "option": "value"
    },
    "plugin2": {
      "anotheroption": "anothervalue",
      "athirdoption": "athirdvalue"
    }
  },
  "proxies": {
    "default": {
      "httpProxy":  "http://user:pass@example.com:3128",
      "httpsProxy": "https://my-proxy.example.com:3129",
      "noProxy":    "intra.mycorp.example.com",
      "ftpProxy":   "http://user:pass@example.com:3128",
      "allProxy":   "socks://example.com:1234"
    },
    "https://manager1.mycorp.example.com:2377": {
      "httpProxy":  "http://user:pass@example.com:3128",
      "httpsProxy": "https://my-proxy.example.com:3129"
    }
  }
}
```

--------------------------------

### Complete Dockerfile for Go Application

Source: https://docs.docker.com/guides/golang/build-images

This is the complete Dockerfile that combines all the previous steps: setting the base image, defining the working directory, copying module files, downloading dependencies, copying source code, building the application, and specifying the command to run.

```dockerfile
# syntax=docker/dockerfile:1

FROM golang:1.19

# Set destination for COPY
WORKDIR /app

# Download Go modules
COPY go.mod go.sum ./
RUN go mod download

# Copy the source code. Note the slash at the end, as explained in
# https://docs.docker.com/reference/dockerfile/#copy
COPY *.go .

# Build
RUN CGO_ENABLED=0 GOOS=linux go build -o /docker-gs-ping

# Optional:
# To bind to a TCP port, runtime parameters must be supplied to the docker command.
# But we can document in the Dockerfile what ports
# the application is going to listen on by default.
# https://docs.docker.com/reference/dockerfile/#expose
EXPOSE 8080

# CMD specifies the default command to run when the container starts
CMD ["/docker-gs-ping"]
```

--------------------------------

### Docker Buildx Bake: Default File Lookup Example

Source: https://docs.docker.com/build/bake/overrides

Demonstrates the default file lookup order for Docker Buildx Bake, showing how it reads compose and bake definition files. It illustrates the merging process when multiple files are present and how the last definition takes precedence.

```console
$ docker buildx bake --print
[+] Building 0.0s (1/1) FINISHED                                                                                                                                                                                            
 => [internal] load local bake definitions                                                                                                                                                                             0.0s
 => => reading compose.yaml 45B / 45B                                                                                                                                                                                  0.0s
 => => reading docker-bake.hcl 113B / 113B                                                                                                                                                                             0.0s
 => => reading docker-bake.override.hcl 65B / 65B
```

--------------------------------

### Validate Node.js Installation

Source: https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers

Executes a simple Node.js script to confirm that Node.js has been successfully installed and is operational within the container.

```console
$ node -e 'console.log("Hello world!")'
```

--------------------------------

### Dockerfile: Use Absolute WORKDIR Paths

Source: https://docs.docker.com/reference/build-checks/workdir-relative-path

This example shows the correct way to specify the WORKDIR in a Dockerfile using an absolute path. Starting the path with '/' ensures that the working directory is consistently set to '/usr/share/nginx/html', regardless of the base image's default working directory, preventing potential build issues.

```dockerfile
FROM nginx AS web
WORKDIR /usr/share/nginx/html
COPY public .
```

--------------------------------

### Start Traefik Container with Docker Provider (Official Image)

Source: https://docs.docker.com/guides/traefik

Starts a Traefik container in detached mode using the official Traefik image. It connects to the 'traefik-demo' network, exposes port 80, mounts the Docker socket for configuration updates, and enables the Docker provider.

```bash
docker run -d --network=traefik-demo \
  -p 80:80 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  traefik:v3.6.2 \
  --providers.docker
```

--------------------------------

### Bake file syntax: HCL example

Source: https://docs.docker.com/build/bake/reference

The same Bake file as the JSON example, but written in HCL (HashiCorp Configuration Language). HCL is the preferred format for Bake files due to its richer feature set.

```hcl
variable "TAG" {
  default = "latest"
}

group "default" {
  targets = ["webapp"]
}

target "webapp" {
  dockerfile = "Dockerfile"
  tags = ["docker.io/username/webapp:${TAG}"]
}
```

--------------------------------

### Dockerfile: Avoid Relative WORKDIR Paths

Source: https://docs.docker.com/reference/build-checks/workdir-relative-path

This example demonstrates the incorrect use of a relative WORKDIR path in a Dockerfile. Using a relative path like 'usr/share/nginx/html' can lead to unexpected working directories if the base image's WORKDIR changes. It's recommended to always use an absolute path starting with a '/'.

```dockerfile
FROM nginx AS web
WORKDIR usr/share/nginx/html
COPY public .
```

--------------------------------

### Manually Install Docker Compose CLI Plugin

Source: https://docs.docker.com/compose/install/linux

Downloads and installs the Docker Compose CLI plugin manually for the current user. It sets up the necessary directory structure and downloads the plugin binary from GitHub. This method does not support automatic updates and requires manual intervention for upgrades. It also allows customization for different architectures and installation scopes (current user vs. all users).

```bash
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}
mkdir -p $DOCKER_CONFIG/cli-plugins
curl -SL https://github.com/docker/compose/releases/download/v5.0.1/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose
```

--------------------------------

### Docker Compose Pull Command Execution Example

Source: https://docs.docker.com/reference/cli/docker/compose/pull

An example of executing the 'docker compose pull' command for a specific service ('db') and the resulting output showing the image pull process.

```console
$ docker compose pull db
[+] Running 1/15
  ⠸ db Pulling                                                             12.4s
   ⠿ 45b42c59be33 Already exists                                           0.0s
   ⠹ 40adec129f1a Downloading  3.374MB/4.178MB                             9.3s
   ⠹ b4c431d00c78 Download complete                                        9.3s
   ⠹ 2696974e2815 Download complete                                        9.3s
   ⠹ 564b77596399 Downloading  5.622MB/7.965MB                             9.3s
   ⠹ 5044045cf6f2 Downloading  216.7kB/391.1kB                             9.3s
   ⠹ d736e67e6ac3 Waiting                                                  9.3s
   ⠹ 390c1c9a5ae4 Waiting                                                  9.3s
   ⠹ c0e62f172284 Waiting                                                  9.3s
   ⠹ ebcdc659c5bf Waiting                                                  9.3s
   ⠹ 29be22cb3acc Waiting                                                  9.3s
   ⠹ f63c47038e66 Waiting                                                  9.3s
   ⠹ 77a0c198cde5 Waiting                                                  9.3s
   ⠹ c8752d5b785c Waiting                                                  9.3s
```

--------------------------------

### VOLUME Instruction Example

Source: https://docs.docker.com/engine/reference/builder

Demonstrates the VOLUME instruction in a Dockerfile, which creates a mount point for external volumes. It shows how to specify a volume path and how data within that path in the base image is initialized into the new volume upon container creation.

```dockerfile
FROM ubuntu
RUN mkdir /myvol
RUN echo "hello world" > /myvol/greeting
VOLUME /myvol
```

--------------------------------

### Command to Copy Environment File

Source: https://docs.docker.com/guides/nodejs/containerize

A console command to copy the example environment file (.env.example) to a new file (.env), which can then be customized for the application's configuration.

```bash
cp .env.example .env
```

--------------------------------

### Install and Use awscli-local for Local S3 Bucket Creation

Source: https://docs.docker.com/guides/localstack

This snippet covers installing the `awscli-local` tool using pip and then using the `awslocal` command to create a new S3 bucket named 'mysamplebucket' within the LocalStack environment. This is useful for testing S3 interactions without AWS credentials.

```console
$ pip install awscli-local
$ awslocal s3 mb s3://mysamplebucket
```

--------------------------------

### Dockerfile: Set Runtime Environment Variable with ENV

Source: https://docs.docker.com/build/building/variables

This Dockerfile example shows how to declare an environment variable (ENV) to configure the runtime environment. By setting `NODE_ENV` to `production`, it influences the `npm install` command to omit development-specific packages, optimizing the final image. This variable will be available in containers created from the image.

```dockerfile
# syntax=docker/dockerfile:1

FROM node:20
WORKDIR /app
COPY package*.json ./
ENV NODE_ENV=production
RUN npm ci && npm cache clean --force
COPY . .
CMD ["node", "app.js"]
```

--------------------------------

### POST /images/create

Source: https://docs.docker.com/reference/api/engine/sdk/examples

Pulls an image from a registry. This operation can be performed with or without authentication credentials.

```APIDOC
## Pull an image

### Description
Pull an image, similar to the `docker pull` command.

### Method
POST

### Endpoint
/images/create

### Query Parameters
- **fromImage** (string) - Required - The name of the image to pull (e.g., `alpine`).
- **tag** (string) - Optional - The tag of the image to pull (defaults to `latest`).

### Request Body
None

### Request Example
```console
$ curl --unix-socket /var/run/docker.sock \
  -X POST "http://localhost/v1.53/images/create?fromImage=alpine"
```

### Success Response (200)
- **status** (string) - The status of the pull operation.
- **id** (string) - The ID of the image or layer being processed.
- **progressDetail** (object) - Details about the download progress.
- **progress** (string) - A string indicating the download progress.

### Response Example
```json
{"status":"Pulling from library/alpine","id":"3.1"}
{"status":"Pulling fs layer","progressDetail":{},"id":"8f13703509f7"}
{"status":"Downloading","progressDetail":{"current":32768,"total":2244027},"progress":"[\u003e                                                  ] 32.77 kB/2.244 MB","id":"8f13703509f7"}
... 
```

## Pull an image with authentication

### Description
Pull an image with authentication credentials. It's recommended to use HTTPS for registries.

### Method
POST

### Endpoint
/images/create

### Query Parameters
- **fromImage** (string) - Required - The name of the image to pull (e.g., `alpine`).
- **tag** (string) - Optional - The tag of the image to pull (defaults to `latest`).

### Headers
- **X-Registry-Auth** (string) - Required - Base-64 encoded JSON string of registry authentication configuration.

### Request Body
None

### Request Example
```console
$ JSON=$(echo '{"username": "string", "password": "string", "serveraddress": "string"}' | base64)

$ curl --unix-socket /var/run/docker.sock \
  -H "Content-Type: application/tar" \
  -X POST "http://localhost/v1.53/images/create?fromImage=alpine" \
  -H "X-Registry-Auth" \
  -d "$JSON"
```

### Success Response (200)
- **status** (string) - The status of the pull operation.
- **id** (string) - The ID of the image or layer being processed.
- **progressDetail** (object) - Details about the download progress.
- **progress** (string) - A string indicating the download progress.

### Response Example
```json
{"status":"Pulling from library/alpine","id":"3.1"}
{"status":"Pulling fs layer","progressDetail":{},"id":"8f13703509f7"}
{"status":"Downloading","progressDetail":{"current":32768,"total":2244027},"progress":"[\u003e                                                  ] 32.77 kB/2.244 MB","id":"8f13703509f7"}
... 
```
```

--------------------------------

### Set up Docker Compose Action

Source: https://docs.docker.com/build/ci/github-actions/cache

This snippet demonstrates using the `docker/setup-compose-action` to install the latest version of Docker Compose, which is necessary for compatibility with the updated GitHub Cache service API.

```yaml
- name: Set up Docker Compose
  uses: docker/setup-compose-action@v1
  with:
   version: latest
```

--------------------------------

### Format Docker Search Output with Go Templates

Source: https://docs.docker.com/reference/cli/docker/search

This example demonstrates using the '--format' option with a Go template to customize the output of the 'docker search' command. It specifies placeholders like '{{.Name}}' and '{{.StarCount}}' to control which information is displayed and how it's presented. This allows for precise data extraction and presentation.

```console
$ docker search --format "{{.Name}}: {{.StarCount}}" nginx

nginx: 5441
jwilder/nginx-proxy: 953
richarvey/nginx-php-fpm: 353
million12/nginx-php: 75
webdevops/php-nginx: 70
h3nrik/nginx-ldap: 35
bitnami/nginx: 23
evild/alpine-nginx: 14
million12/nginx: 9
maxexcloo/nginx: 7
```

--------------------------------

### Install rclone Docker Volume Plugin

Source: https://docs.docker.com/storage/volumes

Installs the rclone/docker-volume-rclone plugin on a Docker host, granting it all necessary permissions and aliasing it as 'rclone'. This enables the use of rclone for managing remote storage as Docker volumes.

```bash
$ docker plugin install --grant-all-permissions rclone/docker-volume-rclone --aliases rclone

```

--------------------------------

### Enable SBOM and Provenance Attestations (GitHub Actions YAML)

Source: https://docs.docker.com/guides/gha

This configuration extends the Docker image build process to include SBOM and provenance attestations. It requires 'docker/setup-buildx-action' to be run beforehand and enables the 'provenance' and 'sbom' options in the 'docker/build-push-action'. This enhances security and traceability of the built image.

```yaml
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3
      
      - name: Build and push Docker image
        uses: docker/build-push-action@v6
        with:
          push: ${{ github.event_name != 'pull_request' }}
          tags: ${{ steps.meta.outputs.tags }}
          annotations: ${{ steps.meta.outputs.annotations }}
          provenance: true
          sbom: true
```

--------------------------------

### Format Docker Service List as JSON

Source: https://docs.docker.com/reference/cli/docker/service/ls

This example shows how to use the `--format json` directive to output all service details in JSON format. This is useful for programmatic parsing of service information.

```console
$ docker service ls --format json
{"ID":"ssniordqolsi","Image":"hello-world:latest","Mode":"replicated","Name":"hello","Ports":"","Replicas":"0/1"}
```

--------------------------------

### Dockerfile: Add Labels and Copy Backend Service

Source: https://docs.docker.com/extensions/extensions-sdk/build/backend-extension-tutorial

This Dockerfile snippet demonstrates adding labels and copying the compiled backend service executable into the Docker image. It sets the command to run the service upon container startup.

```dockerfile
# ... add labels and copy the frontend application

COPY --from=builder /backend/bin/service /
CMD /service -socket /run/guest-services/extension-allthethings-extension.sock
```

--------------------------------

### Report Health Check Success (Shell)

Source: https://docs.docker.com/ai/model-runner/examples

This script is executed only if the preceding steps in the workflow have succeeded. It prints a success message indicating the completion of the Docker Model Runner daily health check and lists the individual tests that have passed, including installation, version command, model operations, API endpoint operations, and cleanup.

```shell
echo "🎉 Docker Model Runner daily health check completed successfully!"
echo "All tests passed:"
echo "  ✅ docker-model-plugin installation successful"
echo "  ✅ docker model version command working"
echo "  ✅ Model pull and run operations successful"
echo "  ✅ API endpoint operations successful"
echo "  ✅ Cleanup operations successful"
```

--------------------------------

### Update Package Installation Commands (Dockerfile)

Source: https://docs.docker.com/dhi/migration/migrate-from-ubuntu

Demonstrates updating package installation commands within a Dockerfile when migrating from Ubuntu to DHI Debian. It highlights the use of `apt-get update` and `apt-get install` within a `dev` image context, ensuring package managers are available.

```dockerfile
```diff
- ## Ubuntu: Installing packages
- FROM ubuntu/go:1.22-24.04
- RUN apt-get update && apt-get install -y \
-     git \
-     && rm -rf /var/lib/apt/lists/*

+ ## DHI: Use a language-specific dev image with package manager
+ FROM dhi.io/golang:1-debian13-dev
+ RUN apt-get update && apt-get install -y \
+     git \
+     && rm -rf /var/lib/apt/lists/*
```
```

--------------------------------

### Develop React.js Applications with Docker

Source: https://docs.docker.com/llms

Learn to develop React.js applications locally using Docker containers. This guide helps set up a containerized development environment for React.

```Dockerfile
FROM node:latest

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

--------------------------------

### Add PostgreSQL Database Service to Docker Compose

Source: https://docs.docker.com/guides/nodejs/develop

This YAML snippet defines a PostgreSQL database service for a Docker Compose setup. It specifies the image, environment variables for credentials, volume for data persistence, port mapping, restart policy, health check, and network configuration. Ensure Docker and Docker Compose are installed.

```yaml
services:
  # ... existing app services ...

  # ========================================
  # PostgreSQL Database Service
  # ========================================
  db:
    image: postgres:18-alpine
    container_name: todoapp-db
    environment:
      POSTGRES_DB: '${POSTGRES_DB:-todoapp}'
      POSTGRES_USER: '${POSTGRES_USER:-todoapp}'
      POSTGRES_PASSWORD: '${POSTGRES_PASSWORD:-todoapp_password}'
    volumes:
      - postgres_data:/var/lib/postgresql
    ports:
      - '${DB_PORT:-5432}:5432'
    restart: unless-stopped
    healthcheck:
      test: ['CMD-SHELL', 'pg_isready -U ${POSTGRES_USER:-todoapp} -d ${POSTGRES_DB:-todoapp}']
      interval: 10s
      timeout: 5s
      retries: 5
      start_period: 5s
    networks:
      - todoapp-network

# ========================================
# Volume Configuration
# ========================================
volumes:
  postgres_data:
    name: todoapp-postgres-data
    driver: local

# ========================================
# Network Configuration
# ========================================
networks:
  todoapp-network:
    name: todoapp-network
    driver: bridge

```

--------------------------------

### Initialize and Use Host Directory Bind Mount Volume

Source: https://docs.docker.com/reference/cli/docker/container/create

This snippet shows how to create a Docker container that bind mounts a host directory (`/home/docker`) into the container (`/docker`). This bind mount can then be used by subsequent containers.

```console
$ docker create -v /home/docker:/docker --name docker ubuntu

9aa88c08f319cd1e4515c3c46b0de7cc9aa75e878357b1e96f91e2c773029f03

$ docker run --rm --volumes-from docker ubuntu ls -la /docker

total 20
drwxr-sr-x  5 1000 staff  180 Dec  5 04:00 .
drwxr-xr-x 48 root root  4096 Dec  5 04:13 ..
-rw-rw-r--  1 1000 staff 3833 Dec  5 04:01 .ash_history
-rw-r--r--  1 1000 staff   446 Nov 28 11:51 .ashrc
-rw-r--r--  1 1000 staff   25 Dec  5 04:00 .gitconfig
drwxr-sr-x  3 1000 staff   60 Dec  1 03:28 .local
-rw-r--r--  1 1000 staff  920 Nov 28 11:51 .profile
drwx--S---  2 1000 staff  460 Dec  5 00:51 .ssh
drwxr-xr-x 32 1000 staff 1140 Dec  5 04:01 docker
```

--------------------------------

### .dockerignore File Example

Source: https://docs.docker.com/build/building/best-practices

Example content for a .dockerignore file, specifying patterns for files to be excluded from the Docker build context. This helps reduce build time and image size by preventing unnecessary files from being sent to the Docker daemon.

```plaintext
*.md
```

--------------------------------

### Incorrect Dockerfile EXPOSE Syntax Examples

Source: https://docs.docker.com/reference/build-checks/expose-invalid-format

Illustrates common incorrect usages of the EXPOSE instruction in Dockerfiles. These examples show the pitfalls of including IP addresses or host-port mappings, which are not supported by the EXPOSE instruction.

```dockerfile
FROM alpine
EXPOSE 127.0.0.1:80:80
```

```dockerfile
FROM alpine
EXPOSE 80:80
```

--------------------------------

### Install Python Package with RUN Instruction

Source: https://docs.docker.com/build/concepts/dockerfile

This `RUN` instruction uses `pip` to install a specific Python package, `flask`, with a version constraint. This command requires `pip` to be installed in the container, which is typically handled by a preceding `RUN` instruction.

```dockerfile
RUN pip install flask==3.0.*
```

--------------------------------

### Start Dex Docker Container

Source: https://docs.docker.com/guides/dex

This command starts the Dex Docker container defined in the 'docker-compose.yaml' file in detached mode. It will download the Dex image if it's not already present on your system.

```bash
docker compose up -d
```

--------------------------------

### Docker Compose Production Configuration

Source: https://docs.docker.com/guides/frameworks/laravel/production-setup

This Docker Compose file defines the services for a production Laravel environment. It includes services for Nginx, PHP-FPM, and a database (MySQL in this example). It specifies image versions, build contexts, environment variables, volumes for persistent data and logs, and network configurations to enable communication between services.

```yaml
version: '3.8'

services:
  nginx:
    build:
      context: ./docker/nginx
      dockerfile: Dockerfile
    ports:
      - '80:80'
    volumes:
      - .:/var/www
      - ./docker/nginx/conf.d:/etc/nginx/conf.d
      - ./logs/nginx:/var/log/nginx
    depends_on:
      - php-fpm
    networks:
      - laravel_network

  php-fpm:
    build:
      context: ./docker/php-fpm
      dockerfile: Dockerfile
    volumes:
      - .:/var/www
      - ./logs/php-fpm:/var/log/php-fpm
    environment:
      - DB_HOST=mysql
      - DB_PORT=3306
      - DB_DATABASE=laravel
      - DB_USERNAME=root
      - DB_PASSWORD=secret
    depends_on:
      - mysql
    networks:
      - laravel_network

  mysql:
    image: mysql:8.0
    ports:
      - '3306:3306'
    volumes:
      - mysql_data:/var/lib/mysql
      - ./logs/mysql:/var/log/mysql
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: laravel
    networks:
      - laravel_network

volumes:
  mysql_data:

networks:
  laravel_network:
    driver: bridge

```

--------------------------------

### Install Node.js in Container

Source: https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers

Updates the package list and installs Node.js within the running Ubuntu container. This command modifies the container's filesystem.

```console
$ apt update && apt install -y nodejs
```

--------------------------------

### Set Up Docker Repository on CentOS

Source: https://docs.docker.com/engine/install/centos

Installs the DNF plugins core package and adds the official Docker CE repository to the CentOS system. This enables the installation and management of Docker Engine from Docker's repositories.

```console
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

--------------------------------

### Initialize Private Marketplace Configuration Files

Source: https://docs.docker.com/extensions/private-marketplace

Commands to create the necessary configuration files (`admin-settings.json` and `extensions.txt`) for a private Docker extension marketplace. These commands differ based on the operating system.

```bash
mkdir my-marketplace
cd my-marketplace
/Applications/Docker.app/Contents/Resources/bin/extension-admin init
```

```powershell
mkdir my-marketplace
cd my-marketplace
"C:\Program Files\Docker\Docker\resources\bin\extension-admin" init
```

```bash
mkdir my-marketplace
cd my-marketplace
/opt/docker-desktop/extension-admin init
```

--------------------------------

### Configure X Server Access for Docker (Linux)

Source: https://docs.docker.com/guides/ros2/turtlesim-example

Allows Docker containers to access the local X server for GUI applications like Turtlesim. This command grants local Docker clients access to your X display.

```bash
xhost +local:docker
```

--------------------------------

### Docker Scout Quickview: Image Overview (Console)

Source: https://docs.docker.com/reference/cli/docker/scout/quickview

Demonstrates how to get a quick overview of a specific Docker image using the 'docker scout quickview' command. This command analyzes the image and its base image for vulnerabilities and provides refresh/update recommendations.

```console
docker scout quickview golang:1.19.4
    ...Pulling
    ✓ Pulled
    ✓ SBOM of image already cached, 278 packages indexed

  Your image  golang:1.19.4                          │    5C     3H     6M    63L
  Base image  buildpack-deps:bullseye-scm            │    5C     1H     3M    48L     6?
  Refreshed base image  buildpack-deps:bullseye-scm  │    0C     0H     0M    42L
                                                     │    -5     -1     -3     -6     -6
  Updated base image  buildpack-deps:sid-scm         │    0C     0H     1M    29L
                                                     │    -5     -1     -2    -19     -6
```

--------------------------------

### Install Specific Docker Engine Version (Fedora)

Source: https://docs.docker.com/engine/install/fedora

Installs a specific version of Docker Engine, Docker CLI, containerd.io, and Docker Compose plugin. Replace `<VERSION_STRING>` with the desired version obtained from `dnf list --showduplicates`.

```bash
sudo dnf install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io docker-buildx-plugin docker-compose-plugin
```

--------------------------------

### POST /containers/create

Source: https://docs.docker.com/engine/release-notes/27

Creates a container. Supports `Options` as part of `HostConfig.Mounts.TmpfsOptions` for setting options for tmpfs mounts.

```APIDOC
## POST /containers/create

### Description
Creates a container. Supports `Options` as part of `HostConfig.Mounts.TmpfsOptions` allowing to set options for tmpfs mounts.

### Method
POST

### Endpoint
`/containers/create`

### Parameters
#### Request Body
- **HostConfig.Mounts.TmpfsOptions.Options** (object) - Optional - Options for tmpfs mounts.
  - **Mode** (string) - Optional - Permissions mode for the tmpfs mount.
  - **SizeBytes** (integer) - Optional - Size in bytes for the tmpfs mount.
  - **UID** (integer) - Optional - User ID for the tmpfs mount.
  - **GID** (integer) - Optional - Group ID for the tmpfs mount.

### Response
#### Success Response (200)
- **Id** (string) - The ID of the created container.
- **Warnings** (array) - An array of warnings generated during container creation.

#### Response Example
```json
{
  "Id": "container_id",
  "Warnings": []
}
```
```

--------------------------------

### Docker Desktop Installer Flags: Security and Access Control

Source: https://docs.docker.com/desktop/setup/install/windows-install

Demonstrates installer flags for enhancing security and controlling access to Docker Desktop. This includes enforcing membership in a specific Docker Hub organization and disabling Windows containers.

```console
"Docker Desktop Installer.exe" install --allowed-org="my-docker-org" --no-windows-containers
```

--------------------------------

### Specify Default Command to Run

Source: https://docs.docker.com/get-started/docker-concepts/building-images/writing-a-dockerfile

Defines the default command that will be executed when a container is started from the built image. This instruction starts the Node.js application using 'node ./src/index.js'.

```dockerfile
CMD ["node", "./src/index.js"]
```

--------------------------------

### Build All Variants with Buildx Bake (Console)

Source: https://docs.docker.com/guides/bake

This command first removes the existing build directory and then executes the 'bin-all' target. This process generates release and debug variants of the binary for all specified platforms, organized into respective subdirectories.

```bash
rm -r ./build/
docker buildx bake bin-all
```

--------------------------------

### Install Docker Compose Plugin using APT (Ubuntu/Debian)

Source: https://docs.docker.com/compose/install/linux

Installs the latest version of the Docker Compose plugin on Ubuntu and Debian-based systems using the APT package manager. This command updates the package index and then installs the 'docker-compose-plugin' package. It assumes Docker Engine and CLI are already installed.

```bash
$ sudo apt-get update
$ sudo apt-get install docker-compose-plugin
```

--------------------------------

### List Running Containers using Docker API

Source: https://docs.docker.com/reference/api/engine/sdk/examples

Lists all running containers on the Docker host. This functionality is equivalent to the `docker ps` command. It requires the Docker SDK for Go or Python, or direct HTTP requests to the Docker API.

```go
package main

import (
	"context"
	"fmt"

	"github.com/moby/moby/client"
)

func main() {
	ctx := context.Background()
	apiClient, err := client.New(client.FromEnv)
	if err != nil {
		panic(err)
	}
	defer apiClient.Close()

	containers, err := apiClient.ContainerList(ctx, client.ContainerListOptions{})
	if err != nil {
		panic(err)
	}

	for _, container := range containers.Items {
		fmt.Println(container.ID)
	}
}
```

```python
import docker
client = docker.from_env()
for container in client.containers.list():
  print(container.id)
```

```http
$ curl --unix-socket /var/run/docker.sock http://localhost/v1.53/containers/json
[
{
  "Id":"ae63e8b89a26f01f6b4b2c9a7817c31a1b6196acf560f66586fbc8809ffcd772",
  "Names":["/tender_wing"],
  "Image":"bfirsh/reticulate-splines",
  ...
}]
```

--------------------------------

### Docker Desktop Installation with Embedded PAC Script

Source: https://docs.docker.com/desktop/setup/install/mac-install

This command illustrates installing Docker Desktop with a specific user and an embedded PAC script for proxy configuration. This method takes precedence over specifying a PAC file URL.

```console
sudo /Applications/Docker.app/Contents/MacOS/install --user testuser --proxy-http-mode="manual" --override-proxy-embedded-pac="function FindProxyForURL(url, host) { return \"DIRECT\"; }"
```

--------------------------------

### Create E2B Sandbox with GitHub & SonarQube MCP (Python)

Source: https://docs.docker.com/guides/github-sonarqube-sandbox/workflow

Initializes an E2B sandbox with GitHub and SonarQube MCP servers. It loads environment variables, creates the sandbox, retrieves MCP gateway information, configures the Claude CLI, and then terminates the sandbox. Requires 'python-dotenv' and 'e2b' packages.

```python
import os
import asyncio
from dotenv import load_dotenv
from e2b import AsyncSandbox

load_dotenv()

async def test_connection():
    print("Creating E2B sandbox with GitHub and SonarQube MCP servers...\n")

    sbx = await AsyncSandbox.beta_create(
        envs={
            "ANTHROPIC_API_KEY": os.getenv("ANTHROPIC_API_KEY"),
            "GITHUB_TOKEN": os.getenv("GITHUB_TOKEN"),
            "SONARQUBE_TOKEN": os.getenv("SONARQUBE_TOKEN"),
        },
        mcp={
            "githubOfficial": {
                "githubPersonalAccessToken": os.getenv("GITHUB_TOKEN"),
            },
            "sonarqube": {
                "org": os.getenv("SONARQUBE_ORG"),
                "token": os.getenv("SONARQUBE_TOKEN"),
                "url": "https://sonarcloud.io",
            },
        },
    )

    mcp_url = sbx.beta_get_mcp_url()
    mcp_token = await sbx.beta_get_mcp_token()

    print(" Sandbox created successfully!")
    print(f"MCP Gateway URL: {mcp_url}\n")

    # Wait for MCP initialization
    await asyncio.sleep(1)

    # Configure Claude to use the MCP gateway
    print("Connecting Claude CLI to MCP gateway...")
    await sbx.commands.run(
        f'claude mcp add --transport http e2b-mcp-gateway {mcp_url} --header "Authorization: Bearer {mcp_token}"' ,
        timeout=0,
        on_stdout=print,
        on_stderr=print,
    )

    print("\n Connection successful! Cleaning up...")
    await sbx.kill()

if __name__ == "__main__":
    asyncio.run(test_connection())

```

--------------------------------

### Inspect Docker Buildx Builder Configuration

Source: https://docs.docker.com/build/building/cdi

Inspects the configuration of an existing Docker Buildx builder, named 'gpubuilder' in this example. It displays details such as the driver, nodes, BuildKit version, supported platforms, and crucially, the detected devices like 'nvidia.com/gpu'. This command helps verify that GPU support has been correctly set up.

```console
docker buildx inspect gpubuilder
```

--------------------------------

### Install gnome-terminal on Fedora

Source: https://docs.docker.com/desktop/setup/install/linux/fedora

Installs the gnome-terminal package, which is required for terminal access from Docker Desktop if not using GNOME.

```bash
$ sudo dnf install gnome-terminal
```

--------------------------------

### Disable Docker Desktop Analytics via MSI Installer

Source: https://docs.docker.com/enterprise/enterprise-deployment/msi-install-and-configure

This command demonstrates how to disable anonymous usage statistics collection during Docker Desktop installation using the MSI installer. It utilizes the `DISABLEANALYTICS=1` property.

```powershell
msiexec /i "win\msi\bin\en-US\DockerDesktop.msi" /L*V ".\msi.log" DISABLEANALYTICS=1
```

--------------------------------

### Containerize Deno Application with Docker

Source: https://docs.docker.com/llms

Learn how to create a Docker container for your Deno application. This guide helps you package your Deno project for consistent deployment.

```Dockerfile
# Example Dockerfile for a Deno application
FROM denoland/deno

WORKDIR /app

COPY . .

RUN deno cache main.ts

EXPOSE 8000

CMD ["run", "--allow-net", "main.ts"]
```

--------------------------------

### Check Docker and Docker Compose Versions

Source: https://docs.docker.com/desktop/setup/install/linux/ubuntu

These commands verify the installed versions of Docker Compose and the Docker CLI. This is useful after installation or upgrades to ensure the correct versions are active.

```console
docker compose version
docker --version
docker version
```

--------------------------------

### Stop and Start Docker Service

Source: https://docs.docker.com/engine/storage/drivers/vfs-driver

Commands to stop and start the Docker service using systemctl. These are necessary steps when modifying the Docker daemon configuration.

```bash
$ sudo systemctl stop docker
```

```bash
$ sudo systemctl start docker
```

--------------------------------

### List Active ROS 2 Topics

Source: https://docs.docker.com/guides/ros2/turtlesim-example

Lists all currently active topics in the ROS 2 system. This is useful for understanding the communication channels between nodes.

```bash
ros2 topic list
```

--------------------------------

### Docker Desktop Installer Flags: Proxy Configuration (Embedded PAC Script)

Source: https://docs.docker.com/desktop/setup/install/windows-install

Illustrates how to specify an embedded Proxy Auto-Config (PAC) script directly within the installer command. This method takes precedence over a PAC file URL when both are specified.

```console
"Docker Desktop Installer.exe" install --proxy-http-mode="manual" --override-proxy-embedded-pac="function FindProxyForURL(url, host) { return \"DIRECT\"; }"
```

--------------------------------

### Build Local Binary with Buildx Bake (Console)

Source: https://docs.docker.com/guides/bake

This command executes the 'bin' target defined in the `docker-bake.hcl` file using `docker buildx bake`. It triggers the build process and exports the compiled binary for the local platform to the './build/bin' directory.

```bash
docker buildx bake bin
```

--------------------------------

### Update apt and install Docker Desktop DEB package on Debian

Source: https://docs.docker.com/desktop/setup/install/linux/debian

Updates the apt package list and installs the Docker Desktop DEB package. This is part of the recommended installation process for Docker Desktop on Debian.

```bash
sudo apt-get update
$ sudo apt-get install ./docker-desktop-amd64.deb
```

--------------------------------

### Install D-Bus for User Sessions

Source: https://docs.docker.com/engine/security/rootless/troubleshoot

This snippet shows commands to install the D-Bus user session package, which can resolve errors related to OCI runtime creation failures on cgroup v2 hosts. It provides package installation commands for Debian/Ubuntu and Fedora/RHEL based systems.

```shell
# For Debian/Ubuntu:
sudo apt-get install -y dbus-user-session

# For Fedora/RHEL:
sudo dnf install -y dbus-daemon

# After installation, relogin and try:
systemctl --user enable --now dbus
```

--------------------------------

### Update Container Kernel Memory (Stopped or Running)

Source: https://docs.docker.com/reference/cli/docker/container/update

This example illustrates updating a container's kernel memory limit. For kernel versions older than 4.6, this requires the container to be stopped or started with `--kernel-memory`. For newer kernels, it can be updated on running containers without this restriction. Note: `--kernel-memory` is deprecated since Docker 20.10.

```console
docker run -dit --name test --kernel-memory 50M ubuntu bash
docker update --kernel-memory 80M test
```

```console
docker run -dit --name test2 --memory 300M ubuntu bash
# Update kernel memory of running container test2 will fail.
You need to stop the container before updating the --kernel-memory setting.
```

--------------------------------

### Docker Buildx with Scoped GitHub Actions Cache

Source: https://docs.docker.com/build/cache/backends/gha

This example shows how to use the GitHub Actions cache with specific scopes for different images. By setting the 'scope' parameter to the image name, each image gets its own isolated cache, preventing overwrites between builds. This requires specifying the cache type as 'gha' and providing URL and token parameters.

```console
docker buildx build --push -t <registry>/<image> \
  --cache-to type=gha,url=...,token=...,scope=image \
  --cache-from type=gha,url=...,token=...,scope=image .

```

```console
docker buildx build --push -t <registry>/<image2> \
  --cache-to type=gha,url=...,token=...,scope=image2 \
  --cache-from type=gha,url=...,token=...,scope=image2 .
```

--------------------------------

### Scan Docker Hardened Image with Trivy

Source: https://docs.docker.com/llms

This example demonstrates how to scan a Docker Hardened Image for known vulnerabilities using Trivy. It shows the command-line usage for initiating a scan and interpreting the results.

```bash
trivy image docker.io/your-org/my-hardened-image:1.0.0
```

--------------------------------

### Install Specific Docker Engine Version

Source: https://docs.docker.com/engine/install/debian

Installs a specific version of Docker Engine. It first lists available versions and then uses a version string to install the desired package, ensuring compatibility or specific feature requirements.

```console
$ VERSION_STRING=5:29.2.1-1~debian.12~bookworm
$ sudo apt install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-buildx-plugin docker-compose-plugin
```

--------------------------------

### Execute Command in PostgreSQL Container

Source: https://docs.docker.com/guides/dotnet/develop

Executes a command within a specified Docker container. This example connects to a PostgreSQL database named 'example' as the 'postgres' user, using the container ID.

```console
docker exec -it 39fdcf0aff7b psql -d example -U postgres
```

--------------------------------

### Dockerfile CMD/ENTRYPOINT Exec Form Recommendation

Source: https://docs.docker.com/compose/support-and-feedback/faq

Provides an example of the recommended 'exec' form for `CMD` and `ENTRYPOINT` directives in a Dockerfile. Using the JSON array format `["program", "arg1", "arg2"]` ensures proper signal handling within containers, unlike the string form.

```dockerfile
# Recommended exec form
CMD ["program", "arg1", "arg2"]

# Avoid this string form
# CMD "program arg1 arg2"
```

--------------------------------

### Install Docker Compose Plugin using YUM (RPM-based)

Source: https://docs.docker.com/compose/install/linux

Installs the latest version of the Docker Compose plugin on RPM-based Linux distributions (like CentOS, Fedora) using the YUM package manager. This command updates the package index and then installs the 'docker-compose-plugin' package. It assumes Docker Engine and CLI are already installed.

```bash
$ sudo yum update
$ sudo yum install docker-compose-plugin
```

--------------------------------

### Simulate System Account Installation for docker-users Group Issue (PowerShell)

Source: https://docs.docker.com/enterprise/enterprise-deployment/faq

This command uses PsExec to run the Docker Desktop MSI installer in the context of the system account. This helps reproduce an issue where the 'docker-users' group is not populated correctly during MDM deployments, as MDM solutions often run installers under the system account.

```powershell
psexec -i -s msiexec /i "DockerDesktop.msi"

```

--------------------------------

### Install gnome-terminal on Debian

Source: https://docs.docker.com/desktop/setup/install/linux/debian

Installs the gnome-terminal package, which is required for terminal access from Docker Desktop if not using the GNOME desktop environment.

```bash
sudo apt install gnome-terminal
```

--------------------------------

### Dockerfile Syntax and Comments

Source: https://docs.docker.com/guides/golang/build-images

Demonstrates the correct placement of Dockerfile directives (like syntax) and comments. Directives must be at the very top, followed by comments, and then the rest of the Dockerfile instructions.

```dockerfile
# syntax=docker/dockerfile:1
# A sample microservice in Go packaged into a container image.

FROM golang:1.19

# ...
```

--------------------------------

### Clone Bun Docker Sample Application

Source: https://docs.docker.com/guides/bun/develop

Clones the sample Bun Docker application repository to your local machine. This command requires Git to be installed and accessible in your terminal.

```console
git clone https://github.com/dockersamples/bun-docker.git && cd bun-docker
```

--------------------------------

### Install BuildKit Binaries and Update PATH

Source: https://docs.docker.com/build/buildkit

Installs the extracted BuildKit binaries into the Program Files directory and updates the system's PATH environment variable. This makes the `buildkitd.exe` and `buildctl.exe` commands accessible from any terminal.

```powershell
# after the binaries are extracted in the bin directory
# move them to an appropriate path in your $Env:PATH directories or:
Copy-Item -Path ".\bin" -Destination "$Env:ProgramFiles\buildkit" -Recurse -Force
# add `buildkitd.exe` and `buildctl.exe` binaries in the $Env:PATH
$Path = [Environment]::GetEnvironmentVariable("PATH", "Machine") +
    [IO.Path]::PathSeparator + "$Env:ProgramFiles\buildkit"
[Environment]::SetEnvironmentVariable( "Path", $Path, "Machine")
$Env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" +
    [System.Environment]::GetEnvironmentVariable("Path","User")
```

--------------------------------

### Building Docker Image with Dockerfile from Stdin

Source: https://docs.docker.com/build/building/context

Shows how to build a Docker image using a local directory as the build context while providing the Dockerfile content via standard input using a here-document. This is useful for dynamic Dockerfile creation.

```bash
# create a directory to work in
mkdir example
cd example

# create an example file
touch somefile.txt

# build an image using the current directory as context
# and a Dockerfile passed through stdin
docker build -t myimage:latest -f- . <<EOF
FROM busybox
COPY somefile.txt ./
RUN cat /somefile.txt
EOF

```

--------------------------------

### Install Docker Engine RPM packages on RHEL

Source: https://docs.docker.com/engine/install/rhel

Installs Docker Engine, CLI, containerd, and Docker Compose by using `dnf` to install the downloaded RPM files. This command assumes you have downloaded the necessary .rpm files to the current directory.

```bash
sudo dnf install ./containerd.io-<version>.<arch>.rpm \
  ./docker-ce-<version>.<arch>.rpm \
  ./docker-ce-cli-<version>.<arch>.rpm \
  ./docker-buildx-plugin-<version>.<arch>.rpm \
  ./docker-compose-plugin-<version>.<arch>.rpm
```

--------------------------------

### List Docker Images using API

Source: https://docs.docker.com/reference/api/engine/sdk/examples

Lists all images available on the Docker host, similar to the `docker image ls` command. This functionality is implemented using the Docker SDK for Go or Python, or by making direct HTTP requests to the Docker API.

```go
package main

import (
	"context"
	"fmt"

	"github.com/moby/moby/client"
)

func main() {
	ctx := context.Background()
	apiClient, err := client.New(client.FromEnv)
	if err != nil {
		panic(err)
	}
	defer apiClient.Close()

	images, err := apiClient.ImageList(ctx, client.ImageListOptions{})
	if err != nil {
		panic(err)
	}

	for _, image := range images.Items {
		fmt.Println(image.ID)
	}
}
```

```python
import docker
client = docker.from_env()
for image in client.images.list():
  print(image.id)
```

```http
$ curl --unix-socket /var/run/docker.sock http://localhost/v1.53/images/json
[
{
  "Id":"sha256:31d9a31e1dd803470c5a151b8919ef1988ac3efd44281ac59d43ad623f275dcd",
  "ParentId":"sha256:ee4603260daafe1a8c2f3b78fd760922918ab2441cbb2853ed5c439e59c52f96",
  ...
}]
```

--------------------------------

### List Available Docker Engine Versions (Fedora)

Source: https://docs.docker.com/engine/install/fedora

Lists all available versions of Docker Engine in the repository, sorted in descending order. This is useful for identifying the exact version string needed for a specific installation.

```bash
dnf list docker-ce --showduplicates | sort -r
```

--------------------------------

### Initialize Docker Assets with Docker Init (Java)

Source: https://docs.docker.com/guides/java/containerize

Demonstrates the interactive prompts and responses for the `docker init` command when containerizing a Java application. It helps generate Dockerfile, .dockerignore, and compose.yaml files.

```console
$ docker init
Welcome to the Docker Init CLI!

This utility will walk you through creating the following files with sensible defaults for your project:
  - .dockerignore
  - Dockerfile
  - compose.yaml
  - README.Docker.md

Let's get started!

WARNING: The following Docker files already exist in this directory:
  - docker-compose.yml
? Do you want to overwrite them? Yes
? What application platform does your project use? Java
? What's the relative directory (with a leading .) for your app? ./src
? What version of Java do you want to use? 21
? What port does your server listen on? 8080
```

--------------------------------

### Start Container API Request (POST)

Source: https://docs.docker.com/reference/api/engine/latest

This API endpoint initiates the start of a specified Docker container. It accepts the container ID as a path parameter and an optional `detachKeys` query parameter to override the default detachment key sequence. Responses include 204 for success, 304 if already started, 404 if the container is not found, and 500 for server errors.

```http
POST /v1.53/containers/{id}/start?detachKeys=<string> HTTP/1.1
Host: localhost:2375
Content-Type: application/json


```

--------------------------------

### Start Docker daemon with flags (Console)

Source: https://docs.docker.com/engine/daemon

Manually start the Docker daemon using command-line flags for configuration. This is useful for troubleshooting and allows overriding JSON file settings. Ensure correct paths for certificates and host configuration.

```console
dockerd --debug \
  --tls=true \
  --tlscert=/var/docker/server.pem \
  --tlskey=/var/docker/serverkey.pem \
  --host tcp://192.168.59.3:2376
```

--------------------------------

### Install Docker Engine Packages

Source: https://docs.docker.com/engine/install/raspberry-pi-os

Installs Docker Engine packages on Debian-based systems. This includes the Docker CE, CLI, containerd.io, and necessary plugins. Users can choose to install the latest version or a specific version.

```bash
# Install the latest version:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```bash
# List the available versions:
apt-cache madison docker-ce | awk '{ print $3 }'

# Install a specific version:
VERSION_STRING=5:29.2.1-1~raspbian.12~bookworm
sudo apt-get install docker-ce=$VERSION_STRING docker-ce-cli=$VERSION_STRING containerd.io docker-buildx-plugin docker-compose-plugin
```

--------------------------------

### Manage Service Mounts (Add and Remove)

Source: https://docs.docker.com/reference/cli/docker/service/update

Demonstrates adding and removing mounts (volumes or bind mounts) for a Docker service. It covers creating a service with a mount, updating it to add another mount, and then removing a mount by its target path.

```console
docker service create \
    --name=myservice \
    --mount type=volume,source=test-data,target=/somewhere \
    nginx:alpine

myservice

docker service update \
    --mount-add type=volume,source=other-volume,target=/somewhere-else \
    myservice

myservice

docker service update --mount-rm /somewhere myservice

myservice
```

--------------------------------

### Security Validation Example (Console)

Source: https://docs.docker.com/enterprise/security/hardened-desktop/enhanced-container-isolation/config

This console example demonstrates how Docker Desktop validates image digests against an allowlist. It shows that re-tagging a malicious image to match an allowed image name (like 'docker:cli') will fail if the underlying image digest does not match the trusted image.

```bash
$ docker tag malicious-image docker:cli
$ docker run -v /var/run/docker.sock:/var/run/docker.sock docker:cli
# This fails because the digest doesn't match the real docker:cli image
```

--------------------------------

### Install Docker Desktop Package on Arch Linux

Source: https://docs.docker.com/desktop/setup/install/linux/archlinux

This command installs the Docker Desktop package on an Arch-based Linux distribution using `pacman`. The package is typically downloaded from the release notes. Docker Desktop will be installed in `/opt/docker-desktop` by default.

```console
$ sudo pacman -U ./docker-desktop-x86_64.pkg.tar.zst
```

--------------------------------

### Registry Authentication Configuration Example

Source: https://docs.docker.com/reference/api/engine/latest

Example of the `X-Registry-Config` header value for the Docker build API, showing a base64-encoded JSON object for authenticating with multiple registries. Includes configurations for `docker.example.com` and Docker Hub.

```json
{
  "docker.example.com": {
    "username": "janedoe",
    "password": "hunter2"
  },
  "https://index.docker.io/v1/": {
    "username": "mobydock",
    "password": "conta1n3rize14"
  }
}
```

--------------------------------

### Configure Windowsfilter Storage Driver Options

Source: https://docs.docker.com/reference/cli/dockerd

This example shows how to configure the Docker daemon on Windows to use the Windowsfilter storage driver and specify a custom size for container sandboxes using the --storage-opt size flag. This allows for adjusting the default sandbox size.

```powershell
C:\> dockerd --storage-opt size=40G

```

--------------------------------

### Stop Docker Offload using CLI

Source: https://docs.docker.com/offload/quickstart

Terminates the Docker Offload service and its associated cloud environment. This action removes all running containers and images. The service can also automatically idle and terminate after a period of inactivity.

```bash
docker offload stop
```

--------------------------------

### Install Ruff Linter and Formatter

Source: https://docs.docker.com/guides/python/lint-format-typing

Installs the Ruff package, a fast Python linter and formatter, using pip. Ensure your virtual environment is activated before running this command.

```bash
pip install ruff
```

--------------------------------

### llama.cpp API Endpoint Example

Source: https://docs.docker.com/ai/model-runner/inference-engines

Provides an example of the API endpoint path used for chat completions when the llama.cpp inference engine is active.

```text
POST /engines/llama.cpp/v1/chat/completions
```

--------------------------------

### Docker Compose Service Management Commands

Source: https://docs.docker.com/compose/support-and-feedback/faq

Explains the primary functions of `docker compose up`, `docker compose run`, and `docker compose start`. `up` is for starting/restarting all services, `run` is for one-off tasks, and `start` is for restarting previously created but stopped containers.

```console
# Start or restart all services (attached mode)
docker compose up

# Start or restart all services (detached mode)
docker compose up -d

# Run a one-off task for a specific service
docker compose run <service_name>

# Start containers that were previously created and stopped
docker compose start
```

--------------------------------

### Limit Container CPU Usage with --cpus

Source: https://docs.docker.com/engine/containers/resource_constraints

This example demonstrates how to limit a container's CPU usage to a fraction of the host machine's available CPUs. The `--cpus` flag provides a convenient way to set CPU limits, equivalent to manually configuring `--cpu-period` and `--cpu-quota`.

```bash
docker run -it --cpus=".5" ubuntu /bin/bash
```

--------------------------------

### Clone C++ Docker Sample Application

Source: https://docs.docker.com/guides/cpp/containerize

Clones the sample C++ application repository from GitHub. This is the first step to containerizing the application. It requires a Git client to be installed.

```console
git clone https://github.com/dockersamples/c-plus-plus-docker.git
```

--------------------------------

### Dockerfile RUN Instruction: Shell Form Example

Source: https://docs.docker.com/engine/reference/builder

Demonstrates the shell form of the RUN instruction, which is the most common. It allows for multi-line commands using newline escapes or heredocs, making longer instructions more readable.

```dockerfile
RUN <<EOF
apt-get update
apt-get install -y curl
EOF
```

--------------------------------

### Start Docker Application in Development Mode

Source: https://docs.docker.com/guides/nodejs/develop

Command to build and start the 'app-dev' service defined in the docker-compose.yml file. This command ensures the application is built with the latest changes and then runs it.

```bash
$ docker compose up app-dev --build
```

--------------------------------

### Run Sandbox Connection Script (Bash)

Source: https://docs.docker.com/guides/github-sonarqube-sandbox/workflow

Executes the TypeScript or Python script to create an E2B sandbox and verify MCP server configuration. This command assumes you have Node.js and tsx installed for TypeScript, or Python installed for the Python script.

```bash
npx tsx 01-test-connection.ts
```

```bash
python 01_test_connection.py
```

--------------------------------

### Docker Desktop Installer Flags: Proxy Configuration (PAC File)

Source: https://docs.docker.com/desktop/setup/install/windows-install

Demonstrates how to configure Docker Desktop to use a Proxy Auto-Config (PAC) file for proxy settings. This involves providing the URL to the PAC file.

```console
"Docker Desktop Installer.exe" install --proxy-http-mode="manual" --override-proxy-pac="http://localhost:8080/myproxy.pac"
```

--------------------------------

### Running cAdvisor Container with Docker

Source: https://docs.docker.com/storage/troubleshooting_volume_errors

This command demonstrates how to run the Google cAdvisor container, which requires bind-mounting the Docker system directory. This setup can lead to filesystem removal errors if not managed properly.

```bash
sudo docker run \
  --volume=/:/rootfs:ro \
  --volume=/var/run:/var/run:rw \
  --volume=/sys:/sys:ro \
  --volume=/var/lib/docker/:/var/lib/docker:ro \
  --publish=8080:8080 \
  --detach=true \
  --name=cadvisor \
  google/cadvisor:latest

```

--------------------------------

### Log in to Docker Hardened Images Registry

Source: https://docs.docker.com/dhi/get-started

Authenticates your Docker client with the DHI registry. This is a prerequisite for pulling DHI images.

```console
docker login dhi.io
```

--------------------------------

### Create Platform-Specific Shell Scripts for Host Execution

Source: https://docs.docker.com/extensions/extensions-sdk/guides/invoke-host-binaries

This snippet demonstrates creating 'hello world' scripts for both Unix-like systems (macOS, Linux) and Windows. These scripts accept a parameter and print a greeting. They are essential for invoking host binaries from your extension.

```bash
#!/bin/sh
echo "Hello, $1!"

```

```batch
@echo off
echo "Hello, %1!"

```

--------------------------------

### Test Internal Registry Policy with Dockerfile Examples

Source: https://docs.docker.com/build/policies/validate-images

These Dockerfile examples demonstrate how the internal registry policy works. It shows which image sources are allowed (Docker Hub, company registry) and which are denied (other registries).

```dockerfile
FROM alpine                                    # Allowed (Docker Hub)
FROM registry.company.com/myapp:latest         # Allowed (company registry)
FROM ghcr.io/someorg/image:latest              # Denied (wrong registry)
```

--------------------------------

### Install Docker Desktop RPM Package

Source: https://docs.docker.com/desktop/setup/install/linux/rhel

Installs the Docker Desktop RPM package on RHEL. This command assumes the RPM file has been downloaded to the current directory.

```bash
sudo dnf install ./docker-desktop-x86_64-rhel.rpm
```

--------------------------------

### Specify Network Prefix Size with Docker Subnet Options

Source: https://docs.docker.com/engine/release-notes/29

This example demonstrates how to request a specific prefix size for networks allocated from default pools using the `--subnet` option. This provides more granular control over network allocation. This functionality is available in recent Docker versions.

```bash
docker run ... --subnet 0.0.0.0/24 --subnet ::/96
```

--------------------------------

### Install gnome-terminal for Non-GNOME Desktops

Source: https://docs.docker.com/desktop/setup/install/linux/rhel

Installs the 'gnome-terminal' package. This is a requirement for users not using the GNOME desktop environment to enable terminal access from Docker Desktop.

```bash
sudo dnf install gnome-terminal
```

--------------------------------

### Mount Block Device as Volume in Docker Container

Source: https://docs.docker.com/storage/volumes

This process demonstrates creating an ext4 filesystem on a raw disk image, setting up a loop device, and mounting it as a volume within an Ubuntu container. It requires Linux kernel support for filesystem and loop devices.

```bash
$ fallocate -l 1G disk.raw
$ mkfs.ext4 disk.raw
$ losetup -f --show disk.raw
/dev/loop5
$ docker run -it --rm \
  --mount='type=volume,dst=/external-drive,volume-driver=local,volume-opt=device=/dev/loop5,volume-opt=type=ext4' \
  ubuntu bash
$ losetup -d /dev/loop5
```

--------------------------------

### Install CA Certificates Package in Container (Console)

Source: https://docs.docker.com/engine/network/ca-certs

This command updates the package list and installs the 'ca-certificates' package within a running Linux container. This is a prerequisite for updating the trusted certificate store.

```bash
apt-get update && apt-get install -y ca-certificates
```

--------------------------------

### Docker: Default Command and Options Syntax

Source: https://docs.docker.com/engine/reference/run

Illustrates the general syntax for the 'docker run' command, showing where to specify options, the image, and optional command and arguments to override the image's default CMD instruction.

```bash
$ docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]

```

--------------------------------

### Install and Extract Docker Binaries on Windows (PowerShell)

Source: https://docs.docker.com/engine/install/binaries

This snippet demonstrates how to extract the downloaded Docker static binary archive to the Program Files directory using PowerShell's Expand-Archive cmdlet. Ensure you replace '<FILE>.zip' with the actual downloaded filename.

```powershell
Expand-Archive /path/to/<FILE>.zip -DestinationPath $Env:ProgramFiles
```

--------------------------------

### Verify Docker Model Runner Installation

Source: https://docs.docker.com/ai/cagent/local-models

This command checks if Docker Model Runner is installed and accessible on your system. It should return version information if the installation is successful.

```console
docker model version
```

--------------------------------

### Scale BuildKit Replicas with Docker Buildx

Source: https://docs.docker.com/build/builders/drivers/kubernetes

This command demonstrates how to create and bootstrap a BuildKit builder named 'kube' using the Kubernetes driver, setting the namespace to 'buildkit' and scaling the number of replicas to 4. This allows for increased build load handling by distributing BuildKit pods across multiple nodes in a Kubernetes cluster.

```bash
docker buildx create \
  --bootstrap \
  --name=kube \
  --driver=kubernetes \
  --driver-opt=namespace=buildkit,replicas=4
```

--------------------------------

### Configure GitHub Actions CI/CD for Python

Source: https://docs.docker.com/llms

Automate build and deployment for Python applications using GitHub Actions. This guide focuses on setting up CI/CD pipelines.

```YAML
# Example GitHub Actions workflow for Python
name: Python CI/CD

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Python 3.9
      uses: actions/setup-python@v4
      with:
        python-version: '3.9'
    - name: Install dependencies
      run: pip install -r requirements.txt
    - name: Run tests
      run: pytest
```

--------------------------------

### Mount FUSE Filesystem with SYS_ADMIN and Device Access

Source: https://docs.docker.com/reference/run

Explains the necessary steps to mount a FUSE-based filesystem, requiring both the SYS_ADMIN capability and access to the /dev/fuse device. This example shows the commands to achieve this.

```bash
$ docker run --rm -it --cap-add SYS_ADMIN sshfs sshfs sven@10.10.10.20:/home/sven /mnt
fuse: failed to open /dev/fuse: Operation not permitted

$ docker run --rm -it --device /dev/fuse sshfs sshfs sven@10.10.10.20:/home/sven /mnt
fusermount: mount failed: Operation not permitted

$ docker run --rm -it --cap-add SYS_ADMIN --device /dev/fuse sshfs
# sshfs sven@10.10.10.20:/home/sven /mnt
The authenticity of host '10.10.10.20 (10.10.10.20)' can't be established.
ECDSA key fingerprint is 25:34:85:75:25:b0:17:46:05:19:04:93:b5:dd:5f:c6.
Are you sure you want to continue connecting (yes/no)? yes
sven@10.10.10.20's password:

root@30aa0cfaf1b5:/# ls -la /mnt/src/docker

total 1516
drwxrwxr-x 1 1000 1000   4096 Dec  4 06:08 .
drwxrwxr-x 1 1000 1000   4096 Dec  4 11:46 ..
-rw-rw-r-- 1 1000 1000     16 Oct  8 00:09 .dockerignore
-rwxrwxr-x 1 1000 1000    464 Oct  8 00:09 .drone.yml
drwxrwxr-x 1 1000 1000   4096 Dec  4 06:11 .git
-rw-rw-r-- 1 1000 1000    461 Dec  4 06:08 .gitignore
....

```

--------------------------------

### Use Docker Cache Mount for Ruby Gem Installs

Source: https://docs.docker.com/build/cache/optimize

This Dockerfile snippet shows how to use a cache mount for the Ruby gem directory (`/root/.gem`). This persists installed gems across builds, accelerating subsequent `bundle install` commands by reusing already installed gems.

```dockerfile
RUN --mount=type=cache,target=/root/.gem \
    bundle install
```

--------------------------------

### Mount Volume Subdirectory for Logs

Source: https://docs.docker.com/storage/volumes

Creates a volume named 'logs', initializes subdirectories 'app1' and 'app2' within it, and then starts two containers, each mounting a specific subdirectory of the 'logs' volume. This isolates logs for each container.

```bash
$ docker volume create logs
$ docker run --rm \
  --mount src=logs,dst=/logs \
  alpine mkdir -p /logs/app1 /logs/app2
$ docker run -d \
  --name=app1 \
  --mount src=logs,dst=/var/log/app1,volume-subpath=app1 \
  app1:latest
$ docker run -d \
  --name=app2 \
  --mount src=logs,dst=/var/log/app2,volume-subpath=app2 \
  app2:latest

```

--------------------------------

### GET /websites/docker/HttpService

Source: https://docs.docker.com/reference/api/extensions-sdk/HttpService

Performs an HTTP GET request to a backend service.

```APIDOC
## GET /websites/docker/HttpService

### Description
Performs an HTTP GET request to a backend service.

### Method
GET

### Endpoint
/websites/docker/HttpService

### Parameters
#### Query Parameters
- **url** (string) - Required - The URL of the backend service.

### Request Example
```typescript
ddClient.extension.vm.service.get("/some/service").then((value: any) => console.log(value))
```

### Response
#### Success Response (200)
- **unknown** (unknown) - The response from the backend service.

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Example: Configure Local Logging with Max Size and File Count

Source: https://docs.docker.com/engine/logging/drivers/local

An example demonstrating how to configure a container to use the 'local' logging driver with specific limits on log file size (`max-size`) and the maximum number of log files (`max-file`). This ensures logs do not exceed 10MB per file and are limited to 3 files.

```bash
$ docker run -it --log-driver local --log-opt max-size=10m --log-opt max-file=3 alpine ash
```

--------------------------------

### Runtime Execution of Docker Image

Source: https://docs.docker.com/engine/reference/builder

This example shows how to build and run a Docker image created with the previous Dockerfile. It demonstrates how to override the ARG variable at runtime using the -e flag with 'docker run', showing the dynamic output of the script.

```bash
docker build -t heredoc .
docker run -e FOO=world heredoc
```

--------------------------------

### Run containerd Standalone using dockerd CLI

Source: https://docs.docker.com/reference/cli/dockerd

This command allows manual control over the `containerd` startup process. By passing the path to the `containerd` socket using the `--containerd` flag, the Docker daemon will use the manually started `containerd` instance instead of starting its own.

```bash
$ sudo dockerd --containerd /run/containerd/containerd.sock
```

--------------------------------

### Publish UDP Ports on Overlay Network (Newer Syntax)

Source: https://docs.docker.com/engine/swarm/networking

This example demonstrates publishing a UDP port on an overlay network using the newer comma-separated value syntax. It maps UDP port 80 on the service to port 8080 on the routing mesh. This syntax enhances readability for UDP port configurations.

```console
-p published=8080,target=80,protocol=udp
```

--------------------------------

### Create Dockerfile with ADD instruction

Source: https://docs.docker.com/build/policies/intro

A simple Dockerfile that uses the ADD instruction to download a file from a specified URL. This is used to demonstrate policy validation.

```dockerfile
FROM scratch
ADD https://example.com/index.html /index.html
```

--------------------------------

### Containerize React.js Application with Docker

Source: https://docs.docker.com/llms

Learn to containerize a React.js application using Docker. This guide covers creating optimized, production-ready images with best practices for performance and security.

```Dockerfile
# Example Dockerfile for a React.js application (multi-stage build)
# Build stage
FROM node:18-alpine as build

WORKDIR /app

COPY package*.json ./ 
RUN npm install

COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80
```

--------------------------------

### GitHub Actions: Build with Docker Buildx CLI

Source: https://docs.docker.com/build-cloud/ci

This example demonstrates how to use the `docker buildx build` command directly within a GitHub Actions workflow after setting up Docker Buildx with a cloud builder. It utilizes the `BUILDX_BUILDER` environment variable to specify the cloud builder.

```yaml
- name: Set up Docker Buildx
  id: builder
  uses: docker/setup-buildx-action@v3
  with:
    driver: cloud
    endpoint: "${{ vars.DOCKER_ACCOUNT }}/${{ vars.CLOUD_BUILDER_NAME }}"

- name: Build
  run: |
    docker build . 
  env:
    BUILDX_BUILDER: ${{ steps.builder.outputs.name }}
```

--------------------------------

### Basic RUN with SHELL Instruction (Windows)

Source: https://docs.docker.com/reference/dockerfile

A simple Dockerfile example demonstrating the initial use of the SHELL instruction to set the default shell to cmd /S /C before a RUN command.

```dockerfile
SHELL ["cmd", "/S", "/C"]
RUN echo hello
```

--------------------------------

### Raw Log Message Format Example (Console)

Source: https://docs.docker.com/engine/logging/drivers/splunk

The raw format prefixes attributes and tags directly to the message. This example demonstrates how both simple strings and JSON objects are formatted.

```console
MyImage/MyContainer env1=val1 label1=label1 my message
```

```console
MyImage/MyContainer env1=val1 label1=label1 {"foo": "bar"}
```

--------------------------------

### Start Containers on Isolated IPvlan Networks

Source: https://docs.docker.com/engine/network/drivers/ipvlan

Starts containers attached to networks created with the '--internal' flag or without a specified parent interface, demonstrating isolated network creation.

```bash
$ docker run --net=isolated1 --name=cid1 -it --rm alpine /bin/sh
$ docker run --net=isolated2 --name=cid2 -it --rm alpine /bin/sh
$ docker run --net=isolated3 --name=cid3 -it --rm alpine /bin/sh
```

--------------------------------

### Multi-stage Dockerfile with Hardened Images

Source: https://docs.docker.com/dhi/migration/migrate-from-doi

This example demonstrates a multi-stage Dockerfile using hardened images for both the build and runtime stages. The build stage compiles the application, and the runtime stage copies only the necessary artifacts, resulting in a minimal and secure final image.

```dockerfile
# Build stage
FROM dhi.io/golang:1.25-debian12-dev AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

# Runtime stage
FROM dhi.io/golang:1.25-debian12
WORKDIR /app
COPY --from=builder /app/myapp .
ENTRYPOINT ["/app/myapp"]
```

--------------------------------

### Create and Use Docker Config with Redis Service (Linux)

Source: https://docs.docker.com/engine/swarm/configs

This snippet demonstrates how to create a Docker config from standard input, attach it to a Redis service, and verify its content. It also shows how to remove the config after detaching it from the service. Dependencies include Docker and a Redis image.

```console
echo "This is a config" | docker config create my-config -
docker service create --name redis --config my-config redis:alpine
docker service ps redis
docker ps --filter name=redis -q
docker container exec $(docker ps --filter name=redis -q) ls -l /my-config
docker container exec $(docker ps --filter name=redis -q) cat /my-config
docker config ls
docker config rm my-config
docker service update --config-rm my-config redis
docker container exec -it $(docker ps --filter name=redis -q) cat /my-config
docker service rm redis
docker config rm my-config
```

--------------------------------

### Node.js Dockerfile Migration to Docker Hardened Images (DOI)

Source: https://docs.docker.com/dhi/migration/examples/node

This Dockerfile example illustrates a Node.js application prior to migrating to Docker Hardened Images, using a Docker Official Image (DOI). It outlines the process of setting the working directory, copying package files, installing npm dependencies, copying source code, and defining the command to execute the Node.js application.

```dockerfile
#syntax=docker/dockerfile:1

FROM node:latest
WORKDIR /usr/src/app

COPY package*.json ./

# Install any additional packages if needed using apt
# RUN apt-get update && apt-get install -y python3 make g++ && rm -rf /var/lib/apt/lists/*

RUN npm install

COPY . .

CMD ["node", "index.js"]
```

--------------------------------

### Start cagent A2A Server (CLI)

Source: https://docs.docker.com/ai/cagent/integrations/a2a

Demonstrates the basic command to start a cagent agent in A2A mode. This exposes the agent as an HTTP server accessible by other systems. It requires a YAML configuration file for the agent.

```console
$ cagent a2a ./agent.yaml
```

```console
$ cagent a2a ./agent.yaml --port 8080
```

```console
$ cagent a2a ./agent.yaml --agent engineer
```

```console
$ cagent a2a agentcatalog/pirate --port 9000
```

--------------------------------

### Configure HAProxy for External Load Balancing in Docker Swarm

Source: https://docs.docker.com/engine/swarm/ingress

This HAProxy configuration example demonstrates how to set up an external load balancer to distribute traffic to Docker Swarm nodes. It configures HAProxy to listen on port 80 and forward requests to swarm nodes on port 8080, which is assumed to be the published port for the swarm service. This setup works with or without the Swarm routing mesh.

```bash
global
        log /dev/log    local0
        log /dev/log    local1 notice
...
snip...

# Configure HAProxy to listen on port 80
frontend http_front
   bind *:80
   stats uri /haproxy?stats
   default_backend http_back

# Configure HAProxy to route requests to swarm nodes on port 8080
backend http_back
   balance roundrobin
   server node1 192.168.99.100:8080 check
   server node2 192.168.99.101:8080 check
   server node3 192.168.99.102:8080 check
```

--------------------------------

### Publish Ports on Overlay Network (Legacy Syntax)

Source: https://docs.docker.com/engine/swarm/networking

This example shows how to publish a service port on an overlay network using the legacy colon-separated syntax. It maps TCP port 80 on the service to port 8080 on the routing mesh. This is a common way to make service ports accessible outside the swarm.

```console
-p 8080:80
```

--------------------------------

### Continuous Integration for Docker Extensions (YAML)

Source: https://docs.docker.com/llms

An example of a CI configuration for automatically testing and validating Docker extensions. This snippet outlines the steps typically involved in a CI pipeline for extensions.

```yaml
name: Docker Extension CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
    - name: Install dependencies
      run: npm install
    - name: Build extension
      run: npm run build
    - name: Run tests
      run: npm test
    - name: Validate extension
      run: docker extension validate ./dist
```

--------------------------------

### Create Docker Service with Resource Constraints (CLI)

Source: https://docs.docker.com/engine/swarm/services

This command creates a Docker service named 'my-nginx' with 5 replicas, constrained to run only on nodes where the label 'region' is set to 'east'. It demonstrates the use of `--constraint` flag for placement.

```console
docker service create \
  --name my-nginx \
  --replicas 5 \
  --constraint node.labels.region==east \
  nginx
```

--------------------------------

### Install Docker Rootless Mode Without Packages

Source: https://docs.docker.com/engine/security/rootless

Installs Docker in rootless mode using a curl script from `get.docker.com/rootless`. This method is suitable when package managers are not available. Binaries are installed in `~/bin`.

```bash
$ curl -fsSL https://get.docker.com/rootless | sh
```

--------------------------------

### Publish Ports on Overlay Network (Newer Syntax)

Source: https://docs.docker.com/engine/swarm/networking

This example shows how to publish a service port on an overlay network using the newer comma-separated value syntax. It maps TCP port 80 on the service to port 8080 on the routing mesh. This syntax is more self-documenting and preferred for clarity.

```console
-p published=8080,target=80
```

--------------------------------

### Install Latest Docker Engine Packages

Source: https://docs.docker.com/engine/install/debian

Installs the latest stable version of Docker Engine, including the CLI and necessary plugins, using the apt package manager. This is the recommended method for most users.

```console
$ sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

--------------------------------

### Example Resolved Build Configuration JSON

Source: https://docs.docker.com/build/bake/variables

An example of the JSON output generated by `docker buildx bake --print`, showcasing the interpolated variable values within the build configuration.

```json
{
  "group": {
    "default": {
      "targets": ["webapp"]
    }
  },
  "target": {
    "webapp": {
      "context": ".",
      "dockerfile": "Dockerfile",
      "tags": ["docker.io/username/webapp:latest"]
    }
  }
}
```

--------------------------------

### Configure GPU Support in Docker Desktop for Windows

Source: https://docs.docker.com/llms

Guide on how to enable and use GPU acceleration within Docker Desktop on Windows. This allows containers to access the host machine's GPU, which is essential for machine learning, deep learning, and other GPU-intensive workloads.

```bash
# Enable GPU support in Docker Desktop settings:
# Settings > Resources > WSL INTEGRATION > Enable "Use the host's GPUs when running containers"
```

--------------------------------

### Start Traefik Container with Docker Provider (Hardened Image)

Source: https://docs.docker.com/guides/traefik

Starts a Traefik container in detached mode using the Docker Hardened Image. It connects to the 'traefik-demo' network, exposes port 80, mounts the Docker socket for configuration updates, and enables the Docker provider.

```bash
docker login dhi.io
docker run -d --network=traefik-demo \
  -p 80:80 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  dhi.io/traefik:3.6.2 \
  --providers.docker
```

--------------------------------

### Docker V0 Plugin Configuration Example (JSON)

Source: https://docs.docker.com/engine/extend/config

An example of a Docker V0 plugin configuration serialized in JSON format. This configuration specifies details for a sample volume plugin, including its description, entrypoint, environment variables, interface type, and network settings.

```json
{
  "Args": {
    "Description": "",
    "Name": "",
    "Settable": null,
    "Value": null
  },
  "Description": "A sample volume plugin for Docker",
  "Documentation": "https://docs.docker.com/engine/extend/plugins/",
  "Entrypoint": [
    "/usr/bin/sample-volume-plugin",
    "/data"
  ],
  "Env": [
    {
      "Description": "",
      "Name": "DEBUG",
      "Settable": [
        "value"
      ],
      "Value": "0"
    }
  ],
  "Interface": {
    "Socket": "plugin.sock",
    "Types": [
      "docker.volumedriver/1.0"
    ]
  },
  "Linux": {
    "Capabilities": null,
    "AllowAllDevices": false,
    "Devices": null
  },
  "Mounts": null,
  "Network": {
    "Type": ""
  },
  "PropagatedMount": "/data",
  "User": {},
  "Workdir": ""
}
```

--------------------------------

### Create a Docker Volume and Use it in a Container

Source: https://docs.docker.com/reference/cli/docker/volume/create

This snippet demonstrates the basic workflow of creating a Docker volume named 'hello' and then running a container that mounts this volume to the '/world' directory. It highlights how to persist data across container lifecycles.

```console
docker volume create hello

hello

docker run -d -v hello:/world busybox ls /world
```

--------------------------------

### Select Container Runtime with Docker Run

Source: https://docs.docker.com/reference/cli/dockerd

This command demonstrates how to select a specific container runtime, such as a Kata Containers shim, when running a Docker container. This is useful when the runtime is installed on the system's PATH.

```console
docker run --runtime io.containerd.kata.v2
```

--------------------------------

### Install QEMU for Multi-Platform Builds (Shell)

Source: https://docs.docker.com/build/building/multi-platform

Installs QEMU binaries and registers them with binfmt_misc on the host OS to enable emulation of non-native file formats. This is necessary for builders outside of Docker Desktop, such as Docker Engine on Linux. It requires Linux kernel version 4.8+ and binfmt-support 2.1.7+.

```shell
docker run --privileged --rm tonistiigi/binfmt --install all
```

--------------------------------

### Docker Custom Certificate Directory Structure Example

Source: https://docs.docker.com/desktop/troubleshoot-and-support/faqs/macfaqs

This example shows a typical directory structure for custom certificates used by Docker. The `ca.crt` file is the certificate authority that signed the registry's certificate, and `client.cert` and `client.key` are for client authentication. This structure is recognized by Docker Desktop.

```text
/etc/docker/certs.d/        <-- Certificate directory
└── localhost:5000          <-- Hostname:port
   ├── client.cert          <-- Client certificate
   ├── client.key           <-- Client key
   └── ca.crt               <-- Certificate authority that signed
                                the registry certificate
```

--------------------------------

### GET /containers/list

Source: https://docs.docker.com/engine/release-notes/27

Lists containers. Now returns container annotations.

```APIDOC
## GET /containers/list

### Description
Lists containers. Now returns container annotations.

### Method
GET

### Endpoint
`/containers/list`

### Parameters
#### Query Parameters
- **all** (boolean) - Optional - Show all containers (default: false).
- **size** (boolean) - Optional - Show the size of the container (default: false).
- **filters** (map) - Optional - A JSON encoded map of filters to process on the list of containers.

### Response
#### Success Response (200)
- **Id** (string) - The ID of the container.
- **Names** (array) - An array of names for the container.
- **Image** (string) - The image used by the container.
- **State** (string) - The current state of the container.
- **Status** (string) - The status of the container.
- **Labels** (map) - A map of labels associated with the container.
- **Annotations** (map) - A map of annotations associated with the container.

#### Response Example
```json
[
  {
    "Id": "container_id",
    "Names": ["/my_container"],
    "Image": "ubuntu:latest",
    "State": "running",
    "Status": "up 10 minutes",
    "Labels": {},
    "Annotations": {"my.annotation": "value"}
  }
]
```
```

--------------------------------

### Debug a Container with No Shell (hello-world)

Source: https://docs.docker.com/reference/cli/docker/debug

Demonstrates how to get a debug shell into a container that lacks a shell, like the `hello-world` image. It shows how to inspect the filesystem and execute binaries within the debug environment. This is useful for understanding the contents of minimal containers.

```console
docker run --name my-app hello-world
docker debug my-app
docker > ls
dev  etc  hello  nix  proc  sys
docker > /hello
```

--------------------------------

### POST /commit

Source: https://docs.docker.com/reference/api/engine/sdk/examples

Commits the state of a container to create a new image.

```APIDOC
## Commit a container

### Description
Commit a container to create an image from its contents.

### Method
POST

### Endpoint
/commit

### Query Parameters
- **container** (string) - Required - The ID of the container to commit.
- **repo** (string) - Required - The name of the repository for the new image.
- **tag** (string) - Optional - The tag for the new image.
- **comment** (string) - Optional - A comment describing the new image.
- **author** (string) - Optional - The author of the new image.
- **changes** (array) - Optional - A list of strings representing changes to apply to the image (e.g., `["CMD=/usr/sbin/nginx", "ENTRYPOINT=/usr/sbin/nginx"]`).
- **pause** (boolean) - Optional - Whether to pause the container during the commit process (defaults to `true`).

### Request Body
None

### Request Example
```console
$ docker run -d alpine touch /helloworld
0888269a9d584f0fa8fc96b3c0d8d57969ceea3a64acf47cd34eebb4744dbc52
$ curl --unix-socket /var/run/docker.sock\ 
  -X POST "http://localhost/v1.53/commit?container=0888269a9d&repo=helloworld"
```

### Success Response (200)
- **Id** (string) - The ID of the newly created image.

### Response Example
```json
{"Id":"sha256:6c86a5cd4b87f2771648ce619e319f3e508394b5bfc2cdbd2d60f59d52acda6c"}
```
```

--------------------------------

### Manage Docker Container Capabilities with ALL and DROP

Source: https://docs.docker.com/reference/run

Demonstrates how to grant all capabilities to a container while excluding specific ones, such as MKNOD. This is useful for fine-grained privilege management.

```bash
$ docker run --cap-add=ALL --cap-drop=MKNOD ...

```

--------------------------------

### Install GNOME Extensions for Docker Desktop (RHEL 9)

Source: https://docs.docker.com/desktop/setup/install/linux/rhel

Installs the AppIndicator GNOME extension and enables it for RHEL 9. This is required for Docker Desktop to function correctly with a GNOME desktop environment.

```bash
# enable EPEL as described above
sudo dnf install gnome-shell-extension-appindicator
sudo gnome-extensions enable appindicatorsupport@rgcjonas.gmail.com
```

--------------------------------

### Start Docker container with host directory obscuring container contents (-v)

Source: https://docs.docker.com/engine/storage/bind-mounts

Illustrates mounting a host directory ('/tmp') over a non-empty directory ('/usr') within a container using the '-v' flag. This scenario highlights how bind mounts can obscure existing container files, potentially causing issues with container startup.

```console
$ docker run -d \
  -it \
  --name broken-container \
  -v /tmp:/usr \
  nginx:latest
```

--------------------------------

### Verify WSL 2 installation and status

Source: https://docs.docker.com/desktop/troubleshoot-and-support/troubleshoot/topics

These PowerShell commands verify that WSL 2 is installed and functioning correctly. They list available WSL distributions and their states, and test communication with a specific distribution.

```powershell
PS C:\users\> wsl -l -v
  NAME              STATE           VERSION
* Ubuntu            Running         2
  docker-desktop    Stopped         2
PS C:\users\> wsl -d docker-desktop echo WSL 2 is working
WSL 2 is working
```

--------------------------------

### Build and Push Image with Kubernetes Builder

Source: https://docs.docker.com/build/builders/drivers/kubernetes

Builds a container image using the specified Docker Buildx builder ('kube') and pushes it to a registry. This command demonstrates the practical application of the configured Kubernetes builder for image creation.

```console
# Replace <registry> with your Docker username
# and <image> with the name of the image you want to build
docker buildx build \
  --builder=kube \
  -t <registry>/<image> \
  --push .
```

--------------------------------

### Install Docker Desktop RPM package on Fedora

Source: https://docs.docker.com/desktop/setup/install/linux/fedora

Installs the Docker Desktop RPM package using the dnf package manager. This command assumes the RPM file has been downloaded to the current directory.

```bash
$ sudo dnf install ./docker-desktop-x86_64.rpm
```

--------------------------------

### Example JSON Build Configuration Output

Source: https://docs.docker.com/guides/compose-bake

This JSON output represents a build configuration generated by Docker Buildx Bake. It details groups and targets, including context, Dockerfile path, and target stages for each service.

```json
{
  "group": {
    "default": {
      "targets": [
        "vote",
        "result",
        "worker",
        "seed"
      ]
    }
  },
  "target": {
    "result": {
      "context": "result",
      "dockerfile": "Dockerfile"
    },
    "seed": {
      "context": "seed-data",
      "dockerfile": "Dockerfile"
    },
    "vote": {
      "context": "vote",
      "dockerfile": "Dockerfile",
      "target": "dev"
    },
    "worker": {
      "context": "worker",
      "dockerfile": "Dockerfile"
    }
  }
}
```

--------------------------------

### Specify BuildKit daemon flags (--buildkitd-flags)

Source: https://docs.docker.com/reference/cli/docker/buildx/create

This example shows how to specify flags for the BuildKit daemon, overriding configuration file settings. It includes an example of setting the network mode for the BuildKit daemon.

```console
--buildkitd-flags '--debug --debugaddr 0.0.0.0:6666'
```

```console
--buildkitd-flags '--oci-worker-net bridge'
```

--------------------------------

### Create Dex Project Directory

Source: https://docs.docker.com/guides/dex

This command creates a new directory named 'dex-mock-server' and navigates into it, preparing the workspace for Dex configuration files.

```bash
mkdir dex-mock-server
cd dex-mock-server
```

--------------------------------

### Install Docker Extension API Client Types for TypeScript

Source: https://docs.docker.com/extensions/extensions-sdk/build/frontend-extension-tutorial

Installs type definitions for the Docker Extension APIs as a development dependency. This enhances the development experience in TypeScript by providing type checking and auto-completion.

```bash
npm install @docker/extension-api-client-types --save-dev
```

--------------------------------

### Console commands for Docker build and policy testing

Source: https://docs.docker.com/build/policies/intro

Command-line instructions to create a directory, navigate into it, and perform Docker builds to test policy evaluation. Includes commands for initial successful build and subsequent failed build due to policy violation.

```bash
$ mkdir policy-tutorial
$ cd policy-tutorial
$ docker build .
$ docker build .
```

--------------------------------

### Install Bash Completion Package

Source: https://docs.docker.com/engine/cli/completion

Installs the bash-completion package, which provides shell completion functions for Bash. This is a prerequisite for enabling Docker CLI completion in Bash. Installation methods vary by package manager.

```bash
sudo apt install bash-completion
```

```bash
brew install bash-completion@2
# Homebrew install for older versions of Bash:
brew install bash-completion
```

```bash
sudo pacman -S bash-completion
```

--------------------------------

### Configuring Dockerfile CMD/ENTRYPOINT for Signal Handling

Source: https://docs.docker.com/compose/faq

Demonstrates the correct way to define `CMD` and `ENTRYPOINT` in a Dockerfile using the exec form (JSON array) to ensure proper signal handling, which is crucial for graceful container shutdowns.

```dockerfile
# Correct exec form
CMD ["program", "arg1", "arg2"]
ENTRYPOINT ["/app/entrypoint.sh"]
```

--------------------------------

### Log Output Example with Template Markup (Text)

Source: https://docs.docker.com/engine/logging/log_tags

This example shows the expected format of log messages when using a custom tag that includes template markup such as {{.ImageName}}, {{.Name}}, and {{.ID}}. It illustrates how Docker substitutes these placeholders with container-specific information.

```text
Aug  7 18:33:19 HOSTNAME hello-world/foobar/5790672ab6a0[9103]: Hello from Docker.
```

--------------------------------

### Create Docker Service with Multiple Placement Constraints (CLI)

Source: https://docs.docker.com/engine/swarm/services

This command creates a global Docker service named 'my-nginx', constrained to run on nodes where the 'region' label is 'east' and the 'type' label is not 'devel'. It shows how to apply multiple constraints.

```console
docker service create \
  --name my-nginx \
  --mode global \
  --constraint node.labels.region==east \
  --constraint node.labels.type!=devel \
  nginx
```

--------------------------------

### Start Docker Daemon with Flags

Source: https://docs.docker.com/config/daemon

Manually start the Docker daemon with specific configurations using command-line flags. This is useful for troubleshooting and provides an alternative to JSON configuration. It requires specifying debug mode, TLS settings, and host options.

```bash
$ dockerd --debug \
  --tls=true \
  --tlscert=/var/docker/server.pem \
  --tlskey=/var/docker/serverkey.pem \
  --host tcp://192.168.59.3:2376

```

--------------------------------

### Start Docker Compose Application from OCI Artifact

Source: https://docs.docker.com/compose/how-tos/oci-artifact

Starts a Docker Compose application by pulling the Compose file from an OCI-compliant registry. The `oci://` prefix specifies that the Compose file should be retrieved from a registry instead of the local filesystem.

```console
$ docker compose -f oci://docker.io/username/my-compose-app:latest up
```

--------------------------------

### Run Docker Containers with Custom Networks

Source: https://docs.docker.com/engine/network/drivers/bridge

Launches Docker containers and assigns them to specific networks. This example shows how to connect containers to a user-defined bridge network ('alpine-net') and the default bridge network.

```console
docker run -dit --name alpine1 --network alpine-net alpine ash
docker run -dit --name alpine2 --network alpine-net alpine ash
docker run -dit --name alpine3 alpine ash
docker run -dit --name alpine4 --network alpine-net alpine ash
docker network connect bridge alpine4
```

--------------------------------

### Multiple Here-Documents in a Single RUN Instruction

Source: https://docs.docker.com/reference/dockerfile

An advanced example showing how to use multiple here-documents within a single RUN instruction to redirect content to different files or commands.

```dockerfile
# syntax=docker/dockerfile:1
FROM alpine
RUN <<FILE1 cat > file1 && <<FILE2 cat > file2
I am
first
FILE1
I am
second
FILE2
```

--------------------------------

### HTTP Methods - GET

Source: https://docs.docker.com/reference/api/extensions-sdk/BackendV0

Performs an HTTP GET request to a backend service.

```APIDOC
## GET /_docker/http/get

### Description
Performs an HTTP GET request to a backend service.

### Method
GET

### Endpoint
/_docker/http/get

### Parameters
#### Query Parameters
- **url** (string) - Required - The URL of the backend service.

### Request Example
```bash
GET /_docker/http/get?url=/some/service
```

### Response
#### Success Response (200)
- **data** (unknown) - The response data from the backend service.

#### Response Example
```json
{
  "data": "some response data"
}
```

**Note:** This method is deprecated and will be removed in a future version. Use `window.ddClient.backend.get` instead.
```

--------------------------------

### GET /info

Source: https://docs.docker.com/engine/release-notes/27

Retrieves system-wide information. Now includes a `Containerd` field with details about the containerd API socket and namespaces.

```APIDOC
## GET /info

### Description
Retrieves system-wide information. Now includes a `Containerd` field containing information about the location of the containerd API socket and containerd namespaces used by the daemon to run containers and plugins.

### Method
GET

### Endpoint
`/info`

### Response
#### Success Response (200)
- **ID** (string) - The daemon ID.
- **Containers** (integer) - The number of containers.
- **ContainersRunning** (integer) - The number of running containers.
- **ContainersPaused** (integer) - The number of paused containers.
- **ContainersStopped** (integer) - The number of stopped containers.
- **Images** (integer) - The number of images.
- **Driver** (string) - The storage driver name.
- **DriverStatus** (array) - An array of driver status information.
- **DockerRootDir** (string) - The Docker root directory path.
- **Plugins** (object) - Information about installed plugins.
- **MemoryLimit** (boolean) - Whether memory limit is enabled.
- **SwapLimit** (boolean) - Whether swap limit is enabled.
- **OOMKillDisable** (boolean) - Whether OOM killer is disabled.
- **Labels** (map) - Daemon labels.
- **Architecture** (string) - The system architecture.
- **IndexServerAddress** (string) - The index server address.
- **RegistryConfig** (object) - Registry configuration.
- **NCPU** (integer) - The number of CPUs.
- **MemTotal** (integer) - Total memory in bytes.
- **GenericResources** (array) - Generic resources.
- **Isolation** (string) - The container isolation technology.
- **InitBinary** (string) - The path to the init binary.
- **Containerd** (object) - Information about containerd.
  - **version** (string) - The version of containerd.
  - **root** (string) - The root directory of containerd.
  - **state** (string) - The state of containerd.
  - **snapshotter** (string) - The snapshotter used by containerd.
  - **plugins** (array) - List of containerd plugins.
  - **grpc_endpoint** (string) - The gRPC endpoint for containerd.
  - **debug_mode** (boolean) - Whether debug mode is enabled for containerd.

#### Response Example
```json
{
  "ID": "daemon_id",
  "Containers": 10,
  "ContainersRunning": 5,
  "ContainersPaused": 0,
  "ContainersStopped": 5,
  "Images": 50,
  "Driver": "overlay2",
  "DriverStatus": [
    ["Backing Filesystem", "extfs"]
  ],
  "DockerRootDir": "/var/lib/docker",
  "Plugins": {
    "Volume": ["local"],
    "Network": ["bridge", "host", "overlay"],
    "Authorization": []
  },
  "MemoryLimit": true,
  "SwapLimit": true,
  "OOMKillDisable": false,
  "Labels": {},
  "Architecture": "x86_64",
  "IndexServerAddress": "https://index.docker.io/v1/",
  "RegistryConfig": {
    "IndexConfigs": {
      "docker.io": {
        "Name": "Docker Hub",
        "Mirrors": [],
        "Secure": true,
        "OfficialImageNames": ["library/ubuntu"]
      }
    }
  },
  "NCPU": 4,
  "MemTotal": 8589934592,
  "GenericResources": [],
  "Isolation": "",
  "InitBinary": "/usr/libexec/docker/docker-init",
  "Containerd": {
    "version": "1.7.5",
    "root": "/var/lib/containerd",
    "state": "/run/containerd",
    "snapshotter": "overlayfs",
    "plugins": [
      "io.containerd.grpc.v1.cri",
      "io.containerd.grpc.v1.ttrpc"
    ],
    "grpc_endpoint": "/run/containerd/containerd.sock",
    "debug_mode": false
  }
}
```
```

--------------------------------

### Start Alpine Containers on Default Bridge Network

Source: https://docs.docker.com/engine/network/drivers/bridge

Starts two detached alpine containers, 'alpine1' and 'alpine2', using the default bridge network. The '-dit' flags ensure they run interactively in the background with a TTY. Containers not explicitly assigned to a network use the default bridge.

```console
$ docker run -dit --name alpine1 alpine ash
$ docker run -dit --name alpine2 alpine ash
```

--------------------------------

### Create Minimal Container with Scratch

Source: https://docs.docker.com/build/building/base-images

An example Dockerfile that uses the 'scratch' base image to create a minimal container. It adds an executable binary 'hello' and sets it as the command to run. Assumes 'hello' exists in the build context.

```dockerfile
# syntax=docker/dockerfile:1
FROM scratch
ADD hello /
CMD ["/hello"]
```

--------------------------------

### Install or Update WSL via Terminal

Source: https://docs.docker.com/desktop/setup/install/windows-install

Installs or updates the Windows Subsystem for Linux (WSL) using command-line commands. This method requires administrator privileges for PowerShell or Command Prompt. A system restart may be prompted.

```console
wsl --install

wsl --update
```

--------------------------------

### Build Docker Image using Dockerfile

Source: https://docs.docker.com/guides/golang/develop

This command builds a Docker image for the application. It tags the image as 'docker-gs-ping-roach' and uses the current directory as the build context. This process compiles the Go application and creates a lean, distroless final image.

```bash
docker build --tag docker-gs-ping-roach .

```

--------------------------------

### Docker Compose Configuration

Source: https://docs.docker.com/compose/gettingstarted

Defines and configures the services for a multi-container Docker application. This file specifies the web service built from the local Dockerfile and the Redis service using a public Redis image.

```yaml
services:
  web:
    build: .
    ports:
      - "8000:5000"
  redis:
    image: "redis:alpine"

```

--------------------------------

### Example Dockerfile-specific .dockerignore files

Source: https://docs.docker.com/build/building/context

Illustrates how to use Dockerfile-specific .dockerignore files. By prefixing the ignore file with the Dockerfile name (e.g., build.Dockerfile.dockerignore), you can associate specific ignore rules with individual Dockerfiles in the same directory.

```tree
. 
├── index.ts
├── src/
├── docker
│   ├── build.Dockerfile
│   ├── build.Dockerfile.dockerignore
│   ├── lint.Dockerfile
│   ├── lint.Dockerfile.dockerignore
│   ├── test.Dockerfile
│   └── test.Dockerfile.dockerignore
├── package.json
└── package-lock.json
```

--------------------------------

### Containerize PHP Application with Docker

Source: https://docs.docker.com/llms

Learn to containerize a PHP application using Docker. This guide focuses on creating efficient and production-ready Docker images for PHP projects.

```Dockerfile
# Example Dockerfile for a PHP application (using Apache)
FROM php:8.1-apache

COPY src/ /var/www/html/

RUN docker-php-ext-install mysqli pdo pdo_mysql

COPY apache/000-default.conf /etc/apache2/sites-available/000-default.conf

EXPOSE 80
```

--------------------------------

### Dockerfile Example: CUDA-Powered LLaMA Inference with --device

Source: https://docs.docker.com/reference/dockerfile

An example Dockerfile snippet demonstrating the use of the RUN --device flag to integrate a CUDA-enabled NVIDIA GPU for LLaMA inference via CDI. This showcases advanced hardware acceleration in Docker builds.

```dockerfile
# Example usage within a Dockerfile
# Assuming CDI is configured and devices are available
# RUN --device=vendor1.com/device=cuda_gpu
# RUN apt-get update && apt-get install -y git build-essential
# RUN git clone https://github.com/ggerganov/llama.cpp.git
# WORKDIR /llama.cpp
# RUN make
# RUN ./main -m <path_to_model> -p "Your prompt here"
```

--------------------------------

### Start Multi-Container Application with Docker Compose

Source: https://docs.docker.com/get-started/docker-concepts/the-basics/what-is-docker-compose

This command builds and starts all services defined in the `compose.yaml` file in detached mode. It downloads necessary images, creates networks and volumes, and runs the containers for the application.

```bash
docker compose up -d --build
```

--------------------------------

### Configure GitHub Actions CI/CD for React.js

Source: https://docs.docker.com/llms

Automate build and deployment for React.js applications using GitHub Actions. This guide focuses on setting up CI/CD pipelines for React projects.

```YAML
# Example GitHub Actions workflow for React.js
name: React.js CI/CD

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Use Node.js 18.x
      uses: actions/setup-node@v3
      with:
        node-version: '18.x'
        cache: 'npm'
    - run: npm ci
    - run: npm run build
    # Add deployment steps here (e.g., to Netlify, Vercel, S3, etc.)
```

--------------------------------

### Configure Environment Variables for Docker Application

Source: https://docs.docker.com/guides/nodejs/develop

Copies an example environment file to `.env` and provides an example `.env` file content. This file is used to configure application and database settings for the Dockerized environment.

```bash
$ cp .env.example .env
```

```env
# Application Configuration
NODE_ENV=development
APP_PORT=3000
VITE_PORT=5173
DEBUG_PORT=9230

# Database Configuration
POSTGRES_HOST=db
POSTGRES_PORT=5432
POSTGRES_DB=todoapp
POSTGRES_USER=todoapp
POSTGRES_PASSWORD=todoapp_password

# Security Configuration
ALLOWED_ORIGINS=http://localhost:3000,http://localhost:5173

```

--------------------------------

### Run Docker Application Stack

Source: https://docs.docker.com/get-started/workshop/08_using_compose

Commands to start, manage, and view logs for the Docker application stack defined in `compose.yaml`. Includes starting in detached mode and following logs.

```console
$ docker compose up -d
$ docker compose logs -f
$ docker compose logs -f app
```

--------------------------------

### Expose Multiple Specific GPUs

Source: https://docs.docker.com/config/containers/resource_constraints

Starts a Docker container and exposes a selection of NVIDIA GPUs based on their indices. The `--gpus '"device=0,2

--------------------------------

### Install Rosetta 2 on Mac

Source: https://docs.docker.com/desktop/setup/install/mac-install

Installs Rosetta 2 on macOS, which is recommended for a better experience with Docker Desktop, especially for certain command-line tools on Intel-based Macs. This command-line utility is part of the macOS software update system.

```bash
softwareupdate --install-rosetta
```

--------------------------------

### Dockerfile using additional build context

Source: https://docs.docker.com/reference/cli/docker/build

Example Dockerfile demonstrating how to use an additional build context named 'project' to copy a file. This assumes the --build-context flag was used to define 'project'.

```dockerfile
# syntax=docker/dockerfile:1
FROM alpine
COPY --from=project myfile /

```

--------------------------------

### Develop Rust Applications Locally

Source: https://docs.docker.com/llms

Learn how to develop your Rust application locally. This guide focuses on setting up a productive development environment for Rust projects.

```Dockerfile
# Example Dockerfile for Rust development
FROM rust:latest

WORKDIR /app

COPY . .

# You can add commands here to set up your development environment
# For example, installing linters or formatters
# RUN cargo install clippy

CMD ["cargo", "run"]
```

--------------------------------

### Create Symbolic Link for Docker Compose on Linux

Source: https://docs.docker.com/compose/install/standalone

Creates a symbolic link for the Docker Compose standalone binary, making it accessible from directories included in the system's PATH, such as /usr/bin. This is useful if the 'docker-compose' command fails after installation.

```console
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```

--------------------------------

### Build and Push Multi-platform Docker Images with GitHub Actions

Source: https://docs.docker.com/build/ci/github-actions/multi-platform

This workflow demonstrates how to build and push multi-platform Docker images (e.g., for amd64 and arm64 architectures) using GitHub Actions. It includes steps for logging into Docker Hub, setting up QEMU for cross-platform emulation, and configuring Docker Buildx for multi-platform builds. The `platforms` option specifies the target architectures, and `push: true` ensures the image is pushed to the registry.

```yaml
name: ci

on:
  push:

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ vars.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Set up QEMU
        uses: docker/setup-qemu-action@v3

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      - name: Build and push
        uses: docker/build-push-action@v6
        with:
          platforms: linux/amd64,linux/arm64
          push: true
          tags: user/app:latest
```

--------------------------------

### Dockerfile with Multiple ARG Declarations

Source: https://docs.docker.com/reference/dockerfile

An example of a Dockerfile that includes multiple ARG instructions to define several build-time variables.

```dockerfile
FROM busybox
ARG user1
ARG buildno
# ...
```

--------------------------------

### Set up Testcontainers Cloud Locally

Source: https://docs.docker.com/llms

Set up Testcontainers Cloud by Docker in a local development environment. This guide helps you configure Testcontainers Cloud for local testing workflows.

```Bash
# Example commands for setting up Testcontainers Cloud locally
# Ensure you have Docker running
# export TESTCONTAINERS_CLOUD_TOKEN="your-token-here"
# export TESTCONTAINERS_HOST_GO dibawah="docker"
# Your tests will now use Testcontainers Cloud
```

--------------------------------

### Docker Buildx Build Command with Multiple Registry Caches

Source: https://docs.docker.com/build/cache/backends

This example shows how to export cache to one registry location and import from multiple locations using Docker Buildx. It's useful for maintaining caches for different branches, such as the current branch and the main branch, to optimize build times.

```console
docker buildx build --push -t <registry>/<image> \
  --cache-to type=registry,ref=<registry>/<cache-image>:<branch> \
  --cache-from type=registry,ref=<registry>/<cache-image>:<branch> \
  --cache-from type=registry,ref=<registry>/<cache-image>:main .
```

--------------------------------

### Using Here-Documents with RUN (Default Shell)

Source: https://docs.docker.com/reference/dockerfile

Shows a Dockerfile example where a here-document is used with the RUN instruction without specifying a shell interpreter. The command's contents are evaluated by the default shell.

```dockerfile
# syntax=docker/dockerfile:1
FROM debian
RUN <<EOT
  mkdir -p foo/bar
EOT
```

--------------------------------

### Containerize Node.js Application with Docker

Source: https://docs.docker.com/llms

Learn to create an optimized, production-ready Docker image for a Node.js application. This guide covers best practices for performance, security, and scalability.

```Dockerfile
# Example Dockerfile for a Node.js application
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./ 
RUN npm install

COPY . .

EXPOSE 3000
CMD [ "node", "index.js" ]
```

--------------------------------

### Adding Labels to Docker Images

Source: https://docs.docker.com/build/building/best-practices

These Dockerfile examples show various ways to add labels to Docker images using the LABEL instruction. Labels can include version information, vendor details, and release dates. They help in organizing images and can be used for automation or querying.

```dockerfile
# Set one or more individual labels
LABEL com.example.version="0.0.1-beta"
LABEL vendor1="ACME Incorporated"
LABEL vendor2=ZENITH\ Incorporated
LABEL com.example.release-date="2015-02-12"
LABEL com.example.version.is-production=""
```

```dockerfile
# Set multiple labels on one line
LABEL com.example.version="0.0.1-beta" com.example.release-date="2015-02-12"
```

```dockerfile
# Set multiple labels at once, using line-continuation characters to break long lines
LABEL vendor=ACME\ Incorporated \
      com.example.is-beta= \
      com.example.is-production="" \
      com.example.version="0.0.1-beta" \
      com.example.release-date="2015-02-12"
```

--------------------------------

### GET /info - Deprecated Fields

Source: https://docs.docker.com/engine/release-notes/28

The GET /info endpoint previously returned `BridgeNfIptables` and `BridgeNfIp6tables` fields. These fields have been deprecated and are now omitted.

```APIDOC
## GET /info

### Description
This endpoint returns system-wide information about the Docker installation. Note that certain fields related to network bridge iptables have been deprecated and are no longer included.

### Method
GET

### Endpoint
/info

### Parameters
None

### Request Example
```bash
curl "http://localhost:2375/info"
```

### Response
#### Success Response (200)
- **ID** (string) - The unique ID of the Docker daemon.
- **Containers** (integer) - The total number of containers.
- **ContainersRunning** (integer) - The number of running containers.
- **ContainersPaused** (integer) - The number of paused containers.
- **ContainersStopped** (integer) - The number of stopped containers.
- **Images** (integer) - The total number of images.
- **Driver** (string) - The storage driver name.
- **DriverStatus** (array) - An array of key-value pairs representing the status of the storage driver.
- **DockerRootDir** (string) - The path to the Docker root directory.
- **EphemeralStorage** (object) - Information about ephemeral storage.
- **FileDescriptorLimit** (integer) - The file descriptor limit for the Docker daemon.
- **HttpProxy** (string) - The HTTP proxy configured for the Docker daemon.
- **HttpsProxy** (string) - The HTTPS proxy configured for the Docker daemon.
- **Name** (string) - The name of the Docker daemon.
- **NoProxy** (string) - The no-proxy list for the Docker daemon.
- **OSType** (string) - The operating system type.
- **Architecture** (string) - The system architecture.
- **IndexServerAddress** (string) - The address of the Docker registry index server.
- **RegistryConfig** (object) - Registry configuration details.
- **NCPU** (integer) - The number of CPUs available.
- **MemTotal** (integer) - The total amount of memory in bytes.
- **GenericResources** (array) - A list of generic resources.
- **Isolation** (string) - The isolation technology used by the Docker daemon.
- **KernelVersion** (string) - The kernel version of the host.
- **OperatingSystem** (string) - The operating system name.
- **ServerVersion** (string) - The version of the Docker server.
- **ClusterStore** (string) - The cluster store used by the Docker daemon.
- **ClusterAdvertise** (string) - The cluster advertise address.
- **CgroupDriver** (string) - The cgroup driver used by the Docker daemon.
- **NEventsListenerStartsBlockedTemporarily** (boolean) - Whether event listener starts are temporarily blocked.
- **LCOWCompatEnabled** (boolean) - Whether LCOW compatibility is enabled.
- **Warnings** (array) - A list of warnings.

#### Response Example
```json
{
  "ID": "abcdef1234567890abcdef1234567890abcdef1234567890",
  "Containers": 10,
  "ContainersRunning": 5,
  "ContainersPaused": 0,
  "ContainersStopped": 5,
  "Images": 50,
  "Driver": "overlay2",
  "DriverStatus": [
    ["Backing Filesystem", "extfs"],
    ["Supports d_type", "true"]
  ],
  "DockerRootDir": "/var/lib/docker",
  "EphemeralStorage": {
    "Enabled": true,
    "Total": 10000000000
  },
  "FileDescriptorLimit": 1024,
  "HttpProxy": "",
  "HttpsProxy": "",
  "Name": "my-docker-host",
  "NoProxy": "localhost,127.0.0.1",
  "OSType": "linux",
  "Architecture": "x86_64",
  "IndexServerAddress": "https://index.docker.io/v1/",
  "RegistryConfig": {
    "IndexConfigs": {
      "docker.io": {
        "Name": "Docker Hub",
        "Mirrors": []
      }
    }
  },
  "NCPU": 8,
  "MemTotal": 16777216000,
  "GenericResources": [],
  "Isolation": "",
  "KernelVersion": "5.15.0-88-generic",
  "OperatingSystem": "Ubuntu 22.04 LTS",
  "ServerVersion": "24.0.5",
  "ClusterStore": "",
  "ClusterAdvertise": "",
  "CgroupDriver": "systemd",
  "NEventsListenerStartsBlockedTemporarily": false,
  "LCOWCompatEnabled": false,
  "Warnings": []
}
```
```

--------------------------------

### Stop Docker Compose Services

Source: https://docs.docker.com/compose/gettingstarted

Stops and removes all containers, networks, and volumes defined in the `docker-compose.yaml` file. This command is used to gracefully shut down the application stack.

```console
$ docker compose down
```

--------------------------------

### Pull Docker Hardened Python Image

Source: https://docs.docker.com/dhi/get-started

Downloads the specified Python DHI from the dhi.io registry. This makes the image available locally for use.

```console
docker pull dhi.io/python:3.13
```

--------------------------------

### Specify Docker Service Image Version using Tag

Source: https://docs.docker.com/engine/swarm/services

This example shows how to create a Docker service using a specific version of an image identified by a tag, such as 'ubuntu:16.04'. Using specific tags helps ensure that all service replicas use a consistent and stable version of the image, preventing unexpected behavior due to frequent updates of 'latest' or 'nightly' tags.

```console
$ docker service create --name="myservice" ubuntu:16.04
```

--------------------------------

### Clone Python Docker Dev Example Repository

Source: https://docs.docker.com/guides/python/develop

Clones the sample Python application repository used for Docker development. This command fetches the necessary project files from GitHub.

```bash
$ git clone https://github.com/estebanx64/python-docker-dev-example
```

--------------------------------

### Dockerfile Best Practices and Build Checks

Source: https://docs.docker.com/llms

Documentation on various checks and best practices for writing Dockerfiles.

```APIDOC
## Dockerfile Best Practices and Build Checks

### Description
Guidelines and checks for writing efficient and maintainable Dockerfiles.

### Checks

- **ConsistentInstructionCasing**: [https://docs.docker.com/reference/build-checks/consistent-instruction-casing/](https://docs.docker.com/reference/build-checks/consistent-instruction-casing/)
- **CopyIgnoredFile**: [https://docs.docker.com/reference/build-checks/copy-ignored-file/](https://docs.docker.com/reference/build-checks/copy-ignored-file/)
- **DuplicateStageName**: [https://docs.docker.com/reference/build-checks/duplicate-stage-name/](https://docs.docker.com/reference/build-checks/duplicate-stage-name/)
- **ExposeInvalidFormat**: [https://docs.docker.com/reference/build-checks/expose-invalid-format/](https://docs.docker.com/reference/build-checks/expose-invalid-format/)
- **ExposeProtoCasing**: [https://docs.docker.com/reference/build-checks/expose-proto-casing/](https://docs.docker.com/reference/build-checks/expose-proto-casing/)
- **FromAsCasing**: [https://docs.docker.com/reference/build-checks/from-as-casing/](https://docs.docker.com/reference/build-checks/from-as-casing/)
- **FromPlatformFlagConstDisallowed**: [https://docs.docker.com/reference/build-checks/from-platform-flag-const-disallowed/](https://docs.docker.com/reference/build-checks/from-platform-flag-const-disallowed/)
- **InvalidDefaultArgInFrom**: [https://docs.docker.com/reference/build-checks/invalid-default-arg-in-from/](https://docs.docker.com/reference/build-checks/invalid-default-arg-in-from/)
- **InvalidDefinitionDescription**: [https://docs.docker.com/reference/build-checks/invalid-definition-description/](https://docs.docker.com/reference/build-checks/invalid-definition-description/)
- **JSONArgsRecommended**: [https://docs.docker.com/reference/build-checks/json-args-recommended/](https://docs.docker.com/reference/build-checks/json-args-recommended/)
- **LegacyKeyValueFormat**: [https://docs.docker.com/reference/build-checks/legacy-key-value-format/](https://docs.docker.com/reference/build-checks/legacy-key-value-format/)
- **MaintainerDeprecated**: [https://docs.docker.com/reference/build-checks/maintainer-deprecated/](https://docs.docker.com/reference/build-checks/maintainer-deprecated/)
- **MultipleInstructionsDisallowed**: [https://docs.docker.com/reference/build-checks/multiple-instructions-disallowed/](https://docs.docker.com/reference/build-checks/multiple-instructions-disallowed/)
- **NoEmptyContinuation**: [https://docs.docker.com/reference/build-checks/no-empty-continuation/](https://docs.docker.com/reference/build-checks/no-empty-continuation/)
- **RedundantTargetPlatform**: [https://docs.docker.com/reference/build-checks/redundant-target-platform/](https://docs.docker.com/reference/build-checks/redundant-target-platform/)
- **ReservedStageName**: [https://docs.docker.com/reference/build-checks/reserved-stage-name/](https://docs.docker.com/reference/build-checks/reserved-stage-name/)
- **SecretsUsedInArgOrEnv**: [https://docs.docker.com/reference/build-checks/secrets-used-in-arg-or-env/](https://docs.docker.com/reference/build-checks/secrets-used-in-arg-or-env/)
```

--------------------------------

### Enable Verbose Logging for MSI Installation Debugging (Command Prompt)

Source: https://docs.docker.com/enterprise/enterprise-deployment/faq

This command enables verbose logging during an MSI installation of Docker Desktop, which is crucial for debugging silent failures. The log file ('msi.log') will contain detailed information, and searching for 'value 3' can help identify the exit code and reason for failure.

```cmd
msiexec /i "DockerDesktop.msi" /L*V ".\msi.log"

```

--------------------------------

### Install PHP Extensions in Dockerfile

Source: https://docs.docker.com/guides/php/develop

This Dockerfile snippet installs the 'pdo' and 'pdo_mysql' PHP extensions, which are necessary for database connectivity. It builds upon a base PHP image and includes steps for installing composer dependencies and copying application code.

```dockerfile
# syntax=docker/dockerfile:1

FROM composer:lts as deps
WORKDIR /app
RUN --mount=type=bind,source=composer.json,target=composer.json \
    --mount=type=bind,source=composer.lock,target=composer.lock \
    --mount=type=cache,target=/tmp/cache \
    composer install --no-dev --no-interaction

FROM php:8.2-apache as final
RUN docker-php-ext-install pdo pdo_mysql
RUN mv "$PHP_INI_DIR/php.ini-production" "$PHP_INI_DIR/php.ini"
COPY --from=deps app/vendor/ /var/www/html/vendor
COPY ./src /var/www/html
USER www-data
```

--------------------------------

### Manually Set CPU Period and Quota for Containers

Source: https://docs.docker.com/engine/containers/resource_constraints

This example shows how to manually configure the CPU scheduler's period and quota for a Docker container. This method offers finer control over CPU resource allocation compared to the simpler `--cpus` flag. It's useful when specific timing or throttling is required.

```bash
docker run -it --cpu-period=100000 --cpu-quota=50000 ubuntu /bin/bash
```

--------------------------------

### Docker Exec Form ENTRYPOINT with CMD Argument

Source: https://docs.docker.com/engine/reference/builder

This example shows how to use the exec form of ENTRYPOINT to set a base command and CMD to provide default arguments. The container runs 'top -b' by default, and '-c' can be appended.

```dockerfile
FROM ubuntu
ENTRYPOINT ["top", "-b"]
CMD ["-c"]
```

--------------------------------

### Suppress Reboot After MSI Installation (Command Prompt)

Source: https://docs.docker.com/enterprise/enterprise-deployment/faq

This command installs Docker Desktop using MSI and suppresses the automatic reboot prompt at the end of the installation. This is useful for automated deployments or when a reboot is not immediately desired. Verbose logging is also enabled.

```cmd
msiexec /i "DockerDesktop.msi" /L*V ".\msi.log" /norestart

```

--------------------------------

### Publish TCP and UDP Ports on Overlay Network (Newer Syntax)

Source: https://docs.docker.com/engine/swarm/networking

This example publishes both TCP and UDP ports on an overlay network using the newer comma-separated value syntax. It maps TCP port 80 to TCP port 8080 and UDP port 80 to UDP port 8080 on the routing mesh. This explicit configuration improves clarity for dual-protocol port mapping.

```console
-p published=8080,target=80,protocol=tcp -p published=8080,target=80,protocol=udp
```

--------------------------------

### Configure AppArmor Profile for RootlessKit on Ubuntu

Source: https://docs.docker.com/engine/security/rootless/troubleshoot

This snippet demonstrates how to manually create and install an AppArmor profile for `rootlesskit` on Ubuntu when the rootless extras are installed via the installation script. It defines the profile to allow unprivileged user namespaces for the `rootlesskit` executable.

```shell
$ filename=$(echo $HOME/bin/rootlesskit | sed -e 's@^/@@' -e 's@/@.@g')
$ [ ! -z "${filename}" ] && sudo cat <<EOF > /etc/apparmor.d/${filename}
abi <abi/4.0>,
include <tunables/global>

"$HOME/bin/rootlesskit" flags=(unconfined) {
  userns,

  include if exists <local/${filename}>
}
EOF
```

--------------------------------

### Starting Specific Profiles with Docker Compose CLI

Source: https://docs.docker.com/compose/how-tos/profiles

This console command shows how to start Docker Compose services associated with a specific profile using the `--profile` flag. This ensures only the services within the specified profile, along with any unprofiled services, are activated.

```bash
$ docker compose --profile debug up
```

--------------------------------

### Example JSON Output for Image Configuration

Source: https://docs.docker.com/reference/cli/docker/buildx/imagetools/inspect

This is an example of the JSON output for an image's configuration when inspected using `docker buildx imagetools`. It includes details such as creation timestamp, architecture, operating system, environment variables, command history, and root filesystem layers.

```json
{
  "created": "2022-12-01T11:46:47.713777178Z",
  "architecture": "amd64",
  "os": "linux",
  "config": {
    "Env": [
      "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
    ],
    "Cmd": [
      "/bin/sh"
    ]
  },
  "rootfs": {
    "type": "layers",
    "diff_ids": [
      "sha256:ded7a220bb058e28ee3254fbba04ca90b679070424424761a53a043b93b612bf",
      "sha256:d85d09ab4b4e921666ccc2db8532e857bf3476b7588e52c9c17741d7af14204f"
    ]
  },
  "history": [
    {
      "created": "2022-11-22T22:19:28.870801855Z",
      "created_by": "/bin/sh -c #(nop) ADD file:587cae71969871d3c6456d844a8795df9b64b12c710c275295a1182b46f630e7 in / "
    },
    {
      "created": "2022-11-22T22:19:29.008562326Z",
      "created_by": "/bin/sh -c #(nop)  CMD [\"/bin/sh\"]",
      "empty_layer": true
    },
    {
      "created": "2022-12-01T11:46:47.713777178Z",
      "created_by": "RUN /bin/sh -c apk add curl # buildkit",
      "comment": "buildkit.dockerfile.v0"
    }
  ]
}
```

--------------------------------

### Install GNOME Extensions for Docker Desktop (RHEL 8)

Source: https://docs.docker.com/desktop/setup/install/linux/rhel

Installs necessary GNOME extensions, including AppIndicator and Desktop Icons, and enables the AppIndicator extension for RHEL 8. This is required for Docker Desktop to function correctly with a GNOME desktop environment.

```bash
# enable EPEL as described above
sudo dnf install gnome-shell-extension-appindicator
sudo dnf install gnome-shell-extension-desktop-icons
sudo gnome-shell-extension-tool -e appindicatorsupport@rgcjonas.gmail.com
```

--------------------------------

### Go: Initialize Docker Compose SDK Service

Source: https://docs.docker.com/compose/compose-sdk

Initializes a new Docker Compose service instance using the provided Docker CLI client. This service is the entry point for all Compose operations, handling interactions with the Docker daemon and Compose file management. It requires a compatible Docker CLI setup.

```go
package main

import (
    "context"
    "log"

	"github.com/docker/cli/cli/command"
	"github.com/docker/cli/cli/flags"
    "github.com/docker/compose/v5/pkg/api"
    "github.com/docker/compose/v5/pkg/compose"
)

func main() {
    ctx := context.Background()

	dockerCLI, err := command.NewDockerCli()
	if err != nil {
		log.Fatalf("Failed to create docker CLI: %v", err)
	}
	err = dockerCLI.Initialize(&flags.ClientOptions{})
	if err != nil {
		log.Fatalf("Failed to initialize docker CLI: %v", err)
	}
	
    // Create a new Compose service instance
    service, err := compose.NewComposeService(dockerCLI)
    if err != nil {
        log.Fatalf("Failed to create compose service: %v", err)
    }

    // Load the Compose project from a compose file
    project, err := service.LoadProject(ctx, api.ProjectLoadOptions{
        ConfigPaths: []string{"compose.yaml"},
        ProjectName: "my-app",
    })
    if err != nil {
        log.Fatalf("Failed to load project: %v", err)
    }

    // Start the services defined in the Compose file
    err = service.Up(ctx, project, api.UpOptions{
        Create: api.CreateOptions{},
        Start:  api.StartOptions{},
    })
    if err != nil {
        log.Fatalf("Failed to start services: %v", err)
    }

    log.Printf("Successfully started project: %s", project.Name)
}
```

--------------------------------

### GET /containers/json (ImageManifestDescriptor)

Source: https://docs.docker.com/engine/release-notes/28

Lists containers, now returning `ImageManifestDescriptor` field.

```APIDOC
## GET /containers/json

### Description
Lists containers, returning the `ImageManifestDescriptor` field.

### Method
GET

### Endpoint
/containers/json

### Response
#### Success Response (200)
- **ImageManifestDescriptor** (object) - OCI descriptor of the platform-specific image manifest.

#### Response Example
```json
[
  {
    "Id": "container_id",
    "ImageManifestDescriptor": {
      "mediaType": "application/vnd.oci.image.manifest.v1+json",
      "size": 702,
      "digest": "sha256:...
    }
  }
]
```
```

--------------------------------

### Use Local OCI Registry with GitHub Actions

Source: https://docs.docker.com/llms

This example demonstrates setting up and using a local OCI registry within a GitHub Actions workflow. This allows for testing image pushes and pulls without relying on external registries.

```yaml
name: Local Registry Example
on: [push]

jobs:
  local-registry-test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2
    - name: Start local registry
      run: docker run -d -p 5000:5000 --name registry registry:2
    - name: Build and push to local registry
      uses: docker/build-push-action@v4
      with:
        context: .
        file: ./Dockerfile
        push: true
        tags: localhost:5000/my-local-image:latest
    - name: Stop and remove local registry
      run: docker stop registry && docker rm registry
```

--------------------------------

### Initialize Node.js Project for E2B Sandbox Integration

Source: https://docs.docker.com/ai/mcp-catalog-and-toolkit/e2b-sandboxes

Sets up a new Node.js project directory, initializes npm, and configures it for ES modules. This is a prerequisite for running the E2B sandbox integration example.

```bash
mkdir mcp-e2b-quickstart
cd mcp-e2b-quickstart
npm init -y
```

--------------------------------

### Docker Port Mapping Examples

Source: https://docs.docker.com/engine/network/port-publishing

Demonstrates various ways to map container ports to host ports using the `docker run` command with the `-p` flag. This includes mapping to all host interfaces, specific host IPs, and specifying protocols like UDP or TCP.

```console
docker run -p 8080:80 [...]
```

```console
docker run -p 8080:80/udp [...]
```

```console
docker run -p 8080:80/tcp -p 8080:80/udp [...]
```

```console
docker run -p 192.168.1.100:8080:80 [...]
```

--------------------------------

### Docker Plugin Commands

Source: https://docs.docker.com/llms

Commands for creating, disabling, enabling, inspecting, installing, listing, pushing, removing, setting, and upgrading Docker plugins.

```APIDOC
## Docker Plugin Create

### Description
Create a Docker plugin.

### Method
`docker plugin create`

### Endpoint
`/plugin/create`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the plugin.
- **path** (string) - Required - The path to the plugin source code.

### Request Example
```json
{
  "example": "docker plugin create --name my-plugin ./my-plugin-source"
}
```

### Response
#### Success Response (200)
- **Plugin ID** (string) - The ID of the created plugin.

#### Response Example
```json
{
  "example": "plugin_id"
}
```

## Docker Plugin Disable

### Description
Disable a Docker plugin.

### Method
`docker plugin disable`

### Endpoint
`/plugin/disable`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name or ID of the plugin to disable.

### Request Example
```json
{
  "example": "docker plugin disable my-plugin"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Plugin my-plugin disabled."
}
```

## Docker Plugin Enable

### Description
Enable a Docker plugin.

### Method
`docker plugin enable`

### Endpoint
`/plugin/enable`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name or ID of the plugin to enable.

### Request Example
```json
{
  "example": "docker plugin enable my-plugin"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Plugin my-plugin enabled."
}
```

## Docker Plugin Inspect

### Description
Inspect a Docker plugin.

### Method
`docker plugin inspect`

### Endpoint
`/plugin/inspect`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name or ID of the plugin to inspect.

### Request Example
```json
{
  "example": "docker plugin inspect my-plugin"
}
```

### Response
#### Success Response (200)
- **Plugin Details** (object) - Detailed information about the plugin.

#### Response Example
```json
{
  "example": "{ \"ID\": \"plugin_id\", \"Name\": \"my-plugin\", ... }"
}
```

## Docker Plugin Install

### Description
Install a Docker plugin.

### Method
`docker plugin install`

### Endpoint
`/plugin/install`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the plugin to install.

#### Query Parameters
- **grant-permissions** (boolean) - Optional - Grant all necessary permissions.
- **disable** (boolean) - Optional - Do not enable the plugin on install.

### Request Example
```json
{
  "example": "docker plugin install my-plugin --grant-permissions"
}
```

### Response
#### Success Response (200)
- **Plugin ID** (string) - The ID of the installed plugin.

#### Response Example
```json
{
  "example": "plugin_id"
}
```

## Docker Plugin List

### Description
List installed Docker plugins.

### Method
`docker plugin ls`

### Endpoint
`/plugin/ls`

### Request Example
```json
{
  "example": "docker plugin ls"
}
```

### Response
#### Success Response (200)
- **Plugin List** (array) - A list of installed plugins.

#### Response Example
```json
{
  "example": "[ { \"ID\": \"plugin_id\", \"Name\": \"my-plugin\", \"Enabled\": true, ... } ]"
}
```

## Docker Plugin Push

### Description
Push a Docker plugin to a registry.

### Method
`docker plugin push`

### Endpoint
`/plugin/push`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name of the plugin to push.

### Request Example
```json
{
  "example": "docker plugin push my-plugin"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Plugin my-plugin pushed successfully."
}
```

## Docker Plugin Remove

### Description
Remove a Docker plugin.

### Method
`docker plugin rm`

### Endpoint
`/plugin/rm`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name or ID of the plugin to remove.

#### Query Parameters
- **force** (boolean) - Optional - Force removal of the plugin.

### Request Example
```json
{
  "example": "docker plugin rm -f my-plugin"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Plugin my-plugin removed."
}
```

## Docker Plugin Set

### Description
Set a configuration for a Docker plugin.

### Method
`docker plugin set`

### Endpoint
`/plugin/set`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name or ID of the plugin.

#### Request Body
- **key** (string) - Required - The configuration key to set.
- **value** (string) - Required - The value for the configuration key.

### Request Example
```json
{
  "example": "docker plugin set my-plugin <key> <value>"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Plugin my-plugin configuration updated."
}
```

## Docker Plugin Upgrade

### Description
Upgrade a Docker plugin.

### Method
`docker plugin upgrade`

### Endpoint
`/plugin/upgrade`

### Parameters
#### Path Parameters
- **name** (string) - Required - The name or ID of the plugin to upgrade.

#### Query Parameters
- **grant-permissions** (boolean) - Optional - Grant all necessary permissions.

### Request Example
```json
{
  "example": "docker plugin upgrade my-plugin --grant-permissions"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Plugin my-plugin upgraded successfully."
}
```
```

--------------------------------

### Docker Sandbox Commands

Source: https://docs.docker.com/llms

Commands for creating, executing, inspecting, listing, managing networks, resetting, removing, running, saving, and getting the version of Docker sandboxes.

```APIDOC
## Docker Sandbox Create

### Description
Create a Docker sandbox with a specified agent.

### Method
`docker sandbox create`

### Endpoint
`/sandbox/create`

### Parameters
#### Path Parameters
- **agent** (string) - Required - The type of agent for the sandbox (e.g., cagent, codex, copilot, gemini, kiro, opencode, shell).

### Request Example
```json
{
  "example": "docker sandbox create shell"
}
```

### Response
#### Success Response (200)
- **Sandbox ID** (string) - The ID of the created sandbox.

#### Response Example
```json
{
  "example": "sandbox_id"
}
```

## Docker Sandbox Exec

### Description
Execute a command within a Docker sandbox.

### Method
`docker sandbox exec`

### Endpoint
`/sandbox/exec`

### Parameters
#### Path Parameters
- **sandbox_id** (string) - Required - The ID of the sandbox.
- **command** (string) - Required - The command to execute.

### Request Example
```json
{
  "example": "docker sandbox exec <sandbox_id> ls -l"
}
```

### Response
#### Success Response (200)
- **Output** (string) - The output of the executed command.

#### Response Example
```json
{
  "example": "file1 file2"
}
```

## Docker Sandbox Inspect

### Description
Inspect a Docker sandbox.

### Method
`docker sandbox inspect`

### Endpoint
`/sandbox/inspect`

### Parameters
#### Path Parameters
- **sandbox_id** (string) - Required - The ID of the sandbox to inspect.

### Request Example
```json
{
  "example": "docker sandbox inspect <sandbox_id>"
}
```

### Response
#### Success Response (200)
- **Sandbox Details** (object) - Detailed information about the sandbox.

#### Response Example
```json
{
  "example": "{ \"ID\": \"sandbox_id\", \"Status\": \"running\", ... }"
}
```

## Docker Sandbox List

### Description
List all Docker sandboxes.

### Method
`docker sandbox ls`

### Endpoint
`/sandbox/ls`

### Request Example
```json
{
  "example": "docker sandbox ls"
}
```

### Response
#### Success Response (200)
- **Sandbox List** (array) - A list of sandboxes.

#### Response Example
```json
{
  "example": "[ { \"ID\": \"sandbox_id\", \"Status\": \"running\", ... } ]"
}
```

## Docker Sandbox Network Log

### Description
Get network logs for a Docker sandbox.

### Method
`docker sandbox network log`

### Endpoint
`/sandbox/network/log`

### Parameters
#### Path Parameters
- **sandbox_id** (string) - Required - The ID of the sandbox.

### Request Example
```json
{
  "example": "docker sandbox network log <sandbox_id>"
}
```

### Response
#### Success Response (200)
- **Network Logs** (string) - The network logs for the sandbox.

#### Response Example
```json
{
  "example": "Log entry 1\nLog entry 2"
}
```

## Docker Sandbox Network Proxy

### Description
Configure network proxy for a Docker sandbox.

### Method
`docker sandbox network proxy`

### Endpoint
`/sandbox/network/proxy`

### Parameters
#### Path Parameters
- **sandbox_id** (string) - Required - The ID of the sandbox.

#### Request Body
- **http_proxy** (string) - Optional - The HTTP proxy URL.
- **https_proxy** (string) - Optional - The HTTPS proxy URL.
- **no_proxy** (string) - Optional - Comma-separated list of hosts to bypass proxy.

### Request Example
```json
{
  "example": "docker sandbox network proxy <sandbox_id> --http-proxy http://proxy.example.com:8080"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Proxy settings updated for sandbox <sandbox_id>."
}
```

## Docker Sandbox Reset

### Description
Reset a Docker sandbox.

### Method
`docker sandbox reset`

### Endpoint
`/sandbox/reset`

### Parameters
#### Path Parameters
- **sandbox_id** (string) - Required - The ID of the sandbox to reset.

### Request Example
```json
{
  "example": "docker sandbox reset <sandbox_id>"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Sandbox <sandbox_id> reset."
}
```

## Docker Sandbox Remove

### Description
Remove a Docker sandbox.

### Method
`docker sandbox rm`

### Endpoint
`/sandbox/rm`

### Parameters
#### Path Parameters
- **sandbox_id** (string) - Required - The ID of the sandbox to remove.

#### Query Parameters
- **force** (boolean) - Optional - Force removal of the sandbox.

### Request Example
```json
{
  "example": "docker sandbox rm -f <sandbox_id>"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Sandbox <sandbox_id> removed."
}
```

## Docker Sandbox Run

### Description
Run a command in a new Docker sandbox.

### Method
`docker sandbox run`

### Endpoint
`/sandbox/run`

### Parameters
#### Path Parameters
- **agent** (string) - Required - The type of agent for the sandbox.
- **command** (string) - Required - The command to run.

### Request Example
```json
{
  "example": "docker sandbox run shell echo 'Hello World'"
}
```

### Response
#### Success Response (200)
- **Output** (string) - The output of the command.

#### Response Example
```json
{
  "example": "Hello World"
}
```

## Docker Sandbox Save

### Description
Save the state of a Docker sandbox.

### Method
`docker sandbox save`

### Endpoint
`/sandbox/save`

### Parameters
#### Path Parameters
- **sandbox_id** (string) - Required - The ID of the sandbox to save.

### Request Example
```json
{
  "example": "docker sandbox save <sandbox_id>"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Sandbox <sandbox_id> state saved."
}
```

## Docker Sandbox Stop

### Description
Stop a Docker sandbox.

### Method
`docker sandbox stop`

### Endpoint
`/sandbox/stop`

### Parameters
#### Path Parameters
- **sandbox_id** (string) - Required - The ID of the sandbox to stop.

### Request Example
```json
{
  "example": "docker sandbox stop <sandbox_id>"
}
```

### Response
#### Success Response (200)
- **Message** (string) - Confirmation message.

#### Response Example
```json
{
  "example": "Sandbox <sandbox_id> stopped."
}
```

## Docker Sandbox Version

### Description
Get the version of the Docker sandbox environment.

### Method
`docker sandbox version`

### Endpoint
`/sandbox/version`

### Request Example
```json
{
  "example": "docker sandbox version"
}
```

### Response
#### Success Response (200)
- **Version** (string) - The version of the Docker sandbox environment.

#### Response Example
```json
{
  "example": "1.0.0"
}
```
```

--------------------------------

### Running a Container with a Specific Image Tag

Source: https://docs.docker.com/engine/reference/run

This example demonstrates how to run a container using a specific version (tag) of an image. Here, it runs version `24.04` of the `ubuntu` image.

```bash
docker run ubuntu:24.04
```

--------------------------------

### Mount Docker Volume Subdirectory (--mount with volume-subpath)

Source: https://docs.docker.com/engine/storage/volumes

This example illustrates mounting a specific subdirectory of a Docker volume into a container using the 'volume-subpath' parameter with the --mount flag. This allows for granular control over which part of a volume is accessible to a container, useful for isolating data like logs.

```console
docker volume create logs
docker run --rm \
  --mount src=logs,dst=/logs \
  alpine mkdir -p /logs/app1 /logs/app2
docker run -d \
  --name=app1 \
  --mount src=logs,dst=/var/log/app1,volume-subpath=app1 \
  app1:latest
docker run -d \
  --name=app2 \
  --mount src=logs,dst=/var/log/app2,volume-subpath=app2 \
  app2:latest
```

--------------------------------

### Run Ubuntu Container with Bind Mount (PowerShell)

Source: https://docs.docker.com/get-started/workshop/06_bind_mounts

Launches an interactive bash session in an Ubuntu container, establishing a bind mount from the current host directory to `/src` within the container. This ensures that modifications to files are reflected instantly across both the host and the container.

```console
docker run -it --mount "type=bind,src=.,target=/src" ubuntu bash
```

--------------------------------

### Publish UDP Ports on Overlay Network (Legacy Syntax)

Source: https://docs.docker.com/engine/swarm/networking

This example demonstrates publishing a UDP port on an overlay network using the legacy colon-separated syntax. It maps UDP port 80 on the service to port 8080 on the routing mesh. This is useful for services that rely on UDP communication.

```console
-p 8080:80/udp
```

--------------------------------

### Example Webhook Payload

Source: https://docs.docker.com/docker-hub/repos/manage/webhooks

This section provides an example of the JSON payload structure that is sent to the webhook destination URL during a push event.

```APIDOC
## Webhook Payload Example

### Description
This is an example of the JSON payload structure sent to your webhook URL when a push event occurs in the repository.

### Request Body Example
```json
{
  "push_data": {
    "pushed_at": 1417566161,
    "pusher": "trustedbuilder",
    "tag": "latest"
  },
  "repository": {
    "comment_count": 0,
    "date_created": 1417494799,
    "description": "",
    "dockerfile": "#\n# BUILD\t\tdocker build -t svendowideit/apt-cacher .\n# RUN\t\tdocker run -d -p 3142:3142 -name apt-cacher-run apt-cacher\n#\n# and then you can run containers with:\n# \t\tdocker run -t -i -rm -e http_proxy http://192.168.1.2:3142/ debian bash\n#\nFROM\t\tubuntu\n\n\nVOLUME\t[/var/cache/apt-cacher-ng]\nRUN\t\tapt-get update ; apt-get install -yq apt-cacher-ng\n\nEXPOSE \t3142\nCMD\t\tchmod 777 /var/cache/apt-cacher-ng ; /etc/init.d/apt-cacher-ng start ; tail -f /var/log/apt-cacher-ng/*\n",
    "full_description": "Docker Hub based automated build from a GitHub repo",
    "is_official": false,
    "is_private": true,
    "is_trusted": true,
    "name": "testhook",
    "namespace": "svendowideit",
    "owner": "svendowideit",
    "repo_name": "svendowideit/testhook",
    "repo_url": "https://registry.hub.docker.com/u/svendowideit/testhook/",
    "star_count": 0,
    "status": "Active"
  }
}
```

> [!NOTE]
> The `callback_url` field is a legacy field and is no longer supported.
```

--------------------------------

### Set Specific Device Blkio Weight in Docker

Source: https://docs.docker.com/engine/containers/run

This example shows how to set a specific block IO weight for a device within a Docker container using the --blkio-weight-device flag. The format is 'DEVICE_NAME:WEIGHT'. This allows for fine-grained control over IO for particular storage devices.

```console
docker run -it \
    --blkio-weight-device "/dev/sda:200" \
    ubuntu
```

--------------------------------

### Clone Sample Application Repository

Source: https://docs.docker.com/guides/rust/develop

Clones the sample Rust and PostgreSQL application repository from GitHub using Git. This is the first step to obtain the application code and Docker-related files.

```bash
$ git clone https://github.com/docker/docker-rust-postgres
```

--------------------------------

### Dockerfile Exec Form Instruction Example

Source: https://docs.docker.com/engine/reference/builder

Illustrates the exec form of a Dockerfile instruction, specifically ENTRYPOINT. This form uses a JSON array syntax and is suitable for invoking commands directly without a shell.

```dockerfile
ENTRYPOINT ["/bin/bash", "-c", "echo hello"]
```

--------------------------------

### Run Container with SFTP Volume

Source: https://docs.docker.com/engine/storage/volumes

Starts an Nginx container named 'rclone-container' that uses a pre-created SFTP volume. The volume is mounted to '/app' inside the container, and SFTP connection details are provided as volume options.

```bash
docker run -d \
  --name rclone-container \
  --mount type=volume,volume-driver=rclone,src=rclonevolume,target=/app,volume-opt=type=sftp,volume-opt=path=remote, volume-opt=sftp-host=1.2.3.4,volume-opt=sftp-user=user,volume-opt=-o "sftp-password=$(cat file_containing_password_for_remote_host)" \
  nginx:latest
```

--------------------------------

### Docker ENTRYPOINT for Running Apache in Foreground

Source: https://docs.docker.com/engine/reference/builder

This Dockerfile snippet configures the ENTRYPOINT to execute Apache in the foreground, ensuring it runs as PID 1. It includes necessary setup for Apache.

```dockerfile
FROM debian:stable
RUN apt-get update && apt-get install -y --force-yes apache2
EXPOSE 80 443
VOLUME ["/var/www", "/var/log/apache2", "/etc/apache2"]
ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```

--------------------------------

### View Docker Image History

Source: https://docs.docker.com/get-started/docker-concepts/building-images/understanding-image-layers

This command displays the layers that make up a Docker image (`sample-app`), including creation details, commands used, and size. It's useful for understanding how an image was built and troubleshooting.

```console
$ docker image history sample-app
```

--------------------------------

### Load Docker Container Labels from File

Source: https://docs.docker.com/reference/cli/docker/container/run

Illustrates how to load multiple labels for a Docker container from a file using the --label-file flag. Each label in the file should be on a new line, and comments starting with '#' are ignored. Labels without explicit values are treated as empty strings. This is useful for managing a large number of labels.

```console
$ docker run --label-file ./labels ubuntu bash
```

```text
com.example.label1="a label"

# this is a comment
com.example.label2=another\ label
com.example.label3
```

--------------------------------

### Restart a Docker Container

Source: https://docs.docker.com/guides/golang/run-containers

Restarts a stopped Docker container. The container will be started with the same flags and commands it was originally started with. Replace 'inspiring_ishizaka' with the actual container name.

```console
$ docker restart inspiring_ishizaka
```

--------------------------------

### Create a Docker Volume with Local Driver Options (NFS)

Source: https://docs.docker.com/reference/cli/docker/volume/create

This example shows how to create a Docker volume using the 'local' driver for an NFS mount. It specifies the NFS server address, mount options (read-write), and the device path on the NFS server.

```console
docker volume create --driver local \
    --opt type=nfs \
    --opt o=addr=192.168.1.1,rw \
    --opt device=:/path/to/dir \
    foo
```

--------------------------------

### Install Packages in JupyterLab (Console)

Source: https://docs.docker.com/guides/jupyter

This command is executed within a JupyterLab notebook to install necessary Python packages like matplotlib and scikit-learn. It uses pip, the standard package installer for Python. This is typically done when setting up an environment for data analysis or visualization within the notebook.

```console
!pip install --no-cache-dir matplotlib scikit-learn
```

--------------------------------

### Configure Memory Toolset (YAML)

Source: https://docs.docker.com/ai/cagent/reference/toolsets

Illustrates the configuration of the 'memory' toolset using YAML. It includes the basic setup and an option to define a specific path for the memory database file.

```yaml
toolsets:
  - type: memory

  # Optional: specify database location
  - type: memory
    path: ./agent-memories.db
```

--------------------------------

### Make Docker Compose Plugin Executable

Source: https://docs.docker.com/compose/install/linux

Applies executable permissions to the Docker Compose CLI plugin binary after manual installation. This command is necessary for the system to run the plugin. The command varies slightly depending on whether the plugin was installed for the current user or for all users.

```bash
$ chmod +x $DOCKER_CONFIG/cli-plugins/docker-compose
```

```bash
$ sudo chmod +x /usr/local/lib/docker/cli-plugins/docker-compose
```

--------------------------------

### Test Docker Image Before Pushing with GitHub Actions

Source: https://docs.docker.com/llms

This example demonstrates how to validate a Docker image before pushing it to a registry using GitHub Actions. It allows for running tests or checks on the built image to ensure its quality and integrity.

```yaml
name: Test Before Push

on: [push]

jobs:
  test-and-push:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2
    - name: Build image
      id: build
      uses: docker/build-push-action@v4
      with:
        context: .
        file: ./Dockerfile
        outputs: type=inline
        tags: your-dockerhub-username/test-image:latest
    - name: Run tests on image
      run: docker run --rm your-dockerhub-username/test-image:latest echo "Tests passed!"
    - name: Push image if tests pass
      if: success()
      uses: docker/build-push-action@v4
      with:
        context: .
        file: ./Dockerfile
        push: true
        tags: your-dockerhub-username/test-image:latest
```

--------------------------------

### Create Docker Buildx Kubernetes Builder

Source: https://docs.docker.com/build/builders/drivers/kubernetes

Initializes a new Docker Buildx builder using the Kubernetes driver. It specifies the builder name, driver type, and the Kubernetes namespace for Buildx resources. The `--bootstrap` flag ensures the builder is ready for use immediately.

```console
docker buildx create \
  --bootstrap \
  --name=kube \
  --driver=kubernetes \
  --driver-opt=namespace=buildkit
```

--------------------------------

### POST /plugins/pull

Source: https://docs.docker.com/reference/api/engine/latest

Pulls and installs a plugin. After the plugin is installed, it can be enabled using the `POST /plugins/{name}/enable` endpoint.

```APIDOC
## POST /plugins/pull

### Description
Pulls and installs a plugin. After the plugin is installed, it can be enabled using the `POST /plugins/{name}/enable` endpoint.

### Method
POST

### Endpoint
/v1.53/plugins/pull

### Parameters
#### Query Parameters
- **remote** (string) - Required - Remote reference for plugin to install. The `:latest` tag is optional, and is used as the default if omitted.
- **name** (string) - Required - Local name for the pulled plugin. The `:latest` tag is optional, and is used as the default if omitted.

#### Header Parameters
- **X-Registry-Auth** (string) - Required - A base64url-encoded auth configuration to use when pulling a plugin from a registry. Refer to the authentication section for details.

#### Request Body
- **Name** (string) - Required - Name of the plugin component.
- **Description** (string) - Optional - Description of the plugin component.
- **Value** (Array of strings) - Required - Value associated with the plugin component.

### Request Example
```json
[
  {
    "Name": "network",
    "Description": "",
    "Value": [
      "host"
    ]
  },
  {
    "Name": "mount",
    "Description": "",
    "Value": [
      "/data"
    ]
  },
  {
    "Name": "device",
    "Description": "",
    "Value": [
      "/dev/cpu_dma_latency"
    ]
  }
]
```

### Response
#### Success Response (204)
- no error

#### Error Response (500)
- **message** (string) - Description of the error.

#### Response Example (500)
```json
{
  "message": "Something went wrong."
}
```
```

--------------------------------

### Configure GitHub Actions CI/CD for R

Source: https://docs.docker.com/llms

Automate build and deployment for R applications using GitHub Actions. This guide focuses on setting up CI/CD pipelines for R projects.

```YAML
# Example GitHub Actions workflow for R
name: R CI/CD

on:
  push:
    branches: [ main ]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Set up R
      uses: r-lib/actions/setup-r@v2
      with:
        r-version: '4.2.0'
    - name: Install packages
      run: Rscript -e "install.packages(c('shiny', 'testthat'))"
    - name: Run tests
      run: Rscript -e "library(testthat); test_dir('tests')
```

--------------------------------

### Set Up Docker's APT Repository on Debian

Source: https://docs.docker.com/engine/install/debian

This snippet configures the Docker apt repository on Debian-based systems. It adds the Docker GPG key and the repository source list, ensuring that Docker packages can be retrieved and installed via apt.

```bash
# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/debian
Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
Components: stable
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update
```

--------------------------------

### Deploy Node.js Application to Kubernetes

Source: https://docs.docker.com/llms

Learn to deploy a containerized Node.js application to Kubernetes with production-ready configurations. This guide covers deployment strategies and best practices.

```YAML
# Example Kubernetes deployment for Node.js
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nodejs-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nodejs-app
  template:
    metadata:
      labels:
        app: nodejs-app
    spec:
      containers:
      - name: nodejs-app
        image: your-dockerhub-username/nodejs-app:latest
        ports:
        - containerPort: 3000
```

--------------------------------

### Starting Specific Profiles with COMPOSE_PROFILES Environment Variable

Source: https://docs.docker.com/compose/how-tos/profiles

This console command illustrates starting Docker Compose services for a specific profile by setting the `COMPOSE_PROFILES` environment variable. This method achieves the same result as using the `--profile` command-line option.

```bash
$ COMPOSE_PROFILES=debug docker compose up
```

--------------------------------

### Start Container on IPvlan Network

Source: https://docs.docker.com/engine/network/drivers/ipvlan

Starts a container with an explicit name in daemon mode, attached to a specified IPvlan network.

```bash
$ docker run --net=db_net_ipv --name=ipv1 -itd alpine /bin/sh
```

--------------------------------

### Run Nginx with Read-Only Volume (--mount)

Source: https://docs.docker.com/storage/volumes

Starts an Nginx container with a named volume mounted as read-only. This prevents the container from writing to the volume. The `readonly` option is added to the `--mount` flag.

```bash
$ docker run -d \
  --name=nginxtest \
  --mount source=nginx-vol,destination=/usr/share/nginx/html,readonly \
  nginx:latest

```

--------------------------------

### List Allowed Extensions in Text File

Source: https://docs.docker.com/extensions/private-marketplace

Example format for the `extensions.txt` file, specifying which Docker extensions are permitted in the private marketplace. Each line represents an extension in the `org/repo:tag` format. Comments can be added using '#'.

```text
# This is a comment
docker/disk-usage-extension:0.2.8
other-org/custom-extension:latest
```

--------------------------------

### Build Multi-Platform Image with QEMU Emulation

Source: https://docs.docker.com/build/building/multi-platform

Demonstrates building a multi-platform Docker image for `linux/amd64` and `linux/arm64` using QEMU emulation. This is suitable for simple images where build speed is not critical. It requires Docker Desktop or Docker Engine with QEMU installed.

```dockerfile
# syntax=docker/dockerfile:1
FROM alpine
RUN uname -m > /arch
```

```bash
docker build --platform linux/amd64,linux/arm64 -t multi-platform .
docker run --rm multi-platform cat /arch
```

--------------------------------

### Build Docker Extension Image

Source: https://docs.docker.com/extensions/extensions-sdk/build/minimal-frontend-extension

Command to build the Docker extension image. This command tags the resulting image with a specified name and version, preparing it for installation.

```bash
$ docker build --tag=awesome-inc/my-extension:latest .
```

--------------------------------

### Run Docker Image with Custom Arguments

Source: https://docs.docker.com/develop/security-best-practices

Illustrates how to run a Docker container and pass specific arguments to the command defined by ENTRYPOINT. This overrides the default CMD arguments.

```shell
$ docker run s3cmd ls s3://mybucket
```

--------------------------------

### Using Bind Mount for Temporary Build Context Files

Source: https://docs.docker.com/build/building/best-practices

Shows how to use a bind mount with a RUN instruction to temporarily include a file from the build context into the container. This is an efficient alternative to COPY for executing commands that require specific files.

```dockerfile
RUN --mount=type=bind,source=requirements.txt,target=/tmp/requirements.txt \
    pip install --requirement /tmp/requirements.txt
```

--------------------------------

### Find Docker Desktop Product Code (PowerShell)

Source: https://docs.docker.com/enterprise/enterprise-deployment/msi-install-and-configure

Retrieves the product code for Docker Desktop using WMI. This command queries installed products and filters for 'Docker Desktop' to identify its unique identifier, necessary for uninstallation if the original MSI is unavailable.

```powershell
Get-WmiObject Win32_Product | Select-Object IdentifyingNumber, Name | Where-Object {$_.Name -eq "Docker Desktop"}
```

--------------------------------

### Dockerfile Environment Variable Substitution Examples

Source: https://docs.docker.com/engine/reference/builder

Demonstrates various ways to use environment variables in Dockerfile instructions, including basic substitution, literal escapes, and the use of bash-like modifiers for string manipulation. It also shows how variable values are interpreted throughout the Dockerfile.

```dockerfile
FROM busybox
ENV FOO=/bar
WORKDIR ${FOO}   # WORKDIR /bar
ADD . $FOO       # ADD . /bar
COPY $FOO /quux # COPY $FOO /quux
```

```shell
str=foobarbaz echo ${str#f*b}     # arbaz
```

```shell
str=foobarbaz echo ${str##f*b}    # az
```

```shell
string=foobarbaz echo ${string%b*}    # foobar
```

```shell
string=foobarbaz echo ${string%%b*}   # foo
```

```shell
string=foobarbaz echo ${string/ba/fo}  # fooforbaz
```

```shell
string=foobarbaz echo ${string//ba/fo}  # fooforfoz
```

```dockerfile
ENV abc=hello
ENV abc=bye def=$abc
ENV ghi=$abc
```

--------------------------------

### Configure Docker Service Runtime Environment

Source: https://docs.docker.com/engine/swarm/services

This snippet demonstrates how to create a Docker service with specific runtime configurations. It sets environment variables, defines the working directory, and specifies the user to run the service as. This is useful for isolating service environments and ensuring consistent execution.

```console
$ docker service create --name helloworld \
  --env MYVAR=myvalue \
  --workdir /tmp \
  --user my_user \
  alpine ping docker.com
```

--------------------------------

### Remove Docker Compose for All Users

Source: https://docs.docker.com/compose/install/uninstall

Removes the Docker Compose CLI plugin installed for all users from the system directory. This command targets installations in the /usr/local/lib/docker/cli-plugins/ path.

```bash
rm /usr/local/lib/docker/cli-plugins/docker-compose
```

--------------------------------

### Install fuse-overlayfs on RHEL 8

Source: https://docs.docker.com/engine/security/rootless/troubleshoot

This command installs the `fuse-overlayfs` package, which is recommended for RHEL 8 and similar distributions when using Docker's rootless mode. `fuse-overlayfs` provides an overlay filesystem implementation that works in user space.

```shell
sudo dnf install -y fuse-overlayfs
```

--------------------------------

### GET /containers/json (GwPriority)

Source: https://docs.docker.com/engine/release-notes/28

Lists containers, now returning `GwPriority` in `NetworkSettings` for each network endpoint.

```APIDOC
## GET /containers/json

### Description
Lists containers, returning `GwPriority` in `NetworkSettings`.

### Method
GET

### Endpoint
/containers/json

### Response
#### Success Response (200)
- **NetworkSettings.Networks.GwPriority** (integer) - The gateway priority.

#### Response Example
```json
[
  {
    "Id": "container_id",
    "NetworkSettings": {
      "Networks": {
        "mynetwork": {
          "GwPriority": 10
        }
      }
    }
  }
]
```
```

--------------------------------

### Clone Sample Node.js Application using Git

Source: https://docs.docker.com/guides/nodejs/containerize

This command clones a sample Node.js application from a GitHub repository. It requires a git client to be installed on your system. The output is the cloned repository in your current directory.

```bash
git clone https://github.com/kristiyan-velkov/docker-nodejs-sample
```

--------------------------------

### Create and Manage Multiple Sandboxes

Source: https://docs.docker.com/ai/sandboxes/workflows

Demonstrates how to create separate sandboxes for different projects and how to remove unused sandboxes to free up disk space. Each sandbox provides a completely isolated environment.

```console
$ docker sandbox create claude ~/project-a
$ docker sandbox create codex ~/project-b
$ docker sandbox create copilot ~/work/client-project
$ docker sandbox rm <sandbox-name>
```

--------------------------------

### Console: Build and run Docker image with heredoc script

Source: https://docs.docker.com/reference/dockerfile

These console commands show how to build a Docker image from a Dockerfile and then run it. The output demonstrates the effect of build-time variable expansion from the first Dockerfile example.

```console
$ docker build -t heredoc .
$ docker run heredoc
```

--------------------------------

### Configure metadata.json for VM Image

Source: https://docs.docker.com/extensions/extensions-sdk/build/backend-extension-tutorial

This JSON snippet shows how to configure the 'vm' section in the metadata.json file to specify the Docker image for the extension's backend service. It uses a placeholder that is automatically replaced during installation.

```json
{
  "vm": {
    "image": "${DESKTOP_PLUGIN_IMAGE}"
  },
  "icon": "docker.svg",
  "ui": {
    ...
  }
}
```

--------------------------------

### Start Docker Compose Services

Source: https://docs.docker.com/engine/cli/otel

Command to start the Docker Compose services defined in the `compose.yaml` file. This command brings up the OpenTelemetry collector and Prometheus instances.

```console
docker compose up
```

--------------------------------

### Dockerfile: Multi-stage Build for Certificate Installation

Source: https://docs.docker.com/guides/zscaler

This Dockerfile demonstrates a multi-stage build process. The first stage compiles an application, and the second stage installs the Zscaler root CA certificate and the compiled application into a slim runtime image. This ensures the certificate is present for runtime operations.

```dockerfile
FROM debian:bookworm AS build
WORKDIR /build
RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    curl \
    git
RUN --mount=target=. cmake -B output/

FROM debian:bookworm-slim AS final
ADD --checksum=sha256:24454f830cdb571e2c4ad15481119c43b3cafd48dd869a9b2945d1036d1dc68d \
    https://artifacts.example/certs/zscaler-root-ca.crt /usr/local/share/ca-certificates/zscaler-root-ca.crt
RUN apt-get update && \
    apt-get install -y ca-certificates && \
    update-ca-certificates
WORKDIR /app
COPY --from=build /build/output/bin .
ENTRYPOINT ["/app/bin"]
```

--------------------------------

### Format Docker System Info Output as JSON

Source: https://docs.docker.com/reference/cli/docker/system/info

This example demonstrates how to format the output of the 'docker system info' command into JSON format using the --format option with the 'json .' template. This is useful for programmatic parsing of Docker system information.

```console
docker info --format '{{json .}}'
```

--------------------------------

### Dockerfile RUN Instruction Forms and Heredocs

Source: https://docs.docker.com/reference/dockerfile

Illustrates the two forms of the RUN instruction (shell and exec) and how to use heredocs for multi-line commands. This allows for more readable and manageable build steps.

```dockerfile
# Shell form:
RUN [OPTIONS] <command> ...
# Exec form:
RUN [OPTIONS] [ "<command>", ... ]
```

```dockerfile
RUN <<EOF
apt-get update
apt-get install -y curl
EOF
```

--------------------------------

### Verify Customized Target Stage (JSON)

Source: https://docs.docker.com/guides/compose-bake

Inspect the build configuration for a specific target using `docker buildx bake --print <target>` to verify changes. This example shows the updated 'vote' target configuration with the 'final' stage.

```console
$ docker buildx bake --print vote
```

```json
{
  "group": {
    "default": {
      "targets": ["vote"]
    }
  },
  "target": {
    "vote": {
      "context": "vote",
      "dockerfile": "Dockerfile",
      "tags": ["username/vote"],
      "target": "final"
    }
  }
}
```

--------------------------------

### Listen for Docker Events

Source: https://docs.docker.com/reference/cli/docker/system/events

This command streams events from the Docker daemon in real-time. It requires no arguments to start listening. To exit, press CTRL+C.

```console
$ docker events
```

--------------------------------

### Build and Run Minimal Container

Source: https://docs.docker.com/build/building/base-images

Commands to build a Docker image from the minimal Dockerfile and then run it. This is used after creating a Dockerfile like the 'Create Minimal Container with Scratch' example.

```bash
$ docker build --tag hello .
$ docker run --rm hello
```

--------------------------------

### GET /distribution/{name}/json

Source: https://docs.docker.com/reference/api/engine/latest

Get image information from the registry. This endpoint contacts the registry to return image digest and platform information.

```APIDOC
## GET /distribution/{name}/json

### Description
Get image information from the registry. Return image digest and platform information by contacting the registry.

### Method
GET

### Endpoint
/v1.53/distribution/{name}/json

### Parameters
#### Path Parameters
- **name** (string) - Required - Image name or id.

### Responses
#### Success Response (200)
- **Descriptor** (object) - The image descriptor.
- **Platform** (object) - The platform information for the image.

#### Error Response (401)
Failed authentication or no image found

#### Error Response (500)
Server error

### Request Example
```
GET /v1.53/distribution/alpine:latest/json
```

### Response Example (200)
```json
{
  "Descriptor": {
    "mediaType": "application/vnd.docker.distribution.manifest.v2+json",
    "size": 1234,
    "digest": "sha256:abcdef123456...",
    "url": "http://example.com/registry/image"
  },
  "Platform": {
    "architecture": "amd64",
    "os": "linux"
  }
}
```
```

--------------------------------

### Create Service with Multiple Placement Preferences

Source: https://docs.docker.com/engine/swarm/services

Creates a Docker service named 'redis_2' with 9 replicas, applying two placement preferences sequentially. Tasks are first spread across nodes by 'datacenter' label, and then by 'rack' label. This ensures a more robust distribution.

```console
docker service create \
  --replicas 9 \
  --name redis_2 \
  --placement-pref 'spread=node.labels.datacenter' \
  --placement-pref 'spread=node.labels.rack' \
  redis:7.4.0
```

--------------------------------

### GET /images/json

Source: https://docs.docker.com/engine/release-notes/27

Lists images. When the `manifests` option is enabled, the original order of manifests in the manifest-index is now preserved.

```APIDOC
## GET /images/json

### Description
Lists images. When the `manifests` option is enabled, the original order of manifests in the manifest-index is now preserved.

### Method
GET

### Endpoint
/images/json

### Parameters
#### Query Parameters
- **all** (boolean) - Optional - Show all images.
- **dangling** (boolean) - Optional - Show only dangling images.
- **filters** (string) - Optional - Filters to process on the image list.
- **manifests** (boolean) - Optional - Include manifest list information. Preserves original order.

#### Request Body
None

### Request Example
```bash
curl "http://localhost:2375/images/json?manifests=true"
```

### Response
#### Success Response (200)
- **[]** (array) - A list of image objects.
  - **Id** (string) - The image ID.
  - **RepoTags** (array) - List of repository tags for the image.
  - **Created** (integer) - Timestamp of when the image was created.
  - **Size** (integer) - Size of the image in bytes.
  - **SharedSize** (integer) - Size of the image when shared between layers.
  - **VirtualSize** (integer) - Total size of image layers.
  - **Labels** (object) - User-defined metadata for the image.
  - **Manifests** (array) - (When `manifests=true`) List of manifest objects, preserving original order.

#### Response Example
```json
[
  {
    "Id": "sha25e5117135f...",
    "RepoTags": [
      "ubuntu:latest"
    ],
    "Created": 1678886400,
    "Size": 77827000,
    "SharedSize": 0,
    "VirtualSize": 77827000,
    "Labels": {},
    "Manifests": [
      {
        "Digest": "sha25e5117135f...",
        "Platform": {
          "Architecture": "amd64",
          "Os": "linux"
        }
      },
      {
        "Digest": "sha1234567890...",
        "Platform": {
          "Architecture": "arm64",
          "Os": "linux"
        }
      }
    ]
  }
]
```
```

--------------------------------

### Uninstall conflicting Docker packages on RHEL

Source: https://docs.docker.com/engine/install/rhel

This command removes existing Docker-related packages and potentially conflicting container runtimes like Podman and runc from your RHEL system. It ensures a clean slate before installing the official Docker Engine. The `dnf` command might indicate that none of these packages are installed, which is also a valid outcome.

```bash
sudo dnf remove \
                  docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine \
                  podman \
                  runc
```

--------------------------------

### Configure SELinux Label with -v Flag

Source: https://docs.docker.com/engine/storage/bind-mounts

This example demonstrates how to configure SELinux labels for bind mounts using the `-v` flag with the 'z' option. The 'z' option indicates that the bind mount content is shared among multiple containers. Note that SELinux labels are ignored when using bind mounts with services.

```bash
docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app:z \
  nginx:latest
```

--------------------------------

### Use Docker Build Cloud in CI

Source: https://docs.docker.com/llms

Learn how to integrate Docker Build Cloud into your Continuous Integration (CI) process to accelerate your application builds. This guide focuses on optimizing build times in CI environments.

```YAML
# Example GitHub Actions workflow using Docker Build Cloud
name: Docker Build Cloud CI

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Build and push Docker image with Build Cloud
      uses: docker/build-push-action@v4
      with:
        context: .
        push: true
        tags: your-dockerhub-username/your-app:latest
        builder: docker://buildx-cloud
```