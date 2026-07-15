### Example Output: Helm Releases List

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

This example shows the typical output from the helm list -A command after a successful installation of the Actions Runner Controller. It displays the arc controller and arc-runner-set with a 'deployed' status, along with their respective namespaces, revisions, and chart versions. This output confirms that the Helm charts have been correctly installed.

```text
NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                                       APP VERSION
arc             arc-systems     1               2023-04-12 11:45:59.152090536 +0000 UTC deployed        gha-runner-scale-set-controller-0.4.0       0.4.0
arc-runner-set  arc-runners     1               2023-04-12 11:46:13.451041354 +0000 UTC deployed        gha-runner-scale-set-0.4.0                  0.4.0
```

--------------------------------

### Setup Node.js Action with Version Configuration

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

GitHub Actions step that uses the 'actions/setup-node@v4' action to install Node.js version 20 on the runner. This action configures both the 'node' and 'npm' commands in the PATH environment variable, making them available for subsequent workflow steps.

```yaml
- uses: actions/setup-node@v4
  with:
    node-version: '20'
```

--------------------------------

### Example Output: Kubernetes Pod Status

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

This example illustrates the expected output from the kubectl get pods -n arc-systems command, showing the healthy status of the Actions Runner Controller and listener pods. It provides details such as pod names, readiness, current status ('Running'), restart count, and age. This output confirms the operational state of the controller components.

```text
NAME                                                   READY   STATUS    RESTARTS   AGE
arc-gha-runner-scale-set-controller-594cdc976f-m7cjs   1/1     Running   0          64s
arc-runner-set-754b578d-listener                       1/1     Running   0          12s
```

--------------------------------

### Install Go dependencies in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

This GitHub Actions workflow sequence demonstrates how to install Go project dependencies using `go get`. It first checks out the repository and sets up a specific Go version (`1.21.x`) using `actions/setup-go`. Subsequently, it executes `go get` commands to fetch modules, including the current module, specific external modules, and modules at a particular version.

```yaml
    steps:
      - uses: actions/checkout@v5
      - name: Setup Go
        uses: actions/setup-go@v5
        with:
          go-version: '1.21.x'
      - name: Install dependencies
        run: |
          go get .
          go get example.com/octo-examplemodule
          go get example.com/octo-examplemodule@v1.3.4
```

--------------------------------

### Setup Swift Environment in GitHub Actions Workflow

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/swift

This GitHub Actions workflow snippet demonstrates how to initialize a Swift development environment. It utilizes the `swift-actions/setup-swift` action to install a specific Swift version (5.3.3) and includes a step to verify the installation by checking the Swift compiler version.

```yaml
# separate terms of service, privacy policy, and support
# documentation.
steps:
  - uses: swift-actions/setup-swift@65540b95f51493d65f5e59e97dcef9629ddf11bf
    with:
      swift-version: "5.3.3"
  - name: Get swift version
    run: swift --version # Swift 5.3.3
```

--------------------------------

### Install GitHub Actions Runner Scale Set with Helm

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

This command installs the GitHub Actions Runner Scale Set using Helm, configuring it with a specified name, Kubernetes namespace, GitHub configuration URL, and a Personal Access Token. It creates the namespace if it doesn't exist and pulls the chart from the GitHub Container Registry. Users must update placeholder values for INSTALLATION_NAME, NAMESPACE, GITHUB_CONFIG_URL, and GITHUB_PAT.

```bash
INSTALLATION_NAME="arc-runner-set"
NAMESPACE="arc-runners"
GITHUB_CONFIG_URL="https://github.com/<your_enterprise/org/repo>"
GITHUB_PAT="<PAT>"
helm install "${INSTALLATION_NAME}" \
    --namespace "${NAMESPACE}" \
    --create-namespace \
    --set githubConfigUrl="${GITHUB_CONFIG_URL}" \
    --set githubConfigSecret.github_token="${GITHUB_PAT}" \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set
```

--------------------------------

### Build and test Go code with GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

Complete workflow that checks out code, sets up Go 1.21.x, installs dependencies with go get, builds the project with go build, and runs tests with go test. This workflow runs on push events and uses ubuntu-latest runner.

```yaml
name: Go
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5
      - name: Setup Go
        uses: actions/setup-go@v5
        with:
          go-version: '1.21.x'
      - name: Install dependencies
        run: go get .
      - name: Build
        run: go build -v ./...
      - name: Test with the Go CLI
        run: go test
```

--------------------------------

### Install NuGet dependencies in GitHub Actions workflow

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/net

Demonstrates how to install NuGet package dependencies using the dotnet CLI in a GitHub Actions workflow. This example installs the Newtonsoft.Json package version 12.0.1 after setting up .NET 6.0.x.

```yaml
steps:
- uses: actions/checkout@v5
- name: Setup dotnet
  uses: actions/setup-dotnet@v4
  with:
    dotnet-version: '6.0.x'
- name: Install dependencies
  run: dotnet add package Newtonsoft.Json --version 12.0.1
```

--------------------------------

### Create GitHub Actions Workflow with Runner Scale Set

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

A basic GitHub Actions workflow that uses runner scale set runners via Actions Runner Controller. The workflow is triggered manually and runs a simple echo command on the arc-runner-set. The 'runs-on' value must match the Helm installation name used during ARC setup.

```yaml
name: Actions Runner Controller Demo
on:
  workflow_dispatch:

jobs:
  Explore-GitHub-Actions:
    # You need to use the INSTALLATION_NAME from the previous step
    runs-on: arc-runner-set
    steps:
    - run: echo "🎉 This job uses runner scale set runners!"
```

--------------------------------

### Install Dependencies with npm install in GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Uses npm install to install dependencies defined in package.json file. This method allows for dependency updates within specified version ranges. Requires Node.js setup action and checkout action.

```yaml
steps:
- uses: actions/checkout@v5
- name: Use Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20.x'
- name: Install dependencies
  run: npm install
```

--------------------------------

### Install Python Dependencies from requirements.txt

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

Sets up Python environment and installs project dependencies from requirements.txt file. Uses actions/checkout to clone the repository and actions/setup-python to configure the Python version. Upgrades pip before installing dependencies to ensure compatibility.

```yaml
steps:
- uses: actions/checkout@v5
- name: Set up Python
  uses: actions/setup-python@v5
  with:
    python-version: '3.x'
- name: Install dependencies
  run: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt
```

--------------------------------

### GitHub Actions Workflow: Trigger on Push, Install Bats, and Check Version (YAML)

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

This YAML configuration defines a GitHub Actions workflow that automatically runs when code is pushed to the repository. The workflow, named 'learn-github-actions', executes on an `ubuntu-latest` virtual machine. It performs several steps: checking out the repository's code, setting up Node.js version 20, globally installing the `bats` testing framework, and finally running `bats -v` to verify its installation and version.

```yaml
name: learn-github-actions
run-name: ${{ github.actor }} is learning GitHub Actions
on: [push]
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm install -g bats
      - run: bats -v
```

--------------------------------

### Configuring Primary and Service Containers for Databases in CI/CD

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-circleci

This example illustrates how to configure primary and service containers, such as a PostgreSQL database, for CI/CD environments in both CircleCI and GitHub Actions. It shows how to define container images, set environment variables, and include steps for database setup and testing, highlighting the syntactic differences between the two platforms.

```yaml
---
version: 2.1

jobs:

  ruby-26:
    docker:
      - image: circleci/ruby:2.6.3-node-browsers-legacy
        environment:
          PGHOST: localhost
          PGUSER: administrate
          RAILS_ENV: test
      - image: postgres:10.1-alpine
        environment:
          POSTGRES_USER: administrate
          POSTGRES_DB: ruby26
          POSTGRES_PASSWORD: ""

    working_directory: ~/administrate

    steps:
      - checkout

      # Bundle install dependencies
      - run: bundle install --path vendor/bundle

      # Wait for DB
      - run: dockerize -wait tcp://localhost:5432 -timeout 1m

      # Setup the environment
      - run: cp .sample.env .env

      # Setup the database
      - run: bundle exec rake db:setup

      # Run the tests
      - run: bundle exec rake

workflows:
  version: 2
  build:
    jobs:
      - ruby-26
...

- attach_workspace:
    at: /tmp/workspace
```

```yaml
name: Containers

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    container: circleci/ruby:2.6.3-node-browsers-legacy

    env:
      PGHOST: postgres
      PGUSER: administrate
      RAILS_ENV: test

    services:
      postgres:
        image: postgres:10.1-alpine
        env:
          POSTGRES_USER: administrate
          POSTGRES_DB: ruby25
          POSTGRES_PASSWORD: ""
        ports:
          - 5432:5432
        # Add a health check
        options: --health-cmd pg_isready --health-interval 10s --health-timeout 5s --health-retries 5

    steps:
      # This Docker file changes sets USER to circleci instead of using the default user, so we need to update file permissions for this image to work on GH Actions.
      # See https://docs.github.com/actions/using-github-hosted-runners/about-github-hosted-runners#docker-container-filesystem

      - name: Setup file system permissions
        run: sudo chmod -R 777 $GITHUB_WORKSPACE /github /__w/_temp
      - uses: actions/checkout@v5
      - name: Install dependencies
        run: bundle install --path vendor/bundle
      - name: Setup environment configuration
        run: cp .sample.env .env
      - name: Setup database
        run: bundle exec rake db:setup
      - name: Run tests
        run: bundle exec rake
```

--------------------------------

### List Helm Releases Across All Namespaces

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

This command is used to verify the successful deployment of Helm releases across all namespaces in a Kubernetes cluster. It lists all installed charts, including the GitHub Actions Runner Controller and Runner Scale Set, showing their status, version, and other details. The expected output should indicate that both arc and arc-runner-set are deployed.

```bash
helm list -A
```

--------------------------------

### GitHub Actions Importer Configure Command Example

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/circleci-migration

Example output of the configure command showing the interactive prompts and responses for setting up CircleCI and GitHub credentials, including personal access tokens and organization name.

```bash
$ gh actions-importer configure
✔ Which CI providers are you configuring?: CircleCI
Enter the following values (leave empty to omit):
✔ Personal access token for GitHub: ***************
✔ Base url of the GitHub instance: https://github.com
✔ Personal access token for CircleCI: ********************
✔ Base url of the CircleCI instance: https://circleci.com
✔ CircleCI organization name: mycircleciorganization
Environment variables successfully updated.
```

--------------------------------

### ARC Installation Error Messages

Source: https://docs.github.com/en/actions/tutorials/use-actions-runner-controller/troubleshoot

Example error outputs from ARC installation failures indicating resource name character limits. Installation names are limited to 45 characters and namespaces to 63 characters due to ARC's use of generated resource names as labels for other resources.

```text
Error: INSTALLATION FAILED: execution error at (gha-runner-scale-set/templates/autoscalingrunnerset.yaml:5:5): Name must have up to 45 characters

Error: INSTALLATION FAILED: execution error at (gha-runner-scale-set/templates/autoscalingrunnerset.yaml:8:5): Namespace must have up to 63 characters
```

--------------------------------

### Migrate Bamboo build plan with example output

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/bamboo-migration

Example execution of the migrate command for a Bamboo build plan showing the command with actual values and the resulting output including logs path and pull request URL.

```bash
$ gh actions-importer migrate bamboo build --plan-slug :PROJECTKEY-PLANKEY --target-url https://github.com/octo-org/octo-repo --output-dir tmp/migrate
[2022-08-20 22:08:20] Logs: 'tmp/migrate/log/actions-importer-20220916-014033.log'
[2022-08-20 22:08:20] Pull request: 'https://github.com/octo-org/octo-repo/pull/1'
```

--------------------------------

### Install Global npm Package - bats Testing Framework

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

GitHub Actions run step that executes an npm command to install the bats software testing package globally on the runner. This makes the bats command available for use in subsequent workflow steps.

```yaml
- run: npm install -g bats
```

--------------------------------

### Example: Adding New Matrix Configurations

Source: https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

Use the include directive to add entirely new matrix combinations beyond the base matrix. This example adds a Windows with Node.js 17 combination to a 3×3 matrix, resulting in 10 total jobs.

```APIDOC
## Adding New Matrix Configurations

### Description
Add new matrix combinations that don't exist in the base matrix using the include directive.

### Configuration Structure
```yaml
jobs:
  example_matrix:
    strategy:
      matrix:
        os: [macos-latest, windows-latest, ubuntu-latest]
        version: [12, 14, 16]
        include:
          - os: windows-latest
            version: 17
```

### Result
Produces 10 jobs:
- 9 jobs from base matrix (3 os × 3 versions)
- 1 additional job from include (windows-latest with version 17)

### Parameters
- **matrix** (object) - Base matrix variables
- **include** (array) - Additional configurations to add
```

--------------------------------

### Example Dockerfile for a GitHub Action with custom entrypoint

Source: https://docs.github.com/en/actions/reference/dockerfile-support-for-github-actions

This `Dockerfile` provides a complete example for a GitHub Action, using a `debian:9.5-slim` base image. It copies a custom `entrypoint.sh` script into the container and sets it as the `ENTRYPOINT`, allowing the action to execute custom logic and receive arguments from the action's metadata.

```Dockerfile
# Container image that runs your code
FROM debian:9.5-slim

# Copies your code file from your action repository to the filesystem path `/` of the container
COPY entrypoint.sh /entrypoint.sh

# Executes `entrypoint.sh` when the Docker container starts up
ENTRYPOINT ["/entrypoint.sh"]

```

--------------------------------

### Install self-hosted runner service on Windows

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/configure-the-application_platform=linux

Installs the self-hosted runner as a Windows service. Must be executed from the runner installation directory. Service configuration is part of the application setup process.

```powershell
.\svc.sh install
```

--------------------------------

### Verify Installed Package Version

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

GitHub Actions run step that executes the bats command with the '-v' flag to display the installed version of the bats testing framework. This verifies that the package was successfully installed in the previous step.

```yaml
- run: bats -v
```

--------------------------------

### Full GitHub Actions CI Workflow for Ruby with Matrix Testing

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/ruby

This comprehensive GitHub Actions workflow provides a continuous integration setup for Ruby projects. It triggers on push and pull requests to the `main` branch, uses a matrix strategy to test against Ruby versions 3.1, 3.0, and 2.7, and includes steps for checking out code, setting up Ruby, installing dependencies, and running tests.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# GitHub recommends pinning actions to a commit SHA.
# To get a newer version, you will need to update the SHA.
# You can also reference a tag or branch, but the action may change without warning.

name: Ruby CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:

    runs-on: ubuntu-latest

    strategy:
      matrix:
        ruby-version: ['3.1', '3.0', '2.7']

    steps:
      - uses: actions/checkout@v5
      - name: Set up Ruby ${{ matrix.ruby-version }}
        uses: ruby/setup-ruby@ec02537da5712d66d4d50a0f33b7eb52773b5ed1
        with:
          ruby-version: ${{ matrix.ruby-version }}
      - name: Install dependencies
        run: bundle install
      - name: Run tests
        run: bundle exec rake
```

--------------------------------

### Setup specific .NET version in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/net

Configures a GitHub Actions job to use a specific .NET version (6.x) with semantic version syntax to automatically get the latest minor release. Uses the setup-dotnet action to ensure consistent behavior across different runners.

```yaml
    - name: Setup .NET 6.x
      uses: actions/setup-dotnet@v4
      with:
        dotnet-version: '6.x'
```

--------------------------------

### Install Dependencies with npm ci in GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Uses npm ci to install exact dependency versions from package-lock.json or npm-shrinkwrap.json, preventing lock file updates. This approach is faster and more reliable than npm install. Requires Node.js setup action and checkout action.

```yaml
steps:
- uses: actions/checkout@v5
- name: Use Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20.x'
- name: Install dependencies
  run: npm ci
```

--------------------------------

### Example Output of GitHub Actions Importer Configuration

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/gitlab-migration

This example demonstrates the interactive session and expected output when running the `gh actions-importer configure` command. It shows how to select CI providers and input personal access tokens and base URLs for GitHub and GitLab.

```bash
$ gh actions-importer configure
✔ Which CI providers are you configuring?: GitLab
Enter the following values (leave empty to omit):
✔ Personal access token for GitHub: ***************
✔ Base url of the GitHub instance: https://github.com
✔ Private token for GitLab: ***************
✔ Base url of the GitLab instance: http://localhost
Environment variables successfully updated.
```

--------------------------------

### Build and Test Swift Projects with GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/swift

This GitHub Actions workflow example illustrates the process of building and testing Swift code. It first checks out the repository, then sets up Swift version 5.3.3 using `swift-actions/setup-swift`, and finally executes `swift build` and `swift test` commands to compile and run tests for the project.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
steps:
  - uses: actions/checkout@v5
  - uses: swift-actions/setup-swift@65540b95f51493d65f5e59e97dcef9629ddf11bf
    with:
      swift-version: "5.3.3"
  - name: Build
    run: swift build
  - name: Run tests
    run: swift test
```

--------------------------------

### Create a README.md for a GitHub Action

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

This Markdown example demonstrates how to structure a `README.md` file for a GitHub Action. It includes sections for a detailed description, required and optional input/output arguments, secrets, environment variables, and a practical example of how to use the action within a workflow. This README helps users understand and utilize the action effectively.

```Markdown
# Hello world JavaScript action

This action prints "Hello World" or "Hello" + the name of a person to greet to the log.

## Inputs

### `who-to-greet`

**Required** The name of the person to greet. Default `"World"`.

## Outputs

### `time`

The time we greeted you.

## Example usage

```yaml
uses: actions/hello-world-javascript-action@e76147da8e5c81eaf017dede5645551d4b94427b
with:
  who-to-greet: Mona the Octocat
```
```

--------------------------------

### Configure databases and service containers

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-gitlab-cicd-to-github-actions

Set up additional containers for databases, caching services, or other dependencies alongside the main job container. GitLab uses image and services keys with environment variables for configuration, while GitHub Actions uses container and services keys. This example demonstrates PostgreSQL service setup with connection parameters.

```GitLab CI/CD
container-job:
  variables:
    POSTGRES_PASSWORD: postgres
    # The hostname used to communicate with the
    # PostgreSQL service container
    POSTGRES_HOST: postgres
    # The default PostgreSQL port
    POSTGRES_PORT: 5432
  image: node:20-bookworm-slim
  services:
    - postgres
  script:
    # Performs a clean installation of all dependencies
    # in the `package.json` file
    - npm ci
    # Runs a script that creates a PostgreSQL client,
    # populates the client with data, and retrieves data
    - node client.js
  tags:
    - docker
```

--------------------------------

### Install Dependencies with Yarn in GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Uses yarn to install dependencies defined in package.json file. This method allows for dependency updates within specified version ranges. Requires Node.js setup action and checkout action.

```yaml
steps:
- uses: actions/checkout@v5
- name: Use Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20.x'
- name: Install dependencies
  run: yarn
```

--------------------------------

### Execute Single-Line Command in GitHub Actions `run` Step

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example illustrates how to execute a single command-line program within a GitHub Actions workflow step using the `run` keyword. The command `npm install` is run directly by the operating system's shell. If no `name` is provided, the step name defaults to the `run` command itself.

```yaml
- name: Install Dependencies
  run: npm install
```

--------------------------------

### Install self-hosted runner service on Windows

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/configure-the-application

Installs the self-hosted runner as a Windows service during the application configuration process. Must be configured during initial setup; reconfiguration required if not selected initially.

```powershell
./svc.sh install
```

--------------------------------

### Install Ruby dependencies with Bundler in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/ruby

This GitHub Actions workflow step checks out the repository, sets up a specific Ruby version (e.g., '3.1') using the `ruby/setup-ruby` action, and then installs project dependencies using `bundle install`. The Bundler version is automatically determined by your `gemfile.lock` file, or the latest compatible version if not specified.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
steps:
- uses: actions/checkout@v5
- uses: ruby/setup-ruby@ec02537da5712d66d4d50a0f33b7eb52773b5ed1
  with:
    ruby-version: '3.1'
- run: bundle install
```

--------------------------------

### Configure pre-entrypoint setup script in Docker action

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

Defines a pre-entrypoint script that runs before the main entrypoint action in a Docker container. The script executes in a separate container with the same base image, allowing prerequisite setup. Runtime state must be accessed via workspace, HOME, or STATE_ variables.

```yaml
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - 'bzz'
  pre-entrypoint: 'setup.sh'
  entrypoint: 'main.sh'
```

--------------------------------

### Example entrypoint.sh script for GitHub Action arguments

Source: https://docs.github.com/en/actions/reference/dockerfile-support-for-github-actions

This shell script serves as an example `entrypoint.sh` for a GitHub Action. It includes a shebang for POSIX compliance and demonstrates how to access and print arguments (`$@`) passed from the action's metadata, along with the argument count (`$#`). This script is designed to be executed by a Docker `ENTRYPOINT` instruction.

```bash
#!/bin/sh

# `$#` expands to the number of arguments and `$@` expands to the supplied `args`
printf '%d args:' "$#"
printf " '%s'" "$@"
printf '\n'

```

--------------------------------

### Migrate Bamboo deployment project with example output

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/bamboo-migration

Example execution of the migrate command for a Bamboo deployment project showing the command with actual values and the resulting output including logs path and pull request URL.

```bash
$ gh actions-importer migrate bamboo deployment --deployment-project-id 123 --target-url https://github.com/octo-org/octo-repo --output-dir tmp/migrate
[2023-04-20 22:08:20] Logs: 'tmp/migrate/log/actions-importer-20230420-014033.log'
[2023-04-20 22:08:20] Pull request: 'https://github.com/octo-org/octo-repo/pull/1'
```

--------------------------------

### Configure Go versions in GitHub Actions workflow

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

This GitHub Actions workflow demonstrates how to build and test a Go project across multiple Go versions using a strategy matrix. It utilizes `actions/checkout` to get the repository code and `actions/setup-go` to set up different Go versions, displaying the current Go version for verification. This allows for comprehensive testing against various Go environments.

```yaml
name: Go

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        go-version: [ '1.19', '1.20', '1.21.x' ]

    steps:
      - uses: actions/checkout@v5
      - name: Setup Go ${{ matrix.go-version }}
        uses: actions/setup-go@v5
        with:
          go-version: ${{ matrix.go-version }}
      # You can test your matrix by printing the current Go version
      - name: Display Go version
        run: go version
```

--------------------------------

### Configure Command Interactive Output Example

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/travis-ci-migration

Shows the expected interactive output when running the configure command, including prompts for CI provider selection, authentication tokens, and instance URLs. Demonstrates successful configuration with environment variables updated for Travis CI integration.

```bash
$ gh actions-importer configure
✔ Which CI providers are you configuring?: Travis CI
Enter the following values (leave empty to omit):
✔ Personal access token for GitHub: ***************
✔ Base url of the GitHub instance: https://github.com
✔ Personal access token for Travis CI: ***************
✔ Base url of the Travis CI instance: https://travis-ci.com
✔ Travis CI organization name: actions-importer-labs
Environment variables successfully updated.
```

--------------------------------

### Set up JDK 11 for x64 with GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-gradle

Configures the setup-java action to install JDK 11 from Adoptium (Temurin distribution) for x64 architecture. This action sets up the Java runtime environment and configures the PATH variable for subsequent workflow steps. Use this when you need a specific Java version different from the default OpenJDK 8.

```yaml
steps:
  - uses: actions/checkout@v5
  - name: Set up JDK 11 for x64
    uses: actions/setup-java@v4
    with:
      java-version: '11'
      distribution: 'temurin'
      architecture: x64
```

--------------------------------

### Start GitHub self-hosted runner service

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/configure-the-application_platform=mac

These commands start the GitHub self-hosted runner service. On Linux, use `svc.sh` with `sudo`. On Windows, use `Start-Service` in PowerShell.

```bash
sudo ./svc.sh start
```

```powershell
Start-Service "actions.runner.*"
```

--------------------------------

### Build and test Node.js project with npm

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Configures GitHub Actions workflow to checkout code, setup Node.js 20.x, install dependencies, run build scripts, and execute test suite. Uses npm commands defined in package.json with conditional build execution using --if-present flag. Suitable for standard Node.js CI/CD pipelines.

```yaml
steps:
- uses: actions/checkout@v5
- name: Use Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20.x'
- run: npm install
- run: npm run build --if-present
- run: npm test
```

--------------------------------

### Install Dependencies with Yarn Frozen Lockfile in GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Uses yarn with --frozen-lockfile flag to install exact versions from yarn.lock file while preventing lock file updates. This ensures reproducible builds across workflow runs. Requires Node.js setup action and checkout action.

```yaml
steps:
- uses: actions/checkout@v5
- name: Use Node.js
  uses: actions/setup-node@v4
  with:
    node-version: '20.x'
- name: Install dependencies
  run: yarn --frozen-lockfile
```

--------------------------------

### Example: Set Multiline Environment Variable from API Response

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=powershell

Provides workflow examples for setting a multiline environment variable, specifically capturing the output of an API call (e.g., `curl`). Demonstrates implementation using both Bash and PowerShell within GitHub Actions workflow steps.

```YAML (Bash)
steps:
  - name: Set the value in bash
    id: step_one
    run: |
      {
        echo 'JSON_RESPONSE<<EOF'
        curl https://example.com
        echo EOF
      } >> "$GITHUB_ENV"
```

```YAML (PowerShell)
steps:
  - name: Set the value in pwsh
    id: step_one
    run: |
      $EOF = (New-Guid).Guid
      "JSON_RESPONSE<<$EOF" >> $env:GITHUB_ENV
      (Invoke-WebRequest -Uri "https://example.com").Content >> $env:GITHUB_ENV
      "$EOF" >> $env:GITHUB_ENV
    shell: pwsh
```

--------------------------------

### Example Self-Hosted Runner Service Status Output on macOS

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/monitor-and-troubleshoot_platform=linux

Sample output from svc.sh status command showing the launchd service path, started status indicator, process ID, and service name for a self-hosted runner on macOS.

```bash
status actions.runner.example.runner01:
/Users/exampleUsername/Library/LaunchAgents/actions.runner.example.runner01.plist
Started:
379 0 actions.runner.example.runner01
```

--------------------------------

### Define GitHub Actions Workflow Steps

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

This YAML snippet defines a series of steps for a GitHub Actions job. It includes checking out the repository, setting up Node.js version 20, installing the 'bats' testing framework globally using npm, and finally executing 'bats -v' to check its version. These steps are executed sequentially on the workflow runner.

```yaml
steps:
  - uses: actions/checkout@v5
  - uses: actions/setup-node@v4
    with:
      node-version: '20'
  - run: npm install -g bats
  - run: bats -v
```

--------------------------------

### Example Self-Hosted Runner Service Log Output on Linux

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/monitor-and-troubleshoot_platform=linux

Sample journalctl output showing a self-hosted runner starting, connecting to GitHub, receiving a job named testAction, and completing execution. Demonstrates typical log entries and timestamps for monitoring runner activity.

```bash
Feb 11 14:57:07 runner01 runsvc.sh[962]: Starting Runner listener with startup type: service
Feb 11 14:57:07 runner01 runsvc.sh[962]: Started listener process
Feb 11 14:57:07 runner01 runsvc.sh[962]: Started running service
Feb 11 14:57:16 runner01 runsvc.sh[962]: √ Connected to GitHub
Feb 11 14:57:17 runner01 runsvc.sh[962]: 2020-02-11 14:57:17Z: Listening for Jobs
Feb 11 16:06:54 runner01 runsvc.sh[962]: 2020-02-11 16:06:54Z: Running job: testAction
Feb 11 16:07:10 runner01 runsvc.sh[962]: 2020-02-11 16:07:10Z: Job testAction completed with result: Succeeded
```

--------------------------------

### Define GitHub Actions Workflow Steps for Repository Checkout, Dependency Installation, and PostgreSQL Interaction (YAML)

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers

This YAML configuration outlines the sequential steps within a GitHub Actions job. It includes checking out the repository code, installing Node.js project dependencies using `npm ci`, and executing a `node client.js` script. The script connects to a PostgreSQL service, with connection parameters (`POSTGRES_HOST`, `POSTGRES_PORT`) provided via environment variables.

```yaml
steps:
  # Downloads a copy of the code in your repository before running CI tests
  - name: Check out repository code
    uses: actions/checkout@v5

  # Performs a clean installation of all dependencies in the `package.json` file
  # For more information, see https://docs.npmjs.com/cli/ci.html
  - name: Install dependencies
    run: npm ci

  - name: Connect to PostgreSQL
    # Runs a script that creates a PostgreSQL table, populates
    # the table with data, and then retrieves the data
    run: node client.js
    # Environment variables used by the `client.js` script to create
    # a new PostgreSQL table.
    env:
      # The hostname used to communicate with the PostgreSQL service container
      POSTGRES_HOST: localhost
      # The default PostgreSQL port
      POSTGRES_PORT: 5432
```

--------------------------------

### Create Basic GitHub Actions Workflow Template

Source: https://docs.github.com/en/actions/reference/reusable-workflows-reference

A foundational workflow template file demonstrating CI setup with push and pull request triggers on the default branch. Uses the $default-branch placeholder which is automatically replaced with the repository's default branch name. Includes checkout action and a simple echo script step.

```yaml
name: Octo Organization CI
on:
  push:
    branches: [ $default-branch ]
  pull_request:
    branches: [ $default-branch ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - name: Run a one-line script
        run: echo Hello from Octo Organization
```

--------------------------------

### Install apt package on Ubuntu GitHub-hosted runner using GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/manage-runners/github-hosted-runners/customize-runners

This GitHub Actions workflow demonstrates how to install an `apt` package (`jq`) on an Ubuntu GitHub-hosted runner. It first updates the `apt` package list to ensure the latest package information is available before installation. This snippet is useful for adding Linux-specific tools to your CI/CD environment.

```yaml
name: Build on Ubuntu
on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository code
        uses: actions/checkout@v5
      - name: Install jq tool
        run: |
          sudo apt-get update
          sudo apt-get install jq
```

--------------------------------

### Configure Ruby Version in GitHub Actions Workflow

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/ruby

This snippet demonstrates how to set a specific Ruby version within a GitHub Actions workflow using the `ruby/setup-ruby` action. It checks out the repository, configures Ruby 3.1, installs dependencies with `bundle install`, and runs Rake tasks. This setup is suitable for projects requiring a fixed Ruby environment.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
steps:
- uses: actions/checkout@v5
- uses: ruby/setup-ruby@ec02537da5712d66d4d50a0f33b7eb52773b5ed1
  with:
    ruby-version: '3.1' # Not needed with a .ruby-version file
- run: bundle install
- run: bundle exec rake
```

--------------------------------

### YAML Filter Pattern Examples for Branches and Tags

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Provides valid and invalid YAML syntax examples for using filter patterns with special characters in GitHub Actions workflows. Demonstrates proper quoting requirements for patterns starting with `*`, `[`, or `!` to avoid YAML parse errors. Shows both correct and incorrect implementations.

```yaml
# Valid
paths:
  - '**/README.md'

# Invalid - creates a parse error that
# prevents your workflow from running.
paths:
  - **/README.md

# Valid
branches: [ main, 'release/v[0-9].[0-9]' ]

# Invalid - creates a parse error
branches: [ main, release/v[0-9].[0-9] ]
```

--------------------------------

### Install Actions Runner Controller with Helm

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

Installs the Actions Runner Controller operator and custom resource definitions (CRDs) into a Kubernetes cluster using Helm 3. The command creates a namespace for the operator pods and deploys the latest version of the gha-runner-scale-set-controller chart from the GitHub Container Registry. Customize the NAMESPACE variable to specify the desired deployment location.

```bash
NAMESPACE="arc-systems"
helm install arc \
    --namespace "${NAMESPACE}" \
    --create-namespace \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set-controller
```

--------------------------------

### Dockerfile ENTRYPOINT with shell script execution

Source: https://docs.github.com/en/actions/creating-actions/dockerfile-support-for-github-actions

Example Dockerfile that uses a shell script as the entrypoint for a Docker container action. This approach allows proper handling of arguments from the action's metadata file and environment variable substitution. The Dockerfile copies an entrypoint.sh script and executes it when the container starts.

```dockerfile
# Container image that runs your code
FROM debian:9.5-slim

# Copies your code file from your action repository to the filesystem path `/` of the container
COPY entrypoint.sh /entrypoint.sh

# Executes `entrypoint.sh` when the Docker container starts up
ENTRYPOINT ["/entrypoint.sh"]
```

--------------------------------

### Setup CLI tool with version input and PATH configuration - JavaScript

Source: https://docs.github.com/en/actions/how-tos/create-and-publish-actions/create-a-cli-action

Demonstrates how to create a GitHub Action that retrieves a user-specified CLI version as input, downloads and extracts the tool, then adds it to the runner's PATH. Uses @actions/core for input handling and @actions/tool-cache for downloading and extracting the tool tarball. Requires an action.yml metadata file that accepts a version input parameter.

```javascript
const core = require('@actions/core');
const tc = require('@actions/tool-cache');

async function setup() {
  // Get version of tool to be installed
  const version = core.getInput('version');

  // Download the specific version of the tool, e.g. as a tarball
  const pathToTarball = await tc.downloadTool(getDownloadURL());

  // Extract the tarball onto the runner
  const pathToCLI = await tc.extractTar(pathToTarball);

  // Expose the tool by adding it to the PATH
  core.addPath(pathToCLI)
}

module.exports = setup
```

--------------------------------

### Install Dependencies from Private Registry with Authentication in GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Configures npm to use a private registry with scope and authentication token. The setup-node action creates .npmrc file with registry URL and scope settings. Requires NPM_TOKEN secret containing authentication credentials for private registry access.

```yaml
steps:
- uses: actions/checkout@v5
- name: Use Node.js
  uses: actions/setup-node@v4
  with:
    always-auth: true
    node-version: '20.x'
    registry-url: https://registry.npmjs.org
    scope: '@octocat'
- name: Install dependencies
  run: npm ci
  env:
    NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

--------------------------------

### Configure GitHub Actions Job with Ubuntu Runner

Source: https://docs.github.com/en/actions/tutorials/create-an-example-workflow

Defines a job named check-bats-version that runs on the latest Ubuntu Linux runner. This configuration creates a fresh virtual machine hosted by GitHub where all subsequent steps will execute.

```yaml
jobs:
  check-bats-version:
    runs-on: ubuntu-latest
    steps:
```

--------------------------------

### Install Actions Toolkit Packages with npm

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

Install the @actions/core and @actions/github packages from the GitHub Actions toolkit. These packages provide interfaces for workflow commands, input/output variables, and authenticated GitHub API access.

```shell
npm install @actions/core @actions/github
```

--------------------------------

### Check Docker Engine Installation Method Using which Command

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/monitor-and-troubleshoot_platform=linux

Uses the `which` command to determine the Docker engine installation path on a self-hosted runner. This helps identify if Docker was installed via snap (located at /snap/bin/docker) or as a standard binary executable. The output path indicates the installation method and can help diagnose input passing issues in GitHub Actions workflows.

```bash
$ which docker
/snap/bin/docker
```

--------------------------------

### Example Interactive Configuration of GitHub Actions Importer Credentials (Bash)

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/jenkins-migration

This example demonstrates the interactive process of configuring credentials using `gh actions-importer configure`. It shows how to input GitHub and Jenkins personal access tokens, Jenkins username, and instance URLs, confirming successful environment variable updates.

```bash
$ gh actions-importer configure
✔ Which CI providers are you configuring?: Jenkins
Enter the following values (leave empty to omit):
✔ Personal access token for GitHub: ***************
✔ Base url of the GitHub instance: https://github.com
✔ Personal access token for Jenkins: ***************
✔ Username of Jenkins user: admin
✔ Base url of the Jenkins instance: https://localhost
Environment variables successfully updated.
```

--------------------------------

### Install GitHub self-hosted runner service on Linux

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/configure-the-application_platform=mac

These commands install the GitHub self-hosted runner application as a systemd service on Linux. The first form installs it as the current user, while the second allows specifying a different user for the service.

```bash
sudo ./svc.sh install
```

```bash
./svc.sh install USERNAME
```

--------------------------------

### Override Docker Container Action Entrypoint with `entrypoint`

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example shows how to override the default `ENTRYPOINT` defined in a Dockerfile for a GitHub Action. The `entrypoint` keyword specifies a different executable to run when the container starts, allowing for custom command execution within the action's context.

```yaml
steps:
  - name: Run a custom command
    uses: octo-org/action-name@main
    with:
      entrypoint: /a/different/executable
```

--------------------------------

### Install Python Dependencies with pip in GitHub Actions (YAML)

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

This YAML snippet demonstrates how to install or upgrade Python dependencies using `pip` within a GitHub Actions workflow. After setting up a specific Python version with `actions/setup-python`, it executes a `run` step to install common packages like `pip`, `setuptools`, and `wheel`.

```YAML
steps:
- uses: actions/checkout@v5
- name: Set up Python
  uses: actions/setup-python@v5
  with:
    python-version: '3.x'
- name: Install dependencies
  run: python -m pip install --upgrade pip setuptools wheel
```

--------------------------------

### Install PowerShell dependencies from PSGallery in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/powershell

A GitHub Actions job that installs PowerShell modules (SqlServer and PSScriptAnalyzer) from the PowerShell Gallery. The workflow sets the PSGallery installation policy to Trusted before installing modules, which is required for automated module installation in CI/CD pipelines.

```yaml
jobs:
  install-dependencies:
    name: Install dependencies
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - name: Install from PSGallery
        shell: pwsh
        run: |
          Set-PSRepository PSGallery -InstallationPolicy Trusted
          Install-Module SqlServer, PSScriptAnalyzer
```

--------------------------------

### Starting a Just-In-Time (JIT) Self-Hosted Runner

Source: https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions

This command initiates a self-hosted runner in just-in-time (JIT) mode. The `${encoded_jit_config}` variable must be populated with the configuration obtained from the GitHub REST API. This ensures the runner performs a single job before automatic removal, significantly enhancing security by reducing the attack surface.

```shell
./run.sh --jitconfig ${encoded_jit_config}

```

--------------------------------

### Define Custom Shell for GitHub Actions Run Step (Perl Example)

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This snippet demonstrates how to define a custom shell for a `run` step in GitHub Actions, using `perl {0}`. The `{0}` placeholder is where GitHub inserts the temporary script file name. This example executes an inline Perl script to print all environment variables, requiring Perl to be installed on the runner.

```yaml
steps:
  - name: Display the environment variables and their values
    shell: perl {0}
    run: |
      print %ENV
```

--------------------------------

### Include Specific Branches and Tags for GitHub Actions Push Events

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow

This example illustrates how to configure a GitHub Actions workflow to run on `push` events for specific branches and tags. It uses the `branches` filter to include `main`, `mona/octocat`, and any branch starting with `releases/`, and the `tags` filter to include `v2` and any tag starting with `v1.`.

```yaml
on:
  push:
    # Sequence of patterns matched against refs/heads
    branches:
      - main
      - 'mona/octocat'
      - 'releases/**'
    # Sequence of patterns matched against refs/tags
    tags:
      - v2
      - v1.*
```

--------------------------------

### Configure OIDC `sub` claim with system-generated GUIDs in GitHub Actions

Source: https://docs.github.com/en/actions/reference/openid-connect-reference

This example enables predictable OIDC claims using system-generated GUIDs (`repository_id` or `repository_owner_id`) that remain constant even if entities are renamed. This configuration is applied by submitting the appropriate JSON payload to the GitHub Actions OIDC API endpoint for organizations or repositories.

```json
{
   "include_claim_keys": [
       "repository_id"
   ]
}
```

```json
{
   "include_claim_keys": [
       "repository_owner_id"
   ]
}
```

--------------------------------

### prepare_job Response Output JSON

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

Example output from the prepare_job command showing the responseFile contents. This JSON structure contains the state of network and containers, plus context information including container IDs, network configuration, service details, and Alpine Linux detection flag.

```json
{
  "state": {
    "network": "example_network_53269bd575972817b43f7733536b200c",
    "jobContainer": "82e8219701fe096a35941d869cf3d71af1d943b5d8bdd718857fb87ac3042480",
    "serviceContainers": {
      "redis": "60972d9aa486605e66b0dad4abb678dc3d9116f536579e418176eedb8abb9105"
    }
  },
  "context": {
    "container": {
      "id": "82e8219701fe096a35941d869cf3d71af1d943b5d8bdd718857fb87ac3042480",
      "network": "example_network_53269bd575972817b43f7733536b200c"
    },
    "services": {
      "redis": {
        "id": "60972d9aa486605e66b0dad4abb678dc3d9116f536579e418176eedb8abb9105",
        "ports": {
          "8080": "8080"
        },
        "network": "example_network_53269bd575972817b43f7733536b200c"
      }
    },
    "isAlpine": true
  }
}
```

--------------------------------

### Example: Docker Not Found Error Log

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/monitoring-and-troubleshooting-self-hosted-runners

This log output shows the error messages encountered when the `docker` executable is not found on the system. This typically indicates that Docker is not installed or not in the system's PATH, leading to job failures for container-dependent actions.

```text
[2020-02-13 16:56:10Z INFO DockerCommandManager] Which: 'docker'\n[2020-02-13 16:56:10Z INFO DockerCommandManager] Not found.\n[2020-02-13 16:56:10Z ERR  StepsRunner] Caught exception from step: System.IO.FileNotFoundException: File not found: 'docker'
```

--------------------------------

### Use Conditional Expression with Negation Operator in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Apply conditional logic to jobs using expressions with the negation operator (!). When expressions start with !, use the ${{ }} syntax or escape with quotes/parentheses since ! is reserved in YAML. This example prevents job execution when the ref starts with refs/tags/.

```yaml
if: ${{ ! startsWith(github.ref, 'refs/tags/') }}
```

--------------------------------

### Python Virtual Environment Setup and Activation

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/python-to-azure-app-service

Creates and activates a Python virtual environment for isolated dependency management. This step initializes a venv directory and sources the activation script to ensure all subsequent pip installations are isolated from system Python packages.

```bash
python -m venv venv
source venv/bin/activate
```

--------------------------------

### Create README.md for GitHub Action documentation

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-a-docker-container-action

Markdown template for documenting a GitHub Action. Includes action description, input/output specifications, secrets, environment variables, and usage examples for workflows.

```markdown
# Hello world docker action

This action prints "Hello World" or "Hello" + the name of a person to greet to the log.

## Inputs

## `who-to-greet`

**Required** The name of the person to greet. Default `"World"`.

## Outputs

## `time`

The time we greeted you.

## Example usage

uses: actions/hello-world-docker-action@v2
with:
  who-to-greet: 'Mona the Octocat'
```

--------------------------------

### Generate GitHub App Installation Access Token using cURL

Source: https://docs.github.com/en/actions/deployment/protecting-deployments/creating-custom-deployment-protection-rules

This cURL command sends a POST request to the GitHub API to generate an installation access token for a GitHub App. It requires an installation ID, a JSON Web Token (JWT) for authentication, and specifies the repository IDs and necessary permissions (write access for deployments) in the request body. This token is crucial for authenticating subsequent API calls on behalf of the app installation.

```curl
curl --request POST \
--url "https://api.github.com/app/installations/INSTALLATION_ID/ACCESS_TOKENS" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer {jwt}" \
--header "Content-Type: application/json" \
--data \
'{ \
   "repository_ids": [321], \
   "permissions": { \
      "deployments": "write" \
   } \
}'
```

--------------------------------

### Configure Swift CI workflow with matrix strategy

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/swift

Sets up a GitHub Actions workflow that builds and tests a Swift project across multiple Swift versions (5.2, 5.3) and operating systems (Ubuntu, macOS). Uses the swift-actions/setup-swift action to configure the desired Swift version and runs build and test commands. The matrix strategy allows testing against multiple configurations in parallel.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# GitHub recommends pinning actions to a commit SHA.
# To get a newer version, you will need to update the SHA.
# You can also reference a tag or branch, but the action may change without warning.

name: Swift

on: [push]

jobs:
  build:
    name: Swift ${{ matrix.swift }} on ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, macos-latest]
        swift: ["5.2", "5.3"]
    runs-on: ${{ matrix.os }}
    steps:
      - uses: swift-actions/setup-swift@65540b95f51493d65f5e59e97dcef9629ddf11bf
        with:
          swift-version: ${{ matrix.swift }}
      - uses: actions/checkout@v5
      - name: Build
        run: swift build
      - name: Run tests
        run: swift test
```

--------------------------------

### Example output of a successful Travis CI pipeline migration

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/travis-ci-migration

This example shows the typical output after successfully running the `migrate` command. It includes the log file path and the URL to the newly created pull request containing the converted workflow.

```bash
$ gh actions-importer migrate travis-ci --target-url https://github.com/octo-org/octo-repo --output-dir tmp/migrate --travis-ci-repository my-travis-ci-repository
[2022-08-20 22:08:20] Logs: 'tmp/migrate/log/actions-importer-20220916-014033.log'
[2022-08-20 22:08:20] Pull request: 'https://github.com/octo-org/octo-repo/pull/1'
```

--------------------------------

### Configure GitHub Actions Matrix with Array of Objects

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example illustrates how to define a matrix variable as an array of objects in GitHub Actions. This allows for more complex configurations where each object represents a distinct setup, such as different Node.js versions with specific environment variables. The matrix will generate jobs for each combination of `os` and the `node` objects.

```yaml
matrix:
  os:
    - ubuntu-latest
    - macos-latest
  node:
    - version: 14
    - version: 20
      env: NODE_OPTIONS=--openssl-legacy-provider

```

--------------------------------

### Define Pre and Post Hooks for JavaScript GitHub Actions

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This example demonstrates how to use `pre` and `post` hooks in a JavaScript GitHub Action. The `pre: 'setup.js'` script runs before the main action (`main: 'index.js'`), and `post: 'cleanup.js'` executes after the main action completes. These hooks are useful for setting up prerequisites and performing cleanup tasks.

```yaml
runs:
  using: 'node24'
  pre: 'setup.js'
  main: 'index.js'
  post: 'cleanup.js'
```

--------------------------------

### Request JWT using Actions core toolkit and GitHub Script

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/oidc-in-cloud-providers

Demonstrates how to use the actions/github-script action with the @actions/core toolkit to request a JSON Web Token (JWT) from GitHub's OIDC provider. This example installs required dependencies and retrieves the ID token for authentication with cloud providers. The token is then set as an output for use in subsequent workflow steps.

```yaml
jobs:
  job:
    environment: Production
    runs-on: ubuntu-latest
    steps:
    - name: Install OIDC Client from Core Package
      run: npm install @actions/core@1.6.0 @actions/http-client
    - name: Get Id Token
      uses: actions/github-script@v8
      id: idtoken
      with:
        script: |
          const coredemo = require('@actions/core')
          let id_token = await coredemo.getIDToken()
          coredemo.setOutput('id_token', id_token)
```

--------------------------------

### Define GitHub Action README Documentation (Markdown)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-docker-container-action

This Markdown snippet provides the structure and content for a `README.md` file, documenting a GitHub Action. It includes a description, definitions for inputs (`who-to-greet`), outputs (`time`), and an example of how to integrate the action into a GitHub Actions workflow. This helps users understand and utilize the action effectively.

```Markdown
# Hello world docker action

This action prints "Hello World" or "Hello" + the name of a person to greet to the log.

## Inputs

## `who-to-greet`

**Required** The name of the person to greet. Default `"World"`.

## Outputs

## `time`

The time we greeted you.

## Example usage

uses: actions/hello-world-docker-action@v2
with:
  who-to-greet: 'Mona the Octocat'

```

--------------------------------

### Check Kubernetes Pods in ARC Systems Namespace

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

This command retrieves the status of all Kubernetes pods specifically within the arc-systems namespace. Its purpose is to confirm that the Actions Runner Controller manager pod is running correctly after the Helm installation. A successful deployment is indicated by the pods showing a 'Running' status.

```bash
kubectl get pods -n arc-systems
```

--------------------------------

### Build npm packages for Docker and Kubernetes

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

Command to install dependencies and build npm packages for Docker and Kubernetes customization scripts. Generates index.js files in packages/docker/dist and packages/k8s/dist directories.

```bash
npm install && npm run bootstrap && npm run build-all
```

--------------------------------

### Interactively Configure Feature Flags

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/supplemental-arguments-and-settings

Use the configure --features command to interactively enable or disable feature flags and automatically persist them to environment variables. This provides a guided setup process for managing feature flags across multiple command executions.

```shell
$ gh actions-importer configure --features

✔ Which features would you like to configure?: actions/cache, reusable-workflows
✔ actions/cache (disabled): Enable
? reusable-workflows (disabled):
› Enable
  Disable
```

--------------------------------

### Verify GitHub Actions Importer CLI Installation and Commands

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/use-github-actions-importer

This command displays the help message for the GitHub Actions Importer CLI, confirming successful installation and listing all available subcommands. It provides an overview of the tool's capabilities, including updating, configuring, auditing, forecasting, dry-running, and migrating CI pipelines.

```bash
$ gh actions-importer -h
Options:
  -?, -h, --help  Show help and usage information

Commands:
  update     Update to the latest version of GitHub Actions Importer.
  version    Display the version of GitHub Actions Importer.
  configure  Start an interactive prompt to configure credentials used to authenticate with your CI server(s).
  audit      Plan your CI/CD migration by analyzing your current CI/CD footprint.
  forecast   Forecast GitHub Actions usage from historical pipeline utilization.
  dry-run    Convert a pipeline to a GitHub Actions workflow and output its yaml file.
  migrate    Convert a pipeline to a GitHub Actions workflow and open a pull request with the changes.
```

--------------------------------

### Workflow Status Badge URL Construction

Source: https://docs.github.com/en/actions/how-tos/monitor-workflows/add-a-status-badge

Guide for constructing workflow status badge URLs with various parameters to customize the badge display. Includes examples for default branch, specific branches, and event-triggered workflows.

```APIDOC
## Workflow Status Badge URL Patterns

### Description
Construct URLs for GitHub Actions workflow status badges using the workflow file name and optional query parameters. These URLs generate SVG badge images that can be embedded in README files and other web pages.

### Base URL Pattern
https://github.com/{OWNER}/{REPOSITORY}/actions/workflows/{WORKFLOW-FILE}/badge.svg

### URL Patterns with Parameters

#### Default Branch Status
https://github.com/{OWNER}/{REPOSITORY}/actions/workflows/{WORKFLOW-FILE}/badge.svg

#### Specific Branch Status
https://github.com/{OWNER}/{REPOSITORY}/actions/workflows/{WORKFLOW-FILE}/badge.svg?branch={BRANCH-NAME}

#### Event-Triggered Status
https://github.com/{OWNER}/{REPOSITORY}/actions/workflows/{WORKFLOW-FILE}/badge.svg?event={EVENT-TYPE}

#### Combined Parameters
https://github.com/{OWNER}/{REPOSITORY}/actions/workflows/{WORKFLOW-FILE}/badge.svg?branch={BRANCH-NAME}&event={EVENT-TYPE}

### Markdown Embedding Examples

#### Basic Badge
![example workflow](https://github.com/github/docs/actions/workflows/main.yml/badge.svg)

#### Branch-Specific Badge
![example branch parameter](https://github.com/github/docs/actions/workflows/main.yml/badge.svg?branch=feature-1)

#### Event-Specific Badge
![example event parameter](https://github.com/github/docs/actions/workflows/main.yml/badge.svg?event=push)

### Parameter Reference
- **OWNER** - Repository owner (user or organization)
- **REPOSITORY** - Repository name
- **WORKFLOW-FILE** - Workflow file name (e.g., main.yml)
- **BRANCH-NAME** - Specific branch to display status for
- **EVENT-TYPE** - Workflow trigger event (e.g., push, pull_request)
```

--------------------------------

### Example GitHub Action Repository File Structure

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

This snippet illustrates the typical file structure of a GitHub Action repository after it has been bundled and committed. It highlights key components like `action.yml` (metadata), the bundled `dist/index.js`, configuration files, and the source code directory, showing a well-organized action.

```text
hello-world-javascript-action/
├── action.yml
├── dist/
│   └── index.js
├── package.json
├── package-lock.json
├── README.md
├── rollup.config.js
└── src/
    └── index.js
```

--------------------------------

### Build Java Project with Gradle in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/java-with-gradle

This GitHub Actions workflow defines steps to set up a Java 17 environment with Temurin, initialize Gradle using the official action, and then execute a Gradle build command. It specifically uses `./gradlew -b ci.gradle package` to build and package the application based on a custom `ci.gradle` file. This ensures a consistent build process within the CI/CD pipeline.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
steps:
  - uses: actions/checkout@v5
  - uses: actions/setup-java@v4
    with:
      java-version: '17'
      distribution: 'temurin'

  - name: Setup Gradle
    uses: gradle/actions/setup-gradle@017a9effdb900e5b5b2fddfb590a105619dca3c3 # v4.4.2

  - name: Build with Gradle
    run: ./gradlew -b ci.gradle package
```

--------------------------------

### Assign Multiple Labels to Self-Hosted Runner Configuration

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/apply-labels

Assigns multiple comma-separated labels to a self-hosted runner during initial configuration. This example assigns 'gpu', 'x64', and 'linux' labels. Default labels like 'x64' and 'linux' are accepted as-is without validation of actual runner specifications.

```bash
./config.sh --url <REPOSITORY_URL> --token <REGISTRATION_TOKEN> --labels gpu,x64,linux
```

--------------------------------

### Configure WireGuard in GitHub Actions workflow

Source: https://docs.github.com/en/actions/how-tos/manage-runners/github-hosted-runners/connect-to-a-private-network/connect-with-wireguard

This GitHub Actions workflow demonstrates how to set up a WireGuard connection on an `ubuntu-latest` runner. It installs WireGuard, uses a GitHub secret for the private key, configures the `wg0` interface with specific IP addresses, sets up the peer with a public key and endpoint, activates the interface, and then attempts to connect to a service on the overlay network. This enables secure communication between the runner and a private network resource.

```yaml
name: WireGuard example

on:
  workflow_dispatch:

jobs:
  wireguard_example:
    runs-on: ubuntu-latest
    steps:
      - run: sudo apt install wireguard

      - run: echo "${{ secrets.WIREGUARD_PRIVATE_KEY }}" > privatekey

      - run: sudo ip link add dev wg0 type wireguard

      - run: sudo ip address add dev wg0 192.168.1.2 peer 192.168.1.1

      - run: sudo wg set wg0 listen-port 48123 private-key privatekey peer examplepubkey1234... allowed-ips 0.0.0.0/0 endpoint 1.2.3.4:56789

      - run: sudo ip link set up dev wg0

      - run: curl -vvv http://192.168.1.1
```

--------------------------------

### Start self-hosted runner service on Linux

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/configuring-the-self-hosted-runner-application-as-a-service

Starts the self-hosted runner service on Linux systems using the svc.sh script with sudo privileges. The service will begin accepting GitHub Actions workflow jobs.

```bash
sudo ./svc.sh start
```

--------------------------------

### Cache Go dependencies with setup-go action

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

Configure the setup-go action to cache Go dependencies using go.sum file. The action automatically detects the dependency file in the repository root and uses its hash as part of the cache key. Use cache-dependency-path parameter when multiple dependency files exist or are located in different subdirectories.

```yaml
- name: Setup Go
  uses: actions/setup-go@v5
  with:
    go-version: '1.17'
    cache-dependency-path: subdir/go.sum
```

--------------------------------

### runs.args Configuration

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Define an array of strings that serve as inputs for a Docker container. Arguments can include hardcoded strings and are passed to the container's ENTRYPOINT when it starts. Supports variable substitution and environment variable references.

```APIDOC
## runs.args

### Description
Optional property that defines an array of strings serving as inputs for a Docker container. Arguments are passed to the container's `ENTRYPOINT` when the container starts up.

### Property
`runs.args`

### Type
Array of strings

### Required
No (Optional)

### Behavior
- Arguments are used in place of the `CMD` instruction in a `Dockerfile`
- Supports hardcoded strings and variable substitution
- Can reference GitHub context variables using `${{ }}` syntax

### Best Practices
1. Document required arguments in the action's README and omit them from the `CMD` instruction
2. Use defaults that allow using the action without specifying any `args`
3. If the action exposes a `--help` flag, use that to make your action self-documenting

### Variable Substitution
To pass environment variables into an action, ensure your action runs a command shell:
- Set `entrypoint` to `"sh -c"` for shell execution
- Or configure `Dockerfile` `ENTRYPOINT` to run `"sh -c"`
- This allows `args` to execute in a command shell with variable substitution

### Configuration Example
```yaml
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - ${{ inputs.greeting }}
    - 'foo'
    - 'bar'
```

### Notes
- For more information, see Dockerfile support for GitHub Actions
- Arguments are passed directly to the container's ENTRYPOINT
```

--------------------------------

### Enable verbose logging for npm and git

Source: https://docs.github.com/en/actions/how-tos/troubleshoot-workflows

Command-line examples for enabling debug and verbose logging in npm and git to generate detailed output for troubleshooting workflow issues. These commands help diagnose problems when standard workflow logs lack sufficient detail.

```bash
npm install --verbose
```

```bash
GIT_TRACE=1 GIT_CURL_VERBOSE=1 git ...
```

--------------------------------

### Build and Test Java Project with Maven Verify in GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-maven

This YAML snippet illustrates how to build and test a Java project using Maven within a GitHub Actions workflow. It first sets up JDK 17 using `setup-java`. Then, it executes the `mvn --batch-mode --update-snapshots verify` command, which typically compiles, runs tests, and performs other verification steps defined in the project's `pom.xml`.

```yaml
steps:
  - uses: actions/checkout@v5
  - uses: actions/setup-java@v4
    with:
      java-version: '17'
      distribution: 'temurin'
  - name: Run the Maven verify phase
    run: mvn --batch-mode --update-snapshots verify
```

--------------------------------

### Configure multiple .NET versions in GitHub Actions workflow

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/net

Sets up a GitHub Actions workflow to build and test a .NET project across multiple .NET versions (3.1.x and 6.0.x) using a matrix strategy. The workflow checks out code, sets up the specified .NET version, and displays the installed version.

```yaml
name: dotnet package

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        dotnet-version: [ '3.1.x', '6.0.x' ]

    steps:
      - uses: actions/checkout@v5
      - name: Setup dotnet ${{ matrix.dotnet-version }}
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: ${{ matrix.dotnet-version }}
      - name: Display dotnet version
        run: dotnet --version
```

--------------------------------

### Filter pull_request Workflow by Branch Pattern

Source: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows

Configures a pull_request workflow to run only when pull requests target branches matching a specific pattern. This example uses the branches filter to trigger only on pull requests targeting branches starting with 'releases/'.

```yaml
on:
  pull_request:
    types:
      - opened
    branches:
      - 'releases/**'
```

--------------------------------

### Migrate Azure DevOps Release Pipeline with Project Parameter

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/azure-devops-migration

Example output from a successful Azure DevOps release pipeline migration showing the log file location and generated pull request URL. This demonstrates the expected command output format when migration completes successfully.

```bash
$ gh actions-importer migrate azure-devops release --target-url https://github.com/octo-org/octo-repo --output-dir tmp/migrate --azure-devops-project my-azure-devops-project
[2022-08-20 22:08:20] Logs: 'tmp/migrate/log/actions-importer-20220916-014033.log'
[2022-08-20 22:08:20] Pull request: 'https://github.com/octo-org/octo-repo/pull/1'
```

--------------------------------

### Start self-hosted runner service on macOS

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/configuring-the-self-hosted-runner-application-as-a-service

Starts the self-hosted runner service on macOS systems using the svc.sh script. The service uses launchd for management on macOS platforms.

```bash
./svc.sh start
```

--------------------------------

### Dynamic Runner Selection with Workflow Inputs

Source: https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions

This example shows how to use workflow dispatch inputs to dynamically select the runner operating system at workflow trigger time. The chosen OS is passed as a variable to the runs-on property.

```APIDOC
## Dynamic Runner Selection

### Description
Use workflow dispatch inputs to dynamically select runner based on user input at trigger time.

### Configuration
```yaml
on:
  workflow_dispatch:
    inputs:
      chosen-os:
        required: true
        type: choice
        options:
        - Ubuntu
        - macOS

jobs:
  test:
    runs-on: [self-hosted, "${{ inputs.chosen-os }}"]
    steps:
    - run: echo Hello world!
```

### Parameters
- **workflow_dispatch** (trigger) - Allows manual workflow triggering with inputs
- **inputs.chosen-os** (choice) - User-selectable input with predefined options
- **runs-on** (array) - Combines self-hosted label with dynamically selected OS

### Behavior
- Workflow can be triggered manually with user-selected options
- Runner selection changes based on user input
- Expression syntax required for variable interpolation
```

--------------------------------

### Install GitHub Actions Importer CLI Extension

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/use-github-actions-importer

This command installs the GitHub Actions Importer CLI extension, enabling interaction with the Importer's functionalities. It is a prerequisite for using the tool to plan and automate CI/CD migrations to GitHub Actions.

```bash
gh extension install github/gh-actions-importer
```

--------------------------------

### Install Rollup and Plugins for GitHub Action Bundling (npm)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

This `npm` command installs Rollup and its essential plugins (`@rollup/plugin-commonjs`, `@rollup/plugin-node-resolve`) as development dependencies. These tools are crucial for bundling a JavaScript GitHub Action and its dependencies into a single, distributable file, ensuring all required packages are included at runtime.

```bash
npm install --save-dev rollup @rollup/plugin-commonjs @rollup/plugin-node-resolve
```

--------------------------------

### Overwrite or append content to GitHub Actions job summary

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=powershell

This example demonstrates how to manage content in the `GITHUB_STEP_SUMMARY` file. The Bash example shows how to overwrite existing content using `>` after an initial append. The PowerShell example, however, appends new content, rather than overwriting, using `>>`.

```yaml
    - name: Overwrite Markdown
      run: |
        echo "Adding some Markdown content" >> $GITHUB_STEP_SUMMARY
        echo "There was an error, we need to clear the previous Markdown with some new content." > $GITHUB_STEP_SUMMARY
```

```yaml
    - name: Overwrite Markdown
      run: |
        "Adding some Markdown content" >> $env:GITHUB_STEP_SUMMARY
        "There was an error, we need to clear the previous Markdown with some new content." >> $env:GITHUB_STEP_SUMMARY
```

--------------------------------

### Build Python Package Distributions in GitHub Actions

Source: https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-pypi

This shell script, executed within a GitHub Actions `run` step, prepares a Python project for distribution. It first installs the `build` package using pip and then runs `python -m build` to generate standard source and wheel distribution files, which are essential for publishing to package repositories like PyPI.

```bash
python -m pip install build
python -m build
```

--------------------------------

### POST prepare_job - Configure Job Container

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

Initializes a job container with specified Docker image, environment variables, volume mounts, and service containers. This command prepares the complete execution environment for a GitHub Actions job including networking, storage, and registry authentication.

```APIDOC
## POST prepare_job

### Description
Prepares and configures a job container environment for GitHub Actions workflow execution. This command sets up the main job container with Docker image, mounts system and user volumes, configures service containers, and establishes registry authentication.

### Method
POST

### Command
prepare_job

### Request Body

#### Root Properties
- **command** (string) - Required - The command identifier, must be "prepare_job"
- **responseFile** (string) - Required - File path where the response will be written (e.g., "/users/octocat/runner/_work/{guid}.json")
- **state** (object) - Required - State object for tracking command execution
- **args** (object) - Required - Arguments containing job and service container configurations

#### args.jobContainer Properties
- **image** (string) - Required - Docker image to use for the job container (e.g., "node:18")
- **workingDirectory** (string) - Required - Working directory path inside the container
- **createOptions** (string) - Optional - Docker create options (e.g., "--cpus 1")
- **environmentVariables** (object) - Optional - Environment variables to set in the container
- **userMountVolumes** (array) - Optional - User-defined volume mounts
- **systemMountVolumes** (array) - Optional - System volume mounts managed by the runner
- **registry** (object) - Optional - Docker registry credentials for image authentication
- **portMappings** (object) - Optional - Port mappings from container to host

#### Volume Mount Properties
- **sourceVolumePath** (string) - Required - Source path on the host system
- **targetVolumePath** (string) - Required - Target path inside the container
- **readOnly** (boolean) - Required - Whether the mount is read-only

#### Registry Properties
- **username** (string) - Required - Docker registry username
- **password** (string) - Required - Docker registry password or token
- **serverUrl** (string) - Required - Docker registry server URL

#### args.services Array Properties
- **contextName** (string) - Required - Service context identifier
- **image** (string) - Required - Docker image for the service
- **createOptions** (string) - Optional - Docker create options for the service
- **environmentVariables** (object) - Optional - Environment variables for the service
- **userMountVolumes** (array) - Optional - Volume mounts for the service
- **portMappings** (object) - Optional - Port mappings for the service
- **registry** (object) - Optional - Registry credentials for the service image

### Request Example
```json
{
  "command": "prepare_job",
  "responseFile": "/users/octocat/runner/_work/{guid}.json",
  "state": {},
  "args": {
    "jobContainer": {
      "image": "node:18",
      "workingDirectory": "/__w/octocat-test2/octocat-test2",
      "createOptions": "--cpus 1",
      "environmentVariables": {
        "NODE_ENV": "development"
      },
      "userMountVolumes": [
        {
          "sourceVolumePath": "my_docker_volume",
          "targetVolumePath": "/volume_mount",
          "readOnly": false
        }
      ],
      "systemMountVolumes": [
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work",
          "targetVolumePath": "/__w",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/externals",
          "targetVolumePath": "/__e",
          "readOnly": true
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp",
          "targetVolumePath": "/__w/_temp",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_actions",
          "targetVolumePath": "/__w/_actions",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_tool",
          "targetVolumePath": "/__w/_tool",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_home",
          "targetVolumePath": "/github/home",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_workflow",
          "targetVolumePath": "/github/workflow",
          "readOnly": false
        }
      ],
      "registry": {
        "username": "octocat",
        "password": "examplePassword",
        "serverUrl": "https://index.docker.io/v1"
      },
      "portMappings": {
        "80": "801"
      }
    },
    "services": [
      {
        "contextName": "redis",
        "image": "redis",
        "createOptions": "--cpus 1",
        "environmentVariables": {},
        "userMountVolumes": [],
        "portMappings": {
          "80": "801"
        },
        "registry": {
          "username": "octocat",
          "password": "examplePassword",
          "serverUrl": "https://index.docker.io/v1"
        }
      }
    ]
  }
}
```

### Response

#### Success Response
The command writes the response to the specified responseFile path. The response indicates successful job container preparation and readiness for workflow step execution.

#### Response Properties
- **status** (string) - Command execution status
- **containerId** (string) - ID of the prepared container
- **containerReady** (boolean) - Whether the container is ready for use

### Notes
- System mount volumes are automatically managed by the GitHub Actions runner
- Registry credentials are required only if using private Docker images
- Port mappings use container port as key and host port as value
- The responseFile path uses a GUID placeholder that is replaced at runtime
```

--------------------------------

### Start self-hosted runner service on Windows

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/configuring-the-self-hosted-runner-application-as-a-service

Starts the self-hosted runner service on Windows systems using PowerShell. The wildcard pattern matches all runner service instances on the machine.

```powershell
Start-Service "actions.runner.*"
```

--------------------------------

### Install self-hosted runner service with sudo on Linux

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/configuring-the-self-hosted-runner-application-as-a-service

Installs the self-hosted runner as a systemd service on Linux systems using the svc.sh script with elevated privileges. This enables automatic service startup when the machine boots.

```bash
sudo ./svc.sh install
```

--------------------------------

### Include Specific Branches for GitHub Pull Request Workflow (YAML)

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

This example illustrates how to configure a GitHub Actions workflow to run only for pull requests targeting specific branches using the `branches` filter. It accepts glob patterns to match multiple branch names, such as `main`, `mona/octocat`, and any branch starting with `releases/`.

```yaml
on:
  pull_request:
    # Sequence of patterns matched against refs/heads
    branches:
      - main
      - 'mona/octocat'
      - 'releases/**'

```

--------------------------------

### Example Output for GitHub Actions Importer Update Command (Bash)

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/jenkins-migration

This example shows the typical output when running the `gh actions-importer update` command. It indicates whether the container image was successfully updated or if it's already up-to-date, confirming the CLI's readiness.

```bash
Updating ghcr.io/actions-importer/cli:latest...
ghcr.io/actions-importer/cli:latest up-to-date
```

--------------------------------

### Filter workflow_run Trigger by Branch Patterns

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

Uses on.workflow_run with branches filter to trigger a workflow only when a specified workflow runs on branches matching glob patterns. Supports wildcard characters like *, **, +, ?, and ! for pattern matching. The example triggers only on branches starting with 'releases/'.

```yaml
on:
  workflow_run:
    workflows: ["Build"]
    types: [requested]
    branches:
      - 'releases/**'
```

--------------------------------

### Complete reusable workflow example

Source: https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows

A full example of a reusable workflow file that accepts a config-path input and a token secret, then uses them in the actions/labeler action. This workflow can be called from other workflows to avoid duplication of labeling logic.

```yaml
name: Reusable workflow example

on:
  workflow_call:
    inputs:
      config-path:
        required: true
        type: string
    secrets:
      token:
        required: true

jobs:
  triage:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/labeler@v6
      with:
        repo-token: ${{ secrets.token }}
        configuration-path: ${{ inputs.config-path }}
```

--------------------------------

### Define GitHub Actions Workflow Name and Trigger

Source: https://docs.github.com/en/actions/tutorials/create-an-example-workflow

Sets up the workflow metadata including the display name, run-name expression using the github context, and specifies the push event as the trigger. The run-name uses the github.actor variable to display who triggered the workflow.

```yaml
name: learn-github-actions
run-name: ${{ github.actor }} is learning GitHub Actions
on: [push]
```

--------------------------------

### Configure Push Event with Branch and Tag Inclusion Filters

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Configure a GitHub Actions workflow to run on push events to specific branches and tags using inclusion filters. This example demonstrates matching exact branch names, wildcard patterns for branches starting with a prefix, and tag patterns. The workflow triggers on pushes to main, mona/octocat, releases/*, v2, and v1.* tags.

```yaml
on:
  push:
    # Sequence of patterns matched against refs/heads
    branches:
      - main
      - 'mona/octocat'
      - 'releases/**'
    # Sequence of patterns matched against refs/tags
    tags:
      - v2
      - v1.*
```

--------------------------------

### Example inputs Context JSON Structure

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

Shows the JSON structure of the inputs context containing build_id, deploy_target, and perform_deploy properties. This represents the actual values passed to a workflow that has defined these inputs.

```json
{
  "build_id": 123456768,
  "deploy_target": "deployment_sys_1a",
  "perform_deploy": true
}
```

--------------------------------

### Build and Test .NET Code with dotnet CLI

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/net

Demonstrates a GitHub Actions job that builds and tests .NET code using standard dotnet commands. The workflow checks out code, sets up the .NET SDK version 6.0.x, restores dependencies, builds the project, and runs tests. This is a foundational workflow for CI/CD pipelines.

```yaml
steps:
- uses: actions/checkout@v5
- name: Setup dotnet
  uses: actions/setup-dotnet@v4
  with:
    dotnet-version: '6.0.x'
- name: Install dependencies
  run: dotnet restore
- name: Build
  run: dotnet build --no-restore
- name: Test with the dotnet CLI
  run: dotnet test --no-build
```

--------------------------------

### Implement Conditional Step Execution in GitHub Actions Workflow

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This YAML snippet demonstrates using the `if` conditional to control whether a step executes based on an expression. The example prevents a step from running if the `github.ref` starts with `refs/tags/`, ensuring the step only runs on non-tag pushes. This allows for flexible workflow logic and skipping unnecessary operations.

```yaml
if: ${{ ! startsWith(github.ref, 'refs/tags/') }}

```

--------------------------------

### Cache PowerShell Dependencies in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/powershell

Sets up dependency caching for PowerShell modules using the actions/cache action with a unique key based on the runner OS. This allows subsequent workflow runs to restore cached dependencies, reducing installation time. The cache path varies by operating system; the example shows the Ubuntu path for PowerShell modules.

```yaml
steps:
  - uses: actions/checkout@v5
  - name: Setup PowerShell module cache
    id: cacher
    uses: actions/cache@v4
    with:
      path: "~/.local/share/powershell/Modules"
      key: ${{ runner.os }}-SqlServer-PSScriptAnalyzer
  - name: Install required PowerShell modules
    if: steps.cacher.outputs.cache-hit != 'true'
    shell: pwsh
    run: |
      Set-PSRepository PSGallery -InstallationPolicy Trusted
      Install-Module SqlServer, PSScriptAnalyzer -ErrorAction Stop
```

--------------------------------

### Install Chocolatey package on Windows GitHub-hosted runner using GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/manage-runners/github-hosted-runners/customize-runners

This GitHub Actions workflow shows how to install a Chocolatey package (`gh`) on a Windows GitHub-hosted runner. It uses the `choco install` command to add Windows-specific software. This is useful for integrating Windows tools into your CI/CD workflows.

```yaml
name: Build on Windows
on: push
jobs:
  build:
    runs-on: windows-latest
    steps:
      - run: choco install gh
      - run: gh version
```

--------------------------------

### POST /app/installations/{installation_id}/access_tokens

Source: https://docs.github.com/en/actions/how-tos/deploy/configure-and-manage-deployments/create-custom-protection-rules

Generate an installation access token for a GitHub App using a JWT. This token is required to authenticate API requests for approving or rejecting deployments in custom deployment protection rules.

```APIDOC
## POST /app/installations/{installation_id}/access_tokens

### Description
Generates an installation access token for authenticating as a GitHub App. This token is used to make authenticated requests for deployment protection rule operations.

### Method
POST

### Endpoint
https://api.github.com/app/installations/{installation_id}/access_tokens

### Parameters
#### Path Parameters
- **installation_id** (integer) - Required - The ID of the GitHub App installation

#### Request Body
- **repository_ids** (array of integers) - Optional - Array of repository IDs to scope the token to
- **permissions** (object) - Optional - Permissions object specifying access levels
  - **deployments** (string) - Optional - Permission level for deployments (e.g., "write")

### Request Example
```
curl --request POST \
--url "https://api.github.com/app/installations/INSTALLATION_ID/access_tokens" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer {jwt}" \
--header "Content-Type: application/json" \
--data '{
  "repository_ids": [321],
  "permissions": {
    "deployments": "write"
  }
}'
```

### Response
#### Success Response (201)
- **token** (string) - The generated access token for API authentication
- **expires_at** (string) - ISO 8601 timestamp when the token expires
- **permissions** (object) - The permissions granted to this token
- **repository_selection** (string) - Scope of repositories this token can access

#### Response Example
```
{
  "token": "ghu_16C7e42F292c6912E7710c838347Ae178B4a",
  "expires_at": "2024-01-15T23:59:59Z",
  "permissions": {
    "deployments": "write"
  },
  "repository_selection": "selected"
}
```
```

--------------------------------

### Configure GitHub Actions workflow with Apple certificate and provisioning profile installation

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/sign-xcode-applications

A complete GitHub Actions workflow that checks out a repository and installs Apple certificates and provisioning profiles from GitHub secrets onto a macOS runner. The step decodes base64-encoded secrets, creates a temporary keychain, imports the certificate, and applies the provisioning profile. This workflow is designed for iOS/macOS app signing during CI/CD builds.

```yaml
name: App build
on: push

jobs:
  build_with_signing:
    runs-on: macos-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v5
      - name: Install the Apple certificate and provisioning profile
        env:
          BUILD_CERTIFICATE_BASE64: ${{ secrets.BUILD_CERTIFICATE_BASE64 }}
          P12_PASSWORD: ${{ secrets.P12_PASSWORD }}
          BUILD_PROVISION_PROFILE_BASE64: ${{ secrets.BUILD_PROVISION_PROFILE_BASE64 }}
          KEYCHAIN_PASSWORD: ${{ secrets.KEYCHAIN_PASSWORD }}
        run: |
          # create variables
          CERTIFICATE_PATH=$RUNNER_TEMP/build_certificate.p12
          PP_PATH=$RUNNER_TEMP/build_pp.mobileprovision
          KEYCHAIN_PATH=$RUNNER_TEMP/app-signing.keychain-db

          # import certificate and provisioning profile from secrets
          echo -n "$BUILD_CERTIFICATE_BASE64" | base64 --decode -o $CERTIFICATE_PATH
          echo -n "$BUILD_PROVISION_PROFILE_BASE64" | base64 --decode -o $PP_PATH

          # create temporary keychain
          security create-keychain -p "$KEYCHAIN_PASSWORD" $KEYCHAIN_PATH
          security set-keychain-settings -lut 21600 $KEYCHAIN_PATH
          security unlock-keychain -p "$KEYCHAIN_PASSWORD" $KEYCHAIN_PATH

          # import certificate to keychain
          security import $CERTIFICATE_PATH -P "$P12_PASSWORD" -A -t cert -f pkcs12 -k $KEYCHAIN_PATH
          security set-key-partition-list -S apple-tool:,apple: -k "$KEYCHAIN_PASSWORD" $KEYCHAIN_PATH
          security list-keychain -d user -s $KEYCHAIN_PATH

          # apply provisioning profile
          mkdir -p ~/Library/MobileDevice/Provisioning\ Profiles
          cp $PP_PATH ~/Library/MobileDevice/Provisioning\ Profiles
      - name: Build app
          # ...
```

--------------------------------

### Dynamically Choose Runner OS with Workflow Input in GitHub Actions

Source: https://docs.github.com/en/actions/writing-workflows/choosing-where-your-workflow-runs/choosing-the-runner-for-a-job

This example illustrates how to dynamically select a runner's operating system using a workflow input. It combines a static label ('self-hosted') with a dynamic expression ('"${{ inputs.chosen-os }}"') to allow users to choose the OS at workflow dispatch time, providing flexibility for job execution.

```YAML
on:
  workflow_dispatch:
    inputs:
      chosen-os:
        required: true
        type: choice
        options:
        - Ubuntu
        - macOS

jobs:
  test:
    runs-on: [self-hosted, "${{ inputs.chosen-os }}"]
    steps:
    - run: echo Hello world!

```

--------------------------------

### Docker Engine Input Error in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/monitor-and-troubleshoot_platform=linux

Example error message that occurs when GitHub Actions cannot pass inputs to a Docker container due to Docker engine being installed as a shell wrapper or link rather than a binary executable. This commonly happens with snap-installed Docker on Linux runners where environment variables with dashes in their names cannot be properly passed to the container.

```text
Error: Input required and not supplied: java-version
```

--------------------------------

### Control GitHub Actions Job Execution with `runs-on` Labels

Source: https://docs.github.com/en/actions/how-tos/using-github-hosted-runners/using-larger-runners/running-jobs-on-larger-runners_platform=mac

These GitHub Actions workflow examples demonstrate how to use specific labels with the `runs-on` key to target self-hosted runners. The workflows check out the repository, set up Node.js, install `bats`, and run a version check. This ensures jobs run only on runners with the specified labels, allowing for platform-specific execution.

```yaml
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on:
      labels: ubuntu-24.04-16core
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v

```

```yaml
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on:
      labels: windows-2022-16core
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v

```

--------------------------------

### Migrate Azure DevOps Build Pipeline with Project Parameter

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/azure-devops-migration

Example output from a successful Azure DevOps build pipeline migration showing the log file location and generated pull request URL. This demonstrates the expected command output format when migration completes successfully.

```bash
$ gh actions-importer migrate azure-devops pipeline --target-url https://github.com/octo-org/octo-repo --output-dir tmp/migrate --azure-devops-project my-azure-devops-project
[2022-08-20 22:08:20] Logs: 'tmp/migrate/log/actions-importer-20220916-014033.log'
[2022-08-20 22:08:20] Pull request: 'https://github.com/octo-org/octo-repo/pull/1'
```

--------------------------------

### Configure Redis service container in GitHub Actions workflow

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/use-docker-service-containers

Creates a service container labeled 'redis' that runs alongside a job container. The job container (node:16-bullseye) can communicate with the Redis service container using the hostname 'redis' on the same Docker network. This example demonstrates basic service container setup for integration testing scenarios.

```yaml
name: Redis container example
on: push

jobs:
  # Label of the container job
  container-job:
    # Containers must run in Linux based operating systems
    runs-on: ubuntu-latest
    # Docker Hub image that `container-job` executes in
    container: node:16-bullseye

    # Service containers to run with `container-job`
    services:
      # Label used to access the service container
      redis:
        # Docker Hub image
        image: redis
```

--------------------------------

### GitHub Actions Complete Workflow Configuration for Ruby on Rails

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-circleci

A complete GitHub Actions workflow that builds and tests a Ruby on Rails application across multiple Ruby versions (2.5 and 2.6.3) using a matrix strategy. The workflow includes PostgreSQL service configuration with health checks, dependency caching, system package installation, database setup, and test execution using appraisal for multi-version Rails testing.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# GitHub recommends pinning actions to a commit SHA.
# To get a newer version, you will need to update the SHA.
# You can also reference a tag or branch, but the action may change without warning.

name: Containers

on: [push]

jobs:
  build:

    strategy:
      matrix:
        ruby: ['2.5', '2.6.3']

    runs-on: ubuntu-latest

    env:
      PGHOST: localhost
      PGUSER: administrate
      RAILS_ENV: test

    services:
      postgres:
        image: postgres:10.1-alpine
        env:
          POSTGRES_USER: administrate
          POSTGRES_DB: ruby25
          POSTGRES_PASSWORD: ""
        ports:
          - 5432:5432
        # Add a health check
        options: --health-cmd pg_isready --health-interval 10s --health-timeout 5s --health-retries 5

    steps:
      - uses: actions/checkout@v5
      - name: Setup Ruby
        uses: eregon/use-ruby-action@ec02537da5712d66d4d50a0f33b7eb52773b5ed1
        with:
          ruby-version: ${{ matrix.ruby }}
      - name: Cache dependencies
        uses: actions/cache@v4
        with:
          path: vendor/bundle
          key: administrate-${{ matrix.image }}-${{ hashFiles('Gemfile.lock') }}
      - name: Install postgres headers
        run: |
          sudo apt-get update
          sudo apt-get install libpq-dev
      - name: Install dependencies
        run: bundle install --path vendor/bundle
      - name: Setup environment configuration
        run: cp .sample.env .env
      - name: Setup database
        run: bundle exec rake db:setup
      - name: Run tests
        run: bundle exec rake
      - name: Install appraisal
        run: bundle exec appraisal install
      - name: Run appraisal
        run: bundle exec appraisal rake
```

--------------------------------

### Install Python Dependencies from Requirements File

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/python-to-azure-app-service

Installs all Python project dependencies listed in requirements.txt using pip. This command runs after the virtual environment is activated and should be preceded by dependency caching for optimal performance in CI/CD pipelines.

```bash
pip install -r requirements.txt
```

--------------------------------

### Define Docker Container for GitHub Action

Source: https://docs.github.com/en/actions/creating-actions/creating-a-docker-container-action

This Dockerfile sets up the container environment for a GitHub Action. It uses an Alpine Linux base image, copies the `entrypoint.sh` script into the container, and specifies this script as the entry point for execution when the container starts.

```Dockerfile
# Container image that runs your code
FROM alpine:3.10

# Copies your code file from your action repository to the filesystem path `/` of the container
COPY entrypoint.sh /entrypoint.sh

# Code file to execute when the docker container starts up (`entrypoint.sh`)
ENTRYPOINT ["/entrypoint.sh"]
```

--------------------------------

### Use OIDC Credentials for Docker Registry Authentication in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/oidc-in-jfrog

GitHub Actions workflow step demonstrating how to use OIDC credentials from the setup-jfrog-cli action for authenticating with Docker registries. The oidc-user and oidc-token outputs from the setup step are passed to the docker/login-action.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
      - name: Sign in to Artifactory Docker registry
        uses: docker/login-action@v3
        with:
          registry: ${{ env.JF_URL }}
          username: ${{ steps.setup-jfrog-cli.outputs.oidc-user }}
          password: ${{ steps.setup-jfrog-cli.outputs.oidc-token }}
```

--------------------------------

### Define GitHub Actions Workflow with Multi-OS Runners

Source: https://docs.github.com/en/actions/how-tos/manage-runners/github-hosted-runners/use-github-hosted-runners

This YAML workflow demonstrates how to run different jobs on different GitHub-hosted operating systems. It includes a job to run `npm help` on `ubuntu-latest` and another job to install `PSScriptAnalyzer` and list its rules on `windows-latest`, showcasing parallel execution on separate virtual machines.

```yaml
name: Run commands on different operating systems
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  Run-npm-on-Ubuntu:
    name: Run npm on Ubuntu
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '14'
      - run: npm help

  Run-PSScriptAnalyzer-on-Windows:
    name: Run PSScriptAnalyzer on Windows
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v5
      - name: Install PSScriptAnalyzer module
        shell: pwsh
        run: |
          Set-PSRepository PSGallery -InstallationPolicy Trusted
          Install-Module PSScriptAnalyzer -ErrorAction Stop
      - name: Get list of rules
        shell: pwsh
        run: |
          Get-ScriptAnalyzerRule
```

--------------------------------

### Example: Set and Use Single-Line Environment Variable in Workflow

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=powershell

Demonstrates how to define an environment variable within one GitHub Actions workflow step and then access its value in a subsequent step. Examples are provided for both Bash and PowerShell run commands.

```YAML (Bash)
steps:
  - name: Set the value
    id: step_one
    run: |
      echo "action_state=yellow" >> "$GITHUB_ENV"
  - name: Use the value
    id: step_two
    run: |
      printf '%s\n' "$action_state" # This will output 'yellow'
```

```YAML (PowerShell)
steps:
  - name: Set the value
    id: step_one
    run: |
      "action_state=yellow" >> $env:GITHUB_ENV
  - name: Use the value
    id: step_two
    run: |
      Write-Output "$env:action_state" # This will output 'yellow'
```

--------------------------------

### Actions in GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-azure-pipelines-to-github-actions

Demonstrates how to use actions in GitHub Actions as the equivalent to Azure Pipelines tasks. The example uses the setup-python action to configure Python 3.7 with x64 architecture, followed by a run step to execute a Python script.

```yaml
jobs:
  run_python:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/setup-python@v5
        with:
          python-version: '3.7'
          architecture: 'x64'
      - run: python script.py
```

--------------------------------

### Install Homebrew packages and casks on macOS GitHub-hosted runner using GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/manage-runners/github-hosted-runners/customize-runners

This GitHub Actions workflow illustrates how to install Homebrew packages (`gh`) and casks (`microsoft-edge`) on a macOS GitHub-hosted runner. It updates Homebrew before installing to ensure access to the latest versions. This is essential for adding macOS-specific software to your CI/CD pipeline.

```yaml
name: Build on macOS
on: push

jobs:
  build:
    runs-on: macos-latest
    steps:
      - name: Check out repository code
        uses: actions/checkout@v5
      - name: Install GitHub CLI
        run: |
          brew update
          brew install gh
      - name: Install Microsoft Edge
        run: |
          brew update
          brew install --cask microsoft-edge
```

--------------------------------

### Generated .npmrc Configuration for Private Registry

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Example .npmrc file content generated by setup-node action when configuring private registry authentication. Contains authentication token reference, registry URL mapping for scope, and always-auth setting for secure registry communication.

```text
//registry.npmjs.org/:_authToken=${NODE_AUTH_TOKEN}
@octocat:registry=https://registry.npmjs.org/
always-auth=true
```

--------------------------------

### Use Environment Variable for Safe Inline Script Input Handling

Source: https://docs.github.com/en/actions/reference/security/secure-use

Shows how to safely handle untrusted input in inline Bash scripts by storing context values in intermediate environment variables. This approach prevents script injection by separating variable assignment from script generation. The example checks if a pull request title starts with 'octocat' using pattern matching on the environment variable.

```yaml
- name: Check PR title
  env:
    TITLE: ${{ github.event.pull_request.title }}
  run: |
    if [[ "$TITLE" =~ ^octocat ]]; then
    echo "PR title starts with 'octocat'"
    exit 0
    else
    echo "PR title did not start with 'octocat'"
    exit 1
    fi
```

--------------------------------

### Implement Multi-Operating System Builds and Tests

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-jenkins-to-github-actions

These examples demonstrate how to configure CI/CD pipelines to build and test applications across multiple operating systems. Both Jenkins and GitHub Actions utilize a matrix strategy to define different OS environments, ensuring broad compatibility and robust testing.

```groovy
pipeline {
  agent none
  stages {
    stage('Run Tests') {
      matrix {
        axes {
          axis {
            name: 'PLATFORM'
            values: 'macos', 'linux'
          }
        }
        agent { label "${PLATFORM}" }
        stages {
          stage('test') {
            tools { nodejs "node-20" }
            steps {
              dir("scripts/myapp") {
                sh(script: "npm install -g bats")
                sh(script: "bats tests")
              }
            }
          }
        }
      }
    }
  }
}
```

```yaml
name: demo-workflow
on:
  push:
jobs:
  test:
    runs-on: ${{ matrix.os }}
    strategy:
      fail-fast: false
      matrix:
        os: [macos-latest, ubuntu-latest]
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm install -g bats
      - run: bats tests
        working-directory: ./scripts/myapp
```

--------------------------------

### Example Secrets Context Contents (JSON)

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

Shows an example of the `secrets` context, including the automatically generated `GITHUB_TOKEN` and placeholders for other custom secrets (`NPM_TOKEN`, `SUPERSECRET`) that are available to a GitHub Actions workflow run.

```json
{
  "github_token": "***",
  "NPM_TOKEN": "***",
  "SUPERSECRET": "***"
}
```

--------------------------------

### GitHub Actions Docker Container Action with Public Registry Image

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This example demonstrates configuring a Docker container action to utilize an image from a public Docker registry. The `using: 'docker'` keyword is essential, and the `image` property specifies the full path to the desired Docker image, such as `debian:stretch-slim`.

```yaml
runs:
  using: 'docker'
  image: 'docker://debian:stretch-slim'
```

--------------------------------

### Configure GitHub Actions workflow for multiple Python versions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

This workflow demonstrates how to use a matrix strategy in GitHub Actions to test a Python project against multiple Python and PyPy versions. It checks out the repository, sets up the specified Python version using `setup-python@v5`, and then prints the Python version for verification. This ensures compatibility across different environments by running the same job with varying Python configurations.

```YAML
name: Python package

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ["pypy3.10", "3.9", "3.10", "3.11", "3.12", "3.13"]

    steps:
      - uses: actions/checkout@v5
      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}
      # You can test your matrix by printing the current Python version
      - name: Display Python version
        run: python -c "import sys; print(sys.version)"
```

--------------------------------

### Enable Bundler dependency caching with setup-ruby in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/ruby

This GitHub Actions workflow step uses the `ruby/setup-ruby` action with `bundler-cache: true` to automatically handle caching of Ruby gems. This configures Bundler to install gems to `vendor/cache`, which is then cached by GitHub Actions for subsequent workflow runs, improving build times.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
steps:
- uses: ruby/setup-ruby@ec02537da5712d66d4d50a0f33b7eb52773b5ed1
  with:
    bundler-cache: true
```

--------------------------------

### Initialize npm Project in Shell

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

Initialize a new npm project in the hello-world-javascript-action directory to generate a package.json file. This creates the foundation for managing project dependencies and scripts.

```shell
cd hello-world-javascript-action
```

--------------------------------

### Set a specific Go version in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

This GitHub Actions step configures the `setup-go` action to use a specific Go version, such as `1.21.x`. It supports semantic version range syntax or an exact version, ensuring the project builds with a consistent and desired Go environment. This is typically part of a larger workflow job.

```yaml
      - name: Setup Go 1.21.x
        uses: actions/setup-go@v5
        with:
          # Semantic version range syntax or exact version of Go
          go-version: '1.21.x'
```

--------------------------------

### run_script_step JSON Input Configuration

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

Example JSON input structure for the run_script_step command in GitHub Actions runner container hooks. Includes network state, job container reference, service containers, and execution arguments such as entry point, environment variables, and working directory.

```json
{
  "command": "run_script_step",
  "responseFile": null,
  "state": {
    "network": "example_network_53269bd575972817b43f7733536b200c",
    "jobContainer": "82e8219701fe096a35941d869cf3d71af1d943b5d8bdd718857fb87ac3042480",
    "serviceContainers": {
      "redis": "60972d9aa486605e66b0dad4abb678dc3d9116f536579e418176eedb8abb9105"
    }
  },
  "args": {
    "entryPointArgs": ["-e", "/runner/temp/example.sh"],
    "entryPoint": "bash",
    "environmentVariables": {
      "NODE_ENV": "development"
    },
    "prependPath": ["/foo/bar", "bar/foo"],
    "workingDirectory": "/__w/octocat-test2/octocat-test2"
  }
}
```

--------------------------------

### Run npm command in GitHub Actions workflow

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/add-scripts

Execute a shell command (npm install) on the runner using the run keyword. This is the simplest form of running commands in a GitHub Actions job, useful for installing dependencies or running one-off commands.

```yaml
jobs:
  example-job:
    runs-on: ubuntu-latest
    steps:
      - run: npm install -g bats
```

--------------------------------

### Build and Test Node.js Project in GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-travis-ci-to-github-actions

Install dependencies and run build and test scripts for Node.js projects. This workflow installs npm packages, runs the build process, and executes tests in sequence.

```yaml
install:
  - npm install
script:
  - npm run build
  - npm test
```

--------------------------------

### Configure Cache Restore Keys - YAML

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching

Example demonstrating the use of restore-keys parameter for fallback cache matching. When the primary key doesn't match, the action sequentially searches these restore keys for partial matches, allowing more flexible cache restoration strategies with varying specificity levels.

```yaml
restore-keys: |
  npm-feature-${{ hashFiles('package-lock.json') }}
  npm-feature-
  npm-
```

--------------------------------

### Define Input Parameters for a GitHub Action Step using `with`

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates how to define and pass input parameters to a GitHub Action using the `with` keyword within a workflow step. The specified `first_name`, `middle_name`, and `last_name` values will be accessible inside the `hello_world` action as `INPUT_FIRST_NAME`, `INPUT_MIDDLE_NAME`, and `INPUT_LAST_NAME` environment variables, respectively.

```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: actions/hello_world@main
        with:
          first_name: Mona
          middle_name: The
          last_name: Octocat
```

--------------------------------

### Example migrate command output with pull request URL

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/jenkins-migration

Shows the expected output format from a successful migrate command execution, including the log file location and the generated pull request URL that contains the converted GitHub Actions workflow.

```bash
$ gh actions-importer migrate jenkins --target-url https://github.com/octo-org/octo-repo --output-dir tmp/migrate --source-url http://localhost:8080/job/monas_dev_work/job/monas_freestyle
[2022-08-20 22:08:20] Logs: 'tmp/migrate/log/actions-importer-20220916-014033.log'
[2022-08-20 22:08:20] Pull request: 'https://github.com/octo-org/octo-repo/pull/1'
```

--------------------------------

### Define Azure Pipelines Template Path with Parameters

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/azure-devops-migration

This example illustrates how to use a parameter to dynamically specify a template file path in Azure Pipelines. The `template` parameter is defined with a default value, which is then used within the `steps` section to reference the template, providing flexibility in template selection.

```yaml
parameters:
- name: template
  type: string
  default: simple_step.yml

steps:
- template: "./templates/${{ parameters.template }}"
```

--------------------------------

### runs.pre-entrypoint Configuration

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Configure a pre-entrypoint script that runs before the main entrypoint action begins. This allows you to set up prerequisites in a separate container using the same base image. The script can access workspace, HOME, or STATE_ variables.

```APIDOC
## runs.pre-entrypoint

### Description
Optional configuration that allows you to run a script before the `entrypoint` action begins. GitHub Actions uses `docker run` to launch this action in a new container with the same base image.

### Property
`runs.pre-entrypoint`

### Type
String (path to script file)

### Required
No (Optional)

### Default Behavior
The `pre-entrypoint` action always runs by default but can be overridden using `runs.pre-if`.

### Runtime State
The runtime state is different from the main `entrypoint` container. Required state must be accessed via:
- Workspace directory
- `HOME` environment variable
- `STATE_` prefixed variables

### Configuration Example
```yaml
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - 'bzz'
  pre-entrypoint: 'setup.sh'
  entrypoint: 'main.sh'
```

### Notes
- The runtime specified with the `using` syntax will execute this file
- Commonly used for prerequisite setup scripts
- Runs in a separate container from the main entrypoint
```

--------------------------------

### Start GitHub Actions Self-Hosted Runner Service

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/configure-the-application_platform=windows

These commands are used to start the GitHub Actions self-hosted runner service on both Linux and Windows. For Debian-based Linux systems, an additional command is provided to configure `needrestart` to ignore the runner service.

```shell
sudo ./svc.sh start
```

```powershell
Start-Service "actions.runner.*"
```

```shell
./svc.sh start
```

```shell
echo '$nrconf{override_rc}{qr(^actions\.runner\..+\.service$)} = 0;' | sudo tee /etc/needrestart/conf.d/actions_runner_services.conf
```

--------------------------------

### Integrating Public GitHub Actions from Repositories in YAML

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates how to integrate public GitHub Actions into a workflow. It shows how to reference actions from other repositories using either their default branch or a specific version tag, allowing reuse of community-contributed functionality.

```YAML
jobs:
  my_first_job:
    steps:
      - name: My first step
        # Uses the default branch of a public repository
        uses: actions/heroku@main
      - name: My second step
        # Uses a specific version tag of a public repository
        uses: actions/aws@v2.0.1
```

--------------------------------

### Configure GitHub Actions Job and Service Containers (JSON)

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

This JSON snippet illustrates the input structure for the `prepare_job` command in GitHub Actions. It defines the main job container's image, working directory, environment variables, volume mounts (user and system), registry credentials, and port mappings. Additionally, it specifies a service container (e.g., Redis) with its own configuration, including image, creation options, and registry details.

```json
{
  "command": "prepare_job",
  "responseFile": "/users/octocat/runner/_work/{guid}.json",
  "state": {},
  "args": {
    "jobContainer": {
      "image": "node:18",
      "workingDirectory": "/__w/octocat-test2/octocat-test2",
      "createOptions": "--cpus 1",
      "environmentVariables": {
        "NODE_ENV": "development"
      },
      "userMountVolumes": [
        {
          "sourceVolumePath": "my_docker_volume",
          "targetVolumePath": "/volume_mount",
          "readOnly": false
        }
      ],
      "systemMountVolumes": [
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work",
          "targetVolumePath": "/__w",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/externals",
          "targetVolumePath": "/__e",
          "readOnly": true
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp",
          "targetVolumePath": "/__w/_temp",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_actions",
          "targetVolumePath": "/__w/_actions",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_tool",
          "targetVolumePath": "/__w/_tool",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_home",
          "targetVolumePath": "/github/home",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_workflow",
          "targetVolumePath": "/github/workflow",
          "readOnly": false
        }
      ],
      "registry": {
        "username": "octocat",
        "password": "examplePassword",
        "serverUrl": "https://index.docker.io/v1"
      },
      "portMappings": { "80": "801" }
    },
    "services": [
      {
        "contextName": "redis",
        "image": "redis",
        "createOptions": "--cpus 1",
        "environmentVariables": {},
        "userMountVolumes": [],
        "portMappings": { "80": "801" },
        "registry": {
          "username": "octocat",
          "password": "examplePassword",
          "serverUrl": "https://index.docker.io/v1"
        }
      }
    ]
  }
}
```

--------------------------------

### Configure Redis Service Container for GitHub Actions Job in Container (YAML)

Source: https://docs.github.com/en/actions/using-containerized-services/creating-redis-service-containers

This GitHub Actions workflow demonstrates how to set up a Redis service container for a job that runs within another container (e.g., a Node.js container). It defines a `redis` service, configures health checks, checks out repository code, installs dependencies, and then runs a Node.js script (`client.js`) to interact with the Redis service using environment variables for host and port. This setup simplifies networking as Docker containers on the same user-defined bridge network expose all ports to each other.

```yaml
name: Redis container example
on: push

jobs:
  # Label of the container job
  container-job:
    # Containers must run in Linux based operating systems
    runs-on: ubuntu-latest
    # Docker Hub image that `container-job` executes in
    container: node:20-bookworm-slim

    # Service containers to run with `container-job`
    services:
      # Label used to access the service container
      redis:
        # Docker Hub image
        image: redis
        # Set health checks to wait until redis has started
        options: >-
          --health-cmd "redis-cli ping"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      # Downloads a copy of the code in your repository before running CI tests
      - name: Check out repository code
        uses: actions/checkout@v5

      # Performs a clean installation of all dependencies in the `package.json` file
      # For more information, see https://docs.npmjs.com/cli/ci.html
      - name: Install dependencies
        run: npm ci

      - name: Connect to Redis
        # Runs a script that creates a Redis client, populates
        # the client with data, and retrieves data
        run: node client.js
        # Environment variable used by the `client.js` script to create a new Redis client.
        env:
          # The hostname used to communicate with the Redis service container
          REDIS_HOST: redis
          # The default Redis port
          REDIS_PORT: 6379
```

--------------------------------

### Check Docker Engine Installation Path on Linux

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/monitoring-and-troubleshooting-self-hosted-runners

This command is used on Linux to determine the executable path of the 'docker' command. It helps identify if Docker was installed via a package manager like `snap`, which can sometimes cause issues with GitHub Actions self-hosted runners due to how inputs are passed.

```bash
$ which docker
/snap/bin/docker

```

--------------------------------

### Unsupported Action Reference Patterns for Dependabot

Source: https://docs.github.com/en/actions/reference/security/secure-use

Demonstrates action reference patterns that Dependabot does not support for automatic updates. These include local action references, Docker container actions using docker:// syntax, and private registry configurations that require special setup.

```yaml
- uses: ./.github/actions/foo.yml
- uses: docker://myregistry.azurecr.io/myimage:latest
```

--------------------------------

### GitHub Actions workflow for publishing Maven package to GitHub Packages

Source: https://docs.github.com/en/actions/tutorials/publish-packages/publish-java-packages-with-maven

Complete workflow that triggers on release creation, sets up Java JDK using setup-java action, and deploys the Maven package to GitHub Packages. The workflow automatically configures Maven settings.xml with GITHUB_TOKEN authentication and requires read access to contents and write access to packages.

```yaml
name: Publish package to GitHub Packages
on:
  release:
    types: [created]
jobs:
  publish:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-java@v4
        with:
          java-version: '11'
          distribution: 'temurin'
      - name: Publish package
        run: mvn --batch-mode deploy
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

--------------------------------

### Install self-hosted runner service as specific user on Linux

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/configuring-the-self-hosted-runner-application-as-a-service

Installs the self-hosted runner service as a different user on Linux systems. The USERNAME argument allows service execution under a non-root account for security purposes.

```bash
./svc.sh install USERNAME
```

--------------------------------

### Install ARC runner scale set with Helm using PAT

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/using-actions-runner-controller-runners-in-a-workflow

Helm installation command for Actions Runner Controller with Personal Access Token authentication. Sets up a runner scale set named 'arc-runner-set' in the 'arc-runners' namespace with GitHub configuration URL and authentication token.

```bash
# Using a Personal Access Token (PAT)
INSTALLATION_NAME="arc-runner-set"
NAMESPACE="arc-runners"
GITHUB_CONFIG_URL="https://github.com/<your_enterprise/org/repo>"
GITHUB_PAT="<PAT>"
helm install "${INSTALLATION_NAME}" \
    --namespace "${NAMESPACE}" \
    --create-namespace \
    --set githubConfigUrl="${GITHUB_CONFIG_URL}" \
    --set githubConfigSecret.github_token="${GITHUB_PAT}" \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set
```

--------------------------------

### Define Azure Pipelines Template Path with Iteration

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/azure-devops-migration

This example shows how to iteratively apply templates based on a list of steps defined as a parameter in Azure Pipelines. The `each` expression loops through the `steps` parameter, dynamically referencing different templates for each item, enabling repetitive template usage.

```yaml
parameters:
- name: steps
  type: object
  default:
  - build_step
  - release_step
steps:
- ${{ each step in parameters.steps }}:
    - template: "$-variables.yml"
```

--------------------------------

### Configure Node.js versions with matrix strategy in GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Sets up a matrix strategy to build and test code across multiple Node.js versions (18.x and 20.x). Uses the setup-node action to configure each version on the runner and adds necessary binaries to PATH. The matrix context allows each job to access the specific Node.js version being tested.

```yaml
strategy:
  matrix:
    node-version: ['18.x', '20.x']

steps:
- uses: actions/checkout@v5
- name: Use Node.js ${{ matrix.node-version }}
  uses: actions/setup-node@v4
  with:
    node-version: ${{ matrix.node-version }}
```

--------------------------------

### Example Runner Context Contents (JSON)

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

Illustrates the typical structure and values of the `runner` context object for a Linux GitHub-hosted runner, including properties like `os`, `arch`, `name`, `tool_cache`, and `temp`.

```json
{
  "os": "Linux",
  "arch": "X64",
  "name": "GitHub Actions 2",
  "tool_cache": "/opt/hostedtoolcache",
  "temp": "/home/runner/work/_temp"
}
```

--------------------------------

### Example Caller Workflow with Inputs and Secrets in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows

This example illustrates a complete caller workflow that triggers on a pull request to the `main` branch. It calls two different reusable workflows: one without any specific inputs or secrets, and another (`workflow-B.yml`) that passes a `config-path` input and a `GITHUB_TOKEN` secret.

```yaml
name: Call a reusable workflow

on:
  pull_request:
    branches:
      - main

jobs:
  call-workflow:
    uses: octo-org/example-repo/.github/workflows/workflow-A.yml@v1

  call-workflow-passing-data:
    permissions:
      contents: read
      pull-requests: write
    uses: octo-org/example-repo/.github/workflows/workflow-B.yml@main
    with:
      config-path: .github/labeler.yml
    secrets:
      token: ${{ secrets.GITHUB_TOKEN }}
```

--------------------------------

### Define and Use Job Outputs in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates how to define outputs for a job in GitHub Actions and how a subsequent job can access these outputs. It shows mapping step outputs to job outputs and then referencing them in a dependent job using the `needs` context.

```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    # Map a step output to a job output
    outputs:
      output1: ${{ steps.step1.outputs.test }}
      output2: ${{ steps.step2.outputs.test }}
    steps:
      - id: step1
        run: echo "test=hello" >> "$GITHUB_OUTPUT"
      - id: step2
        run: echo "test=world" >> "$GITHUB_OUTPUT"
  job2:
    runs-on: ubuntu-latest
    needs: job1
    steps:
      - env:
          OUTPUT1: ${{needs.job1.outputs.output1}}
          OUTPUT2: ${{needs.job1.outputs.output2}}
        run: echo "$OUTPUT1 $OUTPUT2"
```

--------------------------------

### Matrix Include Strategy for Adding Configurations

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

Extends the base matrix combinations by adding new job configurations through the include property. This example creates 10 jobs from the base matrix (3 os × 3 version combinations) plus 1 additional job for windows-latest with version 17.

```yaml
jobs:
  example_matrix:
    strategy:
      matrix:
        os: [macos-latest, windows-latest, ubuntu-latest]
        version: [12, 14, 16]
        include:
          - os: windows-latest
            version: 17
```

--------------------------------

### Perform matrix testing for Ruby projects in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/ruby

This GitHub Actions workflow sets up a matrix strategy to test a Ruby project across various operating systems (Ubuntu, macOS) and Ruby versions (including stable, head, JRuby, and TruffleRuby). It checks out the code, configures the Ruby environment using `setup-ruby` for each matrix combination, installs dependencies, and executes Rake tasks for testing.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# GitHub recommends pinning actions to a commit SHA.
# To get a newer version, you will need to update the SHA.
# You can also reference a tag or branch, but the action may change without warning.

name: Matrix Testing

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ${{ matrix.os }}-latest
    strategy:
      fail-fast: false
      matrix:
        os: [ubuntu, macos]
        ruby: [2.5, 2.6, 2.7, head, debug, jruby, jruby-head, truffleruby, truffleruby-head]
    continue-on-error: ${{ endsWith(matrix.ruby, 'head') || matrix.ruby == 'debug' }}
    steps:
      - uses: actions/checkout@v5
      - uses: ruby/setup-ruby@ec02537da5712d66d4d50a0f33b7eb52773b5ed1
        with:
          ruby-version: ${{ matrix.ruby }}
      - run: bundle install
      - run: bundle exec rake
```

--------------------------------

### Basic Gradle Build Workflow in GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-gradle

Sets up a GitHub Actions workflow to build a Java project using Gradle. This workflow checks out the repository, sets up Java 17 with Temurin distribution, configures Gradle, and runs a build command. It provides the foundation for automated Java project builds.

```yaml
steps:
  - uses: actions/checkout@v5
  - uses: actions/setup-java@v4
    with:
      java-version: '17'
      distribution: 'temurin'

  - name: Setup Gradle
    uses: gradle/actions/setup-gradle@017a9effdb900e5b5b2fddfb590a105619dca3c3 # v4.4.2

  - name: Build with Gradle
    run: ./gradlew -b ci.gradle package
```

--------------------------------

### Access jobs context outputs in reusable GitHub Actions workflows

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

Example showing the structure of the `jobs` context available only in reusable workflows. The context contains job results (success, failure, cancelled, or skipped) and outputs from jobs in the reusable workflow. This example demonstrates accessing outputs from a job named `example_job`.

```json
{
  "example_job": {
    "result": "success",
    "outputs": {
      "output1": "hello",
      "output2": "world"
    }
  }
}
```

--------------------------------

### Publish Package to npm Registry with Yarn

Source: https://docs.github.com/en/actions/tutorials/publish-packages/publish-nodejs-packages

GitHub Actions workflow for publishing npm packages using Yarn package manager to npmjs registry on release publication. Configures setup-node with npm registry URL and uses Yarn commands for installation and publishing. Requires NPM_TOKEN secret for authentication.

```yaml
name: Publish Package to npmjs
on:
  release:
    types: [published]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      # Setup .npmrc file to publish to npm
      - uses: actions/setup-node@v4
        with:
          node-version: '20.x'
          registry-url: 'https://registry.npmjs.org'
          # Defaults to the user or organization that owns the workflow file
          scope: '@octocat'
      - run: yarn
      - run: yarn npm publish // for Yarn version 1, use `yarn publish` instead
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

--------------------------------

### Install Kustomize CLI for Kubernetes Manifest Customization

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/google-kubernetes-engine

This script downloads a specific version (v3.1.0) of the Kustomize command-line tool from its GitHub releases. Kustomize is a declarative configuration management tool for Kubernetes that allows users to customize raw, template-free YAML files. After download, it makes the binary executable.

```bash
curl -sfLo kustomize https://github.com/kubernetes-sigs/kustomize/releases/download/v3.1.0/kustomize_3.1.0_linux_amd64
chmod u+x ./kustomize
```

--------------------------------

### Access job context properties in GitHub Actions

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

Example showing the structure and contents of the `job` context when using service containers. The context includes job status, check run ID, container network information, and service container details with mapped ports. This example demonstrates a PostgreSQL service container with port mapping.

```json
{
  "status": "success",
  "check_run_id": 51725241954,
  "container": {
    "network": "github_network_53269bd575974817b43f4733536b200c"
  },
  "services": {
    "postgres": {
      "id": "60972d9aa486605e66b0dad4abb638dc3d9116f566579e418166eedb8abb9105",
      "ports": {
        "5432": "49153"
      },
      "network": "github_network_53269bd575974817b43f4733536b200c"
    }
  }
}
```

--------------------------------

### Define and Access GitHub Actions Service Containers via Localhost

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example sets up `nginx` and `redis` as service containers for a GitHub Actions job. It demonstrates how to map ports, including dynamically assigned ones, and access these services from a job running directly on the runner machine using `localhost` and the port values available in the `job.services.<service_name>.ports` context.

```yaml
services:
  nginx:
    image: nginx
    # Map port 8080 on the Docker host to port 80 on the nginx container
    ports:
      - 8080:80
  redis:
    image: redis
    # Map random free TCP port on Docker host to port 6379 on redis container
    ports:
      - 6379/tcp
steps:
  - run: |
      echo "Redis available on 127.0.0.1:${{ job.services.redis.ports['6379'] }}"
      echo "Nginx available on 127.0.0.1:${{ job.services.nginx.ports['80'] }}"

```

--------------------------------

### Prepare Job Command

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/customize-containers

This command initiates the preparation of a job execution environment, specifying details for the main job container and any associated service containers. The command's response is written to a specified file.

```APIDOC
## POST /prepare_job

### Description
Initiates the preparation of a job execution environment for GitHub Actions. This involves configuring the main job container and any dependent service containers, including their images, working directories, environment variables, and volume mounts. The outcome of the preparation is asynchronously written to a designated response file.

### Method
POST

### Endpoint
/prepare_job

### Parameters
#### Path Parameters
(None)

#### Query Parameters
(None)

#### Request Body
- **command** (string) - Required - The specific command to execute. Must be "prepare_job".
- **responseFile** (string) - Required - The absolute path to the file where the command's response will be written upon completion.
- **state** (object) - Required - An arbitrary object for storing state information. Typically empty for this command.
- **args** (object) - Required - Arguments containing the detailed configuration for job and service containers.
  - **jobContainer** (object) - Required - Configuration for the primary job container.
    - **image** (string) - Required - The Docker image to use for the job container (e.g., "node:18").
    - **workingDirectory** (string) - Required - The working directory inside the job container.
    - **createOptions** (string) - Optional - Additional Docker `create` options (e.g., "--cpus 1").
    - **environmentVariables** (object) - Optional - Key-value pairs of environment variables to set in the job container.
    - **userMountVolumes** (array of objects) - Optional - An array of custom volume mounts defined by the user.
      - **sourceVolumePath** (string) - Required - The path on the host or named volume to mount.
      - **targetVolumePath** (string) - Required - The path inside the container where the volume will be mounted.
      - **readOnly** (boolean) - Required - Specifies if the mounted volume should be read-only.
    - **systemMountVolumes** (array of objects) - Optional - An array of system-defined volume mounts for runner internals. Each object has `sourceVolumePath`, `targetVolumePath`, and `readOnly` properties.
    - **registry** (object) - Optional - Docker registry authentication details for pulling the job container image.
      - **username** (string) - Required - Username for the Docker registry.
      - **password** (string) - Required - Password for the Docker registry.
      - **serverUrl** (string) - Required - URL of the Docker registry (e.g., "https://index.docker.io/v1").
    - **portMappings** (object) - Optional - Key-value pairs mapping container ports to host ports (e.g., `{"80": "801"}`).
  - **services** (array of objects) - Optional - An array of configurations for service containers that the job depends on.
    - **contextName** (string) - Required - A unique name for the service container.
    - **image** (string) - Required - The Docker image to use for the service container (e.g., "redis").
    - **createOptions** (string) - Optional - Additional Docker `create` options for the service container.
    - **environmentVariables** (object) - Optional - Key-value pairs of environment variables for the service container.
    - **userMountVolumes** (array of objects) - Optional - An array of custom volume mounts for the service container (same structure as `jobContainer.userMountVolumes`).
    - **portMappings** (object) - Optional - Key-value pairs mapping container ports to host ports for the service container.
    - **registry** (object) - Optional - Docker registry authentication details for pulling the service container image (same structure as `jobContainer.registry`).

### Request Example
```json
{
  "command": "prepare_job",
  "responseFile": "/users/octocat/runner/_work/{guid}.json",
  "state": {},
  "args": {
    "jobContainer": {
      "image": "node:18",
      "workingDirectory": "/__w/octocat-test2/octocat-test2",
      "createOptions": "--cpus 1",
      "environmentVariables": {
        "NODE_ENV": "development"
      },
      "userMountVolumes": [
        {
          "sourceVolumePath": "my_docker_volume",
          "targetVolumePath": "/volume_mount",
          "readOnly": false
        }
      ],
      "systemMountVolumes": [
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work",
          "targetVolumePath": "/__w",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/externals",
          "targetVolumePath": "/__e",
          "readOnly": true
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp",
          "targetVolumePath": "/__w/_temp",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_actions",
          "targetVolumePath": "/__w/_actions",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_tool",
          "targetVolumePath": "/__w/_tool",
          "readOnly": false
        },
        {
          "sourceVolumePath": "/home
```

--------------------------------

### Example GitHub Actions OIDC Token Structure

Source: https://docs.github.com/en/actions/concepts/security/openid-connect

This JSON example illustrates the decoded header and payload of a JSON Web Token (JWT) issued by GitHub's OIDC provider. The first object represents the token's header, containing metadata like type and algorithm. The second object is the token's payload, which includes various claims such as the subject (`sub`) identifying the workflow and repository, along with other contextual information used by the cloud provider for validation.

```json
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "example-thumbprint",
  "kid": "example-key-id"
}
{
  "jti": "example-id",
  "sub": "repo:octo-org/octo-repo:environment:prod",
  "environment": "prod",
  "aud": "https://github.com/octo-org",
  "ref": "refs/heads/main",
  "sha": "example-sha",
  "repository": "octo-org/octo-repo",
  "repository_owner": "octo-org",
  "actor_id": "12",
  "repository_visibility": "private",
  "repository_id": "74",
  "repository_owner_id": "65",
  "run_id": "example-run-id",
  "run_number": "10",
  "run_attempt": "2",
  "runner_environment": "github-hosted",
  "actor": "octocat",
  "workflow": "example-workflow",
  "head_ref": "",
  "base_ref": "",
  "event_name": "workflow_dispatch",
  "ref_type": "branch",
  "job_workflow_ref": "octo-org/octo-automation/.github/workflows/oidc.yml@refs/heads/main",
  "iss": "https://token.actions.githubusercontent.com",
  "nbf": 1632492967,
  "exp": 1632493867,
  "iat": 1632493567
}
```

--------------------------------

### GitHub Actions Python Release Build Job

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/oidc-in-pypi

Defines a job that checks out code, sets up Python 3.x environment, installs the build package, and creates distribution artifacts. The job runs on ubuntu-latest and outputs distributions to the dist/ directory for downstream consumption.

```yaml
jobs:
  release-build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5

      - uses: actions/setup-python@v5
        with:
          python-version: "3.x"

      - name: build release distributions
        run: |
          # NOTE: put your own distribution build steps here.
          python -m pip install build
          python -m build

      - name: upload windows dists
        uses: actions/upload-artifact@v4
        with:
          name: release-dists
          path: dist/
```

--------------------------------

### Define Basic Jobs in GitLab CI/CD and GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-gitlab-cicd

These examples demonstrate how to define a basic job in both GitLab CI/CD and GitHub Actions. GitLab CI/CD uses the `script` key for commands, while GitHub Actions uses the `run` key within `steps`. Both systems allow defining variables and executing shell commands within a job.

```yaml
job1:
  variables:
    GIT_CHECKOUT: "true"
  script:
    - echo "Run your script here"
```

```yaml
jobs:
  job1:
    steps:
      - uses: actions/checkout@v5
      - run: echo "Run your script here"
```

--------------------------------

### Assign Single Label to Self-Hosted Runner Configuration

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/apply-labels

Assigns a single label named 'gpu' to a self-hosted runner during initial configuration using the config script. The label is created automatically if it does not already exist. This approach only works during runner setup, not for existing runners.

```bash
./config.sh --url <REPOSITORY_URL> --token <REGISTRATION_TOKEN> --labels gpu
```

--------------------------------

### Multi-Dimensional Matrix Configuration

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

Create a multi-dimensional matrix by specifying multiple variables. A job will run for each possible combination of the variables. This example demonstrates a matrix with two operating systems and three Node.js versions, resulting in six total job runs.

```APIDOC
## Matrix Strategy Configuration

### Description
Define a multi-dimensional matrix to run jobs across multiple variable combinations in GitHub Actions workflows.

### Configuration Structure
```yaml
jobs:
  example_matrix:
    strategy:
      matrix:
        os: [ubuntu-22.04, ubuntu-24.04]
        version: [10, 12, 14]
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.version }}
```

### Parameters
#### Matrix Variables
- **os** (array) - Operating systems to test against
- **version** (array) - Node.js versions to test against

### Context Variables
- **matrix.os** (string) - Current operating system value from matrix
- **matrix.version** (string) - Current version value from matrix

### Behavior
With 2 OS values and 3 version values, the workflow generates 6 jobs (2 × 3 combinations). Each job receives the corresponding matrix values through context variables.

### Matrix with Object Arrays
```yaml
matrix:
  os:
    - ubuntu-latest
    - macos-latest
  node:
    - version: 14
    - version: 20
      env: NODE_OPTIONS=--openssl-legacy-provider
```

This configuration produces 4 jobs with the following combinations:
- matrix.os: ubuntu-latest, matrix.node.version: 14
- matrix.os: ubuntu-latest, matrix.node.version: 20, matrix.node.env: NODE_OPTIONS=--openssl-legacy-provider
- matrix.os: macos-latest, matrix.node.version: 14
- matrix.os: macos-latest, matrix.node.version: 20, matrix.node.env: NODE_OPTIONS=--openssl-legacy-provider
```

--------------------------------

### Set up specific Swift version in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/swift

Configures a GitHub Actions workflow step to use a specific Swift version (5.3.3) using the swift-actions/setup-swift action. This action retrieves the specified Swift version from the runner's tools cache and adds necessary binaries to PATH for the remainder of the job.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
steps:
  - uses: swift-actions/setup-swift@65540b95f51493d65f5e59e97dcef9629ddf11bf
    with:
      swift-version: "5.3.3"
  - name: Get swift version
    run: swift --version # Swift 5.3.3
```

--------------------------------

### Select self-hosted runners using labels in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/choose-the-runner-for-a-job

This example shows how to configure a job to run on a self-hosted runner by providing an array of labels to the `runs-on` keyword. The job will execute on any self-hosted runner that possesses both the `self-hosted` and `linux` labels, allowing for custom environments.

```yaml
runs-on: [self-hosted, linux]

```

--------------------------------

### Configure Dockerfile Path for GitHub Actions Container Step Input (JSON)

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/customize-containers

This JSON snippet demonstrates the input structure for a GitHub Actions `run_container_step` command. It shows how to specify the path to a Dockerfile using the `"dockerfile"` parameter within the `"args"` object, along with other container configuration options like environment variables, entry points, and volume mounts.

```json
{
  "command": "run_container_step",
  "responseFile": null,
  "state": {
    "network": "example_network_53269bd575972817b43f7733536b200c",
    "jobContainer": "82e8219701fe096a35941d869cf3d71af1d943b5d8bdd71af1d943b5d8bdd718857fb87ac3042480",
    "services": {
      "redis": "60972d9aa486605e66b0dad4abb678dc3d9116f536579e418176eedb8abb9105"
    }
  },
  "args": {
    "image": null,
    "dockerfile": "/__w/_actions/foo/dockerfile",
    "entryPointArgs": ["hello world"],
    "entryPoint": "echo",
    "workingDirectory": "/__w/octocat-test2/octocat-test2",
    "createOptions": "--cpus 1",
    "environmentVariables": {
      "NODE_ENV": "development"
    },
    "prependPath": ["/foo/bar", "bar/foo"],
    "userMountVolumes": [
      {
        "sourceVolumePath": "my_docker_volume",
        "targetVolumePath": "/volume_mount",
        "readOnly": false
      }
    ],
    "systemMountVolumes": [
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work",
        "targetVolumePath": "/__w",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/externals",
        "targetVolumePath": "/__e",
        "readOnly": true
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp",
        "targetVolumePath": "/__w/_temp",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_actions",
        "targetVolumePath": "/__w/_actions",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_tool",
        "targetVolumePath": "/__w/_tool",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_home",
        "targetVolumePath": "/github/home",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_workflow",
        "targetVolumePath": "/github/workflow",
        "readOnly": false
      }
    ],
    "registry": null,
    "portMappings": { "80": "801" }
  }
}
```

--------------------------------

### Install GitHub TrustRoot and ClusterImagePolicy with Helm

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/enforce-artifact-attestations

This Helm command installs the GitHub `TrustRoot` and a `ClusterImagePolicy` into the Kubernetes cluster, leveraging the `artifact-attestations` namespace. It configures the policy to reject artifacts not originating from the specified GitHub organization (`MY-ORGANIZATION`), which must be replaced with the actual organization name. This step establishes the foundational trust for artifact attestation enforcement.

```Bash
helm upgrade trust-policies --install --atomic \
 --namespace artifact-attestations \
 oci://ghcr.io/github/artifact-attestations-helm-charts/trust-policies \
 --version v0.7.0 \
 --set policy.enabled=true \
 --set policy.organization=MY-ORGANIZATION
```

--------------------------------

### runs.entrypoint Configuration

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Override or set the Docker ENTRYPOINT instruction. Use this when the Dockerfile does not specify an ENTRYPOINT or when you need to override the existing one. Supports both shell and exec forms.

```APIDOC
## runs.entrypoint

### Description
Optional property that overrides the Docker `ENTRYPOINT` in the `Dockerfile`, or sets it if one wasn't already specified.

### Property
`runs.entrypoint`

### Type
String (command path or shell command)

### Required
No (Optional)

### Default Behavior
If omitted, the commands specified in the Docker `ENTRYPOINT` instruction will execute.

### Use Cases
- When the `Dockerfile` does not specify an `ENTRYPOINT`
- When you want to override the existing `ENTRYPOINT` instruction
- To specify a different command to execute when the container starts

### Supported Forms
- **Shell form**: `"sh -c"`
- **Exec form**: `["executable", "param1", "param2"]` (recommended)

### Configuration Example
```yaml
runs:
  using: 'docker'
  image: 'Dockerfile'
  entrypoint: 'main.sh'
```

### Notes
- Docker documentation recommends using the exec form of the ENTRYPOINT instruction
- For more information, see Dockerfile support for GitHub Actions
```

--------------------------------

### Complete Node.js CI workflow with single version in GitHub Actions

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

A complete GitHub Actions workflow that builds and tests a Node.js project using a single Node.js version (20.x). Includes checkout, setup-node action, dependency installation with npm ci, optional build step, and test execution. Triggers on push events to the repository.

```yaml
name: Node.js CI

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5
      - name: Use Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20.x'
      - run: npm ci
      - run: npm run build --if-present
      - run: npm test
```

--------------------------------

### GitHub Actions Demo Workflow Configuration

Source: https://docs.github.com/en/actions/get-started/quickstart

A basic GitHub Actions workflow file that demonstrates core workflow concepts including triggers, jobs, steps, and context variables. This workflow runs on push events and executes multiple echo commands on an Ubuntu runner, including repository checkout and file listing. It serves as a foundational template for understanding GitHub Actions syntax and execution flow.

```yaml
name: GitHub Actions Demo
run-name: ${{ github.actor }} is testing out GitHub Actions 🚀
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v5
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```

--------------------------------

### Configure JavaScript Action with Node.js v24 Runtime

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This snippet illustrates how to configure a GitHub JavaScript Action to run using the Node.js v24 runtime. It specifies `using: 'node24'` to select the runtime and `main: 'main.js'` to indicate the entry point file for the action's code. This setup is essential for executing JavaScript-based actions.

```yaml
runs:
  using: 'node24'
  main: 'main.js'
```

--------------------------------

### Docker ENTRYPOINT exec form without variable substitution

Source: https://docs.github.com/en/actions/creating-actions/dockerfile-support-for-github-actions

Example of exec form ENTRYPOINT that does not perform environment variable substitution. In this form, $GITHUB_SHA will be printed literally as a string rather than being expanded to its actual value.

```dockerfile
ENTRYPOINT ["echo $GITHUB_SHA"]
```

--------------------------------

### Define and Access GitHub Actions Job Services

Source: https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

This example illustrates how to define service containers (like Nginx and Redis) for a job in GitHub Actions, including port mapping. It also demonstrates how to access these services from within the job, referencing dynamically assigned host ports using the `${{ job.services.<service_name>.ports['<container_port>'] }}` context.

```yaml
services:
  nginx:
    image: nginx
    # Map port 8080 on the Docker host to port 80 on the nginx container
    ports:
      - 8080:80
  redis:
    image: redis
    # Map random free TCP port on Docker host to port 6379 on redis container
    ports:
      - 6379/tcp
steps:
  - run: |
      echo "Redis available on 127.0.0.1:${{ job.services.redis.ports['6379'] }}"
      echo "Nginx available on 127.0.0.1:${{ job.services.nginx.ports['80'] }}"
```

--------------------------------

### GitHub Actions `with` Keyword for Action Inputs

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This snippet demonstrates how to pass input parameters to an action using the `with` keyword within a composite step. It shows a map of key-value pairs, such as `first_name`, `middle_name`, and `last_name`, which are consumed by the `actions/hello_world` action.

```yaml
runs:
  using: "composite"
  steps:
    - name: My first step
      uses: actions/hello_world@main
      with:
        first_name: Mona
        middle_name: The
        last_name: Octocat
```

--------------------------------

### Bash Script for Rootless DIND Environment Setup in Kubernetes Init Container

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

This bash script is executed by an init container within a Kubernetes pod to prepare a rootless Docker-in-Docker environment. It copies essential system configuration files, creates user and group entries for the `runner` user, and sets up subUID/subGID mappings. Finally, it adjusts file permissions and ownership for the DIND-related directories to ensure proper isolation and functionality.

```bash
set -x
cp -a /etc/. /dind-etc/
echo 'runner:x:1001:1001:runner:/home/runner:/bin/ash' >> /dind-etc/passwd
echo 'runner:x:1001:' >> /dind-etc/group
echo 'runner:100000:65536' >> /dind-etc/subgid
echo 'runner:100000:65536' >> /dind-etc/subuid
chmod 755 /dind-etc;
chmod u=rwx,g=rx+s,o=rx /dind-home
chown 1001:1001 /dind-home
```

--------------------------------

### runs.post-entrypoint Configuration

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Configure a cleanup script that runs after the main entrypoint action completes. Runs in a separate container with the same base image, allowing for post-action cleanup and resource management.

```APIDOC
## runs.post-entrypoint

### Description
Optional property that allows you to run a cleanup script once the `runs.entrypoint` action has completed. GitHub Actions uses `docker run` to launch this action in a new container with the same base image.

### Property
`runs.post-entrypoint`

### Type
String (path to script file)

### Required
No (Optional)

### Default Behavior
The `post-entrypoint` action always runs by default but can be overridden using `runs.post-if`.

### Runtime State
The runtime state is different from the main `entrypoint` container. Required state must be accessed via:
- Workspace directory
- `HOME` environment variable
- `STATE_` prefixed variables

### Configuration Example
```yaml
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - 'bzz'
  entrypoint: 'main.sh'
  post-entrypoint: 'cleanup.sh'
```

### Common Use Cases
- Cleanup temporary files
- Release resources
- Logging and reporting
- Reverting changes made during execution
```

--------------------------------

### Example Output of GitHub Actions Importer Migrate Command

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/gitlab-migration

This snippet illustrates the successful output generated after running the `gh actions-importer migrate` command. It provides the path to the detailed log file and the URL of the newly created pull request on GitHub, confirming the migration.

```bash
$ gh actions-importer migrate gitlab --target-url https://github.com/octo-org/octo-repo --output-dir tmp/migrate --namespace octo-org --project monas-project
[2022-08-20 22:08:20] Logs: 'tmp/migrate/log/actions-importer-20220916-014033.log'
[2022-08-20 22:08:20] Pull request: 'https://github.com/octo-org/octo-repo/pull/1'
```

--------------------------------

### Create and test Redis client with Node.js

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-redis-service-containers

Creates a Redis client instance using the redis npm module, connects to a Redis server using environment variables for host and port configuration, and performs basic operations including setting keys, adding hash fields, and retrieving data. The script demonstrates error handling and proper connection cleanup with the quit() method.

```javascript
const redis = require("redis");

// Creates a new Redis client
// If REDIS_HOST is not set, the default host is localhost
// If REDIS_PORT is not set, the default port is 6379
const redisClient = redis.createClient({
  url: `redis://${process.env.REDIS_HOST}:${process.env.REDIS_PORT}`
});

redisClient.on("error", (err) => console.log("Error", err));

(async () => {
  await redisClient.connect();

  // Sets the key "octocat" to a value of "Mona the octocat"
  const setKeyReply = await redisClient.set("octocat", "Mona the Octocat");
  console.log("Reply: " + setKeyReply);
  // Sets a key to "species", field to "octocat", and "value" to "Cat and Octopus"
  const SetFieldOctocatReply = await redisClient.hSet("species", "octocat", "Cat and Octopus");
  console.log("Reply: " + SetFieldOctocatReply);
  // Sets a key to "species", field to "dinotocat", and "value" to "Dinosaur and Octopus"
  const SetFieldDinotocatReply = await redisClient.hSet("species", "dinotocat", "Dinosaur and Octopus");
  console.log("Reply: " + SetFieldDinotocatReply);
  // Sets a key to "species", field to "robotocat", and "value" to "Cat and Robot"
  const SetFieldRobotocatReply = await redisClient.hSet("species", "robotocat", "Cat and Robot");
  console.log("Reply: " + SetFieldRobotocatReply);

  try {
    // Gets all fields in "species" key
    const replies = await redisClient.hKeys("species");
    console.log(replies.length + " replies:");
    replies.forEach((reply, i) => {
        console.log("    " + i + ": " + reply);
    });
    await redisClient.quit();
  }
  catch (err) {
    // statements to handle any exceptions
  }
})();
```

--------------------------------

### jobs.<job_id>.steps

Source: https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions

Defines a sequence of tasks (steps) to be executed within a job. Each step runs in its own process and can execute commands, setup tasks, or actions.

```APIDOC
## CONFIGURATION jobs.<job_id>.steps

### Description
A job contains a sequence of tasks called `steps`. Steps can run commands, run setup tasks, or run an action. Each step runs in its own process in the runner environment and has access to the workspace and filesystem. Changes to environment variables are not preserved between steps.

### Method
CONFIGURATION

### Endpoint
jobs.<job_id>.steps

### Parameters
#### Request Body
- **steps** (array of objects) - Required - A list of individual steps to be executed in order. Each object in the array represents a single step.

### Request Example
```yaml
name: Greeting from Mona

on: push

jobs:
  my-job:
    name: My Job
    runs-on: ubuntu-latest
    steps:
      - name: Print a greeting
        env:
          MY_VAR: Hi there! My name is
          FIRST_NAME: Mona
          MIDDLE_NAME: The
          LAST_NAME: Octocat
        run: |
          echo $MY_VAR $FIRST_NAME $MIDDLE_NAME $LAST_NAME.
```

### Response
N/A (Configuration setting, no direct response)
```

--------------------------------

### Configure Docker Container Step with Dockerfile in GitHub Actions

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

Demonstrates how to specify a Dockerfile path and configure container execution parameters including entry points, working directory, environment variables, volume mounts, and port mappings. This configuration is used by GitHub Actions runners to execute container-based steps with custom Docker images.

```json
{
  "command": "run_container_step",
  "responseFile": null,
  "state": {
    "network": "example_network_53269bd575972817b43f7733536b200c",
    "jobContainer": "82e8219701fe096a35941d869cf3d71af1d943b5d8bdd718857fb87ac3042480",
    "services": {
      "redis": "60972d9aa486605e66b0dad4abb678dc3d9116f536579e418176eedb8abb9105"
    }
  },
  "args": {
    "image": null,
    "dockerfile": "/__w/_actions/foo/dockerfile",
    "entryPointArgs": ["hello world"],
    "entryPoint": "echo",
    "workingDirectory": "/__w/octocat-test2/octocat-test2",
    "createOptions": "--cpus 1",
    "environmentVariables": {
      "NODE_ENV": "development"
    },
    "prependPath": ["/foo/bar", "bar/foo"],
    "userMountVolumes": [
      {
        "sourceVolumePath": "my_docker_volume",
        "targetVolumePath": "/volume_mount",
        "readOnly": false
      }
    ],
    "systemMountVolumes": [
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work",
        "targetVolumePath": "/__w",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/externals",
        "targetVolumePath": "/__e",
        "readOnly": true
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp",
        "targetVolumePath": "/__w/_temp",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_actions",
        "targetVolumePath": "/__w/_actions",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_tool",
        "targetVolumePath": "/__w/_tool",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_home",
        "targetVolumePath": "/github/home",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_workflow",
        "targetVolumePath": "/github/workflow",
        "readOnly": false
      }
    ],
    "registry": null,
    "portMappings": { "80": "801" }
  }
}
```

--------------------------------

### Shell script entrypoint for GitHub Actions

Source: https://docs.github.com/en/actions/creating-actions/dockerfile-support-for-github-actions

Example entrypoint.sh shell script that processes arguments passed from the action's metadata file. The script uses POSIX-compliant shell syntax with the shebang directive and demonstrates how to handle and display command-line arguments using shell parameter expansion.

```shell
#!/bin/sh

# `$#` expands to the number of arguments and `$@` expands to the supplied `args`
printf '%d args:' "$#"
printf " '%s'" "$@"
printf '\n'
```

--------------------------------

### Define GitHub Actions Job Steps for Containerized Workflow in YAML

Source: https://docs.github.com/en/actions/using-containerized-services/creating-postgresql-service-containers

This YAML snippet outlines the steps for a GitHub Actions job running in a container. It includes checking out the repository, installing Node.js dependencies using `npm ci`, and executing a `node client.js` script. Environment variables `POSTGRES_HOST` and `POSTGRES_PORT` are set to enable the script to connect to the `postgres` service container.

```yaml
steps:
  # Downloads a copy of the code in your repository before running CI tests
  - name: Check out repository code
    uses: actions/checkout@v5

  # Performs a clean installation of all dependencies in the `package.json` file
  # For more information, see https://docs.npmjs.com/cli/ci.html
  - name: Install dependencies
    run: npm ci

  - name: Connect to PostgreSQL
    # Runs a script that creates a PostgreSQL table, populates
    # the table with data, and then retrieves the data.
    run: node client.js
    # Environment variable used by the `client.js` script to create
    # a new PostgreSQL client.
    env:
      # The hostname used to communicate with the PostgreSQL service container
      POSTGRES_HOST: postgres
      # The default PostgreSQL port
      POSTGRES_PORT: 5432

```

--------------------------------

### Store build metadata in GitHub Actions environment

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Example of storing build-related metadata such as timestamps, commit SHAs, or artifact names in environment variables using GITHUB_ENV. This demonstrates storing a build timestamp and using it in a subsequent deployment step.

```yaml
steps:
  - name: Store build timestamp
    run: echo "BUILD_TIME=$(date +'%T')" >> $GITHUB_ENV

  - name: Deploy using stored timestamp
    run: echo "Deploying at $BUILD_TIME"
```

--------------------------------

### Set and Retrieve Output Parameters in GitHub Actions

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

This example demonstrates how to set an output parameter named `SELECTED_COLOR` from one step and then retrieve its value in a subsequent step within a GitHub Actions workflow. It shows both Bash-like and PowerShell-like approaches for writing to `$GITHUB_OUTPUT` to make the parameter available.

```YAML
      - name: Set color
        id: color-selector
        run: echo "SELECTED_COLOR=green" >> "$GITHUB_OUTPUT"
      - name: Get color
        env:
          SELECTED_COLOR: ${{ steps.color-selector.outputs.SELECTED_COLOR }}
        run: echo "The selected color is $SELECTED_COLOR"
```

```YAML
      - name: Set color
        id: color-selector
        run: |
            "SELECTED_COLOR=green" >> $env:GITHUB_OUTPUT
      - name: Get color
        env:
          SELECTED_COLOR: ${{ steps.color-selector.outputs.SELECTED_COLOR }}
        run: Write-Output "The selected color is $env:SELECTED_COLOR"
```

--------------------------------

### Resolved Restore Keys Example in GitHub Actions

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching

Shows the actual resolved restore keys after expression evaluation. The hash `d5ea0750` is computed from the package-lock.json file, and the keys are searched in order of specificity from most to least specific.

```yaml
restore-keys: |
  npm-feature-d5ea0750
  npm-feature-
  npm-
```

--------------------------------

### Create Kubernetes Secret for GitHub App Authentication

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

Creates a Kubernetes secret containing GitHub App credentials (app ID, installation ID, and private key) for authenticating ARC with the GitHub API. The secret must be created in the same namespace where the gha-runner-scale-set chart is installed. This is the recommended approach for managing sensitive authentication data.

```bash
kubectl create secret generic pre-defined-secret \
  --namespace=arc-runners \
  --from-literal=github_app_id=123456 \
  --from-literal=github_app_installation_id=654321 \
  --from-file=github_app_private_key=private-key.pem
```

--------------------------------

### steps Context Structure Reference

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

Provides a JSON example showing the structure of the `steps` context containing information about completed steps with their outputs, outcomes, and conclusions. This demonstrates how step data is organized when accessed in workflow expressions.

```json
{
  "checkout": {
    "outputs": {},
    "outcome": "success",
    "conclusion": "success"
  },
  "generate_number": {
    "outputs": {
      "random_number": "1"
    },
    "outcome": "success",
    "conclusion": "success"
  }
}
```

--------------------------------

### GitHub Actions `uses` Keyword for Referencing Actions

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This example showcases various ways to use the `uses` keyword to reference actions within a composite step. It demonstrates referencing actions by commit SHA, major version, specific version, branch, subdirectory, local path, and Docker registry images, emphasizing versioning best practices.

```yaml
runs:
  using: "composite"
  steps:
    # Reference a specific commit
    - uses: actions/checkout@8f4b7f84864484a7bf31766abe9204da3cbe65b3
    # Reference the major version of a release
    - uses: actions/checkout@v5
    # Reference a specific version
    - uses: actions/checkout@v5.2.0
    # Reference a branch
    - uses: actions/checkout@main
    # References a subdirectory in a public GitHub repository at a specific branch, ref, or SHA
    - uses: actions/aws/ec2@main
    # References a local action
    - uses: ./.github/actions/my-action
    # References a docker public registry action
    - uses: docker://gcr.io/cloud-builders/gradle
    # Reference a docker image published on docker hub
    - uses: docker://alpine:3.8
```

--------------------------------

### Append to job summary content in GitHub Actions (PowerShell)

Source: https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions

This example, found under the 'Overwriting job summaries' section, demonstrates how to append new Markdown content to the `GITHUB_STEP_SUMMARY` environment file using PowerShell commands within a GitHub Actions workflow. Note that this specific code example appends rather than overwrites, despite the section's title, by using the `>>` operator.

```powershell
- name: Overwrite Markdown
  run: |
    "Adding some Markdown content" >> $env:GITHUB_STEP_SUMMARY
    "There was an error, we need to clear the previous Markdown with some new content." >> $env:GITHUB_STEP_SUMMARY
```

--------------------------------

### Repository Checkout Action

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

GitHub Actions step using 'actions/checkout@v5' to check out the repository code onto the runner. This action is essential when workflows need to access, build, test, or perform other operations on the repository's source code.

```yaml
- uses: actions/checkout@v5
```

--------------------------------

### runs.steps[*].with

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Provides input parameters to the action specified by `uses`.

```APIDOC
## Configuration Property runs.steps[*].with

### Description
A `map` of the input parameters defined by the action. Each input parameter is a key/value pair.

### Method
Configuration Property

### Endpoint
runs.steps[*].with

### Parameters
#### Request Body
- **with** (object) - Optional - A map of input parameters for the action.
  - **KEY** (string) - Required - The name of the input parameter.
  - **VALUE** (string) - Required - The value of the input parameter.

### Request Example
{
  "with": {
    "first_name": "Mona",
    "middle_name": "The",
    "last_name": "Octocat"
  }
}
```

--------------------------------

### Overwrite GitHub Actions Job Summary Content

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

This example demonstrates how to overwrite existing content in a GitHub Actions job summary using Bash's `>` operator to replace the summary's content. The PowerShell example provided shows appending new content, which might not achieve a full overwrite as described in the surrounding text.

```YAML
- name: Overwrite Markdown
  run: |
    echo "Adding some Markdown content" >> $GITHUB_STEP_SUMMARY
    echo "There was an error, we need to clear the previous Markdown with some new content." > $GITHUB_STEP_STEP_SUMMARY
```

```YAML
- name: Overwrite Markdown
  run: |
    "Adding some Markdown content" >> $env:GITHUB_STEP_SUMMARY
    "There was an error, we need to clear the previous Markdown with some new content." >> $env:GITHUB_STEP_SUMMARY
```

--------------------------------

### Docker ENTRYPOINT exec form with environment variable substitution

Source: https://docs.github.com/en/actions/creating-actions/dockerfile-support-for-github-actions

Example of using the exec form of ENTRYPOINT with a shell to enable environment variable substitution. This approach executes a shell directly to properly expand variables like $GITHUB_SHA, which would otherwise be printed literally in the exec form without shell interpretation.

```dockerfile
ENTRYPOINT ["sh", "-c", "echo $GITHUB_SHA"]
```

--------------------------------

### Defining Multiple Matrices with Job Outputs in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/run-job-variations

This example illustrates how to dynamically define matrices for multiple jobs using the output from a preceding job in GitHub Actions. It shows a workflow where one job defines a list of colors, which are then used by subsequent jobs to produce and consume artifacts, with each artifact associated with a matrix value.

```yaml
name: shared matrix
on:
  push:
  workflow_dispatch:

jobs:
  define-matrix:
    runs-on: ubuntu-latest

    outputs:
      colors: ${{ steps.colors.outputs.colors }}

    steps:
      - name: Define Colors
        id: colors
        run: |
          echo 'colors=["red", "green", "blue"]' >> "$GITHUB_OUTPUT"

  produce-artifacts:
    runs-on: ubuntu-latest
    needs: define-matrix
    strategy:
      matrix:
        color: ${{ fromJSON(needs.define-matrix.outputs.colors) }}

    steps:
      - name: Define Color
        env:
          color: ${{ matrix.color }}
        run: |
          echo "$color" > color
      - name: Produce Artifact
        uses: actions/upload-artifact@v4
        with:
          name: ${{ matrix.color }}
          path: color

  consume-artifacts:
    runs-on: ubuntu-latest
    needs:
    - define-matrix
    - produce-artifacts
    strategy:
      matrix:
        color: ${{ fromJSON(needs.define-matrix.outputs.colors) }}

    steps:
    - name: Retrieve Artifact
      uses: actions/download-artifact@v5
      with:
        name: ${{ matrix.color }}

    - name: Report Color
      run: |
        cat color
```

--------------------------------

### Workflow trigger configuration with on field

Source: https://docs.github.com/en/actions/how-tos/troubleshoot-workflows

YAML configuration example showing the `on:` field structure for defining workflow triggers. This field specifies which events should trigger the workflow execution and is essential for understanding and troubleshooting unexpected workflow behavior.

```yaml
on:
  push:
  pull_request:
  schedule:
    - cron: '0 0 * * *'
  issues:
```

--------------------------------

### GET /repos/{owner}/{repo}/actions/runs/{run_id}/approvals

Source: https://docs.github.com/en/actions/how-tos/deploy/configure-and-manage-deployments/create-custom-protection-rules

Retrieve the approval status for a workflow run. Use this endpoint to check the current state of deployment protection rule approvals.

```APIDOC
## GET /repos/{owner}/{repo}/actions/runs/{run_id}/approvals

### Description
Retrieve the approval status and details for a specific workflow run. This endpoint allows you to query the current state of deployment protection rule evaluations.

### Method
GET

### Endpoint
/repos/{owner}/{repo}/actions/runs/{run_id}/approvals

### Parameters
#### Path Parameters
- **owner** (string) - Required - The account owner of the repository
- **repo** (string) - Required - The name of the repository
- **run_id** (integer) - Required - The unique identifier of the workflow run

### Response
#### Success Response (200)
- **approvals** (array) - Array of approval objects
  - **environment** (string) - The environment name
  - **state** (string) - The approval state ("approved", "rejected", or "pending")
  - **comment** (string) - Any comment or status report provided
  - **reviewer** (object) - Information about the reviewer (if applicable)

#### Response Example
```
{
  "approvals": [
    {
      "environment": "production",
      "state": "approved",
      "comment": "Deployment approved by security review",
      "reviewer": {
        "login": "security-bot",
        "id": 12345
      }
    }
  ]
}
```
```

--------------------------------

### Define GitHub Actions Job Steps for Containerized Workflow in YAML

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers

This YAML snippet illustrates the steps within a GitHub Actions job that runs in a containerized environment. It includes common actions like checking out the repository code and installing Node.js dependencies. Crucially, it shows how to run a Node.js script (`client.js`) that connects to the PostgreSQL service container by setting `POSTGRES_HOST` and `POSTGRES_PORT` environment variables, making the service accessible to the job's steps.

```YAML
steps:
  # Downloads a copy of the code in your repository before running CI tests
  - name: Check out repository code
    uses: actions/checkout@v5

  # Performs a clean installation of all dependencies in the `package.json` file
  # For more information, see https://docs.npmjs.com/cli/ci.html
  - name: Install dependencies
    run: npm ci

  - name: Connect to PostgreSQL
    # Runs a script that creates a PostgreSQL table, populates
    # the table with data, and then retrieves the data.
    run: node client.js
    # Environment variable used by the `client.js` script to create
    # a new PostgreSQL client.
    env:
      # The hostname used to communicate with the PostgreSQL service container
      POSTGRES_HOST: postgres
      # The default PostgreSQL port
      POSTGRES_PORT: 5432
```

--------------------------------

### Define Azure Pipelines Template Path with Variables

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/azure-devops-migration

This example demonstrates how to use a variable to define a template file path in Azure Pipelines. The `azure-pipelines.yml` file references a template path that includes a variable, which is defined in a separate `vars.yml` file, allowing for dynamic template inclusion.

```yaml
# File: azure-pipelines.yml
variables:
- template: 'templates/vars.yml'

steps:
- template: "./templates/$"
```

```yaml
# File: templates/vars.yml
variables:
  one: 'simple_step.yml'
```

--------------------------------

### Matrix Context Usage

Source: https://docs.github.com/en/actions/reference/accessing-contextual-information-about-workflow-runs

The matrix context allows you to create multiple job configurations using different combinations of variables. This example demonstrates how to use matrix.os and matrix.node properties to run jobs across different operating systems and Node.js versions.

```APIDOC
## Matrix Context

### Description
The `matrix` context contains properties that allow you to create multiple job configurations by combining different variable values. Each combination creates a separate job run.

### Context Properties
- **matrix.os** (string) - Operating system from the matrix configuration
- **matrix.node** (string) - Node.js version from the matrix configuration
- **matrix.<key>** (string) - Any custom key defined in the strategy.matrix section

### Usage Example
```yaml
name: Test matrix
on: push

jobs:
  build:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest]
        node: [14, 16]
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}
      - name: Output node version
        run: node --version
```

### Matrix Expansion
This configuration creates 4 jobs (2 OS × 2 Node versions):
- ubuntu-latest with Node 14
- ubuntu-latest with Node 16
- windows-latest with Node 14
- windows-latest with Node 16
```

--------------------------------

### Define a GitHub Actions Workflow using a Private Action (YAML)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

This YAML workflow demonstrates how to set up a GitHub Action that triggers on pushes to the 'main' branch. It checks out the repository, executes a private action located in the root directory ('./'), passes an input ('who-to-greet'), and then retrieves and prints an output ('time') from that action. This setup is ideal for testing or using actions developed within the same repository.

```yaml
on:
  push:
    branches:
      - main

jobs:
  hello_world_job:
    name: A job to say hello
    runs-on: ubuntu-latest

    steps:
      # To use this repository's private action,
      # you must check out the repository
      - name: Checkout
        uses: actions/checkout@v5

      - name: Hello world action step
        uses: ./ # Uses an action in the root directory
        id: hello
        with:
          who-to-greet: Mona the Octocat

      # Use the output from the `hello` step
      - name: Get the output time
        run: echo "The time was ${{ steps.hello.outputs.time }}"
```

--------------------------------

### Define action inputs and outputs in action.yml

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/find-and-customize-actions

Shows the structure of an action.yml configuration file that defines inputs and outputs for a custom GitHub Action. The inputs section specifies required parameters with descriptions and default values, while the outputs section defines return values that subsequent steps can reference. This example defines a required file-path input and a results-file output.

```yaml
name: "Example"
description: "Receives file and generates output"
inputs:
  file-path: # id of input
    description: "Path to test script"
    required: true
    default: "test-file.js"
outputs:
  results-file: # id of output
    description: "Path to results file"
```

--------------------------------

### Matrix with Object Configuration

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

Defines matrix variables as arrays of objects to create complex combinations with additional properties. This example produces 4 jobs combining os and node configurations, where the node variable includes both version and optional environment variables.

```yaml
matrix:
  os:
    - ubuntu-latest
    - macos-latest
  node:
    - version: 14
    - version: 20
      env: NODE_OPTIONS=--openssl-legacy-provider
```

--------------------------------

### Cache Python Dependencies with setup-python

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

Caches pip dependencies using the setup-python action's built-in cache feature to improve workflow performance. Automatically detects and caches requirements.txt file. Subsequent workflow runs will restore cached packages, reducing installation time.

```yaml
steps:
- uses: actions/checkout@v5
- uses: actions/setup-python@v5
  with:
    python-version: '3.12'
    cache: 'pip'
- run: pip install -r requirements.txt
- run: pip test
```

--------------------------------

### Configure action inputs with YAML metadata

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

Define input parameters for a GitHub Action using YAML syntax. This example shows how to specify required and optional inputs with descriptions and default values. Inputs are converted to uppercase environment variables prefixed with INPUT_.

```yaml
inputs:
  num-octocats:
    description: 'Number of Octocats'
    required: false
    default: '1'
  octocat-eye-color:
    description: 'Eye color of the Octocats'
    required: true
```

--------------------------------

### Monitor Runner Pods with Kubernetes kubectl

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

Bash command to monitor runner pods being created during workflow execution in the arc-runners namespace. The '-w' flag watches for real-time updates to pod status, showing pod readiness, status, restart count, and age.

```bash
kubectl get pods -n arc-runners -w
```

--------------------------------

### Conditionally Run Step Based on GitHub Event Context in YAML

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates how to use GitHub Actions contexts to conditionally execute a step. The step runs only when the event is a `pull_request` and its action is `unassigned`, showcasing conditional logic based on event data.

```YAML
steps:
  - name: My first step
    if: ${{ github.event_name == 'pull_request' && github.event.action == 'unassigned' }}
    run: echo This event is a pull request that had an assignee removed.
```

--------------------------------

### View Workflow Run Logs with GitHub CLI

Source: https://docs.github.com/en/actions/how-tos/monitor-workflows/use-workflow-run-logs

GitHub CLI commands for viewing and filtering GitHub Actions workflow logs. Supports viewing logs for specific runs or jobs, searching logs with grep, and filtering for failed steps only. Requires GitHub CLI to be installed and authenticated.

```bash
gh run view RUN_ID --log
```

```bash
gh run view --job JOB_ID --log
```

```bash
gh run view --job JOB_ID --log | grep error
```

```bash
gh run view --job JOB_ID --log-failed
```

--------------------------------

### Set and Use Environment Variable in PowerShell Workflow

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Complete GitHub Actions workflow example demonstrating setting an environment variable in one step and accessing it in a subsequent step using PowerShell. Shows variable persistence across steps with PowerShell syntax.

```yaml
steps:
  - name: Set the value
    id: step_one
    run: |
      "action_state=yellow" >> $env:GITHUB_ENV
  - name: Use the value
    id: step_two
    run: |
      Write-Output "$env:action_state" # This will output 'yellow'
```

--------------------------------

### Define GitHub Actions Steps for Container Job with Redis Connection (YAML)

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-redis-service-containers

This YAML snippet outlines the steps for a GitHub Actions container job. It includes checking out the repository, installing Node.js dependencies using `npm ci`, and running a `client.js` script to interact with a Redis service. Environment variables `REDIS_HOST` and `REDIS_PORT` are set to facilitate communication with the `redis` service container.

```yaml
steps:
  # Downloads a copy of the code in your repository before running CI tests
  - name: Check out repository code
    uses: actions/checkout@v5

  # Performs a clean installation of all dependencies in the `package.json` file
  # For more information, see https://docs.npmjs.com/cli/ci.html
  - name: Install dependencies
    run: npm ci

  - name: Connect to Redis
    # Runs a script that creates a Redis client, populates
    # the client with data, and retrieves data
    run: node client.js
    # Environment variable used by the `client.js` script to create a new Redis client.
    env:
      # The hostname used to communicate with the Redis service container
      REDIS_HOST: redis
      # The default Redis port
      REDIS_PORT: 6379
```

--------------------------------

### Specify GitHub-hosted Operating System in Workflow

Source: https://docs.github.com/en/actions/using-jobs/choosing-the-runner-for-a-job

Configure the runs-on key to specify a GitHub-hosted runner with a particular operating system. This example uses ubuntu-latest, which is the latest stable Ubuntu image provided by GitHub. The runs-on key accepts workflow labels that correspond to specific virtual machine configurations.

```yaml
runs-on: ubuntu-latest
```

--------------------------------

### Configure GitHub Actions Workflow with PostgreSQL Service Container

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers

This YAML workflow demonstrates how to set up a GitHub Actions job that utilizes a PostgreSQL service container. It configures the PostgreSQL service with environment variables, health checks, and maps its port to the Docker host, allowing the runner to connect via `localhost`. The workflow also includes steps for checking out repository code, installing Node.js dependencies, and executing a script to interact with the PostgreSQL database.

```yaml
name: PostgreSQL Service Example
on: push

jobs:
  # Label of the runner job
  runner-job:
    # You must use a Linux environment when using service containers or container jobs
    runs-on: ubuntu-latest

    # Service containers to run with `runner-job`
    services:
      # Label used to access the service container
      postgres:
        # Docker Hub image
        image: postgres
        # Provide the password for postgres
        env:
          POSTGRES_PASSWORD: postgres
        # Set health checks to wait until postgres has started
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
        ports:
          # Maps tcp port 5432 on service container to the host
          - 5432:5432

    steps:
      # Downloads a copy of the code in your repository before running CI tests
      - name: Check out repository code
        uses: actions/checkout@v5

      # Performs a clean installation of all dependencies in the `package.json` file
      # For more information, see https://docs.npmjs.com/cli/ci.html
      - name: Install dependencies
        run: npm ci

      - name: Connect to PostgreSQL
        # Runs a script that creates a PostgreSQL table, populates
        # the table with data, and then retrieves the data
        run: node client.js
        # Environment variables used by the `client.js` script to create
        # a new PostgreSQL table.
        env:
          # The hostname used to communicate with the PostgreSQL service container
          POSTGRES_HOST: localhost
          # The default PostgreSQL port
          POSTGRES_PORT: 5432
```

--------------------------------

### Illustrate `vars` Context Structure in GitHub Actions (JSON)

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

This JSON snippet provides an example of the structure of the `vars` context in GitHub Actions. It shows how custom configuration variables, defined at organization, repository, or environment levels, are represented as a mapping of variable names to their corresponding values.

```json
{
  "mascot": "Mona"
}
```

--------------------------------

### GitHub Actions `if` Conditional with Contexts

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This example illustrates how to use the `if` conditional to execute a step only when specific GitHub event contexts are met. The step will run if the event type is a `pull_request` and the action associated with that event is `unassigned`.

```yaml
steps:
  - run: echo This event is a pull request that had an assignee removed.
    if: ${{ github.event_name == 'pull_request' && github.event.action == 'unassigned' }}
```

--------------------------------

### Configure runs-on for Custom Image Runner - GitHub Actions YAML

Source: https://docs.github.com/en/actions/how-tos/manage-runners/larger-runners/use-custom-images

Sets the runs-on key to reference a custom runner in GitHub Actions workflow jobs. This directs the workflow to execute on the specified custom runner with the installed custom image.

```yaml
jobs:
  build:
    runs-on: my-custom-runner
    steps:
    # Add any steps for your workflow here
```

--------------------------------

### Execute Script in Composite Action Using github.action_path Context

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This example shows how to define a `run` step within a composite GitHub Action, executing a script located relative to the action's path. It uses the `github.action_path` context to dynamically reference the script's location. The `shell: bash` specifies the shell to use for execution.

```yaml
runs:
  using: "composite"
  steps:
    - run: ${{ github.action_path }}/test/script.sh
      shell: bash
```

--------------------------------

### Configure alternative source code provider in credentials file

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/supplemental-arguments-and-settings

Specify a provider type (gitlab, bitbucket_server, azure_devops) in the credentials file to enable GitHub Actions Importer to automatically fetch source code from non-GitHub repositories. The importer uses the provided access token to authenticate requests to the specified provider URL.

```yaml
- url: https://gitlab.com
  access_token: super_secret_token
  provider: gitlab
```

--------------------------------

### Set Job-Level GITHUB_TOKEN Permissions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Configure GITHUB_TOKEN permissions for a specific job within a workflow. This example demonstrates granting write access to issues and pull-requests for a single job while all other permissions remain restricted.

```APIDOC
## Job-Level Permissions Configuration

### Description
Set GITHUB_TOKEN permissions that apply only to a specific job in a workflow.

### Configuration Key
jobs.<job_id>.permissions

### Example: Stale Job with Limited Permissions
```yaml
jobs:
  stale:
    runs-on: ubuntu-latest
    permissions:
      issues: write
      pull-requests: write
    steps:
      - uses: actions/stale@v10
```

### Configuration Details
- **Job ID**: stale
- **Runner**: ubuntu-latest
- **Permissions Granted**:
  - issues: write - Allows writing to issues
  - pull-requests: write - Allows writing to pull requests
- **All Other Permissions**: none (default)

### Notes
- Job-level permissions override workflow-level permissions
- Only specified permissions are granted; all others default to none
- This approach is useful for applying principle of least privilege to individual jobs
```

--------------------------------

### Deploy Sigstore Policy Controller with Helm

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/enforce-artifact-attestations

This command deploys the Sigstore Policy Controller into a Kubernetes cluster using its Helm chart. It creates the `artifact-attestations` namespace and installs the controller, which will later be used to enforce artifact attestations. Prerequisites include Kubernetes 1.27+, Helm 3.0+, and kubectl.

```Bash
helm upgrade policy-controller --install --atomic \
  --create-namespace --namespace artifact-attestations \
  oci://ghcr.io/sigstore/helm-charts/policy-controller \
  --version 0.10.5
```

--------------------------------

### Add Specific Markdown Content to GitHub Actions Job Summary

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

This example demonstrates how to add a specific 'Hello world!' Markdown heading with an emoji to a GitHub Actions job summary. It uses the `>>` operator to append content to the `$GITHUB_STEP_SUMMARY` environment file, showcasing a practical use case for custom run summaries.

```Bash
echo "### Hello world! :rocket:" >> $GITHUB_STEP_SUMMARY
```

```PowerShell
"### Hello world! :rocket:" >> $env:GITHUB_STEP_SUMMARY
```

--------------------------------

### Publish Python Package to PyPI using GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

This GitHub Actions workflow automates the process of building a Python package and publishing it to PyPI. It triggers on a 'published' release, builds distribution files, uploads them as an artifact, and then downloads and publishes them to PyPI using the 'pypa/gh-action-pypi-publish' action with OIDC for secure authentication. It requires a 'pypi' environment and 'id-token: write' permission for trusted publishing.

```yaml
name: Upload Python Package

on:
  release:
    types: [published]

permissions:
  contents: read

jobs:
  release-build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5

      - uses: actions/setup-python@v5
        with:
          python-version: "3.x"

      - name: Build release distributions
        run: |
          # NOTE: put your own distribution build steps here.
          python -m pip install build
          python -m build

      - name: Upload distributions
        uses: actions/upload-artifact@v4
        with:
          name: release-dists
          path: dist/

  pypi-publish:
    runs-on: ubuntu-latest

    needs:
      - release-build

    permissions:
      # IMPORTANT: this permission is mandatory for trusted publishing
      id-token: write

    # Dedicated environments with protections for publishing are strongly recommended.
    environment:
      name: pypi
      # OPTIONAL: uncomment and update to include your PyPI project URL in the deployment status:
      # url: https://pypi.org/p/YOURPROJECT

    steps:
      - name: Retrieve release distributions
        uses: actions/download-artifact@v5
        with:
          name: release-dists
          path: dist/

      - name: Publish release distributions to PyPI
        uses: pypa/gh-action-pypi-publish@6f7e8d9c0b1a2c3d4e5f6a7b8c9d0e1f2a3b4c5d
```

--------------------------------

### Reference Local GitHub Action in Same Repository

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This snippet demonstrates how to use an action defined within the same repository as the workflow. It requires checking out the repository first and then referencing the action using a relative path from the workflow's default working directory. The example shows a `hello-world-action` located in `.github/actions/hello-world-action`.

```yaml
jobs:
  my_first_job:
    runs-on: ubuntu-latest
    steps:
      # This step checks out a copy of your repository.
      - name: My first step - check out repository
        uses: actions/checkout@v5
      # This step references the directory that contains the action.
      - name: Use local hello-world-action
        uses: ./.github/actions/hello-world-action
```

--------------------------------

### Configure Container Registry Credentials in GitHub Actions

Source: https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

This example demonstrates how to provide authentication credentials (username and password) for pulling a container image from a private registry within a GitHub Actions job. These credentials are the same values you would provide to the `docker login` command.

```yaml
container:
  image: ghcr.io/owner/image
  credentials:
     username: ${{ github.actor }}
     password: ${{ secrets.github_token }}
```

--------------------------------

### Specify Job Runners in GitLab CI/CD and GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-gitlab-cicd-to-github-actions

This example illustrates how to specify the execution environment (runner) for jobs in GitLab CI/CD and GitHub Actions. GitLab CI/CD uses `tags` to select specific runners, whereas GitHub Actions uses the `runs-on` key to define the operating system or runner label for a job.

```yaml
windows_job:
  tags:
    - windows
  script:
    - echo Hello, %USERNAME%!

linux_job:
  tags:
    - linux
  script:
    - echo "Hello, $USER!"

```

```yaml
windows_job:
  runs-on: windows-latest
  steps:
    - run: echo Hello, %USERNAME%!

linux_job:
  runs-on: ubuntu-latest
  steps:
    - run: echo "Hello, $USER!"

```

--------------------------------

### Configure Proxy Settings in .env File for Self-Hosted Runners

Source: https://docs.github.com/en/actions/how-tos/manage-runners/use-proxy-servers

Example .env file configuration for setting proxy settings on self-hosted GitHub Actions runners. This approach is used when the runner is configured as a service under a system account. The runner reads these variables at startup for proxy configuration. Note: This method is not applicable to GitHub-hosted runners.

```shell
https_proxy=http://proxy.local:8080
no_proxy=example.com,myserver.local:443
```

--------------------------------

### Tasks in Azure Pipelines

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-azure-pipelines-to-github-actions

Shows how to use tasks in Azure Pipelines to perform reusable operations. The example uses the UsePythonVersion task to set up Python 3.7 with x64 architecture, followed by a script step to run a Python script.

```yaml
jobs:
  - job: run_python
    pool:
      vmImage: 'ubuntu-latest'
    steps:
      - task: UsePythonVersion@0
        inputs:
          versionSpec: '3.7'
          architecture: 'x64'
      - script: python script.py
```

--------------------------------

### Specify Working Directory for GitHub Actions `run` Step

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example shows how to define a specific working directory for a `run` step using the `working-directory` keyword. Commands within this step will be executed relative to the specified path, in this case, `./temp`. This allows for targeted operations on files within a particular subdirectory of the repository.

```yaml
- name: Clean temp directory
  run: rm -rf *
  working-directory: ./temp
```

--------------------------------

### Combine runner groups and labels for precise job targeting in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/choose-the-runner-for-a-job

This example demonstrates how to combine runner groups and labels to precisely target a job. The job will run on a runner that is part of the `ubuntu-runners` group AND has the `ubuntu-24.04-16core` label, ensuring specific hardware and environment requirements are met for the workflow.

```yaml
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on:
      group: ubuntu-runners
      labels: ubuntu-24.04-16core
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v

```

--------------------------------

### Conditional Job Execution with always()

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Use the always() conditional expression to allow a job to run even if its dependent jobs fail or are skipped. This example demonstrates how job3 executes regardless of job1 and job2 outcomes.

```APIDOC
## Conditional Job Execution - always() Expression

### Description
Allow a job to run even if dependent jobs do not succeed using the always() conditional expression.

### Configuration Key
jobs.<job_id>.if

### Example: Job Runs Regardless of Dependencies
```yaml
jobs:
  job1:
  job2:
    needs: job1
  job3:
    if: ${{ always() }}
    needs: [job1, job2]
```

### Execution Behavior
- job1 - Runs first
- job2 - Runs after job1 completes (success or failure)
- job3 - Always runs after job1 and job2 complete, regardless of their outcomes

### Conditional Expression Syntax
- **Expression Syntax**: `${{ always() }}`
- **Alternative**: Can omit `${{ }}` in most cases, but required when expression starts with `!`
- **Escaped Format**: Use `''`, `""`, or `()` when expression starts with `!`

### Example: Negation Expression
```yaml
if: ${{ ! startsWith(github.ref, 'refs/tags/') }}
```

### Notes
- The always() function evaluates to true regardless of previous job outcomes
- Useful for cleanup jobs, notifications, or reporting that should always execute
- Conditional expressions are evaluated before strategy.matrix is applied
```

--------------------------------

### Create entrypoint.sh for GitHub Docker Action

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-a-docker-container-action

Shell script that serves as the entry point for a Docker-based GitHub Action. It accepts input parameters, processes them, and writes output variables to the $GITHUB_OUTPUT environment file for use by subsequent actions in the workflow.

```shell
#!/bin/sh -l

echo "Hello $1"
time=$(date)
echo "time=$time" >> $GITHUB_OUTPUT
```

--------------------------------

### Set and use environment variables in GitHub Actions workflow

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Demonstrates a complete GitHub Actions workflow that sets environment variables using GITHUB_ENV and uses them in subsequent steps. This example shows setting MY_ENV_VAR and then echoing its value in a later step.

```yaml
name: Example Workflow for Environment Files

on: push

jobs:
  set_and_use_env_vars:
    runs-on: ubuntu-latest
    steps:
      - name: Set environment variable
        run: echo "MY_ENV_VAR=myValue" >> $GITHUB_ENV

      - name: Use environment variable
        run: |
          echo "The value of MY_ENV_VAR is $MY_ENV_VAR"
```

--------------------------------

### Pull Request Workflow - Combined Filters

Source: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows

Configure a workflow with multiple filters to run only when specific conditions are met. This example runs when a pull request is opened on a release branch and includes JavaScript file changes.

```APIDOC
## Pull Request Workflow - Combined Filters

### Description
Trigger a workflow when multiple conditions are satisfied simultaneously, such as specific branch patterns and file changes.

### Event Type
`pull_request`

### Configuration
```yaml
on:
  pull_request:
    types:
      - opened
    branches:
      - 'releases/**'
    paths:
      - '**.js'
```

### Parameters
- **types** (array) - Optional - Activity types that trigger the workflow (e.g., 'opened', 'synchronize')
- **branches** (array) - Optional - Branch name patterns using glob syntax
- **paths** (array) - Optional - File path patterns that must be changed

### Behavior
- Workflow runs only when ALL specified filters are satisfied
- Branch pattern uses glob syntax (e.g., `releases/**` matches `releases/v1.0`)
- File changes must match the specified paths

### Example Scenario
Run deployment workflow when a pull request is opened on any release branch and includes JavaScript changes
```

--------------------------------

### jobs.<job_id>.steps

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

A job contains a sequence of tasks called steps. Steps can run commands, setup tasks, or actions from repositories or Docker registries. Each step runs in its own process with access to the workspace and filesystem. GitHub displays the first 1,000 checks but allows unlimited steps within workflow usage limits.

```APIDOC
## jobs.<job_id>.steps

### Description
A job contains a sequence of tasks called `steps`. Steps can run commands, run setup tasks, or run an action in your repository, a public repository, or an action published in a Docker registry.

### Characteristics
- Not all steps run actions, but all actions run as a step
- Each step runs in its own process in the runner environment
- Each step has access to the workspace and filesystem
- Changes to environment variables are not preserved between steps
- GitHub provides built-in steps to set up and complete a job

### Limits
- GitHub displays the first 1,000 checks
- Unlimited number of steps can be run within workflow usage limits
- Subject to billing and usage limits for GitHub-hosted runners
- Subject to Actions limits for self-hosted runner usage

### Example: Basic Steps Configuration

```yaml
name: Greeting from Mona

on: push

jobs:
  my-job:
    name: My Job
    runs-on: ubuntu-latest
    steps:
      - name: Print a greeting
        env:
          MY_VAR: Hi there! My name is
          FIRST_NAME: Mona
          MIDDLE_NAME: The
          LAST_NAME: Octocat
        run: |
          echo $MY_VAR $FIRST_NAME $MIDDLE_NAME $LAST_NAME.
```
```

--------------------------------

### Configure HTTP Proxy Environment Variables

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/supplemental-arguments-and-settings

Set OCTOKIT_PROXY for GitHub servers and HTTP_PROXY or HTTPS_PROXY for other servers to route requests through a proxy. If proxy authentication is required, include username and password in the URL format: https://username:password@proxy.url:port.

```shell
export OCTOKIT_PROXY=https://proxy.example.com:8443
export HTTPS_PROXY=$OCTOKIT_PROXY
```

--------------------------------

### Example of Self-Hosted Runner Update Log Entry

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/monitoring-and-troubleshooting-self-hosted-runners

This log entry snippet illustrates how the self-hosted runner's `Runner_` log files indicate the availability of an update. Monitoring these logs is important to ensure the runner stays up-to-date and can process jobs effectively.

```text
[Feb 12 12:37:07 INFO SelfUpdater] An update is available.
```

--------------------------------

### Conditional expressions in GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-azure-pipelines-to-github-actions

Demonstrates conditional step execution in GitHub Actions using the 'if' key with infix notation. The example uses the '==' and '&&' operators to evaluate multiple conditions, replacing Azure Pipelines' function-based syntax.

```yaml
jobs:
  conditional:
    runs-on: ubuntu-latest
    steps:
      - run: echo "This step runs with str equals 'ABC' and num equals 123"
        if: ${{ env.str == 'ABC' && env.num == 123 }}
```

--------------------------------

### cleanup_job Command Input JSON

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

Example input for the cleanup_job command which is called at the end of a job execution. This command receives the current state including network and container identifiers but no additional arguments. The cleanup_job is responsible for stopping and deleting containers, networks, and cleaning up all job-related resources.

```json
{
  "command": "cleanup_job",
  "responseFile": null,
  "state": {
    "network": "example_network_53269bd575972817b43f7733536b200c",
    "jobContainer": "82e8219701fe096a35941d869cf3d71af1d943b5d8bdd718857fb87ac3042480",
    "serviceContainers": {
      "redis": "60972d9aa486605e66b0dad4abb678dc3d9116f536579e418176eedb8abb9105"
    }
  },
  "args": {}
}
```

--------------------------------

### Package and Upload Test Artifacts in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/net

Demonstrates a complete GitHub Actions workflow that builds and tests .NET projects across multiple SDK versions using a matrix strategy, then uploads test results as artifacts. The workflow uses the upload-artifact action to store test results for analysis, with conditional execution to ensure artifacts are uploaded even when tests fail.

```yaml
name: dotnet package

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        dotnet-version: [ '3.1.x', '6.0.x' ]

      steps:
        - uses: actions/checkout@v5
        - name: Setup dotnet
          uses: actions/setup-dotnet@v4
          with:
            dotnet-version: ${{ matrix.dotnet-version }}
        - name: Install dependencies
          run: dotnet restore
        - name: Test with dotnet
          run: dotnet test --no-restore --logger trx --results-directory "TestResults-${{ matrix.dotnet-version }}"
        - name: Upload dotnet test results
          uses: actions/upload-artifact@v4
          with:
            name: dotnet-results-${{ matrix.dotnet-version }}
            path: TestResults-${{ matrix.dotnet-version }}
          if: ${{ always() }}
```

--------------------------------

### Trigger GitHub Actions workflow on repository star (watch:started event)

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

This snippet illustrates how to configure a GitHub Actions workflow to run specifically when a repository is starred, corresponding to the `started` activity type of the `watch` event. It uses the `types` keyword to filter for this specific activity, ensuring the workflow only runs for star events.

```yaml
on:
  watch:
    types: [started]
```

--------------------------------

### GitHub Actions: Running Jobs in a Container

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/run-jobs-in-a-container

This section provides an overview of how to configure a GitHub Actions job to run its steps within a Docker container, ensuring a consistent and isolated execution environment. It covers the basic setup and general behavior.

```APIDOC
## CONFIGURATION jobs.<job_id>.container

### Description
This configuration block defines a Docker container to run all steps in a job that don't already specify a container. Container actions will run as sibling containers on the same network with the same volume mounts.

### Method
CONFIGURATION

### Endpoint
jobs.<job_id>.container

### Parameters
#### Path Parameters
- No path parameters.

#### Query Parameters
- No query parameters.

#### Request Body
- **image** (string) - Optional - The Docker image to use for the container (e.g., `node:18`).
- **env** (object) - Optional - A map of environment variables to set inside the container.
- **ports** (array of numbers) - Optional - An array of ports to expose on the container.
- **volumes** (array of strings) - Optional - An array of volumes to mount into the container.
- **options** (string) - Optional - Additional Docker container resource options (e.g., `--cpus 1`).
- **credentials** (object) - Optional - Credentials for authenticating with private container registries.

### Request Example
```yaml
name: CI
on:
  push:
    branches: [ main ]
jobs:
  container-test-job:
    runs-on: ubuntu-latest
    container:
      image: node:18
      env:
        NODE_ENV: development
      ports:
        - 80
      volumes:
        - my_docker_volume:/volume_mount
      options: --cpus 1
    steps:
      - name: Check for dockerenv file
        run: (ls /.dockerenv && echo Found dockerenv) || (echo No dockerenv)

```

### Response
#### Success Response (N/A)
- Job steps run within the specified container.

#### Response Example
```json
{}
```
```

--------------------------------

### Build Xamarin.iOS Application with GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/xamarin-apps

This GitHub Actions workflow demonstrates how to build a Xamarin.iOS application. It configures specific Xamarin SDK and Xcode versions on a macOS runner, sets up the .NET Core SDK, restores NuGet dependencies, and then compiles the project using MSBuild. The workflow requires a solution file path (`<sln_file_path>`) and a project file path (`<csproj_file_path>`) as inputs for the restore and build steps.

```yaml
name: Build Xamarin.iOS app

on: [push]

jobs:
  build:

    runs-on: macos-latest

    steps:
    - uses: actions/checkout@v5
    - name: Set default Xamarin SDK versions
      run: |
        $VM_ASSETS/select-xamarin-sdk-v2.sh --mono=6.12 --ios=14.10

    - name: Set default Xcode 12.3
      run: |
        XCODE_ROOT=/Applications/Xcode_12.3.0.app
        echo "MD_APPLE_SDK_ROOT=$XCODE_ROOT" >> $GITHUB_ENV
        sudo xcode-select -s $XCODE_ROOT

    - name: Setup .NET Core SDK 5.0.x
      uses: actions/setup-dotnet@v4
      with:
        dotnet-version: '5.0.x'

    - name: Install dependencies
      run: nuget restore <sln_file_path>

    - name: Build
      run: msbuild <csproj_file_path> /p:Configuration=Debug /p:Platform=iPhoneSimulator /t:Rebuild
```

--------------------------------

### Lint and Format Code with Ruff

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

Installs and runs Ruff for code linting and formatting checks with Python 3.9 target version. Outputs linting results in GitHub format for inline annotations. Formatting check has continue-on-error enabled to prevent workflow failure on formatting issues.

```yaml
steps:
- uses: actions/checkout@v5
- name: Set up Python
  uses: actions/setup-python@v5
  with:
    python-version: '3.x'
- name: Install the code linting and formatting tool Ruff
  run: pipx install ruff
- name: Lint code with Ruff
  run: ruff check --output-format=github --target-version=py39
- name: Check code formatting with Ruff
  run: ruff format --diff --target-version=py39
  continue-on-error: true
```

--------------------------------

### Create Kubernetes Secret for Proxy Authentication

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

Creates a Kubernetes secret containing proxy authentication credentials (username and password) for authenticated proxy access. The secret must be created in the same namespace where the gha-runner-scale-set chart is installed.

```bash
kubectl create secret generic proxy-auth \
  --namespace=arc-runners \
  --from-literal=username=proxyUsername \
  --from-literal=password=proxyPassword
```

--------------------------------

### Persist Data Between Jobs - CircleCI YAML Syntax

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-circleci

CircleCI workspace persistence syntax using persist_to_workspace to save artifacts and attach_workspace to retrieve them in subsequent jobs. This example persists math-homework.txt from workspace root and attaches it to /tmp/workspace.

```yaml
- persist_to_workspace:
    root: workspace
    paths:
      - math-homework.txt

...

- attach_workspace:
    at: /tmp/workspace
```

--------------------------------

### Configure OIDC `sub` claim for reusable workflow, repo, and context in GitHub Actions

Source: https://docs.github.com/en/actions/reference/openid-connect-reference

This example combines the requirement for a specific reusable workflow with additional claims like `repo` and `context`. It demonstrates using `"context"` to define conditions, such as environment names, and is applied via the GitHub Actions OIDC API for organizations or repositories.

```json
{
   "include_claim_keys": [
       "repo",
       "context",
       "job_workflow_ref"
   ]
}
```

--------------------------------

### Check Docker Service Status (Linux systemctl)

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/monitoring-and-troubleshooting-self-hosted-runners

This `systemctl` command is used on Linux systems to verify if the Docker service is actively running. For self-hosted runners that require containers, Docker must be installed and active for jobs to succeed.

```bash
sudo systemctl is-active docker.service
```

--------------------------------

### Configure Container Registry Credentials in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates how to provide authentication credentials for a container registry when pulling an image for a GitHub Actions job container. The `username` and `password` are typically sourced from GitHub contexts or secrets, similar to how `docker login` would use them.

```yaml
container:
  image: ghcr.io/owner/image
  credentials:
     username: ${{ github.actor }}
     password: ${{ secrets.github_token }}

```

--------------------------------

### Declare Outputs for GitHub Composite Actions

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This example demonstrates how to declare outputs for a composite GitHub Action. It defines a `random-number` output, providing a description and mapping its value to an output from a preceding step within the composite action. This allows the output to be consumed by subsequent jobs or steps in the workflow.

```yaml
outputs:
  random-number:
    description: "Random number"
    value: ${{ steps.random-number-generator.outputs.random-id }}
runs:
  using: "composite"
  steps:
    - id: random-number-generator
      run: echo "random-id=$(echo $RANDOM)" >> $GITHUB_OUTPUT
      shell: bash
```

--------------------------------

### Access job outputs in dependent job

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/pass-job-outputs

Accesses outputs from a dependent job using the needs.<job_id>.outputs.<output_name> syntax. The example demonstrates how job2 retrieves output1 and output2 from job1 and uses them as environment variables in a step.

```yaml
jobs:
  job2:
    runs-on: ubuntu-latest
    needs: job1
    steps:
      - env:
          OUTPUT1: ${{needs.job1.outputs.output1}}
          OUTPUT2: ${{needs.job1.outputs.output2}}
        run: echo "$OUTPUT1 $OUTPUT2"
```

--------------------------------

### Ruby Gem Publishing Workflow - GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/ruby

A complete GitHub Actions workflow that builds and publishes Ruby gems to both GitHub Package Registry and RubyGems. The workflow triggers on manual dispatch, push to main branch, or pull requests. It sets up Ruby 2.6, installs dependencies, and publishes packages using stored credentials from repository secrets. Requires GITHUB_TOKEN and RUBYGEMS_AUTH_TOKEN secrets to be configured.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# GitHub recommends pinning actions to a commit SHA.
# To get a newer version, you will need to update the SHA.
# You can also reference a tag or branch, but the action may change without warning.

name: Ruby Gem

on:
  # Manually publish
  workflow_dispatch:
  # Alternatively, publish whenever changes are merged to the `main` branch.
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    name: Build + Publish
    runs-on: ubuntu-latest
    permissions:
      packages: write
      contents: read

    steps:
      - uses: actions/checkout@v5
      - name: Set up Ruby 2.6
        uses: ruby/setup-ruby@ec02537da5712d66d4d50a0f33b7eb52773b5ed1
        with:
          ruby-version: '2.6'
      - run: bundle install

      - name: Publish to GPR
        run: |
          mkdir -p $HOME/.gem
          touch $HOME/.gem/credentials
          chmod 0600 $HOME/.gem/credentials
          printf -- "---\n:github: ${GEM_HOST_API_KEY}\n" > $HOME/.gem/credentials
          gem build *.gemspec
          gem push --KEY github --host https://rubygems.pkg.github.com/${OWNER} *.gem
        env:
          GEM_HOST_API_KEY: "Bearer ${{secrets.GITHUB_TOKEN}}"
          OWNER: ${{ github.repository_owner }}

      - name: Publish to RubyGems
        run: |
          mkdir -p $HOME/.gem
          touch $HOME/.gem/credentials
          chmod 0600 $HOME/.gem/credentials
          printf -- "---\n:rubygems_api_key: ${GEM_HOST_API_KEY}\n" > $HOME/.gem/credentials
          gem build *.gemspec
          gem push *.gem
        env:
          GEM_HOST_API_KEY: "${{secrets.RUBYGEMS_AUTH_TOKEN}}"
```

--------------------------------

### Set Job-Level Environment Variables in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates how to define environment variables that are available to all steps within a specific job in a GitHub Actions workflow. Environment variables set at this level override workflow-level variables with the same name.

```yaml
jobs:
  job1:
    env:
      FIRST_NAME: Mona
```

--------------------------------

### Conditional Job Execution with Repository Check

Source: https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions

This example demonstrates how to use the `if` conditional statement to control job execution based on repository name and organization. The production-deploy job will only run when the repository matches the specified organization and repository name, otherwise it will be marked as skipped.

```APIDOC
## Conditional Job Execution

### Description
Control job execution using conditional statements based on repository context variables.

### Configuration
```yaml
name: example-workflow
on: [push]
jobs:
  production-deploy:
    if: github.repository == 'octo-org/octo-repo-prod'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '14'
      - run: npm install -g bats
```

### Parameters
- **if** (string) - Conditional expression that determines whether the job runs. Use `github.repository` to check repository name and organization.
- **runs-on** (string) - Specifies the runner type (e.g., `ubuntu-latest`)
- **steps** (array) - List of actions and commands to execute

### Behavior
- Job runs only if condition evaluates to `true`
- Job is marked as _skipped_ if condition evaluates to `false`
- Supports complex conditional logic with operators like `==`, `!=`, `&&`, `||`
```

--------------------------------

### Create Kubernetes Secret for GitHub App Authentication

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/authenticating-to-the-github-api

Creates a Kubernetes secret containing GitHub App credentials (App ID, Installation ID, and private key) for Actions Runner Controller authentication. The secret must be created in the same namespace where the gha-runner-scale-set chart is installed (e.g., arc-runners). This secret is referenced in the values.yaml file via the githubConfigSecret property.

```bash
kubectl create secret generic pre-defined-secret \
   --namespace=arc-runners \
   --from-literal=github_app_id=123456 \
   --from-literal=github_app_installation_id=654321 \
   --from-literal=github_app_private_key='-----BEGIN RSA PRIVATE KEY-----********'
```

--------------------------------

### Connect to PostgreSQL Service and Test Data Operations with Node.js

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers

Node.js script that establishes a connection to a PostgreSQL service container using environment variables, creates a student table, inserts placeholder data, and retrieves the results. The script uses the pg npm module and supports customization for any PostgreSQL operations needed in your workflow. Connection defaults to localhost:5432 if host and port are not specified.

```javascript
const { Client } = require('pg');

const pgclient = new Client({
    host: process.env.POSTGRES_HOST,
    port: process.env.POSTGRES_PORT,
    user: 'postgres',
    password: 'postgres',
    database: 'postgres'
});

pgclient.connect();

const table = 'CREATE TABLE student(id SERIAL PRIMARY KEY, firstName VARCHAR(40) NOT NULL, lastName VARCHAR(40) NOT NULL, age INT, address VARCHAR(80), email VARCHAR(40))'
const text = 'INSERT INTO student(firstname, lastname, age, address, email) VALUES($1, $2, $3, $4, $5) RETURNING *'
const values = ['Mona the', 'Octocat', 9, '88 Colin P Kelly Jr St, San Francisco, CA 94107, United States', 'octocat@github.com']

pgclient.query(table, (err, res) => {
    if (err) throw err
});

pgclient.query(text, values, (err, res) => {
    if (err) throw err
});

pgclient.query('SELECT * FROM student', (err, res) => {
    if (err) throw err
    console.log(err, res.rows) // Print the data in student table
    pgclient.end()
});
```

--------------------------------

### GitHub Actions Workflow to Test a Public Action (YAML)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

This YAML defines a GitHub Actions workflow that runs on `push` events to the `main` branch. It demonstrates how to integrate and test a public GitHub Action by specifying its `uses` path, passing inputs via `with`, and accessing its outputs, providing a practical example of action consumption.

```yaml
on:
  push:
    branches:
      - main

jobs:
  hello_world_job:
    name: A job to say hello
    runs-on: ubuntu-latest

    steps:
      - name: Hello world action step
        id: hello
        uses: octocat/hello-world-javascript-action@1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b
        with:
          who-to-greet: Mona the Octocat

      # Use the output from the `hello` step
      - name: Get the output time
        run: echo "The time was ${{ steps.hello.outputs.time }}"
```

--------------------------------

### Make entrypoint script executable (Shell)

Source: https://docs.github.com/en/actions/reference/dockerfile-support-for-github-actions

This shell command grants execute permissions to the `entrypoint.sh` file. It is a crucial step to ensure that the script can be run by the Docker container's `ENTRYPOINT` instruction. Without execute permissions, the container will fail to start the action.

```bash
chmod +x entrypoint.sh

```

--------------------------------

### Prepare Shell Script for GitHub Composite Action

Source: https://docs.github.com/en/actions/tutorials/create-actions/create-a-composite-action_platform=linux

These shell commands demonstrate how to create a simple script, make it executable, and manage its version control within a Git repository. This script will serve as a component of a composite GitHub Action, enabling reusable steps in workflows.

```Shell
echo "echo Goodbye" > goodbye.sh
```

```Shell
chmod +x goodbye.sh
```

```Shell
git add --chmod=+x -- goodbye.sh
```

```Shell
git add goodbye.sh
git commit -m "Add goodbye script"
git push
```

```Shell
git commit -m "Add goodbye script"
git push
```

--------------------------------

### Use YAML Anchors and Aliases for Environment Variables

Source: https://docs.github.com/en/actions/reference/reusable-workflows-reference

Reduce repetition in GitHub Actions workflows by using YAML anchors (&) to define reusable content and aliases (*) to reference it in multiple jobs. This example demonstrates reusing environment variables across different jobs, eliminating the need to duplicate variable definitions.

```yaml
jobs:
  job1:
    env: &env_vars # Define the anchor on first use
      NODE_ENV: production
      DATABASE_URL: ${{ secrets.DATABASE_URL }}
    steps:
      - run: echo "Using production settings"

  job2:
    env: *env_vars # Reuse the environment variables
    steps:
      - run: echo "Same environment variables here"
```

--------------------------------

### GET /.../badge.svg?branch=BRANCH-NAME

Source: https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/adding-a-workflow-status-badge

Retrieves a status badge image for a specific workflow file, filtered by a designated branch.

```APIDOC
## GET /OWNER/REPOSITORY/actions/workflows/WORKFLOW-FILE/badge.svg?branch=BRANCH-NAME

### Description
Retrieves a status badge image for a specific workflow file, filtered by a designated branch. This allows displaying the status for a branch other than the default.

### Method
GET

### Endpoint
/OWNER/REPOSITORY/actions/workflows/WORKFLOW-FILE/badge.svg

### Parameters
#### Path Parameters
- **OWNER** (string) - Required - The owner of the repository (user or organization).
- **REPOSITORY** (string) - Required - The name of the repository.
- **WORKFLOW-FILE** (string) - Required - The path to the workflow file within the `.github/workflows` directory (e.g., `main.yml`).

#### Query Parameters
- **branch** (string) - Optional - The name of the branch to display the workflow status for.

#### Request Body
(None)

### Request Example
{}

### Response
#### Success Response (200)
- **Content-Type** (string) - `image/svg+xml`
- **Body** (image) - An SVG image representing the workflow's current status for the specified branch.

#### Response Example
{}
```

--------------------------------

### Conditional expressions in Azure Pipelines

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-azure-pipelines-to-github-actions

Shows how to use conditional expressions in Azure Pipelines workflows using the 'condition' key with function-based syntax. The example uses the 'and' and 'eq' functions to evaluate multiple conditions before executing a step.

```yaml
jobs:
  - job: conditional
    pool:
      vmImage: 'ubuntu-latest'
    steps:
      - script: echo "This step runs with str equals 'ABC' and num equals 123"
        condition: and(eq(variables.str, 'ABC'), eq(variables.num, 123))
```

--------------------------------

### Example Output of GitHub Actions Importer Migrate Command

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/circleci-migration

This snippet illustrates the expected output after successfully running the `gh actions-importer migrate` command. It shows the path to the generated log file and, crucially, the URL of the pull request created in the GitHub repository, which contains the converted workflow.

```bash
$ gh actions-importer migrate circle-ci --target-url https://github.com/octo-org/octo-repo --output-dir tmp/migrate --circle-ci-project my-circle-ci-project
[2022-08-20 22:08:20] Logs: 'tmp/migrate/log/actions-importer-20220916-014033.log'
[2022-08-20 22:08:20] Pull request: 'https://github.com/octo-org/octo-repo/pull/1'
```

--------------------------------

### GET /.../badge.svg?event=EVENT-TYPE

Source: https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/adding-a-workflow-status-badge

Retrieves a status badge image for a specific workflow file, filtered by the event that triggered the workflow run.

```APIDOC
## GET /OWNER/REPOSITORY/actions/workflows/WORKFLOW-FILE/badge.svg?event=EVENT-TYPE

### Description
Retrieves a status badge image for a specific workflow file, filtered by the event that triggered the workflow run. This allows displaying the status for runs initiated by a specific event type (e.g., `push`).

### Method
GET

### Endpoint
/OWNER/REPOSITORY/actions/workflows/WORKFLOW-FILE/badge.svg

### Parameters
#### Path Parameters
- **OWNER** (string) - Required - The owner of the repository (user or organization).
- **REPOSITORY** (string) - Required - The name of the repository.
- **WORKFLOW-FILE** (string) - Required - The path to the workflow file within the `.github/workflows` directory (e.g., `main.yml`).

#### Query Parameters
- **event** (string) - Optional - The type of event that triggered the workflow run (e.g., `push`).

#### Request Body
(None)

### Request Example
{}

### Response
#### Success Response (200)
- **Content-Type** (string) - `image/svg+xml`
- **Body** (image) - An SVG image representing the workflow's current status for runs triggered by the specified event.

#### Response Example
{}
```

--------------------------------

### Exclude Specific Python Version Combinations in GitHub Actions Matrix (YAML)

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

This YAML example illustrates how to use the `exclude` keyword within a GitHub Actions matrix strategy. It prevents specific combinations of operating systems and Python versions from running, which is useful for avoiding unsupported or problematic configurations in your CI/CD pipeline.

```YAML
name: Python package

on: [push]

jobs:
  build:

    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, macos-latest, windows-latest]
        python-version: ["3.9", "3.11", "3.13", "pypy3.10"]
        exclude:
          - os: macos-latest
            python-version: "3.11"
          - os: windows-latest
            python-version: "3.11"
```

--------------------------------

### Specify shell command execution in GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-azure-pipelines-to-github-actions

Demonstrates how to run commands in different shells on GitHub Actions runners. The example shows running PowerShell by default on Windows and explicitly specifying CMD shell. Use the 'shell' key to override the default shell for a specific step.

```yaml
jobs:
  run_command:
    runs-on: windows-latest
    steps:
      - run: echo "This step runs in PowerShell on Windows by default"
      - run: echo "This step runs in CMD on Windows explicitly"
        shell: cmd
```

--------------------------------

### on.workflow_call.secrets

Source: https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

Defines secrets that can be passed to and used within a called workflow. It specifies whether secrets are required and provides an example of passing them to actions or nested workflows.

```APIDOC
## on.workflow_call.secrets

### Description
A map of the secrets that can be used in the called workflow. Within the called workflow, you can use the `secrets` context to refer to a secret. If a caller workflow passes a secret that is not specified in the called workflow, this results in an error.

### Method
N/A (Configuration)

### Endpoint
N/A (Configuration Path)

### Parameters
#### Request Body
- **access-token** (string) - Optional - 'A token passed from the caller workflow'

### Request Example
```yaml
on:
  workflow_call:
    secrets:
      access-token:
        description: 'A token passed from the caller workflow'
        required: false

jobs:

  pass-secret-to-action:
    runs-on: ubuntu-latest
    steps:
    # passing the secret to an action
      - name: Pass the received secret to an action
        uses: ./.github/actions/my-action
        with:
          token: ${{ secrets.access-token }}

  # passing the secret to a nested reusable workflow
  pass-secret-to-workflow:
    uses: ./.github/workflows/my-workflow
    secrets:
       token: ${{ secrets.access-token }}

```

### Response
N/A
```

--------------------------------

### Set and Use Environment Variable in Bash Workflow

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Complete GitHub Actions workflow example demonstrating setting an environment variable in one step and accessing it in a subsequent step using Bash. Shows the variable persists across steps within the same job.

```yaml
steps:
  - name: Set the value
    id: step_one
    run: |
      echo "action_state=yellow" >> "$GITHUB_ENV"
  - name: Use the value
    id: step_two
    run: |
      printf '%s\n' "$action_state" # This will output 'yellow'
```

--------------------------------

### Commit, Tag, and Push GitHub Action Release (Git)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

These Git commands prepare and publish a new version of the GitHub Action. They stage relevant files, create a commit with a descriptive message, apply an annotated tag for versioning, and push both the commit and the tags to the remote repository, making the action available for use.

```shell
git add src/index.js dist/index.js rollup.config.js package.json package-lock.json README.md action.yml
git commit -m "Initial commit of my first action"
git tag -a -m "My first action release" v1.1
git push --follow-tags
```

--------------------------------

### Execute GitHub Actions Importer Dry Run with Custom Configuration File

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/bamboo-migration

This example demonstrates using the `--config-file-path` argument with the `gh actions-importer dry-run bamboo build` subcommand. It specifies a YAML configuration file to define the source for the dry run, allowing the importer to process pipeline content based on the provided file. The `repository_slug` is derived from the `--plan-slug` option, and the source file path is matched from the config.

```bash
gh actions-importer dry-run bamboo build --plan-slug IN-COM -o tmp/bamboo --config-file-path "./path/to/my/bamboo/config.yml"
```

--------------------------------

### Set proxy environment variables on Linux and macOS

Source: https://docs.github.com/en/actions/how-tos/manage-runners/use-proxy-servers

Export proxy environment variables for HTTPS and HTTP traffic with optional bypass list for direct connections. These variables must be set before starting the runner application and are case-sensitive on Linux/macOS systems.

```shell
export https_proxy=http://proxy.local:8080
export http_proxy=http://proxy.local:8080
export no_proxy=example.com,localhost,127.0.0.1
```

--------------------------------

### Define Steps and Environment Variables in GitHub Actions Job

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This YAML example illustrates how to define a sequence of steps within a GitHub Actions job, including setting step-level environment variables. It demonstrates how to access these variables within a `run` command to print a greeting message. This pattern is useful for encapsulating specific tasks and their required configuration.

```yaml
name: Greeting from Mona

on: push

jobs:
  my-job:
    name: My Job
    runs-on: ubuntu-latest
    steps:
      - name: Print a greeting
        env:
          MY_VAR: Hi there! My name is
          FIRST_NAME: Mona
          MIDDLE_NAME: The
          LAST_NAME: Octocat
        run: |
          echo $MY_VAR $FIRST_NAME $MIDDLE_NAME $LAST_NAME.

```

--------------------------------

### Conditionally Run Pre-Action Hook Based on OS in GitHub Actions

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This snippet shows how to conditionally execute a `pre` action hook using `pre-if`. The `cleanup.js` script will only run if the runner's operating system is Linux, as specified by `runner.os == 'linux'`. This allows for platform-specific setup or validation before the main action.

```yaml
  pre: 'cleanup.js'
  pre-if: runner.os == 'linux'
```

--------------------------------

### Automate PHP Azure Web App Deployment with GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/php-to-azure-app-service

This YAML configuration defines a GitHub Actions workflow that triggers on pushes to the `main` branch. It consists of two jobs: `build` and `deploy`. The `build` job sets up PHP, checks for `composer.json`, caches Composer dependencies, runs `composer install`, and uploads the application as an artifact. The `deploy` job downloads the artifact and deploys it to the specified Azure Web App using a publish profile secret.

```yaml
name: Build and deploy PHP app to Azure Web App

env:
  AZURE_WEBAPP_NAME: MY_WEBAPP_NAME   # set this to your application's name
  AZURE_WEBAPP_PACKAGE_PATH: '.'      # set this to the path to your web app project, defaults to the repository root
  PHP_VERSION: '8.x'                  # set this to the PHP version to use

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5

      - name: Setup PHP
        uses: shivammathur/setup-php@1f2e3d4c5b6a7f8e9d0c1b2a3e4f5d6c7b8a9e0f
        with:
          php-version: ${{ env.PHP_VERSION }}

      - name: Check if composer.json exists
        id: check_files
        uses: andstor/file-existence-action@2a3b4c5d6e7f8a9b0c1d2e3f4a5b6c7d8e9f0a1b
        with:
          files: 'composer.json'

      - name: Get Composer Cache Directory
        id: composer-cache
        if: steps.check_files.outputs.files_exists == 'true'
        run: |
          echo "dir=$(composer config cache-files-dir)" >> $GITHUB_OUTPUT

      - name: Set up dependency caching for faster installs
        uses: actions/cache@v4
        if: steps.check_files.outputs.files_exists == 'true'
        with:
          path: ${{ steps.composer-cache.outputs.dir }}
          key: ${{ runner.os }}-composer-${{ hashFiles('**/composer.lock') }}
          restore-keys: |
            ${{ runner.os }}-composer-

      - name: Run composer install if composer.json exists
        if: steps.check_files.outputs.files_exists == 'true'
        run: composer validate --no-check-publish && composer install --prefer-dist --no-progress

      - name: Upload artifact for deployment job
        uses: actions/upload-artifact@v4
        with:
          name: php-app
          path: .

  deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: 'production'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}

    steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v5
        with:
          name: php-app

      - name: 'Deploy to Azure Web App'
        id: deploy-to-webapp
        uses: azure/webapps-deploy@85270a1854658d167ab239bce43949edb336fa7c
        with:
          app-name: ${{ env.AZURE_WEBAPP_NAME }}
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
          package: .
```

--------------------------------

### Filter Workflow Trigger by Branch

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

Shows how to use the `branches` filter with the `workflow_run` event to restrict workflow execution to specific branches. This example triggers only when the 'Build' workflow runs on the 'canary' branch.

```yaml
on:
  workflow_run:
    workflows: [Build]
    types: [requested]
    branches: [canary]
```

--------------------------------

### Configure Specific Python Version in GitHub Actions (YAML)

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

This YAML snippet demonstrates how to use the `actions/setup-python@v5` action to specify a particular Python version (e.g., '3.x' for the latest minor release) and optionally define the architecture (e.g., 'x64'). It also includes a step to display the current Python version for verification within the workflow.

```YAML
name: Python package

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5
      - name: Set up Python
        # This is the version of the action for setting up Python, not the Python version.
        uses: actions/setup-python@v5
        with:
          # Semantic version range syntax or exact version of a Python version
          python-version: '3.x'
          # Optional - x64 or x86 architecture, defaults to x64
          architecture: 'x64'
      # You can test your matrix by printing the current Python version
      - name: Display Python version
        run: python -c "import sys; print(sys.version)"
```

--------------------------------

### Job Conditional Statements

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Use the if conditional to prevent a job from running unless a condition is met. Supports any context and expression, with special syntax requirements for expressions starting with negation operators.

```APIDOC
## jobs.<job_id>.if - Job Conditionals

### Description
Prevent a job from running unless a condition is met using conditional expressions.

### Configuration Key
jobs.<job_id>.if

### Supported Contexts
- github context
- env context
- secrets context
- vars context
- job context
- steps context
- runner context
- strategy context

### Expression Syntax Rules

#### Standard Expression
```yaml
if: ${{ expression }}
```

#### Optional Syntax (without ${{ }})
```yaml
if: expression
```

#### Required Syntax for Negation
```yaml
if: ${{ ! startsWith(github.ref, 'refs/tags/') }}
```

#### Escaped Negation Alternatives
```yaml
if: ${{ !'string' }}
if: ${{ !"string" }}
if: ${{ !(expression) }}
```

### Common Conditional Examples

#### Check Branch
```yaml
if: ${{ github.ref == 'refs/heads/main' }}
```

#### Check Event Type
```yaml
if: ${{ github.event_name == 'push' }}
```

#### Check Tag
```yaml
if: ${{ startsWith(github.ref, 'refs/tags/') }}
```

### Notes
- Conditionals are evaluated before strategy.matrix is applied
- The `!` character is reserved in YAML, requiring special escaping
- For detailed expression syntax, see Evaluate expressions in workflows and actions documentation
```

--------------------------------

### Publish .NET Package to GitHub Packages Registry

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/net

Demonstrates a GitHub Actions workflow that publishes a .NET package to GitHub Packages upon release creation. The workflow builds the project in Release configuration, creates a NuGet package using dotnet pack, and pushes it to the GitHub Package Registry using authentication via GITHUB_TOKEN secret.

```yaml
name: Upload dotnet package

on:
  release:
    types: [created]

jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      packages: write
      contents: read
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-dotnet@v4
        with:
          dotnet-version: '6.0.x'
          source-url: https://nuget.pkg.github.com/<owner>/index.json
        env:
          NUGET_AUTH_TOKEN: ${{secrets.GITHUB_TOKEN}}
      - run: dotnet build --configuration Release <my project>
      - name: Create the package
        run: dotnet pack --configuration Release <my project>
      - name: Publish the package to GPR
        run: dotnet nuget push <my project>/bin/Release/*.nupkg
```

--------------------------------

### GitHub Actions Workflow for Node.js CI

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-travis-ci-to-github-actions

This GitHub Actions workflow defines a continuous integration pipeline for Node.js projects. It checks out the repository, sets up a specified Node.js version (16.x), installs dependencies using npm, builds the project, and then runs tests.

```yaml
name: Node.js CI
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - name: Use Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '16.x'
      - run: npm install
      - run: npm run build
      - run: npm test
```

--------------------------------

### Reuse Complete Job Configuration with YAML Anchors

Source: https://docs.github.com/en/actions/reference/reusable-workflows-reference

Use YAML anchors to define and reuse an entire job configuration across multiple jobs in a workflow. This approach is useful for complex job setups with multiple steps, environment variables, and settings that need to be replicated with minimal changes.

```yaml
jobs:
  test: &base_job # Define the anchor on first use
    runs-on: ubuntu-latest
    timeout-minutes: 30
    env:
      NODE_VERSION: '18'
    steps:
      - uses: actions/checkout@v5
      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: ${{ env.NODE_VERSION }}
      - run: npm test

  alt-test: *base_job # Reuse the entire job configuration
```

--------------------------------

### GitHub Actions workflow for Pester testing in PowerShell

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/powershell

A complete workflow file that runs Pester tests on Ubuntu when code is pushed to the repository. The workflow checks for a results file and executes tests from a Pester test file using the pwsh shell. This example demonstrates basic test validation with Should assertions and Invoke-Pester command execution.

```yaml
name: Test PowerShell on Ubuntu
on: push

jobs:
  pester-test:
    name: Pester test
    runs-on: ubuntu-latest
    steps:
      - name: Check out repository code
        uses: actions/checkout@v5
      - name: Perform a Pester test from the command-line
        shell: pwsh
        run: Test-Path resultsfile.log | Should -Be $true
      - name: Perform a Pester test from the Tests.ps1 file
        shell: pwsh
        run: |
          Invoke-Pester Unit.Tests.ps1 -Passthru
```

--------------------------------

### Cache npm dependencies with setup-node action

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Configures GitHub Actions workflow to cache npm dependencies using the setup-node action with Node.js version 20. This reduces build time by reusing cached dependencies across workflow runs. Requires actions/checkout and actions/setup-node actions.

```yaml
steps:
- uses: actions/checkout@v5
- uses: actions/setup-node@v4
  with:
    node-version: '20'
    cache: 'npm'
- run: npm install
- run: npm test
```

--------------------------------

### Exclude Branches from workflow_run Trigger

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

Uses on.workflow_run with branches-ignore filter to prevent workflow execution on specific branches. Cannot be combined with branches filter for the same event. The example excludes the 'canary' branch from triggering the workflow.

```yaml
on:
  workflow_run:
    workflows: ["Build"]
    types: [requested]
    branches-ignore:
      - "canary"
```

--------------------------------

### Build Xamarin.Android Application with GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/xamarin-apps

This GitHub Actions workflow demonstrates how to build a Xamarin.Android application. It configures specific Xamarin SDK versions on a macOS runner, sets up the .NET Core SDK, restores NuGet dependencies, and then compiles and packages the Android project using MSBuild. The workflow requires a solution file path (`<sln_file_path>`) and a project file path (`<csproj_file_path>`) as inputs for the restore and build steps.

```yaml
name: Build Xamarin.Android app

on: [push]

jobs:
  build:

    runs-on: macos-latest

    steps:
    - uses: actions/checkout@v5
    - name: Set default Xamarin SDK versions
      run: |
        $VM_ASSETS/select-xamarin-sdk-v2.sh --mono=6.10 --android=10.2

    - name: Setup .NET Core SDK 5.0.x
      uses: actions/setup-dotnet@v4
      with:
        dotnet-version: '5.0.x'

    - name: Install dependencies
      run: nuget restore <sln_file_path>

    - name: Build
      run: msbuild <csproj_file_path> /t:PackageForAndroid /p:Configuration=Debug
```

--------------------------------

### Add Directory to System PATH in GitHub Actions (Bash)

Source: https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions

Prepends a directory to the system PATH variable using Bash, making it available to all subsequent actions in the current job. This example adds the user's local bin directory ($HOME/.local/bin) to PATH by appending to the GITHUB_PATH environment variable.

```bash
echo "$HOME/.local/bin" >> "$GITHUB_PATH"
```

--------------------------------

### Configure GitHub Actions for Binary SBOM Attestation

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/use-artifact-attestations

This snippet details how to configure a GitHub Actions workflow to generate signed Software Bill of Materials (SBOM) attestations for binaries. It includes the necessary permissions (`id-token`, `contents`, `attestations`) and a step using `actions/attest-sbom@v2`. The action requires `subject-path` for the binary and `sbom-path` for the generated SBOM file.

```yaml
permissions:
  id-token: write
  contents: read
  attestations: write
```

```yaml
- name: Generate SBOM attestation
  uses: actions/attest-sbom@v2
  with:
    subject-path: 'PATH/TO/ARTIFACT'
    sbom-path: 'PATH/TO/SBOM'
```

--------------------------------

### Add Directory to System PATH in GitHub Actions

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Prepends a directory to the system PATH variable, making it available to all subsequent actions in the current job. This example demonstrates adding the user's local bin directory to PATH using both Bash and PowerShell approaches.

```bash
echo "$HOME/.local/bin" >> "$GITHUB_PATH"
```

```powershell
"$env:HOMEPATH/.local/bin" | Out-File -FilePath "$env:GITHUB_PATH" -Append
```

--------------------------------

### Kubernetes Pod Template Spec with Init Containers

Source: https://docs.github.com/en/actions/tutorials/use-actions-runner-controller/deploy-runner-scale-sets

Defines a Kubernetes PodSpec with three init containers that set up Docker-in-Docker (Dind) environment. The first container copies external files, the second configures rootless Docker user/group settings, and the third starts the Docker daemon. Includes security contexts, volume mounts, and startup probes for container health checking.

```yaml
template:
  spec:
    initContainers:
    - name: init-dind-externals
      image: ghcr.io/actions/actions-runner:latest
      command: ["cp", "-r", "/home/runner/externals/.", "/home/runner/tmpDir/"]
      volumeMounts:
        - name: dind-externals
          mountPath: /home/runner/tmpDir
    - name: init-dind-rootless
      image: docker:dind-rootless
      command:
        - sh
        - -c
        - |
          set -x
          cp -a /etc/. /dind-etc/
          echo 'runner:x:1001:1001:runner:/home/runner:/bin/ash' >> /dind-etc/passwd
          echo 'runner:x:1001:' >> /dind-etc/group
          echo 'runner:100000:65536' >> /dind-etc/subgid
          echo 'runner:100000:65536' >> /dind-etc/subuid
          chmod 755 /dind-etc;
          chmod u=rwx,g=rx+s,o=rx /dind-home
          chown 1001:1001 /dind-home
      securityContext:
        runAsUser: 0
      volumeMounts:
        - mountPath: /dind-etc
          name: dind-etc
        - mountPath: /dind-home
          name: dind-home
    - name: dind
      image: docker:dind-rootless
      args:
        - dockerd
        - --host=unix:///run/user/1001/docker.sock
      securityContext:
        privileged: true
        runAsUser: 1001
        runAsGroup: 1001
      restartPolicy: Always
      startupProbe:
        exec:
          command:
            - docker
            - info
        initialDelaySeconds: 0
        failureThreshold: 24
        periodSeconds: 5
      volumeMounts:
        - name: work
          mountPath: /home/runner/_work
        - name: dind-sock
          mountPath: /run/user/1001
        - name: dind-externals
          mountPath: /home/runner/externals
        - name: dind-etc
          mountPath: /etc
        - name: dind-home
          mountPath: /home/runner
```

--------------------------------

### npm Registry Configuration File (.npmrc)

Source: https://docs.github.com/en/actions/publishing-packages/publishing-nodejs-packages

Configuration file generated by the setup-node action that configures npm authentication and registry settings. The NODE_AUTH_TOKEN environment variable is referenced for authentication, and always-auth is enabled to ensure credentials are sent with all requests to the npm registry.

```text
//registry.npmjs.org/:_authToken=${NODE_AUTH_TOKEN}
registry=https://registry.npmjs.org/
always-auth=true
```

--------------------------------

### Filter files by path patterns for push events in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow

Configure a GitHub Actions workflow to run only when specific file paths are changed using the `paths` filter with glob patterns. This example triggers the workflow when any JavaScript file is pushed to the repository.

```yaml
on:
  push:
    paths:
      - '**.js'
```

--------------------------------

### Define Workflow Steps for GitHub Actions Job Interacting with Redis (YAML)

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-redis-service-containers

This YAML snippet outlines the `steps` within a GitHub Actions job. It includes checking out the repository code, installing Node.js dependencies using `npm ci`, and running a `node client.js` script. Environment variables `REDIS_HOST` and `REDIS_PORT` are set for the `Connect to Redis` step, allowing the script to communicate with the Redis service container.

```yaml
steps:
  # Downloads a copy of the code in your repository before running CI tests
  - name: Check out repository code
    uses: actions/checkout@v5

  # Performs a clean installation of all dependencies in the `package.json` file
  # For more information, see https://docs.npmjs.com/cli/ci.html
  - name: Install dependencies
    run: npm ci

  - name: Connect to Redis
    # Runs a script that creates a Redis client, populates
    # the client with data, and retrieves data
    run: node client.js
    # Environment variable used by the `client.js` script to create
    # a new Redis client.
    env:
      # The hostname used to communicate with the Redis service container
      REDIS_HOST: localhost
      # The default Redis port
      REDIS_PORT: 6379
```

--------------------------------

### Pull Request Workflow - File Path Filter

Source: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows

Configure a workflow to run when a pull request modifies specific file types. This example triggers the workflow whenever JavaScript files are changed in a pull request.

```APIDOC
## Pull Request Workflow - File Path Filter

### Description
Trigger a workflow when a pull request includes changes to specific file paths or patterns.

### Event Type
`pull_request`

### Configuration
```yaml
on:
  pull_request:
    paths:
      - '**.js'
```

### Parameters
- **paths** (array) - Optional - File path patterns that trigger the workflow. Supports glob patterns.

### Use Cases
- Run tests only when source code files change
- Deploy only when configuration files are modified
- Trigger linting on specific file types

### Notes
- Glob patterns support `**` for recursive matching
- Multiple path patterns can be specified
- Workflow runs only when both branches and paths filters are satisfied (if both are specified)
```

--------------------------------

### Configure Workflow-Level GITHUB_TOKEN Permissions in GitHub Actions (YAML)

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates how to set `GITHUB_TOKEN` permissions at the top level of a GitHub Actions workflow, applying the `read-all` setting to all jobs within the workflow. This provides a global permission configuration for the entire workflow.

```yaml
name: "My workflow"

on: [ push ]

permissions: read-all

jobs:
  ...
```

--------------------------------

### Example: Docker Permission Denied Error

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/monitoring-and-troubleshooting-self-hosted-runners

This error message indicates a permission issue when the self-hosted runner attempts to connect to the Docker daemon socket. It suggests that the user account running the runner service lacks the necessary permissions to interact with Docker.

```text
dial unix /var/run/docker.sock: connect: permission denied
```

--------------------------------

### Define GitHub Actions Matrix Jobs Solely with `include`

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates using the `include` keyword as the exclusive source for defining matrix jobs, without specifying any base matrix variables. The workflow will run a job for each entry listed under `include`. This approach is beneficial when you need to define a fixed set of distinct job configurations without the combinatorial expansion of a traditional matrix.

```yaml
jobs:
  includes_only:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        include:
          - site: "production"
            datacenter: "site-a"
          - site: "staging"
            datacenter: "site-b"

```

--------------------------------

### Filter GitHub Actions Job Logs with Grep via GitHub CLI

Source: https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/using-workflow-run-logs

This command demonstrates how to pipe the output of GitHub CLI's log viewing into `grep` to filter for specific keywords. In this example, it searches for log entries containing the word 'error' for a given `JOB_ID`, which is useful for debugging and pinpointing issues.

```shell
gh run view --job JOB_ID --log | grep error
```

--------------------------------

### Access GitHub Actions Context Variables in Workflow

Source: https://docs.github.com/en/actions/reference/variables-reference

Demonstrates how to access default environment variables using GitHub Actions context syntax within workflow steps. The example shows accessing the GITHUB_REF variable through the context property instead of the environment variable directly, which is the recommended approach for workflow processing.

```yaml
- name: Print GitHub Reference
  run: echo "The branch or tag ref is ${{ github.ref }}"

- name: Print GitHub Actor
  run: echo "Workflow triggered by ${{ github.actor }}"

- name: Print GitHub Event Name
  run: echo "Event that triggered workflow: ${{ github.event_name }}"
```

--------------------------------

### Define GitHub Action Entrypoint Script (Shell)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-docker-container-action

This shell script serves as the entrypoint for a GitHub Action. It prints a greeting using an input variable and captures the current time, exporting it as a GitHub Action output variable named `time` by writing to `$GITHUB_OUTPUT`. This allows subsequent workflow steps to consume the `time` value.

```Shell
#!/bin/sh -l

echo "Hello $1"
time=$(date)
echo "time=$time" >> $GITHUB_OUTPUT

```

--------------------------------

### Job dependencies in GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-azure-pipelines-to-github-actions

Demonstrates how to define job dependencies in GitHub Actions using the 'needs' key. The example creates an equivalent workflow to Azure Pipelines with an initial job, parallel fanout jobs, and a final job depending on multiple predecessors.

```yaml
jobs:
  initial:
    runs-on: ubuntu-latest
    steps:
      - run: echo "This job will be run first."
  fanout1:
    runs-on: ubuntu-latest
    needs: initial
    steps:
      - run: echo "This job will run after the initial job, in parallel with fanout2."
  fanout2:
    runs-on: ubuntu-latest
    needs: initial
    steps:
      - run: echo "This job will run after the initial job, in parallel with fanout1."
  fanin:
    runs-on: ubuntu-latest
    needs: [fanout1, fanout2]
    steps:
      - run: echo "This job will run after fanout1 and fanout2 have finished."
```

--------------------------------

### Referencing a Docker Container Image as a GitHub Action

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/find-and-customize-actions

This YAML snippet shows how to use a published Docker container image from Docker Hub directly as an action in a GitHub workflow. It employs the `docker://{image}:{tag}` syntax to specify the container, for example, `docker://alpine:3.8`.

```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: docker://alpine:3.8
```

--------------------------------

### Deserialize JSON string to object for matrix strategy in GitHub Actions (YAML)

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/expressions

This example illustrates using `fromJSON` to parse a JSON string output from a previous job into a usable JSON object for a matrix strategy. It demonstrates passing complex data structures between jobs in a GitHub Actions workflow.

```yaml
name: build
on: push
jobs:
  job1:
    runs-on: ubuntu-latest
    outputs:
      matrix: ${{ steps.set-matrix.outputs.matrix }}
    steps:
      - id: set-matrix
        run: echo "matrix={"include":[{"project":"foo","config":"Debug"},{"project":"bar","config":"Release"}]}" >> $GITHUB_OUTPUT
  job2:
    needs: job1
    runs-on: ubuntu-latest
    strategy:
      matrix: ${{ fromJSON(needs.job1.outputs.matrix) }}
    steps:
      - run: echo "Matrix - Project ${{ matrix.project }}, Config ${{ matrix.config }}"
```

--------------------------------

### Environment Variable Script Injection Test Example

Source: https://docs.github.com/en/actions/reference/security/secure-use

Demonstrates a test case showing how the environment variable approach prevents script injection attacks. When a malicious payload is assigned to the TITLE variable, it is treated as literal text rather than executable code, resulting in safe handling and proper error output.

```yaml
env:
  TITLE: a"; ls $GITHUB_WORKSPACE"
PR title did not start with 'octocat'
```

--------------------------------

### Exclude Branches from workflow_run Trigger

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow

Shows how to use the branches-ignore filter to exclude specific branches from triggering a workflow. In this example, the workflow will run on any branch except 'canary'. Note that branches and branches-ignore filters cannot be used together for the same event.

```yaml
on:
  workflow_run:
    workflows: ["Build"]
    types: [requested]
    branches-ignore:
      - "canary"
```

--------------------------------

### Write to GITHUB_STATE file in JavaScript

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Demonstrates how to write environment variables to the GITHUB_STATE file using Node.js fs module. The saved value becomes accessible as an environment variable with the STATE_ prefix in subsequent actions. This example creates a STATE_processID variable with value 12345.

```javascript
import * as fs from 'fs'
import * as os from 'os'

fs.appendFileSync(process.env.GITHUB_STATE, `processID=12345${os.EOL}`, {
  encoding: 'utf8'
})
```

--------------------------------

### Use a Public GitHub Action in Workflow (YAML)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-docker-container-action

This workflow demonstrates how to integrate a public GitHub Action, such as 'actions/hello-world-docker-action', into your repository. It defines a job that runs on 'ubuntu-latest', uses the specified action with an input, and then retrieves and displays an output from that action. This code should be placed in a `.github/workflows/main.yml` file.

```yaml
on: [push]

jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: A job to say hello
    steps:
      - name: Hello world action step
        id: hello
        uses: actions/hello-world-docker-action@v2
        with:
          who-to-greet: 'Mona the Octocat'
      # Use the output from the `hello` step
      - name: Get the output time
        run: echo "The time was ${{ steps.hello.outputs.time }}"
```

--------------------------------

### Example Contents of the Environment Context (JSON)

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

This JSON snippet illustrates the structure of the `env` context, which holds custom environment variables defined within a workflow, job, or step. It shows how variable names map to their string values, emphasizing that its contents are dynamic and specific to its point of access in the workflow.

```json
{
  "first_name": "Mona",
  "super_duper_var": "totally_awesome"
}
```

--------------------------------

### Use Public Docker Registry Action (Google Container Registry)

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates how to use a Docker image from a generic public registry, specifically Google Container Registry (`gcr.io`), as an action within a GitHub Actions workflow. The `uses` keyword points to the Docker image path, allowing the workflow to execute the containerized tool. This showcases flexibility in sourcing actions from various container registries.

```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: docker://gcr.io/cloud-builders/gradle
```

--------------------------------

### jobs.<job_id>.steps[*].if

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

A conditional statement that prevents a step from running unless a condition is met. Supports any context and expression, with optional ${{ }} expression syntax unless the expression starts with ! (which requires explicit syntax).

```APIDOC
## jobs.<job_id>.steps[*].if

### Description
You can use the `if` conditional to prevent a step from running unless a condition is met. You can use any supported context and expression to create a conditional.

### Expression Syntax
- Optional `${{ }}` expression syntax can be omitted in most cases
- GitHub Actions automatically evaluates the `if` conditional as an expression
- Exception: Must always use `${{ }}` syntax or escape with `''`, `""`, or `()` when expression starts with `!`
- The `!` character is reserved notation in YAML format

### Example: Conditional with Negation

```yaml
if: ${{ ! startsWith(github.ref, 'refs/tags/') }}
```

### Notes
- For supported contexts in this key, see Contexts reference
- For more information on expressions, see Evaluate expressions in workflows and actions
```

--------------------------------

### Define Job Dependencies with needs in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Use the needs keyword to specify job dependencies, ensuring jobs run sequentially in the correct order. This example shows job1 must complete before job2, and job3 waits for both job1 and job2 to complete successfully.

```yaml
jobs:
  job1:
  job2:
    needs: job1
  job3:
    needs: [job1, job2]
```

--------------------------------

### Define Post-Action Hook for Cleanup in GitHub Actions

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This example illustrates how to use the `post` hook in a GitHub Action to run a cleanup script after the main action has completed. The `post: 'cleanup.js'` directive ensures that `cleanup.js` is executed, regardless of the main action's success or failure. This is useful for releasing resources or performing finalization steps.

```yaml
runs:
  using: 'node24'
  main: 'index.js'
  post: 'cleanup.js'
```

--------------------------------

### Configure GitHub Actions Job with Windows Runner Label

Source: https://docs.github.com/en/actions/how-tos/manage-runners/larger-runners/use-larger-runners_platform=linux

Sets up a GitHub Actions workflow that routes a job to a Windows runner with the `windows-2022-16core` label. The workflow performs the same operations as the Ubuntu example but executes on a Windows 2022 larger runner with 16 cores.

```yaml
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on:
      labels: windows-2022-16core
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v
```

--------------------------------

### Define a Custom Transformer for a JavaScript Build Step in Ruby

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/extending-github-actions-importer-with-custom-transformers

This Ruby DSL example provides a custom transformer that converts a build step identified as 'buildJavaScriptApp' into a GitHub Actions workflow step. It maps the original item to a sequence of `npm` commands, demonstrating how to define custom logic for converting existing build steps.

```ruby
transform "buildJavaScriptApp" do |item|
  command = ["build", "package", "deploy"].map do |script|
    "npm run #{script}"
  end

  {
    name: "build javascript app",
    run: command.join("\n")
  }
end
```

--------------------------------

### Filter pull_request_target by Target Branch Pattern

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

Configure a workflow to run only when pull requests target branches matching a specific pattern, such as branches starting with 'releases/'. Uses the branches filter to specify target branch patterns.

```yaml
on:
  pull_request_target:
    types:
      - opened
    branches:
      - 'releases/**'
```

--------------------------------

### Access Context Properties Using Index and Property Syntax

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

Demonstrates two methods to access context information in GitHub Actions expressions. Index syntax uses bracket notation while property dereference syntax uses dot notation. Property names must start with a letter or underscore and contain only alphanumeric characters, hyphens, or underscores for dereference syntax.

```yaml
# Index syntax
github['sha']

# Property dereference syntax
github.sha
```

--------------------------------

### Configure GitHub App Credentials in values.yaml

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

Specifies GitHub App authentication credentials directly in the values.yaml file, including app ID, installation ID, and private key. This approach is less secure than using Kubernetes secrets and should only be used when necessary, as it exposes private keys in plain text.

```yaml
githubConfigSecret:
  github_app_id: "123456"
  github_app_installation_id: "654321"
  github_app_private_key: |
    -----BEGIN RSA PRIVATE KEY-----
    ...
    HkVN9...
    ...
    -----END RSA PRIVATE KEY-----
```

--------------------------------

### Define Job Dependencies with needs

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Use the needs keyword to specify job dependencies, ensuring jobs run in the correct order. Jobs listed in needs must complete successfully before the dependent job runs. This example shows sequential job execution with multiple dependency chains.

```APIDOC
## jobs.<job_id>.needs - Job Dependencies

### Description
Identify jobs that must complete successfully before the current job will run.

### Configuration Key
jobs.<job_id>.needs

### Value Type
String or array of strings

### Example: Sequential Job Execution
```yaml
jobs:
  job1:
  job2:
    needs: job1
  job3:
    needs: [job1, job2]
```

### Execution Order
1. job1 - Runs first
2. job2 - Runs after job1 completes successfully
3. job3 - Runs after both job1 and job2 complete successfully

### Dependency Rules
- If a job fails or is skipped, all jobs that need it are skipped
- A failure or skip applies to all jobs in the dependency chain from that point onwards
- Use conditional expressions to override this behavior

### Notes
- Single dependency: `needs: job1`
- Multiple dependencies: `needs: [job1, job2]`
- Dependencies must complete successfully unless conditional expressions are used
```

--------------------------------

### Conditional Step Execution in GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-travis-ci-to-github-actions

Use `if` conditionals to control whether a step executes based on environment variables or expressions. This example runs a step only when specific conditions are met (string equals 'ABC' and number equals 123).

```yaml
jobs:
  conditional:
    runs-on: ubuntu-latest
    steps:
      - run: echo "This step runs with str equals 'ABC' and num equals 123"
        if: env.str == 'ABC' && env.num == 123
```

--------------------------------

### Create Custom GitHub Actions ARC Runner Image with Dockerfile

Source: https://docs.github.com/en/actions/concepts/runners/about-actions-runner-controller

This Dockerfile provides a template for building a custom GitHub Actions self-hosted runner image for Actions Runner Controller (ARC). It sets up the runner environment, installs necessary dependencies, downloads and extracts the runner binaries and container hooks, and configures user permissions. Users must replace the `RUNNER_VERSION` and `RUNNER_CONTAINER_HOOKS_VERSION` arguments with the latest release versions.

```Dockerfile
FROM mcr.microsoft.com/dotnet/runtime-deps:6.0 as build

# Replace value with the latest runner release version
# source: https://github.com/actions/runner/releases
# ex: 2.303.0
ARG RUNNER_VERSION=""
ARG RUNNER_ARCH="x64"
# Replace value with the latest runner-container-hooks release version
# source: https://github.com/actions/runner-container-hooks/releases
# ex: 0.3.1
ARG RUNNER_CONTAINER_HOOKS_VERSION=""

ENV DEBIAN_FRONTEND=noninteractive
ENV RUNNER_MANUALLY_TRAP_SIG=1
ENV ACTIONS_RUNNER_PRINT_LOG_TO_STDOUT=1

RUN apt update -y && apt install curl unzip -y

RUN adduser --disabled-password --gecos "" --uid 1001 runner \
    && groupadd docker --gid 123 \
    && usermod -aG sudo runner \
    && usermod -aG docker runner \
    && echo "%sudo ALL=(ALL:ALL) NOPASSWD:ALL" > /etc/sudoers \
    && echo "Defaults env_keep += \"DEBIAN_FRONTEND\"" >> /etc/sudoers

WORKDIR /home/runner

RUN curl -f -L -o runner.tar.gz https://github.com/actions/runner/releases/download/v${RUNNER_VERSION}/actions-runner-linux-${RUNNER_ARCH}-${RUNNER_VERSION}.tar.gz \
    && tar xzf ./runner.tar.gz \
    && rm runner.tar.gz

RUN curl -f -L -o runner-container-hooks.zip https://github.com/actions/runner-container-hooks/releases/download/v${RUNNER_CONTAINER_HOOKS_VERSION}/actions-runner-hooks-k8s-${RUNNER_CONTAINER_HOOKS_VERSION}.zip \
    && unzip ./runner-container-hooks.zip -d ./k8s \
    && rm runner-container-hooks.zip

USER runner
```

--------------------------------

### Configure GitHub Repository URL for Runner Deployment

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

Sets the GitHub configuration URL to specify where runner scale sets should be deployed. This can point to a repository, organization, or enterprise level. The example demonstrates deploying runners to a specific repository within an organization.

```yaml
githubConfigUrl: "https://github.com/octo-ent/octo-org/octo-repo"
```

--------------------------------

### Generate package.json with npm

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

Create a package.json file with default values using npm init. This file tracks project metadata and dependencies required for the JavaScript action.

```shell
npm init -y
```

--------------------------------

### Cache Dependencies - CircleCI YAML Syntax

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-circleci

CircleCI caching syntax using restore_cache with checksum-based keys for npm dependencies. This example restores cached node modules based on package-lock.json checksums, falling back to a general cache key if exact match not found.

```yaml
- restore_cache:
    keys:
      - v1-npm-deps-{{ checksum "package-lock.json" }}
      - v1-npm-deps-
```

--------------------------------

### Docker Image Build and Push Step

Source: https://docs.github.com/en/actions/tutorials/publish-packages/publish-docker-images

Builds the Docker image from the Dockerfile and pushes it to the container registry. Uses context parameter to define build files and applies tags and labels from the metadata step.

```yaml
- name: Build and push Docker image
  id: push
  uses: docker/build-push-action@f2a1d5e99d037542a71f64918e516c093c6f3fc4
  with:
    context: .
    push: true
    tags: ${{ steps.meta.outputs.tags }}
    labels: ${{ steps.meta.outputs.labels }}
```

--------------------------------

### Define Script Steps in Azure Pipelines and GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-azure-pipelines

These examples demonstrate how to configure script execution within CI/CD workflows for both Azure Pipelines and GitHub Actions. Azure Pipelines uses specific keys like `script`, `bash`, `pwsh`, or a `PowerShell@2` task for different shells, while GitHub Actions uses a universal `run` key with an optional `shell` specifier to define the execution environment.

```yaml
jobs:
  - job: scripts
    pool:
      vmImage: 'windows-latest'
    steps:
      - script: echo "This step runs in the default shell"
      - bash: echo "This step runs in bash"
      - pwsh: Write-Host "This step runs in PowerShell Core"
      - task: PowerShell@2
        inputs:
          script: Write-Host "This step runs in PowerShell"

```

```yaml
jobs:
  scripts:
    runs-on: windows-latest
    steps:
      - run: echo "This step runs in the default shell"
      - run: echo "This step runs in bash"
        shell: bash
      - run: Write-Host "This step runs in PowerShell Core"
        shell: pwsh
      - run: Write-Host "This step runs in PowerShell"
        shell: powershell

```

--------------------------------

### Repository dispatch event payload for matrix configuration

Source: https://docs.github.com/en/actions/how-tos/writing-workflows/choosing-what-your-workflow-does/running-variations-of-jobs-in-a-workflow

Example JSON payload sent via repository dispatch webhook that contains version values used to dynamically configure the matrix strategy. This demonstrates how external events can drive workflow matrix generation.

```json
{
  "event_type": "test",
  "client_payload": {
    "versions": [12, 14, 16]
  }
}
```

--------------------------------

### Specify Multiple Custom Transformer Files with GitHub Actions Importer CLI using Glob

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/extending-github-actions-importer-with-custom-transformers

This example illustrates how to use a glob pattern with the `--custom-transformers` CLI option to include multiple Ruby transformer files from a specified directory. This is useful for organizing and applying several custom mapping definitions to `gh actions-importer` commands.

```bash
gh actions-importer ... --custom-transformers transformers/*.rb
```

--------------------------------

### Deploy Application to GKE Cluster using Kustomize and Kubectl

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/google-kubernetes-engine

This sequence of commands performs the actual deployment to the GKE cluster. It first uses Kustomize to update the image tag in the Kubernetes manifests, then builds the final YAML configuration, pipes it to 'kubectl apply' for deployment, waits for the deployment rollout to complete, and finally lists the deployed services for verification.

```bash
./kustomize edit set image gcr.io/PROJECT_ID/IMAGE:TAG=gcr.io/$PROJECT_ID/$IMAGE:$GITHUB_SHA
./kustomize build . | kubectl apply -f -
kubectl rollout status deployment/$DEPLOYMENT_NAME
kubectl get services -o wide
```

--------------------------------

### Function: prepare_job

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/customize-containers

Describes the input arguments for the `prepare_job` function, which configures job and service containers in GitHub Actions.

```APIDOC
## Function: prepare_job

### Description
This section details the arguments required to configure a job and its associated services within a GitHub Actions workflow. It covers container specifications, environment setup, and volume management.

### Method
N/A

### Endpoint
N/A

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
- **jobContainer** (object) - Optional - An object containing information about the specified job container.
    - **image** (string) - Required - A string containing the Docker image.
    - **workingDirectory** (string) - Required - A string containing the absolute path of the working directory.
    - **createOptions** (string) - Optional - The optional _create_ options specified in the YAML. For more information, see Running jobs in a container.
    - **environmentVariables** (object) - Optional - Sets a map of key environment variables.
    - **userMountVolumes** (array of objects) - Optional - An array of user mount volumes set in the YAML. For more information, see Running jobs in a container.
        - **sourceVolumePath** (string) - Required - The source path to the volume that will be mounted into the Docker container.
        - **targetVolumePath** (string) - Required - The target path to the volume that will be mounted into the Docker container.
        - **readOnly** (boolean) - Required - Determines whether or not the mount should be read-only.
    - **systemMountVolumes** (array of objects) - Required - An array of mounts to mount into the container, same fields as `userMountVolumes`.
    - **registry** (object) - Optional - The Docker registry credentials for a private container registry.
        - **username** (string) - Optional - The username of the registry account.
        - **password** (string) - Optional - The password to the registry account.
        - **serverUrl** (string) - Optional - The registry URL.
    - **portMappings** (object) - Optional - A key value hash of _source:target_ ports to map into the container.
- **services** (array of objects) - Optional - An array of service containers to spin up.
    - **contextName** (string) - Required - The name of the service in the Job context.
    - **image** (string) - Required - A string containing the Docker image.
    - **createOptions** (string) - Optional - The optional _create_ options specified in the YAML. For more information, see Running jobs in a container.
    - **environmentVariables** (object) - Optional - Sets a map of key environment variables.
    - **userMountVolumes** (array of objects) - Optional - An array of mounts to mount into the container, same fields as `jobContainer.userMountVolumes`.
    - **registry** (object) - Optional - The Docker registry credentials for the private container registry, same fields as `jobContainer.registry`.
    - **portMappings** (object) - Optional - A key value hash of _source:target_ ports to map into the container, same fields as `jobContainer.portMappings`.

### Request Example
```json
{
  "jobContainer": {
    "image": "ubuntu:latest",
    "workingDirectory": "/app",
    "createOptions": "--network host",
    "environmentVariables": {
      "NODE_ENV": "production"
    },
    "userMountVolumes": [
      {
        "sourceVolumePath": "/host/path",
        "targetVolumePath": "/container/path",
        "readOnly": false
      }
    ],
    "systemMountVolumes": [
      {
        "sourceVolumePath": "/sys/path",
        "targetVolumePath": "/sys/container/path",
        "readOnly": true
      }
    ],
    "registry": {
      "username": "myuser",
      "password": "mypassword",
      "serverUrl": "docker.io"
    },
    "portMappings": {
      "8080": "80"
    }
  },
  "services": [
    {
      "contextName": "my-db",
      "image": "postgres:13",
      "createOptions": "--shm-size=256m",
      "environmentVariables": {
        "POSTGRES_DB": "mydb"
      },
      "userMountVolumes": [
        {
          "sourceVolumePath": "/data/db",
          "targetVolumePath": "/var/lib/postgresql/data",
          "readOnly": false
        }
      ],
      "registry": {
        "username": "dbuser",
        "password": "dbpassword",
        "serverUrl": "myregistry.com"
      },
      "portMappings": {
        "5432": "5432"
      }
    }
  ]
}
```

### Response
N/A

#### Success Response (200)
N/A

#### Response Example
N/A
```

--------------------------------

### Pass Specific Secret to Nested Workflow

Source: https://docs.github.com/en/actions/how-tos/reuse-automations/reuse-workflows

Demonstrates selective secret passing to a nested workflow by explicitly mapping individual secrets. In this example, workflow B passes only the `personal_access_token` secret to workflow C, while other secrets passed to B are not forwarded.

```yaml
jobs:
  workflowB-calls-workflowC:
    uses: different-org/example-repo/.github/workflows/C.yml@main
    secrets:
      repo-token: ${{ secrets.personal_access_token }} # pass just this secret
```

--------------------------------

### Demonstrate Failed Script Injection Attempt in GitHub Actions Environment Variable

Source: https://docs.github.com/en/actions/security-guides/security-hardening-for-github-actions

This snippet shows an example of an attempted script injection into an environment variable within a GitHub Actions workflow. It highlights how the previously defined security measure (using an intermediate environment variable) successfully prevents the malicious script from executing.

```yaml
   env:
     TITLE: a"; ls $GITHUB_WORKSPACE"
```

--------------------------------

### Build and Deploy Azure Static Web App using GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/azure-static-web-app

This GitHub Actions workflow defines a CI/CD pipeline to build and deploy a web application to Azure Static Web Apps. It triggers on 'push' events to the 'main' branch and various 'pull_request' events (opened, synchronize, reopened). The workflow checks out the repository, builds the application, and deploys it using the 'Azure/static-web-apps-deploy' action. It requires 'AZURE_STATIC_WEB_APPS_API_TOKEN' and 'GITHUB_TOKEN' secrets for authentication and defines environment variables for app, API, and output locations.

```yaml
name: Deploy web app to Azure Static Web Apps

env:
  APP_LOCATION: "/" # location of your client code
  API_LOCATION: "api" # location of your api source code - optional
  OUTPUT_LOCATION: "build" # location of client code build output

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main

permissions:
  issues: write
  contents: read
  pull-requests: write

jobs:
  build_and_deploy:
    if: github.event_name == 'push' || (github.event_name == 'pull_request' && github.event.action != 'closed')
    runs-on: ubuntu-latest
    name: Build and Deploy
    steps:
      - uses: actions/checkout@v5
        with:
          submodules: true
      - name: Build And Deploy
        uses: Azure/static-web-apps-deploy@1a947af9992250f3bc2e68ad0754c0b0c11566c9
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          repo_token: ${{ secrets.GITHUB_TOKEN }}
          action: "upload"
          app_location: ${{ env.APP_LOCATION }}
          api_location: ${{ env.API_LOCATION }}
          output_location: ${{ env.OUTPUT_LOCATION }}
```

--------------------------------

### Perform Dry-Run Migration of Bamboo Build Plan

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/bamboo-migration

Run the dry-run command to convert a Bamboo build plan to an equivalent GitHub Actions workflow without opening a pull request. Replace :my_plan_slug with the plan's project and plan key in the format <projectKey>-<planKey> (for example: PAN-SCRIP).

```bash
gh actions-importer dry-run bamboo build --plan-slug :my_plan_slug --output-dir tmp/dry-run
```

--------------------------------

### Conditionally Run Job Based on Head Branch Reference

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

Use the github.head_ref context variable in a conditional statement to execute a job only when the pull request's head branch matches a specific pattern, such as branches starting with 'releases/'.

```yaml
on:
  pull_request_target:
    types:
      - opened
jobs:
  run_if:
    if: startsWith(github.head_ref, 'releases/')
    runs-on: ubuntu-latest
    steps:
      - run: echo "The head of this PR starts with 'releases/'"
```

--------------------------------

### Publish Package to npm Registry with GitHub Actions

Source: https://docs.github.com/en/actions/publishing-packages/publishing-nodejs-packages

GitHub Actions workflow that publishes an npm package to the npm registry when a release is published. The workflow uses the setup-node action to configure npm authentication via NODE_AUTH_TOKEN environment variable and includes provenance flag for supply chain security. Requires NPM_TOKEN secret to be configured in the repository.

```yaml
name: Publish Package to npmjs
on:
  release:
    types: [published]
jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      id-token: write
    steps:
      - uses: actions/checkout@v5
      # Setup .npmrc file to publish to npm
      - uses: actions/setup-node@v4
        with:
          node-version: '20.x'
          registry-url: 'https://registry.npmjs.org'
      - run: npm ci
      - run: npm publish --provenance --access public
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

--------------------------------

### Schedule Workflow with Basic Cron Expression

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

Demonstrates how to configure a GitHub Actions workflow to run at a scheduled time using POSIX cron syntax. This example runs at minute 15 of the 4th and 5th hour UTC daily. The workflow executes on the latest commit of the default branch.

```yaml
on:
  schedule:
    - cron: "15 4,5 * * *"
```

--------------------------------

### Configure workflow_run Event with Branch Filters

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow

Demonstrates how to use the workflow_run event with branch filters to trigger workflows based on specific branch patterns. The example shows filtering for branches matching 'releases/**' pattern. Supports glob patterns with special characters like *, **, +, ?, and ! for pattern matching.

```yaml
on:
  workflow_run:
    workflows: ["Build"]
    types: [requested]
    branches:
      - 'releases/**'
```

--------------------------------

### General GitHub Actions Runner Scale Set Configuration in values.yaml

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

This `values.yaml` snippet provides an example of general configuration parameters for a GitHub Actions runner scale set. It includes settings for the GitHub configuration URL, the Kubernetes secret for authentication, maximum and minimum runner counts for autoscaling, the runner group name, and the runner scale set name. This configuration forms the basis for managing runner deployments.

```yaml
## githubConfigUrl is the GitHub url for where you want to configure runners
## ex: https://github.com/myorg/myrepo or https://github.com/myorg
githubConfigUrl: "https://github.com/actions/actions-runner-controller"

## githubConfigSecret is the k8s secrets to use when auth with GitHub API.
## You can choose to use GitHub App or a PAT token
githubConfigSecret: my-super-safe-secret

## maxRunners is the max number of runners the autoscaling runner set will scale up to.
maxRunners: 5

## minRunners is the min number of idle runners. The target number of runners created will be
## calculated as a sum of minRunners and the number of jobs assigned to the scale set.
minRunners: 0

runnerGroup: "my-custom-runner-group"

## name of the runner scale set to create. Defaults to the helm release name
runnerScaleSetName: "my-awesome-scale-set"

## template is the PodSpec for each runner Pod
```

--------------------------------

### GitHub Actions contains() Function - String and Array Examples

Source: https://docs.github.com/en/actions/reference/evaluate-expressions-in-workflows-and-actions

Demonstrates the contains() function for checking if a string contains a substring or if an array contains an element. Shows usage with plain strings, object filters for issue labels, and combined with fromJSON() for array matching.

```text
contains('Hello world', 'llo')
```

```text
contains(github.event.issue.labels.*.name, 'bug')
```

```text
contains(fromJSON('["push", "pull_request"]'), github.event_name)
```

--------------------------------

### Job dependencies in Azure Pipelines

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-azure-pipelines-to-github-actions

Shows how to define job dependencies in Azure Pipelines using the 'dependsOn' key. The example creates a workflow where an initial job runs first, followed by parallel jobs, and finally a job that depends on multiple predecessors.

```yaml
jobs:
  - job: initial
    pool:
      vmImage: 'ubuntu-latest'
    steps:
      - script: echo "This job will be run first."
  - job: fanout1
    pool:
      vmImage: 'ubuntu-latest'
    dependsOn: initial
    steps:
      - script: echo "This job will run after the initial job, in parallel with fanout2."
  - job: fanout2
    pool:
      vmImage: 'ubuntu-latest'
    dependsOn: initial
    steps:
      - script: echo "This job will run after the initial job, in parallel with fanout1."
  - job: fanin
    pool:
      vmImage: 'ubuntu-latest'
    dependsOn: [fanout1, fanout2]
    steps:
      - script: echo "This job will run after fanout1 and fanout2 have finished."
```

--------------------------------

### Conditionally Execute Steps Based on Secret Presence in GitHub Actions YAML

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates how to conditionally run steps based on whether a secret is set in GitHub Actions. It shows how to pass a secret into a job-level environment variable and then use that variable in `if` conditions to check for its presence or absence.

```YAML
name: Run a step if a secret has been set
on: push
jobs:
  my-jobname:
    runs-on: ubuntu-latest
    env:
      super_secret: ${{ secrets.SuperSecret }}
    steps:
      - if: ${{ env.super_secret != '' }}
        run: echo 'This step will only run if the secret has a value set.'
      - if: ${{ env.super_secret == '' }}
        run: echo 'This step will only run if the secret does not have a value set.'
```

--------------------------------

### Kubernetes PodSpec for GitHub Actions Runner with DIND Setup

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

This Kubernetes PodSpec defines the configuration for a GitHub Actions runner pod. It includes two init containers: one to copy external dependencies and another to set up a rootless Docker-in-Docker (DIND) environment by modifying system files and permissions. The main `runner` container executes the runner script, and a `dind` sidecar container runs the Docker daemon, both configured with specific security contexts and volume mounts for isolated operation.

```yaml
template:
  spec:
    initContainers:
    - name: init-dind-externals
      image: ghcr.io/actions/actions-runner:latest
      command: ["cp", "-r", "/home/runner/externals/.", "/home/runner/tmpDir/"]
      volumeMounts:
        - name: dind-externals
          mountPath: /home/runner/tmpDir
    - name: init-dind-rootless
      image: docker:dind-rootless
      command:
        - sh
        - -c
        - |
          set -x
          cp -a /etc/. /dind-etc/
          echo 'runner:x:1001:1001:runner:/home/runner:/bin/ash' >> /dind-etc/passwd
          echo 'runner:x:1001:' >> /dind-etc/group
          echo 'runner:100000:65536' >> /dind-etc/subgid
          echo 'runner:100000:65536' >> /dind-etc/subuid
          chmod 755 /dind-etc;
          chmod u=rwx,g=rx+s,o=rx /dind-home
          chown 1001:1001 /dind-home
      securityContext:
        runAsUser: 0
      volumeMounts:
        - mountPath: /dind-etc
          name: dind-etc
        - mountPath: /dind-home
          name: dind-home
    containers:
    - name: runner
      image: ghcr.io/actions/actions-runner:latest
      command: ["/home/runner/run.sh"]
      env:
        - name: DOCKER_HOST
          value: unix:///run/user/1001/docker.sock
      securityContext:
        privileged: true
        runAsUser: 1001
        runAsGroup: 1001
      volumeMounts:
        - name: work
          mountPath: /home/runner/_work
        - name: dind-sock
          mountPath: /run/user/1001
    - name: dind
      image: docker:dind-rootless
      args:
        - dockerd
        - --host=unix:///run/user/1001/docker.sock
      securityContext:
        privileged: true
        runAsUser: 1001
        runAsGroup: 1001
      volumeMounts:
        - name: work
          mountPath: /home/runner/_work
        - name: dind-sock
          mountPath: /run/user/1001
        - name: dind-externals
          mountPath: /home/runner/externals
        - name: dind-etc
          mountPath: /etc
        - name: dind-home
          mountPath: /home/runner
    volumes:
    - name: work
      emptyDir: {}
    - name: dind-externals
      emptyDir: {}
    - name: dind-sock
      emptyDir: {}
    - name: dind-etc
      emptyDir: {}
    - name: dind-home
      emptyDir: {}
```

--------------------------------

### Lint Ruby code with RuboCop in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/ruby

This GitHub Actions workflow integrates RuboCop for linting Ruby code. It checks out the repository, sets up a specified Ruby version (e.g., '2.6'), installs dependencies including RuboCop, and then executes RuboCop with the `-f github` formatter. This displays linting errors directly as annotations in the GitHub UI, such as in the 'Files changed' tab of a pull request.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# GitHub recommends pinning actions to a commit SHA.
# To get a newer version, you will need to update the SHA.
# You can also reference a tag or branch, but the action may change without warning.

name: Linting

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - uses: ruby/setup-ruby@ec02537da5712d66d4d50a0f33b7eb52773b5ed1
        with:
          ruby-version: '2.6'
      - run: bundle install
      - name: Rubocop
        run: rubocop -f github
```

--------------------------------

### Docker-in-Docker Pod Template for Kubernetes >= v1.29

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

Complete pod specification for Kubernetes v1.29 and later using sidecar containers to run the Docker daemon. Includes init containers for externals setup, runner container with Docker socket mounting, and dind sidecar with startup probes and privileged security context.

```yaml
template:
  spec:
    initContainers:
      - name: init-dind-externals
        image: ghcr.io/actions/actions-runner:latest
        command: ["cp", "-r", "/home/runner/externals/.", "/home/runner/tmpDir/"]
        volumeMounts:
          - name: dind-externals
            mountPath: /home/runner/tmpDir
      - name: dind
        image: docker:dind
        args:
          - dockerd
          - --host=unix:///var/run/docker.sock
          - --group=$(DOCKER_GROUP_GID)
        env:
          - name: DOCKER_GROUP_GID
            value: "123"
        securityContext:
          privileged: true
        restartPolicy: Always
        startupProbe:
          exec:
            command:
              - docker
              - info
          initialDelaySeconds: 0
          failureThreshold: 24
          periodSeconds: 5
        volumeMounts:
          - name: work
            mountPath: /home/runner/_work
          - name: dind-sock
            mountPath: /var/run
          - name: dind-externals
            mountPath: /home/runner/externals
    containers:
      - name: runner
        image: ghcr.io/actions/actions-runner:latest
        command: ["/home/runner/run.sh"]
        env:
          - name: DOCKER_HOST
            value: unix:///var/run/docker.sock
          - name: RUNNER_WAIT_FOR_DOCKER_IN_SECONDS
            value: "120"
        volumeMounts:
          - name: work
            mountPath: /home/runner/_work
          - name: dind-sock
            mountPath: /var/run
    volumes:
      - name: work
        emptyDir: {}
      - name: dind-sock
        emptyDir: {}
      - name: dind-externals
        emptyDir: {}
```

--------------------------------

### Configure pull_request Workflow with Activity Types

Source: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows

Defines a GitHub Actions workflow that runs on pull_request events filtered by specific activity types. This example triggers the workflow only when a pull request is opened or reopened, rather than on all pull request activities.

```yaml
on:
  pull_request:
    types: [opened, reopened]
```

--------------------------------

### Example `matrix` context object content in GitHub Actions matrix job

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

This JSON snippet displays the content of the `matrix` context object for a specific job within a GitHub Actions matrix. It shows how custom matrix properties, such as `os` and `node`, are reflected in the context for a job executing with `ubuntu-latest` and Node.js version `16`. This context allows steps to adapt based on the current matrix combination.

```json
{
  "os": "ubuntu-latest",
  "node": 16
}
```

--------------------------------

### Generate, mask, and output a secret within a single job

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Demonstrates generating a random secret, masking it with add-mask, and making it available to other steps in the same job via GITHUB_OUTPUT. The secret is protected by masking when referenced in subsequent steps. Examples show both Bash and PowerShell implementations.

```yaml
on: push
jobs:
  generate-a-secret-output:
    runs-on: ubuntu-latest
    steps:
      - id: sets-a-secret
        name: Generate, mask, and output a secret
        run: |
          the_secret=$((RANDOM))
          echo "::add-mask::$the_secret"
          echo "secret-number=$the_secret" >> "$GITHUB_OUTPUT"
      - name: Use that secret output (protected by a mask)
        run: |
          echo "the secret number is ${{ steps.sets-a-secret.outputs.secret-number }}"
```

```yaml
on: push
jobs:
  generate-a-secret-output:
    runs-on: ubuntu-latest
    steps:
      - id: sets-a-secret
        name: Generate, mask, and output a secret
        shell: pwsh
        run: |
          Set-Variable -Name TheSecret -Value (Get-Random)
          Write-Output "::add-mask::$TheSecret"
          "secret-number=$TheSecret" >> $env:GITHUB_OUTPUT
      - name: Use that secret output (protected by a mask)
        shell: pwsh
        run: |
          Write-Output "the secret number is ${{ steps.sets-a-secret.outputs.secret-number }}"
```

--------------------------------

### Conditionally Define Service Container Image in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This snippet shows how to conditionally set the Docker image for a service container based on an expression, such as a workflow option. If the expression evaluates to an empty string, the service will not be started, enabling flexible workflow configurations.

```yaml
services:
  nginx:
    image: ${{ options.nginx == true && 'nginx' || '' }}

```

--------------------------------

### GitHub Actions `if` Conditional with Negation

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

This snippet demonstrates using the `if` conditional in GitHub Actions to prevent a step from running based on a negated expression. It highlights the requirement to use `${{ }}` or escape with quotes when the expression starts with `!` due to YAML's reserved notation.

```yaml
if: ${{ ! startsWith(github.ref, 'refs/tags/') }}
```

--------------------------------

### GET Workflow Status Badge

Source: https://docs.github.com/en/actions/how-tos/monitor-workflows/add-a-status-badge

Retrieve a workflow status badge SVG image that displays the current status of a GitHub Actions workflow. The badge shows whether the workflow is passing or failing on the default branch or a specified branch.

```APIDOC
## GET /actions/workflows/{WORKFLOW-FILE}/badge.svg

### Description
Retrieve an SVG status badge image for a GitHub Actions workflow. The badge displays the current status (passing or failing) of workflow runs. By default, it shows the status of the default branch, but can be customized with query parameters.

### Method
GET

### Endpoint
https://github.com/{OWNER}/{REPOSITORY}/actions/workflows/{WORKFLOW-FILE}/badge.svg

### Parameters
#### Path Parameters
- **OWNER** (string) - Required - The organization or user that owns the repository
- **REPOSITORY** (string) - Required - The name of the repository
- **WORKFLOW-FILE** (string) - Required - The workflow file name or path (e.g., main.yml)

#### Query Parameters
- **branch** (string) - Optional - The branch name to display status for. If not specified, displays status of the default branch
- **event** (string) - Optional - The event type that triggers the workflow (e.g., push, pull_request). Filters badge status to show only runs triggered by this event

### Request Example
https://github.com/github/docs/actions/workflows/main.yml/badge.svg

https://github.com/github/docs/actions/workflows/main.yml/badge.svg?branch=feature-1

https://github.com/github/docs/actions/workflows/main.yml/badge.svg?event=push

### Response
#### Success Response (200)
- **Content-Type** (string) - image/svg+xml - SVG image data representing the workflow status badge
- **Status Indicator** (string) - Visual representation showing either passing (green) or failing (red) status

#### Response Example
SVG image content displaying workflow status badge

### Notes
- Workflow badges in private repositories are not accessible externally
- If no workflow runs exist on the specified branch, the badge displays the status of the most recent run across all branches
- The badge URL can be embedded in Markdown using the image syntax: ![alt text](badge-url)
```

--------------------------------

### Add Directory to System PATH in GitHub Actions (PowerShell)

Source: https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions

Prepends a directory to the system PATH variable using PowerShell, making it available to all subsequent actions in the current job. This example adds the user's local bin directory ($env:HOMEPATH/.local/bin) to PATH by appending to the GITHUB_PATH environment variable.

```powershell
"$env:HOMEPATH/.local/bin" | Out-File -FilePath "$env:GITHUB_PATH" -Append
```

--------------------------------

### Run Command with PowerShell Core (pwsh) in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This snippet illustrates how to use PowerShell Core (`pwsh`) for a `run` step in a GitHub Actions workflow. It configures the step to display the `PATH` environment variable using PowerShell syntax, compatible with both Windows and non-Windows runners where PowerShell Core is installed.

```yaml
steps:
  - name: Display the path
    shell: pwsh
    run: echo ${env:PATH}
```

--------------------------------

### Use Runner Context for Temporary Logs and Artifact Upload (GitHub Actions YAML)

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

Demonstrates a GitHub Actions workflow that leverages the `runner.temp` property to create a temporary directory for storing build logs. It also shows how to conditionally upload these logs as an artifact if the build step fails, providing an example of error handling and artifact management.

```yaml
name: Build
on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - name: Build with logs
        run: |
          mkdir ${{ runner.temp }}/build_logs
          echo "Logs from building" > ${{ runner.temp }}/build_logs/build.logs
          exit 1
      - name: Upload logs on fail
        if: ${{ failure() }}
        uses: actions/upload-artifact@v4
        with:
          name: Build failure logs
          path: ${{ runner.temp }}/build_logs
```

--------------------------------

### GitHub Actions: Using Docker Public Registry Action

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Demonstrates how to use a Docker image from any public Docker registry, such as Google Container Registry, as an action.

```APIDOC
## Configuration: Using a Docker public registry action

### Description
This configuration allows you to use a Docker image from any public Docker registry (e.g., `gcr.io`) as an action in your workflow.

### Method
N/A (Workflow Configuration)

### Endpoint
N/A (Workflow Configuration)

### Parameters
#### Configuration Parameters
- **uses** (string) - Required - The public Docker registry image reference in the format `docker://{host}/{image}:{tag}`.

### Request Example
```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: docker://gcr.io/cloud-builders/gradle
```

### Response
N/A
```

--------------------------------

### Define Inputs for Reusable GitHub Actions Workflow (YAML)

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This YAML example illustrates how to define `inputs` for a reusable GitHub Actions workflow using `on.workflow_call`. It specifies input properties like `description`, `default` value, `required` status, and `type`, and shows how to access the input value within a job.

```yaml
on:
  workflow_call:
    inputs:
      username:
        description: 'A username passed from the caller workflow'
        default: 'john-doe'
        required: false
        type: string

jobs:
  print-username:
    runs-on: ubuntu-latest

    steps:
      - name: Print the input name to STDOUT
        run: echo The username is ${{ inputs.username }}
```

--------------------------------

### Run Tests with pytest and Coverage Reporting

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

Executes pytest tests with code coverage analysis using pytest-cov plugin. Generates JUnit XML format test results and Cobertura XML/HTML coverage reports. Includes doctest module execution for testing embedded documentation examples.

```yaml
steps:
- uses: actions/checkout@v5
- name: Set up Python
  uses: actions/setup-python@v5
  with:
    python-version: '3.x'
- name: Install dependencies
  run: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt
- name: Test with pytest
  run: |
    pip install pytest pytest-cov
    pytest tests.py --doctest-modules --junitxml=junit/test-results.xml --cov=com --cov-report=xml --cov-report=html
```

--------------------------------

### Navigate to Repository Directory - Shell

Source: https://docs.github.com/en/actions/creating-actions/creating-a-composite-action

Change the current working directory to the newly created composite action repository. This command is executed in the terminal to navigate into the hello-world-composite-action folder.

```shell
cd hello-world-composite-action
```

--------------------------------

### Set Job-Level GITHUB_TOKEN Permissions in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Configure permissions for a specific job in a workflow. This example grants write access to issues and pull-requests for the stale job while all other permissions default to none. Job-level permissions override workflow-level settings.

```yaml
jobs:
  stale:
    runs-on: ubuntu-latest

    permissions:
      issues: write
      pull-requests: write

    steps:
      - uses: actions/stale@v10
```

--------------------------------

### Add New GitHub Actions Matrix Configurations with `include`

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This YAML snippet shows how to use the `include` keyword to add entirely new job configurations that are not part of the base matrix combinations. The workflow will run jobs for all combinations of `os` and `version`, plus an additional job specifically for `windows-latest` with `version: 17`. This is useful for testing specific edge cases or unique setups.

```yaml
jobs:
  example_matrix:
    strategy:
      matrix:
        os: [macos-latest, windows-latest, ubuntu-latest]
        version: [12, 14, 16]
        include:
          - os: windows-latest
            version: 17

```

--------------------------------

### Define GitHub Actions Job Container with Shorthand Image (YAML)

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/run-jobs-in-a-container

This YAML snippet shows a simplified way to define a container for a GitHub Actions job by directly providing the image name. It omits the `image` keyword when no other container options are needed. This is useful for quick container setup.

```YAML
jobs:
  container-test-job:
    runs-on: ubuntu-latest
    container: node:18

```

--------------------------------

### Commit, Tag, and Push GitHub Action Files (Git Shell)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-docker-container-action

These Git commands stage, commit, and push the necessary files for a GitHub Action (`action.yml`, `entrypoint.sh`, `Dockerfile`, `README.md`) to a remote repository. It also tags the commit with a version (`v1`) to manage releases, which is a best practice for GitHub Actions. This makes the action available for use.

```Shell
git add action.yml entrypoint.sh Dockerfile README.md
git commit -m "My first action is ready"
git tag -a -m "My first action release" v1
git push --follow-tags

```

--------------------------------

### Access Step Outputs Using steps Context

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

Shows how to use the `steps` context to access outputs from previous steps in a workflow. This example generates a random number in one step and uses it in a conditional statement in a subsequent step, demonstrating how to reference step outputs with `${{ steps.<step_id>.outputs.<output_name> }}`.

```yaml
name: Generate random failure
on: push
jobs:
  randomly-failing-job:
    runs-on: ubuntu-latest
    steps:
      - name: Generate 0 or 1
        id: generate_number
        run: echo "random_number=$(($RANDOM % 2))" >> $GITHUB_OUTPUT
      - name: Pass or fail
        run: |
          if [[ ${{ steps.generate_number.outputs.random_number }} == 0 ]]; then exit 0; else exit 1; fi
```

--------------------------------

### Define job dependencies and execution order

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-gitlab-cicd-to-github-actions

Configure sequential and parallel job execution using stages (GitLab) or needs keyword (GitHub). Jobs in the same stage run in parallel, while dependent jobs wait for prerequisites to complete. This example shows build jobs running in parallel, followed by test and deploy stages.

```GitLab CI/CD
stages:
  - build
  - test
  - deploy

build_a:
  stage: build
  script:
    - echo "This job will run first."

build_b:
  stage: build
  script:
    - echo "This job will run first, in parallel with build_a."

test_ab:
  stage: test
  script:
    - echo "This job will run after build_a and build_b have finished."

deploy_ab:
  stage: deploy
  script:
    - echo "This job will run after test_ab is complete"
```

```GitHub Actions
jobs:
  build_a:
    runs-on: ubuntu-latest
    steps:
      - run: echo "This job will be run first."

  build_b:
    runs-on: ubuntu-latest
    steps:
      - run: echo "This job will be run first, in parallel with build_a"

  test_ab:
    runs-on: ubuntu-latest
    needs: [build_a,build_b]
    steps:
      - run: echo "This job will run after build_a and build_b have finished"

  deploy_ab:
    runs-on: ubuntu-latest
    needs: [test_ab]
    steps:
      - run: echo "This job will run after test_ab is complete"
```

--------------------------------

### Use Init Container to Fix Volume Ownership in Kubernetes

Source: https://docs.github.com/en/actions/tutorials/use-actions-runner-controller/troubleshoot

Implements an alternative solution using initContainers to change mounted volume ownership before the runner container starts. This approach uses chown to recursively set ownership to UID 1001 and GID 123 on the /home/runner/_work directory, bypassing the need to modify the security context when that option is not viable.

```yaml
template:
  spec:
    initContainers:
      - name: kube-init
        image: ghcr.io/actions/actions-runner:latest
        command: ["sudo", "chown", "-R", "1001:123", "/home/runner/_work"]
    volumeMounts:
      - name: work
        mountPath: /home/runner/_work
    containers:
      - name: runner
        image: ghcr.io/actions/actions-runner:latest
        command: ["/home/runner/run.sh"]
```

--------------------------------

### Manually cache Ruby dependencies using actions/cache in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/ruby

This GitHub Actions workflow demonstrates manual caching of Ruby gems using the `actions/cache` action. It specifies `vendor/bundle` as the cache path and generates a cache key based on the runner's OS and a hash of `Gemfile.lock`. After restoring or creating the cache, it configures Bundler to install gems into the specified path.

```yaml
steps:
- uses: actions/cache@v4
  with:
    path: vendor/bundle
    key: ${{ runner.os }}-gems-${{ hashFiles('**/Gemfile.lock') }}
    restore-keys: |
      ${{ runner.os }}-gems-
- name: Bundle install
  run: |
    bundle config path vendor/bundle
    bundle install --jobs 4 --retry 3
```

--------------------------------

### Stop and resume workflow commands in PowerShell

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Demonstrates disabling GitHub Actions workflow command processing in PowerShell using a unique GUID token, then re-enabling it. Allows safe logging of content containing workflow command-like syntax without accidental execution.

```powershell
Write-Output '::warning:: This is a warning message, to demonstrate that commands are being processed.'
$stopMarker = New-Guid
Write-Output "::stop-commands::$stopMarker"
Write-Output '::warning:: This will NOT be rendered as a warning, because stop-commands has been invoked.'
Write-Output "::$stopMarker::"
Write-Output '::warning:: This is a warning again, because stop-commands has been turned off.'
```

--------------------------------

### GitHub Actions Workflow for Azure Login with OIDC

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/oidc-in-azure

This GitHub Actions workflow defines a job that authenticates to Azure using OpenID Connect (OIDC). It sets necessary permissions for `id-token` and `contents`, then uses the `azure/login` action with client, tenant, and subscription IDs from GitHub secrets to establish an Azure CLI session. After successful login, it executes example Azure CLI commands (`az account show`, `az group list`).

```yaml
name: Run Azure Login with OIDC
on: [push]

permissions:
  id-token: write
  contents: read
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: 'Az CLI login'
        uses: azure/login@8c334a195cbb38e46038007b304988d888bf676a
        with:
          client-id: ${{ secrets.AZURE_CLIENT_ID }}
          tenant-id: ${{ secrets.AZURE_TENANT_ID }}
          subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }}

      - name: 'Run az commands'
        run: |
          az account show
          az group list
```

--------------------------------

### Configure Redis service container in GitHub Actions workflow

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-redis-service-containers

Sets up a Redis service container with health checks in a GitHub Actions workflow running on Ubuntu with Node.js. The workflow checks out code, installs dependencies, and connects to Redis using environment variables for hostname and port configuration.

```yaml
name: Redis container example
on: push

jobs:
  # Label of the container job
  container-job:
    # Containers must run in Linux based operating systems
    runs-on: ubuntu-latest
    # Docker Hub image that `container-job` executes in
    container: node:20-bookworm-slim

    # Service containers to run with `container-job`
    services:
      # Label used to access the service container
      redis:
        # Docker Hub image
        image: redis
        # Set health checks to wait until redis has started
        options: >
          --health-cmd "redis-cli ping"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      # Downloads a copy of the code in your repository before running CI tests
      - name: Check out repository code
        uses: actions/checkout@v5

      # Performs a clean installation of all dependencies in the `package.json` file
      # For more information, see https://docs.npmjs.com/cli/ci.html
      - name: Install dependencies
        run: npm ci

      - name: Connect to Redis
        # Runs a script that creates a Redis client, populates
        # the client with data, and retrieves data
        run: node client.js
        # Environment variable used by the `client.js` script to create a new Redis client.
        env:
          # The hostname used to communicate with the Redis service container
          REDIS_HOST: redis
          # The default Redis port
          REDIS_PORT: 6379
```

--------------------------------

### Define job outputs in GitHub Actions workflow

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/pass-job-outputs

Defines outputs for a job by mapping them to step outputs using the jobs.<job_id>.outputs syntax. The example shows job1 with two outputs (output1 and output2) that capture results from step1 and step2 respectively, using echo commands to write to $GITHUB_OUTPUT.

```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    outputs:
      output1: ${{ steps.step1.outputs.test }}
      output2: ${{ steps.step2.outputs.test }}
    steps:
      - id: step1
        run: echo "test=hello" >> "$GITHUB_OUTPUT"
      - id: step2
        run: echo "test=world" >> "$GITHUB_OUTPUT"
```

--------------------------------

### Lint PowerShell Code with PSScriptAnalyzer

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/powershell

Installs PSScriptAnalyzer module and runs it recursively on all .ps1 files in the repository to identify code quality issues. The script categorizes findings by severity level (Error/Warning) and fails the job if errors are detected, ensuring code quality standards are met before deployment.

```yaml
lint-with-PSScriptAnalyzer:
  name: Install and run PSScriptAnalyzer
  runs-on: ubuntu-latest
  steps:
    - uses: actions/checkout@v5
    - name: Install PSScriptAnalyzer module
      shell: pwsh
      run: |
        Set-PSRepository PSGallery -InstallationPolicy Trusted
        Install-Module PSScriptAnalyzer -ErrorAction Stop
    - name: Lint with PSScriptAnalyzer
      shell: pwsh
      run: |
        Invoke-ScriptAnalyzer -Path *.ps1 -Recurse -Outvariable issues
        $errors   = $issues.Where({$_.Severity -eq 'Error'})
        $warnings = $issues.Where({$_.Severity -eq 'Warning'})
        if ($errors) {
            Write-Error "There were $($errors.Count) errors and $($warnings.Count) warnings total." -ErrorAction Stop
        } else {
            Write-Output "There were $($errors.Count) errors and $($warnings.Count) warnings total."
        }
```

--------------------------------

### Configure GitHub Actions Workflow for PyPI Publishing with OIDC

Source: https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-pypi

This GitHub Actions workflow demonstrates how to securely publish Python packages to PyPI using OpenID Connect (OIDC). It includes a `release-build` job to build and upload distribution artifacts, and a `pypi-publish` job that downloads these artifacts and uses the `pypa/gh-action-pypi-publish` action with `id-token: write` permissions for OIDC-based authentication to PyPI.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
jobs:
  release-build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5

      - uses: actions/setup-python@v5
        with:
          python-version: "3.x"

      - name: build release distributions
        run: |
          # NOTE: put your own distribution build steps here.
          python -m pip install build
          python -m build

      - name: upload windows dists
        uses: actions/upload-artifact@v4
        with:
          name: release-dists
          path: dist/

  pypi-publish:
    runs-on: ubuntu-latest
    needs:
      - release-build
    permissions:
      id-token: write

    steps:
      - name: Retrieve release distributions
        uses: actions/download-artifact@v5
        with:
          name: release-dists
          path: dist/

      - name: Publish release distributions to PyPI
        uses: pypa/gh-action-pypi-publish@3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f
```

--------------------------------

### Configure Cache Action with Multiple Paths - YAML

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching

Example of using the GitHub Actions cache action to cache multiple Gradle directories. The action searches for exact key matches first, then partial matches, and uses restore-keys as fallback. This configuration caches both the Gradle caches and wrapper directories.

```yaml
- name: Cache Gradle packages
  uses: actions/cache@v4
  with:
    path: |
      ~/.gradle/caches
      ~/.gradle/wrapper
```

--------------------------------

### Specify Bamboo Source File Path for GitHub Actions Importer Dry Run

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/bamboo-migration

This example demonstrates using the `--source-file-path` argument with the `gh actions-importer dry-run bamboo build` subcommand. It directs the GitHub Actions Importer to use a local YAML file as the source for the Bamboo pipeline content instead of fetching it directly from the Bamboo instance. This is useful for testing migrations with pre-existing pipeline definitions.

```bash
gh actions-importer dry-run bamboo build --plan-slug IN-COM -o tmp/bamboo --source-file-path ./path/to/my/bamboo/file.yml
```

--------------------------------

### Update GitHub Actions Workflow to Use New Runners (YAML)

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-runners

This YAML snippet demonstrates how to modify the `runs-on` field in a GitHub Actions workflow to specify new GitHub-hosted runner labels. It shows an example of targeting `github-larger-runner` and `linux-x64` for a build job, including steps for checking out code and running a build command.

```yaml
jobs:
  build:
    runs-on: [github-larger-runner, linux-x64]
    steps:
      - name: Checkout code
        uses: actions/checkout@v5
      - name: Build project
        run: make build
```

--------------------------------

### Apply Conditional Logic to Jobs in GitLab CI/CD and GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-gitlab-cicd-to-github-actions

This example demonstrates how to apply conditional logic to determine if a job should run based on specific criteria, such as the branch name. GitLab CI/CD uses `rules` with an `if` condition to control job execution, while GitHub Actions uses the `if` keyword directly on the job definition with expression syntax.

```yaml
deploy_prod:
  stage: deploy
  script:
    - echo "Deploy to production server"
  rules:
    - if: '$CI_COMMIT_BRANCH == "master"'

```

```yaml
jobs:
  deploy_prod:
    if: contains( github.ref, 'master')
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploy to production server"

```

--------------------------------

### Display workflow status badge in README with Markdown image syntax

Source: https://docs.github.com/en/actions/how-tos/monitor-workflows/add-a-status-badge

Embeds a GitHub Actions workflow status badge in a README.md file using Markdown image markup. The example shows a badge for the main.yml workflow in the github/docs repository.

```markdown
![example workflow](https://github.com/github/docs/actions/workflows/main.yml/badge.svg)
```

--------------------------------

### Specify Arguments for a Docker Container Action's Entrypoint

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This snippet illustrates how to provide arguments to a Docker container action using the `args` keyword. The `args` string is passed to the container's `ENTRYPOINT` and is used in place of the `CMD` instruction in a `Dockerfile`. Here, it constructs a message based on the `github.event_name`.

```yaml
steps:
  - name: Explain why this job ran
    uses: octo-org/action-name@main
    with:
      entrypoint: /bin/echo
      args: The ${{ github.event_name }} event triggered this step.
```

--------------------------------

### Use Docker Hub Action in GitHub Actions Workflow

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example illustrates how to integrate an action published on Docker Hub into a GitHub Actions workflow. The action is referenced using the `docker://{image}:{tag}` format, directly pulling the specified Docker image to execute its defined entrypoint. Here, the `alpine:3.8` image is used as a simple action.

```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: docker://alpine:3.8
```

--------------------------------

### Convert Apple Provisioning Profile to Base64 for GitHub Actions Secret

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/sign-xcode-applications

This command converts an Apple provisioning profile (.mobileprovision file) into a Base64 encoded string. The output is copied to the clipboard, ready to be used as a GitHub secret (e.g., BUILD_PROVISION_PROFILE_BASE64). This is a prerequisite for securely storing and using the provisioning profile in a CI workflow on GitHub Actions.

```bash
base64 -i PROVISIONING_PROFILE.mobileprovision | pbcopy
```

--------------------------------

### Example `strategy` context object content in GitHub Actions matrix job

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

This JSON snippet illustrates the structure and values of the `strategy` context object within a GitHub Actions matrix job. It shows properties like `fail-fast`, `job-index`, `job-total`, and `max-parallel` for a matrix with four jobs, specifically from the final job (index 3). This context provides runtime information about the matrix execution strategy.

```json
{
  "fail-fast": true,
  "job-index": 3,
  "job-total": 4,
  "max-parallel": 4
}
```

--------------------------------

### Configure GitHub Actions workflow with runner group

Source: https://docs.github.com/en/actions/how-tos/manage-runners/larger-runners/use-larger-runners_platform=linux

This YAML workflow configuration demonstrates how to use the `runs-on` key with a runner group to send jobs to available runners in the specified group. The example shows a workflow that checks the bats version using Ubuntu runners from the `ubuntu-runners` group.

```yaml
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on:
      group: ubuntu-runners
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v
```

--------------------------------

### Configure Kubernetes Mode with Container Lifecycle Hooks in values.yaml

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

This example shows how to enable Kubernetes mode using container lifecycle hooks, which improves portability and performance by leveraging local storage instead of shared persistent volumes. To activate this mode, set `containerMode.type` to `kubernetes-novolume` in your `values.yaml` file. Note that containers must run as `root` for lifecycle hook operations.

```yaml
containerMode:
  type: "kubernetes-novolume"
```

--------------------------------

### Download and Process Artifact from Triggering Workflow

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

Uses the `actions/github-script` action to download artifacts from a triggering workflow via the GitHub REST API, extract the artifact contents, and perform actions based on the data. This example downloads a PR number artifact and comments on the associated pull request.

```yaml
name: Use the data

on:
  workflow_run:
    workflows: [Upload data]
    types:
      - completed

jobs:
  download:
    runs-on: ubuntu-latest
    steps:
      - name: 'Download artifact'
        uses: actions/github-script@v8
        with:
          script: |
            let allArtifacts = await github.rest.actions.listWorkflowRunArtifacts({
               owner: context.repo.owner,
               repo: context.repo.repo,
               run_id: context.payload.workflow_run.id,
            });
            let matchArtifact = allArtifacts.data.artifacts.filter((artifact) => {
              return artifact.name == "pr_number"
            })[0];
            let download = await github.rest.actions.downloadArtifact({
               owner: context.repo.owner,
               repo: context.repo.repo,
               artifact_id: matchArtifact.id,
               archive_format: 'zip',
            });
            const fs = require('fs');
            const path = require('path');
            const temp = '${{ runner.temp }}/artifacts';
            if (!fs.existsSync(temp)){
              fs.mkdirSync(temp);
            }
            fs.writeFileSync(path.join(temp, 'pr_number.zip'), Buffer.from(download.data));

      - name: 'Unzip artifact'
        run: unzip "${{ runner.temp }}/artifacts/pr_number.zip" -d "${{ runner.temp }}/artifacts"

      - name: 'Comment on PR'
        uses: actions/github-script@v8
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          script: |
            const fs = require('fs');
            const path = require('path');
            const temp = '${{ runner.temp }}/artifacts';
            const issue_number = Number(fs.readFileSync(path.join(temp, 'pr_number')));
            await github.rest.issues.createComment({
              owner: context.repo.owner,
              repo: context.repo.repo,
              issue_number: issue_number,
              body: 'Thank you for the PR!'
            });
```

--------------------------------

### Build matrix from repository dispatch event payload

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/run-job-variations

Uses GitHub Actions contexts to dynamically populate matrix variables from webhook event data. The workflow triggers on repository_dispatch events and extracts version information from the client payload to configure Node.js setup across multiple versions.

```yaml
on:
  repository_dispatch:
    types:
      - test

jobs:
  example_matrix:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        version: ${{ github.event.client_payload.versions }}
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.version }}
```

--------------------------------

### Configure GitHub Actions Job with PostgreSQL Service Container

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-gitlab-cicd-to-github-actions

Sets up a GitHub Actions workflow job that runs in a Node.js container with a PostgreSQL service container. The workflow checks out code, installs dependencies, and connects to PostgreSQL using environment variables for host and port configuration. Requires actions/checkout@v5 and assumes a client.js script exists for database operations.

```yaml
jobs:
  container-job:
    runs-on: ubuntu-latest
    container: node:20-bookworm-slim

    services:
      postgres:
        image: postgres
        env:
          POSTGRES_PASSWORD: postgres

    steps:
      - name: Check out repository code
        uses: actions/checkout@v5

      - name: Install dependencies
        run: npm ci

      - name: Connect to PostgreSQL
        run: node client.js
        env:
          POSTGRES_HOST: postgres
          POSTGRES_PORT: 5432
```

--------------------------------

### Publish Package to GitHub Packages with npm using GitHub Actions

Source: https://docs.github.com/en/actions/publishing-packages/publishing-nodejs-packages

A GitHub Actions workflow that publishes an npm package to GitHub Packages registry on release publication. Uses setup-node action to configure .npmrc file with GitHub Packages registry URL and authenticates via GITHUB_TOKEN secret. Requires contents read and packages write permissions.

```yaml
name: Publish package to GitHub Packages
on:
  release:
    types: [published]
jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    steps:
      - uses: actions/checkout@v5
      # Setup .npmrc file to publish to GitHub Packages
      - uses: actions/setup-node@v4
        with:
          node-version: '20.x'
          registry-url: 'https://npm.pkg.github.com'
          # Defaults to the user or organization that owns the workflow file
          scope: '@octocat'
      - run: npm ci
      - run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

--------------------------------

### Configure Just-In-Time Runner with Encoded Config

Source: https://docs.github.com/en/actions/reference/secure-use-reference

Pass an encoded JIT configuration to a self-hosted runner at startup using the run.sh script. The configuration is obtained from the REST API response and enables ephemeral runner registration that automatically removes the runner after job completion.

```bash
./run.sh --jitconfig ${encoded_jit_config}
```

--------------------------------

### Referencing a Local GitHub Action in a Workflow

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/find-and-customize-actions

This YAML snippet demonstrates how to use an action that is defined within the same repository as the workflow file. It includes steps to check out the repository and then reference the local action using a relative path.

```yaml
jobs:
  my_first_job:
    runs-on: ubuntu-latest
    steps:
      # This step checks out a copy of your repository.
      - name: My first step - check out repository
        uses: actions/checkout@v5
      # This step references the directory that contains the action.
      - name: Use local hello-world-action
        uses: ./.github/actions/hello-world-action
```

--------------------------------

### Set Default Shell and Working Directory for a Specific GitHub Actions Job

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/set-default-values-for-jobs

This example illustrates how to configure a default shell and working directory specifically for `run` steps within a particular job in a GitHub Actions workflow. It uses `jobs.<job_id>.defaults.run` to set `bash` as the shell and `./scripts` as the working directory, overriding any workflow-level defaults for this job.

```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    defaults:
      run:
        shell: bash
        working-directory: ./scripts
```

--------------------------------

### Define Single-Dimension Matrix Strategy in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example illustrates how to use a single-dimension matrix strategy in a GitHub Actions workflow to run a job multiple times with different values for a specified variable. The `matrix` context allows accessing the current variable value (e.g., `matrix.version`) within the job steps, enabling automated testing or builds across various configurations, such as different Node.js versions.

```yaml
jobs:
  example_matrix:
    strategy:
      matrix:
        version: [10, 12, 14]
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.version }}
```

--------------------------------

### Mask an environment variable in GitHub Actions workflow

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Shows how to mask an environment variable value in a GitHub Actions workflow. The workflow defines an environment variable and masks it using add-mask before outputting it. Examples demonstrate both Bash and PowerShell shells running on different OS environments.

```yaml
jobs:
  bash-example:
    runs-on: ubuntu-latest
    env:
      MY_NAME: "Mona The Octocat"
    steps:
      - name: bash-version
        run: echo "::add-mask::$MY_NAME"
```

```yaml
jobs:
  powershell-example:
    runs-on: windows-latest
    env:
      MY_NAME: "Mona The Octocat"
    steps:
      - name: powershell-version
        run: Write-Output "::add-mask::$env:MY_NAME"
```

--------------------------------

### Secrets Context Usage

Source: https://docs.github.com/en/actions/reference/accessing-contextual-information-about-workflow-runs

The secrets context provides access to sensitive credentials in GitHub Actions workflows. This example demonstrates using the GITHUB_TOKEN secret with the GitHub CLI to create issues programmatically. The secret is passed through environment variables to the workflow step.

```APIDOC
## Secrets Context

### Description
Access sensitive credentials and secrets defined in GitHub repository settings or organization settings within workflow steps.

### Context Properties
- **secrets** (object) - Required - Contains all secrets available to the workflow
- **secrets.GITHUB_TOKEN** (string) - Required - Automatically generated token for GitHub API authentication
- **secrets.<custom_secret_name>** (string) - Optional - Custom secrets defined in repository or organization settings

### Usage Example
Access secrets using the `${{ secrets.SECRET_NAME }}` syntax in workflow steps.

### Workflow Example
```yaml
name: Open new issue
on: workflow_dispatch

jobs:
  open-issue:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      issues: write
    steps:
      - run: |
          gh issue --repo ${{ github.repository }} \
            create --title "Issue title" --body "Issue body"
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Request Example
```json
{
  "GH_TOKEN": "${{ secrets.GITHUB_TOKEN }}",
  "repository": "${{ github.repository }}",
  "title": "Issue title",
  "body": "Issue body"
}
```

### Response Example
```json
{
  "status": "success",
  "issue_created": true,
  "issue_url": "https://github.com/owner/repo/issues/1"
}
```
```

--------------------------------

### Define GitHub Actions Workflow for Python Package Release and PyPI Publish

Source: https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/configuring-openid-connect-in-pypi

This YAML configuration defines a complete GitHub Actions workflow for automating the release process of a Python package. It includes two jobs: `release-build` which handles checking out code, setting up Python, building distribution artifacts, and uploading them; and `pypi-publish` which downloads these artifacts and publishes them to PyPI, managing job dependencies and necessary permissions.

```yaml
jobs:
  release-build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5

      - uses: actions/setup-python@v5
        with:
          python-version: "3.x"

      - name: build release distributions
        run: |
          # NOTE: put your own distribution build steps here.
          python -m pip install build
          python -m build

      - name: upload windows dists
        uses: actions/upload-artifact@v4
        with:
          name: release-dists
          path: dist/

  pypi-publish:
    runs-on: ubuntu-latest
    needs:
      - release-build
    permissions:
      id-token: write

    steps:
      - name: Retrieve release distributions
        uses: actions/download-artifact@v5
        with:
          name: release-dists
          path: dist/

      - name: Publish release distributions to PyPI
        uses: pypa/gh-action-pypi-publish@3e4f5a6b7c8d9e0f1a2b3c4d5e6f7a8b9c0d1e2f
```

--------------------------------

### Include and exclude file paths with combined patterns in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow

Configure a GitHub Actions workflow to run on specific file paths while excluding certain subdirectories using the `paths` filter with both positive and negative patterns. This example triggers on changes in the `sub-project` directory except for the `docs` subdirectory.

```yaml
on:
  push:
    paths:
      - 'sub-project/**'
      - '!sub-project/docs/**'
```

--------------------------------

### Verify SBOM Attestation with JSON Output and JQ Filtering

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/use-artifact-attestations

Verify SBOM attestations and format the output as JSON, then use jq to extract the predicate information. Useful for detailed review of SBOM attestation contents.

```bash
gh attestation verify PATH/TO/YOUR/BUILD/ARTIFACT-BINARY \
  -R ORGANIZATION_NAME/REPOSITORY_NAME \
  --predicate-type https://spdx.dev/Document/v2.3 \
  --format json \
  --jq '.[].verificationResult.statement.predicate'
```

--------------------------------

### Specify Rust Toolchain Version in GitHub Actions Workflow

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/rust

This YAML snippet demonstrates how to configure a GitHub Actions runner to use the nightly Rust toolchain and then output the installed Rust version. It uses `rustup override set nightly` to change the toolchain and `rustup --version` to verify the change.

```YAML
      - name: Temporarily modify the rust toolchain version
        run: rustup override set nightly
      - name: Output rust version for educational purposes
        run: rustup --version
```

--------------------------------

### Configure GitHub Actions Job Container and Service in YAML

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers

This YAML snippet demonstrates how to define a GitHub Actions job that runs within a specified Docker container (e.g., `node:20-bookworm-slim`). It also shows how to set up a dependent service container, such as PostgreSQL, including its image, environment variables (like `POSTGRES_PASSWORD`), and health check options to ensure the service is ready before the main job proceeds.

```YAML
jobs:
  # Label of the container job
  container-job:
    # Containers must run in Linux based operating systems
    runs-on: ubuntu-latest
    # Docker Hub image that `container-job` executes in
    container: node:20-bookworm-slim

    # Service containers to run with `container-job`
    services:
      # Label used to access the service container
      postgres:
        # Docker Hub image
        image: postgres
        # Provide the password for postgres
        env:
          POSTGRES_PASSWORD: postgres
        # Set health checks to wait until postgres has started
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
```

--------------------------------

### Identify Docker Not Found Error in Runner Logs (Log File)

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/monitor-and-troubleshoot_platform=linux

This log output indicates that the self-hosted runner failed to find the 'docker' executable, leading to a `FileNotFoundException`. This error typically occurs when Docker is not installed or not accessible in the runner's environment, preventing container-dependent jobs from running.

```log
[2020-02-13 16:56:10Z INFO DockerCommandManager] Which: 'docker'
[2020-02-13 16:56:10Z INFO DockerCommandManager] Not found.
[2020-02-13 16:56:10Z ERR  StepsRunner] Caught exception from step: System.IO.FileNotFoundException: File not found: 'docker'
```

--------------------------------

### Configure Redis Service Container in GitHub Actions Workflow

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-redis-service-containers

GitHub Actions workflow that sets up a Redis service container on an Ubuntu runner with health checks and port mapping. The workflow checks out repository code, installs dependencies, and connects to Redis using environment variables. Requires a Node.js client script (client.js) to interact with the Redis service.

```yaml
name: Redis runner example
on: push

jobs:
  runner-job:
    runs-on: ubuntu-latest

    services:
      redis:
        image: redis
        options: >
          --health-cmd "redis-cli ping"
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
        ports:
          - 6379:6379

    steps:
      - name: Check out repository code
        uses: actions/checkout@v5

      - name: Install dependencies
        run: npm ci

      - name: Connect to Redis
        run: node client.js
        env:
          REDIS_HOST: localhost
          REDIS_PORT: 6379
```

--------------------------------

### Configure OIDC `sub` claim for context values with colons in GitHub Actions

Source: https://docs.github.com/en/actions/reference/openid-connect-reference

This example demonstrates how to handle OIDC `sub` claim context values that contain colons, such as an environment name like `production:eastus`. It requires including `environment` and `repository_owner` claim keys in the configuration submitted to the GitHub Actions OIDC API for organizations or repositories.

```json
{
   "include_claim_keys": [
       "environment",
       "repository_owner"
   ]
}
```

--------------------------------

### Cache Yarn dependencies with setup-node action

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Configures GitHub Actions workflow to cache Yarn dependencies using the setup-node action with Node.js version 20. This optimizes build performance by caching Yarn's dependency tree. Requires actions/checkout and actions/setup-node actions.

```yaml
steps:
- uses: actions/checkout@v5
- uses: actions/setup-node@v4
  with:
    node-version: '20'
    cache: 'yarn'
- run: yarn
- run: yarn test
```

--------------------------------

### GitHub Actions Script Steps Syntax

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-azure-pipelines-to-github-actions

Demonstrates how to define script steps in GitHub Actions using the run key with optional shell specification. Shows equivalent syntax for default shell, bash, PowerShell Core, and PowerShell execution on windows-latest.

```yaml
jobs:
  scripts:
    runs-on: windows-latest
    steps:
      - run: echo "This step runs in the default shell"
      - run: echo "This step runs in bash"
        shell: bash
      - run: Write-Host "This step runs in PowerShell Core"
        shell: pwsh
      - run: Write-Host "This step runs in PowerShell"
        shell: powershell
```

--------------------------------

### GitHub Actions Workflow: Build and Deploy Container to GKE

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/google-kubernetes-engine

This YAML workflow defines a GitHub Actions job to build a Docker image, push it to Google Container Registry (GCR), and deploy it to a Google Kubernetes Engine (GKE) cluster. It leverages `google-github-actions` for `gcloud` setup and GKE credentials, uses `docker` for image operations, and `kustomize` with `kubectl` for deployment. Users must configure `PROJECT_ID`, `GKE_CLUSTER`, `GKE_ZONE`, `DEPLOYMENT_NAME`, and `IMAGE` environment variables, and provide `GKE_SA_KEY` as a secret.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# GitHub recommends pinning actions to a commit SHA.
# To get a newer version, you will need to update the SHA.
# You can also reference a tag or branch, but the action may change without warning.

name: Build and Deploy to GKE

on:
  push:
    branches:
      - main

env:
  PROJECT_ID: ${{ secrets.GKE_PROJECT }}
  GKE_CLUSTER: cluster-1    # Add your cluster name here.
  GKE_ZONE: us-central1-c   # Add your cluster zone here.
  DEPLOYMENT_NAME: gke-test # Add your deployment name here.
  IMAGE: static-site

jobs:
  setup-build-publish-deploy:
    name: Setup, Build, Publish, and Deploy
    runs-on: ubuntu-latest
    environment: production

    steps:
    - name: Checkout
      uses: actions/checkout@v5

    # Setup gcloud CLI
    - uses: google-github-actions/setup-gcloud@1bee7de035d65ec5da40a31f8589e240eba8fde5
      with:
        service_account_key: ${{ secrets.GKE_SA_KEY }}
        project_id: ${{ secrets.GKE_PROJECT }}

    # Configure Docker to use the gcloud command-line tool as a credential
    # helper for authentication
    - run: |-
        gcloud --quiet auth configure-docker

    # Get the GKE credentials so we can deploy to the cluster
    - uses: google-github-actions/get-gke-credentials@db150f2cc60d1716e61922b832eae71d2a45938f
      with:
        cluster_name: ${{ env.GKE_CLUSTER }}
        location: ${{ env.GKE_ZONE }}
        credentials: ${{ secrets.GKE_SA_KEY }}

    # Build the Docker image
    - name: Build
      run: |-
        docker build \
          --tag "gcr.io/$PROJECT_ID/$IMAGE:$GITHUB_SHA" \
          --build-arg GITHUB_SHA="$GITHUB_SHA" \
          --build-arg GITHUB_REF="$GITHUB_REF" \
          .

    # Push the Docker image to Google Container Registry
    - name: Publish
      run: |-
        docker push "gcr.io/$PROJECT_ID/$IMAGE:$GITHUB_SHA"

    # Set up kustomize
    - name: Set up Kustomize
      run: |-
        curl -sfLo kustomize https://github.com/kubernetes-sigs/kustomize/releases/download/v3.1.0/kustomize_3.1.0_linux_amd64
        chmod u+x ./kustomize

    # Deploy the Docker image to the GKE cluster
    - name: Deploy
      run: |-
        ./kustomize edit set image gcr.io/PROJECT_ID/IMAGE:TAG=gcr.io/$PROJECT_ID/$IMAGE:$GITHUB_SHA
        ./kustomize build . | kubectl apply -f -
        kubectl rollout status deployment/$DEPLOYMENT_NAME
        kubectl get services -o wide
```

--------------------------------

### Run Python Tests with Tox Across Multiple Versions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

GitHub Actions workflow that executes tox tests across multiple Python versions (3.9, 3.11, 3.13) using a matrix strategy. The workflow checks out code, sets up the specified Python version, installs tox, and runs tests using the `-e py` option to use the Python version in PATH. This approach distributes testing workload across multiple jobs.

```yaml
name: Python package

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        python: ["3.9", "3.11", "3.13"]

    steps:
      - uses: actions/checkout@v5
      - name: Setup Python
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python }}
      - name: Install tox and any other packages
        run: pip install tox
      - name: Run tox
        # Run tox using the version of Python in `PATH`
        run: tox -e py
```

--------------------------------

### Implement GitHub Actions Workflow for Secret Generation and Consumption with PowerShell

Source: https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions

This workflow provides an alternative implementation for generating, storing, and consuming secrets, using PowerShell scripts within the GitHub Actions `run` steps. Similar to the Bash example, it leverages an imaginary `secret-store` and demonstrates passing data between jobs via `GITHUB_OUTPUT` and masking sensitive output with `::add-mask::`.

```yaml
on: push

jobs:
  secret-generator:
    runs-on: ubuntu-latest
    steps:
    - uses: some/secret-store@27b31702a0e7fc50959f5ad993c78deac1bdfc29
      with:
        credentials: ${{ secrets.SECRET_STORE_CREDENTIALS }}
        instance: ${{ secrets.SECRET_STORE_INSTANCE }}
    - name: generate secret
      shell: pwsh
      run: |
        Set-Variable -Name Generated_Secret -Value (Get-Random)
        Write-Output "::add-mask::$Generated_Secret"
        Set-Variable -Name Secret_Handle -Value (Store-Secret "$Generated_Secret")
        "handle=$Secret_Handle" >> $env:GITHUB_OUTPUT
  secret-consumer:
    runs-on: macos-latest
    needs: secret-generator
    steps:
    - uses: some/secret-store@27b31702a0e7fc50959f5ad993c78deac1bdfc29
      with:
        credentials: ${{ secrets.SECRET_STORE_CREDENTIALS }}
        instance: ${{ secrets.SECRET_STORE_INSTANCE }}
    - name: use secret
      shell: pwsh
      run: |
        Set-Variable -Name Secret_Handle -Value "${{ needs.secret-generator.outputs.handle }}"
        Set-Variable -Name Retrieved_Secret -Value (Retrieve-Secret "$Secret_Handle")
        echo "::add-mask::$Retrieved_Secret"
        echo "We retrieved our masked secret: $RETRIEVED_SECRET"
```

```powershell
Set-Variable -Name Generated_Secret -Value (Get-Random)
Write-Output "::add-mask::$Generated_Secret"
Set-Variable -Name Secret_Handle -Value (Store-Secret "$Generated_Secret")
"handle=$Secret_Handle" >> $env:GITHUB_OUTPUT
```

```powershell
Set-Variable -Name Secret_Handle -Value "${{ needs.secret-generator.outputs.handle }}"
Set-Variable -Name Retrieved_Secret -Value (Retrieve-Secret "$Secret_Handle")
echo "::add-mask::$Retrieved_Secret"
echo "We retrieved our masked secret: $RETRIEVED_SECRET"
```

--------------------------------

### Define GitHub Actions Workflow for GKE Build and Deploy

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/google-kubernetes-engine

This YAML defines a complete GitHub Actions workflow that automates the build, publish, and deployment process of a containerized application to Google Kubernetes Engine (GKE). It triggers on pushes to the 'main' branch, sets up environment variables, checks out code, configures GCP authentication, builds and pushes a Docker image, and finally deploys it to GKE using Kustomize and Kubectl.

```yaml
name: Build and Deploy to GKE

on:
  push:
    branches:
      - main

env:
  PROJECT_ID: ${{ secrets.GKE_PROJECT }}
  GKE_CLUSTER: cluster-1    # Add your cluster name here.
  GKE_ZONE: us-central1-c   # Add your cluster zone here.
  DEPLOYMENT_NAME: gke-test # Add your deployment name here.
  IMAGE: static-site

jobs:
  setup-build-publish-deploy:
    name: Setup, Build, Publish, and Deploy
    runs-on: ubuntu-latest
    environment: production

    steps:
    - name: Checkout
      uses: actions/checkout@v5

    # Setup gcloud CLI
    - uses: google-github-actions/setup-gcloud@1bee7de035d65ec5da40a31f8589e240eba8fde5
      with:
        service_account_key: ${{ secrets.GKE_SA_KEY }}
        project_id: ${{ secrets.GKE_PROJECT }}

    # Configure Docker to use the gcloud command-line tool as a credential
    # helper for authentication
    - run: |-
        gcloud --quiet auth configure-docker

    # Get the GKE credentials so we can deploy to the cluster
    - uses: google-github-actions/get-gke-credentials@db150f2cc60d1716e61922b832eae71d2a45938f
      with:
        cluster_name: ${{ env.GKE_CLUSTER }}
        location: ${{ env.GKE_ZONE }}
        credentials: ${{ secrets.GKE_SA_KEY }}

    # Build the Docker image
    - name: Build
      run: |-
        docker build \
          --tag "gcr.io/$PROJECT_ID/$IMAGE:$GITHUB_SHA" \
          --build-arg GITHUB_SHA="$GITHUB_SHA" \
          --build-arg GITHUB_REF="$GITHUB_REF" \
          .

    # Push the Docker image to Google Container Registry
    - name: Publish
      run: |-
        docker push "gcr.io/$PROJECT_ID/$IMAGE:$GITHUB_SHA"

    # Set up kustomize
    - name: Set up Kustomize
      run: |-
        curl -sfLo kustomize https://github.com/kubernetes-sigs/kustomize/releases/download/v3.1.0/kustomize_3.1.0_linux_amd64
        chmod u+x ./kustomize

    # Deploy the Docker image to the GKE cluster
    - name: Deploy
      run: |-
        ./kustomize edit set image gcr.io/PROJECT_ID/IMAGE:TAG=gcr.io/$PROJECT_ID/$IMAGE:$GITHUB_SHA
        ./kustomize build . | kubectl apply -f -
        kubectl rollout status deployment/$DEPLOYMENT_NAME
        kubectl get services -o wide
```

--------------------------------

### runs.steps[*].env

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Defines environment variables specific to a single step.

```APIDOC
## Configuration Property runs.steps[*].env

### Description
Sets a `map` of environment variables for only that step. If you want to modify the environment variable stored in the workflow, use `echo "{name}={value}" >> $GITHUB_ENV` in a composite step.

### Method
Configuration Property

### Endpoint
runs.steps[*].env

### Parameters
#### Request Body
- **env** (object) - Optional - A map of environment variables.
  - **KEY** (string) - Required - The name of the environment variable.
  - **VALUE** (string) - Required - The value of the environment variable.

### Request Example
{
  "env": {
    "MY_VAR": "my_value",
    "ANOTHER_VAR": "another_value"
  }
}
```

--------------------------------

### Set Multiline Environment Variable in PowerShell with Delimiter

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Sets a multiline environment variable in PowerShell using a dynamically generated GUID as delimiter. Captures web request content into the JSON_RESPONSE variable. Uses pwsh shell specification for PowerShell Core.

```yaml
steps:
  - name: Set the value in pwsh
    id: step_one
    run: |
      $EOF = (New-Guid).Guid
      "JSON_RESPONSE<<$EOF" >> $env:GITHUB_ENV
      (Invoke-WebRequest -Uri "https://example.com").Content >> $env:GITHUB_ENV
      "$EOF" >> $env:GITHUB_ENV
    shell: pwsh
```

--------------------------------

### CircleCI Complete Workflow Configuration for Ruby on Rails

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-circleci

A complete CircleCI configuration file (version 2.1) that defines shared steps for dependency caching, database setup, and test execution. It includes job definitions for testing against Ruby 2.5 and 2.6 with PostgreSQL services, and a workflow that runs both jobs. The configuration uses caching to optimize build times and includes health checks for database connectivity.

```yaml
---
version: 2.1

commands:
  shared_steps:
    steps:
      - checkout

      # Restore Cached Dependencies
      - restore_cache:
          name: Restore bundle cache
          key: administrate-{{ checksum "Gemfile.lock" }}

      # Bundle install dependencies
      - run: bundle install --path vendor/bundle

      # Cache Dependencies
      - save_cache:
          name: Store bundle cache
          key: administrate-{{ checksum "Gemfile.lock" }}
          paths:
            - vendor/bundle

      # Wait for DB
      - run: dockerize -wait tcp://localhost:5432 -timeout 1m

      # Setup the environment
      - run: cp .sample.env .env

      # Setup the database
      - run: bundle exec rake db:setup

      # Run the tests
      - run: bundle exec rake

default_job: &default_job
  working_directory: ~/administrate
  steps:
    - shared_steps
    # Run the tests against multiple versions of Rails
    - run: bundle exec appraisal install
    - run: bundle exec appraisal rake

jobs:
  ruby-25:
    <<: *default_job
    docker:
      - image: circleci/ruby:2.5.0-node-browsers
        environment:
          PGHOST: localhost
          PGUSER: administrate
          RAILS_ENV: test
      - image: postgres:10.1-alpine
        environment:
          POSTGRES_USER: administrate
          POSTGRES_DB: ruby25
          POSTGRES_PASSWORD: ""

  ruby-26:
    <<: *default_job
    docker:
      - image: circleci/ruby:2.6.3-node-browsers-legacy
        environment:
          PGHOST: localhost
          PGUSER: administrate
          RAILS_ENV: test
      - image: postgres:10.1-alpine
        environment:
          POSTGRES_USER: administrate
          POSTGRES_DB: ruby26
          POSTGRES_PASSWORD: ""

workflows:
  version: 2
  multiple-rubies:
    jobs:
      - ruby-26
      - ruby-25
```

--------------------------------

### Install and Configure Trust Policies Helm Chart with Image Matching

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/enforce-artifact-attestations

Deploys the trust-policies Helm chart with attestation enforcement for specific image patterns. Uses glob patterns to match images from a specific organization while exempting Docker Hub busybox images. The command sets policy enforcement, organization context, and image matching rules.

```bash
helm upgrade trust-policies --install --atomic \
 --namespace artifact-attestations \
 oci://ghcr.io/github/artifact-attestations-helm-charts/trust-policies \
 --version v0.7.0 \
 --set policy.enabled=true \
 --set policy.organization=MY-ORGANIZATION \
 --set-json 'policy.exemptImages=["index.docker.io/library/busybox**"]' \
 --set-json 'policy.images=["ghcr.io/MY-ORGANIZATION/**"]'
```

--------------------------------

### View Resulting Matrix Job Combinations from Object Array

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This snippet displays the individual job configurations that result from a matrix defined with an array of objects. It shows how each combination of `os` and `node` (including its nested properties like `version` and `env`) forms a unique job context. This helps visualize the expansion of complex matrix definitions.

```yaml
- matrix.os: ubuntu-latest
  matrix.node.version: 14
- matrix.os: ubuntu-latest
  matrix.node.version: 20
  matrix.node.env: NODE_OPTIONS=--openssl-legacy-provider
- matrix.os: macos-latest
  matrix.node.version: 14
- matrix.os: macos-latest
  matrix.node.version: 20
  matrix.node.env: NODE_OPTIONS=--openssl-legacy-provider

```

--------------------------------

### Matrix Include - Expanding Configurations

Source: https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions

Use the include option to add additional variables to specific matrix combinations. This allows you to expand configurations without creating a full matrix, adding extra variables only to jobs that match certain criteria.

```APIDOC
## jobs.<job_id>.strategy.matrix.include

### Description
Add additional key:value pairs to specific matrix combinations. Original matrix values are preserved and cannot be overwritten by include entries.

### Behavior
- Processes after the base matrix is created
- Adds variables only to matching combinations
- Creates new matrix combinations if no match exists
- Original matrix values cannot be overwritten
- Added values can be overwritten by subsequent includes

### Example: Expanding Configurations
```yaml
jobs:
  example_matrix:
    strategy:
      matrix:
        os: [windows-latest, ubuntu-latest]
        node: [14, 16]
        include:
          - os: windows-latest
            node: 16
            npm: 6
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}
      - if: ${{ matrix.npm }}
        run: npm install -g npm@${{ matrix.npm }}
      - run: npm --version
```

### Result
- 4 base combinations (2 OS × 2 node versions)
- When `os: windows-latest` and `node: 16` match, `npm: 6` is added
- Total: 4 jobs with one job having the additional npm variable

### Example: Adding New Configurations
```yaml
matrix:
  os: [macos-latest, windows-latest, ubuntu-latest]
  version: [12, 14, 16]
  include:
    - os: windows-latest
      version: 17
```

### Result
- 9 base combinations (3 OS × 3 versions)
- 1 additional combination (windows-latest with version 17)
- Total: 10 jobs

### Include-Only Matrix
```yaml
matrix:
  include:
    - site: "production"
      datacenter: "site-a"
    - site: "staging"
      datacenter: "site-b"
```

### Result
- Runs 2 jobs without a base matrix
- Each include entry creates one job
- Useful for non-uniform configurations
```

--------------------------------

### Mount Volumes in GitHub Actions Job Container

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This snippet illustrates how to define volumes for a GitHub Actions job container, allowing data sharing between services or steps. It shows examples of mounting named Docker volumes, anonymous Docker volumes, and bind mounts from the host machine into specified paths within the container.

```yaml
volumes:
  - my_docker_volume:/volume_mount
  - /data/my_data
  - /source/directory:/destination/directory

```

--------------------------------

### Define Inputs for Manual Workflow Dispatch

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow

Shows how to define multiple input types for the workflow_dispatch event, including choice, boolean, string, and environment types. The example includes a conditional job that runs based on a boolean input value. Maximum 25 top-level input properties and 65,535 character payload limit apply.

```yaml
on:
  workflow_dispatch:
    inputs:
      logLevel:
        description: 'Log level'
        required: true
        default: 'warning'
        type: choice
        options:
          - info
          - warning
          - debug
      print_tags:
        description: 'True to print to STDOUT'
        required: true
        type: boolean
      tags:
        description: 'Test scenario tags'
        required: true
        type: string
      environment:
        description: 'Environment to run tests against'
        type: environment
        required: true

jobs:
  print-tag:
    runs-on: ubuntu-latest
    if: ${{ inputs.print_tags }}
    steps:
      - name: Print the input tag to STDOUT
        run: echo  The tags are ${{ inputs.tags }}
```

--------------------------------

### Configure Runner Scale Set Name in Helm values.yaml

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

Sets the name of the runner scale set to be created, defaulting to the Helm release name if not specified. This is a basic configuration property in the values.yaml file used during Helm installation.

```yaml
runnerScaleSetName: "my-runners"
```

--------------------------------

### Run forecast command for Jenkins pipeline analysis

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/jenkins-migration

Executes a forecast analysis on a Jenkins instance to predict GitHub Actions resource requirements. By default, analyzes the previous seven days of build data and generates a forecast report in the specified output directory. Requires the paginated-builds plugin to be installed on the Jenkins server.

```bash
gh actions-importer forecast jenkins --output-dir tmp/forecast
```

--------------------------------

### GitHub Actions Workflow - Node.js Build and Azure WebApp Deploy

Source: https://docs.github.com/en/actions/deployment/deploying-to-your-cloud-provider/deploying-to-azure/deploying-nodejs-to-azure-app-service

A complete GitHub Actions workflow that automates building a Node.js application and deploying it to Azure WebApp. The workflow includes environment variable configuration, Node.js setup with npm caching, build/test execution, artifact upload/download, and Azure deployment with production environment tracking. Requires AZURE_WEBAPP_PUBLISH_PROFILE secret to be configured in repository settings.

```yaml
on:
  push:
    branches:
      - main

env:
  AZURE_WEBAPP_NAME: MY_WEBAPP_NAME
  AZURE_WEBAPP_PACKAGE_PATH: '.'
  NODE_VERSION: '14.x'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v5

    - name: Set up Node.js
      uses: actions/setup-node@v4
      with:
        node-version: ${{ env.NODE_VERSION }}
        cache: 'npm'

    - name: npm install, build, and test
      run: |
        npm install
        npm run build --if-present
        npm run test --if-present
    - name: Upload artifact for deployment job
      uses: actions/upload-artifact@v4
      with:
        name: node-app
        path: .

  deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: 'production'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}

    steps:
    - name: Download artifact from build job
      uses: actions/download-artifact@v5
      with:
        name: node-app

    - name: 'Deploy to Azure WebApp'
      id: deploy-to-webapp
      uses: azure/webapps-deploy@85270a1854658d167ab239bce43949edb336fa7c
      with:
        app-name: ${{ env.AZURE_WEBAPP_NAME }}
        publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
        package: ${{ env.AZURE_WEBAPP_PACKAGE_PATH }}
```

--------------------------------

### Generate SBOM Attestation for a Binary using GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/security-for-github-actions/using-artifact-attestations/using-artifact-attestations-to-establish-provenance-for-builds

This GitHub Actions step uses the `attest-sbom` action to create an SBOM attestation for a binary. It requires `subject-path` to specify the binary the SBOM describes and `sbom-path` to indicate the location of the generated SBOM file.

```yaml
- name: Generate SBOM attestation
  uses: actions/attest-sbom@v2
  with:
    subject-path: 'PATH/TO/ARTIFACT'
    sbom-path: 'PATH/TO/SBOM'
```

--------------------------------

### Creating Error Annotations in GitHub Actions Workflows

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands

This example demonstrates two methods for creating an error annotation in GitHub Actions. The first shows using the `core.error` function from the `actions/toolkit` in JavaScript. The second illustrates the equivalent `::error` workflow command, which can be directly embedded in a YAML `run` step using `echo` for Bash or `Write-Output` for PowerShell.

```JavaScript
core.error('Missing semicolon', {file: 'app.js', startLine: 1})
```

```YAML
      - name: Create annotation for build error
        run: echo "::error file=app.js,line=1::Missing semicolon"
```

```YAML
      - name: Create annotation for build error
        run: Write-Output "::error file=app.js,line=1::Missing semicolon"
```

--------------------------------

### Configure Event Activity Types in GitHub Actions Workflow

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow

Specifies which activity types for an event should trigger a workflow. The example shows triggering on label creation only. Multiple activity types can be specified, and any one occurring will trigger a run. If multiple triggering types occur simultaneously, multiple workflow runs are initiated.

```yaml
on:
  label:
    types:
      - created
```

--------------------------------

### Configure GitHub Actions for Binary Build Provenance Attestation

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/use-artifact-attestations

This snippet demonstrates how to configure a GitHub Actions workflow to generate artifact attestations for binaries. It includes the necessary permissions (`id-token`, `contents`, `attestations`) and a step using `actions/attest-build-provenance@v3` to attest a binary located at `subject-path`. The `subject-path` parameter specifies the path to the built binary artifact.

```yaml
permissions:
  id-token: write
  contents: read
  attestations: write
```

```yaml
- name: Generate artifact attestation
  uses: actions/attest-build-provenance@v3
  with:
    subject-path: 'PATH/TO/ARTIFACT'
```

--------------------------------

### Limiting Concurrent Matrix Jobs with `max-parallel` in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/run-job-variations

This example illustrates how to use `jobs.<job_id>.strategy.max-parallel` to set the maximum number of jobs that can run simultaneously when utilizing a matrix job strategy in GitHub Actions. It ensures that even if more runners are available, only a specified number of jobs from the matrix will execute concurrently.

```yaml
jobs:
  example_matrix:
    strategy:
      max-parallel: 2
      matrix:
        version: [10, 12, 14]
        os: [ubuntu-latest, windows-latest]
```

--------------------------------

### runs.steps[*].uses

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Selects an action to run as part of a step, supporting various action sources and versions.

```APIDOC
## Configuration Property runs.steps[*].uses

### Description
Selects an action to run as part of a step in your job. An action is a reusable unit of code. You can use an action defined in the same repository as the workflow, a public repository, or in a published Docker container image. We strongly recommend that you include the version of the action you are using by specifying a Git ref, SHA, or Docker tag number. If you don't specify a version, it could break your workflows or cause unexpected behavior when the action owner publishes an update.

### Method
Configuration Property

### Endpoint
runs.steps[*].uses

### Parameters
#### Request Body
- **uses** (string) - Optional - The action to use (e.g., `owner/repo@ref`, `./path/to/action`, `docker://image`).

### Request Example
{
  "uses_examples": [
    "actions/checkout@8f4b7f84864484a7bf31766abe9204da3cbe65b3",
    "actions/checkout@v5",
    "actions/checkout@v5.2.0",
    "actions/checkout@main",
    "actions/aws/ec2@main",
    "./.github/actions/my-action",
    "docker://gcr.io/cloud-builders/gradle",
    "docker://alpine:3.8"
  ]
}
```

--------------------------------

### Define sequential job dependencies in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-jobs

This example illustrates how to define dependencies between jobs using the `needs` keyword in a GitHub Actions workflow. Jobs specified in `needs` must complete successfully before the current job will run. This ensures sequential execution, where `job1` runs first, then `job2` (after `job1` succeeds), and finally `job3` (after both `job1` and `job2` succeed).

```yaml
jobs:
  job1:
  job2:
    needs: job1
  job3:
    needs: [job1, job2]
```

--------------------------------

### Upload Java Ant Build Artifacts using GitHub Actions YAML

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/java-with-ant

This GitHub Actions workflow snippet demonstrates how to build a Java project using Ant and then upload the resulting build artifacts. It checks out the repository, sets up Java Development Kit (JDK) version 17 using Temurin distribution, executes the Ant build script, and finally uploads the contents of the 'build/jar' directory as an artifact named 'Package'. This allows for easy access to compiled binaries after a successful workflow run.

```yaml
steps:
  - uses: actions/checkout@v5
  - uses: actions/setup-java@v4
    with:
      java-version: '17'
      distribution: 'temurin'

  - run: ant -noinput -buildfile build.xml
  - uses: actions/upload-artifact@v4
    with:
      name: Package
      path: build/jar
```

--------------------------------

### Implement Job-Level Concurrency with Specific Groups in GitHub Actions

Source: https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

These examples illustrate how to apply concurrency control at the job level within a GitHub Actions workflow. By defining a `concurrency` group for a job (e.g., `example-group` or `staging_environment`), it ensures that only one instance of that specific job within the defined group can run concurrently, canceling any previous in-progress runs. This is useful for managing resources or preventing conflicts for specific tasks like deployments.

```yaml
on:
  push:
    branches:
      - main

jobs:
  job-1:
    runs-on: ubuntu-latest
    concurrency:
      group: example-group
      cancel-in-progress: true
```

```yaml
jobs:
  job-1:
    runs-on: ubuntu-latest
    concurrency:
      group: staging_environment
      cancel-in-progress: true
```

--------------------------------

### Configure release webhook event in GitHub Actions workflow

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

Triggers a workflow when a release is published in the repository. The `types` keyword filters which release activity types should trigger the workflow. This example runs the workflow only when a release is published, not on other release activities like creation or deletion.

```yaml
on:
  release:
    types: [published]
```

--------------------------------

### Use Environment Variables for API Compatibility

Source: https://docs.github.com/en/actions/how-tos/create-and-publish-actions/manage-custom-actions

Demonstrates using GitHub environment variables to ensure action compatibility across different GitHub platforms (GitHub.com, GitHub Enterprise Server, custom domains). Avoids hard-coded API URLs by using GITHUB_API_URL and GITHUB_GRAPHQL_URL variables.

```text
For the REST API, use the GITHUB_API_URL environment variable.
For GraphQL, use the GITHUB_GRAPHQL_URL environment variable.
```

--------------------------------

### Configure GitHub Action Metadata with YAML

Source: https://docs.github.com/en/actions/creating-actions/creating-a-docker-container-action

This `action.yml` file defines the metadata for a GitHub Action. It declares a `who-to-greet` input with a default value and a `time` output. The action is configured to run using Docker, building from the local `Dockerfile`, and passes the `who-to-greet` input as an argument to the container.

```YAML
# action.yml
name: 'Hello World'
description: 'Greet someone and record the time'
inputs:
  who-to-greet:  # id of input
    description: 'Who to greet'
    required: true
    default: 'World'
outputs:
  time: # id of output
    description: 'The time we greeted you'
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - ${{ inputs.who-to-greet }}
```

--------------------------------

### Mount Volumes in GitHub Actions Container (YAML)

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-where-workflows-run/run-jobs-in-a-container

This YAML snippet demonstrates various ways to mount volumes within a GitHub Actions container. It shows examples of named Docker volumes, anonymous Docker volumes, and bind mounts from the host machine to the container. Volumes are used for sharing data between services or job steps.

```YAML
volumes:
  - my_docker_volume:/volume_mount
  - /data/my_data
  - /source/directory:/destination/directory

```

--------------------------------

### Configure GitHub Actions Runner Job with PostgreSQL Service Container (YAML)

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers

This YAML configuration defines a GitHub Actions job that runs on an `ubuntu-latest` runner. It sets up a PostgreSQL service container, specifying its Docker image, environment variables for the password, health check options to ensure the service is ready, and maps port 5432 from the container to the host machine for accessibility.

```yaml
jobs:
  # Label of the runner job
  runner-job:
    # You must use a Linux environment when using service containers or container jobs
    runs-on: ubuntu-latest

    # Service containers to run with `runner-job`
    services:
      # Label used to access the service container
      postgres:
        # Docker Hub image
        image: postgres
        # Provide the password for postgres
        env:
          POSTGRES_PASSWORD: postgres
        # Set health checks to wait until postgres has started
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5
        ports:
          # Maps tcp port 5432 on service container to the host
          - 5432:5432
```

--------------------------------

### Perform GitHub Actions Importer Audit with Custom Configuration File

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/bamboo-migration

This example shows how to use the `--config-file-path` argument with the `gh actions-importer audit bamboo` subcommand. It instructs the GitHub Actions Importer to use a specified YAML configuration file to define the source files for the audit, rather than relying on default fetching mechanisms. This allows for auditing multiple repositories or specific pipeline definitions.

```bash
gh actions-importer audit bamboo -o tmp/bamboo --config-file-path "./path/to/my/bamboo/config.yml"
```

--------------------------------

### Configure Kubernetes Security Context for Runner Pod

Source: https://docs.github.com/en/actions/tutorials/use-actions-runner-controller/troubleshoot

Sets up fsGroup security context in Kubernetes to resolve permission mismatches when runner containers run as non-root users with persistent volumes. This configuration ensures the mounted volume ownership matches the runner's GID (123 in this example). Replace the fsGroup value and container image version as needed for your deployment.

```yaml
template:
  spec:
    securityContext:
      fsGroup: 123
    containers:
      - name: runner
        image: ghcr.io/actions/actions-runner:latest
        command: ["/home/runner/run.sh"]
```

--------------------------------

### View Policy Controller Helm Chart Configuration Options

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/enforce-artifact-attestations

Displays all available configuration values for the Sigstore Policy Controller Helm chart version 0.10.5. This command helps users understand all customizable options before deploying the policy controller.

```bash
helm show values oci://ghcr.io/sigstore/helm-charts/policy-controller --version 0.10.5
```

--------------------------------

### Filter Pull Requests by Target Branch in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow

Configures a pull_request workflow to run only when targeting specific branches using the branches filter. Supports glob patterns for flexible branch matching. The example triggers for PRs targeting main, mona/octocat, or any releases/* branch.

```yaml
on:
  pull_request:
    # Sequence of patterns matched against refs/heads
    branches:
      - main
      - 'mona/octocat'
      - 'releases/**'
```

--------------------------------

### Configure OIDC Subject for GitHub Actions in Cloud Providers

Source: https://docs.github.com/en/actions/reference/security/oidc

This snippet demonstrates how to configure the OIDC subject string in various cloud providers' trust relationships. The subject 'repo:octo-org/octo-repo:ref:refs/heads/demo-branch' is used to define which GitHub repository and branch are authorized to assume a role. Each example shows the specific syntax required by AWS, Azure, Google Cloud Platform, and HashiCorp Vault.

```AWS
"token.actions.githubusercontent.com:sub": "repo:octo-org/octo-repo:ref:refs/heads/demo-branch"
```

```Azure
repo:octo-org/octo-repo:ref:refs/heads/demo-branch
```

```Google Cloud Platform
(assertion.sub=='repo:octo-org/octo-repo:ref:refs/heads/demo-branch')
```

```HashiCorp Vault
bound_subject="repo:octo-org/octo-repo:ref:refs/heads/demo-branch"
```

--------------------------------

### Configure Push Event with Mixed Branch Inclusion and Exclusion

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Configure a GitHub Actions workflow using both positive and negative patterns for branch filtering. This example shows how to include all releases/* branches while excluding those ending with -alpha using the negation operator (!). Pattern order matters: negative patterns after positive matches will exclude the ref, and positive patterns after negative matches will include it again.

```yaml
on:
  push:
    branches:
      - 'releases/**'
      - '!releases/**-alpha'
```

--------------------------------

### Dynamic Concurrency Groups with Branch References

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Uses dynamic expressions to create concurrency groups based on git references (branches or tags). When a new commit is pushed to main while a previous run is in progress, the previous run is cancelled and the new one starts. This prevents multiple concurrent deployments on the same branch.

```yaml
on:
  push:
    branches:
      - main

concurrency:
  group: ci-${{ github.ref }}
  cancel-in-progress: true
```

--------------------------------

### Configure credentials file for GitHub Actions Importer authentication

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/supplemental-arguments-and-settings

Create a YAML credentials file containing server URLs and access tokens for GitHub Actions Importer to authenticate to multiple servers. The importer uses the credentials for the URL that most closely matches the network request being made.

```yaml
- url: https://github.com
  access_token: ghp_mygeneraltoken
- url: https://github.com/specific_org/
  access_token: ghp_myorgspecifictoken
- url: https://jenkins.org
  access_token: abc123
  username: marty_mcfly
```

--------------------------------

### Get custom OIDC token audience with GitHub Actions toolkit

Source: https://docs.github.com/en/actions/reference/openid-connect-reference

Retrieve a custom OIDC token audience using the GitHub Actions toolkit command. This allows you to set a custom audience claim instead of using the default repository owner URL. The command returns the OIDC token with the specified audience.

```javascript
core.getIDToken(audience)
```

--------------------------------

### Verify SBOM Attestation in SPDX Format with GitHub CLI

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/use-artifact-attestations

Verify SBOM attestations using the GitHub CLI with the SPDX predicate type. Requires specifying the predicate-type flag to reference the SPDX Document v2.3 format.

```bash
gh attestation verify PATH/TO/YOUR/BUILD/ARTIFACT-BINARY \
  -R ORGANIZATION_NAME/REPOSITORY_NAME \
  --predicate-type https://spdx.dev/Document/v2.3
```

--------------------------------

### Convert Apple Signing Certificate to Base64 for GitHub Actions Secret

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/sign-xcode-applications

This command converts an Apple signing certificate (.p12 file) into a Base64 encoded string. The output is copied to the clipboard, ready to be used as a GitHub secret (e.g., BUILD_CERTIFICATE_BASE64). This is a prerequisite for securely storing and using the certificate in a CI workflow on GitHub Actions.

```bash
base64 -i BUILD_CERTIFICATE.p12 | pbcopy
```

--------------------------------

### GitHub-Hosted Runners: Standard Specifications

Source: https://docs.github.com/en/actions/writing-workflows/workflow-syntax-for-github-actions

Reference table of standard GitHub-hosted runner specifications for public repositories, including processor, memory, storage, and architecture details for Linux, Windows, and macOS runners.

```APIDOC
## Standard GitHub-Hosted Runners for Public Repositories

### Description
Standard GitHub-hosted runners available for public repositories with free and unlimited usage.

### Runner Specifications

| Operating System | CPU | Memory | Storage | Architecture | Workflow Label |
|---|---|---|---|---|---|
| Linux | 1 | 5 GB | 14 GB | x64 | `ubuntu-slim` |
| Linux | 4 | 16 GB | 14 GB | x64 | `ubuntu-latest`, `ubuntu-24.04`, `ubuntu-22.04` |
| Windows | 4 | 16 GB | 14 GB | x64 | `windows-latest`, `windows-2025`, `windows-2025-vs2026` (public preview), `windows-2022` |
| Linux | 4 | 16 GB | 14 GB | arm64 | `ubuntu-24.04-arm`, `ubuntu-22.04-arm` |
| Windows | 4 | 16 GB | 14 GB | arm64 | `windows-11-arm` |
| macOS | 4 | 14 GB | 14 GB | Intel | `macos-15-intel` |
| macOS | 3 (M1) | 7 GB | 14 GB | arm64 | `macos-latest`, `macos-14`, `macos-15`, `macos-26` (public preview) |

### Notes
- Each job runs in a fresh instance of the specified runner image
- Single-CPU runners are hosted in containers on shared VMs
- Multi-CPU runners are dedicated virtual machines
- Usage is free and unlimited for public repositories
```

--------------------------------

### GitHub Actions format() Function - String Replacement

Source: https://docs.github.com/en/actions/reference/evaluate-expressions-in-workflows-and-actions

Demonstrates the format() function for replacing placeholders in a string using the {N} syntax where N is an integer index. Supports multiple replacement values and requires escaping curly braces with double braces.

```text
format( string, replaceValue0, replaceValue1, ..., replaceValueN)
```

--------------------------------

### Create GitHub Action Metadata File (action.yml)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-composite-action

Defines a composite GitHub Action with inputs, outputs, and execution steps. The action accepts a 'who-to-greet' input, generates a random number, sets the GitHub path, and executes a goodbye script. Uses bash shell for all steps and exports outputs via $GITHUB_OUTPUT.

```yaml
name: 'Hello World'
description: 'Greet someone'
inputs:
  who-to-greet:  # id of input
    description: 'Who to greet'
    required: true
    default: 'World'
outputs:
  random-number:
    description: "Random number"
    value: ${{ steps.random-number-generator.outputs.random-number }}
runs:
  using: "composite"
  steps:
    - name: Set Greeting
      run: echo "Hello $INPUT_WHO_TO_GREET."
      shell: bash
      env:
        INPUT_WHO_TO_GREET: ${{ inputs.who-to-greet }}

    - name: Random Number Generator
      id: random-number-generator
      run: echo "random-number=$(echo $RANDOM)" >> $GITHUB_OUTPUT
      shell: bash

    - name: Set GitHub Path
      run: echo "$GITHUB_ACTION_PATH" >> $GITHUB_PATH
      shell: bash
      env:
        GITHUB_ACTION_PATH: ${{ github.action_path }}

    - name: Run goodbye.sh
      run: goodbye.sh
      shell: bash
```

--------------------------------

### Run Job Regardless of Dependency Status with always() in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Use the always() conditional expression with the needs keyword to run a job even if its dependencies fail or are skipped. This example shows job3 running after job1 and job2 complete, regardless of their success status.

```yaml
jobs:
  job1:
  job2:
    needs: job1
  job3:
    if: ${{ always() }}
    needs: [job1, job2]
```

--------------------------------

### Matrix Configuration - Travis CI vs GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-travis-ci-to-github-actions

Demonstrates how to define test matrices in both Travis CI and GitHub Actions. Travis CI uses the 'matrix' key with 'include' to specify Ruby versions, while GitHub Actions uses 'strategy.matrix' under jobs. Both allow testing across multiple environment configurations.

```yaml
matrix:
  include:
    - rvm: '2.5'
    - rvm: '2.6.3'
```

```yaml
jobs:
  build:
    strategy:
      matrix:
        ruby: ['2.5', '2.6.3']
```

--------------------------------

### Setting Debug Messages in GitHub Actions Workflows

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands

This snippet shows how to output debug messages to the GitHub Actions log using the `::debug` workflow command. To view these messages, a secret named `ACTIONS_STEP_DEBUG` must be set to `true` in the repository or organization settings. Examples are provided for general syntax, Bash, and PowerShell.

```Text
::debug::{message}
```

```Bash
echo "::debug::Set the Octocat variable"
```

```PowerShell
Write-Output "::debug::Set the Octocat variable"
```

--------------------------------

### Configure repository_dispatch webhook event in GitHub Actions workflow

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

Triggers a workflow using a custom webhook event via the GitHub API. The `types` keyword specifies which `event_type` values should trigger the workflow. This example runs the workflow when a `test_result` event type is dispatched to the repository.

```yaml
on:
  repository_dispatch:
    types: [test_result]
```

--------------------------------

### Compile GitHub Action JavaScript with Rollup (CLI)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

This command-line instruction executes Rollup using the `rollup.config.js` file. It triggers the bundling process, which combines the GitHub Action's source code and its dependencies into a single `dist/index.js` file, ready for deployment and use in workflows.

```bash
rollup --config rollup.config.js
```

--------------------------------

### Configure post-entrypoint cleanup script in Docker action

Source: https://docs.github.com/en/actions/creating-actions/metadata-syntax-for-github-actions

Defines a post-entrypoint script that runs after the main entrypoint action completes, typically for cleanup operations. Executes in a new container with the same base image, requiring state access through workspace, HOME, or STATE_ variables.

```yaml
runs:
  using: 'docker'
  image: 'Dockerfile'
  args:
    - 'bzz'
  entrypoint: 'main.sh'
  post-entrypoint: 'cleanup.sh'
```

--------------------------------

### Trigger GitHub Actions Workflow on `milestone` Event

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

This configuration triggers a GitHub Actions workflow when a milestone in the repository is created or modified. The example specifically runs the workflow when a milestone has been `opened` or `deleted`. Workflows triggered by this event will only run if the workflow file exists on the default branch.

```yaml
on:
  milestone:
    types: [opened, deleted]

```

--------------------------------

### Configure GitHub Actions Job with Ubuntu Runner Label

Source: https://docs.github.com/en/actions/how-tos/manage-runners/larger-runners/use-larger-runners_platform=linux

Sets up a GitHub Actions workflow that routes a job to an Ubuntu runner with the `ubuntu-24.04-16core` label. The workflow checks out code, sets up Node.js version 14, installs bats globally, and runs bats version check. This ensures the job runs on a larger Ubuntu runner with sufficient resources.

```yaml
name: learn-github-actions
on: [push]
jobs:
  check-bats-version:
    runs-on:
      labels: ubuntu-24.04-16core
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '14'
      - run: npm install -g bats
      - run: bats -v
```

--------------------------------

### Referencing an External GitHub Action from a Different Repository

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/find-and-customize-actions

This YAML snippet illustrates how to incorporate an action hosted in a different public repository into a workflow. It uses the `{owner}/{repo}@{ref}` syntax to specify the action and its version, such as `actions/setup-node@v4`.

```yaml
jobs:
  my_first_job:
    steps:
      - name: My first step
        uses: actions/setup-node@v4
```

--------------------------------

### Illustrating GitHub Actions Local Repository Structure

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/find-and-customize-actions

This snippet displays a typical file structure for a GitHub repository that contains a local action. It shows the relative placement of the workflow file and the action's definition within the repository's `.github` directory.

```text
|-- hello-world (repository)
|   |__ .github
|       └── workflows
|           └── my-first-workflow.yml
|       └── actions
|           |__ hello-world-action
|               └── action.yml
```

--------------------------------

### Using `format` for string interpolation in GitHub Actions expressions

Source: https://docs.github.com/en/actions/learn-github-actions/expressions

The `format` function allows for string interpolation using positional arguments. It replaces placeholders like `{0}`, `{1}` with provided values. This function is useful for constructing dynamic messages or strings within GitHub Actions workflows. The examples demonstrate basic usage and how to escape literal curly braces.

```github-actions-expression
format('Hello {0} {1} {2}', 'Mona', 'the', 'Octocat')
```

```github-actions-expression
format('{{Hello {0} {1} {2}!}}', 'Mona', 'the', 'Octocat')
```

--------------------------------

### Implement Conditional Job Execution in GitLab CI/CD and GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/manual-migrations/migrate-from-gitlab-cicd

These examples demonstrate how to make jobs run conditionally based on specific criteria. GitLab CI/CD uses `rules` with an `if` condition, often checking environment variables like `CI_COMMIT_BRANCH`. GitHub Actions uses the `if` keyword directly on the job, evaluating expressions like `contains(github.ref, 'master')`.

```yaml
deploy_prod:
  stage: deploy
  script:
    - echo "Deploy to production server"
  rules:
    - if: '$CI_COMMIT_BRANCH == "master"'
```

```yaml
jobs:
  deploy_prod:
    if: contains( github.ref, 'master')
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploy to production server"
```

--------------------------------

### GitHub Actions Workflow - Python to Azure Web App

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/python-to-azure-app-service

Complete GitHub Actions workflow that builds a Python application and deploys it to Azure Web App. The workflow runs on push to main branch, sets up Python environment, installs dependencies with caching, uploads build artifacts, and deploys to Azure using the official Azure webapps-deploy action. Requires AZURE_WEBAPP_PUBLISH_PROFILE secret to be configured.

```yaml
name: Build and deploy Python app to Azure Web App

env:
  AZURE_WEBAPP_NAME: MY_WEBAPP_NAME   # set this to your application's name
  PYTHON_VERSION: '3.8'               # set this to the Python version to use

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5

      - name: Set up Python version
        uses: actions/setup-python@v5
        with:
          python-version: ${{ env.PYTHON_VERSION }}

      - name: Create and start virtual environment
        run: |
          python -m venv venv
          source venv/bin/activate

      - name: Set up dependency caching for faster installs
        uses: actions/cache@v4
        with:
          path: ~/.cache/pip
          key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
          restore-keys: |
            ${{ runner.os }}-pip-

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Upload artifact for deployment jobs
        uses: actions/upload-artifact@v4
        with:
          name: python-app
          path: |
            .
            !venv/
  deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: 'production'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}

    steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v5
        with:
          name: python-app
          path: .

      - name: 'Deploy to Azure Web App'
        id: deploy-to-webapp
        uses: azure/webapps-deploy@85270a1854658d167ab239bce43949edb336fa7c
        with:
          app-name: ${{ env.AZURE_WEBAPP_NAME }}
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
```

--------------------------------

### Create Kubernetes Secret for Personal Access Token Authentication

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/authenticating-to-the-github-api

Creates a Kubernetes secret containing a personal access token (classic) for Actions Runner Controller authentication. The secret must be created in the same namespace where the gha-runner-scale-set chart is installed (e.g., arc-runners). Required scopes are 'repo' for repository runners or 'admin:org' for organization runners.

```bash
kubectl create secret generic pre-defined-secret \
   --namespace=arc-runners \
   --from-literal=github_token='YOUR-PAT'
```

--------------------------------

### Configure Push Event with Branch and Tag Exclusion Filters

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Configure a GitHub Actions workflow to skip execution on specific branches and tags using exclusion filters. This example demonstrates how to exclude branches matching patterns like mona/octocat and releases/**-alpha, as well as specific tags. The workflow runs on all push events except those matching the exclusion patterns.

```yaml
on:
  push:
    # Sequence of patterns matched against refs/heads
    branches-ignore:
      - 'mona/octocat'
      - 'releases/**-alpha'
    # Sequence of patterns matched against refs/tags
    tags-ignore:
      - v2
      - v1.*
```

--------------------------------

### Define GitHub Actions Expression Literals

Source: https://docs.github.com/en/actions/learn-github-actions/expressions

This example demonstrates how to define various literal data types (null, boolean, integer, float, hexadecimal, exponential numbers, and strings) within GitHub Actions workflow expressions. Strings can be defined directly or within single quotes inside expressions, with single quotes escaped by doubling them.

```yaml
env:
  myNull: ${{ null }}
  myBoolean: ${{ false }}
  myIntegerNumber: ${{ 711 }}
  myFloatNumber: ${{ -9.2 }}
  myHexNumber: ${{ 0xff }}
  myExponentialNumber: ${{ -2.99e-2 }}
  myString: Mona the Octocat
  myStringInBraces: ${{ 'It''s open source!' }}
```

--------------------------------

### Define GitHub Actions environment variables at workflow, job, and step levels

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/use-variables

This GitHub Actions workflow demonstrates how to define environment variables at different scopes: workflow-level (`DAY_OF_WEEK`), job-level (`Greeting`), and step-level (`First_Name`). These variables are then accessed within a `run` step using shell environment variable syntax. This example illustrates variable scoping and access within a single workflow.

```yaml
name: Greeting on variable day

on:
  workflow_dispatch

env:
  DAY_OF_WEEK: Monday

jobs:
  greeting_job:
    runs-on: ubuntu-latest
    env:
      Greeting: Hello
    steps:
      - name: "Say Hello Mona it's Monday"
        run: echo "$Greeting $First_Name. Today is $DAY_OF_WEEK!"
        env:
          First_Name: Mona
```

--------------------------------

### Build Docker Image for GKE Deployment

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/google-kubernetes-engine

This 'docker build' command constructs a Docker image from the Dockerfile in the current directory. It tags the image with a unique identifier combining the Google Cloud Project ID, image name, and the Git commit SHA, ensuring version traceability. It also passes the 'GITHUB_SHA' and 'GITHUB_REF' as build arguments.

```bash
docker build \
          --tag "gcr.io/$PROJECT_ID/$IMAGE:$GITHUB_SHA" \
          --build-arg GITHUB_SHA="$GITHUB_SHA" \
          --build-arg GITHUB_REF="$GITHUB_REF" \
          .
```

--------------------------------

### List GitHub Actions Runner Services on Linux

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/monitor-and-troubleshoot_platform=linux

Query systemctl to display all running GitHub Actions runner services with their status and descriptions. Useful for identifying available self-hosted runners on a Linux system.

```bash
systemctl --type=service | grep actions.runner
```

--------------------------------

### Secure Inline Script Input with Environment Variables in GitHub Actions

Source: https://docs.github.com/en/actions/reference/secure-use-reference

This example shows how to safely handle untrusted input within inline shell scripts in GitHub Actions by assigning the input to an intermediate environment variable. The `github.event.pull_request.title` value is stored in the `TITLE` environment variable, which is then processed by a Bash script. This method prevents script injection by isolating the input from the script generation process.

```yaml
- name: Check PR title
        env:
          TITLE: ${{ github.event.pull_request.title }}
        run: |
          if [[ "$TITLE" =~ ^octocat ]]; then
          echo "PR title starts with 'octocat'"
          exit 0
          else
          echo "PR title did not start with 'octocat'"
          exit 1
          fi
```

--------------------------------

### GitHub App Credentials JSON Format for Azure Key Vault

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/authenticating-to-the-github-api

Defines the JSON structure required for storing GitHub App credentials in Azure Key Vault. The secret must include the app ID, installation ID, and private key for GitHub App authentication.

```json
{
  "github_app_id": "APP_ID_OR_CLIENT_ID",
  "github_app_installation_id": "INSTALLATION_ID",
  "github_app_private_key": "PRIVATE_KEY"
}
```

--------------------------------

### Configure GitHub Actions Matrix Strategy for OS and Node.js Versions

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

This workflow demonstrates using the `matrix` context in GitHub Actions to run jobs across multiple operating systems and Node.js versions. It defines a matrix with `os` and `node` keys, then uses these properties to set the runner type and Node.js version for each job. This allows for efficient testing across various environments.

```yaml
name: Test matrix
on: push

jobs:
  build:
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest]
        node: [14, 16]
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node }}
      - name: Output node version
        run: node --version
```

--------------------------------

### Disable TLS certificate verification for GitHub Actions self-hosted runner

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/monitoring-and-troubleshooting-self-hosted-runners

This snippet shows how to temporarily disable TLS certificate verification for a self-hosted runner by setting the `GITHUB_ACTIONS_RUNNER_TLS_NO_VERIFY` environment variable to `1`. This can be useful for troubleshooting network problems, but is not recommended for production environments due to security implications. It includes examples for both Linux/macOS and Windows environments.

```bash
export GITHUB_ACTIONS_RUNNER_TLS_NO_VERIFY=1
./config.sh --url https://github.com/YOUR-ORG/YOUR-REPO --token
./run.sh
```

```cmd
[Environment]::SetEnvironmentVariable('GITHUB_ACTIONS_RUNNER_TLS_NO_VERIFY', '1')
./config.cmd --url https://github.com/YOUR-ORG/YOUR-REPO --token
./run.cmd
```

--------------------------------

### Filter Workflow by Event Types in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Define specific activity types that trigger a workflow using the `types` keyword under an event name. This narrows down which activities cause the workflow to run. For example, filtering the `label` event to only trigger on `created` and `edited` activities, not `deleted`.

```yaml
on:
  label:
    types: [created, edited]
```

--------------------------------

### runs.steps[*].working-directory

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Specifies the working directory for the step's commands.

```APIDOC
## Configuration Property runs.steps[*].working-directory

### Description
Specifies the working directory where the command is run.

### Method
Configuration Property

### Endpoint
runs.steps[*].working-directory

### Parameters
#### Request Body
- **working-directory** (string) - Optional - The path to the working directory.

### Request Example
{
  "working-directory": "./src"
}
```

--------------------------------

### GitHub App Configuration for Deployment Protection Rules

Source: https://docs.github.com/en/actions/how-tos/deploy/configure-and-manage-deployments/create-custom-protection-rules

Configure a GitHub App with the required permissions and event subscriptions to enable custom deployment protection rules. This includes setting up repository permissions and subscribing to deployment protection rule events.

```APIDOC
## GitHub App Configuration for Deployment Protection Rules

### Description
Step-by-step configuration guide for setting up a GitHub App to handle custom deployment protection rules.

### Required Configuration Steps

#### 1. Callback URL (Optional)
- **Field**: Callback URL
- **Location**: "Identifying and authorizing users" section
- **Purpose**: URL for user authorization callbacks
- **Reference**: See About the user authorization callback URL

#### 2. Repository Permissions
- **Actions**: Access: Read-only
  - Allows reading workflow and action information
- **Deployments**: Access: Read and write
  - Allows reading and modifying deployment states

#### 3. Event Subscriptions
- **Required Event**: Deployment protection rule
  - Triggers when a workflow reaches a job referencing an environment with the custom deployment protection rule enabled
  - Sends a POST request with `deployment_protection_rule` payload

### Webhook Payload Structure
```
{
  "action": "requested",
  "deployment_protection_rule": {
    "id": 12345,
    "node_id": "MDEyOkRlcGxveW1lbnRQcm90ZWN0aW9uUnVsZTEyMzQ1",
    "app": {
      "id": 67890,
      "slug": "my-deployment-app",
      "name": "My Deployment App"
    }
  },
  "deployment": {
    "id": 11111,
    "node_id": "MDEyOkRlcGxveW1lbnQxMTExMQ==",
    "url": "https://api.github.com/repos/OWNER/REPO/deployments/11111",
    "environment": "production",
    "ref": "refs/heads/main",
    "sha": "abc123def456",
    "task": "deploy",
    "payload": {},
    "original_environment": "production",
    "description": "Deployment to production",
    "creator": {
      "login": "octocat",
      "id": 1
    },
    "created_at": "2024-01-10T10:00:00Z",
    "updated_at": "2024-01-10T10:00:00Z",
    "statuses_url": "https://api.github.com/repos/OWNER/REPO/deployments/11111/statuses",
    "repository_url": "https://api.github.com/repos/OWNER/REPO"
  },
  "pull_requests": [],
  "repository": {
    "id": 22222,
    "name": "REPO",
    "full_name": "OWNER/REPO",
    "owner": {
      "login": "OWNER",
      "id": 2
    },
    "private": false,
    "html_url": "https://github.com/OWNER/REPO",
    "description": "Repository description",
    "url": "https://api.github.com/repos/OWNER/REPO"
  },
  "organization": {
    "login": "OWNER",
    "id": 2
  },
  "sender": {
    "login": "github-actions[bot]",
    "id": 41898282
  },
  "installation": {
    "id": 33333,
    "node_id": "MDIzOkluc3RhbGxhdGlvbjMzMzMz"
  }
}
```

### Security Requirements
1. Validate incoming POST requests (see Validating webhook deliveries)
2. Use JWT authentication as a GitHub App
3. Generate installation tokens with appropriate permissions
4. Scope tokens to specific repositories when possible
```

--------------------------------

### Configure Credentials for GitHub Actions Importer

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/use-github-actions-importer

This command initiates an interactive prompt to set up authentication credentials for GitHub Actions Importer. These credentials are vital for the Importer to securely communicate with both GitHub and your existing CI servers during the migration process.

```bash
gh actions-importer configure
```

--------------------------------

### Publish Maven packages to Maven Central and GitHub Packages workflow

Source: https://docs.github.com/en/actions/tutorials/publish-packages/publish-java-packages-with-maven

GitHub Actions workflow that publishes Java packages to both Maven Central Repository and GitHub Packages. The workflow triggers on release creation, checks out the repository, configures Java with setup-java action twice (once for OSSRH, once for GitHub Packages), and runs Maven deploy commands with appropriate authentication credentials from secrets.

```yaml
name: Publish package to the Maven Central Repository and GitHub Packages
on:
  release:
    types: [created]
jobs:
  publish:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
    steps:
      - uses: actions/checkout@v5
      - name: Set up Java for publishing to Maven Central Repository
        uses: actions/setup-java@v4
        with:
          java-version: '11'
          distribution: 'temurin'
          server-id: ossrh
          server-username: MAVEN_USERNAME
          server-password: MAVEN_PASSWORD
      - name: Publish to the Maven Central Repository
        run: mvn --batch-mode deploy
        env:
          MAVEN_USERNAME: ${{ secrets.OSSRH_USERNAME }}
          MAVEN_PASSWORD: ${{ secrets.OSSRH_TOKEN }}
      - name: Set up Java for publishing to GitHub Packages
        uses: actions/setup-java@v4
        with:
          java-version: '11'
          distribution: 'temurin'
      - name: Publish to GitHub Packages
        run: mvn --batch-mode deploy
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

--------------------------------

### jobs.<job_id>.services.<service_id>.options

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

Provides additional Docker container resource options, mirroring those available for `docker create` commands. Note that the `--network` option is not supported.

```APIDOC
## CONFIG jobs.<job_id>.services.<service_id>.options

### Description
Provides additional Docker container resource options, mirroring those available for `docker create` commands. Note that the `--network` option is not supported.

### Method
CONFIG

### Endpoint
jobs.<job_id>.services.<service_id>.options

### Parameters
#### Request Body
- **<docker_option>** (string) - Optional - A Docker `create` option, e.g., `--cpus 1`.

### Request Example
```yaml
services:
  my-service:
    image: my-image
    options: --cpus 1 --memory 2g
```

### Response
#### Success Response (200)
- No direct response. Configuration applied.
```

--------------------------------

### Define a reusable GitHub Actions workflow using workflow_call

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

This example shows how to mark a GitHub Actions workflow as callable by other workflows using the `workflow_call` event. When triggered this way, the called workflow receives the same event payload as the calling workflow, enabling efficient workflow reuse and modularity.

```yaml
on: workflow_call
```

--------------------------------

### Example Output of a GitHub Actions Script Injection Attack

Source: https://docs.github.com/en/actions/concepts/security/script-injections

This console output illustrates the successful execution of an injected command within a GitHub Actions workflow. By providing a malicious pull request title like `a"; ls $GITHUB_WORKSPACE"`, an attacker can bypass the intended logic and execute arbitrary shell commands, such as listing the contents of the runner's workspace.

```shell
Run title="a"; ls $GITHUB_WORKSPACE""
README.md
code.yml
example.js
```

--------------------------------

### Clean up keychain and provisioning profile on self-hosted runners

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/sign-xcode-applications

A GitHub Actions workflow step that removes sensitive Apple certificate and provisioning profile files from self-hosted runners after job completion. This step uses the `always()` condition to ensure cleanup occurs regardless of job success or failure, preventing sensitive files from persisting on the runner.

```yaml
- name: Clean up keychain and provisioning profile
  if: ${{ always() }}
  run: |
    security delete-keychain $RUNNER_TEMP/app-signing.keychain-db
    rm ~/Library/MobileDevice/Provisioning\ Profiles/build_pp.mobileprovision
```

--------------------------------

### Access repository_dispatch client payload in GitHub Actions workflow

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

Demonstrates how to access custom data from a `repository_dispatch` event's `client_payload` in a workflow. This example uses conditional logic to run a job only if the test passed is false, and accesses the error message from the payload via environment variables.

```yaml
on:
  repository_dispatch:
    types: [test_result]

jobs:
  run_if_failure:
    if: ${{ !github.event.client_payload.passed }}
    runs-on: ubuntu-latest
    steps:
      - env:
          MESSAGE: ${{ github.event.client_payload.message }}
        run: echo $MESSAGE
```

--------------------------------

### GitHub Actions Workflow: Build, Push, and Attest Docker Image

Source: https://docs.github.com/en/actions/tutorials/publish-packages/publish-docker-images

This GitHub Actions workflow defines a single job that runs on `ubuntu-latest` to build and push a Docker image to a container registry. It includes steps for repository checkout, logging into the registry, extracting image metadata (tags, labels), building and pushing the Docker image, and generating an artifact attestation to enhance supply chain security.

```yaml
jobs:
  build-and-push-image:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      packages: write
      attestations: write
      id-token: write
    steps:
      - name: Checkout repository
        uses: actions/checkout@v5
      - name: Log in to the Container registry
        uses: docker/login-action@65b78e6e13532edd9afa3aa52ac7964289d1a9c1
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      - name: Extract metadata (tags, labels) for Docker
        id: meta
        uses: docker/metadata-action@9ec57ed1fcdbf14dcef7dfbe97b2010124a938b7
        with:
          images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
      - name: Build and push Docker image
        id: push
        uses: docker/build-push-action@f2a1d5e99d037542a71f64918e516c093c6f3fc4
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
          labels: ${{ steps.meta.outputs.labels }}
      - name: Generate artifact attestation
        uses: actions/attest-build-provenance@v3
        with:
          subject-name: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME}}
          subject-digest: ${{ steps.push.outputs.digest }}
          push-to-registry: true
```

--------------------------------

### Run Job Conditionally on `pull_request` Review Request by Specific Team (YAML)

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

This example illustrates how to trigger a workflow when a review is requested on a pull request, and then conditionally execute a specific job. The `specific_review_requested` job will only run if the review request originates from the 'octo-team', utilizing the `github.event.requested_team.name` context in an `if` condition.

```yaml
on:
  pull_request:
    types: [review_requested]
jobs:
  specific_review_requested:
    runs-on: ubuntu-latest
    if: ${{ github.event.requested_team.name == 'octo-team'}}
    steps:
      - run: echo 'A review from octo-team was requested'

```

--------------------------------

### Verify File Permissions in Git Index (Git Shell)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-docker-container-action

This Git command checks and displays the permission mode of a file as recorded in the Git index. It confirms that the executable permission (`+x`) has been successfully applied to `entrypoint.sh`. An output like `755` indicates executable permission.

```Shell
git ls-files --stage entrypoint.sh

```

--------------------------------

### Check GitHub Actions self-hosted runner network connectivity

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/monitoring-and-troubleshooting-self-hosted-runners

This snippet demonstrates how to use the `config` script with the `--check` parameter to verify that a self-hosted runner can access all required network services on GitHub. It requires a GitHub URL and a personal access token (PAT) with `workflow` scope or fine-grained access. The script outputs `PASS` or `FAIL` for each service, with detailed logs available in the `_diag` directory.

```bash
./config.sh --check --url URL --pat ghp_abcd1234
```

```cmd
config.cmd --check --url https://github.com/YOUR-ORG/YOUR-REPO --pat GHP_ABCD1234
```

--------------------------------

### Authenticate GitHub Actions Service Containers with Image Registries (Docker Hub, GHCR) YAML

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/use-docker-service-containers

This example illustrates how to provide authentication credentials for service containers in GitHub Actions. It shows how to authenticate with Docker Hub using secrets for username and password, and with GitHub Container Registry (GHCR) using `github.repository_owner` and a secret for the password. This enables using private images or bypassing Docker Hub rate limits.

```yaml
jobs:
  build:
    services:
      redis:
        # Docker Hub image
        image: redis
        ports:
          - 6379:6379
        credentials:
          username: ${{ secrets.dockerhub_username }}
          password: ${{ secrets.dockerhub_password }}
      db:
        # Private registry image
        image: ghcr.io/octocat/testdb:latest
        credentials:
          username: ${{ github.repository_owner }}
          password: ${{ secrets.ghcr_password }}
```

--------------------------------

### GitHub Actions Workflow to Stop and Start Commands (YAML)

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands

This GitHub Actions workflow demonstrates how to temporarily disable and re-enable the processing of workflow commands within a job. It illustrates the use of a unique token (generated via `uuidgen` on Ubuntu or `New-Guid` on Windows) to control when `::warning::` commands are processed, preventing accidental command execution for specific log outputs.

```yaml
jobs:
  workflow-command-job:
    runs-on: ubuntu-latest
    steps:
      - name: Disable workflow commands
        run: |
          echo '::warning:: This is a warning message, to demonstrate that commands are being processed.'
          stopMarker=$(uuidgen)
          echo "::stop-commands::$stopMarker"
          echo '::warning:: This will NOT be rendered as a warning, because stop-commands has been invoked.'
          echo "::$stopMarker::"
          echo '::warning:: This is a warning again, because stop-commands has been turned off.'
```

```yaml
jobs:
  workflow-command-job:
    runs-on: windows-latest
    steps:
      - name: Disable workflow commands
        run: |
          Write-Output '::warning:: This is a warning message, to demonstrate that commands are being processed.'
          $stopMarker = New-Guid
          Write-Output "::stop-commands::$stopMarker"
          Write-Output '::warning:: This will NOT be rendered as a warning, because stop-commands has been invoked.'
          Write-Output "::$stopMarker::"
          Write-Output '::warning:: This is a warning again, because stop-commands has been turned off.'
```

--------------------------------

### Use Kubernetes Init Container to Change Volume Ownership for GitHub Actions Runner

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/troubleshooting-actions-runner-controller-errors

This YAML snippet illustrates how to use an `initContainer` in a Kubernetes pod template to recursively change the ownership of a mounted volume (`/home/runner/_work`) before the main runner container starts. This workaround addresses permission denied errors when `securityContext.fsGroup` is not a viable solution, ensuring the runner has proper access to its work directory.

```yaml
template:
  spec:
    initContainers:
      - name: kube-init
        image: ghcr.io/actions/actions-runner:latest
        command: ["sudo", "chown", "-R", "1001:123", "/home/runner/_work"]
    volumeMounts:
      - name: work
        mountPath: /home/runner/_work
    containers:
      - name: runner
        image: ghcr.io/actions/actions-runner:latest
        command: ["/home/runner/run.sh"]

```

--------------------------------

### Format a string with positional arguments in GitHub Actions

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/expressions

Demonstrates the basic usage of the `format` function to substitute placeholders with provided arguments. It takes a format string and a variable number of arguments, returning the formatted string.

```expression
format('Hello {0} {1} {2}', 'Mona', 'the', 'Octocat')
```

--------------------------------

### Set Minimum Active Runners in ARC (YAML)

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

This example shows how to configure the Actions Runner Controller (ARC) to maintain a specified minimum number of active runners. By setting `minRunners` to a positive value and commenting out `maxRunners`, ARC ensures that a constant pool of idle runners is always available, ready to pick up jobs immediately. This helps reduce job startup latency.

```yaml
## maxRunners is the max number of runners the auto scaling runner set will scale up to.
# maxRunners: 0

## minRunners is the min number of idle runners. The target number of runners created will be
## calculated as a sum of minRunners and the number of jobs assigned to the scale set.
minRunners: 20

```

--------------------------------

### Configure Job-Level Concurrency in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

Limits concurrency at the individual job level within a workflow using the concurrency keyword. This allows different jobs to have different concurrency settings. The example shows a job running on ubuntu-latest with a named concurrency group that cancels in-progress runs.

```yaml
on:
  push:
    branches:
      - main

jobs:
  job-1:
    runs-on: ubuntu-latest
    concurrency:
      group: example-group
      cancel-in-progress: true
```

--------------------------------

### Output to Container Mounted Directory

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/supplemental-arguments-and-settings

Path arguments in GitHub Actions Importer are relative to the container's disk. The container's /data directory is mounted to the directory where the command is executed. Use /data/ prefix for output paths to ensure files are written to the correct host directory.

```shell
gh actions-importer audit --output-dir /data/out
```

--------------------------------

### Display GitHub Actions Importer Dry-Run Subcommand Help

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/use-github-actions-importer

This command displays the help message for the `dry-run` subcommand of the GitHub Actions Importer CLI. It outlines how to convert a pipeline from various CI/CD platforms to a GitHub Actions workflow and output the resulting YAML file to the local filesystem without actually performing a migration.

```shell
gh actions-importer dry-run -h
```

--------------------------------

### Create Action Metadata Configuration in YAML

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

Define the action.yml metadata file that specifies the action's name, description, inputs (who-to-greet), outputs (time), and runtime configuration (Node.js 20). This file tells the action runner how to execute the JavaScript action.

```yaml
name: Hello World
description: Greet someone and record the time

inputs:
  who-to-greet: # id of input
    description: Who to greet
    required: true
    default: World

outputs:
  time: # id of output
    description: The time we greeted you

runs:
  using: node20
  main: dist/index.js
```

--------------------------------

### Set Step Output Using GITHUB_OUTPUT File Path

Source: https://docs.github.com/en/actions/reference/variables-reference

Demonstrates how to use the GITHUB_OUTPUT variable to set outputs for the current step that can be referenced by subsequent steps in a workflow. The GITHUB_OUTPUT variable contains the path to a file used for setting step outputs via workflow commands.

```bash
#!/bin/bash
echo "status=success" >> $GITHUB_OUTPUT
echo "version=1.0.0" >> $GITHUB_OUTPUT
echo "build_time=$(date)" >> $GITHUB_OUTPUT
```

--------------------------------

### GitHub Actions Workflow Filter Patterns with YAML Quoting

Source: https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

These YAML snippets demonstrate the correct and incorrect syntax for defining path and branch filters in GitHub Actions workflows, particularly when using special characters like `*` or `[` and `]`. It highlights the critical need to enclose patterns in single quotes (`'`) when they start with or contain YAML special characters to prevent parsing errors and ensure the workflow runs as intended.

```yaml
# Valid
paths:
  - '**/README.md'
```

```yaml
# Invalid - creates a parse error that
# prevents your workflow from running.
paths:
  - **/README.md
```

```yaml
# Valid
branches: [ main, 'release/v[0-9].[0-9]' ]
```

```yaml
# Invalid - creates a parse error
branches: [ main, release/v[0-9].[0-9] ]
```

--------------------------------

### Delete Job Summary Content in GitHub Actions

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-commands_tool=bash

Removes all job summary content by appending markdown to the summary file and then deleting it. This example shows implementations for both Bash and PowerShell shells. Note that job summaries are uploaded after step completion, so deletion must occur before the step ends.

```bash
- name: Delete all summary content
  run: |
    echo "Adding Markdown content that we want to remove before the step ends" >> $GITHUB_STEP_SUMMARY
    rm $GITHUB_STEP_SUMMARY
```

```powershell
- name: Delete all summary content
  run: |
    "Adding Markdown content that we want to remove before the step ends" >> $env:GITHUB_STEP_SUMMARY
    Remove-Item $env:GITHUB_STEP_SUMMARY
```

--------------------------------

### Configure AWS Credentials and Upload to S3 - GitHub Actions Workflow

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/security-harden-deployments/oidc-in-aws

A GitHub Actions workflow that authenticates with AWS using OIDC, configures AWS credentials, and uploads files to an S3 bucket. The workflow requires id-token write permission for JWT requests and contents read permission for repository checkout. Replace BUCKET-NAME, AWS-REGION, and ROLE-TO-ASSUME with your actual values.

```yaml
# Sample workflow to access AWS resources when workflow is tied to branch
# The workflow creates a static website using Amazon S3
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
name: AWS example workflow
on:
  push
env:
  BUCKET_NAME : "BUCKET-NAME"
  AWS_REGION : "AWS-REGION"
# permission can be added at job level or workflow level
permissions:
  id-token: write   # This is required for requesting the JWT
  contents: read    # This is required for actions/checkout
jobs:
  S3PackageUpload:
    runs-on: ubuntu-latest
    steps:
      - name: Git clone the repository
        uses: actions/checkout@v5
      - name: configure aws credentials
        uses: aws-actions/configure-aws-credentials@e3dd6a429d7300a6a4c196c26e071d42e0343502
        with:
          role-to-assume: ROLE-TO-ASSUME
          role-session-name: samplerolesession
          aws-region: ${{ env.AWS_REGION }}
      # Upload a file to AWS s3
      - name: Copy index.html to s3
        run: |
          aws s3 cp ./index.html s3://${{ env.BUCKET_NAME }}/

```

--------------------------------

### Excluding Matrix Configurations in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/run-job-variations

This snippet demonstrates how to use `jobs.<job_id>.strategy.matrix.exclude` to prevent specific job configurations from running within a GitHub Actions workflow matrix. It shows an example where certain combinations of OS, version, and environment are explicitly excluded from the workflow execution.

```yaml
strategy:
  matrix:
    os: [macos-latest, windows-latest]
    version: [12, 14, 16]
    environment: [staging, production]
    exclude:
      - os: macos-latest
        version: 12
        environment: production
      - os: windows-latest
        version: 16
runs-on: ${{ matrix.os }}
```

--------------------------------

### Build and Push Docker Image using GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/publish-packages/publish-docker-images

This GitHub Actions step uses the `docker/build-push-action` to build a Docker image from the repository's `Dockerfile` and push it to GitHub Packages. It configures the build context to the current directory and applies dynamic tags and labels generated from a previous 'meta' step, enhancing image traceability and organization.

```yaml
uses: docker/build-push-action@f2a1d5e99d037542a71f64918e516c093c6f3fc4
with:
  context: .
  push: true
  tags: ${{ steps.meta.outputs.tags }}
  labels: ${{ steps.meta.outputs.labels }}
```

--------------------------------

### Pin GitHub Action to branch reference

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/find-and-customize-actions

Demonstrates referencing a GitHub Action using a branch name (e.g., @main) to always run the current version on that branch. This approach automatically receives all updates but can introduce breaking changes if the branch is updated with incompatible modifications. Use with caution in production workflows.

```yaml
steps:
  - uses: actions/javascript-action@main
```

--------------------------------

### Configure Windows Proxy using netsh for WinHTTP

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/use-proxy-servers

This command configures system-wide proxy settings on Windows using `netsh winhttp`. It sets a proxy server and specifies bypass addresses for applications that rely on the WinHTTP API. Using `setting-scope=machine` ensures persistence across reboots and during VM imaging.

```Shell
netsh winhttp set advproxy setting-scope=machine settings={\"Proxy\":\"proxy.local:8080\",\"ProxyBypass\":\"168.63.129.16;169.254.169.254\",\"AutoconfigUrl\":\"\",\"AutoDetect\":false}
```

--------------------------------

### Upload Go test results as artifacts

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

Workflow that tests Go code across multiple versions (1.19, 1.20, 1.21.x) using a matrix strategy, generates JSON test results, and uploads them as artifacts using the upload-artifact action. Each test result is stored with a version-specific name for later analysis.

```yaml
name: Upload Go test results

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        go-version: [ '1.19', '1.20', '1.21.x' ]

    steps:
      - uses: actions/checkout@v5
      - name: Setup Go
        uses: actions/setup-go@v5
        with:
          go-version: ${{ matrix.go-version }}
      - name: Install dependencies
        run: go get .
      - name: Test with Go
        run: go test -json > TestResults-${{ matrix.go-version }}.json
      - name: Upload Go test results
        uses: actions/upload-artifact@v4
        with:
          name: Go-results-${{ matrix.go-version }}
          path: TestResults-${{ matrix.go-version }}.json
```

--------------------------------

### Configure ARC for Job Queue Draining (YAML)

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller

This example demonstrates how to configure the Actions Runner Controller (ARC) to stop creating new runner pods, effectively draining the job queue. By setting both `maxRunners` and `minRunners` to `0`, ARC will not provision new runners even when new jobs become available. This is useful for troubleshooting, maintenance, or gracefully shutting down runner capacity.

```yaml
## maxRunners is the max number of runners the auto scaling runner set will scale up to.
maxRunners: 0

## minRunners is the min number of idle runners. The target number of runners created will be
## calculated as a sum of minRunners and the number of jobs assigned to the scale set.
minRunners: 0

```

--------------------------------

### runs.using for Docker Container Actions

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Specifies the execution environment for Docker container actions.

```APIDOC
## Configuration Property runs.using for Docker Container Actions

### Description
You must set this value to `'docker'`.

### Method
Configuration Property

### Endpoint
runs.using

### Parameters
#### Request Body
- **using** (string) - Required - Must be set to `'docker'`.

### Request Example
{
  "using": "docker"
}
```

--------------------------------

### Use `strategy.job-index` for unique log files in GitHub Actions matrix jobs

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

This GitHub Actions workflow demonstrates how to leverage the `strategy.job-index` property within a matrix job. It creates a unique log file for each job in the matrix using the index and then uploads these logs as artifacts. This ensures distinct naming for each job's output, useful for debugging and tracking.

```yaml
name: Test strategy
on: push

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        test-group: [1, 2]
        node: [14, 16]
    steps:
      - run: echo "Mock test logs" > test-job-${{ strategy.job-index }}.txt
      - name: Upload logs
        uses: actions/upload-artifact@v4
        with:
          name: Build log for job ${{ strategy.job-index }}
          path: test-job-${{ strategy.job-index }}.txt
```

--------------------------------

### Recommended Action Directory Structure

Source: https://docs.github.com/en/actions/how-tos/create-and-publish-actions/manage-custom-actions

Shows the recommended directory structure for storing multiple actions within a single repository. Actions should be organized under the .github/actions directory to keep them separate from application code while maintaining them in a single repository.

```text
.github/actions/action-a
.github/actions/action-b
```

--------------------------------

### Build and Deploy ASP.Net Core App to Azure Web App with GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/net-to-azure-app-service

This GitHub Actions workflow automates the build and deployment of an ASP.Net Core application to an Azure Web App. It sets up the .NET environment, caches dependencies, builds and publishes the application, uploads the build artifact, and finally deploys it to the specified Azure Web App using a publish profile. It requires `AZURE_WEBAPP_NAME`, `AZURE_WEBAPP_PACKAGE_PATH`, `DOTNET_VERSION` environment variables and `AZURE_WEBAPP_PUBLISH_PROFILE` secret.

```yaml
name: Build and deploy ASP.Net Core app to an Azure Web App

env:
  AZURE_WEBAPP_NAME: MY_WEBAPP_NAME   # set this to your application's name
  AZURE_WEBAPP_PACKAGE_PATH: '.'      # set this to the path to your web app project, defaults to the repository root
  DOTNET_VERSION: '5'                 # set this to the .NET Core version to use

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v5

      - name: Set up .NET Core
        uses: actions/setup-dotnet@v4
        with:
          dotnet-version: ${{ env.DOTNET_VERSION }}

      - name: Set up dependency caching for faster builds
        uses: actions/cache@v4
        with:
          path: ~/.nuget/packages
          key: ${{ runner.os }}-nuget-${{ hashFiles('**/packages.lock.json') }}
          restore-keys: |
            ${{ runner.os }}-nuget-

      - name: Build with dotnet
        run: dotnet build --configuration Release

      - name: dotnet publish
        run: dotnet publish -c Release -o ${{env.DOTNET_ROOT}}/myapp

      - name: Upload artifact for deployment job
        uses: actions/upload-artifact@v4
        with:
          name: .net-app
          path: ${{env.DOTNET_ROOT}}/myapp

  deploy:
    runs-on: ubuntu-latest
    needs: build
    environment:
      name: 'production'
      url: ${{ steps.deploy-to-webapp.outputs.webapp-url }}

    steps:
      - name: Download artifact from build job
        uses: actions/download-artifact@v5
        with:
          name: .net-app

      - name: Deploy to Azure Web App
        id: deploy-to-webapp
        uses: azure/webapps-deploy@85270a1854658d167ab239bce43949edb336fa7c
        with:
          app-name: ${{ env.AZURE_WEBAPP_NAME }}
          publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
          package: ${{ env.AZURE_WEBAPP_PACKAGE_PATH }}
```

--------------------------------

### Make proxy settings persistent on Linux and macOS

Source: https://docs.github.com/en/actions/how-tos/manage-runners/use-proxy-servers

Write proxy environment variables to /etc/environment file to ensure configuration persists across system reboots and image rebuilds during custom image generation.

```shell
echo 'http_proxy=http://proxy.local' >> /etc/environment
```

--------------------------------

### Run GitHub Actions job conditionally based on commit status state

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

This example demonstrates how to trigger a GitHub Actions workflow on a commit status change and then run a specific job only if the new commit state is `error` or `failure`. It uses the `github.event.state` context to evaluate the condition and access event details.

```yaml
on:
  status
jobs:
  if_error_or_failure:
    runs-on: ubuntu-latest
    if: >-
      github.event.state == 'error' ||
      github.event.state == 'failure'
    steps:
      - env:
          DESCRIPTION: ${{ github.event.description }}
        run: |
          echo The status is error or failed: $DESCRIPTION
```

--------------------------------

### Trigger GitHub Actions Workflow on Pull Request with Specific File Changes (JavaScript)

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

This workflow demonstrates how to configure a GitHub Actions workflow to run only when a pull request includes changes to files matching a specific pattern. In this example, the workflow will trigger if any JavaScript file (`.js`) is modified in the pull request.

```yaml
on:
  pull_request:
    paths:
      - '**.js'

```

--------------------------------

### Test Composite Action in GitHub Workflow

Source: https://docs.github.com/en/actions/creating-actions/creating-a-composite-action

GitHub Actions workflow that tests the hello-world composite action by checking out code, invoking the custom action with a 'who-to-greet' input, and capturing the random-number output. Runs on push events on ubuntu-latest runner.

```yaml
on: [push]

jobs:
  hello_world_job:
    runs-on: ubuntu-latest
    name: A job to say hello
    steps:
      - uses: actions/checkout@v5
      - id: foo
        uses: OWNER/hello-world-composite-action@SHA
        with:
          who-to-greet: 'Mona the Octocat'
      - run: echo random-number "$RANDOM_NUMBER"
        shell: bash
        env:
          RANDOM_NUMBER: ${{ steps.foo.outputs.random-number }}
```

--------------------------------

### Configure job-level concurrency with static group name

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/control-workflow-concurrency

Limits concurrency of individual jobs within a workflow by applying the `concurrency` keyword at the job level. This example uses a static concurrency group name `example-group` and enables `cancel-in-progress` to cancel any running job in the same group when a new job is queued.

```yaml
on:
  push:
    branches:
      - main

jobs:
  job-1:
    runs-on: ubuntu-latest
    concurrency:
      group: example-group
      cancel-in-progress: true
```

--------------------------------

### List Available Feature Flags

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/supplemental-arguments-and-settings

Display all available feature flags supported by GitHub Actions Importer, including their current status (enabled/disabled) and minimum required GitHub Enterprise Server version. This command helps identify which features can be toggled for your migration.

```shell
gh actions-importer list-features
```

--------------------------------

### runs.image Configuration

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/metadata-syntax

Specify the Docker image to use as the container for running the action. Supports Docker base images, local Dockerfile references, or public images from Docker Hub or other registries.

```APIDOC
## runs.image

### Description
Required property that specifies the Docker image to use as the container to run the action.

### Property
`runs.image`

### Type
String

### Required
Yes (Required)

### Accepted Values
- Docker base image name (e.g., `ubuntu:20.04`)
- Local `Dockerfile` path relative to action metadata file (e.g., `Dockerfile`)
- Public image from Docker Hub (e.g., `node:14`)
- Public image from other registries

### Local Dockerfile Requirements
- File must be named `Dockerfile`
- Path must be relative to your action metadata file
- The `docker` application will execute this file

### Configuration Examples
```yaml
# Using a Docker base image
runs:
  using: 'docker'
  image: 'ubuntu:20.04'

# Using a local Dockerfile
runs:
  using: 'docker'
  image: 'Dockerfile'

# Using a public image
runs:
  using: 'docker'
  image: 'node:14'
```
```

--------------------------------

### Implement a GitHub Action in JavaScript

Source: https://docs.github.com/en/actions/creating-actions/creating-a-javascript-action

This JavaScript code defines a GitHub Action that retrieves an input variable ('who-to-greet'), prints a greeting, sets the current time as an output variable, and logs the full webhook event payload. It utilizes the `@actions/core` and `@actions/github` packages for interaction with the GitHub Actions environment. Errors are caught and reported using `core.setFailed`.

```JavaScript
import * as core from "@actions/core";
import * as github from "@actions/github";

try {
  // `who-to-greet` input defined in action metadata file
  const nameToGreet = core.getInput("who-to-greet");
  core.info(`Hello ${nameToGreet}!`);

  // Get the current time and set it as an output variable
  const time = new Date().toTimeString();
  core.setOutput("time", time);

  // Get the JSON webhook payload for the event that triggered the workflow
  const payload = JSON.stringify(github.context.payload, undefined, 2);
  core.info(`The event payload: ${payload}`);
} catch (error) {
  core.setFailed(error.message);
}
```

--------------------------------

### Cache Hits and Misses

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/dependency-caching

Understand the difference between cache hits (exact key match) and cache misses (no exact match). Learn how the action handles each scenario and automatically creates new caches on successful job completion.

```APIDOC
## Cache Hits and Misses

### Description
Explains the behavior of the cache action when cache keys match or don't match existing caches, and how restore-keys are used as fallback options.

### Cache Hit
- **Definition**: Occurs when `key` exactly matches an existing cache
- **Behavior**: The action restores cached files to the specified `path` directory
- **Output**: `cache-hit` returns `true`

### Cache Miss
- **Definition**: Occurs when `key` doesn't match any existing cache
- **Behavior**: Action searches `restore-keys` for partial matches sequentially
- **Fallback Process**:
  1. If exact match found in `restore-keys`, restore files to `path` directory
  2. If no exact match, search for partial matches of restore keys
  3. Restore most recent cache matching partial key to `path` directory
- **Auto-Creation**: New cache automatically created if job completes successfully
- **Output**: `cache-hit` returns `false`

### Key Matching Rules
- Cannot modify contents of existing cache
- Must create new cache with new key to update cached content
- Restore-keys are checked in order provided
- Most recent matching cache is restored on partial match

### Workflow Sequence on Cache Miss
1. Action completes after searching restore-keys
2. Next job step executes
3. If job completes successfully, new cache created with `path` directory contents
4. New cache uses provided `key` for future reference
```

--------------------------------

### run_container_step Function Arguments

Source: https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/customize-containers

Complete reference for all arguments accepted by the run_container_step function. This function configures Docker container execution within GitHub Actions workflows, supporting custom images, dockerfiles, environment configuration, and volume mounting.

```APIDOC
## run_container_step Function Arguments

### Description
Configures and executes a container step in GitHub Actions. Accepts arguments for Docker image selection, entry point configuration, working directory, environment variables, volume mounts, and registry authentication.

### Parameters

#### Image Configuration
- **image** (string) - Optional - A string containing the Docker image URI. Either image or dockerfile must be provided.
- **dockerfile** (string) - Optional - A string containing the path to the dockerfile. Either dockerfile or image must be provided.

#### Entry Point Configuration
- **entryPoint** (string) - Optional - The container entry point to use if the default image entrypoint should be overwritten.
- **entryPointArgs** (array) - Optional - A list containing the entry point arguments to pass to the container.

#### Working Directory
- **workingDirectory** (string) - Required - A string containing the absolute path of the working directory for container execution.

#### Container Options
- **createOptions** (string) - Optional - The optional create options specified in the YAML configuration. For more information, see Running jobs in a container.

#### Environment Configuration
- **environmentVariables** (object) - Optional - Sets a map of key-value environment variables to be available in the container.
- **prependPath** (array) - Optional - An array of additional paths to prepend to the $PATH variable within the container.

#### Volume Mounts
- **userMountVolumes** (array) - Optional - An array of user-defined mount volumes set in the YAML configuration. For more information, see Running jobs in a container.
  - **sourceVolumePath** (string) - Required - The source path to the volume that will be mounted into the Docker container.
  - **targetVolumePath** (string) - Required - The target path to the volume that will be mounted into the Docker container.
  - **readOnly** (boolean) - Required - Determines whether or not the mount should be read-only.

- **systemMountVolumes** (array) - Required - An array of system mounts to mount into the container, using the same fields as userMountVolumes.
  - **sourceVolumePath** (string) - Required - The source path to the volume that will be mounted into the Docker container.
  - **targetVolumePath** (string) - Required - The target path to the volume that will be mounted into the Docker container.
  - **readOnly** (boolean) - Required - Determines whether or not the mount should be read-only.

#### Registry Authentication
- **registry** (object) - Optional - The Docker registry credentials for a private container registry.
  - **username** (string) - Optional - The username of the registry account.
  - **password** (string) - Optional - The password to the registry account.
  - **serverUrl** (string) - Optional - The registry URL.

#### Port Mapping
- **portMappings** (object) - Optional - A key-value hash of the source:target ports to map into the container.

### Request Example
{
  "image": "ubuntu:20.04",
  "workingDirectory": "/home/runner/work",
  "entryPoint": "/bin/bash",
  "entryPointArgs": ["-c", "echo hello"],
  "environmentVariables": {
    "NODE_ENV": "production",
    "DEBUG": "true"
  },
  "prependPath": ["/usr/local/bin", "/opt/bin"],
  "userMountVolumes": [
    {
      "sourceVolumePath": "/tmp/source",
      "targetVolumePath": "/mnt/target",
      "readOnly": false
    }
  ],
  "systemMountVolumes": [
    {
      "sourceVolumePath": "/var/run/docker.sock",
      "targetVolumePath": "/var/run/docker.sock",
      "readOnly": true
    }
  ],
  "registry": {
    "username": "myuser",
    "password": "mypassword",
    "serverUrl": "https://registry.example.com"
  },
  "portMappings": {
    "8080:8080": "",
    "3000:3000": ""
  }
}
```

--------------------------------

### Conditional Cancellation Based on Branch Pattern

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax

Uses a conditional expression to control when in-progress runs are cancelled based on branch naming patterns. In this example, runs on release branches are not cancelled, while runs on other branches like 'main' will cancel in-progress runs. The expression evaluates to true when the branch does not contain 'release/'.

```yaml
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: ${{ !contains(github.ref, 'release/') }}
```

--------------------------------

### Configure `pull_request_target` for specific GitHub Actions activity types

Source: https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows

This YAML snippet demonstrates how to use the `types` keyword within the `pull_request_target` event configuration to explicitly define which pull request activity types will trigger the workflow. By default, only `opened`, `synchronize`, or `reopened` trigger the workflow, but this example expands it to include `assigned`.

```yaml
on:
  pull_request_target:
    types: [assigned, opened, synchronize, reopened]

```

--------------------------------

### Download Artifacts and Publish Release with GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/rust

Downloads previously uploaded artifacts from a workflow and publishes them as a GitHub release using the gh CLI. Requires appropriate repository permissions and GITHUB_TOKEN authentication. Uses actions/download-artifact@v5 to retrieve artifacts and gh release create to publish them.

```yaml
- uses: actions/checkout@v5
- name: Download release artifact
  uses: actions/download-artifact@v5
  with:
    name: <my-app>
    path: ./<my-app>
- name: Publish built binary to GitHub releases
- run: |
    gh release create --generate-notes ./<my-app>/<my-project>#<my-app>
```

--------------------------------

### Trigger Workflow on `pull_request` with Branch and Path Filters (YAML)

Source: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows

This advanced example demonstrates combining both `branches` and `paths` filters for a `pull_request` event. The workflow will only execute if a pull request is opened, targets a branch matching 'releases/**', AND includes changes to any JavaScript (`.js`) files. This provides fine-grained control over workflow triggers.

```yaml
on:
  pull_request:
    types:
      - opened
    branches:
      - 'releases/**'
    paths:
      - '**.js'

```

--------------------------------

### Dynamically map environment variables to secrets using regex groups (Ruby)

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/extending-github-actions-importer-with-custom-transformers

This transformer uses a regular expression with a capture group to dynamically map environment variables ending with '_SSH_KEY' to corresponding GitHub Actions secrets. For example, 'MYAPP_SSH_KEY' would map to a secret named 'MYAPP_SSH_KEY'.

```Ruby
env /^(.+)_SSH_KEY/, secret("%s_SSH_KEY)
```

--------------------------------

### GitHub Actions Importer Dry-Run with Configuration File

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/azure-devops-migration

Execute a dry-run migration using a configuration file to specify source files. The pipeline is selected by matching the repository_slug in the configuration file to the Azure DevOps organization and project options.

```bash
gh actions-importer dry-run azure-devops pipeline --output-dir ./output/ --config-file-path ./path/to/azure_devops/config.yml
```

--------------------------------

### Publish Package to npm Registry with Yarn using GitHub Actions

Source: https://docs.github.com/en/actions/publishing-packages/publishing-nodejs-packages

A GitHub Actions workflow that publishes an npm package to the public npm registry using Yarn package manager on release publication. Configures setup-node with npm registry URL and authenticates via NPM_TOKEN secret. Supports both Yarn v2+ and v1 syntax.

```yaml
name: Publish Package to npmjs
on:
  release:
    types: [published]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      # Setup .npmrc file to publish to npm
      - uses: actions/setup-node@v4
        with:
          node-version: '20.x'
          registry-url: 'https://registry.npmjs.org'
          # Defaults to the user or organization that owns the workflow file
          scope: '@octocat'
      - run: yarn
      - run: yarn npm publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

--------------------------------

### Exclude Specific Branches and Tags for GitHub Actions Push Events

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow

This snippet shows how to prevent a GitHub Actions workflow from running on `push` events for certain branches and tags. It utilizes the `branches-ignore` filter to exclude `mona/octocat` and branches matching `releases/**-alpha`, and the `tags-ignore` filter to exclude `v2` and tags starting with `v1.`.

```yaml
on:
  push:
    # Sequence of patterns matched against refs/heads
    branches-ignore:
      - 'mona/octocat'
      - 'releases/**-alpha'
    # Sequence of patterns matched against refs/tags
    tags-ignore:
      - v2
      - v1.*
```

--------------------------------

### Create Azure Web App with .NET Runtime using Azure CLI

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/net-to-azure-app-service

Creates a new Azure App Service web app with .NET 5.0 runtime using the Azure CLI. Replace MY_WEBAPP_NAME with your desired web app name, MY_APP_SERVICE_PLAN with your App Service plan name, and MY_RESOURCE_GROUP with your resource group. Adjust the DOTNET version as needed.

```bash
az webapp create \
    --name MY_WEBAPP_NAME \
    --plan MY_APP_SERVICE_PLAN \
    --resource-group MY_RESOURCE_GROUP \
    --runtime "DOTNET|5.0"
```

--------------------------------

### Login and Publish Rust Package to crates.io

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/rust

Authenticates with crates.io using a secret token, builds the project in release mode, packages it as a tarball, and publishes it as a library. Requires CRATES_IO secret to be configured in the repository. Ensure Cargo.toml metadata is properly configured before publishing.

```yaml
- name: Login into crates.io
  run: cargo login ${{ secrets.CRATES_IO }}
- name: Build binaries in "release" mode
  run: cargo build -r
- name: "Package for crates.io"
  run: cargo package
- name: "Publish to crates.io"
  run: cargo publish
```

--------------------------------

### Configure GitHub Actions Job and PostgreSQL Service Container in YAML

Source: https://docs.github.com/en/actions/using-containerized-services/creating-postgresql-service-containers

This YAML snippet defines a GitHub Actions job (`container-job`) that executes within a `node:20-bookworm-slim` Docker container on an `ubuntu-latest` runner. It also sets up a `postgres` service container, providing a password and health check options to ensure the database is ready before the job proceeds.

```yaml
jobs:
  # Label of the container job
  container-job:
    # Containers must run in Linux based operating systems
    runs-on: ubuntu-latest
    # Docker Hub image that `container-job` executes in
    container: node:20-bookworm-slim

    # Service containers to run with `container-job`
    services:
      # Label used to access the service container
      postgres:
        # Docker Hub image
        image: postgres
        # Provide the password for postgres
        env:
          POSTGRES_PASSWORD: postgres
        # Set health checks to wait until postgres has started
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

```

--------------------------------

### Pin GitHub Action to specific semantic version tag

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/find-and-customize-actions

Demonstrates how to reference a GitHub Action using a semantic version tag (e.g., v1.0.1) in a workflow step. Tags allow flexibility in version management but are mutable and can be moved or deleted by maintainers. This approach is useful for automatically receiving minor and patch updates while controlling major version changes.

```yaml
steps:
  - uses: actions/javascript-action@v1.0.1
```

--------------------------------

### Implement GitHub Actions Job Dependencies and Output Sharing with Needs

Source: https://docs.github.com/en/actions/learn-github-actions/contexts

This workflow illustrates defining job dependencies and sharing outputs using the `needs` context in GitHub Actions. It includes a `build` job, a `deploy` job dependent on `build`, and a `debug` job dependent on both, running only on failure. The `deploy` job accesses an output from the `build` job, showcasing inter-job data flow.

```yaml
name: Build and deploy
on: push

jobs:
  build:
    runs-on: ubuntu-latest
    outputs:
      build_id: ${{ steps.build_step.outputs.build_id }}
    steps:
      - name: Build
        id: build_step
        run: echo "build_id=$RANDOM" >> $GITHUB_OUTPUT
  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying build ${{ needs.build.outputs.build_id }}"
  debug:
    needs: [build, deploy]
    runs-on: ubuntu-latest
    if: ${{ failure() }}
    steps:
      - run: echo "Failed to build and deploy"
```

--------------------------------

### Run Command with PowerShell Desktop in GitHub Actions

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This snippet demonstrates how to use PowerShell Desktop (`powershell`) for a `run` step in a GitHub Actions workflow. It configures the step to display the `PATH` environment variable using PowerShell syntax, primarily for Windows runners.

```yaml
steps:
  - name: Display the path
    shell: powershell
    run: echo ${env:PATH}
```

--------------------------------

### Configure Docker Container Execution for GitHub Actions

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

This JSON configuration defines how a Docker container step should be executed within a GitHub Actions workflow. It specifies the Docker image (`node:18`), entry point, working directory, environment variables, CPU limits, and various volume mounts (user-defined and system-defined) for the container. It also includes network and container IDs for state management.

```json
{
  "command": "run_container_step",
  "responseFile": null,
  "state": {
    "network": "example_network_53269bd575972817b43f7733536b200c",
    "jobContainer": "82e8219701fe096a35941d869cf3d71af1d943b5d8bdd718857fb87ac3042480",
    "serviceContainers": {
      "redis": "60972d9aa486605e66b0dad4abb678dc3d9116f536579e418176eedb8abb9105"
    }
  },
  "args": {
    "image": "node:18",
    "dockerfile": null,
    "entryPointArgs": ["-f", "/dev/null"],
    "entryPoint": "tail",
    "workingDirectory": "/__w/octocat-test2/octocat-test2",
    "createOptions": "--cpus 1",
    "environmentVariables": {
      "NODE_ENV": "development"
    },
    "prependPath": ["/foo/bar", "bar/foo"],
    "userMountVolumes": [
      {
        "sourceVolumePath": "my_docker_volume",
        "targetVolumePath": "/volume_mount",
        "readOnly": false
      }
    ],
    "systemMountVolumes": [
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work",
        "targetVolumePath": "/__w",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/externals",
        "targetVolumePath": "/__e",
        "readOnly": true
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp",
        "targetVolumePath": "/__w/_temp",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_actions",
        "targetVolumePath": "/__w/_actions",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_tool",
        "targetVolumePath": "/__w/_tool",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_home",
        "targetVolumePath": "/github/home",
        "readOnly": false
      },
      {
        "sourceVolumePath": "/home/octocat/git/runner/_layout/_work/_temp/_github_workflow",
        "targetVolumePath": "/github/workflow",
        "readOnly": false
      }
    ],
    "registry": null,
    "portMappings": { "80": "801" }
  }
}
```

--------------------------------

### Set Executable Permissions for GitHub Action Entrypoint (Git Shell)

Source: https://docs.github.com/en/actions/creating-actions/creating-a-docker-container-action

These Git commands ensure the `entrypoint.sh` script is marked as executable within the Git repository. `git add` stages the file, and `git update-index --chmod=+x` explicitly sets the executable permission bit. This prevents permission issues when the repository is cloned or forked.

```Shell
git add entrypoint.sh
git update-index --chmod=+x entrypoint.sh

```

--------------------------------

### Cache Maven Dependencies with setup-java Action

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-maven

Configure GitHub Actions to cache Maven dependencies using the setup-java action with cache parameter. The cache key is based on the hashed contents of pom.xml, so any changes to pom.xml will invalidate the cache. This stores the local Maven repository (.m2 directory) to avoid re-downloading dependencies in future workflow runs.

```yaml
steps:
  - uses: actions/checkout@v5
  - name: Set up JDK 17
    uses: actions/setup-java@v4
    with:
      java-version: '17'
      distribution: 'temurin'
      cache: maven
  - name: Build with Maven
    run: mvn --batch-mode --update-snapshots verify
```

--------------------------------

### Configure Self-hosted Runner with Labels

Source: https://docs.github.com/en/actions/using-jobs/choosing-the-runner-for-a-job

Use the runs-on key with an array of labels to target self-hosted runners. The self-hosted label must be listed first, followed by additional labels for targeting specific operating systems or architectures. Jobs will only queue on runners that have all specified labels.

```yaml
runs-on: [self-hosted, linux]
```

--------------------------------

### Verify Artifact Attestation for Binaries with GitHub CLI

Source: https://docs.github.com/en/actions/how-tos/secure-your-work/use-artifact-attestations/use-artifact-attestations

Use the GitHub CLI to validate artifact attestations for binary files. Requires the path to the binary artifact and repository information in the format ORGANIZATION_NAME/REPOSITORY_NAME.

```bash
gh attestation verify PATH/TO/YOUR/BUILD/ARTIFACT-BINARY -R ORGANIZATION_NAME/REPOSITORY_NAME
```

--------------------------------

### Make scripts executable and run in GitHub Actions

Source: https://docs.github.com/en/actions/how-tos/write-workflows/choose-what-workflows-do/add-scripts

Set execute permissions on script files using chmod and then run multiple scripts in a single step. This approach ensures scripts have proper permissions before execution and demonstrates running multiple commands in sequence using pipe syntax.

```yaml
jobs:
  example-job:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./scripts
    steps:
      - name: Check out the repository to the runner
        uses: actions/checkout@v5
      - name: Make the script files executable
        run: chmod +x my-script.sh my-other-script.sh
      - name: Run the scripts
        run: |
          ./my-script.sh
          ./my-other-script.sh
```

--------------------------------

### Build and Upload Java Artifacts with Gradle in GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/java-with-gradle

This GitHub Actions workflow extends the basic build process by adding artifact uploading. After setting up Java 17 and Gradle, and executing a standard `./gradlew build` command, it uses `actions/upload-artifact@v4` to store the compiled Java packages. The artifacts, typically found in `build/libs`, are uploaded with the name 'Package' for later retrieval and testing.

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.
steps:
  - uses: actions/checkout@v5
  - uses: actions/setup-java@v4
    with:
      java-version: '17'
      distribution: 'temurin'

  - name: Setup Gradle
    uses: gradle/actions/setup-gradle@017a9effdb900e5b5b2fddfb590a105619dca3c3 # v4.4.2

  - name: Build with Gradle
    run: ./gradlew build

  - name: Upload build artifacts
    uses: actions/upload-artifact@v4
    with:
      name: Package
      path: build/libs
```

--------------------------------

### OIDC JWT Token Structure for Reusable Workflows

Source: https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/using-openid-connect-with-reusable-workflows

Example OIDC token payload presented by GitHub's OIDC provider during a workflow run that includes both standard claims about the calling workflow and a custom job_workflow_ref claim about the called reusable workflow. This token is used for cloud provider authentication and trust validation.

```json
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "example-thumbprint",
  "kid": "example-key-id"
}
{
  "jti": "example-id",
  "sub": "repo:octo-org/octo-repo:environment:prod",
  "aud": "https://github.com/octo-org",
  "ref": "refs/heads/main",
  "sha": "example-sha",
  "repository": "octo-org/octo-repo",
  "repository_owner": "octo-org",
  "actor_id": "12",
  "repository_id": "74",
  "repository_owner_id": "65",
  "run_id": "example-run-id",
  "run_number": "10",
  "run_attempt": "2",
  "actor": "octocat",
  "workflow": "example-workflow",
  "head_ref": "",
  "base_ref": "",
  "event_name": "workflow_dispatch",
  "ref_type": "branch",
  "job_workflow_ref": "octo-org/octo-automation/.github/workflows/oidc.yml@refs/heads/main",
  "iss": "https://token.actions.githubusercontent.com",
  "nbf": 1632492967,
  "exp": 1632493867,
  "iat": 1632493567
}
```