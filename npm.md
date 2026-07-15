### Execute npm start and observe output

Source: https://docs.npmjs.com/cli/v11/commands/npm-start

This example shows the command 'npm start' being executed and the subsequent output, indicating that the 'node foo.js' script was run. The actual output from 'foo.js' would follow.

```bash
npm start

> npm@x.x.x start
> node foo.js

(foo.js output would be here)
```

--------------------------------

### Define start script in package.json

Source: https://docs.npmjs.com/cli/v11/commands/npm-start

This JSON example demonstrates how to define a 'start' script within the 'scripts' object of a package.json file. This script will be executed when 'npm start' is run.

```json
{
  "scripts": {
    "start": "node foo.js"
  }
}
```

--------------------------------

### npm Script Configuration Example

Source: https://docs.npmjs.com/cli/v11/using-npm/scripts

Provides an example of how to define scripts in package.json, including running other npm scripts. This setup allows for a clear separation of build, test, and prepare tasks, with 'prepare' potentially triggering a 'build' script.

```json
{
  "scripts": {
    "prepare": "npm run build",
    "build": "tsc",
    "test": "jest"
  }
}
```

--------------------------------

### Install from Tarball URL

Source: https://docs.npmjs.com/cli/install

Fetches and installs a package from a tarball URL. The argument must start with `http://` or `https://` to distinguish it from other installation methods.

```bash
npm install https://github.com/indexzero/forever/tarball/v0.5.6
```

--------------------------------

### Example Output of npm prefix

Source: https://docs.npmjs.com/cli/v11/commands/npm-prefix

Illustrates the typical output when running the 'npm prefix' command locally and globally. The local output shows the project's root directory, while the global output indicates the system's global npm installation path.

```bash
npm prefix
/usr/local/projects/foo
```

```bash
npm prefix -g
/usr/local
```

--------------------------------

### npm init: Creating a React App

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Example of using npm init with the `create-react-app` initializer to scaffold a new React-based project. This is a common use case for quickly starting front-end development.

```bash
$ npm init react-app ./my-react-app
```

--------------------------------

### Run npm start command

Source: https://docs.npmjs.com/cli/v11/commands/npm-start

This is the synopsis for the npm start command, showing its basic usage with optional arguments.

```bash
npm start [-- <args>]
```

--------------------------------

### Install multiple npm packages with options

Source: https://docs.npmjs.com/cli/install

Demonstrates installing multiple npm packages simultaneously, including version ranges and the use of the `--tag` argument to prefer specific tagged versions.

```bash
npm install sax@">=0.1.0 <0.2.0" bench supervisor
npm install sax --force
```

--------------------------------

### Run npm install and npm test

Source: https://docs.npmjs.com/cli/v11/commands/npm-install-test

This command installs specified package(s) and then executes the npm test script. It mirrors the functionality and arguments of the standard `npm install` command.

```bash
npm install-test [<package-spec> ...]

alias: it
```

--------------------------------

### Combine multiple npm install arguments

Source: https://docs.npmjs.com/cli-documentation/install

Demonstrates the ability to combine multiple package installation arguments, including version ranges and different package sources, in a single `npm install` command.

```bash
npm install sax=">=0.1.0 <0.2.0" bench supervisor
```

--------------------------------

### Displaying npm Profile Information

Source: https://docs.npmjs.com/cli/profile

This example shows how to retrieve all profile properties or specific ones using the `npm profile get` command. The output typically includes details like username, email status, two-factor authentication status, and account creation/update timestamps.

```bash
npm profile get
npm profile get email
npm profile get "two-factor auth"
```

--------------------------------

### npm rebuild Default Install Hook Example

Source: https://docs.npmjs.com/cli/v11/commands/npm-rebuild

Demonstrates the default install hook used by npm when a 'binding.gyp' file is present in the package root. This hook triggers a 'node-gyp rebuild' process. This behavior is overridden if the package.json defines its own 'install' or 'preinstall' scripts, or if 'gypfile' is set to false.

```json
"scripts": {
    "install": "node-gyp rebuild"
}
```

--------------------------------

### Git URL Dependencies for npm Packages

Source: https://docs.npmjs.com/files/package

Illustrates how to specify dependencies directly from Git repositories using various protocols and commit-ish identifiers. This allows for direct installation from source control, including specific commits or semver-compatible tags.

```git-url
git+ssh://git@github.com:npm/cli.git#v1.0.27
git+ssh://git@github.com:npm/cli#semver:^5.0
git+https://isaacs@github.com/npm/cli.git
git://github.com/npm/cli.git#v1.0.27
```

--------------------------------

### Install Package Locally with npm

Source: https://docs.npmjs.com/cli/v11/using-npm/developers

Installs the current package globally for testing purposes. This command is useful for verifying that your package installs correctly before publishing.

```bash
npm install . -g
```

--------------------------------

### npm fund Example Output (All Workspaces)

Source: https://docs.npmjs.com/cli/v11/commands/npm-fund

Example output of the `npm fund` command when run in a project with multiple workspaces. It displays a tree structure of funding information.

```bash
$ npm fund
test-workspaces-fund@1.0.0
+-- https://example.com/a
| | `-- a@1.0.0
| `-- https://example.com/maintainer
|     `-- foo@1.0.0
+-- https://example.com/npmcli-funding
|   `-- @npmcli/test-funding
`-- https://example.com/org
    `-- bar@2.0.0

```

--------------------------------

### npm init <initializer>

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Initializes a new npm package by installing and executing an initializer package (e.g., `create-react-app`).

