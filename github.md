### Get GitHub CLI Help

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Provides help information for GitHub CLI commands. Appending `--help` to any command displays its usage details.

```bash
gh --help
gh issue --help
gh issue create --help

```

--------------------------------

### Start a New Repository and Publish to GitHub with Git

Source: https://docs.github.com/en/get-started/using-git/about-git

This example guides you through initializing a new local Git repository, adding files, committing them, connecting to a remote GitHub repository, and pushing your initial commit. Ensure you create an empty repository on GitHub first.

```bash
# create a new directory, and initialize it with git-specific functions
git init my-repo

# change into the `my-repo` directory
cd my-repo

# create the first file in the project
touch README.md

# git isn't aware of the file, stage it
git add README.md

# take a snapshot of the staging area
git commit -m "add README to initial commit"

# provide the path for the repository you created on github
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME.git

# push changes to github
git push --set-upstream origin main

```

--------------------------------

### Install Go dependencies using go get (YAML)

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

This workflow snippet illustrates how to install project dependencies using the `go get` command. It first checks out the code and sets up a specific Go version ('1.21.x') using the `actions/setup-go@v5` action. Then, it uses a multi-line `run` command to execute `go get .` to install current dependencies, followed by `go get example.com/octo-examplemodule` and `go get example.com/octo-examplemodule@v1.3.4` to install specific modules and a particular version of a module.

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

### Setup Node.js Environment using actions/setup-node

Source: https://docs.github.com/en/actions/tutorials/create-an-example-workflow

This step installs a specified version of Node.js on the runner, making 'node' and 'npm' commands available in the PATH. It utilizes the 'actions/setup-node' action and requires the 'node-version' input. This is crucial for Node.js projects.

```yaml
- uses: actions/setup-node@v4
    with:
      node-version: '20'
```

--------------------------------

### Install Dependencies with npm

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/quickstart

This command installs the necessary Node.js dependencies for the GitHub App. Ensure you have Node.js version 12 or greater installed. This step is crucial for the application to function correctly.

```bash
npm install
```

--------------------------------

### Install Git LFS using Windows setup wizard

Source: https://docs.github.com/en/repositories/working-with-files/managing-large-files/installing-git-large-file-storage_platform=linux

Installs Git LFS on Windows by running the downloaded executable file. This launches a setup wizard that guides the user through the installation process.

```powershell
.git-lfs-windows-1.X.X.exe
```

--------------------------------

### Setup GitHub Copilot in Vim/Neovim

Source: https://docs.github.com/en/copilot/how-tos/set-up/install-copilot-extension_tool=eclipse

Command to initiate the setup process for GitHub Copilot within Vim or Neovim after installation. Ensures the extension is ready for use.

```vimscript
:Copilot setup
```

--------------------------------

### Make a GET request using GitHub CLI

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=cli

This example demonstrates making a GET request to the '/octocat' endpoint using the GitHub CLI's 'api' subcommand. It specifies the HTTP method using the '--method' flag. This is useful for retrieving metadata.

```shell
gh api /octocat --method GET

```

--------------------------------

### Get Installation by ID - cURL Request Example

Source: https://docs.github.com/en/rest/apps/apps

This cURL command demonstrates how to fetch installation information using the installation ID. It requires setting the 'Accept', 'Authorization', and 'X-GitHub-Api-Version' headers. Replace '<YOUR-TOKEN>' with your actual JWT.

```shell
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/app/installations/1
```

--------------------------------

### Get Installation by ID - JavaScript Request Example

Source: https://docs.github.com/en/rest/apps/apps

This JavaScript snippet shows how to make a request to get installation details using the installation ID. It utilizes the Fetch API to send a GET request with the necessary headers. Ensure you replace '<YOUR-TOKEN>' with your JWT.

```javascript
async function getInstallation(installationId) {
  const response = await fetch(`https://api.github.com/app/installations/${installationId}`, {
    method: 'GET',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer <YOUR-TOKEN>`, // Replace with your JWT
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  
  const data = await response.json();
  return data;
}

// Example usage:
// getInstallation(1).then(installation => console.log(installation));
```

--------------------------------

### Complete devcontainer.json Example with Composer and Extensions

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-php-project-for-codespaces

This is a complete example of a devcontainer.json file incorporating the configurations for installing the Composer extension and running 'composer install' post-creation. It also includes other common settings like the container name, image, and forwarded ports.

```json
// For format details, see https://aka.devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/php
{
  "name": "PHP",
  // Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
  "image": "mcr.microsoft.com/devcontainers/php:1-8.2-bullseye",

  // Configure tool-specific properties.
  "customizations": {
    // Configure properties specific to VS Code.
    "vscode": {
      "extensions": [
        "ikappas.composer"
      ]
    }
  },

  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  "forwardPorts": [
    8080
  ],
  "features": {
    "ghcr.io/devcontainers/features/github-cli:1": {}
  },

  // Use 'postCreateCommand' to run commands after the container is created.
  "postCreateCommand": "sudo chmod a+x \"$(pwd)\" && sudo rm -rf /var/www/html && sudo ln -s \"$(pwd)\" /var/www/html; if [ -f composer.json ];then composer install;fi"

  // Uncomment to connect as root instead. More info: https://aka.dev-containers-non-root.
  // "remoteUser": "root"
}
```

--------------------------------

### Example Server Output

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/building-ci-checks-with-a-github-app

This is an example of the expected output when the Sinatra web server starts successfully. It indicates the port and environment the server is running on.

```text
> == Sinatra (v2.2.3) has taken the stage on 3000 for development with backup from Puma
> Puma starting in single mode...
> * Puma version: 6.3.0 (ruby 3.1.2-p20) ("Mugi No Toki Itaru")
> *  Min threads: 0
> *  Max threads: 5
> *  Environment: development
> *          PID: 14915
> * Listening on http://0.0.0.0:3000
> Use Ctrl-C to stop

```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/quickstart

This example makes a request to the "Get Octocat" endpoint, which uses the method GET and the path /octocat.

```APIDOC
## GET /octocat

### Description
Retrieves information about the "Octocat" endpoint.

### Method
GET

### Endpoint
/octocat

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```
gh api /octocat --method GET
```

### Response
#### Success Response (200)
- **(type)** - Description

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Install npm Packages using npm install

Source: https://docs.github.com/en/actions/tutorials/create-an-example-workflow

This step executes an npm command to install global packages on the runner. It uses the 'run' keyword to execute shell commands. In this example, it installs the 'bats' software testing package globally.

```yaml
- run: npm install -g bats
```

--------------------------------

### Install Dependencies and Commit Changes

Source: https://docs.github.com/en/packages/quickstart

This snippet covers installing project dependencies using npm, adding necessary files to Git staging, committing the changes with a message, and pushing them to the remote repository.

```bash
npm install
git add index.js package.json package-lock.json
git commit -m "initialize npm package"
git push
```

--------------------------------

### Create Repository using GitHub CLI

Source: https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories_tool=webui

This snippet demonstrates how to create a new repository on GitHub using the GitHub CLI. It covers interactive prompts for setup and an alternative method using flags for repository name and visibility. The `--clone` flag can be used to clone the repository locally.

```bash
gh repo create <repository-name> --public
gh repo create <repository-name> --private
gh repo create <repository-name> --internal
gh repo create <repository-name> --public --clone
gh repo create <organization-name>/<repository-name>
```

--------------------------------

### Get Installation by ID - GitHub CLI Example

Source: https://docs.github.com/en/rest/apps/apps

This GitHub CLI command retrieves installation information for a given installation ID. It automatically handles authentication and header management. Replace '1' with the desired installation ID.

```bash
gh api /app/installations/1 -H "X-GitHub-Api-Version: 2022-11-28"
```

--------------------------------

### Start Sinatra Web Server

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/building-ci-checks-with-a-github-app

Starts the local Sinatra web server using the `server.rb` file. This command assumes Bundler is installed and project dependencies are met.

```shell
bundle exec ruby server.rb

```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=cli

This endpoint retrieves information about 'Octocat'. The example demonstrates using GitHub CLI to make a GET request to this endpoint.

```APIDOC
## GET /octocat

### Description
Retrieves information about 'Octocat'.

### Method
GET

### Endpoint
/octocat

### Parameters

### Request Example
```shell
gh api /octocat --method GET
```

### Response
#### Success Response (200)
- **field** (type) - Description

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### View GitHub Repository

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Shows the description and README.md of a specified GitHub repository. It can also open the repository in a web browser.

```bash
gh repo view OWNER/REPO
gh repo view OWNER/REPO --web

```

--------------------------------

### Set up Node.js Environment with actions/setup-node

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

This step utilizes the `actions/setup-node` action to install a specified version of Node.js (e.g., version 20). This action ensures that `node` and `npm` commands are available in the system's PATH for subsequent steps.

```yaml
- uses: actions/setup-node@v4
  with:
    node-version: '20'

```

--------------------------------

### Octokit.js Setup and Request Example

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&tool=cli

This section details how to set up Octokit.js, authenticate requests with a personal access token, and make a 'Create an issue' request.

```APIDOC
## POST /repos/{owner}/{repo}/issues

### Description
Creates a new issue in a specified repository.

### Method
POST

### Endpoint
`/repos/{owner}/{repo}/issues`

### Parameters
#### Path Parameters
- **owner** (string) - Required - The owner of the repository.
- **repo** (string) - Required - The name of the repository.

#### Query Parameters
None

#### Request Body
- **title** (string) - Required - The title of the issue.
- **body** (string) - Optional - The content of the issue.

### Request Example
```javascript
const octokit = new Octokit({
  auth: 'YOUR-TOKEN'
});

await octokit.request('POST /repos/{owner}/{repo}/issues', {
  owner: 'octocat',
  repo: 'Spoon-Knife',
  title: 'Created with the REST API',
  body: 'This is a test issue created by the REST API'
});
```

### Response
#### Success Response (201 Created)
- **issue** (object) - The created issue object.

#### Response Example
```json
{
  "url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1",
  "repository_url": "https://api.github.com/repos/octocat/Spoon-Knife",
  "labels_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/labels{/name}",
  "comments_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/comments",
  "events_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/events",
  "html_url": "https://github.com/octocat/Spoon-Knife/issues/1",
  "id": 1,
  "node_id": "MDU6SXNzdWUx",
  "number": 1,
  "title": "Created with the REST API",
  "user": {
    "login": "octocat",
    "id": 1,
    "node_id": "MDQ6VXNlcjE=",
    "avatar_url": "https://github.com/images/error/octocat_happy.gif",
    "gravatar_id": "",
    "url": "https://api.github.com/users/octocat",
    "html_url": "https://github.com/octocat",
    "followers_url": "https://api.github.com/users/octocat/followers",
    "following_url": "https://api.github.com/users/octocat/following{/other_user}",
    "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
    "organizations_url": "https://api.github.com/users/octocat/orgs",
    "repos_url": "https://api.github.com/users/octocat/repos",
    "events_url": "https://api.github.com/users/octocat/events{/privacy}",
    "received_events_url": "https://api.github.com/users/octocat/received_events",
    "type": "User",
    "site_admin": false
  },
  "labels": [],
  "state": "open",
  "locked": false,
  "assignee": null,
  "assignees": [],
  "milestone": null,
  "comments": 0,
  "created_at": "2011-04-22T13:33:48Z",
  "updated_at": "2011-04-22T13:33:48Z",
  "closed_at": null,
  "author_association": "OWNER",
  "body": "This is a test issue created by the REST API"
}
```
```

--------------------------------

### Get a code scanning default setup configuration

Source: https://docs.github.com/en/rest/code-scanning

Gets the default setup configuration for code scanning.

```APIDOC
## GET /repos/{owner}/{repo}/code-scanning/default-setup

### Description
Gets the default setup configuration for code scanning.

### Method
GET

### Endpoint
/repos/{owner}/{repo}/code-scanning/default-setup

### Parameters
#### Path Parameters
- **owner** (string) - Required - The account owner of the repository.
- **repo** (string) - Required - The name of the repository.
```

--------------------------------

### List Installations for Authenticated App (JavaScript)

Source: https://docs.github.com/en/rest/apps/apps

Example of how to list installations for an authenticated GitHub App using JavaScript. This snippet demonstrates making a GET request to the GitHub API with necessary headers.

```javascript
async function listInstallations() {
  const token = "<YOUR-TOKEN>";
  const response = await fetch("https://api.github.com/app/installations", {
    headers: {
      "Accept": "application/vnd.github+json",
      "Authorization": `Bearer ${token}`,
      "X-GitHub-Api-Version": "2022-11-28"
    }
  });
  const data = await response.json();
  console.log(data);
}

listInstallations();
```

--------------------------------

### Checkout Repository and Setup Node.js

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

Includes steps to checkout the repository code using 'actions/checkout@v5' and set up Node.js version 20 using 'actions/setup-node@v4'. These are prerequisites for using npm.

```yaml
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
```

--------------------------------

### Run Shell Command: Install npm package

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

The `run` keyword allows you to execute shell commands directly on the runner. This example demonstrates installing the `bats` software testing package globally using `npm`.

```yaml
- run: npm install -g bats

```

--------------------------------

### Get Organization Installation (JavaScript)

Source: https://docs.github.com/en/rest/apps/apps

Retrieves installation information for a GitHub App within a specific organization using JavaScript. This example demonstrates making a GET request to the GitHub API, including necessary headers and the API endpoint.

```javascript
async function getOrgInstallation(octokit, org) {
  return octokit.request('GET /orgs/{org}/installation', {
    org: org
  });
}
```

--------------------------------

### Example User-Agent Header for GitHub REST API

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

This snippet shows an example of a User-Agent header for an application interacting with the GitHub REST API. It's crucial for identifying your application and ensuring requests are not rejected.

```text
User-Agent: Awesome-Octocat-App
```

--------------------------------

### CodeQL CLI Setup and Verification

Source: https://docs.github.com/en/code-security/codeql-cli/using-the-advanced-functionality-of-the-codeql-cli/advanced-setup-of-the-codeql-cli

Instructions for extracting the CodeQL CLI, launching it, and verifying the setup using commands like `codeql resolve languages` and `codeql resolve qlpacks`.

```APIDOC
## CodeQL CLI Setup

### Description
This section details how to extract the CodeQL CLI tar archive, launch the `codeql` executable, and verify your setup.

### Extracting the CodeQL CLI
Extract the tar archive into a designated directory. For example, if your CodeQL repository path is `$HOME/codeql-home/codeql-repo`, extract the CLI into `$HOME/codeql-home/`.

### Launching `codeql`
Once extracted, you can run CodeQL processes in two ways:
1. Execute `<extraction-root>/codeql/codeql`, where `<extraction-root>` is the folder where you extracted the CodeQL CLI package.
2. Add `<extraction-root>/codeql` to your `PATH` to run the executable as `codeql`.

### Verifying CodeQL CLI Setup
Use the following subcommands to verify your setup:

*   `codeql resolve languages`: Shows available languages for database creation.
*   `codeql resolve qlpacks`: Displays CodeQL packs the CLI can find, including query, library, example, and legacy packs.
```

--------------------------------

### Create GitHub Repository

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Initiates the creation of a new repository on GitHub. It can create an empty repository, clone it locally, or push an existing local repository.

```bash
gh repo create

```

--------------------------------

### Devcontainer.json Configuration Example

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-php-project-for-codespaces

An example of a devcontainer.json file showing common configurations like image, forwarded ports, and features. This file defines the environment for a development container, specifying the base image, ports to forward, and features to install. It supports various options for customizing the development setup.

```json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/php
{
  "name": "PHP",
  // Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
  "image": "mcr.microsoft.com/devcontainers/php:1-8.2-bullseye",

  // Features to add to the dev container. More info: https://containers.dev/features.
  // "features": {},

  // Configure tool-specific properties.
  // "customizations": {},

  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  "forwardPorts": [
    8080
  ],
  "features": {
    "ghcr.io/devcontainers/features/github-cli:1": {}
  }

  // Use 'postCreateCommand' to run commands after the container is created.
  // "postCreateCommand": "sudo chmod a+x \"$(pwd)\" && sudo rm -rf /var/www/html && sudo ln -s \"$(pwd)\" /var/www/html"

  // Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
  // "remoteUser": "root"
}

```

--------------------------------

### Get Repository README - JavaScript

Source: https://docs.github.com/en/rest/repos/contents_apiversion=2022-11-28

This JavaScript example shows how to retrieve a repository's README file using the GitHub API. It requires setting the appropriate headers and making a GET request to the API endpoint. Ensure you have the necessary libraries (e.g., node-fetch or Axios) installed.

```javascript
async function getRepoReadme(owner, repo, token) {
  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/readme`, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  const data = await response.json();
  return data;
}
```

--------------------------------

### GET /repos/{owner}/{repo}/issues

Source: https://docs.github.com/en/rest/quickstart

This example workflow uses the List repository issues endpoint, and requests a list of issues in the octocat/Spoon-Knife repository.

```APIDOC
## GET /repos/{owner}/{repo}/issues

### Description
Lists issues in a specified repository.

### Method
GET

### Endpoint
/repos/{owner}/{repo}/issues

### Parameters
#### Path Parameters
- **owner** (string) - Required - The owner of the repository.
- **repo** (string) - Required - The name of the repository.

#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
on:
  workflow_dispatch:
jobs:
  use_api:
    runs-on: ubuntu-latest
    permissions:
      issues: read
    steps:
      - env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          gh api https://api.github.com/repos/octocat/Spoon-Knife/issues
```

### Response
#### Success Response (200)
- **(type)** - Description

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Analyze with Downloaded CodeQL Packs

Source: https://docs.github.com/en/code-security/codeql-cli/codeql-cli-reference/about-codeql-packs

This example demonstrates downloading and analyzing with CodeQL packs using the `codeql database analyze --download` command. It shows how to specify packs, versions, and individual queries, and includes output indicating successful downloads and query execution.

```bash
$ echo $OCTO-ORG_ACCESS_TOKEN | codeql database analyze --download /codeql-dbs/example-repo \
    octo-org/security-queries \
    octo-org/optional-security-queries@~1.0.1:queries/csrf.ql \
    --format=sarif-latest --output=/temp/example-repo-js.sarif

> Download location: /Users/mona/.codeql/packages
> Installed fresh octo-org/security-queries@1.0.0
> Installed fresh octo-org/optional-security-queries@1.0.2
> Running queries.
> Compiling query plan for /Users/mona/.codeql/packages/octo-org/security-queries/1.0.0/potential-sql-injection.ql.
> [1/2] Found in cache: /Users/mona/.codeql/packages/octo-org/security-queries/1.0.0/potential-sql-injection.ql.
> Starting evaluation of octo-org/security-queries/query1.ql.
> Compiling query plan for /Users/mona/.codeql/packages/octo-org/optional-security-queries/1.0.2/queries/csrf.ql.
> [2/2] Found in cache: /Users/mona/.codeql/packages/octo-org/optional-security-queries/1.0.2/queries/csrf.ql.
> Starting evaluation of octo-org/optional-security-queries/queries/csrf.ql.
> [2/2 eval 694ms] Evaluation done; writing results to octo-org/security-queries/query1.bqrs.
> Shutting down query evaluator.
> Interpreting results.

```

--------------------------------

### Authenticated Request with Curl (Shell)

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

This example outlines the process of making an authenticated request to the GitHub REST API using `curl`. It assumes `curl` is installed and details the steps for choosing an endpoint, identifying HTTP methods and paths, and constructing authentication credentials, typically an access token sent in the `Authorization` header.

```shell
# Example placeholder for curl command structure
# curl -X POST <API_ENDPOINT> \
#   -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
#   -H "Accept: application/vnd.github+json" \
#   -d '{"title":"My Issue Title","body":"My issue body"}'
```

--------------------------------

### Create GitHub Repository using GitHub CLI

Source: https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories

This snippet demonstrates how to create a new GitHub repository using the GitHub CLI. It covers creating a repository from scratch, specifying organization ownership, and setting visibility. It also includes an option to clone the repository locally.

```shell
gh repo create project-name --public
gh repo create organization-name/project-name --private --clone
```

--------------------------------

### Create a GitHub Repository using GitHub CLI

Source: https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories_tool=cli

This snippet demonstrates how to create a new GitHub repository from the command line using the `gh repo create` command. It supports creating repositories from scratch, specifying visibility, and optionally cloning the repository locally. Ensure you have GitHub CLI installed and authenticated.

```bash
gh repo create project-name --public --clone
```

--------------------------------

### Install Git and GCM on Linux

Source: https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git_platform=linux

Provides instructions for installing Git and Git Credential Manager (GCM) on Linux. GCM setup on Linux may vary depending on the distribution and requires configuration to select a backing store.

```text
Install Git using your distro's package manager.
Install GCM following instructions in the GCM repo.
Configure Git to use GCM by selecting a backing store as per GCM Linux documentation.
```

--------------------------------

### Example Copilot Instructions File Structure

Source: https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot

This example illustrates effective repository custom instructions. It provides an overview of the project, its folder structure, and the libraries/frameworks used, offering Copilot comprehensive context for better assistance.

```markdown
# Project Overview

This project is a web application that allows users to manage their tasks and to-do lists. It is built using React and Node.js, and uses MongoDB for data storage.

## Folder Structure

- /src: Contains the source code for the frontend.
- /server: Contains the source code for the Node.js backend.
- /docs: Contains documentation for the project, including API specifications and user guides.

## Libraries and Frameworks

- React and Tailwind CSS for the frontend.
- Node.js and Express for the backend.
- MongoDB for data storage.

```

--------------------------------

### Example Installation Response JSON

Source: https://docs.github.com/en/rest/apps/installations

This JSON object represents a successful response from an API endpoint listing GitHub App installations. It includes details about each installation, such as its ID, account information, associated permissions, and events it's configured for. The `permissions` key within each installation object specifies the access level granted (e.g., 'write', 'read').

```json
{
  "total_count": 2,
  "installations": [
    {
      "id": 1,
      "account": {
        "login": "octocat",
        "id": 1,
        "node_id": "MDQ6VXNlcjE=",
        "avatar_url": "https://github.com/images/error/octocat_happy.gif",
        "gravatar_id": "",
        "url": "https://api.github.com/users/octocat",
        "html_url": "https://github.com/octocat",
        "followers_url": "https://api.github.com/users/octocat/followers",
        "following_url": "https://api.github.com/users/octocat/following{/other_user}",
        "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
        "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
        "organizations_url": "https://api.github.com/users/octocat/orgs",
        "repos_url": "https://api.github.com/users/octocat/repos",
        "events_url": "https://api.github.com/users/octocat/events{/privacy}",
        "received_events_url": "https://api.github.com/users/octocat/received_events",
        "type": "User",
        "site_admin": false
      },
      "access_tokens_url": "https://api.github.com/app/installations/1/access_tokens",
      "repositories_url": "https://api.github.com/installation/repositories",
      "html_url": "https://github.com/organizations/github/settings/installations/1",
      "app_id": 1,
      "target_id": 1,
      "target_type": "Organization",
      "permissions": {
        "checks": "write",
        "metadata": "read",
        "contents": "read"
      },
      "events": [
        "push",
        "pull_request"
      ],
      "single_file_name": "config.yaml",
      "has_multiple_single_files": true,
      "single_file_paths": [
        "config.yml",
        ".github/issue_TEMPLATE.md"
      ],
      "repository_selection": "all",
      "created_at": "2017-07-08T16:18:44-04:00",
      "updated_at": "2017-07-08T16:18:44-04:00",
      "app_slug": "github-actions",
      "suspended_at": null,
      "suspended_by": null
    },
    {
      "id": 3,
      "account": {
        "login": "octocat",
        "id": 2,
        "node_id": "MDQ6VXNlcjE=",
        "avatar_url": "https://github.com/images/error/octocat_happy.gif",
        "gravatar_id": "",
        "url": "https://api.github.com/users/octocat",
        "html_url": "https://github.com/octocat",
        "followers_url": "https://api.github.com/users/octocat/followers",
        "following_url": "https://api.github.com/users/octocat/following{/other_user}",
        "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
        "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
        "organizations_url": "https://api.github.com/users/octocat/orgs",
        "repos_url": "https://api.github.com/users/octocat/repos",
        "events_url": "https://api.github.com/users/octocat/events{/privacy}",
        "received_events_url": "https://api.github.com/users/octocat/received_events",
        "type": "User",
        "site_admin": false
      },
      "access_tokens_url": "https://api.github.com/app/installations/1/access_tokens",
      "repositories_url": "https://api.github.com/installation/repositories",
      "html_url": "https://github.com/organizations/github/settings/installations/1",
      "app_id": 1,
      "target_id": 1,
      "target_type": "Organization",
      "permissions": {
        "checks": "write",
        "metadata": "read",
        "contents": "read"
      },
      "events": [
        "push",
        "pull_request"
      ],
      "single_file_name": "config.yaml",
      "has_multiple_single_files": true,
      "single_file_paths": [
        "config.yml",
        ".github/issue_TEMPLATE.md"
      ],
      "repository_selection": "all",
      "created_at": "2017-07-08T16:18:44-04:00",
      "updated_at": "2017-07-08T16:18:44-04:00",
      "app_slug": "github-actions",
      "suspended_at": null,
      "suspended_by": null
    }
  ]
}
```

--------------------------------

### Authenticated API Request with Curl (Shell)

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_tool=curl

This example demonstrates how to make an authenticated request to the GitHub REST API using `curl`. It requires `curl` to be installed and an authentication token to be set in the `Authorization` header. Specific endpoints and parameters would need to be configured based on the desired API interaction.

```shell
# Example placeholder for a curl request
# Replace with actual endpoint, method, and parameters
curl -X GET \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  "https://api.github.com/user/repos"
```

--------------------------------

### Clone Repository and Initialize Project

Source: https://docs.github.com/en/packages/quickstart

This snippet demonstrates how to clone a GitHub repository and initialize a new Node.js project using npm. It includes commands for cloning, navigating into the directory, and initializing the npm package.

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
```

--------------------------------

### Install and Run Bats Package

Source: https://docs.github.com/en/actions/tutorials/creating-an-example-workflow

Installs the 'bats' software testing package globally using npm and then executes the 'bats -v' command to display its version. This verifies the installation and the tool's availability.

```yaml
      - run: npm install -g bats
      - run: bats -v
```

--------------------------------

### GET /repos/{owner}/{repo}/issues

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=cli

This endpoint retrieves a list of issues for a specific repository. The example demonstrates how to authenticate using a personal access token via the Authorization header.

```APIDOC
## GET /repos/{owner}/{repo}/issues

### Description
Retrieves a list of issues for a specified repository.

### Method
GET

### Endpoint
`https://api.github.com/repos/octocat/Spoon-Knife/issues`

### Parameters
#### Header Parameters
- **Accept** (string) - Required - Specifies the media type for the response, e.g., `application/vnd.github+json`.
- **Authorization** (string) - Required - Authentication token, typically `Bearer YOUR-TOKEN` or `token YOUR-TOKEN`.

### Request Example
```bash
curl --request GET \
--url "https://api.github.com/repos/octocat/Spoon-Knife/issues" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer YOUR-TOKEN"
```

### Response
#### Success Response (200)
- **Array of Issues** (object array) - A list of issue objects, each containing details like title, body, user, state, etc.

#### Response Example
```json
[
  {
    "url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1",
    "repository_url": "https://api.github.com/repos/octocat/Spoon-Knife",
    "labels_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/labels{/name}",
    "comments_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/comments",
    "events_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/events",
    "html_url": "https://github.com/octocat/Spoon-Knife/issues/1",
    "id": 1,
    "node_id": "MDU6SXNzdWUx",
    "number": 1,
    "title": "An issue example",
    "user": {
      "login": "octocat",
      "id": 1,
      "node_id": "MDQ6VXNlcjE=",
      "avatar_url": "https://github.com/images/error/octocat_happy.gif",
      "gravatar_id": "",
      "url": "https://api.github.com/users/octocat",
      "html_url": "https://github.com/octocat",
      "followers_url": "https://api.github.com/users/octocat/followers",
      "following_url": "https://api.github.com/users/octocat/following{/other_user}",
      "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
      "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
      "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
      "organizations_url": "https://api.github.com/users/octocat/orgs",
      "repos_url": "https://api.github.com/users/octocat/repos",
      "events_url": "https://api.github.com/users/octocat/events{/privacy}",
      "received_events_url": "https://api.github.com/users/octocat/received_events",
      "type": "User",
      "site_admin": false
    },
    "labels": [],
    "state": "open",
    "locked": false,
    "assignee": null,
    "assignees": [],
    "milestone": null,
    "comments": 0,
    "created_at": "2023-10-27T10:00:00Z",
    "updated_at": "2023-10-27T10:00:00Z",
    "closed_at": null,
    "author_association": "OWNER",
    "body": "This is a sample issue.",
    "reactions": {
      "url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/reactions",
      "total_count": 0,
      "+(-1)": 0,
      "+1": 0,
      "laugh": 0,
      "hooray": 0,
      "confused": 0,
      "heart": 0,
      "rocket": 0,
      "eyes": 0
    },
    "timeline_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/timeline",
    "performed_via_github_app": null,
    "state_reason": null
  }
]
```
```

--------------------------------

### Make GitHub API Request with curl (Command Line)

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=cli

This snippet shows how to use the `curl` command to make a GET request to the GitHub API. It includes setting the `Accept` and `Authorization` headers with a personal access token. Ensure `curl` is installed and replace `YOUR-TOKEN` with your actual token.

```shell
curl --request GET \
--url "https://api.github.com/repos/octocat/Spoon-Knife/issues" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer YOUR-TOKEN"
```

--------------------------------

### GitHub Actions - GET /repos/{owner}/{repo}/issues

Source: https://docs.github.com/en/rest/quickstart

This example shows how to use curl within a GitHub Actions workflow to fetch issues from a repository, utilizing a GitHub secret for authentication.

```APIDOC
## GitHub Actions - GET /repos/{owner}/{repo}/issues

### Description
Example of using `curl` within a GitHub Actions workflow to retrieve issues, authenticating with a GitHub secret.

### Method
GET

### Endpoint
https://api.github.com/repos/octocat/Spoon-Knife/issues

### Parameters

#### Query Parameters
None

#### Headers
- **Accept** (string) - Required - Specifies the media type for the response, e.g., `application/vnd.github+json`.
- **Authorization** (string) - Required - Contains the access token for authentication. Format: `Bearer $GH_TOKEN`, where `$GH_TOKEN` is a GitHub secret.

### Request Example
```yaml
on:
  workflow_dispatch:
jobs:
  use_api:
    runs-on: ubuntu-latest
    permissions:
      issues: read
    steps:
      - env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          curl --request GET \
          --url "https://api.github.com/repos/octocat/Spoon-Knife/issues" \
          --header "Accept: application/vnd.github+json" \
          --header "Authorization: Bearer $GH_TOKEN"
```

### Response
#### Success Response (200)
- **Array of Issue Objects** (array) - A list of issue objects.

#### Response Example
(Same as the general `curl` example above)
```

--------------------------------

### Initialize CodeQL Action with Custom Configuration and Queries

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

This example demonstrates initializing the CodeQL action with a custom configuration file and additional queries. The '+' prefix for `queries` and `packs` merges them with settings from the configuration file. It specifies a `config-file` and lists extra queries and packs.

```yaml
- uses: github/codeql-action/init@v3
  with:
    config-file: ./.github/codeql/codeql-config.yml
    queries: +security-and-quality,octo-org/python-qlpack/show_ifs.ql@main
    packs: +scope/pack1,scope/pack2@1.2.3,scope/pack3@4.5.6:path/to/queries

```

```yaml
- uses: github/codeql-action/init@v3
  with:
    config-file: ./.github/codeql/codeql-config.yml
    queries: +security-and-quality,octo-org/python-qlpack/show_ifs.ql@main
    packs: +scope/pack1,scope/pack2@1.2.3,scope/pack3@4.5.6:path/to/queries

```

--------------------------------

### Setup Node.js Environment

Source: https://docs.github.com/en/actions/tutorials/create-an-example-workflow

Sets up the specified version of Node.js (v20 in this case) using the 'actions/setup-node@v4' action. This makes the 'node' and 'npm' commands available in the PATH for subsequent steps.

```yaml
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
```

--------------------------------

### Next Steps and Further Resources

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

Provides guidance on next steps and directs users to additional relevant documentation.

```APIDOC
## Next Steps and Further Resources

### Description
This documentation has covered listing and creating issues. For further practice and exploration, consider interacting with comments, editing issue titles, or closing issues.

### Related Endpoints
- Create an issue comment
- Update an issue

### Additional Information
For a comprehensive list of available endpoints, please refer to the official GitHub REST API reference documentation.
```

--------------------------------

### Simple Dockerfile for Dev Container

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/introduction-to-dev-containers

This Dockerfile example sets up a Node.js development environment. It uses ARG to define a build-time variable for the Node.js version, FROM to specify the base image, COPY to include a script from the repository, and RUN to update package lists and execute the script. It also includes commented-out options for installing additional Node.js versions.

```dockerfile
ARG VARIANT="16"
FROM mcr.microsoft.com/devcontainers/javascript-node:1-${VARIANT}

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends bundler

# [Optional] Uncomment if you want to install an additional version
#  of node using nvm
# ARG EXTRA_NODE_VERSION=18
# RUN su node -c "source /usr/local/share/nvm/nvm.sh \
#    && nvm install ${EXTRA_NODE_VERSION}"

COPY ./script-in-your-repo.sh /tmp/scripts/script-in-codespace.sh
RUN apt-get update && bash /tmp/scripts/script-in-codespace.sh

```

--------------------------------

### Create GitHub Pull Request

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Initiates the creation of a new pull request on GitHub. Follows on-screen prompts for configuration.

```bash
gh pr create

```

--------------------------------

### Initialize npm Package and Set Test Script

Source: https://docs.github.com/en/packages/quickstart

This snippet shows the process of initializing an npm package and configuring a test script. It guides through the npm init wizard, specifying package name and test command, which generates a package.json file.

```bash
$ npm init
  ...
  package name: @YOUR-USERNAME/YOUR-REPOSITORY
  ...
  test command: exit 0
  ...
```

--------------------------------

### Example Webhook Event Reception

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/building-ci-checks-with-a-github-app

This output shows that the server successfully received an 'installation' webhook event from GitHub. It indicates the app is connected and receiving events.

```text
> D, [2023-06-08T15:45:43.773077 #30488] DEBUG -- : ---- received event installation
> D, [2023-06-08T15:45:43.773141 #30488]] DEBUG -- : ----    action created
> 192.30.252.44 - - [08/Jun/2023:15:45:43 -0400] "POST /event_handler HTTP/1.1" 200 - 0.5390

```

--------------------------------

### Start Development Server

Source: https://docs.github.com/en/apps/creating-github-apps/guides/building-a-github-app-that-responds-to-webhook-events

This command starts your application's development server using npm. It assumes a script named 'server' is defined in your package.json. The server will listen for events at the specified local webhook URL.

```bash
npm run server
```

--------------------------------

### Clone and Start Blackbeard Agent Locally

Source: https://docs.github.com/en/copilot/tutorials/try-extensions_tool=bash

Clones the Blackbeard agent repository, installs dependencies, and starts the agent. Requires Node.js and npm.

```shell
git clone https://github.com/copilot-extensions/blackbeard-extension.git
cd blackbeard-extension
npm install
npm start
```

--------------------------------

### Set up Python Environment and Install Flask

Source: https://docs.github.com/en/copilot/tutorials/migrate-a-project

This process involves creating a virtual environment for the project and installing the Flask framework and any other necessary packages using pip. It ensures a clean and isolated development environment. The commands are executed in the terminal.

```bash
python3 -m venv venv
source venv/bin/activate
pip install Flask
pip list
```

--------------------------------

### Restart a Codespace and Open in Browser using GitHub CLI

Source: https://docs.github.com/en/codespaces/developing-in-a-codespace/stopping-and-starting-a-codespace_tool=vscode

This command-line interface (CLI) instruction guides you on restarting a GitHub codespace and opening it in your web browser. The GitHub CLI must be installed and authenticated. A selection prompt will appear for available codespaces.

```shell
gh codespace open --web
```

--------------------------------

### Build and Test Node.js Code with setup-node

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/nodejs

This example demonstrates a standard workflow for building and testing Node.js code. It checks out the repository, sets up Node.js v20.x, installs npm dependencies, runs build steps if present (`npm run build --if-present`), and executes tests (`npm test`). This is useful for CI pipelines.

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

### Generating GitHub App Installation Access Token

Source: https://docs.github.com/en/rest/quickstart

This section details how to generate an installation access token for a GitHub App within a workflow. It involves storing the App ID and private key as configuration variables and secrets.

```APIDOC
## Generate GitHub App Installation Access Token

### Description
This process describes how to generate an installation access token for a GitHub App within a GitHub Actions workflow. The token is valid for 60 minutes and can be used to authenticate API requests.

### Method
Not Applicable (Workflow Step)

### Endpoint
Not Applicable (Workflow Step)

### Parameters
#### Configuration Variables
- **APP_ID** (string) - Required - The ID of your GitHub App. Store this as a configuration variable.

#### Secrets
- **APP_PEM** (string) - Required - The private key content of your GitHub App. Store the entire contents of the file (including BEGIN/END markers) as a secret.

### Request Example
```yaml
jobs:
  track_pr:
    runs-on: ubuntu-latest
    steps:
      - name: Generate token
        id: generate-token
        uses: actions/create-github-app-token@v2
        with:
          app-id: "${{ vars.APP_ID }}"
          private-key: "${{ secrets.APP_PEM }}"
      - name: Use API
        env:
          GH_TOKEN: "${{ steps.generate-token.outputs.token }}"
        run: |
          gh api https://api.github.com/repos/octocat/Spoon-Knife/issues
```

### Response
#### Success Response (Output Token)
- **token** (string) - The generated installation access token.

#### Response Example
(Output is available via `steps.generate-token.outputs.token` in GitHub Actions)
```

--------------------------------

### Create CodeQL Databases for Multiple Languages (Python, C/C++)

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

This example demonstrates creating CodeQL databases for multiple languages (Python and C/C++) simultaneously using the `--db-cluster` and `--language` options. It specifies the build command with `--command` and uses `--no-run-unnecessary-builds` to optimize the process by skipping unnecessary build commands for certain languages. The `--source-root` option points to the codebase directory.

```shell
codeql database create /codeql-dbs/example-repo-multi \
    --db-cluster --language python,c-cpp \
    --command make --no-run-unnecessary-builds \
    --source-root /checkouts/example-repo-multi
```

--------------------------------

### GET /repos/{owner}/{repo}/issues

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

Retrieves a list of issues for a specified repository. The response includes status codes and custom GitHub headers like rate limit information. Examples are provided for both `gh api` CLI and Octokit.js.

```APIDOC
## GET /repos/{owner}/{repo}/issues

### Description
Fetches a list of issues for a given repository. This endpoint returns standard HTTP status codes and custom GitHub headers, such as rate limiting information.

### Method
GET

### Endpoint
`/repos/{owner}/{repo}/issues`

### Parameters
#### Path Parameters
- **owner** (string) - Required - The owner of the repository.
- **repo** (string) - Required - The name of the repository.

#### Query Parameters
- **per_page** (integer) - Optional - The number of results per page.

### Request Example (CLI)
```bash
curl --request GET \
--url "https://api.github.com/repos/octocat/Spoon-Knife/issues?per_page=2" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer YOUR-TOKEN" \
--include
```

### Request Example (Octokit.js)
```javascript
try {
  const result = await octokit.request("GET /repos/{owner}/{repo}/issues", {
    owner: "REPO-OWNER",
    repo: "REPO-NAME",
    per_page: 2,
  });

  console.log(`Success! Status: ${result.status}. Rate limit remaining: ${result.headers["x-ratelimit-remaining"]}`)

} catch (error) {
  console.log(`Error! Status: ${error.status}. Rate limit remaining: ${error.headers["x-ratelimit-remaining"]}. Message: ${error.response.data.message}`)
}
```

### Response
#### Success Response (200)
- **status** (integer) - The HTTP status code of the response.
- **headers** (object) - An object containing the response headers, including custom GitHub headers like `x-ratelimit-remaining`.

#### Response Example (Headers)
```
HTTP/2.0 200 OK
Access-Control-Allow-Origin: *
Access-Control-Expose-Headers: ETag, Link, Location, Retry-After, X-RateLimit-Limit, X-RateLimit-Remaining, X-RateLimit-Used, X-RateLimit-Resource, X-RateLimit-Reset, X-OAuth-Scopes, X-Accepted-OAuth-Scopes, X-Poll-Interval, X-GitHub-Media-Type, X-GitHub-SSO, X-GitHub-Request-Id, Deprecation, Sunset
Cache-Control: private, max-age=60, s-maxage=60
Content-Security-Policy: default-src 'none'
Content-Type: application/json; charset=utf-8
Date: Thu, 04 Aug 2022 19:56:41 GMT
Etag: W/"a63dfbcfdb73621e9d2e89551edcf9856731ced534bd7f1e114a5da1f5f73418"
Link: <https://api.github.com/repositories/1300192/issues?per_page=1&page=2>; rel="next", <https://api.github.com/repositories/1300192/issues?per_page=1&page=14817>; rel="last"
Referrer-Policy: origin-when-cross-origin, strict-origin-when-cross-origin
Server: GitHub.com
Strict-Transport-Security: max-age=31536000; includeSubdomains; preload
Vary: Accept, Authorization, Cookie, Accept-Encoding, Accept, X-Requested-With
X-Accepted-Oauth-Scopes: repo
X-Content-Type-Options: nosniff
X-Frame-Options: deny
X-Github-Api-Version-Selected: 2022-08-09
X-Github-Media-Type: github.v3; format=json
X-Github-Request-Id: 1C73:26D4:E2E500:1EF78F4:62EC2479
X-Oauth-Client-Id: 178c6fc778ccc68e1d6a
X-Oauth-Scopes: gist, read:org, repo, workflow
X-Ratelimit-Limit: 15000
X-Ratelimit-Remaining: 14996
X-Ratelimit-Reset: 1659645499
X-Ratelimit-Resource: core
X-Ratelimit-Used: 4
X-Xss-Protection: 0
```

#### Error Response Examples
- **status** (integer) - The HTTP status code indicating an error.
- **headers** (object) - The response headers, which may include rate limit information.
- **response.data.message** (string) - A message describing the error.
```

--------------------------------

### GET /repos/{owner}/{repo}/issues

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=cli

This endpoint lists issues for a specified repository. The example shows how to use GitHub CLI within a GitHub Actions workflow to authenticate with an access token and list issues.

```APIDOC
## GET /repos/{owner}/{repo}/issues

### Description
Lists issues for a specified repository.

### Method
GET

### Endpoint
/repos/octocat/Spoon-Knife/issues

### Parameters
#### Path Parameters
- **owner** (string) - Required - The owner of the repository.
- **repo** (string) - Required - The name of the repository.

#### Query Parameters

#### Request Body

### Request Example
```yaml
on:
  workflow_dispatch:
jobs:
  use_api:
    runs-on: ubuntu-latest
    permissions:
      issues: read
    steps:
      - env:
          GH_TOKEN: "${{ secrets.GITHUB_TOKEN }}"
        run: |
          gh api https://api.github.com/repos/octocat/Spoon-Knife/issues
```

### Response
#### Success Response (200)
- **field** (type) - Description

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Sinatra Application Setup (Ruby)

Source: https://docs.github.com/en/apps/creating-github-apps/guides/creating-ci-tests-with-the-checks-api

This section sets up a basic Sinatra web application. It includes the necessary `require` statements for various gems used throughout the application, such as Sinatra, Octokit, and OpenSSL. The `run!` method is conditionally called to start the server when the script is executed directly. This code is intended for running the Sinatra app directly or with Rack.

```ruby
require 'sinatra/base'
require 'octokit'
require 'dotenv/load'
require 'json'
require 'openssl'
require 'jwt'
require 'time'
require 'logger'

# This code is a Sinatra app, for two reasons:
#   1. Because the app will require a landing page for installation.

run! if __FILE__ == $0
```

--------------------------------

### List Repositories Accessible to App Installation (GitHub CLI)

Source: https://docs.github.com/en/rest/apps/installations

Example GitHub CLI command to list repositories accessible to a GitHub App installation. This command simplifies API interactions and handles authentication implicitly if configured.

```bash
gh api /installation/repositories
```

--------------------------------

### POST /repos/{owner}/{repo}/issues

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_tool=curl

Example of creating an issue in a GitHub repository using Octokit.js. This involves specifying the owner, repository, issue title, and body.

```APIDOC
## POST /repos/{owner}/{repo}/issues

### Description
Creates a new issue in a specified GitHub repository. Requires authentication and appropriate permissions.

### Method
POST

### Endpoint
/repos/{owner}/{repo}/issues

### Parameters
#### Path Parameters
- **owner** (string) - Required - The owner of the repository.
- **repo** (string) - Required - The name of the repository.

#### Request Body
- **title** (string) - Required - The title of the issue.
- **body** (string) - Optional - The content of the issue.

### Request Example
```json
{
  "owner": "octocat",
  "repo": "Spoon-Knife",
  "title": "Created with the REST API",
  "body": "This is a test issue created by the REST API"
}
```

### Response
#### Success Response (201 Created)
- **issue** (object) - Details of the created issue.

#### Response Example
```json
{
  "url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1",
  "repository_url": "https://api.github.com/repos/octocat/Spoon-Knife",
  "labels_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/labels{/name}",
  "comments_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/comments",
  "events_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/events",
  "html_url": "https://github.com/octocat/Spoon-Knife/issues/1",
  "id": 1,
  "node_id": "MDU6SXNzdWUx",
  "number": 1,
  "title": "Created with the REST API",
  "user": {
    "login": "octocat",
    "id": 1,
    "node_id": "MDQ6VXNlcjE=",
    "avatar_url": "https://github.com/images/error/octocat_happy.gif",
    "gravatar_id": "",
    "url": "https://api.github.com/users/octocat",
    "html_url": "https://github.com/octocat",
    "followers_url": "https://api.github.com/users/octocat/followers",
    "following_url": "https://api.github.com/users/octocat/following{/other_user}",
    "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
    "organizations_url": "https://api.github.com/users/octocat/orgs",
    "repos_url": "https://api.github.com/users/octocat/repos",
    "events_url": "https://api.github.com/users/octocat/events{/privacy}",
    "received_events_url": "https://api.github.com/users/octocat/received_events",
    "type": "User",
    "site_admin": false
  },
  "labels": [],
  "state": "open",
  "locked": false,
  "assignee": null,
  "assignees": [],
  "milestone": null,
  "comments": 0,
  "created_at": "2023-01-01T12:00:00Z",
  "updated_at": "2023-01-01T12:00:00Z",
  "closed_at": null,
  "author_association": "OWNER",
  "body": "This is a test issue created by the REST API"
}
```
```

--------------------------------

### Create a Markdown Table for Profile Information

Source: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/quickstart-for-writing-on-github

Organize information in your profile README using Markdown tables. This example shows how to create a table with a header and rows, including right-aligning numeric columns.

```markdown
## About me

| Header 1 | Header 2 | Header 3 |
| :------- | :------: | -------: |
| Content 1 | Content 2 | Content 3 |
| Content 4 | Content 5 | Content 6 |
```

--------------------------------

### Create an issue with body parameters

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

This endpoint allows you to create a new issue in a repository. The example demonstrates how to provide the issue title and body as request body parameters.

```APIDOC
## POST /repos/{owner}/{repo}/issues

### Description
Creates a new issue in the specified repository. The example shows how to set the title and body of the issue.

### Method
POST

### Endpoint
/repos/{owner}/{repo}/issues

### Parameters
#### Path Parameters
- **owner** (string) - Required - The account owner of the repository.
- **repo** (string) - Required - The name of the repository.

#### Headers
- **Accept** (string) - Required - `application/vnd.github+json`
- **X-GitHub-Api-Version** (string) - Required - The API version to use, e.g., `2022-11-28`.

#### Request Body
- **title** (string) - Required - The title of the issue.
- **body** (string) - Optional - The text of the issue.

### Request Example
```shell
$ gh api --method POST /repos/octocat/Spoon-Knife/issues \
--header "Accept: application/vnd.github+json" \
--header "X-GitHub-Api-Version: 2022-11-28" \
-f title='Created with the REST API' \
-f body='This is a test issue created by the REST API' \
```

### Response
#### Success Response (201)
- **Issue object** - Details of the newly created issue, including `html_url`.
```

--------------------------------

### GET /events

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api

An example of a GET request with query parameters to list public events.

```APIDOC
## GET /events

### Description
Lists public events, with options to paginate results.

### Method
GET

### Endpoint
https://api.github.com/events

### Parameters

#### Query Parameters
- **per_page** (integer) - Optional - Number of results per page (default: 30).
- **page** (integer) - Optional - Page number of the results to fetch.

#### Request Body
None

### Request Example
```bash
curl --request GET \
--url "https://api.github.com/events?per_page=2&page=1" \
--header "Accept: application/vnd.github+json" \
--header "X-GitHub-Api-Version: 2022-11-28"
```

### Response
#### Success Response (200)
- **Array of event objects** (array) - A list of public events.

#### Response Example
```json
[
  {
    "id": "...",
    "type": "PushEvent",
    "actor": { ... },
    "repo": { ... },
    "payload": { ... }
  }
]
```
```

--------------------------------

### Complete Dev Container Configuration Example

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-python-project-for-codespaces

This is a comprehensive example of a `devcontainer.json` file, integrating settings for Python development. It includes specifying the base image, adding features like code coverage, defining a post-create command for dependency installation, and configuring VS Code extensions.

```json
{
  "name": "Python 3",
  // Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
  "image": "mcr.microsoft.com/devcontainers/python:0-3.11-bullseye",
  "features": {
    "ghcr.io/devcontainers-contrib/features/coverage-py:2": {}
  },

  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  // "forwardPorts": [],

  // Use 'postCreateCommand' to run commands after the container is created.
  "postCreateCommand": "pip3 install --user -r requirements.txt",

  // Configure tool-specific properties.
  "customizations": {
    // Configure properties specific to VS Code.
    "vscode": {
      // Add the IDs of extensions you want installed when the container is created.
      "extensions": [
        "streetsidesoftware.code-spell-checker"
      ]
    }
  }

  // Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
  // "remoteUser": "root"
}
```

--------------------------------

### GitHub CLI Request Example for Get Package

Source: https://docs.github.com/en/rest/packages/packages

Example of how to make a request to the 'Get a package for the authenticated user' endpoint using the GitHub CLI. This command-line approach simplifies API interactions.

```shell
gh api /user/packages/PACKAGE_TYPE/PACKAGE_NAME --jq '.[]'
```

--------------------------------

### Add and Commit a README File using Git

Source: https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories_tool=cli

This snippet shows how to create a README.md file, stage it, commit the changes with a message, and then push the commit to the remote repository. This is a fundamental Git workflow for tracking changes. It requires Git to be installed and configured.

```bash
echo "info about this project" >> README.md
git add README.md && git commit -m "Add README"
git push --set-upstream origin HEAD
```

--------------------------------

### Authenticate with GitHub App Token using Octokit in Node.js

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=cli

This workflow demonstrates authenticating API requests using a token generated by a GitHub App. It checks out the repository, sets up Node.js, installs `octokit`, generates an installation access token using `actions/create-github-app-token`, and then runs a Node.js script that uses this token.

```yaml
on:
  workflow_dispatch:
jobs:
  use_api_via_script:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repo content
        uses: actions/checkout@v5

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '16.17.0'
          cache: npm

      - name: Install dependencies
        run: npm install octokit

      - name: Generate token
        id: generate-token
        uses: actions/create-github-app-token@v2
        with:
          app-id: ${{ vars.APP_ID }}
          private-key: ${{ secrets.APP_PEM }}

      - name: Run script
        run: |
          node .github/actions-scripts/use-the-api.mjs
        env:
          TOKEN: ${{ steps.generate-token.outputs.token }}


```

--------------------------------

### JavaScript Request Example for Get Package

Source: https://docs.github.com/en/rest/packages/packages

Example of how to make a request to the 'Get a package for the authenticated user' endpoint using JavaScript's Fetch API. This shows how to set headers and construct the request URL.

```javascript
async function getPackage(packageType, packageName) {
  const response = await fetch(`https://api.github.com/user/packages/${packageType}/${packageName}`, {
    method: 'GET',
    headers: {
      'Accept': 'application/vnd.github+json',
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  const data = await response.json();
  return data;
}
```

--------------------------------

### Add and Commit README file using Git CLI

Source: https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories

This snippet shows how to add a README file to your local project and commit it using Git commands. It covers creating the README file, staging it for commit, committing it with a message, and pushing the changes to the remote repository.

```shell
echo "info about this project" >> README.md
git status
git add README.md && git commit -m "Add README"
git push --set-upstream origin HEAD
```

--------------------------------

### List public events with query parameters

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

This endpoint returns a list of public events. The example shows how to use `per_page` and `page` query parameters to control the number of results and the page number.

```APIDOC
## GET /events

### Description
Lists public events. By default, it returns thirty issues. This example uses query parameters to return two issues and fetch the first page.

### Method
GET

### Endpoint
/events

### Parameters
#### Query Parameters
- **per_page** (integer) - Optional - The number of results per page (default: 30).
- **page** (integer) - Optional - The page number of the results to fetch.

### Request Example
```shell
$ gh api --method GET /events -F per_page=2 -F page=1 \
--header 'Accept: application/vnd.github+json' \
```

### Response
#### Success Response (200)
- **Array of event objects** - Description of the event objects returned.
```

--------------------------------

### cURL Request Example for Get Package

Source: https://docs.github.com/en/rest/packages/packages

Example of how to make a request to the 'Get a package for the authenticated user' endpoint using cURL. This demonstrates the necessary headers and URL structure.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/user/packages/PACKAGE_TYPE/PACKAGE_NAME
```

--------------------------------

### Instantiate Installation Client (Ruby)

Source: https://docs.github.com/en/apps/creating-github-apps/guides/creating-ci-tests-with-the-checks-api

This code snippet is a placeholder for instantiating an Octokit client that is authenticated as an installation of a GitHub App. This client is used to perform API operations on behalf of the installed app.

```ruby
# Instantiate an Octokit client, authenticated as an installation of a
# GitHub App, to run API operations.
```

--------------------------------

### Get Pending Deployments for Workflow Run (GitHub CLI)

Source: https://docs.github.com/en/rest/actions/workflow-runs_apiversion=2022-11-28

This example shows how to use the GitHub CLI to retrieve pending deployments for a workflow run. It requires the CLI to be installed and authenticated.

```bash
gh api repos/OWNER/REPO/actions/runs/RUN_ID/pending_deployments \
  --header 'Accept: application/vnd.github+json' \
  --header 'X-GitHub-Api-Version: 2022-11-28'
```

--------------------------------

### Get Deployment Protection Rules (GitHub CLI)

Source: https://docs.github.com/en/rest/deployments/protection-rules

This example shows how to use the GitHub CLI to retrieve all custom deployment protection rules for a specific environment. It requires the `gh` CLI to be installed and authenticated. The command specifies the repository, environment name, and requests the protection rules.

```shell
gh api repos/OWNER/REPO/environments/ENVIRONMENT_NAME/deployment_protection_rules --jq '.custom_deployment_protection_rules[]'
```

--------------------------------

### List Installation Requests - JavaScript

Source: https://docs.github.com/en/rest/apps/apps

This JavaScript example shows how to make a request to the GitHub API to list installation requests for an authenticated GitHub App. It uses the `fetch` API and requires setting the appropriate headers. The response is parsed as JSON.

```javascript
async function listInstallationRequests() {
  const response = await fetch("https://api.github.com/app/installation-requests", {
    method: "GET",
    headers: {
      "Accept": "application/vnd.github+json",
      "Authorization": "Bearer <YOUR-TOKEN>",
      "X-GitHub-Api-Version": "2022-11-28"
    }
  });
  const data = await response.json();
  console.log(data);
}
```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=cli

Retrieves the octocat as ASCII art. This is a simple GET request example.

```APIDOC
## GET /octocat

### Description
Retrieves the octocat as ASCII art.

### Method
GET

### Endpoint
https://api.github.com/octocat

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```shell
curl --request GET \
--url "https://api.github.com/octocat" \
--header "Accept: application/vnd.github+json" \
--header "X-GitHub-Api-Version: 2022-11-28"
```

### Response
#### Success Response (200)
- **body** (string) - ASCII art representation of the octocat.

#### Response Example
```json
{
  "example": "ASCII art of octocat"
}
```
```

--------------------------------

### Initialize Octokit.js with Authentication

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&tool=cli

Demonstrates how to create an instance of Octokit.js and authenticate using a personal access token. Replace 'YOUR-TOKEN' with your actual GitHub token.

```javascript
const { Octokit } = require("octokit");

const octokit = new Octokit({
  auth: 'YOUR-TOKEN'
});

```

```javascript
import { Octokit } from "octokit";

const octokit = new Octokit({
  auth: 'YOUR-TOKEN'
});

```

--------------------------------

### Define GitHub CLI Aliases

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Create shortcuts for frequently used commands using `gh alias set`. This allows you to execute complex commands with a shorter alias. For example, `pr create --draft` can be aliased to `prd`.

```shell
gh alias set prd "pr create --draft"
```

--------------------------------

### Initializing CodeQL Action with External Configuration

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

Demonstrates how to use the `external-repository-token` parameter when the `config-file` is located in a private external repository.

```APIDOC
## POST /github/codeql-action/init@v3 (external private config)

### Description
Initializes the CodeQL action when the custom configuration file resides in a private external repository, requiring an `external-repository-token`.

### Method
POST

### Endpoint
/github/codeql-action/init@v3

### Parameters
#### Request Body
- **config-file** (string) - Required - Path to the custom configuration file in an external repository (e.g., `OWNER/REPOSITORY/FILENAME@BRANCH`).
- **external-repository-token** (string) - Required - Token with access to the private external repository containing the configuration file.

### Request Example
```yaml
- uses: github/codeql-action/init@v3
  with:
    config-file: "octo-org/shared/codeql-config.yml@main"
    external-repository-token: "${{ secrets.ACCESS_TOKEN }}"
```

### Response
#### Success Response (200)
No specific response body is detailed for this action, it primarily configures the environment for subsequent steps.

#### Response Example
(No example provided)
```

--------------------------------

### Get CodeQL Variant Analysis Summary - JavaScript

Source: https://docs.github.com/en/rest/code-scanning/code-scanning

This JavaScript example shows how to fetch the summary of a CodeQL variant analysis using the Octokit library. Ensure you have the library installed and properly configured with your authentication token. Replace placeholders with actual values.

```javascript
const { Octokit } = require("@octokit/core");
const octokit = new Octokit({ auth: "YOUR-TOKEN" });

async function getVariantAnalysisSummary(owner, repo, codeqlVariantAnalysisId) {
  try {
    const response = await octokit.request('GET /repos/{owner}/{repo}/code-scanning/codeql/variant-analyses/{codeql_variant_analysis_id}', {
      owner: owner,
      repo: repo,
      codeql_variant_analysis_id: codeqlVariantAnalysisId,
      headers: {
        'X-GitHub-Api-Version': '2022-11-28'
      }
    });
    return response.data;
  } catch (error) {
    console.error("Error fetching variant analysis summary:", error);
    throw error;
  }
}

// Example usage:
// getVariantAnalysisSummary('OWNER', 'REPO', CODEQL_VARIANT_ANALYSIS_ID).then(summary => console.log(summary));
```

--------------------------------

### Flask Application Setup - app.py

Source: https://docs.github.com/en/copilot/tutorials/migrate-a-project

This Python file sets up a basic Flask application for handling routing and views. It imports necessary modules from Flask and the os library, initializes the Flask app, and defines a configuration dictionary. It also includes placeholder functions for routing and rendering templates, indicating where routes would be mapped to views.

```Python
from flask import Flask, render_template, request
import os

app = Flask(__name__)

config = {
   'name': 'Simple Python Website',
   'site_url': '',
   'pretty_uri': False,
   'nav_menu': {
      '': 'Home',
      'about-us': 'About Us',
      'products': 'Products',
      'contact': 'Contact',
   },
   'template_path': 'template',
   'content_path': 'content',
   'version': 'v3.1',

```

--------------------------------

### Create Deployment Request (GitHub CLI)

Source: https://docs.github.com/en/rest/deployments/deployments

Example usage of the GitHub CLI to create a deployment. This command-line approach simplifies interacting with the GitHub API for deployment tasks, requiring minimal setup.

```bash
gh api repos/OWNER/REPO/deployments \
  --method POST \
  --header 'Accept: application/vnd.github+json' \
  --header 'X-GitHub-Api-Version: 2022-11-28' \
  --input deploy.json
```

--------------------------------

### List Installations for Authenticated App (GitHub CLI)

Source: https://docs.github.com/en/rest/apps/apps

Example of how to list installations for an authenticated GitHub App using the GitHub CLI. This command simplifies API interactions.

```bash
gh api /app/installations --jq '.'
```

--------------------------------

### Example: Apply Instructions to All Files

Source: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions_tool=visualstudio

This code snippet demonstrates the use of the `applyTo: "**"` directive in the frontmatter of a path-specific instructions file. This configuration ensures that the provided instructions are applied to all files and directories within the repository.

```yaml
---
applyTo: "**"
---
```

--------------------------------

### GitHub Actions Workflow Configuration Example (YAML)

Source: https://docs.github.com/en/copilot/tutorials/customization-library/custom-instructions/github-actions-helper

This snippet demonstrates a basic GitHub Actions workflow configuration using YAML. It includes common elements like triggers, job definitions, runner selection, caching, and steps for checking out code, setting up Node.js, installing dependencies, and running tests. It is intended to be a starting point for workflow customization.

```yaml
name: CI
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm test
```

--------------------------------

### Set Up Local GitHub Docs Environment

Source: https://docs.github.com/en/contributing/setting-up-your-environment-to-work-on-github-docs/creating-a-local-environment

Commands to clone the GitHub Docs repository, navigate into the directory, install project dependencies cleanly, and start the local development server.

```shell
git clone https://github.com/github/docs
cd docs
npm ci
npm start
```

--------------------------------

### Configure CodeQL Init Action with GitHub Actions Variable

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

This example shows how to use a GitHub Actions variable (`vars.CODEQL_CONF`) to provide the CodeQL configuration to the `init` action. This allows for centralized management of configurations across multiple repositories.

```yaml
- uses: github/codeql-action/init@v3
  with:
    languages: ${{ matrix.language }}
    config: ${{ vars.CODEQL_CONF }}

```

--------------------------------

### List User Repositories Request Example (cURL)

Source: https://docs.github.com/en/rest/apps/installations

Example of how to request a list of repositories accessible to a user access token using cURL. This includes setting the necessary headers for authentication and API versioning.

```bash
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/user/installations/1/repositories
```

--------------------------------

### Multi-dimensional Matrix Example

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

This example demonstrates a multi-dimensional matrix where jobs are created for each combination of 'os' and 'version'. Each job runs on a specific OS and sets up a specific Node.js version. Dependencies include the 'actions/setup-node' action.

```yaml
jobs:
  example_matrix:
    strategy:
      matrix:
        os: [ubuntu-22.04, ubuntu-20.04]
        version: [10, 12, 14]
    runs-on: ${{ matrix.os }}
    steps:
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.version }}

```

--------------------------------

### Multi-language CodeQL setup with different build modes

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/codeql-code-scanning-for-compiled-languages

This example demonstrates how to configure the CodeQL action to use different build modes for various languages within a single repository. It uses a matrix strategy to include configurations for C/C++ (manual build), C# (autobuild), and Java (none build). The `actions/checkout@v5` action is used to checkout the repository, and the `github/codeql-action/init@v3` action initializes CodeQL tools and creates a database. A conditional step is included for the manual build mode to specify build commands.

```yaml
strategy:
  matrix:
    include:
      # Analyzes C and C++ code using the commands in `Build C and C++ code`
      - language: c-cpp
        build-mode: manual
      # Analyzes C# code by automatically detecting a build
      - language: csharp
        build-mode: autobuild
      # Analyzes Java code directly from the codebase without a build
      - language: java-kotlin
        build-mode: none # analyzes Java only
steps:
- name: Checkout repository
  uses: actions/checkout@v5

# Initializes CodeQL tools and creates a codebase for analysis.
- name: Initialize CodeQL
  uses: github/codeql-action/init@v3
  with:
    languages: ${{ matrix.language }}
- if: ${{ matrix.build-mode == 'manual' }}
  name: Build C and C++ code
  run: |
    echo 'If you are using a "manual" build mode for one or more of the' \
      'languages you are analyzing, replace this with the commands to build' \
      'your code, for example:'
    echo ' make bootstrap'
    echo ' make release'
    exit 1

```

--------------------------------

### Authenticated GitHub API Request using curl

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&tool=curl

Demonstrates making an authenticated request to the GitHub REST API using `curl`. This requires `curl` to be installed and an access token for authentication, which is sent in the `Authorization` header. The example guides through choosing an endpoint, method, path, and handling path parameters.

```shell
# Example setup (replace with actual endpoint and token)
# curl -H "Authorization: Bearer YOUR_ACCESS_TOKEN" https://api.github.com/some/endpoint
```

--------------------------------

### Contribute to an Existing Repository with Git

Source: https://docs.github.com/en/get-started/using-git/about-git

This example demonstrates how to clone a remote repository, create a new branch, make changes, stage them, commit them, and push them to GitHub. It assumes you are starting from scratch or contributing to a project that exists on GitHub.

```bash
# download a repository on GitHub to our machine
# Replace `owner/repo` with the owner and name of the repository to clone
git clone https://github.com/owner/repo.git

# change into the `repo` directory
cd repo

# create a new branch to store any new changes
git branch my-branch

# switch to that branch (line of development)
git checkout my-branch

# make changes, for example, edit `file1.md` and `file2.md` using the text editor

# stage the changed files
git add file1.md file2.md

# take a snapshot of the staging area (anything that's been added)
git commit -m "my snapshot"

# push changes to github
git push --set-upstream origin my-branch

```

--------------------------------

### Install GitHub CLI on Windows Runner using Chocolatey

Source: https://docs.github.com/en/actions/how-tos/manage-runners/github-hosted-runners/customize-runners

Shows how to install the GitHub CLI on a Windows-hosted GitHub runner using Chocolatey. The example includes a subsequent step to verify the installation.

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

### Initialize CodeQL Action with Private Repository Token

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

This example demonstrates initializing the CodeQL action and accessing resources from a private repository. It uses the `external-repository-token` parameter to provide credentials for checking out private repositories containing queries or configuration files.

```yaml
- uses: github/codeql-action/init@v3
  with:
    external-repository-token: ${{ secrets.ACCESS_TOKEN }}

```

```yaml
- uses: github/codeql-action/init@v3
  with:
    external-repository-token: ${{ secrets.ACCESS_TOKEN }}

```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api

Retrieves the 'octocat' as ASCII art. This example demonstrates a basic GET request with necessary headers.

```APIDOC
## GET /octocat

### Description
This endpoint retrieves the 'octocat' as ASCII art. It serves as a simple example for making authenticated requests to the GitHub API.

### Method
GET

### Endpoint
/octocat

### Parameters
#### Query Parameters
None

#### Request Body
None

### Request Example
```shell
gh api --method GET /octocat \
--header 'Accept: application/vnd.github+json' \
--header "X-GitHub-Api-Version: 2022-11-28"
```

### Response
#### Success Response (200)
- **ascii_art** (string) - The 'octocat' as ASCII art.

#### Response Example
```json
{
  "message": "Hello from Octocat!",
  "ascii": "... (ASCII art representation of Octocat) ..."
}
```
```

--------------------------------

### Start User Migration Request Example

Source: https://docs.github.com/en/rest/migrations/users

Demonstrates how to initiate a user migration archive using the GitHub API. This example shows the cURL command for making a POST request to the /user/migrations endpoint, including required headers and a JSON payload to specify repositories and lock them during migration.

```bash
curl -L \
  -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/user/migrations \
  -d '{"repositories":["octocat/Hello-World"],"lock_repositories":true}'
```

--------------------------------

### Generate GitHub App Token and Use API (YAML)

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=cli

This snippet shows a GitHub Actions workflow that generates an installation access token for a GitHub App and then uses this token to make a GET request to the GitHub API. It requires the App ID and private key to be stored as repository secrets. The generated token has a 60-minute expiration.

```yaml
on:
  workflow_dispatch:
jobs:
  use_api:
    runs-on: ubuntu-latest
    steps:
      - name: Generate token
        id: generate-token
        uses: actions/create-github-app-token@v2
        with:
          app-id: ${{ vars.APP_ID }}
          private-key: ${{ secrets.APP_PEM }}

      - name: Use API
        env:
          GH_TOKEN: ${{ steps.generate-token.outputs.token }}
        run: |
          curl --request GET \
          --url "https://api.github.com/repos/octocat/Spoon-Knife/issues" \
          --header "Accept: application/vnd.github+json" \
          --header "Authorization: Bearer $GH_TOKEN"
```

--------------------------------

### Create Root Custom Instructions File

Source: https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot_tool=vscode

To provide general instructions for Copilot across the entire repository, create a file named `copilot-instructions.md` in the root directory. This file should contain natural language instructions in Markdown format that are broadly applicable to most requests within the repository.

```markdown
# Project Overview

This project is a web application that allows users to manage their tasks and to-do lists. It is built using React and Node.js, and uses MongoDB for data storage.

## Folder Structure

- `/src`: Contains the source code for the frontend.
- `/server`: Contains the source code for the Node.js backend.
- `/docs`: Contains documentation for the project, including API specifications and user guides.

## Libraries and Frameworks

- React and Tailwind CSS for the frontend.
- Node.js and Express for the backend.
- MongoDB for data storage.

```

--------------------------------

### Authenticate with Installation Access Token using curl

Source: https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-as-a-github-app-installation

This example shows how to authenticate API requests using a previously generated installation access token. The token is included in the `Authorization` header with the `Bearer` prefix. This method works for both REST and GraphQL API endpoints.

```bash
curl --request GET \
--url "https://api.github.com/meta" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer INSTALLATION_ACCESS_TOKEN" \
--header "X-GitHub-Api-Version: 2022-11-28"

```

--------------------------------

### GET /events with Query Parameters

Source: https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api_tool=cli

An example of making a GET request to the '/events' endpoint with query parameters `per_page` and `page` to control pagination.

```APIDOC
## GET /events

### Description
Lists public events, with the ability to control the number of events per page and the page number.

### Method
GET

### Endpoint
https://api.github.com/events

### Parameters
#### Path Parameters
None

#### Query Parameters
- **per_page** (integer) - Optional - The number of results per page (max 100). Default is 30.
- **page** (integer) - Optional - Page number of the results to fetch.

#### Request Body
None

### Request Example
```bash
curl --request GET \
--url "https://api.github.com/events?per_page=2&page=1" \
--header "Accept: application/vnd.github+json" \
--header "X-GitHub-Api-Version: 2022-11-28"
```

### Response
#### Success Response (200)
- **Events**: array - A list of event objects.
  - **event object**: object - Contains details of a specific event.

#### Response Example
```json
{
  "example": "[ { ... event object ... }, { ... event object ... } ]"
}
```
```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

This endpoint retrieves the GitHub Octocat as ASCII art. It demonstrates a basic GET request with required headers.

```APIDOC
## GET /octocat

### Description
Retrieves the GitHub Octocat as ASCII art.

### Method
GET

### Endpoint
/octocat

### Parameters
#### Query Parameters
- **cat** (string) - Optional - Cat name to return. Defaults to "shipiaoc" if not provided.
- **s** (string) - Optional - Number of spiders to return. Defaults to "10" if not provided.

#### Request Body
None

### Request Example
```shell
gh api --method GET /octocat \
--header 'Accept: application/vnd.github+json' \
--header "X-GitHub-Api-Version: 2022-11-28"
```

### Response
#### Success Response (200)
- **(string)** - ASCII art representation of the Octocat.

#### Response Example
```json
"\n      \"\"\n     / \\ / \\  \n    /  .)  (\\  \n   /  / \\/ \\ \\ \n  /  / \\/ \\ \\ \\ \n /  / \\/ \\ \\ \\ \n( _/ /_  )/_ )_)
```
```

--------------------------------

### Get CodeQL Database for Repository (GitHub CLI)

Source: https://docs.github.com/en/rest/code-scanning/code-scanning

This example uses the GitHub CLI (`gh`) to retrieve a CodeQL database. The `gh api` command allows direct interaction with the GitHub API, simplifying authentication and request construction. Ensure you have the GitHub CLI installed and authenticated.

```bash
gh api repos/OWNER/REPO/code-scanning/codeql/databases/LANGUAGE \
  --header 'Accept: application/vnd.github+json' \
  --header 'X-GitHub-Api-Version: 2022-11-28'
```

--------------------------------

### GET /app/installations/{installation_id}

Source: https://docs.github.com/en/rest/apps/apps

Retrieves details about a specific GitHub app installation. You can use this endpoint to get information about the installation ID, the account it's associated with, permissions granted, and more.

```APIDOC
## GET /app/installations/{installation_id}

### Description
Retrieves details about a specific GitHub app installation.

### Method
GET

### Endpoint
`/app/installations/{installation_id}`

### Parameters
#### Path Parameters
- **installation_id** (integer) - Required - The unique identifier of the installation.

### Request Example
(No request body for this GET request)

### Response
#### Success Response (200)
- **id** (integer) - The unique identifier of the installation.
- **account** (object) - Information about the owner of the installation.
  - **login** (string) - The login name of the owner.
  - **id** (integer) - The unique identifier of the owner.
  - **node_id** (string) - The GraphQL Node ID of the owner.
  - **avatar_url** (string) - URL for the owner's avatar image.
  - **gravatar_id** (string) - Gravatar ID of the owner.
  - **url** (string) - URL for the owner's API.
  - **html_url** (string) - URL for the owner's profile page.
  - **followers_url** (string) - URL for the owner's followers.
  - **following_url** (string) - URL for the owner's following list.
  - **gists_url** (string) - URL for the owner's gists.
  - **starred_url** (string) - URL for the owner's starred repositories.
  - **subscriptions_url** (string) - URL for the owner's subscriptions.
  - **organizations_url** (string) - URL for the owner's organizations.
  - **repos_url** (string) - URL for the owner's repositories.
  - **events_url** (string) - URL for the owner's events.
  - **received_events_url** (string) - URL for the owner's received events.
  - **type** (string) - The type of the owner (e.g., 'Organization', 'User').
  - **site_admin** (boolean) - Whether the owner is a site administrator.
- **repository_selection** (string) - Indicates which repositories are visible to the app (e.g., 'all', 'selected').
- **access_tokens_url** (string) - URL to access the installation's access tokens.
- **repositories_url** (string) - URL to list the repositories accessible to the installation.
- **html_url** (string) - URL to the installation's settings page on GitHub.
- **app_id** (integer) - The ID of the GitHub App.
- **client_id** (string) - The client ID for the GitHub App.
- **target_id** (integer) - The ID of the owner of the installation.
- **target_type** (string) - The type of the owner (e.g., 'Organization', 'User').
- **permissions** (object) - The permissions granted to the installation.
  - **checks** (string) - Access level for checks.
  - **metadata** (string) - Access level for metadata.
  - **contents** (string) - Access level for contents.
- **events** (array) - A list of events the installation is subscribed to.
- **created_at** (string) - Timestamp when the installation was created (ISO 8601 format).
- **updated_at** (string) - Timestamp when the installation was last updated (ISO 8601 format).
- **single_file_name** (string) - The name of a single file configured for the installation.
- **has_multiple_single_files** (boolean) - Indicates if multiple single files are configured.
- **single_file_paths** (array) - A list of paths for single files.
- **app_slug** (string) - The slug of the GitHub App.
- **suspended_at** (string) - Timestamp when the installation was suspended (ISO 8601 format), or null if not suspended.
- **suspended_by** (string) - Information about who suspended the installation, or null.

#### Response Example
```json
{
  "id": 1,
  "account": {
    "login": "github",
    "id": 1,
    "node_id": "MDEyOk9yZ2FuaXphdGlvbjE=",
    "avatar_url": "https://github.com/images/error/hubot_happy.gif",
    "gravatar_id": "",
    "url": "https://api.github.com/orgs/github",
    "html_url": "https://github.com/github",
    "followers_url": "https://api.github.com/users/github/followers",
    "following_url": "https://api.github.com/users/github/following{/other_user}",
    "gists_url": "https://api.github.com/users/github/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/github/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/github/subscriptions",
    "organizations_url": "https://api.github.com/users/github/orgs",
    "repos_url": "https://api.github.com/orgs/github/repos",
    "events_url": "https://api.github.com/orgs/github/events",
    "received_events_url": "https://api.github.com/users/github/received_events",
    "type": "Organization",
    "site_admin": false
  },
  "repository_selection": "all",
  "access_tokens_url": "https://api.github.com/app/installations/1/access_tokens",
  "repositories_url": "https://api.github.com/installation/repositories",
  "html_url": "https://github.com/organizations/github/settings/installations/1",
  "app_id": 1,
  "client_id": "Iv1.ab1112223334445c",
  "target_id": 1,
  "target_type": "Organization",
  "permissions": {
    "checks": "write",
    "metadata": "read",
    "contents": "read"
  },
  "events": [
    "push",
    "pull_request"
  ],
  "created_at": "2018-02-09T20:51:14Z",
  "updated_at": "2018-02-09T20:51:14Z",
  "single_file_name": "config.yml",
  "has_multiple_single_files": true,
  "single_file_paths": [
    "config.yml",
    ".github/issue_TEMPLATE.md"
  ],
  "app_slug": "github-actions",
  "suspended_at": null,
  "suspended_by": null
}
```
```

--------------------------------

### Complete devcontainer.json Example

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-java-project-for-codespaces

This is a comprehensive example of a `devcontainer.json` file incorporating Java and Ant SDK features, a post-create command to generate a file, and the installation of specified VS Code extensions. It also includes basic container configuration like name and image.

```json
{
  "name": "Java",
  // Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
  "image": "mcr.microsoft.com/devcontainers/java:0-17",

  "features": {
    "ghcr.io/devcontainers/features/java:1": {
      "version": "none",
      "installMaven": "true",
      "installGradle": "false"
    },
    "ghcr.io/devcontainers-contrib/features/ant-sdkman:2": {}
  },

  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  // "forwardPorts": [],

  // Use 'postCreateCommand' to run commands after the container is created.
  "postCreateCommand": "echo \"This file was added by the postCreateCommand.\" > TEMP.md",

  // Configure tool-specific properties.
  "customizations": {
    // Configure properties specific to VS Code.
    "vscode": {
      // Add the IDs of extensions you want installed when the container is created.
      "extensions": [
        "streetsidesoftware.code-spell-checker",
        "vscjava.vscode-java-pack"
      ]
    }
  }

  // Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
  // "remoteUser": "root"
}
```

--------------------------------

### Initialize CodeQL database for indirect build tracing

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Initializes a CodeQL database with tracing enabled, creating skeleton files and scripts for setting up the tracing environment. Requires a path for the new database and optionally accepts tracing options. The output indicates the successful creation of the database skeleton and the location of tracing environment scripts.

```bash
codeql database init <database> --begin-tracing
```

--------------------------------

### View GitHub CLI Status

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Displays details of your current work on GitHub across all subscribed repositories. This command provides an overview of your activity.

```bash
gh status

```

--------------------------------

### Cache Yarn Dependencies with setup-node

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/nodejs

This example demonstrates caching Yarn dependencies using the `actions/setup-node` action. It sets up Node.js v20 and specifically configures caching for Yarn. The workflow checks out code, sets up Node.js with Yarn caching, installs dependencies using `yarn`, and runs tests with `yarn test`.

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

### Configure Copilot Setup Steps Workflow in YAML

Source: https://docs.github.com/en/copilot/customizing-copilot/customizing-the-development-environment-for-copilot-coding-agent

This YAML workflow file, placed at `.github/workflows/copilot-setup-steps.yml`, defines steps to set up the Copilot agent's environment before it starts. It includes actions for checking out code, setting up Node.js, and installing JavaScript dependencies, which are crucial for projects using npm. The workflow is triggered on push, pull request, or manually.

```yaml
name: "Copilot Setup Steps"

# Automatically run the setup steps when they are changed to allow for easy validation, and
# allow manual testing through the repository's "Actions" tab
on:
  workflow_dispatch:
  push:
    paths:
      - .github/workflows/copilot-setup-steps.yml
  pull_request:
    paths:
      - .github/workflows/copilot-setup-steps.yml

jobs:
  # The job MUST be called `copilot-setup-steps` or it will not be picked up by Copilot.
  copilot-setup-steps:
    runs-on: ubuntu-latest

    # Set the permissions to the lowest permissions possible needed for your steps.
    # Copilot will be given its own token for its operations.
    permissions:
      # If you want to clone the repository as part of your setup steps, for example to install dependencies, you'll need the `contents: read` permission. If you don't clone the repository in your setup steps, Copilot will do this for you automatically after the steps complete.
      contents: read

    # You can define any steps you want, and they will run before the agent starts.
    # If you do not check out your code, Copilot will do this for you.
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: "20"
          cache: "npm"

      - name: Install JavaScript dependencies
        run: npm ci

```

--------------------------------

### Install Octokit.js

Source: https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api

This code snippet shows how to install the Octokit.js library using npm. Ensure you have Node.js and npm installed on your system. This is a prerequisite for using the Octokit.js library in your project.

```bash
npm install octokit
```

--------------------------------

### Construct GitHub App Installation URL

Source: https://docs.github.com/en/apps/creating-github-apps/guides/migrating-oauth-apps-to-github-apps

This URL format allows users to install your GitHub App. You can pre-select repositories by appending '/permissions' and query parameters like 'suggested_target_id' and 'repository_ids[]'. The maximum number of pre-selected repositories is 100. Ensure 'suggested_target_id' is provided, and 'repository_ids[]' can be omitted to select all repositories.

```text
https://github.com/apps/YOUR_APP_NAME/installations/new
https://github.com/apps/YOUR_APP_NAME/installations/new/permissions?suggested_target_id=ID_OF_USER_OR_ORG&repository_ids[]=REPO_A_ID&repository_ids[]=REPO_B_ID
```

--------------------------------

### List GitHub Pull Requests

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Lists open pull requests for a specified repository. Supports filtering by author or label. Can search for pull requests requiring your review.

```bash
gh pr list --repo OWNER/REPO
gh pr list --author "@me"
gh pr list --label LABEL-NAME
gh search prs --review-requested=@me --state=open

```

--------------------------------

### Generated `codeql-pack.lock.yml` Example

Source: https://docs.github.com/en/code-security/codeql-cli/using-the-advanced-functionality-of-the-codeql-cli/about-codeql-workspaces

An example of a lock file generated after `codeql pack install`. It records the resolved versions of downloaded dependencies, but not workspace-resolved source dependencies.

```yaml
dependencies:
  codeql/cpp-all:
    version: 0.2.2

```

--------------------------------

### Get Release Assets Example (cURL, JavaScript, GitHub CLI)

Source: https://docs.github.com/en/rest/releases/assets

Example of how to retrieve release assets for a specific release using different tools. This involves making a GET request to the GitHub API. Ensure you include the necessary authentication headers.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/releases/RELEASE_ID/assets
```

```javascript
async function getReleaseAssets(owner, repo, releaseId, token) {
  const url = `https://api.github.com/repos/${owner}/${repo}/releases/${releaseId}/assets`;
  const headers = {
    'Accept': 'application/vnd.github+json',
    'Authorization': `Bearer ${token}`,
    'X-GitHub-Api-Version': '2022-11-28'
  };

  try {
    const response = await fetch(url, {
      method: 'GET',
      headers: headers
    });
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const assets = await response.json();
    console.log(assets);
    return assets;
  } catch (error) {
    console.error('Error fetching release assets:', error);
  }
}

// Example usage:
// getReleaseAssets('OWNER', 'REPO', 'RELEASE_ID', '<YOUR-TOKEN>');
```

```github cli
gh api repos/OWNER/REPO/releases/RELEASE_ID/assets --jq '.'
```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_tool=curl

This endpoint retrieves the GitHub Octocat as ASCII art. It demonstrates a basic authenticated GET request using the GitHub CLI.

```APIDOC
## GET /octocat

### Description
Retrieves the GitHub Octocat as ASCII art. This is a simple example of making an authenticated GET request.

### Method
GET

### Endpoint
/octocat

### Parameters
#### Query Parameters
- **per_page** (integer) - Optional - The number of results to return per page.
- **page** (integer) - Optional - The page number to retrieve.

#### Request Body
None

### Request Example
```sh
gh api --method GET /octocat \
--header 'Accept: application/vnd.github+json' \
--header "X-GitHub-Api-Version: 2022-11-28"
```

### Response
#### Success Response (200)
- **ascii_art** (string) - The Octocat represented as ASCII art.

#### Response Example
```json
{
  "ascii_art": "\n      \/\n     /  |\n    /  / 
   /  / 
  /  /\n /  /\n/  /\n\/ /\n \/ /
  \/ 
"
}
```
```

--------------------------------

### Initialize CodeQL Action with Configuration File

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

This snippet shows how to initialize the CodeQL action by specifying a custom configuration file using the `config-file` parameter. This allows for centralized management of analysis settings, query inclusion/exclusion, and scan directories.

```yaml
- uses: github/codeql-action/init@v3
  with:
    config-file: ./.github/codeql/codeql-config.yml

```

```yaml
- uses: github/codeql-action/init@v3
  with:
    config-file: ./.github/codeql/codeql-config.yml

```

--------------------------------

### GitHub CLI GraphQL Query Example

Source: https://docs.github.com/en/graphql/guides/using-graphql-clients

An example of how to run a GraphQL query using the GitHub CLI. This command sends a query to the GitHub GraphQL endpoint and returns the viewer's login. Requires installation and authentication of GitHub CLI.

```bash
gh api graphql -f query='query { viewer { login } }'

```

--------------------------------

### Get Commit Object Request Example (cURL)

Source: https://docs.github.com/en/rest/git/commits

Example of how to fetch a commit object using cURL. It includes necessary headers like Accept, Authorization, and X-GitHub-Api-Version.

```shell
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/git/commits/COMMIT_SHA
```

--------------------------------

### Manage GitHub Codespaces

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Commands for interacting with GitHub Codespaces, including creating, listing, and opening codespaces. 'cs' can be used as a shorthand for 'codespace'.

```bash
gh codespace create
gh codespace list
gh codespace code -w
cs list

```

--------------------------------

### Install Runner Scale Set using Helm

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

Installs the latest version of the runner scale set Helm chart. Ensure to update INSTALLATION_NAME, NAMESPACE, GITHUB_CONFIG_URL, and GITHUB_PAT with your specific values. For specific versions, use the --version argument. Best practices include using separate namespaces for operator and runner pods and employing Kubernetes secrets.

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

### Start a Codespace using GitHub CLI

Source: https://docs.github.com/en/rest/codespaces/codespaces

This example shows how to start a codespace using the GitHub Command Line Interface (CLI). It leverages the `gh codespace start` command, which abstracts the API call. Ensure you are authenticated with the CLI (`gh auth login`) and replace `CODESPACE_NAME` with your target codespace.

```bash
gh codespace start --codespace CODESPACE_NAME
```

--------------------------------

### List Installed Helm Releases

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

Checks the status of all deployed Helm releases across all namespaces. This command helps verify if the runner scale set was successfully installed and is running.

```bash
helm list -A

```

```bash
helm list -A

```

--------------------------------

### List Repositories Accessible to App Installation (JavaScript)

Source: https://docs.github.com/en/rest/apps/installations

Example JavaScript request to list repositories accessible to a GitHub App installation using the Fetch API. It demonstrates setting the required 'Accept' and 'X-GitHub-Api-Version' headers. Authentication may be required depending on the resource's privacy.

```javascript
async function listInstallationRepositories() {
  const response = await fetch('https://api.github.com/installation/repositories', {
    headers: {
      'Accept': 'application/vnd.github+json',
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  const data = await response.json();
  console.log(data);
}
```

--------------------------------

### Install GitHub Copilot in Vim/Neovim (Windows)

Source: https://docs.github.com/en/copilot/managing-copilot/configure-personal-settings/installing-the-github-copilot-extension-in-your-environment

Clones the GitHub Copilot Vim plugin into the Neovim or Vim start directory for Windows systems using Git Bash. This facilitates AI coding suggestions in the editor.

```shell
git clone https://github.com/github/copilot.vim.git \
$HOME/AppData/Local/nvim/pack/github/start/copilot.vim
```

```shell
git clone https://github.com/github/copilot.vim.git \
$HOME/vimfiles/pack/github/start/copilot.vim
```

--------------------------------

### List Repositories Accessible to App Installation (cURL)

Source: https://docs.github.com/en/rest/apps/installations

Example cURL request to list repositories accessible to a GitHub App installation. It requires setting the 'Accept' and 'X-GitHub-Api-Version' headers. This endpoint can be used without authentication for public resources.

```bash
curl \
  -L \
  -H "Accept: application/vnd.github+json" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/installation/repositories
```

--------------------------------

### Get Combined Commit Status (GitHub CLI)

Source: https://docs.github.com/en/rest/commits/statuses

Example of how to retrieve the combined commit status for a specific reference using the GitHub CLI (gh). This command simplifies API interactions by handling authentication and request formatting. It requires the GitHub CLI to be installed and authenticated.

```bash
gh api repos/OWNER/REPO/commits/REF/status \
  --header 'Accept: application/vnd.github+json' \
  --header 'X-GitHub-Api-Version: 2022-11-28'
```

--------------------------------

### Verify GitHub Actions Importer Installation (Bash)

Source: https://docs.github.com/en/actions/tutorials/migrate-to-github-actions/automated-migrations/travis-ci-migration

Verifies that the GitHub Actions Importer CLI extension is installed by displaying its help information. This command is used after installation to confirm successful setup.

```Bash
gh actions-importer -h
```

--------------------------------

### Set up Kustomize

Source: https://docs.github.com/en/actions/how-tos/deploy/deploy-to-third-party-platforms/google-kubernetes-engine

Downloads and makes executable the Kustomize binary, a tool for customizing Kubernetes manifests. This is used to manage deployment configurations.

```yaml
    # Set up kustomize
    - name: Set up Kustomize
      run: |-
        curl -sfLo kustomize https://github.com/kubernetes-sigs/kustomize/releases/download/v3.1.0/kustomize_3.1.0_linux_amd64
        chmod u+x ./kustomize
```

--------------------------------

### Create Single CodeQL Database for JavaScript/TypeScript

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

This example demonstrates how to create a single CodeQL database for JavaScript and TypeScript code within a repository. It specifies the output directory, the language, and the source root of the repository. The command initializes, extracts, and finalizes the database.

```bash
$ codeql database create /codeql-dbs/example-repo --language=javascript-typescript \
    --source-root /checkouts/example-repo

> Initializing database at /codeql-dbs/example-repo.
> Running command [/codeql-home/codeql/javascript/tools/autobuild.cmd]
    in /checkouts/example-repo.
> [build-stdout] Single-threaded extraction.
> [build-stdout] Extracting
...
> Finalizing database at /codeql-dbs/example-repo.
> Successfully created database at /codeql-dbs/example-repo.


```

--------------------------------

### Create or update environment request examples (cURL, JavaScript, GitHub CLI)

Source: https://docs.github.com/en/rest/deployments/environments

Examples demonstrating how to send a PUT request to create or update a GitHub environment. These examples cover cURL, JavaScript using the fetch API, and the GitHub CLI, providing variations for different automation needs. Ensure you replace placeholders like OWNER, REPO, ENVIRONMENT_NAME, and YOUR-TOKEN with actual values.

```curl
curl -L \
  -X PUT \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/environments/ENVIRONMENT_NAME \
  -d '{"wait_timer":30,"prevent_self_review":false,"reviewers":[{"type":"User","id":1},{"type":"Team","id":1}],"deployment_branch_policy":{"protected_branches":false,"custom_branch_policies":true}}'
```

```javascript
async function createOrUpdateEnvironment() {
  const owner = 'OWNER';
  const repo = 'REPO';
  const environmentName = 'ENVIRONMENT_NAME';
  const token = 'YOUR-TOKEN';

  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/environments/${environmentName}`, {
    method: 'PUT',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    },
    body: JSON.stringify({
      "wait_timer": 30,
      "prevent_self_review": false,
      "reviewers": [
        {
          "type": "User",
          "id": 1
        },
        {
          "type": "Team",
          "id": 1
        }
      ],
      "deployment_branch_policy": {
        "protected_branches": false,
        "custom_branch_policies": true
      }
    })
  });

  if (!response.ok) {
    const errorData = await response.json();
    console.error('Error creating or updating environment:', response.status, errorData);
    return;
  }

  const data = await response.json();
  console.log('Environment created or updated:', data);
}

createOrUpdateEnvironment();
```

```bash
gh api repos/OWNER/REPO/environments/ENVIRONMENT_NAME \
  --method PUT \
  --header "Accept: application/vnd.github+json" \
  --header "X-GitHub-Api-Version: 2022-11-28" \
  --body '{"wait_timer":30,"prevent_self_review":false,"reviewers":[{"type":"User","id":1},{"type":"Team","id":1}],"deployment_branch_policy":{"protected_branches":false,"custom_branch_policies":true}}'
```

--------------------------------

### GitHub Sponsors GraphQL API - Introduction

Source: https://docs.github.com/en/sponsors/integrating-with-github-sponsors/getting-started-with-the-sponsors-graphql-api

This section provides an overview of the GitHub Sponsors GraphQL API and how to get started with it. It includes links to introductory materials and reference documentation.

```APIDOC
## GitHub Sponsors GraphQL API Overview

### Description
Use the GraphQL API to build custom integrations for managing or reviewing your GitHub sponsorships. This API allows for programmatic interaction with sponsorship data.

### Getting Started
- **Introduction to GraphQL**: For a foundational understanding of GraphQL, refer to the [Introduction to GraphQL](https://graphql.org/learn/).
- **Sponsors GraphQL API Reference**: Detailed information about the API's queries, mutations, and types can be found in the [Reference Docs](https://docs.github.com/graphql/reference/mutations#createsponsorship).
- **Using GraphQL Clients**: Recommendations and guidance on using GraphQL clients to construct your API calls are available in the [Using GraphQL Clients](https://docs.github.com/graphql/guides/using-graphql-clients) documentation.

### Known Issues
- **`createSponsorship` Mutation**: The `createSponsorship` mutation currently has a known issue where it does not function correctly for one-time payments. Further details and discussion can be found [here](https://github.com/github/feedback/discussions/6806).
```

--------------------------------

### Create Installation Access Token Request (cURL)

Source: https://docs.github.com/en/rest/apps/apps

Example cURL request to create an installation access token for an app. This requires the installation ID and specifies desired repository and permission scopes. The response will include the generated token.

```bash
curl -L \
  -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/app/installations/1/access_tokens \
  -d '{"repositories":["Hello-World"],"permissions":{"issues":"write","contents":"read"}}'
```

--------------------------------

### Initializing CodeQL Action with Queries

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

This section describes how to use the `queries` and `external-repository-token` parameters within the `github/codeql-action/init@v3` step to specify queries or query suites for analysis. It also explains the use of built-in query suites like `security-extended` and `security-and-quality`.

```APIDOC
## POST /github/codeql-action/init@v3

### Description
Initializes the CodeQL action, allowing the specification of queries, query suites, and authentication for private repositories.

### Method
POST

### Endpoint
/github/codeql-action/init@v3

### Parameters
#### Request Body
- **queries** (string) - Required - Comma-separated list of queries, packs, or suites to run. Can include paths or built-in suites like `security-extended` or `security-and-quality`.
- **external-repository-token** (string) - Optional - A token to access queries stored in private repositories.

### Request Example
```yaml
- uses: github/codeql-action/init@v3
  with:
    queries: security-extended
    external-repository-token: "${{ secrets.ACCESS_TOKEN }}"
```

### Response
#### Success Response (200)
No specific response body is detailed for this action, it primarily configures the environment for subsequent steps.

#### Response Example
(No example provided)
```

--------------------------------

### Get Issue Comment - JavaScript Request Example

Source: https://docs.github.com/en/rest/issues/comments

This JavaScript example shows how to make a request to the GitHub API to get an issue comment using the Fetch API. It demonstrates setting the appropriate headers for authentication and accepting specific media types.

```javascript
async function getIssueComment(owner, repo, commentId, token) {
  const url = `https://api.github.com/repos/${owner}/${repo}/issues/comments/${commentId}`;
  const headers = {
    'Accept': 'application/vnd.github+json',
    'Authorization': `Bearer ${token}`,
    'X-GitHub-Api-Version': '2022-11-28'
  };

  try {
    const response = await fetch(url, {
      method: 'GET',
      headers: headers
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error fetching issue comment:', error);
    return null;
  }
}

// Example usage:
// const owner = 'OWNER';
// const repo = 'REPO';
// const commentId = 'COMMENT_ID';
// const token = '<YOUR-TOKEN>';
// getIssueComment(owner, repo, commentId, token).then(comment => {
//   if (comment) {
//     console.log(comment);
//   }
// });
```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=cli

An example endpoint to demonstrate making a request with custom headers using Octokit.js.

```APIDOC
## GET /octocat

### Description
An example endpoint to demonstrate making a request with custom headers.

### Method
GET

### Endpoint
`/octocat`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "headers": {
    "content-type": "text/plain",
    "X-GitHub-Api-Version": "2022-11-28"
  }
}
```

### Response
#### Success Response (200 OK)
- **message** (string) - A greeting message from the API.

#### Response Example
```json
{
  "message": "Hello from GitHub!"
}
```
```

--------------------------------

### Specify .NET Core SDK Version with setup-dotnet Action

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/xamarin-apps

The `setup-dotnet` action is used to install and configure a specific version of the .NET Core SDK on GitHub-hosted runners. This ensures consistent .NET environments across jobs and is the recommended approach for .NET development workflows.

```yaml
uses: actions/setup-dotnet@v4
with:
  dotnet-version: '5.0.x'

```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=curl

This endpoint is an example to demonstrate how to send custom headers with your requests.

```APIDOC
## GET /octocat

### Description
An example endpoint to demonstrate sending custom headers.

### Method
GET

### Endpoint
/octocat

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "headers": {
    "content-type": "text/plain",
    "X-GitHub-Api-Version": "2022-11-28"
  }
}
```

### Response
#### Success Response (200 OK)
- **message** (string) - A greeting message from Octocat.

#### Response Example
```json
{
  "message": "Hello from Octocat!"
}
```
```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

An example endpoint to demonstrate how to set custom headers for a request using Octokit.js.

```APIDOC
## GET /octocat

### Description
An example endpoint to demonstrate sending custom headers with a request.

### Method
GET

### Endpoint
`/octocat`

### Parameters
#### Query Parameters
None

#### Headers
- **content-type** (string) - Optional - The content type of the request.
- **X-GitHub-Api-Version** (string) - Optional - The GitHub API version to use.

### Request Example
```json
{
  "headers": {
    "content-type": "text/plain",
    "X-GitHub-Api-Version": "2022-11-28"
  }
}
```

### Response
#### Success Response (200 OK)
- **response** (object) - The response from the API.

#### Response Example
```json
{
  "data": {
    "message": "Hello from GitHub API!",
    "documentation_url": "https://docs.github.com/rest"
  }
}
```
```

--------------------------------

### Get a repository installation for the authenticated app

Source: https://docs.github.com/en/rest/apps/apps

Retrieves the installation information for a GitHub App on a specific repository.

```APIDOC
## GET /repos/{owner}/{repo}/installation

### Description
Retrieves the installation information for a GitHub App on a specific repository. This endpoint does not work with GitHub App user access tokens, GitHub App installation access tokens, or fine-grained personal access tokens.

### Method
GET

### Endpoint
`/repos/{owner}/{repo}/installation`

### Parameters
#### Path Parameters
- **owner** (string) - Required - The account owner of the repository. The name is not case sensitive.
- **repo** (string) - Required - The name of the repository without the `.git` extension. The name is not case sensitive.

#### Headers
- **Accept** (string) - Recommended: `application/vnd.github+json`
- **Authorization** (string) - Required: Bearer `<YOUR-TOKEN>`
- **X-GitHub-Api-Version** (string) - Required: `2022-11-28`

### Request Example
```json
{
  "example": "curl -L \
  -H \"Accept: application/vnd.github+json\" \
  -H \"Authorization: Bearer <YOUR-TOKEN>\" \
  -H \"X-GitHub-Api-Version: 2022-11-28\" \
  https://api.github.com/repos/OWNER/REPO/installation"
}
```

### Response
#### Success Response (200)
- **id** (integer) - The installation ID.
- **account** (object) - Information about the account the installation belongs to.
- **repository_selection** (string) - Indicates whether all repositories or a subset are selected.
- **access_tokens_url** (string) - URL to retrieve access tokens for the installation.
- **repositories_url** (string) - URL to retrieve repositories associated with the installation.
- **html_url** (string) - The URL to the installation settings page.
- **app_id** (integer) - The ID of the GitHub App.
- **client_id** (string) - The client ID of the GitHub App.
- **target_id** (integer) - The ID of the entity the installation is associated with (e.g., user or organization).
- **target_type** (string) - The type of the target entity (e.g., 'Organization', 'User').
- **permissions** (object) - The permissions granted to the app by this installation.
- **events** (array) - A list of events the app is subscribed to.
- **created_at** (string) - The date and time the installation was created.
- **updated_at** (string) - The date and time the installation was last updated.
- **single_file_name** (string) - The name of a single file if only one is configured.
- **has_multiple_single_files** (boolean) - Indicates if multiple single files are configured.
- **single_file_paths** (array) - A list of paths for single files if configured.
- **app_slug** (string) - The slug of the GitHub App.
- **suspended_at** (string|null) - The date and time the installation was suspended, or null.
- **suspended_by** (object|null) - Information about who suspended the installation, or null.

#### Response Example
```json
{
  "example": {
    "id": 1,
    "account": {
      "login": "github",
      "id": 1,
      "node_id": "MDEyOk9yZ2FuaXphdGlvbjE=",
      "avatar_url": "https://github.com/images/error/hubot_happy.gif",
      "gravatar_id": "",
      "url": "https://api.github.com/orgs/github",
      "html_url": "https://github.com/github",
      "followers_url": "https://api.github.com/users/github/followers",
      "following_url": "https://api.github.com/users/github/following{/other_user}",
      "gists_url": "https://api.github.com/users/github/gists{/gist_id}",
      "starred_url": "https://api.github.com/users/github/starred{/owner}{/repo}",
      "subscriptions_url": "https://api.github.com/users/github/subscriptions",
      "organizations_url": "https://api.github.com/users/github/orgs",
      "repos_url": "https://api.github.com/orgs/github/repos",
      "events_url": "https://api.github.com/orgs/github/events",
      "received_events_url": "https://api.github.com/users/github/received_events",
      "type": "Organization",
      "site_admin": false
    },
    "repository_selection": "all",
    "access_tokens_url": "https://api.github.com/app/installations/1/access_tokens",
    "repositories_url": "https://api.github.com/installation/repositories",
    "html_url": "https://github.com/organizations/github/settings/installations/1",
    "app_id": 1,
    "client_id": "Iv1.ab1112223334445c",
    "target_id": 1,
    "target_type": "Organization",
    "permissions": {
      "checks": "write",
      "metadata": "read",
      "contents": "read"
    },
    "events": [
      "push",
      "pull_request"
    ],
    "created_at": "2018-02-09T20:51:14Z",
    "updated_at": "2018-02-09T20:51:14Z",
    "single_file_name": "config.yml",
    "has_multiple_single_files": true,
    "single_file_paths": [
      "config.yml",
      ".github/issue_TEMPLATE.md"
    ],
    "app_slug": "github-actions",
    "suspended_at": null,
    "suspended_by": null
  }
}
```
```

--------------------------------

### Example `run_script_step` JSON Input

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

This JSON object demonstrates the arguments that can be passed to the `run_script_step` command within GitHub Actions. It includes optional parameters such as `entryPointArgs`, `entryPoint`, `environmentVariables`, and `prependPath`, along with the required `workingDirectory`. The `state` object contains details about the runner environment.

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

### Commit Workflow and Configuration Changes

Source: https://docs.github.com/en/packages/quickstart

This snippet demonstrates how to add the workflow and configuration files to Git, commit these changes with a descriptive message, and push them to the remote repository.

```bash
$ git add .github/workflows/release-package.yml
# Also add the file you created or edited in the previous step.
$ git add .npmrc or package.json
$ git commit -m "workflow to publish package"
$ git push
```

--------------------------------

### Clone GitHub Repository

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Clones a specified GitHub repository to your local machine. If run within a local Git repository's directory, it clones the remote repository.

```bash
gh repo clone OWNER/REPO

```

--------------------------------

### Initialize CodeQL Database (Shell)

Source: https://docs.github.com/en/code-security/codeql-cli/codeql-cli-manual/database-init

Creates an empty CodeQL database structure for a given source root and language(s). It prepares the database for subsequent extraction and analysis steps. Dependencies include the CodeQL CLI and potentially a GitHub PAT for automatic language detection.

```Shell
codeql database init --source-root=<dir> [--language=<lang>[,<lang>...]] [--github-auth-stdin] [--github-url=<url>] [--extractor-option=<extractor-option-name=value>] <options>... -- <database>
```

```Shell
codeql database init --source-root=<dir> [--language=<lang>[,<lang>...]] [--github-auth-stdin] [--github-url=<url>] [--extractor-option=<extractor-option-name=value>] <options>... -- <database>
```

--------------------------------

### GET /app/installations/{installation_id}/repositories

Source: https://docs.github.com/en/rest/apps/installations

Lists repositories that the authenticated user has explicit permission to access for a given installation. It includes the type of access granted for each repository.

```APIDOC
## GET /app/installations/{installation_id}/repositories

### Description
Lists repositories that the authenticated user has explicit permission to access for a given installation. The access level (read, write, admin) for each repository is included.

### Method
GET

### Endpoint
`/app/installations/{installation_id}/repositories`

### Parameters
#### Headers
- **accept** (string) - Required - Setting to `application/vnd.github+json` is recommended.

#### Path Parameters
- **installation_id** (integer) - Required - The unique identifier of the installation.

#### Query Parameters
- **per_page** (integer) - Optional - The number of results per page (max 100). Default: `30`
- **page** (integer) - Optional - The page number of the results to fetch. Default: `1`

### Request Example
```json
{
  "message": "Example request body not applicable for GET request."
}
```

### Response
#### Success Response (200)
- **total_count** (integer) - The total number of repositories.
- **installations** (array) - A list of installation objects, each containing:
  - **id** (integer) - The ID of the installation.
  - **account** (object) - Information about the account (user or organization).
  - **access_tokens_url** (string) - URL to access tokens for the installation.
  - **repositories_url** (string) - URL to fetch repositories for the installation.
  - **html_url** (string) - The HTML URL of the installation settings.
  - **app_id** (integer) - The ID of the associated application.
  - **target_id** (integer) - The ID of the target (user or organization).
  - **target_type** (string) - The type of the target (`User` or `Organization`).
  - **permissions** (object) - The permissions granted for this installation (e.g., `checks`, `metadata`, `contents`).
  - **events** (array) - A list of events the app is subscribed to.
  - **single_file_name** (string) - The name of a single file to be managed, if applicable.
  - **has_multiple_single_files** (boolean) - Indicates if multiple single files can be managed.
  - **single_file_paths** (array) - A list of paths for single files, if applicable.
  - **repository_selection** (string) - Indicates the repository selection strategy (`all`, `selected`).
  - **created_at** (string) - The timestamp when the installation was created.
  - **updated_at** (string) - The timestamp when the installation was last updated.
  - **app_slug** (string) - The slug of the associated application.
  - **suspended_at** (string|null) - The timestamp when the installation was suspended, if applicable.
  - **suspended_by** (string|null) - The user who suspended the installation, if applicable.

#### Response Example
```json
{
  "total_count": 2,
  "installations": [
    {
      "id": 1,
      "account": {
        "login": "octocat",
        "id": 1,
        "node_id": "MDQ6VXNlcjE=",
        "avatar_url": "https://github.com/images/error/octocat_happy.gif",
        "gravatar_id": "",
        "url": "https://api.github.com/users/octocat",
        "html_url": "https://github.com/octocat",
        "followers_url": "https://api.github.com/users/octocat/followers",
        "following_url": "https://api.github.com/users/octocat/following{/other_user}",
        "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
        "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
        "organizations_url": "https://api.github.com/users/octocat/orgs",
        "repos_url": "https://api.github.com/users/octocat/repos",
        "events_url": "https://api.github.com/users/octocat/events{/privacy}",
        "received_events_url": "https://api.github.com/users/octocat/received_events",
        "type": "User",
        "site_admin": false
      },
      "access_tokens_url": "https://api.github.com/app/installations/1/access_tokens",
      "repositories_url": "https://api.github.com/installation/repositories",
      "html_url": "https://github.com/organizations/github/settings/installations/1",
      "app_id": 1,
      "target_id": 1,
      "target_type": "Organization",
      "permissions": {
        "checks": "write",
        "metadata": "read",
        "contents": "read"
      },
      "events": [
        "push",
        "pull_request"
      ],
      "single_file_name": "config.yaml",
      "has_multiple_single_files": true,
      "single_file_paths": [
        "config.yml",
        ".github/issue_TEMPLATE.md"
      ],
      "repository_selection": "all",
      "created_at": "2017-07-08T16:18:44-04:00",
      "updated_at": "2017-07-08T16:18:44-04:00",
      "app_slug": "github-actions",
      "suspended_at": null,
      "suspended_by": null
    }
  ]
}
```
```

--------------------------------

### Verify 'bats' Version

Source: https://docs.github.com/en/actions/tutorials/create-an-example-workflow

Runs the 'bats' command with the '-v' flag to output the installed version of the 'bats' software. This step confirms that the installation was successful.

```yaml
      - run: bats -v
```

--------------------------------

### Configure and Start Node.js Server

Source: https://docs.github.com/en/webhooks/using-webhooks/configuring-your-server-to-receive-payloads

Defines the port for the Express server to listen on and starts the server. This code snippet assumes the `express` library has already been installed and the `app` object is initialized.

```javascript
const port = 3000;

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
```

--------------------------------

### Get Hourly Commit Count Request Example (JavaScript)

Source: https://docs.github.com/en/rest/metrics/statistics

This JavaScript example shows how to fetch the hourly commit count data for a repository. It uses the fetch API to make a GET request to the punch_card endpoint, including authentication and API version headers.

```javascript
async function getHourlyCommitCount(owner, repo, token) {
  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/stats/punch_card`, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}
```

--------------------------------

### Setup Single Specific Swift Version (YAML)

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/swift

This snippet demonstrates how to configure a job to use a single, specific version of Swift (e.g., "5.3.3"). It uses the `swift-actions/setup-swift` action to install the exact Swift version required and then runs a command to display the Swift version, confirming the setup. This is useful for ensuring consistent builds with a precise Swift environment.

```yaml
steps:
  - uses: swift-actions/setup-swift@65540b95f51493d65f5e59e97dcef9629ddf11bf
    with:
      swift-version: "5.3.3"
  - name: Get swift version
    run: swift --version # Swift 5.3.3

```

--------------------------------

### Get a repository installation for the authenticated app

Source: https://docs.github.com/en/rest/apps/apps

Fetches installation information for a specified repository, allowing authenticated GitHub Apps to determine installation details. Requires a JWT for authentication.

```APIDOC
## GET /repos/{owner}/{repo}/installation

### Description
Enables an authenticated GitHub App to find the repository's installation information. The installation's account type will be either an organization or a user account, depending which account the repository belongs to. You must use a JWT to access this endpoint.

### Method
GET

### Endpoint
`/repos/{owner}/{repo}/installation`

### Parameters
#### Path Parameters
- **owner** (string) - Required - The account owner of the repository. The name is not case sensitive.
- **repo** (string) - Required - The name of the repository.

#### Headers
- **Accept** (string) - Required - Setting to `application/vnd.github+json` is recommended.
- **Authorization** (string) - Required - Bearer token for authentication.
- **X-GitHub-Api-Version** (string) - Required - API version, e.g., `2022-11-28`.

### Request Example
```bash
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/installation
```

### Response
#### Success Response (200)
- **id** (integer) - The unique identifier of the installation.
- **account** (object) - Information about the account that owns the installation.
- **repository_selection** (string) - Indicates if all repositories or a subset are accessible.
- **access_tokens_url** (string) - URL to retrieve access tokens for the installation.
- **repositories_url** (string) - URL to list repositories accessible by the installation.
- **html_url** (string) - HTML URL for the installation settings.
- **app_id** (integer) - The ID of the GitHub App.
- **client_id** (string) - The client ID of the GitHub App.
- **target_id** (integer) - The ID of the target (organization or user).
- **target_type** (string) - The type of the target (`Organization` or `User`).
- **permissions** (object) - Permissions granted to the installation.
- **events** (array of strings) - Events the installation is subscribed to.
- **created_at** (string) - Timestamp when the installation was created.
- **updated_at** (string) - Timestamp when the installation was last updated.
- **single_file_name** (string) - If applicable, the name of a single file managed by the installation.
- **has_multiple_single_files** (boolean) - Indicates if multiple single files are managed.
- **single_file_paths** (array of strings) - Paths to single files managed by the installation.
- **app_slug** (string) - The slug of the GitHub App.
- **suspended_at** (string or null) - Timestamp if the installation is suspended.
- **suspended_by** (string or null) - User who suspended the installation.

#### Response Example
```json
{
  "id": 1,
  "account": {
    "login": "octocat",
    "id": 1,
    "node_id": "MDQ6VXNlcjE=",
    "avatar_url": "https://github.com/images/error/octocat_happy.gif",
    "gravatar_id": "",
    "url": "https://api.github.com/users/octocat",
    "html_url": "https://github.com/octocat",
    "followers_url": "https://api.github.com/users/octocat/followers",
    "following_url": "https://api.github.com/users/octocat/following{/other_user}",
    "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
    "organizations_url": "https://api.github.com/users/octocat/orgs",
    "repos_url": "https://api.github.com/users/octocat/repos",
    "events_url": "https://api.github.com/users/octocat/events{/privacy}",
    "received_events_url": "https://api.github.com/users/octocat/received_events",
    "type": "User",
    "site_admin": false
  },
  "repository_selection": "all",
  "access_tokens_url": "https://api.github.com/app/installations/1/access_tokens",
  "repositories_url": "https://api.github.com/installation/repositories",
  "html_url": "https://github.com/organizations/octocat/settings/installations/1",
  "app_id": 1,
  "client_id": "Iv1.ab1112223334445c",
  "target_id": 1,
  "target_type": "User",
  "permissions": {
    "metadata": "read",
    "contents": "read",
    "issues": "write",
    "single_file": "write"
  },
  "events": [
    "push",
    "pull_request"
  ],
  "created_at": "2017-07-08T16:18:44-04:00",
  "updated_at": "2017-07-08T16:18:44-04:00",
  "single_file_name": null,
  "has_multiple_single_files": false,
  "single_file_paths": [],
  "app_slug": "octoapp",
  "suspended_at": null,
  "suspended_by": null
}
```
```

--------------------------------

### Example devcontainer.json Configuration

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-java-project-for-codespaces

This is an example of a devcontainer.json file, a configuration file for development containers. It specifies the container image, features to install (like Java, Maven, Gradle, and Ant), and other settings. It uses JSON format and can be customized with various properties.

```json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/java
{
  "name": "Java",
  // Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
  "image": "mcr.microsoft.com/devcontainers/java:0-17",

  "features": {
    "ghcr.io/devcontainers/features/java:1": {
      "version": "none",
      "installMaven": "true",
      "installGradle": "false"
    },
    "ghcr.io/devcontainers-contrib/features/ant-sdkman:2": {}
  }

  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  // "forwardPorts": [],

  // Use 'postCreateCommand' to run commands after the container is created.
  // "postCreateCommand": "java -version",

  // Configure tool-specific properties.
  // "customizations": {},

  // Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
  // "remoteUser": "root"
}

```

--------------------------------

### Example Response for Get Deployment Status

Source: https://docs.github.com/en/rest/deployments/statuses

This is an example JSON response for the 'Get a deployment status' endpoint when the request is successful (HTTP status 200). It details various attributes of the deployment status, including its URL, ID, state, creator, description, environment, and timestamps.

```json
{
  "url": "https://api.github.com/repos/octocat/example/deployments/42/statuses/1",
  "id": 1,
  "node_id": "MDE2OkRlcGxveW1lbnRTdGF0dXMx",
  "state": "success",
  "creator": {
    "login": "octocat",
    "id": 1,
    "node_id": "MDQ6VXNlcjE=",
    "avatar_url": "https://github.com/images/error/octocat_happy.gif",
    "gravatar_id": "",
    "url": "https://api.github.com/users/octocat",
    "html_url": "https://github.com/octocat",
    "followers_url": "https://api.github.com/users/octocat/followers",
    "following_url": "https://api.github.com/users/octocat/following{/other_user}",
    "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
    "organizations_url": "https://api.github.com/users/octocat/orgs",
    "repos_url": "https://api.github.com/users/octocat/repos",
    "events_url": "https://api.github.com/users/octocat/events{/privacy}",
    "received_events_url": "https://api.github.com/users/octocat/received_events",
    "type": "User",
    "site_admin": false
  },
  "description": "Deployment finished successfully.",
  "environment": "production",
  "target_url": "https://example.com/deployment/42/output",
  "created_at": "2012-07-20T01:19:13Z",
  "updated_at": "2012-07-20T01:19:13Z",
  "deployment_url": "https://api.github.com/repos/octocat/example/deployments/42",
  "repository_url": "https://api.github.com/repos/octocat/example",
  "environment_url": "https://test-branch.lab.acme.com",
  "log_url": "https://example.com/deployment/42/output"
}
```

--------------------------------

### Creating Databases for Ruby

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Instructions for creating a CodeQL database for a Ruby project using the command line. No additional dependencies are required for Ruby.

```APIDOC
## POST /codeql database create (Ruby)

### Description
Creates a CodeQL database for a Ruby project.

### Method
POST

### Endpoint
/codeql database create

### Parameters
#### Query Parameters
- **language** (string) - Required - Must be set to `ruby`.
- **source-root** (string) - Optional - The path to the source code folder.
- **output-folder** (string) - Required - The folder where the database will be created.

### Request Example
```bash
codeql database create --language=ruby --source-root <folder-to-extract> <output-folder>/ruby-database
```

### Response
#### Success Response (200)
Indicates successful database creation.

#### Response Example
```json
{
  "status": "success",
  "message": "Ruby database created successfully."
}
```
```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

This endpoint retrieves information about the authenticated user (or a specific user if provided). It can also be used to demonstrate custom headers.

```APIDOC
## GET /octocat

### Description
Retrieves information about the authenticated user or demonstrates custom headers.

### Method
GET

### Endpoint
/octocat

### Parameters
#### Query Parameters
- **username** (string) - Optional - The username of the user to retrieve information for.

#### Headers
- **content-type** (string) - Optional - Custom content type header.
- **X-GitHub-Api-Version** (string) - Optional - Specifies the API version.

### Request Example
```json
{
  "headers": {
    "content-type": "text/plain",
    "X-GitHub-Api-Version": "2022-11-28"
  }
}
```

### Response
#### Success Response (200 OK)
- **data** (object) - User information.

#### Response Example
```json
{
  "login": "octocat",
  "id": 1,
  "node_id": "MDQ6VXNlcjE=",
  "avatar_url": "https://github.com/images/icons/icon- 80x80.png",
  "gravatar_id": "",
  "url": "https://api.github.com/users/octocat",
  "html_url": "https://github.com/octocat"
}
```
```

--------------------------------

### Using Octokit.js to Interact with GitHub REST API

Source: https://docs.github.com/en/rest/quickstart

This section explains how to use the Octokit.js library to make requests to the GitHub REST API from JavaScript scripts. It covers authentication, installation, and making requests.

```APIDOC
## Using Octokit.js to Interact with GitHub REST API

### Description
Octokit.js is a JavaScript library that allows you to interact with the GitHub REST API. This guide covers setting up Octokit, authenticating, and making requests.

### Method
Not Applicable (Library Usage)

### Endpoint
Not Applicable (Library Usage)

### Parameters
#### Authentication Token
- **Access Token** (string) - Required - A personal access token or GitHub App user access token with the necessary scopes/permissions for the API endpoint.

#### Octokit Initialization
- **auth** (string) - Required - The authentication token used to initialize the Octokit instance.

### Request Example (Initialization)
```javascript
import { Octokit } from "octokit";

const octokit = new Octokit({
  auth: 'YOUR-TOKEN'
});
```

### Request Example (API Call)
```javascript
await octokit.request("GET /repos/{owner}/{repo}/issues", {
  owner: "octocat",
  repo: "Spoon-Knife"
});
```

### Response
#### Success Response
- The response structure depends on the specific API endpoint called.

#### Response Example
(Refer to GitHub REST API documentation for specific endpoint responses)
```

--------------------------------

### SSH Key File Save Prompt (Windows Example)

Source: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent_platform=linux

Example prompt for saving the SSH key file on Windows. Pressing Enter accepts the default file location.

```text
> Enter a file in which to save the key (c:\Users\YOU\.ssh\id_ed25519_sk):[Press enter]
```

--------------------------------

### REST API Authentication Example

Source: https://docs.github.com/en/rest/authentication/authenticating-to-the-rest-api

This example demonstrates how to authenticate a GET request to the `/octocat` endpoint using a personal access token in the Authorization header.

```APIDOC
## GET /octocat

### Description
This endpoint retrieves information about the "octocat" entity. Authentication is required for full access and higher rate limits.

### Method
GET

### Endpoint
https://api.github.com/octocat

### Parameters

#### Header Parameters
- **Authorization** (string) - Required - Authentication token. Use `Bearer YOUR-TOKEN` or `token YOUR-TOKEN`.
- **X-GitHub-Api-Version** (string) - Required - Specifies the API version to use for the request.

### Request Example
```bash
curl --request GET \
  --url "https://api.github.com/octocat" \
  --header "Authorization: Bearer YOUR-TOKEN" \
  --header "X-GitHub-Api-Version: 2022-11-28"
```

### Response
#### Success Response (200)
- **data** (object) - Contains the response data for the request.

#### Response Example
```json
{
  "data": "..."
}
```

### Error Handling
- **401 Unauthorized**: Returned when credentials are invalid.
- **403 Forbidden**: Returned when the token has insufficient permissions or due to temporary lockout after repeated invalid credentials.
- **404 Not Found**: May be returned if authentication is missing or token has insufficient permissions.
```

--------------------------------

### Create Go CodeQL Database with Custom Build Script

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Creates a CodeQL database for a Go project using a custom build script. The build script path is provided as an argument to the `--command` option.

```bash
codeql database create go-database --language=go --command='./scripts/build.sh'
```

--------------------------------

### Run Post-Create Command for Package Installation

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-python-project-for-codespaces

This configuration adds a `postCreateCommand` to install Python packages listed in `requirements.txt`. This command runs automatically after the container is created, ensuring all necessary dependencies are installed.

```jsonc
// Use 'postCreateCommand' to run commands after the container is created.
"postCreateCommand": "pip3 install --user -r requirements.txt"
```

--------------------------------

### Authenticating as an Installation

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/building-ci-checks-with-a-github-app

This method initializes an Octokit client authenticated on behalf of a specific installation of a GitHub App. It uses a previously authenticated app client to create an installation access token, which is then used to initialize a new Octokit client for making API operations on behalf of that installation.

```APIDOC
## POST /authenticate/installation

### Description
Initializes an Octokit client authenticated as a specific installation of a GitHub App. This method uses the app client to generate an installation access token and then creates a new client using that token.

### Method
POST

### Endpoint
`/authenticate/installation`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
- **payload** (object) - Required - The webhook payload containing the installation details.
  - **installation** (object) - Required - The installation object from the webhook payload.
    - **id** (integer) - Required - The ID of the GitHub App installation.

### Request Example
```json
{
  "installation": {
    "id": 1234567
  }
}
```

### Response
#### Success Response (200)
- **client** (Octokit::Client) - An authenticated Octokit client instance for the installation.

#### Response Example
(Octokit::Client instance)
```json
{
  "message": "Successfully authenticated as GitHub App installation"
}
```
```

--------------------------------

### Example .env File Content for GitHub App

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/building-ci-checks-with-a-github-app

This example shows the structure of a `.env` file after populating it with actual GitHub App credentials. It includes the App ID, a webhook secret, and the full content of the private key, ensuring the private key is enclosed in double quotes.

```dotenv
GITHUB_APP_IDENTIFIER=12345
GITHUB_WEBHOOK_SECRET=your webhook secret
GITHUB_PRIVATE_KEY="-----BEGIN RSA PRIVATE KEY-----
...
HkVN9...
...
-----END RSA PRIVATE KEY-----"

```

--------------------------------

### GET /app/installation-requests

Source: https://docs.github.com/en/rest/apps/apps

Lists all pending installation requests for the authenticated GitHub App. This endpoint is useful for managing app installations and understanding pending requests.

```APIDOC
## GET /app/installation-requests

### Description
Lists all the pending installation requests for the authenticated GitHub App.

### Method
GET

### Endpoint
/app/installation-requests

### Parameters
#### Headers
- **accept** (string) - Required - Setting to `application/vnd.github+json` is recommended.
- **Authorization** (string) - Required - Your GitHub App token.
- **X-GitHub-Api-Version** (string) - Required - The API version to use, e.g., `2022-11-28`.

#### Query Parameters
- **per_page** (integer) - Optional - The number of results per page (max 100). Defaults to `30`.
- **page** (integer) - Optional - The page number of the results to fetch. Defaults to `1`.

### Request Example
```bash
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/app/installation-requests
```

### Response
#### Success Response (200)
- **installations** (array) - A list of installation requests.
  - **id** (integer) - The ID of the installation.
  - **slug** (string) - The slug of the app.
  - **node_id** (string) - The node ID of the installation.
  - **account** (object) - The account that the installation is associated with.
    - **login** (string) - The login name of the account.
    - **id** (integer) - The ID of the account.
    - **node_id** (string) - The node ID of the account.
    - **url** (string) - The URL of the account API endpoint.
    - **repos_url** (string) - The URL of the account's repositories API endpoint.
    - **events_url** (string) - The URL of the account's events API endpoint.
    - **avatar_url** (string) - The URL of the account's avatar.
    - **html_url** (string) - The HTML URL of the account.
    - **type** (string) - The type of the account (e.g., 'User', 'Organization').
  - **repository_selection** (string) - Indicates whether repositories were selected ('all' or 'selected').
  - **access_tokens_url** (string) - The URL to get access tokens for this installation.
  - **repositories_url** (string) - The URL to get repositories for this installation.
  - **html_url** (string) - The HTML URL for the installation.
  - **app_id** (integer) - The ID of the GitHub App.
  - **app_slug** (string) - The slug of the GitHub App.
  - **target_id** (integer) - The ID of the target account for the installation.
  - **target_type** (string) - The type of the target account ('User' or 'Organization').
  - **permissions** (object) - The permissions granted to the app for this installation.
  - **events** (array) - A list of events the app is subscribed to.
  - **created_at** (string) - The date and time the installation was created.
  - **updated_at** (string) - The date and time the installation was last updated.

#### Response Example
```json
{
  "id": 1,
  "slug": "octoapp",
  "node_id": "MDxOkludGVncmF0aW9uMQ==",
  "owner": {
    "login": "github",
    "id": 1,
    "node_id": "MDEyOk9yZ2FuaXphdGlvbjE=",
    "url": "https://api.github.com/orgs/github",
    "repos_url": "https://api.github.com/orgs/github/repos",
    "events_url": "https://api.github.com/orgs/github/events",
    "avatar_url": "https://github.com/images/error/octocat_happy.gif",
    "gravatar_id": "",
    "html_url": "https://github.com/octocat",
    "followers_url": "https://api.github.com/users/octocat/followers",
    "following_url": "https://api.github.com/users/octocat/following{/other_user}",
    "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
    "organizations_url": "https://api.github.com/users/octocat/orgs",
    "received_events_url": "https://api.github.com/users/octocat/received_events",
    "type": "User",
    "site_admin": true
  },
  "name": "Octocat App",
  "description": "",
  "external_url": "https://example.com",
  "html_url": "https://github.com/apps/octoapp",
  "created_at": "2017-07-08T16:18:44-04:00",
  "updated_at": "2017-07-08T16:18:44-04:00",
  "permissions": {
    "metadata": "read",
    "contents": "read",
    "issues": "write",
    "single_file": "write"
  },
  "events": [
    "push",
    "pull_request"
  ],
  "client_id": "Iv1.8a61f9b3a7aba766",
  "client_secret": "1726be1638095a19edd134c77bde3aa2ece1e5d8",
  "webhook_secret": "e340154128314309424b7c8e90325147d99fdafa",
  "pem": "-----BEGIN RSA PRIVATE KEY-----\nMIIEowIBAAKCAQEAuEPzOUE+kiEH1WLiMeBytTEF856j0hOVcSUSUkZxKvqczkWM\n9vo1gDyC7ZXhdH9fKh32aapba3RSsp4ke+giSmYTk2mGR538ShSDxh0OgpJmjiKP\nX0Bj4j5sFqfXuCtl9SkH4iueivv4R53ktqM+n6hk98l6hRwC39GVIblAh2lEM4L/\n6WvYwuQXPMM5OG2Ryh2tDZ1WS5RKfgq+9ksNJ5Q9UtqtqHkO+E63N5OK9sbzpUUm\noNaOl3udTlZD3A8iqwMPVxH4SxgATBPAc+bmjk6BMJ0qIzDcVGTrqrzUiywCTLma\nszdk8GjzXtPDmuBgNn+o6s02qVGpyydgEuqmTQIDAQABAoIBACL6AvkjQVVLn8kJ\ndBYznJJ4M8ECo+YEgaFwgAHODT0zRQCCgzd+Vxl4YwHmKV2Lr+y2s0drZt8GvYva\nKOK8NYYZyi15IlwFyRXmvvykF1UBpSXluYFDH7KaVroWMgRreHcIys5LqVSIb6Bo\ngDmK0yBLPp8qR29s2b7ScZRtLaqGJiX+j55rNzrZwxHkxFHyG9OG+u9IsBElcKCP\nkYCVE8ZdYexfnKOZbgn2kZB9qu0T/Mdvki8yk3I2bI6xYO24oQmhnT36qnqWoCBX\nNuCNsBQgpYZeZET8mEAUmo9d+ABmIHIvSs005agK8xRaP4+6jYgy6WwoejJRF5yd\nNBuF7aECgYEA50nZ4FiZYV0vcJDxFYeY3kYOvVuKn8OyW+2rg7JIQTremIjv8FkE\nZnwuF9ZRxgqLxUIfKKfzp/5l5LrycNoj2YKfHKnRejxRWXqG+ZETfxxlmlRns0QG\nJ4+BYL0CoanDSeA4fuyn4Bv7cy/03TDhfg/Uq0Aeg+hhcPE/vx3ebPsCgYEAy/Pv\neDLssOSdeyIxf0Brtocg6aPXIVaLdus+bXmLg77rJIFytAZmTTW8SkkSczWtucI3\nFI1I6sei/8FdPzAl62/JDdlf7Wd9K7JIotY4TzT7Tm7QU7xpfLLYIP1bOFjN81rk\n77oOD4LsXcosB/U6s1blPJMZ6AlO2EKs10UuR1cCgYBipzuJ2ADEaOz9RLWwi0AH\nPza2Sj+c2epQD9ZivD7Zo/Sid3ZwvGeGF13JyR7kLEdmAkgsHUdu1rI7mAolXMaB\n1pdrsHureeLxGbRM6za3tzMXWv1Il7FQWoPC8ZwXvMOR1VQDv4nzq7vbbA8z8c+c\n57+8tALQHOTDOgQIzwK61QKBgERGVc0EJy4Uag+VY8J4m1ZQKBluqo7TfP6DQ7O8\nM5MX73maB/7yAX8pVO39RjrhJlYACRZNMbK+v/ckEQYdJSSKmGCVe0JrGYDuPtic\nI9+IGfSorf7KHPoMmMN6bPYQ7Gjh7a++tgRFTMEc8956Hnt4xGahy9NcglNtBpVN\n6G8jAoGBAMCh028pdzJa/xeBHLLaVB2sc0Fe7993WlsPmnVE779dAz7qMscOtXJK\nfgtriltLSSD6rTA9hUAsL/X62rY0wdXuNdijjBb/qvrx7CAV6i37NK1CjABNjsfG\nZM372Ac6zc1EqSrid2IjET1YqyIW2KGLI1R2xbQc98UGlt48OdWu\n-----END RSA PRIVATE KEY-----"
}
```
```

--------------------------------

### Create Root Copilot Instructions File

Source: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions_tool=eclipse

This snippet shows how to create the main instructions file for GitHub Copilot at the root of a repository. This file, `.github/copilot-instructions.md`, allows for repository-wide custom instructions.

```bash
mkdir -p .github
cd .github
touch copilot-instructions.md
```

--------------------------------

### Generate copilot-instructions.md using Markdown Prompt

Source: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions_tool=webui

This prompt instructs the Copilot coding agent to create a `.github/copilot-instructions.md` file. The file should contain comprehensive information about the repository to enhance the agent's efficiency, including its purpose, high-level details, build and validation instructions, and project layout. It aims to reduce agent errors and the need for manual searching.

```markdown
Your task is to "onboard" this repository to Copilot coding agent by adding a .github/copilot-instructions.md file in the repository that contains information describing how a coding agent seeing it for the first time can work most efficiently.

You will do this task only one time per repository and doing a good job can SIGNIFICANTLY improve the quality of the agent's work, so take your time, think carefully, and search thoroughly before writing the instructions.

<Goals>
- Reduce the likelihood of a coding agent pull request getting rejected by the user due to
generating code that fails the continuous integration build, fails a validation pipeline, or
having misbehavior.
- Minimize bash command and build failures.
- Allow the agent to complete its task more quickly by minimizing the need for exploration using grep, find, str_replace_editor, and code search tools.
</Goals>

<Limitations>
- Instructions must be no longer than 2 pages.
- Instructions must not be task specific.
</Limitations>

<WhatToAdd>

Add the following high level details about the codebase to reduce the amount of searching the agent has to do to understand the codebase each time:
<HighLevelDetails>

- A summary of what the repository does.
- High level repository information, such as the size of the repo, the type of the project, the languages, frameworks, or target runtimes in use.
</HighLevelDetails>

Add information about how to build and validate changes so the agent does not need to search and find it each time.
<BuildInstructions>

- For each of bootstrap, build, test, run, lint, and any other scripted step, document the sequence of steps to take to run it successfully as well as the versions of any runtime or build tools used.
- Each command should be validated by running it to ensure that it works correctly as well as any preconditions and postconditions.
- Try cleaning the repo and environment and running commands in different orders and document errors and and misbehavior observed as well as any steps used to mitigate the problem.
- Run the tests and document the order of steps required to run the tests.
- Make a change to the codebase. Document any unexpected build issues as well as the workarounds.
- Document environment setup steps that seem optional but that you have validated are actually required.
- Document the time required for commands that failed due to timing out.
- When you find a sequence of commands that work for a particular purpose, document them in detail.
- Use language to indicate when something should always be done. For example: "always run npm install before building".
- Record any validation steps from documentation.
</BuildInstructions>

List key facts about the layout and architecture of the codebase to help the agent find where to make changes with minimal searching.
<ProjectLayout>

- A description of the major architectural elements of the project, including the relative paths to the main project files, the location
of configuration files for linting, compilation, testing, and preferences.
- A description of the checks run prior to check in, including any GitHub workflows, continuous integration builds, or other validation pipelines.
- Document the steps so that the agent can replicate these itself.
- Any explicit validation steps that the agent can consider to have further confidence in its changes.
- Dependencies that aren't obvious from the layout or file structure.
- Finally, fill in any remaining space with detailed lists of the following, in order of priority: the list of files in the repo root,
the contents of the README, the contents of any key source files, the list of files in the next level down of directories, giving priority to the more structurally important and snippets of code from key source files, such as the one containing the main method.
</ProjectLayout>
</WhatToAdd>

<StepsToFollow>
- Perform a comprehensive inventory of the codebase. Search for and view:
- README.md, CONTRIBUTING.md, and all other documentation files.
- Search the codebase for build steps and indications of workarounds like 'HACK', 'TODO', etc.
- All scripts, particularly those pertaining to build and repo or environment setup.
- All build and actions pipelines.
- All project files.
- All configuration and linting files.
- For each file:

```

--------------------------------

### Get a user installation for the authenticated app

Source: https://docs.github.com/en/rest/apps/apps

Retrieves the installation information for a GitHub App associated with a specific user account.

```APIDOC
## GET /users/{username}/installation

### Description
Enables an authenticated GitHub App to find the user’s installation information. You must use a JWT to access this endpoint. This endpoint does not work with GitHub App user access tokens, GitHub App installation access tokens, or fine-grained personal access tokens.

### Method
GET

### Endpoint
`/users/{username}/installation`

### Parameters
#### Path Parameters
- **username** (string) - Required - The handle for the GitHub user account.

#### Headers
- **Accept** (string) - Recommended: `application/vnd.github+json`
- **Authorization** (string) - Required: Bearer `<YOUR-TOKEN>`
- **X-GitHub-Api-Version** (string) - Required: `2022-11-28`

### Request Example
```json
{
  "example": "curl -L \
  -H \"Accept: application/vnd.github+json\" \
  -H \"Authorization: Bearer <YOUR-TOKEN>\" \
  -H \"X-GitHub-Api-Version: 2022-11-28\" \
  https://api.github.com/users/USERNAME/installation"
}
```

### Response
#### Success Response (200)
- **id** (integer) - The installation ID.
- **account** (object) - Information about the user account the installation belongs to.
- **repository_selection** (string) - Indicates whether all repositories or a subset are selected.
- **access_tokens_url** (string) - URL to retrieve access tokens for the installation.
- **repositories_url** (string) - URL to retrieve repositories associated with the installation.
- **html_url** (string) - The URL to the installation settings page.
- **app_id** (integer) - The ID of the GitHub App.
- **client_id** (string) - The client ID of the GitHub App.
- **target_id** (integer) - The ID of the user.
- **target_type** (string) - The type of the target entity ('User').
- **permissions** (object) - The permissions granted to the app by this installation.
- **events** (array) - A list of events the app is subscribed to.
- **created_at** (string) - The date and time the installation was created.
- **updated_at** (string) - The date and time the installation was last updated.
- **single_file_name** (string) - The name of a single file if only one is configured.
- **has_multiple_single_files** (boolean) - Indicates if multiple single files are configured.
- **single_file_paths** (array) - A list of paths for single files if configured.
- **app_slug** (string) - The slug of the GitHub App.
- **suspended_at** (string|null) - The date and time the installation was suspended, or null.
- **suspended_by** (object|null) - Information about who suspended the installation, or null.

#### Response Example
```json
{
  "example": {
    "id": 1,
    "account": {
      "login": "octocat",
      "id": 1,
      "node_id": "MDQ6VXNlcjE=",
      "avatar_url": "https://github.com/images/error/octocat_happy.gif",
      "gravatar_id": "",
      "url": "https://api.github.com/users/octocat",
      "html_url": "https://github.com/octocat",
      "followers_url": "https://api.github.com/users/octocat/followers",
      "following_url": "https://api.github.com/users/octocat/following{/other_user}",
      "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
      "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
      "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
      "organizations_url": "https://api.github.com/users/octocat/orgs",
      "repos_url": "https://api.github.com/users/octocat/repos",
      "events_url": "https://api.github.com/users/octocat/events{/privacy}",
      "received_events_url": "https://api.github.com/users/octocat/received_events",
      "type": "User",
      "site_admin": false
    },
    "repository_selection": "all",
    "access_tokens_url": "https://api.github.com/app/installations/1/access_tokens",
    "repositories_url": "https://api.github.com/installation/repositories",
    "html_url": "https://github.com/settings/installations/1",
    "app_id": 1,
    "client_id": "Iv1.ab1112223334445c",
    "target_id": 1,
    "target_type": "User",
    "permissions": {
      "checks": "write",
      "metadata": "read",
      "contents": "read"
    },
    "events": [
      "push",
      "pull_request"
    ],
    "created_at": "2018-02-09T20:51:14Z",
    "updated_at": "2018-02-09T20:51:14Z",
    "single_file_name": null,
    "has_multiple_single_files": false,
    "single_file_paths": [],
    "app_slug": "github-actions",
    "suspended_at": null,
    "suspended_by": null
  }
}
```
```

--------------------------------

### Introspection Query: Get Specific Type Details

Source: https://docs.github.com/en/graphql/guides/introduction-to-graphql

This example shows how to query the `__type` to get specific details about a named type, such as 'Repository'.

```APIDOC
## Query __type

### Description
Retrieves detailed information about a specific type within the GraphQL schema.

### Method
POST

### Endpoint
https://api.github.com/graphql

### Parameters
#### Request Body
- **query** (string) - Required - The GraphQL query string.

### Request Example
```json
{
  "query": "query { __type(name: \"Repository\") { name kind description fields { name } } }"
}
```

### Response
#### Success Response (200)
- **data** (object) - The response data containing type information.
  - **__type** (object) - Information about the requested type.
    - **name** (string) - The name of the type.
    - **kind** (string) - The kind of the type.
    - **description** (string) - A description of the type.
    - **fields** (array) - An array of field objects.
      - **name** (string) - The name of the field.

#### Response Example
```json
{
  "data": {
    "__type": {
      "name": "Repository",
      "kind": "OBJECT",
      "description": "A repository.",
      "fields": [
        {
          "name": "id"
        },
        {
          "name": "name"
        }
      ]
    }
  }
}
```
```

--------------------------------

### List Environments using JavaScript

Source: https://docs.github.com/en/rest/deployments/environments

Example of how to list environments for a repository using JavaScript with the Fetch API. This demonstrates making a GET request with necessary headers for authentication and API versioning.

```javascript
async function listEnvironments(owner, repo, token) {
  const url = `https://api.github.com/repos/${owner}/${repo}/environments`;
  const headers = {
    "Accept": "application/vnd.github+json",
    "Authorization": `Bearer ${token}`,
    "X-GitHub-Api-Version": "2022-11-28"
  };

  try {
    const response = await fetch(url, {
      method: "GET",
      headers: headers
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    console.log(data);
    return data;
  } catch (error) {
    console.error("Error listing environments:", error);
  }
}

// Example usage:
// const owner = "OWNER";
// const repo = "REPO";
// const token = "<YOUR-TOKEN>";
// listEnvironments(owner, repo, token);
```

--------------------------------

### Building and Testing Go Code with GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

Demonstrates a basic GitHub Actions workflow for Go projects. It checks out the code, sets up the Go environment, installs dependencies using `go get`, builds the project with `go build`, and runs tests with `go test`.

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

### Get workflow run attempt example (JavaScript)

Source: https://docs.github.com/en/rest/actions/workflow-runs_apiversion=2022-11-28

Example of how to retrieve a specific workflow run attempt using JavaScript with the GitHub API. This code snippet demonstrates making an authenticated GET request to the appropriate endpoint. Ensure you replace placeholders with actual values.

```javascript
// JavaScript example for getting a workflow run attempt
async function getWorkflowRunAttempt(owner, repo, runId, attemptNumber, token) {
  const url = `https://api.github.com/repos/${owner}/${repo}/actions/runs/${runId}/attempts/${attemptNumber}`;
  const response = await fetch(url, {
    method: 'GET',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}

// Example usage:
// const owner = 'OWNER';
// const repo = 'REPO';
// const runId = 1234567890;
// const attemptNumber = 1;
// const token = '<YOUR-TOKEN>';
// getWorkflowRunAttempt(owner, repo, runId, attemptNumber, token)
//   .then(data => console.log(data))
//   .catch(error => console.error('Error:', error));
```

--------------------------------

### Start Smee.io Proxy for Webhooks

Source: https://docs.github.com/en/apps/creating-github-apps/guides/building-a-github-app-that-responds-to-webhook-events

This command starts a local server using Smee.io to forward GitHub webhooks to your development environment. It requires a webhook proxy URL and specifies the local endpoint for receiving events. Ensure your server is running on the specified port.

```bash
npx smee -u WEBHOOK_PROXY_URL -t http://localhost:3000/api/webhook
```

--------------------------------

### Get Deployment Details (JavaScript)

Source: https://docs.github.com/en/rest/deployments/deployments

Retrieves details for a specific deployment using JavaScript. This example demonstrates how to make the API call with appropriate headers and parameters. Ensure you replace placeholders with actual values.

```javascript
async function getDeployment(owner, repo, deploymentId) {
  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/deployments/${deploymentId}`, {
    method: 'GET',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': 'Bearer <YOUR-TOKEN>',
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}

// Example usage:
// getDeployment('OWNER', 'REPO', 'DEPLOYMENT_ID').then(data => console.log(data));
```

--------------------------------

### Install GitHub Copilot in Vim/Neovim (macOS/Linux)

Source: https://docs.github.com/en/copilot/managing-copilot/configure-personal-settings/installing-the-github-copilot-extension-in-your-environment

Clones the GitHub Copilot Vim plugin into the Neovim or Vim start directory for macOS and Linux systems. This enables AI-powered coding suggestions within the editor.

```shell
git clone https://github.com/github/copilot.vim \
~/.config/nvim/pack/github/start/copilot.vim
```

```shell
git clone https://github.com/github/copilot.vim \
~/.vim/pack/github/start/copilot.vim
```

--------------------------------

### Create CodeQL Database (Basic)

Source: https://docs.github.com/en/code-security/codeql-cli/using-the-codeql-cli/creating-codeql-databases

This command creates a CodeQL database for a specified language. It requires a path for the new database and a language identifier. The database directory will be created automatically.

```bash
codeql database create <database> --language=<language-identifier>
```

--------------------------------

### GET /events (with query parameters)

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

This endpoint lists public events. It shows how to use query parameters like `per_page` and `page` to paginate results.

```APIDOC
## GET /events

### Description
Lists public events. This example demonstrates how to use query parameters to control the number of results per page and the page number.

### Method
GET

### Endpoint
https://api.github.com/events

### Parameters
#### Query Parameters
- **per_page** (integer) - Optional - The number of results to return per page. Defaults to 30.
- **page** (integer) - Optional - The page number of the results to fetch.

#### Headers
- **Accept** (string) - Required - The media type for the request, e.g., `application/vnd.github+json`.
- **X-GitHub-Api-Version** (string) - Required - The version of the GitHub API to use, e.g., `2022-11-28`.

### Request Example
```shell
curl --request GET \
--url "https://api.github.com/events?per_page=2&page=1" \
--header "Accept: application/vnd.github+json" \
--header "X-GitHub-Api-Version: 2022-11-28"
```

### Response
#### Success Response (200)
- **events** (array) - An array of public event objects.

#### Response Example
```json
{
  "events": [
    {
      "example": "event object"
    }
  ]
}
```
```

--------------------------------

### Install 'bats' Package with npm

Source: https://docs.github.com/en/actions/tutorials/create-an-example-workflow

Executes an npm command to globally install the 'bats' software testing package on the runner. This makes the 'bats' command available for use in later steps.

```yaml
      - run: npm install -g bats
```

--------------------------------

### Get SSH Signing Key Example Response

Source: https://docs.github.com/en/rest/users/ssh-signing-keys

An example of a successful HTTP 200 response when retrieving details for an SSH signing key.

```json
{ "key": "2Sg8iYjAxxmI2LvUXpJjkYrMxURPc8r+dB7TJyvv1234", "id": 2, "url": "https://api.github.com/user/keys/2", "title": "ssh-rsa AAAAB3NzaC1yc2EAAA", "created_at": "2020-06-11T21:31:57Z" }
```

--------------------------------

### Download CodeQL Packs from GitHub Enterprise Server

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

This example shows how to configure the CodeQL action to download query packs from a GitHub Enterprise Server (GHE) instance. It utilizes the `registries` input to specify the GHE registry URL, package patterns, and a secret token for authentication. It also includes an example for the default GitHub Container Registry.

```yaml
- uses: github/codeql-action/init@v3
  with:
    registries: |
      # URL to the container registry, usually in this format
      - url: https://containers.GHEHOSTNAME1/v2/

        # List of package glob patterns to be found at this registry
        packages:
          - my-company/*
          - my-company2/*

        # Token, which should be stored as a secret
        token: ${{ secrets.GHEHOSTNAME1_TOKEN }}

      # URL to the default container registry
      - url: https://ghcr.io/v2/
        # Packages can also be a string
        packages: "*/*"
        token: ${{ secrets.GHCR_TOKEN }}


```

--------------------------------

### Authenticate Installation with Access Token using Octokit.rb

Source: https://docs.github.com/en/apps/creating-github-apps/guides/creating-ci-tests-with-the-checks-api

Initializes an Octokit client authenticated as a specific installation of a GitHub App. This method takes a payload object, extracts the installation ID from it, and then uses the app client to create an installation access token. The new client is then initialized with this installation-specific token, enabling API operations on behalf of that installation. Dependencies include a pre-initialized app client and the Octokit.rb library.

```ruby
def authenticate_installation(payload)
  installation_id = payload['installation']['id']
  installation_token = @app_client.create_app_installation_access_token(installation_id)[:token]
  @installation_client = Octokit::Client.new(bearer_token: installation_token)
end

```

--------------------------------

### Create and Start HTTP Server

Source: https://docs.github.com/en/apps/creating-github-apps/guides/building-a-github-app-that-responds-to-webhook-events

Creates an HTTP server using Node.js's http module and starts it listening on the specified port. The server uses the previously defined middleware to handle incoming webhook requests and logs a message indicating it is listening.

```javascript
import http from "http";

http.createServer(middleware).listen(port, () => {
  console.log(`Server is listening for events at: ${localWebhookUrl}`);
  console.log('Press Ctrl + C to quit.')
});
```

--------------------------------

### GET /orgs/{org}/installations

Source: https://docs.github.com/en/rest/orgs/orgs

Lists all GitHub Apps installed in an organization. The installation count includes all GitHub Apps installed on repositories in the organization. The authenticated user must be an organization owner to use this endpoint.

```APIDOC
## GET /orgs/{org}/installations

### Description
Lists all GitHub Apps installed in an organization. The installation count includes all GitHub Apps installed on repositories in the organization. The authenticated user must be an organization owner to use this endpoint.

### Method
GET

### Endpoint
`/orgs/{org}/installations`

### Parameters
#### Path Parameters
- **org** (string) - Required - The organization name. The name is not case sensitive.

#### Query Parameters
- **per_page** (integer) - Optional - The number of results per page (max 100). Defaults to `30`.
- **page** (integer) - Optional - The page number of the results to fetch. Defaults to `1`.

#### Headers
- **accept** (string) - Recommended: `application/vnd.github+json`
- **Authorization** (string) - Required: Bearer <YOUR-TOKEN>
- **X-GitHub-Api-Version** (string) - Required: `2022-11-28`

### Request Example
```json
{
  "example": "curl -L \n  -H \"Accept: application/vnd.github+json\" \n  -H \"Authorization: Bearer <YOUR-TOKEN>\" \n  -H \"X-GitHub-Api-Version: 2022-11-28\" \n  https://api.github.com/orgs/ORG/installations"
}
```

### Response
#### Success Response (200)
- **total_count** (integer) - The total number of installations.
- **installations** (array) - A list of installation objects.
  - **id** (integer) - The ID of the installation.
  - **account** (object) - The account associated with the installation.
    - **login** (string) - The login name of the account.
    - **id** (integer) - The ID of the account.
    - **node_id** (string)
    - **avatar_url** (string)
    - **gravatar_id** (string)
    - **url** (string)
    - **html_url** (string)
    - **followers_url** (string)
    - **following_url** (string)
    - **gists_url** (string)
    - **starred_url** (string)
    - **subscriptions_url** (string)
    - **organizations_url** (string)
    - **repos_url** (string)
    - **events_url** (string)
    - **received_events_url** (string)
    - **type** (string)
    - **site_admin** (boolean)
  - **repository_selection** (string) - Indicates whether repositories are selected or all are included.
  - **access_tokens_url** (string) - URL to access tokens for the installation.
  - **repositories_url** (string) - URL to repositories for the installation.
  - **html_url** (string) - HTML URL for the installation settings.
  - **app_id** (integer) - The ID of the GitHub App.
  - **target_id** (integer) - The ID of the target (organization or user).
  - **target_type** (string) - The type of the target (e.g., 'Organization').
  - **permissions** (object) - Permissions granted to the installation.
    - **deployments** (string)
    - **metadata** (string)
    - **pull_requests** (string)
    - **statuses** (string)
  - **events** (array) - Events subscribed to by the installation.
  - **created_at** (string) - Timestamp of creation.
  - **updated_at** (string) - Timestamp of last update.
  - **single_file_name** (string) - Name of a single file managed by the installation.
  - **has_multiple_single_files** (boolean) - Indicates if multiple single files are managed.
  - **single_file_paths** (array) - Paths of single files managed by the installation.
  - **app_slug** (string) - The slug of the GitHub App.
  - **suspended_at** (string/null) - Timestamp of suspension, or null if not suspended.
  - **suspended_by** (string/null) - User who suspended the installation, or null if not suspended.

#### Response Example
```json
{
  "total_count": 1,
  "installations": [
    {
      "id": 25381,
      "account": {
        "login": "octo-org",
        "id": 6811672,
        "node_id": "MDEyOk9yZ2FuaXphdGlvbjY4MTE2NzI=",
        "avatar_url": "https://avatars3.githubusercontent.com/u/6811672?v=4",
        "gravatar_id": "",
        "url": "https://api.github.com/users/octo-org",
        "html_url": "https://github.com/octo-org",
        "followers_url": "https://api.github.com/users/octo-org/followers",
        "following_url": "https://api.github.com/users/octo-org/following{/other_user}",
        "gists_url": "https://api.github.com/users/octo-org/gists{/gist_id}",
        "starred_url": "https://api.github.com/users/octo-org/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/octo-org/subscriptions",
        "organizations_url": "https://api.github.com/users/octo-org/orgs",
        "repos_url": "https://api.github.com/users/octo-org/repos",
        "events_url": "https://api.github.com/users/octo-org/events{/privacy}",
        "received_events_url": "https://api.github.com/users/octo-org/received_events",
        "type": "Organization",
        "site_admin": false
      },
      "repository_selection": "selected",
      "access_tokens_url": "https://api.github.com/app/installations/25381/access_tokens",
      "repositories_url": "https://api.github.com/installation/repositories",
      "html_url": "https://github.com/organizations/octo-org/settings/installations/25381",
      "app_id": 2218,
      "target_id": 6811672,
      "target_type": "Organization",
      "permissions": {
        "deployments": "write",
        "metadata": "read",
        "pull_requests": "read",
        "statuses": "read"
      },
      "events": [
        "deployment",
        "deployment_status"
      ],
      "created_at": "2017-05-16T08:47:09.000-07:00",
      "updated_at": "2017-06-06T11:23:23.000-07:00",
      "single_file_name": "config.yml",
      "has_multiple_single_files": true,
      "single_file_paths": [
        "config.yml",
        ".github/issue_TEMPLATE.md"
      ],
      "app_slug": "github-actions",
      "suspended_at": null,
      "suspended_by": null
    }
  ]
}
```
```

--------------------------------

### Downloading CodeQL Databases from GitHub.com

Source: https://docs.github.com/en/code-security/codeql-cli/using-the-advanced-functionality-of-the-codeql-cli/advanced-setup-of-the-codeql-cli

Instructions and API examples for checking the availability of CodeQL databases for a repository and downloading them.

```APIDOC
## Downloading CodeQL Databases from GitHub.com

### Description
This section describes how to use the GitHub REST API to check for and download CodeQL databases for repositories.

### Checking for Available CodeQL Databases
To check if a repository has CodeQL databases available, use the `/repos/<owner>/<repo>/code-scanning/codeql/databases` endpoint.

#### Example using GitHub CLI:
```
gh api /repos/<owner>/<repo>/code-scanning/codeql/databases
```

This command returns information about available CodeQL databases, including language and last updated time. An empty response indicates no databases are available.

### Downloading a CodeQL Database
Once you've confirmed a database exists, you can download it using the following command, replacing `<language>` with the desired language (e.g., `java`, `python`).

#### Example using GitHub CLI:
```
gh api /repos/<owner>/<repo>/code-scanning/codeql/databases/<language> -H 'Accept: application/zip' > path/to/local/database.zip
```

**Note:** After downloading, you must unzip the databases before running an analysis with the CodeQL CLI.
```

--------------------------------

### Start Local Development Server

Source: https://docs.github.com/en/contributing/setting-up-your-environment-to-work-on-github-docs/troubleshooting-your-environment

This command launches the local development server for the GitHub Docs project. It's essential for testing changes locally and debugging staging issues by allowing you to preview the site on 'https://localhost:4000'.

```shell
npm start
```

--------------------------------

### Example Deployment Response (JSON)

Source: https://docs.github.com/en/rest/deployments/deployments

An example of a successful response (Status: 201 Created) when creating a deployment via the GitHub API. This JSON object contains details about the created deployment, including its ID, SHA, ref, and associated metadata.

```json
{ "url": "https://api.github.com/repos/octocat/example/deployments/1", "id": 1, "node_id": "MDEwOkRlcGxveW1lbnQx", "sha": "a84d88e7554fc1fa21bcbc4efae3c782a70d2b9d", "ref": "topic-branch", "task": "deploy", "payload": {}, "original_environment": "staging", "environment": "production", "description": "Deploy request from hubot", "creator": { "login": "octocat", "id": 1, "node_id": "MDQ6VXNlcjE=", "avatar_url": "https://github.com/images/error/octocat_happy.gif", "gravatar_id": "", "url": "https://api.github.com/users/octocat", "html_url": "https://github.com/octocat", "followers_url": "https://api.github.com/users/octocat/followers", "following_url": "https://api.github.com/users/octocat/following{/other_user}", "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}", "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}", "subscriptions_url": "https://api.github.com/users/octocat/subscriptions", "organizations_url": "https://api.github.com/users/octocat/orgs", "repos_url": "https://api.github.com/users/octocat/repos", "events_url": "https://api.github.com/users/octocat/events{/privacy}", "received_events_url": "https://api.github.com/users/octocat/received_events", "type": "User", "site_admin": false }, "created_at": "2012-07-20T01:19:13Z", "updated_at": "2012-07-20T01:19:13Z", "statuses_url": "https://api.github.com/repos/octocat/example/deployments/1/statuses", "repository_url": "https://api.github.com/repos/octocat/example", "transient_environment": false, "production_environment": true }
```

--------------------------------

### Initializing Git Repository and Creating GitHub Release Assets

Source: https://docs.github.com/en/github-cli/github-cli/creating-github-cli-extensions

This set of commands demonstrates initializing a Git repository, creating a `.gitignore` file to exclude build artifacts, committing initial source files, and creating a GitHub release. It includes cross-compiling the Go extension for different operating systems and architectures (Windows, Linux, macOS) and then uploading these compiled binaries as assets to a newly created Git tag and release.

```bash
git init -b main
echo "gh-EXTENSION-NAME" >> .gitignore
git add main.go go.* .gitignore && git commit -m 'Initial commit'
gh repo create "gh-EXTENSION-NAME"
git tag v1.0.0
git push origin v1.0.0
GOOS=windows GOARCH=amd64 go build -o gh-EXTENSION-NAME-windows-amd64.exe
GOOS=linux GOARCH=amd64 go build -o gh-EXTENSION-NAME-linux-amd64
GOOS=darwin GOARCH=amd64 go build -o gh-EXTENSION-NAME-darwin-amd64
gh release create v1.0.0 ./*amd64*

```

--------------------------------

### List Installations for Authenticated App (cURL)

Source: https://docs.github.com/en/rest/apps/apps

Example of how to list installations for an authenticated GitHub App using cURL. It requires an Authorization header with a token and specifies the API version and accept header.

```bash
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/app/installations
```

--------------------------------

### Get File Content (Example Response)

Source: https://docs.github.com/en/rest/repos/contents

This JSON object represents an example response when retrieving file content from a GitHub repository. It includes details such as file type, encoding, size, name, path, and the base64 encoded content. Other metadata like SHA, URL, and links are also provided.

```json
{ "type": "file", "encoding": "base64", "size": 5362, "name": "README.md", "path": "README.md", "content": "encoded content ...", "sha": "3d21ec53a331a6f037a91c368710b99387d012c1", "url": "https://api.github.com/repos/octokit/octokit.rb/contents/README.md", "git_url": "https://api.github.com/repos/octokit/octokit.rb/git/blobs/3d21ec53a331a6f037a91c368710b99387d012c1", "html_url": "https://github.com/octokit/octokit.rb/blob/master/README.md", "download_url": "https://raw.githubusercontent.com/octokit/octokit.rb/master/README.md", "_links": { "git": "https://api.github.com/repos/octokit/octokit.rb/git/blobs/3d21ec53a331a6f037a91c368710b99387d012c1", "self": "https://api.github.com/repos/octokit/octokit.rb/contents/README.md", "html": "https://github.com/octokit/octokit.rb/blob/master/README.md" } }
```

--------------------------------

### Create Repository-Wide Copilot Instructions

Source: https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot

This snippet shows how to create a repository-wide custom instructions file for GitHub Copilot. Instructions are placed in `.github/copilot-instructions.md` and are written in Markdown format.

```markdown
## Creating repository-wide custom instructions
  1. In the root of your repository, create a file named `.github/copilot-instructions.md`.
Create the `.github` directory if it does not already exist.
  2. Add natural language instructions to the file, in Markdown format.
Whitespace between instructions is ignored, so the instructions can be written as a single paragraph, each on a new line, or separated by blank lines for legibility.
```

--------------------------------

### Get Repository README - GitHub CLI

Source: https://docs.github.com/en/rest/repos/contents

Example command using the GitHub CLI to retrieve a repository's README file. This command leverages existing authentication configured with the CLI.

```bash
gh api repos/OWNER/REPO/readme \
  --header 'Accept: application/vnd.github+json' \
  --header 'X-GitHub-Api-Version: 2022-11-28'
```

--------------------------------

### Set up tracing environment variables for CodeQL

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Sets up the necessary environment variables for CodeQL to trace build commands. This can be done by sourcing a script or by processing a JSON file containing the variables, depending on the CI system's capabilities. The example shows how to integrate this with Azure DevOps.

```bash
# Example using shell script (Linux/macOS)
source <database>/temp/tracingEnvironment/start-tracing.sh

# Example for Azure DevOps using JSON output
# Assuming 'start-tracing.json' contains JSON output of environment variables
# jq -r '. | to_entries[] | "##vso[task.setvariable variable=\( .key \)]\(.value)"' <database>/temp/tracingEnvironment/start-tracing.json
```

```powershell
# Example using PowerShell script (Windows)
. <database>\temp\tracingEnvironment\start-tracing.ps1
```

```batch
// Example using batch script (Windows)
CALL <database>\temp\tracingEnvironment\start-tracing.bat
```

--------------------------------

### Get Git Tag Request Example

Source: https://docs.github.com/en/rest/git/tags

Example of how to retrieve a specific Git tag using the GitHub API. This snippet shows the cURL command with required headers and the API endpoint, including placeholders for owner, repository, and tag SHA.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/git/tags/TAG_SHA
```

```javascript
const owner = "OWNER";
const repo = "REPO";
const tagSha = "TAG_SHA";

fetch(`https://api.github.com/repos/${owner}/${repo}/git/tags/${tagSha}`, {
  method: "GET",
  headers: {
    "Accept": "application/vnd.github+json",
    "Authorization": "Bearer <YOUR-TOKEN>",
    "X-GitHub-Api-Version": "2022-11-28"
  }
})
.then(response => response.json())
.then(data => console.log(data));
```

--------------------------------

### Example GitHub App Registration URL with Query Parameters

Source: https://docs.github.com/en/apps/creating-github-apps/setting-up-a-github-app/creating-a-github-app-using-url-parameters

This example demonstrates how to construct a URL to register a new GitHub App with pre-configured settings. It includes parameters for the app name, description, callback URL, OAuth request, public status, permissions, webhook activation, and subscribed events. Users can still edit these values on the registration page before submitting.

```url
https://github.com/settings/apps/new?name=octocat-github-app&description=An%20Octocat%20App&callback_urls[]=https://example.com&request_oauth_on_install=true&public=true&checks=write&webhook_active=true&events[]=check_run&events[]=check_suite
```

--------------------------------

### Get Commit Object Response Example (JSON)

Source: https://docs.github.com/en/rest/git/commits

Example JSON response for a successfully retrieved Git commit object. It includes details like SHA, author, committer, message, and verification status.

```json
{ "sha": "7638417db6d59f3c431d3e1f261cc637155684cd", "node_id": "MDY6Q29tbWl0NzYzODQxN2RiNmQ1OWYzYzQzMWQzZTFmMjYxY2M2MzcxNTU2ODRjZA==", "url": "https://api.github.com/repos/octocat/Hello-World/git/commits/7638417db6d59f3c431d3e1f261cc637155684cd", "author": { "date": "2014-11-07T22:01:45Z", "name": "Monalisa Octocat", "email": "octocat@github.com" }, "committer": { "date": "2014-11-07T22:01:45Z", "name": "Monalisa Octocat", "email": "octocat@github.com" }, "message": "my commit message", "tree": { "url": "https://api.github.com/repos/octocat/Hello-World/git/trees/827efc6d56897b048c772eb4087f854f46256132", "sha": "827efc6d56897b048c772eb4087f854f46256132" }, "parents": [ { "url": "https://api.github.com/repos/octocat/Hello-World/git/commits/7d1b31e74ee336d15cbd21741bc88a537ed063a0", "sha": "7d1b31e74ee336d15cbd21741bc88a537ed063a0", "html_url": "https://github.com/octocat/Hello-World/commit/7d1b31e74ee336d15cbd21741bc88a537ed063a0" } ], "verification": { "verified": false, "reason": "unsigned", "signature": null, "payload": null, "verified_at": null }, "html_url": "https://github.com/octocat/Hello-World/commit/7638417db6d59f3c431d3e1f261cc637155684cd" }
```

--------------------------------

### Get Commonly Used Licenses Response Example

Source: https://docs.github.com/en/rest/licenses/licenses

This is an example of a successful (200 OK) response from the "Get all commonly used licenses" endpoint. The response is a JSON array containing objects, where each object represents a license and includes its key, name, SPDX ID, URL, and node ID.

```json
[ { "key": "mit", "name": "MIT License", "spdx_id": "MIT", "url": "https://api.github.com/licenses/mit", "node_id": "MDc6TGljZW5zZW1pdA==" }, { "key": "lgpl-3.0", "name": "GNU Lesser General Public License v3.0", "spdx_id": "LGPL-3.0", "url": "https://api.github.com/licenses/lgpl-3.0", "node_id": "MDc6TGljZW5zZW1pdA==" }, { "key": "mpl-2.0", "name": "Mozilla Public License 2.0", "spdx_id": "MPL-2.0", "url": "https://api.github.com/licenses/mpl-2.0", "node_id": "MDc6TGljZW5zZW1pdA==" }, { "key": "agpl-3.0", "name": "GNU Affero General Public License v3.0", "spdx_id": "AGPL-3.0", "url": "https://api.github.com/licenses/agpl-3.0", "node_id": "MDc6TGljZW5zZW1pdA==" }, { "key": "unlicense", "name": "The Unlicense", "spdx_id": "Unlicense", "url": "https://api.github.com/licenses/unlicense", "node_id": "MDc6TGljZW5zZW1pdA==" }, { "key": "apache-2.0", "name": "Apache License 2.0", "spdx_id": "Apache-2.0", "url": "https://api.github.com/licenses/apache-2.0", "node_id": "MDc6TGljZW5zZW1pdA==" }, { "key": "gpl-3.0", "name": "GNU General Public License v3.0", "spdx_id": "GPL-3.0", "url": "https://api.github.com/licenses/gpl-3.0", "node_id": "MDc6TGljZW5zZW1pdA==" } ]
```

--------------------------------

### Run Local PHP Development Server

Source: https://docs.github.com/en/copilot/tutorials/migrate-a-project

This command starts a local development server for the PHP website on a specified port. It allows for local testing and verification of the website's functionality before migration. Ensure PHP is installed and accessible in your environment.

```shell
php -S localhost:8000
```

--------------------------------

### Authenticate with Installation Access Token

Source: https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-as-a-github-app-installation

Details on how to use the generated installation access token to authenticate subsequent REST API or GraphQL API requests.

```APIDOC
## Authenticating REST API or GraphQL API Requests

### Description
Send the generated installation access token in the `Authorization` header of your REST API or GraphQL API requests to authenticate as the GitHub App installation.

### Method
GET, POST, PUT, DELETE, etc. (for REST API)
POST (for GraphQL API)

### Endpoint
Any applicable GitHub REST API endpoint or GraphQL API endpoint.

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
Depends on the specific API endpoint.

### Request Example (REST API)
```bash
curl -H "Authorization: Bearer INSTALLATION_ACCESS_TOKEN" https://api.github.com/user/repos
```

### Response
#### Success Response
Depends on the specific API endpoint.

#### Response Example
Depends on the specific API endpoint.
```

--------------------------------

### SSH Key File Save Prompt (Linux Example)

Source: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent_platform=linux

Example prompt for saving the SSH key file on Linux. Pressing Enter accepts the default file location.

```text
> Enter a file in which to save the key (/home/YOU/.ssh/id_ed25519_sk):[Press enter]
```

--------------------------------

### Example Response for Get Community Profile Metrics

Source: https://docs.github.com/en/rest/metrics/community

This is an example JSON response for the 'Get community profile metrics' endpoint. It includes the 'health_percentage' score, repository description, and details about various community files like 'code_of_conduct', 'license', 'readme', etc. Note that 'content_reports_enabled' is only returned for organization-owned repositories.

```json
{
  "health_percentage": 100,
  "description": "My first repository on GitHub!",
  "documentation": null,
  "files": {
    "code_of_conduct": {
      "name": "Contributor Covenant",
      "key": "contributor_covenant",
      "url": "https://api.github.com/codes_of_conduct/contributor_covenant",
      "html_url": "https://github.com/octocat/Hello-World/blob/master/CODE_OF_CONDUCT.md"
    },
    "code_of_conduct_file": {
      "url": "https://api.github.com/repos/octocat/Hello-World/contents/CODE_OF_CONDUCT.md",
      "html_url": "https://github.com/octocat/Hello-World/blob/master/CODE_OF_CONDUCT.md"
    },
    "contributing": {
      "url": "https://api.github.com/repos/octocat/Hello-World/contents/CONTRIBUTING",
      "html_url": "https://github.com/octocat/Hello-World/blob/master/CONTRIBUTING"
    },
    "issue_template": {
      "url": "https://api.github.com/repos/octocat/Hello-World/contents/ISSUE_TEMPLATE",
      "html_url": "https://github.com/octocat/Hello-World/blob/master/ISSUE_TEMPLATE"
    },
    "pull_request_template": {
      "url": "https://api.github.com/repos/octocat/Hello-World/contents/PULL_REQUEST_TEMPLATE",
      "html_url": "https://github.com/octocat/Hello-World/blob/master/PULL_REQUEST_TEMPLATE"
    },
    "license": {
      "name": "MIT License",
      "key": "mit",
      "spdx_id": "MIT",
      "url": "https://api.github.com/licenses/mit",
      "html_url": "https://github.com/octocat/Hello-World/blob/master/LICENSE",
      "node_id": "MDc6TGljZW5zZW1pdA=="
    },
    "readme": {
      "url": "https://api.github.com/repos/octocat/Hello-World/contents/README.md",
      "html_url": "https://github.com/octocat/Hello-World/blob/master/README.md"
    }
  },
  "updated_at": "2017-02-28T19:09:29Z",
  "content_reports_enabled": true
}
```

--------------------------------

### Hypermedia Links

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

Details the use of `*_url` properties for linking to related resources and constructing URLs.

```APIDOC
## Hypermedia Links

### Description
Resources may contain one or more `*_url` properties that link to other related resources. API clients are strongly recommended to use these explicit URLs instead of constructing them manually to ensure compatibility with future API upgrades.

### URI Templates
All provided URLs are expected to be proper RFC 6570 URI templates.

### Usage Example
URI templates can be expanded using libraries. For instance, using a hypothetical `URITemplate` library:

```
tmpl = URITemplate.new('/notifications{?since,all,participating}')
tmpl.expand()
# => "/notifications"

tmpl.expand all: 1
# => "/notifications?all=1"

tmpl.expand all: 1, participating: 1
# => "/notifications?all=1&participating=1"
```
```

--------------------------------

### Get a code scanning default setup configuration

Source: https://docs.github.com/en/rest/code-scanning/code-scanning

Retrieves the current code scanning default setup configuration for a repository. Requires fine-grained tokens with 'Administration' repository permissions (read).

```APIDOC
## GET /repos/{owner}/{repo}/code-scanning/default-setup

### Description
Retrieves the current code scanning default setup configuration for a repository.

### Method
GET

### Endpoint
/repos/{owner}/{repo}/code-scanning/default-setup

### Parameters
#### Path Parameters
- **owner** (string) - Required - The account owner of the repository. The name is not case sensitive.
- **repo** (string) - Required - The name of the repository without the `.git` extension. The name is not case sensitive.

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "example": "GET /repos/OWNER/REPO/code-scanning/default-setup"
}
```

### Response
#### Success Response (200)
- **state** (string) - The current state of the code scanning default setup.
- **languages** (array of strings) - The list of languages configured for code scanning.
- **query_suite** (string) - The query suite being used.
- **threat_model** (string) - The threat model configuration.
- **updated_at** (string) - The timestamp when the configuration was last updated.
- **schedule** (string) - The schedule for code scanning.

#### Response Example
```json
{
  "state": "configured",
  "languages": [
    "ruby",
    "python"
  ],
  "query_suite": "default",
  "threat_model": "remote",
  "updated_at": "2023-01-19T11:21:34Z",
  "schedule": "weekly"
}
```
```

--------------------------------

### Get Repository Analysis Status - JavaScript

Source: https://docs.github.com/en/rest/code-scanning/code-scanning

Example JavaScript code using the GitHub API to get the analysis status of a repository in a CodeQL variant analysis. This snippet demonstrates making a GET request with appropriate headers.

```javascript
async function getRepoAnalysisStatus(owner, repo, codeqlVariantAnalysisId, repoOwner, repoName, token) {
  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/code-scanning/codeql/variant-analyses/${codeqlVariantAnalysisId}/repos/${repoOwner}/${repoName}`, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  const data = await response.json();
  return data;
}
```

--------------------------------

### Create Octokit Instance with Authentication

Source: https://docs.github.com/en/rest/overview/media-types

Demonstrates how to create an instance of Octokit.js and authenticate it using a personal access token. Replace 'YOUR-TOKEN' with your actual GitHub token.

```javascript
import { Octokit } from "octokit";

const octokit = new Octokit({
  auth: 'YOUR-TOKEN'
});
```

--------------------------------

### Get an organization installation for the authenticated app

Source: https://docs.github.com/en/rest/apps/apps

Retrieves installation information for a given organization, which is useful for authenticated GitHub Apps. Requires a JWT for authentication.

```APIDOC
## GET /orgs/{org}/installation

### Description
Enables an authenticated GitHub App to find the organization's installation information. You must use a JWT to access this endpoint.

### Method
GET

### Endpoint
`/orgs/{org}/installation`

### Parameters
#### Path Parameters
- **org** (string) - Required - The organization name. The name is not case sensitive.

#### Headers
- **Accept** (string) - Required - Setting to `application/vnd.github+json` is recommended.
- **Authorization** (string) - Required - Bearer token for authentication.
- **X-GitHub-Api-Version** (string) - Required - API version, e.g., `2022-11-28`.

### Request Example
```bash
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/orgs/ORG/installation
```

### Response
#### Success Response (200)
- **id** (integer) - The unique identifier of the installation.
- **account** (object) - Information about the account that owns the installation.
- **repository_selection** (string) - Indicates if all repositories or a subset are accessible.
- **access_tokens_url** (string) - URL to retrieve access tokens for the installation.
- **repositories_url** (string) - URL to list repositories accessible by the installation.
- **html_url** (string) - HTML URL for the installation settings.
- **app_id** (integer) - The ID of the GitHub App.
- **client_id** (string) - The client ID of the GitHub App.
- **target_id** (integer) - The ID of the target (organization or user).
- **target_type** (string) - The type of the target (`Organization` or `User`).
- **permissions** (object) - Permissions granted to the installation.
- **events** (array of strings) - Events the installation is subscribed to.
- **created_at** (string) - Timestamp when the installation was created.
- **updated_at** (string) - Timestamp when the installation was last updated.
- **single_file_name** (string) - If applicable, the name of a single file managed by the installation.
- **has_multiple_single_files** (boolean) - Indicates if multiple single files are managed.
- **single_file_paths** (array of strings) - Paths to single files managed by the installation.
- **app_slug** (string) - The slug of the GitHub App.
- **suspended_at** (string or null) - Timestamp if the installation is suspended.
- **suspended_by** (string or null) - User who suspended the installation.

#### Response Example
```json
{
  "id": 1,
  "account": {
    "login": "github",
    "id": 1,
    "node_id": "MDEyOk9yZ2FuaXphdGlvbjE=",
    "avatar_url": "https://github.com/images/error/hubot_happy.gif",
    "gravatar_id": "",
    "url": "https://api.github.com/orgs/github",
    "html_url": "https://github.com/github",
    "followers_url": "https://api.github.com/users/github/followers",
    "following_url": "https://api.github.com/users/github/following{/other_user}",
    "gists_url": "https://api.github.com/users/github/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/github/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/github/subscriptions",
    "organizations_url": "https://api.github.com/users/github/orgs",
    "repos_url": "https://api.github.com/orgs/github/repos",
    "events_url": "https://api.github.com/orgs/github/events",
    "received_events_url": "https://api.github.com/users/github/received_events",
    "type": "Organization",
    "site_admin": false
  },
  "repository_selection": "all",
  "access_tokens_url": "https://api.github.com/app/installations/1/access_tokens",
  "repositories_url": "https://api.github.com/installation/repositories",
  "html_url": "https://github.com/organizations/github/settings/installations/1",
  "app_id": 1,
  "client_id": "Iv1.ab1112223334445c",
  "target_id": 1,
  "target_type": "Organization",
  "permissions": {
    "checks": "write",
    "metadata": "read",
    "contents": "read"
  },
  "events": [
    "push",
    "pull_request"
  ],
  "created_at": "2018-02-09T20:51:14Z",
  "updated_at": "2018-02-09T20:51:14Z",
  "single_file_name": "config.yml",
  "has_multiple_single_files": true,
  "single_file_paths": [
    "config.yml",
    ".github/issue_TEMPLATE.md"
  ],
  "app_slug": "github-actions",
  "suspended_at": null,
  "suspended_by": null
}
```
```

--------------------------------

### Resource Representations

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

Explains the difference between detailed and summary representations of resources returned by the API.

```APIDOC
## Resource Representations

### Description
Responses can include all attributes for a resource (detailed representation) or only a subset (summary representation), depending on whether an individual resource or a list of resources is fetched.

### Detailed Representation
When fetching an individual resource (e.g., a specific repository), the response typically includes all attributes.

### Summary Representation
When fetching a list of resources (e.g., multiple repositories), the response includes only a subset of attributes for each resource. This is done to optimize performance, as some attributes are computationally expensive to provide.

### Authorization Influence
Authorization can sometimes affect the level of detail included in a representation. Attributes excluded from summary representations can be obtained by fetching the detailed representation.

### Example Responses
Each API method provides an example response illustrating all attributes returned by that method.
```

--------------------------------

### Initializing CodeQL Action with Custom Database Location

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

This example demonstrates how to use the `db-location` parameter within the `init` action of the CodeQL GitHub Action to specify a custom directory for CodeQL databases.

```APIDOC
## Initializing CodeQL Action with Custom Database Location

### Description
This section details how to configure the `github/codeql-action/init@v3` to create CodeQL databases in a user-specified directory using the `db-location` parameter. This is useful for scenarios like uploading databases as workflow artifacts or when custom handling of database locations is required.

### Method
This configuration is applied within a GitHub Actions workflow YAML file using the `uses` directive for the CodeQL action.

### Endpoint
`github/codeql-action/init@v3`

### Parameters
#### Action Parameters
- **db-location** (string) - Required - The path where the CodeQL database should be created. This directory must be writable and either not exist or be empty. Examples: `${{ github.runner_temp }}/my_location`.

### Request Example
```yaml
- uses: github/codeql-action/init@v3
  with:
    db-location: '${{ github.runner_temp }}/my_location'
```

### Response
This action initializes the CodeQL environment. Successful execution means the `db-location` is set and the directory is ready for database creation. Errors might occur if the specified location is not writable or improperly configured.

#### Success Response (Implicit)
No explicit success response is returned, but the action completes without error, indicating the CodeQL environment is set up with the specified database location.

#### Response Example
(N/A - This is a configuration step within a workflow)

### Notes
- The directory specified by `db-location` must be writable by the workflow runner.
- For self-hosted runners or Docker containers, ensure the chosen directory is cleared between runs or databases are removed manually.
- If `db-location` is not specified, CodeQL databases will be created in a default temporary location (e.g., `${{ github.runner_temp }}/codeql_databases`).
```

--------------------------------

### Get Commonly Used Licenses Request Examples

Source: https://docs.github.com/en/rest/licenses/licenses

These examples demonstrate how to make a request to the "Get all commonly used licenses" endpoint using cURL, JavaScript, and the GitHub CLI. This endpoint retrieves a list of the most common open source licenses on GitHub. It requires the 'Accept' header and optionally accepts query parameters for pagination and filtering.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/licenses
```

```javascript
async function getCommonLicenses() {
  const response = await fetch('https://api.github.com/licenses', {
    headers: {
      'Accept': 'application/vnd.github+json',
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  const data = await response.json();
  console.log(data);
}
getCommonLicenses();
```

```github cli
gh api --method GET "/licenses" --header "Accept: application/vnd.github+json" --header "X-GitHub-Api-Version: 2022-11-28"
```

--------------------------------

### Get Repository Webhook Delivery (JavaScript)

Source: https://docs.github.com/en/rest/repos/webhooks

Example of how to get a repository webhook delivery using JavaScript. This function assumes you have a configured Octokit client.

```javascript
await octokit.request('GET /repos/{owner}/{repo}/hooks/{hook_id}/deliveries/{delivery_id}', {
  owner: 'OWNER',
  repo: 'REPO',
  hook_id: HOOK_ID,
  delivery_id: DELIVERY_ID,
  headers: {
    'Accept': 'application/vnd.github+json',
    'X-GitHub-Api-Version': '2022-11-28'
  }
})
```

--------------------------------

### Initialize Sinatra Application for GitHub Webhooks

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/building-ci-checks-with-a-github-app

Sets up the basic Sinatra application, including the port, binding address, and loading of private key and secrets from environment variables. It also configures logging for development.

```ruby
class GHAapp < Sinatra::Application

  set :port, 3000
  set :bind, '0.0.0.0'

  PRIVATE_KEY = OpenSSL::PKey::RSA.new(ENV['GITHUB_PRIVATE_KEY'].gsub('\n', "\n"))

  WEBHOOK_SECRET = ENV['GITHUB_WEBHOOK_SECRET']

  APP_IDENTIFIER = ENV['GITHUB_APP_IDENTIFIER']

  configure :development do
    set :logging, Logger::DEBUG
  end

  # ... rest of the application

  run! if __FILE__ == $0
end
```

--------------------------------

### GitHub Actions Workflow for Node.js Package Release

Source: https://docs.github.com/en/packages/quickstart

This YAML workflow defines steps to build and publish a Node.js package to GitHub Packages. It checks out code, sets up Node.js, installs dependencies, runs tests, and publishes the package upon release creation.

```yaml
name: Node.js Package

on:
  release:
    types: [created]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: 20
      - run: npm ci
      - run: npm test

  publish-gpr:
    needs: build
    runs-on: ubuntu-latest
    permissions:
      packages: write
      contents: read
    steps:
      - uses: actions/checkout@v5
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          registry-url: https://npm.pkg.github.com/
      - run: npm ci
      - run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{secrets.GITHUB_TOKEN}}
```

--------------------------------

### GET Request with Query Parameters using `curl`

Source: https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api_tool=javascript

This example shows how to make a GET request to the GitHub API's events endpoint and use query parameters to control the number of results per page and the page number. It requires `Accept` and `X-GitHub-Api-Version` headers.

```shell
curl --request GET \
--url "https://api.github.com/events?per_page=2&page=1" \
--header "Accept: application/vnd.github+json" \
--header "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/events
```

```shell
curl --request GET \
--url "https://api.github.com/events?per_page=2&page=1" \
--header "Accept: application/vnd.github+json" \
--header "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/events
```

--------------------------------

### Complete Initial Ruby CLI Script

Source: https://docs.github.com/en/apps/creating-github-apps/guides/building-a-cli-with-a-github-app

This snippet represents the complete 'app_cli.rb' file after initial setup. It includes the shebang line, standard library dependencies, the 'main' function with basic command handling, and the call to execute 'main'. The order of functions does not impact execution as long as the 'main' call is last.

```ruby
#!/usr/bin/env ruby

require "net/http"
require "json"
require "uri"
require "fileutils"

def main
  case ARGV[0]
  when "help"
    puts "`help` is not yet defined"
  when "login"
    puts "`login` is not yet defined"
  when "whoami"
    puts "`whoami` is not yet defined"
  else
    puts "Unknown command `#{ARGV[0]}`"
  end
end

main
```

--------------------------------

### Make a GET request with query parameters using curl

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=cli

Shows how to make a `curl` GET request to the GitHub API with query parameters. This example illustrates adding parameters like `per_page` and `page` to the URL to control the results. It includes setting the `Accept` and `X-GitHub-Api-Version` headers.

```shell
curl --request GET \
--url "https://api.github.com/events?per_page=2&page=1" \
--header "Accept: application/vnd.github+json" \
--header "X-GitHub-Api-Version: 2022-11-28"
```

--------------------------------

### Authenticating with an Installation Access Token

Source: https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-as-a-github-app-installation

How to use a generated installation access token to authenticate API requests.

```APIDOC
## Authenticating with an Installation Access Token

### Description
To authenticate with an installation access token, include it in the `Authorization` header of an API request. The access token will work with both the GraphQL API and the REST API.

### Method
GET (example for `/meta` endpoint)

### Endpoint
`https://api.github.com/meta` (example)

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
curl --request GET \
--url "https://api.github.com/meta" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer INSTALLATION_ACCESS_TOKEN" \
--header "X-GitHub-Api-Version: 2022-11-28"
```

### Response
#### Success Response (200)
Depends on the endpoint being called. The installation access token authorizes the request.

#### Response Example
(Example for `/meta` endpoint)
```json
{
  "api": {
    "hooks": {
      "url": "https://api.github.com/hooks"
    },
    "git": {
      "ssh_url": "git@github.com:xxx",
      "https_url": "https://github.com:xxx"
    }
  }
}
```

### Note
- Your app must have the required permissions to use the endpoint.
- In most cases, you can use `Authorization: Bearer` or `Authorization: token` to pass a token. However, if you are passing a JSON web token (JWT), you must use `Authorization: Bearer`.
```

--------------------------------

### Make a GET Request to GitHub API using GitHub CLI

Source: https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api

This example demonstrates how to make a GET request to the '/octocat' endpoint using the GitHub CLI. It includes specifying the HTTP method, setting 'Accept' and 'X-GitHub-Api-Version' headers. This method is useful for retrieving data from the GitHub API.

```shell
gh api --method GET /octocat \
--header 'Accept: application/vnd.github+json' \
--header "X-GitHub-Api-Version: 2022-11-28"
```

--------------------------------

### Start Organization Migration with JavaScript

Source: https://docs.github.com/en/rest/migrations/orgs

This JavaScript example shows how to start an organization migration using the GitHub API. It utilizes the fetch API to send a POST request with the necessary headers and a JSON body containing migration parameters. Replace ORG and <YOUR-TOKEN> with your specific values.

```javascript
async function startOrgMigration(org, token) {
  const url = `https://api.github.com/orgs/${org}/migrations`;
  const body = JSON.stringify({
    repositories: ["github/Hello-World"],
    lock_repositories: true
  });

  const response = await fetch(url, {
    method: 'POST',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28',
      'Content-Type': 'application/json'
    },
    body: body
  });

  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }

  return await response.json();
}

// Example usage:
// const orgName = "YOUR_ORG_NAME";
// const githubToken = "YOUR_GITHUB_TOKEN";
// startOrgMigration(orgName, githubToken).then(data => console.log(data)).catch(error => console.error('Error:', error));
```

--------------------------------

### Install GitHub CLI Webhook Extension

Source: https://docs.github.com/en/webhooks/testing-and-troubleshooting-webhooks/using-the-github-cli-to-forward-webhooks-for-testing

Installs the 'gh-webhook' extension for the GitHub CLI, enabling webhook forwarding capabilities. This is the first step to start receiving webhooks locally.

```bash
gh extension install cli/gh-webhook

```

--------------------------------

### Configure CodeQL Build Mode for C/C++ and Go Analysis

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/codeql-code-scanning-for-compiled-languages

This example configures the CodeQL action to use the 'autobuild' mode for analyzing C/C++ and Go code. 'Autobuild' is used when default setup is enabled for languages not supporting 'none' build, or when explicitly specified in advanced setup workflows.

```yaml
# Initializes the CodeQL tools for scanning.
name: Analyze
strategy:
  matrix:
    include:
      # Analyze C and C++ code
      - language: c-cpp
        build-mode: autobuild
      # Analyze Go code
      - language: go
        build-mode: autobuild

steps:
  - uses: github/codeql-action/init@v3
    with:
      languages: ${{ matrix.language }}
      build-mode: ${{ matrix.build-mode }}

```

--------------------------------

### Get Repository README - JavaScript

Source: https://docs.github.com/en/rest/repos/contents

Example JavaScript request using the Octokit library to retrieve a repository's README file. Assumes Octokit is configured with appropriate authentication and permissions. Handles response parsing.

```javascript
const { Octokit } = require("@octokit/core");
const octokit = new Octokit({ auth: "YOUR-TOKEN" });

async function getReadme() {
  try {
    const response = await octokit.request('GET /repos/{owner}/{repo}/readme', {
      owner: 'OWNER',
      repo: 'REPO',
      headers: {
        'X-GitHub-Api-Version': '2022-11-28'
      }
    });
    console.log(response.data);
  } catch (error) {
    console.error(error);
  }
}

getReadme();
```

--------------------------------

### YAML Workflow for Actions Runner Controller Demo

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

This YAML file defines a GitHub Actions workflow that utilizes runner scale sets. Ensure the `runs-on` value matches your Helm installation name for the autoscaling runner set. This workflow is designed for demonstration purposes and triggers manually.

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

### Get Latest Release - cURL

Source: https://docs.github.com/en/rest/releases/releases

Example cURL request to retrieve the latest release for a repository. This GET request requires the owner and repository name. The 'Accept' header should be set to 'application/vnd.github+json'.

```shell
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/releases/latest
```

--------------------------------

### Execute Shell Commands using run

Source: https://docs.github.com/en/actions/tutorials/create-an-example-workflow

The 'run' keyword allows direct execution of shell commands on the runner. This is useful for various tasks like installing software, running scripts, or checking versions. The example shows how to display the version of the 'bats' command.

```yaml
- run: bats -v
```

--------------------------------

### Making a Request (Example)

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=javascript

Illustrates how to make a request to the GitHub REST API using common tools like `curl` or Octokit.js, focusing on the User-Agent header.

```APIDOC
## Making a Request

### Request Example (User-Agent Header)

```
User-Agent: Awesome-Octocat-App
```

Requests without a `User-Agent` header will be rejected. Providing an invalid `User-Agent` header will result in a `403 Forbidden` response.
```

--------------------------------

### Install VS Code Extension in Dev Container

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-python-project-for-codespaces

This snippet demonstrates how to install the 'Code Spell Checker' VS Code extension. It's configured within the `customizations.vscode.extensions` block in `devcontainer.json`, ensuring the extension is available when the container starts.

```jsonc
// Configure tool-specific properties.
"customizations": {
  // Configure properties specific to VS Code.
  "vscode": {
    // Add the IDs of extensions you want installed when the container is created.
    "extensions": [
      "streetsidesoftware.code-spell-checker"
    ]
  }
}
```

--------------------------------

### GraphQL API Authentication and Setup

Source: https://docs.github.com/en/graphql/guides/managing-enterprise-accounts

Instructions for authenticating with the GitHub GraphQL API using a personal access token and setting up a GraphQL client like Insomnia.

```APIDOC
## Authentication with Personal Access Token

### Description
To authenticate with the GraphQL API, you need to generate a personal access token (PAT) with appropriate permissions. The PAT should be kept secure and added to your GraphQL client.

### Scopes Recommended
* `repo`: Full control of private repositories.
* `admin:org`: Full control of organizations.
* `user`: Access to user data.
* `admin:enterprise`: Full control of enterprises (includes `manage_runners:enterprise`, `manage_billing:enterprise`, and `read:enterprise`).
* `manage_billing:enterprise`: Read and write enterprise billing data.
* `read:enterprise`: Read enterprise profile data.

### GraphQL Client Setup (Example: Insomnia)

1.  **Method**: `POST`
2.  **Base URL**:
    *   GitHub Enterprise Cloud: `https://api.github.com/graphql`
    *   GitHub Enterprise Cloud with Data Residency: `https://api.SUBDOMAIN.ghe.com/graphql`
    *   Self-hosted enterprise instance: `https://<HOST>/api/graphql`
3.  **Authentication**: 
    *   Go to the "Auth" menu and select "Bearer Token".
    *   In the "TOKEN" field, enter your generated personal access token.
4.  **Headers**: 
    *   Add a header with the key `Content-Type` and the value `application/json`.
```

--------------------------------

### Search Users Request Example (JavaScript)

Source: https://docs.github.com/en/rest/search/search

Example of how to search for users using the GitHub API with JavaScript. It demonstrates making a GET request with appropriate headers and query parameters.

```javascript
async function searchUsers() {
  const response = await fetch('https://api.github.com/search/users?q=Q', {
    headers: {
      'Accept': 'application/vnd.github+json',
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  const data = await response.json();
  console.log(data);
}
```

--------------------------------

### Customize Copilot Reviews with Repository Instructions

Source: https://docs.github.com/en/copilot/how-tos/agents/copilot-code-review/using-copilot-code-review

Example of a `.github/copilot-instructions.md` file used to customize GitHub Copilot code reviews for a repository. These instructions guide Copilot's review process, such as language preference, adherence to specific checklists, and coding style preferences. This allows for tailored feedback based on project-specific requirements.

```markdown
When performing a code review, respond in Spanish.

When performing a code review, apply the checks in the `/security/security-checklist.md` file.

When performing a code review, focus on readability and avoid nested ternary operators.

```

--------------------------------

### JavaScript Request Example for Get a Gist

Source: https://docs.github.com/en/rest/gists/gists

This snippet provides a JavaScript example for fetching a gist from the GitHub API. It utilizes the fetch API to make the request and handles the response.

```javascript
async function getGist(gistId) {
  const response = await fetch(`https://api.github.com/gists/${gistId}`, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  const data = await response.json();
  console.log(data);
}
```

--------------------------------

### Example Helm values.yaml for Listener Volume Mount

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/authenticating-to-the-github-api

This is an example snippet from a scale set's `values.yaml` file, specifically showing how the listener container's volume mounts and volumes are configured to include a certificate volume. This ensures the listener has access to necessary credentials for vault integration.

```yaml
listenerTemplate:
  spec:
    containers:
      - name: listener
        volumeMounts:
          - name: cert-volume
            mountPath: /akv
            readOnly: true
    volumes:
      - name: cert-volume
        secret:
          secretName: my-cert-secret
```

--------------------------------

### startOrganizationMigration

Source: https://docs.github.com/en/graphql/reference/mutations

Starts a GitHub Enterprise Importer organization migration.

```APIDOC
## startOrganizationMigration

### Description
Starts a GitHub Enterprise Importer organization migration.

### Method
POST

### Endpoint
/graphql

### Parameters
#### Query Parameters
None

#### Request Body
- **input** (StartOrganizationMigrationInput!) - Input object for the mutation.

### Request Example
```json
{
  "query": "mutation StartOrganizationMigration($input: StartOrganizationMigrationInput!) { startOrganizationMigration(input: $input) { clientMutationId orgMigration { ... } } }",
  "variables": {
    "input": {
      "clientMutationId": "unique-client-mutation-id",
      "sourceOrgName": "source-org",
      "targetEnterpriseId": "target-enterprise-id"
    }
  }
}
```

### Response
#### Success Response (200)
- **clientMutationId** (String) - A unique identifier for the client performing the mutation.
- **orgMigration** (OrganizationMigration) - The new organization migration.

#### Response Example
```json
{
  "data": {
    "startOrganizationMigration": {
      "clientMutationId": "unique-client-mutation-id",
      "orgMigration": {
        "id": "migration-id",
        "state": "QUEUED"
      }
    }
  }
}
```
```

--------------------------------

### Get Secret Scanning Scan History - cURL

Source: https://docs.github.com/en/rest/secret-scanning/secret-scanning_apiversion=2022-11-28

Example of retrieving the secret scanning scan history for a repository using cURL. This requires specifying the owner and repository in the GET request.

```shell
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/secret-scanning/scan-history
```

--------------------------------

### Create C/C++ CodeQL Database with Make

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Creates a CodeQL database for a C/C++ project using the `make` build system. It's recommended to disable parallel execution using `-j1` or similar methods.

```bash
# Disable parallel execution via `-j1` or other techniques: https://www.gnu.org/software/make/manual/make.html#Parallel-Execution
codeql database create cpp-database --language=c-cpp --command=make
```

--------------------------------

### Complete devcontainer.json Example

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-dotnet-project-for-codespaces

This is a complete example of a devcontainer.json file incorporating dotnet feature, port forwarding, a post-create command, and VS Code extension customization.

```jsonc
// For format details, see https://aka.devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/dotnet
{
  "name": "C# (.NET)",
  // Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
  "image": "mcr.microsoft.com/devcontainers/dotnet:0-7.0",
  "features": {
    "ghcr.io/devcontainers/features/dotnet:1": {}
  },

  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  "forwardPorts": [5000],
  // "portsAttributes": {
  //   "5001": {
  //     "protocol": "https"
  //   }
  // }

  // Use 'postCreateCommand' to run commands after the container is created.
  "postCreateCommand": "dotnet restore",

  // Configure tool-specific properties.
  "customizations": {
    // Configure properties specific to VS Code.
    "vscode": {
      // Add the IDs of extensions you want installed when the container is created.
      "extensions": [
        "streetsidesoftware.code-spell-checker"
      ]
    }
  }

  // Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
  // "remoteUser": "root"
}

```

--------------------------------

### Configure Copilot for Java, JavaScript, and Jira Integration

Source: https://docs.github.com/en/copilot/concepts/about-customizing-github-copilot-chat-responses_tool=webui

This example `.github/copilot-instructions.md` file configures Copilot's behavior for a repository. It specifies using Bazel for Java dependencies, double quotes and tabs for JavaScript, and notes the use of Jira for work tracking.

```markdown
We use Bazel for managing our Java dependencies, not Maven, so when talking about Java packages, always give me instructions and code samples that use Bazel.

We always write JavaScript with double quotes and tabs for indentation, so when your responses include JavaScript code, please follow those conventions.

Our team uses Jira for tracking items of work.

```

--------------------------------

### Get a Workflow Run - JavaScript Example

Source: https://docs.github.com/en/rest/actions/workflow-runs_apiversion=2022-11-28

Example of how to retrieve a specific workflow run using JavaScript. This utilizes the fetch API to make a GET request to the GitHub API endpoint. Ensure you handle the response and potential errors appropriately. Replace placeholders with your actual repository owner, repository name, and workflow run ID.

```javascript
async function getWorkflowRun(owner, repo, runId, token) {
  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/actions/runs/${runId}`, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  const data = await response.json();
  return data;
}

// Example usage:
// const owner = 'OWNER';
// const repo = 'REPO';
// const runId = 'RUN_ID';
// const token = '<YOUR-TOKEN>';
// getWorkflowRun(owner, repo, runId, token).then(run => console.log(run)).catch(error => console.error(error));
```

--------------------------------

### Include Guides in Product Pages

Source: https://docs.github.com/en/contributing/syntax-and-versioning-for-github-docs/using-yaml-frontmatter

Renders a list of articles on product guide pages, filterable by 'type' and 'topics'. This property is only applicable when used with 'layout: product-guides'.

```yaml
includeGuides:
  - /actions/guides/about-continuous-integration
  - /actions/guides/setting-up-continuous-integration-using-workflow-templates
  - /actions/guides/building-and-testing-nodejs
  - /actions/guides/building-and-testing-powershell
```

--------------------------------

### Get Repository README from Directory - JavaScript

Source: https://docs.github.com/en/rest/repos/contents_apiversion=2022-11-28

This JavaScript example fetches a README file from a specified directory within a repository. It includes the 'dir' path parameter in the API request. Ensure correct headers and authentication are provided.

```javascript
async function getRepoReadmeFromDir(owner, repo, dir, token) {
  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/readme/${dir}`, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  const data = await response.json();
  return data;
}
```

--------------------------------

### Creating Databases for Go Projects

Source: https://docs.github.com/en/code-security/codeql-cli/using-the-codeql-cli/creating-codeql-databases

Create a CodeQL database for a Go project. This can be done using the `CODEQL_EXTRACTOR_GO_BUILD_TRACING=on` environment variable or a custom build script.

```APIDOC
## POST /codeql/database/create/go

### Description
Creates a CodeQL database for a Go project, with options for build tracing or custom build scripts.

### Method
POST

### Endpoint
`/codeql/database/create/go`

### Parameters
#### Path Parameters
- **database-name** (string) - Required - The name for the Go database.

#### Query Parameters
- **language** (string) - Required - Must be set to `go`.
- **command** (string) - Optional - A custom build script to execute (e.g., `'./scripts/build.sh'`).

### Request Example (with build tracing)
```bash
CODEQL_EXTRACTOR_GO_BUILD_TRACING=on codeql database create go-database --language=go
```

### Request Example (with custom script)
```bash
codeql database create go-database --language=go --command='./scripts/build.sh'
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation that the database creation command was issued.

#### Response Example
```json
{
  "message": "CodeQL database creation command for Go initiated."
}
```
```

--------------------------------

### Get Repository Installation

Source: https://docs.github.com/en/rest/apps/apps

Enables an authenticated GitHub App to find the repository's installation information. The installation's account type will be either an organization or a user account, depending which account the repository belongs to. You must use a JWT to access this endpoint.

```plaintext
This endpoint retrieves installation information for a GitHub App associated with a specific repository. It requires authentication using a JWT and is applicable for both user and organization-owned repositories.
```

--------------------------------

### Media Types

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_tool=curl

Learn how to specify the desired data format for your API requests using the `Accept` header.

```APIDOC
## Media Types

### Description

Media types specify the format of the data you want to consume from the API. They are specific to resources and can be changed independently.

### Supported Media Types

- `application/vnd.github+json`: The most common GitHub media type.
- `application/json`: Standard JSON media type.
- Custom Media Types: `application/vnd.github.PARAM+json` (e.g., `application/vnd.github.diff+json`, `application/vnd.github.raw+json`)

### Usage

Specify the desired media type in the `Accept` header of your request.

### Example

```http
GET /users/octocat
Accept: application/vnd.github.v3+json
```
```

--------------------------------

### Basic Dependency Review Workflow Setup (YAML)

Source: https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/configuring-the-dependency-review-action

This snippet demonstrates the basic structure of a GitHub workflow file to enable the Dependency Review action. It triggers on pull requests and checks out the repository before running the action.

```yaml
name: 'Dependency Review'
on: [pull_request]

permissions:
  contents: read

jobs:
  dependency-review:
    runs-on: ubuntu-latest
    steps:
     - name: 'Checkout Repository'
       uses: actions/checkout@v5
     - name: Dependency Review
       uses: actions/dependency-review-action@v4

```

--------------------------------

### Search Code Example using JavaScript

Source: https://docs.github.com/en/rest/search/search

This example shows how to perform a code search using JavaScript. It utilizes the fetch API to make a GET request to the GitHub API, including necessary headers and query parameters.

```javascript
async function searchCode(query) {
  const response = await fetch('https://api.github.com/search/code', {
    method: 'GET',
    headers: {
      'Accept': 'application/vnd.github+json',
      'X-GitHub-Api-Version': '2022-11-28',
      'Authorization': 'token YOUR_GITHUB_TOKEN' // Replace with your token
    },
    params: {
      q: query
    }
  });
  const data = await response.json();
  return data;
}

// Example usage:
searchCode('addClass+in:file+language:js+repo:jquery/jquery').then(results => {
  console.log(results);
});
```

--------------------------------

### Get Issue Comment - GitHub CLI Example

Source: https://docs.github.com/en/rest/issues/comments

This example demonstrates how to use the GitHub CLI (gh) to retrieve an issue comment. It simplifies the process of interacting with the GitHub API from the command line.

```bash
gh api repos/OWNER/REPO/issues/comments/COMMENT_ID \
  --jq '.body' # Example to extract just the body
```

--------------------------------

### Create GitHub Codespace via CLI

Source: https://docs.github.com/en/codespaces/developing-in-a-codespace/creating-a-codespace-for-a-repository

This snippet demonstrates how to create a GitHub codespace using the GitHub CLI. It shows the basic command and an example with flags to specify repository, branch, dev container path, and machine type. Ensure you have the GitHub CLI installed and authenticated to use these commands.

```bash
gh codespace create
```

```bash
gh codespace create -r OWNER/REPO -b BRANCH --devcontainer-path PATH -m MACHINE-TYPE
```

--------------------------------

### GET /user/installations/{installation_id}/repositories

Source: https://docs.github.com/en/rest/apps/installations

Retrieves a list of repositories accessible to the user's access token. The permissions for each repository are included in the response.

```APIDOC
## GET /user/installations/{installation_id}/repositories

### Description
Lists all repositories that the authenticated user can access. The `permissions` hash included in the response indicates the user's access level for each repository.

### Method
GET

### Endpoint
/user/installations/{installation_id}/repositories

### Parameters
#### Path Parameters
- **installation_id** (integer) - Required - The unique identifier of the GitHub App installation.

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "example": "curl -L \
  -H \"Accept: application/vnd.github+json\" \
  -H \"Authorization: Bearer <YOUR-TOKEN>\" \
  -H \"X-GitHub-Api-Version: 2022-11-28\" \
  https://api.github.com/user/installations/1/repositories"
}
```

### Response
#### Success Response (200)
- **permissions** (object) - A hash containing the user's access level for each repository.
- **repositories** (array) - A list of repositories accessible to the user.

#### Response Example
```json
{
  "example": "{\"repositories\":[{\"id\":12962694,\"name\":\"a-great-repo\",\"full_name\":\"octocat/a-great-repo\",\"owner\":{\"login\":\"octocat\",\"id\":1,\"avatar_url\":\"https://github.com/images/error/octocat_happy.gif\",\"url\":\"https://api.github.com/users/octocat\",\"html_url\":\"https://github.com/octocat\",\"type\":\"User\",\"site_admin\":true},\"private\":false,\"fork\":false,\"created_at\":\"2011-01-26T19:01:12Z\",\"updated_at\":\"2011-01-26T19:01:12Z\",\"pushed_at\":\"2011-01-26T19:01:12Z\",\"homepage\":\"https://github.com\",\"size\":104,\"stargazers_count\":11,\"watchers_count\":11,\"language\":\"Common Lisp\",\"has_issues\":true,\"has_projects\":true,\"has_wiki\":true,\"has_pages\":false,\"forks_count\":0,\"mirror_url\":null,\"open_issues_count\":0,\"license\":{\"key\":\"mit\",\"name\":\"MIT License\",\"spdx_id\":\"MIT\",\"url\":null,\"node_id\":\"MDc6TGljZW5zZTE1\"},\"allow_forking\":true,\"is_template\":false,\"web_commit_signoff_required\":false,\"topics\":[\"octocat\",\"atom\",\"electron\",\"github\"],\"visibility\":\"public\"}],\"permissions\":{\"read\":true,\"maintain\":false,\"admin\":false,\"push\":false,\"triage\":false},\"total_count\":1}"}
```

### Error Handling
- **200** - OK: The access the user has to each repository is included in the hash under the `permissions` key.
- **304** - Not Modified
- **403** - Forbidden
- **404** - Resource not found
```

--------------------------------

### Get Dependabot Alerts via GitHub CLI

Source: https://docs.github.com/en/rest/dependabot/alerts

Example of how to list Dependabot alerts for a repository using the GitHub CLI. This command simplifies authentication and API interaction.

```shell
gh api repos/OWNER/REPO/dependabot/alerts
```

--------------------------------

### Get Repository Commits - GitHub CLI Example

Source: https://docs.github.com/en/rest/commits/commits

This example uses the GitHub CLI to retrieve commits for a repository. The `gh` command simplifies authentication and API interaction. The output is typically JSON, which can be further processed.

```bash
gh api repos/OWNER/REPO/commits/REF --jq '.'
```

--------------------------------

### Get Repository README for Directory - GitHub CLI

Source: https://docs.github.com/en/rest/repos/contents

Example command using the GitHub CLI to retrieve a README file from a specific directory within a repository. Authentication is handled by the CLI.

```bash
gh api repos/OWNER/REPO/readme/DIR \
  --header 'Accept: application/vnd.github.raw+json' \
  --header 'X-GitHub-Api-Version: 2022-11-28'
```

--------------------------------

### Get Repository Permissions Response Example (200 OK)

Source: https://docs.github.com/en/rest/collaborators/collaborators

Example JSON response when a user has admin permissions for a repository. It includes the `permission` level (e.g., 'admin') and the `role_name`, along with user details.

```json
{ "permission": "admin", "role_name": "admin", "user": { "login": "octocat", "id": 1, "node_id": "MDQ6VXNlcjE=", "avatar_url": "https://github.com/images/error/octocat_happy.gif", "gravatar_id": "", "url": "https://api.github.com/users/octocat", "html_url": "https://github.com/octocat", "followers_url": "https://api.github.com/users/octocat/followers", "following_url": "https://api.github.com/users/octocat/following{/other_user}", "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}", "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}", "subscriptions_url": "https://api.github.com/users/octocat/subscriptions", "organizations_url": "https://api.github.com/users/octocat/orgs", "repos_url": "https://api.github.com/users/octocat/repos", "events_url": "https://api.github.com/users/octocat/events{/privacy}", "received_events_url": "https://api.github.com/users/octocat/received_events", "type": "User", "site_admin": false } }
```

--------------------------------

### Build Customization Scripts with npm

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

This command installs npm dependencies, bootstraps the project, and builds all npm packages. This process generates the `index.js` files necessary for triggering customization scripts in `packages/docker/dist` and `packages/k8s/dist`.

```bash
npm install && npm run bootstrap && npm run build-all
```

--------------------------------

### Integration Installation API

Source: https://docs.github.com/en/organizations/keeping-your-organization-secure/managing-security-settings-for-your-organization/audit-log-events-for-your-organization

This section details events related to the installation of a GitHub App.

```APIDOC
## POST /integration_installation/create

### Description
Handles the event when a GitHub App is installed.

### Method
POST

### Endpoint
/integration_installation/create

### Parameters
#### Request Body
- `operation_type` (string) - Required - The type of operation performed.
- `name` (string) - Required - The name of the integration.
- `repository_selection` (string) - Required - Specifies how repositories are selected for the installation.
- `user_id` (integer) - Required - The ID of the user who installed the app.
- `action` (string) - Required - The action performed, e.g., "installed".
- `user_agent` (string) - Required - The user agent string of the client.
- `user` (object) - Required - Information about the user.
- `created_at` (string) - Required - The timestamp when the installation occurred.
- `integration` (object) - Required - Information about the GitHub App integration.
- `programmatic_access_type` (string) - Optional - The type of programmatic access granted.
- `application_client_id` (string) - Optional - The client ID of the GitHub App.

### Response
#### Success Response (200)
- `message` (string) - Indicates successful processing of the installation event.

#### Response Example
```json
{
  "message": "Integration installed successfully."
}
```
```

```APIDOC
## POST /integration_installation/destroy

### Description
Handles the event when a GitHub App is uninstalled.

### Method
POST

### Endpoint
/integration_installation/destroy

### Parameters
#### Request Body
- `operation_type` (string) - Required - The type of operation performed.
- `name` (string) - Required - The name of the integration.
- `repository_selection` (string) - Required - Specifies how repositories were selected for the installation.
- `user_id` (integer) - Required - The ID of the user who uninstalled the app.
- `action` (string) - Required - The action performed, e.g., "uninstalled".
- `user_agent` (string) - Required - The user agent string of the client.
- `user` (object) - Required - Information about the user.
- `created_at` (string) - Required - The timestamp when the uninstallation occurred.
- `integration` (object) - Required - Information about the GitHub App integration.
- `actor` (object) - Required - Information about the actor performing the uninstallation.
- `programmatic_access_type` (string) - Optional - The type of programmatic access that was removed.
- `application_client_id` (string) - Optional - The client ID of the GitHub App.

### Response
#### Success Response (200)
- `message` (string) - Indicates successful processing of the uninstallation event.

#### Response Example
```json
{
  "message": "Integration uninstalled successfully."
}
```
```

```APIDOC
## POST /integration_installation/repositories_added

### Description
Handles the event when repositories are added to a GitHub App installation.

### Method
POST

### Endpoint
/integration_installation/repositories_added

### Parameters
#### Request Body
- `operation_type` (string) - Required - The type of operation performed.
- `name` (string) - Required - The name of the integration.
- `repository_selection` (string) - Required - Specifies how repositories are selected for the installation.
- `user_id` (integer) - Required - The ID of the user associated with the installation.
- `action` (string) - Required - The action performed, e.g., "repositories_added".
- `user_agent` (string) - Required - The user agent string of the client.
- `user` (object) - Required - Information about the user.
- `created_at` (string) - Required - The timestamp when repositories were added.
- `integration` (object) - Required - Information about the GitHub App integration.
- `actor` (object) - Required - Information about the actor performing the action.
- `repositories_added` (array) - Required - A list of repositories added.
- `repositories_added_names` (array) - Required - A list of names of the repositories added.
- `token_scopes` (array) - Optional - The scopes of the access token.
- `actor_is_bot` (boolean) - Optional - Indicates if the actor is a bot.
- `programmatic_access_type` (string) - Optional - The type of programmatic access granted.
- `application_client_id` (string) - Optional - The client ID of the GitHub App.

### Response
#### Success Response (200)
- `message` (string) - Indicates successful processing of the repositories added event.

#### Response Example
```json
{
  "message": "Repositories added successfully."
}
```
```

```APIDOC
## POST /integration_installation/repositories_removed

### Description
Handles the event when repositories are removed from a GitHub App installation.

### Method
POST

### Endpoint
/integration_installation/repositories_removed

### Parameters
#### Request Body
- `operation_type` (string) - Required - The type of operation performed.
- `name` (string) - Required - The name of the integration.
- `repository_selection` (string) - Required - Specifies how repositories are selected for the installation.
- `user_id` (integer) - Required - The ID of the user associated with the installation.
- `action` (string) - Required - The action performed, e.g., "repositories_removed".
- `user_agent` (string) - Required - The user agent string of the client.
- `user` (object) - Required - Information about the user.
- `created_at` (string) - Required - The timestamp when repositories were removed.
- `integration` (object) - Required - Information about the GitHub App integration.
- `actor` (object) - Required - Information about the actor performing the action.
- `repositories_removed` (array) - Required - A list of repositories removed.
- `repositories_removed_names` (array) - Required - A list of names of the repositories removed.
- `actor_is_bot` (boolean) - Optional - Indicates if the actor is a bot.
- `programmatic_access_type` (string) - Optional - The type of programmatic access that was affected.
- `application_client_id` (string) - Optional - The client ID of the GitHub App.

### Response
#### Success Response (200)
- `message` (string) - Indicates successful processing of the repositories removed event.

#### Response Example
```json
{
  "message": "Repositories removed successfully."
}
```
```

```APIDOC
## POST /integration_installation/suspend

### Description
Handles the event when a GitHub App is suspended.

### Method
POST

### Endpoint
/integration_installation/suspend

### Parameters
#### Request Body
- `operation_type` (string) - Required - The type of operation performed.
- `name` (string) - Required - The name of the integration.
- `repository_selection` (string) - Required - Specifies how repositories are selected for the installation.
- `user_id` (integer) - Required - The ID of the user associated with the installation.
- `action` (string) - Required - The action performed, e.g., "suspended".
- `user_agent` (string) - Required - The user agent string of the client.
- `user` (object) - Required - Information about the user.
- `created_at` (string) - Required - The timestamp when the suspension occurred.
- `integration` (object) - Required - Information about the GitHub App integration.
- `actor` (object) - Required - Information about the actor performing the suspension.
- `request_access_security_header` (string) - Optional - Security header information.
- `application_client_id` (string) - Optional - The client ID of the GitHub App.

### Response
#### Success Response (200)
- `message` (string) - Indicates successful processing of the suspension event.

#### Response Example
```json
{
  "message": "Integration suspended successfully."
}
```
```

```APIDOC
## POST /integration_installation/unsuspend

### Description
Handles the event when a GitHub App is unsuspended.

### Method
POST

### Endpoint
/integration_installation/unsuspend

### Parameters
#### Request Body
- `operation_type` (string) - Required - The type of operation performed.
- `name` (string) - Required - The name of the integration.
- `repository_selection` (string) - Required - Specifies how repositories are selected for the installation.
- `user_id` (integer) - Required - The ID of the user associated with the installation.
- `action` (string) - Required - The action performed, e.g., "unsuspended".
- `user_agent` (string) - Required - The user agent string of the client.
- `user` (object) - Required - Information about the user.
- `created_at` (string) - Required - The timestamp when the unsuspension occurred.
- `integration` (object) - Required - Information about the GitHub App integration.
- `actor` (object) - Required - Information about the actor performing the unsuspension.
- `application_client_id` (string) - Optional - The client ID of the GitHub App.

### Response
#### Success Response (200)
- `message` (string) - Indicates successful processing of the unsuspension event.

#### Response Example
```json
{
  "message": "Integration unsuspended successfully."
}
```
```

```APIDOC
## POST /integration_installation/version_updated

### Description
Handles the event when permissions for a GitHub App are updated.

### Method
POST

### Endpoint
/integration_installation/version_updated

### Parameters
#### Request Body
- `operation_type` (string) - Required - The type of operation performed.
- `name` (string) - Required - The name of the integration.
- `repository_selection` (string) - Required - Specifies how repositories are selected for the installation.
- `user_id` (integer) - Required - The ID of the user associated with the installation.
- `action` (string) - Required - The action performed, e.g., "permissions_updated".
- `user_agent` (string) - Required - The user agent string of the client.
- `user` (object) - Required - Information about the user.
- `created_at` (string) - Required - The timestamp when the permissions were updated.
- `integration` (object) - Required - Information about the GitHub App integration.
- `actor` (object) - Required - Information about the actor performing the update.
- `application_client_id` (string) - Optional - The client ID of the GitHub App.

### Response
#### Success Response (200)
- `message` (string) - Indicates successful processing of the version update event.

#### Response Example
```json
{
  "message": "Integration version updated successfully."
}
```
```

--------------------------------

### Generate Installation Access Token

Source: https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-as-a-github-app-installation

This section describes how to generate an installation access token to authenticate as a GitHub App installation. This token is required before making subsequent API requests.

```APIDOC
## POST /app/installations/{installation_id}/access_tokens

### Description
Generates an installation access token for a GitHub App installation. This token is used to authenticate API requests on behalf of the installation.

### Method
POST

### Endpoint
/app/installations/{installation_id}/access_tokens

### Parameters
#### Path Parameters
- **installation_id** (integer) - Required - The unique identifier of the installation.

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "example": ""
}
```

### Response
#### Success Response (201)
- **token** (string) - The installation access token.
- **expires_at** (string) - The expiration date and time of the token.

#### Response Example
```json
{
  "token": "v1.1f1f7524a1d0b225737d0b656f41736f6c2c636f6d",
  "expires_at": "2023-10-27T10:00:00Z"
}
```
```

--------------------------------

### Authenticate with GITHUB_TOKEN using Octokit in Node.js

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=cli

This workflow demonstrates how to authenticate API requests using the `GITHUB_TOKEN` within a Node.js script. It checks out the repository, sets up Node.js, installs the `octokit` dependency, and runs a script that accesses the token via the `TOKEN` environment variable.

```yaml
on:
  workflow_dispatch:
jobs:
  use_api_via_script:
    runs-on: ubuntu-latest
    permissions:
      issues: read
    steps:
      - name: Check out repo content
        uses: actions/checkout@v5

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '16.17.0'
          cache: npm

      - name: Install dependencies
        run: npm install octokit

      - name: Run script
        run: |
          node .github/actions-scripts/use-the-api.mjs
        env:
          TOKEN: ${{ secrets.GITHUB_TOKEN }}

```

--------------------------------

### Get Repository Webhook Delivery (JavaScript)

Source: https://docs.github.com/en/rest/webhooks/repos

Example using JavaScript to fetch a specific delivery for a repository webhook. This demonstrates making an authenticated GET request to the GitHub API.

```javascript
async function getRepoWebhookDelivery(owner, repo, hookId, deliveryId, token) {
  const url = `https://api.github.com/repos/${owner}/${repo}/hooks/${hookId}/deliveries/${deliveryId}`;
  const response = await fetch(url, {
    method: 'GET',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}
```

--------------------------------

### Get User Information via JavaScript

Source: https://docs.github.com/en/rest/users/users

Example of fetching user data using JavaScript. It utilizes the fetch API to make a GET request to the GitHub API. Requires 'Accept' and 'X-GitHub-Api-Version' headers.

```javascript
async function getUser(username) {
  const response = await fetch(`https://api.github.com/users/${username}`, {
    headers: {
      "Accept": "application/vnd.github+json",
      "X-GitHub-Api-Version": "2022-11-28"
    }
  });
  const data = await response.json();
  console.log(data);
}
```

--------------------------------

### GET /api/PATH with GitHub Token in GitHub Actions

Source: https://docs.github.com/en/rest/overview/other-authentication-methods

This example demonstrates how to make an authenticated GET request to a GitHub API endpoint within a GitHub Actions workflow using `curl` and a `GITHUB_TOKEN`.

```APIDOC
## GET /PATH

### Description
Makes an authenticated GET request to a specified GitHub API path using a GitHub Token.

### Method
GET

### Endpoint
`https://api.github.com/PATH`

### Parameters
#### Query Parameters
None

#### Request Body
None

### Request Example
```yaml
jobs:
  use_api:
    runs-on: ubuntu-latest
    permissions: {}
    steps:
      - env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          curl --request GET \
          --url "https://api.github.com/PATH" \
          --header "Authorization: Bearer $GH_TOKEN"
```

### Response
#### Success Response (200)
- **body** (object) - The API response data.

#### Response Example
```json
{
  "example": "response body"
}
```
```

--------------------------------

### Caching Go Dependencies with setup-go

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

Configures the `setup-go` action to cache Go dependencies. It automatically detects `go.sum` for cache keys but can be customized with `cache-dependency-path` for non-standard locations or multiple dependency files.

```yaml
      - name: Setup Go
        uses: actions/setup-go@v5
        with:
          go-version: '1.17'
          cache-dependency-path: subdir/go.sum

```

```yaml
      - name: Setup Go
        uses: actions/setup-go@v5
        with:
          go-version: '1.17'
          cache-dependency-path: subdir/go.sum

```

--------------------------------

### List GitHub Issues

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Lists open issues for a specified repository. It supports filtering by assignee or author. If run within a local Git repository, the `--repo` flag can be omitted.

```bash
gh issue list --repo OWNER/REPO
gh issue list --assignee "@me"
gh issue list --author monalisa

```

--------------------------------

### Conditional Job Execution with 'if' and Negation

Source: https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

Provides an example of using the 'if' conditional with a negated expression, specifically checking if the GitHub ref does not start with 'refs/tags/'. The `${{ }}` syntax is required when the expression starts with '!' in YAML.

```yaml
if: "${{ ! startsWith(github.ref, 'refs/tags/') }}"

```

--------------------------------

### startRepositoryMigration

Source: https://docs.github.com/en/graphql/reference/mutations

Starts a GitHub Enterprise Importer (GEI) repository migration.

```APIDOC
## startRepositoryMigration

### Description
Starts a GitHub Enterprise Importer (GEI) repository migration.

### Method
POST

### Endpoint
/graphql

### Parameters
#### Query Parameters
None

#### Request Body
- **input** (StartRepositoryMigrationInput!) - Input object for the mutation.

### Request Example
```json
{
  "query": "mutation StartRepositoryMigration($input: StartRepositoryMigrationInput!) { startRepositoryMigration(input: $input) { clientMutationId repositoryMigration { ... } } }",
  "variables": {
    "input": {
      "clientMutationId": "unique-client-mutation-id",
      "repositoryId": "repo-id",
      "targetOrgId": "target-org-id"
    }
  }
}
```

### Response
#### Success Response (200)
- **clientMutationId** (String) - A unique identifier for the client performing the mutation.
- **repositoryMigration** (RepositoryMigration) - The new repository migration.

#### Response Example
```json
{
  "data": {
    "startRepositoryMigration": {
      "clientMutationId": "unique-client-mutation-id",
      "repositoryMigration": {
        "id": "migration-id",
        "state": "IN_PROGRESS"
      }
    }
  }
}
```
```

--------------------------------

### Install Git and GCM on Linux

Source: https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git_platform=windows

General steps for installing Git and Git Credential Manager (GCM) on Linux. Specific installation commands for GCM will vary depending on the Linux distribution. After installation, Git needs to be configured to use GCM.

```shell
Install Git using your distro's packaging system.
Follow instructions in the GCM repo for installation specific to your Linux flavor.
Configure Git to use GCM, referring to GCM Linux documentation for available backing stores.
```

--------------------------------

### Copilot Instructions Prompt for Repository Onboarding

Source: https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot

This markdown prompt is used to instruct the Copilot coding agent on how to onboard a repository. It specifies the goals, limitations, and content to be included in the `.github/copilot-instructions.md` file, aiming to improve the agent's efficiency and reduce errors in code generation and validation.

```markdown
Your task is to "onboard" this repository to Copilot coding agent by adding a .github/copilot-instructions.md file in the repository that contains information describing how a coding agent seeing it for the first time can work most efficiently.

You will do this task only one time per repository and doing a good job can SIGNIFICANTLY improve the quality of the agent's work, so take your time, think carefully, and search thoroughly before writing the instructions.

<Goals>
- Reduce the likelihood of a coding agent pull request getting rejected by the user due to
generating code that fails the continuous integration build, fails a validation pipeline, or
having misbehavior.
- Minimize bash command and build failures.
- Allow the agent to complete its task more quickly by minimizing the need for exploration using grep, find, str_replace_editor, and code search tools.
</Goals>

<Limitations>
- Instructions must be no longer than 2 pages.
- Instructions must not be task specific.
</Limitations>

<WhatToAdd>

Add the following high level details about the codebase to reduce the amount of searching the agent has to do to understand the codebase each time:
<HighLevelDetails>

- A summary of what the repository does.
- High level repository information, such as the size of the repo, the type of the project, the languages, frameworks, or target runtimes in use.
</HighLevelDetails>

Add information about how to build and validate changes so the agent does not need to search and find it each time.
<BuildInstructions>

- For each of bootstrap, build, test, run, lint, and any other scripted step, document the sequence of steps to take to run it successfully as well as the versions of any runtime or build tools used.
- Each command should be validated by running it to ensure that it works correctly as well as any preconditions and postconditions.
- Try cleaning the repo and environment and running commands in different orders and document errors and and misbehavior observed as well as any steps used to mitigate the problem.
- Run the tests and document the order of steps required to run the tests.
- Make a change to the codebase. Document any unexpected build issues as well as the workarounds.
- Document environment setup steps that seem optional but that you have validated are actually required.
- Document the time required for commands that failed due to timing out.
- When you find a sequence of commands that work for a particular purpose, document them in detail.
- Use language to indicate when something should always be done. For example: "always run npm install before building".
- Record any validation steps from documentation.
</BuildInstructions>

List key facts about the layout and architecture of the codebase to help the agent find where to make changes with minimal searching.
<ProjectLayout>

- A description of the major architectural elements of the project, including the relative paths to the main project files, the location
of configuration files for linting, compilation, testing, and preferences.
- A description of the checks run prior to check in, including any GitHub workflows, continuous integration builds, or other validation pipelines.
- Document the steps so that the agent can replicate these itself.
- Any explicit validation steps that the agent can consider to have further confidence in its changes.
- Dependencies that aren't obvious from the layout or file structure.
- Finally, fill in any remaining space with detailed lists of the following, in order of priority: the list of files in the repo root,
the
contents of the README, the contents of any key source files, the list of files in the next level down of directories, giving priority to the more structurally important and snippets of code from key source files, such as the one containing the main method.
</ProjectLayout>
</WhatToAdd>

<StepsToFollow>
- Perform a comprehensive inventory of the codebase. Search for and view:
- README.md, CONTRIBUTING.md, and all other documentation files.
- Search the codebase for build steps and indications of workarounds like 'HACK', 'TODO', etc.
- All scripts, particularly those pertaining to build and repo or environment setup.
- All build and actions pipelines.
- All project files.
- All configuration and linting files.
- For each file:

```

--------------------------------

### Request Parameters

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_tool=curl

Details on the different types of parameters you can use to modify your API requests.

```APIDOC
## Request Parameters

### Description

API methods often require or allow additional information to be sent in your request. There are three main types of parameters: Path, Body, and Query.

#### Path Parameters

- **Description**: Modify the endpoint path. These parameters are **required** in your request.

#### Body Parameters

- **Description**: Allow you to pass additional data to the API. These parameters can be **optional** or **required**, depending on the endpoint. For example, when creating an issue, you can optionally specify assignees or labels.

- **Usage**: Must authenticate your request to pass body parameters.

#### Query Parameters

- **Description**: Parameters appended to the URL after a `?` to filter or modify the request. Their usage and requirements vary by endpoint.
```

--------------------------------

### Define Workflow Steps: Checkout, Install Dependencies, Connect to PostgreSQL (YAML)

Source: https://docs.github.com/en/actions/tutorials/use-containerized-services/create-postgresql-service-containers

This YAML snippet outlines the steps for a GitHub Actions workflow. It includes checking out repository code, installing npm dependencies, and running a Node.js script to connect to a PostgreSQL service. Environment variables `POSTGRES_HOST` and `POSTGRES_PORT` are set to facilitate the connection from the `client.js` script to the running PostgreSQL service container.

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

### Authenticated Request using Curl (Shell)

Source: https://docs.github.com/en/rest/overview/media-types

This example demonstrates how to make an authenticated request to the GitHub REST API using `curl`. It assumes `curl` is installed and an access token has been generated. The example highlights setting up `curl`, choosing an endpoint, and creating authentication credentials by including the token in the `Authorization` header.

```shell
# Example: Replace placeholders with actual values
# curl -H "Authorization: token YOUR_ACCESS_TOKEN" https://api.github.com/some/endpoint
```

--------------------------------

### Install Actions Runner Controller with Helm

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/quickstart-for-actions-runner-controller

Installs the ARC operator and CRDs into a specified Kubernetes namespace using Helm. Ensure the namespace allows access to the Kubernetes API server. This command deploys the latest version; specify a version using the --version flag.

```Bash
NAMESPACE="arc-systems"
helm install arc \
    --namespace "${NAMESPACE}" \
    --create-namespace \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set-controller

```

```Bash
NAMESPACE="arc-systems"
helm install arc \
    --namespace "${NAMESPACE}" \
    --create-namespace \
    oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set-controller

```

--------------------------------

### Example: Setting default run step options for a job

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

An example demonstrating how to set default shell and working directory for run steps within a job.

```APIDOC
### Example: Setting default `run` step options for a job
```yaml
jobs:
  job1:
    runs-on: ubuntu-latest
    defaults:
      run:
        shell: bash
        working-directory: ./scripts

```
```

--------------------------------

### Get GPG Key - Example Response

Source: https://docs.github.com/en/rest/users/gpg-keys

An example of a successful JSON response when retrieving a GPG key for the authenticated user. It includes details such as the key ID, name, public key, and associated emails.

```json
{
  "id": 3,
  "name": "Octocat's GPG Key",
  "primary_key_id": 2,
  "key_id": "3262EFF25BA0D270",
  "public_key": "xsBNBFayYZ...",
  "emails": [
    {
      "email": "octocat@users.noreply.github.com",
      "verified": true
    }
  ],
  "subkeys": [
    {
      "id": 4,
      "primary_key_id": 3,
      "key_id": "4A595D4C72EE49C7",
      "public_key": "zsBNBFayYZ...",
      "emails": [],
      "can_sign": false,
      "can_encrypt_comms": true,
      "can_encrypt_storage": true,
      "can_certify": false,
      "created_at": "2016-03-24T11:31:04-06:00",
      "expires_at": "2016-03-24T11:31:04-07:00",
      "revoked": false
    }
  ],
  "can_sign": true,
  "can_encrypt_comms": false,
  "can_encrypt_storage": false,
  "can_certify": true,
  "created_at": "2016-03-24T11:31:04-06:00",
  "expires_at": "2016-03-24T11:31:04-07:00",
  "revoked": false,
  "raw_key": "-----BEGIN PGP PUBLIC KEY BLOCK-----\nVersion: GnuPG v2\n\nmQENBFayYZ0BCAC4hScoJXXpyR+MXGcrBxElqw3FzCVvkViuyeko+Jp76QJhg8kr\nucRTxbnOoHfda/FmilEa/wxf9ch5/PSrrL26FxEoPHhJolp8fnIDLQeITn94NYdB\nZtnnEKslpPrG97qSUWIchvyqCPtvOb8+8fWvGx9K/ZWcEEdh1X8+WFR2jMENMeoX\nwxHWQoPnS7LpX/85/M7VUcJxvDVfv+eHsnQupmE5bGarKNih0oMe3LbdN3qA5PTz\nSCm6Iudar1VsQ+xTz08ymL7t4pnEtLguQ7EyatFHCjxNblv5RzxoL0tDgN3HqoDz\nc7TEA+q4RtDQl9amcvQ95emnXmZ974u7UkYdABEBAAG0HlNvbWUgVXNlciA8c29t\nZXVzZXJAZ21haWwuY29tPokBOAQTAQIAIgUCVrJhnQIbAwYLCQgHAwIGFQgCCQoL\nBBYCAwECHgECF4AACgkQMmLv8lug0nAViQgArWjI55+7p48URr2z9Jvak+yrBTx1\nzkufltQAnHTJkq+Kl9dySSmTnOop8o3rE4++IOpYV5Y36PkKf9EZMk4n1RQiDPKE\nAFtRVTkRaoWzOir9KQXJPfhKrl01j/QzY+utfiMvUoBJZ9ybq8Pa885SljW9lbaX\nIYw+hl8ZdJ2KStvGrEyfQvRyq3aN5c9TV//4BdGnwx7Qabq/U+G18lizG6f/yq15\ned7t0KELaCfeKPvytp4VE9/z/Ksah/h3+Qilx07/oG2Ae5kC1bEC9coD/ogPUhbv\nb2bsBIoY9E9YwsLoif2lU+o1t76zLgUktuNscRRUKobW028H1zuFS/XQhrkBDQRW\nsmGdAQgApnyyv3i144OLYy0O4UKQxd3e10Y3WpDwfnGIBefAI1m7RxnUxBag/DsU\n7gi9qLEC4VHSfq4eiNfr1LJOyCL2edTgCWFgBhVjbXjZe6YAOrAnhxwCErnN0Y7N\n6s8wVh9fObSOyf8ZE6G7JeKpcq9Q6gd/KxagfD48a1v+fyRHpyQc6J9pUEmtrDJ7\nBjmsd2VWzLBvNWdHyxDNtZweIaqIO9VUYYpr1mtTliNBOZLUelmgrt7HBRcJpWMA\nS8muVVbuP5MK0trLBq/JB8qUH3zRzB/PhMgzmkIfjEK1VYDWm4E8DYyTWEJcHqkb\neqFsNjrIlwPaA122BWC6gUOPwwH+oQARAQABiQEfBBgBAgAJBQJWsmGdAhsMAAoJ\nEDJi7/JboNJwAyAIALd4xcdmGbZD98gScJzqwzkOMcO8zFHqHNvJ42xIFvGny7c0\n1Rx7iyrdypOby5AxE+viQcjG4rpLZW/xKYBNGrCfDyQO7511I0v8x20EICMlMfD/\nNrWQCzesEPcUlKTP07d+sFyP8AyseOidbzY/92CpskTgdSBjY/ntLSaoknl/fjJE\nQM8OkPqU7IraO1Jzzdnm20d5PZL9+PIwIWdSTedU/vBMTJyNcoqvSfKf1wNC66XP\nhqfYgXJE564AdWZKA3C0IyCqiv+LHwxLnUHio1a4/r91C8KPzxs6tGxRDjXLd7ms\nuYFGWymiUGOE/giHlcxdYcHzwLnPDliMQOLiTkK5AQ0EVuxMygEIAOD+bW1cDTmE\nBxh5JECoqeHuwgl6DlLhnubWPkQ4ZeRzBRAsFcEJQlwlJjrzFDicL+lnm6Qq4tt0\n560TwHdf15/AKTZIZu7H25axvGNzgeaUkJEJdYAq9zTKWwX7wKyzBszi485nQg97\nMfAqwhMpDW0Qqf8+7Ug+WEmfBSGv9uL3aQC6WEeIsHfri0n0n8v4XgwhfShXguxO\nCsOztEsuW7WWKW9P4TngKKv4lCHdPlV6FwxeMzODBJvc2fkHVHnqc0PqszJ5xcF8\n6gZCpMM027SbpeYWCAD5zwJyYP9ntfO1p2HjnQ1dZaP9FeNcO7uIV1Lnd1eGCu6I\nsrVp5k1f3isAEQEAAYkCPgQYAQIACQUCVuxMygIbAgEpCRAyYu/yW6DScMBdIAQZ\nAQIABgUCVuxMygAKCRCKohN4dhq2b4tcCACHxmOHVXNpu47OvUGYQydLgMACUlXN\nlj+HfE0VReqShxdDmpasAY9IRpuMB2RsGK8GbNP+4SlOlAiPf5SMhS7nZNkNDgQQ\naZ3HFpgrFmFwmE10BKT4iQtoxELLM57z0qGOAfTsEjWFQa4sF+6IHAQR/ptkdkkI\nBUEXiMnAwVwBysLIJiLO8qdjB6qp52QkT074JVrwywT/P+DkMfC2k4r/AfEbf6eF\ndmPDuPk6KD87+hJZsSa5MaMUBQVvRO/mgEkhJRITVu58eWGaBOcQJ8gqurhCqM5P\nDfUA4TJ7wiqM6sS764vV1rOioTTXkszzhClQqET7hPVnVQjenYgv0EZHNyQH/1f1\n/CYqvV1vFjM9vJjMbxXsATCkZe6wvBVKD8vLsJAr8N+onKQz+4OPc3kmKq7aESu3\nCi/iuie5KKVwnuNhr9AzT61vEkKxwHcVFEvHB77F6ZAAInhRvjzmQbD2dlPLLQCC\nqDj71ODSSAPTEmUy6969bgD9PfWei7kNkBIx7s3eBv8yzytSc2EcuUgopqFazquw\nFs1+tqGHjBvQfTo6bqbJjp/9Ci2pvde3ElV2rAgUlb3lqXyXjRDqrXosh5GcRPQj\nK8Nhj1BNhnrCVskE4BP0LYbOHuzgm86uXwGCFsY+w2VOsSm16Jx5GHyG5S5WU3+D\nIts/HFYRLiFgDLmTlxo=\n=+OzK\n-----END PGP PUBLIC KEY BLOCK-----
```

--------------------------------

### Creating Databases for C/C++ Projects (Make)

Source: https://docs.github.com/en/code-security/codeql-cli/using-the-codeql-cli/creating-codeql-databases

Create a CodeQL database for a C/C++ project that uses `make` as its build system.

```APIDOC
## POST /codeql/database/create/cpp/make

### Description
Creates a CodeQL database for a C/C++ project built using `make`.

### Method
POST

### Endpoint
`/codeql/database/create/cpp/make`

### Parameters
#### Path Parameters
- **database-name** (string) - Required - The name for the C++ database.

#### Query Parameters
- **language** (string) - Required - Must be set to `c-cpp`.
- **command** (string) - Required - The build command, typically `make`.

### Request Example
```bash
codeql database create cpp-database --language=c-cpp --command=make
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation that the database creation command was issued.

#### Response Example
```json
{
  "message": "CodeQL database creation command for C/C++ using make initiated."
}
```
```

--------------------------------

### Start Organization Migration with GitHub CLI

Source: https://docs.github.com/en/rest/migrations/orgs

This example demonstrates initiating an organization migration using the GitHub CLI. It specifies the target organization and provides the migration details, including the repositories to be migrated and the option to lock them. Ensure your GitHub CLI is authenticated.

```bash
gh api --method POST --header 'Accept: application/vnd.github+json' --header 'X-GitHub-Api-Version: 2022-11-28' repos/ORG/migrations --input - <<EOF
{
  "repositories": ["github/Hello-World"],
  "lock_repositories": true
}
EOF
```

--------------------------------

### Get a repository variable example

Source: https://docs.github.com/en/rest/actions/variables

Retrieves a specific repository variable. Requires the repository owner, repository name, and variable name. Returns the variable's name, value, and timestamps.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/actions/variables/NAME
```

```javascript
fetch("https://api.github.com/repos/OWNER/REPO/actions/variables/NAME", {
  method: "GET",
  headers: {
    "Accept": "application/vnd.github+json",
    "Authorization": "Bearer <YOUR-TOKEN>",
    "X-GitHub-Api-Version": "2022-11-28"
  }
})
  .then(response => response.json())
  .then(data => console.log(data));
```

```github-cli
gh api repos/OWNER/REPO/actions/variables/NAME
```

--------------------------------

### Set up multiple Go versions in a workflow (YAML)

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/go

This workflow configures a build job to run with multiple Go versions ('1.19', '1.20', '1.21.x') using a matrix strategy. It utilizes the `actions/checkout@v5` action to check out the repository code and the `actions/setup-go@v5` action to install and set up the specified Go version for each job. A subsequent step demonstrates verifying the installed Go version.

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

### Create Go CodeQL Database with Build Tracing

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Creates a CodeQL database for a Go project by enabling build tracing via the `CODEQL_EXTRACTOR_GO_BUILD_TRACING` environment variable. This method forces CodeQL to limit extraction to files compiled by the build script.

```bash
CODEQL_EXTRACTOR_GO_BUILD_TRACING=on codeql database create go-database --language=go
```

--------------------------------

### Get Code Scanning Default Setup Configuration

Source: https://docs.github.com/en/rest/code-scanning/code-scanning

Retrieves the default setup configuration for code scanning in a repository. Requires 'Administration' repository read permissions. Accepts 'application/vnd.github+json'.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/code-scanning/default-setup
```

```javascript
const owner = "OWNER";
const repo = "REPO";

fetch(`https://api.github.com/repos/${owner}/${repo}/code-scanning/default-setup`, {
  headers: {
    "Accept": "application/vnd.github+json",
    "Authorization": "Bearer <YOUR-TOKEN>",
    "X-GitHub-Api-Version": "2022-11-28"
  }
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

```githubcli
gh api repos/OWNER/REPO/code-scanning/default-setup \
  --jq '.state' \
  --jq '.languages[]' \
  --jq '.query_suite' \
  --jq '.threat_model' \
  --jq '.updated_at' \
  --jq '.schedule'
```

--------------------------------

### Initialize CodeQL Database for Indirect Tracing

Source: https://docs.github.com/en/code-security/codeql-cli/using-the-codeql-cli/creating-codeql-databases

Initializes a CodeQL database and creates scripts to set up an environment for tracing build commands. This is useful when CodeQL CLI autobuilders do not work with your CI workflow. The command requires a path for the new database and the `--begin-tracing` flag.

```bash
codeql database init ... --begin-tracing <database>
```

--------------------------------

### Get route stats by actor - Example JSON Response

Source: https://docs.github.com/en/rest/orgs/api-insights

This is an example JSON response for the 'Get route stats by actor' endpoint when a `200 OK` status is returned. It provides an array of objects, where each object details statistics for a specific API route, including the HTTP method, the route itself, total request counts, rate-limited request counts, and timestamps for the last requests.

```json
[ {
  "http_method": "GET",
  "api_route": "/repositories/:repository_id",
  "total_request_count": 544665,
  "rate_limited_request_count": 13,
  "last_request_timestamp": "2024-09-18T15:43:03Z",
  "last_rate_limited_timestamp": "2024-09-18T06:30:09Z"
} ]
```

--------------------------------

### Create an Issue Example

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=curl

This example shows how to use the GitHub CLI to make a POST request to create an issue in a repository.

```APIDOC
## POST /repos/{owner}/{repo}/issues

### Description
Creates an issue in a specified repository.

### Method
POST

### Endpoint
/repos/{owner}/{repo}/issues

### Parameters
#### Path Parameters
- **owner** (string) - Required - The account owner of the repository.
- **repo** (string) - Required - The name of the repository.

#### Request Body
- **title** (string) - Required - The title of the issue.
- **body** (string) - Optional - The contents of the issue.
- **assignee** (string) - Optional - The username to assign to the issue.
- **milestone** (integer) - Optional - The ID of the milestone to associate with the issue.
- **labels** (array of strings) - Optional - Labels to associate with the issue.
- **assignees** (array of strings) - Optional - Users to assign to the issue.

### Request Example
```shell
gh api --method POST /repos/YOUR_OWNER/YOUR_REPO/issues \
--header 'Accept: application/vnd.github+json' \
--header "X-GitHub-Api-Version: 2022-11-28" \
-f title='My first issue' \
-f body='This is the body of my issue.'
```

### Response
#### Success Response (201)
- **html_url** (string) - URL for the issue.
- **number** (integer) - Issue number.
- **title** (string) - Title of the issue.
```

--------------------------------

### Ineffective Custom Instructions for Copilot

Source: https://docs.github.com/en/copilot/concepts/prompting/response-customization

This example illustrates potentially problematic custom instructions for GitHub Copilot. These instructions, such as referring to external style guides, adopting specific response styles, or imposing strict length constraints, may not yield the desired results, especially in large or diverse repositories.

```markdown
Always conform to the coding styles defined in styleguide.md in repo my-org/my-repo when generating code.

Use @terminal when answering questions about Git.

Answer all questions in the style of a friendly colleague, using informal language.

Answer all questions in less than 1000 characters, and words of no more than 12 characters.

```

--------------------------------

### Initialize Octokit.js with Authentication Token

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=curl

Demonstrates how to create an Octokit instance with a personal access token for authenticated API requests. Ensure 'YOUR-TOKEN' is replaced with your actual token. This is a prerequisite for making authorized calls to the GitHub API.

```javascript
const octokit = new Octokit({
  auth: 'YOUR-TOKEN'
});
```

```javascript
const octokit = new Octokit({
  auth: 'YOUR-TOKEN'
});
```

--------------------------------

### GET /octocat

Source: https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api_tool=cli

This endpoint retrieves information about the authenticated user, often referred to as 'octocat' in examples. It can be used to test authentication and API access.

```APIDOC
## GET /octocat

### Description
Retrieves information about the authenticated user.

### Method
GET

### Endpoint
`/octocat`

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
```json
{
  "headers": {
    "content-type": "text/plain",
    "X-GitHub-Api-Version": "2022-11-28"
  }
}
```

### Response
#### Success Response (200 OK)
- **login** (string) - The username of the authenticated user.
- **id** (integer) - The user ID.

#### Response Example
```json
{
  "login": "octocat",
  "id": 1,
  "avatar_url": "https://github.com/images/icons/icon-80x80.png",
  "name": "The Octocat"
}
```
```

--------------------------------

### Example Output for prepare_job Command (JSON)

Source: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/customizing-the-containers-used-by-jobs

This JSON output represents the state and context after a job has been prepared. It includes network details, container IDs for the job and services, and service port information. This output is typically written to a response file.

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

### Get Repository Installation for Authenticated App

Source: https://docs.github.com/en/rest/apps/apps

Retrieves the installation for a specific repository for the authenticated GitHub App. Requires `owner` and `repo` path parameters. The `Accept` header should be set to `application/vnd.github+json`.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/installation
```

```javascript
async function getRepoInstallation(owner, repo, token) {
  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/installation`, {
    headers: {
      "Accept": "application/vnd.github+json",
      "Authorization": `Bearer ${token}`,
      "X-GitHub-Api-Version": "2022-11-28"
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}
```

```github cli
gh api repos/OWNER/REPO/installation --jq .id
```

--------------------------------

### Get Repository Rule Suite Request Examples

Source: https://docs.github.com/en/rest/repos/rule-suites

Demonstrates how to request repository rule suite details using cURL, JavaScript, and GitHub CLI. These examples show the necessary headers, authentication, and API endpoint. Ensure you replace placeholders like OWNER, REPO, RULE_SUITE_ID, and <YOUR-TOKEN> with your specific values.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/rulesets/rule-suites/RULE_SUITE_ID
```

```javascript
async function getRepoRuleSuite(owner, repo, ruleSuiteId, token) {
  const url = `https://api.github.com/repos/${owner}/${repo}/rulesets/rule-suites/${ruleSuiteId}`;
  const response = await fetch(url, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}

// Example usage:
// const owner = 'OWNER';
// const repo = 'REPO';
// const ruleSuiteId = 'RULE_SUITE_ID';
// const token = '<YOUR-TOKEN>';
// getRepoRuleSuite(owner, repo, ruleSuiteId, token).then(data => console.log(data)).catch(error => console.error(error));
```

```githubcli
gh api repos/OWNER/REPO/rulesets/rule-suites/RULE_SUITE_ID \
  --jq '.id'
```

--------------------------------

### Create CodeQL Database for Bazel Projects

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Creates a CodeQL database for a project built with Bazel. This command includes specific Bazel flags to ensure CodeQL can properly detect the build process by disabling caching and specifying local execution.

```bash
# Navigate to the Bazel workspace.

# Before building, remove cached objects
# and stop all running Bazel server processes.
bazel clean --expunge

# Build using the following Bazel flags, to help CodeQL detect the build:
# `--spawn_strategy=local`: build locally, instead of using a distributed build
# `--nouse_action_cache`: turn off build caching, which might prevent recompilation of source code
# `--noremote_accept_cached`, `--noremote_upload_local_results`: avoid using a remote cache
# `--disk_cache=`: avoid using a disk cache. Note that a disk cache is no longer considered a remote cache as of Bazel 6.
codeql database create new-database --language=<language> \
--command='bazel build --spawn_strategy=local --nouse_action_cache --noremote_accept_cached --noremote_upload_local_results --disk_cache= //path/to/package:target'

# After building, stop all running Bazel server processes.
# This ensures future build commands start in a clean Bazel server process
# without CodeQL attached.
bazel shutdown
```

--------------------------------

### Get User Migration Status - GitHub CLI Example

Source: https://docs.github.com/en/rest/migrations/users

Example of how to retrieve a user migration status using the GitHub CLI. This command requires authentication to be configured and specifies the migration ID.

```bash
gh api user/migrations/MIGRATION_ID
```

--------------------------------

### Explain Command with GitHub Copilot CLI

Source: https://docs.github.com/en/copilot/github-copilot-in-the-cli/using-github-copilot-in-the-cli

This snippet demonstrates how to use the `gh copilot explain` command to get an explanation for a given command. It requires the GitHub CLI and the Copilot in the CLI extension to be installed. The input is a shell command string, and the output is an explanation of that command.

```shell
gh copilot explain "sudo apt-get"
```

--------------------------------

### Start SSH Agent and List Keys (Git Bash/Windows)

Source: https://docs.github.com/en/authentication/troubleshooting-ssh/error-permission-denied-publickey_platform=windows

These commands initiate the SSH agent in the background and then list the SSH keys currently loaded into the agent. This is crucial for ensuring your SSH keys are active and available for use with Git. This example is specific to Git Bash or similar Windows environments.

```shell
# start the ssh-agent in the background
$ eval "$(ssh-agent -s)"
> Agent pid 59566
$ ssh-add -l -E sha256
> 2048 SHA256:274ffWxgaxq/tSINAykStUL7XWyRNcRTlcST1Ei7gBQ /Users/USERNAME/.ssh/id_rsa (RSA)
```

--------------------------------

### Create CodeQL Database for Java with Maven

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Creates a CodeQL database for a Java project built using Maven. This command cleans and installs the project before creating the database.

```bash
codeql database create java-database --language=java-kotlin --command='mvn clean install'
```

--------------------------------

### Get Weekly Commit Count Response Example (JSON)

Source: https://docs.github.com/en/rest/metrics/statistics

This is an example JSON response for the weekly commit count API. The 'all' and 'owner' arrays represent commit counts for each week, ordered from oldest to most recent.

```json
{
  "all": [
    11,
    21,
    15,
    2,
    8,
    1,
    8,
    23,
    17,
    21,
    11,
    10,
    33,
    91,
    38,
    34,
    22,
    23,
    32,
    3,
    43,
    87,
    71,
    18,
    13,
    5,
    13,
    16,
    66,
    27,
    12,
    45,
    110,
    117,
    13,
    8,
    18,
    9,
    19,
    26,
    39,
    12,
    20,
    31,
    46,
    91,
    45,
    10,
    24,
    9,
    29,
    7
  ],
  "owner": [
    3,
    2,
    3,
    0,
    2,
    0,
    5,
    14,
    7,
    9,
    1,
    5,
    0,
    48,
    19,
    2,
    0,
    1,
    10,
    2,
    23,
    40,
    35,
    8,
    8,
    2,
    10,
    6,
    30,
    0,
    2,
    9,
    53,
    104,
    3,
    3,
    10,
    4,
    7,
    11,
    21,
    4,
    4,
    22,
    26,
    63,
    11,
    2,
    14,
    1,
    10,
    3
  ]
}
```

--------------------------------

### Get Enterprise Billing Usage Report - JavaScript

Source: https://docs.github.com/en/rest/enterprise-admin/billing

Example JavaScript code using the GitHub API to retrieve billing usage for an enterprise. This snippet demonstrates making an authenticated GET request.

```javascript
async function getBillingUsage(enterpriseSlug, token) {
  const response = await fetch(`https://api.github.com/enterprises/${enterpriseSlug}/settings/billing/usage`, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}

// Example usage:
// const enterprise = 'YOUR_ENTERPRISE_SLUG';
// const githubToken = 'YOUR_PERSONAL_ACCESS_TOKEN';
// getBillingUsage(enterprise, githubToken)
//   .then(data => console.log(data))
//   .catch(error => console.error('Error fetching billing usage:', error));
```

--------------------------------

### Create CodeQL Database for Java with Ant

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Creates a CodeQL database for a Java project built using Ant. It executes the specified Ant build file.

```bash
codeql database create java-database --language=java-kotlin --command='ant -f build.xml'
```

--------------------------------

### Create Codespace using GitHub CLI (Interactive)

Source: https://docs.github.com/en/codespaces/developing-in-a-codespace/creating-a-codespace-for-a-repository_tool=cli

This command initiates the interactive creation of a codespace. You will be prompted to select a repository, branch, dev container configuration, and machine type. This is useful for users who prefer guided setup or when options are not predetermined.

```bash
gh codespace create

```

--------------------------------

### hashFiles Examples

Source: https://docs.github.com/en/actions/learn-github-actions/expressions

Examples demonstrating the usage of the hashFiles function to match files based on single or multiple patterns.

```APIDOC
## `hashFiles` Examples

### Single Pattern

*   **Description**: Matches any `package-lock.json` file in the repository.
    *   **Usage**: `hashFiles('**/package-lock.json')`

*   **Description**: Matches all `.js` files in the `src` directory at the root level, ignoring subdirectories.
    *   **Usage**: `hashFiles('/src/*.js')`

*   **Description**: Matches all `.rb` files in the `lib` directory at the root level, including subdirectories.
    *   **Usage**: `hashFiles('/lib/**/*.rb')`

### Multiple Patterns

*   **Description**: Creates a hash for `package-lock.json` and `Gemfile.lock` files.
    *   **Usage**: `hashFiles('**/package-lock.json', '**/Gemfile.lock')`

*   **Description**: Matches `.rb` files in `lib` but excludes those in `lib/foo`.
    *   **Usage**: `hashFiles('/lib/**/*.rb', '!/lib/foo/*.rb')`
```

--------------------------------

### Get Self-Hosted Runner Group (JavaScript)

Source: https://docs.github.com/en/rest/actions/self-hosted-runner-groups

Example of retrieving a specific self-hosted runner group for a GitHub organization using JavaScript. This function demonstrates making a GET request to the appropriate API endpoint.

```javascript
async function getRunnerGroup(token, org, runnerGroupId) {
  const response = await fetch(`https://api.github.com/orgs/${org}/actions/runner-groups/${runnerGroupId}`, {
    method: 'GET',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  return await response.json();
}
```

--------------------------------

### Migrate Python Setup and Script Execution from Travis CI to GitHub Actions

Source: https://docs.github.com/en/actions/migrating-to-github-actions/manually-migrating-to-github-actions/migrating-from-travis-ci-to-github-actions

This shows the migration of setting up a Python environment and running a script from Travis CI's syntax to GitHub Actions. It highlights the use of 'uses' for actions like setup-python and 'run' for script execution.

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

### Configure Java Version and Architecture with setup-java Action

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-gradle

This snippet demonstrates how to configure the `setup-java` action in a GitHub Actions workflow to specify a particular Java Development Kit (JDK) version and architecture. It ensures the correct Java runtime is available for building and testing your project. Dependencies include the `actions/checkout` and `actions/setup-java` actions.

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

### Verifying Apex Domain A Records with dig

Source: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

This command-line snippet demonstrates how to verify that your A records are correctly configured for your apex domain using the `dig` utility. Replace EXAMPLE.COM with your actual domain.

```bash
$ dig EXAMPLE.COM +noall +answer -t A
> EXAMPLE.COM    3600    IN A     185.199.108.153
> EXAMPLE.COM    3600    IN A     185.199.109.153
> EXAMPLE.COM    3600    IN A     185.199.110.153
> EXAMPLE.COM    3600    IN A     185.199.111.153
```

--------------------------------

### Configure OIDC Claims with System-Generated GUIDs (JSON)

Source: https://docs.github.com/en/actions/reference/security/oidc

This configuration snippet enables predictable OIDC claims using system-generated GUIDs, such as `repository_id` or `repository_owner_id`. These GUIDs remain consistent even if the entity is renamed. Submit this configuration via API to your cloud provider's OIDC setup, specifically in the `sub` condition.

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

### Install npm dependencies using `npm ci`

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

This snippet demonstrates how to install Node.js dependencies using `npm ci`. This command is generally faster than `npm install` and is recommended for CI environments as it installs versions directly from the `package-lock.json` or `npm-shrinkwrap.json` file, ensuring reliable builds. It requires Node.js to be set up using `actions/setup-node@v4`.

```YAML
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

### Get Organization Installation (GitHub CLI)

Source: https://docs.github.com/en/rest/apps/apps

Retrieves installation information for a GitHub App within a specific organization using the GitHub CLI. This command-line approach simplifies the process of interacting with the GitHub API.

```bash
gh api /orgs/ORG/installation
```

--------------------------------

### Initializing CodeQL Action with Custom Configuration File

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

This section explains how to use the `config-file` parameter to specify a custom YAML configuration file for CodeQL analysis. It also details how to merge additional packs or queries from the workflow with those defined in the configuration file using the `+` prefix.

```APIDOC
## POST /github/codeql-action/init@v3 (with config-file)

### Description
Initializes the CodeQL action using a specified custom configuration file. Allows merging workflow-defined packs/queries with those in the configuration file.

### Method
POST

### Endpoint
/github/codeql-action/init@v3

### Parameters
#### Request Body
- **config-file** (string) - Required - Path to the custom configuration file (e.g., `./.github/codeql/codeql-config.yml`). Can reference files in external repositories using `OWNER/REPOSITORY/FILENAME@BRANCH` syntax.
- **queries** (string) - Optional - Additional queries or suites to run. Prefix with `+` to merge with `config-file` settings.
- **packs** (string) - Optional - Additional packs to run. Prefix with `+` to merge with `config-file` settings.
- **external-repository-token** (string) - Optional - Token for accessing private external repositories containing configuration files or queries.

### Request Example
```yaml
- uses: github/codeql-action/init@v3
  with:
    config-file: "./.github/codeql/codeql-config.yml"
    queries: "+security-and-quality,octo-org/python-qlpack/show_ifs.ql@main"
    packs: "+scope/pack1,scope/pack2@1.2.3,scope/pack3@4.5.6:path/to/queries"
```

### Response
#### Success Response (200)
No specific response body is detailed for this action, it primarily configures the environment for subsequent steps.

#### Response Example
(No example provided)
```

--------------------------------

### Get Repository Commits - cURL Example

Source: https://docs.github.com/en/rest/commits/commits

This example shows how to use cURL to fetch commits for a specific repository. It requires authentication with a GitHub token and specifies the API version. The output is a JSON object containing commit details.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/commits/REF
```

--------------------------------

### Download CodeQL Database from GitHub via GitHub CLI

Source: https://docs.github.com/en/code-security/codeql-cli/using-the-advanced-functionality-of-the-codeql-cli/advanced-setup-of-the-codeql-cli

This command downloads a CodeQL database for a specified language from a repository using the GitHub CLI and the REST API. The downloaded database is saved as a zip archive to a local path. The `Accept` header is crucial for receiving the database as a zip file.

```bash
gh api /repos/<owner>/<repo>/code-scanning/codeql/databases/<language> -H 'Accept: application/zip' > path/to/local/database.zip
```

--------------------------------

### Install Git and GCM on Linux

Source: https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git_platform=mac

General steps to install Git and Git Credential Manager (GCM) on Linux. Installation methods for both Git and GCM vary depending on the Linux distribution. After installation, Git needs to be configured to use GCM, potentially with different backing stores.

```shell
# 1. Install Git using your distro's package manager (e.g., apt, yum, dnf).
# 2. Install GCM following instructions from the GCM repository.
# 3. Configure Git to use GCM (refer to GCM Linux docs for backing store options).
```

--------------------------------

### Direct Download of CodeQL Packs

Source: https://docs.github.com/en/code-security/codeql-cli/codeql-cli-reference/about-codeql-packs

This command allows you to download CodeQL packs directly without immediately running them. This is useful for offline analysis or pre-downloading dependencies. The syntax follows the pattern of specifying scope, name, version, and path.

```bash
echo $OCTO-ORG_ACCESS_TOKEN | codeql pack download <scope/name@version:path> <scope/name@version:path> ...
```

--------------------------------

### Get Specific App Webhook Delivery Request Example

Source: https://docs.github.com/en/rest/apps/webhooks

Shows how to retrieve details for a specific webhook delivery for a GitHub App using its ID. Requires JWT authentication. Examples provided for cURL and JavaScript.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/app/hook/deliveries/DELIVERY_ID
```

```javascript
fetch('https://api.github.com/app/hook/deliveries/DELIVERY_ID', {
  method: 'GET',
  headers: {
    'Accept': 'application/vnd.github+json',
    'Authorization': 'Bearer <YOUR-TOKEN>',
    'X-GitHub-Api-Version': '2022-11-28'
  }
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

--------------------------------

### Get All Organization Repository Rulesets - JavaScript Request

Source: https://docs.github.com/en/rest/orgs/rules

Example JavaScript code to fetch all repository rulesets for an organization using the GitHub API. This snippet demonstrates making a GET request with necessary headers and handling the response.

```javascript
async function getOrgRulesets(orgName, token) {
  const url = `https://api.github.com/orgs/${orgName}/rulesets`;
  const headers = {
    "Accept": "application/vnd.github+json",
    "Authorization": `Bearer ${token}`,
    "X-GitHub-Api-Version": "2022-11-28"
  };

  try {
    const response = await fetch(url, {
      method: "GET",
      headers: headers
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    console.log(JSON.stringify(data, null, 2));
    return data;
  } catch (error) {
    console.error("Error fetching organization rulesets:", error);
    return null;
  }
}

// Example usage:
// const org = "YOUR_ORG_NAME";
// const githubToken = "YOUR_GITHUB_TOKEN";
// getOrgRulesets(org, githubToken);
```

--------------------------------

### Specifying CodeQL Queries by Name and Version

Source: https://docs.github.com/en/code-security/codeql-cli/codeql-cli-reference/about-codeql-packs

Demonstrates various ways to reference CodeQL query packs and specific queries within them. This includes specifying the pack name, version constraints (exact, compatible), and paths to query suites or directories.

```text
codeql/python-queries
codeql/python-queries@1.2.3
codeql/python-queries@~1.2.3
codeql/python-queries:Functions
codeql/python-queries@1.2.3:Functions
codeql/python-queries@1.2.3:codeql-suites/python-code-scanning.qls
suites/my-suite.qls
```

--------------------------------

### Create C# CodeQL Database with Dotnet Build

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Creates a CodeQL database for a C# project using `dotnet build`. It is advised to include `/t:rebuild` to ensure all code is built, or perform a `dotnet clean` beforehand.

```bash
codeql database create csharp-database --language=csharp --command='dotnet build /t:rebuild'
```

--------------------------------

### Get Repository README for Directory - JavaScript

Source: https://docs.github.com/en/rest/repos/contents

Example JavaScript request using the Octokit library to retrieve a README file from a specific directory within a repository. Allows specifying media types for raw content or HTML rendering.

```javascript
const { Octokit } = require("@octokit/core");
const octokit = new Octokit({ auth: "YOUR-TOKEN" });

async function getDirectoryReadme() {
  try {
    const response = await octokit.request('GET /repos/{owner}/{repo}/readme/{dir}', {
      owner: 'OWNER',
      repo: 'REPO',
      dir: 'DIR',
      headers: {
        'Accept': 'application/vnd.github.raw+json',
        'X-GitHub-Api-Version': '2022-11-28'
      }
    });
    console.log(response.data);
  } catch (error) {
    console.error(error);
  }
}

getDirectoryReadme();
```

--------------------------------

### Get Shared Storage Billing (JavaScript)

Source: https://docs.github.com/en/rest/billing/billing

Example of how to retrieve shared storage billing information for a GitHub user using JavaScript. This code snippet demonstrates making an authenticated GET request to the GitHub API.

```javascript
async function getSharedStorageBilling(username, token) {
  const response = await fetch(`https://api.github.com/users/${username}/settings/billing/shared-storage`, {
    method: 'GET',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}

// Example usage:
// const username = 'USERNAME';
// const token = '<YOUR-TOKEN>';
// getSharedStorageBilling(username, token).then(data => console.log(data)).catch(error => console.error(error));
```

--------------------------------

### Enable Specific Languages in Local Server

Source: https://docs.github.com/en/contributing/setting-up-your-environment-to-work-on-github-docs/creating-a-local-environment

Example of how to modify the `start` script in `package.json` to enable specific languages for the local server. This involves setting the `ENABLED_LANGUAGES` environment variable.

```json
"start": "ENABLED_LANGUAGES='en,ja,pt' node script.js"
```

--------------------------------

### Get Repository File Contents (GitHub CLI)

Source: https://docs.github.com/en/rest/repos/contents

Example of how to retrieve the contents of a file in a GitHub repository using the GitHub CLI. This command directly interacts with the GitHub API and requires authentication to be set up in the CLI.

```shell
gh api repos/OWNER/REPO/contents/PATH --header 'Accept: application/vnd.github.object' --header 'X-GitHub-Api-Version: 2022-11-28'
```

--------------------------------

### Example GitHub API Response for Repository Permissions

Source: https://docs.github.com/en/rest/apps/installations

This JSON object represents a successful API response (Status: 200) detailing repository information and the access permissions a user has to it. The `permissions` key, though not explicitly shown in this truncated example, would contain the user's access level.

```json
{
  "total_count": 1,
  "repositories": [
    {
      "id": 1296269,
      "node_id": "MDEwOlJlcG9zaXRvcnkxMjk2MjY5",
      "name": "Hello-World",
      "full_name": "octocat/Hello-World",
      "owner": {
        "login": "octocat",
        "id": 1,
        "node_id": "MDQ6VXNlcjE=",
        "avatar_url": "https://github.com/images/error/octocat_happy.gif",
        "gravatar_id": "",
        "url": "https://api.github.com/users/octocat",
        "html_url": "https://github.com/octocat",
        "followers_url": "https://api.github.com/users/octocat/followers",
        "following_url": "https://api.github.com/users/octocat/following{/other_user}",
        "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
        "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
        "organizations_url": "https://api.github.com/users/octocat/orgs",
        "repos_url": "https://api.github.com/users/octocat/repos",
        "events_url": "https://api.github.com/users/octocat/events{/privacy}",
        "received_events_url": "https://api.github.com/users/octocat/received_events",
        "type": "User",
        "site_admin": false
      },
      "private": false,
      "html_url": "https://github.com/octocat/Hello-World",
      "description": "This your first repo!",
      "fork": false,
      "url": "https://api.github.com/repos/octocat/Hello-World",
      "archive_url": "https://api.github.com/repos/octocat/Hello-World/{archive_format}{/ref}",
      "assignees_url": "https://api.github.com/repos/octocat/Hello-World/assignees{/user}",
      "blobs_url": "https://api.github.com/repos/octocat/Hello-World/git/blobs{/sha}",
      "branches_url": "https://api.github.com/repos/octocat/Hello-World/branches{/branch}",
      "collaborators_url": "https://api.github.com/repos/octocat/Hello-World/collaborators{/collaborator}",
      "comments_url": "https://api.github.com/repos/octocat/Hello-World/comments{/number}",
      "commits_url": "https://api.github.com/repos/octocat/Hello-World/commits{/sha}",
      "compare_url": "https://api.github.com/repos/octocat/Hello-World/compare/{base}...{head}",
      "contents_url": "https://api.github.com/repos/octocat/Hello-World/contents/{+path}",
      "contributors_url": "https://api.github.com/repos/octocat/Hello-World/contributors",
      "deployments_url": "https://api.github.com/repos/octocat/Hello-World/deployments",
      "downloads_url": "https://api.github.com/repos/octocat/Hello-World/downloads",
      "events_url": "https://api.github.com/repos/octocat/Hello-World/events",
      "forks_url": "https://api.github.com/repos/octocat/Hello-World/forks",
      "git_commits_url": "https://api.github.com/repos/octocat/Hello-World/git/commits{/sha}",
      "git_refs_url": "https://api.github.com/repos/octocat/Hello-World/git/refs{/sha}",
      "git_tags_url": "https://api.github.com/repos/octocat/Hello-World/git/tags{/sha}",
      "git_url": "git:github.com/octocat/Hello-World.git",
      "issue_comment_url": "https://api.github.com/repos/octocat/Hello-World/issues/comments{/number}",
      "issue_events_url": "https://api.github.com/repos/octocat/Hello-World/issues/events{/number}",
      "issues_url": "https://api.github.com/repos/octocat/Hello-World/issues{/number}",
      "keys_url": "https://api.github.com/repos/octocat/Hello-World/keys{/key_id}",
      "labels_url": "https://api.github.com/repos/octocat/Hello-World/labels{/name}",
      "languages_url": "https://api.github.com/repos/octocat/Hello-World/languages",
      "merges_url": "https://api.github.com/repos/octocat/Hello-World/merges",
      "milestones_url": "https://api.github.com/repos/octocat/Hello-World/milestones{/number}",
      "notifications_url": "https://api.github.com/repos/octocat/Hello-World/notifications{?since,all,participating}",
      "pulls_url": "https://api.github.com/repos/octocat/Hello-World/pulls{/number}",
      "releases_url": "https://api.github.com/repos/octocat/Hello-World/releases{/id}",
      "ssh_url": "git@github.com:octocat/Hello-World.git",
      "stargazers_url": "https://api.github.com/repos/octocat/Hello-World/stargazers",
      "statuses_url": "https://api.github.com/repos/octocat/Hello-World/statuses/{sha}",
      "subscribers_url": "https://api.github.com/repos/octocat/Hello-World/subscribers",
      "subscription_url": "https://api.github.com/repos/octocat/Hello-World/subscription",
      "tags_url": "https://api.github.com/repos/octocat/Hello-World/tags",
      "teams_url": "https://api.github.com/repos/octocat/Hello-World/teams",
      "trees_url": "https://api.github.com/repos/octocat/Hello-World/git/trees{/sha}",
      "clone_url": "https://github.com/octocat/Hello-World.git",
      "mirror_url": "git:git.example.com/octocat/Hello-World",
      "hooks_url": "https://api.github.com/repos/octocat/Hello-World/hooks",
      "svn_url": "https://svn.github.com/octocat/Hello-World",
      "homepage": "https://github.com",
      "language": null,
      "forks_count": 9,
      "stargazers_count": 80,
      "watchers_count": 80,
      "size": 108,
      "default_branch": "master",
      "open_issues_count": 0,
      "is_template": true,
      "topics": [
        "octocat",
        "atom",
        "electron",
        "api"
      ],
      "has_issues": true,
      "has_projects": true
    }
  ]
}
```

--------------------------------

### Install Project Dependencies

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/building-ci-checks-with-a-github-app

Installs all the necessary Ruby gems for the project as defined in the Gemfile. This command reads the Gemfile.lock to ensure reproducible builds.

```shell
bundle install

```

--------------------------------

### GET /repos/{owner}/{repo}/pulls

Source: https://docs.github.com/en/rest/pulls/pulls

Retrieves a list of pull requests for a given repository. Supports cURL, JavaScript, and GitHub CLI examples.

```APIDOC
## GET /repos/{owner}/{repo}/pulls

### Description
This endpoint retrieves a list of pull requests for a specified GitHub repository. It allows filtering and sorting of the pull requests based on various parameters.

### Method
GET

### Endpoint
/repos/{owner}/{repo}/pulls

### Parameters
#### Path Parameters
- **owner** (string) - Required - The owner of the repository.
- **repo** (string) - Required - The name of the repository.

#### Query Parameters
- **state** (string) - Optional - The state of the pull requests to return. Possible values are `open`, `closed`, and `all`. Defaults to `open`.
- **sort** (string) - Optional - The property to sort the results by. Possible values are `created`, `updated`, `popularity`, and `long-running`. Defaults to `created`.
- **direction** (string) - Optional - The direction of the sort. Possible values are `asc` and `desc`. Defaults to `desc`.
- **count** (integer) - Optional - The number of results to retrieve per page. Maximum value is 100. Defaults to 30.
- **page** (integer) - Optional - The page number of the results to retrieve.

### Request Example
```json
{
  "example": "curl -L \
  -H \"Accept: application/vnd.github+json\" \
  -H \"Authorization: Bearer <YOUR-TOKEN>\" \
  -H \"X-GitHub-Api-Version: 2022-11-28\" \
  https://api.github.com/repos/OWNER/REPO/pulls"
}
```

### Response
#### Success Response (200)
- **url** (string) - The URL of the pull request.
- **id** (integer) - The unique identifier of the pull request.
- **node_id** (string) - The GraphQL node ID of the pull request.
- **html_url** (string) - The URL to the pull request on GitHub.
- **diff_url** (string) - The URL to the diff of the pull request.
- **patch_url** (string) - The URL to the patch of the pull request.
- **issue_url** (string) - The URL to the issue associated with the pull request.
- **state** (string) - The current state of the pull request (`open` or `closed`).
- **locked** (boolean) - Indicates if the pull request is locked.
- **title** (string) - The title of the pull request.
- **user** (object) - Information about the user who created the pull request.
- **body** (string) - The body text of the pull request.
- **created_at** (string) - The timestamp when the pull request was created.
- **updated_at** (string) - The timestamp when the pull request was last updated.
- **closed_at** (string) - The timestamp when the pull request was closed.
- **merged_at** (string) - The timestamp when the pull request was merged.
- **merge_commit_sha** (string) - The SHA of the merge commit.
- **assignee** (object) - Information about the user assigned to the pull request.
- **assignees** (array) - A list of users assigned to the pull request.
- **requested_reviewers** (array) - A list of users requested for review.
- **requested_teams** (array) - A list of teams requested for review.
- **labels** (array) - A list of labels associated with the pull request.
- **milestone** (object) - Information about the milestone associated with the pull request.
- **commits_url** (string) - The URL to the commits associated with the pull request.
- **review_comments_url** (string) - The URL to the review comments for the pull request.
- **review_comment_url** (string) - The URL to a specific review comment.
- **comments_url** (string) - The URL to the comments on the pull request.
- **statuses_url** (string) - The URL to the statuses of the commit.
- **head** (object) - Information about the head branch of the pull request.
- **base** (object) - Information about the base branch of the pull request.
- **_links** (object) - Links to related resources.

#### Response Example
```json
{
  "example": "{\"url\": \"https://api.github.com/repos/OWNER/REPO/pulls/1\", \"id\": 123456789, \"node_id\": \"PR_kwDO....\", \"html_url\": \"https://github.com/OWNER/REPO/pull/1\", \"diff_url\": \"https://github.com/OWNER/REPO/pull/1.diff\", \"patch_url\": \"https://github.com/OWNER/REPO/pull/1.patch\", \"issue_url\": \"https://api.github.com/repos/OWNER/REPO/issues/1\", \"state\": \"open\", \"locked\": false, \"title\": \"Fix: Resolve login issue\", \"user\": {\"login\": \"octocat\", \"id\": 1, \"node_id\": \"MDQ6VXNlcjE=\", \"avatar_url\": \"https://avatars.githubusercontent.com/u/1?v=4\", \"html_url\": \"https://github.com/octocat\", \"type\": \"User\"}, \"body\": \"This PR fixes the login issue reported in #1.\", \"created_at\": \"2023-01-01T12:00:00Z\", \"updated_at\": \"2023-01-01T12:00:00Z\", \"closed_at\": null, \"merged_at\": null, \"merge_commit_sha\": null, \"assignee\": null, \"assignees\": [], \"requested_reviewers\": [], \"requested_teams\": [], \"labels\": [], \"milestone\": null, \"commits_url\": \"https://api.github.com/repos/OWNER/REPO/pulls/1/commits\", \"review_comments_url\": \"https://api.github.com/repos/OWNER/REPO/pulls/1/comments\", \"review_comment_url\": \"https://api.github.com/repos/OWNER/REPO/pulls/comments{/number}\", \"comments_url\": \"https://api.github.com/repos/OWNER/REPO/issues/1/comments\", \"statuses_url\": \"https://api.github.com/repos/OWNER/REPO/statuses/abcdef1234567890abcdef1234567890abcdef12\", \"head\": {\"label\": \"octocat:fix-login\", \"ref\": \"fix-login\", \"sha\": \"abcdef1234567890abcdef1234567890abcdef12\", \"user\": {\"login\": \"octocat\"}, \"repo\": {}}, \"base\": {\"label\": \"OWNER:main\", \"ref\": \"main\", \"sha\": \"fedcba0987654321fedcba0987654321fedcba09\", \"user\": {\"login\": \"OWNER\"}, \"repo\": {}}, \"_links\": {\"self\": {\"href\": \"https://api.github.com/repos/OWNER/REPO/pulls/1\"}, \"html\": {\"href\": \"https://github.com/OWNER/REPO/pull/1\"}, \"issue\": {\"href\": \"https://api.github.com/repos/OWNER/REPO/issues/1\"}, \"comments\": {\"href\": \"https://api.github.com/repos/OWNER/REPO/issues/1/comments\"}, \"review_comments\": {\"href\": \"https://api.github.com/repos/OWNER/REPO/pulls/1/comments\"}, \"review_comment\": {\"href\": \"https://api.github.com/repos/OWNER/REPO/pulls/comments{/number}\"}, \"commits\": {\"href\": \"https://api.github.com/repos/OWNER/REPO/pulls/1/commits\"}, \"attachments\": {\"href\": \"https://api.github.com/repos/OWNER/REPO/pulls/1/attachments\"}, \"statuses\": {\"href\": \"https://api.github.com/repos/OWNER/REPO/statuses/abcdef1234567890abcdef1234567890abcdef12\"}}}"
}
```
```

--------------------------------

### Authenticate Installation with Octokit.rb

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/building-ci-checks-with-a-github-app

Initializes an Octokit client authenticated as a specific installation of a GitHub App. It uses a client already authenticated as the app to create an installation access token using the installation ID from a webhook payload. The generated token is then used to initialize the installation client.

```ruby
def authenticate_installation(payload)
  installation_id = payload['installation']['id']
  installation_token = @app_client.create_app_installation_access_token(installation_id)[:token]
  @installation_client = Octokit::Client.new(bearer_token: installation_token)
end
```

--------------------------------

### Authenticate GitHub App Installation (Ruby)

Source: https://docs.github.com/en/apps/creating-github-apps/guides/creating-ci-tests-with-the-checks-api

This method authenticates a GitHub App installation by retrieving an installation ID and generating an access token. It then initializes an Octokit client with this token for further API interactions. Dependencies include the Octokit gem.

```ruby
def authenticate_installation(payload)
  @installation_id = payload['installation']['id']
  @installation_token = @app_client.create_app_installation_access_token(@installation_id)[:token]
  @installation_client = Octokit::Client.new(bearer_token: @installation_token)
end
```

--------------------------------

### Installation Access Tokens API

Source: https://docs.github.com/en/apps/creating-github-apps/setting-up-a-github-app/best-practices-for-creating-a-github-app

This section describes the use of installation access tokens, which are used to make API requests on behalf of an app installation. These tokens attribute activity to the app itself and are useful for automations.

```APIDOC
## Installation Access Tokens

### Description
Installation access tokens are used to make API requests on behalf of an app installation. They attribute activity to your app and are ideal for automations that act independently of users. Generating these tokens requires your app's private key.

### Method
POST

### Endpoint
`/app/installations/{installation_id}/access_tokens`

### Parameters
#### Path Parameters
- **installation_id** (integer) - Required - The unique identifier of the installation.

#### Request Body
N/A

### Request Example
```
POST /app/installations/12345678/access_tokens
```

### Response
#### Success Response (200 OK)
- **token** (string) - The installation access token.
- **expires_at** (string) - The expiration date and time of the token in ISO 8601 format.

#### Response Example
```json
{
  "token": "gho_xxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "expires_at": "2023-12-31T23:59:59Z"
}
```
```

--------------------------------

### Interactively Configure Features

Source: https://docs.github.com/en/actions/migrating-to-github-actions/automated-migrations/supplemental-arguments-and-settings

Use the `configure --features` command for an interactive setup of feature flags. This command guides you through enabling or disabling features and automatically updates your environment variables.

```shell
$ gh actions-importer configure --features

```

```shell
✔ Which features would you like to configure?: actions/cache, reusable-workflows
✔ actions/cache (disabled): Enable
? reusable-workflows (disabled):
› Enable
  Disable

```

--------------------------------

### Install Ruby Dependencies with Bundler

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/ruby

Installs Ruby dependencies using Bundler. The `setup-ruby` action automatically manages Bundler installation based on your `gemfile.lock`. If no lockfile is present, the latest compatible version is installed.

```yaml
steps:
- uses: actions/checkout@v5
- uses: ruby/setup-ruby@ec02537da5712d66d4d50a0f33b7eb52773b5ed1
  with:
    ruby-version: '3.1'
- run: bundle install

```

--------------------------------

### Get Repository Code Security Configuration (API Response Example)

Source: https://docs.github.com/en/rest/code-security/configurations

This snippet shows an example JSON response when successfully retrieving the code security configuration for a repository. It includes details about the repository's current security status and associated metadata. This is useful for understanding the structure of the data returned by the API.

```json
[ { "status": "attached", "repository": { "value": { "id": 1296269, "node_id": "MDEwOlJlcG9zaXRvcnkxMjk2MjY5", "name": "Hello-World", "full_name": "octocat/Hello-World", "owner": { "login": "octocat", "id": 1, "node_id": "MDQ6VXNlcjE=", "avatar_url": "https://github.com/images/error/octocat_happy.gif", "gravatar_id": "", "url": "https://api.github.com/users/octocat", "html_url": "https://github.com/octocat", "followers_url": "https://api.github.com/users/octocat/followers", "following_url": "https://api.github.com/users/octocat/following{/other_user}", "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}", "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}", "subscriptions_url": "https://api.github.com/users/octocat/subscriptions", "organizations_url": "https://api.github.com/users/octocat/orgs", "repos_url": "https://api.github.com/users/octocat/repos", "events_url": "https://api.github.com/users/octocat/events{/privacy}", "received_events_url": "https://api.github.com/users/octocat/received_events", "type": "User", "site_admin": false }, "private": false, "html_url": "https://github.com/octocat/Hello-World", "description": "This your first repo!", "fork": false, "url": "https://api.github.com/repos/octocat/Hello-World", "archive_url": "https://api.github.com/repos/octocat/Hello-World/{archive_format}{/ref}", "assignees_url": "https://api.github.com/repos/octocat/Hello-World/assignees{/user}", "blobs_url": "https://api.github.com/repos/octocat/Hello-World/git/blobs{/sha}", "branches_url": "https://api.github.com/repos/octocat/Hello-World/branches{/branch}", "collaborators_url": "https://api.github.com/repos/octocat/Hello-World/collaborators{/collaborator}", "comments_url": "https://api.github.com/repos/octocat/Hello-World/comments{/number}", "commits_url": "https://api.github.com/repos/octocat/Hello-World/commits{/sha}", "compare_url": "https://api.github.com/repos/octocat/Hello-World/compare/{base}...{head}", "contents_url": "https://api.github.com/repos/octocat/Hello-World/contents/{+path}", "contributors_url": "https://api.github.com/repos/octocat/Hello-World/contributors", "deployments_url": "https://api.github.com/repos/octocat/Hello-World/deployments", "downloads_url": "https://api.github.com/repos/octocat/Hello-World/downloads", "events_url": "https://api.github.com/repos/octocat/Hello-World/events", "forks_url": "https://api.github.com/repos/octocat/Hello-World/forks", "git_commits_url": "https://api.github.com/repos/octocat/Hello-World/git/commits{/sha}", "git_refs_url": "https://api.github.com/repos/octocat/Hello-World/git/refs{/sha}", "git_tags_url": "https://api.github.com/repos/octocat/Hello-World/git/tags{/sha}", "git_url": "git:github.com/octocat/Hello-World.git", "issue_comment_url": "https://api.github.com/repos/octocat/Hello-World/issues/comments{/number}", "issue_events_url": "https://api.github.com/repos/octocat/Hello-World/issues/events{/number}", "issues_url": "https://api.github.com/repos/octocat/Hello-World/issues{/number}", "keys_url": "https://api.github.com/repos/octocat/Hello-World/keys{/key_id}", "labels_url": "https://api.github.com/repos/octocat/Hello-World/labels{/name}", "languages_url": "https://api.github.com/repos/octocat/Hello-World/languages", "merges_url": "https://api.github.com/repos/octocat/Hello-World/merges", "milestones_url": "https://api.github.com/repos/octocat/Hello-World/milestones{/number}", "notifications_url": "https://api.github.com/repos/octocat/Hello-World/notifications{?since,all,participating}", "pulls_url": "https://api.github.com/repos/octocat/Hello-World/pulls{/number}", "releases_url": "https://api.github.com/repos/octocat/Hello-World/releases{/id}", "ssh_url": "git@github.com:octocat/Hello-World.git", "stargazers_url": "https://api.github.com/repos/octocat/Hello-World/stargazers", "statuses_url": "https://api.github.com/repos/octocat/Hello-World/statuses/{sha}", "subscribers_url": "https://api.github.com/repos/octocat/Hello-World/subscribers", "subscription_url": "https://api.github.com/repos/octocat/Hello-World/subscription", "tags_url": "https://api.github.com/repos/octocat/Hello-World/tags", "teams_url": "https://api.github.com/repos/octocat/Hello-World/teams", "trees_url": "https://api.github.com/repos/octocat/Hello-World/git/trees{/sha}", "hooks_url": "http://api.github.com/repos/octocat/Hello-World/hooks" } } } ]
```

--------------------------------

### Make GitHub API Request and View Headers (curl)

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_apiversion=2022-11-28&apiversion=2022-11-28&apiversion=2022-11-28&tool=cli

This example demonstrates how to make a GET request to the GitHub API to retrieve issues from a repository and display the response code and headers. It uses the `curl` command with the `--include` or `-i` option. Custom headers like `x-ratelimit-remaining` provide rate limiting information.

```shell
gh api \
--header 'Accept: application/vnd.github+json' \
--method GET /repos/octocat/Spoon-Knife/issues \
-F per_page=2 --include
```

```shell
curl --request GET \
--url "https://api.github.com/repos/octocat/Spoon-Knife/issues?per_page=2" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer YOUR-TOKEN" \
--include
```

--------------------------------

### GET /repos/{owner}/{repo}/code-scanning/default-setup

Source: https://docs.github.com/en/rest/code-scanning/code-scanning

Retrieves the code scanning default setup configuration for a repository. This configuration determines the default behavior for code scanning.

```APIDOC
## Get a code scanning default setup configuration

Gets a code scanning default setup configuration.

OAuth app tokens and personal access tokens (classic) need the `repo` scope to use this endpoint with private or public repositories, or the `public_repo` scope to use this endpoint with only public repositories.

### Method
GET

### Endpoint
`/repos/{owner}/{repo}/code-scanning/default-setup`

### Parameters
#### Path Parameters
- **owner** (string) - Required - The account owner of the repository. The name is not case sensitive.
- **repo** (string) - Required - The name of the repository. The name is not case sensitive.

### Request Example
```json
{
  "example": "GET /repos/octocat/Hello-World/code-scanning/default-setup"
}
```

### Response
#### Success Response (200)
- **repository** (object) - Information about the repository and its code scanning setup.
  - **id** (integer) - Unique identifier for the repository.
  - **node_id** (string) - GraphQL Node ID of the repository.
  - **name** (string) - The name of the repository.
  - **full_name** (string) - The full name of the repository (owner/name).
  - **owner** (object) - Information about the repository owner.
    - **login** (string) - The username of the owner.
    - **id** (integer) - The user ID of the owner.
    - **node_id** (string) - GraphQL Node ID of the owner.
    - **avatar_url** (string) - URL of the owner's avatar.
    - **gravatar_id** (string) - Gravatar ID of the owner.
    - **url** (string) - URL of the owner's API endpoint.
    - **html_url** (string) - URL of the owner's profile page.
    - **followers_url** (string) - URL to the owner's followers.
    - **following_url** (string) - URL to the owner's following list.
    - **gists_url** (string) - URL to the owner's gists.
    - **starred_url** (string) - URL to the owner's starred repositories.
    - **subscriptions_url** (string) - URL to the owner's subscriptions.
    - **organizations_url** (string) - URL to the owner's organizations.
    - **repos_url** (string) - URL to the owner's repositories.
    - **events_url** (string) - URL to the owner's events.
    - **received_events_url** (string) - URL to the owner's received events.
    - **type** (string) - The type of the owner (e.g., 'User').
    - **site_admin** (boolean) - Whether the owner is a site administrator.
  - **private** (boolean) - Whether the repository is private.
  - **html_url** (string) - URL of the repository's homepage.
  - **description** (string) - The description of the repository.
  - **fork** (boolean) - Whether the repository is a fork.
  - **url** (string) - URL of the repository's API endpoint.
  - **archive_url** (string) - URL for accessing repository archives.
  - **assignees_url** (string) - URL for accessing repository assignees.
  - **blobs_url** (string) - URL for accessing repository blobs.
  - **branches_url** (string) - URL for accessing repository branches.
  - **collaborators_url** (string) - URL for accessing repository collaborators.
  - **comments_url** (string) - URL for accessing repository comments.
  - **commits_url** (string) - URL for accessing repository commits.
  - **compare_url** (string) - URL for comparing branches.
  - **contents_url** (string) - URL for accessing repository contents.
  - **contributors_url** (string) - URL for accessing repository contributors.
  - **deployments_url** (string) - URL for accessing repository deployments.
  - **downloads_url** (string) - URL for accessing repository downloads.
  - **events_url** (string) - URL for accessing repository events.
  - **forks_url** (string) - URL for accessing repository forks.
  - **git_commits_url** (string) - URL for accessing repository git commits.
  - **git_refs_url** (string) - URL for accessing repository git refs.
  - **git_tags_url** (string) - URL for accessing repository git tags.
  - **issue_comment_url** (string) - URL for accessing issue comments.
  - **issue_events_url** (string) - URL for accessing issue events.
  - **issues_url** (string) - URL for accessing issues.
  - **keys_url** (string) - URL for accessing repository keys.
  - **labels_url** (string) - URL for accessing repository labels.
  - **languages_url** (string) - URL for accessing repository languages.
  - **merges_url** (string) - URL for accessing repository merges.
  - **milestones_url** (string) - URL for accessing repository milestones.
  - **notifications_url** (string) - URL for accessing repository notifications.
  - **pulls_url** (string) - URL for accessing repository pulls.
  - **releases_url** (string) - URL for accessing repository releases.
  - **stargazers_url** (string) - URL for accessing repository stargazers.
  - **statuses_url** (string) - URL for accessing repository statuses.
  - **subscribers_url** (string) - URL for accessing repository subscribers.
  - **subscription_url** (string) - URL for accessing repository subscription.
  - **tags_url** (string) - URL for accessing repository tags.
  - **teams_url** (string) - URL for accessing repository teams.
  - **trees_url** (string) - URL for accessing repository git trees.
  - **hooks_url** (string) - URL for accessing repository hooks.
  - **analysis_status** (string) - The status of the code scanning analysis.
  - **artifact_size_in_bytes** (integer) - The size of the code scanning artifact in bytes.
  - **result_count** (integer) - The number of code scanning results found.
  - **database_commit_sha** (string) - The SHA of the commit associated with the code scanning results.
  - **source_location_prefix** (string) - The prefix for source locations in the code scanning results.
  - **artifact_url** (string) - The URL to download the code scanning artifact.

#### Response Example
```json
{
  "repository": {
    "id": 1296269,
    "node_id": "MDEwOlJlcG9zaXRvcnkxMjk2MjY5",
    "name": "Hello-World",
    "full_name": "octocat/Hello-World",
    "owner": {
      "login": "octocat",
      "id": 1,
      "node_id": "MDQ6VXNlcjE=",
      "avatar_url": "https://github.com/images/error/octocat_happy.gif",
      "gravatar_id": "",
      "url": "https://api.github.com/users/octocat",
      "html_url": "https://github.com/octocat",
      "followers_url": "https://api.github.com/users/octocat/followers",
      "following_url": "https://api.github.com/users/octocat/following{/other_user}",
      "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
      "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
      "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
      "organizations_url": "https://api.github.com/users/octocat/orgs",
      "repos_url": "https://api.github.com/users/octocat/repos",
      "events_url": "https://api.github.com/users/octocat/events{/privacy}",
      "received_events_url": "https://api.github.com/users/octocat/received_events",
      "type": "User",
      "site_admin": false
    },
    "private": false,
    "html_url": "https://github.com/octocat/Hello-World",
    "description": "This your first repo!",
    "fork": false,
    "url": "https://api.github.com/repos/octocat/Hello-World",
    "archive_url": "https://api.github.com/repos/octocat/Hello-World/{archive_format}{/ref}",
    "assignees_url": "https://api.github.com/repos/octocat/Hello-World/assignees{/user}",
    "blobs_url": "https://api.github.com/repos/octocat/Hello-World/git/blobs{/sha}",
    "branches_url": "https://api.github.com/repos/octocat/Hello-World/branches{/branch}",
    "collaborators_url": "https://api.github.com/repos/octocat/Hello-World/collaborators{/collaborator}",
    "comments_url": "https://api.github.com/repos/octocat/Hello-World/comments{/number}",
    "commits_url": "https://api.github.com/repos/octocat/Hello-World/commits{/sha}",
    "compare_url": "https://api.github.com/repos/octocat/Hello-World/compare/{base}...{head}",
    "contents_url": "https://api.github.com/repos/octocat/Hello-World/contents/{+path}",
    "contributors_url": "https://api.github.com/repos/octocat/Hello-World/contributors",
    "deployments_url": "https://api.github.com/repos/octocat/Hello-World/deployments",
    "downloads_url": "https://api.github.com/repos/octocat/Hello-World/downloads",
    "events_url": "https://api.github.com/repos/octocat/Hello-World/events",
    "forks_url": "https://api.github.com/repos/octocat/Hello-World/forks",
    "git_commits_url": "https://api.github.com/repos/octocat/Hello-World/git/commits{/sha}",
    "git_refs_url": "https://api.github.com/repos/octocat/Hello-World/git/refs{/sha}",
    "git_tags_url": "https://api.github.com/repos/octocat/Hello-World/git/tags{/sha}",
    "issue_comment_url": "https://api.github.com/repos/octocat/Hello-World/issues/comments{/number}",
    "issue_events_url": "https://api.github.com/repos/octocat/Hello-World/issues/events{/number}",
    "issues_url": "https://api.github.com/repos/octocat/Hello-World/issues{/number}",
    "keys_url": "https://api.github.com/repos/octocat/Hello-World/keys{/key_id}",
    "labels_url": "https://api.github.com/repos/octocat/Hello-World/labels{/name}",
    "languages_url": "https://api.github.com/repos/octocat/Hello-World/languages",
    "merges_url": "https://api.github.com/repos/octocat/Hello-World/merges",
    "milestones_url": "https://api.github.com/repos/octocat/Hello-World/milestones{/number}",
    "notifications_url": "https://api.github.com/repos/octocat/Hello-World/notifications{?since,all,participating}",
    "pulls_url": "https://api.github.com/repos/octocat/Hello-World/pulls{/number}",
    "releases_url": "https://api.github.com/repos/octocat/Hello-World/releases{/id}",
    "stargazers_url": "https://api.github.com/repos/octocat/Hello-World/stargazers",
    "statuses_url": "https://api.github.com/repos/octocat/Hello-World/statuses/{sha}",
    "subscribers_url": "https://api.github.com/repos/octocat/Hello-World/subscribers",
    "subscription_url": "https://api.github.com/repos/octocat/Hello-World/subscription",
    "tags_url": "https://api.github.com/repos/octocat/Hello-World/tags",
    "teams_url": "https://api.github.com/repos/octocat/Hello-World/teams",
    "trees_url": "https://api.github.com/repos/octocat/Hello-World/git/trees{/sha}",
    "hooks_url": "https://api.github.com/repos/octocat/Hello-World/hooks"
  },
  "analysis_status": "succeeded",
  "artifact_size_in_bytes": 12345,
  "result_count": 532,
  "database_commit_sha": "2d870c2a717a524627af38fa2da382188a096f90",
  "source_location_prefix": "/",
  "artifact_url": "https://example.com"
}
```
```

--------------------------------

### Get Secret Scanning Alert - JavaScript Request

Source: https://docs.github.com/en/rest/secret-scanning/secret-scanning_apiversion=2022-11-28

Example JavaScript code to fetch a secret scanning alert using the GitHub API. This snippet demonstrates how to make a GET request with appropriate headers for authentication and API versioning.

```javascript
async function getSecretScanningAlert(owner, repo, alertNumber, token) {
  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/secret-scanning/alerts/${alertNumber}`, {
    method: 'GET',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}

// Example usage:
// const owner = 'OWNER';
// const repo = 'REPO';
// const alertNumber = 1;
// const token = '<YOUR-TOKEN>';
// getSecretScanningAlert(owner, repo, alertNumber, token).then(alert => console.log(alert)).catch(error => console.error(error));
```

--------------------------------

### Docker ENTRYPOINT Shell Form Example

Source: https://docs.github.com/en/actions/creating-actions/dockerfile-support-for-github-actions

This example demonstrates the shell form of the Docker ENTRYPOINT instruction, which allows for environment variable substitution. It's recommended when args from the action's metadata file need to be processed with environment variables.

```dockerfile
ENTRYPOINT ["sh", "-c", "echo $GITHUB_SHA"]
```

--------------------------------

### Create User Project (JavaScript)

Source: https://docs.github.com/en/rest/projects-classic/projects

Example of creating a user project using JavaScript. It demonstrates how to use the fetch API to create a new project for the authenticated user.

```javascript
async function createUserProject() {
  const response = await fetch('https://api.github.com/user/projects',
  {
    method: 'POST',
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': 'Bearer <YOUR-TOKEN>',
      'X-GitHub-Api-Version': '2022-11-28'
    },
    body: JSON.stringify({
      name: "My Projects",
      body: "A board to manage my personal projects."
    })
  });
  const data = await response.json();
  console.log(data);
}
```

--------------------------------

### Get Latest Release - JavaScript

Source: https://docs.github.com/en/rest/releases/releases

Example JavaScript request to retrieve the latest release for a repository using the GitHub API. This function would typically use a library like 'axios' or the built-in 'fetch' API to make a GET request.

```javascript
async function getLatestRelease(owner, repo, token) {
  const url = `https://api.github.com/repos/${owner}/${repo}/releases/latest`;
  const headers = {
    'Accept': 'application/vnd.github+json',
    'Authorization': `Bearer ${token}`,
    'X-GitHub-Api-Version': '2022-11-28'
  };

  try {
    const response = await fetch(url, {
      method: 'GET',
      headers: headers
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error getting latest release:', error);
    throw error;
  }
}

// Example Usage:
// const owner = 'OWNER';
// const repo = 'REPO';
// const token = '<YOUR-TOKEN>';
// getLatestRelease(owner, repo, token).then(release => console.log(release));
```

--------------------------------

### Generate README Template for Open-Source Project

Source: https://docs.github.com/en/copilot/tutorials/copilot-chat-cookbook/communicate-effectively/creating-templates

This example demonstrates how to prompt Copilot Chat to create a comprehensive README template for an open-source project. The template includes standard sections like Description, Installation, Usage, Contributing, License, and Contact, designed to be clear and easy to follow.

```markdown
# Project Name

> **Short description:**  
> A brief summary of what your project does, its main features, and its purpose.

---

## Table of Contents

- [Description](#description)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

## Description

Provide a detailed explanation of what your project does, why it exists, and any important background information.  
You may want to include:
- Key features
- Supported platforms or languages
- Screenshots or diagrams

---

## Installation

1. **Clone the repository**
   ```sh
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

2. **Install dependencies**
   ```sh
   # Example for Node.js projects
   npm install

   # Example for Python projects
   pip install -r requirements.txt
   ```

3. **Additional setup**
   - List any other required steps (e.g., environment variables, configuration files)

---

## Usage

Provide clear usage instructions and code examples.

```sh
# Example command
your-command --option value
```

```python
# Example in Python
import your_module

result = your_module.do_something()
print(result)
```

- Explain any CLI options, configuration, or parameters.
- Link to more detailed documentation if available.

---

## Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork the repository**
2. **Create a new branch**
   ```sh
   git checkout -b feature/your-feature-name
   ```
3. **Make your changes**
4. **Test your changes**
5. **Commit and push**
   ```sh
   git commit -m "Add feature: your-feature-name"
   git push origin feature/your-feature-name
   ```
6. **Open a pull request**

**Code of Conduct:**  
Please be respectful and follow our [Code of Conduct](CODE_OF_CONDUCT.md).

**Issues & Suggestions:**  
Open an issue for bugs, questions, or feature requests.

---

## License

This project is licensed under the [INSERT LICENSE](link to relevant license information).

---

## Contact

- **Maintainer:** [Your Name](mailto:your@email.com)
- **Project Link:** https://github.com/your-username/your-repo-name

---

```

--------------------------------

### Authentication

Source: https://docs.github.com/en/rest/using-the-rest-api/getting-started-with-the-rest-api_tool=curl

Understand the different methods for authenticating your API requests to access protected endpoints and receive additional information.

```APIDOC
## Authentication

### Description

Many endpoints require authentication to access or return additional information. Authenticated requests also allow for higher rate limits.

### Authentication Methods

1.  **Personal Access Token**: Create a token with the required scopes or permissions.
2.  **GitHub App Token**: Generate a token using a GitHub App.
3.  **`GITHUB_TOKEN`**: Use the built-in token available in GitHub Actions workflows.
4.  **GitHub CLI**: Use the `gh auth login` command to authenticate.

### Usage

Provide an authentication token with the required scopes or permissions in your request headers.

### Security Warning

Treat your access token with the same care as your passwords or other sensitive credentials.
```

--------------------------------

### Start Just-In-Time (JIT) Runner with Configuration

Source: https://docs.github.com/en/actions/security-guides/using-githubs-security-features-to-secure-your-use-of-github-actions

This snippet demonstrates how to start a self-hosted runner using a configuration obtained from the REST API. The `--jitconfig` flag is used to pass the encoded configuration, ensuring the runner is ephemeral and performs at most one job before removal. This approach enhances runner registration security.

```bash
./run.sh --jitconfig ${encoded_jit_config}

```

--------------------------------

### GET /repositories

Source: https://docs.github.com/en/rest/actions/permissions

Retrieves a list of repositories, potentially with filtering or sorting options. This example shows a response for a successful retrieval.

```APIDOC
## GET /repositories

### Description
Retrieves a list of repositories. This endpoint is used to fetch repository data.

### Method
GET

### Endpoint
/repositories

### Parameters

#### Query Parameters
- **sort** (string) - Optional - Used for sorting results.
- **direction** (string) - Optional - The direction of the sort. Accepted values are `asc` and `desc`.
- **per_page** (integer) - Optional - The number of results per page (max 100). Default: 30.
- **page** (integer) - Optional - Page number of the results to fetch.

### Request Example
(No request body for GET requests)

### Response
#### Success Response (200)
- **total_count** (integer) - The total number of repositories found.
- **repositories** (array) - An array of repository objects.
  - **id** (integer) - Unique identifier for the repository.
  - **name** (string) - The name of the repository.
  - **full_name** (string) - The full name of the repository (owner/name).
  - **owner** (object) - Information about the repository owner.
    - **login** (string) - The username of the owner.
    - **id** (integer) - The unique ID of the owner.
    - **avatar_url** (string) - URL for the owner's avatar.
  - **private** (boolean) - Indicates if the repository is private.
  - **html_url** (string) - URL to the repository on GitHub.
  - **description** (string) - Description of the repository.
  - **forks_count** (integer) - Number of forks.
  - **stargazers_count** (integer) - Number of stars.
  - **watchers_count** (integer) - Number of watchers.
  - **language** (string) - Primary programming language of the repository.
  - **topics** (array of strings) - An array of topics associated with the repository.

#### Response Example
```json
{
  "total_count": 1,
  "repositories": [
    {
      "id": 1296269,
      "node_id": "MDEwOlJlcG9zaXRvcnkxMjk2MjY5",
      "name": "Hello-World",
      "full_name": "octocat/Hello-World",
      "owner": {
        "login": "octocat",
        "id": 1,
        "node_id": "MDQ6VXNlcjE=",
        "avatar_url": "https://github.com/images/error/octocat_happy.gif",
        "gravatar_id": "",
        "url": "https://api.github.com/users/octocat",
        "html_url": "https://github.com/octocat",
        "followers_url": "https://api.github.com/users/octocat/followers",
        "following_url": "https://api.github.com/users/octocat/following{/other_user}",
        "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
        "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
        "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
        "organizations_url": "https://api.github.com/users/octocat/orgs",
        "repos_url": "https://api.github.com/users/octocat/repos",
        "events_url": "https://api.github.com/users/octocat/events{/privacy}",
        "received_events_url": "https://api.github.com/users/octocat/received_events",
        "type": "User",
        "site_admin": false
      },
      "private": false,
      "html_url": "https://github.com/octocat/Hello-World",
      "description": "This your first repo!",
      "fork": false,
      "url": "https://api.github.com/repos/octocat/Hello-World",
      "archive_url": "https://api.github.com/repos/octocat/Hello-World/{archive_format}{/ref}",
      "assignees_url": "https://api.github.com/repos/octocat/Hello-World/assignees{/user}",
      "blobs_url": "https://api.github.com/repos/octocat/Hello-World/git/blobs{/sha}",
      "branches_url": "https://api.github.com/repos/octocat/Hello-World/branches{/branch}",
      "collaborators_url": "https://api.github.com/repos/octocat/Hello-World/collaborators{/collaborator}",
      "comments_url": "https://api.github.com/repos/octocat/Hello-World/comments{/number}",
      "commits_url": "https://api.github.com/repos/octocat/Hello-World/commits{/sha}",
      "compare_url": "https://api.github.com/repos/octocat/Hello-World/compare/{base}...{head}",
      "contents_url": "https://api.github.com/repos/octocat/Hello-World/contents/{+path}",
      "contributors_url": "https://api.github.com/repos/octocat/Hello-World/contributors",
      "deployments_url": "https://api.github.com/repos/octocat/Hello-World/deployments",
      "downloads_url": "https://api.github.com/repos/octocat/Hello-World/downloads",
      "events_url": "https://api.github.com/repos/octocat/Hello-World/events",
      "forks_url": "https://api.github.com/repos/octocat/Hello-World/forks",
      "git_commits_url": "https://api.github.com/repos/octocat/Hello-World/git/commits{/sha}",
      "git_refs_url": "https://api.github.com/repos/octocat/Hello-World/git/refs{/sha}",
      "git_tags_url": "https://api.github.com/repos/octocat/Hello-World/git/tags{/sha}",
      "git_url": "git:github.com/octocat/Hello-World.git",
      "issue_comment_url": "https://api.github.com/repos/octocat/Hello-World/issues/comments{/number}",
      "issue_events_url": "https://api.github.com/repos/octocat/Hello-World/issues/events{/number}",
      "issues_url": "https://api.github.com/repos/octocat/Hello-World/issues{/number}",
      "keys_url": "https://api.github.com/repos/octocat/Hello-World/keys{/key_id}",
      "labels_url": "https://api.github.com/repos/octocat/Hello-World/labels{/name}",
      "languages_url": "https://api.github.com/repos/octocat/Hello-World/languages",
      "merges_url": "https://api.github.com/repos/octocat/Hello-World/merges",
      "milestones_url": "https://api.github.com/repos/octocat/Hello-World/milestones{/number}",
      "notifications_url": "https://api.github.com/repos/octocat/Hello-World/notifications{?since,all,participating}",
      "pulls_url": "https://api.github.com/repos/octocat/Hello-World/pulls{/number}",
      "releases_url": "https://api.github.com/repos/octocat/Hello-World/releases{/id}",
      "ssh_url": "git@github.com:octocat/Hello-World.git",
      "stargazers_url": "https://api.github.com/repos/octocat/Hello-World/stargazers",
      "statuses_url": "https://api.github.com/repos/octocat/Hello-World/statuses/{sha}",
      "subscribers_url": "https://api.github.com/repos/octocat/Hello-World/subscribers",
      "subscription_url": "https://api.github.com/repos/octocat/Hello-World/subscription",
      "tags_url": "https://api.github.com/repos/octocat/Hello-World/tags",
      "teams_url": "https://api.github.com/repos/octocat/Hello-World/teams",
      "trees_url": "https://api.github.com/repos/octocat/Hello-World/git/trees{/sha}",
      "clone_url": "https://github.com/octocat/Hello-World.git",
      "mirror_url": "git:git.example.com/octocat/Hello-World",
      "hooks_url": "https://api.github.com/repos/octocat/Hello-World/hooks",
      "svn_url": "https://svn.github.com/octocat/Hello-World",
      "homepage": "https://github.com",
      "language": null,
      "forks_count": 9,
      "stargazers_count": 80,
      "watchers_count": 80,
      "size": 108,
      "default_branch": "master",
      "open_issues_count": 0,
      "is_template": true,
      "topics": [
        "octocat",
        "atom",
        "electron",
        "api"
      ],
      "has_issues": true,
      "has_projects": true,
      "has_wiki": true,
      "has_pages": false,
      "has_downloads": true,
      "archived": false
    }
  ]
}
```
```

--------------------------------

### Add Multiple Repositories for Export using a File

Source: https://docs.github.com/en/enterprise-server/migrations/using-ghe-migrator/exporting-migration-data-from-github-enterprise-server

To prepare multiple repositories for export simultaneously, create a text file with each repository URL on a new line. Then, use the `ghe-migrator add` command with the `-i` flag followed by the path to your text file.

```shell
ghe-migrator add -i PATH/TO/YOUR/REPOSITORY_URL.txt
```

--------------------------------

### GET /orgs/{org}/copilot/metrics

Source: https://docs.github.com/en/copilot/managing-copilot/managing-github-copilot-in-your-organization/reviewing-activity-related-to-github-copilot-in-your-organization/analyzing-usage-over-time-with-the-copilot-metrics-api

Retrieves Copilot usage metrics for a given organization. The example demonstrates how to fetch this data and append it to a local JSON file.

```APIDOC
## GET /orgs/{org}/copilot/metrics

### Description
Fetches Copilot usage metrics for a specified organization. This endpoint is part of a larger script that saves the data to a local JSON file, preserving historical data.

### Method
GET

### Endpoint
`/orgs/${org}/copilot/metrics`

### Parameters
#### Path Parameters
- **org** (string) - Required - The name of the organization.

#### Query Parameters
None

#### Request Body
None

### Request Example
```javascript
// Authentication and organization details are set globally
const resp = await octokit.request(`GET /orgs/${org}/copilot/metrics`, {
  org: 'ORG',
  headers: {
    'X-GitHub-Api-Version': '2022-11-28'
  }
});

const copilotUsage = resp.data;
```

### Response
#### Success Response (200)
- **data** (array) - An array of objects, where each object contains daily Copilot usage metrics for the organization.

#### Response Example
```json
[
  {
    "date": "2023-01-01",
    "total_suggestions_count": 1000,
    "total_acceptances_count": 500,
    "total_lines_suggested": 2000,
    "total_lines_accepted": 1000,
    "editors_with_copilot": [
      "vscode",
      "vim"
    ],
    "languages": {
      "javascript": {
        "total_suggestions_count": 800,
        "total_acceptances_count": 400,
        "total_lines_suggested": 1600,
        "total_lines_accepted": 800
      },
      "python": {
        "total_suggestions_count": 200,
        "total_acceptances_count": 100,
        "total_lines_suggested": 400,
        "total_lines_accepted": 200
      }
    }
  }
  // ... more daily entries
]
```
```

--------------------------------

### GET /repos/{owner}/{repo}/issues

Source: https://docs.github.com/en/rest/quickstart

This endpoint retrieves a list of issues for a specified repository. It demonstrates how to authenticate requests using an access token via the Authorization header.

```APIDOC
## GET /repos/{owner}/{repo}/issues

### Description
Retrieves a list of issues for a specified repository.

### Method
GET

### Endpoint
https://api.github.com/repos/octocat/Spoon-Knife/issues

### Parameters

#### Query Parameters
None

#### Headers
- **Accept** (string) - Required - Specifies the media type for the response, e.g., `application/vnd.github+json`.
- **Authorization** (string) - Required - Contains the access token for authentication. Format: `Bearer YOUR-TOKEN` or `token YOUR-TOKEN`.

### Request Example
```bash
curl --request GET \
--url "https://api.github.com/repos/octocat/Spoon-Knife/issues" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer YOUR-TOKEN"
```

### Response
#### Success Response (200)
- **Array of Issue Objects** (array) - A list of issue objects.

#### Response Example
```json
[
  {
    "url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1",
    "repository_url": "https://api.github.com/repos/octocat/Spoon-Knife",
    "labels_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/labels{/name}",
    "comments_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/comments",
    "events_url": "https://api.github.com/repos/octocat/Spoon-Knife/issues/1/events",
    "html_url": "https://github.com/octocat/Spoon-Knife/issues/1",
    "id": 1,
    "node_id": "MDU6SXNzdWUx",
    "number": 1,
    "title": "Found a bug",
    "user": {
      "login": "octocat",
      "id": 1,
      "node_id": "MDQ6VXNlcjE=",
      "avatar_url": "https://github.com/images/error/octocat_happy.gif",
      "gravatar_id": "",
      "url": "https://api.github.com/users/octocat",
      "html_url": "https://github.com/octocat",
      "followers_url": "https://api.github.com/users/octocat/followers",
      "following_url": "https://api.github.com/users/octocat/following{/other_user}",
      "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
      "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
      "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
      "organizations_url": "https://api.github.com/users/octocat/orgs",
      "repos_url": "https://api.github.com/users/octocat/repos",
      "events_url": "https://api.github.com/users/octocat/events{/privacy}",
      "received_events_url": "https://api.github.com/users/octocat/received_events",
      "type": "User",
      "site_admin": false
    },
    "state": "open",
    "locked": false,
    "assignee": null,
    "assignees": [],
    "milestone": null,
    "comments": 0,
    "created_at": "2011-04-22T13:33:48Z",
    "updated_at": "2011-04-22T13:33:48Z",
    "closed_at": null,
    "author_association": "OWNER",
    "body": "I am having a problem with this one."
  }
]
```
```

--------------------------------

### Build and Test Node.js Code with setup-node

Source: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs

Sets up a Node.js environment and executes common build and test commands for a Node.js project. It installs dependencies, runs build scripts if present, and executes tests.

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

### Devcontainer JSON Configuration Example

Source: https://docs.github.com/en/codespaces/setting-up-your-project-for-codespaces/adding-a-dev-container-configuration/setting-up-your-python-project-for-codespaces

A sample devcontainer.json file showing essential properties such as name, image, and features. It also includes commented-out examples for forwardPorts, postCreateCommand, customizations, and remoteUser, providing a template for setting up a Python development environment.

```json
{
  "name": "Python 3",
  "image": "mcr.microsoft.com/devcontainers/python:0-3.11-bullseye",
  "features": {
    "ghcr.io/devcontainers-contrib/features/coverage-py:2": {}
  }

  // Features to add to the dev container. More info: https://containers.dev/features.
  // "features": {},

  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  // "forwardPorts": [],

  // Use 'postCreateCommand' to run commands after the container is created.
  // "postCreateCommand": "pip3 install --user -r requirements.txt",

  // Configure tool-specific properties.
  // "customizations": {},

  // Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
  // "remoteUser": "root"
}
```

--------------------------------

### Get Organization Installation (cURL)

Source: https://docs.github.com/en/rest/apps/apps

Retrieves installation information for a GitHub App within a specific organization. Requires an Accept header, Authorization token, and the GitHub API version. The 'org' parameter specifies the target organization.

```shell
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/orgs/ORG/installation
```

--------------------------------

### Using Octokit.js to Interact with GitHub REST API

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=curl

This section explains how to use the Octokit.js library to make authenticated requests to the GitHub REST API from JavaScript scripts or within GitHub Actions.

```APIDOC
## Using Octokit.js

### Description
Octokit.js is a JavaScript library that allows you to interact with the GitHub REST API. This guide covers installation, authentication, and making requests.

### Authentication
1. **Create Access Token**: Generate a personal access token or a GitHub App user access token. Ensure it has the necessary scopes/permissions.
   - **Warning**: Treat your access token like a password.
   - **Security**: Store tokens as secrets in GitHub Actions or as Codespaces secrets for secure usage.

### Installation
Use npm or another package manager to install Octokit:
```bash
npm install octokit
```

### Usage
1. **Import**: Import the `Octokit` class into your JavaScript file.
   ```javascript
   import { Octokit } from "octokit";
   ```
2. **Instantiate**: Create an instance of `Octokit`, providing your authentication token.
   ```javascript
   const octokit = new Octokit({
     auth: 'YOUR-TOKEN'
   });
   ```
3. **Make Requests**: Use the `octokit.request` method with the HTTP method and endpoint path, followed by an object containing parameters.

### Example Request
```javascript
await octokit.request("GET /repos/{owner}/{repo}/issues", {
  owner: "octocat",
  repo: "Spoon-Knife"
});
```

### Parameters
- **Path Parameters**: Defined within the endpoint URL (e.g., `{owner}`, `{repo}`).
- **Query Parameters**: Passed in the second argument object.
- **Request Body**: Passed in the second argument object for methods like POST or PUT.
```

--------------------------------

### Complete Sinatra App for GitHub OAuth in Ruby

Source: https://docs.github.com/en/apps/creating-github-apps/guides/building-a-login-with-github-button-with-a-github-app

An example of a complete Ruby Sinatra application that includes dependencies, credential loading, generating an authorization link, and handling the callback to retrieve the authorization code. This serves as a starting point for implementing GitHub OAuth.

```ruby
require "sinatra"
require "dotenv/load"
require "net/http"
require "json"

CLIENT_ID = ENV.fetch("CLIENT_ID")
CLIENT_SECRET = ENV.fetch("CLIENT_SECRET")

get "/" do
  link = '<a href="https://github.com/login/oauth/authorize?client_id=<%= CLIENT_ID %>">Login with GitHub</a>'
  erb link
end

get "CALLBACK_URL" do
  code = params["code"]
  render = "Successfully authorized! Got code #{code}."
  erb render
end

```

--------------------------------

### Generate Installation Access Token with curl

Source: https://docs.github.com/en/apps/creating-github-apps/authenticating-with-a-github-app/authenticating-as-a-github-app-installation

This snippet demonstrates how to generate an installation access token using a curl command. It requires a pre-generated JSON web token (JWT) and the installation ID. The token is sent in the `Authorization` header. Optionally, repository access and permissions can be specified in the request body. The generated token expires after 1 hour.

```bash
curl --request POST \
--url "https://api.github.com/app/installations/INSTALLATION_ID/access_tokens" \
--header "Accept: application/vnd.github+json" \
--header "Authorization: Bearer JWT" \
--header "X-GitHub-Api-Version: 2022-11-28"

```

--------------------------------

### Get Parent Issue - JavaScript Request Example

Source: https://docs.github.com/en/rest/issues/sub-issues

This example shows how to fetch the parent issue of a sub-issue using JavaScript. It utilizes the 'fetch' API and includes the required 'Accept', 'Authorization', and 'X-GitHub-Api-Version' headers. Remember to substitute placeholders with your specific details.

```javascript
async function getParentIssue(owner, repo, issueNumber, token) {
  const response = await fetch(`https://api.github.com/repos/${owner}/${repo}/issues/${issueNumber}/parent`, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });

  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }

  const data = await response.json();
  return data;
}

// Example usage:
// const owner = 'OWNER';
// const repo = 'REPO';
// const issueNumber = ISSUE_NUMBER;
// const token = '<YOUR-TOKEN>';
//
// getParentIssue(owner, repo, issueNumber, token)
//   .then(issue => console.log(issue))
//   .catch(error => console.error('Error:', error));
```

--------------------------------

### Get Repository Commits - JavaScript Example

Source: https://docs.github.com/en/rest/commits/commits

This example demonstrates fetching repository commits using JavaScript, likely with the `fetch` API. It requires constructing the correct URL and including necessary headers for authentication and API versioning. The response is expected to be JSON.

```javascript
async function getCommits(owner, repo, ref, token) {
  const url = `https://api.github.com/repos/${owner}/${repo}/commits/${ref}`;
  const response = await fetch(url, {
    headers: {
      'Accept': 'application/vnd.github+json',
      'Authorization': `Bearer ${token}`,
      'X-GitHub-Api-Version': '2022-11-28'
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}

// Example usage:
// const owner = 'OWNER';
// const repo = 'REPO';
// const ref = 'REF';
// const token = 'YOUR-TOKEN';
// getCommits(owner, repo, ref, token).then(data => console.log(data)).catch(error => console.error('Error:', error));
```

--------------------------------

### Get Organization Package Example (cURL, JavaScript, GitHub CLI)

Source: https://docs.github.com/en/rest/packages/packages

This snippet demonstrates how to retrieve a specific package within a GitHub organization. It includes examples for cURL, JavaScript, and GitHub CLI, showing the necessary headers and URL structure. The response includes package details such as ID, name, type, owner information, and version count.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/orgs/ORG/packages/PACKAGE_TYPE/PACKAGE_NAME
```

```javascript
// JavaScript example would go here, making a GET request to the API endpoint.
```

```github cli
# GitHub CLI example would go here, using appropriate gh api commands.
```

--------------------------------

### Instantiate Authenticated Octokit Client for Installation

Source: https://docs.github.com/en/apps/creating-github-apps/writing-code-for-a-github-app/building-ci-checks-with-a-github-app

Initializes an Octokit client authenticated as an installation of a GitHub App. This client is used to perform API operations on behalf of the installed app.

```ruby
# Instantiate an Octokit client, authenticated as an installation of a
# GitHub App, to run API operations.

```

--------------------------------

### Create Path-Specific Custom Instructions

Source: https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot_tool=vscode

For instructions tailored to specific files or directories, create files within the `.github/instructions` directory. These files must be named `NAME.instructions.md` and include a `applyTo` frontmatter block specifying glob patterns for the target files or directories.

```markdown
---
applyTo: "app/models/**/*.rb"
---

These are specific instructions for Ruby model files.

```

```markdown
---
applyTo: "**/*.ts,**/*.tsx"
---

These instructions apply to all TypeScript files in the repository.

```

```markdown
---
applyTo: "**"
---

These instructions apply to all files in the repository.

```

--------------------------------

### Execute Language Server

Source: https://docs.github.com/en/code-security/codeql-cli/codeql-cli-manual/execute-language-server

Starts the CodeQL language server, which provides online support for the QL language within IDEs. This command is intended for IDE extensions to run in the background and communicate via a special protocol.

```APIDOC
## codeql execute language-server

### Description
[Plumbing] On-line support for the QL language in IDEs. This command is only relevant for authors of QL language extensions for IDEs. It is started by the IDE extension in the background and communicates with it through a special protocol on its standard input and output streams.

### Method
SHELL

### Endpoint
`codeql execute language-server --check-errors=<checkErrors> <options>...`

### Parameters
#### Primary Options
- **`--check-errors=<checkErrors>`** (string) - Mandatory - How to check errors. One of: ON_CHANGE, EXPLICIT.
- **`--search-path=<dir>[:<dir>...]`** (string) - This works like the similar option to `codeql query compile` (q.v.). There are no `--additional-packs` or `--library-path` options, as the corresponding values are provided online by the IDE extension through the language server protocol. (Note: On Windows the path separator is `;`).
- **`--synchronous`** (boolean) - Carry out actions a single main thread rather than in a threaded executor.

#### Common options
- **`-h, --help`** (boolean) - Show this help text.
- **`-J=<opt>`** (string) - [Advanced] Give option to the JVM running the command. (Beware that options containing spaces will not be handled correctly.)
- **`-v, --verbose`** (boolean) - Incrementally increase the number of progress messages printed.
- **`-q, --quiet`** (boolean) - Incrementally decrease the number of progress messages printed.
- **`--verbosity=<level>`** (string) - [Advanced] Explicitly set the verbosity level to one of errors, warnings, progress, progress+, progress++, progress+++. Overrides `-v` and `-q`.
- **`--logdir=<dir>`** (string) - [Advanced] Write detailed logs to one or more files in the given directory, with generated names that include timestamps and the name of the running subcommand. (To write a log file with a name you have full control over, instead give `--log-to-stderr` and redirect stderr as desired.)
- **`--common-caches=<dir>`** (string) - [Advanced] Controls the location of cached data on disk that will persist between several runs of the CLI, such as downloaded QL packs and compiled query plans. If not set explicitly, this defaults to a directory named `.codeql` in the user's home directory; it will be created if it doesn't already exist. Available since `v2.15.2`.

### Request Example
```json
{
  "command": "codeql execute language-server",
  "arguments": {
    "checkErrors": "ON_CHANGE",
    "searchPath": "/path/to/ql/packs",
    "synchronous": false
  }
}
```

### Response
(This command typically communicates via standard input/output streams with the IDE extension, rather than returning a direct JSON response for success/failure in the traditional sense. The success of the operation is indicated by the language server running and communicating correctly.)

#### Success Response (200)
(N/A - Communication is stream-based)

#### Response Example
(N/A - Communication is stream-based)
```

--------------------------------

### Get Weekly Commit Count Request Example (cURL)

Source: https://docs.github.com/en/rest/metrics/statistics

This snippet demonstrates how to make a cURL request to the GitHub API to get the weekly commit count for a repository. It requires authentication with a personal access token and specifies the API version.

```shell
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/stats/participation
```

--------------------------------

### Get Repository File Contents (JavaScript)

Source: https://docs.github.com/en/rest/repos/contents

Example of how to retrieve the contents of a file in a GitHub repository using JavaScript. This snippet assumes the Octokit SDK is being used and demonstrates setting headers for authentication and API versioning.

```javascript
async () => {
  const octokit = require("@octokit/core").Octokit
  const octo = new octokit({ auth: "YOUR-TOKEN" })

  await octo.request('GET /repos/{owner}/{repo}/contents/{path}', {
    owner: 'OWNER',
    repo: 'REPO',
    path: 'PATH',
    headers: {
      'X-GitHub-Api-Version': '2022-11-28',
      'accept': 'application/vnd.github.object'
    }
  })
}
```

--------------------------------

### GET /app/installations

Source: https://docs.github.com/en/rest/apps/apps

Lists all the repositories accessible by the authenticated GitHub App. This endpoint retrieves a list of integration installation requests, including details about the account and requester, and the creation timestamp.

```APIDOC
## GET /app/installations

### Description
Lists all the repositories accessible by the authenticated GitHub App. This endpoint retrieves a list of integration installation requests, including details about the account and requester, and the creation timestamp.

### Method
GET

### Endpoint
/app/installations

### Parameters
#### Headers
- **Accept** (string) - Required - Setting to `application/vnd.github+json` is recommended.
- **Authorization** (string) - Required - Bearer token for authentication.
- **X-GitHub-Api-Version** (string) - Required - Specifies the API version.

#### Query Parameters
- **per_page** (integer) - Optional - The number of results per page (max 100). Defaults to `30`.
- **page** (integer) - Optional - The page number of the results to fetch. Defaults to `1`.
- **since** (string) - Optional - Only show results that were last updated after the given time. This is a timestamp in ISO 8601 format: `YYYY-MM-DDTHH:MM:SSZ`.
- **outdated** (string) - Optional - Filters results based on outdated status.

### Request Example
```json
{
  "request": "GET /app/installations"
}
```

### Response
#### Success Response (200)
- **id** (integer) - The unique identifier for the installation.
- **node_id** (string) - The GraphQL Node ID for the installation.
- **account** (object) - Information about the account that owns the installation.
  - **login** (string) - The username or organization name.
  - **id** (integer) - The unique identifier for the account.
  - **node_id** (string) - The GraphQL Node ID for the account.
  - **avatar_url** (string) - URL for the account's avatar.
  - **gravatar_id** (string) - Gravatar ID if available.
  - **url** (string) - URL for the account API endpoint.
  - **html_url** (string) - URL for the account's profile page.
  - **followers_url** (string) - URL for the account's followers.
  - **following_url** (string) - URL for the account's following list.
  - **gists_url** (string) - URL for the account's gists.
  - **starred_url** (string) - URL for the account's starred repositories.
  - **subscriptions_url** (string) - URL for the account's subscriptions.
  - **organizations_url** (string) - URL for the account's organizations.
  - **repos_url** (string) - URL for the account's repositories.
  - **events_url** (string) - URL for the account's events.
  - **received_events_url** (string) - URL for the account's received events.
  - **type** (string) - The type of account (e.g., 'Organization', 'User').
  - **site_admin** (boolean) - Whether the account is a site administrator.
- **requester** (object) - Information about the user who requested the installation.
  - **id** (integer) - The unique identifier for the requester.
  - **node_id** (string) - The GraphQL Node ID for the requester.
  - **avatar_url** (string) - URL for the requester's avatar.
  - **gravatar_id** (string) - Gravatar ID if available.
  - **url** (string) - URL for the requester API endpoint.
  - **html_url** (string) - URL for the requester's profile page.
  - **followers_url** (string) - URL for the requester's followers.
  - **following_url** (string) - URL for the requester's following list.
  - **gists_url** (string) - URL for the requester's gists.
  - **starred_url** (string) - URL for the requester's starred repositories.
  - **subscriptions_url** (string) - URL for the requester's subscriptions.
  - **organizations_url** (string) - URL for the requester's organizations.
  - **repos_url** (string) - URL for the requester's repositories.
  - **events_url** (string) - URL for the requester's events.
  - **received_events_url** (string) - URL for the requester's received events.
  - **type** (string) - The type of the requester (e.g., 'User').
  - **site_admin** (boolean) - Whether the requester is a site administrator.
- **created_at** (string) - The timestamp when the installation was created in ISO 8601 format.

#### Response Example
```json
{
  "id": 25381,
  "node_id": "MDEyOkludGVncmF0aW9uMTIzNDU2Nzg5MA==",
  "account": {
    "login": "octo-org",
    "id": 6811672,
    "node_id": "MDEyOk9yZ2FuaXphdGlvbjY4MTE2NzI=",
    "avatar_url": "https://avatars3.githubusercontent.com/u/6811672?v=4",
    "gravatar_id": "",
    "url": "https://api.github.com/users/octo-org",
    "html_url": "https://github.com/octo-org",
    "followers_url": "https://api.github.com/users/octo-org/followers",
    "following_url": "https://api.github.com/users/octo-org/following{/other_user}",
    "gists_url": "https://api.github.com/users/octo-org/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/octo-org/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/octo-org/subscriptions",
    "organizations_url": "https://api.github.com/users/octo-org/orgs",
    "repos_url": "https://api.github.com/users/octo-org/repos",
    "events_url": "https://api.github.com/users/octo-org/events{/privacy}",
    "received_events_url": "https://api.github.com/users/octo-org/received_events",
    "type": "Organization",
    "site_admin": false
  },
  "requester": {
    "id": 1,
    "node_id": "MDQ6VXNlcjE=",
    "avatar_url": "https://github.com/images/error/octocat_happy.gif",
    "gravatar_id": "",
    "url": "https://api.github.com/users/octocat",
    "html_url": "https://github.com/octocat",
    "followers_url": "https://api.github.com/users/octocat/followers",
    "following_url": "https://api.github.com/users/octocat/following{/other_user}",
    "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
    "organizations_url": "https://api.github.com/users/octocat/orgs",
    "repos_url": "https://api.github.com/users/octocat/repos",
    "events_url": "https://api.github.com/users/octocat/events{/privacy}",
    "received_events_url": "https://api.github.com/users/octocat/received_events",
    "type": "User",
    "site_admin": false
  },
  "created_at": "2022-07-08T16:18:44-04:00"
}
```

### Error Handling
- **401 Unauthorized**: Returned if the authenticated user does not have permission to access the endpoint.
- **404 Not Found**: Returned if the resource is not found.
```

--------------------------------

### Authenticate with GitHub App using create-github-app-token in Node.js

Source: https://docs.github.com/en/rest/quickstart

This snippet shows how to authenticate with the GitHub API using a token generated by a GitHub App. It utilizes the 'actions/create-github-app-token' action to create a short-lived installation access token. This token is then used in a Node.js script to interact with the GitHub API. Ensure your App ID and private key (PEM) are stored as repository variables and secrets respectively.

```yaml
on:
  workflow_dispatch:
jobs:
  use_api_via_script:
    runs-on: ubuntu-latest
    steps:
      - name: Check out repo content
        uses: actions/checkout@v5

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '16.17.0'
          cache: npm

      - name: Install dependencies
        run: npm install octokit

      - name: Generate token
        id: generate-token
        uses: actions/create-github-app-token@v2
        with:
          app-id: ${{ vars.APP_ID }}
          private-key: ${{ secrets.APP_PEM }}

      - name: Run script
        run: |
          node .github/actions-scripts/use-the-api.mjs
        env:
          TOKEN: ${{ steps.generate-token.outputs.token }}

```

--------------------------------

### Configure Site Title and Description for GitHub Pages (YAML)

Source: https://docs.github.com/en/pages/quickstart

This snippet demonstrates how to configure the title and description for a GitHub Pages site by editing the `_config.yml` file. This file is used by Jekyll to build the site. Ensure the file is correctly formatted as YAML.

```yaml
theme: jekyll-theme-minimal
title: Octocat's homepage
description: Bookmark this to keep an eye on my project updates!
```

--------------------------------

### Get User Installation for Authenticated App

Source: https://docs.github.com/en/rest/apps/apps

Enables an authenticated GitHub App to find the user’s installation information. Requires a JWT to access this endpoint and the `username` path parameter. The `Accept` header should be set to `application/vnd.github+json`.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/users/USERNAME/installation
```

```javascript
async function getUserInstallation(username, token) {
  const response = await fetch(`https://api.github.com/users/${username}/installation`, {
    headers: {
      "Accept": "application/vnd.github+json",
      "Authorization": `Bearer ${token}`,
      "X-GitHub-Api-Version": "2022-11-28"
    }
  });
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.json();
}
```

```github cli
gh api users/USERNAME/installation --jq .id
```

--------------------------------

### Ruby Sinatra App Setup with GitHub API Libraries

Source: https://docs.github.com/en/apps/creating-github-apps/guides/creating-ci-tests-with-the-checks-api

Initializes a Sinatra web application in Ruby, setting up dependencies for interacting with the GitHub API using Octokit. It also includes dotenv for managing environment variables, JSON for data manipulation, OpenSSL for webhook signature verification, JWT for GitHub App authentication, Time for date formatting, and Logger for debugging.

```ruby
require 'sinatra/base'
require 'octokit'
require 'dotenv/load'
require 'json'
require 'openssl'
require 'jwt'
require 'time'
require 'logger'

# This code is a Sinatra app, for two reasons:
#   1. Because the app will require a landing page for installation.

```

--------------------------------

### Create Global Copilot Instructions File

Source: https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot

This snippet shows how to create a global instructions file for GitHub Copilot at the root of your repository. This file, named `copilot-instructions.md`, allows you to provide natural language instructions that Copilot will consider for all interactions within the repository.

```bash
1. In the root of your repository, create a file named .github/copilot-instructions.md.
Create the .github directory if it does not already exist.
```

--------------------------------

### Build and Test Swift Code with GitHub Actions

Source: https://docs.github.com/en/actions/tutorials/build-and-test-code/swift

This snippet shows how to set up a Swift environment and run build and test commands in a GitHub Actions job. It depends on the `actions/checkout` and `swift-actions/setup-swift` actions. The inputs include the Swift version, and the outputs are the build artifacts and test results.

```YAML
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

### Get User Migration Status - cURL Example

Source: https://docs.github.com/en/rest/migrations/users

Example of how to fetch a user migration status using cURL. Requires setting the Accept and Authorization headers, and specifying the migration ID in the URL. Includes the GitHub API version.

```shell
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/user/migrations/MIGRATION_ID
```

--------------------------------

### Example Complex Query: Octocat/Hello-World Repository

Source: https://docs.github.com/en/graphql/guides/forming-calls-with-graphql

This example demonstrates a complex GraphQL query to retrieve specific information about issues and labels from the 'octocat/Hello-World' repository.

```APIDOC
## Example Query: Octocat/Hello-World Repository

This query retrieves the 20 most recent closed issues from the `octocat/Hello-World` repository and includes the title, URL, and the first 5 labels for each issue.

### Method
GET

### Endpoint
`/graphql`

### Query
```graphql
query {
  repository(owner:"octocat", name:"Hello-World") {
    issues(last:20, states:CLOSED) {
      edges {
        node {
          title
          url
          labels(first:5) {
            edges {
              node {
                name
              }
            }
          }
        }
      }
    }
  }
}
```

### Explanation of Query Composition:

- **`query {`**: The root operation for reading data. If no operation is specified, `query` is the default.
- **`repository(owner:"octocat", name:"Hello-World") {`**: Selects the `repository` object, requiring `owner` and `name` arguments.
- **`issues(last:20, states:CLOSED) {`**: Retrieves `issues` from the repository. Arguments used:
    - `last: 20`: Specifies fetching the last 20 issues.
    - `states: CLOSED`: Filters issues to only include those that are `CLOSED`.
- **`edges {`**: Navigates through the connection to access individual issue data.
- **`node {`**: Accesses the specific `Issue` object.
- **`title`**, **`url`**: Retrieves the title and URL of the issue.
- **`labels(first:5) {`**: Retrieves the first 5 labels associated with the issue.
    - **`edges {`**: Navigates through the label connection.
    - **`node {`**: Accesses the specific `Label` object.
        - **`name`**: Retrieves the name of the label.

### Response Example (Success - 200)
```json
{
  "data": {
    "repository": {
      "issues": {
        "edges": [
          {
            "node": {
              "title": "Example Issue Title",
              "url": "https://github.com/octocat/Hello-World/issues/1",
              "labels": {
                "edges": [
                  {
                    "node": {
                      "name": "bug"
                    }
                  }
                ]
              }
            }
          }
        ]
      }
    }
  }
}
```
```

--------------------------------

### Get Code Scanning Alert Request Example

Source: https://docs.github.com/en/rest/code-scanning/code-scanning

This snippet demonstrates how to retrieve a specific code scanning alert from a GitHub repository. It includes the necessary API endpoint and headers for authentication and versioning. The example utilizes cURL for the request.

```curl
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/repos/OWNER/REPO/code-scanning/alerts/ALERT_NUMBER
```

--------------------------------

### SSH Key File Save Prompt (macOS Example)

Source: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent_platform=linux

Example prompt for saving the SSH key file on macOS. Pressing Enter accepts the default file location.

```text
> Enter a file in which to save the key (/Users/YOU/.ssh/id_ed25519_sk): [Press enter]
```

--------------------------------

### Set Up CLI Action with JavaScript

Source: https://docs.github.com/en/actions/how-tos/create-and-publish-actions/create-a-cli-action

This JavaScript code snippet demonstrates how to create a GitHub Action to set up a CLI. It uses the `actions/core` and `actions/tool-cache` packages to get the version input, download the CLI tool, extract it, and add it to the system's PATH. Ensure you replace `getDownloadURL()` with your actual download URL function.

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

### Get billing usage report for a user - Response Example

Source: https://docs.github.com/en/rest/billing/enhanced-billing

Example JSON response when successfully retrieving a user's billing usage report. It includes an array of usage items, each detailing date, product, quantity, price, and repository.

```json
{ "usageItems": [ { "date": "2023-08-01", "product": "Actions", "sku": "Actions Linux", "quantity": 100, "unitType": "minutes", "pricePerUnit": 0.008, "grossAmount": 0.8, "discountAmount": 0, "netAmount": 0.8, "repositoryName": "user/example" } ] }
```

--------------------------------

### Start SSH Agent and List Keys (Other Terminals)

Source: https://docs.github.com/en/authentication/troubleshooting-ssh/error-permission-denied-publickey_platform=windows

These commands initiate the SSH agent in the background and then list the SSH keys currently loaded into the agent. This is crucial for ensuring your SSH keys are active and available for use with Git. This example is for terminals other than Git Bash, such as standard Linux/macOS terminals.

```shell
# start the ssh-agent in the background
$ eval $(ssh-agent -s)
> Agent pid 59566
```

```shell
$ ssh-add -l -E sha256
> 2048 SHA256:274ffWxgaxq/tSINAykStUL7XWyRNcRTlcST1Ei7gBQ /Users/USERNAME/.ssh/id_rsa (RSA)
```

--------------------------------

### List Repository Security Advisories (JavaScript)

Source: https://docs.github.com/en/rest/security-advisories/repository-advisories

Example using JavaScript (with the Octokit library) to list security advisories for a repository. This demonstrates how to make authenticated requests to the GitHub API. Ensure you have the 'octokit' library installed (`npm install octokit`).

```javascript
import { Octokit } from "@octokit/core";

const octokit = new Octokit({
  auth: "YOUR-TOKEN"
});

async function listSecurityAdvisories() {
  try {
    const response = await octokit.request('GET /repos/{owner}/{repo}/security-advisories', {
      owner: 'OWNER',
      repo: 'REPO',
      headers: {
        'X-GitHub-Api-Version': '2022-11-28',
        'Accept': 'application/vnd.github+json'
      }
    });
    console.log(response.data);
  } catch (error) {
    console.error('Error fetching security advisories:', error);
  }
}

listSecurityAdvisories();
```

--------------------------------

### Switch GitHub CLI Accounts

Source: https://docs.github.com/en/github-cli/github-cli/quickstart

Manage authentication for multiple GitHub accounts on the same platform using the `gh auth switch` command. This command facilitates seamless switching between different authenticated accounts.

```shell
gh auth switch
```

--------------------------------

### POST /user/codespaces/{codespace_name}/start - Start a codespace for the authenticated user

Source: https://docs.github.com/en/rest/codespaces

Starts a stopped codespace.

```APIDOC
## POST /user/codespaces/{codespace_name}/start

### Description
Starts a codespace for the authenticated user.

### Method
POST

### Endpoint
/user/codespaces/{codespace_name}/start

### Parameters
#### Path Parameters
- **codespace_name** (string) - Required - The name of the codespace.

### Response
#### Success Response (202)
- No content
```

--------------------------------

### REST API - Getting User Followers

Source: https://docs.github.com/en/rest/overview/about-githubs-apis

This example shows how to get the login of a user's followers using the REST API. It requires an initial request to retrieve the followers, and potentially subsequent requests for each follower's details.

```APIDOC
## REST API - Getting User Followers

### Description
Retrieves the login of a user's followers. This is often the first step in a multi-request process to gather detailed follower information.

### Method
GET

### Endpoint
/user/followers

### Parameters
#### Path Parameters
None

#### Query Parameters
- **username** (String) - The username of the user whose followers you want to retrieve.

### Request Example
```bash
curl \
  https://api.github.com/user/followers \
  -H "Accept: application/vnd.github.v3+json"
```

### Response
#### Success Response (200)
- **login** (String) - The username of the follower.
- Other fields pertaining to the follower.

#### Response Example
```json
[
  {
    "login": "follower1",
    "id": 12345,
    "node_id": "MDQ6VXNlcjEyMzQ1",
    "avatar_url": "https://avatars.github.usercontent.com/u/12345?v=4",
    "gravatar_id": "",
    "url": "https://api.github.com/users/follower1",
    "html_url": "https://github.com/follower1",
    "followers_url": "https://api.github.com/users/follower1/followers",
    "following_url": "https://api.github.com/users/follower1/following{/other_user}",
    "gists_url": "https://api.github.com/users/follower1/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/follower1/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/follower1/subscriptions",
    "organizations_url": "https://api.github.com/users/follower1/orgs",
    "repos_url": "https://api.github.com/users/follower1/repos",
    "events_url": "https://api.github.com/users/follower1/events{/privacy}",
    "received_events_url": "https://api.github.com/users/follower1/received_events",
    "type": "User",
    "site_admin": false
  }
]
```

--------------------------------

### Create CodeQL Database with Custom Build Script

Source: https://docs.github.com/en/code-security/codeql-cli/getting-started-with-the-codeql-cli/preparing-your-code-for-codeql-analysis

Creates a CodeQL database for a project using a custom build script. This script should contain all necessary commands to build the project for CodeQL analysis.

```bash
codeql database create new-database --language=<language> --command='./scripts/build.sh'
```

--------------------------------

### Initialize Octokit.js with Authentication Token

Source: https://docs.github.com/en/rest/quickstart_apiversion=2022-11-28&tool=cli

This code shows how to initialize the Octokit.js client for interacting with the GitHub REST API. It requires an authentication token, which can be a personal access token or a GitHub App user access token. The token should be stored securely, for example, as a GitHub secret.

```javascript
const octokit = new Octokit({
  auth: 'YOUR-TOKEN'
});

```

--------------------------------

### GET /websites/github_en

Source: https://docs.github.com/en/rest/code-scanning/code-scanning

Retrieves default response details for the GitHub API, including example responses and schemas.

```APIDOC
## GET /websites/github_en

### Description
Retrieves default response details for the GitHub API.

### Method
GET

### Endpoint
/websites/github_en

### Parameters
#### Path Parameters
None

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **id** (integer) - The ID of the controller repository.
- **controller_repo** (object) - Details of the controller repository.
  - **id** (integer) - Repository ID.
  - **node_id** (string) - Node ID of the repository.
  - **name** (string) - Repository name.
  - **full_name** (string) - Full name of the repository (owner/name).
  - **owner** (object) - Information about the repository owner.
    - **login** (string) - Owner's username.
    - **id** (integer) - Owner's ID.
    - **node_id** (string) - Owner's node ID.
    - **avatar_url** (string) - URL to the owner's avatar.
    - **gravatar_id** (string) - Owner's Gravatar ID.
    - **url** (string) - API URL for the owner.
    - **html_url** (string) - HTML URL for the owner.
    - **followers_url** (string) - URL to retrieve followers.
    - **following_url** (string) - URL to retrieve following information.
    - **gists_url** (string) - URL to retrieve gists.
    - **starred_url** (string) - URL to retrieve starred repositories.
    - **subscriptions_url** (string) - URL to retrieve subscriptions.
    - **organizations_url** (string) - URL to retrieve organizations.
    - **repos_url** (string) - URL to retrieve repositories.
    - **events_url** (string) - URL to retrieve events.
    - **received_events_url** (string) - URL to retrieve received events.
    - **type** (string) - Type of the owner (e.g., 'User').
    - **site_admin** (boolean) - Indicates if the owner is a site administrator.
  - **private** (boolean) - Indicates if the repository is private.
  - **html_url** (string) - HTML URL of the repository.
  - **description** (string) - Description of the repository.
  - **fork** (boolean) - Indicates if the repository is a fork.
  - **url** (string) - API URL of the repository.
  - **archive_url** (string) - URL for archive formats.
  - **assignees_url** (string) - URL for assignees.
  - **blobs_url** (string) - URL for blobs.
  - **branches_url** (string) - URL for branches.
  - **collaborators_url** (string) - URL for collaborators.
  - **comments_url** (string) - URL for comments.
  - **commits_url** (string) - URL for commits.
  - **compare_url** (string) - URL for compare views.
  - **contents_url** (string) - URL for contents.
  - **contributors_url** (string) - URL for contributors.
  - **deployments_url** (string) - URL for deployments.
  - **downloads_url** (string) - URL for downloads.
  - **events_url** (string) - URL for events.
  - **forks_url** (string) - URL for forks.
  - **git_commits_url** (string) - URL for git commits.
  - **git_refs_url** (string) - URL for git refs.
  - **git_tags_url** (string) - URL for git tags.
  - **issue_comment_url** (string) - URL for issue comments.
  - **issue_events_url** (string) - URL for issue events.
  - **issues_url** (string) - URL for issues.
  - **keys_url** (string) - URL for keys.
  - **labels_url** (string) - URL for labels.
  - **languages_url** (string) - URL for languages.
  - **merges_url** (string) - URL for merges.
  - **milestones_url** (string) - URL for milestones.
  - **notifications_url** (string) - URL for notifications.
  - **pulls_url** (string) - URL for pulls.
  - **releases_url** (string) - URL for releases.
  - **stargazers_url** (string) - URL for stargazers.
  - **statuses_url** (string) - URL for statuses.
  - **subscribers_url** (string) - URL for subscribers.
  - **subscription_url** (string) - URL for subscription.
  - **tags_url** (string) - URL for tags.
  - **teams_url** (string) - URL for teams.
  - **trees_url** (string) - URL for trees.
  - **hooks_url** (string) - URL for hooks.
- **actor** (object) - Information about the actor performing the action.
  - **login** (string) - Actor's username.
  - **id** (integer) - Actor's ID.
  - **node_id** (string) - Actor's node ID.
  - **avatar_url** (string) - URL to the actor's avatar.
  - **gravatar_id** (string) - Actor's Gravatar ID.
  - **url** (string) - API URL for the actor.
  - **html_url** (string) - HTML URL for the actor.
  - **followers_url** (string) - URL to retrieve followers.
  - **following_url** (string) - URL to retrieve following information.
  - **gists_url** (string) - URL to retrieve gists.
  - **starred_url** (string) - URL to retrieve starred repositories.
  - **subscriptions_url** (string) - URL to retrieve subscriptions.
  - **organizations_url** (string) - URL to retrieve organizations.

#### Response Example
```json
{
  "id": 1,
  "controller_repo": {
    "id": 1296269,
    "node_id": "MDEwOlJlcG9zaXRvcnkxMjk2MjY5",
    "name": "Hello-World",
    "full_name": "octocat/Hello-World",
    "owner": {
      "login": "octocat",
      "id": 1,
      "node_id": "MDQ6VXNlcjE=",
      "avatar_url": "https://github.com/images/error/octocat_happy.gif",
      "gravatar_id": "",
      "url": "https://api.github.com/users/octocat",
      "html_url": "https://github.com/octocat",
      "followers_url": "https://api.github.com/users/octocat/followers",
      "following_url": "https://api.github.com/users/octocat/following{/other_user}",
      "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
      "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
      "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
      "organizations_url": "https://api.github.com/users/octocat/orgs",
      "repos_url": "https://api.github.com/users/octocat/repos",
      "events_url": "https://api.github.com/users/octocat/events{/privacy}",
      "received_events_url": "https://api.github.com/users/octocat/received_events",
      "type": "User",
      "site_admin": false
    },
    "private": false,
    "html_url": "https://github.com/octocat/Hello-World",
    "description": "This your first repo!",
    "fork": false,
    "url": "https://api.github.com/repos/octocat/Hello-World",
    "archive_url": "https://api.github.com/repos/octocat/Hello-World/{archive_format}{/ref}",
    "assignees_url": "https://api.github.com/repos/octocat/Hello-World/assignees{/user}",
    "blobs_url": "https://api.github.com/repos/octocat/Hello-World/git/blobs{/sha}",
    "branches_url": "https://api.github.com/repos/octocat/Hello-World/branches{/branch}",
    "collaborators_url": "https://api.github.com/repos/octocat/Hello-World/collaborators{/collaborator}",
    "comments_url": "https://api.github.com/repos/octocat/Hello-World/comments{/number}",
    "commits_url": "https://api.github.com/repos/octocat/Hello-World/commits{/sha}",
    "compare_url": "https://api.github.com/repos/octocat/Hello-World/compare/{base}...{head}",
    "contents_url": "https://api.github.com/repos/octocat/Hello-World/contents/{+path}",
    "contributors_url": "https://api.github.com/repos/octocat/Hello-World/contributors",
    "deployments_url": "https://api.github.com/repos/octocat/Hello-World/deployments",
    "downloads_url": "https://api.github.com/repos/octocat/Hello-World/downloads",
    "events_url": "https://api.github.com/repos/octocat/Hello-World/events",
    "forks_url": "https://api.github.com/repos/octocat/Hello-World/forks",
    "git_commits_url": "https://api.github.com/repos/octocat/Hello-World/git/commits{/sha}",
    "git_refs_url": "https://api.github.com/repos/octocat/Hello-World/git/refs{/sha}",
    "git_tags_url": "https://api.github.com/repos/octocat/Hello-World/git/tags{/sha}",
    "issue_comment_url": "https://api.github.com/repos/octocat/Hello-World/issues/comments{/number}",
    "issue_events_url": "https://api.github.com/repos/octocat/Hello-World/issues/events{/number}",
    "issues_url": "https://api.github.com/repos/octocat/Hello-World/issues{/number}",
    "keys_url": "https://api.github.com/repos/octocat/Hello-World/keys{/key_id}",
    "labels_url": "https://api.github.com/repos/octocat/Hello-World/labels{/name}",
    "languages_url": "https://api.github.com/repos/octocat/Hello-World/languages",
    "merges_url": "https://api.github.com/repos/octocat/Hello-World/merges",
    "milestones_url": "https://api.github.com/repos/octocat/Hello-World/milestones{/number}",
    "notifications_url": "https://api.github.com/repos/octocat/Hello-World/notifications{?since,all,participating}",
    "pulls_url": "https://api.github.com/repos/octocat/Hello-World/pulls{/number}",
    "releases_url": "https://api.github.com/repos/octocat/Hello-World/releases{/id}",
    "stargazers_url": "https://api.github.com/repos/octocat/Hello-World/stargazers",
    "statuses_url": "https://api.github.com/repos/octocat/Hello-World/statuses/{sha}",
    "subscribers_url": "https://api.github.com/repos/octocat/Hello-World/subscribers",
    "subscription_url": "https://api.github.com/repos/octocat/Hello-World/subscription",
    "tags_url": "https://api.github.com/repos/octocat/Hello-World/tags",
    "teams_url": "https://api.github.com/repos/octocat/Hello-World/teams",
    "trees_url": "https://api.github.com/repos/octocat/Hello-World/git/trees{/sha}",
    "hooks_url": "https://api.github.com/repos/octocat/Hello-World/hooks"
  },
  "actor": {
    "login": "octocat",
    "id": 1,
    "node_id": "MDQ6VXNlcjE=",
    "avatar_url": "https://github.com/images/error/octocat_happy.gif",
    "gravatar_id": "",
    "url": "https://api.github.com/users/octocat",
    "html_url": "https://github.com/octocat",
    "followers_url": "https://api.github.com/users/octocat/followers",
    "following_url": "https://api.github.com/users/octocat/following{/other_user}",
    "gists_url": "https://api.github.com/users/octocat/gists{/gist_id}",
    "starred_url": "https://api.github.com/users/octocat/starred{/owner}{/repo}",
    "subscriptions_url": "https://api.github.com/users/octocat/subscriptions",
    "organizations_url": "https://api.github.com/users/octocat/orgs"
  }
}
```
```

--------------------------------

### Initialize CodeQL Action with Queries

Source: https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/customizing-your-advanced-setup-for-code-scanning

This snippet shows how to initialize the CodeQL action to run specific queries or query suites. It uses the `queries` parameter to list the desired analysis sets. An `external-repository-token` can be provided for accessing private query repositories.

```yaml
- uses: github/codeql-action/init@v3
  with:
    queries: security-extended
    external-repository-token: ${{ secrets.ACCESS_TOKEN }}

```

```yaml
- uses: github/codeql-action/init@v3
  with:
    queries: security-extended
    external-repository-token: ${{ secrets.ACCESS_TOKEN }}

```

--------------------------------

### Setup and Enable GitHub Copilot in Vim/Neovim

Source: https://docs.github.com/en/copilot/configuring-github-copilot/installing-the-github-copilot-extension-in-your-environment_tool=jetbrains

Commands to set up and enable the GitHub Copilot plugin within Vim or Neovim. These commands are run directly in the Vim/Neovim command mode.

```shell
:Copilot setup
:Copilot enable
```

--------------------------------

### Get Project for User - cURL Request Example

Source: https://docs.github.com/en/rest/projects/projects

This cURL example demonstrates how to retrieve a specific user-owned project. It requires setting the Accept header to 'application/vnd.github+json' and includes placeholders for authentication token and user/project identifiers. The API version is also specified.

```shell
curl -L \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer <YOUR-TOKEN>" \
  -H "X-GitHub-Api-Version: 2022-11-28" \
  https://api.github.com/users/USER_ID/projectsV2/PROJECT_NUMBER
```

--------------------------------

### Start an import

Source: https://docs.github.com/en/rest/migrations/source-imports

Starts a source import to a GitHub repository using GitHub Importer. Importing into a GitHub repository with GitHub Actions enabled is not supported.

```APIDOC
## POST /repos/{owner}/{repo}/import

### Description
Starts a source import to a GitHub repository using GitHub Importer. Importing into a GitHub repository with GitHub Actions enabled is not supported and will return a status `422 Unprocessable Entity` response.

**Note:** This endpoint is closing down on April 12, 2024.

### Method
POST

### Endpoint
`/repos/{owner}/{repo}/import`

### Parameters
#### Path Parameters
- **owner** (string) - Required - The account owner of the repository. The name is not case sensitive.
- **repo** (string) - Required - The name of the repository without the `.git` extension. The name is not case sensitive.

#### Request Body
- **vcs_url** (string) - Required - The URL of the originating repository.
- **vcs** (string) - Optional - The originating VCS type. Can be one of: `subversion`, `git`, `mercurial`, `tfvc`.
- **vcs_username** (string) - Optional - If authentication is required, the username to provide to `vcs_url`.
- **vcs_password** (string) - Optional - If authentication is required, the password to provide to `vcs_url`.
- **tfvc_project** (string) - Optional - For a tfvc import, the name of the project that is being imported.

### Request Example
```json
{
  "vcs": "subversion",
  "vcs_url": "http://svn.mycompany.com/svn/myproject",
  "vcs_username": "octocat",
  "vcs_password": "secret"
}
```

### Response
#### Success Response (201)
- **vcs** (string) - The originating VCS type.
- **use_lfs** (boolean) - Whether to use LFS for the import.
- **vcs_url** (string) - The URL of the originating repository.
- **status** (string) - The current status of the import.
- **status_text** (string) - A human-readable status message.
- **has_large_files** (boolean) - Whether the repository contains large files.
- **large_files_size** (integer) - The total size of large files in bytes.
- **large_files_count** (integer) - The number of large files.
- **authors_count** (integer) - The number of authors detected.
- **url** (string) - The API URL for the import.
- **html_url** (string) - The HTML URL for the import.
- **authors_url** (string) - The API URL for the import authors.
- **repository_url** (string) - The API URL for the repository.

#### Response Example
```json
{
  "vcs": "subversion",
  "use_lfs": true,
  "vcs_url": "http://svn.mycompany.com/svn/myproject",
  "status": "importing",
  "status_text": "Importing...",
  "has_large_files": false,
  "large_files_size": 0,
  "large_files_count": 0,
  "authors_count": 0,
  "commit_count": 1042,
  "url": "https://api.github.com/repos/octocat/socm/import",
  "html_url": "https://import.github.com/octocat/socm/import",
  "authors_url": "https://api.github.com/repos/octocat/socm/import/authors",
  "repository_url": "https://api.github.com/repos/octocat/socm"
}
```

#### Error Responses
- **404** - Resource not found
- **422** - Validation failed, or the endpoint has been spammed.
- **503** - Unavailable due to service under maintenance.
```

--------------------------------

### Example of jobs.<job_id>.steps

Source: https://docs.github.com/en/actions/automating-your-workflow-with-github-actions/workflow-syntax-for-github-actions

A complete example illustrating the structure and usage of steps within a GitHub Actions job.

```APIDOC
### Example of `jobs.<job_id>.steps`
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