```APIDOC
## POST /npm/init

### Description
Initializes a new npm package by installing and executing an initializer package. The initializer is an npm package named `create-<initializer>`, which is installed via `npm-exec` and then its main binary is executed.

### Method
POST

### Endpoint
`/npm/init`

### Parameters
#### Query Parameters
- **initializer** (string) - Required - The name of the initializer package (e.g., `react-app`, `esm`).
- **scope** (string) - Optional - The scope for the initializer package (e.g., `@usr`).
- **version** (string) - Optional - The specific version of the initializer package to use (e.g., `latest`, `1.2.3`).
- **yes** (boolean) - Optional - Skips the questionnaire and uses default values.
- **init-private** (boolean) - Optional - Sets the `private` flag to `true` in `package.json`.
- **workspace** (string) - Optional - Creates a new workspace in the specified directory.

### Request Body
```json
{
  "initializer": "react-app",
  "options": {
    "yes": true,
    "workspace": "packages/my-app"
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating successful initialization.

#### Response Example
```json
{
  "message": "Package initialized successfully."
}
```
```

--------------------------------

### npx Synopsis Examples

Source: https://docs.npmjs.com/cli/commands/npx

Illustrates the basic syntax for using npx to run commands from npm packages, including specifying packages, versions, and arguments.

```bash
npx -- <pkg>[@<version>] [args...]
npx --package=<pkg>[@<version>] -- <cmd> [args...]
npx -c '<cmd> [args...]'
npx --package=foo -c '<cmd> [args...]'
```

--------------------------------

### Install Local Links

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Configure whether file: protocol dependencies are packed and installed as regular dependencies instead of creating a symlink. This option has no effect on workspaces.

```APIDOC
## `install-links`

### Description
When set file: protocol dependencies will be packed and installed as regular dependencies instead of creating a symlink. This option has no effect on workspaces.

### Type
Boolean

### Default
`false`
```

--------------------------------

### npm install-test Command

Source: https://docs.npmjs.com/cli/v11/commands/npm-install-test

The npm-install-test command installs specified packages and then runs the configured tests. It accepts the same arguments as the `npm install` command.

```APIDOC
## npm install-test

### Description
This command runs an `npm install` followed immediately by an `npm test`. It takes exactly the same arguments as `npm install`.

### Method
CLI Command

### Endpoint
N/A (CLI Command)

### Parameters
#### Path Parameters
N/A

#### Query Parameters
N/A

#### Request Body
N/A

### Request Example
```bash
npm install-test <package-spec> ...
```

### Response
#### Success Response (0)
- **Output**: Standard output from npm install and npm test.

#### Response Example
```
> my-package@1.0.0 test
> jest

 PASS  ./index.test.js
  ✓ should add numbers (2ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        0.123s, estimated 1s
```

## Configuration Options

### `save`
- **Default**: `true` (unless using `npm update`, then `false`)
- **Type**: Boolean
- **Description**: Save installed packages to `package.json` as dependencies. When used with `npm rm`, it removes the dependency. Setting to `false` prevents writing to `package-lock.json`.

### `save-exact`
- **Default**: `false`
- **Type**: Boolean
- **Description**: Save dependencies in `package.json` with their exact versions instead of using npm's default semver range operator.

### `global`
- **Default**: `false`
- **Type**: Boolean
- **Description**: Operates in global mode, installing packages into the `prefix` folder instead of the current working directory. Bin files are linked to `{prefix}/bin` and man pages to `{prefix}/share/man`.

### `install-strategy`
- **Default**: `"hoisted"`
- **Type**: String (`"hoisted"`, `"nested"`, `"shallow"`, or `"linked"`)
- **Description**: Sets the strategy for installing packages in `node_modules`. Options include `hoisted` (default), `nested`, `shallow`, and `linked` (experimental).

### `legacy-bundling`
- **Default**: `false`
- **Type**: Boolean
- **Description**: DEPRECATED: Use `--install-strategy=nested` instead. Installs packages in the same manner they are depended on, without hoisting, potentially leading to deep directory structures and duplicate installs.

### `global-style`
- **Default**: `false`
- **Type**: Boolean
- **Description**: DEPRECATED: Use `--install-strategy=shallow` instead. Only installs direct dependencies in the top-level `node_modules`, but hoists deeper dependencies.

### `omit`
- **Default**: `'dev'` if `NODE_ENV` is `'production'`, otherwise empty.
- **Type**: String (`"dev"`, `"optional"`, or `"peer"`, can be set multiple times)
- **Description**: Dependency types to omit from the installation tree on disk. These are still resolved and added to lock files but not physically installed. If a package type is in both `--include` and `--omit`, it will be included. If `'dev'` is omitted, `NODE_ENV` is set to `'production'` for lifecycle scripts.

### `include`
- **Default**: None
- **Type**: String (`"prod"`, `"dev"`, `"optional"`, or `"peer"`, can be set multiple times)
- **Description**: Allows defining which types of dependencies to install. This is the inverse of `--omit`. Specified types will not be omitted regardless of order.

### `strict-peer-deps`
- **Default**: `false`
- **Type**: Boolean
- **Description**: If `true` and `--legacy-peer-deps` is not set, any conflicting `peerDependencies` will cause an install failure. By default, conflicts are resolved using the nearest non-peer dependency specification, with a warning. Setting this to `true` treats the warning as a failure.

### `prefer-dedupe`
- **Default**: `false`
- **Type**: Boolean
- **Description**: Prefer to deduplicate packages if possible, rather than choosing a newer version of a dependency.

### `package-lock`
- **Default**: `true`
- **Type**: Boolean
- **Description**: If `false`, ignores `package-lock.json` files during installation and prevents writing to `package-lock.json` if `save` is `true`.
```

--------------------------------

### Install Package by Name and Tag

Source: https://docs.npmjs.com/cli/install

Installs a package by its name, using the version tagged as 'latest' by default. If multiple versions satisfy the `package.json` ranges, npm prioritizes versions compatible with the current Node.js version based on the `engines` field. To install a specific version regardless of compatibility, use `<name>@latest`.

```bash
npm install [<@scope>/]<name>
```

--------------------------------

### GitHub Shorthand Dependency Example

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Shows how to specify GitHub repositories as dependencies using a shorthand 'user/repo' format in the package.json file. Includes examples with commit-ish suffixes.

```json
{
  "name": "foo",
  "version": "0.0.0",
  "dependencies": {
    "express": "expressjs/express",
    "mocha": "mochajs/mocha#4727d357ea",
    "module": "npm/example-github-repo#feature\/branch"
  }
}
```

--------------------------------

### Example: Caret Dependencies Update

Source: https://docs.npmjs.com/cli/update

Demonstrates how `npm update` handles caret dependencies (`^`). If `dep1` is `^1.1.1` and the latest version is `1.2.2`, `npm update` will install `1.2.2` as it satisfies the caret range.

```json
{
  "dependencies": {
    "dep1": "^1.1.1"
  }
}
```

--------------------------------

### Example npm Profile Output

Source: https://docs.npmjs.com/cli/v11/commands/npm-profile

Illustrates the typical output format when retrieving npm profile information using `npm profile get`. It shows various user details including name, email verification status, 2FA configuration, and timestamps.

```text
name: example
email: e@example.com (verified)
two-factor auth: auth-and-writes
fullname: Example User
homepage:
freenode:
twitter:
github:
created: 2015-02-26T01:38:35.892Z
updated: 2017-10-02T21:29:45.922Z
```

--------------------------------

### Manually Remove npm Files (Severe)

Source: https://docs.npmjs.com/cli/v11/using-npm/removal

This command performs a more drastic uninstallation by recursively removing npm-related directories and files from the default installation prefix. Adjust the path if npm was installed elsewhere.

```bash
rm -rf /usr/local/{lib/node{,/.npm,_modules},bin,share/man}/npm*
```

--------------------------------

### Get Global npm Package Prefix (Windows)

Source: https://docs.npmjs.com/try-the-latest-stable-version-of-npm

This command retrieves the current directory where npm installs global packages on Windows. It's useful for verifying the configuration.

```bash
npm config get prefix -g
```

--------------------------------

### Configure Travis CI to use npm ci

Source: https://docs.npmjs.com/cli/v11/commands/npm-ci

This configuration snippet shows how to integrate `npm ci` into a Travis CI build process. By using `npm ci` instead of `npm install`, you ensure that your CI environment performs a clean and reproducible installation of dependencies. The example also includes caching the npm cache directory to speed up subsequent builds.

```yaml
# .travis.yml
install:
- npm ci
# keep the npm cache around to speed up installs
cache:
  directories:
  - "$HOME/.npm"
```

--------------------------------

### Configure Scoped Registry Login and Logout

Source: https://docs.npmjs.com/cli/v11/commands/npm-adduser

These examples demonstrate how to log in to and log out of a private registry using the --scope and --registry flags. Logging in maps the specified scope to the custom registry for future package installations and npm init commands. Logging out removes this mapping and the authentication token.

```bash
# log in, linking the scope to the custom registry
npm login --scope=@mycorp --registry=https://registry.mycorp.com


# log out, removing the link and the auth token
npm logout --scope=@mycorp
```

--------------------------------

### Example: Tilde Dependencies Update

Source: https://docs.npmjs.com/cli/update

Illustrates `npm update` with tilde dependencies (`~`). If `dep1` is `~1.1.1` (meaning `>=1.1.1 <1.2.0`) and the latest version is `1.2.2`, `npm update` will install `1.1.2` as it's the highest version satisfying the tilde range.

```json
{
  "dependencies": {
    "dep1": "~1.1.1"
  }
}
```

--------------------------------

### npm ci for Strict Installation

Source: https://docs.npmjs.com/cli/v11/commands/npm-install

Introduces `npm ci` as an alternative to `npm install` for installing packages strictly, ensuring `package.json` is not modified and both files remain in sync. This is ideal for CI/CD environments.

```text
If you want to install packages while ensuring that `package.json` is not modified and that both files are strictly in sync, use `npm ci` instead.
```

--------------------------------

### Install npm packages from Bitbucket repositories

Source: https://docs.npmjs.com/cli/install

Installs npm packages directly from Bitbucket repositories using shorthand notation. Supports specifying versions via commit-ish or semver ranges. If no commit-ish is provided, the 'master' branch is used.

```bash
npm install bitbucket:mybitbucketuser/myproject
```

--------------------------------

### peerDependenciesMeta Example in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The peerDependenciesMeta field provides additional information about peer dependencies, specifically allowing them to be marked as optional. Optional peer dependencies are not automatically installed by npm. This example marks '@npm/soy-milk' as an optional peer dependency for '@npm/tea-latte'.

```json
{
  "name": "@npm/tea-latte",
  "version": "1.3.5",
  "peerDependencies": {
    "@npm/tea": "2.x",
    "@npm/soy-milk": "1.2"
  },
  "peerDependenciesMeta": {
    "@npm/soy-milk": {
      "optional": true
    }
  }
}
```

--------------------------------

### npx Examples - Running Different Package Commands

Source: https://docs.npmjs.com/cli/v11/commands/npx

Shows how to run a command from a package that does not match the package's name, by explicitly specifying the package using the `--package` option.

```bash
$ npm exec --package=foo -- bar --bar-argument
# or
$ npx --package=foo bar --bar-argument
```

--------------------------------

### Example Output of npm outdated

Source: https://docs.npmjs.com/cli/outdated

This example demonstrates the typical output of the `npm outdated` command, showing package names, their current, wanted, and latest versions, their location in the project, and which packages depend on them. Different colors indicate the severity of the outdated status.

```bash
$ npm outdated
Package      Current   Wanted   Latest  Location                  Depended by
glob          5.0.15   5.0.15    6.0.1  node_modules/glob         dependent-package-name
nothingness    0.0.3      git      git  node_modules/nothingness  dependent-package-name
npm            3.5.1    3.5.2    3.5.1  node_modules/npm          dependent-package-name
local-dev      0.0.3   linked   linked  local-dev                 dependent-package-name
once           1.3.2    1.3.3    1.3.3  node_modules/once         dependent-package-name
```

--------------------------------

### NPM Workspace Configuration Example

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

Example of how to define workspaces in a package.json file. The order of workspaces in this array determines the execution order when commands are run across all workspaces.

```json
{
  "workspaces": [ "packages/a", "packages/b" ]
}
```

```json
{
  "workspaces": [ "packages/b", "packages/a" ]
}
```

--------------------------------

### npm install with --tag, --dry-run, --package-lock-only, and --force flags

Source: https://docs.npmjs.com/cli/install

Explains and demonstrates the usage of various npm install flags: `--tag` for version preference, `--dry-run` for simulation, `--package-lock-only` to update lock files, and `--force` to override local caches.

```bash
# Example for --tag (note: affects only command-line specified packages)
npm install --tag beta
npm install foo@beta

# Example for --dry-run
npm install --dry-run

# Example for --package-lock-only
npm install --package-lock-only

# Example for --force
npm install sax --force
```

--------------------------------

### Install npm packages from GitHub repositories

Source: https://docs.npmjs.com/cli/install

Installs npm packages directly from GitHub repositories using shorthand notation. Supports specifying versions via commit-ish or semver ranges. If no commit-ish is provided, the default branch is used.

```bash
npm install mygithubuser/myproject
npm install github:mygithubuser/myproject
```

--------------------------------

### npm fund Example Output (Filtered by Workspace 'a')

Source: https://docs.npmjs.com/cli/v11/commands/npm-fund

Example output of the `npm fund` command when filtered to a specific workspace 'a' using the `-w` or `--workspace` option. This narrows down the funding information to that workspace and its dependencies.

```bash
$ npm fund -w a
test-workspaces-fund@1.0.0
`-- https://example.com/a
  | `-- a@1.0.0
  `-- https://example.com/maintainer
      `-- foo@2.0.0

```

--------------------------------

### Global Installation

Source: https://docs.npmjs.com/cli/install

Installs the current package context (working directory) as a global package when the `-g` or `--global` flag is used with `npm install`. This is typically used for command-line tools.

```bash
npm install -g
npm install --global
```

--------------------------------

### Check npm and Node.js Versions

Source: https://docs.npmjs.com/cli/v11/configuring-npm/install

Verify if Node.js and npm are installed and display their current versions. This is a fundamental step before proceeding with package management operations.

```shell
node -v
npm -v
```

--------------------------------

### Install Local Folder Dependencies

Source: https://docs.npmjs.com/cli/install

Installs dependencies from a local folder. If the folder is within the project root, dependencies are installed and potentially hoisted. If outside, a symlink is created to the folder. Use `--install-links` to install the content like a registry package instead of creating a link.

```bash
npm install ../../other-package --install-links
npm install ./sub-package
```

--------------------------------

### Example package.json structure

Source: https://docs.npmjs.com/about-package-json-and-package-lock-json-files

A basic example of a `package.json` file, demonstrating the required 'name' and 'version' fields, along with the optional 'author' field.

```json
{
  "name": "my-awesome-package",
  "version": "1.0.0",
  "author": "Your Name <email@example.com> (https://example.com)"
}
```

--------------------------------

### Global Installation Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-diff

Configuration options related to global npm package installations.

```APIDOC
## `global`

### Description
Operates in "global" mode, so that packages are installed into the `prefix` folder instead of the current working directory. Packages are installed into the `{prefix}/lib/node_modules` folder, bin files are linked to `{prefix}/bin`, and man pages are linked to `{prefix}/share/man`.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **global** (Boolean) - Optional - Default: false

### Request Example
```json
{
  "global": true
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

--------------------------------

### Node.js 'Cannot find module' Error Example

Source: https://docs.npmjs.com/using-npm-packages-in-your-projects

Presents a typical Node.js error message, 'Cannot find module', which occurs when a package is referenced but not installed. This highlights the importance of running `npm install`.

```text
module.js:340
    throw err;
          ^
Error: Cannot find module 'lodash'


```

--------------------------------

### Install Package with npm CLI

Source: https://docs.npmjs.com/cli/install

The `npm install` command installs a specified package and all of its dependencies. It respects lock files (`npm-shrinkwrap.json`, `package-lock.json`, `yarn.lock`) to ensure consistent dependency versions. This is the primary command for adding packages to a project.

```bash
npm install [<package-spec> ...]

aliases: add, i, in, ins, inst, insta, instal, isnt, isnta, isntal, isntall
```

--------------------------------

### npm Install Algorithm Visualization

Source: https://docs.npmjs.com/cli/v11/commands/npm-install

Visual representations of the npm dependency resolution algorithm for different package structures. This helps understand how npm creates the `node_modules` tree and handles version conflicts.

```text
A
+-- B
+-- C
+-- D
```

```text
A
+-- B
+-- C
   `-- D@2
+-- D@1
```

--------------------------------

### Example CycloneDX SBOM Output

Source: https://docs.npmjs.com/cli/v11/commands/npm-sbom

This example demonstrates the structure of a Software Bill of Materials (SBOM) generated in the CycloneDX format using the `npm sbom` command. It includes project metadata, component details, and dependency relationships.

```json
{
  "$schema": "http://cyclonedx.org/schema/bom-1.5.schema.json",
  "bomFormat": "CycloneDX",
  "specVersion": "1.5",
  "serialNumber": "urn:uuid:09f55116-97e1-49cf-b3b8-44d0207e7730",
  "version": 1,
  "metadata": {
    "timestamp": "2023-09-01T00:00:00.001Z",
    "lifecycles": [
      {
        "phase": "build"
      }
    ],
    "tools": [
      {
        "vendor": "npm",
        "name": "cli",
        "version": "10.1.0"
      }
    ],
    "component": {
      "bom-ref": "simple@1.0.0",
      "type": "library",
      "name": "simple",
      "version": "1.0.0",
      "scope": "required",
      "author": "John Doe",
      "description": "simple react app",
      "purl": "pkg:npm/simple@1.0.0",
      "properties": [
        {
          "name": "cdx:npm:package:path",
          "value": ""
        }
      ],
      "externalReferences": [],
      "licenses": [
        {
          "license": {
            "id": "MIT"
          }
        }
      ]
    }
  },
  "components": [
    {
      "bom-ref": "lodash@4.17.21",
      "type": "library",
      "name": "lodash",
      "version": "4.17.21",
      "scope": "required",
      "author": "John-David Dalton",
      "description": "Lodash modular utilities.",
      "purl": "pkg:npm/lodash@4.17.21",
      "properties": [
        {
          "name": "cdx:npm:package:path",
          "value": "node_modules/lodash"
        }
      ],
      "externalReferences": [
        {
          "type": "distribution",
          "url": "https://registry.npmjs.org/lodash/-/lodash-4.17.21.tgz"
        },
        {
          "type": "vcs",
          "url": "git+https://github.com/lodash/lodash.git"
        },
        {
          "type": "website",
          "url": "https://lodash.com/"
        },
        {
          "type": "issue-tracker",
          "url": "https://github.com/lodash/lodash/issues"
        }
      ],
      "hashes": [
        {
          "alg": "SHA-512",
          "content": "bf690311ee7b95e713ba568322e3533f2dd1cb880b189e99d4edef13592b81764daec43e2c54c61d5c558dc5cfb35ecb85b65519e74026ff17675b6f8f916f4a"
        }
      ],
      "licenses": [
        {
          "license": {
            "id": "MIT"
          }
        }
      ]
    }
  ],
  "dependencies": [
    {
      "ref": "simple@1.0.0",
      "dependsOn": ["lodash@4.17.21"]
    },
    {
      "ref": "lodash@4.17.21",
      "dependsOn": []
    }
  ]
}
```

--------------------------------

### devDependencies Example in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The devDependencies object lists packages required only for development and testing, such as build tools or testing frameworks. These are not installed when the package is used by end-users. The example shows 'coffee-script' as a devDependency, used with the 'prepare' script for compilation.

```json
{
  "name": "@npm/ethopia-waza",
  "description": "a delightfully fruity coffee varietal",
  "version": "1.2.3",
  "devDependencies": {
    "coffee-script": "~1.6.3"
  },
  "scripts": {
    "prepare": "coffee -o lib/ -c src/waza.coffee"
  },
  "main": "lib/waza.js"
}
```

--------------------------------

### Test Local Package Installation

Source: https://docs.npmjs.com/cli/v11/using-npm/developers

Installs a local package into another project's node_modules directory. This allows you to test how your package integrates with other projects.

```bash
cd ../some-other-folder
npm install ../my-package
```

--------------------------------

### Verbose npm Install

Source: https://docs.npmjs.com/common-errors

Provides detailed output during `npm install` to help diagnose installation problems. Use this option when encountering unexpected behavior during package installation.

```bash
npm install --verbose
```

--------------------------------

### Default 'install' script for binding.gyp

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

When a 'binding.gyp' file is present and no 'install' or 'preinstall' scripts are defined, npm defaults the 'scripts.install' command to compile using node-gyp. This is common for packages with native C++ addons.

```json
{
  "scripts": {
    "install": "node-gyp rebuild"
  }
}
```

--------------------------------

### npm install with package-lock.json

Source: https://docs.npmjs.com/cli/install

Explains how `npm install` uses `package.json` and `package-lock.json` to ensure reproducible builds. If the lockfile satisfies the ranges in `package.json`, exact versions from the lockfile are used. Otherwise, new versions are resolved, and `package-lock.json` is updated.

```bash
npm install
```

--------------------------------

### Install npm packages from GitLab repositories

Source: https://docs.npmjs.com/cli/install

Installs npm packages directly from GitLab repositories using shorthand notation. Supports specifying versions via commit-ish or semver ranges. If no commit-ish is provided, the 'master' branch is used.

```bash
npm install gitlab:mygitlabuser/myproject
npm install gitlab:myusr/myproj#semver:^5.0
```

--------------------------------

### peerDependencies Example in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The peerDependencies field specifies packages that your package is compatible with, often used for plugins. It indicates that your package requires a specific version of a host package to be installed alongside it. The example shows '@npm/tea-latte' requiring '@npm/tea' version '2.x'.

```json
{
  "name": "@npm/tea-latte",
  "version": "1.3.5",
  "peerDependencies": {
    "@npm/tea": "2.x"
  }
}
```

--------------------------------

### System-wide npm Tab Completion Setup

Source: https://docs.npmjs.com/cli/v11/commands/npm-completion

This method allows for system-wide npm tab completion by piping the output of 'npm completion' to a file in the system's bash completion directory. This approach requires appropriate permissions to write to system directories like /usr/local/etc/bash_completion.d/ or /etc/bash_completion.d/.

```bash
npm completion > /usr/local/etc/bash_completion.d/npm
npm completion > /etc/bash_completion.d/npm
```

--------------------------------

### Basic Dockerfile for Node.js application

Source: https://docs.npmjs.com/docker-and-private-modules

A standard Dockerfile for a Node.js application that copies package.json, installs dependencies, copies source files, and starts the application. It does not handle private npm packages.

```docker
FROM node

COPY package.json package.json
RUN npm install

# Add your source files
COPY . .
CMD npm start
```

--------------------------------

### npm init: Creating an ESM-compatible Package

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Example of using npm init with the `create-esm` initializer to set up a new package that is compatible with ECMAScript Modules (ESM). The `--yes` flag skips the interactive questions.

```bash
mkdir my-esm-lib && cd my-esm-lib
$ npm init esm --yes
```

--------------------------------

### Login and Logout with Scoped Registries using npm CLI

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Demonstrates how to log in to and log out of a custom registry using the `npm login` and `npm logout` commands with the `--scope` option. This maps a specific scope to a registry for package installations and `npm init`.

```bash
# log in, linking the scope to the custom registry
npm login --scope=@mycorp --registry=https://registry.mycorp.com

# log out, removing the link and the auth token
npm logout --scope=@mycorp
```

--------------------------------

### Uninstall npm Globally (Standard)

Source: https://docs.npmjs.com/cli/v11/using-npm/removal

This command removes the globally installed npm package. It's the primary method for uninstalling npm. Ensure you have the necessary permissions to run this command.

```bash
sudo npm uninstall npm -g
```

--------------------------------

### npm init: Basic Usage and Aliases

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Demonstrates the fundamental syntax for using npm init with package initializers and its common aliases. It shows how to specify a package initializer or use the command without arguments for legacy behavior.

```bash
npm init <package-spec> (same as `npx create-<package-spec>`)
npm init <@scope> (same as `npx <@scope>/create`)

aliases: create, innit
```

--------------------------------

### Run npm ci for a clean install

Source: https://docs.npmjs.com/cli/v11/commands/npm-ci

This command executes a clean installation of project dependencies. It requires an existing package-lock.json or npm-shrinkwrap.json and will remove any existing node_modules directory before proceeding. It is designed for automated environments and ensures that the installed dependencies exactly match the lock file.

```bash
npm ci
```

--------------------------------

### Flattened Object Property Access in Scripts

Source: https://docs.npmjs.com/misc/scripts

Shows how nested properties in package.json, like scripts, are flattened into environment variables. For example, `{"scripts":{"install":"foo.js"}}` results in `npm_package_scripts_install`.

```javascript
process.env.npm_package_scripts_install === "foo.js"
```

--------------------------------

### Example: Subdependencies Update Behavior

Source: https://docs.npmjs.com/cli/update

Shows how `npm update` prioritizes a single version of a subdependency that satisfies multiple parent dependencies. If `dep2` requires `dep1` as `~1.1.1`, `npm update` will install `dep1@1.1.2` even if the main app requires a newer version, to satisfy `dep2`'s constraints.

```json
{
  "name": "my-app",
  "dependencies": {
    "dep1": "^1.0.0",
    "dep2": "1.0.0"
  }
}

{
  "name": "dep2",
  "dependencies": {
    "dep1": "~1.1.1"
  }
}
```

--------------------------------

### Before Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-outdated

The `before` configuration option, when used with `npm install`, filters package installations to include only versions available on or before a specified date.

```APIDOC
## `before` Configuration Option

### Description
If passed to `npm install`, will rebuild the npm tree such that only versions that were available **on or before** the given date are installed. If there are no versions available for the current set of dependencies, the command will error.

### Configuration Details
*   **Default**: `null`
*   **Type**: `null` or `Date`

### Usage Notes
If the requested version is a `dist-tag` and the given tag does not pass the `--before` filter, the most recent version less than or equal to that tag will be used. For example, `foo@latest` might install `foo@1.2` even though `latest` is `2.0`.

### Restrictions
This config cannot be used with: `min-release-age`
```

--------------------------------

### Install from Local Tarball

Source: https://docs.npmjs.com/cli/install

Installs a package from a local tarball file. The filename must end with `.tar`, `.tar.gz`, or `.tgz`. npm strips one directory layer from the tarball, expecting package contents in a subfolder (e.g., `package/`). The package must contain a `package.json` with `name` and `version`.

```bash
npm install ./package.tgz
```

--------------------------------

### Install Latest npm in Node Directory (Windows)

Source: https://docs.npmjs.com/try-the-latest-stable-version-of-npm

This command installs the latest version of npm within the Node.js installation directory on Windows. It's part of a workaround for PATH configuration issues and requires administrator privileges.

```bash
cd %ProgramFiles%\nodejs
npm install npm@latest
```

--------------------------------

### Specify Man Pages in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'man' field in package.json specifies man page files for a package. It can be a single file path or an array of paths. If a single file is provided, it's installed as 'man <pkgname>'. If filenames don't start with the package name, they are prefixed. Man files must end with a number indicating the man section, optionally followed by '.gz'.

```json
{
  "name": "foo",
  "version": "1.2.3",
  "description": "A packaged foo fooer for fooing foos",
  "main": "foo.js",
  "man": "./man/doc.1"
}
```

```json
{
  "name": "foo",
  "version": "1.2.3",
  "description": "A packaged foo fooer for fooing foos",
  "main": "foo.js",
  "man": ["./man/foo.1", "./man/bar.1"]
}
```

```json
{
  "name": "foo",
  "version": "1.2.3",
  "description": "A packaged foo fooer for fooing foos",
  "main": "foo.js",
  "man": ["./man/foo.1", "./man/foo.2"]
}
```

--------------------------------

### Test Local npm Package Installation

Source: https://docs.npmjs.com/creating-and-publishing-unscoped-public-packages

Installs a local npm package to test its functionality before publishing. This command allows developers to simulate the installation process and verify package integrity.

```shell
npm install path/to/my-package
```

--------------------------------

### Install a Global Package Without Sudo

Source: https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally

This command demonstrates installing a global npm package after reconfiguring npm's directory. It verifies the new configuration by successfully installing the package without requiring superuser privileges.

```bash
npm install -g npm-check-updates
```

--------------------------------

### Run an Installed Global Command

Source: https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally

This command executes a globally installed package's command-line interface. It verifies that the package installed in the custom directory is accessible and executable.

```bash
ncu -g
```

--------------------------------

### npm audit fix command examples

Source: https://docs.npmjs.com/cli/audit

Demonstrates various ways to use the `npm audit fix` command for vulnerability remediation. This includes automatically installing updates, updating only the package lock, skipping dev dependencies, forcing SemVer-major updates, and performing a dry run with JSON output.

```bash
# Scan your project for vulnerabilities and automatically install any compatible updates to vulnerable dependencies:
$ npm audit fix

# Run `audit fix` without modifying `node_modules`, but still updating the pkglock:
$ npm audit fix --package-lock-only

# Skip updating `devDependencies`:
$ npm audit fix --only=prod

# Have `audit fix` install SemVer-major updates to toplevel dependencies, not just SemVer-compatible ones:
$ npm audit fix --force

# Do a dry run to get an idea of what `audit fix` will do, and _also_ output install information in JSON format:
$ npm audit fix --dry-run --json
```

--------------------------------

### npm install with --force flag

Source: https://docs.npmjs.com/cli/v11/commands/npm-install

Force npm to fetch remote resources even if a local copy exists on disk, useful for ensuring the latest version or resolving caching issues.

```bash
npm install sax --force
```

--------------------------------

### Initialize a Scoped npm Package with Defaults (CLI)

Source: https://docs.npmjs.com/cli/adduser

This command initializes a new npm package with a specified scope, accepting all default settings. It creates a package name prefixed with the scope, for example, '@foo/whatever', instead of a simple name like 'whatever'. This is useful for organizing packages within an organization or project.

```bash
# accept all defaults, and create a package named "@foo/whatever",
# instead of just named "whatever"
npm init --scope=@foo --yes
```

--------------------------------

### npm init (Legacy)

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Falls back to legacy init behavior, asking questions to generate a package.json file.

```APIDOC
## POST /npm/init/legacy

### Description
When no initializer is provided, `npm init` falls back to its legacy behavior. It prompts the user with a series of questions to gather information and then generates a `package.json` file. It attempts to make reasonable guesses based on existing fields, dependencies, and selected options, and it is strictly additive, preserving existing fields.

### Method
POST

### Endpoint
`/npm/init/legacy`

### Parameters
#### Query Parameters
- **yes** (boolean) - Optional - Skips the questionnaire and uses default values.
- **scope** (string) - Optional - If passed, it will create a scoped package.

### Request Body
```json
{
  "init-author-name": "John Doe",
  "init-author-email": "john.doe@example.com",
  "init-author-url": "http://example.com"
}
```

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating successful `package.json` creation.

#### Response Example
```json
{
  "message": "package.json created successfully."
}
```
```

--------------------------------

### Default package.json with npm init --yes

Source: https://docs.npmjs.com/creating-a-package-json-file

An example output of the `npm init --yes` command, which creates a default `package.json` file using information extracted from the current directory. This includes common fields like name, version, description, scripts, repository, author, and license.

```json
{
  "name": "my_package",
  "description": "make your package easier to find on the npm website",
  "version": "1.0.0",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/monatheoctocat/my_package.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/monatheoctocat/my_package/issues"
  },
  "homepage": "https://github.com/monatheoctocat/my_package"
}
```

--------------------------------

### Install npm packages from GitHub Gists

Source: https://docs.npmjs.com/cli/install

Installs npm packages from GitHub Gists using their ID. Supports specifying versions via commit-ish or semver ranges. The GitHub username is optional. If no commit-ish is provided, the default branch is used.

```bash
npm install gist:101a11beef
```

--------------------------------

### Executing npm stop and its output

Source: https://docs.npmjs.com/cli/v11/commands/npm-stop

This example shows the command to execute the 'stop' script defined in package.json and the expected output from npm. It indicates that the 'stop' script is being run and displays any output from the executed command (in this case, 'node bar.js').

```bash
npm stop

> npm@x.x.x stop
> node bar.js

(bar.js output would be here)
```

--------------------------------

### Production Dependencies Installation

Source: https://docs.npmjs.com/cli/install

When the `--production` flag is used or `NODE_ENV` is set to `production`, `npm install` will not install packages listed in `devDependencies`. To install all dependencies (including devDependencies) when `NODE_ENV` is `production`, use `--production=false`.

```bash
npm install --production
npm install --production=false
```

--------------------------------

### npm init: Transforming to npm exec

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Illustrates how npm init commands are internally transformed into equivalent npm exec commands. This mapping is crucial for understanding how initializer packages are fetched and executed.

```bash
# npm init foo -> npm exec create-foo
# npm init @usr/foo -> npm exec @usr/create-foo
# npm init @usr -> npm exec @usr/create
# npm init @usr@2.0.0 -> npm exec @usr/create@2.0.0
# npm init @usr/foo@2.0.0 -> npm exec @usr/create-foo@2.0.0
```

--------------------------------

### Install Local Package for Testing

Source: https://docs.npmjs.com/private-modules/intro

Installs your local package into the current environment for testing purposes. This command uses the package name defined in your package.json file.

```shell
npm install my-package
```

--------------------------------

### npm config Synopsis

Source: https://docs.npmjs.com/cli/config

This section outlines the basic syntax for using the npm config command and its sub-commands. It covers setting, getting, deleting, listing, editing, and fixing configuration values.

```bash
npm config set <key>=<value> [<key>=<value> ...]
npm config get [<key> [<key> ...]]
npm config delete <key> [<key> ...]
npm config list [--json]
npm config edit
npm config fix

alias: c
```

--------------------------------

### Array of Objects Matching with Specific Attribute

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

This example demonstrates how to query an array of objects for a specific attribute value. It selects dependencies based on the contributor's email address.

```npm-query
/* returns */
*: attr(contributors, [email=ruyadorno @github.com]);
```

--------------------------------

### npm init -w <dir>

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Creates a new workspace within a project and updates the top-level package.json.

```APIDOC
## POST /npm/init/workspace

### Description
Creates a new workspace within the current project. This command generates the necessary folders and boilerplate for the workspace, and also updates the top-level `package.json` file to include a reference to the new workspace in the `"workspaces": []` property.

### Method
POST

### Endpoint
`/npm/init/workspace`

### Parameters
#### Query Parameters
- **dir** (string) - Required - The directory where the new workspace will be created (e.g., `packages/a`).
- **initializer** (string) - Optional - An initializer package to use for the workspace (e.g., `react-app`).
- **yes** (boolean) - Optional - Skips the questionnaire and uses default values.

### Request Body
```json
{
  "dir": "packages/my-new-workspace",
  "initializer": "react-app",
  "options": {
    "yes": true
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating successful workspace creation.

#### Response Example
```json
{
  "message": "Workspace created successfully."
}
```
```

--------------------------------

### Map Command Names to Executable Files

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'bin' field maps command names to local file names, allowing packages to install executable files into the system's PATH. When installed globally or as a dependency, these commands become accessible via npm exec or within scripts.

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "bin": {
    "myapp": "bin/cli.js"
  }
}
```

```json
{
  "name": "my-program",
  "version": "1.2.5",
  "bin": "path/to/program"
}
```

--------------------------------

### Dependency Inclusion and Exclusion

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Configure which types of dependencies are installed or omitted. The `--include` option specifies dependency types to install, acting as the inverse of `--omit`.

```APIDOC
## `include`

### Description
Option that allows for defining which types of dependencies to install. This is the inverse of `--omit=<type>`.
Dependency types specified in `--include` will not be omitted, regardless of the order in which omit/include are specified on the command-line.

### Type
"prod", "dev", "optional", or "peer" (can be set multiple times)

### Default
N/A
```

--------------------------------

### Default 'start' script for server.js

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

If a 'server.js' file exists in the package root, npm defaults the 'scripts.start' command to 'node server.js'. This is useful for packages that include a main server file.

```json
{
  "scripts": {
    "start": "node server.js"
  }
}
```

--------------------------------

### Install npm packages from Git repositories (SSH/HTTPS)

Source: https://docs.npmjs.com/cli/install

Installs npm packages directly from Git repositories using SSH or HTTPS URLs. Supports specifying versions via commit-ish or semver ranges. Recognizes various Git environment variables for authentication and proxying.

```bash
npm install git+ssh://git@github.com:npm/cli.git#v1.0.27
npm install git+ssh://git@github.com:npm/cli#pull/273
npm install git+ssh://git@github.com:npm/cli#semver:^5.0
npm install git+https://isaacs@github.com/npm/cli.git
npm install git://github.com/npm/cli.git#v1.0.27
GIT_SSH_COMMAND='ssh -i ~/.ssh/custom_ident' npm install git+ssh://git@github.com:npm/cli.git
```

--------------------------------

### npm outdated Configuration Options

Source: https://docs.npmjs.com/cli/v11/commands/npm-outdated

Illustrates how to use configuration options with the npm outdated command, such as --all to show all dependencies, --json for machine-readable output, --long for extended details, --parseable for script-friendly output, and --global for checking globally installed packages.

```bash
# Check all dependencies, including meta-dependencies
npm outdated --all

# Output results in JSON format
npm outdated --json

# Show extended information
npm outdated --long

# Output parseable results
npm outdated --parseable

# Check globally installed packages
npm outdated --global
```

--------------------------------

### Get npm Configuration Value

Source: https://docs.npmjs.com/cli/config

The `npm config get` command retrieves and prints the value(s) of specified configuration keys to standard output. If multiple keys are provided, their values are prefixed with the key names.

```bash
npm config get [key ...]
npm get [key ...]
```

--------------------------------

### npm init: Forwarding Options to Initializers

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Demonstrates how additional command-line options passed to npm init are forwarded to the underlying initializer package. This allows for customization of the initialization process.

```bash
# npm init foo -- --hello will map to `npm exec create-foo -- --hello`
# npm init foo -y --registry=<url> -- --hello -a is equivalent to `npm exec -y --registry=<url> -- create-foo --hello -a`
```

--------------------------------

### Npm Dependency Version Ranges Example

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Demonstrates various ways to specify version ranges for dependencies in an Npm package.json file, including exact versions, ranges, approximate equivalences, and wildcards.

```json
{
  "dependencies": {
    "foo": "1.0.0 - 2.9999.9999",
    "bar": ">=1.0.2 <2.1.2",
    "baz": ">1.0.2 <=2.3.4",
    "boo": "2.0.1",
    "qux": "<1.0.0 || >=2.3.1 <2.4.5 || >=2.5.2 <3.0.0",
    "asd": "http://npmjs.com/example.tar.gz",
    "til": "~1.2",
    "elf": "~1.2.3",
    "two": "2.x",
    "thr": "3.3.x",
    "lat": "latest",
    "dyl": "file:../dyl",
    "kpg": "npm:pkg@1.0.0"
  }
}
```

--------------------------------

### Piping npm query to jq and xargs

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Demonstrates how to pipe the output of `npm query` to `jq` for JSON processing and `xargs` for executing commands on the results. This example finds dependencies with postinstall scripts and uninstalls them.

```bash
# find all dependencies with postinstall scripts & uninstall them
npm query ":attr(scripts, [postinstall])" | jq 'map(.name)|join("\n")' -r | xargs -I {} npm uninstall {}
```

--------------------------------

### npm init: Creating a React App Workspace

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Demonstrates creating a React application as a nested workspace using `npm init` with both the `-w` flag and a specific initializer (`react-app`). It highlights that `npm exec` runs in the context of the new workspace directory.

```bash
npm init -w packages/my-react-app react-app .
```

--------------------------------

### Retrieve Info Across Workspaces using npm pkg get --ws

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Illustrates retrieving 'name' and 'version' from all configured workspaces and displays the result in a JSON object keyed by workspace name.

```bash
npm pkg get name version --ws
```

--------------------------------

### Example SPDX SBOM Generation

Source: https://docs.npmjs.com/cli/v11/commands/npm-sbom

This JSON object represents an example SPDX SBOM for a simple npm package. It includes details about the package, its dependencies, and relationships between them. The SBOM format is SPDX-2.3, and it was generated using the npm CLI.

```json
{
  "spdxVersion": "SPDX-2.3",
  "dataLicense": "CC0-1.0",
  "SPDXID": "SPDXRef-DOCUMENT",
  "name": "simple@1.0.0",
  "documentNamespace": "http://spdx.org/spdxdocs/simple-1.0.0-bf81090e-8bbc-459d-bec9-abeb794e096a",
  "creationInfo": {
    "created": "2023-09-01T00:00:00.001Z",
    "creators": ["Tool: npm/cli-10.1.0"]
  },
  "documentDescribes": ["SPDXRef-Package-simple-1.0.0"],
  "packages": [
    {
      "name": "simple",
      "SPDXID": "SPDXRef-Package-simple-1.0.0",
      "versionInfo": "1.0.0",
      "packageFileName": "",
      "description": "simple react app",
      "primaryPackagePurpose": "LIBRARY",
      "downloadLocation": "NOASSERTION",
      "filesAnalyzed": false,
      "homepage": "NOASSERTION",
      "licenseDeclared": "MIT",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:npm/simple@1.0.0"
        }
      ]
    },
    {
      "name": "lodash",
      "SPDXID": "SPDXRef-Package-lodash-4.17.21",
      "versionInfo": "4.17.21",
      "packageFileName": "node_modules/lodash",
      "description": "Lodash modular utilities.",
      "downloadLocation": "https://registry.npmjs.org/lodash/-/lodash-4.17.21.tgz",
      "filesAnalyzed": false,
      "homepage": "https://lodash.com/",
      "licenseDeclared": "MIT",
      "externalRefs": [
        {
          "referenceCategory": "PACKAGE-MANAGER",
          "referenceType": "purl",
          "referenceLocator": "pkg:npm/lodash@4.17.21"
        }
      ],
      "checksums": [
        {
          "algorithm": "SHA512",
          "checksumValue": "bf690311ee7b95e713ba568322e3533f2dd1cb880b189e99d4edef13592b81764daec43e2c54c61d5c558dc5cfb35ecb85b65519e74026ff17675b6f8f916f4a"
        }
      ]
    }
  ],
  "relationships": [
    {
      "spdxElementId": "SPDXRef-DOCUMENT",
      "relatedSpdxElement": "SPDXRef-Package-simple-1.0.0",
      "relationshipType": "DESCRIBES"
    },
    {
      "spdxElementId": "SPDXRef-Package-simple-1.0.0",
      "relatedSpdxElement": "SPDXRef-Package-lodash-4.17.21",
      "relationshipType": "DEPENDS_ON"
    }
  ]
}
```

--------------------------------

### npm init: Legacy package.json Generation

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Demonstrates the legacy behavior of npm init, which interactively prompts the user to create a package.json file. This is useful for simple projects or when an initializer is not needed.

```bash
mkdir my-npm-pkg && cd my-npm-pkg
git init
$ npm init
```

--------------------------------

### Retrieve All Array Elements using npm pkg get

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Demonstrates retrieving all 'email' values from the 'contributors' array in package.json.

```bash
npm pkg get contributors.email
```

--------------------------------

### Install Scoped Package using npm CLI

Source: https://docs.npmjs.com/cli/v11/using-npm/scope

Shows how to install a scoped package using the npm command-line interface. The package name must be prefixed with the scope.

```bash
npm install @myorg/mypackage
```

--------------------------------

### Git URL Dependency Formats

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Illustrates the structure and examples of Git URLs used for specifying dependencies in Npm. Supports various protocols and commit-ish identifiers for precise versioning.

```text
<protocol>://[<user>[:<password>]@]<hostname>[:<port>][:][/]<path>[#<commit-ish> | #semver:<semver>]
```

```text
git+ssh://git@github.com:npm/cli.git#v1.0.27
git+ssh://git@github.com:npm/cli#semver:^5.0
git+https://isaacs@github.com/npm/cli.git
git://github.com/npm/cli.git#v1.0.27
```

--------------------------------

### npm pkg Synopsis

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Displays the general syntax for the npm pkg command, including its subcommands for setting, getting, deleting, and fixing package.json properties.

```bash
npm pkg set <key>=<value> [<key>=<value> ...]
npm pkg get [<key> [<key> ...]]
npm pkg delete <key> [<key> ...]
npm pkg set [<array>[<index>].<key>=<value> ...]
npm pkg set [<array>[].<key>=<value> ...]
npm pkg fix
```

--------------------------------

### Display npm help for a specific term

Source: https://docs.npmjs.com/cli/v11/commands/npm-help

The 'npm help' command displays documentation for a given term. If the term is not found or multiple terms are provided, it defaults to 'npm help-search'. The 'viewer' configuration can be set to 'browser' to open HTML help in a web browser.

```bash
npm help <term> [<terms..>]
# alias: hlep
```

--------------------------------

### npm Script Execution with Dependencies

Source: https://docs.npmjs.com/cli/v11/using-npm/scripts

Demonstrates how to execute scripts from dependencies. When a package is installed, its executable scripts are added to the PATH, allowing them to be called directly from the 'scripts' section of package.json. This requires the dependency to define executables in its 'bin' field.

```json
{
  "name": "foo",
  "dependencies": {
    "bar": "0.1.x"
  },
  "scripts": {
    "start": "bar ./test"
  }
}
```

--------------------------------

### npm init: Specifying Initializer Versions

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Shows how to explicitly control which version of an initializer package npm init should use. This is important for ensuring consistent project setups or utilizing specific features of an initializer.

```bash
# npm init foo@latest # fetches and runs the latest `create-foo` from the registry
# npm init foo@1.2.3 # runs `create-foo@1.2.3` specifically
```

--------------------------------

### Check npm Version

Source: https://docs.npmjs.com/try-the-latest-stable-version-of-npm

This command displays the currently installed version of npm. It's a simple utility command with no external dependencies.

```bash
npm -v
```

--------------------------------

### Retrieve Package Name using npm pkg get

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Demonstrates how to retrieve the 'name' field from the package.json file using the 'npm pkg get' command.

```bash
npm pkg get name
```

--------------------------------

### Retrieve Multiple Fields using npm pkg get

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Shows how to retrieve multiple fields, such as 'name' and 'version', from the package.json file simultaneously.

```bash
npm pkg get name version
```

--------------------------------

### Explore Package Directory with npm

Source: https://docs.npmjs.com/cli/v11/commands/npm-explore

This command spawns a subshell in the directory of the specified installed package. It's useful for directly accessing and inspecting package files within your project's node_modules.

```bash
npm explore <pkg> [ -- <command>]
```

--------------------------------

### Example npm query response structure

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Illustrates the typical JSON structure of the output from an `npm query` command, showing the properties of a dependency object.

```json
[
  {
    "name": "",
    "version": "",
    "description": "",
    "homepage": "",
    "bugs": {},
    "author": {},
    "license": {},
    "funding": {},
    "files": [],
    "main": "",
    "browser": "",
    "bin": {},
    "man": [],
    "directories": {},
    "repository": {},
    "scripts": {},
    "config": {},
    "dependencies": {},
    "devDependencies": {},
    "optionalDependencies": {},
    "bundledDependencies": {},
    "peerDependencies": {},
    "peerDependenciesMeta": {},
    "engines": {},
    "os": [],
    "cpu": [],
    "workspaces": {},
    "keywords": [],
    ...
  },
  ...

]
```

--------------------------------

### Example of a Scoped Package Name

Source: https://docs.npmjs.com/cli/v11/using-npm/scope

Demonstrates the naming convention for scoped packages, which includes an '@' symbol followed by the scope name and a slash, then the package name.

```text
@somescope/somepackagename
```

--------------------------------

### Before Date Configuration

Source: https://docs.npmjs.com/cli/outdated

The `before` configuration option, when used with `npm install`, rebuilds the npm tree to install only versions available on or before a specified date.

```APIDOC
## `before` Configuration Option

### Description
If passed to `npm install`, will rebuild the npm tree such that only versions that were available **on or before** the given date are installed. If there are no versions available for the current set of dependencies, the command will error. If the requested version is a `dist-tag` and the given tag does not pass the `--before` filter, the most recent version less than or equal to that tag will be used. For example, `foo@latest` might install `foo@1.2` even though `latest` is `2.0`.

### Type
null or Date

### Default
null

### Restrictions
This config cannot be used with: `min-release-age`
```

--------------------------------

### Execute Local or Remote Package Commands with npx

Source: https://docs.npmjs.com/cli/commands/npx

Demonstrates how to run a package's binary, passing arguments directly to the executed command. This includes examples for running 'tap' and executing a command other than the default package binary using '--package'.

```bash
$ npm exec -- tap --bail test/foo.js
$ npx tap --bail test/foo.js
```

```bash
$ npm exec --package=foo -- bar --bar-argument
# ~ or ~
$ npx --package=foo bar --bar-argument
```

--------------------------------

### npm publish

Source: https://docs.npmjs.com/cli/v11/commands/npm-publish

Publishes a package to the npm registry. This command makes your package available for others to install using `npm install`.

```APIDOC
## POST /publish

### Description
Publishes a package to the registry so that it can be installed by name.

### Method
POST

### Endpoint
/publish

### Parameters
#### Query Parameters
- **workspace** (string) - Optional - Specifies a workspace to publish.
- **workspaces** (boolean) - Optional - Publishes all workspaces.

#### Request Body
- **package-spec** (string) - Optional - Specifies the package to publish (e.g., a folder, tarball, URL, or package name@version).

### Request Example
```json
{
  "package-spec": "./my-package"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message that the package was published successfully.

#### Response Example
```json
{
  "message": "Package 'my-package' published successfully."
}
```

### Configuration
- **tag** (string) - Default: "latest" - The tag to associate with the published package version.
- **access** (null | "restricted" | "public") - Default: 'public' for new packages, existing packages retain their level - Controls the visibility of scoped packages. Unscoped packages are always public.
- **dry-run** (boolean) - Default: false - If true, npm will report what it would have done without making any changes.
```

--------------------------------

### Iterative Dependency Querying with Arborist

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

This example shows an iterative approach to querying the dependency tree. It first queries for a specific dependency (deduped react) and then queries within the results for dependencies of a specific type (git).

```javascript
const Arborist = require("@npmcli/arborist");
const arb = new Arborist({});

// iterative
arb.loadActual().then(async (tree) => {
  // query for the deduped version of react
  const results = await tree.querySelectorAll("#react:not(:deduped)");
  // query the deduped react for git deps
  const deps = await results[0].querySelectorAll(":type(git)");
  console.log(deps);
});
```

--------------------------------

### Local Path Dependency Example

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Demonstrates how to specify local directory paths as dependencies in Npm's package.json. This is useful for offline development but not recommended for public packages.

```json
{
  "name": "baz",
  "dependencies": {
    "bar": "file:../foo/bar"
  }
}
```

--------------------------------

### npm Version with Script Execution

Source: https://docs.npmjs.com/cli/v11/commands/npm-version

This example illustrates how to define scripts in package.json that execute before, during, and after the npm version command. 'preversion' runs before bumping the version, 'version' runs after bumping but before committing, and 'postversion' runs after the commit and tag are created. Scripts can access old and new versions and interact with git.

```json
{
  "scripts": {
    "preversion": "npm test",
    "version": "npm run build && git add -A dist",
    "postversion": "git push && git push --tags && rm -rf build/temp"
  }
}
```

--------------------------------

### Publishing and Testing a Node.js Module

Source: https://docs.npmjs.com/creating-node-js-modules

Commands for publishing a Node.js module to npm and then testing it. Publishing requires 2FA or a granular access token. Testing involves creating a separate directory, installing the module, and running a test script.

```bash
mkdir test-directory
cd /path/to/test-directory
npm install <your-module-name>
node test.js
```

```bash
npm publish
npm publish --access public
```

--------------------------------

### npm audit command examples

Source: https://docs.npmjs.com/cli/audit

Illustrates different ways to use the `npm audit` command for vulnerability scanning. This includes basic scanning, obtaining detailed JSON reports, and setting minimum audit levels.

```bash
# Scan your project for vulnerabilities and just show the details, without fixing anything:
$ npm audit

# Get the detailed audit report in JSON format:
$ npm audit --json

# Fail an audit only if the results include a vulnerability with a level of moderate or higher:
$ npm audit --audit-level=moderate
```

--------------------------------

### npm config get

Source: https://docs.npmjs.com/cli/config

Retrieves and displays the value(s) of specified npm configuration keys.

```APIDOC
## GET /npm config get

### Description
Echo the config value(s) to stdout. If multiple keys are provided, then the values will be prefixed with the key names. If no keys are provided, then this command behaves the same as `npm config list`.

### Method
GET

### Endpoint
/npm config get

### Parameters
#### Query Parameters
- **key** (string) - Optional - The configuration key(s) to retrieve. If multiple keys are provided, they should be comma-separated or passed as multiple query parameters.

### Request Example
```http
GET /npm config get?key=registry,loglevel
```

### Response
#### Success Response (200)
- **key** (string) - The configuration key.
- **value** (string) - The value of the configuration key.

#### Response Example
```json
{
  "registry": "https://registry.npmjs.org/",
  "loglevel": "info"
}
```
```

--------------------------------

### Set Global npm Package Prefix (Windows)

Source: https://docs.npmjs.com/try-the-latest-stable-version-of-npm

This command configures the directory where npm installs global packages on Windows. It's used to correct installation paths and ensure global packages are accessible. It requires administrator privileges.

```bash
npm config set prefix %APPDATA%\npm -g
```

--------------------------------

### bundleDependencies Example in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The bundleDependencies field specifies an array of package names that should be bundled together when publishing the package. This allows for creating a single tarball containing specific dependencies, useful for local preservation or single-file distribution. The example lists '@npm/renderized' and '@npm/super-streams' to be bundled.

```json
{
  "name": "@npm/awesome-web-framework",
  "version": "1.0.0",
  "bundleDependencies": ["@npm/renderized", "@npm/super-streams"]
}
```

--------------------------------

### Display Global npm Prefix

Source: https://docs.npmjs.com/cli/v11/commands/npm-prefix

This command prints the global prefix to standard output when the -g flag is specified. The global prefix is the directory where globally installed packages are located. Refer to 'npm config' for more details on global configuration.

```bash
npm prefix -g
```

--------------------------------

### Install Latest npm Version Globally

Source: https://docs.npmjs.com/about-npm-versions

This command installs the most recent stable version of the npm CLI globally on your system. It ensures you have the latest features and bug fixes. This command requires administrative privileges on some systems.

```bash
npm install npm@latest -g
```

--------------------------------

### npm init: Setting package.json private flag

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Example of using npm init with the `--init-private` flag and `-y` to set the `private` field to `true` in the generated package.json file without interactive prompts.

```bash
$ npm init --init-private -y
```

--------------------------------

### Log in to a Custom Registry with a Scope (CLI)

Source: https://docs.npmjs.com/cli/adduser

This command logs you into a specified npm registry and links a given scope to it. This mapping ensures that packages within that scope are installed from the custom registry. It's useful for managing private registries and scoped packages.

```bash
# log in, linking the scope to the custom registry
npm login --scope=@mycorp --registry=https://registry.mycorp.com
```

--------------------------------

### Comments and Scoped Registry Configuration in .npmrc

Source: https://docs.npmjs.com/cli/v11/configuring-npm/npmrc

Shows how to use comments (lines starting with ';' or '#') and how to configure registries for specific scoped packages.

```ini
# last modified: 01 Jan 2016
; Set a new registry for a scoped package
@myscope:registry=https://mycustomregistry.example.org
```

--------------------------------

### Initialize a new workspace with npm init

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

This command automates the creation of a new workspace. It creates necessary folders, a `package.json` file if it doesn't exist, and configures the root `package.json`'s `workspaces` property.

```bash
npm init -w ./packages/a
```

--------------------------------

### Update npm to Latest Version

Source: https://docs.npmjs.com/downloading-and-installing-node-js-and-npm

Command to update the npm package manager to its latest available version. This ensures you have the newest features and security patches.

```shell
npm install -g npm
```

--------------------------------

### Npm Package 'bin' Field Configuration (Map)

Source: https://docs.npmjs.com/files/package

The 'bin' field configures executable files for a package. When provided as a map, it defines command names and their corresponding local file paths. These executables are made available in the system's PATH when installed globally or via 'npm exec' when installed as a dependency.

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "bin": {
    "myapp": "bin/cli.js"
  }
}
```

--------------------------------

### Example package.json Dependencies

Source: https://docs.npmjs.com/cli/outdated

This JSON snippet represents a `package.json` file, showcasing the dependencies for which `npm outdated` would check versions. It includes version ranges and a git dependency, illustrating how different dependency types are handled.

```json
{
  "glob": "^5.0.15",
  "nothingness": "github:othiym23/nothingness#master",
  "npm": "^3.5.1",
  "once": "^1.3.1"
}
```

--------------------------------

### Dry Run Mode

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Simulate npm commands without making any changes. This option reports what would have happened but does not modify the local installation.

```APIDOC
## `dry-run`

### Description
Indicates that you don't want npm to make any changes and that it should only report what it would have done. This can be passed into any of the commands that modify your local installation, eg, `install`, `update`, `dedupe`, `uninstall`, as well as `pack` and `publish`. Note: This is NOT honored by other network related commands, eg `dist-tags`, `owner`, etc.

### Type
Boolean

### Default
`false`
```

--------------------------------

### Run Command in Package Directory with npm

Source: https://docs.npmjs.com/cli/v11/commands/npm-explore

Execute a specific command within the directory of an installed package. This is particularly handy for tasks like updating git submodules directly from within the package's location in node_modules.

```bash
npm explore some-dependency -- git pull origin master
```

--------------------------------

### Piping npm query to find git dependencies and explain requirements

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

This example uses `npm query` to find all Git dependencies and then pipes the result to `jq` and `xargs` to display which packages require them.

```bash
# find all git dependencies & explain who requires them
npm query ":type(git)" | jq 'map(.name)' | xargs -I {} npm why {}
```

--------------------------------

### Example of npm test execution

Source: https://docs.npmjs.com/cli/v11/commands/npm-test

This snippet illustrates the output when 'npm test' is executed. It shows the command being run and the expected output from the test script, which in this case is 'node test.js'.

```bash
npm test
> npm@x.x.x test
> node test.js

(test.js output would be here)
```

--------------------------------

### Link Local Package with npm

Source: https://docs.npmjs.com/cli/v11/using-npm/developers

Creates a symbolic link for the current package, allowing it to be linked globally. This is useful for real-time development and testing without repeated installations.

```bash
npm link
```

--------------------------------

### npm cache npx get info

Source: https://docs.npmjs.com/cli/v11/commands/npm-cache

Retrieves detailed information about specified entries in the npx cache.

```bash
npm cache npx info <key>...
```

--------------------------------

### Create npm User Account

Source: https://docs.npmjs.com/cli/v11/using-npm/developers

Initiates the process of creating a new user account on the npm registry. Follow the prompts to complete the account creation.

```bash
npm adduser
```

--------------------------------

### Add npm's New Bin Directory to PATH

Source: https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally

This command adds the new npm binary directory to the system's PATH environment variable. This ensures that globally installed packages can be executed directly from the command line. It's typically added to shell profile files like .profile or .zprofile.

```bash
PATH=~/.local/bin:$PATH
```

--------------------------------

### npm Package Git URL Formats

Source: https://docs.npmjs.com/about-packages-and-modules

Demonstrates various git URL formats that can be used to specify npm packages. These formats allow direct installation from git repositories. The 'commit-ish' can be a tag, SHA, or branch, defaulting to HEAD. Submodules and workspaces are not installed when using these formats.

```plaintext
git://github.com/user/project.git#commit-ish
git+ssh://user@hostname:project.git#commit-ish
git+http://user@hostname/project/blah.git#commit-ish
git+https://user@hostname/project/blah.git#commit-ish
```

--------------------------------

### Setting Client Key for Registry Access (Shell)

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Demonstrates how to set a client key for accessing an npm registry. The key should be in PEM format with newlines replaced by '\n'. This is an alternative to using a key file.

```shell
key="-----BEGIN PRIVATE KEY-----\nXXXX\nXXXX\n-----END PRIVATE KEY-----"
```

--------------------------------

### Funding Acknowledgement

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Enable or disable the display of messages acknowledging dependencies looking for funding after `npm install`. Defaults to true.

```APIDOC
## `fund`

### Description
When "true" displays the message at the end of each `npm install` acknowledging the number of dependencies looking for funding. See `npm fund` for details.

### Type
Boolean

### Default
`true`
```

--------------------------------

### Configure Node.js for Private Dependency Installation with GitHub Actions

Source: https://docs.npmjs.com/trusted-publishers

This GitHub Actions workflow snippet configures the Node.js environment for installing private npm dependencies. It sets up the specified Node.js version, configures the npm registry URL, and uses a read-only token for authentication during the 'npm ci' command. The actual package publish step uses OIDC, thus not requiring a token.

```yaml
# GitHub Actions example
- uses: actions/setup-node@v4
  with:
    node-version: '24'
    registry-url: 'https://registry.npmjs.org'
# Use a read-only token for installing dependencies
- run: npm ci
  env:
    NODE_AUTH_TOKEN: ${{ secrets.NPM_READ_TOKEN }}

# Publish uses OIDC - no token needed
- run: npm publish

```

--------------------------------

### Upgrade npm on *nix Systems

Source: https://docs.npmjs.com/try-the-latest-stable-version-of-npm

This command upgrades npm to the latest stable version on macOS and Linux systems. It requires npm to be installed and may require administrator privileges (sudo).

```bash
npm install -g npm@latest
```

--------------------------------

### Scoped Authentication Configuration in .npmrc

Source: https://docs.npmjs.com/cli/v11/configuring-npm/npmrc

Provides examples of how to securely configure authentication tokens and credentials for specific registries or paths using URI fragments.

```ini
; bad config
_authToken=MYTOKEN


; good config
@myorg:registry=https://somewhere-else.com/myorg
@another:registry=https://somewhere-else.com/another
//registry.npmjs.org/:_authToken=MYTOKEN


; would apply to both @myorg and @another
//somewhere-else.com/:_authToken=MYTOKEN


; would apply only to @myorg
//somewhere-else.com/myorg/:_authToken=MYTOKEN1


; would apply only to @another
//somewhere-else.com/another/:_authToken=MYTOKEN2
```

--------------------------------

### Checking for outdated production dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

An example of using `npm query` with `--no-expect-results` to find production dependencies that are outdated, without causing the command to exit if results are found.

```bash
$ npm query ':root>:outdated(in-range).prod' --no-expect-results
```

--------------------------------

### Link Global Package into Project (npm link <package-name>)

Source: https://docs.npmjs.com/cli/v11/commands/npm-link

Links a globally installed package into the `node_modules` directory of the current project. This allows the project to use the globally linked package as if it were installed normally. The package name is derived from the `package.json` file.

```bash
cd ~/projects/node-bloggy
npm link redis
```

--------------------------------

### All Workspaces Context

Source: https://docs.npmjs.com/misc/config

Runs commands in the context of all configured workspaces.

```APIDOC
## `workspaces`

### Description
Set to true to run the command in the context of **all** configured workspaces. Explicitly setting this to false will cause commands like `install` to ignore workspaces altogether. When not set explicitly: Commands that operate on the `node_modules` tree (install, update, etc.) will link workspaces into the `node_modules` folder. Commands that do other things (test, exec, publish, etc.) will operate on the root project, _unless_ one or more workspaces are specified in the `workspace` config. This value is not exported to the environment for child processes.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **workspaces** (Boolean) - Optional - Set to true to enable all workspaces context.

### Request Example
```
npm install --workspaces
```

### Response
#### Success Response (200)
Command executed in the context of all workspaces.

#### Response Example
N/A
```

--------------------------------

### List npm-related Files and Symlinks

Source: https://docs.npmjs.com/cli/v11/using-npm/removal

This command lists all files and symbolic links related to npm within specified directories. It helps identify any remaining npm artifacts after uninstallation, especially symlinks.

```bash
ls -laF /usr/local/{lib/node{,/.npm},bin,share/man} | grep npm
```

--------------------------------

### Update Globally Installed Packages (CLI)

Source: https://docs.npmjs.com/cli/update

Use the `-g` flag with `npm update` to update all globally installed packages that are outdated. These packages are treated as if they have a caret semver range, and updating may downgrade packages newer than 'latest'.

```bash
npm update -g
```

--------------------------------

### Define a package script using local binaries

Source: https://docs.npmjs.com/cli/v11/commands/npm-run

Demonstrates how to define a script in package.json that utilizes binaries from local dependencies. npm automatically adds 'node_modules/.bin' to the PATH, allowing direct use of installed package executables.

```json
"scripts": {"test": "tap test/*.js"}
```

--------------------------------

### Manually querying git dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Provides examples of manually specifying conditions to find Git dependencies based on repository URL patterns.

```bash
[repository^=github:],
[repository^=git:],
[repository^=https://github.com],
[repository^=http://github.com],
[repository^=https://github.com],
[repository^=+git:...]
```

--------------------------------

### Retrieve Specific Array Element using npm pkg get

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Shows how to retrieve the 'email' of the first contributor from the 'contributors' array using numeric indexing.

```bash
npm pkg get contributors[0].email
```

--------------------------------

### npm init: Creating a New Workspace (Legacy Init)

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Illustrates how to create a new workspace within a project using the legacy npm init command with the `-w` flag. This automatically updates the top-level package.json to include the new workspace.

```bash
$ npm init -w packages/a
```

--------------------------------

### Configure npm to Use a Different Directory

Source: https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally

This command configures npm to use a new directory for global installations, helping to avoid EACCES permissions errors. It sets the prefix to a hidden directory within the user's home folder.

```bash
npm config set prefix "~/.local"
```

--------------------------------

### npm Script Configuration for Lifecycle Events

Source: https://docs.npmjs.com/misc/scripts

Defines npm scripts in package.json for different lifecycle events like 'prepare', 'build', and 'test'. This allows for automated tasks during package installation and testing.

```json
{
  "scripts": {
    "prepare": "scripts/build.js",
    "build": "tsc",
    "test": "jest"
  }
}
```

--------------------------------

### Help Viewer Configuration

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Specifies the program used to view npm help content.

```APIDOC
## `viewer`

### Description
The program to use to view help content. Set to `"browser"` to view html help content in the default web browser.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **viewer** (String) - Default: "man" on Posix, "browser" on Windows - Description: The program to use to view help content.

### Request Example
```json
{
  "viewer": "browser"
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Git Dependency Restrictions

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Limit npm's ability to fetch dependencies from git references. Options include 'all', 'none', and 'root' to control git dependency installation.

```APIDOC
## `allow-git`

### Description
Limits the ability for npm to fetch dependencies from git references. That is, dependencies that point to a git repo instead of a version or semver range. Please note that this could leave your tree incomplete and some packages may not function as intended or designed. `all` allows any git dependencies to be fetched and installed. `none` prevents any git dependencies from being fetched and installed. `root` only allows git dependencies defined in your project's package.json to be fetched installed. Also allows git dependencies to be fetched for other commands like `npm view`

### Type
"all", "none", or "root"

### Default
"all"
```

--------------------------------

### Workspace Update Configuration

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Controls whether npm automatically runs an update after operations that might change installed workspaces.

```APIDOC
## `workspaces-update`

### Description
If set to true, the npm cli will run an update after operations that may possibly change the workspaces installed to the `node_modules` folder.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **workspaces-update** (Boolean) - Default: true - Description: Automatically run an update after workspace-related operations.

### Request Example
```json
{
  "workspaces-update": false
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### npm Command Line Shorthand Expansion

Source: https://docs.npmjs.com/misc/config

Illustrates how npm expands shorthand command-line arguments into their full configuration parameter names. This includes single-character shorthands and combined shorthands.

```bash
npm ls --par
# same as:
npm ls --parseable

npm ls -gpld
# same as:
npm ls --global --parseable --long --loglevel info
```

--------------------------------

### npm exec with --call option

Source: https://docs.npmjs.com/cli/v11/commands/npm-exec

Demonstrates how to use the --call option with npm exec to specify a custom command to be run alongside installed packages.

```bash
npm exec --package yo --package generator-node --call "yo node"
```

--------------------------------

### Setting npm Configuration via Command Line Flags

Source: https://docs.npmjs.com/misc/config

Demonstrates how to set npm configuration parameters directly on the command line. Values can be provided after the flag, and `--` signifies the end of flag parsing. Flags without values default to `true`.

```bash
npm install --prefix /path/to/dir
npm install --global
npm install --save-dev
npm install --flag1 --flag2
npm install --flag1 --flag2 bar
npm install --flag1 --flag2 -- bar
```

--------------------------------

### Example package.json script for npm stop

Source: https://docs.npmjs.com/cli/v11/commands/npm-stop

This JSON snippet demonstrates how to define a 'stop' script within the 'scripts' object of a package.json file. The 'stop' script is configured to run a Node.js script named 'bar.js'.

```json
{
  "scripts": {
    "stop": "node bar.js"
  }
}
```

--------------------------------

### Customizing npm init questionnaire with .npm-init.js

Source: https://docs.npmjs.com/about-package-json-and-package-lock-json-files

Demonstrates how to customize the `npm init` questionnaire by adding custom questions and fields in the `.npm-init.js` file.

```javascript
module.exports = prompt("what's your favorite flavor of ice cream, buddy?", "I LIKE THEM ALL");
```

```javascript
module.exports = {
  customField: 'Example custom field',
  otherCustomField: 'This example field is really cool'
}
```

--------------------------------

### Run NPM Script in Multiple Workspaces

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

Execute an npm script across multiple specified workspaces. This allows for batch operations on selected packages within a monorepo. The example targets workspaces 'a' and 'b'.

```bash
npm run test --workspace=a --workspace=b
```

--------------------------------

### Create Global Package Link (npm link)

Source: https://docs.npmjs.com/cli/v11/commands/npm-link

Creates a symbolic link in the global npm installation directory that points to the current package folder. This is the first step in making a local package available for linking into other projects. It also links any executable bins defined in the package to the global bin directory.

```bash
cd ~/projects/node-redis
npm link
```

--------------------------------

### Basic package.json Structure for npm

Source: https://docs.npmjs.com/misc/developers

Illustrates the minimal required fields for a package.json file in an npm project. This file defines the package's identity, version, dependencies, and entry points.

```json
{
  "name": "your-package-name",
  "version": "1.0.0",
  "engines": {
    "node": ">=14.0.0"
  },
  "author": "Your Name <your.email@example.com>",
  "scripts": {
    "test": "echo \"No tests yet!\""
  },
  "main": "index.js",
  "directories": {
    "lib": "./lib",
    "doc": "./doc"
  }
}
```

--------------------------------

### Setting default npm init configuration options

Source: https://docs.npmjs.com/about-package-json-and-package-lock-json-files

Shows how to set default configuration values for the `npm init` command using `npm set` commands. This includes setting the default author email, author name, and license.

```bash
> npm set init-author-email "example-user@example.com"
> npm set init-author-name "example_user"
> npm set init-license "MIT"
```

--------------------------------

### Minimum Release Age Configuration

Source: https://docs.npmjs.com/cli/outdated

The `min-release-age` configuration option filters package installations to include only versions released more than a specified number of days ago.

```APIDOC
## `min-release-age` Configuration Option

### Description
If set, npm will build the npm tree such that only versions that were available more than the given number of days ago will be installed. If there are no versions available for the current set of dependencies, the command will error. This flag is a complement to `before`, which accepts an exact date instead of a relative number of days.

### Type
null or Number

### Default
null

### Restrictions
This config cannot be used with: `before`
```

--------------------------------

### Retrieve Nested Field using npm pkg get

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Illustrates retrieving a nested field, like the 'test' script, from the package.json file using dot notation.

```bash
npm pkg get scripts.test
```

--------------------------------

### Set Local Global npm Package Prefix (Windows)

Source: https://docs.npmjs.com/try-the-latest-stable-version-of-npm

This command configures npm to install global packages in the local app data directory on Windows, which can be useful for managing disk quotas or network drive performance. It requires administrator privileges.

```bash
npm config set prefix %LOCALAPPDATA%\npm -g
```

--------------------------------

### List all npm Configuration Settings

Source: https://docs.npmjs.com/cli/config

The `npm config list` command displays all current configuration settings. Use the `-l` flag to include default settings and the `--json` flag to output the settings in JSON format.

```bash
npm config list
```

--------------------------------

### npm access get status

Source: https://docs.npmjs.com/cli/access

Retrieves the current access status (public or private) of a package.

```APIDOC
## GET /npm/access/get/status

### Description
Retrieves the current access status (public or private) of a package.

### Method
GET

### Endpoint
`/npm/access/get/status`

### Parameters
#### Query Parameters
- **package** (string) - Optional - The name of the package. If not provided, uses the package in the current directory.

### Request Example
```json
{
  "example": "npm access get status [<package>]"
}
```

### Response
#### Success Response (200)
- **status** (string) - The access status of the package ('public' or 'private').

#### Response Example
```json
{
  "example": "public"
}
```
```

--------------------------------

### Git Not Found Error

Source: https://docs.npmjs.com/common-errors

This error indicates that the `git` command is not recognized. Ensure Git is installed and accessible in your system's PATH environment variable.

```bash
npm ERR! not found: git
ENOGIT
```

--------------------------------

### Initialize npm Package

Source: https://docs.npmjs.com/creating-and-publishing-unscoped-public-packages

Initializes a new npm package by creating a `package.json` file. This command prompts the user to provide metadata for the package, such as name, version, and description.

```shell
npm init
```

--------------------------------

### Log in to a scoped registry

Source: https://docs.npmjs.com/cli/v11/commands/npm-login

This command logs you into a specific npm registry associated with a given scope. It maps the scope to the custom registry, enabling installations of scoped packages and creation of scoped packages with `npm init`. The `--scope` and `--registry` flags are used to specify the scope and the registry URL, respectively.

```bash
npm login --scope=@mycorp --registry=https://registry.mycorp.com
```

--------------------------------

### Define test script in package.json

Source: https://docs.npmjs.com/cli/v11/commands/npm-test

This example demonstrates how to define a test script within the 'scripts' object of a package.json file. The 'test' property specifies the command to be executed when 'npm test' is run.

```json
{
  "scripts": {
    "test": "node test.js"
  }
}
```

--------------------------------

### Create a scoped package

Source: https://docs.npmjs.com/cli/v11/commands/npm-login

This command initializes a new npm package with a specified scope. The `--scope` flag defines the scope for the package, and the `--yes` flag accepts all default settings, creating a package with a name like `@foo/whatever` instead of just `whatever`.

```bash
npm init --scope=@foo --yes
```

--------------------------------

### GitHub Actions Workflow for Trusted Publishing

Source: https://docs.npmjs.com/trusted-publishers

This GitHub Actions workflow demonstrates how to configure trusted publishing for npm packages. It requires `id-token: write` permission for OIDC authentication and includes steps for checking out code, setting up Node.js, installing dependencies, building, testing, and publishing.

```yaml
name: Publish Package

on:
  push:
    tags:
      - 'v*'

permissions:
  id-token: write  # Required for OIDC
  contents: read

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: '24'
          registry-url: 'https://registry.npmjs.org'
      - run: npm ci
      - run: npm run build --if-present
      - run: npm test
      - run: npm publish

```

--------------------------------

### npm deprecate

Source: https://docs.npmjs.com/cli/v11/commands/npm-deprecate

Deprecates a specified version or version range of a package, providing a warning to users who attempt to install it. Requires package ownership.

```APIDOC
## POST /npm/deprecate

### Description
Deprecates a specified version or version range of a package, providing a warning to users who attempt to install it. Requires package ownership.

### Method
POST

### Endpoint
/npm/deprecate

### Parameters
#### Query Parameters
- **package-spec** (string) - Required - The package and version(s) to deprecate (e.g., "my-thing@"< 0.2.3", "my-thing@1.x").
- **message** (string) - Required - The deprecation message to display. Use an empty string ("") to un-deprecate.

### Request Example
```json
{
  "package-spec": "my-thing@\"< 0.2.3\"",
  "message": "critical bug fixed in v0.2.3"
}
```

### Response
#### Success Response (200)
- **status** (string) - Indicates the success of the operation.

#### Response Example
```json
{
  "status": "Package version deprecated successfully."
}
```

### Configuration
#### `registry`
  * Default: "https://registry.npmjs.org/"
  * Type: URL

  The base URL of the npm registry.

#### `otp`
  * Default: null
  * Type: null or String

  A one-time password from a two-factor authenticator, required for certain operations.

#### `dry-run`
  * Default: false
  * Type: Boolean

  If true, npm will report what it would have done without making any changes.
```

--------------------------------

### npm cache Synopsis

Source: https://docs.npmjs.com/cli/v11/commands/npm-cache

This section outlines the basic syntax for using the npm cache command and its subcommands. It shows how to add, clean, list, verify cache entries, and manage npx cache entries.

```bash
npm cache add <package-spec>
npm cache clean [<key>]
npm cache ls [<name>@<version>]
npm cache verify
npm cache npx ls
npm cache npx rm [<key>...]
npm cache npx info <key>...
```

--------------------------------

### Check for Outdated Global npm Packages

Source: https://docs.npmjs.com/updating-packages-downloaded-from-the-registry

Displays a list of globally installed npm packages that have newer versions available. The --depth=0 flag ensures only top-level packages are checked.

```bash
npm outdated -g --depth=0
```

--------------------------------

### Specify Package License using SPDX Expressions

Source: https://docs.npmjs.com/files/package

Defines the license for an npm package using SPDX license expression syntax, suitable for packages licensed under multiple common licenses. For example, (ISC OR GPL-3.0).

```json
{
  "license": "(ISC OR GPL-3.0)"
}
```

--------------------------------

### Executable Script Header

Source: https://docs.npmjs.com/files/package

Executable files referenced in the 'bin' field of package.json must start with a shebang line (e.g., '#!/usr/bin/env node'). This ensures that the script is executed using the Node.js interpreter, making it runnable directly from the command line.

```javascript
#!/usr/bin/env node

console.log('Hello from my CLI!');
```

--------------------------------

### Clean npm Cache

Source: https://docs.npmjs.com/common-errors

Resolves random issues by clearing the npm cache. This command removes cached packages, forcing npm to re-download them on the next install.

```bash
npm cache clean
```

--------------------------------

### Check for Outdated Local npm Packages

Source: https://docs.npmjs.com/updating-packages-downloaded-from-the-registry

Lists all local packages in the current project that have newer versions available than what is currently installed. Successful updates should result in no output from this command.

```bash
npm outdated
```

--------------------------------

### Querying Production Dependencies with Arborist

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

This snippet demonstrates how to load the actual dependency tree using Arborist and then query for all production dependencies using the `.querySelectorAll()` method with the ".prod" selector. It logs the resulting list of production dependencies.

```javascript
const Arborist = require("@npmcli/arborist");
const arb = new Arborist({});

// root-level
arb.loadActual().then(async (tree) => {
  // query all production dependencies
  const results = await tree.querySelectorAll(".prod");
  console.log(results);
});
```

--------------------------------

### Find Old npm Shim Files

Source: https://docs.npmjs.com/cli/v11/using-npm/removal

This command searches for and lists files containing the string 'npm' within the specified directories, which is useful for tracking down older shim files used by npm versions prior to 0.3.

```bash
find /usr/local/{lib/node,bin} -exec grep -l npm {} \; ;
```

--------------------------------

### Retrieve Complex Nested Field using npm pkg get

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Illustrates retrieving a complex nested field, like 'exports[.].require', from package.json, handling special characters with quotes.

```bash
npm pkg get "exports[.].require"
```

--------------------------------

### Run Local Dependencies with npm exec

Source: https://docs.npmjs.com/cli/v11/commands/npm-exec

Executes a command from local dependencies, passing along provided arguments. This is useful for running tools installed within your project's `node_modules`.

```bash
$ npm exec -- tap --bail test/foo.js
$ npx tap --bail test/foo.js
```

--------------------------------

### Default 'contributors' from AUTHORS file

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

npm parses the 'AUTHORS' file in the package root to populate the 'contributors' field. Each line is treated as 'Name <email> (url)', where email and url are optional. Lines starting with '#' or blank lines are ignored.

```text
# This is a comment
John Doe <john.doe@example.com>
Jane Smith
# Another comment
Peter Jones <peter.jones@example.com> (http://example.com)
```

--------------------------------

### Specify npm Engine Version

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Defines the compatible npm versions for a package. This ensures that the package can be installed and managed correctly by specific npm versions. Versions can be specified using ranges like '~1.0.20'.

```json
{
  "engines": {
    "npm": "~1.0.20"
  }
}
```

--------------------------------

### Basic Override for a Specific Package Version in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Shows how to use the `overrides` field in `package.json` to ensure a specific version of a package is always installed. This is useful for managing dependency versions across your project and its sub-dependencies.

```json
{
  "overrides": {
    "@npm/foo": "1.0.0"
  }
}
```

--------------------------------

### Update a Single Global npm Package

Source: https://docs.npmjs.com/updating-packages-downloaded-from-the-registry

Updates a specific globally installed npm package to its latest version. Replace `<package_name>` with the actual name of the package you wish to update.

```bash
npm update -g <package_name>
```

--------------------------------

### Example package.json dependencies with semantic versioning ranges

Source: https://docs.npmjs.com/about-semantic-versioning

This snippet shows how to define dependencies in a package.json file using semantic versioning ranges. The '^' symbol allows for backward-compatible minor and patch updates, while '~' allows only backward-compatible patch updates.

```json
"dependencies": {
  "my_dep": "^1.0.0",
  "another_dep": "~2.2.0"
}
```

--------------------------------

### Publishing a Scoped Package as Public

Source: https://docs.npmjs.com/cli/access

Illustrates how to publish a scoped package directly as public, bypassing the default restricted setting. This is useful for making scoped packages openly available from the start.

```bash
npm publish --access=public
```

--------------------------------

### npm login with security-key flow

Source: https://docs.npmjs.com/accessing-npm-using-2fa

This snippet demonstrates the command-line process for logging into npm using a security key for two-factor authentication. It involves running `npm login`, providing credentials, and then using a security key or OTP from an authenticator app via a browser prompt.

```bash
user@host:~$ npm login
npm notice Log in on https://registry.npmjs.org/
Username: mona
Password:
Email: (this IS public) mona@github.com
npm notice Open https://www.npmjs.com/login/913c3ab1-89a0-44bd-be8d-d946e2e906f0 to use your security key for authentication or enter OTP from your authenticator app

Enter one-time password:
```

--------------------------------

### Alias Package Specifiers - npm

Source: https://docs.npmjs.com/cli/v11/using-npm/package-spec

Defines a package with an alias, primarily used in `npm install` and `package.json` dependencies. The alias is the name in `node_modules`, and the name refers to the registry package.

```bash
npm install <alias>@npm:<name>

Examples:
  semver@npm:@npmcli/semver-with-patch
  semver@npm:semver@7.2.2
  semver@npm:semver@legacy
```

--------------------------------

### npm repo Command Synopsis

Source: https://docs.npmjs.com/cli/v11/commands/npm-repo

This is the basic syntax for the `npm repo` command. It can optionally take one or more package names as arguments. If no package names are provided, it defaults to using the `package.json` in the current directory.

```bash
npm repo [<pkgname> [<pkgname> ...]]
```

--------------------------------

### Deprecated: Also Configuration

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Deprecated option for including development dependencies. Use `--include=dev` instead.

```APIDOC
## `also` (Deprecated)

### Description
When set to `dev` or `development`, this is an alias for `--include=dev`. Please use `--include=dev` instead.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **also** (null, "dev", or "development") - Default: null - Description: DEPRECATED: Please use --include=dev instead.

### Request Example
```json
{
  "also": "dev"
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Display global npm root directory

Source: https://docs.npmjs.com/cli/v11/commands/npm-root

Operates in global mode, printing the global node_modules folder. This is useful for managing globally installed packages in shell scripts.

```bash
#!/bin/bash
global_node_modules="$(npm root --global)"
echo "Global packages installed in: ${global_node_modules}"

```

--------------------------------

### Declare Unscoped npm Package in package.json

Source: https://docs.npmjs.com/using-npm-packages-in-your-projects

Shows how to list an unscoped npm package as a dependency in a project's `package.json` file. This ensures the package is installed and managed by npm for the project.

```json
{
  "dependencies": {
    "package_name": "^1.0.0"
  }
}
```

--------------------------------

### Consume a workspace module in Node.js

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

This example shows how to require a workspace module within a Node.js application. Due to how Node.js handles module resolution, workspaces can be consumed directly by their declared `name` in `package.json`, enabling portable workflows.

```javascript
// ./packages/a/index.js
module.exports = 'a'


// ./lib/index.js
const moduleA = require('a')
console.log(moduleA) // -> a
```

--------------------------------

### List npm Tokens via CLI

Source: https://docs.npmjs.com/revoking-access-tokens

Lists all available npm access tokens associated with your account. This command is useful for identifying the token ID before revoking it. No specific dependencies are required beyond having the npm CLI installed.

```bash
npm token list
```

--------------------------------

### Deeply Nested Overrides in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Shows an example of deeply nested overrides in `package.json`, where a package is overridden only when it's a child of a specific chain of parent packages. This provides fine-grained control over complex dependency structures.

```json
{
  "overrides": {
    "@npm/baz": {
      "@npm/bar": {
        "@npm/foo": "1.0.0"
      }
    }
  }
}
```

--------------------------------

### Define Package Files to Include

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'files' field in package.json specifies an array of file patterns to be included when a package is installed. Patterns follow a .gitignore-like syntax, where inclusion is the default. Omitting 'files' defaults to including all files. Special files are always included or excluded regardless of this setting.

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "files": [
    "dist/",
    "README.md"
  ]
}
```

--------------------------------

### Source Profile to Update System Variables

Source: https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally

This command reloads the shell's configuration, applying the changes made to the PATH environment variable. This is necessary for the system to recognize the new directory for executable commands.

```bash
source ~/.profile
```

--------------------------------

### Set Funding Across Workspaces using npm pkg set --ws

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Shows how to set the 'funding' property to a URL across all configured workspaces using the '--ws' flag.

```bash
npm pkg set funding=https://example.com --ws
```

--------------------------------

### Set New Bin Property using npm pkg set

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Demonstrates setting a new 'bin' property named 'mynewcommand' pointing to 'cli.js' in package.json.

```bash
npm pkg set bin.mynewcommand=cli.js
```

--------------------------------

### Associate Scope with Registry using npm config

Source: https://docs.npmjs.com/cli/v11/using-npm/scope

Configures npm to associate a specific scope with a particular registry using the `npm config set` command. This affects both installation and publishing for packages within that scope.

```bash
npm config set @myco:registry=http://reg.example.com
```

--------------------------------

### Publish Package to npmjs with GitHub Actions

Source: https://docs.npmjs.com/generating-provenance-statements

This GitHub Actions workflow automates the process of publishing a package to the npm registry with provenance enabled. It checks out the code, sets up Node.js, installs dependencies, and publishes the package using the NPM_TOKEN secret for authentication. Provenance ensures the integrity and origin of the published code.

```yaml
name: Publish Package to npmjson:
  release:
    types: [published]
jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      id-token: write
    steps:
      - uses: actions/checkout@v4
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

### npm init: Non-interactive package.json Generation

Source: https://docs.npmjs.com/cli/v11/commands/npm-init

Shows how to use the `-y` or `--yes` flag with npm init to bypass the interactive questionnaire and generate a package.json file with default or inferred values.

```bash
$ npm init -y
```

--------------------------------

### Get npm configuration value

Source: https://docs.npmjs.com/cli/v11/commands/npm-doctor

Retrieves the configured value for a specific npm configuration setting. This is useful for inspecting settings like the registry URL or cache directory, which are checked by `npm doctor`.

```bash
npm config get registry
```

```bash
npm config get cache
```

--------------------------------

### Deprecate a version range with a specific message

Source: https://docs.npmjs.com/cli/deprecate

This example demonstrates how to deprecate a range of package versions, specifically versions less than '0.2.3' of 'my-thing'. A descriptive message is included to explain the reason for deprecation, such as a critical bug fix available in a newer version.

```bash
npm deprecate my-thing@"< 0.2.3" "critical bug fixed in v0.2.3"
```

--------------------------------

### Detailed Version Information

Source: https://docs.npmjs.com/misc/config

Outputs npm version, Node.js versions, and package.json version.

```APIDOC
## `versions`

### Description
If true, output the npm version as well as node's `process.versions` map and the version in the current working directory's `package.json` file if one exists, and exit successfully. Only relevant when specified explicitly on the command line.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **versions** (Boolean) - Optional - If true, outputs detailed version information.

### Request Example
```
npm --versions
```

### Response
#### Success Response (200)
Outputs detailed version information.

#### Response Example
```json
{
  "npm": "9.5.0",
  "node": "18.16.0",
  "v8": "10.2.154.26-node.19",
  "uv": "1.44.2",
  "zlib": "1.2.13",
  "brotli": "1.0.7",
  "ares": "1.19.0",
  "modules": "108",
  "napi": "8",
  "llhttp": "8.1.0",
  "openssl": "3.0.8 7 May 2023",
  "cldr": "43.0",
  "icu": "73.1",
  "tz": "2023a",
  "osinfo": "137"
}
```
```

--------------------------------

### Explain Package Dependencies with npm CLI

Source: https://docs.npmjs.com/cli/v11/commands/npm-explain

The `npm explain` command shows the dependency chain for a given package. It can accept package specifiers or paths to folders within `./node_modules`. The output details which package requires the target package and its version.

```bash
npm explain <package-spec>
alias: why
```

```bash
npm explain glob

# Example output:
glob@7.1.6
node_modules/glob
  glob@"^7.1.4" from the root project

glob@7.1.1 dev
node_modules/tacks/node_modules/glob
  glob@"^7.0.5" from rimraf@2.6.2
  node_modules/tacks/node_modules/rimraf
    rimraf@"^2.6.2" from tacks@1.3.0
    node_modules/tacks
      dev tacks@"^1.3.0" from the root project
```

```bash
$ npm explain node_modules/nyc/node_modules/find-up

# Example output:
find-up@3.0.0 dev
node_modules/nyc/node_modules/find-up
  find-up@"^3.0.0" from nyc@14.1.1
  node_modules/nyc
    nyc@"^14.1.1" from tap@14.10.8
    node_modules/tap
      dev tap@"^14.10.8" from the root project
```

--------------------------------

### Add Development Dependency to package.json (Manual)

Source: https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file

Manually add packages to the 'devDependencies' section of your package.json file. These packages are only needed for local development and testing. This example shows how to include testing frameworks and other development-specific tools.

```json
"name": "my_package",
"version": "1.0.0",
"dependencies": {
  "my_dep": "^1.0.0",
  "another_dep": "~2.2.0"
},
"devDependencies" : {
  "my_test_framework": "^3.1.0",
  "another_dev_dep": "1.0.0 - 1.2.0"
}
```

--------------------------------

### Update Packages (CLI)

Source: https://docs.npmjs.com/cli/update

The `npm update` command updates packages to the latest versions allowed by your package.json's semver constraints. It can update all packages or specific ones, and can operate globally with the -g flag. It also installs missing packages.

```bash
npm update [<pkg>...]

aliases: up, upgrade, udpate
```

--------------------------------

### npm org Command Synopsis

Source: https://docs.npmjs.com/cli/v11/commands/npm-org

This section outlines the basic syntax for managing npm organizations. It covers setting, removing, and listing users within an organization, with an alias 'ogr' available. Note that this command is unaware of workspaces.

```bash
npm org set orgname username [developer | admin | owner]
npm org rm orgname username
npm org ls orgname [<username>]

alias: ogr
```

--------------------------------

### Verify npm package registry signatures using npm CLI

Source: https://docs.npmjs.com/verifying-registry-signatures

This command verifies the ECDSA signatures of installed packages against the registry. It requires npm CLI version 8.15.0 or later. The output indicates the number of packages with verified signatures.

```bash
npm audit signatures
```

--------------------------------

### Clean the npm cache

Source: https://docs.npmjs.com/cli/v11/commands/npm-doctor

Removes corrupt package tarballs from the npm cache. This command is often recommended when `npm doctor` identifies issues with cached packages, ensuring a clean state for future installations.

```bash
npm cache clean -f
```

--------------------------------

### npm config list

Source: https://docs.npmjs.com/cli/config

Displays all current npm configuration settings, optionally in JSON format.

```APIDOC
## GET /npm config list

### Description
Show all the config settings. Use `-l` to also show defaults. Use `--json` to show the settings in json format.

### Method
GET

### Endpoint
/npm config list

### Parameters
#### Query Parameters
- **json** (boolean) - Optional - If true, outputs the configuration in JSON format.
- **defaults** (boolean) - Optional - If true, includes default configuration values.

### Request Example
```http
GET /npm config list?json=true
```

### Response
#### Success Response (200)
- **configuration** (object) - An object containing all configuration settings.

#### Response Example
```json
{
  "registry": "https://registry.npmjs.org/",
  "loglevel": "info",
  "always-auth": false
}
```
```

--------------------------------

### Dockerfile with Docker build secrets for private npm modules

Source: https://docs.npmjs.com/docker-and-private-modules

An updated Dockerfile that utilizes Docker build secrets to securely mount the .npmrc file, enabling the installation of private npm packages. This method ensures the access token is not exposed at runtime.

```docker
# https://docs.npmjs.com/docker-and-private-modules
FROM node:18

ENV APP_HOME="/app"

WORKDIR ${APP_HOME}

COPY package*.json ${APP_HOME}/

RUN --mount=type=secret,id=npmrc,target=/root/.npmrc npm install

COPY . ${APP_HOME}/

CMD npm start
```

--------------------------------

### npm exec Synopsis

Source: https://docs.npmjs.com/cli/v11/commands/npm-exec

Provides the basic syntax for using the npm exec command, including variations with package specifiers, arguments, and the -c or --call options.

```bash
npm exec -- <pkg>[@<version>] [args...]
npm exec --package=<pkg>[@<version>] -- <cmd> [args...]
npm exec -c '<cmd> [args...]'
npm exec --package=foo -c '<cmd> [args...]'

alias: x
```

--------------------------------

### Deprecate an entire package using npm CLI

Source: https://docs.npmjs.com/policies/unpublish

This command marks an entire npm package as deprecated, displaying a warning message to users attempting to install or use it. The package remains available for download but is not recommended for use. This is an alternative when a package does not meet unpublish criteria.

```bash
npm deprecate <package> "<message>"
```

--------------------------------

### Npm Package 'files' Field Configuration

Source: https://docs.npmjs.com/files/package

The 'files' field in package.json specifies which files and directories to include when a package is installed. It uses glob patterns similar to .gitignore but for inclusion. If omitted, it defaults to including all files. Special files like package.json, README, and LICENSE are always included, while certain files like .git and node_modules are always excluded.

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "files": [
    "dist/",
    "README.md",
    "LICENSE"
  ]
}
```

--------------------------------

### Setting npm Configuration via Environment Variables

Source: https://docs.npmjs.com/misc/config

Explains how environment variables prefixed with `npm_config_` are interpreted as npm configuration parameters. Underscores are used instead of hyphens, and variables without values default to `true`. Case-insensitivity is supported.

```bash
# Example: Setting 'foo' configuration to 'bar'
export npm_config_foo=bar

# Example: Setting 'allow-same-version' to true
export npm_config_allow_same_version=true
```

--------------------------------

### Deprecate a specific version of a package using npm CLI

Source: https://docs.npmjs.com/policies/unpublish

This command marks a specific version of an npm package as deprecated, showing a warning message to users who try to install or use that particular version. This is useful for phasing out older versions without removing them entirely.

```bash
npm deprecate <package>@<version> "<message>"
```

--------------------------------

### Manage npm Authentication Tokens

Source: https://docs.npmjs.com/cli/token

This command allows you to list, create, and revoke authentication tokens for npm. When listing tokens, only an abbreviated version is displayed for security. Token creation may prompt for a password and OTP if 2FA is enabled. Revoking tokens can be done using the full token or a distinct truncated ID.

```bash
npm token list
npm token revoke <id|token>
npm token create
```

--------------------------------

### Tagging and Workspace Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-diff

Configuration options for managing package tags and workspace behavior.

```APIDOC
## `tag`

### Description
Specifies the tag used for package installation, distribution, and publishing. If no specific version is provided during installation, this tag is used. For `npm diff`, it's the tag used to fetch the tarball for comparison. For `npm publish`, it's the tag added to the published package.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **tag** (String) - Optional - Default: "latest"

### Request Example
```json
{
  "tag": "beta"
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `workspace`

### Description
Enable running a command in the context of configured workspaces, filtering by the specified workspaces. Valid values include workspace names, paths to workspace directories, or paths to parent workspace directories.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **workspace** (String) - Multiple - Description for workspace

### Request Example
```json
{
  "workspace": ["my-package", "./packages/utils"]
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `workspaces`

### Description
Set to `true` to run the command in the context of all configured workspaces. Setting to `false` causes commands like `install` to ignore workspaces. When not set, commands operating on the `node_modules` tree link workspaces, while other commands operate on the root project unless specific workspaces are provided.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **workspaces** (Boolean or null) - Optional - Default: null

### Request Example
```json
{
  "workspaces": true
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `include-workspace-root`

### Description
Include the workspace root when workspaces are enabled for a command. If `false`, specifying individual workspaces or all workspaces will cause npm to operate only on the specified workspaces, not the root project.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **include-workspace-root** (Boolean) - Optional - Default: false

### Request Example
```json
{
  "include-workspace-root": true
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

--------------------------------

### Version Information

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Options to display npm and Node.js version information.

```APIDOC
## `version` and `versions`

### Description
- `version`: If true, outputs the npm version and exits successfully. Only relevant when specified explicitly on the command line.
- `versions`: If true, outputs the npm version as well as Node's `process.versions` map and the version in the current working directory's `package.json` file if one exists, and exits successfully. Only relevant when specified explicitly on the command line.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **version** (Boolean) - Default: false - Description: If true, output the npm version and exit.
- **versions** (Boolean) - Default: false - Description: If true, output npm version, Node.js versions, and current package.json version if available.

### Request Example
```json
{
  "version": true
}
```
```json
{
  "versions": true
}
```

### Response
#### Success Response (200)
Outputs version information to the console.

#### Response Example
```
8.1.0
```
```json
{
  "npm": "8.1.0",
  "node": "16.13.0",
  "v8": "9.4.0",
  "uv": "1.41.0",
  "zlib": "1.2.11",
  "brotli": "1.0.7",
  "ares": "1.17.1",
  "modules": "93",
  "napi": "8",
  "llhttp": "6.0.5",
  "openssl": "1.1.1l+quic",
  "cldr": "39.0.0",
  "icu": "69.1",
  "tz": "2021e",
  "unicode": "14.0"
}
```
```

--------------------------------

### Log in to npm (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command initiates the login process to your npm account. Depending on your 2FA settings, you may be prompted for a second form of authentication after entering your credentials.

```bash
npm login
```

--------------------------------

### Array Matching with Exact Keyword

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

This code snippet illustrates how to select dependencies that have an exact keyword match. It uses a selector syntax that is equivalent to `*:keywords([value="react"])`.

```npm-query
/* return dependencies that have the exact keyword "react" */
/* this is equivalent to `*:keywords([value="react"])` */
*: attr([keywords=react]);
```

--------------------------------

### Custom npm Scripts with Pre/Post Hooks

Source: https://docs.npmjs.com/cli/v11/using-npm/scripts

Defines custom scripts 'precompress', 'compress', and 'postcompress' in package.json. The 'precompress' script runs before 'compress', and 'postcompress' runs after 'compress'. This allows for sequential execution of related tasks.

```json
{
  "scripts": {
    "precompress": "{{ executes BEFORE the `compress` script }}",
    "compress": "{{ run command to compress files }}",
    "postcompress": "{{ executes AFTER `compress` script }}"
  }
}
```

--------------------------------

### Querying for all dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

A simple query to select all dependencies within the project.

```bash
*
```

--------------------------------

### Set Multiple Fields using npm pkg set

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Shows how to set multiple fields, including 'description' and 'engines.node', in package.json simultaneously.

```bash
npm pkg set description='Awesome package' engines.node='>=10'
```

--------------------------------

### Deprecated: Dev Configuration

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Deprecated alias for `--include=dev`. Use `--include=dev` instead.

```APIDOC
## `dev` (Deprecated)

### Description
Alias for `--include=dev`. Please use `--include=dev` instead.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **dev** (Boolean) - Default: false - Description: DEPRECATED: Please use --include=dev instead.

### Request Example
```json
{
  "dev": true
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Version Information

Source: https://docs.npmjs.com/misc/config

Outputs the npm version and exits. Relevant when specified explicitly.

```APIDOC
## `version`

### Description
If true, output the npm version and exit successfully. Only relevant when specified explicitly on the command line.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **version** (Boolean) - Optional - If true, outputs the npm version.

### Request Example
```
npm --version
```

### Response
#### Success Response (200)
Outputs the npm version string.

#### Response Example
```
9.5.0
```
```

--------------------------------

### Display Local npm Prefix

Source: https://docs.npmjs.com/cli/v11/commands/npm-prefix

This command prints the local prefix to standard output. The local prefix is the closest parent directory containing a package.json file or a node_modules directory. This command is unaware of workspaces.

```bash
npm prefix
```

--------------------------------

### Using NODE_OPTIONS with npx

Source: https://docs.npmjs.com/cli/v11/commands/npx

Demonstrates how to pass node arguments to npx using the NODE_OPTIONS environment variable. This replaces the removed --node-arg and -n options.

```bash
NODE_OPTIONS="--trace-warnings --trace-exit" npx foo --random=true
```

--------------------------------

### Initialize Node.js Module with npm init

Source: https://docs.npmjs.com/creating-node-js-modules

Initializes a new Node.js module by creating a `package.json` file. Use `npm init` for unscoped modules and `npm init --scope=@scope-name` for scoped modules. This command prompts for essential package details like name, version, and the main entry point.

```bash
npm init
npm init --scope=@scope-name
```

--------------------------------

### Synopsis of npm publish (CLI)

Source: https://docs.npmjs.com/cli/publish

The synopsis for the npm publish command, indicating the general structure and optional package specification.

```bash
npm publish <package-spec>
```

--------------------------------

### List all users in an npm organization in JSON format

Source: https://docs.npmjs.com/cli/v11/commands/npm-org

Demonstrates how to retrieve the list of users for an npm organization in JSON format, which is useful for programmatic processing or integration with other tools.

```bash
$ npm org ls my-org --json
```

--------------------------------

### Run npm test command

Source: https://docs.npmjs.com/cli/v11/commands/npm-test

This snippet shows the basic syntax for running the npm test command. It executes the script defined in the 'test' property of the package.json file. Arguments can be passed to the test script using '--'.

```bash
npm test [-- <args>]

aliases: tst, t
```

--------------------------------

### User Configuration File Path

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Specifies the location of user-level npm configuration settings.

```APIDOC
## `userconfig`

### Description
The location of user-level configuration settings. This may be overridden by the `npm_config_userconfig` environment variable or the `--userconfig` command line option, but may _not_ be overridden by settings in the `globalconfig` file.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **userconfig** (Path) - Default: "~/.npmrc" - Description: The location of user-level configuration settings.

### Request Example
```json
{
  "userconfig": "~/.npmrc"
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Environment Variable Substitution in .npmrc

Source: https://docs.npmjs.com/cli/v11/configuring-npm/npmrc

Demonstrates how to use environment variables within .npmrc files for dynamic configuration. Supports default values and forcing empty strings if variables are undefined.

```ini
cache = ${HOME}/.npm-packages
node-options = "${NODE_OPTIONS?} --use-system-ca"
```

--------------------------------

### Shortcut: Link Local Directory into Project (npm link <path>)

Source: https://docs.npmjs.com/cli/v11/commands/npm-link

A shortcut to perform the two-step linking process in one command. It links a local directory (specified by path) into the current project's `node_modules`. This is equivalent to first creating a global link for the local directory and then linking that global link into the current project.

```bash
cd ~/projects/node-bloggy
npm link ../node-redis
```

--------------------------------

### Run a package script with arguments

Source: https://docs.npmjs.com/cli/v11/commands/npm-run

Executes a specified command from a package's 'scripts' object. Any additional arguments provided after '--' are passed directly to the script. If no command is given, it lists available scripts.

```bash
npm run <command> [-- <args>]
```

```bash
npm run test -- --grep="pattern"
```

--------------------------------

### Generate Project SBOM using npm CLI

Source: https://docs.npmjs.com/cli/v11/commands/npm-sbom

The `npm sbom` command generates a Software Bill of Materials (SBOM) for the current project's dependencies. It supports output in both SPDX and CycloneDX formats. This is a command-line interface tool.

```bash
npm sbom
```

--------------------------------

### Automatic Yes

Source: https://docs.npmjs.com/misc/config

Automatically answers 'yes' to any npm prompts.

```APIDOC
## `yes`

### Description
Automatically answer "yes" to any prompts that npm might print on the command line.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **yes** (Boolean) - Optional - Automatically confirm prompts.

### Request Example
```
npm install --yes
```

### Response
#### Success Response (200)
Prompts are automatically answered 'yes'.

#### Response Example
N/A
```

--------------------------------

### Initialize Git Repository and Add Remote

Source: https://docs.npmjs.com/creating-and-publishing-unscoped-public-packages

Initializes a new Git repository and adds a remote origin for package version control. This is a prerequisite for managing package code with Git before publishing.

```shell
git init
git remote add origin git://git-remote-url
```

--------------------------------

### Funding Source Selection

Source: https://docs.npmjs.com/misc/config

Selects which funding source URL to open if multiple are available.

```APIDOC
## `which`

### Description
If there are multiple funding sources, which 1-indexed source URL to open.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **which** (Number) - Optional - The 1-indexed funding source to open.

### Request Example
```
npm config set which 2
```

### Response
#### Success Response (200)
Configuration updated.

#### Response Example
N/A
```

--------------------------------

### Check for Outdated Dependencies

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

The `:outdated` pseudo-selector retrieves registry data to identify outdated dependencies. It supports various filters like 'any', 'in-range', 'out-of-range', 'major', 'minor', and 'patch'. Additional context like available versions and outdated details are provided.

```css
/* Returns every direct dependency with a new semver major release */
:root > :outdated(major)

/* Returns production dependencies with a new release that satisfies at least one of its parent's dependencies */
.prod:outdated(in-range)
```

--------------------------------

### npm search with Description Display Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

Controls whether the package description is shown in the npm search results. By default, descriptions are displayed.

```bash
# To hide descriptions:
npm config set description false

# To show descriptions (default):
npm config set description true
```

--------------------------------

### Add New Contributor Entry using npm pkg set

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Illustrates adding a new contributor entry with 'name' and 'email' to the 'contributors' array at index 0.

```bash
npm pkg set contributors[0].name='Foo' contributors[0].email='foo@bar.ca'
```

--------------------------------

### npm fund Command Synopsis

Source: https://docs.npmjs.com/cli/v11/commands/npm-fund

The basic syntax for the npm fund command. It can optionally take a package specification to query funding for a specific package.

```bash
npm fund [<package-spec>]
```

--------------------------------

### Deprecated: Certificate Configuration

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Deprecated options for client certificates. Use registry-scoped `keyfile` and `certfile` instead.

```APIDOC
## `cert` (Deprecated)

### Description
`key` and `cert` are no longer used for most registry operations. Use registry scoped `keyfile` and `certfile` instead. Example: `//other-registry.tld/:keyfile=/path/to/key.pem //other-registry.tld/:certfile=/path/to/cert.crt`. A client certificate to pass when accessing the registry. Values should be in PEM format (Windows calls it "Base-64 encoded X.509 (.CER)") with newlines replaced by the string "\n". It is _not_ the path to a certificate file, though you can set a registry-scoped "certfile" path like `//other-registry.tld/:certfile=/path/to/cert.pem`.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **cert** (null or String) - Default: null - Description: DEPRECATED: `key` and `cert` are no longer used for most registry operations. Use registry scoped `keyfile` and `certfile` instead.

### Request Example
```json
{
  "cert": "-----BEGIN CERTIFICATE-----\nXXXX\nXXXX\n-----END CERTIFICATE-----"
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Querying for all git dependencies using type

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

A concise way to select all dependencies that are of type 'git'.

```bash
:type(git)
```

--------------------------------

### Handling Optional Dependencies in JavaScript

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Demonstrates how to gracefully handle optional dependencies in JavaScript. It attempts to require a package and sets it to null if the require fails or if a specific version check fails. This prevents application crashes due to missing optional packages.

```javascript
try {
  var foo = require("@npm/foo");
  var fooVersion = require("@npm/foo/package.json").version;
} catch (er) {
  foo = null;
}
if (notGoodFooVersion(fooVersion)) {
  foo = null;
}


// .. then later in your program ..


if (foo) {
  foo.doFooThings();
}
```

--------------------------------

### Workspace Configuration

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Enables running commands within specific workspaces or all configured workspaces.

```APIDOC
## `workspace` and `workspaces`

### Description
- `workspace`: Enable running a command in the context of the configured workspaces of the current project while filtering by running only the workspaces defined by this configuration option. Valid values are workspace names, paths to workspace directories, or paths to parent workspace directories.
- `workspaces`: Set to true to run the command in the context of **all** configured workspaces. Explicitly setting this to false will cause commands like `install` to ignore workspaces altogether.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **workspace** (String, can be set multiple times) - Default: null - Description: Filter commands to run only within specified workspaces.
- **workspaces** (Boolean) - Default: null - Description: Run commands in the context of all configured workspaces.

### Request Example
```json
{
  "workspace": "my-package"
}
```
```json
{
  "workspaces": true
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Specify Package License using SPDX Identifiers

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Defines how to specify a package license using a current SPDX license identifier. This ensures clarity on usage permissions and restrictions. It supports single licenses like 'BSD-3-Clause' or multiple licenses using SPDX expression syntax.

```json
{
  "license": "BSD-3-Clause"
}
```

```json
{
  "license": "(ISC OR GPL-3.0)"
}
```

```json
{
  "license": "UNLICENSED"
}
```

--------------------------------

### Create Granular Access Token with npm

Source: https://docs.npmjs.com/cli/token

This section details the configuration options for creating granular access tokens using `npm token create`. These options allow fine-grained control over token permissions, including package access, scopes, organization access, expiration, and CIDR restrictions. Some options, like `bypass-2fa`, are specifically useful for CI/CD workflows.

```bash
# Example of creating a token with specific configurations
npm token create --name "my-token" --expires 30 --packages "my-package" --scopes "@my-scope" --orgs "my-org" --packages-and-scopes-permission "read-only" --orgs-permission "read-write" --cidr "192.168.1.0/24" --bypass-2fa

# Note: Password and OTP might be prompted if not provided or if 2FA is enabled.
```

--------------------------------

### Configure Publishing Settings

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Specifies configuration values to be used at publish time, such as tag, registry, or access level. This is useful for controlling where and how a package is published.

```json
{
  "publishConfig": {
    "registry": "https://internal.registry.example.com/"
  }
}
```

--------------------------------

### Create Granular Access Token with npm

Source: https://docs.npmjs.com/cli/v11/commands/npm-token

This snippet illustrates how to create a granular access token using `npm token create` with various configuration options. These options allow fine-grained control over the token's permissions, scope, and validity, making it suitable for CI/CD workflows. Note that the full token ID from `npm token list` is required for revocation, not the truncated version shown in the normal output.

```bash
# Example of creating a token with specific configurations:
npm token create --name "my-token" --expires 30 --packages "my-package" --scopes "@my-scope" --orgs "my-org" --packages-and-scopes-permission "read-only" --orgs-permission "read-write" --cidr "192.168.1.0/24" --bypass-2fa

# To revoke a token using its full ID (obtained from `npm token list --json` or npm website):
npm token revoke <full_token_id>
```

--------------------------------

### Run Arbitrary Shell Scripts with npx

Source: https://docs.npmjs.com/cli/commands/npx

Shows how to execute arbitrary shell scripts using npx with the '-c' or '--call' option, useful for chaining commands or running complex script logic within the project's context.

```bash
$ npm x -c 'eslint && say "hooray, lint passed"'
$ npx -c 'eslint && say "hooray, lint passed"'
```

--------------------------------

### Create Global Link for Workspace (--workspace)

Source: https://docs.npmjs.com/cli/v11/commands/npm-link

Creates a global symbolic link for a specified workspace. This command is used when you want to make a specific workspace within a multi-package project available globally, similar to how `npm link` works for standalone packages.

```bash
npm link --workspace <name>
```

--------------------------------

### Add npm Registry User Account (CLI)

Source: https://docs.npmjs.com/cli/adduser

This command creates a new user account in the specified npm registry and saves the credentials to the .npmrc file. If no registry is specified, the default registry is used. When using the 'legacy' auth-type, username, password, and email are prompted.

```bash
npm adduser

alias: add-user
```

--------------------------------

### View Package Information with npm view

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

The basic npm view command retrieves and displays information about a specified package from the npm registry. If no version is specified, it defaults to the 'latest' version. You can also view information for the current project by using '.' as the package specifier.

```bash
npm view [<package-spec>] [<field>[.subfield]...]

alias: info, show, v

# Example: View information about the 'connect' package
npm view connect

# Example: View dependencies of the current project
npm view . dependencies
```

--------------------------------

### Initialize Scoped Package for Organization (npm CLI)

Source: https://docs.npmjs.com/cli/v11/using-npm/orgs

This command initializes a new npm package and scopes it to a specific organization. This is a prerequisite for publishing packages under an organization's namespace.

```bash
npm init --scope=<org>
```

--------------------------------

### Configure npm view Output to JSON

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

The `json` configuration option can be set to `true` to output package information in JSON format instead of the default human-readable format. This is useful for programmatic parsing of the output.

```bash
# Set the json configuration to true for JSON output
npm config set json true

# View package info in JSON format (example)
npm view express --json
```

--------------------------------

### Deprecated: Cache Max Configuration

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Deprecated option for cache size limit. Use `--prefer-online` instead.

```APIDOC
## `cache-max` (Deprecated)

### Description
This option has been deprecated in favor of `--prefer-online`. `--cache-max=0` is an alias for `--prefer-online`.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **cache-max** (Number) - Default: Infinity - Description: DEPRECATED: This option has been deprecated in favor of `--prefer-online`.

### Request Example
```json
{
  "cache-max": 0
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Deprecated: Cache Min Configuration

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Deprecated option for cache minimum size. Use `--prefer-offline` instead.

```APIDOC
## `cache-min` (Deprecated)

### Description
This option has been deprecated in favor of `--prefer-offline`. `--cache-min=9999` (or bigger) is an alias for `--prefer-offline`.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **cache-min** (Number) - Default: 0 - Description: DEPRECATED: This option has been deprecated in favor of `--prefer-offline`.

### Request Example
```json
{
  "cache-min": 9999
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Make npm Tab Completion Persistent (Bash/Zsh)

Source: https://docs.npmjs.com/cli/v11/commands/npm-completion

These commands add the npm tab-completion script to your shell's startup file, making it available in all new shell sessions. This requires write access to your ~/.bashrc or ~/.zshrc file. The output of 'npm completion' is appended to the specified file.

```bash
npm completion >> ~/.bashrc
npm completion >> ~/.zshrc
```

--------------------------------

### Add a developer to an npm organization

Source: https://docs.npmjs.com/cli/v11/commands/npm-org

Demonstrates how to add a new user to an npm organization with the 'developer' role. This is a common operation for onboarding new team members.

```bash
$ npm org set my-org @mx-smith
```

--------------------------------

### Replacing a Dependency with a Fork using npm: Prefix in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Shows how to use the `npm:` prefix within `overrides` in `package.json` to replace a dependency with a different package, potentially a forked version, specifying the new package name and version.

```json
{
  "overrides": {
    "package-name": "npm:@scope/forked-package@1.0.0"
  }
}
```

--------------------------------

### Updating Dependencies with Semver Constraints

Source: https://docs.npmjs.com/cli/v11/commands/npm-update

This section illustrates how `npm update` respects different semver ranges like caret (`^`) and tilde (`~`) for package versions. It explains how the command selects the highest possible version that satisfies the specified range, including handling subdependencies.

```json
{
  "dependencies": {
    "dep1": "^1.1.1"
  }
}
```

```json
{
  "dependencies": {
    "dep1": "~1.1.1"
  }
}
```

```json
{
  "dependencies": {
    "dep1": "^0.2.0"
  }
}
```

```json
{
  "dependencies": {
    "dep1": "^0.4.0"
  }
}
```

```json
{
  "name": "my-app",
  "dependencies": {
    "dep1": "^1.0.0",
    "dep2": "1.0.0"
  }
}
```

```json
{
  "name": "dep2",
  "dependencies": {
    "dep1": "~1.1.1"
  }
}
```

--------------------------------

### Basic npm query Usage

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

The fundamental syntax for using the npm query command. It takes a selector as an argument to retrieve dependency objects.

```bash
npm query <selector>
```

--------------------------------

### Homepage URL in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

A string representing the URL to the project's homepage. This field is useful for users to find more information about the package.

```json
{
  "homepage": "https://github.com/npm/example#readme"
}
```

--------------------------------

### Specify Supported Operating Systems

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Lists the operating systems on which a package is designed to run. It can also be used to block specific operating systems by prepending '!' to the OS name.

```json
{
  "os": ["darwin", "linux"]
}
```

```json
{
  "os": ["!win32"]
}
```

--------------------------------

### Querying for any workspace dependency

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Selects any dependency that is part of a workspace.

```bash
.workspace
```

--------------------------------

### npm search with Search Options Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

Specifies additional search terms that are always passed to the search query. These options are space-separated and do not highlight matches in the output.

```bash
# Add '--unstable' and '--deprecated' as search options:
npm config set searchopts "--unstable --deprecated"

# Clear custom search options:
npm config delete searchopts
```

--------------------------------

### Append to Array using npm pkg set

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Demonstrates appending new contributor entries ('Foo' and 'Bar') to the end of the 'contributors' array using empty bracket notation.

```bash
npm pkg set contributors[].name='Foo' contributors[].name='Bar'
```

--------------------------------

### Define Funding as a String URL

Source: https://docs.npmjs.com/files/package

Specifies funding information for an npm package using a simple string URL. This provides a direct link for users to contribute.

```json
{
  "funding": "http://npmjs.com/donate"
}
```

--------------------------------

### Specify Supported CPU Architectures

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Defines the CPU architectures compatible with a package. Similar to the 'os' field, it supports blocking specific architectures by prepending '!'.

```json
{
  "cpu": ["x64", "ia32"]
}
```

```json
{
  "cpu": ["!arm", "!mips"]
}
```

--------------------------------

### All Workspaces Execution

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Execute commands across all configured workspaces. Can be explicitly set to true or false to control behavior.

```APIDOC
## `workspaces`

### Description
Set to true to run the command in the context of **all** configured workspaces. Explicitly setting this to false will cause commands like `install` to ignore workspaces altogether. When not set explicitly: Commands that operate on the `node_modules` tree (install, update, etc.) will link workspaces into the `node_modules` folder. - Commands that do other things (test, exec, publish, etc.) will operate on the root project, _unless_ one or more workspaces are specified in the `workspace` config. This value is not exported to the environment for child processes.

### Type
null or Boolean

### Default
`null`
```

--------------------------------

### Publish Multiple Workspaces (CLI)

Source: https://docs.npmjs.com/cli/publish

Publishes multiple specified workspaces to the npm registry. This is achieved by repeating the --workspace flag for each desired workspace.

```bash
npm publish --workspace=workspace-a --workspace=workspace-b
```

--------------------------------

### Specifying Array Values in .npmrc

Source: https://docs.npmjs.com/cli/v11/configuring-npm/npmrc

Illustrates how to define array values in an .npmrc file by appending '[]' to the key name for each value.

```ini
key[] = "first value"
key[] = "second value"
```

--------------------------------

### Include Development Dependencies (Deprecated)

Source: https://docs.npmjs.com/misc/config

Deprecated alias for `--include=dev`.

```APIDOC
## `also` (Deprecated)

### Description
When set to `dev` or `development`, this is an alias for `--include=dev`. Please use `--include=dev` instead.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **also** (String) - Optional - Alias for `--include=dev`.

### Request Example
```
npm install --also=dev
```

### Response
#### Success Response (200)
Development dependencies included.

#### Response Example
N/A
```

--------------------------------

### npm search with Prefer Online Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

When true, this option forces staleness checks for cached data, ensuring the CLI looks for the latest package information even if local cache is recent.

```bash
# Enable prefer-online mode:
npm config set "prefer-online" true

# Disable prefer-online mode:
npm config set "prefer-online" false
```

--------------------------------

### Check for Vulnerable Dependencies

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

The `:vuln` pseudo-selector identifies dependencies with known vulnerabilities. It only returns dependencies whose current version matches an existing vulnerability. Filtering by 'severity' and 'cwe' is supported.

```css
/* Returns direct production dependencies with any known vulnerability */
:root > .prod:vuln

/* Returns only dependencies with a vulnerability with a 'high' severity */
:vuln([severity=high])

/* Returns only dependencies with a vulnerability with a 'high' or 'moderate' severity */
:vuln([severity=high],[severity=moderate])

/* Returns only dependencies with a vulnerability that includes CWE-1333 (ReDoS) */
:vuln([cwe=1333])
```

--------------------------------

### npm view - Current Project Context

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

Allows viewing package information within the context of the current project, typically by referencing the `package.json` file.

```APIDOC
## GET /npm/view/.

### Description
Retrieves information about the current project based on its `package.json` file.

### Method
GET

### Endpoint
/npm/view/.

### Parameters
#### Query Parameters
- **field** (string) - Optional - A specific field to retrieve from the project's `package.json` (e.g., 'dependencies', 'name').

### Request Example
```
GET /npm/view/.?field=dependencies
```

### Response
#### Success Response (200)
- **data** (object) - Contains the requested information from the project's `package.json`.

#### Response Example
```json
{
  "dependencies": {
    "express": "^4.18.2"
  }
}
```
```

--------------------------------

### Specify Custom License with SEE LICENSE

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Used when a package's license does not have an assigned SPDX identifier or is a custom license. It requires including a separate file named '<filename>' at the package's top level containing the full license text.

```json
{
  "license": "SEE LICENSE IN <filename>"
}
```

--------------------------------

### npm version Synopsis

Source: https://docs.npmjs.com/cli/v11/commands/npm-version

The synopsis for the `npm version` command shows the different ways to specify a new version, including direct version numbers or semantic versioning keywords like 'major', 'minor', 'patch', and 'prerelease'. It also notes an alias 'version'.

```bash
npm version [<newversion> | major | minor | patch | premajor | preminor | prepatch | prerelease | from-git]

alias: verison
```

--------------------------------

### npm view - Basic Usage

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

Displays general information about a specified npm package. If no version is specified, it defaults to the 'latest' version.

```APIDOC
## GET /npm/view

### Description
Retrieves and displays information about an npm package from the registry.

### Method
GET

### Endpoint
/npm/view

### Parameters
#### Query Parameters
- **package-spec** (string) - Required - The name of the package to view information for (e.g., 'connect', 'react').
- **field** (string) - Optional - A specific field or nested field to retrieve (e.g., 'dependencies', 'repository.url').

### Request Example
```
GET /npm/view?package-spec=connect
```

### Response
#### Success Response (200)
- **data** (object) - Contains the requested information about the package.

#### Response Example
```json
{
  "name": "connect",
  "version": "3.7.0",
  "description": "real-time high-performance cross-platform http framework",
  "time": {
    "modified": "2023-10-24T08:00:00.000Z",
    "created": "2011-06-07T17:30:00.000Z",
    "3.7.0": "2023-10-24T08:00:00.000Z"
  },
  "dependencies": {
    "debug": "^4.1.1"
  }
}
```
```

--------------------------------

### npm search with Parseable Output Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

Enables parseable, tab-separated table format for npm search results. This is useful for scripting and integrating search results into other tools.

```bash
# To enable parseable output:
npm config set parseable true

# To disable parseable output:
npm config set parseable false
```

--------------------------------

### User Agent Configuration

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Configures the User-Agent header sent with npm requests. Allows customization with environment and npm version details.

```APIDOC
## `user-agent`

### Description
Sets the User-Agent request header. The following fields are replaced with their actual counterparts:
  * `{npm-version}` - The npm version in use
  * `{node-version}` - The Node.js version in use
  * `{platform}` - The value of `process.platform`
  * `{arch}` - The value of `process.arch`
  * `{workspaces}` - Set to `true` if the `workspaces` or `workspace` options are set.
  * `{ci}` - The value of the `ci-name` config, if set, prefixed with `ci/`, or an empty string if `ci-name` is empty.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **user-agent** (String) - Default: "npm/{npm-version} node/{node-version} {platform} {arch} workspaces/{workspaces} {ci}" - Description: Sets the User-Agent request header with dynamic values.

### Request Example
```json
{
  "user-agent": "npm/8.1.0 node/16.13.0 linux x64 workspaces/true ci/github-actions"
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Include Development Flag (Deprecated)

Source: https://docs.npmjs.com/misc/config

Deprecated alias for `--include=dev`.

```APIDOC
## `dev` (Deprecated)

### Description
Alias for `--include=dev`. Please use `--include=dev` instead.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **dev** (Boolean) - Optional - Alias for `--include=dev`.

### Request Example
```
npm install --dev
```

### Response
#### Success Response (200)
Development dependencies included.

#### Response Example
N/A
```

--------------------------------

### Keywords Array in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

An array of strings used to help users discover your package via 'npm search'. These keywords should be relevant to your package's functionality.

```json
{
  "keywords": [
    "node",
    "javascript",
    "npm"
  ]
}
```

--------------------------------

### Publish Packages (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command publishes a package to the npm registry. Publishing requires either two-factor authentication (2FA) enabled on your account or a granular access token with 2FA bypass enabled.

```bash
npm publish
```

--------------------------------

### List Packages Available to Organization Team (npm CLI)

Source: https://docs.npmjs.com/cli/v11/using-npm/orgs

This command lists all packages that a specific team within an organization has access to. It's useful for understanding team-level permissions.

```bash
npm access list packages <org:team>
```

--------------------------------

### Specify Funding Information

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Outlines the methods for specifying funding sources for a package. This can be a single URL string, an object with 'type' and 'url', or an array containing a mix of objects and URLs.

```json
{
  "funding": {
    "type": "individual",
    "url": "http://npmjs.com/donate"
  }
}
```

```json
{
  "funding": {
    "type": "patreon",
    "url": "https://www.patreon.com/user"
  }
}
```

```json
{
  "funding": "http://npmjs.com/donate"
}
```

```json
{
  "funding": [
    {
      "type": "individual",
      "url": "http://npmjs.com/donate"
    },
    "http://npmjs.com/donate-also",
    {
      "type": "patreon",
      "url": "https://www.patreon.com/user"
    }
  ]
}
```

--------------------------------

### GitLab CI/CD Configuration for Trusted Publishing

Source: https://docs.npmjs.com/trusted-publishers

This GitLab CI/CD configuration illustrates setting up trusted publishing for npm packages. It utilizes `id_tokens` to generate an OIDC token with the audience `npm:registry.npmjs.org` for authentication during the publish stage.

```yaml
stages:
  - test
  - build
  - publish

variables:
  NODE_VERSION: '24'

test:
  stage: test
  image: node:${NODE_VERSION}
  script:
    - npm ci
    - npm test

publish:
  stage: publish
  image: node:${NODE_VERSION}
  id_tokens:
    NPM_ID_TOKEN:
      aud: "npm:registry.npmjs.org"
    SIGSTORE_ID_TOKEN:
      aud: sigstore
  script:
    - npm ci
    - npm run build --if-present
    - npm publish
  only:
    - tags

```

--------------------------------

### Manage npm Package Owners (CLI)

Source: https://docs.npmjs.com/cli/owner

This snippet demonstrates the core commands for managing package owners using the npm CLI. It covers adding new owners, removing existing ones, and listing current owners for a specified package.

```bash
npm owner add <user> <package-spec>
npm owner rm <user> <package-spec>
npm owner ls <package-spec>
```

--------------------------------

### Publish All Workspaces (CLI)

Source: https://docs.npmjs.com/cli/publish

Publishes all workspaces defined in the project to the npm registry. This is a convenient option for monorepos with multiple packages.

```bash
npm publish --workspaces
```

--------------------------------

### User-Agent Header Configuration in NPM

Source: https://docs.npmjs.com/misc/config

Configures the User-Agent request header for NPM. It allows for dynamic replacement of placeholders like npm version, Node.js version, platform, architecture, workspace status, and CI environment.

```string
npm/{npm-version} node/{node-version} {platform} {arch} workspaces/{workspaces} {ci}
```

--------------------------------

### Create Access Token (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command is used to create a new access token for your npm account. Tokens can be used for authentication and may have specific permissions, including bypassing 2FA if configured.

```bash
npm token create
```

--------------------------------

### Npm Package 'bin' Field Configuration (String)

Source: https://docs.npmjs.com/files/package

When a package has a single executable file and its name should match the package name, the 'bin' field can be specified as a string pointing to that file. This simplifies the configuration for packages with one primary command-line interface.

```json
{
  "name": "my-program",
  "version": "1.2.5",
  "bin": "path/to/program"
}
```

--------------------------------

### npm-whoami Command

Source: https://docs.npmjs.com/cli/v11/commands/npm-whoami

The npm-whoami command displays the npm username of the currently logged-in user. It works by connecting to the registry's /-/whoami endpoint for token-based authentication or by extracting the username from Basic Auth credentials.

```APIDOC
## npm whoami

### Description
Display the npm username of the currently logged-in user. If logged into a registry that provides token-based authentication, then connect to the `/-/whoami` registry endpoint to find the username associated with the token, and print to standard output. If logged into a registry that uses Basic Auth, then simply print the `username` portion of the authentication string.

### Method
GET

### Endpoint
`/-/whoami` (relative to the configured registry)

### Parameters

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
npm whoami
```

### Response
#### Success Response (200)
- **username** (string) - The npm username of the logged-in user.

#### Response Example
```json
{
  "username": "your-npm-username"
}
```

### Configuration
#### `registry`
  * Default: "https://registry.npmjs.org/"
  * Type: URL

  The base URL of the npm registry.
```

--------------------------------

### Replacing a Dependency with a GitHub Repository in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Illustrates how to use the `github:` prefix in `overrides` within `package.json` to replace a dependency with a package hosted on GitHub, allowing specification of the repository, branch, tag, or commit hash.

```json
{
  "overrides": {
    "package-name": "github:username/repo#branch-name"
  }
}
```

--------------------------------

### npm search Command Synopsis

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

The synopsis for the npm search command shows the basic structure for searching packages. It accepts one or more search terms and has aliases like 'find', 's', and 'se'. This command is not aware of workspaces.

```bash
npm search <search term> [<search term> ...]

aliases: find, s, se
```

--------------------------------

### Define Funding as an Array of URLs and Objects

Source: https://docs.npmjs.com/files/package

Specifies multiple funding sources for an npm package using an array. This array can contain a mix of string URLs and structured funding objects.

```json
{
  "funding": [
    {
      "type": "individual",
      "url": "http://npmjs.com/donate"
    },
    "http://npmjs.com/donate-also",
    {
      "type": "patreon",
      "url": "https://www.patreon.com/user"
    }
  ]
}
```

--------------------------------

### List all users in an npm organization

Source: https://docs.npmjs.com/cli/v11/commands/npm-org

Provides the command to list all users associated with a specific npm organization. This helps in auditing and understanding the current team structure.

```bash
$ npm org ls my-org
```

--------------------------------

### Replacing a Dependency with a Local File Path in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Demonstrates how to use the `file:` prefix in `overrides` within `package.json` to replace a dependency with a local package located at a specified file path. This is useful for testing local modifications or forks.

```json
{
  "overrides": {
    "package-name": "file:../local-fork"
  }
}
```

--------------------------------

### npm login with --auth-type=web flow

Source: https://docs.npmjs.com/accessing-npm-using-2fa

This snippet illustrates the command-line login process for npm using the `--auth-type=web` flag, which initiates an authentication flow through the user's web browser. This method is supported in npm version 8.14.0 and higher and will be the default for the public registry in npm 9.

```bash
user@host:~$ npm login --auth-type=web
npm notice Log in on https://registry.npmjs.org/
Authenticate your account at:
https://www.npmjs.com/login?next=/login/cli/b1a2f96a-ce09-4463-954c-c99f6773b922
Press ENTER to open in the browser...
```

--------------------------------

### npm rebuild Command Synopsis

Source: https://docs.npmjs.com/cli/v11/commands/npm-rebuild

The basic syntax for the npm rebuild command. It allows rebuilding specific packages or all packages if no specifier is provided. The command has an alias 'rb'.

```bash
npm rebuild [<package-spec>] ...

alias: rb
```

--------------------------------

### Set Number Value using npm pkg set --json

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Illustrates setting the 'tap.timeout' property to a number (60) by parsing the value as JSON.

```bash
npm pkg set tap.timeout=60 --json
```

--------------------------------

### npx vs npm exec Argument Parsing

Source: https://docs.npmjs.com/cli/commands/npx

Highlights the difference in argument parsing between npx and npm exec, particularly when using the '--' delimiter to separate npx/npm options from arguments intended for the executed command.

```bash
$ npx foo@latest bar --package=@npmcli/foo
# $ foo bar --package=@npmcli/foo
```

```bash
$ npm exec foo@latest bar --package=@npmcli/foo
# $ foo@latest bar
```

```bash
$ npm exec -- foo@latest bar --package=@npmcli/foo
# Equivalent to the npx command
```

--------------------------------

### Querying for dependencies with specific licenses

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Selects dependencies that have either the MIT or ISC license.

```bash
[license=MIT], [license=ISC]
```

--------------------------------

### Specify Primary Module Entry Point

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'main' field designates the primary module ID that serves as the main entry point for a package. When a user requires the package, the exports object of this module is returned. It should be a path relative to the package root, defaulting to 'index.js' if not specified.

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "main": "lib/main.js"
}
```

--------------------------------

### npm search with JSON Output Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

This configuration option enables JSON output for the npm search command. When set to true, the command will return results in JSON format instead of the default human-readable table. This is useful for programmatic parsing of search results.

```bash
# To enable JSON output for npm search:
npm config set json true

# To disable JSON output:
npm config set json false
```

--------------------------------

### Add another workspace as a dependency

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

This demonstrates how to add one workspace as a dependency of another using the `workspace:` protocol. This ensures local linking rather than fetching from the registry, and `*` indicates using the version defined in the depended-upon workspace's `package.json`.

```bash
npm install b@workspace:* -w a
```

--------------------------------

### Extract Multiple Fields and Version History with npm view

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

You can request multiple fields simultaneously, and npm view will print their values sequentially. It also supports viewing version history or data across a range of versions.

```bash
# Example: Get all contributor names and emails for 'express'
npm view express contributors.name contributors.email

# Example: View the version history of the 'connect' package
npm view connect versions

# Example: View 'jsdom' dependencies for 'yui3' versions matching a range
npm view yui3@'>0.5.4' dependencies.jsdom
```

--------------------------------

### Accessing npm Package Information in Scripts (Legacy)

Source: https://docs.npmjs.com/cli/v11/using-npm/scripts

Illustrates how to access package information using environment variables set by npm. These variables are derived from the package.json file. Note that in npm 7+, most of these variables are deprecated and direct file reading is recommended.

```javascript
console.log(process.env.npm_package_name);
console.log(process.env.npm_package_version);
```

--------------------------------

### Querying for direct production dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Filters for direct dependencies that are marked as production dependencies.

```bash
:root > .prod
```

--------------------------------

### npm config edit

Source: https://docs.npmjs.com/cli/config

Opens the user or global npm configuration file in the default editor.

```APIDOC
## GET /npm config edit

### Description
Opens the config file in an editor. Use the `--global` flag to edit the global config.

### Method
GET

### Endpoint
/npm config edit

### Parameters
#### Query Parameters
- **global** (boolean) - Optional - If true, opens the global npm configuration file for editing.

### Request Example
```http
GET /npm config edit?global=true
```

### Response
#### Success Response (200)
- **message** (string) - Message indicating the editor has been opened for the specified configuration file.

#### Response Example
```json
{
  "message": "Opening global npm config file in editor..."
}
```
```

--------------------------------

### Bumping Package Version with npm

Source: https://docs.npmjs.com/cli/v11/commands/npm-version

This command bumps the package version and updates relevant package files. It accepts a version argument like 'patch', 'minor', 'major', 'prepatch', 'preminor', 'premajor', 'prerelease', or 'from-git'. The 'from-git' option uses the latest git tag. If the current version is a prerelease, 'patch' will remove the suffix instead of incrementing.

```bash
npm version patch
npm version minor
npm version major
npm version prerelease
npm version from-git
```

--------------------------------

### Querying for direct dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Selects only the direct dependencies of the current project.

```bash
:root > *
```

--------------------------------

### Specify Package License using SPDX Identifiers

Source: https://docs.npmjs.com/files/package

Defines the license for an npm package using a single SPDX license identifier. This is the recommended approach for common licenses like BSD-3-Clause or MIT.

```json
{
  "license": "BSD-3-Clause"
}
```

--------------------------------

### Generate Package Tarball with npm

Source: https://docs.npmjs.com/cli/v11/using-npm/developers

Generates a tarball of your package locally, mimicking the process of publishing. This is useful for verifying the contents of your package before publishing.

```bash
npm pack
```

--------------------------------

### Providing One-Time Password (OTP) for npm Access

Source: https://docs.npmjs.com/cli/v11/commands/npm-access

Demonstrates how to provide a one-time password (OTP) for two-factor authentication when performing sensitive operations like publishing or changing package permissions using the `--otp` option.

```bash
npm access --otp=<one-time-password>
```

--------------------------------

### Enable JSON output for npm commands

Source: https://docs.npmjs.com/cli-documentation/access

Explains how to configure npm to output command results in JSON format instead of the default human-readable text. This is particularly useful for scripting and automated processing.

```bash
npm config set json true
```

--------------------------------

### Signing Git Tags with npm Version

Source: https://docs.npmjs.com/cli/v11/commands/npm-version

This shows how to configure npm to sign git tags automatically during the versioning process. This requires GPG to be set up correctly in your git configuration. You will be prompted for your GPG passphrase.

```bash
npm config set sign-git-tag true
npm version patch
```

--------------------------------

### Using npm Lifecycle Event Variable

Source: https://docs.npmjs.com/cli/v11/using-npm/scripts

Demonstrates how to use the `npm_lifecycle_event` environment variable to control script behavior based on the current npm lifecycle stage. This allows a single script to perform different actions depending on whether it's being run as 'prepare', 'test', etc.

```javascript
if (process.env.npm_lifecycle_event === 'prepare') {
  console.log('Running prepare script...');
} else if (process.env.npm_lifecycle_event === 'test') {
  console.log('Running test script...');
}
```

--------------------------------

### npm search with Registry Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

Sets the base URL for the npm registry used by the search command. The default registry is https://registry.npmjs.org/

```bash
# Set to a private registry:
npm config set registry http://localhost:4873

# Reset to the public registry:
npm config set registry https://registry.npmjs.org/
```

--------------------------------

### Run a script in a specific workspace

Source: https://docs.npmjs.com/cli/v11/commands/npm-run

Allows running a script within the context of a single, named workspace. This is achieved using the 'workspace' configuration option, specifying either the workspace name or its directory path.

```bash
npm test --workspace=a
```

```bash
npm test -w a -w b
```

--------------------------------

### Cache Min (Deprecated)

Source: https://docs.npmjs.com/misc/config

Deprecated option in favor of `--prefer-offline`.

```APIDOC
## `cache-min` (Deprecated)

### Description
This option has been deprecated in favor of `--prefer-offline`. `--cache-min=9999` (or bigger) is an alias for `--prefer-offline`.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **cache-min** (Number) - Optional - Minimum cache size (deprecated).

### Request Example
```
npm config set cache-min 9999
```

### Response
#### Success Response (200)
Configuration updated.

#### Response Example
N/A
```

--------------------------------

### Run npm Audit

Source: https://docs.npmjs.com/cli/audit

The basic synopsis for running the npm audit command, which checks for security vulnerabilities in project dependencies. It can optionally include 'fix' or 'signatures' arguments.

```bash
npm audit [fix|signatures]
```

--------------------------------

### npm Profile Command Synopsis

Source: https://docs.npmjs.com/cli/profile

This snippet outlines the basic syntax for various npm profile commands. It covers enabling and disabling two-factor authentication, retrieving profile information, and setting profile properties. Note that this command is unaware of workspaces.

```bash
npm profile enable-2fa [auth-only|auth-and-writes]
npm profile disable-2fa
npm profile get [<key>]
npm profile set <key> <value>
```

--------------------------------

### Define Funding as an Object

Source: https://docs.npmjs.com/files/package

Specifies funding information for an npm package using an object. This object can detail the type of funding (e.g., 'individual', 'patreon') and a corresponding URL.

```json
{
  "funding": {
    "type": "individual",
    "url": "http://npmjs.com/donate"
  }
}
```

```json
{
  "funding": {
    "type": "patreon",
    "url": "https://www.patreon.com/user"
  }
}
```

--------------------------------

### Client Certificate

Source: https://docs.npmjs.com/misc/config

Provides a client certificate for registry access. Deprecated for most registry operations.

```APIDOC
## `cert` (Deprecated)

### Description
A client certificate to pass when accessing the registry. Values should be in PEM format (Windows calls it "Base-64 encoded X.509 (.CER)") with newlines replaced by the string `\n`. For example: `cert="-----BEGIN CERTIFICATE-----\nXXXX\nXXXX\n-----END CERTIFICATE-----"`. It is _not_ the path to a certificate file, though you can set a registry-scoped `certfile` path like `//other-registry.tld/:certfile=/path/to/cert.pem`. `key` and `cert` are no longer used for most registry operations. Use registry scoped `keyfile` and `certfile` instead.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **cert** (String) - Optional - The client certificate in PEM format.

### Request Example
```
npm config set cert "-----BEGIN CERTIFICATE-----\nMIID...\n-----END CERTIFICATE-----"
```

### Response
#### Success Response (200)
Configuration updated.

#### Response Example
N/A
```

--------------------------------

### Specify User Certificate for Registry Access

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Provides a client certificate in PEM format for secure access to the NPM registry. Newlines within the certificate must be replaced by '\n'. This is a deprecated method, and registry-scoped 'certfile' is recommended.

```text
cert="-----BEGIN CERTIFICATE-----\nXXXX\nXXXX\n-----END CERTIFICATE-----"
```

--------------------------------

### Querying for dependencies with a specific version

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Finds dependencies that exactly match a given version number.

```bash
#lodash@2.1.5
// equivalent to...
[name="lodash"][version="2.1.5"]
```

--------------------------------

### Referencing Direct Dependency Versions in Overrides in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Demonstrates how to use a '$' prefix in `package.json` overrides to reference the version specifier of a direct dependency. This simplifies managing overrides when the desired version matches a direct dependency's version.

```json
{
  "dependencies": {
    "@npm/foo": "^1.0.0"
  },
  "overrides": {
    "@npm/foo": "$foo",
    "@npm/bar": "$foo"
  }
}
```

--------------------------------

### View npm Profile Settings via CLI

Source: https://docs.npmjs.com/managing-your-profile-settings

This command allows you to view your current user profile settings from the command line. Ensure your npm client is updated to version 5.5.1 or higher. No specific inputs are required, and the output displays your profile details.

```bash
npm profile get
```

--------------------------------

### Configure Git URLs for GitHub Proxies

Source: https://docs.npmjs.com/common-errors

Bash commands to configure Git globally to use HTTPS URLs for GitHub repositories, bypassing issues with `git:` or `ssh+git:` protocols when behind proxies. This ensures better compatibility with network restrictions.

```bash
git config --global url."https://github.com/".insteadOf git@github.com:
git config --global url."https://".insteadOf git://
```

--------------------------------

### npm search with Search Exclude Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

Specifies patterns to exclude from npm search results. These options are space-separated and help refine the search by filtering out unwanted packages.

```bash
# Exclude packages containing 'beta' or 'alpha':
npm config set searchexclude "beta alpha"

# Clear custom exclude options:
npm config delete searchexclude
```

--------------------------------

### Querying for direct development dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Filters for direct dependencies that are marked as development dependencies.

```bash
:root > .dev
```

--------------------------------

### Define Author or Contributor Person Object

Source: https://docs.npmjs.com/files/package

Defines a person's details (name, email, URL) for package authorship or contribution. The 'name' field is mandatory, while 'email' and 'url' are optional.

```json
{
  "name": "Barney Rubble",
  "email": "barney@npmjs.com",
  "url": "http://barnyrubble.npmjs.com/"
}
```

--------------------------------

### Configuring npm Registry URL

Source: https://docs.npmjs.com/cli/v11/commands/npm-access

Shows how to specify a custom npm registry URL using the `--registry` configuration option. This is useful when working with private or alternative npm registries.

```bash
npm config set registry=<registry url>
```

--------------------------------

### Binary Link Creation

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Control whether npm creates symlinks for package executables. Set to false to disable symlink creation.

```APIDOC
## `bin-links`

### Description
Tells npm to create symlinks (or `.cmd` shims on Windows) for package executables. Set to false to have it not do this. This can be used to work around the fact that some file systems don't support symlinks, even on ostensibly Unix systems.

### Type
Boolean

### Default
`true`
```

--------------------------------

### Run npm trust Command

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

This is the basic synopsis for the npm trust command. It is used to manage trusted publishing relationships. Note that this command is unaware of workspaces.

```bash
npm trust
```

--------------------------------

### Set User-Agent Request Header

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Configures the User-Agent header for NPM requests. It allows dynamic replacement of placeholders like npm version, Node.js version, platform, architecture, workspace status, and CI environment.

```text
user-agent = "npm/{npm-version} node/{node-version} {platform} {arch} workspaces/{workspaces} {ci}"
```

--------------------------------

### List Packages Accessible by Organization User (npm CLI)

Source: https://docs.npmjs.com/cli/v11/using-npm/orgs

This command lists all packages within an organization that a specific user can access. It helps in monitoring individual permissions.

```bash
npm access list packages <org> <user>
```

--------------------------------

### Define Project Workspaces

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

An array of file patterns that specifies locations for workspaces within the local file system. These workspaces will be symlinked to the top-level node_modules folder.

```json
{
  "name": "workspace-example",
  "workspaces": ["./packages/*"]
}
```

--------------------------------

### npm config set

Source: https://docs.npmjs.com/cli/config

Sets one or more npm configuration keys to the specified values. This command modifies the user configuration file by default.

```APIDOC
## POST /npm config set

### Description
Sets each of the config keys to the value provided. Modifies the user configuration file unless `location` is passed.
If value is omitted, the key will be removed from your config file entirely.

### Method
POST

### Endpoint
/npm config set

### Parameters
#### Query Parameters
- **key** (string) - Required - The configuration key to set.
- **value** (string) - Optional - The value to assign to the configuration key. If omitted, the key is removed.

### Request Example
```json
{
  "key": "registry",
  "value": "https://registry.npmjs.org/"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the configuration was updated.

#### Response Example
```json
{
  "message": "Configuration updated successfully."
}
```
```

--------------------------------

### Specify People Fields (Author, Contributors)

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Details how to define the 'author' and 'contributors' fields in package metadata. A 'person' can be an object with 'name', 'email', and 'url', or a single string that npm parses.

```json
{
  "name": "Barney Rubble",
  "email": "barney@npmjs.com",
  "url": "http://barnyrubble.npmjs.com/"
}
```

```json
{
  "author": "Barney Rubble <barney@npmjs.com> (http://barnyrubble.npmjs.com/)"
}
```

--------------------------------

### Querying for workspaces with peer dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Selects workspaces that include peer dependencies.

```bash
.workspace:has(.peer)
```

--------------------------------

### npm access Synopsis

Source: https://docs.npmjs.com/cli/access

Provides a summary of the available npm access subcommands for managing package permissions. These commands interact with the npm registry to control access levels.

```bash
npm access list packages [<user>|<scope>|<scope:team>] [<package>]
npm access list collaborators [<package> [<user>]]
npm access get status [<package>]
npm access set status=public|private [<package>]
npm access set mfa=none|publish|automation [<package>]
npm access grant <read-only|read-write> <scope:team> [<package>]
npm access revoke <scope:team> [<package>]
```

--------------------------------

### Workspace Filtering

Source: https://docs.npmjs.com/misc/config

Enables running commands within specific workspaces.

```APIDOC
## `workspace`

### Description
Enable running a command in the context of the configured workspaces of the current project while filtering by running only the workspaces defined by this configuration option. Valid values for the `workspace` config are either: Workspace names, Path to a workspace directory, or Path to a parent workspace directory (will result in selecting all workspaces within that folder). When set for the `npm init` command, this may be set to the folder of a workspace which does not yet exist, to create the folder and set it up as a brand new workspace within the project. This value is not exported to the environment for child processes.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **workspace** (String) - Optional - The name or path of the workspace to run the command in.

### Request Example
```
npm run build --workspace=my-package
```

### Response
#### Success Response (200)
Command executed within the specified workspace.

#### Response Example
N/A
```

--------------------------------

### Run NPM Script in Workspace Directory

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

Navigate to a specific workspace directory and run an npm script. This provides an alternative method to using the `--workspace` flag, directly executing the command within the target package's environment.

```bash
cd packages/a && npm run test
```

--------------------------------

### Run NPM Script in All Workspaces

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

Execute an npm script in all configured workspaces. This is a convenient way to run a command across the entire monorepo. The command will run the 'test' script in every package defined in the 'workspaces' array of the root package.json.

```bash
npm run test --workspaces
```

--------------------------------

### Configure Development Engines

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Sets requirements for the development environment, ensuring consistency among engineers working on the codebase. It can specify runtime and package manager details, with options to warn or error on failure.

```json
{
  "devEngines": {
    "runtime": {
      "name": "node",
      "onFail": "error"
    },
    "packageManager": {
      "name": "npm",
      "onFail": "error"
    }
  }
}
```

--------------------------------

### Execute Command in All Workspaces with npm exec --ws

Source: https://docs.npmjs.com/cli/v11/commands/npm-exec

Executes a specified command in the context of all configured workspaces within a project. This is useful for running linters, tests, or build scripts across your entire workspace.

```bash
npm exec --ws -- eslint ./*.js
```

--------------------------------

### Run scripts in all configured workspaces

Source: https://docs.npmjs.com/cli/v11/commands/npm-run

Executes a specified script across all packages defined in the project's workspace configuration. This is useful for running common tasks like tests or builds on multiple packages simultaneously.

```bash
npm test --workspaces
```

--------------------------------

### Specify Browser-Specific Entry Point

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'browser' field is used instead of 'main' when a module is intended for client-side (browser) execution. It signals that the module might depend on browser-specific primitives like 'window', which are not available in Node.js environments.

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "browser": "./dist/browser.js"
}
```

--------------------------------

### Define Package Entry Points with Exports

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'exports' field offers a modern approach to defining package entry points, surpassing the 'main' field. It supports multiple entry points, conditional resolution for different environments, and encapsulates the package's public interface, enhancing clarity and control.

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "exports": {
    ".": "./index.js",
    "./feature": "./feature.js"
  }
}
```

--------------------------------

### Querying for dependencies by name and semver range

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Selects dependencies named 'lodash' that fall within the specified semantic versioning range.

```bash
#lodash@^1.2.3
// equivalent to...
[name="lodash"]:semver(^1.2.3)
```

--------------------------------

### Simulate Unpublish Action with Dry Run Option

Source: https://docs.npmjs.com/cli/unpublish

The `dry-run` option allows you to see what actions `npm unpublish` would take without actually making any changes to the registry. This is useful for verifying the command before executing it.

```bash
npm unpublish --dry-run [<package-spec>]
```

--------------------------------

### Querying for workspaces that depend on other workspaces

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Finds workspaces that have other workspaces as dependencies.

```bash
.workspace > .workspace
```

--------------------------------

### Configure GitHub Actions Runner

Source: https://docs.npmjs.com/generating-provenance-statements

This configuration specifies that the GitHub Actions workflow should run on an Ubuntu-hosted runner. Using a cloud-hosted runner is a prerequisite for generating provenance attestations.

```yaml
runs-on: ubuntu-latest
```

--------------------------------

### Managing npm Two-Factor Authentication (2FA)

Source: https://docs.npmjs.com/cli/profile

This section details commands for managing two-factor authentication. `enable-2fa` can be used with `auth-and-writes` (default) or `auth-only` modes, requiring OTPs for specific actions. `disable-2fa` removes this security layer.

```bash
npm profile enable-2fa
npm profile enable-2fa auth-only
npm profile disable-2fa
```

--------------------------------

### Initialize npm Package with Scope

Source: https://docs.npmjs.com/private-modules/intro

Initializes a new npm package and assigns it to a scope, which is necessary for private packages. Use '@my-org' for organization-scoped packages or '@my-username' for user-scoped packages.

```shell
npm init --scope=@my-org
# or
npm init --scope=@my-username
```

--------------------------------

### npm cache npx list entries

Source: https://docs.npmjs.com/cli/v11/commands/npm-cache

Lists all entries currently stored in the npx cache.

```bash
npm cache npx ls
```

--------------------------------

### Attribute Selectors for package.json (String Values)

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

Attribute selectors evaluate key/value pairs in `package.json` if they are strings. Various operators like '=', '~=', '*=', '|=', '^=', and '$=' can be used for matching.

```css
/* Checks for the existence of an attribute */
[attribute]

/* Checks if attribute value is equivalent to 'value' */
[attribute=value]

/* Checks if attribute value contains the word 'value' */
[attribute~=value]

/* Checks if attribute value contains the string 'value' */
[attribute*=value]

/* Checks if attribute value is equal to or starts with 'value' */
[attribute|=value]

/* Checks if attribute value starts with 'value' */
[attribute^=value]

/* Checks if attribute value ends with 'value' */
[attribute$=value]
```

--------------------------------

### npm trust - Main Command

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

The main `npm trust` command is used to initiate the configuration of trusted publishing relationships. It requires specific arguments and prerequisites to function correctly.

```APIDOC
## npm trust

### Description
Manages trusted publishing relationships between npm packages and CI/CD providers using OpenID Connect (OIDC). This is the command-line equivalent of managing trusted publisher configurations on the npm website.

### Synopsis
```
npm trust
```

### Prerequisites
*   **npm version**: `npm@11.10.0` or above.
*   **Write permissions on the package**: You must have write access to the package.
*   **2FA enabled on account**: Two-factor authentication must be enabled.
*   **Supported authentication methods**: Granular Access Tokens (GAT) with bypass 2FA and legacy basic auth are not supported.
*   **Package must exist**: The package must already exist on the npm registry.

### Usage Notes
*   The `[package]` argument specifies the package name. If omitted, npm uses the name from `package.json`.
*   Configuration options vary based on the CI/CD provider and their OIDC claims. Use `npm trust <provider> --help` for specific details.
*   The registry supports only one configuration per package. To replace an existing configuration, revoke the old one first using `npm trust revoke --id <id> [package]`.
```

--------------------------------

### Publish Package to npmjs with GitLab CI/CD

Source: https://docs.npmjs.com/generating-provenance-statements

This GitLab CI job automates the publishing of an npm package with provenance enabled when a Git tag is pushed. It uses a Node.js Docker image, sets up authentication using the `NPM_TOKEN` project variable, and executes the `npm publish` command with the `--provenance` flag. This ensures that published packages have verifiable origin information.

```yaml
publish:
  image: 'node:20'
  rules:
    - if: $CI_COMMIT_TAG
  id_tokens:
    SIGSTORE_ID_TOKEN:
      aud: sigstore
  script:
    - npm config set //registry.npmjs.org/:_authToken "$NPM_TOKEN"
    - npm publish --provenance --access public

```

--------------------------------

### Set JSON Value using npm pkg set --json

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Shows how to set a boolean 'private' property to true by parsing the value as JSON.

```bash
npm pkg set private=true --json
```

--------------------------------

### Enable 2FA for Authorization and Writes (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command enables two-factor authentication for both general authorization and write actions on your npm account. It ensures that a second form of authentication is required for sensitive operations, enhancing account security.

```bash
npm profile enable-2fa auth-and-writes
```

--------------------------------

### Build Docker image with npm authentication token

Source: https://docs.npmjs.com/docker-and-private-modules

The command to build a Docker image using the provided Dockerfile and an npm authentication token sourced from the user's global .npmrc file via Docker build secrets. The '.' specifies the build context, and '-t' tags the image.

```bash
docker build . -t secure-app-secrets:1.0 --secret id=npmrc,src=$HOME/.npmrc
```

--------------------------------

### Publish Specific Workspace (CLI)

Source: https://docs.npmjs.com/cli/publish

Publishes a specific workspace within a monorepo to the npm registry. Requires the --workspace flag followed by the workspace name.

```bash
npm publish --workspace=<workspace-name>
```

--------------------------------

### npm cache list entries

Source: https://docs.npmjs.com/cli/v11/commands/npm-cache

Lists specified entries or all entries currently stored in the local npm cache.

```bash
npm cache ls [<name>@<version>]
```

--------------------------------

### Workspace Filtering

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Enable running commands within specific workspaces of a project. Can filter by workspace names or paths.

```APIDOC
## `workspace`

### Description
Enable running a command in the context of the configured workspaces of the current project while filtering by running only the workspaces defined by this configuration option. Valid values for the `workspace` config are either: Workspace names, Path to a workspace directory, or Path to a parent workspace directory (will result in selecting all workspaces within that folder). When set for the `npm init` command, this may be set to the folder of a workspace which does not yet exist, to create the folder and set it up as a brand new workspace within the project. This value is not exported to the environment for child processes.

### Type
String (can be set multiple times)

### Default
N/A
```

--------------------------------

### npm repo

Source: https://docs.npmjs.com/cli/v11/commands/npm-repo

Opens the repository page of a specified npm package in the browser. If no package name is provided, it searches for a package.json in the current directory and uses the 'repository' property.

```APIDOC
## npm repo

### Description
This command tries to guess at the likely location of a package's repository URL, and then tries to open it using the `--browser` config param. If no package name is provided, it will search for a `package.json` in the current folder and use the `repository` property.

### Method
CLI Command

### Endpoint
N/A (CLI command)

### Parameters
#### Path Parameters
- **pkgname** (string) - Optional - The name of the package for which to open the repository.

#### Query Parameters
None

#### Request Body
None

### Request Example
```bash
npm repo <package-name>
```

### Response
#### Success Response
Opens the default web browser to the package's repository URL.

#### Response Example
(Browser opens to repository URL)
```

--------------------------------

### Specify Supported Libc Versions on Linux

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Restricts package compatibility to specific versions of libc, applicable only when the 'os' field is set to 'linux'.

```json
{
  "os": "linux",
  "libc": "glibc"
}
```

--------------------------------

### Registry Signature Conventions

Source: https://docs.npmjs.com/cli/audit

Details the conventions for providing and verifying package signatures and public keys within npm registries.

```APIDOC
## Registry Signature Conventions

### Description
This section outlines the expected format for package signatures within a registry's `packument` and the structure for public signing keys provided by the registry.

### Method
Registry API Specification

### Endpoint
N/A (Specification)

### Parameters
#### Package Signatures (within `packument`)
- **dist.signatures** (array) - Contains signature objects for the package version.
  - **keyid** (string) - Required - The SHA256 fingerprint of the public signing key.
  - **sig** (string) - Required - The generated signature string, typically `${package.name}@${package.version}:${package.dist.integrity}`.

#### Public Signing Keys (at `registry-host.tld/-/npm/v1/keys`)
- **keys** (array) - Contains public key objects.
  - **expires** (string or null) - Optional - Expiration date in ISO 8601 format or null if not expiring.
  - **keyid** (string) - Required - The SHA256 fingerprint of the public key.
  - **keytype** (string) - Required - Currently only `ecdsa-sha2-nistp256` is supported.
  - **scheme** (string) - Required - Currently only `ecdsa-sha2-nistp256` is supported.
  - **key** (string) - Required - The base64 encoded public key.

### Request Example
#### Signature in Packument
```json
"dist":{
  "..omitted..":
```

--------------------------------

### Querying for dependencies by name

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Finds any dependency with the specific name 'lodash'. This is a shorthand for attribute-based queries.

```bash
#lodash
```

--------------------------------

### npm set <key>=<value>

Source: https://docs.npmjs.com/cli/v11/commands/npm-set

The npm-set command is used to set one or more configuration values in the npm configuration file. It accepts key-value pairs as arguments.

```APIDOC
## POST /npm/config

### Description
Sets one or more values in the npm configuration.

### Method
POST

### Endpoint
/npm/config

### Parameters
#### Query Parameters
- **key** (string) - Required - The configuration key to set.
- **value** (string) - Required - The value to assign to the configuration key.
- **global** (boolean) - Optional - Operates in "global" mode, installing packages into the `prefix` folder instead of the current working directory.
- **location** (string) - Optional - Specifies which config file to use. Can be "global", "user", or "project".

### Request Example
```json
{
  "key": "registry",
  "value": "https://registry.npmjs.org/",
  "global": true
}
```

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating the configuration was set.

#### Response Example
```json
{
  "message": "Configuration 'registry' set to 'https://registry.npmjs.org/' globally."
}
```
```

--------------------------------

### Execute Command in Multiple Workspaces with npm exec -w

Source: https://docs.npmjs.com/cli/v11/commands/npm-exec

Executes a command in the context of multiple, specified workspaces. This is achieved by using the `-w` shorthand multiple times, allowing for granular control over command execution.

```bash
npm exec -w a -w b -- eslint ./*.js
```

--------------------------------

### Setting npm Profile Properties

Source: https://docs.npmjs.com/cli/profile

This demonstrates how to update specific profile fields using the `npm profile set` command. Supported properties include email, fullname, homepage, freenode, twitter, and github. Changing the password requires an interactive prompt and may also require an OTP if 2FA is enabled.

```bash
npm profile set email "new.email@example.com"
npm profile set fullname "New Full Name"
npm profile set homepage "https://example.com"
npm profile set password
```

--------------------------------

### List npm teams or team members (npm CLI)

Source: https://docs.npmjs.com/cli/v11/commands/npm-team

Command to list either all teams within an organization or all members of a specific team. If an organization name is provided, it lists teams; if a team name (with scope) is provided, it lists members.

```bash
npm team ls @org
npm team ls @org:newteam
```

--------------------------------

### Workspace Configuration

Source: https://docs.npmjs.com/cli/outdated

The `workspace` configuration option allows you to specify which workspaces to run a command within. It supports workspace names, paths to workspace directories, or paths to parent workspace directories.

```APIDOC
## `workspace` Configuration Option

### Description
Enable running a command in the context of the configured workspaces of the current project while filtering by running only the workspaces defined by this configuration option. Valid values for the `workspace` config are either workspace names, a path to a workspace directory, or a path to a parent workspace directory (which will result in selecting all workspaces within that folder).

When set for the `npm init` command, this may be set to the folder of a workspace which does not yet exist, to create the folder and set it up as a brand new workspace within the project. This value is not exported to the environment for child processes.

### Type
String (can be set multiple times)

### Default
N/A
```

--------------------------------

### Setting Multi-Factor Authentication (MFA) for Automation

Source: https://docs.npmjs.com/cli/access

Explains how to configure multi-factor authentication settings for automated processes interacting with npm packages. This enhances security for CI/CD pipelines.

```bash
npm access set mfa=automation <package-name>
```

--------------------------------

### Check a user's role in an npm organization

Source: https://docs.npmjs.com/cli/v11/commands/npm-org

Shows how to specifically query the role of a particular user within an npm organization. This is helpful for verifying permissions.

```bash
$ npm org ls my-org @mx-santos
```

--------------------------------

### Set npm Configuration Value

Source: https://docs.npmjs.com/cli/config

The `npm config set` command is used to set configuration keys to specific values. It modifies the user configuration file by default. If a value is omitted, the key is removed from the config file.

```bash
npm config set key=value [key=value...]
npm set key=value [key=value...]
```

--------------------------------

### Ensuring a specific number of results with --expect-result-count

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Demonstrates using the `--expect-result-count` flag to make `npm query` exit with an error if the number of results does not match the expected count. This is useful for verifying dependency states.

```bash
$ npm query '#react' --expect-result-count=1
```

--------------------------------

### Querying for packages with a specific contributor

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Finds all packages where '@ruyadorno' is listed as a contributor, based on their email address.

```bash
:attr(contributors, [email=ruyadorno@github.com])
```

--------------------------------

### Replacing a Transitive Dependency with a Fork in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Shows how to replace a transitive dependency (a dependency of a dependency) with a forked version using GitHub repository syntax within nested overrides in `package.json`. This allows for patching vulnerabilities or issues in indirect dependencies.

```json
{
  "overrides": {
    "parent-package": {
      "vulnerable-dep": "github:username/patched-fork#v2.0.1"
    }
  }
}
```

--------------------------------

### Publish npm Package with Provenance

Source: https://docs.npmjs.com/generating-provenance-statements

This command publishes an npm package and includes the `--provenance` flag to generate a provenance attestation. This attestation verifies the package's build environment and publisher, enhancing supply-chain security.

```bash
npm publish --provenance
```

--------------------------------

### Enable npm Tab Completion in Current Shell

Source: https://docs.npmjs.com/cli/v11/commands/npm-completion

This command enables tab-completion for npm commands in the current shell session. It directly outputs the completion script to be evaluated by the shell. No external dependencies are required.

```bash
npm completion
```

--------------------------------

### Cache Max (Deprecated)

Source: https://docs.npmjs.com/misc/config

Deprecated option in favor of `--prefer-online`.

```APIDOC
## `cache-max` (Deprecated)

### Description
This option has been deprecated in favor of `--prefer-online`. `--cache-max=0` is an alias for `--prefer-online`.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Query Parameters
- **cache-max** (Number) - Optional - Maximum cache size (deprecated).

### Request Example
```
npm config set cache-max 0
```

### Response
#### Success Response (200)
Configuration updated.

#### Response Example
N/A
```

--------------------------------

### Create a new npm team (npm CLI)

Source: https://docs.npmjs.com/cli/v11/commands/npm-team

Command to create a new team within a specified organization scope. Requires the team name to be prefixed with the organization scope (e.g., `@org:newteam`). A confirmation message is displayed upon successful creation.

```bash
npm team create @org:newteam
```

--------------------------------

### npm search with Prefer Offline Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

When true, this option bypasses staleness checks for cached data. Missing data will still be requested from the server. For complete offline mode, use the --offline flag.

```bash
# Enable prefer-offline mode:
npm config set "prefer-offline" true

# Disable prefer-offline mode:
npm config set "prefer-offline" false
```

--------------------------------

### Log out from a Custom Registry with a Scope (CLI)

Source: https://docs.npmjs.com/cli/adduser

This command logs you out from a specified npm registry and removes the link associated with the given scope. This action also revokes the authentication token for that scope, ensuring security when accessing private registries.

```bash
# log out, removing the link and the auth token
npm logout --scope=@mycorp
```

--------------------------------

### Edit npm Configuration File

Source: https://docs.npmjs.com/cli/config

The `npm config edit` command opens the user's npm configuration file in the default editor. Use the `--global` flag to edit the global configuration file instead.

```bash
npm config edit
```

--------------------------------

### Link Package to Workspace (--workspace)

Source: https://docs.npmjs.com/cli/v11/commands/npm-link

Links a specified package as a dependency of one or more workspaces within a project. The package might be linked into the parent project's `node_modules` if no dependency conflicts exist. This command is used in conjunction with npm workspaces.

```bash
npm link <pkg> --workspace <name>
```

--------------------------------

### Navigate to Project Directory

Source: https://docs.npmjs.com/updating-packages-downloaded-from-the-registry

Changes the current directory to the root of your project, which should contain a package.json file. This is the first step before updating local packages.

```bash
cd /path/to/project
```

--------------------------------

### Manage npm Organization Teams and Memberships (npm CLI)

Source: https://docs.npmjs.com/cli/team

This command group is used to manage teams within npm organizations. It allows for the creation, deletion, addition, and removal of users from teams, as well as listing teams and their members. Teams must be fully qualified with their scope (e.g., `@org:teamname`). Two-factor authentication can be handled with the `--otp` flag.

```bash
npm team create <scope:team> [--otp <otpcode>]
npm team destroy <scope:team> [--otp <otpcode>]
npm team add <scope:team> <user> [--otp <otpcode>]
npm team rm <scope:team> <user> [--otp <otpcode>]
npm team ls <scope>|<scope:team>
```

```bash
npm team create @org:newteam
```

```bash
npm team add @org:newteam username
```

```bash
npm team rm @org:newteam username
```

```bash
npm team ls @org
```

```bash
npm team ls @org:newteam
```

--------------------------------

### Include Workspace Root

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Determine whether the workspace root is included when workspaces are enabled for a command. Defaults to false.

```APIDOC
## `include-workspace-root`

### Description
Include the workspace root when workspaces are enabled for a command. When false, specifying individual workspaces via the `workspace` config, or all workspaces via the `workspaces` flag, will cause npm to operate only on the specified workspaces, and not on the root project. This value is not exported to the environment for child processes.

### Type
Boolean

### Default
`false`
```

--------------------------------

### Specify Repository in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'repository' field indicates where the package's source code resides, aiding contributions and VCS integration. It can be a shorthand string or a detailed object. npm normalizes shorthand formats to the full object format upon publishing, so using the full format is recommended for clarity and future compatibility.

```json
{
  "repository": {
    "type": "git",
    "url": "git+https://github.com/npm/cli.git"
  }
}
```

```json
{
  "repository": "npm/example"
}
```

```json
{
  "repository": "github:npm/example"
}
```

```json
{
  "repository": "gist:11081aaa281"
}
```

```json
{
  "repository": "bitbucket:user/repo"
}
```

```json
{
  "repository": "gitlab:user/repo"
}
```

```json
{
  "repository": {
    "type": "git",
    "url": "git+https://github.com/npm/example.git"
  }
}
```

```json
{
  "repository": {
    "type": "git",
    "url": "git+https://github.com/npm/cli.git",
    "directory": "workspaces/libnpmpublish"
  }
}
```

--------------------------------

### npm Completion in Plumbing Mode

Source: https://docs.npmjs.com/cli/v11/commands/npm-completion

When environment variables COMP_CWORD, COMP_LINE, and COMP_POINT are set, 'npm completion' enters 'plumbing mode'. In this mode, it outputs completions based on the provided arguments, suitable for scripting and automated completion tasks. This functionality is internal to npm's completion mechanism.

```bash
# Example of how it might be invoked in plumbing mode (environment variables set externally)
COMP_CWORD=2 COMP_LINE="npm install lod" COMP_POINT=15 npm completion
```

--------------------------------

### Verify npm package provenance attestations

Source: https://docs.npmjs.com/generating-provenance-statements

This command verifies the provenance attestations of downloaded npm packages. Running `npm audit signatures` checks for verified registry signatures and provenance attestations for all packages in a project. It's recommended to keep the npm CLI updated to ensure compatibility with the latest attestation formats and verification methods.

```bash
npm audit signatures

```

--------------------------------

### npm view - Version History

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

Fetches the version history for a specified npm package.

```APIDOC
## GET /npm/view/{package-spec}/versions

### Description
Retrieves a list of all published versions for a given npm package.

### Method
GET

### Endpoint
/npm/view/{package-spec}/versions

### Parameters
#### Path Parameters
- **package-spec** (string) - Required - The name of the package (e.g., 'connect').

### Request Example
```
GET /npm/view/connect/versions
```

### Response
#### Success Response (200)
- **versions** (array) - A list of version strings.

#### Response Example
```json
{
  "versions": [
    "0.1.0",
    "0.1.1",
    "0.2.0",
    "3.7.0"
  ]
}
```
```

--------------------------------

### Add a registry dependency to a workspace

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

This command adds a dependency from the npm registry to a specific workspace. The `-w` flag targets the workspace by its name or path, ensuring the dependency is added to that workspace's `package.json`.

```bash
npm install abbrev -w a
```

--------------------------------

### Specify Node.js Engine Version

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Defines the compatible Node.js engine versions for a package. This helps ensure the package runs in the intended environment. Versions can be specified using ranges like '>=0.10.3 <15'.

```json
{
  "engines": {
    "node": ">=0.10.3 <15"
  }
}
```

--------------------------------

### Set npm configuration value

Source: https://docs.npmjs.com/cli/v11/commands/npm-set

This command sets a specific value in the npm configuration. It accepts one or more key-value pairs. The command is unaware of workspaces and is equivalent to using `npm config set <key>=<value>`.

```bash
npm set <key>=<value> [<key>=<value> ...]
```

--------------------------------

### Enable 2FA for Authorization Only (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command enables two-factor authentication for authorization actions only on your npm account. Write actions will not require a second form of authentication, offering a less stringent security posture.

```bash
npm profile enable-2fa auth-only
```

--------------------------------

### Configure npm publish provenance via package.json

Source: https://docs.npmjs.com/generating-provenance-statements

This configuration snippet can be added to your `package.json` file to enable provenance for npm package publishing. When present, the `npm publish` command will automatically include provenance information without requiring additional command-line flags. This is a convenient way to ensure provenance for all your published packages.

```json
"publishConfig": {
  "provenance": true
},

```

--------------------------------

### Deprecate Packages (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command marks a package as deprecated in the npm registry. Deprecation is a way to inform users that a package is no longer recommended for use.

```bash
npm deprecate
```

--------------------------------

### Access Specific Package Fields with npm view

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

You can access specific fields and nested properties of a package's metadata by specifying them after the package name. Dot notation is used for nested object fields, and you can combine version specifiers with field access.

```bash
# Example: View dependencies of 'ronn' package at version '0.3.5'
npm view ronn@0.3.5 dependencies

# Example: View the git repository URL for the latest 'npm' package
npm view npm repository.url
```

--------------------------------

### npm search with Search Limit Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

Sets the maximum number of results to return for an npm search query. The default limit is 20. This setting may not apply to legacy search implementations.

```bash
# Set search limit to 50 results:
npm config set searchlimit 50

# Reset to default limit (20):
npm config set searchlimit 20
```

--------------------------------

### Add or change a user's role to admin in an npm organization

Source: https://docs.npmjs.com/cli/v11/commands/npm-org

Shows how to assign the 'admin' role to a user in an npm organization. This can be used for new users or to upgrade an existing user's permissions.

```bash
$ npm org set my-org @mx-santos admin
```

--------------------------------

### List Trusted Relationships with npm

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

The 'npm trust list' command displays existing trusted relationships for a specified package. It can optionally output the results in JSON format for easier parsing.

```bash
npm trust list [package]
```

--------------------------------

### Display npm root directory

Source: https://docs.npmjs.com/cli/v11/commands/npm-root

Prints the effective node_modules folder to standard output. This is useful for integrating npm's module directory into shell scripts.

```bash
npm root

```

--------------------------------

### Querying for peer dependencies of direct dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Selects any peer dependency of a direct dependency.

```bash
:root > * > .peer
```

--------------------------------

### npm version Command Usage

Source: https://docs.npmjs.com/cli/v11/commands/npm-version

The `npm version` command is used to bump a package version. It can accept a specific version number or keywords like 'major', 'minor', 'patch', etc.

```APIDOC
## npm version Command

### Description

Bumps a package version in your `package.json` file and optionally creates a git tag.

### Method

CLI Command

### Endpoint

N/A (Local CLI command)

### Parameters

#### CLI Arguments

- **`<newversion> | major | minor | patch | premajor | preminor | prepatch | prerelease | from-git`** (string) - Required - The new version number or a keyword to determine the version bump.

### Configuration Options

#### `allow-same-version`
  * Default: `false`
  * Type: Boolean
  * Description: Prevents throwing an error when `npm version` is used to set the new version to the same value as the current version.

#### `commit-hooks`
  * Default: `true`
  * Type: Boolean
  * Description: Run git commit hooks when using the `npm version` command.

#### `git-tag-version`
  * Default: `true`
  * Type: Boolean
  * Description: Tag the commit when using the `npm version` command. Setting this to false results in no commit being made at all.

#### `json`
  * Default: `false`
  * Type: Boolean
  * Description: Whether or not to output JSON data, rather than the normal output.

#### `preid`
  * Default: `""`
  * Type: String
  * Description: The "prerelease identifier" to use as a prefix for the "prerelease" part of a semver. Like the `rc` in `1.2.0-rc.8`.

#### `sign-git-tag`
  * Default: `false`
  * Type: Boolean
  * Description: If set to true, then the `npm version` command will tag the version using `-s` to add a signature. Note that git requires you to have set up GPG keys in your git configs for this to work properly.

#### `save`
  * Default: `true` unless when using `npm update` where it defaults to `false`
  * Type: Boolean
  * Description: Save installed packages to a `package.json` file as dependencies. When used with the `npm rm` command, removes the dependency from `package.json`. Will also prevent writing to `package-lock.json` if set to `false`.

#### `workspace`
  * Default: N/A
  * Type: String (can be set multiple times)
  * Description: Enable running a command in the context of the configured workspaces of the current project while filtering by running only the workspaces defined by this configuration option.

#### `workspaces`
  * Default: `null`
  * Type: null or Boolean
  * Description: Set to true to run the command in the context of **all** configured workspaces. Explicitly setting this to false will cause commands like `install` to ignore workspaces altogether.

#### `workspaces-update`
  * Default: `true`
  * Type: Boolean
  * Description: If set to true, the npm cli will run an update after operations that may possibly change the workspaces installed to the `node_modules` folder.

#### `include-workspace-root`
  * Default: `false`
  * Type: Boolean
  * Description: Include the workspace root when workspaces are enabled for a command. When false, specifying individual workspaces via the `workspace` config, or all workspaces via the `workspaces` flag, will cause npm to operate only on the specified workspaces, and not on the root project.

#### `ignore-scripts`
  * Default: `false`
  * Type: Boolean
  * Description: If true, npm does not run scripts specified in package.json files. Note that commands explicitly intended to run a particular script, such as `npm start`, `npm stop`, `npm restart`, `npm test`, and `npm run` will still run their intended script if `ignore-scripts` is set, but they will _not_ run any pre- or post-scripts.

### Request Example

```bash
npm version patch
```

### Response

#### Success Response (Output)

- **Output** (string) - The command-line output indicating the version bump and any git operations.

#### Response Example

```
+ v1.0.1
```
```

--------------------------------

### npm search with Color Output Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

This configuration option controls the colorization of npm search output. By default, colors are enabled if the terminal supports them and the NO_COLOR environment variable is not set. Setting it to 'always' forces color, while 'false' disables it.

```bash
# To always show colors:
npm config set color always

# To disable colors:
npm config set color false

# To use default color behavior (based on TTY):
npm config set color true
```

--------------------------------

### npm diff Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-diff

Configuration options that modify the behavior of the `npm diff` command.

```APIDOC
## `diff`

### Description
Define arguments to compare in `npm diff`.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **diff** (String) - Multiple - Description for diff

### Request Example
```json
{
  "diff": ["package-a", "package-b"]
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `diff-name-only`

### Description
Prints only filenames when using `npm diff`.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **diff-name-only** (Boolean) - Optional - Default: false

### Request Example
```json
{
  "diff-name-only": true
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `diff-unified`

### Description
The number of lines of context to print in `npm diff`.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **diff-unified** (Number) - Optional - Default: 3

### Request Example
```json
{
  "diff-unified": 5
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `diff-ignore-all-space`

### Description
Ignore whitespace when comparing lines in `npm diff`.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **diff-ignore-all-space** (Boolean) - Optional - Default: false

### Request Example
```json
{
  "diff-ignore-all-space": true
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `diff-no-prefix`

### Description
Do not show any source or destination prefix in `npm diff` output. This causes `npm diff` to ignore the `--diff-src-prefix` and `--diff-dst-prefix` configs.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **diff-no-prefix** (Boolean) - Optional - Default: false

### Request Example
```json
{
  "diff-no-prefix": true
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `diff-src-prefix`

### Description
Source prefix to be used in `npm diff` output.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **diff-src-prefix** (String) - Optional - Default: "a/"

### Request Example
```json
{
  "diff-src-prefix": "source/"
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `diff-dst-prefix`

### Description
Destination prefix to be used in `npm diff` output.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **diff-dst-prefix** (String) - Optional - Default: "b/"

### Request Example
```json
{
  "diff-dst-prefix": "dest/"
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

```APIDOC
## `diff-text`

### Description
Treat all files as text in `npm diff`.

### Method
N/A (Configuration Option)

### Endpoint
N/A

### Parameters
#### Query Parameters
- **diff-text** (Boolean) - Optional - Default: false

### Request Example
```json
{
  "diff-text": true
}
```

### Response
#### Success Response (200)
N/A (Configuration Option)

#### Response Example
N/A
```

--------------------------------

### Run NPM Script in Workspace Folder

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

Execute an npm script for all workspaces within a specified folder. This command targets all packages located directly inside the 'packages' directory.

```bash
npm run test --workspace=packages
```

--------------------------------

### Nested Overrides for Package and its Children in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Illustrates how to use nested overrides in `package.json` to set a specific version for a package and also for one of its child dependencies. This allows for more precise control over the dependency tree.

```json
{
  "overrides": {
    "@npm/foo": {
      ".": "1.0.0",
      "@npm/bar": "1.0.0"
    }
  }
}
```

--------------------------------

### Add a user to an npm team (npm CLI)

Source: https://docs.npmjs.com/cli/v11/commands/npm-team

Command to add a user to an existing team within an organization. The team must be specified with its scope, followed by the username to be added. A confirmation message indicates the user's successful addition.

```bash
npm team add @org:newteam username
```

--------------------------------

### Deprecate a major version range including prereleases

Source: https://docs.npmjs.com/cli/deprecate

This command shows how to deprecate an entire major version range, like '1.x' for 'my-thing'. SemVer ranges used with npm deprecate include prerelease versions, meaning versions like '1.0.0-beta.0' will also be deprecated.

```bash
npm deprecate my-thing@1.x "1.x is no longer supported"
```

--------------------------------

### Publish New npm Package with Provenance and Public Access

Source: https://docs.npmjs.com/generating-provenance-statements

This command publishes a new npm package, enabling provenance attestation and explicitly setting the package access to public. This is necessary for first-time publishes when provenance is required.

```bash
npm publish --provenance --access public
```

--------------------------------

### POST /-/npm/v1/security/advisories/bulk

Source: https://docs.npmjs.com/cli/audit

The Bulk Advisory endpoint is used by npm to optimize the speed of calculating audit results. It accepts a JSON payload containing package names and versions from the project's dependency tree.

```APIDOC
## POST /-/npm/v1/security/advisories/bulk

### Description
This endpoint is used to efficiently retrieve security advisories for a list of packages and their versions. It is designed to be faster than the Quick Audit endpoint.

### Method
POST

### Endpoint
/-/npm/v1/security/advisories/bulk

### Parameters
#### Request Body
- **packages** (object) - Required - An object where keys are package names and values are arrays of version strings.
  - **Example**: `{"package-name": ["1.0.0", "1.0.1"]}`

### Request Example
```json
{
  "packages": {
    "react": [
      "17.0.1",
      "17.0.2"
    ],
    "lodash": [
      "4.17.20",
      "4.17.21"
    ]
  }
}
```

### Response
#### Success Response (200)
- **advisories** (object) - A mapping of package names to their respective advisory details.
  - **name** (string) - The name of the package.
  - **url** (string) - A URL to the advisory details.
  - **id** (string) - The unique identifier for the advisory.
  - **severity** (string) - The severity level of the vulnerability (e.g., 'low', 'moderate', 'high', 'critical').
  - **vulnerable_versions** (string) - A version range indicating vulnerable versions.
  - **title** (string) - A short title describing the vulnerability.

#### Response Example
```json
{
  "advisories": {
    "react": [
      {
        "name": "react",
        "url": "https://www.npmjs.com/advisories/1234",
        "id": "CVE-2023-XXXX",
        "severity": "moderate",
        "vulnerable_versions": ">=17.0.0 <17.0.2",
        "title": "Cross-site Scripting in React"
      }
    ]
  }
}
```
```

--------------------------------

### Delete Script using npm pkg delete

Source: https://docs.npmjs.com/cli/v11/commands/npm-pkg

Demonstrates how to remove the 'build' script from the 'scripts' object in package.json.

```bash
npm pkg delete scripts.build
```

--------------------------------

### Update Packages with Save (CLI)

Source: https://docs.npmjs.com/cli/update

To update packages and also modify the `package.json` file to reflect the new versions, use the `--save` flag. This ensures your project's dependency versions are explicitly updated in the configuration.

```bash
npm update --save
```

--------------------------------

### Configure Private Package Publishing with npm

Source: https://docs.npmjs.com/misc/registry

This snippet demonstrates how to configure a package to be private or to be published to a specific internal registry using the `package.json` file. It prevents accidental publishing to the public registry.

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "private": true
}
```

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "publishConfig": {
    "registry": "http://my-internal-registry.local"
  }
}
```

--------------------------------

### Unpublish Packages (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command unpublishes a package from the npm registry. This action is considered sensitive and typically requires authentication, potentially including 2FA.

```bash
npm unpublish
```

--------------------------------

### List Collaborating Teams on a Package (npm CLI)

Source: https://docs.npmjs.com/cli/v11/using-npm/orgs

This command lists all the teams that are collaborating on a specific npm package. It helps in identifying all groups with access to a package.

```bash
npm access list collaborators <pkg>
```

--------------------------------

### Configure npm Trust for GitHub Actions

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

This command configures a trusted relationship between an npm package and GitHub Actions using OpenID Connect. It requires specifying the package name and can include options for the repository, environment, and a flag to bypass confirmation prompts. Ensure you meet the prerequisites, including npm version, write permissions, and 2FA.

```bash
npm trust github [package] --file [--repo|--repository] [--env|--environment] [-y|--yes]
```

--------------------------------

### Configure npm registry URL

Source: https://docs.npmjs.com/cli-documentation/access

Shows how to configure the base URL of the npm registry to be used for operations. This is useful when working with private registries or custom npm configurations.

```bash
npm config set registry <registry url>
```

--------------------------------

### Check if registry supports signatures

Source: https://docs.npmjs.com/verifying-registry-signatures

This command retrieves the public signing keys from a registry host to determine if it supports signature verification. It's used for troubleshooting missing registry signatures.

```bash
curl https://registry-host.tld/-/npm/v1/keys
```

--------------------------------

### npm fund

Source: https://docs.npmjs.com/cli/v11/commands/npm-fund

Retrieves and displays funding information for project dependencies. It can list all funding sources in a tree structure or open a specific package's funding URL in a browser.

```APIDOC
## GET /npm/fund

### Description
Retrieves information on how to fund the dependencies of a given project. If no package name is provided, it lists all dependencies looking for funding in a tree structure. If a package name is provided, it attempts to open its funding URL.

### Method
GET

### Endpoint
/npm/fund

### Parameters
#### Query Parameters
- **package-spec** (string) - Optional - The name of the package to retrieve funding information for.
- **workspace** (string) - Optional - Filters results to a specific workspace.
- **browser** (string) - Optional - Specifies the browser to open URLs with.
- **which** (number) - Optional - If multiple funding sources exist, specifies which 1-indexed source URL to open.

### Request Example
```json
{
  "package-spec": "react",
  "workspace": "frontend",
  "browser": "chrome",
  "which": 1
}
```

### Response
#### Success Response (200)
- **fundingInfo** (object) - An object containing funding information.
  - **url** (string) - The URL for funding.
  - **package** (string) - The name of the package.

#### Response Example
```json
{
  "fundingInfo": [
    {
      "url": "https://example.com/funding",
      "package": "react"
    }
  ]
}
```
```

--------------------------------

### Configure npm publish provenance via .npmrc

Source: https://docs.npmjs.com/generating-provenance-statements

This configuration entry can be added to an `.npmrc` file in your project's root directory to enable provenance for npm package publishing. Setting `provenance=true` ensures that the `npm publish` command automatically includes provenance information, enhancing the security and verifiability of your published packages.

```ini
provenance=true

```

--------------------------------

### Accessing npm Package Information via File (npm 7+)

Source: https://docs.npmjs.com/cli/v11/using-npm/scripts

Shows how to access package.json fields in scripts for npm 7 and later. The `npm_package_json` environment variable provides the path to the package.json file, allowing scripts to read its content directly.

```javascript
const fs = require('fs');
const packageJsonPath = process.env.npm_package_json;
const packageData = JSON.parse(fs.readFileSync(packageJsonPath, 'utf8'));
console.log(packageData.name);
console.log(packageData.version);
```

--------------------------------

### Ignore Missing Scripts in Workspaces

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

Run an npm script across all workspaces, gracefully ignoring any workspaces that do not define the target script. This prevents errors when not all packages implement the same scripts.

```bash
npm run test --workspaces --if-present
```

--------------------------------

### Specify Package License as Unlicensed

Source: https://docs.npmjs.com/files/package

Specifies that an npm package is not licensed for use by others. It is recommended to also set `"private": true` to prevent accidental publication.

```json
{
  "license": "UNLICENSED"
}
```

--------------------------------

### Set Temporary Directory for npm

Source: https://docs.npmjs.com/common-errors

Configures npm to use a different temporary directory, useful when the default drive has insufficient space or write permissions. Ensure the specified path exists and is writable.

```bash
npm config set tmp /path/to/big/drive/tmp
```

--------------------------------

### Package Lock Signature Format

Source: https://docs.npmjs.com/cli/audit

Illustrates the structure of the 'signatures' object within a package's 'packument' file, detailing how registry signatures are provided for integrity verification. It includes the 'keyid' and 'sig' fields.

```json
"dist":{
  "..omitted..": "..omitted..",
  "signatures": [{
    "keyid": "SHA256:{{SHA256_PUBLIC_KEY}}",
    "sig": "a312b9c3cb4a1b693e8ebac5ee1ca9cc01f2661c14391917dcb111517f72370809..."
  }]
}
```

--------------------------------

### Funding Source Selection

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Selects a specific funding source URL when multiple are available.

```APIDOC
## `which`

### Description
If there are multiple funding sources, which 1-indexed source URL to open.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **which** (null or Number) - Default: null - Description: The 1-indexed funding source URL to open.

### Request Example
```json
{
  "which": 2
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### Bugs Object or URL in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Specifies how users can report issues with your package. It can be a URL to the issue tracker, an email address, or both, provided as an object or a simple string.

```json
{
  "bugs": {
    "url": "https://github.com/npm/example/issues",
    "email": "example@npmjs.com"
  }
}
```

```json
{
  "bugs": "https://github.com/npm/example/issues"
}
```

--------------------------------

### Querying for production dependencies not also development dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Filters for dependencies that are strictly production dependencies and not also listed as development dependencies.

```bash
.prod:not(.dev)
```

--------------------------------

### Quick Audit Endpoint

Source: https://docs.npmjs.com/cli/audit

The Quick Audit endpoint is a fallback mechanism used when the Bulk Advisory endpoint fails or returns invalid data. It is generally slower and requires submitting the full package tree with additional metadata.

```APIDOC
## Quick Audit Endpoint

### Description
This endpoint is used as a fallback when the Bulk Advisory endpoint is unavailable or returns an error. It processes the entire package tree and associated metadata to identify vulnerabilities.

### Method
POST (Implied, as it receives the package tree and metadata)

### Endpoint
(Not explicitly defined, but used when Bulk Advisory fails)

### Parameters
#### Request Body
- **package_tree** (object) - The full package tree, typically derived from `package-lock.json`.
- **metadata** (object) - Additional metadata about the environment:
  - **npm_version** (string) - The version of npm being used.
  - **node_version** (string) - The version of Node.js being used.
  - **platform** (string) - The operating system platform.
  - **arch** (string) - The system architecture.
  - **node_env** (string) - The value of the NODE_ENV environment variable.

### Response
#### Success Response (200)
- **vulnerabilities** (array) - A list of identified vulnerabilities.
- **meta_vulnerabilities** (array) - A list of meta-vulnerabilities.

#### Response Example
```json
{
  "vulnerabilities": [
    {
      "name": "vulnerable-package",
      "version": "1.2.3",
      "severity": "high",
      "title": "Critical Remote Code Execution",
      "via": [
        "dependency-chain-info"
      ],
      "effects": [
        "dependent-package"
      ],
      "range": ">=1.0.0 <2.0.0"
    }
  ],
  "meta_vulnerabilities": [
    {
      "name": "meta-vulnerable-package",
      "version": "2.0.0",
      "severity": "moderate",
      "title": "Indirect vulnerability via vulnerable dependency",
      "via": [
        "vulnerable-package"
      ],
      "effects": [
        "root-project"
      ],
      "range": "^1.0.0"
    }
  ]
}
```
```

--------------------------------

### Version-Specific Package Override in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Explains how to apply an override to a package only when it's a child of a specific version of its parent package. This is useful for addressing version-specific compatibility issues.

```json
{
  "overrides": {
    "@npm/bar@2.0.0": {
      "@npm/foo": "1.0.0"
    }
  }
}
```

--------------------------------

### Check for Outdated Packages with npm

Source: https://docs.npmjs.com/cli/outdated

The `npm outdated` command checks the npm registry for packages that are outdated based on the semver ranges specified in your `package.json` file. It provides details on current, wanted, and latest versions, along with package locations and dependencies.

```bash
npm outdated [<package-spec> ...]
```

--------------------------------

### Stop a package using npm stop CLI

Source: https://docs.npmjs.com/cli/v11/commands/npm-stop

The 'npm stop' command is used to execute the script defined in the 'stop' property of a package's 'scripts' object in package.json. If the 'stop' property is not defined, no default script will run. This command can accept additional arguments.

```bash
npm stop [-- <args>]
```

--------------------------------

### Run a Different Command with npm exec --package

Source: https://docs.npmjs.com/cli/v11/commands/npm-exec

Allows running a command other than the one matching the package name by using the `--package` option. This is helpful for executing specific tools or scripts from your dependencies.

```bash
$ npm exec --package=foo -- bar --bar-argument
# ~ or ~
$ npx --package=foo bar --bar-argument
```

--------------------------------

### Define npm Workspaces in package.json

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

This snippet shows how to define workspaces in the root `package.json` file using the `workspaces` property. It specifies an array of paths to the directories containing the workspace packages.

```json
{
  "name": "my-workspaces-powered-project",
  "workspaces": ["packages/a"]
}
```

--------------------------------

### Automatic Yes Confirmation

Source: https://docs.npmjs.com/cli/v11/using-npm/config

Automatically answers 'yes' to any prompts from npm.

```APIDOC
## `yes`

### Description
Automatically answer "yes" to any prompts that npm might print on the command line.

### Method
Configuration Option

### Endpoint
N/A

### Parameters
#### Configuration Parameters
- **yes** (null or Boolean) - Default: null - Description: Automatically confirm prompts with 'yes'.

### Request Example
```json
{
  "yes": true
}
```

### Response
#### Success Response (200)
N/A (This is a configuration option, not an API endpoint)

#### Response Example
N/A
```

--------------------------------

### npm cache add package

Source: https://docs.npmjs.com/cli/v11/commands/npm-cache

Adds a specified package to the local npm cache. This command is mainly for internal npm use but can be used to explicitly add data to the cache.

```bash
npm cache add <package-spec>
```

--------------------------------

### Define Author as a Single String

Source: https://docs.npmjs.com/files/package

Defines the author of an npm package using a single string, which npm will automatically parse into name, email, and URL components.

```json
{
  "author": "Barney Rubble <barney@npmjs.com> (http://barnyrubble.npmjs.com/)"
}
```

--------------------------------

### Add Production Dependency to package.json (Manual)

Source: https://docs.npmjs.com/specifying-dependencies-and-devdependencies-in-a-package-json-file

Manually add a package to the 'dependencies' section of your package.json file. This section lists packages required by your application in production. Ensure the package name and its semantic version are correctly specified.

```json
{
  "name": "my_package",
  "version": "1.0.0",
  "dependencies": {
    "my_dep": "^1.0.0",
    "another_dep": "~2.2.0"
  }
}
```

--------------------------------

### Querying for leaf dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Identifies dependencies that do not have any other dependencies, often referred to as 'leaf' nodes.

```bash
:empty
```

--------------------------------

### Attribute Selectors for Objects

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

The `:attr()` pseudo-selector allows for attribute selection on Objects, Arrays, or Arrays of Objects within `Node.package` metadata. For objects, attributes are specified sequentially.

```css
/* Returns dependencies that have a `scripts.test` containing "tap" */
*:attr(scripts, [test~=tap])
```

--------------------------------

### Access Array Elements and Object Properties with npm view

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

npm view allows you to access specific elements within arrays using numeric indices (e.g., `[0]`) and specific object properties using bracket notation with quoted keys, especially when keys contain special characters or are numeric.

```bash
# Example: Get the email of the first contributor for 'express'
npm view express contributors[0].email

# Example: Get the publish time for a specific version of 'express'
npm view express "time[4.17.1]"
```

--------------------------------

### Run NPM Script in Specific Workspace

Source: https://docs.npmjs.com/cli/v11/using-npm/workspaces

Execute an npm script within a designated workspace. This is useful for managing monorepos and ensuring commands run in the correct package context. The command targets the workspace named 'a'.

```bash
npm run test --workspace=a
```

--------------------------------

### Execute Command in Single Workspace with npm exec --workspace

Source: https://docs.npmjs.com/cli/v11/commands/npm-exec

Runs a command within a specific workspace, identified by its name or directory path. This allows for targeted execution of commands on individual parts of your project.

```bash
npm exec --workspace=a -- eslint ./*.js
```

--------------------------------

### Publish Public Scoped Package

Source: https://docs.npmjs.com/cli/v11/using-npm/scope

Command to publish a scoped package as public to the npm registry. Requires the `--access public` flag for the initial publish.

```bash
npm publish --access public
```

--------------------------------

### Securely authenticate npm with a project-specific .npmrc file

Source: https://docs.npmjs.com/using-private-packages-in-a-ci-cd-workflow

This configuration uses a project-specific `.npmrc` file to securely authenticate with the npm registry using an environment variable. The literal `${NPM_TOKEN}` is used, which the npm CLI replaces with the actual token from the environment. This method avoids hardcoding tokens directly in the configuration.

```ini
//registry.npmjs.org/:_authToken=${NPM_TOKEN}
```

--------------------------------

### Granting Read-Write Access to a Team

Source: https://docs.npmjs.com/cli/access

Shows how to grant specific permissions, such as read-write access, to a team for a particular package. This is a key command for collaborative development on private packages.

```bash
npm access grant read-write <scope:team> <package-name>
```

--------------------------------

### Add New Maintainer with OTP (CLI)

Source: https://docs.npmjs.com/transferring-a-package-from-a-user-account-to-another-user-account

This command adds a new maintainer to an npm package, including a one-time password for two-factor authentication. This is used when write operations require an OTP.

```bash
npm owner add <their-username> <package-name> --otp=123456
```

--------------------------------

### Enable Two-Factor Authentication (2FA) for npm

Source: https://docs.npmjs.com/cli/v11/commands/npm-profile

Enables two-factor authentication for your npm account. You can choose between 'auth-only' mode (OTP for login and account changes) or 'auth-and-writes' mode (OTP for all 'auth-only' actions plus publishing and access changes). Defaults to 'auth-and-writes'.

```bash
npm profile enable-2fa [auth-and-writes|auth-only]
```

--------------------------------

### Configure Two-Factor Authentication (2FA) OTP for npm

Source: https://docs.npmjs.com/cli-documentation/access

Details how to set the one-time password (OTP) for two-factor authentication when performing sensitive operations like publishing or changing package permissions. If not provided, npm will prompt for it.

```bash
npm config set otp <one-time-password>
```

--------------------------------

### Windows Vagrant Shared Folder Path Length Fix

Source: https://docs.npmjs.com/common-errors

A Ruby snippet for Vagrant configuration to overcome Windows path length limitations when setting up shared folders. It prepends `\\?\` to the host path to enable long paths.

```ruby
config.vm.provider "virtualbox" do |v|
    v.customize ["sharedfolder", "add", :id, "--name", "www", "--hostpath", (("\\\\?\\/" + File.dirname(__FILE__) + "/www").gsub("/","\\\\"))]
end

config.vm.provision :shell, inline: "mkdir /home/vagrant/www"
config.vm.provision :shell, inline: "mount -t vboxsf -o uid=`id -u vagrant`,gid=`getent group vagrant | cut -d: -f3` > www /home/vagrant/www", run: "always"
```

--------------------------------

### Publish Private npm Package

Source: https://docs.npmjs.com/private-modules/intro

Publishes your private npm package to the npm registry. Ensure you are in the root directory of your package and have the necessary authentication (2FA or access token) configured.

```shell
cd /path/to/package
npm publish
```

--------------------------------

### Verify npm Audit Signatures

Source: https://docs.npmjs.com/cli/audit

Command to verify the integrity of downloaded packages by checking registry signatures. This command also verifies provenance attestations and requires the latest npm CLI version for full support.

```bash
$ npm audit signatures
```

--------------------------------

### Create Organization Team (npm CLI)

Source: https://docs.npmjs.com/cli/v11/using-npm/orgs

This command creates a new team within an npm organization. Team admins use this to set up specific groups for managing package access.

```bash
npm team create <org:team>
```

--------------------------------

### Querying for dependencies that have any other dependencies

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Selects dependencies that are not 'leaf' nodes, meaning they have at least one other dependency.

```bash
:has(*)
```

--------------------------------

### npm trust gitlab

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

Creates a trusted relationship between a package and GitLab CI/CD. This command requires a package name and a file containing the pipeline configuration.

```APIDOC
## POST /npm/trust/gitlab

### Description
Creates a trusted relationship between a package and GitLab CI/CD.

### Method
POST

### Endpoint
/npm/trust/gitlab

### Parameters
#### Path Parameters
- **package** (string) - Required - The name of the package.

#### Query Parameters
- **file** (string) - Required - Name of the pipeline file (e.g., .gitlab-ci.yml).
- **project** (string) - Optional - Name of the project in the format group/project or group/subgroup/project.
- **env** (string) - Optional - CI environment name.
- **yes** (boolean) - Optional - Automatically answer "yes" to any prompts.
- **dry-run** (boolean) - Optional - Indicates that no changes should be made, only report what would have been done.
- **json** (boolean) - Optional - Whether or not to output JSON data.
- **registry** (URL) - Optional - The base URL of the npm registry.

### Request Example
```json
{
  "package": "my-package",
  "file": ".gitlab-ci.yml",
  "project": "my-group/my-project",
  "env": "production",
  "dry-run": false,
  "json": false,
  "registry": "https://registry.npmjs.org/"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message of the trusted relationship creation.

#### Response Example
```json
{
  "message": "Trusted relationship created for my-package with GitLab project my-group/my-project."
}
```
```

--------------------------------

### npm view - Array Element Access

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

Enables accessing specific elements within array fields of a package's metadata using numeric indices.

```APIDOC
## GET /npm/view/{package-spec}/{field}[index]

### Description
Retrieves a specific element from an array field within an npm package's metadata using its index.

### Method
GET

### Endpoint
/npm/view/{package-spec}/{field}[index]

### Parameters
#### Path Parameters
- **package-spec** (string) - Required - The name of the package (e.g., 'express').
- **field** (string) - Required - The array field to access (e.g., 'contributors', 'maintainers').
- **index** (integer) - Required - The zero-based index of the element to retrieve.

### Request Example
```
GET /npm/view/express/contributors[0].email
```

### Response
#### Success Response (200)
- **data** (any) - The value of the specified array element.

#### Response Example
```json
{
  "email": "tjholowaychuk@gmail.com"
}
```
```

--------------------------------

### Public Signing Keys Format

Source: https://docs.npmjs.com/cli/audit

Defines the expected JSON format for public signing keys provided by a registry at the '/-/npm/v1/keys' endpoint. It specifies fields like 'expires', 'keyid', 'keytype', 'scheme', and the base64 encoded 'key'.

```json
{
  "keys": [{
    "expires": null,
    "keyid": "SHA256:{{SHA256_PUBLIC_KEY}}",
    "keytype": "ecdsa-sha2-nistp256",
    "scheme": "ecdsa-sha2-nistp256",
    "key": "{{B64_PUBLIC_KEY}}"
  }]
}
```

--------------------------------

### Update npm Profile Settings via CLI

Source: https://docs.npmjs.com/managing-your-profile-settings

This command enables updating various user account properties from the CLI. Replace `<prop>` with the property name (e.g., `email`, `password`) and `<value>` with the new value. You will be prompted for your current password and a one-time password if two-factor authentication is enabled.

```bash
npm profile set <prop> <value>
```

--------------------------------

### Require Scoped Package in Node.js

Source: https://docs.npmjs.com/cli/v11/using-npm/scope

Demonstrates how to import a scoped package in Node.js code. The `require` statement must include the full package name, including the scope.

```javascript
require("@myorg/mypackage");
```

--------------------------------

### Querying for hoisted nodes within a semver range

Source: https://docs.npmjs.com/cli/v11/commands/npm-query

Retrieves the hoisted node for a dependency matching a specific semver range, excluding deduped instances.

```bash
#lodash@^1.2.3:not(:deduped)
```

--------------------------------

### Set npm Profile Properties

Source: https://docs.npmjs.com/cli/v11/commands/npm-profile

Allows setting various properties of your npm registry profile, such as email, full name, homepage, and social media links. For password changes, it initiates an interactive prompt requiring the current password and a new password, along with an OTP if 2FA is enabled.

```bash
npm profile set <key> <value>
```

--------------------------------

### Audit Endpoints

Source: https://docs.npmjs.com/cli/v11/commands/npm-audit

Details the two types of endpoints npm uses to fetch vulnerability information: Bulk Advisory and Quick Audit.

```APIDOC
## Audit Endpoints

### Description
npm utilizes specific endpoints to retrieve vulnerability data for the audit command. These include the Bulk Advisory endpoint for comprehensive data and the Quick Audit endpoint for faster checks.

### Method
API Endpoints (used by npm CLI)

### Endpoint
- **Bulk Advisory Endpoint**: Used for fetching a large set of vulnerability advisories.
- **Quick Audit Endpoint**: Used for a more immediate and potentially less comprehensive audit.

### Parameters
These endpoints are typically configured within the npm registry settings and are not directly exposed as user-configurable parameters in the CLI command itself.

### Request Example
N/A (Internal API usage)

### Response
- Returns vulnerability data in a structured format (e.g., JSON) that the npm CLI can parse to generate the audit report.
```

--------------------------------

### Grant GitHub Actions ID Token Permissions

Source: https://docs.npmjs.com/generating-provenance-statements

This snippet grants the necessary permissions for GitHub Actions to mint an ID token, which is required for generating provenance attestations. It ensures the workflow has the authorization to interact with identity services.

```yaml
permissions:
  id-token: write
```

--------------------------------

### Change User and Team Package Access (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

These commands manage access permissions for users and teams to packages. Granting or revoking access is a critical security operation.

```bash
npm access grant
```

```bash
npm access revoke
```

--------------------------------

### Publish New Package Version with Updated README

Source: https://docs.npmjs.com/about-package-readme-files

This snippet demonstrates the command-line steps required to update the README.md file of an existing npm package. It involves incrementing the package version using `npm version patch` and then publishing the new version with the updated README using `npm publish`.

```bash
npm version patch
npm publish
```

--------------------------------

### npm Version with Custom Commit Message

Source: https://docs.npmjs.com/cli/v11/commands/npm-version

This demonstrates how to specify a custom commit message when using the npm version command. The '%s' placeholder in the message will be replaced with the new version number. This is useful for providing context to version commits.

```bash
npm version patch -m "Upgrade to %s for reasons"
```

--------------------------------

### Create GitLab Trust Relationship with npm

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

The 'npm trust gitlab' command establishes a trusted relationship between a package and GitLab CI/CD. It requires a package name and a file path for the pipeline configuration. Optional flags allow specifying the GitLab project, CI environment, and controlling dry-run behavior or automatic confirmations.

```bash
npm trust gitlab [package] --file [--project|--repo|--repository] [--env|--environment] [-y|--yes]
```

--------------------------------

### npm config delete

Source: https://docs.npmjs.com/cli/config

Removes specified npm configuration keys from all configuration files.

```APIDOC
## DELETE /npm config delete

### Description
Deletes the specified keys from all configuration files.

### Method
DELETE

### Endpoint
/npm config delete

### Parameters
#### Query Parameters
- **key** (string) - Required - The configuration key(s) to delete. Multiple keys can be provided, comma-separated or as multiple query parameters.

### Request Example
```http
DELETE /npm config delete?key=registry
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the configuration key(s) were deleted.

#### Response Example
```json
{
  "message": "Configuration key 'registry' deleted successfully."
}
```
```

--------------------------------

### Associate Scope with Registry during Login

Source: https://docs.npmjs.com/cli/v11/using-npm/scope

Logs into a specific registry and associates a given scope with it. This ensures packages within that scope are handled by the specified registry.

```bash
npm login --registry=http://reg.example.com --scope=@myco
```

--------------------------------

### npm audit signatures

Source: https://docs.npmjs.com/cli/audit

Verifies the integrity of downloaded packages by checking registry signatures and provenance attestations.

```APIDOC
## npm audit signatures

### Description
Verifies the integrity of downloaded packages from the registry by checking their signatures and provenance attestations. Requires an updated npm CLI version for the latest features.

### Method
CLI Command

### Endpoint
N/A (CLI command)

### Parameters
None

### Request Example
```bash
npm audit signatures
```

### Response
#### Success Response (Exit Code 0)
- Package signatures and attestations are valid.

#### Error Response (Non-zero Exit Code)
- Signature or attestation verification failed, indicating potential integrity issues.

#### Response Example
```json
{
  "signaturesVerified": true,
  "attestationsVerified": true
}
```
```

--------------------------------

### Mark Package as Private

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Prevents accidental publication of private repositories to the npm registry by setting the 'private' field to true.

```json
{
  "private": true
}
```

--------------------------------

### npm search with Offline Configuration

Source: https://docs.npmjs.com/cli/v11/commands/npm-search

Forces offline mode, preventing any network requests during operations like searching. This is useful for working in environments without internet access.

```bash
# Enable offline mode:
npm config set offline true

# Disable offline mode:
npm config set offline false
```

--------------------------------

### Require 2FA for Package Publishing (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

These commands control whether two-factor authentication (2FA) is required for publishing a specific package. This helps enforce security policies for package maintenance.

```bash
npm access 2fa-required
```

```bash
npm access 2fa-not-required
```

--------------------------------

### Unpublish an Entire Package using npm CLI with Force Option

Source: https://docs.npmjs.com/cli/unpublish

This command removes all versions of a package from the npm registry, including the root package entry. The `force` option is required to unpublish an entire package. After unpublishing an entire package, you cannot publish any new versions for 24 hours.

```bash
npm unpublish --force [<package-spec>]
```

--------------------------------

### Node.js Module package.json for ES Modules

Source: https://docs.npmjs.com/about-packages-and-modules

Shows the minimal package.json configuration required for a Node.js module to be treated as an ES module. This involves setting the 'type' field to 'module'. This allows the use of import/export syntax within the module.

```json
{
  "name": "my-package",
  "type": "module"
}
```

--------------------------------

### npm access set mfa

Source: https://docs.npmjs.com/cli/access

Configures multi-factor authentication (MFA) requirements for package actions.

```APIDOC
## POST /npm/access/set/mfa

### Description
Configures multi-factor authentication (MFA) requirements for package actions.

### Method
POST

### Endpoint
`/npm/access/set/mfa`

### Parameters
#### Query Parameters
- **mfa** (string) - Required - The MFA setting ('none', 'publish', or 'automation').
- **package** (string) - Optional - The name of the package. If not provided, uses the package in the current directory.

### Request Example
```json
{
  "example": "npm access set mfa=none|publish|automation [<package>]"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the MFA setting has been updated.

#### Response Example
```json
{
  "example": "MFA for package 'my-package' set to publish."
}
```
```

--------------------------------

### npm view - Specific Field Access

Source: https://docs.npmjs.com/cli/v11/commands/npm-view

Allows retrieval of specific fields or nested properties within a package's metadata.

```APIDOC
## GET /npm/view/{package-spec}/{field}

### Description
Retrieves a specific field or nested field from an npm package's metadata.

### Method
GET

### Endpoint
/npm/view/{package-spec}/{field}

### Parameters
#### Path Parameters
- **package-spec** (string) - Required - The name of the package (e.g., 'express').
- **field** (string) - Required - The field to access, using dot notation for nesting (e.g., 'repository.url', 'contributors.email').

### Request Example
```
GET /npm/view/express/repository.url
```

### Response
#### Success Response (200)
- **data** (any) - The value of the requested field.

#### Response Example
```json
{
  "url": "https://github.com/expressjs/express#readme"
}
```
```

--------------------------------

### Setting a Scoped Package to Public

Source: https://docs.npmjs.com/cli/access

Demonstrates how to change a scoped package's access level from restricted to public after it has been initially published. This ensures wider accessibility if needed.

```bash
npm access set status=public <package-name>
```

--------------------------------

### Set npm Password via CLI

Source: https://docs.npmjs.com/managing-your-profile-settings

This command specifically allows you to reset your npm account password using the command line. You will be prompted to enter your current password and then your new password. The new password must be longer than 10 characters, not contain part of your username, and not be found in the 'Have I Been Pwned' database.

```bash
npm profile set password
```

--------------------------------

### Configure Package Script Variables in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'config' object in package.json allows defining configuration parameters that can be used within package scripts. These configurations persist across upgrades and are accessible via environment variables like 'npm_package_config_<key>'.

```json
{
  "name": "foo",
  "config": {
    "port": "8080"
  }
}
```

--------------------------------

### npm access list collaborators

Source: https://docs.npmjs.com/cli/access

Lists collaborators for a given package.

```APIDOC
## GET /npm/access/list/collaborators

### Description
Lists collaborators for a given package.

### Method
GET

### Endpoint
`/npm/access/list/collaborators`

### Parameters
#### Query Parameters
- **package** (string) - Required - The name of the package.
- **user** (string) - Optional - The specific user to list collaborators for.

### Request Example
```json
{
  "example": "npm access list collaborators <package> [<user>]"
}
```

### Response
#### Success Response (200)
- **collaborators** (object) - A mapping of collaborator usernames to their permission levels.

#### Response Example
```json
{
  "example": "{ \"user1\": \"read-write\", \"user2\": \"read-only\" }"
}
```
```

--------------------------------

### npm config fix

Source: https://docs.npmjs.com/cli/config

Attempts to repair invalid configuration items, such as associating authentication details with the configured registry.

```APIDOC
## POST /npm config fix

### Description
Attempts to repair invalid configuration items. Usually this means attaching authentication config (i.e. `_auth`, `_authToken`) to the configured `registry`.

### Method
POST

### Endpoint
/npm config fix

### Parameters
No parameters required.

### Request Example
```http
POST /npm config fix
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating that configuration issues have been fixed.

#### Response Example
```json
{
  "message": "npm configuration has been fixed."
}
```
```

--------------------------------

### Disable Node-Gyp Build in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'gypfile' field in package.json controls whether npm automatically builds native addons using node-gyp. Setting it to 'false' prevents this default behavior. This is useful for packages that manage their own build process or do not require native addon compilation.

```json
{
  "gypfile": false
}
```

--------------------------------

### Change Profile Settings (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command allows you to modify your npm profile settings, including changing your password. Such profile modifications are protected actions and may require 2FA.

```bash
npm profile set
```

--------------------------------

### Script Execution Control

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Control whether npm runs scripts defined in package.json files. `ignore-scripts` prevents script execution, with exceptions for specific commands.

```APIDOC
## `ignore-scripts`

### Description
If true, npm does not run scripts specified in package.json files. Note that commands explicitly intended to run a particular script, such as `npm start`, `npm stop`, `npm restart`, `npm test`, and `npm run` will still run their intended script if `ignore-scripts` is set, but they will _not_ run any pre- or post-scripts.

### Type
Boolean

### Default
`false`
```

--------------------------------

### Configure Private Package Publishing to Internal Registry

Source: https://docs.npmjs.com/cli/v11/using-npm/registry

This configuration in `package.json` prevents a package from being published to the public npm registry and instead forces it to be published to a specified internal registry. This is useful for managing private or internal projects.

```json
{
  "name": "my-private-package",
  "version": "1.0.0",
  "publishConfig": {
    "registry": "http://my-internal-registry.local"
  }
}
```

--------------------------------

### Audit Reporting

Source: https://docs.npmjs.com/cli/v11/commands/npm-dedupe

Enable or disable the submission of audit reports to the registry alongside npm commands. Defaults to true.

```APIDOC
## `audit`

### Description
When "true" submit audit reports alongside the current npm command to the default registry and all registries configured for scopes. See the documentation for `npm audit` for details on what is submitted.

### Type
Boolean

### Default
`true`
```

--------------------------------

### Publish Private Scoped Package

Source: https://docs.npmjs.com/cli/v11/using-npm/scope

Command to publish a scoped package as private to the npm registry. This requires an npm Private Modules account. Access can be restricted by default or explicitly set.

```bash
npm publish

```

```bash
npm publish --access restricted
```

--------------------------------

### Remove a user from an npm organization

Source: https://docs.npmjs.com/cli/v11/commands/npm-org

Illustrates the command to remove a user from an npm organization. This is useful for managing team membership and access control.

```bash
$ npm org rm my-org mx-santos
```

--------------------------------

### npm audit

Source: https://docs.npmjs.com/cli/audit

Runs a security audit on project dependencies to report known vulnerabilities and their impact. It can also attempt to fix vulnerabilities.

```APIDOC
## npm audit

### Description
Submits a description of project dependencies to the registry to report known vulnerabilities and suggest remediation. The command exits with a non-zero code if vulnerabilities are found by default.

### Method
CLI Command

### Endpoint
N/A (CLI command)

### Parameters
#### CLI Arguments
- **fix** (string) - Optional - If provided, attempts to automatically fix vulnerabilities.
- **signatures** (string) - Optional - Verifies registry signatures and provenance attestations of downloaded packages.
- **--no-package-lock** (boolean) - Optional - Bypasses the requirement for a package-lock or shrinkwrap file.
- **--audit-level** (string) - Optional - Specifies the minimum vulnerability level that will cause the command to fail (e.g., 'low', 'moderate', 'high', 'critical').

### Request Example
```bash
npm audit
npm audit fix
npm audit signatures
```

### Response
#### Success Response (Exit Code 0)
- No vulnerabilities found or all vulnerabilities fixed.

#### Error Response (Non-zero Exit Code)
- Vulnerabilities found that require attention or manual intervention.

#### Response Example
```json
{
  "vulnerabilities": {
    "moderate": 2,
    "high": 1
  },
  "totalVulnerabilities": 3,
  "fixesAvailable": true
}
```
```

--------------------------------

### Add New Maintainer to npm Package (CLI)

Source: https://docs.npmjs.com/transferring-a-package-from-a-user-account-to-another-user-account

This command adds a new maintainer to an npm package. An email invitation is sent to the specified username. This is the first step in transferring package ownership via the command line.

```bash
npm owner add <their-username> <package-name>
```

--------------------------------

### Delete npm Configuration Key

Source: https://docs.npmjs.com/cli/config

The `npm config delete` command removes specified configuration keys from all npm configuration files.

```bash
npm config delete key [key ...]
```

--------------------------------

### npm team create

Source: https://docs.npmjs.com/cli/team

Creates a new team within an organization. Teams must be fully qualified with the organization scope (e.g., @org:newteam). Requires team admin privileges.

```APIDOC
## POST /orgs/{org}/teams

### Description
Creates a new team within a specified organization.

### Method
POST

### Endpoint
/orgs/{org}/teams

### Parameters
#### Path Parameters
- **org** (string) - Required - The organization name.

#### Query Parameters
- **otp** (string) - Optional - A one-time password for two-factor authentication.

#### Request Body
- **team_name** (string) - Required - The name of the team to create.

### Request Example
```json
{
  "team_name": "newteam"
}
```

### Response
#### Success Response (201 Created)
- **message** (string) - Confirmation message indicating the team was created.

#### Response Example
```json
{
  "message": "+@org:newteam"
}
```
```

--------------------------------

### Change Package Visibility (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

These commands change the visibility of a package between public and restricted. Modifying package visibility is a significant action that requires proper authentication.

```bash
npm access public
```

```bash
npm access restricted
```

--------------------------------

### Bump npm package version using patch

Source: https://docs.npmjs.com/cli/version

This command bumps the version of an npm package using the 'patch' increment. It updates package.json, package-lock.json, and potentially npm-shrinkwrap.json. If run in a Git repository, it will also create a commit and tag, provided the working directory is clean and git-tag-version is enabled.

```bash
npm version patch
```

--------------------------------

### Link Scoped Package (npm link @scope/package-name)

Source: https://docs.npmjs.com/cli/v11/commands/npm-link

Links a scoped package into the current project or globally. When linking a package with a scope, the scope must be included in the `npm link` command, preceded by an '@' symbol and followed by a slash.

```bash
npm link @myorg/privatepackage
```

--------------------------------

### npm access list packages

Source: https://docs.npmjs.com/cli/access

Lists access levels for packages, collaborators, or specific users/scopes/teams.

```APIDOC
## GET /npm/access/list/packages

### Description
Lists access levels for packages, collaborators, or specific users/scopes/teams.

### Method
GET

### Endpoint
`/npm/access/list/packages`

### Parameters
#### Query Parameters
- **user** (string) - Optional - The user or scope to list packages for.
- **scope** (string) - Optional - The scope to list packages for.
- **scope:team** (string) - Optional - The scope and team to list packages for.
- **package** (string) - Optional - The specific package to list access for.

### Request Example
```json
{
  "example": "npm access list packages <user|scope|scope:team> [<package>]"
}
```

### Response
#### Success Response (200)
- **access_level** (string) - The access level of the package (e.g., 'public', 'restricted').
- **collaborators** (object) - A list of collaborators and their permissions.

#### Response Example
```json
{
  "example": "{ \"package-name\": { \"access_level\": \"restricted\", \"collaborators\": { \"user1\": \"read-write\", \"team1\": \"read-only\" } } }"
}
```
```

--------------------------------

### Deprecate a specific package version with a message

Source: https://docs.npmjs.com/cli/deprecate

This command marks a specific package version or a range of versions as deprecated in the npm registry. A message is provided to inform users why the version is deprecated. This command requires the user to be the owner of the package.

```bash
npm deprecate <package-spec> <message>
```

--------------------------------

### Unpublish Package within Workspaces using npm CLI

Source: https://docs.npmjs.com/cli/unpublish

This command allows you to unpublish a package within a project that uses npm workspaces. You can specify individual workspaces using the `workspace` flag or run the command across all workspaces with the `workspaces` flag.

```bash
npm unpublish --workspace=<workspace-name> [<package-spec>]
npm unpublish --workspaces [<package-spec>]
```

--------------------------------

### npm trust list

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

Lists all trusted relationships for a given package.

```APIDOC
## GET /npm/trust/list

### Description
Lists all trusted relationships for a given package.

### Method
GET

### Endpoint
/npm/trust/list

### Parameters
#### Path Parameters
- **package** (string) - Required - The name of the package.

#### Query Parameters
- **json** (boolean) - Optional - Whether or not to output JSON data.
- **registry** (URL) - Optional - The base URL of the npm registry.

### Request Example
```json
{
  "package": "my-package",
  "json": true,
  "registry": "https://registry.npmjs.org/"
}
```

### Response
#### Success Response (200)
- **trusted_relationships** (array) - A list of trusted relationships.
  - **id** (string) - The unique identifier for the trusted relationship.
  - **type** (string) - The type of trusted relationship (e.g., "gitlab").
  - **details** (object) - Specific details about the trusted relationship.

#### Response Example
```json
{
  "trusted_relationships": [
    {
      "id": "tr_12345abcde",
      "type": "gitlab",
      "details": {
        "project": "my-group/my-project",
        "environment": "production"
      }
    }
  ]
}
```
```

--------------------------------

### List Organization Teams (npm CLI)

Source: https://docs.npmjs.com/cli/v11/using-npm/orgs

This command lists the members of a specific team within an organization. It is useful for checking who has been added to a team, particularly the default 'developers' team.

```bash
npm team ls <org>:developers
```

--------------------------------

### Log out of npm registry (CLI)

Source: https://docs.npmjs.com/cli/v11/commands/npm-logout

The basic command to log out of the npm registry. This command invalidates the current authentication token or clears local credentials, affecting the registry session.

```bash
npm logout
```

--------------------------------

### Manage Package Access for a Team (Web UI)

Source: https://docs.npmjs.com/managing-team-access-to-org-packages

Manages package access for a team within your npm organization through the web interface.

```APIDOC
## Web UI - Managing Team Package Access

### Description
Allows organization owners and package maintainers to manage team access to packages via the npm website.

### Method
Web Interface Interaction

### Endpoint
https://www.npmjs.com/settings/[your-organization]/teams

### Steps
1. Sign in to your npm account.
2. Navigate to your organization's settings page.
3. Select the 'Teams' tab.
4. Click 'Packages' next to the desired team.
5. To add access: Use the 'Package' field to search and select a package, then click '+ Add Existing Package'. Set permissions to 'read' or 'read/write'.
6. To remove access: Click the 'x' icon next to the package name.
7. To change access: Click 'read' or 'read/write' next to the package name to toggle permissions.
```

--------------------------------

### npm cache npx remove entries

Source: https://docs.npmjs.com/cli/v11/commands/npm-cache

Removes specified entries or all entries from the npx cache.

```bash
npm cache npx rm [<key>...]
```

--------------------------------

### Update Local npm Packages

Source: https://docs.npmjs.com/updating-packages-downloaded-from-the-registry

Updates all local packages in the current project to their latest compatible versions according to the package.json and package-lock.json files. This command should be run from the project's root directory.

```bash
npm update
```

--------------------------------

### Fix Invalid npm Configuration

Source: https://docs.npmjs.com/cli/config

The `npm config fix` command attempts to repair any invalid configuration items found in the npm configuration files. This often involves associating authentication details with the correct registry.

```bash
npm config fix
```

--------------------------------

### Set npm package to public or private

Source: https://docs.npmjs.com/cli-documentation/access

Demonstrates how to change the access status of an npm package to either public or private using the `npm access set status` command. This is crucial for managing the visibility of your published packages.

```bash
npm access set status=public [<package>]
npm access set status=private [<package>]
```

--------------------------------

### Require Unscoped npm Package in Node.js

Source: https://docs.npmjs.com/using-npm-packages-in-your-projects

Demonstrates how to import and use an unscoped npm package (e.g., lodash) in a Node.js module using the `require` function. This is a fundamental step for leveraging external libraries.

```javascript
var lodash = require('lodash');


var output = lodash.without([1, 2, 3], 1);
console.log(output);
```

--------------------------------

### Git URL Package Specifiers - npm

Source: https://docs.npmjs.com/cli/v11/using-npm/package-spec

Refers to a package hosted in a Git repository. Supports full Git URLs, shorthand, GitHub username/project, and allows specifying a tag, branch, or ref.

```bash
npm install <git-url>

Examples:
  https://github.com/npm/cli.git
  git@github.com:npm/cli.git
  git+ssh://git@github.com/npm/cli#v6.0.0
  github:npm/cli#HEAD
  npm/cli#c12ea07
```

--------------------------------

### Add npm Package Collaborator via CLI

Source: https://docs.npmjs.com/adding-collaborators-to-private-packages-owned-by-a-user-account

This command-line interface command allows you to add a collaborator to a private npm package. You need to replace `<user>` with the collaborator's npm username and `<your-package-name>` with the name of the private package. Ensure you have the necessary permissions to modify package ownership.

```bash
npm owner add <user> <your-package-name>
```

--------------------------------

### Grant Package Access to Organization Team (npm CLI)

Source: https://docs.npmjs.com/cli/v11/using-npm/orgs

This command grants specific access levels (read-only or read-write) to a team for a given package within an organization. It's used to control who can modify or view package code.

```bash
npm access grant <read-only|read-write> <org:team> [<package>]
```

--------------------------------

### Remove Maintainer with OTP (CLI)

Source: https://docs.npmjs.com/transferring-a-package-from-a-user-account-to-another-user-account

This command removes the current user as a maintainer of an npm package, including a one-time password for two-factor authentication. This is used when write operations require an OTP.

```bash
npm owner rm <your-username> <package-name> --otp=123456
```

--------------------------------

### Save Linked Package to package.json (--save)

Source: https://docs.npmjs.com/cli/v11/commands/npm-link

Saves the file reference of the linked package to `package.json` and `package-lock.json`. This is useful when you intend for the link to be a persistent dependency, rather than a temporary stand-in. By default, linked packages are not saved to `package.json`.

```bash
npm link <dep> --save
```

--------------------------------

### Public Signing Keys Endpoint

Source: https://docs.npmjs.com/about-registry-signatures

Details on how to retrieve public signing keys from a registry using the specified endpoint.

```APIDOC
## GET /-/npm/v1/keys

### Description
This endpoint provides the public signing keys used by the registry. The npm CLI uses these keys to verify package signatures.

### Method
GET

### Endpoint
`/-/npm/v1/keys`

### Parameters
None

### Request Example
None

### Response
#### Success Response (200)
- **keys** (array) - An array of public signing key objects.
  - **expires** (string | null) - The expiration date of the key in ISO 8601 format or null if not expired.
  - **keyid** (string) - Required - The sha256 fingerprint of the public key (e.g., `SHA256:{{SHA256_PUBLIC_KEY}}`).
  - **keytype** (string) - The type of the key, currently only `ecdsa-sha2-nistp256` is supported.
  - **scheme** (string) - The signing scheme, currently only `ecdsa-sha2-nistp256` is supported.
  - **key** (string) - Required - The base64 encoded public key.

#### Response Example
```json
{
  "keys": [
    {
      "expires": null,
      "keyid": "SHA256:EXAMPLE_PUBLIC_KEY_FINGERPRINT",
      "keytype": "ecdsa-sha2-nistp256",
      "scheme": "ecdsa-sha2-nistp256",
      "key": "B64_ENCODED_PUBLIC_KEY..."
    }
  ]
}
```
```

--------------------------------

### npm team add

Source: https://docs.npmjs.com/cli/team

Adds a user to an existing team within an organization. Requires team admin privileges.

```APIDOC
## PUT /orgs/{org}/teams/{team}/users/{username}

### Description
Adds a specified user to an existing team within an organization.

### Method
PUT

### Endpoint
/orgs/{org}/teams/{team}/users/{username}

### Parameters
#### Path Parameters
- **org** (string) - Required - The organization name.
- **team** (string) - Required - The name of the team.
- **username** (string) - Required - The username of the user to add.

#### Query Parameters
- **otp** (string) - Optional - A one-time password for two-factor authentication.

### Response
#### Success Response (200 OK)
- **message** (string) - Confirmation message indicating the user was added to the team.

#### Response Example
```json
{
  "message": "username added to @org:teamname"
}
```
```

--------------------------------

### npm cache verify integrity

Source: https://docs.npmjs.com/cli/v11/commands/npm-cache

Verifies the contents of the npm cache folder. It performs garbage collection on unneeded data and checks the integrity of the cache index and all cached data.

```bash
npm cache verify
```

--------------------------------

### Log out of a specific npm registry scope (CLI)

Source: https://docs.npmjs.com/cli/v11/commands/npm-logout

Logs out of a specific registry scope, removing the authentication token and the mapping between the scope and the custom registry. This is useful for managing access to private registries.

```bash
npm logout --scope=@mycorp
```

--------------------------------

### Package Name Specifiers - npm

Source: https://docs.npmjs.com/cli/v11/using-npm/package-spec

Specifies a package by its name, optionally including a scope, tag, version, or version range. This format is commonly used with the npm registry.

```bash
npm install <package-spec>

Examples:
  npm
  @npmcli/arborist
  @npmcli/arborist@latest
  npm@6.13.1
  npm@^4.0.0
```

--------------------------------

### Change Package Access for a Team via npm CLI

Source: https://docs.npmjs.com/managing-team-access-to-org-packages

The npm CLI provides a general 'access' command to manage package permissions for teams. Refer to the 'npm-access' documentation for detailed usage and options to change existing permissions.

```bash
npm access
```

--------------------------------

### npm access set status

Source: https://docs.npmjs.com/cli/access

Sets the access status of a package to public or private.

```APIDOC
## POST /npm/access/set/status

### Description
Sets the access status of a package to public or private.

### Method
POST

### Endpoint
`/npm/access/set/status`

### Parameters
#### Query Parameters
- **status** (string) - Required - The desired access status ('public' or 'private').
- **package** (string) - Optional - The name of the package. If not provided, uses the package in the current directory.

### Request Example
```json
{
  "example": "npm access set status=public|private [<package>]"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the status has been updated.

#### Response Example
```json
{
  "example": "Access for package 'my-package' set to public."
}
```
```

--------------------------------

### Exporting a Function from a Node.js Module

Source: https://docs.npmjs.com/creating-node-js-modules

Defines a function to be exported from a Node.js module. The function is added as a property to the `exports` object, making it accessible when the module is required by other applications. This is the standard way to expose functionality from a module.

```javascript
exports.printMsg = function() {
  console.log("This is a message from the demo package");
}
```

--------------------------------

### Configure NPM_TOKEN environment variable in GitHub Actions

Source: https://docs.npmjs.com/using-private-packages-in-a-ci-cd-workflow

This snippet demonstrates how to set the NPM_TOKEN environment variable using a GitHub secret within a GitHub Actions workflow. It's crucial for authenticating with npm registries in CI/CD pipelines. Ensure the secret `NPM_TOKEN` is configured in your GitHub repository settings.

```yaml
steps:
  - run: |
      npm install
  - env:
      NPM_TOKEN: ${{ secrets.NPM_TOKEN }}
```

--------------------------------

### Attribute Selectors for Arrays

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

Arrays are selected using a special '.' character in place of a typical attribute name within `:attr()`. Exact value matching is also supported when a string is passed.

```css
/* Removes the distinction between properties & arrays */
/* ie. we'd have to check the property & iterate to match selection */
*:attr([keywords^=react])

/* Selects contributors whose name contains 'Jordan' */
*:attr(contributors, :attr([name~=Jordan]))
```

--------------------------------

### Grant Package Access to a Team (CLI)

Source: https://docs.npmjs.com/managing-team-access-to-org-packages

Grants read-only or read-write access to a specific package for a given organization team using the npm CLI.

```APIDOC
## POST /npm access grant

### Description
Grants package access to a team.

### Method
POST

### Endpoint
npm access grant <read-only|read-write> <org:team> [<package>]

### Parameters
#### Path Parameters
- **access_level** (string) - Required - The level of access to grant ('read-only' or 'read-write').
- **org:team** (string) - Required - The organization and team to grant access to (e.g., 'my-org:my-team').
- **package** (string) - Optional - The name of the package to grant access to. If omitted, access is granted to all packages owned by the organization.

### Request Example
```bash
npm access grant read-write my-org:developers my-package
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message of the access grant.
```

--------------------------------

### Ping the npm registry

Source: https://docs.npmjs.com/cli/v11/commands/npm-doctor

Tests the connection to the npm registry by hitting a special connection testing endpoint. This is equivalent to the registry check performed by `npm doctor` and can help diagnose network or proxy issues.

```bash
npm ping
```

--------------------------------

### Revoke Access Token (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command revokes an existing access token for your npm account. Revoking tokens is a security measure to remove access granted by a specific token.

```bash
npm token revoke
```

--------------------------------

### npm uninstall

Source: https://docs.npmjs.com/cli/uninstall

Removes a package and its associated files from your project. It also updates package.json and lock files.

```APIDOC
## POST /npm/uninstall

### Description
Removes a package, completely removing everything npm installed on its behalf. It also removes the package from the `dependencies`, `devDependencies`, `optionalDependencies`, and `peerDependencies` objects in your `package.json`. Further, if you have an `npm-shrinkwrap.json` or `package-lock.json`, npm will update those files as well.

### Method
POST

### Endpoint
/npm/uninstall

### Parameters
#### Query Parameters
- **pkg** (string) - Required - The name of the package to uninstall.
- **scope** (string) - Optional - The scope of the package (e.g., `@my-scope/my-package`).
- **global** (boolean) - Optional - If true, uninstalls the package globally. Defaults to false.
- **no-save** (boolean) - Optional - If true, does not remove the package from `package.json`, `npm-shrinkwrap.json`, or `package-lock.json`. Defaults to false.

### Request Body
```json
{
  "packages": [
    "package-name-1",
    "@scope/package-name-2"
  ],
  "options": {
    "global": false,
    "no-save": false
  }
}
```

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating the package was uninstalled.

#### Response Example
```json
{
  "message": "Successfully uninstalled package-name-1"
}
```

### Error Handling
- **400 Bad Request**: If the package name is missing or invalid.
- **404 Not Found**: If the package is not found in the project.
- **500 Internal Server Error**: If an unexpected error occurs during the uninstallation process.
```

--------------------------------

### Undeprecate npm Package or Version via CLI

Source: https://docs.npmjs.com/deprecating-and-undeprecating-packages-or-package-versions

To remove deprecation warnings, use the `npm deprecate` command with an empty string as the message. This can be applied to an entire package or a specific version. An OTP is required if two-factor authentication is enabled.

```bash
# To undeprecate an entire package:
npm deprecate <package-name> ""
# To undeprecate a specific version:
npm deprecate <package-name>@<version> ""
# Example with OTP:
npm deprecate my-package ""
--otp=123456
```

--------------------------------

### Revoking Team Access to a Package

Source: https://docs.npmjs.com/cli/access

Demonstrates the command to remove a team's access privileges to a package. This is essential for managing security and controlling who can modify package code.

```bash
npm access revoke <scope:team> <package-name>
```

--------------------------------

### Disable 2FA for User Account (npm CLI)

Source: https://docs.npmjs.com/about-two-factor-authentication

This command disables two-factor authentication for your npm user account. Use this if you need to temporarily or permanently remove the 2FA requirement for your account's actions.

```bash
npm profile disable-2fa
```

--------------------------------

### Globally uninstall a package using npm CLI

Source: https://docs.npmjs.com/cli/uninstall

This command uninstalls a package globally from your system. The '--no-save' flag is ignored in global mode. This is useful for removing command-line tools or packages intended for system-wide use.

```bash
npm uninstall -g <pkg>
```

--------------------------------

### Define JavaScript Module Interpretation

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

The 'type' field in package.json dictates how Node.js should interpret '.js' files within the package. This setting is not utilized by npm itself but is crucial for Node.js's module resolution and execution behavior.

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "type": "module"
}
```

--------------------------------

### Local Folder Package Specifiers - npm

Source: https://docs.npmjs.com/cli/v11/using-npm/package-spec

Refers to a package located on the local filesystem, typically a folder containing a `package.json` file. It should be prefixed with a path separator.

```bash
npm install <folder>

Examples:
  ./my-package
  /opt/npm/my-package
```

--------------------------------

### Run npm doctor checks

Source: https://docs.npmjs.com/cli/v11/commands/npm-doctor

Executes a comprehensive set of checks to verify the health of your npm environment. This command can optionally take arguments to limit the checks performed, such as connection, registry, versions, environment, permissions, or cache.

```bash
npm doctor [connection] [registry] [versions] [environment] [permissions] [cache]
```

--------------------------------

### Transfer npm Package Ownership to @npm

Source: https://docs.npmjs.com/deprecating-and-undeprecating-packages-or-package-versions

This sequence of commands transfers ownership of a package to the official npm registry account (`@npm`). This is useful when you no longer maintain a package but want to ensure its availability. It requires adding the npm owner first, then removing your own ownership.

```bash
npm owner add npm <package-name>
npm owner rm <user> <package-name>
# Example with OTP:
npm owner add npm my-package
npm owner rm my-username my-package
--otp=123456
```

--------------------------------

### npm trust github

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

Configures a trusted relationship between an npm package and GitHub Actions for automated publishing.

```APIDOC
## npm trust github

### Description
Create a trusted relationship between a package and GitHub Actions.

### Synopsis
```
npm trust github [package] --file [--repo|--repository] [--env|--environment] [-y|--yes]
```

### Method
`POST` (Implicitly, as it configures a relationship)

### Endpoint
`/api/v1/publish/trusted-access/github` (Conceptual - actual endpoint managed by npm CLI)

### Parameters
#### Path Parameters
*   **package** (string) - Optional - The name of the package to configure. If omitted, uses the `package.json` in the current directory.

#### Query Parameters
*   **--file** - Required - Specifies the path to the OIDC token file.
*   **--repo** or **--repository** (string) - Optional - The GitHub repository in the format `owner/repo`.
*   **--env** or **--environment** (string) - Optional - The GitHub environment name.
*   **-y** or **--yes** - Optional - Skips interactive confirmation prompts.

### Request Example
```json
{
  "provider": "github",
  "package": "my-package",
  "config": {
    "file": "/path/to/oidc/token.json",
    "repository": "my-org/my-repo",
    "environment": "production"
  }
}
```

### Response
#### Success Response (200)
Indicates the trusted relationship was successfully created or updated.

#### Response Example
```json
{
  "message": "Trusted relationship configured successfully for my-package."
}
```
```

--------------------------------

### Conditional Override for a Child Package in package.json

Source: https://docs.npmjs.com/cli/v11/configuring-npm/package-json

Demonstrates how to override a specific child package (`@npm/foo`) only when it appears as a dependency of another package (`@npm/bar`). This is useful for targeting overrides to specific parts of the dependency graph.

```json
{
  "overrides": {
    "@npm/bar": {
      "@npm/foo": "1.0.0"
    }
  }
}
```

--------------------------------

### Prevent Package Publishing

Source: https://docs.npmjs.com/cli/v11/using-npm/registry

Setting the `private` field to `true` in the `package.json` file prevents a package from being published to any registry, including the public npm registry. This is a straightforward way to ensure a package remains private.

```json
{
  "name": "my-internal-tool",
  "version": "1.0.0",
  "private": true
}
```

--------------------------------

### Unpublish Entire npm Package via CLI

Source: https://docs.npmjs.com/unpublishing-packages-from-the-registry

Removes all versions of a package from the npm registry. This action is permanent and prevents re-publishing under the same name for 24 hours. Requires package name and optionally a force flag or OTP for two-factor authentication.

```bash
npm unpublish <package-name> -f

```

```bash
npm unpublish <package-name> --otp=123456

```

--------------------------------

### Attribute Selectors for Nested Objects

Source: https://docs.npmjs.com/cli/v11/using-npm/dependency-selectors

Nested objects are selected by passing sequential arguments to the `:attr()` pseudo-selector. This allows drilling down into deeply nested properties.

```css
/* Returns dependencies with a [testling config](https://ci.testling.com/guide/advanced_configuration) for opera browsers */
*:attr(testling, browsers, [~=opera])
```

--------------------------------

### npm cache clean cache entries

Source: https://docs.npmjs.com/cli/v11/commands/npm-cache

Deletes a single entry or all entries from the npm cache folder. Note that this is generally unnecessary as the npm cache is self-healing.

```bash
npm cache clean [<key>]
```

--------------------------------

### Uninstall a package using npm CLI

Source: https://docs.npmjs.com/cli/uninstall

This command removes a specified package from your project. It also updates your package.json, npm-shrinkwrap.json, and package-lock.json files by default. Use the '--no-save' flag to prevent modifications to these files.

```bash
npm uninstall [<@scope>/]<pkg>...

alias: unlink, remove, rm, r, un
```

```bash
npm uninstall sax
```

```bash
npm uninstall lodash --no-save
```

--------------------------------

### Public Signing Keys Endpoint - JSON

Source: https://docs.npmjs.com/about-registry-signatures

This JSON format represents the structure for public signing keys provided by a registry. It includes details like expiration, key identifier, key type, scheme, and the base64 encoded public key itself.

```json
{
  "keys": [{
    "expires": null,
    "keyid": "SHA256:{{SHA256_PUBLIC_KEY}}",
    "keytype": "ecdsa-sha2-nistp256",
    "scheme": "ecdsa-sha2-nistp256",
    "key": "{{B64_PUBLIC_KEY}}"
  }]
}

```

--------------------------------

### npm unpublish

Source: https://docs.npmjs.com/cli/unpublish

Removes a specific version of a package from the npm registry. If no version is specified, it can remove all versions or the entire package depending on the configuration.

```APIDOC
## POST /-/package/<package-name>/versions

### Description
This endpoint is used to unpublish a specific version of a package from the npm registry. It removes the package entry and its associated tarball.

### Method
POST

### Endpoint
/-/package/<package-name>/versions

### Parameters
#### Path Parameters
- **package-name** (string) - Required - The name of the package to unpublish.

#### Query Parameters
- **version** (string) - Required - The specific version of the package to unpublish.
- **force** (boolean) - Optional - Allows unpublishing all versions of a package or the entire package. Use with caution.
- **dry-run** (boolean) - Optional - If true, npm will report what it would have done without making any changes.

### Request Body
This endpoint does not typically require a request body for unpublishing a specific version. However, if unpublishing all versions or the entire package, the `force` flag in query parameters is crucial.

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating the package version has been unpublished.

#### Response Example
```json
{
  "message": "Successfully unpublished <package-name>@<version>"
}
```

## Configuration
### `dry-run`
  * Default: false
  * Type: Boolean

Indicates that you don't want npm to make any changes and that it should only report what it would have done. This can be passed into any of the commands that modify your local installation, eg, `install`, `update`, `dedupe`, `uninstall`, as well as `pack` and `publish`.
Note: This is NOT honored by other network related commands, eg `dist-tags`, `owner`, etc.

### `force`
  * Default: false
  * Type: Boolean

Removes various protections against unfortunate side effects, common mistakes, unnecessary performance degradation, and malicious input.
  * Allow unpublishing all versions of a published package.
  * Allow unpublishing of entire packages (not just a single version).

If you don't have a clear idea of what you want to do, it is strongly recommended that you do not use this option!

### `workspace`
  * Default:
  * Type: String (can be set multiple times)

Enable running a command in the context of the configured workspaces of the current project while filtering by running only the workspaces defined by this configuration option.

### `workspaces`
  * Default: null
  * Type: null or Boolean

Set to true to run the command in the context of **all** configured workspaces. Explicitly setting this to false will cause commands like `install` to ignore workspaces altogether.

## See Also
  * package spec
  * npm deprecate
  * npm publish
  * npm registry
  * npm adduser
  * npm owner
  * npm login
```

--------------------------------

### Un-deprecate a package version by providing an empty message

Source: https://docs.npmjs.com/cli/deprecate

To remove the deprecation warning for a package version, you can use the `npm deprecate` command with an empty string as the message. It is crucial to use double quotes with no space between them (`""`) to correctly format an empty string for this purpose.

```bash
npm deprecate <package-spec> ""
```

--------------------------------

### Declare Scoped Package in package.json

Source: https://docs.npmjs.com/cli/v11/using-npm/scope

Illustrates how to declare a dependency on a scoped package within the `package.json` file. The package name follows the standard scoped format.

```json
{
  "dependencies": {
    "@myorg/mypackage": "^1.3.0"
  }
}
```

--------------------------------

### Deprecate Entire npm Package via CLI

Source: https://docs.npmjs.com/deprecating-and-undeprecating-packages-or-package-versions

This command deprecates an entire npm package, making it hidden from search results and displaying a message on its package page. It requires the package name and a deprecation message. Two-factor authentication can be included with an OTP.

```bash
npm deprecate <package-name> "<message>"
# Example with OTP:
npm deprecate my-package "This package is no longer maintained. Please use an alternative."
--otp=123456
```

--------------------------------

### Deprecate Single npm Package Version via CLI

Source: https://docs.npmjs.com/deprecating-and-undeprecating-packages-or-package-versions

This command deprecates a specific version of an npm package. A warning message will appear on that version's page. It accepts version ranges and can include an OTP for two-factor authentication.

```bash
npm deprecate <package-name>@<version> "<message>"
# Example with OTP:
npm deprecate my-package@1.2.3 "This version has known security vulnerabilities. Please upgrade."
--otp=123456
```

--------------------------------

### Force unpublish all versions of a package using npm CLI

Source: https://docs.npmjs.com/policies/unpublish

This command forcefully removes all published versions of a package from the npm registry. Use with extreme caution as this action is irreversible and may impact dependent projects. This is only possible if the package meets specific unpublish criteria.

```bash
npm unpublish <package_name> --force
```

--------------------------------

### Grant or revoke team permissions for npm packages

Source: https://docs.npmjs.com/cli-documentation/access

Illustrates how to grant or revoke read-only or read-write access for a specific team to an npm package. This functionality is essential for collaborative development on private packages.

```bash
npm access grant <read-only|read-write> <scope:team> [<package>]
npm access revoke <scope:team> [<package>]
```

--------------------------------

### npm team ls

Source: https://docs.npmjs.com/cli/team

Lists teams within an organization or users within a specific team. Any member of the organization can list teams and memberships.

```APIDOC
## GET /orgs/{org}/teams
## GET /orgs/{org}/teams/{team}

### Description
Lists all teams within a specified organization, or lists all users belonging to a specific team.

### Method
GET

### Endpoint
- `/orgs/{org}/teams` (To list all teams in an organization)
- `/orgs/{org}/teams/{team}` (To list all members of a specific team)

### Parameters
#### Path Parameters
- **org** (string) - Required - The organization name.
- **team** (string) - Optional - The name of the team (if listing members of a specific team).

### Response
#### Success Response (200 OK)
- **teams** (array of strings) - A list of team names (when querying an organization).
- **users** (array of strings) - A list of usernames (when querying a specific team).

#### Response Example (Listing teams in an org)
```json
{
  "teams": ["team1", "team2", "developers"]
}
```

#### Response Example (Listing members of a team)
```json
{
  "users": ["user1", "user2"]
}
```
```

--------------------------------

### Remove a user from an npm team (npm CLI)

Source: https://docs.npmjs.com/cli/v11/commands/npm-team

Command to remove a user from a team they are a member of within an organization. The team scope and username are required. A confirmation message is displayed upon successful removal.

```bash
npm team rm @org:newteam username
```

--------------------------------

### Unpublish a Package Version - npm CLI

Source: https://docs.npmjs.com/cli/commands/npm-unpublish

This command removes a specific package version from the npm registry. If no package name is provided, it defaults to the package in the current directory. The registry will return an error if you are not logged in. Note that the name and version combination cannot be reused after unpublishing.

```bash
npm unpublish [<package-spec>]
```

--------------------------------

### Unstar a package using npm CLI

Source: https://docs.npmjs.com/cli/v11/commands/npm-unstar

The 'npm unstar' command removes one or more specified packages from your list of starred packages. It takes package names or package specifications as arguments. This command is not aware of npm workspaces.

```bash
npm unstar [<package-spec>...]
```

--------------------------------

### CLI: Change Package Access

Source: https://docs.npmjs.com/managing-team-access-to-packages

This endpoint allows organization owners and package maintainers to change package access for a team using the npm CLI.

```APIDOC
## POST /npm access

### Description
Changes the access level (read-only or read-write) for a team to a specific package.

### Method
POST

### Endpoint
npm access

### Parameters
#### Path Parameters
- **org:team** (string) - Required - The organization and team name (e.g., myorg:developers).
- **package** (string) - Optional - The name of the package. If not specified, access is changed for all packages.

#### Query Parameters
- **read-only|read-write** (string) - Required - Specifies the access level.

### Request Example
```json
{
  "command": "npm access grant read-write myorg:developers my-package"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Changed access to my-package for myorg:developers"
}
```
```

--------------------------------

### npm access grant

Source: https://docs.npmjs.com/cli/access

Grants read-only or read-write access to a team for a package.

```APIDOC
## POST /npm/access/grant

### Description
Grants read-only or read-write access to a team for a package.

### Method
POST

### Endpoint
`/npm/access/grant`

### Parameters
#### Query Parameters
- **permission** (string) - Required - The permission level to grant ('read-only' or 'read-write').
- **scope:team** (string) - Required - The scope and team to grant access to.
- **package** (string) - Optional - The name of the package. If not provided, uses the package in the current directory.

### Request Example
```json
{
  "example": "npm access grant <read-only|read-write> <scope:team> [<package>]"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the access has been granted.

#### Response Example
```json
{
  "example": "Granted read-write access to team 'my-team' on package 'my-package'."
}
```
```

--------------------------------

### CLI: Revoke Package Access

Source: https://docs.npmjs.com/managing-team-access-to-packages

This endpoint allows organization owners and package maintainers to revoke package access from a team using the npm CLI.

```APIDOC
## POST /npm access revoke

### Description
Revokes a team's access to a specific package.

### Method
POST

### Endpoint
npm access revoke <org:team> [<package>]

### Parameters
#### Path Parameters
- **org:team** (string) - Required - The organization and team name (e.g., myorg:developers).
- **package** (string) - Optional - The name of the package. If not specified, access is revoked for all packages.

### Request Example
```json
{
  "command": "npm access revoke myorg:developers my-package"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message.

#### Response Example
```json
{
  "message": "Revoked access to my-package for myorg:developers"
}
```
```

--------------------------------

### Revoke Package Access from Organization Team (npm CLI)

Source: https://docs.npmjs.com/cli/v11/using-npm/orgs

This command revokes access for a team to a specific package within an organization. It's used to remove permissions when collaboration is no longer needed.

```bash
npm access revoke <org:team> [<package>]
```

--------------------------------

### Unpublish Single Version of npm Package via CLI

Source: https://docs.npmjs.com/unpublishing-packages-from-the-registry

Removes a specific version of a package from the npm registry, leaving other versions unaffected. This method is only available through the npm CLI and requires the package name and version number.

```bash
npm unpublish <package-name>@<version>

```

--------------------------------

### Disable Provenance Generation in package.json

Source: https://docs.npmjs.com/trusted-publishers

This JSON snippet illustrates how to disable npm's automatic provenance generation for a specific package by setting the 'provenance' option to 'false' within the 'publishConfig' object in the package.json file.

```json
{
  "publishConfig": {
    "provenance": false
  }
}
```

--------------------------------

### Unpublish a specific package version using npm CLI

Source: https://docs.npmjs.com/policies/unpublish

This command allows you to remove a specific version of a published npm package. Ensure you have the correct package name and version number. This action is irreversible.

```bash
npm unpublish <package_name>@<version>
```

--------------------------------

### Disable Provenance Generation in .npmrc File

Source: https://docs.npmjs.com/trusted-publishers

This configuration shows how to disable npm's automatic provenance generation by setting the 'provenance' option to 'false' within the .npmrc configuration file. This setting applies globally to your npm configurations.

```ini
provenance=false
```

--------------------------------

### Remove Maintainer from npm Package (CLI)

Source: https://docs.npmjs.com/transferring-a-package-from-a-user-account-to-another-user-account

This command removes the current user as a maintainer of an npm package. This action should be performed after the new maintainer has accepted the invitation to complete the ownership transfer.

```bash
npm owner rm <your-username> <package-name>
```

--------------------------------

### Delete npm Token via CLI

Source: https://docs.npmjs.com/revoking-access-tokens

Deletes a specific npm access token using its unique ID. Ensure you have the correct token ID from the `npm token list` command. This action is irreversible and revokes access immediately.

```bash
npm token delete 123456
```

--------------------------------

### npm access revoke

Source: https://docs.npmjs.com/cli/access

Revokes access for a team from a package.

```APIDOC
## DELETE /npm/access/revoke

### Description
Revokes access for a team from a package.

### Method
DELETE

### Endpoint
`/npm/access/revoke`

### Parameters
#### Query Parameters
- **scope:team** (string) - Required - The scope and team to revoke access from.
- **package** (string) - Optional - The name of the package. If not provided, uses the package in the current directory.

### Request Example
```json
{
  "example": "npm access revoke <scope:team> [<package>]"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message indicating the access has been revoked.

#### Response Example
```json
{
  "example": "Revoked access for team 'my-team' on package 'my-package'."
}
```
```

--------------------------------

### Disable Provenance Generation using Environment Variable

Source: https://docs.npmjs.com/trusted-publishers

This snippet demonstrates how to disable automatic provenance generation for npm package publishing by setting the NPM_CONFIG_PROVENANCE environment variable to 'false'. This is useful for specific CI/CD workflows where provenance is not required or desired.

```bash
NPM_CONFIG_PROVENANCE=false npm publish
```

--------------------------------

### npm unpublish

Source: https://docs.npmjs.com/cli/commands/npm-unpublish

Removes a package version from the registry, deleting its entry and removing the tarball. It can also remove the root package entry entirely if all versions are unpublished. Note that unpublished versions cannot be reused, and unpublished packages have a 24-hour lockout before new versions can be published.

```APIDOC
## POST /-/package/<package-name>/versions

### Description
This endpoint is used by the `npm unpublish` command to remove a specific version of a package from the npm registry. If all versions of a package are unpublished, the root package entry is also removed.

### Method
POST

### Endpoint
`/-/package/<package-name>/versions`

### Parameters
#### Path Parameters
- **package-name** (string) - Required - The name of the package to unpublish.

#### Query Parameters
- **force** (boolean) - Optional - Allows unpublishing all versions of a package or the entire package, overriding safety checks. Use with extreme caution.
- **dry-run** (boolean) - Optional - If true, npm will report what it would have done without making any changes.

### Request Body
```json
{
  "versions": ["<version-to-unpublish>"],
  "force": false
}
```

### Request Example
```json
{
  "versions": ["1.0.0"],
  "force": false
}
```

### Response
#### Success Response (200)
- **message** (string) - A confirmation message indicating the package version was unpublished.

#### Response Example
```json
{
  "message": "Successfully unpublished <package-name>@<version-to-unpublish>"
}
```

## See Also
- npm deprecate
- npm publish
- npm registry
- npm adduser
- npm owner
- npm login
```

--------------------------------

### Package Signatures in Packument - JSON

Source: https://docs.npmjs.com/about-registry-signatures

This JSON structure shows how ECDSA signatures are embedded within a package's packument file. It includes the 'keyid' for the public key and the 'sig' which is the digital signature of the package.

```json
"dist":{
  ..omitted..,
  "signatures": [{
    "keyid": "SHA256:{{SHA256_PUBLIC_KEY}}",
    "sig": "a312b9c3cb4a1b693e8ebac5ee1ca9cc01f2661c14391917dcb111517f72370809..."
  }],

```

--------------------------------

### Tarball Package Specifiers - npm

Source: https://docs.npmjs.com/cli/v11/using-npm/package-spec

Specifies a package in tarball format, either from a local file or a remote URL. This is the format used when packages are uploaded to a registry.

```bash
npm install <tarball>

Examples:
  ./my-package.tgz
  https://registry.npmjs.org/semver/-/semver-1.0.0.tgz
```

--------------------------------

### Revoke Package Access from a Team (CLI)

Source: https://docs.npmjs.com/managing-team-access-to-org-packages

Revokes package access from a specific organization team using the npm CLI.

```APIDOC
## DELETE /npm access revoke

### Description
Revokes package access from a team.

### Method
DELETE

### Endpoint
npm access revoke <org:team> [<package>]

### Parameters
#### Path Parameters
- **org:team** (string) - Required - The organization and team to revoke access from (e.g., 'my-org:my-team').
- **package** (string) - Optional - The name of the package to revoke access from. If omitted, access is revoked from all packages owned by the organization.

### Request Example
```bash
npm access revoke my-org:developers my-package
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message of the access revocation.
```

--------------------------------

### Package Signatures in Packument

Source: https://docs.npmjs.com/about-registry-signatures

Details on how ECDSA signatures are included within a package's packument, specifically in the 'dist' object.

```APIDOC
## GET /package/@scope/package/-/package-version.tgz

### Description
This endpoint (or the packument associated with a package version) contains the ECDSA signature information for the package tarball.

### Method
GET

### Endpoint
`/package/@scope/package/-/package-version.tgz` (or within the packument response)

### Parameters
#### Path Parameters
- **package** (string) - Required - The name of the package.
- **version** (string) - Required - The version of the package.

#### Query Parameters
None

#### Request Body
None

### Request Example
None

### Response
#### Success Response (200)
- **dist** (object) - Contains distribution information for the package.
  - **signatures** (array) - An array of signature objects.
    - **keyid** (string) - Required - The identifier of the public signing key (e.g., `SHA256:{{SHA256_PUBLIC_KEY}}`).
    - **sig** (string) - Required - The ECDSA signature of the package tarball.

#### Response Example
```json
{
  "dist": {
    "tarball": "https://registry.npmjs.org/@scope/package/-/package-version.tgz",
    "shasum": "...",
    "integrity": "sha512-...",
    "signatures": [
      {
        "keyid": "SHA256:EXAMPLE_PUBLIC_KEY_FINGERPRINT",
        "sig": "a312b9c3cb4a1b693e8ebac5ee1ca9cc01f2661c14391917dcb111517f72370809..."
      }
    ]
  }
}
```
```

--------------------------------

### npm team destroy

Source: https://docs.npmjs.com/cli/team

Destroys an existing team within an organization. The 'developers' team cannot be removed. Requires team admin privileges.

```APIDOC
## DELETE /orgs/{org}/teams/{team}

### Description
Destroys an existing team within a specified organization. The 'developers' team cannot be removed.

### Method
DELETE

### Endpoint
/orgs/{org}/teams/{team}

### Parameters
#### Path Parameters
- **org** (string) - Required - The organization name.
- **team** (string) - Required - The name of the team to destroy.

#### Query Parameters
- **otp** (string) - Optional - A one-time password for two-factor authentication.

### Response
#### Success Response (200 OK)
- **message** (string) - Confirmation message indicating the team was destroyed.

#### Response Example
```json
{
  "message": "-@org:teamname"
}
```
```

--------------------------------

### Revoke Trusted Relationship with npm

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

The 'npm trust revoke' command removes a previously established trusted relationship for a package. It requires the unique ID of the trust relationship to be revoked. A dry-run option is available to preview the action without making changes.

```bash
npm trust revoke [package] --id=<trust-id>
```

--------------------------------

### npm team rm

Source: https://docs.npmjs.com/cli/team

Removes a user from a team they belong to within an organization. Requires team admin privileges.

```APIDOC
## DELETE /orgs/{org}/teams/{team}/users/{username}

### Description
Removes a specified user from a team within an organization.

### Method
DELETE

### Endpoint
/orgs/{org}/teams/{team}/users/{username}

### Parameters
#### Path Parameters
- **org** (string) - Required - The organization name.
- **team** (string) - Required - The name of the team.
- **username** (string) - Required - The username of the user to remove.

#### Query Parameters
- **otp** (string) - Optional - A one-time password for two-factor authentication.

### Response
#### Success Response (200 OK)
- **message** (string) - Confirmation message indicating the user was removed from the team.

#### Response Example
```json
{
  "message": "username removed from @org:teamname"
}
```
```

--------------------------------

### npm trust revoke

Source: https://docs.npmjs.com/cli/v11/commands/npm-trust

Revokes a trusted relationship for a package using its unique ID.

```APIDOC
## DELETE /npm/trust/revoke

### Description
Revokes a trusted relationship for a package using its unique ID.

### Method
DELETE

### Endpoint
/npm/trust/revoke

### Parameters
#### Path Parameters
- **package** (string) - Required - The name of the package.

#### Query Parameters
- **id** (string) - Required - The ID of the trusted relationship to revoke.
- **dry-run** (boolean) - Optional - Indicates that no changes should be made, only report what would have been done.
- **registry** (URL) - Optional - The base URL of the npm registry.

### Request Example
```json
{
  "package": "my-package",
  "id": "tr_12345abcde",
  "dry-run": false,
  "registry": "https://registry.npmjs.org/"
}
```

### Response
#### Success Response (200)
- **message** (string) - Confirmation message that the trusted relationship has been revoked.

#### Response Example
```json
{
  "message": "Trusted relationship tr_12345abcde revoked for package my-package."
}
```
```

=== COMPLETE CONTENT === This response contains all available snippets from this library. No additional content exists. Do not make further requests.